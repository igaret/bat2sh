# cmd2sh / bat2sh

A utility to convert Windows batch files (.cmd/.bat) to POSIX-compliant shell scripts (.sh).

## Features

- Converts Windows batch file syntax to shell script syntax
- Handles common batch commands like `if`, `for`, `set`, `echo`, etc.
- Converts variable syntax from `%var%` to `${var}`
- Handles array operations
- Converts `findstr` to `grep`
- Handles `errorlevel` checks
- Converts comments
- Preserves code structure and indentation

## Installation

1. Clone this repository or download the script
2. Make the script executable:
   ```
   chmod +x cmd2sh.py
   ```
3. Optionally, create symbolic links:
   ```
   ln -s cmd2sh.py cmd2sh
   ln -s cmd2sh.py bat2sh
   ```

## Usage

```
./cmd2sh input.bat [options]
```

or

```
./bat2sh input.cmd [options]
```

### Options

- `-o, --output FILE`: Specify output file (default: input file with .sh extension)
- `-f, --force`: Overwrite output file if it exists

## Examples

### Basic Usage

```
./cmd2sh script.bat
```

This will create `script.sh` in the same directory.

### Specifying Output File

```
./cmd2sh script.bat -o converted_script.sh
```

### Forcing Overwrite

```
./cmd2sh script.bat -f
```

## Supported Conversions

| Batch Command | Shell Equivalent |
|---------------|------------------|
| `echo text` | `echo text` |
| `set var=value` | `var=value` |
| `set /a var=expr` | `var=$(( expr ))` |
| `if condition (commands)` | `if [ condition ]; then commands; fi` |
| `if condition (cmds) else (cmds)` | `if [ condition ]; then cmds; else cmds; fi` |
| `for %%i in (items) do (cmds)` | `for i in items; do cmds; done` |
| `for /f "options" %%i in (source) do (cmds)` | `cat source \| while read -r i; do cmds; done` |
| `rem comment` | `# comment` |
| `findstr pattern` | `grep pattern` |
| `errorlevel` | `$?` |
| `%var%` | `${var}` |
| `array[index]=value` | `array[index]=value` |

## Limitations

- Complex batch scripts with goto statements may not convert perfectly
- Some advanced batch features might require manual adjustment
- Windows-specific commands will need to be replaced manually

## License

This script is provided under the MIT License.