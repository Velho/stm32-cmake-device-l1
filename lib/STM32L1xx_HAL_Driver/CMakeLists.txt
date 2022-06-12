
set (STM32L1xx_HAL_INCLUDES
    Inc/stm32l1xx_hal.h
    Inc/stm32l1xx_hal_rcc.h
    Inc/stm32l1xx_hal_rcc_ex.h
    Inc/stm32l1xx_hal_cortex.h
    Inc/stm32l1xx_hal_exti.h
    Inc/stm32l1xx_hal_tim.h
    Inc/stm32l1xx_hal_tim_ex.h
    Inc/stm32l1xx_hal_uart.h
    Inc/Legacy/stm32_hal_legacy.h # Legacy
    Inc/stm32l1xx_hal_def.h
    # Inc/stm32l1xx_hal_dma_ex.h
    Inc/stm32l1xx_hal_dma.h
    Inc/stm32l1xx_hal_pwr.h
    Inc/stm32l1xx_hal_pwr_ex.h
    Inc/stm32l1xx_hal_flash.h
    Inc/stm32l1xx_hal_flash_ex.h
    Inc/stm32l1xx_hal_flash_ramfunc.h
    Inc/stm32l1xx_hal_gpio.h
    Inc/stm32l1xx_hal_gpio_ex.h)

set (STM32L1xx_HAL_SOURCES
    Src/stm32l1xx_hal.c
    Src/stm32l1xx_hal_rcc.c
    Src/stm32l1xx_hal_rcc_ex.c
    Src/stm32l1xx_hal_cortex.c
    Src/stm32l1xx_hal_exti.c
    Src/stm32l1xx_hal_tim.c
    Src/stm32l1xx_hal_tim_ex.c
    Src/stm32l1xx_hal_uart.c
    Src/stm32l1xx_hal.c
    Src/stm32l1xx_hal_dma.c
    Src/stm32l1xx_hal_pwr.c
    Src/stm32l1xx_hal_pwr_ex.c
    Src/stm32l1xx_hal_flash.c
    Src/stm32l1xx_hal_flash_ex.c
    Src/stm32l1xx_hal_flash_ramfunc.c
    Src/stm32l1xx_hal_gpio.c)

set (HAL_SOURCES ${STM32L1xx_HAL_INCLUDES} ${STM32L1xx_HAL_SOURCES})

add_library (l1-hal ${HAL_SOURCES})

target_include_directories (l1-hal
    PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/Inc>
    PRIVATE
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/../CMSIS/Include>)

target_compile_options(l1-hal
    PUBLIC
        -mcpu=cortex-m3
        -mthumb)

# target_link_directories (l1-hal INTERFACE l1-cmsis)