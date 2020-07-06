Working with Object and PyObject
================================

The CPython API is only to be invoked directly from within `src/nrnpython`.

The way to support using Python from outside this folder without introducing a dependency on Python is to declare a function
pointer outside the folder, then have that function pointer be set by something inside e.g. `src/nrnpython/nrnpy_hoc.cpp`.
All uses outside the folder must first check to see if the funciton pointer is not NULL; if it is NULL then Python is not
available. This is done for a number of functions in the `nrnpy_hoc()` function in `src/nrnpython/nrnpy_hoc.cpp`.



To check if a NEURON object is wrapping a PyObject
--------------------------------------------------

To see if an Object* obj is wrapping a PyObject, check if

    obj->ctemplate->sym == nrnpy_pyobj_sym_

The variable `nrnpy_pyobj_sym_` here is a `Symbol*` and it is shared and available at least within `nrnpython`.


To check if a PyObject is wrapping a NEURON object
--------------------------------------------------

Use `PyObject_TypeCheck(po, hocobject_type)` where `po` is the `PyObject`.


To encapsulate a NEURON Object in a PyObject
--------------------------------------------

Use `nrnpy_ho2po`. If the NEURON object is wrapping a `PyObject` it returns the original `PyObject` with the reference count increased by one.
Otherwise it returns a `PyHocObject`. Note: this function does not convert NEURON strings or floats to `PyObject` instances as those are
not internally stored with `Object` instances. Those can be converted directly using the CPython API e.g. `PyFloat_FromDouble`, `PyLong_FromLong`.


To encapsule a PyObject in a NEURON Object
------------------------------------------

Use `nrnpy_po2ho`. If the object is wrapping a NEURON Object, it increments the NEURON object's reference count by 1 and returns the original
NEURON object. Otherwise it returns a new NEURON Object* wrapping the `PyObject`. In particular, it *always* returns a NEURON object, even for
strings and floats that would be more naturally represented in NEURON as their respective datatypes.

To check if a PyObject is a number
----------------------------------

Use `nrnpy_numbercheck(po)` where `po` is the `PyObject*` to check.

This is built-on but has modified semantics from the CPython API `PyNumber_Check` to detect things that NEURON cannot treat directly as numbers,
like complex numbers.
