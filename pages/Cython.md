
- [Working with Python arrays — Cython 3.0a5 documentation](https://cython.readthedocs.io/en/latest/src/tutorial/array.html)
- `longest[start]`
    - cdef list longest, long start
    - `__Pyx_GetItemInt_List(__pyx_cur_scope->__pyx_v_longest, __pyx_cur_scope->__pyx_v_start, long, 1, __Pyx_PyInt_From_long, 1, 1, 1);`
- `$ cython -a -3 g_cython.pyx`
    - `$ cython -3 --embed ./g_cython.pyx`
