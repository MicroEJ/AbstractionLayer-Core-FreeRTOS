![SDK](https://shields.microej.com/endpoint?url=https://repository.microej.com/packages/badges/sdk_6.0.json)
![ARCH](https://shields.microej.com/endpoint?url=https://repository.microej.com/packages/badges/arch_8.3.json)

# Overview

MicroEJ Core Engine Abstraction Layer implementation for FreeRTOS.

This module implements the `LLMJVM` Low Level API for MicroEJ Platforms connected to a Board Support Package based on [FreeRTOS](https://www.freertos.org/).

See the MicroEJ documentation for a description of the `LLMJVM` functions:
- [LLMJVM: MicroEJ Core Engine](https://docs.microej.com/en/latest/PlatformDeveloperGuide/appendix/llapi.html#llmjvm-microej-core-engine)
- [MicroEJ Core Engine: Implementation](https://docs.microej.com/en/latest/PlatformDeveloperGuide/coreEngine.html#implementation)

# Usage

1. These sources can be included in the VEE Port with the method you prefer, by using this repository as a submodule or by doing a copy of the sources in the VEE Port repository.

2. Implement the MicroEJ time functions, as described in [microej_time.h](./inc/microej_time.h).

3. The `LLMJVM_IMPL_scheduleRequest` schedule request function in [LLMJVM_FreeRTOS.c](./src/LLMJVM_FreeRTOS.c) uses a software timer. In order to correctly schedule MicroEJ threads, check the following elements in the FreeRTOS configuration file:

   - Timers are enabled with `#define configUSE_TIMERS 1`
   - `configTIMER_TASK_PRIORITY` is higher than MicroEJ task priority
   - `configTICK_RATE_HZ`: can depend on the application, if it needs a 1 ms precision then the tick rate would be 1000 Hz, the recommended value is between 100 Hz and 1000 Hz

# Requirements

None.

# Validation

This Abstraction Layer implementation can be validated in the target Board Support Package using the [MicroEJ Core Validation](https://github.com/MicroEJ/PlatformQualificationTools/tree/master/tests/core/java/microej-core-validation) Platform Qualification Tools project.

Here is a non exhaustive list of tested environments:
- Hardware
  - STMicroelectronics STM32F7508-DK
  - Espressif ESP-WROVER-KIT V4.1
- Compilers / Integrated Development Environments:
  - IAR Embedded Workbench 8.50.6
  - STM32CubeIDE version 1.3.0 (using GNU GCC toolchain)
  - Espressif IoT Development Framework (``esp-idf``) v4.4.4 (using GNU GCC toolchain) 
- FreeRTOS versions:
  - FreeRTOS V10.4.3
  - FreeRTOS V10.2.0
  - FreeRTOS V8.2.0


# MISRA Compliance

This Abstraction Layer implementation is MISRA-compliant (MISRA C:2012) with some noted exception.
It has been verified with Cppcheck v2.10. Here is the list of deviations from MISRA standard:

| Deviation  | Category | Justification                                                      |
|:----------:|:--------:|:------------------------------------------------------------------ |
|  Rule 8.4  | Required | The Cppcheck analysis is made only on this LL code                 |
|  Rule 5.5  | Required | Intentional usage of macros to define native functions.            |
|  Rule 7.2  | Required | Error detected in FreeRTOS third library.                          |

# Dependencies

- MicroEJ Architecture ``7.x`` or higher.
- FreeRTOS ``8.2.0`` or higher.

# Source

N/A.

# Restrictions

None.

---

_Copyright 2020-2025 MicroEJ Corp. All rights reserved._
_Use of this source code is governed by a BSD-style license that can be found with this software._
 
