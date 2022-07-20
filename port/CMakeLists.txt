# ioLibrary_Driver
add_library(IOLIBRARY_FILES STATIC)

target_sources(IOLIBRARY_FILES PUBLIC
        ${PORT_DIR}/ioLibrary_Driver/src/w5x00_spi.c
        ${PORT_DIR}/ioLibrary_Driver/src/w5x00_gpio_irq.c
        )

target_include_directories(IOLIBRARY_FILES PUBLIC
        ${WIZNET_DIR}/Ethernet
        ${PORT_DIR}/ioLibrary_Driver/inc
        ${PORT_DIR}
        #${PICO_LWIP_PATH}/src/include/lwip
        #${PROJECT_SOURCE_DIR}/src/rp2_commom/pico_lwip/include
        )

target_link_libraries(IOLIBRARY_FILES PRIVATE
        pico_stdlib
        hardware_spi
        hardware_dma
        hardware_clocks
        #pico_lwip_core
        )

# lwip
message(STATUS "PICO_LWIP_PATH = ${PICO_LWIP_PATH}")
add_library(LWIP_FILES STATIC)

target_sources(LWIP_FILES PUBLIC
        ${PORT_DIR}/lwip/w5x00_lwip.c
        )

target_include_directories(LWIP_FILES PUBLIC
        ${WIZNET_DIR}/Ethernet
        ${PORT_DIR}
        ${PORT_DIR}/lwip
        #${PICO_LWIP_PATH}/src/include/lwip
        )

target_link_libraries(LWIP_FILES PRIVATE
        ETHERNET_FILES
        pico_lwip
        #pico_lwip_core4
        #pico_lwip_core
        #pico_lwip_arch
        #pico_base_headers
        #hardware_structs
        #lwip
        #pico_lwip
        #pico_lwip_core
        pico_lwip_nosys
        pico_time
        hardware_irq
        )

# timer
add_library(TIMER_FILES STATIC)

target_sources(TIMER_FILES PUBLIC
        ${PORT_DIR}/timer/timer.c
        )

target_include_directories(TIMER_FILES PUBLIC
        ${PORT_DIR}/timer
        )

target_link_libraries(TIMER_FILES PRIVATE
        pico_stdlib      
        )
