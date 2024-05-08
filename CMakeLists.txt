if (NOT TARGET config)
    add_library(default_config INTERFACE)
    target_include_directories(default_config INTERFACE Config)
    message(WARNING "No target `config` provided, using default configuration")
endif ()

add_library(cmsis-core INTERFACE)
target_include_directories(cmsis-core INTERFACE CMSIS/Core/Include)

add_library(cmsis-air001 STATIC)
target_include_directories(cmsis-air001 PUBLIC CMSIS/Device/AIR001xx/Include)
target_sources(cmsis-air001 PRIVATE CMSIS/Device/AIR001xx/Source/system_air001xx.c)
target_sources(cmsis-air001 PRIVATE CMSIS/Device/AIR001xx/Source/gcc/startup_air001xx.s)
set_property(SOURCE cmsis-air001/Device/AIR001xx/Source/gcc/startup_air001xx.s PROPERTY LANGUAGE ASM)
target_link_libraries(cmsis-air001 PUBLIC cmsis-core)

option(USE_CMSIS_DSP "Use CMSIS DSP library" OFF)
if (USE_CMSIS_DSP)
    add_library(cmsis-dsp STATIC)
    target_include_directories(cmsis-dsp PUBLIC CMSIS-DSP/Include)
    file(GLOB_RECURSE CMSIS_DSP_SOURCES CMSIS-DSP/Source/*.c)
    target_sources(cmsis-dsp PRIVATE ${CMSIS_DSP_SOURCES})
    target_link_libraries(cmsis-dsp PUBLIC cmsis-air001)
    add_compile_definitions(USE_CMSIS_DSP)
endif ()

add_library(hal STATIC)
target_include_directories(hal PUBLIC AIR001xx_HAL_Driver/Inc)
file(GLOB_RECURSE HAL_SOURCES AIR001xx_HAL_Driver/Src/*.c)
target_sources(hal PRIVATE ${HAL_SOURCES})
if (NOT TARGET config)
    target_link_libraries(hal PUBLIC default_config)
    message(WARNING "No target `config` provided. link the hal library with default configuration")
else ()
    message(STATUS "linking hal library with target `config`")
    target_link_libraries(hal PUBLIC config)
endif ()
target_link_libraries(hal PUBLIC cmsis-air001)

add_compile_definitions(
        AIR001_DEV
        ARM_MATH_CM0PLUS
)
