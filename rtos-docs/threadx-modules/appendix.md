---
title: Appendice - Esempi specifici della porta
description: Questo articolo illustra esempi specifici della porta per i moduli ThreadX.
author: philmea
ms.author: philmea
ms.date: 07/15/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: bc4721431810d72a72d5bc69e8382378cb7f95935a8ac755c25a8cff985cd185
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116799371"
---
# <a name="appendix---port-specific-examples"></a>Appendice - Esempi specifici della porta

## <a name="arm11-processor"></a>Processore ARM11

### <a name="arm11-using-gcc"></a>ARM11 con GCC

#### <a name="module-preamble-for-arm11-using-gcc"></a>Preambolo del modulo per ARM11 usando GCC

```armasm
    .arm
    .section .preamble, "ax"

    /* Define the module preamble.  */

    .global _txm_module_preamble
_txm_module_preamble:
    .word       0x4D4F4455                                      @ Module ID
    .word       0x5                                             @ Module Major Version
    .word       0x6                                             @ Module Minor Version
    .word       32                                              @ Module Preamble Size in 32-bit words
    .word       0x12345678                                      @ Module ID (application defined)
    .word       0x02000000                                      @ Module Properties where:
                                                                @   Bits 31-24: Compiler ID
                                                                @           0 -> IAR
                                                                @           1 -> ARM
                                                                @           2 -> GNU
    .word       _txm_module_thread_shell_entry - . - 0          @ Module Shell Entry Point
    .word       demo_module_start - . - 0                       @ Module Start Thread Entry Point
    .word       0                                               @ Module Stop Thread Entry Point
    .word       1                                               @ Module Start/Stop Thread Priority
    .word       1024                                            @ Module Start/Stop Thread Stack Size
    .word       _txm_module_callback_request_thread_entry - . - 0   @ Module Callback Thread Entry
    .word       1                                               @ Module Callback Thread Priority
    .word       1024                                            @ Module Callback Thread Stack Size
    .word       __code_size__                                   @ Module Code Size
    .word       __data_size__                                   @ Module Data Size
    .word       0                                               @ Reserved 0
    .word       0                                               @ Reserved 1
    .word       0                                               @ Reserved 2
    .word       0                                               @ Reserved 3
    .word       0                                               @ Reserved 4
    .word       0                                               @ Reserved 5
    .word       0                                               @ Reserved 6
    .word       0                                               @ Reserved 7  
    .word       0                                               @ Reserved 8  
    .word       0                                               @ Reserved 9
    .word       0                                               @ Reserved 10
    .word       0                                               @ Reserved 11
    .word       0                                               @ Reserved 12
    .word       0                                               @ Reserved 13
    .word       0                                               @ Reserved 14
    .word       0                                               @ Reserved 15
```

#### <a name="module-properties-for-arm11-using-gcc"></a>Proprietà del modulo per ARM11 usando GCC

| bit | Valore | Significato |
|---|---|---|
| [23-0] | 0 | Riservato
| [31-24] | <br />0x00<br />0x01<br />0x02 | **ID compilatore**<br />Iar<br />ARM<br />Gnu |

#### <a name="module-linker-for-arm11-using-gcc"></a>Linker del modulo per ARM11 usando GCC

```c
MEMORY
{
  FLASH (rx) : ORIGIN = 0x080F0000, LENGTH = 0x00010000
  RAM   (wx) : ORIGIN = 0x64001800, LENGTH = 0x00100000
}


SECTIONS
{
  __FLASH_segment_start__ = 0x080F0000;
  __FLASH_segment_end__   = 0x080FFFFF;
  __RAM_segment_start__   = 0x64001800;
  __RAM_segment_end__     = 0x64011800;

  __HEAPSIZE__ = 128;

  __preamble_load_start__ = __FLASH_segment_start__;
  .preamble __FLASH_segment_start__ : AT(__FLASH_segment_start__)
  {
    __preamble_start__ = .;
    *(.preamble .preamble.*)
  }
  __preamble_end__ = __preamble_start__ + SIZEOF(.preamble);

  __dynsym_load_start__ =  ALIGN(__preamble_end__ , 4);
  .dynsym ALIGN(__dynsym_load_start__ , 4) : AT(ALIGN(__dynsym_load_start__ , 4))
  {
    . = ALIGN(4);
    KEEP (*(.dynsym))
    KEEP (*(.dynsym*))
    . = ALIGN(4);
  }
  __dynsym_end__ = __dynsym_load_start__ + SIZEOF(.dynsym);

  __dynstr_load_start__ =  ALIGN(__dynsym_end__ , 4);
  .dynstr ALIGN(__dynstr_load_start__ , 4) : AT(ALIGN(__dynstr_load_start__, 4))
  {
    . = ALIGN(4);
    KEEP (*(.dynstr))
    KEEP (*(.dynstr*))
    . = ALIGN(4);
  }
  __dynstr_end__ = __dynstr_load_start__ + SIZEOF(.dynstr);

  __reldyn_load_start__ =  ALIGN(__dynstr_end__ , 4);
  .rel.dyn ALIGN(__reldyn_load_start__ , 4) : AT(ALIGN(__reldyn_load_start__ , 4))
  {
    . = ALIGN(4);
    KEEP (*(.rel.dyn))
    KEEP (*(.rel.dyn*))
    . = ALIGN(4);
  }
  __reldyn_end__ = __reldyn_load_start__ + SIZEOF(.rel.dyn);

  __relplt_load_start__ =  ALIGN(__reldyn_end__ , 4);
  .rel.plt ALIGN(__relplt_load_start__ , 4) : AT(ALIGN(__relplt_load_start__ , 4))
  {
    . = ALIGN(4);
    KEEP (*(.rel.plt))
    KEEP (*(.rel.plt*))
    . = ALIGN(4);
  }
  __relplt_end__ = __relplt_load_start__ + SIZEOF(.rel.plt);

  __plt_load_start__ =  ALIGN(__relplt_end__ , 4);
  .plt ALIGN(__plt_load_start__ , 4) : AT(ALIGN(__plt_load_start__ , 4))
  {
    . = ALIGN(4);
    KEEP (*(.plt))
    KEEP (*(.plt*))
    . = ALIGN(4);
  }
  __plt_end__ = __plt_load_start__ + SIZEOF(.plt);

  __interp_load_start__ =  ALIGN(__plt_end__ , 4);
  .interp ALIGN(__interp_load_start__ , 4) : AT(ALIGN(__interp_load_start__ , 4))
  {
    . = ALIGN(4);
    KEEP (*(.interp))
    KEEP (*(.interp*))
    . = ALIGN(4);
  }
  __interp_end__ = __interp_load_start__ + SIZEOF(.interp);

  __hash_load_start__ =  ALIGN(__interp_end__ , 4);
  .hash ALIGN(__hash_load_start__ , 4) : AT(ALIGN(__hash_load_start__, 4))
  {
    . = ALIGN(4);
    KEEP (*(.hash))
    KEEP (*(.hash*))
    . = ALIGN(4);
  }
  __hash_end__ = __hash_load_start__ + SIZEOF(.hash);

  __text_load_start__ =  ALIGN(__hash_end__ , 4);
  .text ALIGN(__text_load_start__ , 4) : AT(ALIGN(__text_load_start__, 4))
  {
    __text_start__ = .;
    *(.text .text.* .glue_7t .glue_7 .gnu.linkonce.t.* .gcc_except_table  )
  }
  __text_end__ = __text_start__ + SIZEOF(.text);

  __dtors_load_start__ = ALIGN(__text_end__ , 4);
  .dtors ALIGN(__text_end__ , 4) : AT(ALIGN(__text_end__ , 4))
  {
    __dtors_start__ = .;
    KEEP (*(SORT(.dtors.*))) KEEP (*(.dtors))
  }
  __dtors_end__ = __dtors_start__ + SIZEOF(.dtors);

  __ctors_load_start__ = ALIGN(__dtors_end__ , 4);
  .ctors ALIGN(__dtors_end__ , 4) : AT(ALIGN(__dtors_end__ , 4))
  {
    __ctors_start__ = .;
    KEEP (*(SORT(.ctors.*))) KEEP (*(.ctors))
  }
  __ctors_end__ = __ctors_start__ + SIZEOF(.ctors);

  __got_load_start__ = ALIGN(__ctors_end__ , 4);
  .got ALIGN(__ctors_end__ , 4) : AT(ALIGN(__ctors_end__ , 4))
  {
    . = ALIGN(4);
    _sgot = .;
    KEEP (*(.got))
    KEEP (*(.got*))
    . = ALIGN(4);
    _egot = .;
  }
  __got_end__ =  __got_load_start__ + SIZEOF(.got);

  __rodata_load_start__ = ALIGN(__got_end__ , 4);
  .rodata ALIGN(__got_end__ , 4) : AT(ALIGN(__got_end__ , 4))
  {
    __rodata_start__ = .;
    *(.rodata .rodata.* .gnu.linkonce.r.*)
  }
  __rodata_end__ = __rodata_start__ + SIZEOF(.rodata);

  __code_size__ =  __rodata_end__ - __FLASH_segment_start__;

  __fast_load_start__ = ALIGN(__rodata_end__ , 4);

  __fast_load_end__ = __fast_load_start__ + SIZEOF(.fast);

  __new_got_start__ = ALIGN(__RAM_segment_start__ , 4);

  __new_got_end__ =  __new_got_start__ + SIZEOF(.got);

  .fast ALIGN(__new_got_end__ , 4) : AT(ALIGN(__rodata_end__ , 4))
  {
    __fast_start__ = .;
    *(.fast .fast.*)
  }
  __fast_end__ = __fast_start__ + SIZEOF(.fast);

  .fast_run ALIGN(__fast_end__ , 4) (NOLOAD) :
  {
    __fast_run_start__ = .;
    . = MAX(__fast_run_start__ + SIZEOF(.fast), .);
  }
  __fast_run_end__ = __fast_run_start__ + SIZEOF(.fast_run);

  __data_load_start__ = ALIGN(__fast_load_start__ + SIZEOF(.fast) , 4);
  .data ALIGN(__fast_run_end__ , 4) : AT(ALIGN(__fast_load_start__ + SIZEOF(.fast) , 4))
  {
    __data_start__ = .;
    *(.data .data.* .gnu.linkonce.d.*)
  }
  __data_end__ = __data_start__ + SIZEOF(.data);

  __data_load_end__ = __data_load_start__ + SIZEOF(.data);

  __FLASH_segment_used_end__ = ALIGN(__fast_load_start__ + SIZEOF(.fast) , 4) + SIZEOF(.data);

  .data_run ALIGN(__fast_run_end__ , 4) (NOLOAD) :
  {
    __data_run_start__ = .;
    . = MAX(__data_run_start__ + SIZEOF(.data), .);
  }
  __data_run_end__ = __data_run_start__ + SIZEOF(.data_run);

  __bss_load_start__ = ALIGN(__data_run_end__ , 4);
  .bss ALIGN(__data_run_end__ , 4) (NOLOAD) : AT(ALIGN(__data_run_end__ , 4))
  {
    __bss_start__ = .;
    *(.bss .bss.* .gnu.linkonce.b.*) *(COMMON)
  }
  __bss_end__ = __bss_start__ + SIZEOF(.bss);

  __non_init_load_start__ = ALIGN(__bss_end__ , 4);
  .non_init ALIGN(__bss_end__ , 4) (NOLOAD) : AT(ALIGN(__bss_end__ , 4))
  {
    __non_init_start__ = .;
    *(.non_init .non_init.*)
  }
  __non_init_end__ = __non_init_start__ + SIZEOF(.non_init);

  __heap_load_start__ = ALIGN(__non_init_end__ , 4);
  .heap ALIGN(__non_init_end__ , 4) (NOLOAD) : AT(ALIGN(__non_init_end__ , 4))
  {
    __heap_start__ = .;
    *(.heap)
    . = ALIGN(MAX(__heap_start__ + __HEAPSIZE__ , .), 4);
  }
  __heap_end__ = __heap_start__ + SIZEOF(.heap);

  __data_size__ =  __heap_end__ - __RAM_segment_start__;

}
```

#### <a name="building-modules-for-arm11-using-gcc"></a>Compilazione di moduli per ARM11 con GCC

Un semplice esempio della riga di comando per la compilazione di un modulo ARM11 usando GCC:

```dos
arm-none-eabi-gcc -c -g -mcpu=arm1136j-s -msingle-pic-base -fPIC -mpic-register=r9 txm_module_preamble.S
arm-none-eabi-gcc -c -g -mcpu=arm1136j-s -msingle-pic-base -fPIC -mpic-register=r9 gcc_setup.S
arm-none-eabi-gcc -c -g -mcpu=arm1136j-s -msingle-pic-base -fPIC -mpic-register=r9 demo_threadx_module.c
arm-none-eabi-ld -A arm1136j-s -T demo_threadx_module.ld txm_module_preamble.o gcc_setup.o demo_threadx_module.o txm.a txm.a -o demo_threadx_module.out -M > demo_threadx_module.map
```

#### <a name="thread-extension-definition-for-arm11-using-gcc"></a>Definizione dell'estensione del thread per ARM11 usando GCC

```c
#define TX_THREAD_EXTENSION_2   VOID    *tx_thread_module_instance_ptr;  \
                                VOID    *tx_thread_module_entry_info_ptr;
```

#### <a name="building-module-manager-for-arm11-using-gcc"></a>Compilazione di Gestione moduli per ARM11 usando GCC

Non viene fornito alcun esempio.

#### <a name="attributes-for-external-memory-enable-api-for-arm11-using-gcc"></a>Attributi per l'API di abilitazione della memoria esterna per ARM11 tramite GCC

Questa funzionalità non è abilitata su questa porta.

### <a name="arm11-using-ac5"></a>ARM11 con AC5

#### <a name="module-preamble-for-arm11-using-ac5"></a>Preambolo del modulo per ARM11 con AC5

```armasm
    AREA  Init, CODE, READONLY

;    /* Define public symbols.  */

    EXPORT __txm_module_preamble

;    /* Define application-specific start/stop entry points for the module.  */

    IMPORT demo_module_start

;    /* Define common external references.  */

    IMPORT  _txm_module_thread_shell_entry
    IMPORT  _txm_module_callback_request_thread_entry
    IMPORT  |Image$$ER_RO$$Length|

__txm_module_preamble
        DCD       0x4D4F4455                                        ; Module ID
        DCD       0x5                                               ; Module Major Version
        DCD       0x3                                               ; Module Minor Version
        DCD       32                                                ; Module Preamble Size in 32-bit words
        DCD       0x12345678                                        ; Module ID (application defined)
        DCD       0x01000000                                        ; Module Properties where:
                                                                    ;   Bits 31-24: Compiler ID
                                                                    ;           0 -> IAR
                                                                    ;           1 -> ARM
                                                                    ;           2 -> GNU
                                                                    ;   Bits 23-0:  Reserved
        DCD       _txm_module_thread_shell_entry - . + .            ; Module Shell Entry Point
        DCD       demo_module_start - . + .                         ; Module Start Thread Entry Point
        DCD       0                                                 ; Module Stop Thread Entry Point
        DCD       1                                                 ; Module Start/Stop Thread Priority
        DCD       1024                                              ; Module Start/Stop Thread Stack Size
        DCD       _txm_module_callback_request_thread_entry - . + . ; Module Callback Thread Entry
        DCD       1                                                 ; Module Callback Thread Priority
        DCD       1024                                              ; Module Callback Thread Stack Size
        DCD       |Image$$ER_RO$$Length|                            ; Module Code Size
        DCD       0x4000                                            ; Module Data Size - default to 16K (need to make sure this is large enough for module's data needs!)
        DCD       0                                                 ; Reserved 0
        DCD       0                                                 ; Reserved 1
        DCD       0                                                 ; Reserved 2
        DCD       0                                                 ; Reserved 3
        DCD       0                                                 ; Reserved 4
        DCD       0                                                 ; Reserved 5
        DCD       0                                                 ; Reserved 6
        DCD       0                                                 ; Reserved 7
        DCD       0                                                 ; Reserved 8  
        DCD       0                                                 ; Reserved 9
        DCD       0                                                 ; Reserved 10
        DCD       0                                                 ; Reserved 11
        DCD       0                                                 ; Reserved 12
        DCD       0                                                 ; Reserved 13
        DCD       0                                                 ; Reserved 14
        DCD       0                                                 ; Reserved 15

        END
```

#### <a name="module-properties-for-arm11-using-ac5"></a>Proprietà del modulo per ARM11 tramite AC5

| bit | Valore | Significato |
|---|---|---|
| [23-0] | 0 | Riservato
| [31-24] | <br />0x00<br />0x01<br />0x02 | **ID compilatore**<br />Iar<br />ARM<br />Gnu |

#### <a name="module-linker-for-arm11-using-ac5"></a>Linker del modulo per ARM11 con AC5

Basato sulla riga di comando, nessun esempio di file del linker.

#### <a name="building-modules-for-arm11-using-ac5"></a>Compilazione di moduli per ARM11 con AC5

Un semplice esempio di riga di comando per la compilazione di un modulo ARM11 con AC5:

```dos
armasm -g --cpu ARM1136J-S --apcs /interwork --apcs /ropi --apcs /rwpi txm_module_preamble.s
armcc -g -c -O0 --cpu ARM1136J-S --apcs /interwork --apcs /ropi --apcs /rwpi demo_threadx_module.c
armlink -d -o demo_threadx_module.axf --elf --ro 0 --first txm_module_preamble.o(Init) --entry=_txm_module_thread_shell_entry --ropi --rwpi --remove --map --symbols --list demo_threadx_module.map txm_module_preamble.o demo_threadx_module.o txm.a
```

#### <a name="thread-extension-definition-for-arm11-using-ac5"></a>Definizione dell'estensione thread per ARM11 tramite AC5

```c
#define TX_THREAD_EXTENSION_2   VOID    *tx_thread_module_instance_ptr;  \
                                VOID    *tx_thread_module_entry_info_ptr;
```

#### <a name="building-module-manager-for-arm11-using-ac5"></a>Compilazione di Module Manager per ARM11 con AC5

Un semplice esempio della riga di comando per la compilazione di un modulo arm11 manager con AC5:

```dos
armasm -g --cpu ARM1136J-S --apcs /interwork tx_initialize_low_level.s
armcc -g -c -O2 --cpu ARM1136J-S --apcs /interwork demo_threadx_module_manager.c
armcc -g -c -O2 --cpu ARM1136J-S --apcs /interwork module_code.c
armlink -d -o demo_threadx_module_manager.axf --elf --ro 0 --first tx_initialize_low_level.o(Init) --remove --map --symbols --list demo_threadx_module_manager.map tx_initialize_low_level.o demo_threadx_module_manager.o module_code.o tx.a
```

#### <a name="attributes-for-external-memory-enable-api-for-arm11-using-ac5"></a>Attributi per l'API di abilitazione della memoria esterna per ARM11 tramite AC5

Questa funzionalità non è abilitata su questa porta.

## <a name="cortex-a7-processor"></a>Processore Cortex-A7

### <a name="cortex-a7-using-ac5"></a>Cortex-A7 con AC5

#### <a name="module-preamble-for-cortex-a7-using-ac5"></a>Preambolo del modulo per Cortex-A7 con AC5

```armasm
    AREA  Init, CODE, READONLY

;    /* Define public symbols.  */

    EXPORT __txm_module_preamble

;    /* Define application-specific start/stop entry points for the module.  */

    IMPORT demo_module_start

;    /* Define common external references.  */

    IMPORT  _txm_module_thread_shell_entry
    IMPORT  _txm_module_callback_request_thread_entry
    IMPORT  |Image$$ER_RO$$Length|
    IMPORT  |Image$$ER_RW$$Length|

__txm_module_preamble
    DCD       0x4D4F4455                                        ; Module ID
    DCD       0x5                                               ; Module Major Version
    DCD       0x3                                               ; Module Minor Version
    DCD       32                                                ; Module Preamble Size in 32-bit words
    DCD       0x12345678                                        ; Module ID (application defined)
    DCD       0x01000001                                        ; Module Properties where:
                                                                ;   Bits 31-24: Compiler ID
                                                                ;           0 -> IAR
                                                                ;           1 -> ARM
                                                                ;           2 -> GNU
                                                                ;   Bits 23-1:  Reserved
                                                                ;   Bit 0:  0 -> Privileged mode execution (no MMU protection)
                                                                ;           1 -> User mode execution (MMU protection)
    DCD       _txm_module_thread_shell_entry - . + .            ; Module Shell Entry Point
    DCD       demo_module_start - . + .                         ; Module Start Thread Entry Point
    DCD       0                                                 ; Module Stop Thread Entry Point
    DCD       1                                                 ; Module Start/Stop Thread Priority
    DCD       1024                                              ; Module Start/Stop Thread Stack Size
    DCD       _txm_module_callback_request_thread_entry - . + . ; Module Callback Thread Entry
    DCD       1                                                 ; Module Callback Thread Priority
    DCD       1024                                              ; Module Callback Thread Stack Size
    DCD       |Image$$ER_RO$$Length| + |Image$$ER_RW$$Length|   ; Module Code Size
    DCD       0x4000                                            ; Module Data Size - default to 16K (need to make sure this is large enough for module's data needs!)
    DCD       0                                                 ; Reserved 0
    DCD       0                                                 ; Reserved 1
    DCD       0                                                 ; Reserved 2
    DCD       0                                                 ; Reserved 3
    DCD       0                                                 ; Reserved 4
    DCD       0                                                 ; Reserved 5
    DCD       0                                                 ; Reserved 6
    DCD       0                                                 ; Reserved 7
    DCD       0                                                 ; Reserved 8
    DCD       0                                                 ; Reserved 9
    DCD       0                                                 ; Reserved 10
    DCD       0                                                 ; Reserved 11
    DCD       0                                                 ; Reserved 12
    DCD       0                                                 ; Reserved 13
    DCD       0                                                 ; Reserved 14
    DCD       0                                                 ; Reserved 15

    END
```

#### <a name="module-properties-for-cortex-a7-using-ac5"></a>Proprietà del modulo per Cortex-A7 tramite AC5

| bit | Valore | Significato |
|---|---|---|
| 0 | 0<br />1 | Esecuzione in modalità privilegiata<br />Esecuzione in modalità utente |
| [23-1] | 0 | Riservato
| [31-24] | <br />0x00<br />0x01<br />0x02 | **ID compilatore**<br />Iar<br />ARM<br />Gnu |

#### <a name="module-linker-for-cortex-a7-using-ac5"></a>Linker di modulo per Cortex-A7 con AC5

Basato sulla riga di comando, nessun esempio di file del linker.

#### <a name="building-modules-for-cortex-a7-using-ac5"></a>Compilazione di moduli per Cortex-A7 con AC5

Un semplice esempio della riga di comando per la compilazione di un modulo Cortex-A7 usando AC5:

```dos
armasm -g --cpu=cortex-a7.no_neon --fpu=softvfp --apcs=/interwork/ropi/rwpi txm_module_preamble.s
armcc  -g --cpu=cortex-a7.no_neon --fpu=softvfp -c --apcs=/interwork/ropi/rwpi --lower_ropi demo_threadx_module.c
armlink -d -o demo_threadx_module.axf --elf --ro 0 --first txm_module_preamble.o(Init) --entry=_txm_module_thread_shell_entry --ropi --rwpi --remove --map --symbols --list demo_threadx_module.map txm_module_preamble.o demo_threadx_module.o txm.a
```

#### <a name="thread-extension-definition-for-cortex-a7-using-ac5"></a>Definizione dell'estensione thread per Cortex-A7 tramite AC5

```c
#define TX_THREAD_EXTENSION_2   ULONG   tx_thread_vfp_enable;                   \
                                VOID    *tx_thread_module_instance_ptr;         \
                                VOID    *tx_thread_module_entry_info_ptr;       \
                                ULONG   tx_thread_module_current_user_mode;     \
                                ULONG   tx_thread_module_user_mode;             \
                                VOID    *tx_thread_module_kernel_stack_start;   \
                                VOID    *tx_thread_module_kernel_stack_end;     \
                                ULONG   tx_thread_module_kernel_stack_size;     \
                                VOID    *tx_thread_module_stack_ptr;            \
                                VOID    *tx_thread_module_stack_start;          \
                                VOID    *tx_thread_module_stack_end;            \
                                ULONG   tx_thread_module_stack_size;            \
                                VOID    *tx_thread_module_reserved;
```

#### <a name="building-module-manager-for-cortex-a7-using-ac5"></a>Creazione di Module Manager per Cortex-A7 tramite AC5

Un semplice esempio della riga di comando per la compilazione di un gestore di moduli Cortex-A7 tramite AC5:

```dos
armasm -g --cpu=cortex-a7.no_neon --fpu=softvfp --apcs=interwork tx_initialize_low_level.s
armcc -g --cpu=cortex-a7.no_neon --fpu=softvfp -c demo_threadx_module_manager.c
armcc -g --cpu=cortex-a7.no_neon --fpu=softvfp -c module_code.c
armlink -d -o demo_threadx_module_manager.axf --elf --ro 0x80000000 --first tx_initialize_low_level.o(VECTORS) --remove --map --symbols --list demo_threadx_module_manager.map tx_initialize_low_level.o demo_threadx_module_manager.o module_code.o tx.a
```

#### <a name="attributes-for-external-memory-enable-api-for-cortex-a7-using-ac5"></a>Attributi per l'API di abilitazione della memoria esterna per Cortex-A7 tramite AC5

Per configurare le impostazioni della memoria condivisa, è possibile usare gli attributi seguenti:

| Parametro dell'attributo | Significato |
|---|---|
| TXM_MMU_ATTRIBUTE_XN | Esegui mai |
| TXM_MMU_ATTRIBUTE_B | Impostazione B |
| TXM_MMU_ATTRIBUTE_C | Impostazione di C |
| TXM_MMU_ATTRIBUTE_AP | Impostazione ap |
| TXM_MMU_ATTRIBUTE_TEX | Impostazione TEX |

Per informazioni sulla configurazione di queste impostazioni, vedere la documentazione di ARM.

## <a name="cortex-m3-processor"></a>Processore Cortex-M3

### <a name="cortex-m3-using-ac5"></a>Cortex-M3 con AC5

#### <a name="module-preamble-for-cortex-m3-using-ac5"></a>Preambolo del modulo per Cortex-M3 con AC5

```armasm
    AREA Init, CODE, READONLY

    PRESERVE8

    ; Define public symbols

    EXPORT __txm_module_preamble

    ; Define application-specific start/stop entry points for the module

    EXTERN demo_module_start

    ; Define common external references

    IMPORT  _txm_module_thread_shell_entry
    IMPORT  _txm_module_callback_request_thread_entry
    IMPORT  |Image$$ER_RO$$Length|
    IMPORT  |Image$$ER_RW$$Length|
    IMPORT  |Image$$ER_RW$$RW$$Length|
    IMPORT  |Image$$ER_RW$$ZI$$Length|
    IMPORT  |Image$$ER_ZI$$ZI$$Length|

__txm_module_preamble
    DCD     0x4D4F4455                                          ; Module ID
    DCD     0x6                                                 ; Module Major Version
    DCD     0x1                                                 ; Module Minor Version
    DCD     32                                                  ; Module Preamble Size in 32-bit words
    DCD     0x12345678                                          ; Module ID (application defined)
    DCD     0x01000007                                          ; Module Properties where:
                                                                ;   Bits 31-24: Compiler ID
                                                                ;           0 -> IAR
                                                                ;           1 -> ARM
                                                                ;           2 -> GNU
                                                                ;   Bit 0:  0 -> Privileged mode execution
                                                                ;           1 -> User mode execution
                                                                ;   Bit 1:  0 -> No MPU protection
                                                                ;           1 -> MPU protection (must have user mode selected)
                                                                ;   Bit 2:  0 -> Disable shared/external memory access
                                                                ;           1 -> Enable shared/external memory access
    DCD     _txm_module_thread_shell_entry - __txm_module_preamble              ; Module Shell Entry Point
    DCD     demo_module_start - __txm_module_preamble           ; Module Start Thread Entry Point
    DCD     0                                                   ; Module Stop Thread Entry Point
    DCD     1                                                   ; Module Start/Stop Thread Priority
    DCD     1024                                                ; Module Start/Stop Thread Stack Size
    DCD     _txm_module_callback_request_thread_entry - __txm_module_preamble   ; Module Callback Thread Entry
    DCD     1                                                   ; Module Callback Thread Priority
    DCD     1024                                                ; Module Callback Thread Stack Size
    DCD     |Image$$ER_RO$$Length| + |Image$$ER_RW$$Length|         ; Module Code Size
    DCD     |Image$$ER_RW$$Length| + |Image$$ER_ZI$$ZI$$Length| ; Module Data Size
    DCD     0                                                   ; Reserved 0
    DCD     0                                                   ; Reserved 1
    DCD     0                                                   ; Reserved 2
    DCD     0                                                   ; Reserved 3
    DCD     0                                                   ; Reserved 4
    DCD     0                                                   ; Reserved 5
    DCD     0                                                   ; Reserved 6
    DCD     0                                                   ; Reserved 7
    DCD     0                                                   ; Reserved 8
    DCD     0                                                   ; Reserved 9
    DCD     0                                                   ; Reserved 10
    DCD     0                                                   ; Reserved 11
    DCD     0                                                   ; Reserved 12
    DCD     0                                                   ; Reserved 13
    DCD     0                                                   ; Reserved 14
    DCD     0                                                   ; Reserved 15

    END

```

#### <a name="module-properties-for-cortex-m3-using-ac5"></a>Proprietà del modulo per Cortex-M3 con AC5

| bit | Valore | Significato |
|---|---|---|
| 0 | 0<br />1 | Esecuzione in modalità privilegiata<br />Esecuzione in modalità utente |
| 1 | 0<br />1 | Nessuna protezione MPU<br />Protezione MPU (deve essere selezionata la modalità utente) |
| 2 | 0<br />1 | Disabilitare l'accesso alla memoria condivisa/esterna<br />Abilitare l'accesso alla memoria condivisa/esterna |
| [23-3] | 0 | Riservato
| [31-24] | <br />0x00<br />0x01<br />0x02 | **ID compilatore**<br />Iar<br />ARM<br />Gnu |

#### <a name="module-linker-for-cortex-m3-using-ac5"></a>Linker di modulo per Cortex-M3 con AC5

Non viene fornito alcun file del linker di esempio. Il collegamento viene eseguito nella riga di comando. Vedere la sezione successiva.

#### <a name="building-modules-for-cortex-m3-using-ac5"></a>Compilazione di moduli per Cortex-M3 con AC5

Viene fornito uno script di compilazione di esempio:

```dos
armasm -g --cpu=cortex-m3 --apcs=/interwork/ropi/rwpi txm_module_preamble.S
armcc  -g --cpu=cortex-m3 -c --apcs=/interwork/ropi/rwpi --lower_ropi -I../inc -I../../../../common_modules/inc -I../../../../common_modules/module_manager/inc -I../../../../common/inc sample_threadx_module.c
armlink -d -o sample_threadx_module.axf --elf --ro=0x30000 --rw=0x40000 --first txm_module_preamble.o(Init) --entry=_txm_module_thread_shell_entry --ropi --rwpi --remove --map --symbols --list sample_threadx_module.map txm_module_preamble.o sample_threadx_module.o txm.a
```

#### <a name="thread-extension-definition-for-cortex-m3-using-ac5"></a>Definizione dell'estensione thread per Cortex-M3 con AC5

```c
#define TX_THREAD_EXTENSION_2               VOID    *tx_thread_module_instance_ptr;         \
                                            VOID    *tx_thread_module_entry_info_ptr;       \
                                            ULONG   tx_thread_module_current_user_mode;     \
                                            ULONG   tx_thread_module_user_mode;             \
                                            ULONG   tx_thread_module_saved_lr;              \
                                            VOID    *tx_thread_module_kernel_stack_start;   \
                                            VOID    *tx_thread_module_kernel_stack_end;     \
                                            ULONG   tx_thread_module_kernel_stack_size;     \
                                            VOID    *tx_thread_module_stack_ptr;            \
                                            VOID    *tx_thread_module_stack_start;          \
                                            VOID    *tx_thread_module_stack_end;            \
                                            ULONG   tx_thread_module_stack_size;            \
                                            VOID    *tx_thread_module_reserved;
```

#### <a name="building-module-manager-for-cortex-m3-using-ac5"></a>Creazione di Module Manager per Cortex-M3 tramite AC5

Vedere l'esempio build_threadx_module_manager_demo.bat:

```dos
armasm -g --cpu=cortex-m3 --apcs=interwork tx_initialize_low_level.S
armcc -g --cpu=cortex-m3 -c -I../inc -I../../../../common_modules/inc -I../../../../common_modules/module_manager/inc -I../../../../common/inc sample_threadx_module_manager.c
armlink -d -o sample_threadx_module_manager.axf --elf --ro 0x00000000 --first tx_initialize_low_level.o(RESET) --remove --map --symbols --list sample_threadx_module_manager.map tx_initialize_low_level.o sample_threadx_module_manager.o tx.a
```

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m3-using-ac5"></a>Attributi per l'API di abilitazione della memoria esterna per Cortex-M3 tramite AC5

Il modulo ha sempre accesso in lettura alla memoria condivisa.

| Parametro dell'attributo | Significato |
|---|---|
| TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE | Accesso in scrittura |

### <a name="cortex-m3-using-ac6"></a>Cortex-M3 con AC6

#### <a name="module-preamble-for-cortex-m3-using-ac6"></a>Preambolo del modulo per Cortex-M3 con AC6

```armasm
    .text
    .align 4
    .syntax unified
    .section Init
    
    // Define public symbols
    .global __txm_module_preamble

    // Define application-specific start/stop entry points for the module
    .global demo_module_start

    // Define common external references
    .global  _txm_module_thread_shell_entry
    .global  _txm_module_callback_request_thread_entry

    .eabi_attribute Tag_ABI_PCS_RO_data, 1
    .eabi_attribute Tag_ABI_PCS_R9_use,  1
    .eabi_attribute Tag_ABI_PCS_RW_data, 2

__txm_module_preamble:
    .dc.l   0x4D4F4455                                          // Module ID
    .dc.l   0x6                                                 // Module Major Version
    .dc.l   0x1                                                 // Module Minor Version
    .dc.l   32                                                  // Module Preamble Size in 32-bit words
    .dc.l   0x12345678                                          // Module ID (application defined)
    .dc.l   0x01000007                                          // Module Properties where:
                                                                //   Bits 31-24: Compiler ID
                                                                //           0 -> IAR
                                                                //           1 -> ARM
                                                                //           2 -> GNU
                                                                //   Bit 0:  0 -> Privileged mode execution
                                                                //           1 -> User mode execution
                                                                //   Bit 1:  0 -> No MPU protection
                                                                //           1 -> MPU protection (must have user mode selected)
                                                                //   Bit 2:  0 -> Disable shared/external memory access
                                                                //           1 -> Enable shared/external memory access
    .dc.l   _txm_module_thread_shell_entry - __txm_module_preamble // Module Shell Entry Point
    .dc.l   demo_module_start - __txm_module_preamble           // Module Start Thread Entry Point
    .dc.l   0                                                   // Module Stop Thread Entry Point
    .dc.l   1                                                   // Module Start/Stop Thread Priority
    .dc.l   1024                                                // Module Start/Stop Thread Stack Size
    .dc.l   _txm_module_callback_request_thread_entry - __txm_module_preamble // Module Callback Thread Entry
    .dc.l   1                                                   // Module Callback Thread Priority
    .dc.l   1024                                                // Module Callback Thread Stack Size
    .dc.l   0x10000                                             // Module Code Size
    .dc.l   0x10000                                             // Module Data Size
    .dc.l   0                                                   // Reserved 0
    .dc.l   0                                                   // Reserved 1
    .dc.l   0                                                   // Reserved 2
    .dc.l   0                                                   // Reserved 3
    .dc.l   0                                                   // Reserved 4
    .dc.l   0                                                   // Reserved 5
    .dc.l   0                                                   // Reserved 6
    .dc.l   0                                                   // Reserved 7
    .dc.l   0                                                   // Reserved 8
    .dc.l   0                                                   // Reserved 9
    .dc.l   0                                                   // Reserved 10
    .dc.l   0                                                   // Reserved 11
    .dc.l   0                                                   // Reserved 12
    .dc.l   0                                                   // Reserved 13
    .dc.l   0                                                   // Reserved 14
    .dc.l   0                                                   // Reserved 15
```

#### <a name="module-properties-for-cortex-m3-using-ac6"></a>Proprietà del modulo per Cortex-M3 con AC6

| bit | Valore | Significato |
|---|---|---|
| 0 | 0<br />1 | Esecuzione in modalità privilegiata<br />Esecuzione in modalità utente |
| 1 | 0<br />1 | Nessuna protezione MPU<br />Protezione MPU (deve essere selezionata la modalità utente) |
| 2 | 0<br />1 | Disabilitare l'accesso alla memoria condivisa/esterna<br />Abilitare l'accesso alla memoria condivisa/esterna |
| [23-3] | 0 | Riservato
| [31-24] | <br />0x00<br />0x01<br />0x02 | **ID compilatore**<br />Iar<br />ARM<br />Gnu |

#### <a name="module-linker-for-cortex-m3-using-ac6"></a>Linker di modulo per Cortex-M3 con AC6

Non viene usato alcun file del linker. Vedere le impostazioni del progetto.

#### <a name="building-modules-for-cortex-m3-using-ac6"></a>Compilazione di moduli per Cortex-M3 con AC6

Viene fornita un'area di lavoro di esempio. Compilare la libreria ThreadX, la libreria ThreadX Modules, il progetto di modulo di esempio e il progetto di gestione moduli di esempio.

#### <a name="thread-extension-definition-for-cortex-m3-using-ac6"></a>Definizione dell'estensione thread per Cortex-M3 con AC6

```c
#define TX_THREAD_EXTENSION_2               VOID    *tx_thread_module_instance_ptr;         \
                                            VOID    *tx_thread_module_entry_info_ptr;       \
                                            ULONG   tx_thread_module_current_user_mode;     \
                                            ULONG   tx_thread_module_user_mode;             \
                                            ULONG   tx_thread_module_saved_lr;              \
                                            VOID    *tx_thread_module_kernel_stack_start;   \
                                            VOID    *tx_thread_module_kernel_stack_end;     \
                                            ULONG   tx_thread_module_kernel_stack_size;     \
                                            VOID    *tx_thread_module_stack_ptr;            \
                                            VOID    *tx_thread_module_stack_start;          \
                                            VOID    *tx_thread_module_stack_end;            \
                                            ULONG   tx_thread_module_stack_size;            \
                                            VOID    *tx_thread_module_reserved;
```

#### <a name="building-module-manager-for-cortex-m3-using-ac6"></a>Creazione di Module Manager per Cortex-M3 con AC6

Viene fornita un'area di lavoro di esempio. Compilare la libreria ThreadX, la libreria ThreadX Modules, il progetto di modulo di esempio e il progetto di gestione moduli di esempio.

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m3-using-ac6"></a>Attributi per l'API di abilitazione della memoria esterna per Cortex-M3 tramite AC6

Il modulo ha sempre accesso in lettura alla memoria condivisa.

| Parametro dell'attributo | Significato |
|---|---|
| TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE | Accesso in scrittura |

### <a name="cortex-m3-using-gnu"></a>Cortex-M3 con GNU

#### <a name="module-preamble-for-cortex-m3-using-gnu"></a>Preambolo del modulo per Cortex-M3 con GNU

```armasm
    .text
    .align 4
    .syntax unified

    /* Define public symbols.  */
    .global __txm_module_preamble

    /* Define application-specific start/stop entry points for the module.  */
    .global demo_module_start

    /* Define common external refrences.  */
    .global _txm_module_thread_shell_entry
    .global _txm_module_callback_request_thread_entry

__txm_module_preamble:
    .dc.l      0x4D4F4455                                       // Module ID
    .dc.l      0x6                                              // Module Major Version
    .dc.l      0x1                                              // Module Minor Version
    .dc.l      32                                               // Module Preamble Size in 32-bit words
    .dc.l      0x12345678                                       // Module ID (application defined)
    .dc.l      0x02000007                                       // Module Properties where:
                                                                //   Bits 31-24: Compiler ID
                                                                //           0 -> IAR
                                                                //           1 -> ARM
                                                                //           2 -> GNU
                                                                //   Bits 23-3: Reserved
                                                                //   Bit 2:  0 -> Disable shared/external memory access
                                                                //           1 -> Enable shared/external memory access
                                                                //   Bit 1:  0 -> No MPU protection
                                                                //           1 -> MPU protection (must have user mode selected - bit 0 set)
                                                                //   Bit 0:  0 -> Privileged mode execution
                                                                //           1 -> User mode execution
    .dc.l      _txm_module_thread_shell_entry - . - 0           // Module Shell Entry Point
    .dc.l      demo_module_start - . - 0                        // Module Start Thread Entry Point
    .dc.l      0                                                // Module Stop Thread Entry Point 
    .dc.l      1                                                // Module Start/Stop Thread Priority
    .dc.l      1024                                             // Module Start/Stop Thread Stack Size
    .dc.l      _txm_module_callback_request_thread_entry - . - 0 // Module Callback Thread Entry
    .dc.l      1                                                // Module Callback Thread Priority
    .dc.l      1024                                             // Module Callback Thread Stack Size
    .dc.l      __code_size__                                    // Module Code Size
    .dc.l      __data_size__                                    // Module Data Size
    .dc.l      0                                                // Reserved 0
    .dc.l      0                                                // Reserved 1
    .dc.l      0                                                // Reserved 2
    .dc.l      0                                                // Reserved 3
    .dc.l      0                                                // Reserved 4
    .dc.l      0                                                // Reserved 5
    .dc.l      0                                                // Reserved 6
    .dc.l      0                                                // Reserved 7
    .dc.l      0                                                // Reserved 8
    .dc.l      0                                                // Reserved 9
    .dc.l      0                                                // Reserved 10
    .dc.l      0                                                // Reserved 11
    .dc.l      0                                                // Reserved 12
    .dc.l      0                                                // Reserved 13
    .dc.l      0                                                // Reserved 14
    .dc.l      0                                                // Reserved 15

```

#### <a name="module-properties-for-cortex-m3-using-gnu"></a>Proprietà del modulo per Cortex-M3 con GNU

| bit | Valore | Significato |
|---|---|---|
| 0 | 0<br />1 | Esecuzione in modalità privilegiata<br />Esecuzione in modalità utente |
| 1 | 0<br />1 | Nessuna protezione MPU<br />Protezione MPU (deve essere selezionata la modalità utente) |
| 2 | 0<br />1 | Disabilitare l'accesso alla memoria condivisa/esterna<br />Abilitare l'accesso alla memoria condivisa/esterna |
| [23-3] | 0 | Riservato
| [31-24] | <br />0x00<br />0x01<br />0x02 | **ID compilatore**<br />Iar<br />ARM<br />Gnu |

#### <a name="module-linker-for-cortex-m3-using-gnu"></a>Linker di modulo per Cortex-M3 con GNU

```c
MEMORY
{
  FLASH (rx) : ORIGIN = 0x00030000, LENGTH = 0x00010000
  RAM   (wx) : ORIGIN = 0, LENGTH = 0x00100000
}


SECTIONS
{
  __FLASH_segment_start__ = 0x00030000;
  __FLASH_segment_end__   = 0x00040000;
  __RAM_segment_start__   = 0;
  __RAM_segment_end__     = 0x8000;

  __HEAPSIZE__ = 128;

  __preamble_load_start__ = __FLASH_segment_start__;
  .preamble __FLASH_segment_start__ : AT(__FLASH_segment_start__)
  {
    __preamble_start__ = .;
    *(.preamble .preamble.*)
  }
  __preamble_end__ = __preamble_start__ + SIZEOF(.preamble);

  __dynsym_load_start__ =  ALIGN(__preamble_end__ , 4);
  .dynsym ALIGN(__dynsym_load_start__ , 4) : AT(ALIGN(__dynsym_load_start__ , 4))
  {
    . = ALIGN(4);
    KEEP (*(.dynsym))
    KEEP (*(.dynsym*))
    . = ALIGN(4);
  }
  __dynsym_end__ = __dynsym_load_start__ + SIZEOF(.dynsym);

  __dynstr_load_start__ =  ALIGN(__dynsym_end__ , 4);
  .dynstr ALIGN(__dynstr_load_start__ , 4) : AT(ALIGN(__dynstr_load_start__, 4))
  {
    . = ALIGN(4);
    KEEP (*(.dynstr))
    KEEP (*(.dynstr*))
    . = ALIGN(4);
  }
  __dynstr_end__ = __dynstr_load_start__ + SIZEOF(.dynstr);

  __reldyn_load_start__ =  ALIGN(__dynstr_end__ , 4);
  .rel.dyn ALIGN(__reldyn_load_start__ , 4) : AT(ALIGN(__reldyn_load_start__ , 4))
  {
    . = ALIGN(4);
    KEEP (*(.rel.dyn))
    KEEP (*(.rel.dyn*))
    . = ALIGN(4);
  }
  __reldyn_end__ = __reldyn_load_start__ + SIZEOF(.rel.dyn);

  __relplt_load_start__ =  ALIGN(__reldyn_end__ , 4);
  .rel.plt ALIGN(__relplt_load_start__ , 4) : AT(ALIGN(__relplt_load_start__ , 4))
  {
    . = ALIGN(4);
    KEEP (*(.rel.plt))
    KEEP (*(.rel.plt*))
    . = ALIGN(4);
  }
  __relplt_end__ = __relplt_load_start__ + SIZEOF(.rel.plt);

  __plt_load_start__ =  ALIGN(__relplt_end__ , 4);
  .plt ALIGN(__plt_load_start__ , 4) : AT(ALIGN(__plt_load_start__ , 4))
  {
    . = ALIGN(4);
    KEEP (*(.plt))
    KEEP (*(.plt*))
    . = ALIGN(4);
  }
  __plt_end__ = __plt_load_start__ + SIZEOF(.plt);

  __interp_load_start__ =  ALIGN(__plt_end__ , 4);
  .interp ALIGN(__interp_load_start__ , 4) : AT(ALIGN(__interp_load_start__ , 4))
  {
    . = ALIGN(4);
    KEEP (*(.interp))
    KEEP (*(.interp*))
    . = ALIGN(4);
  }
  __interp_end__ = __interp_load_start__ + SIZEOF(.interp);

  __hash_load_start__ =  ALIGN(__interp_end__ , 4);
  .hash ALIGN(__hash_load_start__ , 4) : AT(ALIGN(__hash_load_start__, 4))
  {
    . = ALIGN(4);
    KEEP (*(.hash))
    KEEP (*(.hash*))
    . = ALIGN(4);
  }
  __hash_end__ = __hash_load_start__ + SIZEOF(.hash);

  __text_load_start__ =  ALIGN(__hash_end__ , 4);
  .text ALIGN(__text_load_start__ , 4) : AT(ALIGN(__text_load_start__, 4))
  {
    __text_start__ = .;
    *(.text .text.* .glue_7t .glue_7 .gnu.linkonce.t.* .gcc_except_table  )
  }
  __text_end__ = __text_start__ + SIZEOF(.text);

  __dtors_load_start__ = ALIGN(__text_end__ , 4);
  .dtors ALIGN(__text_end__ , 4) : AT(ALIGN(__text_end__ , 4))
  {
    __dtors_start__ = .;
    KEEP (*(SORT(.dtors.*))) KEEP (*(.dtors))
  }
  __dtors_end__ = __dtors_start__ + SIZEOF(.dtors);

  __ctors_load_start__ = ALIGN(__dtors_end__ , 4);
  .ctors ALIGN(__dtors_end__ , 4) : AT(ALIGN(__dtors_end__ , 4))
  {
    __ctors_start__ = .;
    KEEP (*(SORT(.ctors.*))) KEEP (*(.ctors))
  }
  __ctors_end__ = __ctors_start__ + SIZEOF(.ctors);

  __got_load_start__ = ALIGN(__ctors_end__ , 4);
  .got ALIGN(__ctors_end__ , 4) : AT(ALIGN(__ctors_end__ , 4))
  {
    . = ALIGN(4);
    _sgot = .;
    KEEP (*(.got))
    KEEP (*(.got*))
    . = ALIGN(4);
    _egot = .;
  } 
  __got_end__ =  __got_load_start__ + SIZEOF(.got);

  __rodata_load_start__ = ALIGN(__got_end__ , 4);
  .rodata ALIGN(__got_end__ , 4) : AT(ALIGN(__got_end__ , 4))
  {
    __rodata_start__ = .;
    *(.rodata .rodata.* .gnu.linkonce.r.*)
  }
  __rodata_end__ = __rodata_start__ + SIZEOF(.rodata);
 
  __code_size__ =  __rodata_end__ - __FLASH_segment_start__;

  __fast_load_start__ = ALIGN(__rodata_end__ , 4);

  __fast_load_end__ = __fast_load_start__ + SIZEOF(.fast);

  __new_got_start__ = ALIGN(__RAM_segment_start__ , 4);

  __new_got_end__ =  __new_got_start__ + SIZEOF(.got);

  .fast ALIGN(__new_got_end__ , 4) : AT(ALIGN(__rodata_end__ , 4))
  {
    __fast_start__ = .;
    *(.fast .fast.*)
  }
  __fast_end__ = __fast_start__ + SIZEOF(.fast);

  .fast_run ALIGN(__fast_end__ , 4) (NOLOAD) :
  {
    __fast_run_start__ = .;
    . = MAX(__fast_run_start__ + SIZEOF(.fast), .);
  }
  __fast_run_end__ = __fast_run_start__ + SIZEOF(.fast_run);

  __data_load_start__ = ALIGN(__fast_load_start__ + SIZEOF(.fast) , 4);
  .data ALIGN(__fast_run_end__ , 4) : AT(ALIGN(__fast_load_start__ + SIZEOF(.fast) , 4))
  {
    __data_start__ = .;
    *(.data .data.* .gnu.linkonce.d.*)
  }
  __data_end__ = __data_start__ + SIZEOF(.data);

  __data_load_end__ = __data_load_start__ + SIZEOF(.data);

  __FLASH_segment_used_end__ = ALIGN(__fast_load_start__ + SIZEOF(.fast) , 4) + SIZEOF(.data);

  .data_run ALIGN(__fast_run_end__ , 4) (NOLOAD) :
  {
    __data_run_start__ = .;
    . = MAX(__data_run_start__ + SIZEOF(.data), .);
  }
  __data_run_end__ = __data_run_start__ + SIZEOF(.data_run);

  __bss_load_start__ = ALIGN(__data_run_end__ , 4);
  .bss ALIGN(__data_run_end__ , 4) (NOLOAD) : AT(ALIGN(__data_run_end__ , 4))
  {
    __bss_start__ = .;
    *(.bss .bss.* .gnu.linkonce.b.*) *(COMMON)
  }
  __bss_end__ = __bss_start__ + SIZEOF(.bss);

  __non_init_load_start__ = ALIGN(__bss_end__ , 4);
  .non_init ALIGN(__bss_end__ , 4) (NOLOAD) : AT(ALIGN(__bss_end__ , 4))
  {
    __non_init_start__ = .;
    *(.non_init .non_init.*)
  }
  __non_init_end__ = __non_init_start__ + SIZEOF(.non_init);

  __heap_load_start__ = ALIGN(__non_init_end__ , 4);
  .heap ALIGN(__non_init_end__ , 4) (NOLOAD) : AT(ALIGN(__non_init_end__ , 4))
  {
    __heap_start__ = .;
    *(.heap)
    . = ALIGN(MAX(__heap_start__ + __HEAPSIZE__ , .), 4);
  }
  __heap_end__ = __heap_start__ + SIZEOF(.heap);

  __data_size__ =  __heap_end__ - __RAM_segment_start__;

}
```

#### <a name="building-modules-for-cortex-m3-using-gnu"></a>Compilazione di moduli per Cortex-M3 con GNU

Vedere build_threadx_module_sample.bat:

```dos
arm-none-eabi-gcc -c -g -mcpu=cortex-m3 -fpie -fno-plt -mpic-data-is-text-relative -msingle-pic-base txm_module_preamble.s
arm-none-eabi-gcc -c -g -mcpu=cortex-m3 -fpie -fno-plt -mpic-data-is-text-relative -msingle-pic-base gcc_setup.S
arm-none-eabi-gcc -c -g -mcpu=cortex-m3 -fpie -fno-plt -mpic-data-is-text-relative -msingle-pic-base -I..\inc -I..\..\..\..\common\inc -I..\..\..\..\common_modules\inc sample_threadx_module.c
arm-none-eabi-ld -A cortex-m3 -T sample_threadx_module.ld txm_module_preamble.o gcc_setup.o sample_threadx_module.o -e _txm_module_thread_shell_entry txm.a -o sample_threadx_module.axf -M > sample_threadx_module.map
```

#### <a name="thread-extension-definition-for-cortex-m3-using-gnu"></a>Definizione dell'estensione del thread per Cortex-M3 con GNU

```c
#define TX_THREAD_EXTENSION_2               VOID    *tx_thread_module_instance_ptr;         \
                                            VOID    *tx_thread_module_entry_info_ptr;       \
                                            ULONG   tx_thread_module_current_user_mode;     \
                                            ULONG   tx_thread_module_user_mode;             \
                                            ULONG   tx_thread_module_saved_lr;              \
                                            VOID    *tx_thread_module_kernel_stack_start;   \
                                            VOID    *tx_thread_module_kernel_stack_end;     \
                                            ULONG   tx_thread_module_kernel_stack_size;     \
                                            VOID    *tx_thread_module_stack_ptr;            \
                                            VOID    *tx_thread_module_stack_start;          \
                                            VOID    *tx_thread_module_stack_end;            \
                                            ULONG   tx_thread_module_stack_size;            \
                                            VOID    *tx_thread_module_reserved;
```

#### <a name="building-module-manager-for-cortex-m3-using-gnu"></a>Building Module Manager for Cortex-M3 using GNU

Vedere build_threadx_module_manager_sample.bat:

```dos
arm-none-eabi-gcc -c -g -mcpu=cortex-m3 -mthumb -I..\inc -I..\..\..\..\common\inc -I..\..\..\..\common_modules\inc sample_threadx_module_manager.c
arm-none-eabi-gcc -c -g -mcpu=cortex-m3 -mthumb tx_simulator_startup.S
arm-none-eabi-gcc -c -g -mcpu=cortex-m3 -mthumb cortexm_crt0.S
arm-none-eabi-ld -A cortex-m3 -ereset_handler -T sample_threadx.ld tx_simulator_startup.o cortexm_crt0.o sample_threadx_module_manager.o tx.a  libc.a -o sample_threadx_module_manager.axf -M > sample_threadx_module_manager.map
```

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m3-using-gnu"></a>Attributi per l'API di abilitazione della memoria esterna per Cortex-M3 tramite GNU

Il modulo ha sempre accesso in lettura alla memoria condivisa.

| Parametro attribute | Significato |
|---|---|
| TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE | Accesso in scrittura |

### <a name="cortex-m3-using-iar"></a>Cortex-M3 con IAR

#### <a name="module-preamble-for-cortex-m3-using-iar"></a>Preambolo del modulo per Cortex-M3 con IAR

```c
    SECTION .text:CODE

    AAPCS INTERWORK, ROPI, RWPI_COMPATIBLE,  VFP_COMPATIBLE
    PRESERVE8

    /* Define public symbols.  */

    PUBLIC __txm_module_preamble


    /* Define application-specific start/stop entry points for the module.  */

    EXTERN demo_module_start


    /* Define common external references.  */

    EXTERN  _txm_module_thread_shell_entry
    EXTERN  _txm_module_callback_request_thread_entry
    EXTERN  ROPI$$Length
    EXTERN  RWPI$$Length

    DATA
__txm_module_preamble:
    DC32      0x4D4F4455                                        ; Module ID
    DC32      0x5                                               ; Module Major Version
    DC32      0x6                                               ; Module Minor Version
    DC32      32                                                ; Module Preamble Size in 32-bit words
    DC32      0x12345678                                        ; Module ID (application defined)
    DC32      0x00000007                                        ; Module Properties where:
                                                                ;   Bits 31-24: Compiler ID
                                                                ;           0 -> IAR
                                                                ;           1 -> ARM
                                                                ;           2 -> GNU
                                                                ;   Bits 23-3: Reserved
                                                                ;   Bit 2:  0 -> Disable shared/external memory access
                                                                ;           1 -> Enable shared/external memory access
                                                                ;   Bit 1:  0 -> No MPU protection
                                                                ;           1 -> MPU protection (must have user mode selected - bit 0 set)
                                                                ;   Bit 0:  0 -> Privileged mode execution
                                                                ;           1 -> User mode execution


    DC32      _txm_module_thread_shell_entry - . - 0            ; Module Shell Entry Point
    DC32      demo_module_start - . - 0                         ; Module Start Thread Entry Point
    DC32      0                                                 ; Module Stop Thread Entry Point
    DC32      1                                                 ; Module Start/Stop Thread Priority
    DC32      1024                                              ; Module Start/Stop Thread Stack Size
    DC32      _txm_module_callback_request_thread_entry - . - 0 ; Module Callback Thread Entry
    DC32      1                                                 ; Module Callback Thread Priority
    DC32      1024                                              ; Module Callback Thread Stack Size
    DC32      ROPI$$Length                                      ; Module Code Size
    DC32      RWPI$$Length                                      ; Module Data Size
    DC32      0                                                 ; Reserved 0
    DC32      0                                                 ; Reserved 1
    DC32      0                                                 ; Reserved 2
    DC32      0                                                 ; Reserved 3
    DC32      0                                                 ; Reserved 4
    DC32      0                                                 ; Reserved 5
    DC32      0                                                 ; Reserved 6
    DC32      0                                                 ; Reserved 7
    DC32      0                                                 ; Reserved 8  
    DC32      0                                                 ; Reserved 9
    DC32      0                                                 ; Reserved 10
    DC32      0                                                 ; Reserved 11
    DC32      0                                                 ; Reserved 12
    DC32      0                                                 ; Reserved 13
    DC32      0                                                 ; Reserved 14
    DC32      0                                                 ; Reserved 15

    END
```

#### <a name="module-properties-for-cortex-m3-using-iar"></a>Proprietà del modulo per Cortex-M3 con IAR

| bit | Valore | Significato |
|---|---|---|
| 0 | 0<br />1 | Esecuzione in modalità privilegiata<br />Esecuzione in modalità utente |
| 1 | 0<br />1 | Nessuna protezione MPU<br />Protezione MPU (deve essere selezionata la modalità utente) |
| 2 | 0<br />1 | Disabilitare l'accesso alla memoria condivisa/esterna<br />Abilitare l'accesso alla memoria condivisa/esterna |
| [23-3] | 0 | Riservato
| [31-24] | <br />0x00<br />0x01<br />0x02 | **ID compilatore**<br />Iar<br />ARM<br />Gnu |

#### <a name="module-linker-for-cortex-m3-using-iar"></a>Linker di modulo per Cortex-M3 con IAR

```c
/*###ICF### Section handled by ICF editor, don't touch! ****/
/*-Editor annotation file-*/
/* IcfEditorFile="$TOOLKIT_DIR$\config\ide\IcfEditor\a_v1_0.xml" */
/*-Specials-*/
define symbol __ICFEDIT_intvec_start__ = 0x0;
/*-Memory Regions-*/
define symbol __ICFEDIT_region_ROM_start__ = 0x080f0000;
define symbol __ICFEDIT_region_ROM_end__   = 0x080fffff;
define symbol __ICFEDIT_region_RAM_start__ = 0x64002800;
define symbol __ICFEDIT_region_RAM_end__   = 0x64100000;
/*-Sizes-*/
define symbol __ICFEDIT_size_cstack__   = 0;
define symbol __ICFEDIT_size_svcstack__ = 0;
define symbol __ICFEDIT_size_irqstack__ = 0;
define symbol __ICFEDIT_size_fiqstack__ = 0;
define symbol __ICFEDIT_size_undstack__ = 0;
define symbol __ICFEDIT_size_abtstack__ = 0;
define symbol __ICFEDIT_size_heap__     = 0x1000;
/**** End of ICF editor section. ###ICF###*/

define memory mem with size = 4G;
define region ROM_region   = mem:[from __ICFEDIT_region_ROM_start__   to __ICFEDIT_region_ROM_end__];
define region RAM_region   = mem:[from __ICFEDIT_region_RAM_start__   to __ICFEDIT_region_RAM_end__];

//define block CSTACK    with alignment = 8, size = __ICFEDIT_size_cstack__   { };
//define block SVC_STACK with alignment = 8, size = __ICFEDIT_size_svcstack__ { };
//define block IRQ_STACK with alignment = 8, size = __ICFEDIT_size_irqstack__ { };
//define block FIQ_STACK with alignment = 8, size = __ICFEDIT_size_fiqstack__ { };
//define block UND_STACK with alignment = 8, size = __ICFEDIT_size_undstack__ { };
//define block ABT_STACK with alignment = 8, size = __ICFEDIT_size_abtstack__ { };
define block HEAP      with alignment = 8, size = __ICFEDIT_size_heap__     { };

initialize by copy { readwrite };
do not initialize  { section .noinit };

//place at address mem:__ICFEDIT_intvec_start__ { readonly section .intvec };

define movable block ROPI with alignment = 4, fixed order
{
  ro object txm_module_preamble_stm32f2xx.o,
  ro,
  ro data
};

define movable block RWPI with alignment = 8, fixed order, static base
{
  rw,
  block HEAP
};

place in ROM_region   { block ROPI };
place in RAM_region   { block RWPI };
```

#### <a name="building-modules-for-cortex-m3-using-iar"></a>Compilazione di moduli per Cortex-M3 con IAR

Viene fornita un'area di lavoro di esempio. Compilare la libreria ThreadX, la libreria dei moduli ThreadX, il progetto di modulo demo e il progetto demo module manager.

#### <a name="thread-extension-definition-for-cortex-m3-using-iar"></a>Definizione dell'estensione thread per Cortex-M3 con IAR

```c
#define TX_THREAD_EXTENSION_2   VOID    *tx_thread_module_instance_ptr;         \
                                VOID    *tx_thread_module_entry_info_ptr;       \
                                ULONG   tx_thread_module_current_user_mode;     \
                                ULONG   tx_thread_module_user_mode;             \
                                ULONG   tx_thread_module_saved_lr;              \
                                VOID    *tx_thread_module_kernel_stack_start;   \
                                VOID    *tx_thread_module_kernel_stack_end;     \
                                ULONG   tx_thread_module_kernel_stack_size;     \
                                VOID    *tx_thread_module_stack_ptr;            \
                                VOID    *tx_thread_module_stack_start;          \
                                VOID    *tx_thread_module_stack_end;            \
                                ULONG   tx_thread_module_stack_size;            \
                                VOID    *tx_thread_module_reserved;             \
                                VOID    *tx_thread_iar_tls_pointer;
```

#### <a name="building-module-manager-for-cortex-m3-using-iar"></a>Building Module Manager for Cortex-M3 using IAR

Viene fornita un'area di lavoro di esempio. Compilare la libreria ThreadX, la libreria dei moduli ThreadX, il progetto di modulo demo e il progetto demo module manager.

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m3-using-iar"></a>Attributi per l'API di abilitazione della memoria esterna per Cortex-M3 con IAR

Il modulo ha sempre accesso in lettura alla memoria condivisa.

| Parametro attribute | Significato |
|---|---|
| TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE | Accesso in scrittura |

## <a name="cortex-m33-processor"></a>Processore Cortex-M33

### <a name="cortex-m33-using-ac6"></a>Cortex-M33 con AC6

#### <a name="module-preamble-for-cortex-m33-using-ac6"></a>Preambolo del modulo per Cortex-M33 con AC6

```c
    .text
    .align 4
    .syntax unified
    .section RESET
    
    // Define public symbols
    .global __txm_module_preamble

    // Define application-specific start/stop entry points for the module
    .global demo_module_start

    // Define common external references
    .global  _txm_module_thread_shell_entry
    .global  _txm_module_callback_request_thread_entry

    .eabi_attribute Tag_ABI_PCS_RO_data, 1
    .eabi_attribute Tag_ABI_PCS_R9_use,  1
    .eabi_attribute Tag_ABI_PCS_RW_data, 2

__txm_module_preamble:
    .dc.l   0x4D4F4455                                          // Module ID
    .dc.l   0x6                                                 // Module Major Version
    .dc.l   0x1                                                 // Module Minor Version
    .dc.l   32                                                  // Module Preamble Size in 32-bit words
    .dc.l   0x12345678                                          // Module ID (application defined)
    .dc.l   0x01000007                                          // Module Properties where:
                                                                //   Bits 31-24: Compiler ID
                                                                //           0 -> IAR
                                                                //           1 -> ARM
                                                                //           2 -> GNU
                                                                //   Bit 0:  0 -> Privileged mode execution
                                                                //           1 -> User mode execution
                                                                //   Bit 1:  0 -> No MPU protection
                                                                //           1 -> MPU protection (must have user mode selected)
                                                                //   Bit 2:  0 -> Disable shared/external memory access
                                                                //           1 -> Enable shared/external memory access
    .dc.l   _txm_module_thread_shell_entry - __txm_module_preamble // Module Shell Entry Point
    .dc.l   demo_module_start - __txm_module_preamble           // Module Start Thread Entry Point
    .dc.l   0                                                   // Module Stop Thread Entry Point
    .dc.l   1                                                   // Module Start/Stop Thread Priority
    .dc.l   1024                                                // Module Start/Stop Thread Stack Size
    .dc.l   _txm_module_callback_request_thread_entry - __txm_module_preamble // Module Callback Thread Entry
    .dc.l   1                                                   // Module Callback Thread Priority
    .dc.l   1024                                                // Module Callback Thread Stack Size
    //the tools can't add two symbols together, but it should look like this:
    //.dc.l   Image$$ER_RO$$Length + Image$$ER_RW$$Length         // Module Code Size
    //.dc.l   Image$$ER_RW$$Length + Image$$ER_ZI$$ZI$$Length     // Module Data Size
    //so instead we'll define hard values:
    .dc.l   0x4000                                              // Module Code Size
    .dc.l   0x4000                                              // Module Data Size
    .dc.l   0                                                   // Reserved 0
    .dc.l   0                                                   // Reserved 1
    .dc.l   0                                                   // Reserved 2
    .dc.l   0                                                   // Reserved 3
    .dc.l   0                                                   // Reserved 4
    .dc.l   0                                                   // Reserved 5
    .dc.l   0                                                   // Reserved 6
    .dc.l   0                                                   // Reserved 7
    .dc.l   0                                                   // Reserved 8
    .dc.l   0                                                   // Reserved 9
    .dc.l   0                                                   // Reserved 10
    .dc.l   0                                                   // Reserved 11
    .dc.l   0                                                   // Reserved 12
    .dc.l   0                                                   // Reserved 13
    .dc.l   0                                                   // Reserved 14
    .dc.l   0                                                   // Reserved 15
```

#### <a name="module-properties-for-cortex-m33-using-ac6"></a>Proprietà del modulo per Cortex-M33 con AC6

| bit | Valore | Significato |
|---|---|---|
| 0 | 0<br />1 | Esecuzione in modalità privilegiata<br />Esecuzione in modalità utente |
| 1 | 0<br />1 | Nessuna protezione MPU<br />Protezione MPU (deve essere selezionata la modalità utente) |
| 2 | 0<br />1 | Disabilitare l'accesso alla memoria condivisa/esterna<br />Abilitare l'accesso alla memoria condivisa/esterna |
| [23-3] | 0 | Riservato
| [31-24] | <br />0x00<br />0x01<br />0x02 | **ID compilatore**<br />Iar<br />ARM<br />Gnu |

#### <a name="module-linker-for-cortex-m33-using-ac6"></a>Linker di modulo per Cortex-M33 con AC6

Nessun file del linker necessario per la toolchain Keil. Vedere le impostazioni di compilazione nel progetto di esempio.
Di seguito sono elencate importanti opzioni del linker:

```c
--entry demo_module_start --first __txm_module_preamble
```

#### <a name="building-modules-for-cortex-m33-using-ac6"></a>Compilazione di moduli per Cortex-M33 con AC6

Impostazioni del compilatore:

```c
-xc -std=c99 --target=arm-arm-none-eabi -mcpu=cortex-m33 -mfpu=fpv5-sp-d16 -mfloat-abi=hard -c
-fno-rtti -funsigned-char -fshort-enums -fshort-wchar
-mlittle-endian -gdwarf-3 -fropi -frwpi -O1 -ffunction-sections -Wno-packed -Wno-missing-variable-declarations -Wno-missing-prototypes -Wno-missing-noreturn -Wno-sign-conversion -Wno-nonportable-include-path -Wno-reserved-id-macro -Wno-unused-macros -Wno-documentation-unknown-command -Wno-documentation -Wno-license-management -Wno-parentheses-equality -I ../../../../../common_modules/inc -I ../../../../../common/inc -I ../../../../../ports_module/cortex_m33/ac6/inc -I ../demo_secure_zone
-I./RTE/_FVP_Simulation_Model
-IC:/Users/your_path/AppData/Local/Arm/Packs/ARM/CMSIS/5.5.1/CMSIS/Core/Include
-IC:/Users/your_path/AppData/Local/Arm/Packs/ARM/CMSIS/5.5.1/Device/ARM/ARMCM33/Include
-D__UVISION_VERSION="531" -D_RTE_ -DARMCM33_DSP_FP_TZ -D_RTE_
-o ./Objects/*.o -MD
```

#### <a name="thread-extension-definition-for-cortex-m33-using-ac6"></a>Definizione dell'estensione thread per Cortex-M33 tramite AC6

```c
#define TX_THREAD_EXTENSION_2                   VOID    *tx_thread_module_instance_ptr;         \
                                                VOID    *tx_thread_module_entry_info_ptr;       \
                                                ULONG   tx_thread_module_current_user_mode;     \
                                                ULONG   tx_thread_module_user_mode;             \
                                                ULONG   tx_thread_module_saved_lr;              \
                                                VOID    *tx_thread_module_kernel_stack_start;   \
                                                VOID    *tx_thread_module_kernel_stack_end;     \
                                                ULONG   tx_thread_module_kernel_stack_size;     \
                                                VOID    *tx_thread_module_stack_ptr;            \
                                                VOID    *tx_thread_module_stack_start;          \
                                                VOID    *tx_thread_module_stack_end;            \
                                                ULONG   tx_thread_module_stack_size;            \
                                                VOID    *tx_thread_module_reserved;
```

#### <a name="building-module-manager-for-cortex-m33-using-ac6"></a>Creazione di Module Manager per Cortex-M33 tramite AC6

Viene fornita un'area di lavoro di esempio. Compilare la libreria ThreadX, la libreria ThreadX Modules, sample_threadx_module progetto e demo_threadx_non-secure_zone progetto.

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m33-using-ac6"></a>Attributi per l'API di abilitazione della memoria esterna per Cortex-M33 tramite AC6

| Parametro dell'attributo |
|---|
| TXM_MODULE_ATTRIBUTE_NON_SHAREABLE |
| TXM_MODULE_ATTRIBUTE_OUTER_SHAREABLE |
| TXM_MODULE_ATTRIBUTE_INNER_SHAREABLE |
| TXM_MODULE_ATTRIBUTE_READ_WRITE |
| TXM_MODULE_ATTRIBUTE_READ_ONLY |

### <a name="cortex-m33-using-gnu"></a>Cortex-M33 con GNU

#### <a name="module-preamble-for-cortex-m33-using-gnu"></a>Preambolo del modulo per Cortex-M33 con GNU

#### <a name="module-properties-for-cortex-m33-using-gnu"></a>Proprietà del modulo per Cortex-M33 tramite GNU

| bit | Valore | Significato |
|---|---|---|
| 0 | 0<br />1 | Esecuzione in modalità privilegiata<br />Esecuzione in modalità utente |
| 1 | 0<br />1 | Nessuna protezione MPU<br />Protezione MPU (deve essere selezionata la modalità utente) |
| 2 | 0<br />1 | Disabilitare l'accesso alla memoria condivisa/esterna<br />Abilitare l'accesso alla memoria condivisa/esterna |
| [23-3] | 0 | Riservato
| [31-24] | <br />0x00<br />0x01<br />0x02 | **ID compilatore**<br />Iar<br />ARM<br />Gnu |

#### <a name="module-linker-for-cortex-m33-using-gnu"></a>Linker di modulo per Cortex-M33 con GNU

#### <a name="building-modules-for-cortex-m33-using-gnu"></a>Compilazione di moduli per Cortex-M33 con GNU

#### <a name="thread-extension-definition-for-cortex-m33-using-gnu"></a>Definizione dell'estensione thread per Cortex-M33 tramite GNU

#### <a name="building-module-manager-for-cortex-m33-using-gnu"></a>Compilazione di Module Manager per Cortex-M33 con GNU

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m33-using-gnu"></a>Attributi per l'API di abilitazione della memoria esterna per Cortex-M33 tramite GNU

| Parametro dell'attributo |
|---|
| TXM_MODULE_ATTRIBUTE_NON_SHAREABLE |
| TXM_MODULE_ATTRIBUTE_OUTER_SHAREABLE |
| TXM_MODULE_ATTRIBUTE_INNER_SHAREABLE |
| TXM_MODULE_ATTRIBUTE_READ_WRITE |
| TXM_MODULE_ATTRIBUTE_READ_ONLY |

### <a name="cortex-m33-using-iar"></a>Cortex-M33 con IAR

#### <a name="module-preamble-for-cortex-m33-using-iar"></a>Preambolo del modulo per Cortex-M33 con IAR

```c
    SECTION .text:CODE

    AAPCS INTERWORK, ROPI, RWPI_COMPATIBLE,  VFP_COMPATIBLE
    PRESERVE8

    /* Define public symbols.  */

    PUBLIC __txm_module_preamble


    /* Define application-specific start/stop entry points for the module.  */

    EXTERN demo_module_start


    /* Define common external refrences.  */

    EXTERN  _txm_module_thread_shell_entry
    EXTERN  _txm_module_callback_request_thread_entry
    EXTERN  ROPI$$Length
    EXTERN  RWPI$$Length

    DATA
__txm_module_preamble:
    DC32      0x4D4F4455                                        // Module ID
    DC32      0x6                                               // Module Major Version
    DC32      0x1                                               // Module Minor Version
    DC32      32                                                // Module Preamble Size in 32-bit words
    DC32      0x12345678                                        // Module ID (application defined)
    DC32      0x00000007                                        // Module Properties where:
                                                                //   Bits 31-24: Compiler ID
                                                                //           0 -> IAR
                                                                //           1 -> ARM
                                                                //           2 -> GNU
                                                                //   Bits 23-3: Reserved
                                                                //   Bit 2:  0 -> Disable shared/external memory access
                                                                //           1 -> Enable shared/external memory access
                                                                //   Bit 1:  0 -> No MPU protection
                                                                //           1 -> MPU protection (must have user mode selected - bit 0 set)
                                                                //   Bit 0:  0 -> Privileged mode execution
                                                                //           1 -> User mode execution
    DC32      _txm_module_thread_shell_entry - . - 0            // Module Shell Entry Point
    DC32      demo_module_start - . - 0                         // Module Start Thread Entry Point
    DC32      0                                                 // Module Stop Thread Entry Point
    DC32      1                                                 // Module Start/Stop Thread Priority
    DC32      1024                                              // Module Start/Stop Thread Stack Size
    DC32      _txm_module_callback_request_thread_entry - . - 0 // Module Callback Thread Entry
    DC32      1                                                 // Module Callback Thread Priority
    DC32      1024                                              // Module Callback Thread Stack Size
    DC32      ROPI$$Length                                      // Module Code Size
    DC32      RWPI$$Length                                      // Module Data Size
    DC32      0                                                 // Reserved 0
    DC32      0                                                 // Reserved 1
    DC32      0                                                 // Reserved 2
    DC32      0                                                 // Reserved 3
    DC32      0                                                 // Reserved 4
    DC32      0                                                 // Reserved 5
    DC32      0                                                 // Reserved 6
    DC32      0                                                 // Reserved 7
    DC32      0                                                 // Reserved 8
    DC32      0                                                 // Reserved 9
    DC32      0                                                 // Reserved 10
    DC32      0                                                 // Reserved 11
    DC32      0                                                 // Reserved 12
    DC32      0                                                 // Reserved 13
    DC32      0                                                 // Reserved 14
    DC32      0                                                 // Reserved 15

    END

```

#### <a name="module-properties-for-cortex-m33-using-iar"></a>Proprietà del modulo per Cortex-M33 con IAR

| bit | Valore | Significato |
|---|---|---|
| 0 | 0<br />1 | Esecuzione in modalità privilegiata<br />Esecuzione in modalità utente |
| 1 | 0<br />1 | Nessuna protezione MPU<br />Protezione MPU (deve essere selezionata la modalità utente) |
| 2 | 0<br />1 | Disabilitare l'accesso alla memoria condivisa/esterna<br />Abilitare l'accesso alla memoria condivisa/esterna |
| [23-3] | 0 | Riservato
| [31-24] | <br />0x00<br />0x01<br />0x02 | **ID compilatore**<br />Iar<br />ARM<br />Gnu |

#### <a name="module-linker-for-cortex-m33-using-iar"></a>Linker di modulo per Cortex-M33 con IAR

```c
/*###ICF### Section handled by ICF editor, don't touch! ****/
/*-Editor annotation file-*/
/* IcfEditorFile="$TOOLKIT_DIR$\config\ide\IcfEditor\a_v1_0.xml" */
/*-Specials-*/
define symbol __ICFEDIT_intvec_start__ = 0x0;
/*-Memory Regions-*/
define symbol __ICFEDIT_region_ROM_start__ = 0x080f0000;
define symbol __ICFEDIT_region_ROM_end__   = 0x080fffff;
define symbol __ICFEDIT_region_RAM_start__ = 0x64002800;
define symbol __ICFEDIT_region_RAM_end__   = 0x64100000;
/*-Sizes-*/
define symbol __ICFEDIT_size_cstack__   = 0;
define symbol __ICFEDIT_size_svcstack__ = 0;
define symbol __ICFEDIT_size_irqstack__ = 0;
define symbol __ICFEDIT_size_fiqstack__ = 0;
define symbol __ICFEDIT_size_undstack__ = 0;
define symbol __ICFEDIT_size_abtstack__ = 0;
define symbol __ICFEDIT_size_heap__     = 0x1000;
/**** End of ICF editor section. ###ICF###*/

define memory mem with size = 4G;
define region ROM_region   = mem:[from __ICFEDIT_region_ROM_start__   to __ICFEDIT_region_ROM_end__];
define region RAM_region   = mem:[from __ICFEDIT_region_RAM_start__   to __ICFEDIT_region_RAM_end__];

//define block CSTACK    with alignment = 8, size = __ICFEDIT_size_cstack__   { };
//define block SVC_STACK with alignment = 8, size = __ICFEDIT_size_svcstack__ { };
//define block IRQ_STACK with alignment = 8, size = __ICFEDIT_size_irqstack__ { };
//define block FIQ_STACK with alignment = 8, size = __ICFEDIT_size_fiqstack__ { };
//define block UND_STACK with alignment = 8, size = __ICFEDIT_size_undstack__ { };
//define block ABT_STACK with alignment = 8, size = __ICFEDIT_size_abtstack__ { };
define block HEAP      with alignment = 8, size = __ICFEDIT_size_heap__     { };

initialize by copy { readwrite };
do not initialize  { section .noinit };

//place at address mem:__ICFEDIT_intvec_start__ { readonly section .intvec };

define movable block ROPI with alignment = 4, fixed order 
{ 
  ro object txm_module_preamble.o,
  ro, 
  ro data 
};

define movable block RWPI with alignment = 8, fixed order, static base
{
  rw,
  block HEAP
};

place in ROM_region   { block ROPI };
place in RAM_region   { block RWPI };
```

#### <a name="building-modules-for-cortex-m33-using-iar"></a>Compilazione di moduli per Cortex-M33 con IAR

#### <a name="thread-extension-definition-for-cortex-m33-using-iar"></a>Definizione dell'estensione thread per Cortex-M33 con IAR

```c
#define TX_THREAD_EXTENSION_2                   VOID    *tx_thread_module_instance_ptr;         \
                                                VOID    *tx_thread_module_entry_info_ptr;       \
                                                ULONG   tx_thread_module_current_user_mode;     \
                                                ULONG   tx_thread_module_user_mode;             \
                                                ULONG   tx_thread_module_saved_lr;              \
                                                VOID    *tx_thread_module_kernel_stack_start;   \
                                                VOID    *tx_thread_module_kernel_stack_end;     \
                                                ULONG   tx_thread_module_kernel_stack_size;     \
                                                VOID    *tx_thread_module_stack_ptr;            \
                                                VOID    *tx_thread_module_stack_start;          \
                                                VOID    *tx_thread_module_stack_end;            \
                                                ULONG   tx_thread_module_stack_size;            \
                                                VOID    *tx_thread_module_reserved;             \
                                                VOID    *tx_thread_iar_tls_pointer;
```

#### <a name="building-module-manager-for-cortex-m33-using-iar"></a>Compilazione di Module Manager per Cortex-M33 con IAR

Non è ancora disponibile un'area di lavoro di esempio. Presto disponibile.

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m33-using-iar"></a>Attributi per l'API di abilitazione della memoria esterna per Cortex-M33 con IAR

| Parametro dell'attributo |
|---|
| TXM_MODULE_ATTRIBUTE_NON_SHAREABLE |
| TXM_MODULE_ATTRIBUTE_OUTER_SHAREABLE |
| TXM_MODULE_ATTRIBUTE_INNER_SHAREABLE |
| TXM_MODULE_ATTRIBUTE_READ_WRITE |
| TXM_MODULE_ATTRIBUTE_READ_ONLY |

## <a name="cortex-m4-processor"></a>Processore Cortex-M4

### <a name="cortex-m4-using-ac5"></a>Cortex-M4 con AC5

#### <a name="module-preamble-for-cortex-m4-using-ac5"></a>Preambolo del modulo per Cortex-M4 con AC5

```armasm
    AREA Init, CODE, READONLY

    PRESERVE8

    /* Define public symbols.  */

    EXPORT __txm_module_preamble

    ; Define application-specific start/stop entry points for the module

    EXTERN demo_module_start

    /* Define common external references.  */

    IMPORT  _txm_module_thread_shell_entry
    IMPORT  _txm_module_callback_request_thread_entry
    IMPORT  |Image$$ER_RO$$Length|
    IMPORT  |Image$$ER_RW$$Length|
    IMPORT  |Image$$ER_RW$$RW$$Length|
    IMPORT  |Image$$ER_RW$$ZI$$Length|
    IMPORT  |Image$$ER_ZI$$ZI$$Length|

__txm_module_preamble
    DCD     0x4D4F4455                                          // Module ID
    DCD     0x6                                                 // Module Major Version
    DCD     0x1                                                 // Module Minor Version
    DCD     32                                                  // Module Preamble Size in 32-bit words
    DCD     0x12345678                                          // Module ID (application defined)
    DCD     0x01000007                                          // Module Properties where:
                                                                //   Bits 31-24: Compiler ID
                                                                //           0 -> IAR
                                                                //           1 -> ARM
                                                                //           2 -> GNU
                                                                //   Bits 23-3: Reserved
                                                                //   Bit 2:  0 -> Disable shared/external memory access
                                                                //           1 -> Enable shared/external memory access
                                                                //   Bit 1:  0 -> No MPU protection
                                                                //           1 -> MPU protection (must have user mode selected)
                                                                //   Bit 0:  0 -> Privileged mode execution
                                                                //           1 -> User mode execution
    DCD     _txm_module_thread_shell_entry - __txm_module_preamble              // Module Shell Entry Point
    DCD     demo_module_start - __txm_module_preamble           // Module Start Thread Entry Point
    DCD     0                                                   // Module Stop Thread Entry Point
    DCD     1                                                   // Module Start/Stop Thread Priority
    DCD     1024                                                // Module Start/Stop Thread Stack Size
    DCD     _txm_module_callback_request_thread_entry - __txm_module_preamble   // Module Callback Thread Entry
    DCD     1                                                   // Module Callback Thread Priority
    DCD     1024                                                // Module Callback Thread Stack Size
    DCD     |Image$$ER_RO$$Length| + |Image$$ER_RW$$Length|     // Module Code Size
    DCD     |Image$$ER_RW$$Length| + |Image$$ER_ZI$$ZI$$Length| // Module Data Size
    DCD     0                                                   // Reserved 0
    DCD     0                                                   // Reserved 1
    DCD     0                                                   // Reserved 2
    DCD     0                                                   // Reserved 3
    DCD     0                                                   // Reserved 4
    DCD     0                                                   // Reserved 5
    DCD     0                                                   // Reserved 6
    DCD     0                                                   // Reserved 7
    DCD     0                                                   // Reserved 8
    DCD     0                                                   // Reserved 9
    DCD     0                                                   // Reserved 10
    DCD     0                                                   // Reserved 11
    DCD     0                                                   // Reserved 12
    DCD     0                                                   // Reserved 13
    DCD     0                                                   // Reserved 14
    DCD     0                                                   // Reserved 15

    END
```

#### <a name="module-properties-for-cortex-m4-using-ac5"></a>Proprietà del modulo per Cortex-M4 con AC5

| bit | Valore | Significato |
|---|---|---|
| 0 | 0<br />1 | Esecuzione in modalità privilegiata<br />Esecuzione in modalità utente |
| 1 | 0<br />1 | Nessuna protezione MPU<br />Protezione MPU (deve essere selezionata la modalità utente) |
| 2 | 0<br />1 | Disabilitare l'accesso alla memoria condivisa/esterna<br />Abilitare l'accesso alla memoria condivisa/esterna |
| [23-3] | 0 | Riservato
| [31-24] | <br />0x00<br />0x01<br />0x02 | **ID compilatore**<br />Iar<br />ARM<br />Gnu |

#### <a name="module-linker-for-cortex-m4-using-ac5"></a>Linker di modulo per Cortex-M4 con AC5

Non viene fornito alcun file del linker di esempio. Il collegamento viene eseguito nella riga di comando. Vedere la sezione successiva.

#### <a name="building-modules-for-cortex-m4-using-ac5"></a>Compilazione di moduli per Cortex-M4 con AC5

Vedere l'esempio build_threadx_module_demo.bat:

```dos
armasm -g --cpreproc --cpu=cortex-m4 --fpu=vfpv4 --apcs=/interwork/ropi/rwpi txm_module_preamble.S
armcc  -g --cpu=cortex-m4 --fpu=vfpv4 -c --apcs=/interwork/ropi/rwpi --lower_ropi -I../inc -I../../../../common_modules/inc -I../../../../common_modules/module_manager/inc -I../../../../common/inc sample_threadx_module.c
armlink -d -o sample_threadx_module.axf --elf --ro=0x30000 --rw=0x40000 --first txm_module_preamble.o(Init) --entry=_txm_module_thread_shell_entry --ropi --rwpi --remove --map --symbols --list sample_threadx_module.map txm_module_preamble.o sample_threadx_module.o txm.a
```

#### <a name="thread-extension-definition-for-cortex-m4-using-ac5"></a>Definizione dell'estensione thread per Cortex-M4 con AC5

```c
#define TX_THREAD_EXTENSION_2               VOID    *tx_thread_module_instance_ptr;         \
                                            VOID    *tx_thread_module_entry_info_ptr;       \
                                            ULONG   tx_thread_module_current_user_mode;     \
                                            ULONG   tx_thread_module_user_mode;             \
                                            ULONG   tx_thread_module_saved_lr;              \
                                            VOID    *tx_thread_module_kernel_stack_start;   \
                                            VOID    *tx_thread_module_kernel_stack_end;     \
                                            ULONG   tx_thread_module_kernel_stack_size;     \
                                            VOID    *tx_thread_module_stack_ptr;            \
                                            VOID    *tx_thread_module_stack_start;          \
                                            VOID    *tx_thread_module_stack_end;            \
                                            ULONG   tx_thread_module_stack_size;            \
                                            VOID    *tx_thread_module_reserved;
```

#### <a name="building-module-manager-for-cortex-m4-using-ac5"></a>Creazione di Module Manager per Cortex-M4 tramite AC5

Vedere l'esempio build_threadx_module_manager_demo.bat:

```dos
armasm -g --cpreproc --cpu=cortex-m4 --fpu=vfpv4 --apcs=/interwork tx_initialize_low_level.S
armcc -g --cpu=cortex-m4 --fpu=vfpv4 -c -I../inc -I../../../../common_modules/inc -I../../../../common_modules/module_manager/inc -I../../../../common/inc sample_threadx_module_manager.c
armlink -d -o sample_threadx_module_manager.axf --elf --ro 0x00000000 --first tx_initialize_low_level.o(RESET) --remove --map --symbols --list sample_threadx_module_manager.map tx_initialize_low_level.o sample_threadx_module_manager.o tx.a
```

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m4-using-ac5"></a>Attributi per l'API di abilitazione della memoria esterna per Cortex-M4 tramite AC5

Il modulo ha sempre accesso in lettura alla memoria condivisa.

| Parametro dell'attributo | Significato |
|---|---|
| TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE | Accesso in scrittura |

### <a name="cortex-m4-using-ac6"></a>Cortex-M4 con AC6

#### <a name="module-preamble-for-cortex-m4-using-ac6"></a>Preambolo del modulo per Cortex-M4 con AC6

```armasm
    .text
    .align 4
    .syntax unified
    .section Init
    
    // Define public symbols
    .global __txm_module_preamble

    // Define application-specific start/stop entry points for the module
    .global demo_module_start

    // Define common external references
    .global  _txm_module_thread_shell_entry
    .global  _txm_module_callback_request_thread_entry

    .eabi_attribute Tag_ABI_PCS_RO_data, 1
    .eabi_attribute Tag_ABI_PCS_R9_use,  1
    .eabi_attribute Tag_ABI_PCS_RW_data, 2

__txm_module_preamble:
    .dc.l   0x4D4F4455                                          // Module ID
    .dc.l   0x6                                                 // Module Major Version
    .dc.l   0x1                                                 // Module Minor Version
    .dc.l   32                                                  // Module Preamble Size in 32-bit words
    .dc.l   0x12345678                                          // Module ID (application defined)
    .dc.l   0x01000007                                          // Module Properties where:
                                                                //   Bits 31-24: Compiler ID
                                                                //           0 -> IAR
                                                                //           1 -> ARM
                                                                //           2 -> GNU
                                                                //   Bit 0:  0 -> Privileged mode execution
                                                                //           1 -> User mode execution
                                                                //   Bit 1:  0 -> No MPU protection
                                                                //           1 -> MPU protection (must have user mode selected)
                                                                //   Bit 2:  0 -> Disable shared/external memory access
                                                                //           1 -> Enable shared/external memory access
    .dc.l   _txm_module_thread_shell_entry - __txm_module_preamble // Module Shell Entry Point
    .dc.l   demo_module_start - __txm_module_preamble           // Module Start Thread Entry Point
    .dc.l   0                                                   // Module Stop Thread Entry Point
    .dc.l   1                                                   // Module Start/Stop Thread Priority
    .dc.l   1024                                                // Module Start/Stop Thread Stack Size
    .dc.l   _txm_module_callback_request_thread_entry - __txm_module_preamble // Module Callback Thread Entry
    .dc.l   1                                                   // Module Callback Thread Priority
    .dc.l   1024                                                // Module Callback Thread Stack Size
    .dc.l   0x10000                                             // Module Code Size
    .dc.l   0x10000                                             // Module Data Size
    .dc.l   0                                                   // Reserved 0
    .dc.l   0                                                   // Reserved 1
    .dc.l   0                                                   // Reserved 2
    .dc.l   0                                                   // Reserved 3
    .dc.l   0                                                   // Reserved 4
    .dc.l   0                                                   // Reserved 5
    .dc.l   0                                                   // Reserved 6
    .dc.l   0                                                   // Reserved 7
    .dc.l   0                                                   // Reserved 8
    .dc.l   0                                                   // Reserved 9
    .dc.l   0                                                   // Reserved 10
    .dc.l   0                                                   // Reserved 11
    .dc.l   0                                                   // Reserved 12
    .dc.l   0                                                   // Reserved 13
    .dc.l   0                                                   // Reserved 14
    .dc.l   0                                                   // Reserved 15
```

#### <a name="module-properties-for-cortex-m4-using-ac6"></a>Proprietà del modulo per Cortex-M4 tramite AC6

| bit | Valore | Significato |
|---|---|---|
| 0 | 0<br />1 | Esecuzione in modalità privilegiata<br />Esecuzione in modalità utente |
| 1 | 0<br />1 | Nessuna protezione MPU<br />Protezione MPU (deve essere selezionata la modalità utente) |
| 2 | 0<br />1 | Disabilitare l'accesso alla memoria condivisa/esterna<br />Abilitare l'accesso alla memoria condivisa/esterna |
| [23-3] | 0 | Riservato
| [31-24] | <br />0x00<br />0x01<br />0x02 | **ID compilatore**<br />Iar<br />ARM<br />Gnu |

#### <a name="module-linker-for-cortex-m4-using-ac6"></a>Linker di modulo per Cortex-M4 con AC6

Non viene usato alcun file del linker. Vedere le impostazioni del progetto.

#### <a name="building-modules-for-cortex-m4-using-ac6"></a>Compilazione di moduli per Cortex-M4 con AC6

Viene fornita un'area di lavoro di esempio. Compilare la libreria ThreadX, la libreria ThreadX Modules, il progetto di modulo di esempio e il progetto di gestione moduli di esempio.

#### <a name="thread-extension-definition-for-cortex-m4-using-ac6"></a>Definizione dell'estensione thread per Cortex-M4 tramite AC6

```c
#define TX_THREAD_EXTENSION_2               VOID    *tx_thread_module_instance_ptr;         \
                                            VOID    *tx_thread_module_entry_info_ptr;       \
                                            ULONG   tx_thread_module_current_user_mode;     \
                                            ULONG   tx_thread_module_user_mode;             \
                                            ULONG   tx_thread_module_saved_lr;              \
                                            VOID    *tx_thread_module_kernel_stack_start;   \
                                            VOID    *tx_thread_module_kernel_stack_end;     \
                                            ULONG   tx_thread_module_kernel_stack_size;     \
                                            VOID    *tx_thread_module_stack_ptr;            \
                                            VOID    *tx_thread_module_stack_start;          \
                                            VOID    *tx_thread_module_stack_end;            \
                                            ULONG   tx_thread_module_stack_size;            \
                                            VOID    *tx_thread_module_reserved;
```

#### <a name="building-module-manager-for-cortex-m4-using-ac6"></a>Creazione di Module Manager per Cortex-M4 tramite AC6

Viene fornita un'area di lavoro di esempio. Compilare la libreria ThreadX, la libreria ThreadX Modules, il progetto di modulo di esempio e il progetto di gestione moduli di esempio.

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m4-using-ac6"></a>Attributi per l'API di abilitazione della memoria esterna per Cortex-M4 tramite AC6

Il modulo ha sempre accesso in lettura alla memoria condivisa.

| Parametro dell'attributo | Significato |
|---|---|
| TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE | Accesso in scrittura |

### <a name="cortex-m4-using-gnu"></a>Cortex-M4 con GNU

#### <a name="module-preamble-for-cortex-m4-using-gnu"></a>Preambolo del modulo per Cortex-M4 con GNU

```armasm
    .text
    .align 4
    .syntax unified

    /* Define public symbols.  */
    .global __txm_module_preamble

    /* Define application-specific start/stop entry points for the module.  */
    .global demo_module_start

    /* Define common external refrences.  */
    .global _txm_module_thread_shell_entry
    .global _txm_module_callback_request_thread_entry

__txm_module_preamble:
    .dc.l      0x4D4F4455                                       // Module ID
    .dc.l      0x6                                              // Module Major Version
    .dc.l      0x1                                              // Module Minor Version
    .dc.l      32                                               // Module Preamble Size in 32-bit words
    .dc.l      0x12345678                                       // Module ID (application defined)
    .dc.l      0x02000007                                       // Module Properties where:
                                                                //   Bits 31-24: Compiler ID
                                                                //           0 -> IAR
                                                                //           1 -> ARM
                                                                //           2 -> GNU
                                                                //   Bits 23-3: Reserved
                                                                //   Bit 2:  0 -> Disable shared/external memory access
                                                                //           1 -> Enable shared/external memory access
                                                                //   Bit 1:  0 -> No MPU protection
                                                                //           1 -> MPU protection (must have user mode selected - bit 0 set)
                                                                //   Bit 0:  0 -> Privileged mode execution
                                                                //           1 -> User mode execution
    .dc.l      _txm_module_thread_shell_entry - . - 0           // Module Shell Entry Point
    .dc.l      demo_module_start - . - 0                        // Module Start Thread Entry Point
    .dc.l      0                                                // Module Stop Thread Entry Point 
    .dc.l      1                                                // Module Start/Stop Thread Priority
    .dc.l      1024                                             // Module Start/Stop Thread Stack Size
    .dc.l      _txm_module_callback_request_thread_entry - . - 0 // Module Callback Thread Entry
    .dc.l      1                                                // Module Callback Thread Priority
    .dc.l      1024                                             // Module Callback Thread Stack Size
    .dc.l      __code_size__                                    // Module Code Size
    .dc.l      __data_size__                                    // Module Data Size
    .dc.l      0                                                // Reserved 0
    .dc.l      0                                                // Reserved 1
    .dc.l      0                                                // Reserved 2
    .dc.l      0                                                // Reserved 3
    .dc.l      0                                                // Reserved 4
    .dc.l      0                                                // Reserved 5
    .dc.l      0                                                // Reserved 6
    .dc.l      0                                                // Reserved 7
    .dc.l      0                                                // Reserved 8
    .dc.l      0                                                // Reserved 9
    .dc.l      0                                                // Reserved 10
    .dc.l      0                                                // Reserved 11
    .dc.l      0                                                // Reserved 12
    .dc.l      0                                                // Reserved 13
    .dc.l      0                                                // Reserved 14
    .dc.l      0                                                // Reserved 15
```

#### <a name="module-properties-for-cortex-m4-using-gnu"></a>Proprietà del modulo per Cortex-M4 con GNU

| bit | Valore | Significato |
|---|---|---|
| 0 | 0<br />1 | Esecuzione in modalità privilegiata<br />Esecuzione in modalità utente |
| 1 | 0<br />1 | Nessuna protezione MPU<br />Protezione MPU (deve essere selezionata la modalità utente) |
| 2 | 0<br />1 | Disabilitare l'accesso alla memoria condivisa/esterna<br />Abilitare l'accesso alla memoria condivisa/esterna |
| [23-3] | 0 | Riservato
| [31-24] | <br />0x00<br />0x01<br />0x02 | **ID compilatore**<br />Iar<br />ARM<br />Gnu |

#### <a name="module-linker-for-cortex-m4-using-gnu"></a>Linker di modulo per Cortex-M4 con GNU

```c
MEMORY
{
  FLASH (rx) : ORIGIN = 0x00030000, LENGTH = 0x00010000
  RAM   (wx) : ORIGIN = 0, LENGTH = 0x00100000
}


SECTIONS
{
  __FLASH_segment_start__ = 0x00030000;
  __FLASH_segment_end__   = 0x00040000;
  __RAM_segment_start__   = 0;
  __RAM_segment_end__     = 0x8000;

  __HEAPSIZE__ = 128;

  __preamble_load_start__ = __FLASH_segment_start__;
  .preamble __FLASH_segment_start__ : AT(__FLASH_segment_start__)
  {
    __preamble_start__ = .;
    *(.preamble .preamble.*)
  }
  __preamble_end__ = __preamble_start__ + SIZEOF(.preamble);

  __dynsym_load_start__ =  ALIGN(__preamble_end__ , 4);
  .dynsym ALIGN(__dynsym_load_start__ , 4) : AT(ALIGN(__dynsym_load_start__ , 4))
  {
    . = ALIGN(4);
    KEEP (*(.dynsym))
    KEEP (*(.dynsym*))
    . = ALIGN(4);
  }
  __dynsym_end__ = __dynsym_load_start__ + SIZEOF(.dynsym);

  __dynstr_load_start__ =  ALIGN(__dynsym_end__ , 4);
  .dynstr ALIGN(__dynstr_load_start__ , 4) : AT(ALIGN(__dynstr_load_start__, 4))
  {
    . = ALIGN(4);
    KEEP (*(.dynstr))
    KEEP (*(.dynstr*))
    . = ALIGN(4);
  }
  __dynstr_end__ = __dynstr_load_start__ + SIZEOF(.dynstr);

  __reldyn_load_start__ =  ALIGN(__dynstr_end__ , 4);
  .rel.dyn ALIGN(__reldyn_load_start__ , 4) : AT(ALIGN(__reldyn_load_start__ , 4))
  {
    . = ALIGN(4);
    KEEP (*(.rel.dyn))
    KEEP (*(.rel.dyn*))
    . = ALIGN(4);
  }
  __reldyn_end__ = __reldyn_load_start__ + SIZEOF(.rel.dyn);

  __relplt_load_start__ =  ALIGN(__reldyn_end__ , 4);
  .rel.plt ALIGN(__relplt_load_start__ , 4) : AT(ALIGN(__relplt_load_start__ , 4))
  {
    . = ALIGN(4);
    KEEP (*(.rel.plt))
    KEEP (*(.rel.plt*))
    . = ALIGN(4);
  }
  __relplt_end__ = __relplt_load_start__ + SIZEOF(.rel.plt);

  __plt_load_start__ =  ALIGN(__relplt_end__ , 4);
  .plt ALIGN(__plt_load_start__ , 4) : AT(ALIGN(__plt_load_start__ , 4))
  {
    . = ALIGN(4);
    KEEP (*(.plt))
    KEEP (*(.plt*))
    . = ALIGN(4);
  }
  __plt_end__ = __plt_load_start__ + SIZEOF(.plt);

  __interp_load_start__ =  ALIGN(__plt_end__ , 4);
  .interp ALIGN(__interp_load_start__ , 4) : AT(ALIGN(__interp_load_start__ , 4))
  {
    . = ALIGN(4);
    KEEP (*(.interp))
    KEEP (*(.interp*))
    . = ALIGN(4);
  }
  __interp_end__ = __interp_load_start__ + SIZEOF(.interp);

  __hash_load_start__ =  ALIGN(__interp_end__ , 4);
  .hash ALIGN(__hash_load_start__ , 4) : AT(ALIGN(__hash_load_start__, 4))
  {
    . = ALIGN(4);
    KEEP (*(.hash))
    KEEP (*(.hash*))
    . = ALIGN(4);
  }
  __hash_end__ = __hash_load_start__ + SIZEOF(.hash);

  __text_load_start__ =  ALIGN(__hash_end__ , 4);
  .text ALIGN(__text_load_start__ , 4) : AT(ALIGN(__text_load_start__, 4))
  {
    __text_start__ = .;
    *(.text .text.* .glue_7t .glue_7 .gnu.linkonce.t.* .gcc_except_table  )
  }
  __text_end__ = __text_start__ + SIZEOF(.text);

  __dtors_load_start__ = ALIGN(__text_end__ , 4);
  .dtors ALIGN(__text_end__ , 4) : AT(ALIGN(__text_end__ , 4))
  {
    __dtors_start__ = .;
    KEEP (*(SORT(.dtors.*))) KEEP (*(.dtors))
  }
  __dtors_end__ = __dtors_start__ + SIZEOF(.dtors);

  __ctors_load_start__ = ALIGN(__dtors_end__ , 4);
  .ctors ALIGN(__dtors_end__ , 4) : AT(ALIGN(__dtors_end__ , 4))
  {
    __ctors_start__ = .;
    KEEP (*(SORT(.ctors.*))) KEEP (*(.ctors))
  }
  __ctors_end__ = __ctors_start__ + SIZEOF(.ctors);

  __got_load_start__ = ALIGN(__ctors_end__ , 4);
  .got ALIGN(__ctors_end__ , 4) : AT(ALIGN(__ctors_end__ , 4))
  {
    . = ALIGN(4);
    _sgot = .;
    KEEP (*(.got))
    KEEP (*(.got*))
    . = ALIGN(4);
    _egot = .;
  } 
  __got_end__ =  __got_load_start__ + SIZEOF(.got);

  __rodata_load_start__ = ALIGN(__got_end__ , 4);
  .rodata ALIGN(__got_end__ , 4) : AT(ALIGN(__got_end__ , 4))
  {
    __rodata_start__ = .;
    *(.rodata .rodata.* .gnu.linkonce.r.*)
  }
  __rodata_end__ = __rodata_start__ + SIZEOF(.rodata);
 
  __code_size__ =  __rodata_end__ - __FLASH_segment_start__;

  __fast_load_start__ = ALIGN(__rodata_end__ , 4);

  __fast_load_end__ = __fast_load_start__ + SIZEOF(.fast);

  __new_got_start__ = ALIGN(__RAM_segment_start__ , 4);

  __new_got_end__ =  __new_got_start__ + SIZEOF(.got);

  .fast ALIGN(__new_got_end__ , 4) : AT(ALIGN(__rodata_end__ , 4))
  {
    __fast_start__ = .;
    *(.fast .fast.*)
  }
  __fast_end__ = __fast_start__ + SIZEOF(.fast);

  .fast_run ALIGN(__fast_end__ , 4) (NOLOAD) :
  {
    __fast_run_start__ = .;
    . = MAX(__fast_run_start__ + SIZEOF(.fast), .);
  }
  __fast_run_end__ = __fast_run_start__ + SIZEOF(.fast_run);

  __data_load_start__ = ALIGN(__fast_load_start__ + SIZEOF(.fast) , 4);
  .data ALIGN(__fast_run_end__ , 4) : AT(ALIGN(__fast_load_start__ + SIZEOF(.fast) , 4))
  {
    __data_start__ = .;
    *(.data .data.* .gnu.linkonce.d.*)
  }
  __data_end__ = __data_start__ + SIZEOF(.data);

  __data_load_end__ = __data_load_start__ + SIZEOF(.data);

  __FLASH_segment_used_end__ = ALIGN(__fast_load_start__ + SIZEOF(.fast) , 4) + SIZEOF(.data);

  .data_run ALIGN(__fast_run_end__ , 4) (NOLOAD) :
  {
    __data_run_start__ = .;
    . = MAX(__data_run_start__ + SIZEOF(.data), .);
  }
  __data_run_end__ = __data_run_start__ + SIZEOF(.data_run);

  __bss_load_start__ = ALIGN(__data_run_end__ , 4);
  .bss ALIGN(__data_run_end__ , 4) (NOLOAD) : AT(ALIGN(__data_run_end__ , 4))
  {
    __bss_start__ = .;
    *(.bss .bss.* .gnu.linkonce.b.*) *(COMMON)
  }
  __bss_end__ = __bss_start__ + SIZEOF(.bss);

  __non_init_load_start__ = ALIGN(__bss_end__ , 4);
  .non_init ALIGN(__bss_end__ , 4) (NOLOAD) : AT(ALIGN(__bss_end__ , 4))
  {
    __non_init_start__ = .;
    *(.non_init .non_init.*)
  }
  __non_init_end__ = __non_init_start__ + SIZEOF(.non_init);

  __heap_load_start__ = ALIGN(__non_init_end__ , 4);
  .heap ALIGN(__non_init_end__ , 4) (NOLOAD) : AT(ALIGN(__non_init_end__ , 4))
  {
    __heap_start__ = .;
    *(.heap)
    . = ALIGN(MAX(__heap_start__ + __HEAPSIZE__ , .), 4);
  }
  __heap_end__ = __heap_start__ + SIZEOF(.heap);

  __data_size__ =  __heap_end__ - __RAM_segment_start__;

}
```

#### <a name="building-modules-for-cortex-m4-using-gnu"></a>Compilazione di moduli per Cortex-M4 con GNU

Vedere build_threadx_module_sample.bat:

```dos
arm-none-eabi-gcc -c -g -mcpu=cortex-m4 -mfloat-abi=hard -mfpu=vfpv4 -fpie -fno-plt -mpic-data-is-text-relative -msingle-pic-base txm_module_preamble.s
arm-none-eabi-gcc -c -g -mcpu=cortex-m4 -mfloat-abi=hard -mfpu=vfpv4 -fpie -fno-plt -mpic-data-is-text-relative -msingle-pic-base gcc_setup.S
arm-none-eabi-gcc -c -g -mcpu=cortex-m4 -mfloat-abi=hard -mfpu=vfpv4 -fpie -fno-plt -mpic-data-is-text-relative -msingle-pic-base -I..\inc -I..\..\..\..\common\inc -I..\..\..\..\common_modules\inc sample_threadx_module.c
arm-none-eabi-ld -A cortex-m4 -T sample_threadx_module.ld txm_module_preamble.o gcc_setup.o sample_threadx_module.o -e _txm_module_thread_shell_entry txm.a -o sample_threadx_module.axf -M > sample_threadx_module.map
```

#### <a name="thread-extension-definition-for-cortex-m4-using-gnu"></a>Definizione dell'estensione thread per Cortex-M4 tramite GNU

```c
#define TX_THREAD_EXTENSION_2               VOID    *tx_thread_module_instance_ptr;         \
                                            VOID    *tx_thread_module_entry_info_ptr;       \
                                            ULONG   tx_thread_module_current_user_mode;     \
                                            ULONG   tx_thread_module_user_mode;             \
                                            ULONG   tx_thread_module_saved_lr;              \
                                            VOID    *tx_thread_module_kernel_stack_start;   \
                                            VOID    *tx_thread_module_kernel_stack_end;     \
                                            ULONG   tx_thread_module_kernel_stack_size;     \
                                            VOID    *tx_thread_module_stack_ptr;            \
                                            VOID    *tx_thread_module_stack_start;          \
                                            VOID    *tx_thread_module_stack_end;            \
                                            ULONG   tx_thread_module_stack_size;            \
                                            VOID    *tx_thread_module_reserved;
```

#### <a name="building-module-manager-for-cortex-m4-using-gnu"></a>Compilazione di Module Manager per Cortex-M4 con GNU

Vedere build_threadx_module_manager_sample.bat:

```dos
arm-none-eabi-gcc -c -g -mcpu=cortex-m4 -mfloat-abi=hard -mfpu=vfpv4 -mthumb cortexm_vectors.S
arm-none-eabi-gcc -c -g -mcpu=cortex-m4 -mfloat-abi=hard -mfpu=vfpv4 -mthumb cortexm_crt0.S
arm-none-eabi-gcc -c -g -mcpu=cortex-m4 -mfloat-abi=hard -mfpu=vfpv4 -mthumb tx_initialize_low_level.S
arm-none-eabi-gcc -c -g -mcpu=cortex-m4 -mfloat-abi=hard -mfpu=vfpv4 -mthumb -I..\inc -I..\..\..\..\common\inc -I..\..\..\..\common_modules\inc sample_threadx_module_manager.c
arm-none-eabi-gcc -g -mcpu=cortex-m4 -mfloat-abi=hard -mfpu=vfpv4 -mthumb -T sample_threadx.ld -ereset_handler -nostartfiles -o sample_threadx_module_manager.out -Wl,-Map=sample_threadx_module_manager.map cortexm_vectors.o cortexm_crt0.o tx_initialize_low_level.o sample_threadx_module_manager.o tx.a
```

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m4-using-gnu"></a>Attributi per l'API di abilitazione della memoria esterna per Cortex-M4 tramite GNU

Il modulo ha sempre accesso in lettura alla memoria condivisa.

| Parametro dell'attributo | Significato |
|---|---|
| TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE | Accesso in scrittura |

### <a name="cortex-m4-using-iar"></a>Cortex-M4 con IAR

#### <a name="module-preamble-for-cortex-m4-using-iar"></a>Preambolo del modulo per Cortex-M4 con IAR

```c
    SECTION .text:CODE

    AAPCS INTERWORK, ROPI, RWPI_COMPATIBLE,  VFP_COMPATIBLE
    PRESERVE8

    /* Define public symbols.  */

    PUBLIC __txm_module_preamble


    /* Define application-specific start/stop entry points for the module.  */

    EXTERN demo_module_start


    /* Define common external references.  */

    EXTERN  _txm_module_thread_shell_entry
    EXTERN  _txm_module_callback_request_thread_entry
    EXTERN  ROPI$$Length
    EXTERN  RWPI$$Length

    DATA
__txm_module_preamble:
    DC32      0x4D4F4455                                        ; Module ID
    DC32      0x5                                               ; Module Major Version
    DC32      0x6                                               ; Module Minor Version
    DC32      32                                                ; Module Preamble Size in 32-bit words
    DC32      0x12345678                                        ; Module ID (application defined)
    DC32      0x00000007                                        ; Module Properties where:
                                                                ;   Bits 31-24: Compiler ID
                                                                ;           0 -> IAR
                                                                ;           1 -> ARM
                                                                ;           2 -> GNU
                                                                ;   Bits 23-3: Reserved
                                                                ;   Bit 2:  0 -> Disable shared/external memory access
                                                                ;           1 -> Enable shared/external memory access
                                                                ;   Bit 1:  0 -> No MPU protection
                                                                ;           1 -> MPU protection (must have user mode selected - bit 0 set)
                                                                ;   Bit 0:  0 -> Privileged mode execution
                                                                ;           1 -> User mode execution


    DC32      _txm_module_thread_shell_entry - . - 0            ; Module Shell Entry Point
    DC32      demo_module_start - . - 0                         ; Module Start Thread Entry Point
    DC32      0                                                 ; Module Stop Thread Entry Point
    DC32      1                                                 ; Module Start/Stop Thread Priority
    DC32      1024                                              ; Module Start/Stop Thread Stack Size
    DC32      _txm_module_callback_request_thread_entry - . - 0 ; Module Callback Thread Entry
    DC32      1                                                 ; Module Callback Thread Priority
    DC32      1024                                              ; Module Callback Thread Stack Size
    DC32      ROPI$$Length                                      ; Module Code Size
    DC32      RWPI$$Length                                      ; Module Data Size
    DC32      0                                                 ; Reserved 0
    DC32      0                                                 ; Reserved 1
    DC32      0                                                 ; Reserved 2
    DC32      0                                                 ; Reserved 3
    DC32      0                                                 ; Reserved 4
    DC32      0                                                 ; Reserved 5
    DC32      0                                                 ; Reserved 6
    DC32      0                                                 ; Reserved 7
    DC32      0                                                 ; Reserved 8  
    DC32      0                                                 ; Reserved 9
    DC32      0                                                 ; Reserved 10
    DC32      0                                                 ; Reserved 11
    DC32      0                                                 ; Reserved 12
    DC32      0                                                 ; Reserved 13
    DC32      0                                                 ; Reserved 14
    DC32      0                                                 ; Reserved 15

    END
```

#### <a name="module-properties-for-cortex-m4-using-iar"></a>Proprietà del modulo per Cortex-M4 con IAR

| bit | Valore | Significato |
|---|---|---|
| 0 | 0<br />1 | Esecuzione in modalità privilegiata<br />Esecuzione in modalità utente |
| 1 | 0<br />1 | Nessuna protezione MPU<br />Protezione MPU (deve essere selezionata la modalità utente) |
| 2 | 0<br />1 | Disabilitare l'accesso alla memoria condivisa/esterna<br />Abilitare l'accesso alla memoria condivisa/esterna |
| [23-3] | 0 | Riservato
| [31-24] | <br />0x00<br />0x01<br />0x02 | **ID compilatore**<br />Iar<br />ARM<br />Gnu |

#### <a name="module-linker-for-cortex-m4-using-iar"></a>Linker di modulo per Cortex-M4 con IAR

```c
/*###ICF### Section handled by ICF editor, don't touch! ****/
/*-Editor annotation file-*/
/* IcfEditorFile="$TOOLKIT_DIR$\config\ide\IcfEditor\a_v1_0.xml" */
/*-Specials-*/
define symbol __ICFEDIT_intvec_start__ = 0x0;
/*-Memory Regions-*/
define symbol __ICFEDIT_region_ROM_start__ = 0x080f0000;
define symbol __ICFEDIT_region_ROM_end__   = 0x080fffff;
define symbol __ICFEDIT_region_RAM_start__ = 0x64002800;
define symbol __ICFEDIT_region_RAM_end__   = 0x64100000;
/*-Sizes-*/
define symbol __ICFEDIT_size_cstack__   = 0;
define symbol __ICFEDIT_size_svcstack__ = 0;
define symbol __ICFEDIT_size_irqstack__ = 0;
define symbol __ICFEDIT_size_fiqstack__ = 0;
define symbol __ICFEDIT_size_undstack__ = 0;
define symbol __ICFEDIT_size_abtstack__ = 0;
define symbol __ICFEDIT_size_heap__     = 0x1000;
/**** End of ICF editor section. ###ICF###*/

define memory mem with size = 4G;
define region ROM_region   = mem:[from __ICFEDIT_region_ROM_start__   to __ICFEDIT_region_ROM_end__];
define region RAM_region   = mem:[from __ICFEDIT_region_RAM_start__   to __ICFEDIT_region_RAM_end__];

//define block CSTACK    with alignment = 8, size = __ICFEDIT_size_cstack__   { };
//define block SVC_STACK with alignment = 8, size = __ICFEDIT_size_svcstack__ { };
//define block IRQ_STACK with alignment = 8, size = __ICFEDIT_size_irqstack__ { };
//define block FIQ_STACK with alignment = 8, size = __ICFEDIT_size_fiqstack__ { };
//define block UND_STACK with alignment = 8, size = __ICFEDIT_size_undstack__ { };
//define block ABT_STACK with alignment = 8, size = __ICFEDIT_size_abtstack__ { };
define block HEAP      with alignment = 8, size = __ICFEDIT_size_heap__     { };

initialize by copy { readwrite };
do not initialize  { section .noinit };

//place at address mem:__ICFEDIT_intvec_start__ { readonly section .intvec };

define movable block ROPI with alignment = 4, fixed order
{
  ro object txm_module_preamble_stm32f4xx.o,
  ro,
  ro data
};

define movable block RWPI with alignment = 8, fixed order, static base
{
  rw,
  block HEAP
};

place in ROM_region   { block ROPI };
place in RAM_region   { block RWPI };
```

#### <a name="building-modules-for-cortex-m4-using-iar"></a>Compilazione di moduli per Cortex-M4 con IAR

Viene fornita un'area di lavoro di esempio. Compilare la libreria ThreadX, la libreria ThreadX Modules, il progetto di modulo demo e il progetto demo module manager.

#### <a name="thread-extension-definition-for-cortex-m4-using-iar"></a>Definizione dell'estensione thread per Cortex-M4 con IAR

```c
#define TX_THREAD_EXTENSION_2   VOID    *tx_thread_module_instance_ptr;         \
                                VOID    *tx_thread_module_entry_info_ptr;       \
                                ULONG   tx_thread_module_current_user_mode;     \
                                ULONG   tx_thread_module_user_mode;             \
                                ULONG   tx_thread_module_saved_lr;              \
                                VOID    *tx_thread_module_kernel_stack_start;   \
                                VOID    *tx_thread_module_kernel_stack_end;     \
                                ULONG   tx_thread_module_kernel_stack_size;     \
                                VOID    *tx_thread_module_stack_ptr;            \
                                VOID    *tx_thread_module_stack_start;          \
                                VOID    *tx_thread_module_stack_end;            \
                                ULONG   tx_thread_module_stack_size;            \
                                VOID    *tx_thread_module_reserved;             \
                                VOID    *tx_thread_iar_tls_pointer;
```

#### <a name="building-module-manager-for-cortex-m4-using-iar"></a>Compilazione di Module Manager per Cortex-M4 con IAR

Viene fornita un'area di lavoro di esempio. Compilare la libreria ThreadX, la libreria dei moduli ThreadX, il progetto di modulo demo e il progetto demo module manager.

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m4-using-iar"></a>Attributi per l'API di abilitazione della memoria esterna per Cortex-M4 con IAR

Il modulo ha sempre accesso in lettura alla memoria condivisa.

| Parametro attribute | Significato |
|---|---|
| TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE | Accesso in scrittura |

## <a name="cortex-m7-processor"></a>Processore Cortex-M7

### <a name="cortex-m7-using-ac5"></a>Cortex-M7 con AC5

#### <a name="module-preamble-for-cortex-m7-using-ac5"></a>Preambolo del modulo per Cortex-M7 con AC5

```c
    AREA Init, CODE, READONLY

    PRESERVE8

    ; Define public symbols

    EXPORT __txm_module_preamble


    ; Define application-specific start/stop entry points for the module

    EXTERN demo_module_start


    ; Define common external references

    IMPORT  _txm_module_thread_shell_entry
    IMPORT  _txm_module_callback_request_thread_entry
    IMPORT  |Image$$ER_RO$$Length|
    IMPORT  |Image$$ER_RW$$Length|
    IMPORT  |Image$$ER_RW$$RW$$Length|
    IMPORT  |Image$$ER_RW$$ZI$$Length|
    IMPORT  |Image$$ER_ZI$$ZI$$Length|

__txm_module_preamble
    DCD     0x4D4F4455                                          ; Module ID
    DCD     0x5                                                 ; Module Major Version
    DCD     0x6                                                 ; Module Minor Version
    DCD     32                                                  ; Module Preamble Size in 32-bit words
    DCD     0x12345678                                          ; Module ID (application defined)
    DCD     0x01000007                                          ; Module Properties where:
                                                                ;   Bits 31-24: Compiler ID
                                                                ;           0 -> IAR
                                                                ;           1 -> ARM
                                                                ;           2 -> GNU
                                                                ;   Bit 0:  0 -> Privileged mode execution
                                                                ;           1 -> User mode execution
                                                                ;   Bit 1:  0 -> No MPU protection
                                                                ;           1 -> MPU protection (must have user mode selected)
                                                                ;   Bit 2:  0 -> Disable shared/external memory access
                                                                ;           1 -> Enable shared/external memory access
    DCD     _txm_module_thread_shell_entry - __txm_module_preamble              ; Module Shell Entry Point
    DCD     demo_module_start - __txm_module_preamble           ; Module Start Thread Entry Point
    DCD     0                                                   ; Module Stop Thread Entry Point
    DCD     1                                                   ; Module Start/Stop Thread Priority
    DCD     1024                                                ; Module Start/Stop Thread Stack Size
    DCD     _txm_module_callback_request_thread_entry - __txm_module_preamble   ; Module Callback Thread Entry
    DCD     1                                                   ; Module Callback Thread Priority
    DCD     1024                                                ; Module Callback Thread Stack Size
    DCD     |Image$$ER_RO$$Length| + |Image$$ER_RW$$Length|         ; Module Code Size
    DCD     |Image$$ER_RW$$Length| + |Image$$ER_ZI$$ZI$$Length| ; Module Data Size
    DCD     0                                                   ; Reserved 0
    DCD     0                                                   ; Reserved 1
    DCD     0                                                   ; Reserved 2
    DCD     0                                                   ; Reserved 3
    DCD     0                                                   ; Reserved 4
    DCD     0                                                   ; Reserved 5
    DCD     0                                                   ; Reserved 6
    DCD     0                                                   ; Reserved 7
    DCD     0                                                   ; Reserved 8
    DCD     0                                                   ; Reserved 9
    DCD     0                                                   ; Reserved 10
    DCD     0                                                   ; Reserved 11
    DCD     0                                                   ; Reserved 12
    DCD     0                                                   ; Reserved 13
    DCD     0                                                   ; Reserved 14
    DCD     0                                                   ; Reserved 15

    END
```

#### <a name="module-properties-for-cortex-m7-using-ac5"></a>Proprietà del modulo per Cortex-M7 con AC5

| bit | Valore | Significato |
|---|---|---|
| 0 | 0<br />1 | Esecuzione in modalità privilegiata<br />Esecuzione in modalità utente |
| 1 | 0<br />1 | Nessuna protezione MPU<br />Protezione MPU (deve essere selezionata la modalità utente) |
| 2 | 0<br />1 | Disabilitare l'accesso alla memoria condivisa/esterna<br />Abilitare l'accesso alla memoria condivisa/esterna |
| [23-3] | 0 | Riservato
| [31-24] | <br />0x00<br />0x01<br />0x02 | **ID compilatore**<br />Iar<br />ARM<br />Gnu |

#### <a name="module-linker-for-cortex-m7-using-ac5"></a>Linker di modulo per Cortex-M7 con AC5

Compilato dalla riga di comando, nessun esempio di file del linker.

#### <a name="building-modules-for-cortex-m7-using-ac5"></a>Compilazione di moduli per Cortex-M7 con AC5

Un semplice esempio di riga di comando per la creazione di un modulo Cortex-M7 con AC5:

```dos
armasm -g --cpu=cortex-m7 --fpu=softvfp --apcs=/interwork/ropi/rwpi txm_module_preamble.s
armcc  -g --cpu=cortex-m7 --fpu=softvfp -c --apcs=/interwork/ropi/rwpi --lower_ropi -I../inc -I../../../../common_modules/inc -I../../../../common_modules/module_manager/inc -I../../../../common/inc sample_threadx_module.c
armlink -d -o sample_threadx_module.axf --elf --ro 0 --first txm_module_preamble.o(Init) --entry=_txm_module_thread_shell_entry --ropi --rwpi --remove --map --symbols --list sample_threadx_module.map txm_module_preamble.o sample_threadx_module.o txm.a
```

#### <a name="thread-extension-definition-for-cortex-m7-using-ac5"></a>Definizione dell'estensione thread per Cortex-M7 con AC5

```c
#define TX_THREAD_EXTENSION_2   VOID    *tx_thread_module_instance_ptr;         \
                                VOID    *tx_thread_module_entry_info_ptr;       \
                                ULONG   tx_thread_module_current_user_mode;     \
                                ULONG   tx_thread_module_user_mode;             \
                                ULONG   tx_thread_module_saved_lr;              \
                                VOID    *tx_thread_module_kernel_stack_start;   \
                                VOID    *tx_thread_module_kernel_stack_end;     \
                                ULONG   tx_thread_module_kernel_stack_size;     \
                                VOID    *tx_thread_module_stack_ptr;            \
                                VOID    *tx_thread_module_stack_start;          \
                                VOID    *tx_thread_module_stack_end;            \
                                ULONG   tx_thread_module_stack_size;            \
                                VOID    *tx_thread_module_reserved;
```

#### <a name="building-module-manager-for-cortex-m7-using-ac5"></a>Building Module Manager for Cortex-M7 using AC5

Un semplice esempio di riga di comando per la creazione di un modulo di gestione Cortex-M7 con AC5:

```dos
armasm -g --cpu=cortex-m7 --fpu=softvfp --apcs=interwork tx_initialize_low_level.s
armcc -g --cpu=cortex-m7 --fpu=softvfp -c demo_threadx_module_manager.c
armcc -g --cpu=cortex-m7 --fpu=softvfp -c module_code.c
armlink -d -o demo_threadx_module_manager.axf --elf --ro 0x00000000 --first tx_initialize_low_level.o(RESET) --remove --map --symbols --list demo_threadx_module_manager.map tx_initialize_low_level.o demo_threadx_module_manager.o module_code.o tx.a
```

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m7-using-ac5"></a>Attributi per l'API di abilitazione della memoria esterna per Cortex-M7 tramite AC5

### <a name="cortex-m7-using-ac6"></a>Cortex-M7 con AC6

#### <a name="module-properties-for-cortex-m7-using-ac6"></a>Proprietà del modulo per Cortex-M7 con AC6

| bit | Valore | Significato |
|---|---|---|
| 0 | 0<br />1 | Esecuzione in modalità privilegiata<br />Esecuzione in modalità utente |
| 1 | 0<br />1 | Nessuna protezione MPU<br />Protezione MPU (deve essere selezionata la modalità utente) |
| 2 | 0<br />1 | Disabilitare l'accesso alla memoria condivisa/esterna<br />Abilitare l'accesso alla memoria condivisa/esterna |
| [23-3] | 0 | Riservato
| [31-24] | <br />0x00<br />0x01<br />0x02 | **ID compilatore**<br />Iar<br />ARM<br />Gnu |

#### <a name="module-linker-for-cortex-m7-using-ac6"></a>Linker del modulo per Cortex-M7 con AC6

Non viene usato alcun file del linker. Vedere le impostazioni del progetto.

#### <a name="building-modules-for-cortex-m7-using-ac6"></a>Compilazione di moduli per Cortex-M7 con AC6

Viene fornita un'area di lavoro di esempio. Compilare la libreria ThreadX, la libreria ThreadX Modules, il progetto di modulo di esempio e il progetto di gestione moduli di esempio.

#### <a name="thread-extension-definition-for-cortex-m7-using-ac6"></a>Definizione dell'estensione thread per Cortex-M7 con AC6

```c
#define TX_THREAD_EXTENSION_2               VOID    *tx_thread_module_instance_ptr;         \
                                            VOID    *tx_thread_module_entry_info_ptr;       \
                                            ULONG   tx_thread_module_current_user_mode;     \
                                            ULONG   tx_thread_module_user_mode;             \
                                            ULONG   tx_thread_module_saved_lr;              \
                                            VOID    *tx_thread_module_kernel_stack_start;   \
                                            VOID    *tx_thread_module_kernel_stack_end;     \
                                            ULONG   tx_thread_module_kernel_stack_size;     \
                                            VOID    *tx_thread_module_stack_ptr;            \
                                            VOID    *tx_thread_module_stack_start;          \
                                            VOID    *tx_thread_module_stack_end;            \
                                            ULONG   tx_thread_module_stack_size;            \
                                            VOID    *tx_thread_module_reserved;
```

#### <a name="building-module-manager-for-cortex-m7-using-ac6"></a>Building Module Manager for Cortex-M7 using AC6

Viene fornita un'area di lavoro di esempio. Compilare la libreria ThreadX, la libreria ThreadX Modules, il progetto di modulo di esempio e il progetto di gestione moduli di esempio.

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m7-using-ac6"></a>Attributi per l'API di abilitazione della memoria esterna per Cortex-M7 tramite AC6

Il modulo ha sempre accesso in lettura alla memoria condivisa.

| Parametro attribute | Significato |
|---|---|
| TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE | Accesso in scrittura |

### <a name="cortex-m7-using-gnu"></a>Cortex-M7 con GNU

#### <a name="module-properties-for-cortex-m7-using-gnu"></a>Proprietà del modulo per Cortex-M7 con GNU

| bit | Valore | Significato |
|---|---|---|
| 0 | 0<br />1 | Esecuzione in modalità privilegiata<br />Esecuzione in modalità utente |
| 1 | 0<br />1 | Nessuna protezione MPU<br />Protezione MPU (deve essere selezionata la modalità utente) |
| 2 | 0<br />1 | Disabilitare l'accesso alla memoria condivisa/esterna<br />Abilitare l'accesso alla memoria condivisa/esterna |
| [23-3] | 0 | Riservato
| [31-24] | <br />0x00<br />0x01<br />0x02 | **ID compilatore**<br />Iar<br />ARM<br />Gnu |

#### <a name="module-linker-for-cortex-m7-using-gnu"></a>Linker di modulo per Cortex-M7 con GNU

```c
MEMORY
{
  FLASH (rx) : ORIGIN = 0x00030000, LENGTH = 0x00010000
  RAM   (wx) : ORIGIN = 0, LENGTH = 0x00100000
}


SECTIONS
{
  __FLASH_segment_start__ = 0x00030000;
  __FLASH_segment_end__   = 0x00040000;
  __RAM_segment_start__   = 0;
  __RAM_segment_end__     = 0x8000;

  __HEAPSIZE__ = 128;

  __preamble_load_start__ = __FLASH_segment_start__;
  .preamble __FLASH_segment_start__ : AT(__FLASH_segment_start__)
  {
    __preamble_start__ = .;
    *(.preamble .preamble.*)
  }
  __preamble_end__ = __preamble_start__ + SIZEOF(.preamble);

  __dynsym_load_start__ =  ALIGN(__preamble_end__ , 4);
  .dynsym ALIGN(__dynsym_load_start__ , 4) : AT(ALIGN(__dynsym_load_start__ , 4))
  {
    . = ALIGN(4);
    KEEP (*(.dynsym))
    KEEP (*(.dynsym*))
    . = ALIGN(4);
  }
  __dynsym_end__ = __dynsym_load_start__ + SIZEOF(.dynsym);

  __dynstr_load_start__ =  ALIGN(__dynsym_end__ , 4);
  .dynstr ALIGN(__dynstr_load_start__ , 4) : AT(ALIGN(__dynstr_load_start__, 4))
  {
    . = ALIGN(4);
    KEEP (*(.dynstr))
    KEEP (*(.dynstr*))
    . = ALIGN(4);
  }
  __dynstr_end__ = __dynstr_load_start__ + SIZEOF(.dynstr);

  __reldyn_load_start__ =  ALIGN(__dynstr_end__ , 4);
  .rel.dyn ALIGN(__reldyn_load_start__ , 4) : AT(ALIGN(__reldyn_load_start__ , 4))
  {
    . = ALIGN(4);
    KEEP (*(.rel.dyn))
    KEEP (*(.rel.dyn*))
    . = ALIGN(4);
  }
  __reldyn_end__ = __reldyn_load_start__ + SIZEOF(.rel.dyn);

  __relplt_load_start__ =  ALIGN(__reldyn_end__ , 4);
  .rel.plt ALIGN(__relplt_load_start__ , 4) : AT(ALIGN(__relplt_load_start__ , 4))
  {
    . = ALIGN(4);
    KEEP (*(.rel.plt))
    KEEP (*(.rel.plt*))
    . = ALIGN(4);
  }
  __relplt_end__ = __relplt_load_start__ + SIZEOF(.rel.plt);

  __plt_load_start__ =  ALIGN(__relplt_end__ , 4);
  .plt ALIGN(__plt_load_start__ , 4) : AT(ALIGN(__plt_load_start__ , 4))
  {
    . = ALIGN(4);
    KEEP (*(.plt))
    KEEP (*(.plt*))
    . = ALIGN(4);
  }
  __plt_end__ = __plt_load_start__ + SIZEOF(.plt);

  __interp_load_start__ =  ALIGN(__plt_end__ , 4);
  .interp ALIGN(__interp_load_start__ , 4) : AT(ALIGN(__interp_load_start__ , 4))
  {
    . = ALIGN(4);
    KEEP (*(.interp))
    KEEP (*(.interp*))
    . = ALIGN(4);
  }
  __interp_end__ = __interp_load_start__ + SIZEOF(.interp);

  __hash_load_start__ =  ALIGN(__interp_end__ , 4);
  .hash ALIGN(__hash_load_start__ , 4) : AT(ALIGN(__hash_load_start__, 4))
  {
    . = ALIGN(4);
    KEEP (*(.hash))
    KEEP (*(.hash*))
    . = ALIGN(4);
  }
  __hash_end__ = __hash_load_start__ + SIZEOF(.hash);

  __text_load_start__ =  ALIGN(__hash_end__ , 4);
  .text ALIGN(__text_load_start__ , 4) : AT(ALIGN(__text_load_start__, 4))
  {
    __text_start__ = .;
    *(.text .text.* .glue_7t .glue_7 .gnu.linkonce.t.* .gcc_except_table  )
  }
  __text_end__ = __text_start__ + SIZEOF(.text);

  __dtors_load_start__ = ALIGN(__text_end__ , 4);
  .dtors ALIGN(__text_end__ , 4) : AT(ALIGN(__text_end__ , 4))
  {
    __dtors_start__ = .;
    KEEP (*(SORT(.dtors.*))) KEEP (*(.dtors))
  }
  __dtors_end__ = __dtors_start__ + SIZEOF(.dtors);

  __ctors_load_start__ = ALIGN(__dtors_end__ , 4);
  .ctors ALIGN(__dtors_end__ , 4) : AT(ALIGN(__dtors_end__ , 4))
  {
    __ctors_start__ = .;
    KEEP (*(SORT(.ctors.*))) KEEP (*(.ctors))
  }
  __ctors_end__ = __ctors_start__ + SIZEOF(.ctors);

  __got_load_start__ = ALIGN(__ctors_end__ , 4);
  .got ALIGN(__ctors_end__ , 4) : AT(ALIGN(__ctors_end__ , 4))
  {
    . = ALIGN(4);
    _sgot = .;
    KEEP (*(.got))
    KEEP (*(.got*))
    . = ALIGN(4);
    _egot = .;
  } 
  __got_end__ =  __got_load_start__ + SIZEOF(.got);

  __rodata_load_start__ = ALIGN(__got_end__ , 4);
  .rodata ALIGN(__got_end__ , 4) : AT(ALIGN(__got_end__ , 4))
  {
    __rodata_start__ = .;
    *(.rodata .rodata.* .gnu.linkonce.r.*)
  }
  __rodata_end__ = __rodata_start__ + SIZEOF(.rodata);
 
  __code_size__ =  __rodata_end__ - __FLASH_segment_start__;

  __fast_load_start__ = ALIGN(__rodata_end__ , 4);

  __fast_load_end__ = __fast_load_start__ + SIZEOF(.fast);

  __new_got_start__ = ALIGN(__RAM_segment_start__ , 4);

  __new_got_end__ =  __new_got_start__ + SIZEOF(.got);

  .fast ALIGN(__new_got_end__ , 4) : AT(ALIGN(__rodata_end__ , 4))
  {
    __fast_start__ = .;
    *(.fast .fast.*)
  }
  __fast_end__ = __fast_start__ + SIZEOF(.fast);

  .fast_run ALIGN(__fast_end__ , 4) (NOLOAD) :
  {
    __fast_run_start__ = .;
    . = MAX(__fast_run_start__ + SIZEOF(.fast), .);
  }
  __fast_run_end__ = __fast_run_start__ + SIZEOF(.fast_run);

  __data_load_start__ = ALIGN(__fast_load_start__ + SIZEOF(.fast) , 4);
  .data ALIGN(__fast_run_end__ , 4) : AT(ALIGN(__fast_load_start__ + SIZEOF(.fast) , 4))
  {
    __data_start__ = .;
    *(.data .data.* .gnu.linkonce.d.*)
  }
  __data_end__ = __data_start__ + SIZEOF(.data);

  __data_load_end__ = __data_load_start__ + SIZEOF(.data);

  __FLASH_segment_used_end__ = ALIGN(__fast_load_start__ + SIZEOF(.fast) , 4) + SIZEOF(.data);

  .data_run ALIGN(__fast_run_end__ , 4) (NOLOAD) :
  {
    __data_run_start__ = .;
    . = MAX(__data_run_start__ + SIZEOF(.data), .);
  }
  __data_run_end__ = __data_run_start__ + SIZEOF(.data_run);

  __bss_load_start__ = ALIGN(__data_run_end__ , 4);
  .bss ALIGN(__data_run_end__ , 4) (NOLOAD) : AT(ALIGN(__data_run_end__ , 4))
  {
    __bss_start__ = .;
    *(.bss .bss.* .gnu.linkonce.b.*) *(COMMON)
  }
  __bss_end__ = __bss_start__ + SIZEOF(.bss);

  __non_init_load_start__ = ALIGN(__bss_end__ , 4);
  .non_init ALIGN(__bss_end__ , 4) (NOLOAD) : AT(ALIGN(__bss_end__ , 4))
  {
    __non_init_start__ = .;
    *(.non_init .non_init.*)
  }
  __non_init_end__ = __non_init_start__ + SIZEOF(.non_init);

  __heap_load_start__ = ALIGN(__non_init_end__ , 4);
  .heap ALIGN(__non_init_end__ , 4) (NOLOAD) : AT(ALIGN(__non_init_end__ , 4))
  {
    __heap_start__ = .;
    *(.heap)
    . = ALIGN(MAX(__heap_start__ + __HEAPSIZE__ , .), 4);
  }
  __heap_end__ = __heap_start__ + SIZEOF(.heap);

  __data_size__ =  __heap_end__ - __RAM_segment_start__;

}
```

#### <a name="building-modules-for-cortex-m7-using-gnu"></a>Compilazione di moduli per Cortex-M7 con GNU

Vedere build_threadx_module_sample.bat:

```dos
arm-none-eabi-gcc -c -g -mcpu=cortex-m7 -mfloat-abi=hard -mfpu=fpv5-d16 -fpie -fno-plt -mpic-data-is-text-relative -msingle-pic-base txm_module_preamble.s
arm-none-eabi-gcc -c -g -mcpu=cortex-m7 -mfloat-abi=hard -mfpu=fpv5-d16 -fpie -fno-plt -mpic-data-is-text-relative -msingle-pic-base gcc_setup.S
arm-none-eabi-gcc -c -g -mcpu=cortex-m7 -mfloat-abi=hard -mfpu=fpv5-d16 -fpie -fno-plt -mpic-data-is-text-relative -msingle-pic-base -I..\inc -I..\..\..\..\common\inc -I..\..\..\..\common_modules\inc sample_threadx_module.c
arm-none-eabi-ld -A cortex-m7 -T sample_threadx_module.ld txm_module_preamble.o gcc_setup.o sample_threadx_module.o -e _txm_module_thread_shell_entry txm.a -o sample_threadx_module.axf -M > sample_threadx_module.map
```

#### <a name="thread-extension-definition-for-cortex-m7-using-gnu"></a>Definizione dell'estensione thread per Cortex-M7 tramite GNU

```c
#define TX_THREAD_EXTENSION_2               VOID    *tx_thread_module_instance_ptr;         \
                                            VOID    *tx_thread_module_entry_info_ptr;       \
                                            ULONG   tx_thread_module_current_user_mode;     \
                                            ULONG   tx_thread_module_user_mode;             \
                                            ULONG   tx_thread_module_saved_lr;              \
                                            VOID    *tx_thread_module_kernel_stack_start;   \
                                            VOID    *tx_thread_module_kernel_stack_end;     \
                                            ULONG   tx_thread_module_kernel_stack_size;     \
                                            VOID    *tx_thread_module_stack_ptr;            \
                                            VOID    *tx_thread_module_stack_start;          \
                                            VOID    *tx_thread_module_stack_end;            \
                                            ULONG   tx_thread_module_stack_size;            \
                                            VOID    *tx_thread_module_reserved;
```

#### <a name="building-module-manager-for-cortex-m7-using-gnu"></a>Compilazione di Module Manager per Cortex-M7 con GNU

Vedere build_threadx_module_manager_sample.bat:

```dos
arm-none-eabi-gcc -c -g -mcpu=cortex-m7 -mfloat-abi=hard -mfpu=fpv5-d16 -mthumb -I..\inc -I..\..\..\..\common\inc -I..\..\..\..\common_modules\inc sample_threadx_module_manager.c
arm-none-eabi-gcc -c -g -mcpu=cortex-m7 -mfloat-abi=hard -mfpu=fpv5-d16 -mthumb tx_simulator_startup.S
arm-none-eabi-gcc -c -g -mcpu=cortex-m7 -mfloat-abi=hard -mfpu=fpv5-d16 -mthumb cortexm_crt0.S
arm-none-eabi-gcc -g -mcpu=cortex-m7 -mfloat-abi=hard -mfpu=fpv5-d16 -mthumb -nostartfiles -ereset_handler -T sample_threadx.ld tx_simulator_startup.o cortexm_crt0.o sample_threadx_module_manager.o tx.a -o sample_threadx_module_manager.axf -Wl,-Map=sample_threadx_module_manager.map
```

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m7-using-gnu"></a>Attributi per l'API di abilitazione della memoria esterna per Cortex-M7 tramite GNU

Il modulo ha sempre accesso in lettura alla memoria condivisa.

| Parametro dell'attributo | Significato |
|---|---|
| TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE | Accesso in scrittura |

### <a name="cortex-m7-using-iar"></a>Cortex-M7 con IAR

#### <a name="module-preamble-for-cortex-m7-using-iar"></a>Preambolo del modulo per Cortex-M7 con IAR

```c
    SECTION .text:CODE

    AAPCS INTERWORK, ROPI, RWPI_COMPATIBLE,  VFP_COMPATIBLE
    PRESERVE8

    /* Define public symbols.  */

    PUBLIC __txm_module_preamble


    /* Define application-specific start/stop entry points for the module.  */

    EXTERN demo_module_start


    /* Define common external references.  */

    EXTERN  _txm_module_thread_shell_entry
    EXTERN  _txm_module_callback_request_thread_entry
    EXTERN  ROPI$$Length
    EXTERN  RWPI$$Length

    DATA
__txm_module_preamble:
    DC32      0x4D4F4455                                        ; Module ID
    DC32      0x5                                               ; Module Major Version
    DC32      0x6                                               ; Module Minor Version
    DC32      32                                                ; Module Preamble Size in 32-bit words
    DC32      0x12345678                                        ; Module ID (application defined)
    DC32      0x00000007                                        ; Module Properties where:
                                                                ;   Bits 31-24: Compiler ID
                                                                ;           0 -> IAR
                                                                ;           1 -> ARM
                                                                ;           2 -> GNU
                                                                ;   Bits 23-3: Reserved
                                                                ;   Bit 2:  0 -> Disable shared/external memory access
                                                                ;           1 -> Enable shared/external memory access
                                                                ;   Bit 1:  0 -> No MPU protection
                                                                ;           1 -> MPU protection (must have user mode selected - bit 0 set)
                                                                ;   Bit 0:  0 -> Privileged mode execution
                                                                ;           1 -> User mode execution


    DC32      _txm_module_thread_shell_entry - . - 0            ; Module Shell Entry Point
    DC32      demo_module_start - . - 0                         ; Module Start Thread Entry Point
    DC32      0                                                 ; Module Stop Thread Entry Point
    DC32      1                                                 ; Module Start/Stop Thread Priority
    DC32      1024                                              ; Module Start/Stop Thread Stack Size
    DC32      _txm_module_callback_request_thread_entry - . - 0 ; Module Callback Thread Entry
    DC32      1                                                 ; Module Callback Thread Priority
    DC32      1024                                              ; Module Callback Thread Stack Size
    DC32      ROPI$$Length                                      ; Module Code Size
    DC32      RWPI$$Length                                      ; Module Data Size
    DC32      0                                                 ; Reserved 0
    DC32      0                                                 ; Reserved 1
    DC32      0                                                 ; Reserved 2
    DC32      0                                                 ; Reserved 3
    DC32      0                                                 ; Reserved 4
    DC32      0                                                 ; Reserved 5
    DC32      0                                                 ; Reserved 6
    DC32      0                                                 ; Reserved 7
    DC32      0                                                 ; Reserved 8  
    DC32      0                                                 ; Reserved 9
    DC32      0                                                 ; Reserved 10
    DC32      0                                                 ; Reserved 11
    DC32      0                                                 ; Reserved 12
    DC32      0                                                 ; Reserved 13
    DC32      0                                                 ; Reserved 14
    DC32      0                                                 ; Reserved 15

    END
```

#### <a name="module-properties-for-cortex-m7-using-iar"></a>Proprietà del modulo per Cortex-M7 con IAR

| bit | Valore | Significato |
|---|---|---|
| 0 | 0<br />1 | Esecuzione in modalità privilegiata<br />Esecuzione in modalità utente |
| 1 | 0<br />1 | Nessuna protezione MPU<br />Protezione MPU (deve essere selezionata la modalità utente) |
| 2 | 0<br />1 | Disabilitare l'accesso alla memoria condivisa/esterna<br />Abilitare l'accesso alla memoria condivisa/esterna |
| [23-3] | 0 | Riservato
| [31-24] | <br />0x00<br />0x01<br />0x02 | **ID compilatore**<br />Iar<br />ARM<br />Gnu |

#### <a name="module-linker-for-cortex-m7-using-iar"></a>Linker di modulo per Cortex-M7 con IAR

```c
/*###ICF### Section handled by ICF editor, don't touch! ****/
/*-Editor annotation file-*/
/* IcfEditorFile="$TOOLKIT_DIR$\config\ide\IcfEditor\cortex_v1_0.xml" */
/*-Specials-*/
define symbol __ICFEDIT_intvec_start__     = 0x00400000;
/*-Memory Regions-*/
define symbol __ICFEDIT_region_RAM_start__ = 0x20450000;
define symbol __ICFEDIT_region_RAM_end__   = 0x2045f000 -1;
define symbol __ICFEDIT_region_RAM_NOCACHE_start__ = 0x2045f000;
define symbol __ICFEDIT_region_RAM_NOCACHE_end__   = 0x20460000 -1;
define symbol __ICFEDIT_region_ROM_start__ = 0x00500000;
define symbol __ICFEDIT_region_ROM_end__   = 0x00600000 -1;
define symbol __ICFEDIT_region_SDRAM_start__ = 0x70000000;
define symbol __ICFEDIT_region_SDRAM_end__   = 0x70200000 -1;

/*-Sizes-*/
define symbol __ICFEDIT_size_cstack__      = 0x2000;
define symbol __ICFEDIT_size_heap__        = 0x1000;
/**** End of ICF editor section. ###ICF###*/

define memory mem with size = 4G;
define region RAM_region    = mem:[from __ICFEDIT_region_RAM_start__ to __ICFEDIT_region_RAM_end__];
define region RAM_NOCACHE_region = mem:[from __ICFEDIT_region_RAM_NOCACHE_start__ to __ICFEDIT_region_RAM_NOCACHE_end__];
define region ROM_region    = mem:[from __ICFEDIT_region_ROM_start__ to __ICFEDIT_region_ROM_end__];
define region SDRAM_region  = mem:[from __ICFEDIT_region_SDRAM_start__ to __ICFEDIT_region_SDRAM_end__];

define block HEAP   with alignment = 8, size = __ICFEDIT_size_heap__   { };

initialize by copy { readwrite };
do not initialize  { section .noinit };

define movable block ROPI with alignment = 4, fixed order
{
  ro object txm_module_preamble.o,
  ro,
  ro data
};

define movable block RWPI with alignment = 8, fixed order, static base
{
  rw,
  block HEAP
};

place in ROM_region   { block ROPI };
place in RAM_region   { block RWPI };
```

#### <a name="building-modules-for-cortex-m7-using-iar"></a>Compilazione di moduli per Cortex-M7 con IAR

Viene fornita un'area di lavoro di esempio. Compilare la libreria ThreadX, la libreria ThreadX Modules, il progetto di modulo demo e il progetto demo module manager.

#### <a name="thread-extension-definition-for-cortex-m7-using-iar"></a>Definizione dell'estensione thread per Cortex-M7 con IAR

```c
#define TX_THREAD_EXTENSION_2   VOID    *tx_thread_module_instance_ptr;         \
                                VOID    *tx_thread_module_entry_info_ptr;       \
                                ULONG   tx_thread_module_current_user_mode;     \
                                ULONG   tx_thread_module_user_mode;             \
                                ULONG   tx_thread_module_saved_lr;              \
                                VOID    *tx_thread_module_kernel_stack_start;   \
                                VOID    *tx_thread_module_kernel_stack_end;     \
                                ULONG   tx_thread_module_kernel_stack_size;     \
                                VOID    *tx_thread_module_stack_ptr;            \
                                VOID    *tx_thread_module_stack_start;          \
                                VOID    *tx_thread_module_stack_end;            \
                                ULONG   tx_thread_module_stack_size;            \
                                VOID    *tx_thread_module_reserved;             \
                                VOID    *tx_thread_iar_tls_pointer;
```

#### <a name="building-module-manager-for-cortex-m7-using-iar"></a>Compilazione di Module Manager per Cortex-M7 con IAR

Viene fornita un'area di lavoro di esempio. Compilare la libreria ThreadX, la libreria ThreadX Modules, il progetto di modulo demo e il progetto demo module manager.

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m7-using-iar"></a>Attributi per l'API di abilitazione della memoria esterna per Cortex-M7 con IAR

Il modulo ha sempre accesso in lettura alla memoria condivisa.

| Parametro dell'attributo | Significato |
|---|---|
| TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE | Accesso in scrittura |

## <a name="cortex-r4-processor"></a>Processore Cortex-R4

### <a name="cortex-r4-using-ac6"></a>Cortex-R4 con AC6

#### <a name="module-preamble-for-cortex-r4-using-ac6"></a>Preambolo del modulo per Cortex-R4 con AC6

```c
    .text

/* Define common external references.  */

.global     _txm_module_thread_shell_entry
.global     demo_module_start
.global     _txm_module_callback_request_thread_entry
.global     Image$$ER_RO$$Length
.global     Image$$ER_RW$$Length
.global     Image$$ER_ZI$$ZI$$Length

/* Stack aligned, ROPI and RWPI, R9 used as data offset register.  */
.eabi_attribute Tag_ABI_align_preserved, 1
.eabi_attribute Tag_ABI_PCS_RO_data, 1
.eabi_attribute Tag_ABI_PCS_R9_use,  1
.eabi_attribute Tag_ABI_PCS_RW_data, 2

__txm_module_preamble:
.word   0x4D4F4455                                          /* Module ID  */
.word   0x5                                                 /* Module Major Version  */
.word   0x3                                                 /* Module Minor Version  */
.word   32                                                  /* Module Preamble Size in 32-bit words  */
.word   0x12345678                                          /* Module ID (application defined)  */
.word   0x01000001                                          /* Module Properties where:
                                                               Bits 31-24: Compiler ID
                                                                       0 -> IAR
                                                                       1 -> RVDS/ARM
                                                                       2 -> GNU
                                                               Bits 23-1:  Reserved
                                                               Bit 0:  0 -> Privileged mode execution (no MMU protection)
                                                                       1 -> User mode execution (MMU protection)  */
.word   _txm_module_thread_shell_entry - __txm_module_preamble  /* Module Shell Entry Point  */
.word   demo_module_start - __txm_module_preamble           /* Module Start Thread Entry Point  */
.word   0                                                   /* Module Stop Thread Entry Point   */
.word   1                                                   /* Module Start/Stop Thread Priority  */
.word   1024                                                /* Module Start/Stop Thread Stack Size  */
.word   _txm_module_callback_request_thread_entry - __txm_module_preamble   /* Module Callback Thread Entry  */
.word   1                                                   /* Module Callback Thread Priority  */
.word   1024                                                /* Module Callback Thread Stack Size  */
.word   9000                                                /* Module Code Size */
.word   11000                                               /* Module Data Size */
.word   0                                                   /* Reserved 0  */
.word   0                                                   /* Reserved 1  */
.word   0                                                   /* Reserved 2  */
.word   0                                                   /* Reserved 3  */
.word   0                                                   /* Reserved 4  */
.word   0                                                   /* Reserved 5  */
.word   0                                                   /* Reserved 6  */
.word   0                                                   /* Reserved 7  */
.word   0                                                   /* Reserved 8  */
.word   0                                                   /* Reserved 9  */
.word   0                                                   /* Reserved 10  */
.word   0                                                   /* Reserved 11  */
.word   0                                                   /* Reserved 12  */
.word   0                                                   /* Reserved 13  */
.word   0                                                   /* Reserved 14  */
.word   0                                                   /* Reserved 15  */
```

#### <a name="module-properties-for-cortex-r4-using-ac6"></a>Proprietà del modulo per Cortex-R4 tramite AC6

| bit | Valore | Significato |
|---|---|---|
| 0 | 0<br />1 | Esecuzione in modalità privilegiata<br />Esecuzione in modalità utente |
| [23-1] | 0 | Riservato
| [31-24] | <br />0x00<br />0x01<br />0x02 | **ID compilatore**<br />Iar<br />ARM<br />Gnu |

#### <a name="module-linker-for-cortex-r4-using-ac6"></a>Linker di modulo per Cortex-R4 con AC6

Basato sulla riga di comando, nessun esempio di file del linker.

#### <a name="building-modules-for-cortex-r4-using-ac6"></a>Compilazione di moduli per Cortex-R4 con AC6

Un semplice esempio della riga di comando per la compilazione di un modulo Cortex-R4 usando AC6:

```dos
armclang -c -g -fropi -frwpi --target=arm-arm-none-eabi -mcpu=cortex-r4 demo_threadx_module.c
armclang -c -g -fropi -frwpi --target=arm-arm-none-eabi -mcpu=cortex-r4 txm_module_preamble.S
armclang -c -g -fropi -frwpi --target=arm-arm-none-eabi -mcpu=cortex-r4 semihosting.c
armlink -d -o demo_threadx_module.axf --elf --ro 0x00100000 --first txm_module_preamble.o --entry=_txm_module_thread_shell_entry --ropi --rwpi --remove --map --symbols --datacompressor=off --list demo_threadx_module.map txm_module_preamble.o demo_threadx_module.o semihosting.o txm.a
```

#### <a name="thread-extension-definition-for-cortex-r4-using-ac6"></a>Definizione dell'estensione thread per Cortex-R4 con AC6

```c
#define TX_THREAD_EXTENSION_2   ULONG   tx_thread_vfp_enable;                   \
                                VOID    *tx_thread_module_instance_ptr;         \
                                VOID    *tx_thread_module_entry_info_ptr;       \
                                ULONG   tx_thread_module_current_user_mode;     \
                                ULONG   tx_thread_module_user_mode;             \
                                VOID    *tx_thread_module_kernel_stack_start;   \
                                VOID    *tx_thread_module_kernel_stack_end;     \
                                ULONG   tx_thread_module_kernel_stack_size;     \
                                VOID    *tx_thread_module_stack_ptr;            \
                                VOID    *tx_thread_module_stack_start;          \
                                VOID    *tx_thread_module_stack_end;            \
                                ULONG   tx_thread_module_stack_size;            \
                                VOID    *tx_thread_module_reserved;
```

#### <a name="building-module-manager-for-cortex-r4-using-ac6"></a>Creazione di Module Manager per Cortex-R4 tramite AC6

Un semplice esempio della riga di comando per la compilazione di un modulo Cortex-R4 manager usando AC6:

```dos
armclang -c -g --target=arm-arm-none-eabi -mcpu=cortex-r4 demo_threadx_module_manager.c
armclang -c -g --target=arm-arm-none-eabi -mcpu=cortex-r4 timer.c
armclang -c -g --target=arm-arm-none-eabi -mcpu=cortex-r4 gic.c
armclang -c -g --target=arm-arm-none-eabi -mcpu=cortex-r4 tx_initialize_low_level.S
armclang -c -g --target=arm-arm-none-eabi -mcpu=cortex-r4 startup.S
armlink -d -o demo_threadx_module_manager.axf --elf --scatter=demo_threadx.scat --remove --map --symbols --list demo_threadx_module_manager.map startup.o timer.o gic.o demo_threadx_module_manager.o tx_initialize_low_level.o tx.a
```

#### <a name="attributes-for-external-memory-enable-api-for-cortex-r4-using-ac6"></a>Attributi per l'API di abilitazione della memoria esterna per Cortex-R4 tramite AC6

Il modulo ha sempre accesso in lettura alla memoria condivisa.

| Parametro dell'attributo | Significato |
|---|---|
| TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE | Accesso in scrittura |

### <a name="cortex-r4-using-iar"></a>Cortex-R4 con IAR

#### <a name="module-preamble-for-cortex-r4-using-iar"></a>Preambolo del modulo per Cortex-R4 con IAR

```c
    SECTION .text:CODE

    AAPCS INTERWORK, ROPI, RWPI_COMPATIBLE,  VFP_COMPATIBLE
    PRESERVE8

    /* Define public symbols.  */
    PUBLIC __txm_module_preamble

    /* Define application-specific start/stop entry points for the module.  */
    EXTERN demo_module_start

    /* Define common external references.  */
    EXTERN  _txm_module_thread_shell_entry
    EXTERN  _txm_module_callback_request_thread_entry
    EXTERN  ROPI$$Length
    EXTERN  RWPI$$Length

    DATA
__txm_module_preamble:
    DC32      0x4D4F4455                                        ; Module ID
    DC32      0x5                                               ; Module Major Version
    DC32      0x6                                               ; Module Minor Version
    DC32      32                                                ; Module Preamble Size in 32-bit words
    DC32      0x12345678                                        ; Module ID (application defined)
    DC32      0x00000001                                        ; Module Properties where:
                                                                ;   Bits 31-24: Compiler ID
                                                                ;           0 -> IAR
                                                                ;           1 -> ARM
                                                                ;           2 -> GNU
                                                                ;   Bits 23-1: Reserved
                                                                ;   Bit 0:  0 -> Privileged mode execution (no MPU protection)
                                                                ;           1 -> User mode execution (MPU protection)
    DC32      _txm_module_thread_shell_entry - . - 0            ; Module Shell Entry Point
    DC32      demo_module_start - . - 0                         ; Module Start Thread Entry Point
    DC32      0                                                 ; Module Stop Thread Entry Point
    DC32      1                                                 ; Module Start/Stop Thread Priority
    DC32      1024                                              ; Module Start/Stop Thread Stack Size
    DC32      _txm_module_callback_request_thread_entry - . - 0 ; Module Callback Thread Entry
    DC32      1                                                 ; Module Callback Thread Priority
    DC32      1024                                              ; Module Callback Thread Stack Size
    DC32      ROPI$$Length                                      ; Module Code Size
    DC32      RWPI$$Length                                      ; Module Data Size
    DC32      0                                                 ; Reserved 0
    DC32      0                                                 ; Reserved 1
    DC32      0                                                 ; Reserved 2
    DC32      0                                                 ; Reserved 3
    DC32      0                                                 ; Reserved 4
    DC32      0                                                 ; Reserved 5
    DC32      0                                                 ; Reserved 6
    DC32      0                                                 ; Reserved 7
    DC32      0                                                 ; Reserved 8  
    DC32      0                                                 ; Reserved 9
    DC32      0                                                 ; Reserved 10
    DC32      0                                                 ; Reserved 11
    DC32      0                                                 ; Reserved 12
    DC32      0                                                 ; Reserved 13
    DC32      0                                                 ; Reserved 14
    DC32      0                                                 ; Reserved 15

    END
```

#### <a name="module-properties-for-cortex-r4-using-iar"></a>Proprietà del modulo per Cortex-R4 con IAR

| bit | Valore | Significato |
|---|---|---|
| 0 | 0<br />1 | Esecuzione in modalità privilegiata<br />Esecuzione in modalità utente |
| [23-1] | 0 | Riservato
| [31-24] | <br />0x00<br />0x01<br />0x02 | **ID compilatore**<br />Iar<br />ARM<br />Gnu |

#### <a name="module-linker-for-cortex-r4-using-iar"></a>Linker di modulo per Cortex-R4 con IAR

```c
/*###ICF### Section handled by ICF editor, don't touch! ****/
/*-Editor annotation file-*/
/* IcfEditorFile="$TOOLKIT_DIR$\config\ide\IcfEditor\a_v1_0.xml" */
/*-Specials-*/
/*-Memory Regions-*/
define symbol __ICFEDIT_region_ROM_start__ = 0x00100000;
define symbol __ICFEDIT_region_ROM_end__   = 0x0013FFFF;
define symbol __ICFEDIT_region_RAM_start__ = 0x08000000;
define symbol __ICFEDIT_region_RAM_end__   = 0x0800FFFF;
/*-Sizes-*/
define symbol __ICFEDIT_size_cstack__   = 0;
define symbol __ICFEDIT_size_svcstack__ = 0;
define symbol __ICFEDIT_size_irqstack__ = 0;
define symbol __ICFEDIT_size_fiqstack__ = 0;
define symbol __ICFEDIT_size_undstack__ = 0;
define symbol __ICFEDIT_size_abtstack__ = 0;
define symbol __ICFEDIT_size_heap__     = 0x100;
/**** End of ICF editor section. ###ICF###*/

define memory mem with size = 4G;
define region ROM_region   = mem:[from __ICFEDIT_region_ROM_start__   to __ICFEDIT_region_ROM_end__];
define region RAM_region   = mem:[from __ICFEDIT_region_RAM_start__   to __ICFEDIT_region_RAM_end__];

define block HEAP      with alignment = 8, size = __ICFEDIT_size_heap__     { };

initialize by copy { readwrite };
do not initialize  { section .noinit };

define movable block ROPI with alignment = 4, fixed order
{
  ro object txm_module_preamble.o,
  ro,
  ro data
};

define movable block RWPI with alignment = 8, fixed order, static base
{
  rw,
  block HEAP
};

place in ROM_region   { block ROPI };
place in RAM_region   { block RWPI };
```

#### <a name="building-modules-for-cortex-r4-using-iar"></a>Compilazione di moduli per Cortex-R4 con IAR

Viene fornita un'area di lavoro di esempio. Compilare la libreria ThreadX, la libreria ThreadX Modules, il progetto di modulo demo e il progetto demo module manager.

#### <a name="thread-extension-definition-for-cortex-r4-using-iar"></a>Definizione dell'estensione thread per Cortex-R4 con IAR

```c
#define TX_THREAD_EXTENSION_2   ULONG   tx_thread_vfp_enable;                   \
                                VOID    *tx_thread_module_instance_ptr;         \
                                VOID    *tx_thread_module_entry_info_ptr;       \
                                ULONG   tx_thread_module_current_user_mode;     \
                                ULONG   tx_thread_module_user_mode;             \
                                VOID    *tx_thread_module_kernel_stack_start;   \
                                VOID    *tx_thread_module_kernel_stack_end;     \
                                ULONG   tx_thread_module_kernel_stack_size;     \
                                VOID    *tx_thread_module_stack_ptr;            \
                                VOID    *tx_thread_module_stack_start;          \
                                VOID    *tx_thread_module_stack_end;            \
                                ULONG   tx_thread_module_stack_size;            \
                                VOID    *tx_thread_module_reserved;             \
                                VOID    *tx_thread_iar_tls_pointer;
```

#### <a name="building-module-manager-for-cortex-r4-using-iar"></a>Compilazione di Module Manager per Cortex-R4 con IAR

Viene fornita un'area di lavoro di esempio. Compilare la libreria ThreadX, la libreria ThreadX Modules, il progetto di modulo demo e il progetto demo module manager.

#### <a name="attributes-for-external-memory-enable-api-for-cortex-r4-using-iar"></a>Attributi per l'API di abilitazione della memoria esterna per Cortex-R4 con IAR

Il modulo ha sempre accesso in lettura alla memoria condivisa.

| Parametro dell'attributo | Significato |
|---|---|
| TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE | Accesso in scrittura |

## <a name="mcf544xx-processor"></a>Processore MCF544xx

### <a name="mcf544xx-using-ghs"></a>MCF544xx con GHS

#### <a name="module-preamble-for-mcf544xx-using-ghs"></a>Preambolo del modulo per MCF544xx con GHS

```c
    SECT    .preamble, x

    /* Define public symbols.  */
    XDEF __txm_module_preamble

__txm_module_preamble:
    DC.L    0x4D4F4455                                  /* Module ID                                */
    DC.L    0x5                                         /* Module Major Version                     */
    DC.L    0x3                                         /* Module Minor Version                     */
    DC.L    32                                          /* Module Preamble Size in 32-bit words     */
    DC.L    0x12345678                                  /* Module ID (application defined)          */
    DC.L    0x03000003                                  /* Module Properties where:                 */
                                                        /* Bits 31-24: Compiler ID                  */
                                                        /*           3 -> GHS                       */
                                                        /* Bits 23-2: Reserved                      */
                                                        /* Bit 1:  0 -> No MMU protection           */
                                                        /*         1 -> MMU protection (must have   */
                                                        /*              user mode selected)         */
                                                        /* Bit 0:  0 -> Supervisor mode execution   */
                                                        /*         1 -> User mode execution         */
    DC.L    _txm_module_thread_shell_entry              /* Module Shell Entry Point                 */
    DC.L    demo_module_start                           /* Module Start Thread Entry Point          */
    DC.L    0                                           /* Module Stop Thread Entry Point           */
    DC.L    1                                           /* Module Start/Stop Thread Priority        */
    DC.L    2048                                        /* Module Start/Stop Thread Stack Size      */
    DC.L    _txm_module_callback_request_thread_entry   /* Module Callback Thread Entry             */
    DC.L    1                                           /* Module Callback Thread Priority          */
    DC.L    2048                                        /* Module Callback Thread Stack Size        */
    DC.L    module_code_size                            /* Module Code Size                         */
    DC.L    module_data_size                            /* Module Data Size                         */
    DC.L    0                                           /* Reserved 0                               */
    DC.L    0                                           /* Reserved 1                               */
    DC.L    0                                           /* Reserved 2                               */
    DC.L    0                                           /* Reserved 3                               */
    DC.L    0                                           /* Reserved 4                               */
    DC.L    0                                           /* Reserved 5                               */
    DC.L    0                                           /* Reserved 6                               */
    DC.L    0                                           /* Reserved 7                               */
    DC.L    0                                           /* Reserved 8                               */
    DC.L    0                                           /* Reserved 9                               */
    DC.L    0                                           /* Reserved 10                              */
    DC.L    0                                           /* Reserved 11                              */
    DC.L    0                                           /* Reserved 12                              */
    DC.L    0                                           /* Reserved 13                              */
    DC.L    0                                           /* Reserved 14                              */
    DC.L    0                                           /* Reserved 15                              */

    END
```

#### <a name="module-properties-for-mcf544xx-using-ghs"></a>Proprietà del modulo per MCF544xx con GHS

| bit | Valore | Significato |
|---|---|---|
| 0 | 0<br />1 | Esecuzione in modalità privilegiata<br />Esecuzione in modalità utente |
| 1 | 0<br />1 | Nessuna protezione MMU<br />Protezione MMU (deve essere selezionata la modalità utente) |
| 2 | 0<br />1 | Disabilitare l'accesso alla memoria condivisa/esterna<br />Abilitare l'accesso alla memoria condivisa/esterna |
| [23-3] | 0 | Riservato
| [31-24] | <br />0x03 | **ID compilatore**<br />Ghs |

#### <a name="module-linker-for-mcf544xx-using-ghs"></a>Linker di modulo per MCF544xx con GHS

```c
DEFAULTS {

    heap_reserve =  256
    stack_reserve = 256
}

//
// Program layout for PIC and PID built programs.
//

-sec
{
//
// The data segment
//
    .pidbase                0x00000000 :
    .sdabase                           :
    .sbss                   NOCLEAR    :
    .sdata                             :
    .data                   NOLOAD     :
    .bss                    NOCLEAR    :
    .heap                   ALIGN(16) PAD( heap_reserve +
        // Add space for call-graph profiling if used:
        (isdefined(__ghs_indgcount)?(2000+(sizeof(.text)/2)):0) +
        // Add estimated space for call-count profiling if used:
        (isdefined(__ghs_indmcount)?10000:0) )
                                             :
    .stack      ALIGN(16) PAD(stack_reserve) :

    module_data_size = sizeof(.pidbase) + sizeof(.sdabase) + sizeof(.sbss) + sizeof(.sdata) + sizeof(.data) + sizeof(.bss) + sizeof(.heap) + sizeof(.stack);

//
// The code segment
//

    .picbase                0x00000000 :
    .preamble                          :
    .text                              :
    .syscall                           :
    .fixaddr                           :
    .fixtype                           :
    .rodata                            :
    .ROM.data               ROM(.data) :
    .secinfo                           :

    module_code_size =  endaddr(.secinfo);
}
```

#### <a name="building-modules-for-mcf544xx-using-ghs"></a>Compilazione di moduli per MCF544xx con GHS

Viene fornita un'area di lavoro di esempio. Compilare la libreria ThreadX, la libreria ThreadX Modules, il progetto di modulo demo e il progetto demo module manager.

#### <a name="thread-extension-definition-for-mcf544xx-using-ghs"></a>Definizione dell'estensione del thread per MCF544xx con GHS

```c
#define TX_THREAD_EXTENSION_2   int     Errno;                                  \
                                VOID    *tx_thread_module_instance_ptr;         \
                                VOID    *tx_thread_module_entry_info_ptr;       \
                                ULONG   tx_thread_module_current_user_mode;     \
                                ULONG   tx_thread_module_user_mode;             \
                                ULONG   tx_thread_module_mmu_protection;        \
                                VOID *  tx_thread_module_dispatch_return;       \
                                VOID    *tx_thread_module_kernel_stack_start;   \
                                VOID    *tx_thread_module_kernel_stack_end;     \
                                ULONG   tx_thread_module_kernel_stack_size;     \
                                VOID    *tx_thread_module_stack_ptr;            \
                                VOID    *tx_thread_module_stack_start;          \
                                VOID    *tx_thread_module_stack_end;            \
                                ULONG   tx_thread_module_stack_size;            \
                                VOID    *tx_thread_module_reserved;
```

#### <a name="building-module-manager-for-mcf544xx-using-ghs"></a>Compilazione di Gestione moduli per MCF544xx con GHS

Viene fornita un'area di lavoro di esempio. Compilare la libreria ThreadX, la libreria ThreadX Modules, il progetto di modulo demo e il progetto demo module manager.

#### <a name="attributes-for-external-memory-enable-api-for-mcf544xx-using-ghs"></a>Attributi per l'API di abilitazione della memoria esterna per MCF544xx con GHS

Questa funzionalità non è abilitata in MCF544xx.

## <a name="rx63-processor"></a>Processore RX63

### <a name="rx63-using-iar"></a>RX63 con IAR

#### <a name="module-preamble-for-rx63-using-iar"></a>Preambolo del modulo per RX63 con IAR

```c
    /* Alignment of 4 (16-byte) */
    SECTION .text:CODE (4)

    /* Define public symbols.  */
    PUBLIC __txm_module_preamble

    /* Define application-specific start/stop entry points for the module.  */
    EXTERN _demo_module_start

    /* Define common external references.  */
    EXTERN  __txm_module_thread_shell_entry
    EXTERN  __txm_module_callback_request_thread_entry
    EXTERN  ROPI$$Length
    EXTERN  RWPI$$Length

    DATA
__txm_module_preamble:
    DC32      0x4D4F4455                                        // Module ID
    DC32      0x5                                               // Module Major Version
    DC32      0x6                                               // Module Minor Version
    DC32      32                                                // Module Preamble Size in 32-bit words
    DC32      0x12345678                                        // Module ID (application defined)
    DC32      0x00000007                                        // Module Properties where:
                                                                //   Bits 31-24: Compiler ID
                                                                //           0 -> IAR
                                                                //           1 -> ARM
                                                                //           2 -> GNU
                                                                //   Bit 0:  0 -> Privileged mode execution
                                                                //           1 -> User mode execution
                                                                //   Bit 1:  0 -> No MPU protection
                                                                //           1 -> MPU protection (must have user mode selected)
                                                                //   Bit 2:  0 -> Disable shared/external memory access
                                                                //           1 -> Enable shared/external memory access
    DC32      __txm_module_thread_shell_entry - $               // Module Shell Entry Point
    DC32      _demo_module_start - $                            // Module Start Thread Entry Point
    DC32      0                                                 // Module Stop Thread Entry Point
    DC32      1                                                 // Module Start/Stop Thread Priority
    DC32      1024                                              // Module Start/Stop Thread Stack Size
    DC32      __txm_module_callback_request_thread_entry - $    // Module Callback Thread Entry
    DC32      1                                                 // Module Callback Thread Priority
    DC32      1024                                              // Module Callback Thread Stack Size
    DC32      ROPI$$Length                                      // Module Code Size
    DC32      RWPI$$Length                                      // Module Data Size
    DC32      0                                                 // Reserved 0
    DC32      0                                                 // Reserved 1
    DC32      0                                                 // Reserved 2
    DC32      0                                                 // Reserved 3
    DC32      0                                                 // Reserved 4
    DC32      0                                                 // Reserved 5
    DC32      0                                                 // Reserved 6
    DC32      0                                                 // Reserved 7
    DC32      0                                                 // Reserved 8  
    DC32      0                                                 // Reserved 9
    DC32      0                                                 // Reserved 10
    DC32      0                                                 // Reserved 11
    DC32      0                                                 // Reserved 12
    DC32      0                                                 // Reserved 13
    DC32      0                                                 // Reserved 14
    DC32      0                                                 // Reserved 15

    END
```

#### <a name="module-properties-for-rx63-using-iar"></a>Proprietà del modulo per RX63 con IAR

| bit | Valore | Significato |
|---|---|---|
| 0 | 0<br />1 | Esecuzione in modalità privilegiata<br />Esecuzione in modalità utente |
| 1 | 0<br />1 | Nessuna protezione MPU<br />Protezione MPU (deve essere selezionata la modalità utente) |
| 2 | 0<br />1 | Disabilitare l'accesso alla memoria condivisa/esterna<br />Abilitare l'accesso alla memoria condivisa/esterna |
| [23-3] | 0 | Riservato
| [31-24] | <br />0x00<br />0x02 | **ID compilatore**<br />Iar<br />Gnu |

#### <a name="module-linker-for-rx63-using-iar"></a>Linker di modulo per RX63 con IAR

```c
//-----------------------------------------------------------------------------
// ILINK command file template for the Renesas RX microcontroller R5F563NB
//-----------------------------------------------------------------------------
define exported symbol __link_file_version_4 = 1;

define memory mem with size = 4G;

// ID Code Protection
define exported symbol __ID_BYTES_1_4   = 0xFFFFFFFF;
define exported symbol __ID_BYTES_5_8   = 0xFFFFFFFF;
define exported symbol __ID_BYTES_9_12  = 0xFFFFFFFF;
define exported symbol __ID_BYTES_13_16 = 0xFFFFFFFF;

// Endian Select Register (MDE)
// Choose between Little endian=0xFFFFFFFF or Big endian=0xFFFFFFF8
define exported symbol __MDES           = 0xFFFFFFFF;

// Option Function Select Register 0 (OFS0)
define exported symbol __OFS0           = 0xFFFFFFFF;

// Option Function Select Register 1 (OFS1)
define exported symbol __OFS1           = 0xFFFFFFFF;

//define region ROM_region16 = mem:[from 0xFFFF8000 to 0xFFFFFFFF];
define region RAM_region16 = mem:[from 0x00010000 to 0x00017FFF];
//define region ROM_region24 = mem:[from 0xFFF00000 to 0xFFFFFFFF];
//define region RAM_region24 = mem:[from 0x00000004 to 0x0001FFFF];
define region ROM_region32 = mem:[from 0xFFF10400 to 0xFFFFFFFF];
//define region RAM_region32 = mem:[from 0x00000004 to 0x0001FFFF];
//define region DATA_FLASH_region = mem:[from 0x00100000 to 0x00107FFF];

initialize by copy { rw, ro section D, ro section D_1, ro section D_2 };
do not initialize  { section .*.noinit };

define block HEAP     with alignment = 4, size = _HEAP_SIZE { };
//define block USTACK   with alignment = 4, size = _USTACK_SIZE { };
//define block ISTACK   with alignment = 4, size = _ISTACK_SIZE { };

//define block STACKS with fixed order { block ISTACK,
//                                       block USTACK };

//place at address mem:0xFFFFFF80 { ro section .nmivec };
//"ROM16":place in ROM_region16        { ro section .code16*,
//                                       ro section .data16* };
//"RAM16":place in RAM_region16        { rw section .data16*,
//                                       rw section __DLIB_PERTHREAD };
//"ROM24":place in ROM_region24        { ro section .code24*,
//                                       ro section .data24* };
//"RAM24":place in RAM_region24        { rw section .data24* };
//"ROM32":place in ROM_region32        { ro };
//"RAM32":place in RAM_region32        { rw,
//                                       ro section D,
//                                       ro section D_1,
//                                       ro section D_2,
//                                       block HEAP,
//                                       block STACKS,
//                                       last section FREEMEM };

//"DATAFLASH":place in DATA_FLASH_region
//                                     { ro section .dataflash* };

define movable block ROPI with alignment = 4, fixed order, static base CB
{
  ro object txm_module_preamble_rx63n.o,
  ro,
  ro data
};

define movable block RWPI with alignment = 8, fixed order, static base SB
{
  rw section .sbdata*,
  rw section .sbrel*,
  rw section __DLIB_PERTHREAD,
  block HEAP
};

place in ROM_region32   { block ROPI };
place in RAM_region16   { block RWPI };
```

#### <a name="building-modules-for-rx63-using-iar"></a>Compilazione di moduli per RX63 con IAR

Viene fornita un'area di lavoro di esempio. Compilare la libreria ThreadX, la libreria ThreadX Modules, il progetto di modulo demo e il progetto demo module manager.

#### <a name="thread-extension-definition-for-rxrx635n-using-iar"></a>Definizione dell'estensione thread per RXRX635N con IAR

```c
#define TX_THREAD_EXTENSION_2   VOID    *tx_thread_module_instance_ptr;       \
                                VOID    *tx_thread_module_entry_info_ptr;     \
                                ULONG   tx_thread_module_current_user_mode;   \
                                ULONG   tx_thread_module_user_mode;           \
                                VOID    *tx_thread_module_kernel_stack_start; \
                                VOID    *tx_thread_module_kernel_stack_end;   \
                                ULONG   tx_thread_module_kernel_stack_size;   \
                                VOID    *tx_thread_module_stack_ptr;          \
                                VOID    *tx_thread_module_stack_start;        \
                                VOID    *tx_thread_module_stack_end;          \
                                ULONG   tx_thread_module_stack_size;          \
                                VOID    *tx_thread_module_reserved;           \
                                VOID    *tx_thread_iar_tls_pointer;
```

#### <a name="building-module-manager-for-rx63-using-iar"></a>Compilazione di Gestione moduli per RX63 con IAR

Viene fornita un'area di lavoro di esempio. Compilare la libreria ThreadX, la libreria ThreadX Modules, il progetto di modulo demo e il progetto demo module manager.

#### <a name="attributes-for-external-memory-enable-api-for-rx63-using-iar"></a>Attributi per l'API di abilitazione della memoria esterna per RX63 con IAR

| Parametro attributo | Significato |
|---|---|
| TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_EXECUTE | Eseguire codice |
| TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE | Accesso in scrittura |
| TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_READ | accesso in lettura |

## <a name="rx65n-processor"></a>Processore RX65N

### <a name="rx65n-using-iar"></a>RX65N con IAR

#### <a name="module-preamble-for-rx65n-using-iar"></a>Preambolo del modulo per RX65N con IAR

```c
    /* Alignment of 4 (16-byte) */
    SECTION .text:CODE (4)

    /* Define public symbols.  */
    PUBLIC __txm_module_preamble

    /* Define application-specific start/stop entry points for the module.  */
    EXTERN _demo_module_start

    /* Define common external references.  */
    EXTERN  __txm_module_thread_shell_entry
    EXTERN  __txm_module_callback_request_thread_entry
    EXTERN  ROPI$$Length
    EXTERN  RWPI$$Length

    DATA
__txm_module_preamble:
    DC32      0x4D4F4455                                        // Module ID
    DC32      0x5                                               // Module Major Version
    DC32      0x6                                               // Module Minor Version
    DC32      32                                                // Module Preamble Size in 32-bit words
    DC32      0x12345678                                        // Module ID (application defined)
    DC32      0x00000007                                        // Module Properties where:
                                                                //   Bits 31-24: Compiler ID
                                                                //           0 -> IAR
                                                                //           1 -> ARM
                                                                //           2 -> GNU
                                                                //   Bit 0:  0 -> Privileged mode execution
                                                                //           1 -> User mode execution
                                                                //   Bit 1:  0 -> No MPU protection
                                                                //           1 -> MPU protection (must have user mode selected)
                                                                //   Bit 2:  0 -> Disable shared/external memory access
                                                                //           1 -> Enable shared/external memory access
    DC32      __txm_module_thread_shell_entry - $               // Module Shell Entry Point
    DC32      _demo_module_start - $                            // Module Start Thread Entry Point
    DC32      0                                                 // Module Stop Thread Entry Point
    DC32      1                                                 // Module Start/Stop Thread Priority
    DC32      1024                                              // Module Start/Stop Thread Stack Size
    DC32      __txm_module_callback_request_thread_entry - $    // Module Callback Thread Entry
    DC32      1                                                 // Module Callback Thread Priority
    DC32      1024                                              // Module Callback Thread Stack Size
    DC32      ROPI$$Length                                      // Module Code Size
    DC32      RWPI$$Length                                      // Module Data Size
    DC32      0                                                 // Reserved 0
    DC32      0                                                 // Reserved 1
    DC32      0                                                 // Reserved 2
    DC32      0                                                 // Reserved 3
    DC32      0                                                 // Reserved 4
    DC32      0                                                 // Reserved 5
    DC32      0                                                 // Reserved 6
    DC32      0                                                 // Reserved 7
    DC32      0                                                 // Reserved 8  
    DC32      0                                                 // Reserved 9
    DC32      0                                                 // Reserved 10
    DC32      0                                                 // Reserved 11
    DC32      0                                                 // Reserved 12
    DC32      0                                                 // Reserved 13
    DC32      0                                                 // Reserved 14
    DC32      0                                                 // Reserved 15

    END
```

#### <a name="module-properties-for-rx65n-using-iar"></a>Proprietà del modulo per RX65N con IAR

| bit | Valore | Significato |
|---|---|---|
| 0 | 0<br />1 | Esecuzione in modalità privilegiata<br />Esecuzione in modalità utente |
| 1 | 0<br />1 | Nessuna protezione MPU<br />Protezione MPU (deve essere selezionata la modalità utente) |
| 2 | 0<br />1 | Disabilitare l'accesso alla memoria condivisa/esterna<br />Abilitare l'accesso alla memoria condivisa/esterna |
| [23-3] | 0 | Riservato
| [31-24] | <br />0x00<br />0x02 | **ID compilatore**<br />Iar<br />Gnu |

#### <a name="module-linker-for-rx65n-using-iar"></a>Linker di modulo per RX65N con IAR

```c
//-----------------------------------------------------------------------------
// ILINK command file template for the Renesas RX microcontroller R5F565N
//-----------------------------------------------------------------------------
define exported symbol __link_file_version_4 = 1;

define memory mem with size = 4G;

// ID Code Protection
define exported symbol __ID_BYTES_1_4   = 0xFFFFFFFF;
define exported symbol __ID_BYTES_5_8   = 0xFFFFFFFF;
define exported symbol __ID_BYTES_9_12  = 0xFFFFFFFF;
define exported symbol __ID_BYTES_13_16 = 0xFFFFFFFF;

// Endian Select Register (MDE)
// Choose between Little endian=0xFFFFFFFF or Big endian=0xFFFFFFF8
define exported symbol __MDES           = 0xFFFFFFFF;

// Option Function Select Register 0 (OFS0)
define exported symbol __OFS0           = 0xFFFFFFFF;

// Option Function Select Register 1 (OFS1)
define exported symbol __OFS1           = 0xFFFFFFFF;

//define region ROM_region16 = mem:[from 0xFFFF8000 to 0xFFFFFFFF];
define region RAM_region16 = mem:[from 0x00010000 to 0x00017FFF];
//define region ROM_region24 = mem:[from 0xFFF00000 to 0xFFFFFFFF];
//define region RAM_region24 = mem:[from 0x00000004 to 0x0001FFFF];
define region ROM_region32 = mem:[from 0xFFF10400 to 0xFFFFFFFF];
//define region RAM_region32 = mem:[from 0x00000004 to 0x0001FFFF];
//define region DATA_FLASH_region = mem:[from 0x00100000 to 0x00107FFF];

initialize by copy { rw, ro section D, ro section D_1, ro section D_2 };
do not initialize  { section .*.noinit };

define block HEAP     with alignment = 4, size = _HEAP_SIZE { };
//define block USTACK   with alignment = 4, size = _USTACK_SIZE { };
//define block ISTACK   with alignment = 4, size = _ISTACK_SIZE { };

//define block STACKS with fixed order { block ISTACK,
//                                       block USTACK };

//place at address mem:0xFFFFFF80 { ro section .nmivec };
//"ROM16":place in ROM_region16        { ro section .code16*,
//                                       ro section .data16* };
//"RAM16":place in RAM_region16        { rw section .data16*,
//                                       rw section __DLIB_PERTHREAD };
//"ROM24":place in ROM_region24        { ro section .code24*,
//                                       ro section .data24* };
//"RAM24":place in RAM_region24        { rw section .data24* };
//"ROM32":place in ROM_region32        { ro };
//"RAM32":place in RAM_region32        { rw,
//                                       ro section D,
//                                       ro section D_1,
//                                       ro section D_2,
//                                       block HEAP,
//                                       block STACKS,
//                                       last section FREEMEM };

//"DATAFLASH":place in DATA_FLASH_region
//                                     { ro section .dataflash* };

define movable block ROPI with alignment = 4, fixed order, static base CB
{
  ro object txm_module_preamble_rx65n.o,
  ro,
  ro data
};

define movable block RWPI with alignment = 8, fixed order, static base SB
{
  rw section .sbdata*,
  rw section .sbrel*,
  rw section __DLIB_PERTHREAD,
  block HEAP
};

place in ROM_region32   { block ROPI };
place in RAM_region16   { block RWPI };
```

#### <a name="building-modules-for-rx65n-using-iar"></a>Compilazione di moduli per RX65N con IAR

Viene fornita un'area di lavoro di esempio. Compilare la libreria ThreadX, la libreria ThreadX Modules, il progetto di modulo demo e il progetto demo module manager.

#### <a name="thread-extension-definition-for-rx65n-using-iar"></a>Definizione dell'estensione thread per RX65N con IAR

```c
#define TX_THREAD_EXTENSION_2   VOID    *tx_thread_module_instance_ptr;         \
                                VOID    *tx_thread_module_entry_info_ptr;       \
                                ULONG   tx_thread_module_current_user_mode;     \
                                ULONG   tx_thread_module_user_mode;             \
                                VOID    *tx_thread_module_kernel_stack_start;   \
                                VOID    *tx_thread_module_kernel_stack_end;     \
                                ULONG   tx_thread_module_kernel_stack_size;     \
                                VOID    *tx_thread_module_stack_ptr;            \
                                VOID    *tx_thread_module_stack_start;          \
                                VOID    *tx_thread_module_stack_end;            \
                                ULONG   tx_thread_module_stack_size;            \
                                VOID    *tx_thread_module_reserved;             \
                                VOID    *tx_thread_iar_tls_pointer;
```

#### <a name="building-module-manager-for-rx65n-using-iar"></a>Compilazione di Module Manager per RX65N con IAR

Viene fornita un'area di lavoro di esempio. Compilare la libreria ThreadX, la libreria ThreadX Modules, il progetto di modulo demo e il progetto demo module manager.

#### <a name="attributes-for-external-memory-enable-api-for-rx65n-using-iar"></a>Attributi per l'API di abilitazione della memoria esterna per RX65N con IAR

| Parametro attributo | Significato |
|---|---|
| TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_EXECUTE | Eseguire codice |
| TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE | Accesso in scrittura |
| TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_READ | accesso in lettura |
