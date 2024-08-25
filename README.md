# ARCstoryMaker
Overview The Story Maker Program is a Python-based application that generates a story based on user input prompts. The program consists of three main parts:
1. Story Writer
2. Image Generator
3. Story Book

Developed on 13th Gen Intel CPU and Intel ARC A750 GPU

Pre-requisites:

Llama CPP running on Intel ARC A750 via vulkan: https://github.com/ggerganov/llama.cpp
- Change IP and port number as per the server configured.
- The code assumes the server is hosted on localhost and default port. 

LLM Model: https://huggingface.co/bartowski/Meta-Llama-3.1-8B-Instruct-GGUF

Comfy UI running in Intel ARC A750 via IPEX: https://github.com/comfyanonymous/ComfyUI 
- Change IP and port number as per the server configured.
- The code assumes the server is hosted on localhost and default port. 

ComfyUI-gguf custom node for Q4 model: https://github.com/city96/ComfyUI-GGUF

Flux.1 quantized Model: https://huggingface.co/city96/FLUX.1-schnell-gguf/tree/main 


Install requrirements for this project and run the .py file using streamlit. 

streamlit run .\storyMaker.py     
