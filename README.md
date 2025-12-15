
# 🐍 Learn Lua in Y Minutes

A fast-paced, practical Lua guide, inspired by Learn X in Y Minutes.

Covers variables, functions, tables, metatables, class-like patterns, and modules.

---

## ⚙️ Setup & Installation

Before running Lua scripts, you need Lua installed:

### Install Lua

Windows: Use Lua for Windows.

macOS: brew install lua (via Homebrew).

Linux: Use your package manager, e.g., sudo apt install lua5.4.

Run scripts
```bash
lua your_script.lua
````

### Optional tools

luac for compiling scripts.

LuaRocks for package management.

---

## 📌 What to Expect

This guide is split into four main sections:

Variables and flow control – Basics of numbers, strings, loops, and conditionals.

Functions – Defining functions, closures, multiple returns, and scope.

Tables – Lua's primary data structure, metatables, and class-like tables.

Modules – How to structure code across multiple files.

---

----------------------------------------------------
### 1. Variables and Flow Control
----------------------------------------------------
```bash
num = 42        -- Numbers (int or float)
s = 'walternate' -- Strings (immutable)
t = "double-quotes" 
u = [[ Multi-line
       strings ]]
t = nil         -- Undefine t

Loops
while num < 50 do
  num = num + 1  -- No ++ or +=
end

for i = 1, 100 do
  num = num + i
end

for j = 100, 1, -1 do
  num = num - j
end

repeat
  print('the way of the future')
  num = num - 1
until num == 0

Conditionals
if num > 40 then
  print('over 40')
elseif s ~= 'walternate' then
  io.write('not over 40\n')
else
  local line = io.read()
  print('Winter is coming, ' .. line)
end

-- Only nil and false are falsy
aBoolValue = false
if not aBoolValue then print('it was false') end

-- Short-circuiting
ans = aBoolValue and 'yes' or 'no'
```

---

----------------------------------------------------
### 2. Functions
----------------------------------------------------
```bash
function fib(n)
  if n < 2 then return 1 end
  return fib(n - 2) + fib(n - 1)
end

-- Closures
function adder(x)
  return function(y) return x + y end
end

a1 = adder(9)
print(a1(16))  --> 25

-- Multiple returns
function bar(a, b, c)
  return 4, 8, 15
end
x, y = bar('zaphod')  --> x=4, y=8
```

### Tips:

local function creates a local function.

function obj:fn(...) automatically passes self.

Single string argument doesn't need parentheses: print 'hello'.


---

----------------------------------------------------
 ## 3. Tables
 ----------------------------------------------------

Lua's only compound data structure: associative arrays.
```baah
Dictionary / Map
t = {key1 = 'value1', key2 = false}
print(t.key1)
t.key2 = nil

u = {['@!#']='qbert', [{}]=1729, [6.28]='tau'}
print(u[6.28])  --> "tau"

List / Array
v = {'value1','value2',1.21}
for i=1,#v do
  print(v[i])
end

Metatables & Metamethods
metafraction = {}
function metafraction.__add(f1,f2)
  return {a=f1.a*f2.b+f2.a*f1.b, b=f1.b*f2.b}
end
setmetatable(f1, metafraction)
s = f1 + f2
````

Common metamethods: __add, __sub, __mul, __index, __call, etc.

---

----------------------------------------------------
### 3.2 Class-like Tables & Inheritance
----------------------------------------------------
```bash
Dog = {}

function Dog:new()
  local newObj = {sound='woof'}
  self.__index = self
  return setmetatable(newObj, self)
end

function Dog:makeSound()
  print('I say ' .. self.sound)
end

mrDog = Dog:new()
mrDog:makeSound()  --> 'I say woof'
```

### Inheritance Example:
```bash
LoudDog = Dog:new()
function LoudDog:makeSound()
  print(self.sound .. ' ' .. self.sound .. ' ' .. self.sound)
end

seymour = LoudDog:new()
seymour:makeSound()  --> 'woof woof woof'
```

Lua uses tables + metatables to mimic classes and inheritance.

: syntax passes self automatically.

---

----------------------------------------------------
### 4. Modules
----------------------------------------------------
```bash
-- mod.lua
local M = {}
local function sayMyName() print('Hrunkner') end
function M.sayHello()
  print('Why hello there')
  sayMyName()
end
return M

-- main.lua
local mod = require('mod')
mod.sayHello()
```

### Notes:

require caches modules (runs only once).

dofile runs files every time.

loadfile/load allow creating functions from files or strings.

---

## ✅ Summary

Lua is lightweight, fast, and flexible.

Variables are global by default unless marked local.

Tables are everywhere: lists, maps, classes.

Metatables provide powerful operator overloading & inheritance.

Modules help organize code.

---

## 📄 License
  
This project is open-source under the MIT License.
Feel free to fork, modify, and learn from it.
