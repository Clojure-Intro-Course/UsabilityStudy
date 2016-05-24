<!-- TOC depthFrom:2 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [UsabilityStudy](#usabilitystudy)
	- [Table of Contents Generator Guide (markdown-toc)](#table-of-contents-generator-guide-markdown-toc)
		- [Installing markdown-toc Package](#installing-markdown-toc-package)
		- [Updating existing Table of Contents on a markdown](#updating-existing-table-of-contents-on-a-markdown)
		- [Creating a new Table of Contents for a markdown without one](#creating-a-new-table-of-contents-for-a-markdown-without-one)

<!-- /TOC -->

## UsabilityStudy

### Table of Contents Generator Guide (markdown-toc)

  *This guide is intended for use with the Atom IDE/Text Editor*

  Note: Due to a bug, you can only use the Table of Contents generator on *one* markdown file at a time. Using the generator with two or more markdowns open in tabs will result in unexpected behavior. You may need to restart Atom if the generator starts acting up.

#### Installing markdown-toc Package

  1. Open the settings tab (Edit ->Preferences)
  2. Click the Install tab in the left column
  3. Search "markdown-toc"
  4. Click "install"

#### Updating existing Table of Contents on a markdown

  1. Open package command list (cntrl-shift-p)
  2. Search for "Markdown-toc Update" and click it

From now on, the Table of Contents will update every time the markdown is
  saved in Atom.

Note: Every time you open Atom you will have to manually update the Table of
  Contents once (following the two steps above) before it will auto update.

#### Creating a new Table of Contents for a markdown without one

  Note: The generator will not work if your markdown skips a depth (i.e. inludes ## and #### but no ###)

  1. Move the first of your markdown down a line or two (i.e. not line 1) and click in line 1. (The table of contents will be inserted wherever you are actively editing.)
  2. Open package command list (cntrl-shift-p)
  3. Search for "Markdown-toc Toggle." If found, click it. Otherwise, search for "Markdown-toc Create" and click it instead.

Note: If you choose to start at a depth other than 1, you must change the depthFrom field in the first commented line of the Table of Contents to the first depth you use.
