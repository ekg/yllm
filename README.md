# yllm - Yet another LLM command line interface

## Description

`yllm` is a Bash script utility designed to interact with various LLM APIs including Anthropic Claude, OpenAI, and others. It supports streaming responses and allows users to input prompts, documents (`-f`), or web pages (`-u`). The tool is designed to be both simple for basic usage and powerful for programmatic prompt construction.

## Pre-configured Models

The `models` directory contains ready-to-use configurations for many popular models:

### Anthropic Models
- Claude 3 Opus (via `models/claude3`)
- Claude 3 Sonnet 3.6 (via `models/sonnet3.6`)
- Claude 3 Sonnet 3.5 (via `models/sonnet3.5`)

### Open Source Models
- Mixtral 8x7B (via `models/mixtral-8x7b`)
- Mixtral 8x22B (via `models/mixtral-8x22b`)
- Yi-34B (via `models/yi-34b`)
- Qwen 72B (via `models/qwen-72b`)
- Llama 70B (via `models/llama-70b`)
- Llama 70B Code (via `models/llama-70b-code`)
- Llama3 70B (via `models/llama3-70b`)
- Llama3 405B (via `models/llama3-405b`)
- Mistral 7B (via `models/mistral-7b`)
- Nous Mixtral (via `models/nous-mixtral`)
- Striped Hyena (via `models/stripedhyena`)
- Striped Hyena Hessian (via `models/stripedhyena-hessian`)

### Multimodal Models
- LLaVA 1.5 7B (via `models/llava-1.5-7b-hf`)

## Setup

The `models` directory contains configuration files for various LLM models. To use a model:

1. Create your yllm config directory:
```bash
mkdir -p ~/.yllm
```

2. Copy your chosen model config, update the API key, and optionally set it as default:
```bash
# Example: copying a model config
cp models/sonnet3.6 ~/.yllm/sonnet3.6
# Edit the file to add your API key
nano ~/.yllm/sonnet3.6

# Optionally set as default model
yllm --set-default sonnet3.6
```

The config files contain the necessary settings for each model - you just need to add your API key. Setting a default model means you don't need to specify `-m model` for every command.

### Examples

Basic usage with any model:
```bash
yllm "What is the capital of France?"  # Uses default model if set
yllm -m sonnet3.6 "What is the capital of France?"  # Explicitly specify model
```

Complex prompts combining multiple inputs:
```bash
yllm "summarize the following code" -f yllm "suggest ways to improve the documentation:" -f README.md
yllm "first document" -u https://cool.site "second document" -u https://xxxx.com "compare the two documents"
```

## Usage

Run the script with your desired prompt as an argument:

```bash
yllm [options] [--] [prompt]
```

If no prompt is provided, it will read from standard input.
The prompt is built from input arguments in the order they are provided.

### Options

- `-h`, `--help`: Print help text and exit.
- `-s`, `--settings <file>`: Load YLLM_* env settings from the given file.
- `-m`, `--model <model>`: The model to use for the completion
- `-D`, `--set-default <model>`: Set the default model (name or path)
- `-S`, `--show-default`: Show the current default model
- `-C`, `--clear-default`: Clear the default model setting
- `-a`, `--api-url <url>`: The API URL to use
- `-k`, `--api-key <key>`: The API key to use
- `-t`, `--temperature <t>`: The temperature for the model (default: 0.1)
- `-p`, `--top-p <p>`: The top-p value for the model (default: 0.9)
- `-l`, `--max-tokens <n>`: The maximum number of tokens to generate (default: 4096)
- `-c`, `--stdin`: Read data from standard input
- `-u`, `--url <url>`: Read text data from the given URL
- `-f`, `--file <file>`: Read text data from the given file
- `-d`, `--dump-prompt`: Write the prompt to stdout and exit
- `-r`, `--raw-stream`: Show the raw JSONL stream from the API
- `-z`, `--just-save-it`: Write inputs and outputs to hash-named file with prefix='./'
- `-Z`, `--save-it-to <prefix>`: Write inputs and outputs to hash-named file with the given prefix
- `-P`, `--pdf-it`: When saving, convert output to PDF

## Dependencies

`yllm` depends on:
- `curl`: For API requests
- `lynx`: For web page text extraction
- `jq`: For JSON processing
- `file`: For file type detection
- `pdftotext`: For PDF text extraction
- `pandoc`: For document format conversion
- `stdbuf`: For output buffering control

## License

`yllm` is licensed under the MIT License. See the [LICENSE](LICENSE) file for more information.
