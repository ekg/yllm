# yllm - Yet another LLM command line interface

## Description

`yllm` is a Bash script utility designed to interact with various LLM APIs including Anthropic Claude, OpenAI, and others. It supports streaming responses and allows users to input prompts, documents (`-f`), or web pages (`-u`). The tool is designed to be both simple for basic usage and powerful for programmatic prompt construction.

## Setup

The `models` directory contains configuration files for various LLM models. To use a model:

1. Create your yllm config directory:
```bash
mkdir -p ~/.yllm
```

2. Copy your chosen model config and update the API key:
```bash
# Example: copying a model config
cp models/yi-34b ~/.yllm/yi-34b
# Edit the file to add your API key
nano ~/.yllm/yi-34b
```

The config files contain the necessary settings for each model - you just need to add your API key.

### Examples

Basic usage with any model:
```bash
yllm -s yi-34b "What is the capital of France?"
```

For example, to use one of the latest models (Claude 3.5 Sonnet):
```bash
cp models/sonnet3.6 ~/.yllm/sonnet3.6
nano ~/.yllm/sonnet3.6  # Add your API key
yllm -s sonnet3.6 "What is the capital of France?"
```

## Usage

Run the script with your desired prompt as an argument. You can input the prompt directly or use options for more complex inputs like documents or web pages.

```bash
yllm [options] [prompt]
```

Prompts can be built from input arguments in the order they are provided. Here are some examples:

```bash
yllm "tell me about goats"
yllm tell me about goats
```

```bash
yllm "summarize the following code" -f yllm "suggest ways to improve the documentation:" -f README.md
yllm "first document" -u https://cool.site "second document" -u https://xxxx.com "compare the two documents"
```

### Options

- `-h`, `--help`: Print help text and exit.
- `-s`, `--settings <file>`: Load `YLLM_*` environment settings from the given file.
- `-a`, `--api-url`: The API URL to use (default: `https://api.fireworks.ai/inference/v1/chat/completions`).
- `-m`, `--model <model>`: The model to use for the completion (default: `accounts/fireworks/models/yi-34b-200k-capybara`).
- `-t`, `--temperature <t>`: The temperature for the model (default: 0.1).
- `-p`, `--top-p <p>`: The top-p value for the model (default: 0.9).
- `-l`, `--max-tokens <n>`: The maximum number of tokens to generate (default: 4096).
- `-c`, `--stdin`: Read data from standard input.
- `-u`, `--url <url>`: Read text data from the given URL.
- `-f`, `--file <file>`: Read text data from the given file.
- `-d`, `--dump-prompt`: Write the prompt to stdout and exit.
- `-r`, `--raw-stream`: Show the raw JSONL stream from the API.

## Dependencies

`yllm` depends on `curl`, `lynx`, `jq`, `file`, `pdftotext`, `pandoc`, and `stdbuf` for its operations.

## License

`yllm` is licensed under the MIT License. See the [LICENSE](LICENSE) file for more information.
