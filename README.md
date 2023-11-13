# Usage
* Clone this repository to setup new LaTeX projects.
* Place your own content inside the ``src`` directory and adjust settings in ``latexmkrc`` according to your personal preferences. **Note**: If you're working on overleaf, move the root file of your project to the project root directory instead and adapt the configuration in ``latexmkrc`` according to the comments therein. Also make sure to change the LaTeX engine for your overleaf project to ``lualatex``.
* Compile your projects using ``latexmk`` on windows, macOS and linux. To force recompilation, use ``latexmk -g`` instead.
* Temporary artefacts are moved into ``tmp``, which is generated during compilation automatically.
* Output artefacts are moved to ``build``, which is generated during compilation automatically.
* Assuming you have not made severy changes to this project structure, you may safely delete directories ``build`` and ``tmp`` at any time without harming the project integrity. Hence, ``build`` and ``tmp`` should never be put under version control.

# Directory structure guidelines
* All source code should be placed  in ``src`` to keep the top-level project directory de-cluttered.
* Only notes and configuration files must reside in the top level project directory.
* Any lasting LaTeX setup should be put inside the package ``customizations.sty`` to ease reuse and declutter the root document.
* When using LaTeX packages ``tikz``, ``pgfplots``, ``bodeplot`` and similar, you should put any pictures in separate ``*.tikz`` files, to declutter code and possible speed up compilation by caching (see next point).
* The auxiliary package ``goodexternalize.sty`` is available for loading in your documents. ``goodexternalize.sty`` is a custom-written wrapper for the TeX macro ``\input``, which branches off inputting of ``tikz``-like graphics. Before ``tikz``-like graphics are input, the comand ``\tikzsetnextfilename`` is executed to replicate the directory structure under ``src`` into ``tmp`` when comiling, e.g. to input a file ``src/path/to/glory.tikz``, the document author must call ``\input{path/to/glory.tikz}`` or ``\input{src/path/to/glory.tikz}``, and all temporary artefacts concering the creation of ``glory.tikz`` will be stored under ``tmp/path/to/glory.log|.aux|...`` respectively. Keeping a synchronized structure tremendously helps with finding, updating and deleting parts of the cache.