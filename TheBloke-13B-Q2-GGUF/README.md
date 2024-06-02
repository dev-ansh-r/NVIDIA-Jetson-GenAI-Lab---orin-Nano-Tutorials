# Performance Results of llama-2-13B Model on Jetson Orin Nano 

The following is the benchmark of Llama2-13B Model on Jetson Orin Nano Development board(8gb). The model is tested using the Jetson GenAI Lab Tutorials provided by NVIDIA and [llama.cpp](https://github.com/ggerganov/llama.cpp) loader from [Georgi Gerganov](https://github.com/ggerganov). 

The benchmark is performed to check the inference time of different quantizations of the model on the board. 

The following table will illustrate the results on the development kit.

On the Jetson GenAI lab tutorial they mentioned that the Jetson Orin Nano will only support 7-b models. However, we made a test on 13b model and upon producing the inference, the gpu isn't invoked in the process. As you can see in the jtop image, the gpu is not used to make an inference and the overall process has been happening on the CPU.


<break><img src="../img/TheBloke-1301.png" width="500" height="300">

<break><img src="../img/TheBloke-1302.png" width="500" height="300">

<break><img src="../img/llama2-13B/jtop.png" width="500" height="300">

## Text-Generation web-ui results

| Task             | Timing           | Description                                                                        |
|------------------|------------------|------------------------------------------------------------------------------------|
| Load time        | 9520.50 ms       | Time to load or initialize components                                               |
| Sample time      | 185.35 ms / 512 runs | Time to sample data (0.36 ms per token, 2762.28.86 tokens/s)                         |
| Prompt eval time | 9520.24 ms / 73 tokens | Time to evaluate prompts (835.50 ms per token, 7.67 tokens/s)                    |
| Eval time        | 2295406.18 ms / 511 runs | Time for evaluations (252.10 ms per token, 0.22 tokens/s)                         |
| Total time       | 2308958.71 ms / 584 tokens | Total time for the task execution (0.22 tokens/second)                                               |

The overall execution takes upto **<u>2311.20 seconds</u>** (0.22 tokens/s, 512 tokens)


<break><img src="../img/llama2-13B/Webui Results.png" width="auto" height="auto">

## Inference results on llama.cpp loader

However, when we use the same model to make an inference in llama.cpp we get full gpu usage and we get a faster inference.


| Task             | Timing           | Description                                                                        |
|------------------|------------------|------------------------------------------------------------------------------------|
| Load time        | 2642.89 ms       | Time to load or initialize components                                               |
| Sample time      | 7.73 ms / 128 runs | Time to sample data (0.06 ms per token, 16558.86 tokens/s)                         |
| Prompt eval time | 6683.99 ms / 8 tokens | Time to evaluate prompts (835.50 ms per token, 1.20 tokens/s)                    |
| Eval time        | 111708.85 ms / 127 runs | Time for evaluations (252.10 ms per token, 1.14 tokens/s)                         |
| Total time       | 118465.74 ms / 135 tokens | Total time for the task execution (3.65 tokens/second)                                                  |

The overall execution takes upto **<u>118.46 seconds</u>** (0.22 tokens/s, 512 tokens)

<break><img src="../img/llama2-13B/llama.cpp results.png" width="auto" height="auto"> 




<!-- <break><img src="../img/llama2-13B/Benchmarks.png" width="auto" height="auto"> -->