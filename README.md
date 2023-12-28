# yllm - Yet another LLM command line interface

## Description

`yllm` is a Bash script utility designed to query OpenAI compatible API endpoints.
It's been tested with llama.cpp and Fireworks.ai, but should work with any endpoint that supports streaming.
It is a simple and easy-to-use tool that allows you to interact with large language models (LLMs) by providing a prompt and receiving a response.
`yllm` covers the three most common uses of LLMs: querying based on a prompt, document (`-f`), and web page (`-u`) inputs.

# Setup

To use `yllm` with llama.cpp, you'd first run the llama.cpp server: `server -m model.gguf`, then set the endpoint in your shell startup script with `export YLLM_API_URL="http://localhost:8080/v1/chat/completions"`.
To use `yllm` with fireworks.ai or another commercial provider, first set your API key in the shell: `export YLLM_API_KEY=.....`, and also set an endpoint, e.g. `export YLLM_API_URL="https://api.fireworks.ai/inference/v1/chat/completions"`.
The same pattern should work for any OpenAI-compatible API endpoint.

Finally, put `yllm` in your `$PATH`.

## Usage

Simply run the script with the desired prompt as an argument.

```bash
yllm [options] [prompt]
```

All positional arguments are concatenated into the prompt, allowing for a quick quote-free style.
The following two examples are the same:

```bash
yllm "tell me about goats"
yllm tell me about goats
```

The prompt is built from input arguments in the order they are provided.
Multiple URLs, files, and prompt sections can be provided.
For instance:

```bash
yllm "summarize the following code" -f yllm "suggest ways to improve the documentation:" -f README.md
yllm "first document" -u https://cool.site "second document" -u https://xxxx.com "compare the two documents"
```

We can also read from stdin into the prompt (with `-c`) at any point, but only once.

### Options

- `-h`, `--help`: Print this help text and exit.
- `-a`, `--api-url`: The API URL to use (default: `https://api.fireworks.ai/inference/v1/chat/completions`).
- `-m`, `--model <model>`: The model to use for the completion (default: `accounts/fireworks/models/yi-34b-200k-capybara`).
- `-t`, `--temperature <t>`: The temperature for the model (default: 0.1).
- `-p`, `--top-p <p>`: The top-p value for the model (default: 0.9).
- `-l`, `--max-tokens <n>`: The maximum number of tokens to generate (default: 4096).
- `-c`, `--stdin`: Read data from standard input.
- `-u`, `--url <url>`: Read text data from the given URL.
- `-f`, `--file <file>`: Read text data from the given file.
- `-d`, `--dump-prompt`: Write the prompt to stdout and exit.

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
