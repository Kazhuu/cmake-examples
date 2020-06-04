message("")
message(STATUS "Variables Example")

# All variables are treated as strings.
set(simpleVar some-text) # simpleVar = "some-text"

# Multiple values are joined to semicolon separated list.
set(simpleList a b c d) # simpleList = "a;b;c;d"
set(simpleList a;b;c;d) # simpleList = "a;b;c;d"

# Variable can contain spaces when quoted.
set(string "a b c d") # string = "a b c d"

# Variables can be accessed with ${}.
set(anotherString ${string}) # anotherString = "a b c d"

# Accessing uninitialized variable is an empty string.
message("Empty variable: ${emptyVariable}")

# Variables can also appear inside string.
set(anotherString "${string} e f") # anotherString = "a b c d e f"
# And inside each other.
set(aa aa)
set(aastring abcd)
set(anotherString ${${aa}string}) # anotherString = "abcd"

# Multi line strings.
set(string "this is
multiline \"string\" with no variable \${string} access.")
message(${string})

# Bracket syntax can also be used to have multi-line string without need to
# escape quotes or variable access. Useful for example when writing inline bash
# scripts. Also supports [=[ ... ]=] syntax.
set(string [[
Some other multiline
strings here with bracket syntax
and no need to escape "quotes" and variables ${string}.
]])
message(${string})

# Unset variable. Both are equivalent.
unset(string)
set(string "")
