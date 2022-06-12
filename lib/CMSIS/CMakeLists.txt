set (CMSIS_INCLUDES
    Include/core_cm3.h
    Device/ST/STM32L1xx/Include/stm32l1xx.h
    Device/ST/STM32L1xx/Include/system_stm32l1xx.h
)

# sourceAsm, startup_stm32l152xe.s is included in the application folder.

add_library (l1-cmsis INTERFACE ${CMSIS_INCLUDES})

target_include_directories (l1-cmsis
    INTERFACE
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/Include>
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/Device/ST/STM32L1xx/Include/>)
