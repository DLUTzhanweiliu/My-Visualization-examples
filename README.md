---
title: "show my graphs"
author: "Zhanwei"
object: help my to query codes
---
# My-Visualization-examples
show my graphs
****
![](./src/figs/flowcharts.phg)

  * [flowcharts.pdf](https://github.com/DLUTzhanweiliu/My-Visualization-examples/tree/main/src/figs/flowcharts.pdf)

```tex
\documentclass[border=10pt]{standalone}
\usepackage{tikz}
\usepackage{color}
\usetikzlibrary{shapes.misc, positioning,arrows.meta, shapes.geometric}
\tikzset{>={Latex[width=2mm,length=2mm]},
  %指定节点风格:
    base/.style = {rounded rectangle, draw=black,
                    minimum width=2.5cm, minimum height=0.5cm,
                    text centered},
    base2/.style = {rectangle, draw=black,
                    minimum width=2.5cm, minimum height=0.5cm,
                    text centered},
    base3/.style = {diamond, draw=black,
    minimum width=3cm, minimum height=0.5cm,aspect=2.5,
    text centered},
}
\begin{document}
  \begin{tikzpicture}[node distance=2cm, every node/.style={fill=white}, align=center]
  % 外边框
   \draw[dashed,fill=green!20] (-3.5,-0.6) rectangle (3.2,-10.3);
   \draw[dashed,fill=yellow!20] (3.3,-0.6) rectangle (9.6,-10.3);
  % 标注
    \node at (-2.5,-1) {\textcolor{blue}{Loose loop}};
    \node at (8.5,-1) {\textcolor{blue}{Strict loop}};
  
    \node (start) [base] {Start};
    \node (init) [base2, below= 0.5cm of start] {Initial gross water \\ head, b1=1};
    \node (model) [base2, below of=init] {Bulid and slove \textcolor{blue}{MILP (model1} \\ \textcolor{blue}{or model2) model}  based on the \\
    gross water head of previous \\
    interation, Set stopping \\
    criterion1 (Time=T1, Gap=G1)};
    \node (vars) [base2, below of=model] {$u_t,v_t$};
    \node (recompute) [base2, below = 0.5cm of vars] {Recompute gross water head \\ via (21), (22) and (38)};
    \node (judge) [base3, below of=recompute] {Meet the stopping \\ criterion (40)};
    \node (inter) [base2, rotate=90, left of=model, yshift=31mm,xshift=0cm] {b1=b1+1};
    \node (b2) [base2, right of=init, yshift=0cm,xshift=4cm] {$hg_t$,b2=1};
    %\node (temp) [right of=judge, yshift=0cm,xshift=0.2cm] {};
    \node (model2) [base2, below of = b2]{Bulid and slove  \textcolor{blue}{MILP (model1} \\ \textcolor{blue}{or model2) model}  based on the \\
    gross water head of previous \\
    interation, Set stopping \\
    criterion1 (Time=T2, Gap=G2)};
    \node (vars2) [base2, below of=model2] {$u_t,v_t$};
     \node (recompute2) [base2, below = 0.5cm of vars2] {Recompute gross water head \\ via (21), (22) and (38) };
    \node (judge2) [base3, below of=recompute2] {Meet the stopping \\ criterion (40)};
    \node (b22) [base2,  rotate=90, below of=inter, yshift=-103mm,xshift=0cm] {b2=b2+1};
    \node (end) [base, below = 1cm of judge2] {End};

    \draw[->] (start) -- (init);
    \draw[->] (init) -- (model);
    \draw[->] (model) -- (vars);
    \draw[->] (vars) -- (recompute);
    \draw[->] (recompute) -- (judge);
    \draw[->] (judge) -| node[yshift=1cm, text width=0.3cm] {No} (inter);
    \draw[->] (inter) |- (model);
   \draw[->] (judge.east) -| ++ (1mm,2cm) |- node[yshift=-6cm, text width=0.45cm]{Yes} (b2.west);
     %\draw (judge) -- (temp);
     %\draw[->] (temp) |- node[yshift=-9cm, text width=0.3cm] {Yes}(b2);
     \draw [->] (b2)--(model2);
     \draw [->] (model2) -- (vars2);
      \draw [->] (vars2) -- (recompute2);
      \draw[->] (recompute2) -- (judge2);
      \draw[->] (b22) |- (model2);
      \draw[->] (judge2) -| node[yshift=1cm, text width=0.3cm]{No}(b22);
      \draw[->] (judge2) -- node[yshift=0.1cm, text width=0.45cm]{Yes}(end);
      
   % \draw[->] (judge.east) -- (judge.east-|b2.west);
   
  \end{tikzpicture}
\end{document}
```
****
