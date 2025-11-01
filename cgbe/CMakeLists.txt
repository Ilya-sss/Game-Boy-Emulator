set(MAIN_SOURCES
  main.c
)

file(GLOB HEADERS "${PROJECT_SOURCE_DIR}/include/*.h")

# Create the executable and link the library
add_executable(cgbe ${HEADERS} ${MAIN_SOURCES})
target_link_libraries(cgbe PRIVATE emu)

if (NOT WIN32)
  target_link_libraries(cgbe PRIVATE ${SDL2_LIBRARIES} ${SDL2_TTF_LIBRARIES})
endif()

target_include_directories(cgbe PUBLIC ${PROJECT_SOURCE_DIR}/include)
