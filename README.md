latex-misc
==========

some macros for LaTeX, I use.  
Please use it if you like.


私が使っているマクロ集です。  
よければお使いください。

- - -

### TwoDigits(二桁化)
this macro supported 0~99.  
0~99までの引数で1桁のものに0をつけます。

```latex
\newcommand{\twoDigits}[1]{\ifnum#1<10 0#1\else#1\fi}

% \twoDigits{1} -> 01
% \twoDigits{10} -> 10
% \twoDigits{100} -> 100 % not supported
```

### LastCompileDate(最終コンパイル日時を印字)
this macro needs twoDigits. If you customize it, change \LastCompiledStr.  
twoDigitsを使ってます。日時のフォーマットを変えたいときは\LastCompiledStrを変えてください。

``` latex
\newcommand{\twoDigits}[1]{\ifnum#1<10 0#1\else#1\fi}
\newcommand{\LastCompileDateStr}{lastcompiled:\the\year/\the\month/\the\day~\twoDigits{\the\hour}:\twoDigits{\the\minute}}
\newcommand{\LastCompileDate}{\vspace*{\fill}\hspace*{\fill} \LastCompileDateStr}

% \LastCompileDateStr -> lastcompiled:2014/3/16 23:03
% ex) \LastCompileDate\end{document}
```

### continuedEnumerate(enumerate環境を区切っても番号は続ける)

``` latex
\newcounter{enumeratelastnumber}
\setcounter{enumeratelastnumber}{0}
\newenvironment{continuedEnumerate}{ %
	\begin{enumerate}
	\setcounter{enumi}{\value{enumeratelastnumber}}
}{ %
	\setcounter{enumeratelastnumber}{\value{enumi}}
	\end{enumerate}
}

% \begin{continuedEnumerate}
% \item first
% \item second
% \end{continuedEnumerate}
% splitted
% \begin{continuedEnumerate}
% \item third
% \item fourth
% \end{continuedEnumerate}
```

## emphasisedItem(itemを強調する)
This macro add `\eitem` command, that add symbol before `\item` in `itemize` or `enumerate`.  
`\item`の前にシンボルを追加します。

``` latex
\newlength{\eitemindent}\setlength{\eitemindent}{12mm}
\newlength{\eiteminnerboxwidth}\setlength{\eiteminnerboxwidth}{5mm}
\newcommand{\eitem}[1][]{ %
	\item\hspace{-\eitemindent}
	\makebox[\eiteminnerboxwidth]{#1}
	\hspace{-\eiteminnerboxwidth}
	\hspace{\eitemindent}
	\hspace{-5.5mm} % space between enumerate number and strings. 
}


% \begin{enumerate}
% \eitem spam
% \eitem impo
% \eitem[$\bigcirc$]important!!!
% \eitem[$\times$]bad
% \eitem[$\bigtriangleup$]so so
% \end{enumerate}
```
