# Geometry Processing Research in Python

This is a Python tutorial for basic geometry processing in Python.
In this tutorial, you will learn a quick way to get started doing geometry
processing research in Python using the [Gpytoolbox](https://gpytoolbox.org) and
[Polyscope](https://polyscope.run) libraries.

This is a very basic introduction to get newcomers started within a
few hours into my preferred style of geometry processing coding and
prototyping - this is not a thorough introduction into computer graphics,
differential geometry, or numerical mathematics.

You will not learn any particular methods or algorithms here.
The goal is to
teach you how to quickly load and display meshes in Python, how to compute and
display basic properties of meshes, how to do simple creation and manipulation
tasks, and how to write your own methods on the basis of Gpytoolbox methods.
*This tutorial will give you the tools to write your own methods.*

This tutorial accompanies an [SGP 2024 graduate school](https://sgp2024.github.io/program/) course.
Click on the image below to see the lecture.

[![SGP course recording](https://img.youtube.com/vi/wQU9H4lp21k/0.jpg)](https://www.youtube.com/watch?v=wQU9H4lp21k)

## How this tutorial works

This repository contains multiple sequentally numbered exercises that are
meant to be completed sequentally, starting with [exercise 00](exercise_00/).
Feel free to skip any one of them if you are already familiar with the
concepts.

The tutorial assumes that you are already pretty familiar with Python and
NumPy - they are required prerequisites for this tutorial.

*This tutorial uses Python 3.10.*

The full list of exercises is:
- [00 Setting up a Python environment](exercise_00/)
- [01 NumPy for geometry processing](exercise_01/)
- [02 Creating, reading, and writing meshes](exercise_02/)
- [03 Visualizing geometry](exercise_03/)
- [04 Shading and perspective](exercise_04/)
- [05 Basic properties of surfaces](exercise_05/)
- [06 Edges, halfedges and adjacency](exercise_06/)
- [07 Randomness](exercise_07/)
- [08 Finite element matrices](exercise_08/)
- [09 Optimization](exercise_09/)
- [10 Subdivision and decimation](exercise_10/)
<!-- FUTURE TODOS: -->
<!-- - [11 Signed distance functions](exercise_11/) -->
<!-- - [12 Mesh booleans](exercise_12/) -->

Have fun!

## FAQ

### What is the difference between Gpytoolbox and libigl?

This question was asked during the SGP course, so I want to answer it explicitly
here.

Both [Gpytoolbox](https://gpytoolbox.org) and [libigl](https://libigl.github.io)
are geometry processing libraries with Python interfaces.
Libigl is a more extensive and more established geometry processing library with
a `C++` core and Python bindings to that `C++` code.
You should use libigl, it is great!
In fact, quite a few Gpytoolbox functions are based on libigl functions or wrap
libigl in some way.

Gpytoolbox is a smaller library with functions mostly written in Python that is
great for research code specifically.
It is geared towards geometry processing researchers, is easy to use, with
well-documented code that is ready for you to use in your projects immediately.


## Citation

If you want to cite this course, use the following BibTeX:
```
@inproceedings{Stein2024GeometryProcessing,
    author = {Stein, Oded},
    booktitle = {SGP 2024 Graduate School Courses},
    title = {Geometry Processing Research in Python},
    year = {2024}}
```

## Acknowledgements

This tutorial and Gpytoolbox would have not been possible without the help
of [Silvia Sellán](https://www.silviasellan.com).
The entire graphics community owes great thanks to
[Nick Sharp](https://nmwsharp.com), the creator of Polyscope, for his useful
software and extremely friendly support.

Thanks to Daniella Levy and Zoë Marschner for debugging the exercises.

## License

This tutorial is licensed under the [CC BY 4.0 license](LICENSE.txt).


---

_Oded Stein 2024. [Geometry Processing Research in Python](https://github.com/odedstein/geometry-processing-research-in-python)_
