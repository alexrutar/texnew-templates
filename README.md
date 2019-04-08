# Introduction
This is a repository for templates to be used with the [texnew](https://github.com/alexrutar/texnew).
 You should install this repository to `~/.texnew`.
 As an example, the following code should work (on Linux or OSX):
~~~
cd ~
git clone https://github.com/alexrutar/texnew-templates .texnew
~~~
For more detailed information, please refer to [texnew](https://github.com/alexrutar/texnew).

# Designing Templates
Templates are organized into template sets which can be found in `.texnew/share`.
If you want to make your own template set, the easiest way is to copy the structure in `base`.
Template files are placed in the `templates` directory.
There are three (mandatory) options to be included in the template:
 - `doctype` can be any valid LaTeX document type (e.g. article, book)
 - `formatting` must be any filename (without extension) defined in Formatting
 - `macros` must be any filename (without extension) defined in Macros.
Additionally, you can define any substitution variables within the template - note that template-defined variables will override any user-defined variables.

## Template set directory structure
See `share/base` for the default example.

1. Macros: `macros/*`
    - Macro files stored here are accessed by the `macro` option in the templates. You can add your own macros, or pretty much whatever you want here.

2. Formatting: `formatting/*.tex`
    - Formatting files stored here are accessed by the `formatting` option in the templates. I've generally used them to define formatting for the file appearance (fonts, titlepages, etc).
    They must include `\begin{document}`; the `\end{docment}` label is automatically placed afterwards.
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
6. `formatting/*.tex`, whatever formatting file you specified
7. A space for the main document (document is placed here when updating).
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
