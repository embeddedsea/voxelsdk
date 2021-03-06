add_library(calculuscdk SHARED
  CalculusCDKCamera.cpp
  CalculusCDKCameraFactory.cpp
  ${COMMON_LIB_FILES}
)

set_voxel_library_output_directory(calculuscdk)

generate_export_header(calculuscdk
  EXPORT_FILE_NAME "SymbolExports.h"
  EXPORT_MACRO_NAME SYMBOL_EXPORT
)

target_link_libraries(calculuscdk 
  ti3dtof voxel ${COMMON_LIBS}
)

install(TARGETS calculuscdk
  LIBRARY DESTINATION lib/voxel COMPONENT ti3dtof
  ARCHIVE DESTINATION lib/voxel COMPONENT ti3dtof
  RUNTIME DESTINATION lib/voxel COMPONENT ti3dtof
)

list(APPEND CONF_FILES
  boards/CalculusCDK/CalculusCDKCamera.conf
  boards/CalculusCDK/CalculusCDKCameraLensOnly.conf
  boards/CalculusCDK/CalculusCDKCameraNormal.conf
)

set(CONF_FILES "${CONF_FILES}" PARENT_SCOPE)

list(APPEND UDEV_FILES
  boards/CalculusCDK/72-CalculusCDK.rules
)

set(UDEV_FILES "${UDEV_FILES}" PARENT_SCOPE)

set_target_properties(calculuscdk PROPERTIES 
                      VERSION ${VOXEL_VERSION} 
                      SOVERSION ${VOXEL_ABI_VERSION})

