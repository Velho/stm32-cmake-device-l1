
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

# Controller linkage setup.

add_executable (controller.elf ${L1_STARTUP_ASM} ${CONTROLLER_SOURCES})

target_include_directories (controller.elf INTERFACE l1-cmsis l1-hal)

target_compile_definitions(controller.elf
    PUBLIC
        USE_HAL_DRIVER
        STM32L152xE
)

target_compile_options(controller.elf
    PUBLIC
        -mcpu=cortex-m3
        -mthumb)

target_link_libraries (controller.elf
    PUBLIC
        l1-cmsis
        l1-hal
)

target_link_libraries (controller.elf
    PRIVATE
        uc-cfg
        uc-lib
        uc-cpu
        uc-os3
)

# OBJCOPY should be part of the arm toolchain.
add_custom_command (
    TARGET controller.elf
    POST_BUILD
    COMMAND ${CMAKE_OBJCOPY} -O ihex $<TARGET_FILE:controller.elf> ${CMAKE_BINARY_DIR}/controller.bin
    WORKING_DIRECTORY ${CMAKE_BINARY_DIR}
)

