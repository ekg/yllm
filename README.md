# yllm - Yet another LLM command line interface

## Description

`yllm` is a Bash script utility designed to query OpenAI compatible API endpoints, including but not limited to llama.cpp, Fireworks.ai, OpenAI, and together.ai. It supports streaming and is compatible with any endpoint that adheres to the OpenAI API specifications. `yllm` simplifies the interaction with large language models (LLMs) by allowing users to input a prompt, document (`-f`), or web page (`-u`) and receive a response. It is designed to be straightforward, covering the three most common uses of LLMs efficiently, and also a powerful tool for rapid programmatic prompt construction.

## Setup

To configure `yllm` for use with LLM APIs, you need to set the API endpoint, the API key, and the model. This can be done on the command line, but a more flexible approach is to set up configuration files containing the key parameters for each model. These configuration files can then be easily loaded to set the necessary variables.

Create a settings file with the following content:

```bash
YLLM_MODEL="accounts/fireworks/models/yi-34b-200k-capybara"
YLLM_API_URL="https://api.fireworks.ai/inference/v1/chat/completions"
YLLM_API_KEY="your_fireworks_api_key_here"
```

Replace `"your_fireworks_api_key_here"` with your actual API key.

To use a settings file, include the `-s` option followed by the path to your settings file when running `yllm`:

```bash
yllm -s path/to/your/settings_file "What is the capital of France?"
```

`yllm` will check if the passed settings file exists, and use it if it does.
If it doesn't it'll check you `~/.yllm` directory, allowing you to organize your settings files neatly (e.g., `~/.yllm/yi-34b`, `~/.yllm/gpt-4`).

The settings feature enables you to switch between different configurations for various models or API providers without manually changing environment or command line variables each time.

### Example

To use an API and model defined in a settings file `yi-34b` located in the `~/.yllm` directory, you can run:

```bash
yllm -s yi-34b "What is the capital of France?"
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
