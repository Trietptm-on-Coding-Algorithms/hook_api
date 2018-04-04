# hook_api
Assembly block for hooking windows API functions.


It finds the addresses of API functions by parsing the `_IMAGE_IMPORT_DESCRIPTOR` structure entries inside the import table of the PE file. It first calculates the ROR(13) hash of the (module name + function name) and compares with the hash passed to block. If the hash matches it replaces IAT entry with the passed address.

![Description](https://github.com/EgeBalci/hook_api/raw/master/flow.png)

<strong>IMPORTANT !!</strong> 
- The function that is called with hook_api must be imported by the PE file or it will crash.
- Target process must not use ASLR or else block couldn't find the import table address.

## Example

Following code hooks the `DeleteFileA` windows API function using the hook_api block. After hooking the function it will always return nonzero value. When a process executes this code it will not able to delete any file.  

[![Description](https://github.com/EgeBalci/hook_api/raw/master/Example.png)]()