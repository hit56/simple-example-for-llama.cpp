# llama.cpp/example/simple

The purpose of this example is to demonstrate a minimal usage of llama.cpp for generating text with a given prompt.

```bash
./build/llama-simple -m ~/private_data/models/Qwen/Qwen3-0.6B-GGUF/Qwen3-0.6B-Q8_0.gguf  "您好!"

...

您好! 今天天气怎么样？我需要准备什么？  今天天气怎么样？我需要准备什么？

看起来你是在询问今天的天气情况和所需准备的
main: decoded 32 tokens in 0.45 s, speed: 71.21 t/s

llama_perf_sampler_print:    sampling time =       5.15 ms /    32 runs   (    0.16 ms per token,  6219.63 tokens per second)
llama_perf_context_print:        load time =   11569.00 ms
llama_perf_context_print: prompt eval time =     115.84 ms /     2 tokens (   57.92 ms per token,    17.26 tokens per second)
llama_perf_context_print:        eval time =     318.55 ms /    31 runs   (   10.28 ms per token,    97.32 tokens per second)
llama_perf_context_print:       total time =   11902.59 ms /    33 tokens
llama_perf_context_print:    graphs reused =         30
```
