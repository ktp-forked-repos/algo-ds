# TI3110TU - Algorithms and Data Structures

Source code for the lecture notes for the TU Delft Algorithms and Data Structures (TI3110TU) minor course. The course language is Python. The course was given in the academic year 2017 -- 2018.

## Dependencies

The course materials are prepared using [RMarkdown](https://rmarkdown.rstudio.com).

On MacOSX, with [Homebrew](https://brew.sh) installed, you need to install
the following dependencies to get going.

```bash
# Install R
brew tap homebrew/science
brew install Caskroom/cask/xquartz
brew install r

# Install rmarkdown and other related dependencies
R --no-save < deps.R

# Install pandoc
brew install pandoc pandoc-citeproc

# Install jupyter
pip install jupyter

# Install TexLive / MacTex (for PDF exports)
wget http://tug.org/cgi-bin/mactex-download/MacTeX.pkg
open MacTeX.pkg
```

## Building the contents

The repository uses a Makefile to drive the compilation process

* `make html` builds an HTML version of all contents, suitable for reading
  online
* `make pdf` builds an PDF version of all contents, suitable for printing
* `make slides` builds an Reveal.js version of the slides, suitable for
  presentations

In addition

* `make exams` Builds PDF versions of the contents of the `exams` dir
* `make book` Builds a book version (aggregated PDF/HTML with all contents) of the
  contents (not perfect yet).

## Repository contents

* `lectures`: contains the source for the course lectures
* `assignments`: source and solutions (in Python) for the course's assignments
* `exams`: exam material
* `livecoding`: Jupyter notebooks I created while teaching in the classroom

## Contributors

The following people contributed to the course's contents:

* [Joseph Hejderup](https://github.com/jhejderup)
* [Maria Kechagia](https://github.com/mkechagia)
* [Mozhan Soltani](https://github.com/Mozhan)
* [Pavel Kucherbaev](https://github.com/pavelk2)

## License

The course contents are copyrighted by TU Delft and their respective authors and
distributed under the [CC BY-NC-SA 4.0 license](https://creativecommons.org/licenses/by-nc-sa/4.0/)
