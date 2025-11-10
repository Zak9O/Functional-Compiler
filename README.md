# Functional Compiler for GCL

A comprehensive compiler toolchain written in F# for the Guarded Command Language (GCL), featuring parsing, compilation, interpretation, and static analysis capabilities.

## Overview

This project implements a complete compiler and analysis framework for a variant of the Guarded Command Language (GCL). The toolchain includes multiple components that work together to parse, compile, execute, and analyze GCL programs. It was developed as part of the 02141 Computer Science Modelling course at DTU.

### What is GCL?

The Guarded Command Language is a programming language developed by Edsger Dijkstra for writing structured programs with non-deterministic control flow. This implementation supports a variant of GCL with features including:

- Variable assignments and array operations
- Conditional statements (`if-fi`)
- Loop statements (`do-od`)
- Guarded commands with non-deterministic choice
- Arithmetic and boolean expressions

For the complete language specification, see [gcl.md](gcl.md).

## Features

The compiler toolchain consists of several integrated components:

### 🔍 **Parser** (Task 1)
- Lexical analysis and syntax parsing for GCL programs
- Abstract Syntax Tree (AST) generation
- Pretty printer for formatted code output
- Syntax error detection and reporting

### ⚙️ **Compiler** (Task 2)
- Converts GCL programs to Program Graphs (PG)
- Supports both deterministic and non-deterministic semantics
- Outputs in DOT format for visualization
- Program graph construction following formal methods

### ▶️ **Interpreter** (Task 3)
- Step-by-step program execution
- Trace generation with complete execution sequences
- Memory state tracking
- Support for deterministic and non-deterministic execution

### 🔒 **Security Analysis** (Task 5)
- Information flow analysis
- Detection of confidential information leaks
- Security property verification

### 🔢 **Sign Analysis** (Task 6)
- Static analysis determining variable signs at program points
- Detection of potential runtime errors (e.g., division by zero)
- Abstract interpretation framework

### 🧮 **Calculator**
- Simple arithmetic expression evaluator
- Demonstrates basic parsing and evaluation techniques

## Project Structure

```
.
├── code/                  # Main source code directory
│   ├── src/
│   │   ├── AST.fs        # Abstract Syntax Tree definitions
│   │   ├── Parser.fs     # Parser implementation
│   │   ├── Lexer.fsl     # Lexer specification
│   │   ├── Grammar.fsy   # Grammar specification
│   │   ├── Compiler.fs   # Compiler to Program Graphs
│   │   ├── Interpreter.fs # Program interpreter
│   │   ├── SecurityAnalysis.fs # Security analysis
│   │   ├── SignAnalysis.fs     # Sign analysis
│   │   ├── Calculator.fs # Arithmetic calculator
│   │   ├── Types.fs      # Shared type definitions
│   │   ├── Io.fs         # Input/output types
│   │   └── Program.fs    # Entry point
│   └── gcl.fsproj        # F# project file
├── gcl.md                # GCL language specification
├── overview.png          # Architecture diagram
└── README.md             # This file
```

## Getting Started

### Prerequisites

- **.NET 8.0 SDK** or later
  - **Windows**: [Download from Microsoft](https://dotnet.microsoft.com/en-us/download)
  - **macOS**: Install via Homebrew: `brew install dotnet-sdk`
  - **Linux**: [Installation guide](https://fsharp.org/use/linux/)

Verify installation:
```bash
dotnet --version  # Should show 8.x.x
```

### Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd Functional-Compiler
```

2. Build the project:
```bash
cd code
dotnet build
```

### Running the Compiler

The compiler provides several commands for different analyses:

```bash
# Parse a GCL program
dotnet run Parser '<input-json>'

# Compile to program graph
dotnet run Compiler '<input-json>'

# Interpret a program
dotnet run Interpreter '<input-json>'

# Run sign analysis
dotnet run Sign '<input-json>'

# Run security analysis
dotnet run Security '<input-json>'

# Evaluate arithmetic expressions
dotnet run Calculator '<input-json>'
```

### Using Inspectify (Recommended)

The easiest way to interact with the compiler is through **Inspectify**, a web-based interface:

```bash
# Windows
.\inspectify.ps1 --open

# macOS/Linux
./inspectify.sh --open
```

This will open a browser at `http://localhost:3000/` where you can:
- Write and parse GCL programs
- Visualize program graphs
- Execute programs step-by-step
- Run analyses interactively
- Compare with reference implementations

## Example Programs

Here's a simple GCL program that computes the maximum of two numbers:

```gcl
if x >= y -> z := x
[] y >= x -> z := y
fi
```

This program uses guarded commands to non-deterministically choose the maximum value.

## Development

### Building from Source

```bash
cd code
dotnet restore  # Restore dependencies
dotnet build    # Compile the project
```

### File Types

- **`.fs`** - F# source files
- **`.fsl`** - FsLex lexer specifications
- **`.fsy`** - FsYacc parser grammar specifications
- **`.fsproj`** - F# project configuration

### Key Technologies

- **F#** - Primary programming language
- **FsLexYacc** - Lexer and parser generator
- **.NET 8.0** - Runtime platform
- **System.Text.Json** - JSON serialization

## Architecture

The compiler follows a traditional multi-phase architecture:

```
Source Code (GCL)
      ↓
  [Lexer] → Tokens
      ↓
  [Parser] → Abstract Syntax Tree
      ↓
  [Compiler] → Program Graph
      ↓
  [Interpreter/Analyzer] → Results
```

Each component is modular and can be used independently or as part of the complete toolchain.

## Documentation

- **[gcl.md](gcl.md)** - Complete GCL language specification
- **[code/README.md](code/README.md)** - Detailed build and development guide
- **[ASSIGNMENT.md](ASSIGNMENT.md)** - Original assignment instructions
- **Task files** (`task1.md` - `task7.md`) - Individual component specifications

## Learning Resources

This project demonstrates several computer science concepts:

- **Compiler Construction**: Lexing, parsing, code generation
- **Formal Methods**: Program graphs, operational semantics
- **Static Analysis**: Abstract interpretation, data flow analysis
- **Programming Languages**: Language design, semantics
- **Functional Programming**: Type systems, pattern matching, immutability

## Contributing

This project was developed as an educational assignment. The codebase follows functional programming principles and F# best practices.

### Code Structure Guidelines

- Type definitions in `AST.fs` and `Types.fs`
- Each analysis in its own module
- Pure functional implementations preferred
- Pattern matching for AST traversal

## License

Educational project for DTU Course 02141 - Computer Science Modelling.

## Acknowledgments

- Based on concepts from [FM4Fun](http://www.formalmethods.dk/fm4fun)
- Implements techniques from formal methods literature
- Developed for DTU's Computer Science Modelling course

## Contact

For questions about this project, please refer to the course materials or contact the course instructors.
