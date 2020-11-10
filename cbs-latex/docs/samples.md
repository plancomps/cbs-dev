---
title: Samples
mathjax: true
---

# Samples
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

The $$\LaTeX$$ markup, embedded in Markdown, is to be generated from plain CBS specifications using Spoofax.
Before implementing it, an editor was used to transform two plain text specifications from CBS-beta into the intended markup.

The resulting web rendering is shown below.
Right-clicking on a displayed formula shows the $$\LaTeX$$ markup.

> All the syntax and semantics names below are linked to their (local or online) declarations, but links for funcon names are generally omitted.
>
> Local links are not yet working properly (partly due to an obscure MathJax issue),

## Language "SIMPLE"

### Statements

$$
\newcommand{\KEY}[1]{\text{\color{Gray}\mit{#1}\;\;}}
\newcommand{\VAR}[1]{\mathit{\small#1}\mspace2mu}
\newcommand{\LEX}[1]{\mathtt{#1}}
\newcommand{\LBRACE}{\unicode{x007b}}
\newcommand{\RBRACE}{\unicode{x007d}}
\newcommand{\STRING}[1]{\mathtt{\unicode{x201c}#1\unicode{x201d}}}
\newcommand{\ATOM}[1]{\mathtt{\unicode{x2018}#1\unicode{x2019}}}

\newcommand{\NAME}[2][\PLAIN]{#1{Name_#2}{\text{\color{Mahogany}#2}}}
\newcommand{\SYN}[2][\PLAIN]{#1{SyntaxName_#2}{\text{\color{ForestGreen}#2}}}
\newcommand{\SEM}[2][\PLAIN]{#1{SemanticsName_#2}{\text{\color{Blue}#2}}}

\newcommand{\PLAIN}[1]{}
\newcommand{\DECL}[1]{\cssId{#1}}
\newcommand{\REF}[1]{\href{samples.html\##1}}
\newcommand{\HYPER}[2]{#1{#2}}

\newcommand{\GROUP}[1]{ {\color{Gray}(} #1 {\color{Gray})} }
\newcommand{\MID}{\mathbin{|}}
\newcommand{\PLUS}{^{\text{\bf+}}}
\newcommand{\STAR}{^{\boldsymbol{\ast}}}
\newcommand{\QUERY}{^{\text{\bf?}}}
\newcommand{\PHRASE}[1]{[\![\, #1 \,]\!]}

\newcommand{\RULE}[2]{\frac{#1}{#2}}
\newcommand{\AXIOM}[1]{\begin{aligned}#1\end{aligned}}
\newcommand{\TO}{\mathop{\Rightarrow}}
\newcommand{\TRANS}{\longrightarrow}

\newcommand{\LanguagesSIMPLE}[2]{\href{https://plancomps.github.io/CBS-beta/Languages-beta/SIMPLE/SIMPLE-cbs/SIMPLE/SIMPLE-#1\##2}}
\newcommand{\FunconsFlowing}[1]{\href{https://plancomps.github.io/CBS-beta/Funcons-beta/Computations/Normal/Flowing\##1}}
\newcommand{\FunconsBinding}[1]{\href{samples.html\##1}}

\begin{alignat*}{2}
\KEY{Syntax}
  \VAR{Block} & : \SYN[\DECL]{block} & ::= ~ & \LEX{\LBRACE} ~ \SYN[\REF]{stmts}\QUERY ~ \LEX{\RBRACE}
\\
  \VAR{Stmts} & : \SYN[\DECL]{stmts} & ::= ~ & \SYN[\REF]{stmt} ~ \SYN[\REF]{stmts}\QUERY
\\
  \VAR{Stmt} & : \SYN[\DECL]{stmt} & ::= ~ & \SYN[\REF]{imp-stmt} \MID \SYN[\HYPER{\LanguagesSIMPLE{4-Declarations}}]{vars-decl}
\\
  \VAR{ImpStmt} & : \SYN[\DECL]{imp-stmt} & ::= ~ & \SYN[\REF]{block} \\
    & & \MID ~ & \SYN[\HYPER{\LanguagesSIMPLE{2-Expressions}}]{exp} ~ \LEX{;} \\
    & & \MID ~ & \LEX{if} ~ \LEX{(} ~ \SYN[\HYPER{\LanguagesSIMPLE{2-Expressions}}]{exp} ~ \LEX{)} ~ \SYN[\REF]{block} ~ \GROUP{ \LEX{else} ~ \SYN[\REF]{block} }\QUERY \\
    & & \MID ~ & \LEX{while} ~ \LEX{(} ~ \SYN[\HYPER{\LanguagesSIMPLE{2-Expressions}}]{exp} ~ \LEX{)} ~ \SYN[\REF]{block} \\
    & & \MID ~ & \LEX{for} ~ \LEX{(} ~ \SYN[\REF]{stmt} ~ \SYN[\HYPER{\LanguagesSIMPLE{2-Expressions}}]{exp} ~ \LEX{;} ~ \SYN[\HYPER{\LanguagesSIMPLE{2-Expressions}}]{exp} ~ \LEX{)} ~ \SYN[\REF]{block} \\
    & & \MID ~ & \LEX{print} ~ \LEX{(} ~ \SYN[\HYPER{\LanguagesSIMPLE{2-Expressions}}]{exps} ~ \LEX{)} ~ \LEX{;} \\
    & & \MID ~ & \LEX{return} ~ \SYN[\HYPER{\LanguagesSIMPLE{2-Expressions}}]{exp}\QUERY ~ \LEX{;} \\
    & & \MID ~ & \LEX{try} ~ \SYN[\REF]{block} ~ \LEX{catch} ~ \LEX{(} ~ \SYN[\HYPER{\LanguagesSIMPLE{1-Lexical}}]{id} ~ \LEX{)} ~ \SYN[\REF]{block} \\
    & & \MID ~ & \LEX{throw} ~ \SYN[\HYPER{\LanguagesSIMPLE{2-Expressions}}]{exp} ~ \LEX{;}
\end{alignat*}
$$

*SVG bug:* The link on $$\SYN[\REF]{imp-stmt}$$ is displayed incorrectly in the production for $$\SYN{stmt}$$ above.

$$
\begin{align*}
\KEY{Rule}
  \PHRASE{ \LEX{if} ~ \LEX{(} ~ \VAR{Exp} ~ \LEX{)} ~ \VAR{Block} } : \SYN[\REF]{stmt} =
  \PHRASE{ \LEX{if} ~ \LEX{(} ~ \VAR{Exp} ~ \LEX{)} ~ \VAR{Block} ~ \LEX{else} ~ \LEX{\LBRACE} ~ \LEX{\RBRACE} }
\end{align*}
$$

$$
\begin{align*}
\KEY{Rule}
  & \PHRASE{ \LEX{for} ~ \LEX{(} ~ \VAR{Stmt} ~ \VAR{Exp}_1 ~ \LEX{;} ~ \VAR{Exp}_2 ~ \LEX{)} ~
       \LEX{\LBRACE} ~ \VAR{Stmts} ~ \LEX{\RBRACE} } : \SYN[\REF]{stmt} = \\
  & \PHRASE{ \LEX{\LBRACE} ~ \VAR{Stmt} ~~
         \LEX{while} ~ \LEX{(} ~ \VAR{Exp}_1 ~ \LEX{)} ~
            \LEX{\LBRACE} ~ \LEX{\LBRACE} ~ \VAR{Stmts} ~ \LEX{\RBRACE} ~ \VAR{Exp}_2 ~ \LEX{;} ~ \LEX{\RBRACE} ~
     \LEX{\RBRACE} }
\end{align*}
$$

$$
\KEY{Semantics}
  \SEM[\DECL]{exec} \PHRASE{ \_:\SYN[\REF]{stmts} } : \TO \NAME{null-type}
$$

$$
\begin{align*}
\KEY{Rule}
  \SEM[\REF]{exec} \PHRASE{ \LEX{\LBRACE} ~ \LEX{\RBRACE} } = \NAME{null}
\end{align*}
$$

$$
\begin{align*}
\KEY{Rule}
  \SEM[\REF]{exec} \PHRASE{ \LEX{\LBRACE} ~ \VAR{Stmts} ~ \LEX{\RBRACE} } = \SEM[\REF]{exec} \PHRASE{ \VAR{Stmts} }
\end{align*}
$$

$$
\begin{align*}
\KEY{Rule}
  \SEM[\REF]{exec} \PHRASE{ \VAR{ImpStmt} ~ \VAR{Stmts} } = 
    \NAME[\HYPER{\FunconsFlowing}]{sequential}(\SEM[\REF]{exec} \PHRASE{ \VAR{ImpStmt} }, \SEM[\REF]{exec} \PHRASE{ \VAR{Stmts} })
\end{align*}
$$

$$
\begin{align*}
\KEY{Rule}
  \SEM[\REF]{exec} \PHRASE{ \VAR{VarsDecl} ~ \VAR{Stmts} } = 
    \NAME[\HYPER{\FunconsBinding}]{scope}(\SEM[\HYPER{\LanguagesSIMPLE{4-Declarations}}]{declare} \PHRASE{ \VAR{VarsDecl} }, \SEM[\REF]{exec} \PHRASE{ \VAR{Stmts} })
\end{align*}
$$

$$
\begin{align*}
\KEY{Rule}
  \SEM[\REF]{exec} \PHRASE{ \VAR{VarsDecl} } = \NAME{effect}(\SEM[\HYPER{\LanguagesSIMPLE{4-Declarations}}]{declare} \PHRASE{ \VAR{VarsDecl}})
\end{align*}
$$

$$
\begin{align*}
\KEY{Rule}
  \SEM[\REF]{exec} \PHRASE{ \VAR{Exp} ~ \LEX{;} } = \NAME{effect}(\SEM[\HYPER{\LanguagesSIMPLE{2-Expressions}}]{rval} \PHRASE{ \VAR{Exp} })
\end{align*}
$$

$$
\begin{align*}
\KEY{Rule}
  & \SEM[\REF]{exec} \PHRASE{ \LEX{if} ~ \LEX{(} ~ \VAR{Exp} ~ \LEX{)} ~ \VAR{Block}_1 ~ \LEX{else} ~ \VAR{Block}_2 } = \\
  & \NAME{if-else}(\SEM[\HYPER{\LanguagesSIMPLE{2-Expressions}}]{rval} \PHRASE{ \VAR{Exp} }, \SEM[\REF]{exec} \PHRASE{ \VAR{Block}_1 ~ }, \SEM[\REF]{exec} \PHRASE{ \VAR{Block}_2 })
\end{align*}
$$

$$
\begin{align*}
\KEY{Rule}
  \SEM[\REF]{exec} \PHRASE{ \LEX{while} ~ \LEX{(} ~ \VAR{Exp} ~ \LEX{)} ~ \VAR{Block} } = \NAME{while}(\SEM[\HYPER{\LanguagesSIMPLE{2-Expressions}}]{rval} \PHRASE{ \VAR{Exp} }, \SEM[\REF]{exec} \PHRASE{ \VAR{Block} })
\end{align*}
$$

$$
\begin{align*}
\KEY{Rule}
\SEM[\REF]{exec} \PHRASE{ \LEX{print} ~ \LEX{(} ~ \VAR{Exps} ~ \LEX{)} ~ \LEX{;} } = \NAME{print}(\SEM[\HYPER{\LanguagesSIMPLE{2-Expressions}}]{rvals} \PHRASE{ \VAR{Exps} })
\end{align*}
$$

$$
\begin{align*}
\KEY{Rule}
  \SEM[\REF]{exec} \PHRASE{ \LEX{return} ~ \VAR{Exp} ~ \LEX{;} } = \NAME{return}(\SEM[\HYPER{\LanguagesSIMPLE{2-Expressions}}]{rval} \PHRASE{ \VAR{Exp} })
\end{align*}
$$

$$
\begin{align*}
\KEY{Rule}
  \SEM[\REF]{exec} \PHRASE{ \LEX{return} ~ \LEX{;} } = \NAME{return}(\NAME{null})
\end{align*}
$$

$$
\begin{align*}
\KEY{Rule}
  & \SEM[\REF]{exec} \PHRASE{ \LEX{try} \VAR{Block}_1 ~ \LEX{catch} \LEX{(} \VAR{Id} \LEX{)} \VAR{Block}_2 } = \\
  & \NAME{handle-thrown}( \\
  & \quad   \SEM[\REF]{exec} \PHRASE{ \VAR{Block}_1 ~ }, \\
  & \quad   \NAME{scope}( \\
  & \quad \quad   \NAME{bind}(\SEM[\HYPER{\LanguagesSIMPLE{1-Lexical}}]{id} \PHRASE{ \VAR{Id} }, \NAME{allocate-initialised-variable}(\NAME{values},\NAME{given})), \\
  & \quad \quad   \SEM[\REF]{exec} \PHRASE{ \VAR{Block}_2 }))
\end{align*}
$$

$$
\begin{align*}
\KEY{Rule}
  \SEM[\REF]{exec} \PHRASE{ \LEX{throw} ~ \VAR{Exp} ~ \LEX{;} } = \NAME{throw}(\SEM[\HYPER{\LanguagesSIMPLE{2-Expressions}}]{rval} \PHRASE{ \VAR{Exp} })
\end{align*}
$$

## Funcons-beta/Computations/Normal

### Binding

#### Contents
{: .no_toc }

$$
\begin{alignat*}{2}
  \KEY{Type}    & \NAME{environments}       &~~& \KEY{Alias} \NAME{envs}
  \\
  \KEY{Datatype}& \NAME{identifiers}        & & \KEY{Alias} \NAME{ids}
  \\
  \KEY{Funcon}  & \NAME{identifier-tagged}  & & \KEY{Alias} \NAME{id-tagged}
  \\
  \KEY{Funcon}  & \NAME{fresh-identifier}
  \\
  \KEY{Entity}  & \NAME{environment}        & & \KEY{Alias} \NAME{env}
  \\
  \KEY{Funcon}  & \NAME{initialise-binding}
  \\
  \KEY{Funcon}  & \NAME{bind-value}         & & \KEY{Alias} \NAME{bind}
  \\
  \KEY{Funcon}  & \NAME{unbind}
  \\
  \KEY{Funcon}  & \NAME{bound-directly}
  \\
  \KEY{Funcon}  & \NAME{bound-value}        & & \KEY{Alias} \NAME{bound}
  \\
  \KEY{Funcon}  & \NAME{closed}
  \\
  \KEY{Funcon}  & \NAME{scope}
  \\
  \KEY{Funcon}  & \NAME{accumulate}
  \\
  \KEY{Funcon}  & \NAME{collateral}
  \\
  \KEY{Funcon}  & \NAME{bind-recursively}
  \\
  \KEY{Funcon}  & \NAME{recursive}
\end{alignat*}
$$

$$
\KEY{Meta-variables}
  T <: \NAME{values}
$$

#### Environments

$$
\begin{align*}
  \KEY{Type}
  & \NAME{environments} \leadsto \NAME{maps}(\NAME{identifiers}, \NAME{values}\QUERY)
\\
  \KEY{Alias}
  & \NAME{envs} = \NAME{environments}
\end{align*}
$$

An environment represents bindings of identifiers to values.
Mapping an identifier to $$ (~) $$ represents that its binding is hidden.

Circularity in environments (due to recursive bindings) is represented using
bindings to cut-points called *links*. Funcons are provided for making
declarations recursive and for referring to bound values without explicit
mention of links, so their existence can generally be ignored.

$$
\begin{align*}
  \KEY{Datatype}
  & \NAME{identifiers} ::= \{\_:\NAME{strings}\} \mid \NAME{identifier-tagged}(\_:\NAME{identifiers}, \_:\NAME{maps})
\\
  \KEY{Alias}
  & \NAME{ids} = \NAME{identifiers}
\\
  \KEY{Alias}
  & \NAME{id-tagged} = \NAME{identifier-tagged}
\end{align*}
$$

An identifier is either a string of characters, or an identifier tagged with
some value (e.g., with the identifier of a namespace).

$$
\KEY{Funcon}
  \NAME{fresh-identifier} : \TO \NAME{identifiers}
$$

$$ \NAME{fresh-identifier} $$ computes an identifier distinct from all previously
computed identifiers.

$$
\KEY{Rule}
  \NAME{fresh-identifier} \leadsto \NAME{identifier-tagged}(\STRING{generated}, \NAME{fresh-atom})
$$

#### Current bindings

$$
\begin{align*}
  \KEY{Entity}
  & \NAME{environment}(\_:\NAME{environments}) \vdash \_ \TRANS \_
\\
  \KEY{Alias}
  & \NAME{env} = \NAME{environment}
\end{align*}
$$

The environment entity allows a computation to refer to the current bindings
of identifiers to values.

$$
\begin{align*}
  \KEY{Funcon}
  & \NAME{initialise-binding}(X:\TO T) : \TO T
\\
  & \quad {} \leadsto \NAME{initialise-linking}(\NAME{initialise-generating}(\NAME{closed}(X)))
\end{align*}
$$

$$ \NAME{initialise-binding}(X) $$ ensures that $$ X $$ does not depend on non-local bindings.
It also ensures that the linking entity (used to represent potentially cyclic
bindings) and the generating entity (for creating fresh identifiers) are 
initialised.

$$
\begin{align*}
  \KEY{Funcon}
  & \NAME{bind-value}(I:\NAME{identifiers}, V:\NAME{maps}) : \TO \NAME{environments}
\\
  & \quad {} \leadsto \{ I \mapsto V \}
\\
  \KEY{Alias}
  & \NAME{bind} = \NAME{bind-value}
\end{align*}
$$

$$ \NAME{bind-value}(I, X) $$ computes the environment that binds only $$ I $$ to the value
computed by $$ X $$.

$$
\begin{align*}
  \KEY{Funcon}
  & \NAME{unbind}(I:\NAME{identifiers}) : \TO \NAME{environments}
\\
  & \quad {} \leadsto \{ I \mapsto (~) \}
\end{align*}
$$

$$ \NAME{unbind}(I) $$ computes the environment that hides the binding of $$ I $$.

$$
\KEY{Funcon}
  \NAME{bound-directly}(\_:\NAME{identifiers}) : \TO \NAME{maps}
$$

$$ \NAME{bound-directly}(I) $$ returns the value to which $$ I $$ is currently bound, if any,
and otherwise fails.

$$ \NAME{bound-directly}(I) $$ does *not* follow links. It is used only in connection with
recursively-bound values when references are not encapsulated in abstractions.

$$
\begin{align*}
  \KEY{Rule} 
  & \RULE{
    \NAME{lookup}(\rho, I) \leadsto (V:\NAME{maps})
    }{
    \NAME{environment}(\rho) \vdash \NAME{bound-directly}(I:\NAME{identifiers}) \TRANS V
    }
\\
  \KEY{Rule} 
  & \RULE{
    \NAME{lookup}(\rho, I) \leadsto (~)
    }{
    \NAME{environment}(\rho) \vdash \NAME{bound-directly}(I:\NAME{identifiers}) \TRANS \NAME{fail}
    }
\end{align*}
$$

$$
\begin{align*}
  \KEY{Funcon}
  & \NAME{bound-value}(I:\NAME{identifiers}) : \TO \NAME{maps}
\\
  & \quad {} \leadsto \NAME{follow-if-link}(\NAME{bound-directly}(I))
\\
  \KEY{Alias}
  & \NAME{bound} = \NAME{bound-value}
\end{align*}
$$

$$ \NAME{bound-value}(I) $$ inspects the value to which $$ I $$ is currently bound, if any,
and otherwise fails. If the value is a link, $$ \NAME{bound-value}(I) $$ returns the
value obtained by following the link, if any, and otherwise fails. If the 
inspected value is not a link, $$ \NAME{bound-value}(I) $$ returns it. 

$$ \NAME{bound-value}(I) $$ is used for references to non-recursive bindings and to
recursively-bound values when references are encapsulated in abstractions.

#### Scope

$$
\KEY{Funcon}
  \NAME{closed}(X:\TO T) : \TO T
$$

$$ \NAME{closed}(X) $$ ensures that $$ X $$ does not depend on non-local bindings.

$$
\begin{align*}
  \KEY{Rule} 
  & \RULE{
    \NAME{environment}(\NAME{map}(~)) \vdash X \TRANS X'
    }{
    \NAME{environment}(\_) \vdash \NAME{closed}(X) \TRANS \NAME{closed}(X')
    }
\\
  \KEY{Rule}
  & \NAME{closed}(V:T) \leadsto V
\end{align*}
$$

$$
\KEY{Funcon}
  \NAME{scope}(\_:\NAME{environments}, \_:\TO T) : \TO T
$$

$$ \NAME{scope}(D,X) $$ executes $$ D $$ with the current bindings, to compute an environment
$$ \rho $$ representing local bindings. It then executes $$ X $$ to compute the result,
with the current bindings extended by $$ \rho $$, which may shadow or hide previous
bindings.

$$ \NAME{closed}(\NAME{scope}(\rho, X)) $$ ensures that $$ X $$ can reference only the bindings
provided by $$ \rho $$.

$$
\begin{align*}
  \KEY{Rule} 
  & \RULE{
    \NAME{environment}(\NAME{map-override}(\rho_1, \rho_0)) \vdash X \TRANS X'
    }{
    \NAME{environment}(\rho_0) \vdash \NAME{scope}(\rho_1:\NAME{environments}, X) \TRANS \NAME{scope}(\rho_1, X')
    }
\\
  \KEY{Rule}
  & \NAME{scope}(\_:\NAME{environments}, V:T) \leadsto V
\end{align*}
$$

$$
\KEY{Funcon}
  \NAME{accumulate}(\_:(\TO \NAME{environments})\STAR) : \TO \NAME{environments}
$$

$$ \NAME{accumulate}(D_1, D_2) $$ executes $$ D_1 $$ with the current bindings, to compute an
environment $$ \rho_1 $$ representing some local bindings. It then executes $$ D_2 $$ to
compute an environment $$ \rho_2 $$ representing further local bindings, with the
current bindings extended by $$ \rho_1 $$, which may shadow or hide previous
current bindings. The result is $$ \rho_1 $$ extended by $$ \rho_2 $$, which may shadow
or hide the bindings of $$ \rho_1 $$.

$$ \NAME{accumulate}(\_, \_) $$ is associative, with $$ \NAME{map}(~) $$ as unit, and extends to any
number of arguments.

$$
\begin{align*}
  \KEY{Rule} 
  & \RULE{
    D_1 \TRANS D_1'
    }{
    \NAME{accumulate}(D_1, D_2) \TRANS \NAME{accumulate}(D_1', D_2)
    }
\\
  \KEY{Rule}
  & \NAME{accumulate}(\rho_1:\NAME{environments}, D_2) \leadsto \NAME{scope}(\rho_1, \NAME{map-override}(D_2, \rho_1))
\\
  \KEY{Rule}
  & \NAME{accumulate}(~) \leadsto \NAME{map}(~)
\\
  \KEY{Rule}
  & \NAME{accumulate}(D_1) \leadsto D_1
\\
  \KEY{Rule}
  & \NAME{accumulate}(D_1, D_2, D\PLUS) \leadsto \NAME{accumulate}(D_1, \NAME{accumulate}(D_2, D\PLUS))
\end{align*}
$$

$$
\begin{align*}
  \KEY{Funcon}
  & \NAME{collateral}(\rho\STAR:\NAME{environments}\STAR) : \TO \NAME{environments}
\\
  & \quad {} \leadsto \NAME{checked} \NAME{map-unite}(\rho\STAR)
   \end{align*}
$$

$$ \NAME{collateral}(D_1, ...) $$ pre-evaluates its arguments with the current bindings,
and unites the resulting maps, which fails if the domains are not pairwise
disjoint.

$$ \NAME{collateral}(D_1, D_2) $$ is associative and commutative with $$ \NAME{map}(~) $$ as unit, 
and extends to any number of arguments.

#### Recurse

$$
\begin{align*}
  \KEY{Funcon}
  & \NAME{bind-recursively}(I:\NAME{identifiers}, E:\TO \NAME{maps}) : \TO \NAME{environments}
\\
  & \quad {} \leadsto \NAME{recursive}({I}, \NAME{bind-value}(I, E))
\end{align*}
$$

$$ \NAME{bind-recursively}(I, E) $$ binds $$ I $$ to a link that refers to the value of $$ E $$, 
representing a recursive binding of $$ I $$ to the value of $$ E $$.
Since $$ \NAME{bound-value}(I) $$ follows links, it should not be executed during the
evaluation of $$ E $$.

$$
\begin{align*}
\KEY{Funcon}
  & \NAME{recursive}(\VAR{SI}:\NAME{sets}(\NAME{identifiers}), D:\TO \NAME{environments}) : \TO \NAME{environments}
\\
  & \quad ~ {} \leadsto \NAME{re-close}(\NAME{bind-to-forward-links}(\VAR{SI}), D)
\end{align*}
$$

$$ \NAME{recursive}(\VAR{SI}, D) $$ executes $$ D $$ with potential recursion on the bindings of 
the identifiers in the set $$ \VAR{SI} $$ (which need not be the same as the set of
identifiers bound by $$ D $$).

$$
\begin{align*}
  & \KEY{Auxiliary Funcon}
\\
  & \quad \NAME{re-close}(M:\NAME{maps}(\NAME{identifiers}, \NAME{links}), D:\TO \NAME{environments}) : \TO \NAME{environments}
\\
  & \quad ~ {} \leadsto \NAME{accumulate}(
    \begin{aligned}[t]
    & \NAME{scope}(M, D), 
    \\
    & \NAME{sequential}(\NAME{set-forward-links}(M), \NAME{map}(~)))
    \end{aligned}
\end{align*}
$$

$$ \NAME{re-close}(M, D) $$ first executes $$ D $$ in the scope $$ M $$, which maps identifiers
to freshly allocated links. This computes an environment $$ \rho $$ where the bound
values may contain links, or implicit references to links in abstraction
values. It then sets the link for each identifier in the domain of $$ M $$ to
refer to its bound value in $$ \rho $$, and returns $$ \rho $$ as the result.

$$
\begin{align*}
  & \KEY{Auxiliary Funcon}
\\
  & \quad \NAME{bind-to-forward-links}(\VAR{SI}:\NAME{sets}(\NAME{identifiers})) : \TO \NAME{maps}(\NAME{identifiers}, \NAME{links})
\\
  & \quad ~ {} \leadsto \NAME{map-unite}(
    \begin{aligned}[t]
    & \NAME{interleave-map}(\NAME{bind-value}(\NAME{given}, \NAME{fresh-link}(\NAME{maps})),
    \\
    & \NAME{set-elements}(\VAR{SI})))
    \end{aligned}
\end{align*}
$$

$$ \NAME{bind-to-forward-links}(\VAR{SI}) $$ binds each identifier in the set $$ \VAR{SI} $$ to a
freshly allocated link.

$$
\begin{align*}
  & \KEY{Auxiliary Funcon}
\\
  & \quad \NAME{set-forward-links}(M:\NAME{maps}(\NAME{identifiers}, \NAME{links})) : \TO \NAME{null-type}
\\
  & \quad ~ {} \leadsto \NAME{effect}(\NAME{interleave-map}(
    \begin{aligned}[t]
    & \NAME{set-link}(\NAME{map-lookup}(M, \NAME{given}), \NAME{bound-value}(\NAME{given})),
    \\
    & \NAME{set-elements}(\NAME{map-domain}(M))))
    \end{aligned}
\end{align*}
$$

For each identifier $$ I $$ in the domain of $$ M $$, $$ \NAME{set-forward-links}(M) $$ sets the 
link to which $$ I $$ is mapped by $$ M $$ to the current bound value of $$ I $$.