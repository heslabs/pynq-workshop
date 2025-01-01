# Jupyter Notebooks

The material in this tutorial is specific to PYNQ.  Wherever possible, however, it re-uses generic documentation describing Jupyter notebooks.  

* What is the Jupyter Notebook?
* Notebook Basics
* Running Code
* Markdown Cells

The original notebooks and further example notebooks are available at [[Jupyter documentation]](http://jupyter-notebook.readthedocs.io/en/latest/examples/Notebook/examples_index.html).


---
## Introduction to Jupyter Notebooks 

* The Jupyter Notebook is an interactive computing environment that enables users to author notebook documents that include:
    * Live code
    * Interactive widgets
    * Plots
    * Narrative text
    * Equations
    * Images
    * Video
* These documents provide a complete and self-contained record of a computation that can be converted to various formats and shared with others electronically, using version control systems (like git/GitHub) or nbviewer.jupyter.org.

---
## Jupyter Notebooks - Components

### The notebook web application
* An interactive web application for writing and running code interactively and authoring notebook documents.

### Kernels
* Separate processes started by the notebook web application that runs users' code in a given language and returns output back to the notebook web application. 
* The kernel also handles things like computations for interactive widgets, tab completion and introspection.

### Notebook documents
* Self-contained documents that contain a representation of all content in the notebook web application, including inputs and outputs of the computations, narrative text, equations, images, and rich media representations of objects. 
* Each notebook document has its own kernel.

---
### Notebook web application
The notebook web application enables users to:
* Edit code in the browser, with automatic syntax highlighting, indentation, and tab completion/introspection.
R* un code from the browser, with the results of computations attached to the code which generated them.
* See the results of computations with rich media representations, such as HTML, LaTeX, PNG, SVG, PDF, etc.
* Create and use interactive JavaScript widgets, which bind interactive user interface controls and visualizations to reactive kernel side computations.
* Author narrative text using the Markdown markup language.
* Build hierarchical documents that are organized into sections with different levels of headings.
* Include mathematical equations using LaTeX syntax in Markdown, which are rendered in-browser by MathJax.

---
### Kernels
The Notebook supports a range of different programming languages. For each notebook that a user opens, the web application starts a kernel that runs the code for that notebook. There are kernels available in the following languages:
* Python https://github.com/ipython/ipython 
* Julia https://github.com/JuliaLang/IJulia.jl 
* R https://github.com/takluyver/IRkernel 
* Ruby https://github.com/minrk/iruby 
* Haskell https://github.com/gibiansky/IHaskell 
* Scala https://github.com/Bridgewater/scala-notebook 
* node.js https://gist.github.com/Carreau/4279371 
* Go https://github.com/takluyver/igo 

PYNQ is written in Python, which is the default kernel for Jupyter Notebook, and the only kernel installed for Jupyter Notebook in the PYNQ distribution.

---
### Notebook Documents
* Notebooks consist of a linear sequence of cells. There are four basic cell types:
  * Code cells: Input and output of live code that is run in the kernel
  * Markdown cells: Narrative text with embedded LaTeX equations
  * Heading cells: Deprecated. Headings are supported in Markdown cells
  * Raw cells: Unformatted text that is included, without modification, when notebooks are converted to different formats using nbconvert
* Notebooks can be exported to different static formats including HTML, reStructeredText, LaTeX, PDF, and slide shows (reveal.js) using Jupyter's nbconvert utility. 

---
### Notebook Dashboard
* The Notebook server runs on the Arm processor of the board.
  * You can open the notebook dashboard by navigating to pynq:9090 when your board is connected to the network.
* The dashboard serves as a home page for notebooks. 
  * By clicking on these breadcrumbs or on sub-directories in the notebook list, you can navigate your filesystem.
  * To create a new notebook, click on the "New" button at the top of the list and select a kernel from the dropdown
  * To shutdown, delete, duplicate, or rename a notebook: check the checkbox next to it and an array of controls will appear at the top of the notebook list.
  * To see all of your running notebooks along with their directories, click on the "Running" tab.

---
### Notebook UI
* If you create a new notebook or open an existing one, you will be taken to the notebook user interface (UI). The notebook UI has the following main areas:
   * Menu
   * Toolbar
   * Notebook area and cells
* Edit mode
   * Edit mode is indicated by a green cell border and a prompt showing in the editor area:
* Command mode
   * Command mode is indicated by a grey cell border with a blue left margin.
* Running Code
   * Run a code cell using Shift-Enter or pressing the play button in the toolbar above. 

---
### Markdown

* Text can be added to Jupyter Notebooks using Markdown cells. Markdown is a popular markup language that is a superset of HTML. Its specification can be found here:
   * http://daringfireball.net/projects/markdown/ 
* Markdown is a text-to-HTML conversion tool for web writers
   * Markdown allows you to write using an easy-to-read, easy-to-write plain text format, then convert it to structurally valid XHTML (or HTML).
* “Markdown” is two things
   * A plain text formatting syntax
   * A software tool, written in Perl, that converts the plain text formatting to HTML
   * See the Syntax page for details pertaining to Markdown’s formatting syntax.
* https://daringfireball.net/projects/markdown/ 

