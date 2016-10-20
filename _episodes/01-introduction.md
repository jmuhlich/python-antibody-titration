---
title: "Building an experimental design"
teaching: 0
exercises: 0
questions:
- "How can I build my experimental design through code?"
objectives:
- "Build an experimental design entirely in Python code."
- "Understand how to refactor code for reusability and readability."
keypoints:
- "Creating regular tables through code is more reliable than manual entry."
- "Comments and documentation in code serves to explain the author's thinking."
---
## Experimental design tables define the layout of experimental variables.

![plate map](../fig/plate_map.jpg)
* They map experimental variables like treatment conditions and replicate
  numbers to the physical experimental samples.
* Confounders such as plate row and column are also useful variables.
* We sometimes like to think of these tables as 2-dimensional grids
  corresponding to our physical microtiter plates or spot arrays.
  * However by the principles
    of [Tidy Data](vita.had.co.nz/papers/tidy-data.pdf) we actually want tall,
    spreadsheet-like tables where each variable is one column and each
    observation or sample is one row.

## Define design tables by creating columns in a new DataFrame

* Create a new DataFrame:

~~~
import pandas as pd
design = pd.DataFrame()
~~~
{: .python}

* Create new column containing plate row name, explicitly.

~~~
design['Row'] = ['A', 'A', 'A', 'A', 'B', 'B', 'B', 'B', 'C', 'C', 'C', 'C']
~~~
{: .python}

* Ask about problems with this approach?
  * Redundant
  * Not general

* Break problem down
* First work on generating a list of 4 'A's
  * Introduce '*' operator on lists
  * Use '*' to produce 4 'A's.
  * Ask what if new experiment has different number of rows?
  * Define 'n_rows' variable set to 4 and use it instead of literal 4
* Next work on adding the 'B's and 'C's
  * Introduce '+' operator on lists
  * Use '+' to append ['A'] * 4 + ['B'] * 4 + ['C'] * 4
  * Ask what if new experiment has different number of columns?
  * Introduce iteration with reduction variable
    * Define row_names = ['A', 'B', 'C']
    * Iterate over row_names, appending lists to reduction variable
* Assign final result to 'Row' column

~~~
design['Column'] = [1, 2, 3, 4, 1, 2, 3, 4, 1, 2, 3, 4]
~~~
{: .python}

* Point out same problems with original explicit Row approach (redundant, not general)
* Break it down
* First work on generating [1,2,3,4].


~~~
design['Well'] = design.Row + design.Column
~~~
{: .python}

* Oops, error. What happened?
  * Incompatible types, need two strings to concatenate
* Convert type using 'astype'

~~~
design['Well'] = design.Row + design.Column.astype(str)
~~~
{: .python}


* import seaborn, show import error, explain how to install new package
* Kernel -> Conda packages -> type "seaborn" -> check it -> click arrow -> click install -> close

~~~
~~~
{: .python}

~~~
~~~
{: .python}

~~~
~~~
{: .python}
