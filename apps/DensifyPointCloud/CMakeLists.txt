if(MSVC)
	FILE(GLOB LIBRARY_FILES_C "*.cpp" "*.rc")
else()
	FILE(GLOB LIBRARY_FILES_C "*.cpp")
endif()

FILE(GLOB LIBRARY_FILES_H "*.h" "*.inl")

cxx_executable_with_flags(DensifyPointCloud "Apps" "${cxx_default}" "MVS;${OpenMVS_EXTRA_LIBS}" ${LIBRARY_FILES_C} ${LIBRARY_FILES_H})

add_library(MySharedLib SHARED /home/sun/MVS/openMVS/libs/IO/read_pose.cpp /home/sun/MVS/openMVS/libs/IO/read_pose.h)
target_link_libraries(DensifyPointCloud MySharedLib)

# Install
INSTALL(TARGETS DensifyPointCloud
	EXPORT OpenMVSTargets
	RUNTIME DESTINATION "${INSTALL_BIN_DIR}" COMPONENT bin)
