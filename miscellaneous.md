Miscellaneous
=============

Raising a NEURON error
----------------------

Use `hoc_exec_error` which takes two `char*` arguments (which can be NULL). e.g.

    hoc_execerror("Message part 1", "Message part 2");

Note: all NEURON errors currently are received by Python as a `RuntimeError` exception, and all errors
print their error messages before returning to Python, meaning that they will always print out, even
inside a try/except block.
