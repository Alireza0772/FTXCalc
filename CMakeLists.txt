cmake_minimum_required (VERSION 3.17)
 
# --- Fetch FTXUI --------------------------------------------------------------
include(FetchContent)
 
set(FETCHCONTENT_UPDATES_DISCONNECTED TRUE)
# set(FETCHCONTENT_BASE_DIR "D:/Programming/FTXCalc/opt/")
FetchContent_Declare(ftxui
  GIT_REPOSITORY https://github.com/ArthurSonzogni/ftxui
  # Important: Specify a GIT_TAG XXXXX here.
)
 
FetchContent_GetProperties(ftxui)
if(NOT ftxui_POPULATED)
  FetchContent_Populate(ftxui)
  add_subdirectory(${ftxui_SOURCE_DIR} ${ftxui_BINARY_DIR} EXCLUDE_FROM_ALL)
endif()

# ------------------------------------------------------------------------------
 
project(FTXCalc
  LANGUAGES CXX
  VERSION 0.1.0
)
add_subdirectory(src)
add_executable(FTXCalc main.cpp)
target_sources(FTXCalc PUBLIC ${sources})
target_include_directories(FTXCalc PRIVATE include)
target_link_libraries(FTXCalc
  PRIVATE ftxui::screen
  PRIVATE ftxui::dom
  PRIVATE ftxui::component # Not needed for this example.
)