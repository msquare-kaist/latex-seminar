# 2019 수문연 편집부 레이텍 세미나

[main.pdf](main.pdf)

## 생각없이 불러오면 편한 패키지들
```tex
\usepackage{kotex}
\usepackage{amsmath,amsfonts,amssymb,mathrsfs,mathtools}
\usepackage{adjustbox,float,graphicx,relsize}
\usepackage{xcolor}
\usepackage{tikz}
\usepackage{setspace}
\usepackage{expl3}
\usepackage{xparse}
\usepackage{enumitem}
\usepackage{forloop}
```


## 쓰인 코드들
```tex
\documentclass[a4paper,10pt]{article}
\usepackage{amsmath}
\usepackage{kotex}
\title{제목}

\begin{document}
\maketitle

안녕하세요? \LaTeX을 배우면 좋은 일이 있을 거예요. % 아닐 수도..

\makeatletter
당신이 입력했던 제목입니다: \@title.\footnote{신기한가요??}
\makeatother
\end{document}
```

```tex
\documentclass[a4paper,10pt]{article}
\usepackage{amsmath,amsfonts,amssymb,mathrsfs,mathtools,kotex}
\title{\scshape Practice}
\begin{document}
\maketitle
\[ \text{근의 공식}:\qquad x = \frac{-b\pm\sqrt{b^2 - 4ac}}{2a}. \]
$\alpha, \beta$는 있지만 \texttt{\char`\\Alpha, \char`\\Beta}는 없다!

Radical of an ideal $\sqrt{\mathfrak a}$

크기가 조절되는 괄호를 열 때에는 $\left( \frac a b \right)$처럼 씁니다.
강의할 때 어느 정도 설명해주세요 \char`\^\char`\^7
\end{document}
```

```tex
\begin{itemize}
  \item 첫 번째
  \item[2] 두 번째
  \item[$\gamma$] wow
\end{itemize}

\begin{enumerate}[label={\roman*\arabic*}]
  \item 자동으로
  \item 올라가는
  \item 번호
\end{enumerate} 
```

```tex
\begin{itemize}
\[ 
  \begin{pmatrix}
    a_{11} & a_{12} \\  
    a_{21} & a_{22}
  \end{pmatrix} \cdot
  \begin{bmatrix}
    b_{11} & b_{12} \\  
    b_{21} & b_{22}
  \end{bmatrix} =
  \begin{vmatrix}
    c_{11} & c_{12} \\  
    c_{21} & c_{22}
  \end{vmatrix} \cdot \mathbf I
\]
```

```tex
\newtheorem{thm}{Theorem} % basic usagae
\newtheorem{lem}[thm]{Lemma} % shares the numbering w/ thm

\theoremstyle{definition}
\newtheorem{defn}{Definition}[section] % Def section.def_number

\theoremstyle{plain} % recover the theoremstyle
\newtheorem*{cor}{Corollary} % no numbering (*)

\begin{lem}[Lemma Name] This lemma is very awesome. \end{lem}
\begin{proof} Leave as an exercise. \end{proof}
```

```tex
% H means that it tries to put on the exact position
\begin{figure}[H] 
  \begin{center}
    \includegraphics[width=0.5\textwidth]{msquare}
    \caption{Gorgeous}
  \end{center}
\end{figure}
```


