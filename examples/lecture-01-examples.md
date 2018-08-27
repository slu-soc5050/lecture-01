Lecture 01 Notebook
================
Christopher Prener, Ph.D.
(August 27, 2018)

## Introduction

This is an [R Markdown](http://rmarkdown.rstudio.com) Notebook. When you
execute code within the notebook, the results appear beneath the code.
We’ll use notebooks throughout the semester for both demonstrating code
and for assignment submission.

Try executing this chunk by clicking the *Run* button within the chunk
or by placing your cursor inside it and pressing *Cmd+Shift+Enter*.

``` r
plot(cars)
```

![](lecture-01-examples_files/figure-gfm/test-chunk-1.png)<!-- -->

## Dependencies

This notebook requires a number of pre-installed packages, including
`base`, `datasets`, and `utils`. These packages are already installed
and loaded each time you open `R`. In addition, there are three packages
we discussed installing during class. We’ll use `install.packages()` to
install CRAN packages, and the `remotes` package to install packages
hosted on GitHub:

``` r
install.packages("cowsay")
install.packages("remotes")
remotes::install_github("chrisprener/testDriveR")
```

It is a best practice not to install packages in a notebook but rather
to install them interactively via the Console. This prevents you from
re-installing an updated version of the package each time you knit the
notebook, potentially breaking your code.

You should update packages when you are not in the middle of an
important project using:

``` r
update.packages()
```

You will have to type `y` or `Y` or `Yes` at each prompt. Packages
installed with `remotes` can be updated by re-executing the
`remotes::install_github()` function as needed.

With those packages installed, we’ll start by opening the one package
that we need immediately. The `library()` function is used to open all
packages:

``` r
library(cowsay)
```

You only need to install `R` packages once using `install.packages()` or
`remotes::install_github()`. At the beginning of each session /
notebook, however, you will have to load them using the `library()`
function. If you get the following error message, it means you need to
use the `library()` function to load the package that your function is
included in:

``` r
> mutate()
Error in mutate() : could not find function "mutate"
```

So, in this case, we would need to load the package that the `mutate()`
function is housed in.

## Load Data

After we load any dependencies we might need, our next task is going to
be to load the data that we need. For this class, that will generally
mean loading data from a package, though you may have to import a data
set from time to time.

Data will be imported into an “object” - a name in your “environment”
(essentially, in `R`’s memory) where it is held so that it can be
referenced later. For example, we could make an object named “prof” and
assign my name to it:

``` r
prof <- "Chris"
```

You should now see the `prof` object in the `Enviornment` tab in
RStudio\! We can enter an object name by itself in the console to print
its contents:

``` r
prof
```

    ## [1] "Chris"

We’ll do the same thing this time, except we’ll load some data from the
`datasets` package. The `datasets` package comes pre-installed with `R`
and contains a variety of fun and/or useful data sets. We’ll load some
data describing eruption intervals from the [Old Faithful
geyser](https://en.wikipedia.org/wiki/Old_Faithful):

``` r
geyser <- faithful
```

To explore the geyser data, we can use two functions. The first, `str()`
or “structure”, gives us a summary of its contents:

``` r
str(geyser)
```

    ## 'data.frame':    272 obs. of  2 variables:
    ##  $ eruptions: num  3.6 1.8 3.33 2.28 4.53 ...
    ##  $ waiting  : num  79 54 74 62 85 55 88 85 51 85 ...

We’ve got two variables - one named `eruptions` and one named `waiting`.

Next, we can use `View()` to open a spreadsheet like view of the data:

``` r
View(geyser)
```

You can also click on the geyser object in the `Enviornment` tab to open
up the same spreadsheet view of the data.

## Working with Functions

So far, all of the functions that we have used have taken a single
argument in the parentheses:

``` r
install.packages("cowsay")
install.packages("remotes")
remotes::install_github("chrisprener/testDriveR")
str(geyser)
View(geyser)
```

Function calls can be made more complex in two ways. First, functions
can be *nested* within each other. For instance, if we want to generate
a list of the animals included in `cowsay`, we could try to print the
`animals` object. It is quite messy, so I won’t do it in the notebook,
but you can try in the console if you’d like:

``` r
animals
```

To extract just the names, we can use the `names()` function:

``` r
names(animals)
```

    ##  [1] "cow"          "chicken"      "clippy"       "poop"        
    ##  [5] "bigcat"       "ant"          "pumpkin"      "ghost"       
    ##  [9] "spider"       "rabbit"       "pig"          "snowman"     
    ## [13] "frog"         "hypnotoad"    "shortcat"     "longcat"     
    ## [17] "fish"         "signbunny"    "facecat"      "behindcat"   
    ## [21] "stretchycat"  "anxiouscat"   "longtailcat"  "cat"         
    ## [25] "trilobite"    "shark"        "buffalo"      "grumpycat"   
    ## [29] "smallcat"     "yoda"         "mushroom"     "endlesshorse"
    ## [33] "bat"          "bat2"         "turkey"       "monkey"      
    ## [37] "daemon"       "egret"        "duckling"     "duck"        
    ## [41] "owl"

This is great, but it would be better if it were presented in
alphabetical order, so we’ll *wrap* the `names(animals)` function call
in the `sort()` function:

``` r
sort(names(animals))
```

    ##  [1] "ant"          "anxiouscat"   "bat"          "bat2"        
    ##  [5] "behindcat"    "bigcat"       "buffalo"      "cat"         
    ##  [9] "chicken"      "clippy"       "cow"          "daemon"      
    ## [13] "duck"         "duckling"     "egret"        "endlesshorse"
    ## [17] "facecat"      "fish"         "frog"         "ghost"       
    ## [21] "grumpycat"    "hypnotoad"    "longcat"      "longtailcat" 
    ## [25] "monkey"       "mushroom"     "owl"          "pig"         
    ## [29] "poop"         "pumpkin"      "rabbit"       "shark"       
    ## [33] "shortcat"     "signbunny"    "smallcat"     "snowman"     
    ## [37] "spider"       "stretchycat"  "trilobite"    "turkey"      
    ## [41] "yoda"

`R` functions are endlessly nestable, but you should do this with
caution - the more times you nest within a function, the harder it
becomes to read and de-bug\!

The second way we can extend functions is by specifying multiple
arguments:

``` r
say(what = "do or do not, there is no try", by = "yoda")
```

    ## 
    ## 
    ## 
    ##  ----- 
    ## do or do not, there is no try 
    ##  ------ 
    ##     \   
    ##      \
    ##                    ____
    ##                 _.' :  `._
    ##             .-.'`.  ;   .'`.-.
    ##    __      / : ___\ ;  /___ ; \      __
    ##   ,'_ ""--.:__;".-.";: :".-.":__;.--"" _`,
    ##   :' `.t""--.. '<@.`;_  ',@>` ..--""j.' `;
    ##        `:-.._J '-.-'L__ `-- ' L_..-;'
    ##           "-.__ ;  .-"  "-.  : __.-"
    ##              L ' /.------.\ ' J
    ##              "-.   "--"   .-"
    ##              __.l"-:_JL_;-";.__
    ##          .-j/'.;  ;""""  / .'\"-.
    ##          .' /:`. "-.:     .-" .';  `.
    ##       .-"  / ;  "-. "-..-" .-"  :    "-.
    ##   .+"-.  : :      "-.__.-"      ;-._   \
    ##   ; \  `.; ;                    : : "+. ;
    ##   :  ;   ; ;                    : ;  : \:
    ##   ;  :   ; :                    ;:   ;  :
    ##   : \  ;  :  ;                  : ;  /  ::
    ##   ;  ; :   ; :                  ;   :   ;:
    ##   :  :  ;  :  ;                : :  ;  : ;
    ##   ;\    :   ; :                ; ;     ; ;
    ##   : `."-;   :  ;              :  ;    /  ;
    ##  ;    -:   ; :              ;  : .-"   :
    ##   :\     \  :  ;            : \.-"      :
    ##   ;`.    \  ; :            ;.'_..--  / ;
    ##   :  "-.  "-:  ;          :/."      .'  :
    ##    \         \ :          ;/  __        :
    ##     \       .-`.\        /t-""  ":-+.   :
    ##      `.  .-"    `l    __/ /`. :  ; ; \  ;
    ##        \   .-" .-"-.-"  .' .'j \  /   ;/
    ##         \ / .-"   /.     .'.' ;_:'    ;
    ##   :-""-.`./-.'     /    `.___.'
    ##                \ `t  ._  /  bug
    ##                 "-.t-._:'
    ## 

Parameters like `what` and `by` give a function specific pieces of
information. Always name the parameters - it makes your function easier
to debug and more explicit\!

## Getting Help

If you want to get help from within `R`, there are two easy way to bring
up documentation files in the `Help` tab in the lower right-hand corner.
The first is the single question mark, which can be used with a package
name:

``` r
?base
```

The single question mark can also be used with a function name:

``` r
?install.packages
```

If you don’t find what you need, or a package/function does not have
help files created for you, you can use the double question mark
operator to search for additional resources:

``` r
??cowsay
```

## `R` Projects and Working Directories

RProjects are a special type of file associated with RStudio. They
create self-contained directories and environments that increase the
reproducibility of your work. They also take care of managing the
working directory for you. The working directory is an often difficult
to grasp concept at first. Think of it as a postal address - this is
where `R` will expect all information to come from and go to about a
project. You can view the current working directory with
    `getwd()`:

``` r
getwd()
```

    ## [1] "/Users/chris/GitHub/SOC5050/LectureRepos/lecture-01/examples"

There are ways to set the working directory in the console, but we want
to avoid them at all costs. Anytime we use an RProject, it will set the
working directory automatically. To create a new RProject, go to `File >
New > Project...`. You’ll have the ability to associate your project
with a new folder or with an existing folder. For this class, you’ll
generally want to associate it with an existing folder\!
