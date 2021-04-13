# ![ubcdown](/Images/ubc_logo.png)

This repository provides a template for writing a PhD dissertation in R Markdown, and rendering those files into a PDF formatted according to [the requirements of the Faculty of Graduate and Postdoctoral Studies of the University of British Columbia](https://www.grad.ubc.ca/current-students/dissertation-thesis-preparation). It follows the 2021 requirements to convert R Markdown files into a PDF formatted ready for submission at UBC. This project has drawn directly on code and ideas from Dan Ovand's [gauchodown](https://github.com/DanOvando/gauchodown), with  the modifications needed to deal with UBC's G+PS requirements. However, unlike [gouchodown](https://github.com/DanOvando/gauchodown), this is not a package but a repository that you download and modify with your information. In addition, this repository was possible thanks to:

-[huskydown](https://github.com/benmarwick/huskydown)

-[thesisdown](https://github.com/ismayc/thesisdown) 

-[bookdown](https://github.com/rstudio/bookdown)


Currently, the repository only renders a fully eddited PDF as required by G+PS and I have no plans to expand this in the future. The word version is usefull for revisions and keeping track changes, but it does not render a final version.

If you are new to working with `bookdown` and `rmarkdown`, please read over the documentation available in gauchodown PDF template (which you can create by following the simple instructions below) and the [bookdown book](https://bookdown.org/yihui/bookdown/).

## Using ubcdown to write your dissertation

### Initial setup

Using **ubcdown** has some prerequisites, such as Pandoc and LaTeX. To compile PDF documents using **R**, you need to have Pandoc, LaTeX and several related packages installed. If you have a recent version of [RStudio](http://www.rstudio.com/products/rstudio/download/), then you already have Pandoc and don't need to do anything more about that. 

Next is LaTeX. By far the easiest way to install LaTeX on any platform is with the [`tinytex`](https://yihui.name/tinytex/) package:

```
install.packages(c('tinytex', 'rmarkdown'))
tinytex::install_tinytex()
# after restarting RStudio, confirm that you have LaTeX with 
tinytex:::is_tinytex()
```

### Starting to write your thesis

To use `gauchodown` from [RStudio](http://www.rstudio.com/products/rstudio/download/):

1) Ensure that you have already installed LaTeX and the fonts described above, and are using the latest version of [RStudio](http://www.rstudio.com/products/rstudio/download/). You can use `gauchodown` without RStudio. For example, you can write the Rmd files in your favourite text editor (e.g. [Atom](https://atom.io/), [Notepad++](https://notepad-plus-plus.org/)). But RStudio is probably the easiest tool for writing both R code and text in your thesis. 

2) Install the `bookdown` package: 

```
install.packages("bookdown")
```

### Your thesis structure

At this point you already `forked` this repository to your own github or download the zip file to your computer and got yourself a nice looking repo with a `main_script.Rmd` file. This is the main script of your disserttation (see below). In addition you will see the following structure (se below for detailed instructions of each section):

- Images; This folder is intended to have any image you will use *outside* your main chapters (e.g., figures of the introduction)

- Reference; this is where you will store your bibliograohy and the reference guideline. Note that, as of March of 2021, G+PS does not require an [specific reference style](https://www.grad.ubc.ca/current-students/dissertation-thesis-preparation). 

  - *reference_format.csl*; This is the bibliography guiding file. The default is [harvard style](https://www.mendeley.com/guides/harvard-citation-guide). If you want to change the format, Zotero provides a [list](https://www.zotero.org/styles) of referencing styles you can download. Just make sure you keep the file name `reference_format.csl`

  - *reference_list.bib*; This file contains your bibliography. I just exported a bibliogrphy from my reference-library program (e.g., Zotero, mendeley) as a `.bib` file. Alternativeley, you can copy the reference foramt to your clipboard and pasted it here. 

- Sections; Here you will find each of the [sections](https://www.grad.ubc.ca/current-students/dissertation-thesis-preparation/structure-theses-dissertations) of the dissertation according to UBC GP+s. Note that some of them (e.g., glossary) are optional. 

- Data; This repository is inteded to store any data needed for rendering the thesis. I strongly suggest you not to have any heavy data files in here. Github will allow you to have up to 2Mb with the [Git Large Files](https://git-lfs.github.com/) plug-in, but anything larget than that should be outside this project.

### Day-to-day writing of your thesis 

You need to edit the individual chapter R Markdown files to write your thesis but you can write in the Rmd files without RStudio on our favourite text editor. However, I suggest you to come back to RStudio to create the PDF and work on the R code in the documents.

While writing, you should `git commit` your work frequently, after every major activity on your thesis. For example, every few paragraphs or section of text, and after major step of analysis development. You should `git push` at the end of each work session before you leave your computer or change task. For gentle novice-friendly guide to getting starting with using Git with R and RStudio, see <http://happygitwithr.com/>.

The main script of your thesis is the `main_script.Rmd` file. This file calls all other sections and builds the final PDF. Note that there are some *few* parts of this script that need modification (e.g., Chapter titles). The "general" disseration sections (e.g., abstract, acknowledgements, introduction), that is, those that are not data chapters, can be found in the `Sections` folder. Each Data chapter is called with the `knitr::knit_child` function (see below).

#### Organizing with `knitr::knit_child`

You can certainly use the same project to house all of the data and code for each of your chapters (and if your analysis runs fast enough you could of course simply do all of your analysis and writing for a chapter in the .Rmd for that chapter). In my experience, I had one R-project *per* chapter which I then knitted together for the final dissertation. Here is an explanation, copied directly from Dan Ovando of `gauchodown`, as I conuld't to better:

*My dissertation had three chapters. For each chapter, I created a separate RStudio project and folder on my computer, call it "~/PhD/zissou" (I nickname all my projects). Inside that folder I stored the data, code, and paper .Rmd for the `zissou` chapter. When I wanted to actually knit the dissertation, rather than copy-and-pasting all the required results or data from `zissou` over to my `dissertation` folder, I simply used `knit_child` (and some voodoo in the chunk options).*

## Rendering

To render your thesis into a PDF, open `main_script.Rmd` in RStudio and then click the "knit" button. To change the output formats between PDF and Word, look at the `output:` field and comment-out the formats you don't want.

The PDF file of your thesis will be deposited in the main directory.

## Components

The following components are the ones you should edit to customize your thesis:

### `main_script.Rmd`

This is the main configuration file for your thesis. It provides the main structure of your thesis and have *some* regions that require modifications. The main sections where you need to modify the file are identified with the label `<!-- Modify me! -->` right above the section. These include the Title of each data chapter and the title of each Apendix.

#### Data Chapters
The basic structure has Four data chapters. If you have more than four data chapters, you can copy and paste the format below after chapter four, (note that for each new chapter you need to change the Title, the figure, and the table numbers):

```
# Chapter Five: Incert Title Chapter Here

<!-- Set figure and table numbering according to the chapter -->
\renewcommand{\thefigure}{5.\arabic{figure}}
\setcounter{figure}{0}
\renewcommand{\thetable}{5.\arabic{table}}
\setcounter{table}{0}
\renewcommand{\theequation}{5.\arabic{equation}}
\setcounter{equation}{0}

{r chapter_five, child = '~chapter_5_path/chapter_5_file.Rmd', eval = T}

```

Adittionally, if you have less than four data chapters you can just comment out the last chapter and set the child option to `eval = F`. Alternativeley you can just errase the chapter info in the main script.

#### Appendices

The basic structure has one appendix for each data chapter. So, for each chapter you also need to createan apendix section as detailed above. Below is the form.


```
\section*{Appendix D - Supplementary information for "Name of Chapter Five"}
\addcontentsline{toc}{section}{Appendix D}


<!-- Set Figure, table and equations numbering according to the chapter -->
\renewcommand{\thefigure}{A5.\arabic{figure}}
\setcounter{figure}{0}
\renewcommand{\thetable}{A5.\arabic{table}}
\setcounter{table}{0}
\renewcommand{\theequation}{A5.\arabic{equation}}
\setcounter{equation}{0}

{r appendix_d, child = '~/path_to_appendix_5/appendix_5.Rmd', eval = T}

```

#### Optional sections

According to UBC's G+PS instructions as of March of 2021, there are some global sections that are optional. The current structure has *all* of the sections. If you want to remove any global section you simply need to comment out the `\section` and `addcontentsline` sections (these give the title in the body and the table of content), and set the child `eval` option to *F*. I recommend you not to delete a section you don't want in case you change your mind latter and want to inldue it. Note that you do not need to worry about page numbering or table of contents! Below is an example of the `Dedication` section commented out. 

```
<!-- Dedication -->
<!-- \section*{Dedication} -->
<!-- \addcontentsline{toc}{section}{Dedication} -->
```

```{r dedication, child = '../Sections/07_Dedication.Rmd', eval = F}

```

### `00_Cover.Rmd`, `01_Committee_form.Rmd`, `02_Abstract.Rmd`, etc.

These are the Rmd files for each *global* chapter in your dissertation. Write your thesis in these. If you're writing in RStudio, you may find the [wordcount addin](https://github.com/benmarwick/wordcountaddin) useful for getting word counts and readability statistics in R markdown documents.

## Related projects

This project has drawn directly on code and ideas from Dan Ovand's [gauchodown](https://github.com/DanOvando/gauchodown).

Other relevant projects include:

- https://github.com/UWIT-IAM/UWThesis    
- https://github.com/stevenpollack/ucbthesis  
- https://github.com/suchow/Dissertate    
- https://github.com/SeungkiKwak/Kwak_S_PhD_thesis    
- https://github.com/dhalperi/uwthesis-tweaked     

- Ed Berry's blog post ['Writing your thesis with bookdown'](https://eddjberry.netlify.com/post/writing-your-thesis-with-bookdown/), Posted on September 25, 2017    
- Rosanna van Hespen's ([@rosannavhespen](https://twitter.com/rosannavhespen?lang=en)) five blog posts on ['Writing your thesis with R Markdown'](https://rosannavanhespenresearch.wordpress.com/2016/02/03/writing-your-thesis-with-r-markdown-1-getting-started/)
- [thesisdowndss](https://github.com/mine-cetinkaya-rundel/thesisdowndss) by Mine Cetinkaya-Rundel at Duke University    
- [beaverdown](https://github.com/zkamvar/beaverdown) by Zhian Kamvar at Oregon State University

## Contributing

If you would like to contribute to this project, please start by reading our [Guide to Contributing](CONTRIBUTING.md). Please note that this project is released with a [Contributor Code of Conduct](CONDUCT.md). By participating in this project you agree to abide by its terms.