# CMake has foreach and while loops. Foreach loop support individual items,
# lists and ranger. CMake loops has C equivalent break() and continue()
# commands which behave similarly.
message("")
message(STATUS "Loops Example")

# LoopVar will be set to each item provided in turn. Will print:
# aaa
# item2
message("foreach loop:")
set(item1 "aaa")
foreach(loopVar ${item1} item2)
    message(${loopVar})
endforeach()

# Use LISTS keyword to give list variable, multiple lists can be provided.
# Will print:
# a
# b
# c
# d
message("LISTS keyword loop:")
set(list a b "c;d")
foreach(loopVar IN LISTS list)
    message(${loopVar})
endforeach()

# Use ITEMS keyword to give individual items. Both LISTS and ITEM keyword can
# also be used.
# Will print:
# a
# b
message("ITEMS keyword loop:")
foreach(loopVar IN ITEMS a b)
    message(${loopVar})
endforeach()

# Use RANGE keyword to give range with start, stop and step to iterate over.
# Syntax: RANGE start stop [step]

# If RANGE 5 is provided, then loop will iterate from 0 to 5. Notice that 5 is
# included in the range, not excluded!

# Will print:
# 1
# 3
# 5
message("RANGE keyword loop:")
foreach(loopVar RANGE 1 5 2)
    message(${loopVar})
endforeach()

# CMake also has while loop which is executed until condition evaluates to
# false.
message("while loop:")
set(condition TRUE)
while(condition)
    message("inside while")
    set(condition FALSE)
endwhile()
