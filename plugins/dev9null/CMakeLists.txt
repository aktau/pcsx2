# Check that people use the good file
if(NOT TOP_CMAKE_WAS_SOURCED)
    message(FATAL_ERROR "
    You did not 'cmake' the good CMakeLists.txt file. Use the one in the top dir.
    It is advice to delete all wrongly generated cmake stuff => CMakeFiles & CMakeCache.txt")
endif(NOT TOP_CMAKE_WAS_SOURCED)


# plugin name
set(Output dev9null-0.5.0)

set(CommonFlags
    -fvisibility=hidden
    -Wall
    )

set(OptimizationFlags
    -O2
    -DNDEBUG
    )

# Debug - Build
if(CMAKE_BUILD_TYPE STREQUAL Debug)
	# add defines
    set(dev9nullFinalFlags
		${CommonFlags} -g
    )
endif(CMAKE_BUILD_TYPE STREQUAL Debug)

# Devel - Build
if(CMAKE_BUILD_TYPE STREQUAL Devel)
	# add defines
	set(dev9nullFinalFlags
		${CommonFlags} ${OptimizationFlags}
	)
endif(CMAKE_BUILD_TYPE STREQUAL Devel)

# Release - Build
if(CMAKE_BUILD_TYPE STREQUAL Release)
	# add defines
	set(dev9nullFinalFlags
		${CommonFlags} ${OptimizationFlags}
	)
endif(CMAKE_BUILD_TYPE STREQUAL Release)

# dev9null sources
set(dev9nullSources
	Config.cpp
	DEV9.cpp)

# dev9null headers
set(dev9nullHeaders
	Config.h
	DEV9.h)

# dev9null Linux sources
set(dev9nullLinuxSources
)

# dev9null Linux headers
set(dev9nullLinuxHeaders
)

# dev9null Windows sources
set(dev9nullWindowsSources
	Windows/dev9null.def)

# dev9null Windows headers
set(dev9nullWindowsHeaders
	)

set(dev9nullFinalSources
	${dev9nullSources}
	${dev9nullHeaders}
	${dev9nullLinuxSources}
	${dev9nullLinuxHeaders}
)

set(dev9nullFinalLibs
	${GTK2_LIBRARIES}
)

add_pcsx2_plugin(${Output} "${dev9nullFinalSources}" "${dev9nullFinalLibs}" "${dev9nullFinalFlags}")
