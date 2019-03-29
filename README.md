# 2019 수문연 편집부 레이텍 세미나

[main.pdf](main.pdf)

* 2018 여름 LaTeX 스터디: http://utophii.dothome.co.kr/tex/

## TinyTeX 설치
[여기 참고](https://github.com/utophii/tinytex-for-korean)


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

## Must-have Packages
혹시 용량이 적은 TeX dist를 설치하셨다면 다음 명령어를 실행시켜주세요.
```bash
tlmgr install adjustbox amscls amsfonts amsmath babel beamer biblatex bibtex booktabs caption changepage cjk-ko cm collectbox dantelogo dehyph dtk dvipdfmx dvips ec enumitem environ etex etoolbox euenc expex fancyhdr fancyvrb float fontspec forloop framed fvextra geometry glyphlist graphics graphics-cfg graphics-def gsftopk helvetic hyperref hyphen-base ifluatex ifmtarg ifplatform iftex ifxetex inconsolata jknapltx knuth-lib kotex-plain kotex-utf kpathsea l3kernel l3packages latex latex-bin latex-fonts latexconfig latexmk lineno listings lm logreq lua-visual-debug luainputenc lualibs luaotfload luatex luatexko makeindex mathspec mathtools metafont mfware ms nanumtype1 natbib oberdiek pdftex pgf pgfplots plain relsize rsfs scheme-infraonly setspace tcolorbox tetex tex tex-ini-files texlive.infra tikz-cd times tipa titlesec titling tools translator trimspaces ulem unicode-data upquote url wrapfig xcolor xetex xetexconfig xifthen xkeyval xstring xunicode zapfding
```

## 쓰인 코드들
```tex
\documentclass[a4paper,10pt]{article}
\usepackage{amsmath}
\usepackage{kotex}
\title{제목}

\makeatletter % 원래 @은 매크로 이름에 쓸 수 없는데 쓸 수 있게 해주는 매크로입니다.
\let\thetitle=\@title
\makeatother % 다시 @을 매크로 이름에 쓸 수 없게 만듭니다. (내부 매크로 보호)
\begin{document}
\maketitle

안녕하세요? \LaTeX을 배우면 좋은 일이 있을 거예요. % 아닐 수도..

당신이 입력했던 제목입니다: \thetitle.\footnote{신기한가요??}
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

```tex
\newcounter{left} \newcounter{right}
\forloop{left}{2}{\value{left} < 10}{%
  \noindent\forloop{right}{2}{\value{right} < 10}{%
    $\arabic{left} \times \arabic{right} =
      \the\numexpr\arabic{left} * \arabic{right}\relax$,
  }
  \par
}
```

```tex
\ExplSyntaxOn % _와 :를 매크로 이름에 쓸 수 있게 만듭니다.
\NewDocumentCommand{\vecNotation}{m O{3}}{
  % \tl_if_eq:nnTF{토큰 리스트1}{토큰 리스트2}{같을 때}{다를 때}
  \tl_if_eq:nnTF{#2}{1}{
    (#1\sb 1) % \ExplSyntaxOn이 _를 문자로 바꾸므로 
              % \sb라는 명령어로 subscript를 만듭니다.
  }{
    \tl_if_eq:nnTF{#2}{2}{
      (#1\sb 1, #1\sb 2)^{\mathsf{T}}
    }{
      \tl_if_eq:nnTF{#2}{3}{
        (#1\sb 1, #1\sb 2, #1\sb 3)^{\mathsf{T}}
      }{
        (#1\sb 1, #1\sb 2, \dots, #1\sb{#2})^{\mathsf{T}}
      }
    }
  }
}
\ExplSyntaxOff % _와 :를 다시 각자의 목적으로 되돌립니다.
```

```tex
\newcommand{\repsum}[3]{%
  \foreach \i in {1,...,#1}{
    \ifnum\i>1
      + #2_{\i} #3_{\i}
    \else
      #2_{\i} #3_{\i}
    \fi
  }
}
```

```tex
\ExplSyntaxOn
\makeatletter
% supposing #1 >= #2 > 0
\newcommand{\euclidalgorithm}[2]{             % example: \euclidalgorithm{60}{33}
    \gdef\@@a{#1}
    \gdef\@@b{#2}
    \[
    \begin{array}{r@{\;=\;}r@{\;\cdot\;}l@{}l@{}l@{\quad}|@{\quad}r@{}r@{}r@{}r@{}r}
        \euclid@lgorithm                                    % initialise
        {#1}{#2}                                            % a and b
        {\int_div_truncate:nn{#1}{#2}}                      % quotient q = floor(a / b)
        {\int_mod:nn{#1}{#2}}                               % remainder a mod b
        {0}{1}                                              % b = 0 * a + 1 * b
        {1}{\the\numexpr-\int_div_truncate:nn{#1}{#2}\relax}% r = 1 * a + (-q) * b
    \end{array}
    \]
}
\newcommand{\euclid@lgorithm}[8]{
    \int_compare:nNnTF {#4} = {0}
    {
        % if remainder is 0, do not call recursively
        #1 & \mathbf{#2} & #3 &&&
    }
    {%
        % print a line
        #1 & #2 & #3 \;&\;+\;&\; #4 & #4 &\;=\;&\;\@@a \;\cdot\; &
        \,{\ifnum#7<\z@ (#7) \else #7\hphantom{)}\fi} + \@@b \;\cdot\;&
        \,{\ifnum#8<\z@ (#8) \else #8\hphantom{)}\fi} \\%
        % call itself recursively
        \euclid@lgorithm
        {#2}{#4}
        {\int_div_truncate:nn{#2}{#4}}
        {\int_mod:nn{#2}{#4}}
        {#7}{#8}
        {\the\numexpr #5 - \int_div_truncate:nn{#2}{#4} * #7\relax}
        {\the\numexpr #6 - \int_div_truncate:nn{#2}{#4} * #8\relax}% 
    }
}
\makeatother
\ExplSyntaxOff
```

```tex
\makeatletter
\def\eqv#1#2{\let\mod=\m@d{#1}\expandafter\eqvB{#2}}
\def\eqvB#1{
  \@ifnextchar\mod{\equiv#1}{\equiv#1\expandafter\eqvB}
}
\def\m@d#1{\quad({\operatorname{mod}}\;#1)}
\makeatother
```

```tex
\def\firstoftwo#1#2{#1}
\def\secondoftwo#1#2{#2}

\def\rev#1#2\revA#3\revB{%
  \if\relax\detokenize{#2}\relax
    \expandafter\firstoftwo
  \else
    \expandafter\secondoftwo
  \fi{#1#3}{\rev#2\revA#1#3\revB}%
}
```

```tex
\makeatletter
\expandafter\def\csname my@array@1\endcsname{1}
\expandafter\def\csname my@array@2\endcsname{2}

% with counter
\newcounter{arrayindex}
\setcounter{arrayindex}{3}
\expandafter\def\csname my@array@\value{arrayindex}\endcsname
  {\value{arrayindex}}
\makeatother
```

