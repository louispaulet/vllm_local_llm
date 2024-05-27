# VLLM OpenAI Server Setup

This guide provides instructions for setting up and using the VLLM (Virtual Large Language Model) OpenAI server using Docker.

## Prerequisites

- Docker installed on your system
- NVIDIA GPU with CUDA support (if you want to utilize GPU acceleration)

## Step 1: Start the Server

Run the following command to start the server:

```bash
docker run --gpus all 
    -v ~/.cache/huggingface:/root/.cache/huggingface 
    --env "HUGGING_FACE_HUB_TOKEN=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" 
    -p 8000:8000 
    --ipc=host 
    vllm/vllm-openai:latest 
    --model TheBloke/Mistral-7B-Instruct-v0.2-AWQ
```

This command starts a Docker container with GPU support, mounts the Hugging Face cache directory, exposes port 8000 for communication, and specifies the model to be used (`TheBloke/Mistral-7B-Instruct-v0.2-AWQ`).

## Step 2: Making API Calls

You can make API calls to the server using tools like `curl`. Here's an example of a "Hello world" API call:

```bash
curl http://localhost:8000/v1/chat/completions 
  -H "Content-Type: application/json" 
  -d '{
     "model": "TheBloke/Mistral-7B-Instruct-v0.2-AWQ",
     "messages": [{"role": "user", "content": "What is the capital of France?"}],
     "temperature": 0.7
   }'
```

This command sends a request to the server running on `localhost:8000`. It specifies the model to use, provides a user message (`"What is the capital of France?"`), and sets the temperature parameter to control the creativity of the response.

## Additional Notes

- Ensure that the Docker container is running and accessible before making API calls.
- Adjust the parameters in the API call (`messages`, `temperature`, etc.) as per your requirements.
- Replace `"What is the capital of France?"` with your desired input text for testing.
