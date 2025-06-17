from building import *
import os

# Import environment variables
Import('env')

# Get the current working directory
cwd = GetCurrentDir()

# Initialize include paths and source files list
path = [os.path.join(cwd, 'Include')]
src = [os.path.join(cwd, 'Source', 'Templates', 'system_stm32h7xx.c')]

# Map microcontroller units (MCUs) to their corresponding startup files
mcu_startup_files = {
    'STM32H7A3xx': 'startup_stm32h7a3xx.s',
    'STM32H7A3xxQ': 'startup_stm32h7a3xxq.s',
    'STM32H7B0xx': 'startup_stm32h7b0xx.s',
    'STM32H7B0xxQ': 'startup_stm32h7b0xxq.s',
    'STM32H7B3xx': 'startup_stm32h7b3xx.s',
    'STM32H7B3xxQ': 'startup_stm32h7b3xxq.s',
    'STM32H723xx': 'startup_stm32h723xx.s',
    'STM32H725xx': 'startup_stm32h725xx.s',
    'STM32H730xx': 'startup_stm32h730xx.s',
    'STM32H730xxQ': 'startup_stm32h730xxq.s',
    'STM32H733xx': 'startup_stm32h733xx.s',
    'STM32H735xx': 'startup_stm32h735xx.s',
    'STM32H742xx': 'startup_stm32h742xx.s',
    'STM32H743xx': 'startup_stm32h743xx.s',
    'STM32H745xG': 'startup_stm32h745xg.s',
    'STM32H745xx': 'startup_stm32h745xx.s',
    'STM32H747xG': 'startup_stm32h747xg.s',
    'STM32H747xx': 'startup_stm32h747xx.s',
    'STM32H750xx': 'startup_stm32h750xx.s',
    'STM32H753xx': 'startup_stm32h753xx.s',
    'STM32H755xx': 'startup_stm32h755xx.s',
    'STM32H757xx': 'startup_stm32h757xx.s',
}

# Check each defined MCU, match the platform and append the appropriate startup file
cpp_defines_tuple = env.get('CPPDEFINES', [])
cpp_defines_list = [item[0] if isinstance(item, tuple) else item for item in cpp_defines_tuple]
for mcu, startup_file in mcu_startup_files.items():
    if mcu in cpp_defines_list:
        if rtconfig.PLATFORM in ['gcc', 'llvm-arm']:
            src += [os.path.join(cwd, 'Source', 'Templates', 'gcc', startup_file)]
        elif rtconfig.PLATFORM in ['armcc', 'armclang']:
            src += [os.path.join(cwd, 'Source', 'Templates', 'arm', startup_file)]
        elif rtconfig.PLATFORM in ['iccarm']:
            src += [os.path.join(cwd, 'Source', 'Templates', 'iar', startup_file)]
        break

# Define the build group
group = DefineGroup('STM32H7-CMSIS', src, depend=['PKG_USING_STM32H7_CMSIS_DRIVER'], CPPPATH=path)

# Return the build group
Return('group')
