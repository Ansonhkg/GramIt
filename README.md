# 🚀 GramIt 📸📝

GramIt is a powerful Rust-based tool that combines and visualizes your code files, creating instant PlantUML diagrams for easy understanding and documentation of your project structure.

## 🌟 Features

- 📁 Combine multiple source files into a single output
- 🗂️ Support for multiple file extensions
- 🔍 Customizable ignore patterns with support for multiple patterns
- 📊 Automatic PlantUML diagram generation with customizable output
- 📏 Line limit option for large codebases
- 🚫 Optional exclusion of import and export statements
- ⚙️ Configuration file support for easy setup and multiple runs
- 🎨 Custom PlantUML instructions support for advanced diagram customization

## 🛠 Installation

```
curl -L -o gramit https://github.com/Ansonhkg/gramit/releases/download/1.1.0/gramit
```

## 🚀 Usage

You can run gramit either using command-line arguments or a configuration file.

### Command-line Usage

Run gramit with the following command:

```bash
gramit [OPTIONS]
```

#### Options

- `--help`: Display the help message
- `--path=<directory>`: Specify a source directory (can be used multiple times)
- `--output=<file>`: Specify the output file path
- `--ext=<extensions>`: Comma-separated list of file extensions to process (default: rs)
- `--ignore=<pattern>`: Custom glob pattern for files to ignore (can be used multiple times)
- `--max-lines=<number>`: Maximum number of lines per output file (enables pagination)
- `--ignore-imports=<bool>`: Whether to ignore import statements (default: true)
- `--ignore-exports=<bool>`: Whether to ignore export statements (default: true)
- `--auto-generate`: Automatically generate PlantUML diagram without prompt
- `--plantuml-dir=<directory>`: Specify the output directory for PlantUML diagrams
- `--plantuml-filename=<name>`: Specify the filename for PlantUML diagrams (without extension)
- `--plantuml-no-timestamp`: Exclude timestamp from PlantUML diagram filename

#### Examples

1. Basic usage:

   ```bash
   gramit --path=/project/src --output=./combined_code.txt
   ```

2. Multiple directories with custom extensions and ignore patterns:

   ```bash
   gramit --path=/project/src --path=/project/tests --output=./combined.rs --ext=rs,py --ignore=*.tmp --ignore=**/node_modules/**
   ```

3. Customize PlantUML output:
   ```bash
   gramit --path=/project --output=./combined_code.txt --plantuml-dir=./diagrams --plantuml-filename=project_structure --plantuml-no-timestamp
   ```

### Configuration File Usage

Create a file named `gramit.config.json` in the same directory as the executable. The file should contain an array of configuration objects:

```json
[
  {
    "source_dirs": ["./src", "./tests"],
    "output_file": "./output/combined_1.txt",
    "file_extensions": ["rs", "toml"],
    "custom_ignore_patterns": ["*.tmp", "**/node_modules/**"],
    "max_lines_per_file": 1000,
    "auto_generate_diagram": true,
    "plantuml_output_dir": "./diagrams",
    "plantuml_output_filename": "project_structure",
    "plantuml_include_timestamp": true,
    "plantuml_custom_instructions": "!theme bluegray\n!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Context.puml"
  },
  {
    "source_dirs": ["./docs"],
    "output_file": "./output/combined_docs.txt",
    "file_extensions": ["md", "txt"],
    "ignore_imports": false,
    "ignore_exports": false,
    "auto_generate_diagram": false
  }
]
```

When a configuration file is present, gramit will process each configuration sequentially.

## 📊 Output

gramit generates:

1. A combined text file containing the processed code
2. A PlantUML diagram (PNG format) visualizing the code structure

The locations of these files will be displayed in the console output.

## 🎨 Custom PlantUML Instructions

You can add custom PlantUML instructions to your diagrams by using the `plantuml_custom_instructions` field in your configuration file. This allows you to add any other PlantUML-specific instructions that should apply to the entire diagram.

Example:

```json
"plantuml_custom_instructions": "Explain like im 5"
```
