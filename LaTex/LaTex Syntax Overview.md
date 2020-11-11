# LaTex Syntax

## Useful settings for pagenumbering:
`Syntax: pagenumbering{option}`
- gobble - no numbers
- arabic - arabic numbers
- roman - roman numbers

## Using LaTex paragraphs and sections

**Syntax**

|   discription    |                                                         comment                                                          |
| :--------------: | :----------------------------------------------------------------------------------------------------------------------: |
|    \section{}    | The Section commands are numbered will appear in the table of contents.If you add * after command.It will be unnumbered. |
|  \subsection{}   |                                            Appear as 1.1.The same as \section                                            |
| \subsubsection{} |                                           Appear as 1.1.1.The same as \section                                           |
|   \paragraph{}   |              The Paragraph commands will not be numbered and will not appear in the table of the contents.               |
|  \subparagraph   |                                          Indent relative to previous paragraph                                           |

## including a package

### Packages add features such as support for pictures, links and bibliography

Including different packages to get various functions.
such as {amsmath}.If you want to type math function without number.You have to include that.
```latex
\usepackage{amsmath}

\begin{equation*}
  f(x) = x^2
\end{equation*}
```

## LaTex Math & Eqations