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

Command used: 

Run below command in new terminal to run Llama server using Llama CPP.

./llama-server.exe -m <model_path> --port 8080 -ngl 99 -c 16384

Comfy UI running in Intel ARC A750 via IPEX: [https://github.com/comfyanonymous/ComfyUI](https://github.com/comfyanonymous/ComfyUI?tab=readme-ov-file#intel-gpus) 
- Change IP and port number as per the server configured.
- The code assumes the server is hosted on localhost and default port. 

ComfyUI-gguf custom node for Q4 model: https://github.com/city96/ComfyUI-GGUF

Flux.1 quantized Model: https://huggingface.co/city96/FLUX.1-schnell-gguf/tree/main 

Open new Anaconda Prompt in administrator mode.

Run C:\Program Files (x86)\Intel\oneAPI\2024.2\oneapi-vars.bat to initialize oneAPI variables. This is required for IPEX. 

Navigate to comfy ui git folder. 

Run comfy ui server using below command: 

python main.py --force-fp16 --bf16-vae --use-pytorch-cross-attention --disable-ipex-optimize --highvram

Install requirements for this project and run the .py file using streamlit. 

streamlit run .\storyMaker.py    

![Story Writer](https://github.com/vishwanathan-iyer/ARCstoryMaker/blob/main/img/story-writer.png)

![Image Generator](https://github.com/vishwanathan-iyer/ARCstoryMaker/blob/main/img/img-writer.png)

![Story Book](https://github.com/vishwanathan-iyer/ARCstoryMaker/blob/main/img/story-book.png)


Hardware Notes:


As long as the LLM server hosted has an OpenAI complaint API, this code should technically work any hardware vendors implementation or backend or other inference application that serve LLM models in OpenAI compliant API. 


Similarly for Comfy UI for image generation as per the supportrd hardware mentioned in its git repo, if the comfy ui server is hoster as per your hardware configuration this application should technically work on any hardware and any model that you choose to use.

Please update the IP in the code if not hosted on localhost and their default ports.

However both of these are not tested currently.The output quality does get impacted due to hardware constraints, model type and model size. 



