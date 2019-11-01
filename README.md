# Introduction
This is a repository for templates to be used with the [texnew](https://github.com/alexrutar/texnew) library.
 You should install this repository to `~/.texnew`.
 As an example, the following code should work (on Linux or OSX):
~~~
cd ~
git clone https://github.com/alexrutar/texnew-templates .texnew
~~~
For more detailed information, please refer to [texnew](https://github.com/alexrutar/texnew).

# Designing Templates
Templates are organized into template sets for a fixed `<+name+>` which can be found in `.texnew/templates/<+name+>`, which have access to the set of packages in `.texnew/packages/<+name+>`.
If you want to make your own template set, the easiest way is to copy the structure in `.texnew/templates/base` and `.texnew/packages/base`.
Template files are placed in the `.texnew/templates/<+name+>` directory.
There are two mandatory options that must be specified in the template:
 - `formatting` must be any filename (without extension) defined in Formatting
 - `contents` must be any filename (without extension) defined in Contents.
Additionally, you can define any substitution variables within the template - note that template-defined variables will override any user-defined variables.
There are a few special substitutions:
- `doctype`: the document type (e.g. `article`, `memoir`, etc.)
- `{l,r,t,b}margin`: the size of the corresponding (left, right, top, bottom) margin

## Template set directory structure
See `packages/base` for the default example.
In this section, all paths are relative to `.texnew/packages/<+name+>`.

1. Macros: `macros/*`
    - Macro files stored here are accessed by the `macro` option in the templates. You can add your own macros, or pretty much whatever you want here.

2. Formatting: `formatting/*.tex`
    - Formatting files stored here are accessed by the `formatting` option in the templates. I've generally used them to define formatting for the file appearance (fonts, titlepages, etc).
    They must include `\begin{document}`; the `\end{document}` label is automatically placed afterwards.
    - Wherever `<+key+>` appears in a formatting document, they are automatically replaced by the relevant info in the `user.yaml` file or a substitution in the `template.yaml` file.
    `key` can be any string. You can define new keys.

3. Defaults: `defaults/doctype.tex` `defaults/packages.tex` `defaults/macros.tex`
    - Default files are loaded every time, regardless of the template used. Don't change the file names or weird things will happen, but feel free to change the defaults to whatever you want. `doctype.tex` must have the document class, and the tag `<+doctype+>` is automatically substituted by the defined value in a template. `macros.tex` is for default macros, and `packages.tex` for default packages, as evidenced by the name.

## Import Order
To avoid errors when designing templates, it is useful to know the order in which the template files are placed.
This is given as follows:
1. `defaults/doctype.tex`
2. `defaults/packages.tex`
3. `defaults/macros.tex`
4. `macros/*.tex` - any macro files included in the template, imported in the same order specified.
5. A space for file-specific macros (user macros are placed here when updating a file).
6. `formatting/*_constants.tex`, if it exists
7. `formatting/*.tex`, whatever formatting file you specified
8. `contents/*.tex`, which specifies some pre-written component of the main document.
As a general rule, I try to avoid importing anything in the formatting file to avoid conflict with user imports (notable exception: font packages).

## Including User Data
(to be written eventually)
To include:
- specifying substitutins within templates
- user substitutions
- substitution priority
- where substitutions come from
- warnings when substitutions overwrite others
- examples of substitutions
