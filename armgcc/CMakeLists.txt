# CROSS COMPILER SETTING
SET(CMAKE_SYSTEM_NAME Generic)
CMAKE_MINIMUM_REQUIRED (VERSION 3.10.0)

# THE VERSION NUMBER
SET (Tutorial_VERSION_MAJOR 1)
SET (Tutorial_VERSION_MINOR 0)

if (DEFINED ENV{SdkRootDirPath})
	SET(SdkRootDirPath "$ENV{SdkRootDirPath}")
endif()

if (NOT DEFINED SdkRootDirPath)
	MESSAGE(FATAL_ERROR "SDK path could not be determined. Please update SdkRootDirPath value from your CMake presets file(s).")
endif()

# ENABLE ASM
ENABLE_LANGUAGE(ASM)

# RESET FLAG VALUES
SET(CMAKE_ASM_FLAGS_DEBUG "")
SET(CMAKE_ASM_FLAGS_RELEASE "")
SET(CMAKE_C_FLAGS_DEBUG "")
SET(CMAKE_C_FLAGS_RELEASE "")
SET(CMAKE_CXX_FLAGS_DEBUG "")
SET(CMAKE_CXX_FLAGS_RELEASE "")
SET(CMAKE_EXE_LINKER_FLAGS_DEBUG "")
SET(CMAKE_EXE_LINKER_FLAGS_RELEASE "")

SET(CMAKE_STATIC_LIBRARY_PREFIX)
SET(CMAKE_STATIC_LIBRARY_SUFFIX)

SET(CMAKE_EXECUTABLE_LIBRARY_PREFIX)
SET(CMAKE_EXECUTABLE_LIBRARY_SUFFIX)

# CURRENT DIRECTORY
SET(ProjDirPath ${CMAKE_CURRENT_SOURCE_DIR})

SET(EXECUTABLE_OUTPUT_PATH ${ProjDirPath}/${CMAKE_BUILD_TYPE})
SET(LIBRARY_OUTPUT_PATH ${ProjDirPath}/${CMAKE_BUILD_TYPE})

set(CMAKE_USER_MAKE_RULES_OVERRIDE "user_override.cmake")

project(evkmimxrt1064_lpuart_interrupt)
set(MCUX_SDK_PROJECT_NAME evkmimxrt1064_lpuart_interrupt.elf)

include(${ProjDirPath}/flags.cmake)

set(sources "${ProjDirPath}/../component/lists/fsl_component_generic_list.h"
"${ProjDirPath}/../component/lists/fsl_component_generic_list.c"
"${ProjDirPath}/../component/uart/fsl_adapter_uart.h"
"${ProjDirPath}/../component/uart/fsl_adapter_lpuart.c"
"${ProjDirPath}/../startup/startup_mimxrt1064.c"
"${ProjDirPath}/../CMSIS/mpu_armv7.h"
"${ProjDirPath}/../CMSIS/core_cm7.h"
"${ProjDirPath}/../CMSIS/cmsis_version.h"
"${ProjDirPath}/../CMSIS/cmsis_iccarm.h"
"${ProjDirPath}/../CMSIS/cmsis_gcc.h"
"${ProjDirPath}/../CMSIS/cmsis_compiler.h"
"${ProjDirPath}/../CMSIS/cmsis_armclang_ltm.h"
"${ProjDirPath}/../CMSIS/cmsis_armclang.h"
"${ProjDirPath}/../CMSIS/cmsis_armcc.h"
"${ProjDirPath}/../source/semihost_hardfault.c"
"${ProjDirPath}/../source/lpuart_interrupt.c"
"${ProjDirPath}/../utilities/fsl_debug_console.h"
"${ProjDirPath}/../utilities/fsl_debug_console.c"
"${ProjDirPath}/../utilities/fsl_assert.c"
"${ProjDirPath}/../drivers/fsl_lpuart.h"
"${ProjDirPath}/../drivers/fsl_lpuart.c"
"${ProjDirPath}/../drivers/fsl_iomuxc.h"
"${ProjDirPath}/../drivers/fsl_gpio.h"
"${ProjDirPath}/../drivers/fsl_gpio.c"
"${ProjDirPath}/../drivers/fsl_common_arm.h"
"${ProjDirPath}/../drivers/fsl_common_arm.c"
"${ProjDirPath}/../drivers/fsl_common.h"
"${ProjDirPath}/../drivers/fsl_common.c"
"${ProjDirPath}/../drivers/fsl_clock.h"
"${ProjDirPath}/../drivers/fsl_clock.c"
"${ProjDirPath}/../device/system_MIMXRT1064.h"
"${ProjDirPath}/../device/system_MIMXRT1064.c"
"${ProjDirPath}/../device/MIMXRT1064_features.h"
"${ProjDirPath}/../device/MIMXRT1064.h"
"${ProjDirPath}/../device/fsl_device_registers.h"
"${ProjDirPath}/../board/pin_mux.h"
"${ProjDirPath}/../board/pin_mux.c"
"${ProjDirPath}/../board/dcd.h"
"${ProjDirPath}/../board/dcd.c"
"${ProjDirPath}/../board/clock_config.h"
"${ProjDirPath}/../board/clock_config.c"
"${ProjDirPath}/../board/board.h"
"${ProjDirPath}/../board/board.c"
"${ProjDirPath}/../xip/fsl_flexspi_nor_boot.h"
"${ProjDirPath}/../xip/fsl_flexspi_nor_boot.c"
"${ProjDirPath}/../xip/evkmimxrt1064_flexspi_nor_config.h"
"${ProjDirPath}/../xip/evkmimxrt1064_flexspi_nor_config.c"
)


add_executable(${MCUX_SDK_PROJECT_NAME} ${sources})



if(${LIBRARY_TYPE} STREQUAL "REDLIB")
    target_include_directories(${MCUX_SDK_PROJECT_NAME} PRIVATE $ENV{ARMGCC_DIR}/redlib/include)
endif()

set(include_directories "${ProjDirPath}/../board"
"${ProjDirPath}/../source"
"${ProjDirPath}/../utilities"
"${ProjDirPath}/../drivers"
"${ProjDirPath}/../device"
"${ProjDirPath}/../component/uart"
"${ProjDirPath}/../component/lists"
"${ProjDirPath}/../xip"
"${ProjDirPath}/../CMSIS"
"${ProjDirPath}/../evkmimxrt1064/driver_examples/lpuart/interrupt"
)


target_include_directories(${MCUX_SDK_PROJECT_NAME} PRIVATE ${include_directories})

set(include_files "")


target_precompile_headers(${MCUX_SDK_PROJECT_NAME} PRIVATE ${include_files})

set(link_directories "")


set(link_libraries "")


target_link_directories(${MCUX_SDK_PROJECT_NAME} PRIVATE ${link_directories})
target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE -Wl,--start-group)
target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE ${TARGET_LINK_SYSTEM_LIBRARIES} ${link_libraries})
target_link_libraries(${MCUX_SDK_PROJECT_NAME} PRIVATE -Wl,--end-group)





