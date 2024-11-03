# yllm - Yet another LLM command line interface

## Description

`yllm` is a Bash script utility designed to interact with various LLM APIs including Anthropic Claude, OpenAI, and others. It supports streaming responses and allows users to input prompts, documents (`-f`), or web pages (`-u`). The tool is designed to be both simple for basic usage and powerful for programmatic prompt construction.

## Setup

To configure `yllm`, you'll need to set up a model configuration file. Here's how to set up Claude 3.5 Sonnet:

1. Create the yllm config directory:
```bash
mkdir -p ~/.yllm
```

2. Create a settings file for Claude 3.5 Sonnet:
```bash
cat > ~/.yllm/sonnet3 << 'EOF'
YLLM_API_KEY=your_anthropic_api_key_here
YLLM_API_URL=https://api.anthropic.com/v1/messages
YLLM_ANTHROPIC_MODE=1
YLLM_EXTRA_CURL_FLAGS="-H 'anthropic-version: 2023-06-01'"
YLLM_MODEL=claude-3-5-sonnet-20240620
EOF
```

Replace `your_anthropic_api_key_here` with your actual Anthropic API key.

### Example

To use Claude 3.5 Sonnet, simply run:

```bash
yllm -s sonnet3 "What is the capital of France?"
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
