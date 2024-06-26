cmake_minimum_required(VERSION 3.12)
project(embedded_python VERSION 0.1.0 LANGUAGES CXX)

if (WIN32)
	# TODO
	find_package(Imath)
	find_package(pybind11 REQUIRED)
elseif(APPLE)
	# TODO
else()
	find_package(pybind11 REQUIRED)  # or `add_subdirectory(pybind11)`
	find_package(spdlog REQUIRED)
	find_package(fmt REQUIRED)
	find_package(Imath)
	find_package(OpenTime REQUIRED)
	find_package(OpenTimelineIO REQUIRED)
endif()



set(SOURCES
	embedded_python.cpp
	embedded_python_actor.cpp
)

add_library(${PROJECT_NAME} SHARED ${SOURCES})
add_library(xstudio::embedded_python ALIAS ${PROJECT_NAME})
default_options(${PROJECT_NAME})
target_compile_options(${PROJECT_NAME}
	PRIVATE -fvisibility=hidden
)
target_link_libraries(${PROJECT_NAME}
	PUBLIC
		caf::core
	PRIVATE
		Imath::Imath
		xstudio::utility
		xstudio::broadcast
		pybind11::embed
		#OTIO::opentime
		#OTIO::opentimelineio
)

set_target_properties(${PROJECT_NAME} PROPERTIES LINK_DEPENDS_NO_SHARED true)
