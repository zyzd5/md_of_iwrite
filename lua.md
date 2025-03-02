```lua
-- print() start
    print(arg1, arg2, arg3)
    -- auto whitespace 
    -- output: arg1 arg2 arg3
    
    print("line1")
    print("line2")
    -- auto new line

    -- cant direct print map
    local table = {a = 1, b = 2, c = 3}
    for key, value in pairs(table) do
        print(key, value)
    end
-- print() end
```
```lua
    local single = 'single'
    local string = "string"
-- they are same

-- long string start
    local long_string = [[ long string,
    it can be split roll ]]
-- long string end

-- function start
    -- multiple return start
        local four_return = function()
            return 1, 2, 3, 4
        end

        one, two, three, four = four_return()
    -- multiple return end

    -- mutable parameter start
        local function my_print(...)
            for key, value in pairs({ ... }) do
                print(key, value)
            end
        end
    -- mutable parameter end

    -- function calling with one parameter start
        local setup = function (opts)
            if opts.enabled == false then
                opts.enabled = true
            end
        end

        setup {enabled = false, other = "hello"}
        -- same with setup({enabled = false, other = "hello"})
    -- function calling with one parameter end

    -- higher_order start
        local higher_order = function(value)
            return function(another)
                return value + another
            end
        end

        local add_one = higher_order(1)
        -- add_one = function(opt) return (1 + opt) end
        print("add_one(2) -> ", add_one(2))
    -- higher_order end
-- function end

-- table start
    local list = {"first", 2, false, function() return 4 end}
    print("first element: " .. list[1])
    -- index start with 1
-- table end

-- map start
    local map = {a = "first", b = 2, c = true}
    
    print(#map)
    -- output: 0, map do not have length
-- map end
```
```lua
-- control flow: `for` start
    local list = {"first", "second", "third"}
    for index = 1, #list do 
        print(index, list[index])
    end
    -- range-like

    for index, value in pairs(list) do 
        print(index, value)
    end
    -- iterater
-- control flow: `for` end

-- control flow: `if` start
    -- nil and false will not get in if condition 
    if condition then 
        -- pass
    elseif condition then
        -- pass
    end
-- control flow: `if` end
```
```lua
-- module start
    -- foo.lua
    local M = {}
    M.a_function = function() return 9 end
    return M

    -- bar.lua
    local foo = require('foo')
    foo.a_function()
-- module end
```
