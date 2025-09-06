# 一、如何编译
```bash
git clone https://github.com/ggml-org/llama.cpp.git
cd llama.cpp
cmake -B build -DGGML_CUDA=ON -DBUILD_SHARED_LIBS=OFF -DLLAMA_CURL=ON -DCMAKE_POSITION_INDEPENDENT_CODE=ON
```
|参数| 解释|
|--|--|
|-B build |build 是生成的构建目录，这是 CMake 将生成的文件存放的地方。|
|-DGGML_CUDA=ON|启用 CUDA 支持|
|-DBUILD_SHARED_LIBS=OFF|生成 静态库|
|-DLLAMA_CURL=ON|启用 CURL 库支持以便支持网络请求|
|-DCMAKE_POSITION_INDEPENDENT_CODE=ON|为了确保编译出的目标文件（即使是静态库）具备「地址无关性」|


```bash
cmake --build build --config Release -j --clean-first
```
|参数| 解释|
|--|--|
|--build build|表示使用build 目录中的构建文件来执行构建过程|
|--config Release|表示指定构建的配置为 Release 配置|
|-j|表示并行编译，默认用的所有 CPU 核心数，也可指定作业数，例如 -j 8 表示使用 8 个进程并行编译|
|--clean-first|表示在构建之前先清理掉之前的构建结果。|

# 二、下载例子

```bash
git clone https://github.com/hit56/simple-example-for-llama.cpp.git
cd simple-example-for-llama.cpp
```

## 生成makefile
```bash
cmake -B build
```
运行结果：
```bash
-- The CXX compiler identification is GNU 9.4.0
-- The CUDA compiler identification is NVIDIA 12.2.91
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/ccache - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Detecting CUDA compiler ABI info
-- Detecting CUDA compiler ABI info - done
-- Check for working CUDA compiler: /usr/local/cuda/bin/nvcc - skipped
-- Detecting CUDA compile features
-- Detecting CUDA compile features - done
-- Found OpenMP_CXX: -fopenmp (found version "4.5")
-- Found OpenMP: TRUE (found version "4.5")
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD - Success
-- Found Threads: TRUE
-- Configuring done (21.8s)
-- Generating done (0.2s)
-- Build files have been written to: /root/private_data/work_space/simple-example-for-llama.cpp/build
```
## 开始make
```bash
cmake --build build --config Release -j --clean-first
```
运行结果：
```bash
[ 50%] Building CXX object CMakeFiles/llama-simple.dir/simple.cpp.o
[100%] Linking CXX executable llama-simple
[100%] Built target llama-simple
```

## 执行

```bash
./build/llama-simple -m ~/private_data/models/Qwen/Qwen3-0.6B-GGUF/Qwen3-0.6B-Q8_0.gguf  "您好!"
```
运行结果：

```bash
llama_kv_cache:      CUDA0 KV buffer size =    28.00 MiB
llama_kv_cache: size =   28.00 MiB (   256 cells,  28 layers,  1/1 seqs), K (f16):   14.00 MiB, V (f16):   14.00 MiB
llama_context: enumerating backends
llama_context: backend_ptrs.size() = 2
llama_context: max_nodes = 2488
llama_context: reserving full memory module
llama_context: worst-case: n_tokens = 64, n_seqs = 1, n_outputs = 1
graph_reserve: reserving a graph for ubatch with n_tokens =    1, n_seqs =  1, n_outputs =    1
llama_context: Flash Attention was auto, set to enabled
graph_reserve: reserving a graph for ubatch with n_tokens =   64, n_seqs =  1, n_outputs =   64
graph_reserve: reserving a graph for ubatch with n_tokens =    1, n_seqs =  1, n_outputs =    1
graph_reserve: reserving a graph for ubatch with n_tokens =   64, n_seqs =  1, n_outputs =   64
llama_context:      CUDA0 compute buffer size =    37.34 MiB
llama_context:  CUDA_Host compute buffer size =     0.31 MiB
llama_context: graph nodes  = 987
llama_context: graph splits = 2
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

三、# 参考文献：
1. [基于llama.cpp的QwQ32B模型推理](https://blog.csdn.net/hbkybkzw/article/details/146327526)
2. [如何用c++调用大模型——关于使用llama.cpp的lib库的简易教程] (https://blog.csdn.net/zh515858237/article/details/151251910?spm=1011.2415.3001.5331)
