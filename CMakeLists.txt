cmake_minimum_required (VERSION 3.8)
project (stm32-device C CXX ASM)


# toolchain defines.
include (cmake/toolchain-arm.cmake)

# set (LINKER_SCRIPT "linker.ld")
# set (CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -T ${LINKER_SCRIPT}")

# STM32L152xE
# STM32L152xE
# For now as debug. ja : remove this or select as build_type
add_definitions (-DDEBUG)
add_definitions (-DUSE_HAL_DRIVER)
add_definitions (-DSTM32L152xE)


include_directories (lib/CMSIS/Device/ST/STM32L1xx/Include)
include_directories (src)

# include libs.
add_subdirectory (lib/CMSIS)
add_subdirectory (lib/STM32L1xx_HAL_Driver)
add_subdirectory (lib/UCOS3)


add_subdirectory (src)

# JA : Add POST_BUILD command to run the objcopy.
# arm-none-eabi-objcopy.exe -Oihex .\src\controller.elf controller.hex