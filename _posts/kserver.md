
% UPDATE Figure 2(b) so that one of the clusters comes over to touch B'

\documentclass[11pt,letterpaper]{article}

\newcommand{\Osp}{O\!}
\newcommand{\isin}{\mathrm{in}}
\newcommand{\isout}{\mathrm{out}}
\newcommand{\depth}{\mathrm{rank}}
\newcommand{\downW}{W_{\vvT}^{1}}
\newcommand{\Tquot}{\vvT/\beta}
\newcommand{\redcost}{\cost^{\beta}_{\vvT}}
\newcommand{\redist}{W^{\beta}_{\vvT}}
\newcommand{\Vext}{\cV(\vvT)}
\newcommand{\Vextquo}{\cV_{\vvT/\beta}}
\newcommand{\Kfin}{\mathsf{K}_{\delta}}
\newcommand{\Ktope}{\mathsf{K}}
\newcommand{\crdet}[2]{\mathsf{D}_{#2}(#1)}
\newcommand{\crprob}[2]{\mathsf{R}_{#2}(#1)}
\newcommand{\jtstar}{j_t^*}
\newcommand{\jstar}{\tau^{-j_t^*} \1_{\{j_t^* > 0\}}}
\newcommand{\prefuse}{\mathrm{pre}}
\newcommand{\mustar}{\cost_{\vvT}^{\beta}(\bm{\mu}^*)}
\newcommand{\heavy}{\mathrm{heavy}}
\newcommand{\indic}{\bm{\mathrm{I}}}
\newcommand{\omegahst}{\Omega^{\hst}}
\newcommand{\omegadel}{\Omega^{\del}}
\newcommand{\hst}{\mathrm{hst}}
\newcommand{\del}{\mathrm{del}}
\newcommand{\ins}{\mathrm{ins}}
\newcommand{\fus}{\mathrm{fus}}
\newcommand{\fis}{\mathrm{fis}}
\newcommand{\tempC}{\tilde{C}}
\newcommand{\tempP}{\tilde{P}}
\newcommand{\temppi}{\tilde{\pi}}
\newcommand{\tempQ}{\tilde{Q}}
\newcommand{\tempR}{\tilde{R}}
\newcommand{\tempLam}{\tilde{\Lambda}}
\newcommand{\inject}{\hookrightarrow}
\newcommand{\bott}{\vvmathbb{b}}
\newcommand{\distT}{\mathrm{dist}_{\vvT}}
\newcommand{\quodist}{\mathrm{dist}_{\vvT/\beta}}
\newcommand{\distTstar}{\mathrm{dist}_{\vvT^*}}
\newcommand{\leavesT}{\cL_{\vvT}}
\newcommand{\eleavesT}{\hat{\cL}_{\vvT}}
\newcommand{\internalT}{\cI_{\vvT}}
\newcommand{\leavesTstar}{\cL_{\vvT^*}}
\newcommand{\lca}{\mathrm{lca}}
\newcommand{\len}{\mathrm{len}}
\newcommand{\lev}{\mathrm{lev}}
\newcommand{\llangle}{\left\langle}
\newcommand{\rrangle}{\right\rangle}
\newcommand{\Sin}{S_{\mathrm{in}}}
\newcommand{\Sout}{S_{\mathrm{out}}}
\newcommand{\descend}{\cL}
\newcommand{\rad}{\mathsf{r}}
\newcommand{\Lip}{\mathrm{Lip}}
\newcommand{\Ent}{\mathrm{Ent}}
\newcommand{\parval}{\mathrm{par}}
\newcommand{\matval}{\mathrm{mat}}
\newcommand{\ispos}{\oplus}
\newcommand{\isneg}{\ominus}
\newcommand{\mE}{\mathbb{E}}
\newcommand{\Alice}{\tilde A_{\sigma}}
\newcommand{\Bob}{\tilde B_{\pi}}
\newcommand{\clip}{\mathrm{clip}}
\newcommand{\primo}{\mathsf{P}^*}
\newcommand{\duo}{\mathsf{D}^*}
\newcommand{\shift}{\mathsf{shift}}
\newcommand{\Exp}{\mathrm{Exp}}
\newcommand{\alg}{\mathrm{alg}}
\newcommand{\HST}{\mathrm{HST}}
\newcommand{\cost}{\mathrm{cost}}
\newcommand{\whst}{W^1_{\vvT}}
\newcommand{\kmeas}{\vvM_k}
\newcommand{\kplusmeas}{\vvM_{k}}
\newcommand{\intmeas}{\widehat{\vvM}_m}
\newcommand{\hash}{\#}
\newcommand{\last}{\mathrm{last}}
\newcommand{\lightscales}{\vvL}
\newcommand{\intscales}{\vvJ}
\newcommand{\intcost}{\cost_{\ell_1(\vvT)}}
\newcommand{\disc}{\mathsf{D}}
\newcommand{\height}{\mathsf{H}}
\newcommand{\auxheight}{\mathsf{A}}
\newcommand{\dsup}{d^{\sup}}
\newcommand{\morph}{\mathrm{mph}}
\newcommand{\ch}{c}
\newcommand{\lip}{\mathrm{hst}}

\newcommand{\vvr}{\vvmathbb{r}}
\newcommand{\blur}{\mathsf{blr}}
\newcommand{\sharpen}{\mathsf{hst}}
\newcommand{\augment}{\mathsf{aug}}
\newcommand{\leaves}{\mathcal{L}}
\newcommand{\tree}{\vvmathbb{T}}
\newcommand{\B}{\mathsf{B}}
\newcommand{\I}{\mathsf{I}}
\newcommand{\sh}{\mathsf{S}}
\newcommand{\augdist}{\mathrm{dist}^{+}}
\newcommand{\augcost}{\cost^{+}}
\newcommand{\augW}{W^{+}}
\newcommand{\intV}{V^{\circ}}

\def\sharemode{1}
\def\stocmode{0}
\def\jamesmode{0}
\def\arxivmode{0}
\def\fastmode{0}
\def\nnrmode{1}
\def\entmaxmode{0}
\def\showauthornotes{0}
\def\showtableofcontents{1}
\def\showkeys{0}
\def\showdraftbox{1}
\def\showcolorlinks{1}
\def\usemicrotype{1}
\def\showfixme{1}
\def\showdefine{0}


\def\mm{\mathrm{match}}
\def\hatgamma{{\hat \gamma}}
\def\distort{\mathfrak{D}}
\def\gauss{\bm{\xi}}

\newcommand{\vph}{\vphantom{\bigoplus}}
\newcommand{\ket}[1]{\,|#1\rangle}
\newcommand{\bra}[1]{\langle#1|}
\newcommand{\Hmin}{H_\infty}
\newcommand{\iRmin}{\vvmathbb{R}^*_{\infty}}
\newcommand{\Rmin}{\vvmathbb{R}_{\infty}}
\newcommand{\Bmin}{\vvmathbb{B}_{\infty}}
\newcommand{\Dmin}{D_\infty}
\newcommand{\vvL}{\vvmathbb{L}}
\newcommand{\vvI}{\vvmathbb{I}}
\newcommand{\vvJ}{\vvmathbb{J}}
\newcommand{\vvT}{\vvmathbb{T}}
\newcommand{\vvX}{\vvmathbb{X}}
\newcommand{\vvM}{\vvmathbb{M}}
\newcommand{\vvY}{\vvmathbb{Y}}
\newcommand{\vvZ}{\vvmathbb{Z}}
\newcommand{\vvS}{\vvmathbb{S}}
\newcommand{\vvP}{\vvmathbb{P}}
\newcommand{\vvQ}{\vvmathbb{Q}}
\newcommand{\loc}{\mathrm{loc}}
\newcommand{\minent}{\vvmathbb{H}_{\infty}}

%
%

\ifnum\fastmode=0
\usepackage{etex}
\fi

%

\ifnum\fastmode=0
\usepackage[l2tabu, orthodox]{nag}
\fi

%

\usepackage{xspace,enumerate}

\usepackage[dvipsnames]{xcolor}

\ifnum\fastmode=0
\usepackage[T1]{fontenc}
\usepackage[full]{textcomp}
\fi

%
%
\usepackage[american]{babel}
%

%

\usepackage{mathtools}


%

%
\newcommand\hmmax{0} %
%

%


%
\usepackage{amsthm}

\newtheorem{theorem}{Theorem}[section]
\newtheorem*{theorem*}{Theorem}
\newtheorem{itheorem}{Theorem}

\newtheorem{subclaim}{Claim}[theorem]
\newtheorem{proposition}[theorem]{Proposition}
\newtheorem*{proposition*}{Proposition}
\newtheorem{lemma}[theorem]{Lemma}
\newtheorem*{lemma*}{Lemma}
\newtheorem{corollary}[theorem]{Corollary}
\newtheorem*{conjecture*}{Conjecture}
\newtheorem{fact}[theorem]{Fact}
\newtheorem*{fact*}{Fact}
\newtheorem{exercise}[theorem]{Exercise}
\newtheorem*{exercise*}{Exercise}
\newtheorem{hypothesis}[theorem]{Hypothesis}
\newtheorem*{hypothesis*}{Hypothesis}
\newtheorem{conjecture}[theorem]{Conjecture}


\theoremstyle{definition}
\newtheorem{definition}[theorem]{Definition}
\newtheorem{construction}[theorem]{Construction}
\newtheorem{example}[theorem]{Example}
\newtheorem{question}[theorem]{Question}
\newtheorem{openquestion}[theorem]{Open Question}
\newtheorem{algorithm}[theorem]{Algorithm}
\newtheorem{problem}[theorem]{Problem}
\newtheorem{protocol}[theorem]{Protocol}
\newtheorem{assumption}[theorem]{Assumption}
\newtheorem{exercise-easy}[theorem]{Exercise}
\newtheorem{exercise-med}[theorem]{Exercise}
\newtheorem{exercise-hard}[theorem]{Exercise$^\star$}
\newtheorem{claim}[theorem]{Claim}
\newtheorem*{claim*}{Claim}


%
\newtheorem{remark}[theorem]{Remark}
\newtheorem*{remark*}{Remark}
\newtheorem{observation}[theorem]{Observation}
\newtheorem*{observation*}{Observation}



%


%
\usepackage[
letterpaper,
top=1in,
bottom=1in,
left=1in,
right=1in]{geometry}

%
%
%
%
%
%


%

\ifnum\arxivmode=0
\usepackage{newpxtext} %
\usepackage{textcomp} %
\usepackage[varg,bigdelims]{newpxmath}
%
\usepackage[scr=rsfso]{mathalfa}%
\usepackage{bm} %
%
\linespread{1.00}%
\let\mathbb\varmathbb
%
%
%
\fi

\ifnum\arxivmode=1
\usepackage[varg]{pxfonts} %
\usepackage{textcomp} %
%
\usepackage[scr=rsfso]{mathalfa}%
\usepackage{bm} %
%
\linespread{1.08}%
%
%
%
%
\fi

%

\ifnum\showkeys=1
\usepackage[color]{showkeys}
\fi

%


\makeatletter
\@ifpackageloaded{hyperref}
{}
{\usepackage[pagebackref]{hyperref}}

\definecolor{bleudefrance}{rgb}{0.01, 0.1, 1.0}
\definecolor{azure}{rgb}{0.0, 0.5, 1.0}

\ifnum\showcolorlinks=1
\hypersetup{
pagebackref=true,
%
colorlinks=true,
urlcolor=blue,
linkcolor=blue,
citecolor=OliveGreen}
\fi

\ifnum\showcolorlinks=0
\hypersetup{
pagebackref=true,
%
colorlinks=false,
pdfborder={0 0 0}}
\fi


%
\usepackage{prettyref}

%
%
%
%
%
%
%
%

\newcommand{\savehyperref}[2]{\texorpdfstring{\hyperref[#1]{#2}}{#2}}

\newrefformat{eq}{\savehyperref{#1}{\textup{(\ref*{#1})}}}
\newrefformat{lem}{\savehyperref{#1}{Lemma~\ref*{#1}}}
\newrefformat{def}{\savehyperref{#1}{Definition~\ref*{#1}}}
\newrefformat{thm}{\savehyperref{#1}{Theorem~\ref*{#1}}}
\newrefformat{cor}{\savehyperref{#1}{Corollary~\ref*{#1}}}
\newrefformat{cha}{\savehyperref{#1}{Chapter~\ref*{#1}}}
\newrefformat{sec}{\savehyperref{#1}{Section~\ref*{#1}}}
\newrefformat{app}{\savehyperref{#1}{Appendix~\ref*{#1}}}
\newrefformat{tab}{\savehyperref{#1}{Table~\ref*{#1}}}
\newrefformat{fig}{\savehyperref{#1}{Figure~\ref*{#1}}}
\newrefformat{hyp}{\savehyperref{#1}{Hypothesis~\ref*{#1}}}
\newrefformat{alg}{\savehyperref{#1}{Algorithm~\ref*{#1}}}
\newrefformat{rem}{\savehyperref{#1}{Remark~\ref*{#1}}}
\newrefformat{item}{\savehyperref{#1}{Item~\ref*{#1}}}
\newrefformat{step}{\savehyperref{#1}{step~\ref*{#1}}}
\newrefformat{conj}{\savehyperref{#1}{Conjecture~\ref*{#1}}}
\newrefformat{fact}{\savehyperref{#1}{Fact~\ref*{#1}}}
\newrefformat{prop}{\savehyperref{#1}{Proposition~\ref*{#1}}}
\newrefformat{prob}{\savehyperref{#1}{Problem~\ref*{#1}}}
\newrefformat{ass}{\savehyperref{#1}{Assumption~\ref*{#1}}}
\newrefformat{claim}{\savehyperref{#1}{Claim~\ref*{#1}}}
\newrefformat{relax}{\savehyperref{#1}{Relaxation~\ref*{#1}}}
\newrefformat{red}{\savehyperref{#1}{Reduction~\ref*{#1}}}
\newrefformat{part}{\savehyperref{#1}{Part~\ref*{#1}}}
\newrefformat{ex}{\savehyperref{#1}{Exercise~\ref*{#1}}}
\newrefformat{property}{\savehyperref{#1}{Property~\ref*{#1}}}

%

%
\newcommand{\Sref}[1]{\hyperref[#1]{\S\ref*{#1}}}

%
%
\usepackage{nicefrac}
%
\newcommand{\flatfrac}[2]{#1/#2}
\newcommand{\varflatfrac}[2]{#1\textfractionsolidus#2}

\let\nfrac=\nicefrac
\let\ffrac=\flatfrac
%

\newcommand{\half}{\nicefrac12}
\newcommand{\onequarter}{\nicefrac14}
\newcommand{\threequarter}{\nicefrac34}




%

\ifnum\fastmode=0
\ifnum\usemicrotype=1
\usepackage{microtype}
\fi
\fi

%
\ifnum\showauthornotes=2
\newcommand{\mynotes}[1]{{\sffamily\small\color{teal}{#1}}\medskip}
\newcommand{\Authornote}[2]{{\sffamily\small\color{teal}{[#1: #2]}}\medskip}
\newcommand{\Authornotecolored}[3]{{\sffamily\small\color{#1}{[#2: #3]}}}
\newcommand{\Authorcomment}[2]{{\sffamily\small\color{gray}{[#1: #2]}}}
\newcommand{\Authorstartcomment}[1]{\sffamily\small\color{gray}[#1: }
\newcommand{\Authorendcomment}{]\rmfamily\normalsize\color{black}}
\newcommand{\Authorfnote}[2]{\footnote{\color{red}{#1: #2}}}
\newcommand{\Authorfixme}[1]{\Authornote{#1}{\textbf{??}}}
\newcommand{\Authormarginmark}[1]{\marginpar{\textcolor{red}{\fbox{\Large #1:!}}}}
\newcommand{\myexplain}[1]{{\sffamily\small\color{red}{\noindent [Explanation:\medskip\newline \begin{quote}#1\hfill]\end{quote}}}\medskip}
\newcommand{\explain}[1]{{\sffamily\small\color{red}{#1}}\medskip}

\else

\newcommand{\mynotes}[1]{}
\newcommand{\Authornote}[2]{}
\newcommand{\Authornotecolored}[3]{}
\newcommand{\Authorcomment}[2]{}
\newcommand{\Authorstartcomment}[1]{}
\newcommand{\Authorendcomment}{}
\newcommand{\Authorfnote}[2]{}
\newcommand{\Authorfixme}[1]{}
\newcommand{\Authormarginmark}[1]{}
\newcommand{\myexplain}[1]{}
\newcommand{\explain}[1]{}

\ifnum\showauthornotes=1
\renewcommand{\myexplain}[1]{{\sffamily\small\color{red}{\noindent \begin{quote}{\bf Explanation:} \medskip\newline #1\end{quote}}}\medskip}
\fi

\fi

\newcommand{\Dnote}{\Authornote{D}}
\newcommand{\Inote}{\Authornotecolored{ForestGreen}{I}}
\newcommand{\inote}{\Inote}
\newcommand{\Gnote}{\Authornote{G}}
\newcommand{\Jcomment}{\Authorcomment{J}}
\newcommand{\Dcomment}{\Authorcomment{D}}
\newcommand{\Dstartcomment}{\Authorstartcomment{D}}
\newcommand{\Dendcomment}{\Authorendcomment}
\newcommand{\Dfixme}{\Authorfixme{D}}
\newcommand{\Dmarginmark}{\Authormarginmark{D}}
\newcommand{\Dfnote}{\Authorfnote{D}}

\newcommand{\Pnote}{\Authornote{P}}
\newcommand{\Pfnote}{\Authorfnote{P}}

\newcommand{\PRnote}{\Authornote{PR}}
\newcommand{\PRfnote}{\Authorfnote{PR}}

\newcommand{\PTnote}{\Authornote{PT}}
\newcommand{\PTfnote}{\Authorfnote{PT}}

\newcommand{\PGnote}{\Authornote{PG}}
\newcommand{\PGfnote}{\Authorfnote{PG}}

\newcommand{\Bnote}{\Authornote{B}}
\newcommand{\Bfnote}{\Authorfnote{B}}

\newcommand{\Jnote}{\Authornote{J}}
\newcommand{\Jfnote}{\Authorfnote{J}}

\newcommand{\jnote}{\Authornote{J}}
\newcommand{\jfnote}{\Authorfnote{J}}

\newcommand{\Mnote}{\Authornote{M}}
\newcommand{\Mfnote}{\Authorfnote{M}}

\newcommand{\Rnote}{\Authornote{M}}
\newcommand{\Rfnote}{\Authorfnote{M}}

\newcommand{\Nnote}{\Authornote{N}}
\newcommand{\Nfnote}{\Authorfnote{N}}

\newcommand{\Snote}{\Authornote{S}}
\newcommand{\Sfnote}{\Authorfnote{S}}

%
%
%

%

%
%
\newcommand{\redmarginmarker}{}

%
\newcommand{\FIXME}{\textbf{\textcolor{red}{??}}\redmarginmarker}

\ifnum\showfixme=0
\renewcommand{\FIXME}{}
\fi


%
\usepackage{boxedminipage}

\newenvironment{mybox}
{\center \noindent\begin{boxedminipage}{1.0\linewidth}}
{\end{boxedminipage}
\noindent
}


%
%
%
\newcommand{\paren}[1]{(#1)}
\newcommand{\Paren}[1]{\left(#1\right)}
\newcommand{\bigparen}[1]{\big(#1\big)}
\newcommand{\Bigparen}[1]{\Big(#1\Big)}
%
\newcommand{\brac}[1]{[#1]}
\newcommand{\Brac}[1]{\left[#1\right]}
\newcommand{\bigbrac}[1]{\big[#1\big]}
\newcommand{\Bigbrac}[1]{\Big[#1\Big]}
%
\newcommand{\abs}[1]{\lvert#1\rvert}
\newcommand{\Abs}[1]{\left\lvert#1\right\rvert}
\newcommand{\bigabs}[1]{\big\lvert#1\big\rvert}
\newcommand{\Bigabs}[1]{\Big\lvert#1\Big\rvert}
\newcommand{\icost}{\mathsf{icost}}
\newcommand{\wt}[1]{\widetilde{#1}}
%
\newcommand{\card}[1]{\lvert#1\rvert}
\newcommand{\Card}[1]{\left\lvert#1\right\rvert}
\newcommand{\bigcard}[1]{\big\lvert#1\big\rvert}
\newcommand{\Bigcard}[1]{\Big\lvert#1\Big\rvert}
%
\newcommand{\set}[1]{\{#1\}}
\newcommand{\Set}[1]{\left\{#1\right\}}
\newcommand{\bigset}[1]{\big\{#1\big\}}
\newcommand{\Bigset}[1]{\Big\{#1\Big\}}
%
\newcommand{\norm}[1]{\lVert#1\rVert}
\newcommand{\Norm}[1]{\left\lVert#1\right\rVert}
\newcommand{\bignorm}[1]{\big\lVert#1\big\rVert}
\newcommand{\Bignorm}[1]{\Big\lVert#1\Big\rVert}
%
\newcommand{\normt}[1]{\norm{#1}_2}
\newcommand{\Normt}[1]{\Norm{#1}_2}
\newcommand{\bignormt}[1]{\bignorm{#1}_2}
\newcommand{\Bignormt}[1]{\Bignorm{#1}_2}
%
\newcommand{\snormt}[1]{\norm{#1}^2_2}
\newcommand{\Snormt}[1]{\Norm{#1}^2_2}
\newcommand{\bigsnormt}[1]{\bignorm{#1}^2_2}
\newcommand{\Bigsnormt}[1]{\Bignorm{#1}^2_2}
%
\newcommand{\snorm}[1]{\norm{#1}^2}
\newcommand{\Snorm}[1]{\Norm{#1}^2}
\newcommand{\bigsnorm}[1]{\bignorm{#1}^2}
\newcommand{\Bigsnorm}[1]{\Bignorm{#1}^2}
%
\newcommand{\normo}[1]{\norm{#1}_1}
\newcommand{\Normo}[1]{\Norm{#1}_1}
\newcommand{\bignormo}[1]{\bignorm{#1}_1}
\newcommand{\Bignormo}[1]{\Bignorm{#1}_1}
%
\newcommand{\normi}[1]{\norm{#1}_\infty}
\newcommand{\Normi}[1]{\Norm{#1}_\infty}
\newcommand{\bignormi}[1]{\bignorm{#1}_\infty}
\newcommand{\Bignormi}[1]{\Bignorm{#1}_\infty}
%
\newcommand{\iprod}[1]{\langle#1\rangle}
\newcommand{\Iprod}[1]{\left\langle#1\right\rangle}
\newcommand{\bigiprod}[1]{\big\langle#1\big\rangle}
\newcommand{\Bigiprod}[1]{\Big\langle#1\Big\rangle}


%
%
\newcommand{\Esymb}{\mathbb{E}}
\newcommand{\Psymb}{\mathbb{P}}
\newcommand{\Vsymb}{\mathbb{V}}

\DeclareMathOperator*{\E}{\Esymb}
\DeclareMathOperator*{\Var}{\Vsymb}
\DeclareMathOperator*{\ProbOp}{\Psymb}

\DeclareMathOperator*{\esssup}{ess\,sup}


\renewcommand{\Pr}{\ProbOp}

%
\newcommand{\prob}[1]{\Pr\set{#1}}
\newcommand{\Prob}[2][]{\Pr_{{#1}}\Set{#2}}

\newcommand{\ex}[1]{\E\brac{#1}}
\newcommand{\Ex}[2][]{\E_{{#1}}\Brac{#2}}
\newcommand{\varex}[1]{\E\paren{#1}}
\newcommand{\varEx}[1]{\E\Paren{#1}}

%
\newcommand{\given}{\mathrel{}\middle\vert\mathrel{}}
%

%

%
%
%


%

%
\newcommand{\suchthat}{\;\middle\vert\;}

%
\newcommand{\tensor}{\otimes}

%
\newcommand{\where}{\text{where}}
\newcommand{\textparen}[1]{\text{(#1)}}
\newcommand{\using}[1]{\textparen{using #1}}
\newcommand{\smallusing}[1]{\text{(\small using #1)}}
\ifx\because\undefined
\newcommand{\because}[1]{\textparen{because #1}}
\else
\renewcommand{\because}[1]{\textparen{because #1}}
\fi
\newcommand{\by}[1]{\textparen{by #1}}


%
\newcommand{\sge}{\succeq}
\newcommand{\sle}{\preceq}

%
\newcommand{\lmin}{\lambda_{\min}}
\newcommand{\lmax}{\lambda_{\max}}

\newcommand{\signs}{\set{1,-1}}
\newcommand{\varsigns}{\set{\pm 1}}
\newcommand{\maximize}{\mathop{\textrm{maximize}}}
\newcommand{\minimize}{\mathop{\textrm{minimize}}}
\newcommand{\subjectto}{\mathop{\textrm{subject to}}}

\renewcommand{\ij}{{ij}}

%
\newcommand{\symdiff}{\Delta}
\newcommand{\varsymdiff}{\bigtriangleup}

%
\newcommand{\bits}{\{0,1\}}
\newcommand{\sbits}{\{-1,1\}}

%
%

%
\newcommand{\listoptions}{\labelsep0mm\topsep-0mm\itemindent-6mm\itemsep0mm}
\newcommand{\displayoptions}[1]{\abovedisplayshortskip#1mm\belowdisplayshortskip#1mm\abovedisplayskip#1mm\belowdisplayskip#1mm}

%
%
%

%
%
%

%
\newcommand{\super}[2]{#1^{\paren{#2}}}
\newcommand{\varsuper}[2]{#1^{\scriptscriptstyle\paren{#2}}}

%
\newcommand{\tensorpower}[2]{#1^{\tensor #2}}


%
\newcommand{\inv}[1]{{#1^{-1}}}

%
\newcommand{\dual}[1]{{#1^*}}

%
%
%

%
\newcommand{\vbig}{\vphantom{\bigoplus}}

%
\newcommand{\sm}{\setminus}

%
\newcommand{\defeq}{\stackrel{\mathrm{def}}=}


%
\newcommand{\seteq}{\mathrel{\mathop:}=}



%
\newcommand{\from}{\colon}

%
\newcommand{\bigmid}{~\big|~}
\newcommand{\Bigmid}{~\Big|~}
\newcommand{\Mid}{\;\middle\vert\;}

%
%
\newcommand{\bvec}[1]{\bar{\vec{#1}}}
\newcommand{\pvec}[1]{\vec{#1}'}
\newcommand{\tvec}[1]{{\tilde{\vec{#1}}}}

%
\newcommand{\mper}{\,.}
\newcommand{\mcom}{\,,}

%
\newcommand\bdot\bullet

%
\newcommand{\trsp}[1]{{#1}^\dagger}

%
\ifx\mathds\undefined %
\newcommand{\Ind}{\mathbb I}
\else
\newcommand{\Ind}{\mathds 1}
\fi

%
%

%

\renewcommand{\th}{\textsuperscript{th}\xspace}
\newcommand{\st}{\textsuperscript{st}\xspace}
\newcommand{\nd}{\textsuperscript{nd}\xspace}
\newcommand{\rd}{\textsuperscript{rd}\xspace}


%
\DeclareMathOperator{\Inf}{Inf}
\DeclareMathOperator{\Tr}{Tr}
%
\DeclareMathOperator{\SDP}{SDP}
\DeclareMathOperator{\sdp}{sdp}
\DeclareMathOperator{\val}{val}
\DeclareMathOperator{\LP}{LP}
\DeclareMathOperator{\OPT}{OPT}
\DeclareMathOperator{\opt}{opt}
\DeclareMathOperator{\vol}{vol}
\DeclareMathOperator{\poly}{poly}
\DeclareMathOperator{\qpoly}{qpoly}
\DeclareMathOperator{\qpolylog}{qpolylog}
\DeclareMathOperator{\qqpoly}{qqpoly}
\DeclareMathOperator{\argmax}{argmax}
\DeclareMathOperator{\polylog}{polylog}
\DeclareMathOperator{\supp}{supp}
\DeclareMathOperator{\dist}{dist}
\DeclareMathOperator{\sign}{sign}
\DeclareMathOperator{\conv}{conv}
\DeclareMathOperator{\Conv}{Conv}

\DeclareMathOperator{\rank}{rank}

%
\DeclareMathOperator*{\median}{median}
\DeclareMathOperator*{\Median}{Median}

%
\DeclareMathOperator*{\varsum}{{\textstyle \sum}}
\DeclareMathOperator{\tsum}{{\textstyle \sum}}

\let\varprod\undefined

\DeclareMathOperator*{\varprod}{{\textstyle \prod}}
\DeclareMathOperator{\tprod}{{\textstyle \prod}}




%

\newcommand{\diffmacro}[1]{\,\mathrm{d}#1}

\newcommand{\dmu}{\diffmacro{\mu}}
\newcommand{\dgamma}{\diffmacro{\gamma}}
\newcommand{\dlambda}{\diffmacro{\lambda}}
\newcommand{\dx}{\diffmacro{x}}
\newcommand{\dt}{\diffmacro{t}}



%

%
\newcommand{\ie}{i.e.,\xspace}
\newcommand{\eg}{e.g.,\xspace}
\newcommand{\Eg}{E.g.,\xspace}
\newcommand{\phd}{Ph.\,D.\xspace}
\newcommand{\msc}{M.\,S.\xspace}
\newcommand{\bsc}{B.\,S.\xspace}

\newcommand{\etal}{et al.\xspace}

\newcommand{\iid}{i.i.d.\xspace}

%

\newcommand\naive{na\"{\i}ve\xspace}
\newcommand\Naive{Na\"{\i}ve\xspace}
\newcommand\naively{na\"{\i}vely\xspace}
\newcommand\Naively{Na\"{\i}vely\xspace}



%
%
\newcommand{\Erdos}{Erd\H{o}s\xspace}
\newcommand{\Renyi}{R\'enyi\xspace}
\newcommand{\Lovasz}{Lov\'asz\xspace}
\newcommand{\Juhasz}{Juh\'asz\xspace}
\newcommand{\Bollobas}{Bollob\'as\xspace}
\newcommand{\Furedi}{F\"uredi\xspace}
\newcommand{\Komlos}{Koml\'os\xspace}
\newcommand{\Luczak}{\L uczak\xspace}
\newcommand{\Kucera}{Ku\v{c}era\xspace}
\newcommand{\Szemeredi}{Szemer\'edi\xspace}
\newcommand{\Hastad}{H{\aa}stad\xspace}
\newcommand{\Hoelder}{H\"{o}lder\xspace}
\newcommand{\Holder}{\Hoelder}
\newcommand{\Brandao}{Brand\~ao\xspace}


%
%
\newcommand{\Z}{\mathbb Z}
\newcommand{\N}{\mathbb N}
\newcommand{\R}{\mathbb R}
\newcommand{\C}{\mathbb C}
\newcommand{\Rnn}{\R_+}
\newcommand{\varR}{\Re}
\newcommand{\varRnn}{\varR_+}
\newcommand{\varvarRnn}{\R_{\ge 0}}


%

%

%
%
\newcommand{\problemmacro}[1]{\texorpdfstring{\textup{\textsc{#1}}}{#1}\xspace}

\newcommand{\pnum}[1]{{\footnotesize #1}}

%
\newcommand{\ug}{\problemmacro{UG}}
\newcommand{\uniquegames}{\problemmacro{unique games}}
\newcommand{\maxcut}{\problemmacro{max cut}}
\newcommand{\multicut}{\problemmacro{multi cut}}
\newcommand{\vertexcover}{\problemmacro{vertex cover}}
\newcommand{\balancedseparator}{\problemmacro{balanced separator}}
\newcommand{\maxtwosat}{\problemmacro{max \pnum{3}-sat}}
\newcommand{\maxthreesat}{\problemmacro{max \pnum{3}-sat}}
\newcommand{\maxthreelin}{\problemmacro{max \pnum{3}-lin}}
\newcommand{\threesat}{\problemmacro{\pnum{3}-sat}}
\newcommand{\labelcover}{\problemmacro{label cover}}
\newcommand{\setcover}{\problemmacro{set cover}}
\newcommand{\maxksat}{\problemmacro{max $k$-sat}}
\newcommand{\mas}{\problemmacro{maximum acyclic subgraph}}
\newcommand{\kwaycut}{\problemmacro{$k$-way cut}}
\newcommand{\sparsestcut}{\problemmacro{sparsest cut}}
\newcommand{\betweenness}{\problemmacro{betweenness}}
\newcommand{\uniformsparsestcut}{\problemmacro{uniform sparsest cut}}
\newcommand{\grothendieckproblem}{\problemmacro{Grothendieck problem}}
\newcommand{\maxfoursat}{\problemmacro{max \pnum{4}-sat}}
\newcommand{\maxkcsp}{\problemmacro{max $k$-csp}}
\newcommand{\maxdicut}{\problemmacro{max dicut}}
\newcommand{\maxcutgain}{\problemmacro{max cut gain}}
\newcommand{\smallsetexpansion}{\problemmacro{small-set expansion}}
\newcommand{\minbisection}{\problemmacro{min bisection}}
\newcommand{\minimumlineararrangement}{\problemmacro{minimum linear arrangement}}
\newcommand{\maxtwolin}{\problemmacro{max \pnum{2}-lin}}
\newcommand{\gammamaxlin}{\problemmacro{$\Gamma$-max \pnum{2}-lin}}
\newcommand{\basicsdp}{\problemmacro{basic sdp}}
\newcommand{\dgames}{\problemmacro{$d$-to-1 games}}
\newcommand{\maxclique}{\problemmacro{max clique}}
\newcommand{\densestksubgraph}{\problemmacro{densest $k$-subgraph}}


%

\newcommand{\cA}{\mathcal A}
\newcommand{\cB}{\mathcal B}
\newcommand{\cC}{\mathcal C}
\newcommand{\cD}{\mathcal D}
\newcommand{\cE}{\mathcal E}
\newcommand{\cF}{\mathcal F}
\newcommand{\cG}{\mathcal G}
\newcommand{\cH}{\mathcal H}
\newcommand{\cI}{\mathcal I}
\newcommand{\cJ}{\mathcal J}
\newcommand{\cK}{\mathcal K}
\newcommand{\cL}{\mathcal L}
\newcommand{\cM}{\mathcal M}
\newcommand{\cN}{\mathcal N}
\newcommand{\cO}{\mathcal O}
\newcommand{\cP}{\mathcal P}
\newcommand{\cQ}{\mathcal Q}
\newcommand{\cR}{\mathcal R}
\newcommand{\cS}{\mathcal S}
\newcommand{\cT}{\mathcal T}
\newcommand{\cU}{\mathcal U}
\newcommand{\cV}{\mathcal V}
\newcommand{\cW}{\mathcal W}
\newcommand{\cX}{\mathcal X}
\newcommand{\cY}{\mathcal Y}
\newcommand{\cZ}{\mathcal Z}

\newcommand{\sfA}{\mathsf A}
\newcommand{\sfB}{\mathsf B}
\newcommand{\sfC}{\mathsf C}
\newcommand{\sfD}{\mathsf D}
\newcommand{\sfE}{\mathsf E}
\newcommand{\sfF}{\mathsf F}
\newcommand{\sfG}{\mathsf G}
\newcommand{\sfH}{\mathsf H}
\newcommand{\sfI}{\mathsf I}
\newcommand{\sfJ}{\mathsf J}
\newcommand{\sfK}{\mathsf K}
\newcommand{\sfL}{\mathsf L}
\newcommand{\sfM}{\mathsf M}
\newcommand{\sfN}{\mathsf N}
\newcommand{\sfO}{\mathsf O}
\newcommand{\sfP}{\mathsf P}
\newcommand{\sfQ}{\mathsf Q}
\newcommand{\sfR}{\mathsf R}
\newcommand{\sfS}{\mathsf S}
\newcommand{\sfT}{\mathsf T}
\newcommand{\sfU}{\mathsf U}
\newcommand{\sfV}{\mathsf V}
\newcommand{\sfW}{\mathsf W}
\newcommand{\sfX}{\mathsf X}
\newcommand{\sfY}{\mathsf Y}
\newcommand{\sfZ}{\mathsf Z}

\newcommand{\scrA}{\mathscr A}
\newcommand{\scrB}{\mathscr B}
\newcommand{\scrC}{\mathscr C}
\newcommand{\scrD}{\mathscr D}
\newcommand{\scrE}{\mathscr E}
\newcommand{\scrF}{\mathscr F}
\newcommand{\scrG}{\mathscr G}
\newcommand{\scrH}{\mathscr H}
\newcommand{\scrI}{\mathscr I}
\newcommand{\scrJ}{\mathscr J}
\newcommand{\scrK}{\mathscr K}
\newcommand{\scrL}{\mathscr L}
\newcommand{\scrM}{\mathscr M}
\newcommand{\scrN}{\mathscr N}
\newcommand{\scrO}{\mathscr O}
\newcommand{\scrP}{\mathscr P}
\newcommand{\scrQ}{\mathscr Q}
\newcommand{\scrR}{\mathscr R}
\newcommand{\scrS}{\mathscr S}
\newcommand{\scrT}{\mathscr T}
\newcommand{\scrU}{\mathscr U}
\newcommand{\scrV}{\mathscr V}
\newcommand{\scrW}{\mathscr W}
\newcommand{\scrX}{\mathscr X}
\newcommand{\scrY}{\mathscr Y}
\newcommand{\scrZ}{\mathscr Z}

\newcommand{\bbB}{\mathbb B}
\newcommand{\bbS}{\mathbb S}
\newcommand{\bbR}{\mathbb R}
\newcommand{\bbZ}{\mathbb Z}
\newcommand{\bbI}{\mathbb I}
\newcommand{\bbQ}{\mathbb Q}
\newcommand{\bbP}{\mathbb P}
\newcommand{\bbE}{\mathbb E}

%
%
\renewcommand{\leq}{\leqslant}
\renewcommand{\le}{\leqslant}
\renewcommand{\geq}{\geqslant}
\renewcommand{\ge}{\geqslant}


%
\ifnum\showdraftbox=1
\newcommand{\draftbox}{\begin{center}
  \fbox{%
    \begin{minipage}{2in}%
      \begin{center}%
%
          \Large\textsc{Working Draft}\\%
%
        Please do not distribute%
      \end{center}%
    \end{minipage}%
  }%
\end{center}
\vspace{0.2cm}}
\else
\newcommand{\draftbox}{}
\fi


%

\let\epsilon=\varepsilon

%
\numberwithin{equation}{section}


%
%
%

%

\newcommand\MYcurrentlabel{xxx}

%
\newcommand{\MYstore}[2]{%
  \global\expandafter \def \csname MYMEMORY #1 \endcsname{#2}%
}

%
\newcommand{\MYload}[1]{%
  \csname MYMEMORY #1 \endcsname%
}

%
\newcommand{\MYnewlabel}[1]{%
  \renewcommand\MYcurrentlabel{#1}%
  \MYoldlabel{#1}%
}

%
\newcommand{\MYdummylabel}[1]{}

\newcommand{\torestate}[1]{%
  %
  \let\MYoldlabel\label%
  \let\label\MYnewlabel%
  #1%
  \MYstore{\MYcurrentlabel}{#1}%
  %
  \let\label\MYoldlabel%
}

\newcommand{\restatetheorem}[1]{%
  %
  \let\MYoldlabel\label
  \let\label\MYdummylabel
  \begin{theorem*}[Restatement of \prettyref{#1}]
    \MYload{#1}
  \end{theorem*}
  \let\label\MYoldlabel
}

\newcommand{\restatelemma}[1]{%
  %
  \let\MYoldlabel\label
  \let\label\MYdummylabel
  \begin{lemma*}[Restatement of \prettyref{#1}]
    \MYload{#1}
  \end{lemma*}
  \let\label\MYoldlabel
}

\newcommand{\restateprop}[1]{%
  %
  \let\MYoldlabel\label
  \let\label\MYdummylabel
  \begin{proposition*}[Restatement of \prettyref{#1}]
    \MYload{#1}
  \end{proposition*}
  \let\label\MYoldlabel
}

\newcommand{\restatefact}[1]{%
  %
  \let\MYoldlabel\label
  \let\label\MYdummylabel
  \begin{fact*}[Restatement of \prettyref{#1}]
    \MYload{#1}
  \end{fact*}
  \let\label\MYoldlabel
}

\newcommand{\restate}[1]{%
  %
  \let\MYoldlabel\label
  \let\label\MYdummylabel
  \MYload{#1}
  \let\label\MYoldlabel
}


%

%
\newcommand{\addreferencesection}{
  \phantomsection
\ifnum\stocmode=0
  \addcontentsline{toc}{section}{References}
\else
  \addcontentsline{toc}{section}{References \hspace*{1in} --------- End of extended abstract ---------}
\fi

}


%

\newcommand{\la}{\leftarrow}
\newcommand{\sse}{\subseteq}
\newcommand{\ra}{\rightarrow}
\newcommand{\e}{\epsilon}
\newcommand{\eps}{\epsilon}
\newcommand{\eset}{\emptyset}


%

\let\origparagraph\paragraph
\renewcommand{\paragraph}[1]{\vspace*{-8pt}\origparagraph{#1.}}


%
%

\allowdisplaybreaks


%
%

\sloppy



%

\newcommand{\cclassmacro}[1]{\texorpdfstring{\textbf{#1}}{#1}\xspace}
\newcommand{\p}{\cclassmacro{P}}
\newcommand{\np}{\cclassmacro{NP}}
\newcommand{\subexp}{\cclassmacro{SUBEXP}}

%

\usepackage{paralist}

%

\usepackage{comment}
\usepackage{subfigure}
 %

%

\let\pref=\prettyref

\renewcommand{\Vsymb}{\mathrm{Var}}

%

\newcommand{\auxdisc}{\hat{\mathsf{D}}}


\newcommand{\PP}{\mathfrak{P}}
\newcommand{\sos}{\mathsf{sos}}
\newcommand{\cone}{\mathrm{cone}}
\newcommand{\gap}{\mathrm{gap}}
\let\super\varsuper
\newcommand{\ML}[2]{\mathrm{\cQ}^{#2}_{#1}}
\newcommand*{\id}{\mathrm{id}}
\newcommand{\Cay}{\mathsf{Cay}}
\newcommand{\var}{\mathrm{Var}}
\newcommand{\cov}{\mathrm{Cov}}
\newcommand{\diam}{\mathrm{diam}}
\newcommand{\dmid}{\,\|\,}
\newcommand{\D}{\mathsf{D}}
\DeclareMathOperator{\tr}{tr}
\newcommand{\Lone}[1]{\left\|#1\right\|_1}
\newcommand{\Linf}[1]{\left\|#1\right\|_{\infty}}

\newcommand{\vertiii}[1]{{\left\vert\kern-0.25ex\left\vert\kern-0.25ex\left\vert #1 
          \right\vert\kern-0.25ex\right\vert\kern-0.25ex\right\vert}}

\newcommand*{\qe}[2]{S(#1\,\|\, #2)}
\newcommand*{\ce}[2]{D(#1\,\|\, #2)}

\newcommand*{\sst}{\substack}
\renewcommand{\Ind}{\vvmathbb{1}}
\ifnum\jamesmode=0
%
\fi
\let\1\Ind

\newcommand*{\hi}{\mathsf{high}}
\newcommand*{\low}{\mathsf{low}}

\newcommand*{\inst}{\Im}
\newcommand*{\GF}[1]{\mathbb F_{#1}}

\newcommand\f{\varphi}
\newcommand{\F}{\mathcal F}
\newcommand{\OR}{\ensuremath{\mathsf{OR}}}
\newcommand*{\gtwo}{\gamma_{2\to 2}^{\mathsf{psd}}}
\newcommand*{\psdrank}{\mathrm{rank}_{\mathsf{psd}}}
\newcommand*{\psdalpha}{\alpha_{\mathsf{psd}}}
\newcommand*{\nnalpha}{\alpha_{+}}
\newcommand{\psd}{\mathsf{psd}}
\newcommand*{\apsdrank}{\rho_{\mathsf{psd}}}
\newcommand*{\nnrank}{\mathrm{rank}_{+}}
\newcommand*{\sosdeg}{\deg_{\mathsf{sos}}}
\newcommand*{\juntadeg}{\deg_{+}}

\newcommand{\polytope}[1]{\text{\textup{\textsc{#1}}}}

\newcommand*{\corr}{\polytope{corr}}
\newcommand*{\tsp}{\polytope{tsp}}
\newcommand*{\cut}{\mathsf{cut}}
\newcommand*{\stab}{\polytope{stab}}

\newcommand*{\ot}{\otimes}
\newcommand*{\pmo}{\{\pm 1\}}


\newcommand*{\maxpi}{\problemmacro{max-$\Pi$}}
\newcommand*{\maxscrP}{\problemmacro{max-$\scrP$}}
\newcommand*{\maxthreecnf}{\problemmacro{max \pnum{3}-cnf}}


%

\newcommand*{\sleq}{\preceq}
\newcommand*{\sgeq}{\succeq}

\DeclareMathOperator{\Id}{\mathrm{Id}}
\DeclareMathOperator{\argmin}{\mathrm{argmin}}
%

\DeclareMathOperator{\pE}{\tilde {\mathbb E}}

%

%
\newcommand*{\uId}{\mathcal{U}}

\newcommand*{\annotaterel}[2]{\stackrel{\scriptscriptstyle\text{#1}}{#2}}
\newcommand{\rootT}{\vvr_{\vvT}}

%
%
%
%
 
\renewcommand{\R}{\vvmathbb{R}}

\setcounter{page}{1}

\usepackage{enumitem}
\usepackage[toc]{appendix}


\begin{document}

\linespread{1.08}
%\setlength{\parskip}{1pt}
\setlength{\parskip}{7pt}%
\setlength{\parindent}{0pt}%

\section{Optimization in the face of uncertainty}

The rise of machine learning in recent decades
has generated a renewed interest in online decision-making,
where algorithms are
equipped only with partial information about the world,
and must take actions in the face of uncertainty about the future.
There are various ways to analyze how much the presence 
of uncertainty 
degrades optimization.  Two of the most general models
are ``probability free'' (aka ``worst-case,'' or ``adversarial''),
in the sense that one can measure the performance of algorithms
without making distributional assumptions on the input.

\paragraph{Competitive analysis}

One such model goes by the name of {\em competitive analysis,}
% https://en.wikipedia.org/wiki/Competitive_analysis_(online_algorithm)
and has been studied in theoretical CS since the 1970s.
% https://dl.acm.org/citation.cfm?id=2793
Imagine, for instance, that one maintains a binary search tree (BST)
with key-value pairs at the nodes.
At every point in time, a key is requested, and
the corresponding value is looked up via binary search.
Along the search path, the algorithm is allowed to modify the
tree using standard tree rotation operations.
% https://en.wikipedia.org/wiki/Tree_rotation

The cost of such an algorithm is the average number
of binary search steps per key-lookup over a long sequence
of requests.
To minimize the cost, it is beneficial for the algorithm
to dynamically rebalance the tree so that frequently-requested
keys are near the root.  Sleator and Tarjan had this
model in mind when they invented the {\em Splay Tree}
data structure.
Their (still unproven) {\em Dynamic Optimality Conjecture}
asserts that, for every sequence of key requests,
the number of operations used by the Splay Tree
is within a constant factor of the number of operations
used by {\em any binary search tree,}
even an {\em offline} algorithm that is allowed to see
the entire sequence of key requests in advance.
(This is a very strong requirement!  We make no assumption
on the structure of the request sequence, and have to compare
our performance to an algorithm that sees the entire
request sequence up front.)

In the language of competitive analysis, the conjecture 
states that the Splay Tree algorithm is "competitive."
In general, an {\em $\alpha$-competitive} online algorithm
is one whose total cost on every input sequence
is within an $\alpha$ factor of the cost incurred by the optimal {\em offline algorithm}
that sees the whole input sequence in advance.

\paragraph{Multi-arm bandits}

Another compelling model arising in online learning
is the {\em multi-armed bandit problem.}
Here, an agent has a set $\cA$ of feasible actions.
At time $t=1,2,3,\ldots$, the agent plays an action $a_t \in \cA$,
and only then the cost of that action is revealed.
Imagine, for instance, 
choosing an advertisement $a_t \in \cA$ to present to a user,
and then learning afterward the probability it
led to a sale.
The goal of an algorithm in this model is to achieve
a total cost (often called the {\em loss}) that
is not too much worse than the best {\em fixed} action
in hindsight.  The gap between the two is called the {\em regret.}

At first blush, it may seem that these two models (multi-arm bandits and competitive analysis)
are quite different.  But their relationship rests on a common theme
in machine learning:  The intimate connection between stability and generalization.
A competitive binary search tree algorithm aspires to be {\em stable}
in the sense that the search tree changes little between lookups
because the requested key is often near the root.
A low-regret advertiser aspires for her decisions to {\em generalize}
in the sense that her past observations about users
are predictive of their future actions.

\paragraph{Hedging and entropic regularization}

A fundamental feature of algorithms
designed in both models is {\em hedging,} i.e., making 
decisions now that protect against the cost of uncertainty in future inputs.
In the bandit model, where one only learns the cost associated to the
action played, hedging involves exploring the action space
(the cost protected against here is opportunity cost).
In competitive analysis, one can think of hedging as maintaining a state
that avoids exploitation by an adversary.  For instance, if there are $10$ keys
that are very frequently requested in a BST, hedging might involve a preference
for a configuration in which all $10$ keys are within distance $100$ of the root,
rather than a configuration in which $9$ keys are within distance $3$ and the $10$th key
is at distance $1000$.  This might be preferable even if those $9$ keys are requested
twice as often as the $10$th.

In these settings, hedging is a tradeoff between cost (or utility)
and entropy.
In modern play of no-limit Texas hold 'em, this tradeoff is now
explicit in the vernacular.  Poker players talk of "balancing
their range."  For instance, it generally makes sense to bet with strong hands,
and even to bet more as a hand gets stronger.  But a player has to
weigh this against their loss in entropy (from the perspective of an observer
who does not know their hole cards):
If I only go all-in before the flop
with aces, my opponent will be able to play optimally against me whenever
that occurs.

The idea of adding an entropic regularizer to the cost function
has played a central (and rather explicit) role in online learning.
The possible application of these ideas to competitive analysis
was already suggested in work of Blum and Burch (2000) and
more recently in a paper conceived at Berkeley by Abernethy,
Barlett, Buchbinder, and Stanton (2010).
Those early attempts, while prescient,
were not able to yield better general
approaches for the classical problems in online algorithms.

But a collaboration seeded at the Simons Institute,
and spanning from the Algorithmic Spectral Graph Theory program (Fall 2014)
to the Continuous and Discrete Optimization problem three years later was key
in developing a theory of entropic regularization suited to competitive analysis,
and leading to the resolution of some long-standing open problems in the field.

%A connection between these two frameworks was explored by Blum and Birch (2000)
%and Abernethy, Barlett, Buchbinder, and Stanton (2010).
%By exploring its true power and mirror descent / convex optimization,
%one can resolve some long-standing open problems in competitive analysis.

%\paragraph{Entropic regularization, hedging, and poker}
%
%The key tool is mirror descent and entropic regularization:  Hedging.
%One example is multiplicative weights update, but the theory is remarkably general.

%\subsection{Taks vs. bandits}
%
%A general problem arising from a long line
%of work on paging and caching
%goes by the name of {\em Metrical Task Systems (MTS),} 
%introduced in 1992 by Borodin, Linial, and Saks.
%
%Roughly speaking, in this framework there is a set $\cA$ of feasible actions.
%At each point in time, the algorithm receives a cost function $c_t$,
%decides on an action $a_t \in \cA$, and incurs the cost $c_t(a_t)$.
%Moreover, there is a {\em switching cost} $d(a_{t-1},a_t)$ incured by
%changing actions from $a_{t-1}$ to $a_t$.

%% http://www.cs.huji.ac.il/~nati/PAPERS/bls_online.pdf
%In MTS, one has a set $\cA$ of feasible actions
%and a metric $d$ on $\cA$, where $d(a,a')$
%describes the cost of switching between two actions $a,a' \in \cA$.
%At each time $t=1,2,3,\ldots$, a cost function $c_t : \cA \to \R_+$
%arrives online, and the algorithm then plays an action $a_t \in \cA$.
%The objective is to minimize the sum of the {\em service cost} and the {\em movement cost:}
%\[
%   \sum_{t=1}^T c_t(a_t) + d(a_{t-1},a_t)\,.
%\]
%(One fixes an arbitrary initial state $a_0 \in \cA$.)

%In competitive analysis, we compare the total cost of our algorithm
%to the total cost of the {\em best offline algorithm} that is able to see
%the entire sequence $c_1,c_2,\ldots,c_T$ of cost functions in advance.
%Roughly speaking, an algorithm is {\em $\alpha$-competitive} if it pays only an $\alpha$-factor
%more than the optimum offline algorithm for any cost sequence (averaged
%over a long enough period of time).
%
%Another compelling model arising in online learning goes by the name of {\em multi-arm bandits.}
%The setup is very similar to MTS, except that (i) there are no switching costs, and
%(ii) one has to play the action $a_t \in \cA$ {\em before learning the cost function} $c_t$ (the
%costs are often called {\em regrets} in this framework).
%In the standard adversarial
%setup, only the value $c_t(a_t)$ is revealed, and the costs
%are restricted to the interval $[0,1]$.
%Here one aims for a stronger additive guarantee on the total cost,
%but the goal is that our dynamic algorithm (allowed to change actions at every step)
%needs to be comparable to the best {\em fixed} strategy $a \in \cA$.
%See the discussion here: \verb|http://blog.tcsmath.org/online/2018/04/01/competitive-analysis/|
%and the references therin.

%At first, it may seem the two models are quite different, but their relationship rests on
%a common theme in machine learning:  The intimate connection between stability
%and generalization.
%% https://www.offconvex.org/2016/03/14/stability/
%At a high level, the MTS model rewards an algorithm for being stable
%(since then the movement cost is small).  On the other hand, the bandits model
%rewards an algorithm for being general:  The action $a_t$ is based on the observed
%costs $c_1(a_1), c_2(a_2), \ldots, c_{t-1}(a_{t-1})$, but the algorithm's goal
%is that $a_t$ is cheap for the the as-of-yet-unknown cost function $c_t$.
%(This encourages the algorithm to choose an action $a_t$ so that $c(a_t)$
%is small for a large fraction of the "expected" cost functions $c$.)
%
%A fruitful connection between these two models
%is suggested in a paper of Abernethy, Barlett, Buchbinder, and Stanton.
%% https://link.springer.com/chapter/10.1007/978-3-642-16108-7_23
%As we will see, exploiting this connection fully
%leads to a breakthrough for one of the most
%famous open problems in competitive analysis.

%\subsection{The $k$-server problem}
%
%By specializing the cost functions and the metric $d$ in MTS, one
%obtains an array of interesting problems.
%Perhaps the most famous is the {\em $k$-server problem:}
%There is a metric space $(X,d)$ and located in the space are $k$ servers 
%sitting at points $\sigma_1, \sigma_2, \ldots, \sigma_k \in X$.
%At time $t$, a request $\rho_t \in X$ arrives, and an online algorithm
%must move one of its servers to the location $\rho_t$ (unless one
%is already there).  The algorithm pays the sum of the movement costs
%of the servers over all time steps.


\end{document}
