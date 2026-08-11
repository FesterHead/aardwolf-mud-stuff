# Lua Modules Directory

This directory contains external shared Lua libraries, utility modules, and script dependencies.

## Purpose

Instead of writing extremely long inline scripts inside the MUSHclient plugin XML definitions, put complex algorithms, modular components, and reusable library scripts here. This keeps the plugins easier to maintain and read.

## Best Practices

1. **Namespace Safety**: Do not pollute the global MUSHclient namespace. Every module should return a local table containing its functions and attributes:

   ```lua
   local MyModule = {}

   function MyModule.doSomething()
       -- implementation
   end

   return MyModule
   ```

2. **Standard Loader Integration**: Use standard `require` to load dependencies, or dynamically add this folder to the package path if loading external modules.
3. **No MUSHclient Direct Globals (when possible)**: Keep general utility scripts decoupled from specific MUSHclient global calls so they are easier to unit test outside the client environment.
