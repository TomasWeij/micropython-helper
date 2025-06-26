# Set location of base MicroPython directory.
get_filename_component(MICROPY_DIR ${CMAKE_CURRENT_LIST_DIR}/micropython ABSOLUTE)

# Set location of the ESP32 port directory.
get_filename_component(MICROPY_PORT_DIR ${MICROPY_DIR}/ports/esp32 ABSOLUTE)

if(IDF_TARGET STREQUAL "esp32c6")
    list(APPEND MICROPY_SOURCE_LIB ${MICROPY_DIR}/shared/runtime/gchelper_generic.c)

    # Select board and set include path for ESP32_GENERIC_C6
    set(BOARD ESP32_GENERIC_C6)
    set_property(TARGET ${COMPONENT_LIB} APPEND PROPERTY
        INCLUDE_DIRECTORIES ${MICROPY_DIR}/ports/esp32/boards/${BOARD}
    )
endif()

include(${CMAKE_CURRENT_LIST_DIR}/esp32_common.cmake)
