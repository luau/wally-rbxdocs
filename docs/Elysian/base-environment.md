# Base Environment

## getrawmetatable
```lua
table getrawmetatable(variant<table, userdata> obj)
```
Returns the metatable from a table or userdata, even if it is locked.

## setrawmetatable
```lua
boolean setrawmetatable(variant<table, userdata> obj, table val)
```
Sets the metatable of a table or userdata, even if it is locked.

## isreadonly
```lua
boolean isreadonly(table val)
```
Returns true if the table is read-only.

## printconsole
```lua
boolean printconsole(string val [, number r, number g, number b])
```
Prints ``val`` to Elysian’s console with color ``r, g, b``. Default color is ``0, 0, 200``.

## printdebug
```lua
boolean printdebug(string val)
```
Prints ``val`` to the console (View->Console->Toggle)

## getobjects
```lua
string getobjects(content)
```
Internal function used by DataModel::GetObjects (see init.lua)

## readfile
```lua
string readfile(string filename)
```
Returns the contents of a file in the workspace folder

## loadfile
```lua
function loadfile(string filename)
```
Loads a file from the workspace folder. Returns nil and an error on error. Similar to executing ``loadstring(readfile(filename))``.

## getgenv
```lua
table getgenv()
```
Returns the global environment for Elysian.

## getrenv
```lua
table getrenv()
```
Returns the global environment for game scripts.

## Clipboard.set
```lua
boolean Clipboard.set(string data)
```
Sets the contents of the clipboard to ``data``.

## mouse1press

```lua
void mouse1press([number x, number y])
```
Presses the left mouse button.

## mouse1release
```lua
void mouse1release([number x, number y])
```
Releases the left mouse button.

## mouse1click
```lua
void mouse1click([number delay, number x, number y])
```
Clicks the left mouse button with an optional delay in between press and release. Delay default is ~0.03 seconds.

## mouse2press
```lua
void mouse2press([number x, number y])
```
Presses the right mouse button.

## mouse2release
```lua
void mouse2release([number x, number y])\
```
Releases the right mouse button.

## mouse2click
```lua
void mouse2click([number delay, number x, number y])
```
Clicks the right mouse button with an optional delay in between press and release. Delay default is ~0.03 seconds.

## keypress
```lua
void keypress(KeyCode key)
```
Presses a key. If a number is passed for ``key``, Elysian will interpret it as a [virtual key code](https://docs.microsoft.com/en-us/windows/win32/inputdev/virtual-key-codes) and attempt to convert it to a [KeyCode](https://developer.roblox.com/en-us/api-reference/enum/KeyCode) for compatibility with scripts created for older versions of Elysian.

## keyrelease
```lua
void keyrelease(KeyCode key)
```
Releases a key. If a number is passed for key, Elysian will interpret it as a virtual key code. See [keypress](../base-environment/#keypress).

## mousemove
```lua
void mousemove(number x, number y [, number dx, number dy])
```
Moves the cursor to a location inside Roblox’s window. ``dx`` and ``dy`` are optional mouse delta parameters to be sent to Roblox. If not provided, they are equivalent to ``x - current_mouse_position.X`` and ``y - current_mouse_position.Y`` respectively.

## mousemoverel
```lua
void mousemoverel(number dx, number dy)
```
Moves the cursor relatively.

## mousescroll
```lua
void mousescroll(boolean forward [, number x, number y])
```
Scrolls the mouse. For compatibility with scripts created for older versions of Elysian, a number can be passed to ``forward`` where a positive number scrolls the mouse up, a negative number scrolls the mouse down, and one scroll “click” is equal to 120.

## writefile
```lua
boolean writefile(string filename, string data [, boolean binary])
```

Writes data to a file in the workspace folder. Returns true if successful. 
!!! note 
	This will fail if attempting to access an outside directory.

## appendfile
```lua
boolean appendfile(string filename, string data [, boolean binary])
```
Appends data to a file in the workspace folder. Returns true if successful.

!!! note 
	This will fail if attempting to access an outside directory.

## saveinstance
```lua
void saveinstance(Instance instance, string name [, table options])
```
Saves an instance to a file in the workspace folder which can be later opened in Roblox Studio. Possible options (and their default values) can be seen below:
```lua
local defaultSettings = {
    DecompileMode = 0, -- 0 = don't decompile scripts, 1 = luadec, 2 = unluac
    NilInstances = false, -- save nil instances
    RemovePlayers = true, -- ignore players
    SavePlayerDescendants = false,
    DecompileTimeout = 10, -- unluac only
    UnluacMaxThreads = 5, -- the max number of java processes that should be running at one time (the higher this value is the faster the decompilation process)
    DecompileIgnore = {"StarterPlayer","Chat"} -- scripts inside these services are saved but not decompiled
}
```

## saveplace
```lua
void saveplace(string name [, table options])
```
Equivalent to ``saveinstance(game, name, options)``

## decompile
```lua
string decompile(variant<Instance, function> script [, string option])
```
Attempts to decompile ``script`` and returns the result. If ``option`` is provided and equal to “dump”, lua bytecode will be returned (similar to string.dump). It should be noted that due to Roblox’s changes to Lua’s VM and parser this bytecode is not reliable to use with unmodified decompilers. Returns nil and an error message on error.

## decompile
```lua
boolean decompile(variant<Instance, function> script, “unluac”, function callback(string result, string error), number timeout = 5)
```
If ``option`` is provided and equal to “unluac”, decompile decompiles with unluac. If invalid parameters are passed, nil and an error is returned. If not, decompile returns with true and a (Windows) thread is created that spawns a java process and waits for its output. Once the process ends, the callback is called with the result. If Java is not installed or another error occurs, the callback is called with nil and the error. 

!!! danger "WARNING: A new java process is created every time this function is called. Calling decompile too quickly or in excessive amounts may cause some java processes to hang or exhaust your computer of resources."

## checkcaller
```lua
boolean checkcaller()
```
Returns true if the function calling the function calling checkcaller is an Elysian function.

## setfflag
```lua
boolean setfflag(string fflag, string value)
```
Sets a FFlag’s value. Returns true if the flag was set succesfully or false if the flag doesn’t exist.

## getreg
```lua
table getreg()
```
Returns Lua’s registry [(LUA_REGISTRYINDEX)](https://www.lua.org/pil/27.3.2.html)

## getnilinstances
```lua
table getnilinstances()
```
Returns a list of nil instances.

## elysianexecute
```lua
void elysianexecute(string script [, Instance localscript])
```
Equivalent to executing a script through Elysian’s interface (pressing the execute button, etc). If ``localscript`` is provided, the script will be binded/linked to that instance. If not present, a new LocalScript will be created.

## newcclosure
```lua
function newcclosure(function f)
```
Disguises Lua function ``f`` as a C function. It is seen as a C function by other scripts and any errors thrown inside ``f`` are viewed as coming from the C function, not ``f`` (in other words, the existence of f can not be detected by viewing the error message, stack trace, or etc.). ``f`` is allowed to yield ( e.g. wait() ) but will resume outside of the function.

## replaceclosure
```lua
function replaceclosure(function target, function replacement)
```
Replaces a function with another function and returns a clone of the original. Once a function is replaced it cannot be replaced with any other function except for its clone/original. For a better understanding, see [this](https://pastebin.com/raw/nJSKgYX4) code. 

!!! danger "It should be noted that Lua doesn’t like people modifying internal structures and improper or extensive use of this function may cause unexpected crashes or other issues."

## restoreclosure
```lua
boolean restoreclosure(function target)
```
Restores a closure that has been overwritten with [replaceclosure](../base-environment/#replaceclosure). Returns false if the function has not been replaced.

## bit library
```lua
functions: bit.tobit, bit.tohex, bit.bnot, bit.band, bit.bor, bit.bxor, bit.lshift, bit.rshift, bit.arshift, bit.rol, bit.ror
```
Attempts to replicate [LuaJIT’s bit library](http://bitop.luajit.org/api.html).

Superseded by Roblox's **bit32** library.

## getallthreads
```lua
table getallthreads()
```
Returns an array of all existing Lua threads.

## getthreadobject
```lua
Instance getthreadobject([thread t])
```
Returns the script associated with a Lua thread. If ``t`` is not provided, the current thread is used.

## gettenv
```lua
table gettenv([thread t])
```
Returns a thread’s environment. If ``t`` is not provided, the current thread is used.

## getsenv
```lua
table getsenv(Instance script)
```
Searches for a thread associated with ``script`` and returns its environment (see init.lua for implementation).

## getlocals
```lua
table getlocals(number level)
```
Returns a Lua function’s local variables. The level parameter represents a function on the callstack, where 1 is the function calling getlocals, 2 is the function calling that function, and so on. The level provided cannot point to an Elysian or C function.

In [Luau-enabled games](../base-environment/#Luau), getlocals returns the function’s stack as an array instead of a dictionary of local names to local variables.

## setlocal
```lua
boolean setlocal(number level, string i, variant v)
```
Sets local variable ``i`` to value ``v`` in the function pointed to by level (see [getlocals](../base-environment/#getlocals)). Like getlocals, the function cannot be an Elysian or C function. Returns true if the variable was set successfully.

In [Luau-enabled games](../base-environment/#Luau), setlocal requires an integer index for i instead of a string.

## getupvals
```lua
table getupvals(variant<number, function> f)
```
Returns a Lua function’s upvalues. If a number is passed for f, it is interpreted as a level (see [getlocals](../base-environment/#getlocals) and [setlocal](../base-environment/#setlocal)). The function cannot be an Elysian or C function.

In [Luau-enabled games](../base-environment/#Luau), getupvals returns the function’s upvalues as an array instead of a dictionary of upvalue names to upvalues.

## setupval
```lua
boolean setupval(variant<number, function> f, string i, variant v)
```
Sets upvalue i to value v in function f. If a number is passed for f, it is interpreted as a level (see [getlocals](../base-environment/#getlocals) and [setlocal](../base-environment/#setlocal)). The function cannot be an Elysian or C function. Returns true if the upvalue was set successfully.

In [Luau-enabled games](../base-environment/#Luau), setupval requires an integer index for i instead of a string.

## getconsts
```lua
table getconsts(variant<number, function> f)
```
Returns a Lua function’s constants. If a number is passed for f, it is interpreted as a level.

## setconst
```lua
void setconst(variant<number, function> f, number i, variant v)
```
Sets constant number ``i`` to value ``v`` in function f. If a number is passed for ``f``, it is interpreted as a level.

## getgc
```lua
table getgc([boolean nomt])
```
Returns an array of all existing allocated objects in Lua. This includes strings, functions, threads, userdata, and more across all Roblox and Elysian scripts. Unless nomt is set, the returned table has a metatable with [__mode set to “v”](http://www.lua.org/manual/5.1/manual.html#2.10.2).

## islclosure
```lua
boolean islclosure(function f)
```
Returns true if ``f`` is a Lua function.

## gethui
```lua
Instance gethui()
```
Returns a hidden renderable container separate from CoreGui, PlayerGui, and et cetera. [ScreenGuis](https://developer.roblox.com/api-reference/class/ScreenGui) and [Messages](https://developer.roblox.com/api-reference/class/Message) parented to this container will render on top of CoreGui. Although parented to [game](https://developer.roblox.com/api-reference/class/DataModel), game scripts cannot enumerate Game’s children to find this container or use functions such as [FindFirstChild](https://developer.roblox.com/api-reference/function/Instance/FindFirstChild) to find the container or any of its descendants. Objects added to and removed from the container will not fire [DescendantAdded](https://developer.roblox.com/api-reference/event/Instance/DescendantAdded) or [DescendantRemoving](https://developer.roblox.com/api-reference/event/Instance/DescendantRemoving) signals on game.

## getbspval
```lua
string getbspval(Instance object, string property [, boolean base64])
```
Reads a BinaryString property’s value. Useful for reading conventionally unreadable BinaryString properties such as Terrain.SmoothGrid, PartOperation.PhysicsData, [BinaryStringValue](https://developer.roblox.com/api-reference/class/BinaryStringValue).Value, and so on.

## getnspval
```lua
variant getnspval(Instance object, string property)
```
Returns a property’s value, even if it is unscriptable.

## getunionassetid
```lua
string getunionassetid(Instance union)
```
Equivalent to ``getnspval(union, "AssetId")``

## getconnections
```lua
table getconnections(RBXScriptSignal signal)
```
Returns a list of Lua and engine connections to signal.

## isluau
```lua
boolean isluau()
```
Returns true if the game is running on Roblox’s new Lua implementation, [Luau](../base-environment/#Luau).

## getnamecallmethod
```lua
string getnamecallmethod()
```
Returns the method parameter in the context of a __namecall metamethod. Only applies to [Luau-enabled games](../base-environment/#Luau). See init.lua for example usage.

## **Luau**

Luau is a custom, speedy Lua implementation created by Roblox. It was first spotted in early April of 2019 before being [publicly announced](https://devforum.roblox.com/t/faster-lua-vm-studio-beta/298659) by Roblox in late June. Luau does not change Lua’s syntax or behavior but implements a much faster runtime using optimizations in the parser and virtual machine.

## Elysian Support (v3.3.0+) & Developer Notes

* Elysian’s Luau support includes most, but not all, of Luau’s available optimizations.
* Decompiling Luau scripts is not yet possible due to Luau’s completely different bytecode and instruction set. A decompiler will be coming soon, courtesy of the [Synapse X](https://x.synapse.to) team <3.
* Luau bytecode does not include local or upvalue name information. As a result, [getlocals](../base-environment/#getlocals), [setlocal](../base-environment/#setlocal), [getupvals](../base-environment/#getupvals), and [setupval](../base-environment/#setupval) now require indices (integers) instead of names (strings) in Luau-enabled games.
* One Luau optimization removes the method parameter of the __namecall metamethod. In Luau-enabled games, this parameter must now be obtained via the [getnamecallmethod]](../base-environment/#getnamecallmethod) function.

## **[RBXScriptSignal](https://developer.roblox.com/api-reference/datatype/RBXScriptSignal) Extensions**

## **Properties**
```lua
boolean Scriptable [readonly]
```
Determines whether or not a signal is scriptable. Calling Connect or Wait on non-scriptable signals has no effect.

## **Functions**
```lua
RBXScriptConnection RBXScriptSignal:Connect(function func)
```
In Elysian, Connect works as normal but can also register connections to non-scriptable signals. A list of non-scriptable/internal signals will appear here in the future.

```lua
table RBXScriptSignal:GetConnections()
```
Equivalent to ``getconnections(signal)``

## **[RBXScriptConnection](https://developer.roblox.com/api-reference/datatype/RBXScriptConnection) Extensions**

## **Properties**
```lua
boolean LuaConnection [readonly]
```
Determines whether or not the connection is attached to a Lua function.

```lua
boolean Enabled
```
Determines whether or not the connection is enabled. Disabled connections will not fire. Both Lua and engine connections can be disabled. Anti-AFK can now by achieved with a few lines of code:
```lua
for i, v in pairs(game:GetService"Players".LocalPlayer.Idled:GetConnections()) do
    if not v.LuaConnection then
        v.Enabled = false
    end
end
```

This works by disabling a connection created by Roblox’s engine responsible for kicking the client when the user has been idle for more than 20 minutes.

## **Functions**
```lua
function RBXScriptConnection:GetFunction()
```
Returns a connection’s associated Lua function or nil if the connection is not a Lua connection or the function belongs to another Lua instance (corescript state, etc.)

```lua
void RBXScriptConnection:GetThread()
```
Returns a connection’s associated Lua thread or nil if the connection is not a Lua connection or the thread belongs to another Lua instance (corescript state, etc.)
