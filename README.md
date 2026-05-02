# Text Editor (NASM x86_64)

This project is a small assembly-language program that:

1. Opens a text file passed as the first CLI argument.
2. Reads up to a configurable buffer size from the file.
3. Prints the file content to stdout.
4. Reads additional input from stdin.
5. Appends the input to the original buffer and writes the result back to the same file.

> Source file: `Text Editor`

## Prerequisites

- Linux (tested with GNU/Linux tooling)
- `nasm`
- `ld` (from `binutils`)

Install dependencies on Debian/Ubuntu:

```bash
sudo apt update
sudo apt install -y nasm binutils
```

## Build

```bash
nasm -f elf64 -o text_editor.o "Text Editor"
ld -o text_editor text_editor.o
```

## Run

1. Create a test file:

```bash
echo "Initial content;" > sample.txt
```

2. Run the program with the file path as first argument:

```bash
./text_editor sample.txt
```

3. Type text in stdin and press `Ctrl+D` to finish input.

The program prints what it reads and updates `sample.txt` with appended content.

## Notes

- The program currently uses Linux syscalls directly (`sys_open`, `sys_read`, `sys_write`, `sys_close`, `sys_exit`).
- The read and working buffers are controlled by `BUFFER_SIZE` in the source file.
- The file path comes from `argv[1]`; if omitted, behavior is undefined.

## Quick start (clone to run)

```bash
git clone <repo-url>
cd Text_editor_assembly
nasm -f elf64 -o text_editor.o "Text Editor"
ld -o text_editor text_editor.o
echo "Initial content;" > sample.txt
./text_editor sample.txt
```
