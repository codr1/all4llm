# all4llm

A command-line tool that assembles multiple source code files (by recursively scanning directories among other ways) into a single string, in a format suitable to send to  Large Language Models (LLMs). It automatically:
- Combines multiple source files into a single string with clear demarcation between the sections representing each file.
- Supports direct clipboard copying for easy pasting into LLM chats
- Recursively scans directories to gather the files
- Handles common source code files by default
- Basic filtering for including / excluding files by extension
- Estimates token count for LLM context planning

## Installation

```bash
# Clone the repository
git clone https://github.com/codr1/all4llm.git
cd all4llm

# Make the script executable
chmod +x all4llm

# Optional: Add to your PATH
sudo ln -s $(pwd)/all4llm /usr/local/bin/all4llm

# For clipboard support on Linux:
sudo apt-get install xclip  # Ubuntu/Debian
sudo dnf install xclip      # Fedora
sudo pacman -S xclip        # Arch
# Note: macOS clipboard support works out of the box
```

## Usage

Basic syntax:
```bash
./all4llm [OPTIONS] DIRECTORY
```

### Common Use Cases

```bash
# View source files in current directory
./all4llm .

# Copy all source files to clipboard (for pasting into ChatGPT, etc.)
./all4llm . -c

# Process subdirectories recursively
./all4llm -r src/

# Save output to a file
./all4llm -r . -o project_code.txt

# Only include Python files
./all4llm . --only "*.py"

# Add custom file patterns
./all4llm . -i "*.conf" -i "*.cfg"
```

### Options

- `-h, --help`: Show help message
- `-r, --recursive`: Include subdirectories recursively
- `-i, --include PATTERN`: Include additional file pattern
- `-o, --output FILE`: Write output to file
- `-c, --clipboard`: Copy output to clipboard
- `--no-hidden`: Skip hidden files and directories
- `--list-defaults`: Show default file extensions
- `--only PATTERN`: Only include specified pattern (disables defaults)

### Default File Types

Automatically includes common source code files:
- C/C++: `.c`, `.h`, `.cpp`, `.hpp`, `.cc`
- Python: `.py`, `.pyw`
- JavaScript/TypeScript: `.js`, `.ts`, `.jsx`, `.tsx`
- Go: `.go`
- Java: `.java`
- Rust: `.rs`
- Ruby: `.rb`
- PHP: `.php`
- Documentation: `.md`, `.rst`
- Config files: `.json`, `.yaml`, `.yml`
- And more... (use `--list-defaults` to see all)

### Output Format

Files are marked in the output like this:
```
<<<< FILE: path/to/file.ext >>>>
[file contents]
<<<< END FILE: path/to/file.ext >>>>
```

The last line of output always shows an estimate of how many tokens the content will consume in your LLM context window.

### Tips
- Use `-c` for direct clipboard copy so you can easily interract with an LLM
- Token count helps you stay within LLM context limits
- Use `--only "*.ext"` to focus on specific file types
- Use `-r` when you need to include subdirectories
