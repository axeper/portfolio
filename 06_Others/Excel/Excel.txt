### GUI

Data -> Filter for a dropdown selection

Data -> Sort -> Options allows left-to-right sorting 

Insert -> Pivot table to "group by" data

Ctr + Shift + Enter to return an array formula (enter returns a scalar)


### Formulas

Absolute reference
=C$2*D$2 (dragging the corner won't change the number 2)

Find a location and return a value
=MATCH("Hamburger",A2:A15,0)

Returns a value
=INDEX(A1:B15,3,2)

Returns value relative to a position
=OFFSET(A1,3,0)

Returns the third smallest value
=SMALL(B2:B15,3)

Find value in other sheet
=VLOOKUP(A2,Calories!$A$1:$B$15,2,FALSE)

Replace text based on content
=SUBSTITUTE(text, old_text, new_text, [instance])


### Add-Ins

Solver: add an objective to maximize/minimize, add contraints, solve using the simplex or evolutionnary algorithm

opensolver.org is an alternative when solver fails (especially with high number of dimensions)