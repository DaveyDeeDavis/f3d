cmake_minimum_required(VERSION 3.21)

project(f3d-plugin-exodus)

include(GNUInstallDirs)

# Check if the plugin is built externally
if(PROJECT_IS_TOP_LEVEL)
  find_package(f3d REQUIRED)
else()
  include(f3dPlugin)
endif()

f3d_plugin_init()

f3d_plugin_declare_reader(
  NAME ExodusII
  EXTENSIONS exo ex2 e
  MIMETYPES application/vnd.exodus
  VTK_READER vtkExodusIIReader
  FORMAT_DESCRIPTION "Exodus II"
  CUSTOM_CODE "${CMAKE_CURRENT_SOURCE_DIR}/exodus.inl"
)

f3d_plugin_build(
  NAME exodus
  VERSION 1.0
  DESCRIPTION "VTK Exodus support"
  VTK_MODULES IOExodus
  MIMETYPE_XML_FILES "${CMAKE_CURRENT_SOURCE_DIR}/f3d-exodus-formats.xml"
  CONFIGURATION_DIRS "${CMAKE_CURRENT_SOURCE_DIR}/configs/config.d" "${CMAKE_CURRENT_SOURCE_DIR}/configs/thumbnail.d"
  FREEDESKTOP
)
