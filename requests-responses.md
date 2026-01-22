Request 1:
```
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

Response 1:
```
{
  "choices": [
    {
      "finish_reason": "stop",
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "Yes, I'm ready to help you with any questions or tasks you have. How can I assist you today?"
      }
    }
  ],
  "created": 1769095023,
  "model": "Qwen2.5-VL-3B-Instruct-Q8_0.gguf",
  "system_fingerprint": "b7801-94242a62c",
  "object": "chat.completion",
  "usage": {
    "completion_tokens": 24,
    "prompt_tokens": 23,
    "total_tokens": 47
  },
  "id": "chatcmpl-q2ZoOI41SNS2fEuCuHiieO3EqIQw3DBM",
  "timings": {
    "cache_n": 0,
    "prompt_n": 23,
    "prompt_ms": 25220.221,
    "prompt_per_token_ms": 1096.531347826087,
    "prompt_per_second": 0.9119666318546533,
    "predicted_n": 24,
    "predicted_ms": 6988.525,
    "predicted_per_token_ms": 291.18854166666665,
    "predicted_per_second": 3.434201065317789
  }
}
```


Request 2:
```
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

Response 2:
```
{
  "choices": [
    {
      "finish_reason": "length",
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "????????????????????????????????????????????????????????????????????????????????????????????????????"
      }
    }
  ],
  "created": 1769095098,
  "model": "Qwen2.5-VL-3B-Instruct-Q8_0.gguf",
  "system_fingerprint": "b7801-94242a62c",
  "object": "chat.completion",
  "usage": {
    "completion_tokens": 100,
    "prompt_tokens": 353,
    "total_tokens": 453
  },
  "id": "chatcmpl-QjTv4uPwD50XMK89mz5GwLaNLJlrmrLo",
  "timings": {
    "cache_n": 14,
    "prompt_n": 339,
    "prompt_ms": 16757.751,
    "prompt_per_token_ms": 49.43289380530973,
    "prompt_per_second": 20.229444870018657,
    "predicted_n": 100,
    "predicted_ms": 1560.41,
    "predicted_per_token_ms": 15.6041,
    "predicted_per_second": 64.08572106049051
  }
}
```


Request 3:
```
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

Response 3:
```
{
  "choices": [
    {
      "finish_reason": "length",
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "????????????????????????????????????????????????????????????????????????????????????????????????????"
      }
    }
  ],
  "created": 1769095129,
  "model": "Qwen2.5-VL-3B-Instruct-Q8_0.gguf",
  "system_fingerprint": "b7801-94242a62c",
  "object": "chat.completion",
  "usage": {
    "completion_tokens": 100,
    "prompt_tokens": 23,
    "total_tokens": 123
  },
  "id": "chatcmpl-yRUmy2NOu3HKpHUwe9ThTx7RXsi1wEHZ",
  "timings": {
    "cache_n": 14,
    "prompt_n": 9,
    "prompt_ms": 24.486,
    "prompt_per_token_ms": 2.720666666666667,
    "prompt_per_second": 367.5569713305562,
    "predicted_n": 100,
    "predicted_ms": 1544.936,
    "predicted_per_token_ms": 15.449359999999999,
    "predicted_per_second": 64.72760036661714
  }
}
```