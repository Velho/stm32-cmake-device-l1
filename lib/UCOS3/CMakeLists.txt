set (UCOS3_APPCFG
    cfg/cpu_cfg.h
    cfg/lib_cfg.h
    cfg/os_app_hooks.h
    cfg/os_cfg.h
    cfg/os_cfg_app.h

    # Implements the OS hooks.
    cfg/os_app_hooks.c)

set (UCOS3_CPU_HEADERS
    uC-CPU/cpu.h
    uC-CPU/cpu_cache.h
    uC-CPU/cpu_core.h
    uC-CPU/cpu_def.h)

set (UCOS3_CPU_SOURCES
    uC-CPU/cpu_a.s
    uC-CPU/cpu_c.c
    uC-CPU/cpu_core.c)

set (UCOS3_LIB_HEADERS
    uC-LIB/lib_def.h
    uC-LIB/lib_ascii.h
    uC-LIB/lib_math.h
    uC-LIB/lib_mem.h
    uC-LIB/lib_str.h)

set (UCOS3_LIB_SOURCES
    uC-LIB/lib_ascii.c
    uC-LIB/lib_math.c
    uC-LIB/lib_mem.c
    uC-LIB/lib_mem_a.s
    uC-LIB/lib_str.c)

set (UCOS3_OS3_SOURCES
    # Enabled?
    uC-OS3/__dbg_uCOS-III.c
    uC-OS3/os_cfg_app.c
    uC-OS3/os_core.c
    uC-OS3/os_cpu_a.S # assembly file
    uC-OS3/os_cpu_c.c
    uC-OS3/os_dbg.c
    uC-OS3/os_flag.c
    uC-OS3/os_mem.c
    uC-OS3/os_msg.c
    uC-OS3/os_mutex.c
    uC-OS3/os_prio.c
    uC-OS3/os_q.c
    uC-OS3/os_sem.c
    uC-OS3/os_stat.c
    uC-OS3/os_task.c
    uC-OS3/os_tick.c
    uC-OS3/os_time.c
    uC-OS3/os_tmr.c
    uC-OS3/os_var.c)

set (UCOS3_OS3_HEADERS
    uC-OS3/os.h
    uC-OS3/os_cpu.h
    uC-OS3/os_trace.h
    uC-OS3/os_type.h)

# ja : create separate targets
add_library (uc-lib ${UCOS3_LIB_SOURCES} ${UCOS3_LIB_HEADERS})
add_library (uc-os3 ${UCOS3_OS3_SOURCES} ${UCOS3_OS3_HEADERS})
add_library (uc-cpu ${UCOS3_CPU_SOURCES} ${UCOS3_CPU_HEADERS})

add_library (uc-cfg OBJECT ${UCOS3_APPCFG})

target_link_libraries (uc-cpu PRIVATE uc-lib)
target_link_libraries (uc-os3 PRIVATE uc-lib uc-cfg)
target_link_libraries (uc-cfg PRIVATE uc-lib)

# Subdirectory wide compile options?
target_compile_options (uc-cpu
    PRIVATE
        -mcpu=cortex-m3
        -mthumb)

target_compile_options (uc-lib
    PRIVATE
        -mcpu=cortex-m3
        -mthumb)

target_compile_options (uc-os3
    PRIVATE
        -mcpu=cortex-m3
        -mthumb)

target_compile_options (uc-cfg
    PRIVATE
        -mcpu=cortex-m3
        -mthumb)

