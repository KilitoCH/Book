## LaTex Syntax

### Useful settings for pagenumbering:
`Syntax: pagenumbering{option}`
- gobble - no numbers
- arabic - arabic numbers
- roman - roman numbers

### Using LaTex paragraphs and sections

**Syntax**

|   discription    |                                                         comment                                                          |
| :--------------: | :----------------------------------------------------------------------------------------------------------------------: |
|    \section{}    | The Section commands are numbered will appear in the table of contents.If you add * after command.It will be unnumbered. |
|  \subsection{}   |                                            Appear as 1.1.The same as \section                                            |
| \subsubsection{} |                                           Appear as 1.1.1.The same as \section                                           |
|   \paragraph{}   |              The Paragraph commands will not be numbered and will not appear in the table of the contents.               |
|  \subparagraph   |                                          Indent relative to previous paragraph                                           |

### including a package

#### Packages add features
such as support for pictures, links and bibliography.

Including different packages to get various functions.
such as {amsmath}.If you want to type math function without number.You have to include that.
```latex
\usepackage{amsmath}

\begin{equation*}
  f(x) = x^2
\end{equation*}
```

### LaTex Math & Eqations
There are two modes of typesetting math in LaTex.
1. One is embedding the math directly into your text by encapsulating your formula in dollar signs.Which is called inline math.
> Such as `This formula $f(x) = x^2$ is an example`.
> It's like $f(x) = x^2$.

2. The other is using a predefined math environment.
   - You can use equation or align to arrange your contents.
       Such as:
       ```LaTex
       \usepackage{amsmath}

       \begin{document}

       \begin{equation*}
         1 + 2 = 3 
       \end{equation*}

       \begin{equation*}
         1 = 3 - 2
       \end{equation*}

       \begin{align*}
         1 + 2 &= 3\\
         1 &= 3 - 2
       \end{align*}

       \end{document}
       ```
       It's like:
      $$\begin{aligned}
        1 + 2 &= 3\\
         1 &= 3 - 2
      \end{aligned}$$
    - Single equations have to be seperated by a linebreak`\\`.Or it won't switch to another line.
     - You have to align the equations ant the ampersand &.
3. Fraction & Other notation
   * It's possible to typeset various notations.Every command has a specific syntax.
   * Here are some examples.
  
    | notation | description |             comments              |           show results            |
    | :------: | :---------: | :-------------------------------: | :-------------------------------: |
    |   '^'    |    power    |           `f(x) = x^2`            |           $f(x) = x^2$            |
    | `\frac`  |  fraction   |       `g(x) = \frac{1}{x}`        |       $g(x) = \frac{1}{x}$        |
    |  `\int`  |  integral   |  `f(x) = \int^a_b \frac{1}{x}dx`  |  $f(x) = \int^a_b\frac{1}{x}dx$   |
    |  \sqrt   | square root | `f(x) = \frac{1}{\sqrt{x^2 + 1}}` | $f(x) = \frac{1}{\sqrt{x^2 + 1}}$ |

4. Matric
   The matrices only work within math environments as `amsmath`
   For example:
   ```LaTex
   \begin{matrix}
   1 & 0\\
   0 & 1
   \end{matrix}
   ```
   It's like:
   $$\begin{matrix}
      1 & 0\\
      0 & 1     
   \end{matrix}
     $$
5. Brackets in math mode - Scaling
   To surround the matrix by brackets, it's necessary to use special statements, because the plain [ ] symbols do not scale as the matrix grows. Such as:

   ```LaTex
    \left[
    \begin{matrix}
    1 & 0\\
    0 & 1
    \end{matrix}
    \right]
    ```  
  $$
      \begin{vmatrix}
        1 & 0\\
        0 & 1
      \end{vmatrix}
  $$

### Insert an image in LaTex
  You can insert captioned images,set image position,multiple images in LaTex.
  > You have to use **`graphicx`** package to arrange images.
#### Captioned images/figures
You have to include the fig into environment:
```LaTex
\usepackage{graphicx}

\begin{document}

\begin{figure}
  \includegraphics[width=linewidth]{sample.jpg}
  \caption{A sample.}
  \lable{fig:sample}
\end{figure}

\end{document}
```

#### image positioning
Setting the float by adding `[option]`behind the figure environment `begin`  tag will force the figure to be shown as you wish.Possible options:
| options | description |            comments             |
| :-----: | :---------: | :-----------------------------: |
|    h    |    here     | the same location as you define |
|    t    |     top     |           top of page           |
|    b    |   bottom    |         bottom of page          |
|    p    |    page     |        on an extra page         |
|    !    |  override   |    force the option to work     |

#### Multiple images /subfigures in LaTex
* First you have to usepackage **`subcaption`**.
* Then use `{figure}` to include `{subfigure}` to arrange multi images:
```LaTex
\begin{figure}[h!]
  \centering
  \begin{subfigure}[b]{0.4\linewidth}
    \includegraphics[width=\linewidth]{coffee.jpg}
    \caption{Coffee.}
  \end{subfigure}
  \begin{subfigure}[b]{0.4\linewidth}
    \includegraphics[width=\linewidth]{coffee.jpg}
    \caption{More coffee.}
  \end{subfigure}
  \caption{The same cup of coffee. Two times.}
  \label{fig:coffee}
\end{figure}
```
* If you want to align more than one figure in one row.You should set the width value to 0.1 less than expected.For examle,if you want to arrange 3 figures,you should set`\begin{subfigure}[b]{0.2\linewidth}`.
* If total width is bigger than 1,the last figure will be placed to another row.

### Create table of contens
* You can just type `tableofcontents` to insert a content.You will get table of contents **after compiling the .tex file twice.**
```LaTex
\begin{document}

\tableofcontents
\newpage

\section{Section}

Dummy text

\subsection{Subsection}

Dummy text

\end{document}
```
* If you want to create list of figures/tables.Use`\listoffigures`&`\listoftables`
* You can control the depth of content.The syntax is like`\setcounter{tocdepth}{number}`.When it's set to **1**,only **sections** will be shown,etc.
* If you just want to control depth in specific section,use `\addtocontents{toc}{\setcounter{tocdepth}{number}}` instead.
### Spacing of contents
The easiest way of changing the spacing of your table of contens and documents is by using **`setspace`** package:
```LaTex
\usepackage{setspace}
\begin{document}

\doublespcaing
\tableofcontens
%only table of contents will be typeset as double spacing.
\singlespacing
```
### Bibliography in LaTex
#### create a .bib file
First we have to create a .bib file to contain our bib info.
Here is one of [generator](https://www.bibme.org/bibtex).It could create .bib like:
> @article{2004 ieee international soi conference (ieee cat no 04ch37573) csics-04_2004, 
title={IEEE Compound Semiconductor Integrated Circuit Symposium. 2004 IEEE CISC Symposium (IEEE Cat. No.04CH37591)},   
DOI={10.1109/csics.2004.1392455},   
journal={2004 IEEE International SOI Conference (IEEE Cat No 04CH37573) CSICS-04},   
year={2004},  
}

### Footnotes && Reference


