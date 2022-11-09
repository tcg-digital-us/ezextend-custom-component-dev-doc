# ezextend-custom-component-dev-doc
Documentation on how to create custom dashboard visualization components

To develop the documentation, you must use [Sphinx](https://www.sphinx-doc.org/en/master/).

## Install Dependencies
Below are listed the dependencies and the commands to install them:

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
  

## Build for web
```
$ cd <repository folder>
$ sphinx-build -b html src build/web
```

## Build for PDF

*TODO*