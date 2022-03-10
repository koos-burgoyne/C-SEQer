# C-Seqer
A C++11 rewrite of the Python SweetSEQer algorithm.

This work is a derivative of the original SweetSEQer algorithm licensed to Oliver Serang (2012):
  https://pubmed.ncbi.nlm.nih.gov/23443135/

## Requirements:
* Docker (if running the container)
* Python 2.7 (for plotting)
  * Matplotlib 1.5.3
  * NetworkX 1.1
  * Numpy 1.16.6
### Linux
  * g++ 9.3.0 compiler
  * gnu plot 5.2 patchlevel 8  
  * (If running in Ubuntu bash shell for Windows 10) Xming server 6.9.0.31 for display of charts
### Windows
  * MinGW compiler for C and C++
  
## Compiling
C-SEQer uses the [Cmake](https://cmake.org/install/) build system which makes compilation from source straightforward.

### Cmake
1. Generate the Makefile (this will appear in the `build/` directory):
<br>&nbsp;&nbsp;&nbsp;&nbsp;`cmake .`
2. Build the executable by executing from the build directory:
<br>&nbsp;&nbsp;&nbsp;&nbsp;Linux: &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`make Makefile`
<br>&nbsp;&nbsp;&nbsp;&nbsp;Windows: `mingw32-make -f Makefile`

### From Source
If compiling from source, navigate to the `src/` directory with the following files:
  * C-SEQER.cpp
  * MGF.hpp
  * main_functions.hpp
  * DeNovo.hpp
  * DiGraph.hpp
  * dictionary.hpp
  * (plot_glycan.py is only required when running the executable and passing in a positive print argument)

Execute `g++ C-SEQER.cpp -o c-seqer.exe`

## Run:
 Required files:
* executable
* .mgf file
* plot_glycan.py if plotting .png format figures

Example of execution command with parameters:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;./c-seqer.exe 0.01 0.01 1 1 500 1 1 120810_JF_HNU142_5.mgf

### Parameters
Run the executable with 8 parameters:
1. **epsilon**: &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; maximum absolute error between predicted and actual peak (in m/z)
2. **lambda**: &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; minimum peak intensity (relative to maximum peak intensity)
3. **p**: &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; minimum length of inferred peptide sequence
4. **g**: &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; minimum size of inferred glycan graph (including isotope peaks, not shown in graph)
5. **tau**: &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; minimum m/z value to include in glycan
6. **print output**: either 0 (doesn't print text results) or 1 (prints text results for matches)
7. **plot results**: &nbsp; either 0 (doesn't plot results) or 1 (interactively plots each matching spectrum
8. **MGF file**: &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; paths to an MGF files to process

## Output
  1. One .txt file with title of format `<MGf file Name>_<epsilon>Da<lambda>int<g>g.txt`
      * Contains a single line per valid spectrum (any spectrum containing glycan fragments meeting the user set p and g parameters) that is contained in the .mgf file, with the following data:
          * Spectrum charge
          * spectrum pepMass
          * spectrum rtInSeconds
          * charge state of spectrum for described fragment
          * start node of fragment
          * end node of fragment
  
2. Two .png files with the spectrum name as image title:
    1. one for the annotated spectrum
    2. another for the glycan graph
