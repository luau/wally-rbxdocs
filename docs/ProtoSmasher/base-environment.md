# Base Environment

## getgenv
```lua
table getgenv()
```
Returns the global environment table for ProtoSmasher.

## getrenv
```lua
table getrenv()
```
Returns the table of all ROBLOX globals.

## getrawmetatable
```lua
table getrawmetatable(variant<Userdata, string, table> object)
```
Returns the metatable of the passed object, ignores the __metatable metafield.
Object could be locked, check is is_readonly, and is_writeable, or change with make_readonly and make_writable

## getsenv
```lua
table getsenv(Object<LocalScript> script)
```
Returns the global environment of the given script.

## getmenv
```lua
table getmenv(Object<ModuleScript> script)
```
Returns the global environment of the given ModuleScript.

## getscriptenvs
```lua
table getscriptenvs(<none>)
```
Returns a table of all scripts and their global environments. (key = script, value = environment)

## loadstring
```lua
variant<function, (nil, string)> loadstring(string sourceCode, string chunkName = "@(Random String)")
```
Converts plain lua source code into a function. Returns nil and a string on error. Will follow the set execution method.

## loadfile
```lua
function loadfile(string filePath)
```
Returns a function from the file, the equivalent of "loadstring(readfile(filePath))", except more efficient. Will follow the set execution method.

## dofile
```lua
function dofile(string filePath)
```
Executes the lua source code from the file, the equivalent of "loadstring(readfile(filePath))()", Will follow the set execution method.

## make_writeable
```lua
void make_writeable(table tbl)
```
Changes the readonly flag of a table.

## make_readonly
```lua
void make_readonly(table tbl)
```
Changes the readonly flag of a table.

## is_writeable
```lua
bool is_writeable(table tbl)
```
Returns weather or not the table is writeable.

## is_readonly
```lua
bool is_readonly(table tbl)
```
Returns weather or not the table is read only.

## is_protosmasher_caller
```lua
boolean is_protosmasher_caller(<none>)
```
This checks if the current caller is a protosmasher thread. (used internally for getobjects)

## is_protosmasher_closure
```lua
boolean is_protosmasher_closure(function f)
```
Returns a boolean based on whether or not the function was created by ProtoSmasher.

## getobjects
```lua
Array<Object> getobjects(Object<DataModel> dataModel, string ContentString)
```
Internal function used by ProtoSmasher for DataModel::GetObjects.

## get_nil_instances
```lua
table<Object> get_nil_instances(<none>)
```
Returns all nil parented instances from the localscript state.

## get_thread_context
```lua
int get_thread_context(<none>)
```
Returns the current context of the caller.

## dump_function
```lua
string dump_function(function f)
```
Returns the regular lua bytecode of the given function.

## get_script_function
```lua
function get_script_function(Object<ModuleScript, LocalScript> script)
```
Returns a function of the script (cannot be called but can be passed to dump_function).

## bytecode_to_lua
```lua
string bytecode_to_lua(string byteCode)
```
Used to convert lua 5.1 bytecode into lua sourcecode (requires unluac.jar in workspace and java be installed)

## writefile
```lua
void writefile(string filePath, string contentsToWrite, boolean isBinary = false)
```
Writes the contents of "contentsToWrite" to the provided file (sandboxed to workspace).

## readfile
```lua
string readfile(string pathToFile)
```
Returns the files contents (sandboxed to workspace).

## decompile
```lua
string decompile(variant<Object, function> obj, string optionalArg = nil)
```
Returns the decompiled source code of a script or function. (if you want bytecode put optionalArg as "dumponly")

## setclipboard
```lua
void setclipboard(string strToCopy)
```
Sets the clipboard text to the contents of strToCopy

## pebc_create
```lua
string pebc_create(function toEncrypt)
```
Returns ProtoSmasher Encrypted Bytecode (TM) of the given function (can only be used by people i select, otherwise it will just throw an error.)

## pebc_load
```lua
function pebc_load(string pebc)
```
Loads ProtoSmasher Encrypted Bytecode (TM) and returns it in a function form.

## saveinstance
```lua
void saveinstance(Object instanceToSave, string fileName, bool enableScriptDecompiling)
```
Converts the given instance into roblox's xml instance format and saves it to the saved under the given file name. When enableScriptDecompiling is enabled it will automatically decompile any modulescript or localscript it encounters.

## disconnect_all
```lua
void disconnect_all(RBXScriptSignal signal)
```
Disconnects all connections from a given signal. (should note this might not work for events on datamodel, same for get_signal_connections)

## unlock_modulescript
```lua
void unlock_modulescript(Object<ModuleScript> signal)
```
Unlocks a given ModuleScript so it can be required via ProtoSmasher (Used by require now)

## printoutput
```lua
void printoutput(string text, Color3 color = Color3(1, 1, 1), bool newLine = true)
```
Prints the output of ProtoSmasher, with optional formatting.

## get_renderstep_list
```lua
table get_renderstep_list(<none>)
```
Return a table of everything thats connected to RenderStep via BindToRenderStepEarly. The table is as following: key 1 is the priority, key 2 is the name, key 3 is the function.

## setfflag
```lua
bool setfflag(string flag, string value)
```
 Set's the value of an FFlag and returns whether it was successfully set or not. Click here to view most if not all FFlags for the client.

## DebuggerManager
```lua
Object<DebuggerManager> DebuggerManager(<none>)
```
 Returns the object interface for ROBLOX's script debugger. You can view its documentation here

## get_calling_script
```lua
Object<LocalScript, ModuleScript> get_calling_script(int level)
```
Returns the script object from the specificed stack level.

## protect_function
```lua
function protect_function(function f)
```
Returns a proxy function that will aide in making the function undetectable via stack trace errors. Function must be a ProtoSmasher closure.

## is_protected_closure
```lua
bool is_protected_closure(function f)
```
Returns a boolean whether or not the function is protected. Will return false instead of erroring with C closures.

## get_loaded_modules
```lua
table<Object> get_loaded_modules(<none>)
```
Returns a table populated with all loaded ModuleScript's in the game. Automatically filters out CoreGui modules.

## detour_function
```lua
function detour_function(function f, function detour)
```
Detour's the given function to the passed detour function, meaning everytime the function is called, your function will be called instead. This replaces the function and therfore does not change the value of tostringing it. A clone of the original function will be returned.

## parse_url
```lua
array<string, string> parse_url(string url)
```
Returns a table populated with various information about the passed url. Current information: protocol, domain, port, resource, query

## get_script_bytecode
```lua
string get_script_bytecode(Object<ModuleScript, LocalScript> script)
```
Returns the given script's bytecode in regular lua format. This is similar to dump_function combined with get_script_function, but this is more efficient.

## get_hidden_gui
```lua
Object get_hidden_gui(<none>)
```
Returns a Instance you can use parent Gui's to. Anything in here will be undetectable from things like CoreGui checks and such.

## get_gc_objects
```lua
array<Variant> get_gc_objects(<none>)
```
Returns a table containing most of the objects that exist in the current lua state.

## click_detector
```lua
void click_detector(Object<ClickDetector> detector, float Distance)
```
Clicks a ClickDetector automatically when called. The distance argument must be less than the MaxActivationDistance property.

## is_l_closure
```lua
bool is_l_closure(function f)
```
Returns a boolean that indicates whether or not the function is a Lua Closure or a C Closure.

## compare_c_functions
```lua
bool compare_c_functions(function f1, function f2)
```
Returns a boolean that indicates whether or not the functions internally call the same C function. Will error if either function is not a C closure.

## appendfile
```lua
void appendfile(string filePath, string contentsToWrite, boolean isBinary = false)
```
Appends the contents of "contentsToWrite" to the end of the provided file (sandboxed to workspace).