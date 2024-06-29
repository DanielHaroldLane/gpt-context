# gpt-context

https://github.com/DanielHaroldLane/gpt-context/assets/20723724/0e9519af-f1ef-46b7-ac85-54721729489f

https://github.com/DanielHaroldLane/gpt-context/assets/20723724/cdf5fbbd-2cef-4112-b55a-c228d6f170ed



## Description/Purpose

The purpose of this shell script is to allow developers to bundle up git repositories of code into a format that is easy for Chat GPT to understand and parse. This enables a developer to upload their repository in plain text and then ask GPT questions about the code, structure, tooling, etc in the repository. There is no need for an OpenAI key to do this and the output file can be used with any LLM, it isn't restricted to Chat GPT.

`gpt-context` is git aware, it will read and parse a .gitignore file and deliberately ignore those files if they exist in the git repository and exclude them from the generated context.

## Compatability

gpt-context is compatible with any POSIX compliant shell for portability. It can be used with macOS, Linux and WSL (Windows Subsystem for Linux)

## Prerequisites

These are almost certainly available on your system out of the box.

- awk
- sed
- find

## Setup

It's necessary to copy the script somewhere that is on your path as defined in your shell of choice. 

`cd` to the directory that contains `gpt-context` e.g. `cd ~/Downloads`, make the script executable and then move it to somewhere on your path.

```
mkdir ~/bin
chmod +x ~/bin/gpt-context
mv gpt-context ~/bin/gpt-context
```

If ~/bin is not on your path, you can update your path by adding the following line to your shell profile.

```
export PATH="$HOME/bin:$PATH"
```
Now, after sourcing your shell profile, e.g. `source ~/zshrc` or `source ~/bashrc` the `gpt-context` command can be executed from any directory.

## Usage

Usage: $0 [--help] [--version] [--input PATH] [--output OUTPUT]
  Defaults input and output to the current directory if not provided.
  --help         Show this help message
  --version      Show version information
  --input  PATH  Git repository path
  --output OUTPUT The path for the output (defaults to gpt_context.txt)

Example commands:

```
# Change directory to a git repository, I'm using my AlertR project from Github
~ cd AlertR
~ gpt-context
Generating GPT Context for GIT repository: ./
GPT Context saved to: gpt_context.txt
```

Alternatively, if you do not wish to have your current working directory as the root of a git repository a path can be provided to gpt-context. `gpt-context` will then create a `gpt_context.txt` file in your current working directory based on the path provided to the `--input` argument.
The `--output` argument is used to specify an output file name that will be written to the current directory.

```
# change directory to home
cd ~
~ gpt-context --input ./personal-projects/AlertR --output alertr-context.txt
Generating GPT Context for GIT repository: ./personal-projects/AlertR
GPT Context saved to: /home/USER/alertr-context.txt
```

Once you have a generated context file it can be uploaded to Chat GPT or fed into any other LLM as part of the prompt to provide the LLM context. After this, the LLM can be asked questions about your code.


