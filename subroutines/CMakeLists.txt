message("")
message(STATUS "Function and macro examples")

# Function always defines a new scope. Variables from this doesn't affect the
# parent scope. And arguments are treated like variables. So in this case if
# statement will evaluate to true.
function(testFunction arg1)
    if (DEFINED arg1)
        message("testFunction arg1 defined")
    else()
        message("testFunction arg1 not defined")
    endif()
endfunction()

testFunction(aaa)

# Macros in CMake works like C preprocessor macros. They are basically copy
# pasted to the calling site. Hence the arguments are treated like string
# replacements rather than variables. So in this case if statement evaluates to
# false instead.
macro(testMacro arg1)
    if (DEFINED arg1)
        message("testMacro arg1 defined")
    else()
        message("testMacro arg1 not defined")
    endif()
endmacro()

testMacro(bbb)

# In CMake function and macros can take more arguments than they specify.
# Arguments that has name in function definition are called named arguments and
# left-over arguments are called unnamed arguments. CMake automatically
# provides some variables for the function when called which can be used to
# access given unnamed arguments.
# ARGC: Total number or arguments given.
# ARGV: List of all argument values given by the caller.
# ARGN: List of all unnamed arguments given.

# Following will print:
# ARGC: 4
# ARGV: aaa;bbb;ccc;ddd
# ARGN: ccc;ddd
function(automaticVariables arg1 arg2)
    message("ARGC: ${ARGC}")
    message("ARGV: ${ARGV}")
    message("ARGN: ${ARGN}")
endfunction()

automaticVariables(aaa bbb ccc ddd)

# CMake supports defining functions with keyword arguments and are the main way
# how existing CMake functions are also used. Support for keyword arguments is
# added with cmake_parse_arguments() function and giving it the supported
# keyword arguments. When variables are parsed. Matching variable is set in the
# caller scope with name of the prefix and name of the keyword argument. This
# way the caller can specify the names of the variables to be used.
function(keywordFunction)
    # Define the supported set of keywords. Each keyword has it's purpose to
    # support no values, single values and multi values.
    set(prefix ARG)
    set(noValues ENABLE_NET COOL_STUFF)
    set(singleValues TARGET)
    set(multiValues SOURCES IMAGES)
    # Process the arguments passed in.
    cmake_parse_arguments(${prefix} "${noValues}" "${singleValues}" "${multiValues}" ${ARGN})
    # Log details for each supported keyword.
    message("Option summary:")
    foreach(arg IN LISTS noValues)
        if(${${prefix}_${arg}})
            message(" ${arg} enabled")
        else()
            message(" ${arg} disabled")
        endif()
    endforeach()
    foreach(arg IN LISTS singleValues multiValues)
        # Single argument values will print as a simple string
        # Multiple argument values will print as a list.
        message(" ${arg} = ${${prefix}_${arg}}")
    endforeach()
endfunction()

# Examples of calling with different combinations of keyword arguments.
keywordFunction(SOURCES foo.cpp bar.cpp TARGET myApp ENABLE_NET)
# Option summary:
#  ENABLE_NET enabled
#  COOL_STUFF disabled
#  TARGET = myApp
#  SOURCES = foo.cpp;bar.cpp
#  IMAGES =
keywordFunction(COOL_STUFF TARGET dummy IMAGES here.png there.png gone.png)
# Option summary:
#  ENABLE_NET disabled
#  COOL_STUFF enabled
#  TARGET = dummy
#  SOURCES =
#  IMAGES = here.png;there.png;gone.png
