# Alpaca.cpp

Run a fast ChatGPT-like model locally on your device. The screencast below is not sped up and running on an M2 Macbook Air with 4GB of weights. 


[![asciicast](screencast.gif)](https://asciinema.org/a/dfJ8QXZ4u978Ona59LPEldtKK)


This combines the [LLaMA foundation model](https://github.com/facebookresearch/llama) with an [open reproduction](https://github.com/tloen/alpaca-lora) of [Stanford Alpaca](https://github.com/tatsu-lab/stanford_alpaca) a fine-tuning of the base model to obey instructions (akin to the [RLHF](https://huggingface.co/blog/rlhf) used to train ChatGPT) and a set of modifications to [llama.cpp](https://github.com/ggerganov/llama.cpp) to add a chat interface. 

## Get Started (7B)

Download the zip file corresponding to your operating system from the [latest release](https://github.com/antimatter15/alpaca.cpp/releases/latest). On Windows, download `alpaca-win.zip`, on Mac (both Intel or ARM) download `alpaca-mac.zip`, and on Linux (x64) download `alpaca-linux.zip`. 

Download [ggml-alpaca-7b-q4.bin](https://huggingface.co/Sosaka/Alpaca-native-4bit-ggml/blob/main/ggml-alpaca-7b-q4.bin) and place it in the same folder as the `chat` executable in the zip file. There are several options: 

Once you've downloaded the model weights and placed them into the same directory as the `chat` or `chat.exe` executable, run:

```
./chat
```

The weights are based on the published fine-tunes from `alpaca-lora`, converted back into a pytorch checkpoint with a [modified script](https://github.com/tloen/alpaca-lora/pull/19) and then quantized with llama.cpp the regular way. 

## Getting Started (13B)

If you have more than 10GB of RAM, you can use the higher quality 13B `ggml-alpaca-13b-q4.bin` model. To download the weights, you can use

```

# Any of these commands will work. 
curl -o ggml-alpaca-13b-q4.bin -C - https://gateway.estuary.tech/gw/ipfs/Qme6wyw9MzqbrUMpFNVq42rC1kSdko7MGT9CL7o1u9Cv9G 
curl -o ggml-alpaca-13b-q4.bin -C - https://ipfs.io/ipfs/Qme6wyw9MzqbrUMpFNVq42rC1kSdko7MGT9CL7o1u9Cv9G 
curl -o ggml-alpaca-13b-q4.bin -C - https://cloudflare-ipfs.com/ipfs/Qme6wyw9MzqbrUMpFNVq42rC1kSdko7MGT9CL7o1u9Cv9G 

# BitTorrent
magnet:?xt=urn:btih:053b3d54d2e77ff020ebddf51dad681f2a651071&dn=ggml-alpaca-13b-q4.bin&tr=udp%3A%2F%2Ftracker.opentrackr.org%3A1337%2Fannounce&tr=udp%3A%2F%2Fopentracker.i2p.rocks%3A6969%2Fannounce&tr=udp%3A%2F%2Ftracker.openbittorrent.com%3A6969%2Fannounce&tr=udp%3A%2F%2F9.rarbg.com%3A2810%2Fannounce
https://btcache.me/torrent/053B3D54D2E77FF020EBDDF51DAD681F2A651071  
https://torrage.info/torrent.php?h=053b3d54d2e77ff020ebddf51dad681f2a651071
```

Once you've downloaded the weights, you can run the following command to enter chat

```
./chat -m ggml-alpaca-13b-q4.bin
```

## Getting Started (30B)

If you have more than 32GB of RAM (and a beefy CPU), you can use the higher quality 30B `alpaca-30B-ggml.bin` model. To download the weights, you can use

```
git clone https://huggingface.co/Pi3141/alpaca-30B-ggml
```

Once you've downloaded the weights, you can run the following command to enter chat

```
./chat -m ggml-model-q4_0.bin
```


## Building from Source (MacOS/Linux)


```sh
git clone https://github.com/antimatter15/alpaca.cpp
cd alpaca.cpp

make chat
./chat
```


## Building from Source (Windows)

- Download and install CMake: <https://cmake.org/download/>
- Download and install `git`. If you've never used git before, consider a GUI client like <https://desktop.github.com/>
- Clone this repo using your git client of choice (for GitHub Desktop, go to File -> Clone repository -> From URL and paste `https://github.com/antimatter15/alpaca.cpp` in as the URL)
- Open a Windows Terminal inside the folder you cloned the repository to
- Run the following commands one by one:

```ps1
cmake .
cmake --build . --config Release
```

- Download the weights via any of the links in "Get started" above, and save the file as `ggml-alpaca-7b-q4.bin` in the main Alpaca directory.
- In the terminal window, run this command:
```ps1
.\Release\chat.exe
```
- (You can add other launch options like `--n 8` as preferred onto the same line)
- You can now type to the AI in the terminal and it will reply. Enjoy!

## Anecdotal Examples/Comparisons of Different AI Models

Here we will provide anecdotal examples/comparisons of responses for prompts between the following AI models: 

- Alpaca 7B
- Alpaca 13B
- Alpaca 30B
- ChatGPT 3.5
- Bing AI

Please note that these examples are not comprehensive, and they should not be used as a basis for a formal evaluation of these AI models. Additionally, performance differs greatly between prompts, and we found that sometimes 7B gave better outputs than 13B and 30B and vice versa. Outputs even differed between consecutive runs in the same version. 

### Example Prompt 1:

Write an email to Trevor with some facts about quantum computing in a Star Wars theme.

#### Responses

##### Alpaca 7B
![Alpaca 7B](7B.jpg)

##### Alpaca 13B
![Alpaca 13B](13B.jpg)

##### Alpaca 30B
![Alpaca 30B](30B.jpg)

##### ChatGPT 3.5
![ChatGPT 3.5](gpt3.5.jpg)

##### Bing AI
![Bing AI](bingAI.jpg)

As you can see from the examples above, the responses generated by each AI model differ in quality and coherence. However, again, it is important to note that these examples are anecdotal, and more comprehensive testing is needed to provide a fair comparison between these AI models.


## Credit

This combines [Facebook's LLaMA](https://github.com/facebookresearch/llama), [Stanford Alpaca](https://crfm.stanford.edu/2023/03/13/alpaca.html), [alpaca-lora](https://github.com/tloen/alpaca-lora) and [corresponding weights](https://huggingface.co/tloen/alpaca-lora-7b/tree/main) by Eric Wang (which uses [Jason Phang's implementation of LLaMA](https://github.com/huggingface/transformers/pull/21955) on top of Hugging Face Transformers), and [llama.cpp](https://github.com/ggerganov/llama.cpp) by Georgi Gerganov. The chat implementation is based on Matvey Soloviev's [Interactive Mode](https://github.com/ggerganov/llama.cpp/pull/61) for llama.cpp. Inspired by [Simon Willison's](https://til.simonwillison.net/llms/llama-7b-m2) getting started guide for LLaMA. [Andy Matuschak](https://twitter.com/andy_matuschak/status/1636769182066053120)'s thread on adapting this to 13B, using fine tuning weights by [Sam Witteveen](https://huggingface.co/samwit/alpaca13B-lora). 


## Disclaimer

Note that the model weights are only to be used for research purposes, as they are derivative of LLaMA, and uses the published instruction data from the Stanford Alpaca project which is generated by OpenAI, which itself disallows the usage of its outputs to train competing models. 


