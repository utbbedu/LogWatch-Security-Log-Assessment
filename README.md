# LogWatch

An AI-powered security log triage tool. It reads security log entries and uses a
coding language model (Qwen Coder, or any OpenAI-compatible model) to classify
each entry as **BENIGN**, **SUSPICIOUS**, or **MALICIOUS**, with a severity
(1&ndash;5) and a one-sentence reason. It processes whole log files in batch and
can generate a detection rule from what it finds.


## What it does
- Classifies each log entry (BENIGN / SUSPICIOUS / MALICIOUS) with a 1&ndash;5 severity and a reason.
- Returns validated JSON, and processes a whole log file in batch.
- Generates a detection rule (for example a Sigma rule) from the suspicious and malicious findings.
- Treats log text as untrusted input and uses a hardened prompt to resist prompt injection.

## Requirements
- Python 3.9 or newer
- The `openai` package (`pip install openai`)
- Access to an OpenAI-compatible model endpoint (a vLLM server, the class Qwen Coder server, etc.)

## Setup
Install the one dependency:

```
pip install openai
```

Set your model endpoint and key as environment variables (never hard-code them):

```
export QWEN_BASE_URL="http://your-server:8000/v1"
export QWEN_API_KEY="your-api-key"
```

## Usage
Open the notebook and run the cells top to bottom, or import the functions into
your own script. Point `LOG_FILE` at a log file (`.txt` or `.csv`) of log lines,
and the tool will assess them and save the results.

## Security notes
- The API key is read at runtime (`getpass`) or from an environment variable; it is never stored in the notebook.
- Log data is treated as untrusted; the tool uses a hardened prompt to resist instructions hidden in the input.

## License
MIT &mdash; see the `LICENSE` file.
