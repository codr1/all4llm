# all4llm

A command-line tool that assembles source code files into a single output with clear file demarcation, making it easy to feed your codebase into Large Language Models (LLMs) for analysis, refactoring, or documentation.

## Installation

```bash
# Clone the repository
git clone https://github.com/codr1/all4llm.git
cd all4llm

# Make the script executable
chmod +x all4llm

# Optional: Add to your PATH
sudo ln -s $(pwd)/all4llm /usr/local/bin/all4llm
```

## Usage

Basic syntax:
```bash
./all4llm [OPTIONS] DIRECTORY
```

### Common Use Cases

```bash
# Assemble all source files in current directory
./all4llm .

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
- `-o, --output FILE`: Write output to file instead of stdout
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

This format makes it easy for LLMs to understand file boundaries and locations when processing your code.
