# Coding Interview Patterns Playbook - Presentation

This repository contains the LaTeX source code and assets for generating the presentation slides of the course.

## Project Structure

- `presentaion/main.tex`: The main LaTeX entry point. It sets up the Beamer theme, packages, styling, metadata, and includes the individual section files.
- `presentaion/section1.tex` to `presentaion/section22.tex`: Individual files containing the slides for each module of the course.
- `presentaion/chart.tex`: TikZ diagram file included dynamically.
- `bigO.png`: External image asset used in the slides.
- `course.md`: The outline and syllabus of the course.

## Prerequisites

To build the presentation PDF, you need a TeX distribution (like **TeX Live** or **MacTeX** on macOS) installed on your system.

### 1. Engine requirement (LuaLaTeX)
The presentation uses the `emoji` package, which requires compiling with **LuaLaTeX** because it relies on native OpenType font loading (such as Apple Color Emoji on macOS).

### 2. Code Syntax Highlighting (Pygments)
The presentation uses the `minted` package for clean syntax highlighting of code examples. This package requires Python's Pygments library:
```bash
pip install Pygments
```

## How to Build the PDF

You can compile the project using `latexmk`, which automatically tracks files and compiles the document the correct number of times:

1. Navigate to the `presentaion` directory:
   ```bash
   cd presentaion
   ```
2. Compile using the LuaLaTeX engine and enabling shell-escape (required for `minted` to execute Pygments):
   ```bash
   latexmk -pdflua -shell-escape main.tex
   ```

If you prefer to compile directly without `latexmk`, you can run:
```bash
lualatex -shell-escape main.tex
```

## How to Modify the Presentation

- **Editing Slides**: Locate the file `presentaion/section[N].tex` corresponding to the section you want to edit and modify its Beamer frames.
- **Global Settings / Theme**: Edit `presentaion/main.tex` to change Beamer colors, fonts, default syntax styles, or package configurations.
- **Adding a New Section**:
  1. Create `presentaion/section[N].tex`.
  2. Reference it in `presentaion/main.tex` with `\input{section[N]}` before `\end{document}`.
