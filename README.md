# ai-agent

A small AI coding agent in Python. It uses Google Gemini's function calling to inspect and change files in a sandboxed project directory. By default that's the included `calculator` app.

## How it works

1. You pass a prompt on the command line.
2. Gemini decides which tool to call.
3. The agent runs the tool, sends the result back to the model, and repeats until the model gives a final answer.

Tools available to the model (all limited to the working directory):

- `get_files_info`: list files and sizes
- `get_file_content`: read a file (truncated at 10,000 characters)
- `write_file`: create or overwrite a file
- `run_python_file`: run a Python file and capture its output

## Run it

Requires Python 3 and [uv](https://docs.astral.sh/uv/).

```sh
echo 'GEMINI_API_KEY=your-key-here' > .env
uv run main.py "fix the bug in the calculator" --verbose
```

`--verbose` prints the full result of each function call.

`tests.py` runs a few manual checks of `run_python_file`, including a path outside the sandbox and a file that doesn't exist.
