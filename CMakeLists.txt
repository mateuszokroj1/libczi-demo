project(Root)

	execute_process(
		WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
		COMMAND git clone https://github.com/Microsoft/vcpkg.git
	)

	set(VCPKG_DIR "${CMAKE_CURRENT_BINARY_DIR}/vcpkg")

	if(DEFINED WIN32)
		set(VCPKG_BOOTSTRAP_SCRIPT bootstrap-vcpkg.bat)
	else()
		set(VCPKG_BOOTSTRAP_SCRIPT bootstrap-vcpkg.sh)
	endif()

	execute_process(
		WORKING_DIRECTORY "${VCPKG_DIR}"
		COMMAND ${VCPKG_BOOTSTRAP_SCRIPT}
	)

	find_program(Vcpkg NAMES vcpkg HINTS ${VCPKG_DIR})

	execute_process(COMMAND ${Vcpkg} update)

	execute_process(COMMAND ${Vcpkg} install opencv)

	include("${VCPKG_DIR}/scripts/buildsystems/vcpkg.cmake")

	add_subdirectory(3rd)
	add_subdirectory(app)