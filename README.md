# yllm - Yet another LLM command line interface

A streamlined command-line tool for interacting with LLM APIs that handles multiple input sources and streaming responses. Supports a wide range of models including Anthropic Claude, OpenAI, and many others.

## Quick Setup

1. Create config directory and copy a model config:
```bash
mkdir -p ~/.yllm
cp models/sonnet3.6 ~/.yllm/sonnet3.6
```

2. Add your API key:
```bash
nano ~/.yllm/sonnet3.6
```

3. Set as default model (optional):
```bash
yllm --set-default sonnet3.6
```

## Basic Usage

Simple queries:
```bash
yllm "What is the capital of France?"
yllm -m mixtral-8x7b "Explain quantum computing"  # Specify model
```

## Working with Input Sources

### Files
```bash
# Single file
yllm -f code.py "Explain this code"

# Multiple files
yllm -f doc1.txt -f doc2.txt "Compare these documents"
yllm -f paper.pdf "Summarize this" -f notes.txt "incorporating these points"
```

### URLs
```bash
# Single URL
yllm -u https://example.com "Summarize this page"

# Multiple URLs
yllm -u https://site1.com -u https://site2.com "Compare these websites"
```

### Mixed Sources
```bash
# Combine files and URLs
yllm -f research.pdf "Analyze this paper" -u https://related.com "in context of this article"

# Complex combinations
yllm "First, consider this code:" -f code.py \
    "Now look at this documentation:" -u https://docs.example.com \
    "Explain how they relate"
```

### Standard Input
```bash
# Implicit stdin (when no other inputs)
echo "Process this" | yllm "What does this mean?"

# Explicit stdin placement
cat data.txt | yllm "Before stdin" -c "after stdin"
```

## Output Control

Save responses:
```bash
# Auto-named files in current directory
yllm -z "Query with saved output"

# Specify output directory
yllm -Z /path/to/outputs/ "Query with saved output"

# Convert to PDF
yllm -P "Generate a report" -f data.txt
```

## Available Model Configurations

YLLM includes configurations for a wide range of models in the `models` directory:

### Anthropic Claude Models
- Claude 3 (`models/claude3`)
- Claude 3 Sonnet 3.6 (`models/sonnet3.6`)
- Claude 3 Sonnet 3.5 (`models/sonnet3.5`)

### Large Language Models
- Cerebras LLaMA 3.1 Series
  - 70B (`models/cerebras-llama3.1-70b`)
  - 8B (`models/cerebras-llama3.1-8b`)
- LLaMA Series
  - LLaMA 3 405B (`models/llama3-405b`)
  - LLaMA 3 70B (`models/llama3-70b`)
  - LLaMA 70B (`models/llama-70b`)
  - LLaMA 70B Code (`models/llama-70b-code`)

### Mixtral Models
- Mixtral 8x22B (`models/mixtral-8x22b`)
- Mixtral 8x7B (`models/mixtral-8x7b`)
- Nous Mixtral (`models/nous-mixtral`)

### Groq-Optimized Models
- Groq Gemma 2 9B (`models/groq-gemma2-9b`)
- Groq LLaMA 3 70B (`models/groq-llama3-70b`)
- Groq Mixtral 8x7B (`models/groq-mixtral-8x7b`)

### Specialized Models
- CMDR Series
  - CMDR (`models/cmdr`)
  - CMDR+ (`models/cmdr+`)
  - CMDR Web (`models/cmdr-web`)
  - CMDR+ Web (`models/cmdr+web`)
- Codestral (`models/codestral`)
- GPT-4 (`models/gpt-4`, `models/gpt4o`)
- LLaVA 1.5 7B (`models/llava-1.5-7b-hf`)
- LZLV 70B (`models/lzlv-70b`)
- Mistral 7B (`models/mistral-7b`)
- PPLX 70B (`models/pplx-70b`)
- Qwen 72B (`models/qwen-72b`)
- Sonar Medium (`models/sonar-medium`)
- Striped Hyena
  - Base (`models/stripedhyena`)
  - Hessian (`models/stripedhyena-hessian`)
- Yi 34B (`models/yi-34b`)

## Options

```
-h, --help                   Print help
-s, --settings <file>       Load YLLM_* settings
-m, --model <model>         Select model
-D, --set-default <model>   Set default model
-S, --show-default         Show default model
-C, --clear-default        Clear default model
-a, --api-url <url>        API URL
-k, --api-key <key>        API key
-t, --temperature <t>      Temperature (default: 0.1)
-p, --top-p <p>           Top-p value (default: 0.9)
-l, --max-tokens <n>      Max tokens (default: 4096)
-c, --stdin               Read from stdin
-u, --url <url>           Read from URL
-f, --file <file>         Read from file
-d, --dump-prompt         Show prompt and exit
-r, --raw-stream          Show raw API stream
-z, --just-save-it        Save to current directory
-Z, --save-it-to <prefix> Save with prefix
-P, --pdf-it              Convert output to PDF
```

## Dependencies

- `curl`: API requests
- `lynx`: Web page extraction
- `jq`: JSON processing
- `file`: File type detection
- `pdftotext`: PDF extraction
- `pandoc`: Format conversion
- `stdbuf`: Output buffering

## License

MIT License - See [LICENSE](LICENSE) file
