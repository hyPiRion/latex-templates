# Classicthesis (English)

This is a huge report stylesheet. As it has a ton of dependencies, I'd recommend
just installing `texlive-full` or an equivalent of *all the packages* on your
operative system/CTAN package manager. Note that this also uses `pygments`, so
installing `pygments` is also required. All in all a pretty dependency-heavy
setup, but in my opinion worth it.

## "Environment Variables"

People would usually like to set their names and values within `config.tex`,
which contains a full list of values shown in the style.

## Utility

The commands `\TODO`, `\NOTE` and `\CHECK` are available for comments inside the
document. It's convenient for development purposes, but serve no purpose other
than point out

## Report structure

The report is split up in many different parts: Abstract, chapters, sections
inside chapters, figures and graphics, code and algorithms, as well as
appendices and bibliography. All of these entities are placed within different
directories, with the following structure:

	core -> report.tex
	layout -> config.tex
	front/back -> fb/*
	chapter -> ch/chapter-name.tex
	seksjon -> ch/chapter-name/section-name.tex
	figures and graphics -> figs/chapter-name/figure-name.tex
	'image files' -> figs/chapter-name/figure-name.[pdf|ps]
	code og algorithms -> code/chapter-naem/code-name.tex
	source code -> code/chapter-name/code-name.[filextension]

It may seem a bit enterprisey, but it is easier to maintain for larger reports
when everyone keeps the convention. If you have something you'd like to patch
up, you can be certain that it is placed at some position you know.

Additionally, this opens the possibility to use versioning systems without
ending up with a lot of merge conflicts. If a conflict turns up, then the fix is
rather straightforward. It is also easier to navigate when you're used to the
structure.

### Including files in Classicthesis

To inluce a new element in the report, use the `\input` command in tex. Examples
on how this is used is shown below:

```tex
\input{abstract.tex} % To add in the abstract
\input{ch/intro.tex} % To add in the intro chapter
\input{ch/intro/foobar.tex} % To add in the section foobar from intro
\input{figs/intro/introfig.tex} % To add in an intro figure
\input{code/intro/introcode.tex} % To add in some intro code
```

For more information on how the different parts should look like, please
continue reading.

**NB**: **DO NOT** use `\include`, as this cannot be nested and enforces page
  breaks.

## Chapters

Chapters should be placed within the `ch` directory, and should have a short and
descriptive name. For instance, a chapter named `Introduction` should be named
`intro.tex` or similar. Chapters should begin with `\chapter{Chapter name}` and
should thereafter have a *preamble* on one to two relatively short paragraphs.
Finally, input-commands to sections should be listed.

If the chapter is very short and doesn't have any natural sections, consider
placing the chapter as a section within some other chapter.

An example on a `chapter.tex` file is shown below:

```tex
\chapter{Introduction}

This is the preamble to introduction.

\input{ch/intro/structure.tex} % Structure of this report
\input{ch/intro/assignment.tex}
\input{ch/intro/specs.tex} % Requirements and specifications
\input{ch/intro/terms.tex} % Terminology, names and conventions
\input{ch/intro/philosophy.tex}
```

### Sections

Sections should be placed within `ch/chapter-name`. If sections are very short
or are naturally connected, they could be placed within same `tex` file.
Otherwise, they should be placed within distinct files. Sections are added
through the `\input` command from within the `chapter-name.tex` file.

Sections can have subsections, if this seems natural. These does not have to lie
inside different `tex` files.
