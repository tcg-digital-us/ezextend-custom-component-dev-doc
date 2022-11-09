# ezextend-custom-component-dev-doc
Documentation on how to create custom dashboard visualization components

The current pdf build of the manual exists [here](build/pdf/latex/ezextenddevelopmentmanual.pdf)

## Install Dependencies

### Sphinx

To develop the documentation, you must use [Sphinx](https://www.sphinx-doc.org/en/master/).

```
$ sudo apt-get install python3-sphinx
```

### Sphinx Dependencies

Below are listed the dependencies for the Sphinx project and the commands to install them:

- Sphinx Read The Docs theme
  - Install:
    ```
    $ pip install sphinx_rtd_theme
    ```

- Sphinx-Panels
  - Purpose: To add drop-down accordian functionality
  - Install:
    ```
    $ pip install sphinx-panels
    ```

### Latex

To be able to build latex-based .pdf's with Sphinx, you will need to install some packages:

```
$ sudo apt-get install latexmk texlive-latex-recommended texlive-latex-extra texlive-fonts-recommended 
```

> If running Sphinx 1.6 or above on GNU/Linux or OSX, you may also need the latexmk package.

## Build

### For web
```
$ cd <repository folder>
$ sphinx-build -b html src build/web
```

### For PDF

```
$ cd <repository folder>
$ sphinx-build -M latexpdf src build/web
```