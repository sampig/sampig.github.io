---
layout: post
title: "Learning Ollama"
date: 2025-03-21 22:25:05 +0200
category: tutorial
tagline: ""
tags: [AI, LLM, Ollama, Docker]
abstract: "Introduction and usage guide for running large language models locally with Ollama."
---
{% include JB/setup %}

* [Intro](#intro)
* [Start Ollama](#start-ollama)
* [Usage of Ollama](#usage-of-ollama)
  * [REST API](#rest-api)
  * [Other Libraries](#other-libraries)
    * [Python](#python)
    * [Javascript](#javascript)
  * [Other Commands](#other-commands)
  * [A Sample](#a-sample)
* [References](#references)


# Intro

Ollama is a lightweight, extensible framework for building and running language models on a local machine.  
It supports **Llama**, **DeepSeek-R1**, **Phi-4**, **Mistral**, **Gemma 3**, and other models.


# Start Ollama

1. Download from the official website and run:

```sh
./ollama serve
```

2. Run with Docker:

```sh
docker run -d \
  -v ollama:/root/.ollama \
  -p 11434:11434 \
  --name ollama ollama/ollama
```

(Run docker pull ollama/ollama first if needed)

After this, a local Ollama server daemon is running.


# Usage of Ollama

Run and chat with a model:

```sh
ollama run llama3
```

Run model inside Docker:

```sh
docker exec -it ollama ollama run llama3
```

## REST API

Generate text:

```sh
curl http://localhost:11434/api/generate -d '{
  "model": "llama3.2",
  "prompt": "Why is the sky blue?"
}'
```

Chat API:

```sh
curl http://localhost:11434/api/chat -d '{
  "model": "llama3.2",
  "messages": [
    { "role": "user", "content": "why is the sky blue?" }
  ]
}'
```

## Other Libraries

### Python

Install:

```sh
pip install ollama
```

### Javascript

Install:

```sh
npm i ollama
```

## Other Commands

List models:

```sh
ollama list
```

Show model info:

```sh
ollama show llama3.2
```

List loaded models:

```sh
ollama ps
```

Stop a running model:

```sh
ollama stop llama3.2
```

Start Ollama:

```sh
ollama serve
```

Python and JavaScript SDKs provide equivalent functions (e.g. ollama.list()).

## A Sample

### Python

Chat with local Ollama in Python

```python
from ollama import Client

client = Client(
    host='http://localhost:11434',
    headers={'x-some-header': 'value-zhuzhu'}
)

response = client.chat(
    model='llama3.2',
    messages=[
        {
            'role': 'user',
            'content': 'Why is the sky blue?',
        },
    ]
)

print(response)
print(response.message.content)
```

Output:

```text
model='llama3.2' created_at='2025-03-19T11:55:43.926128969Z' done=True done_reason='stop' total_duration=1114604658758 load_duration=22662584 prompt_eval_count=31 prompt_eval_duration=5412000000 eval_count=321 eval_duration=1109162000000 message=Message(role='assistant', content="The sky appears blue because of a phenomenon called scattering, which occurs when sunlight interacts with the tiny molecules of gases in the Earth's atmosphere.\n\nHere's what happens:\n\n1. Sunlight enters the Earth's atmosphere and consists of a spectrum of colors, including all the colors of the visible light spectrum.\n2. When sunlight passes through the atmosphere, it encounters tiny molecules of gases such as nitrogen (N2) and oxygen (O2).\n3. These molecules scatter the shorter (blue) wavelengths of light more than the longer (red) wavelengths. This is known as Rayleigh scattering, named after the British physicist Lord Rayleigh, who first described the phenomenon in the late 19th century.\n4. The blue light is scattered in all directions by the atmospheric molecules, while the longer wavelengths of light, such as red and orange, continue to travel in a straight line and reach our eyes from a more direct path.\n5. Since the Earth's atmosphere scatters shorter wavelengths (like blue) more than longer wavelengths (like red), the sky appears blue to our eyes because of this scattering effect.\n\nIt's worth noting that the color of the sky can change under different conditions, such as:\n\n* During sunrise and sunset, when the light has to travel through more of the Earth's atmosphere, which scatters the shorter wavelengths even more, making the sky appear reddish.\n* At high altitudes or in areas with low atmospheric pressure, where there are fewer molecules for the light to scatter off, the sky can appear more blue.\n\nSo, that's the reason why the sky is blue!", images=None, tool_calls=None)
```

### Javascript

Chat with local Ollama in JS

```js
import ollama from 'ollama'

const response = await ollama.chat({
  model: 'llama3.1',
  messages: [{ role: 'user', content: 'Why is the sky blue?' }],
})

console.log(response.message.content)
```


# References

1. [Ollama Official Website](https://ollama.com/){:target=”_blank”}
2. [Ollama GitHub](https://github.com/ollama/ollama){:target=”_blank”}
3. [Ollama Docker Image](https://hub.docker.com/r/ollama/ollama){:target=”_blank”}
4. [ollama-python](https://github.com/ollama/ollama-python){:target=”_blank”}
5. [ollama-js](https://github.com/ollama/ollama-js){:target=”_blank”}
