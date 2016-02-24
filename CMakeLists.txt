cmake_minimum_required (VERSION 3.3.1)

project(develab)

  add_library(IVS_sqlite INTERFACE IMPORTED GLOBAL)

  set(root_dir /opt/ivs/third_party/sqlite-macos-3.8.11.1/ )
  set_property(TARGET IVS_sqlite PROPERTY INTERFACE_SYSTEM_INCLUDE_DIRECTORIES ${root_dir}/include )
  set_property(TARGET IVS_sqlite PROPERTY INTERFACE_LINK_LIBRARIES ${root_dir}/lib/sdsqlite$<$<CONFIG:Debug>:d>.lib ${root_dir}/lib/sqlite$<$<CONFIG:Debug>:d>.lib )
  

add_library(dd STATIC main.cpp)

target_link_libraries(dd IVS_sqlite)