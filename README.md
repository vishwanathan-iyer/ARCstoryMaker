# ARCstoryMaker
Overview The Story Maker Program is a Python-based application that generates a story based on user input prompts. The program consists of three main parts:
1. Story Writer
2. Image Generator
3. Story Book

Developed on 13th Gen Intel CPU and Intel ARC A750 GPU

# Pre-requisites and Steps:
## LLAMA CPP Server Setup:
Llama CPP running on Intel ARC A750 via vulkan(no external dependency)/SYCL(faster optimized): 
- Clone repo from here: https://github.com/ggerganov/llama.cpp

- LLM Model: https://huggingface.co/bartowski/Meta-Llama-3.1-8B-Instruct-GGUF

Run below commands in new command prompt to run Llama server using Llama CPP:
- For vulkan run the command directly: ./llama-server.exe -m <model_path> --port 8080 -ngl 99 -c 16384
- For SYCL ensure that environment is initialized
  - Open Anacoda command prompt in administrator mode
  - Run C:\Program Files (x86)\Intel\oneAPI\2024.2\oneapi-vars.bat to initialize oneAPI variables.
  - set SYCL_CACHE_PERSISTENT=1
  - set ONEAPI_DEVICE_SELECTOR=level_zero:1  -> In multi GPU scenario, this ensures that the model runs on GPU1 (Discrete Graphics)
  - set SYCL_PI_LEVEL_ZERO_USE_IMMEDIATE_COMMANDLISTS=1
  - Then run: ./llama-server.exe -m <model_path> --port 8080 -ngl 99 -c 16384 

## COMFY UI Server Setup:
Comfy UI running in Intel ARC A750 via IPEX: [https://github.com/comfyanonymous/ComfyUI](https://github.com/comfyanonymous/ComfyUI?tab=readme-ov-file#intel-gpus) 

ComfyUI-gguf custom node for Q4 model: https://github.com/city96/ComfyUI-GGUF

Flux.1 quantized Model: https://huggingface.co/city96/FLUX.1-schnell-gguf/tree/main 

- Open new Anaconda Prompt in administrator mode.
- Run C:\Program Files (x86)\Intel\oneAPI\2024.2\oneapi-vars.bat to initialize oneAPI variables. This is required for IPEX. 
- set SYCL_CACHE_PERSISTENT=1
- set ONEAPI_DEVICE_SELECTOR=level_zero:1
- set SYCL_PI_LEVEL_ZERO_USE_IMMEDIATE_COMMANDLISTS=1

Navigate to comfy ui git folder. 

Run comfy ui server using below command: 

python main.py --force-fp16 --bf16-vae --use-pytorch-cross-attention --disable-ipex-optimize --highvram

Note: There are lot of arguments in comfy ui, added one here that is tested to give good outputs, performance depends on size of prompt.

Install requirements for this project and run the .py file using streamlit. 

streamlit run .\storyMaker.py    

# Outputs
## Story Writer 
![Story Writer](https://github.com/vishwanathan-iyer/ARCstoryMaker/blob/main/img/story-writer.png)

## Image Generator
![Image Generator](https://github.com/vishwanathan-iyer/ARCstoryMaker/blob/main/img/img-writer.png)

## Story Book
![Story Book](https://github.com/vishwanathan-iyer/ARCstoryMaker/blob/main/img/story-book.png)

# View stories
To view just the stories if you don't have access to hardware to generate them follow these steps:
1. Make a venv in python: python -m venv ARCstoryMaker
2. Acitvate the environment: .\ARCstoryMaker\Scripts\activate
3. Update pip: python.exe -m pip install --upgrade pip
4. Install requirements: pip install -r .\requirements.txt
5. Then run streamlit run .\storyMaker.py. This will open browser with the app.
6. Navigate to story book section and choose the story you want to read from the dropdowm menu.   


# Hardware Notes:


- As long as the LLM server hosted has an OpenAI complaint API, this code should technically work any hardware vendors implementation or backend or other inference application that serve LLM models in OpenAI compliant API. 


- Similarly for Comfy UI for image generation as per the supportrd hardware mentioned in its git repo, if the comfy ui server is hoster as per your hardware configuration this application should technically work on any hardware and any model that you choose to use.

- Please update the IP in the code if not hosted on localhost and their default ports.

- However both of these are not tested currently.The output quality does get impacted due to hardware constraints, model type and model size. 



