# Base Environment

## Get Global Environment
```lua
table getgenv()
```
Returns the global environment table for ProtoSmasher.

## Get Roblox Environment
```lua
table getrenv()
```
Returns the table of all Roblox globals.

## Get Raw Metatable
```lua
table getrawmetatable(variant<Userdata, string, table> object)
```
Returns the metatable of the passed object, ignores the __metatable metafield.
The object could be locked, to check use `is_readonly` or `is_writeable`, and change accordingly with `make_writeable` or `make_readonly`

## Get Script Environment
```lua
table getsenv(Object<LocalScript> script)
```
Returns the global environment of the given script.

## Get ModuleScript Environment
```lua
table getmenv(Object<ModuleScript> script)
```
Returns the global environment of the given ModuleScript.

## Get Script Environment Table
```lua
table getscriptenvs(<none>)
```
Returns a table of all scripts and their global environments. (key = script, value = environment)

## Loadstring
```lua
variant<function, (nil, string)> loadstring(string sourceCode, string chunkName = "@(Random String)")
```
Converts plain Lua source code into a function. Returns nil and a string on error. Will follow the set execution method.

## Loadfile
```lua
function loadfile(string filePath)
```
Returns a function from the file, the equivalent of "loadstring(readfile(filePath))", except more efficient. Will follow the set execution method.

## Dofile
```lua
function dofile(string filePath)
```
Executes the Lua source code from the file, the equivalent of "loadstring(readfile(filePath))()", Will follow the set execution method.

## Make Writeable
```lua
void make_writeable(table tbl)
```
Changes the readonly flag of a table.

## Make Readonly
```lua
void make_readonly(table tbl)
```
Changes the readonly flag of a table.

## Is Writeable
```lua
bool is_writeable(table tbl)
```
Returns whether or not the table is writeable.

## Is Readonly
```lua
bool is_readonly(table tbl)
```
Returns whether or not the table is read only.

## Is ProtoSmasher Caller
```lua
boolean is_protosmasher_caller(<none>)
```
This checks if the current caller is a ProtoSmasher thread. (used internally for getobjects)

## Is ProtoSmasher Closure
```lua
boolean is_protosmasher_closure(function f)
```
Returns a boolean based on whether or not the function was created by ProtoSmasher.

## Get Objects
```lua
Array<Object> getobjects(Object<DataModel> dataModel, string ContentString)
```
Internal function used by ProtoSmasher for DataModel::GetObjects.

## Get Nil Instances
```lua
table<Object> get_nil_instances(<none>)
```
Returns all nil parented instances from the LocalScript state.

## Get Thread Context
```lua
int get_thread_context(<none>)
```
Returns the current context of the caller.

## Dump Function
```lua
string dump_function(function f)
```
Returns the regular Lua bytecode of the given function.

## Get Script Function
```lua
function get_script_function(Object<ModuleScript, LocalScript> script)
```
Returns a function of the script (cannot be called but can be passed to dump_function).

## Bytecode to Lua
```lua
string bytecode_to_lua(string byteCode)
```
Used to convert Lua 5.1 bytecode into Lua source code (requires unluac.jar in workspace and Java be installed)

## Write File
```lua
void writefile(string filePath, string contentsToWrite, boolean isBinary = false)
```
Writes the contents of `contentsToWrite` to the provided file (sandboxed to workspace).

## Read File
```lua
string readfile(string pathToFile)
```
Returns the contents of the file at `pathToFile` (sandboxed to workspace).

## Decompile
```lua
string decompile(variant<Object, function> obj, string optionalArg = nil)
```
Returns the decompiled source code of a script or function. (if you want bytecode put optionalArg as "dumponly")

## Set Clipboard
```lua
void setclipboard(string strToCopy)
```
Sets the clipboard text to `strToCopy`

## Pebc Create
```lua
string pebc_create(function toEncrypt)
```
Returns ProtoSmasher Encrypted Bytecode (TM) of the given function (can only be used by people I select, otherwise it will just throw an error.)

## Pebc Load
```lua
function pebc_load(string pebc)
```
Loads ProtoSmasher Encrypted Bytecode (TM) and returns it in a function form.

## Save Instance
```lua
void saveinstance(Object instanceToSave, string fileName, bool enableScriptDecompiling)
```
Converts the given instance into Roblox's XML instance format and saves it to the saved under the given file name. When `enableScriptDecompiling` is true it will automatically decompile any ModuleScript or LocalScript it encounters.

## Disconnect all
```lua
void disconnect_all(RBXScriptSignal signal)
```
Disconnects all connections from a given signal. (should note this might not work for events on datamodel, same for get_signal_connections)

## Unlock Modulescript
```lua
void unlock_modulescript(Object<ModuleScript> signal)
```
Unlocks a given ModuleScript so it can be required via ProtoSmasher (Used by require now)

## Print Output
```lua
void printoutput(string text, Color3 color = Color3(1, 1, 1), bool newLine = true)
```
Prints the output of ProtoSmasher, with optional formatting.

## Get Renderstep List
```lua
table get_renderstep_list(<none>)
```
Return a table of everything thats connected to RenderStep via BindToRenderStepEarly. The table is as following: key 1 is the priority, key 2 is the name, key 3 is the function.

## Set Fflag
```lua
bool setfflag(string flag, string value)
```
 Set's the value of an FFlag and returns whether it was successfully set or not. Click [here](https://clientsettings.api.roblox.com/Setting/QuietGet/ClientAppSettings/?apiKey=D6925E56-BFB9-4908-AAA2-A5B1EC4B2D79) to view most if not all FFlags for the client.

## Debugger Manager
```lua
Object<DebuggerManager> DebuggerManager(<none>)
```
 Returns the object interface for Roblox's script debugger. You can view its documentation [here](http://robloxdev.com/api-reference/class/DebuggerManager)

## Get Calling Script
```lua
Object<LocalScript, ModuleScript> get_calling_script(int level)
```
Returns the script object from the specificed stack level.

## Protect Function
```lua
function protect_function(function f)
```
Returns a proxy function that will aide in making the function undetectable via stack trace errors. Function must be a ProtoSmasher closure.

## Is Protected Closure
```lua
bool is_protected_closure(function f)
```
Returns a boolean whether or not the function is protected. Will return false instead of erroring with C closures.

## Get Loaded Modules
```lua
table<Object> get_loaded_modules(<none>)
```
Returns a table populated with all loaded ModuleScript's in the game. Automatically filters out CoreGui modules.

## Detour Function
```lua
void detour_function(function f, function detour, bool ignoreSizeChecks = false)
```
Detours the function `f` to the passed function `detour`, meaning everytime the function is called, your function will be called instead. This replaces the function itself, thus calling `tostring` on it will return the same value. Detour functions that are Lua will have a new global variable called `original_function` that you can call to call the original function. Will error if the detour function is larger than the original function, size increases are caused by upvalues. The parameter `ignoreSizeChecks` will not throw an error if the detour function is bigger than the function to be detoured. This can cause a crash and should be used with caution.

## Parse URL
```lua
array<string, string> parse_url(string url)
```
Returns a table populated with various information about the passed url. Current information: protocol, domain, port, resource, query

## Get Script Bytecode
```lua
string get_script_bytecode(Object<ModuleScript, LocalScript> script)
```
Returns the given script's bytecode in regular Lua format. This is similar to `dump_function` combined with `get_script_function`, but this is more efficient.

## Get Hidden GUI
```lua
Object get_hidden_gui(<none>)
```
Returns a Instance you can use parent GUIs to. Anything in here will be undetectable from things like CoreGui checks and such.

## Get GC Objects
```lua
array<Variant> get_gc_objects(<none>)
```
Returns a table containing most of the objects that exist in the current Lua state.

## Click Detector
```lua
void click_detector(Object<ClickDetector> detector, float Distance)
```
Clicks a ClickDetector automatically when called. The distance argument must be less than the MaxActivationDistance property.

## Is L Closure
```lua
bool is_l_closure(function f)
```
Returns a boolean that indicates whether or not the function is a Lua Closure or a C Closure.

## Compare C Functions
```lua
bool compare_c_functions(function f1, function f2)
```
Returns a boolean that indicates whether or not the functions internally call the same C function. Will error if either function is not a C closure.

## Append File
```lua
void appendfile(string filePath, string contentsToWrite, boolean isBinary = false)
```
Appends the contents of `contentsToWrite` to the end of the file at `filePath` (sandboxed to workspace).