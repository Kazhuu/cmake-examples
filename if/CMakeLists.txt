# CMake has normal programming language like if, else, elseif branching
# commands. CMake values that evaluate to true: 1, ON, YES, TRUE, Y and
# non-zero number.  Test case is case-insensitive.  Values to evaluate to
# false: 0, OFF, NO, N, IGNORE, NOTFOUND, "" and string
# ending -NOTFOUND. Again case-insensitive.

message("")
message(STATUS "If Example")

# Normal and preferred way to use if commands.
set(variable TRUE)
if(variable) # can also be if(${true})
    message("true")
endif()

# Quoted string after CMake version 3.1 always evaluates to false! Doesn't
# happen in some other programming languages!  For this reason prefer to use
# unquoted values in if statements. In version before 3.1 if string name exists
# as a variable, then that string is replaced with the value of the variable.
# Will print:
# "aaa" evaluate to false
set(aaa TRUE)
if("aaa") # This would evaluate to true before version 3.1 because aaa exits as a variable.
    message("\"aaa\" evaluate to true")
else()
    message("\"aaa\" evaluate to false")
endif()

# CMake supports boolean logical operators like NOT, AND, and OR.
# Will print:
# boolean logical operators
if(NOT (TRUE AND FALSE))
    message("boolean logical operators")
endif()

# CMake provides different comparison operators to compare numbers, strings and
# versions. Check page https://cmake.org/cmake/help/latest/command/if.html for
# all operators.
# Will print:
# less
if (1 LESS 2)
    message("less")
elseif(2 GREATER 3)
    message("greater")
elseif(4 LESS_EQUAL 3)
    message("less or equal")
endif()
