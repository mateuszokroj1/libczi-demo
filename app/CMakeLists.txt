project(MainApp)

	set(src
		"src/main.cpp"
	)

	add_executable(libczi-demo)

	target_link_libraries(libczi-demo PRIVATE opencv_core)

	target_sources(libczi-demo PRIVATE ${src})