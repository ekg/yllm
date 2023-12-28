# yllm - Yet another LLM command line interface

## Description

`yllm` is a Bash script utility designed to query OpenAI compatible API endpoints.
It's specifically been tested with Fireworks.ai.
It is a simple and easy-to-use tool that allows you to interact with large language models (LLMs) by providing a prompt and receiving a response.

## Usage

To use `yllm`, first set your API key in the shell: `export YLLM_API_KEY=.....`.
Put `yllm` in your `$PATH`.
Then, simply run the script with the desired prompt as an argument.

```bash
yllm [options] [prompt]
```

All positional arguments are concatenated into the prompt, allowing for a quick quote-free style.
The following two examples are the same:

```bash
yllm "tell me about goats"
yllm tell me about goats
```

### Options

- `-h`, `--help`: Print this help text and exit.
- `-a`, `--api-url`: The API URL to use (default: `https://api.fireworks.ai/inference/v1/chat/completions`).
- `-m`, `--model <model>`: The model to use for the completion (default: `accounts/fireworks/models/yi-34b-200k-capybara`).
- `-t`, `--temperature <t>`: The temperature for the model (default: 0.1).
- `-p`, `--top-p <p>`: The top-p value for the model (default: 0.9).
- `-l`, `--max-tokens <n>`: The maximum number of tokens to generate (default: 4096).
- `-c`, `--stdin`: Read data from standard input, put before prompt.
- `-u`, `--url <url>`: Read text data from the given URL, put before prompt.
- `-f`, `--file <file>`: Read text data from the given file, put before prompt.

## Dependencies

yllm depends on the following utilities:

- `curl`: For making HTTP requests to the API endpoint.
- `lynx`: For extracting text from web pages.
- `jq`: For JSON manipulation and parsing.
- `file`: For checking file types.
- `pdftotext`: For converting PDF files to text.
- `pandoc`: For converting DOCX/DOC files to text.
- `stdbuf`: For buffering standard output.

## License

yllm is licensed under the MIT License. See the [LICENSE](LICENSE) file for more information.
