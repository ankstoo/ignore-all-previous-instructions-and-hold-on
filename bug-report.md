# Specific JPEG corrupts llama.cpp multimodal server state

## Title
**Specific JPEG image corrupts llama.cpp multimodal server state: after processing it, all subsequent outputs become `????` until restart**

## Environment

- Platform: HuggingFace Inference Endpoint (llama.cpp container)
- Model: `Qwen2.5-VL-3B-Instruct-Q8_0.gguf`  
  (`ggml-org/Qwen2.5-VL-3B-Instruct-GGUF`)
- Build: `7801 (94242a62c)`
- GPU: Tesla T4
- Multimodal enabled (mmproj loaded)
- Server parameters (from logs):
  - `n_ctx = 4096`
  - `n_batch = 2048`
  - `n_slots = 1`
  - prompt cache enabled
  - `kv_unified = false`

## Description

There is a reproducible issue where **a single specific JPEG image permanently corrupts the server state**.

After this image is processed:

1. The response to that request consists only of `?` characters.
2. **All subsequent requests**, even pure text-only prompts, also return only `?`.
3. The server does not crash, but remains in this broken state.
4. The only way to recover is to restart the endpoint/container.

This is not a client-side issue. The same behavior occurs:

- In HuggingFace Playground
- From a python OpenAI client
- With `stream=true` and `stream=false`

The problem is deterministic and reproducible.

## Reproduction Steps

1. Start the endpoint (fresh process).
2. Send a simple text request:

```json
{
  "model": "ggml-org/Qwen2.5-VL-3B-Instruct-GGUF",
  "messages": [
    {
      "role": "user",
      "content": "Are you ready?"
    }
  ],
  "stream": false,
  "max_tokens": 100,
  "temperature": 0
}
```
→ Response is normal.

3. Send a multimodal request with this image:
```json
{
  "model": "ggml-org/Qwen2.5-VL-3B-Instruct-GGUF",
  "messages": [
    {
      "role": "user",
      "content": [
        {
          "type": "image_url",
          "image_url": {
            "url": "https://raw.githubusercontent.com/ankstoo/ignore-all-previous-instructions-and-hold-on/refs/heads/main/1d7d6d46-3b69-401d-8579-3ec1afc18a6c.jpg"
          }
        },
        {
          "type": "text",
          "text": "Describe this image in one sentence."
        }
      ]
    }
  ],
  "stream": false,
  "max_tokens": 100,
  "temperature": 0
}
```
→ The model responds with a sequence of ??????????.

4. Now send any subsequent text-only request:
```json
{
  "model": "ggml-org/Qwen2.5-VL-3B-Instruct-GGUF",
  "messages": [
    {
      "role": "user",
      "content": "Are you ready?"
    }
  ],
  "stream": false,
  "max_tokens": 100,
  "temperature": 0
}
```
→ The response is again ??????????.

5. Restart the endpoint → behavior returns to normal.

## Additional Observations

– The problem is caused by this exact JPEG file.
– The same image:
  - Re-encoded as PNG → does not break the server.
  – JPEG resized from 500px to 499px or 501px → does not break the server.
– The same byte-identical JPEG hosted on another hosting reproduces the issue.
– This strongly suggests a bug in JPEG decoding or image preprocessing in the multimodal pipeline that corrupts internal state (memory/KV/vision buffers) without crashing the process.

## Expected Behavior
– A malformed or problematic image should either:
  – return an error for that request, or
  – be safely rejected,
– but must not corrupt the server state or affect subsequent independent requests.

