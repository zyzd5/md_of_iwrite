```lua
local single = 'single'
local string = "string"
-- they are same

-- long string start
local long_string = [[ long string,
it can be split roll ]]
-- long string end

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
```
