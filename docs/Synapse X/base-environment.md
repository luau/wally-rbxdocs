# Base Environment

## hookfunction
```lua
hookfunction(<function> old, <function> hook)
```

Hooks function 'old', replacing it with the function 'hook'. The old function is returned, you must use it to call the function further.

## getgenv
```lua
getgenv(<void>)
```

Returns the environment that will be applied to each script ran by Synapse.

## keyrelease
```lua
keyrelease(<int> key)
```

Releases 'key' on the keyboard. You can access the int key values on MSDN.

## setclipboard
```lua
setclipboard(<string> value)
```

Sets 'value' to the clipboard.

## mouse2press
```lua
mouse2press(<void>)
```

Clicks down on the right mouse button.

## getsenv
```lua
getsenv(<LocalScript, ModuleScript> Script)
```

Returns the environment of Script. Returns nil if the script is not running.

## checkcaller
```lua
checkcaller(<void>)
```

Returns true if the current thread was made by Synapse. Useful for metatable hooks.

# **bit**

!!! note 
	This has been deprecated in favor of Roblox's **bit32** library, which has the same functionality.

## bit.bdiv
```lua
bit.bdiv(<uint> dividend, <uint> divisor)
```

Divides 'dividend' by 'divisor', remainder is not returned.

## bit.badd
```lua
bit.badd(<uint> a, <uint> b)
```

Adds 'a' with 'b', allows overflows (unlike normal Lua).

## bit.badd
```lua
bit.bsub(<uint> a, <uint> b)
```

Subtracts 'a' with 'b', allows overflows (unlike normal Lua).

## bit.rshift
```lua
bit.rshift(<uint> val, <uint> by)
```

Does a right shift on 'val' using 'by'.

## bit.band
```lua
bit.band(<uint> val, <uint> by)
```

Does a logical AND (&) on 'val' using 'by'.

## bit.bor
```lua
bit.bor(<uint> val, <uint> by)
```

Does a logical OR (|) on 'val' using 'by'.

## bit.bxor
```lua
bit.bxor(<uint> val, <uint> by)
```

Does a logical XOR (^) on 'val' using 'by'.

## bit.bnot
```lua
bit.bnot(<uint> val)
```

Does a logical NOT on 'val'.

## bit.bmul
```lua
bit.bmul(<uint> val, <uint> by)
```

Multiplies 'val' using 'by', allows overflows (unlike normal Lua)

## bit.bswap
```lua
bit.bswap(<uint> val)
```

Does a bitwise swap on 'val'.

## bit.tobit
```lua
bit.tobit(<uint> val)
```

Converts 'val' into proper form for bitwise operations.

## bit.ror
```lua
bit.ror(<uint> val, <uint> by)
```

Rotates right 'val' using 'by'.

## bit.lshift
```lua
bit.lshift(<uint> val, <uint> by)
```

Does a left shift on 'val' using 'by'.

## bit.tohex
```lua
bit.tohex(<uint> val)
```

Converts 'val' to a hex string.

# **debug**

## debug.getconstant
```lua
debug.getconstant(<function, int> fi, <int> idx)
```

Returns the constant at index 'idx' in function 'fi' or level 'fi'.

## debug.profilebegin
```lua
debug.profilebegin(<string> label>
```

Opens a microprofiler label.

## debug.profileend
```lua
debug.profileend(<void>)
```

Closes the top microprofiler label.

## debug.traceback
```lua
debug.traceback(<void>)
```

Returns a traceback of the current stack as a string.

## debug.getfenv
```lua
debug.getfenv(<T> o)
```

Returns the environment of object 'o'.

## debug.getupvalue
```lua
debug.getupvalue(<function, int> fi, <string> upval)
```

Returns the upvalue with name 'upval' in function or level 'fi'.

## debug.getlocals
```lua
debug.getlocals(<int> lvl)
```

Returns a table containing the upvalues at level 'lvl'.

## debug.setmetatable
```lua
debug.setmetatable(<T> o, <table> mt)
```

Set the metatable of 'o' to 'mt'.

## debug.getconstants
```lua
debug.getconstants(<function, int> fi)
```

Retrieve the constants in function 'fi' or at level 'fi'.

## debug.getupvalues
```lua
debug.getupvalues(<function, int> fi)
```

Retrieve the upvalues in function 'fi' or at level 'fi'.

## debug.setupvalue
```lua
debug.setupvalue(<function, int> fi, <number> indice, <T> value)
```

Set upvalue at number 'indice' to value 'value' at level or function 'fi'.

## debug.setupvalue
```lua
debug.setconstant(<function, int> fi, <string> consname, <int, bool, nil, string> value)
```

Set constant 'consname' to tuple 'value' at level or function 'fi'.

## debug.getregistry
```lua
debug.getregistry(<void>)
```

Returns the lua registry

## debug.getinfo
```lua
debug.getinfo(<function, int> fi, <string> w)
```

Returns a table of info pertaining to the Lua function 'fi'.

## debug.getlocal
```lua
debug.getlocal(<int> lvl, <number> indice)
```

Returns the local with number 'indice' in level 'lvl'.

## debug.getstack
```lua
table<Variant> debug.getstack(int stackpos[, int index])
```
Returns the stack for the function at level 'stackpos'. Put index for a single value.

## debug.setstack
```lua
void debug.setstack(int stackpos, int index, Variant value)
```
Sets stack at stackpos with index to value.

# debug.\*proto
The new debug.*proto functions are a new useful addition to the debug API that fixes a common problem in scripts: getting inner functions.

!!! note 
	There is not much documentation for these functions, but there are some examples of usage!

Example:
```lua
local wow = "same"

local function test()
    local function asd()
        --we want this function!
        print(wow)
        wow = wow .. "a"
        print'hello!'
    end

    game:GetService("RunService").RenderStepped:Connect(asd)
end
```

While we can use getrenv() iteration since "asd" is connected as an event, lets say we got the 'test' function another way and we want to get 'asd'. This is a great usecase for the new debug API functions.
```lua
local test = ... --found via some other method

for i,v in pairs(debug.getprotos(test)) do 
    print(i, v)
end

--1 function: XXXXXXXX
```

As we can see, we now have the function! There is a catch though - this function is deactivated. We can get the constants (and decompile it once LuaU decompilation is complete), but we cannot call it or get any upvalues. In order to do that, we have to get an activated version of this function instead.
Lets try to get an activated version instead.

```lua
local test = ... --found via some other method

--1 is the index of the function we want to get (the first one in this case), and the 'true' specifies to find activated functions.
for i,v in pairs(debug.getproto(test, 1, true)) do 
    print(i, v)
    print(v()) --We can call it this time...
    table.foreach(debug.getupvalues(v), warn) --..and get upvalues!
end
```

## loadfile
```lua
loadfile(<string> path)
```

Loads in the contents of a file as a chunk and returns it if compilation is successful. Otherwise, if an error has occured during compilation, nil followed by the error message will be returned.

## loadstring
```lua
loadstring(<string> chunk, [<string> chunkname])
```

Loads 'chunk' as a Lua function and returns it if compilation is succesful. Otherwise, if an error has occured during compilation, nil followed by the error message will be returned.

## writefile
```lua
writefile(<string> filepath, <string> contents)
```

Writes 'contents' to the supplied filepath.

## mousescroll
```lua
mousescroll(<signed int> px)
```

Scrolls the mouse wheel virtually by 'px' pixels.

## mouse2click
```lua
mouse2click(<void>)
```

Virtually presses the right mouse button.

## islclosure
```lua
islclosure(<function> f)
```

Returns true if 'f' is an LClosure

## mouse1press
```lua
mouse1press(<void>)
```

Simulates a left mouse button press without releasing it.

## mouse1release
```lua
mouse1release(<void>)
```

Simulates a left mouse button release.

## keypress
```lua
keypress(<int> keycode)
```

Simulates a key press for the specified [keycode](https://docs.microsoft.com/en-us/windows/desktop/inputdev/virtual-key-codes)

## mouse2release
```lua
mouse2release(<void>)
```

Simulates a right mouse button release.

## newcclosure
```lua
newcclosure(<function> f)
```

Pushes a new c closure that invokes function 'f' upon call. Used for metatable hooks.

## getinstances
```lua
getinstances(<void>)
```

Returns a list of all instances within the game.

## getnilinstances
```lua
getnilinstances(<void>)
```

Returns a list of all instances parented to nil within the game.

## readfile
```lua
readfile(<string> path)
```

Reads the contents of the file located at 'path' and returns it. If the file does not exist, it errors.

## getscripts
```lua
getscripts(<void>)
```

Returns a list of all scripts within the game.

## getrunningscripts
```lua
getrunningscripts(<void>)
```

Returns a list of all scripts currently running.

## appendfile
```lua
appendfile(<string> path, <string> content)
```

Appends 'content' to the file contents at 'path'. If the file does not exist, it errors

## listfiles
```lua
listfiles(<string> folder)
```

Returns a table of files in 'folder'.

## isfile
```lua
isfile(<string> path)
```

Returns if 'path' is a file or not.

## isfolder
```lua
isfolder(<string> path)
```

Returns if 'path' is a folder or not.

## delfolder
```lua
delfolder(<string> path)
```

Deletes 'folder' in the workspace directory.

## delfile
```lua
delfile(<string> path)
```

Deletes 'file' from the workspace directory.

## getreg
```lua
getreg(<void>)
```

Returns the Lua registry.

## getgc
```lua
getgc(<void>)
```

Returns a copy of the Lua GC list.

## mouse1click
```lua
mouse1click(<void>)
```

Simulates a full left mouse button press.

## getrawmetatable
```lua
getrawmetatable(<T> value)
```

Retrieve the metatable of value irregardless of value's metatable's __metatable field. Returns nil if it doesn't exist.

## setreadonly
```lua
setreadonly(<table> table, <bool> ro)
```

Sets table's read-only value to ro

## isreadonly
```lua
isreadonly(<table> table)
```

Returns table's read-only condition.

## getrenv
```lua
getrenv(<void>)
```

Returns the global Roblox environment for the LocalScript state.

## decompile
```lua
decompile(<LocalScript, ModuleScript, function> Script, bool Bytecode = false)
```

Decompiles Script and returns the decompiled script. If the decompilation fails, then the return value will be an error message.

## dumpstring
```lua
dumpstring(<string> Script)
```

Returns the Roblox formatted bytecode for source string 'Script'.

## getloadedmodules
```lua
getloadedmodules(<void>)
```

Returns all ModuleScripts loaded in the game.

## getloadedmodules
```lua
isrbxactive(<void>)
```

Returns if the Roblox window is in focus.

## getcallingscript
```lua
getcallingscript(<void>)
```

Gets the script that is calling this function.

## setnonreplicatedproperty
```lua
setnonreplicatedproperty(<Instance> obj, <string> prop, <T> value)
```

Sets the prop property of obj, not replicating to the server. Useful for anticheat bypasses.

## getspecialinfo
```lua
getspecialinfo(<Instance> obj)
```

Gets a list of special properties for MeshParts, UnionOperations, and Terrain.

## messagebox
```lua
messagebox(<string> message, <string> title, <int> options)
```

Makes a MessageBox with 'message', 'title', and 'options' as options. See [this article](https://docs.microsoft.com/en-us/windows/desktop/api/winuser/nf-winuser-messagebox) for more information.

## messageboxasync
```lua
messageboxasync(<string> message, <string> title, <int> options)
```

Makes a MessageBox with 'message', 'title', and 'options' as options. Runs asynchronously. See [this article](https://docs.microsoft.com/en-us/windows/desktop/api/winuser/nf-winuser-messagebox) for more information.

## rconsolename
```lua
rconsolename(<string> title)
```

Sets the currently allocated console title to 'title'.

## rconsoleinput
```lua
rconsoleinput(<void>)
```

Yields until the user inputs information into ther console. Returns the input the put in.

## rconsoleinputasync
```lua
rconsoleinputasync(<void>)
```

Yields until the user inputs information into ther console. Returns the input the put in.

## rconsoleprint
```lua
rconsoleprint(<string> message)
```

Prints 'message' into the console.

## rconsoleinfo
```lua
rconsoleinfo(<string> message)
```

Prints 'message' into the console, with a info text before it.

## rconsolewarn
```lua
rconsolewarn(<string> message)
```

Prints 'message' into the console, with a warning text before it.

## rconsoleerr
```lua
rconsoleerr(<string> message)
```

Prints 'message' into the console, with a error text before it.

## fireclickdetector
```lua
fireclickdetector(<ClickDetector> detector, <number, nil> distance)
```

Fires click detector 'detector' with 'distance'. If a distance is not provided, it will be 0.


!!! note 
	firetouchinterest, getconnections and some other functions are currently broken and will crash when attempting to call them. These functions will hopefully be fixed in the future.

## getconnections
```lua
getconnections(<Signal> obj)
```

Gets a list of connections to the specified signal. You can then use :Disable and :Enable on the connections to disable/enable them.

## firetouchinterest
```lua
firetouchinterest(<Part> part, <TouchTransmitter> transmitter, <number> toggle)
```

Fires touch 'transmitter' with 'part'. Use 0 to toggle it being touched, 1 for it not being toggled.

## saveinstance
```lua
saveinstance(<table> t)
```

Saves the Roblox game into your workspace folder.

# **syn**

## syn.crypt.encrypt
```lua
syn.crypt.encrypt(<string> data, <string> key)
```

Encrypt's data with key.

## syn.crypt.decrypt
```lua
syn.crypt.decrypt(<string> data, <string> key)
```

Decrypt's data with key.

## syn.crypt.decrypt
```lua
syn.crypt.hash(<string> data)
```

Hashes data.

## syn.crypt.base64.encode
```lua
syn.crypt.base64.encode(<string> data)
```

Encodes data with base64.

## syn.crypt.base64.encode
```lua
syn.crypt.base64.decode(<string> data)
```

Decodes data with base64.

## syn.cache_replace
```lua
syn.cache_replace(<Instance> obj, <Instance> t_obj)
```

Replace obj in the cache with t_obj.

## syn.invalidate_cache
```lua
syn.cache_invalidate(<Instance> obj)
```

Invalidate obj's cache entry, forcing a recache upon the next lookup.

## syn.set_thread_identity
```lua
syn.set_thread_identity(<int> n)
```

Sets the current thread identity after a Task Scheduler cycle is performed. (call wait() after invoking this function for the expected results)

## syn.get_thread_identity
```lua
syn.get_thread_identity(<void>)
```

Returns the current thread identity.

## syn.is_cached
```lua
syn.is_cached(<Instance> obj)
```

Returns true if the instance is currently cached within the registry.

## syn.write_clipboard
```lua
syn.write_clipboard(<string> content)
```

Writes 'content' to the current Windows clipboard.

## syn.request
```lua
wally no brain
```

## mousemoverel
```lua
mousemoverel(<int> x, <int> y)
```

Moves the mouse cursor relatively to the current mouse position by coordinates 'x' and 'y'.

## syn.cache_replace
```lua
syn.cache_replace(<Instance> obj, <Instance> t_obj)
```

Replace obj in the cache with t_obj.

## syn.invalidate_cache
```lua
syn.cache_invalidate(<Instance> obj)
```

Invalidate obj's cache entry, forcing a recache upon the next lookup.

## syn.queue_on_teleport
```lua
wally no brain
```

## syn.open_web_socket
```lua
syn.open_web_socket(<string> name)
```

Open's the Synapse WebSocket with channel name. This function will not exist if the user did not enable WebSocket support in theme.json.
