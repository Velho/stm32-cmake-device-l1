
if (CMSIS_INCLUDES)
    message ("${CMSIS_INCLUDES}")
endif ()

set (L1_STARTUP_ASM startup/startup_stm32l152retx.s)

set (APP_HEADERS
    main.h
    stm32l1xx_hal_conf.h
    stm32l1xx_it.h)

set (CONTROLLER_SOURCES
    ${APP_HEADERS}
    system_stm32l1xx.c

    controller/main.c
    controller/stm32l1xx_hal_msp.c
    controller/stm32l1xx_it.c
)


# mcpu=cortex-m3
# thumb
# set (COMPILE_OPTIONS "")

add_executable (controller.elf ${L1_STARTUP_ASM} ${CONTROLLER_SOURCES})

target_include_directories (controller.elf INTERFACE l1-cmsis l1-hal)

target_compile_definitions(controller.elf
    PUBLIC
        USE_HAL_DRIVER
        STM32L152xE
)

message ("SOURCE_DIR : ${CMAKE_SOURCE_DIR}")

target_compile_options(controller.elf
#    PRIVATE
#        "-T ${CMAKE_SOURCE_DIR}/ldscripts/linker.d"
    PUBLIC
        -mcpu=cortex-m3
        -mthumb)

target_link_libraries (controller.elf
    PUBLIC
        l1-cmsis
        l1-hal
)

