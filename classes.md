Classes
=======

Declaring classes
-----------------

Classes are declared using the `class2oc` function, e.g.

	class2oc("ClassName", cons, destruct, members, NULL, retobj_members, NULL)
  
Here `cons` is the constructor, which must take an `Object*` and return a `void*`.

`destruct` is the destructor, which takes a `void*` and has no return.

`members` is a null-terminated array of `Member_func` of methods that in Python could return float, 
integer, or bool. In HOC, these all return doubles.
- To specify the return type as seen by Python, set `hoc_return_type_code`. A value of 0 indicates
  the funciton is returning a float; 1 indicates an integer; a value of 2 indicates a bool.
- Each of these methods must take a `void*` and return a double.

`retobj_methods` is a null-terminated array of `Member_ret_obj_func` of methods that return objects.
(The actual functions implementing them take a `void*` and return an `Object**`.)


