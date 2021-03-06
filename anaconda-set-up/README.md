## How to set up your own anaconda in a scientific way?

###### python2, python3, R in conda

### Introduction

* what is anaconda?

  - According to its own website, Anaconda is the leading open data science platform powered by Python. The open source version of Anaconda is a high performance distribution of Python and R and includes over 100 of the most popular Python, R and Scala packages for data science.
  - Or you can simply regard it as a manager of the packages of your programming languages.

* why we want to use anaconda?

  - Convinient to manage packages
  - Jupyter notebook
 
* object
  - Set up anaconda for a python and r user (linux)
  - I use py2 more often so I set it my default environment

### Get started!

1. Click this [link](https://www.continuum.io/downloads) and download corresponding version of anaconda. 

2. Type the following line in the terminal and the installation will be set up automatically

        ```bash Anaconda2-4.3.1-Linux-x86_64.sh``` . 

  Do include the "bash" command even if you are not using the bash shell.

3. Add the following line to the **.bashrc** or **.zshrc**(if you are a zsh user).

        ```export PATH="/home/zijun/anaconda2/bin:$PATH"```

4. Create python3 environment in your conda. 

        ```conda create -n py3 python=3.5 anaconda```

5. Create R environment in your conda.

        ```conda create -n r -c r r-essentials```
        
6. Install tck for R (enable install.packages() in R)

        ```source activate r
           conda install -c intel tcl=8.6.4```

7. Note1: if you want to remove environment you install:

        ```conda remove --name py3 --all```
        
8. Note2: switch different environment

        ```source activate r
           source deactivate r```


### Some issues you may encounter during the process

Q: tcl not found

> install.packages('highfrequency')  
--- Please select a CRAN mirror for use in this session ---
Error: .onLoad failed in loadNamespace() for 'tcltk', details:
call: fun(libname, pkgname)
error: Can't find a usable init.tcl in the following directories: 
/opt/anaconda1anaconda2anaconda3/lib/tcl8.5 ./lib/tcl8.5 ./lib/tcl8.5 ./library ./library ./tcl8.5.18/library ./tcl8.5.18/library

A: Solution:
- Just do the step 5 above to solve this problem.
- Or add the following lines to the .bashrc or .zshrc

       ``` export TCL_LIBRARY="/home/zijun/anaconda2/lib/tcl8.5"
           export TK_LIBRARY="/home/zijun/anaconda2/lib/tk8.5" ```

- Note1: tck is a package which supports install.packages() function and it is installed in the global environment if you use ```sudo apt-get install tcl8.5-dev tk8.5-dev``` and conda has no access to it. 
- Note2: packages will be installed in /home/zijun/anaconda/envs/r/lib/R/library using install.packages()
              
              
Q: How to install packages in R

A: Since we set up the tcl, we can easily use install.packages() or remove.packages() to manage the R packages. However in this way, conda will lose control over r packages. Also you may find some suggestions using conda-build like this:
  - switch back to the root environment
  - type ```conda install conda-build``` in the terminal
  - Use ```conda skeleton cran``` and ```conda build to install``` packages (you may mind the dependency issue)

However this will **not** give you the control either. Moreover, there might be more issues about shitty sytax in R. So my suggestion is simply using install.packages() in R to install your packages.

