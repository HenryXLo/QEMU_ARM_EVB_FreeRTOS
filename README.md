# QEMU_ARM_EVB_FreeRTOS 
- This is an QEMU environment running ARM Cortex-M3 RISC (LM3S811) on STM32 evaluation board with FreeRTOS.

Basically, this project refers to this link:
https://hkt999.medium.com/%E4%BD%BF%E7%94%A8-qemu-freertos-visual-studio-code-%E4%BE%86%E9%96%8B%E7%99%BC%E5%B5%8C%E5%85%A5%E5%BC%8F%E7%B3%BB%E7%B5%B1-204c5483f62

1. mkdir work; cd work
2. git clone https://github.com/FreeRTOS/FreeRTOS.git
3. cd FreeRTOS; git submodule update --init --recursive
4. Build Kernel of STM32
- goto ~/work/FreeRTOS/FreeRTOS/Demo/CORTEX_LM3S811_GCC/
- edit Makefile, add '-g' of CFLAGS to build symbol table for kernel source level debug.

5. make. Then gcc/RTOSDemo.bin & gcc/RTOSDemo.axf are built
6. Start QEMU gdb server
- qemu-system-arm -machine lm3s811evb -kernel gcc/RTOSDemo.bin -s -S -nographic

7. Connect to QEMU gdb server @ port:1234
- gdb-multiarch -ex="target remote localhost:1234" gcc/RTOSDemo.axf
