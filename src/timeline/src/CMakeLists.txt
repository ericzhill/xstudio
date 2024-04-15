find_package(Imath)
if (WIN32)
	# TODO
elseif(APPLE)
	# TODO
else()
	find_package(OpenTime REQUIRED)
	find_package(OpenTimelineIO REQUIRED)
	find_package(Imath)
endif()


SET(LINK_DEPS
	xstudio::playhead
	xstudio::utility
	caf::core
	#OTIO::opentime
	#OTIO::opentimelineio
	Imath::Imath
)

SET(STATIC_LINK_DEPS
	xstudio::utility_static
	caf::core
	Imath::Imath
	#OTIO::opentime
	#OTIO::opentimelineio
)


create_component_static(timeline 0.1.0 "${LINK_DEPS}" "${STATIC_LINK_DEPS}")

