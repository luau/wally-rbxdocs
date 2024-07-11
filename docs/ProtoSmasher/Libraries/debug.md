# Debug

## debug.getregistry
```lua
table debug.getregistry(<none>)
```
Returns the registry table.

## debug.setmetatable
```lua
void debug.setmetatable(Variant object, table mt)
```
Sets the metatable for the given object to the given table. (mt can be nil)

## debug.getfenv
```lua
table debug.getfenv(Variant object)
```

## debug.setfenv
```lua
Variant debug.setfenv(Variant object, table env)
```
Sets the environment of the given object, returns object.

## debug.getmetatable
```lua
table debug.getmetatable(Variant object)
```
Returns the metatable of given object. (functions exactly like getrawmetatable)

## debug.getupvalue
```lua
variant debug.getupvalue(Variant<int, function> container, string upvalName)
```
Returns the value of a upvalue from the selected container based on the name.

## debug.getupvalues
```lua
table<variant> debug.getupvalues(Variant<int, function> container)
```
Returns a table of all upvalues from the selected container.

## debug.setupvalue
```lua
variant debug.setupvalue(Variant<int, function> container, string upvalName, Variant value)
```
Sets the value of the upvalue from the selected container based on the name. Returns boolean based on whether the upvalue was set successfully or not.

## debug.getconstants
```lua
table<variant> debug.getconstants(Variant<int, function> f)
```
Return's the constants of the given function. Function must be a lua function.

## debug.setconstant
```lua
void debug.setconstant(function f, int index, variant val)
```
Set's the constant at the given index for the given function. Index's are 1-based. Function must be a lua function.

## debug.upvalueid
```lua
userdata debug.upvalueid(function f, int n)
```
Returns an unique identifier (as a light userdata) for the upvalue numbered n from the given function. These unique identifiers allow a program to check whether different closures share upvalues. Lua closures that share an upvalue (that is, that access a same external local variable) will return identical ids for those upvalue indices.

## debug.upvaluejoin
```lua
void debug.upvaluejoin(function f1, int n1, function f2, int n2)
```
Make the n1-th upvalue of the Lua closure f1 refer to the n2-th upvalue of the Lua closure f2.

## debug.upvaluename
```lua
string debug.upvaluename(function f, int n)
```
Returns the name for the upvalue numbered n from the given function. Will return an empty string on C closures.
