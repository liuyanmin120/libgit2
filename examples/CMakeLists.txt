file(GLOB SRC_EXAMPLES *.c *.h)

add_executable(lg2 ${SRC_EXAMPLES})
set_target_properties(lg2 PROPERTIES C_STANDARD 90)

# Ensure that we do not use deprecated functions internally
add_definitions(-DGIT_DEPRECATE_HARD)

target_include_directories(lg2 PRIVATE ${LIBGIT2_INCLUDES} ${LIBGIT2_DEPENDENCY_INCLUDES})
target_include_directories(lg2 SYSTEM PRIVATE ${LIBGIT2_SYSTEM_INCLUDES})

if(WIN32 OR ANDROID)
	target_link_libraries(lg2 git2)
else()
	target_link_libraries(lg2 git2 pthread)
endif()
