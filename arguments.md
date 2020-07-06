Arguments
=========

Only positional arguments (and sec=) are allowed in NEURON *except* for functions with no HOC
equivalent that are handled separately.

Note: NEURON argument indices are always numbered from 1.

Check for the existence of an argument
--------------------------------------

Use `ifarg(n)` to check to see if there is an `n`th argument (the arguments are numbered from 1).

Check the type of an argument
-----------------------------

Relevant functions include:
- `hoc_is_object_arg(n)`
- `hoc_is_pdouble_arg(n)`
- `hoc_is_str_arg(n)`
- `hoc_is_double_arg(n)`

Get the value of an argument
----------------------------

Relevant functions include:
- `hoc_obj_getarg(n)`

   May want to combine this with `nrnpy_ho2po` if you know the argument is a `PyObject`; e.g.
   
       PyObject* obj = nrnpy_ho2po(*hoc_objgetarg(n))
- `hoc_pgetarg(n)` -- returns a `double**`
- `gargstr(n)`
- `getarg(n)` -- returns a `double*`
