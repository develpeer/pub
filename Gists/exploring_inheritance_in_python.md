---
layout: default
title: Gist for - exploring_inheritance_in_python.py
parent: Gist for fun
nav_order: 5
---

# Gist for:  exploring_inheritance_in_python.py

# Source Code 
```  python
# the one and only Dev.E.L'Peer  https://github.com/develpeer
##
# This gist explores class inheritance including multiple inheritance
##
import json
from multiprocessing.util import abstract_sockets_supported

from exploring_python_classes import MY_DERIVED_CLASS


class BABY_BASE:
    """I find Class:BabyBase and Object:baby_base incosistent"""

    base_class_var = 100.1
    
    def __init__(this, param):
        print("BC:constructor")
        this.base_object_var_1 = 101
        this.base_object_var_2 = param
        this.base_object_var_3 = param

    def __repr__(this) -> str:
        d = vars(this)
        d["base_class_var"] = this.base_class_var
        d["CLASS"] = this.__class__.__name__
        return json.dumps(d,indent=4)

    def abstract_func(this):
        raise Exception("No implementation")

class DERIVED_CLASS_1(BABY_BASE):

    def __init__(this, param):
        #have to explicitly call super contructor. but really you can call any function here
        print("DC1:constructor")
        BABY_BASE.__init__(this,param)
        this.base_object_var_3 = this.base_object_var_2 + .50
        this.derived_object_var_3 = this.base_class_var *2
        this.derived_object_var_4 = param
    

class DERIVED_CLASS_2(BABY_BASE):

    def __init__(this, param):
        print("DC2:constructor")
        super().__init__(param)
        this.base_object_var_3 = this.base_object_var_2 + .75
        this.derived_object_var_3 = this.base_class_var *3
        this.derived_object_var_5 = param

    def abstract_func(this):
        return "Yes implementation"

    def regular_func(this):
        return "Just some random value:"+super()

class DERIVED_GRAND_CHILD(DERIVED_CLASS_1,DERIVED_CLASS_2):
    pass

bb = BABY_BASE(100)
print("bb:",bb)
print("isinstance(bb,BABY_BASE)",isinstance(bb,BABY_BASE))
print("issubclass(BABY_BASE,BABY_BASE)",issubclass(BABY_BASE,BABY_BASE))

do = DERIVED_CLASS_1(200)
print("do:",do)
try:
    do.abstract_func()
except BaseException as e:
    print("Above line should throw an error:",e)    
print("isinstance(do,BABY_BASE)",isinstance(do,BABY_BASE))
print("issubclass(DERIVED_CLASS_1,BABY_BASE)",issubclass(DERIVED_CLASS_1,BABY_BASE))


do2 = DERIVED_CLASS_2(300)
print("do2:",do2)
do2.abstract_func()
print("isinstance(do2,BABY_BASE)",isinstance(do2,BABY_BASE))
print("issubclass(DERIVED_CLASS_2,BABY_BASE)",issubclass(DERIVED_CLASS_2,BABY_BASE))

ddc = DERIVED_GRAND_CHILD(400)
#Will invoke the first class' constructor and the second class' methods when the clash
#makes complete sense right?
print("ddc",ddc)
print(ddc.abstract_func()) #This is from the second parent, not the first!!


class B:
    def f(self):
        return "p"

class C1(B):
   #no definition of f
   pass

class C2(B):
    def f(self):
        return "c2"

class G(C1,C2):
    pass

##For most purposes, in the simplest cases, you can 
# think of the search for attributes inherited from a 
# parent class as depth-first, left-to-right, 
# not searching twice in the same class where 
# there is an overlap in the hierarchy. Thus, if an 
# attribute is not found in DerivedClassName, it is 
# searched for in Base1, then (recursively) in the base 
# classes of Base1, and if it was not found there, it 
# was searched for in Base2, and so on.
### I call bullshit ...> This is not depth first, left to right 
### A depth first would have returned "p"
print("WTF python:",G().f())

class T:
    "hello world"

t = T()
print("instance of T:",t)
print("t.doc:",t.__doc__)

print(BABY_BASE.__dict__)



```


# Output
After running the above code snippet, you will get this output

```
>>>
>>> classvar:100, #class var accessed via class
>>> classvar_2:200, #class var accessed via class
>>> o_var_1:300,
>>> o_var_2:3.14,
>>>
>>> ----------------------------------------
>>> All the attribites of o:
>>> __class__
>>> copyGists.sh rebuild.sh __delattr__
>>> copyGists.sh rebuild.sh __dict__
>>> copyGists.sh rebuild.sh __dir__
>>> copyGists.sh rebuild.sh __doc__
>>> copyGists.sh rebuild.sh __eq__
>>> copyGists.sh rebuild.sh __format__
>>> copyGists.sh rebuild.sh __ge__
>>> copyGists.sh rebuild.sh __getattribute__
>>> copyGists.sh rebuild.sh __gt__
>>> copyGists.sh rebuild.sh __hash__
>>> copyGists.sh rebuild.sh __init__
>>> copyGists.sh rebuild.sh __init_subclass__
>>> copyGists.sh rebuild.sh __le__
>>> copyGists.sh rebuild.sh __lt__
>>> copyGists.sh rebuild.sh __module__
>>> copyGists.sh rebuild.sh __ne__
>>> copyGists.sh rebuild.sh __new__
>>> copyGists.sh rebuild.sh __private_var__
>>> copyGists.sh rebuild.sh __reduce__
>>> copyGists.sh rebuild.sh __reduce_ex__
>>> copyGists.sh rebuild.sh __repr__
>>> copyGists.sh rebuild.sh __setattr__
>>> copyGists.sh rebuild.sh __sizeof__
>>> copyGists.sh rebuild.sh __str__
>>> copyGists.sh rebuild.sh __subclasshook__
>>> copyGists.sh rebuild.sh __weakref__
>>> copyGists.sh rebuild.sh class_var
>>> copyGists.sh rebuild.sh class_var_2
>>> copyGists.sh rebuild.sh f1
>>> copyGists.sh rebuild.sh f2
>>> copyGists.sh rebuild.sh o_var_1
>>> copyGists.sh rebuild.sh o_var_2
>>> ----------------------------------------
>>> All the attribites of MyFirstClass:
>>> __class__
>>> copyGists.sh rebuild.sh __delattr__
>>> copyGists.sh rebuild.sh __dict__
>>> copyGists.sh rebuild.sh __dir__
>>> copyGists.sh rebuild.sh __doc__
>>> copyGists.sh rebuild.sh __eq__
>>> copyGists.sh rebuild.sh __format__
>>> copyGists.sh rebuild.sh __ge__
>>> copyGists.sh rebuild.sh __getattribute__
>>> copyGists.sh rebuild.sh __gt__
>>> copyGists.sh rebuild.sh __hash__
>>> copyGists.sh rebuild.sh __init__
>>> copyGists.sh rebuild.sh __init_subclass__
>>> copyGists.sh rebuild.sh __le__
>>> copyGists.sh rebuild.sh __lt__
>>> copyGists.sh rebuild.sh __module__
>>> copyGists.sh rebuild.sh __ne__
>>> copyGists.sh rebuild.sh __new__
>>> copyGists.sh rebuild.sh __private_var__
>>> copyGists.sh rebuild.sh __reduce__
>>> copyGists.sh rebuild.sh __reduce_ex__
>>> copyGists.sh rebuild.sh __repr__
>>> copyGists.sh rebuild.sh __setattr__
>>> copyGists.sh rebuild.sh __sizeof__
>>> copyGists.sh rebuild.sh __str__
>>> copyGists.sh rebuild.sh __subclasshook__
>>> copyGists.sh rebuild.sh __weakref__
>>> copyGists.sh rebuild.sh class_var
>>> copyGists.sh rebuild.sh class_var_2
>>> copyGists.sh rebuild.sh f1
>>> copyGists.sh rebuild.sh f2
>>> 'MY_FIRST_CLASS' object has no attribute 'o_var_1'
>>> !!!!You can delete attributes of an object from outside the object.. WTF!!
>>> So much for encapsulation
>>> MY_FIRST_CLASS.f1 <function MY_FIRST_CLASS.f1 at 0x10aa769e0>
>>> MY_FIRST_CLASS.f1() you get what you so.. do not deserve
>>> o.f1 <bound method MY_FIRST_CLASS.f1 of
>>> classvar:100, #class var accessed via class
>>> classvar_2:200, #class var accessed via class
>>> o_var_1:UNDEFINED,
>>> o_var_2:3.14,
>>> >
>>> I got me some args y'all, because python uses an implicit invocation context to differentiate betwwen instance and class methods
>>> That is if this method is an object method, you must declare its firt arg as 'self', which fuck that ..i'm going tojust call python_sucks..see next method
>>> Stupid stupid python arg =
>>> classvar:100, #class var accessed via class
>>> classvar_2:200, #class var accessed via class
>>> o_var_1:UNDEFINED,
>>> o_var_2:3.14,
>>>
>>> o.f1 you get what you so.. do not deserve
>>> o.f2 <bound method MY_FIRST_CLASS.f2 of
>>> classvar:100, #class var accessed via class
>>> classvar_2:200, #class var accessed via class
>>> o_var_1:UNDEFINED,
>>> o_var_2:3.14,
>>> >
>>> o.f2 returned 314.0
>>> invoking the method at class level will cause a TypeError
>>> This should work just fine. 'of2' is bound to 'o': 314.0
>>> Class variables can be accessed in one of two ways outside the class definition: True
>>> {'o_var_1': 300, 'o_var_2': -200} 100 200 -20000
>>> BC:constructor
>>> bb: {
>>> "base_object_var_1": 101,
>>> "base_object_var_2": 100,
>>> "base_object_var_3": 100,
>>> "base_class_var": 100.1,
>>> "CLASS": "BABY_BASE"
>>> }
>>> isinstance(bb,BABY_BASE) True
>>> issubclass(BABY_BASE,BABY_BASE) True
>>> DC1:constructor
>>> BC:constructor
>>> do: {
>>> "base_object_var_1": 101,
>>> "base_object_var_2": 200,
>>> "base_object_var_3": 200.5,
>>> "derived_object_var_3": 200.2,
>>> "derived_object_var_4": 200,
>>> "base_class_var": 100.1,
>>> "CLASS": "DERIVED_CLASS_1"
>>> }
>>> Above line should throw an error: No implementation
>>> isinstance(do,BABY_BASE) True
>>> issubclass(DERIVED_CLASS_1,BABY_BASE) True
>>> DC2:constructor
>>> BC:constructor
>>> do2: {
>>> "base_object_var_1": 101,
>>> "base_object_var_2": 300,
>>> "base_object_var_3": 300.75,
>>> "derived_object_var_3": 300.29999999999995,
>>> "derived_object_var_5": 300,
>>> "base_class_var": 100.1,
>>> "CLASS": "DERIVED_CLASS_2"
>>> }
>>> isinstance(do2,BABY_BASE) True
>>> issubclass(DERIVED_CLASS_2,BABY_BASE) True
>>> DC1:constructor
>>> BC:constructor
>>> ddc {
>>> "base_object_var_1": 101,
>>> "base_object_var_2": 400,
>>> "base_object_var_3": 400.5,
>>> "derived_object_var_3": 200.2,
>>> "derived_object_var_4": 400,
>>> "base_class_var": 100.1,
>>> "CLASS": "DERIVED_GRAND_CHILD"
>>> }
>>> Yes implementation
>>> WTF python: c2
>>> instance of T: <__main__.T object at 0x10aa6d2d0>
>>> t.doc: hello world
>>> {'__module__': '__main__', '__doc__': 'I find Class:BabyBase and Object:baby_base incosistent', 'base_class_var': 100.1, '__init__': <function BABY_BASE.__init__ at 0x10aa767a0>, '__repr__': <function BABY_BASE.__repr__ at 0x10aa76b00>, 'abstract_func': <function BABY_BASE.abstract_func at 0x10aa76b90>, '__dict__': <attribute '__dict__' of 'BABY_BASE' objects>, '__weakref__': <attribute '__weakref__' of 'BABY_BASE' objects>}
```
