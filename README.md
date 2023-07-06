<div align="center">
  <img src="https://github.com/JWock82/PyNite/raw/master/Resources/Full Logo No Buffer.png" width=40% align="center"/>
  <br>
  <h1>Simple Finite Element Analysis in Python</h1>
</div>

![Build Status](https://github.com/JWock82/PyNite/actions/workflows/build-and-test.yml/badge.svg)
![PyPI - Downloads](https://img.shields.io/pypi/dm/PyNiteFEA)
<img alt="GitHub code size in bytes" src="https://img.shields.io/github/languages/code-size/JWock82/PyNite">
![GitHub last commit](https://img.shields.io/github/last-commit/JWock82/PyNite)
![GitHub](https://img.shields.io/github/license/JWock82/PyNite)
[![Documentation Status](https://readthedocs.org/projects/pynite/badge/?version=latest)](https://pynite.readthedocs.io/en/latest/?badge=latest)

An easy to use elastic 3D structural engineering finite element analysis library for Python.

# Installation
The easiest way to install Pynite is with pip: `pip install PyniteFEA`

For a more detailed discussion on installation options and dependencies see https://pynite.readthedocs.io/en/latest/installation.html

# Current Capabilities
* 3D static analysis of elastic structures.
* P-&Delta; analysis of frame type structures.
* Member point loads, linearly varying distributed loads, and nodal loads are supported.
* Classify loads by load case and create load combinations from load cases.
* Produces shear, moment, and deflection results and diagrams for each member.
* Automatic handling of internal nodes on frame members (physical members).
* Tension-only and compression-only elements.
* Spring elements: two-way, tension-only, and compression-only.
* Spring supports: two-way and one-way.
* Quadrilateral plate elements (MITC4 formulation).
* Rectangular plate elements (12-term polynomial formulation).
* Basic meshing algorithms for some common shapes and for openings in rectangular walls.
* Reports support reactions.
* Rendering of model geometry, supports, load cases, load combinations, and deformed shapes.
* Generates PDF reports for models and model results.

# Project Objectives
As I've gotten into the structural engineering profession, I've found there's a need for an easy to use open-source finite element package. I hope to help fill that need by prioritizing the following:

1. Accuracy: There are no guarantees PyNite is error free, but accuracy and correctness are a priority. When bugs or errors are identified, top priority will be given to eliminate them. PyNite's code is frequently reviewed, and its output is tested against a suite of textbook problems with known solutions using continuous integration (CI) anytime a change to the code base is made. If you do happen to find an error, please report it as an issue.

2. Simplicity: There are other finite element alternatives out there with many more capabilities, but they are often lacking in documentation, written in difficult languages, or require extensive knowledge of finite element theory and/or element formulations to use. PyNite is not intended to be the most technically advanced solver out there. Rather, the goal is to provide a robust yet simple general purpose package.

4. Improvement: PyNite is getting better at what it does. Each new feature provides leverage to build upon previous features in more elaborate ways. Key to improvement is (a) maintaining the core features that other features rely on, and (b) adding new features that are solid stepping stones to other features. Improvement most often happens by getting the small and simple things right incrementally, rather than with sweeping overhauls all at once.

5. Collaboration: If you see a way to improve Pynite, you are encouraged to contribute. There are many simple ways to contribute that don't take much effort. Issue reports and pull requests can be very helpful. One easy way to contribute is to add to or improve the library of simple example problems in the `Examples` folder. Please keep them relatively simple. Most users learn Pynite from following these simple examples. Another way to help Pynite without having to know too much about its internal workings is to help with the documentation files in the `docs\source` folder of this repository. These files help new users learn Pynite. If you are able to make a bigger commitment, and would like to become a regular contributor to the project, please reach out about becoming a collaborator.

# Support
Whether you just need help getting started with PyNite, or are looking to build something more complex, there are a few resources available:
* The examples in the "Examples" folder in this repository cover a variety of simple problems. The comments in the examples provide additional guidance on how PyNite works.
* Documentation is a work in progress and can be found on readthedocs here: https://pynite.readthedocs.io/en/latest/index.html.
* If you're looking for more direct guidance on using PyNite, or for help coding a project, I am available on a private consulting basis. You can reach out to me directly at Building.Code@outlook.com to discuss options.

# Example Projects
Here's a list of projects that use PyNite:

* Building Code (https://building-code.herokuapp.com/) - This one is my personal side project.
* Standard Solver (https://www.standardsolver.com/)
* Civils.ai (https://civils.ai/1/free-3D-finite-element-structural-analysis)
* Phaenotyp (https://github.com/bewegende-Architektur/Phaenotyp) (https://youtu.be/shloSw9HjVI)

# What's New?
v0.0.76
* Simplified P-Delta convergence checks
* Allowed tension/compression-only support springs to reactivate after being deactivated. Erroneous deflections were being reported on very flexible models that experienced a lot of movement with T/C support springs.
* `matplotlib` is now an optional dependency. You'll only need to install it if you want to view plots for members.
* Documentation for installation has been improved.

v0.0.75
* Bug fix & improvements for PDF printing capabilities. Methods used to print PDF's had fallen behind updates to the rest of the program. It should be fixed now. The way PDF's are printed has changed slightly. Examples have been updated to demonstrate this and the documentation on readthedocs has been updated as well: (https://pynite.readthedocs.io/en/latest/reporting.html).

v0.0.74
* Bug fix for rectangular meshes with very close control points. The program now checks for mesh
control points that are for all practical purposes the same and eliminates the duplicates.

v0.0.73
* Bug fix for merging duplicated plate names when using models with multiple meshes.

v0.0.72
* Bug fix for point loads at the ends of physical members. These point loads were erroneously being applied at the end of all segments of the physical member. This error was introduced with the new physical member feature late last year. Prior to that this error did not exist.
* Improvements to plate meshing: (1) Rectangular meshes now automatically renumber nodes and elements to avoid duplicating names that are already in the model. This feature is only available for rectangular meshes at the moment. For other types of meshes you'll need to manually specify the start node and start element for numbering. (2) Meshes also now automatically stay in sync with the model. A node moved in the model will automatically reflect back on the mesh. Changes to elements in the model will automatically be reflected in the mesh. The program used to lose track of this. Once the mesh was generated it was "one and done" and no more.

v0.0.71
* WARNING: This version will require reworking your models to incorporate `Materials`. Be prepared to rework your models before you upgrade. The examples have all been updated to show you how to do this.
* Added `Material` definitions. This does not change Pynite's behavior much, but it prepares the way for future features.
* Greatly simplified the process of meshing plates/quads. Meshes can now be generated directly from the `FEModel3D` object.
* Added data types to the many dictionaries storing data in the `FEModel3D` object. Most development environments will now offer hints when using these dictionaries directly. This makes accessing the results you're interested in more intuitive.
* Simplified internal code for finding unique names for objects.

v0.0.70
* Array output of member force diagrams and displacement diagrams has been added.

v0.0.69
* Bug fix for rotational springs. Exceptions were being thrown due to an inconsistent variable name.
* Cleared out old branches from the repository that were no longer being used.
* Updated CI to check against python 3.10 and 3.11. Removed CI for python 3.6 as it's no longer supported by the latest version of github actions.
* Subtle changes to the logo to make it look a little more "pythonic".
* Bug fix for rendering screenshots. The ability to interact with the render window was being disabled after the first screenshot had been taken, forcing subsequent screenshots to use the same view as the first one.

v0.0.68
* Bug fix for member distributed loads on physical members. Added a unit test to check for this error going forward. This bug only affected physical members (new as of v0.0.67) that had distributed loads and internal nodes.

v0.0.67
* Added physical members. Members now automatically detect internal nodes and subdivide themselves and their loads.
* Refactoring: deprecated old method names for member results. You may now have some errors show up if you still try to get member results using the old method names.
* Bug fix for P-Delta analysis. Global displacements were correct, but member internal forces were neglecting the geometric stiffness matrix. The impact of this bug was minimal, since the strain induced by correct global displacements was still being considered prior to this update. You should see a slight change to member P-Delta results.
* Code simplification for P-Delta analysis.

v0.0.66
* Code simplification and bug fix for merging duplicate nodes.
* When nodes are merged, support conditions for the deleted node are now assigned to the remaining node.
* Added a linear solver for faster analysis of simple models. If you don't need P-Delta analysis or tension/compression-only analysis this solver saves time by only assembling the global stiffness matrix once.