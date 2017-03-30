# Ace2

The Ace3 vanilla version is under development so there will probably be no more updates for the old Ace2 version

## Some Notes:

### Variable Arguments
In vanilla the variable arguments generate extra table so in Ace2 we see many function like

```lua
function foo(...<fixed args>..., a1, a2, a3, ..., a20)
```

to avoid extra table creating cost, but the PC today are much more powerful so I dont think it will be a big issue, sometimes we can reuse the table by rewriting the recursive functions:

```lua
function _foo(param, arg)
    ...
    _foo(param, arg)
    ...

function foo(param, ...)
    ...
    _foo(param, unpack(arg))  -- arg is the variable argument table
    ...
```

### Recursive functions with loop

The iterator must be declared again as local if it will be passed as an argument in the recursive function

```lua
function recur(.....)
    for k, v in ....
        local v = v
        ...
        recur(..., v, ...)
```

This may caused by the scope/visibility problem of old version lua in vanilla

check the modification of function "copyTable" of [AceDB-3.0](https://github.com/zerosnake0/Ace3v/blob/master/AceDB-3.0/AceDB-3.0.lua) in Ace3 in [this commit](https://github.com/zerosnake0/Ace3v/commit/b1a6764affe0812ee5eda660a0cf741a3676d2cd#diff-ed392234c902ccbb69fea450f74c4ab9) and the function "inheritDefaults" of [AceDB-2.0](https://github.com/zerosnake0/Ace2/blob/master/AceDB-2.0/AceDB-2.0.lua) to see the detail

### List of Ace2/Ace3 Components

Ace2|Ace3
---|---
AceAddon-2.0,AceModuleCore-2.0|AceAddon-3.0
AceComm-2.0|AceComm-3.0
AceConsole-2.0|AceConsole-3.0
AceDB-2.0|AceDB-3.0,AceDBOptions-3.0
AceDebug-2.0|-
AceEvent-2.0|AceEvent-3.0,AceBucket-3.0,AceTimer-3.0
AceHook-2.0,2.1|AceHook-3.0
AceLibrary|LibStub
AceLocale-2.0,2.1,2.2|AceLocale-3.0,3.1
AceOO-2.0|-
AceTab-2.0|AceTab-3.0
Dewdrop-2.0, Waterfall-1.0|AceConfig-3.0
Waterfall-1.0 (partialy)|AceGUI-3.0
-|AceSerializer-3.0
-|CallbackHandler-1.0
