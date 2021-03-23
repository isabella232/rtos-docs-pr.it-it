---
title: Appendice-Esempi specifici della porta
description: Questo articolo illustra alcuni esempi specifici della porta per i moduli ThreadX.
author: philmea
ms.author: philmea
ms.date: 07/15/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: b54b8b094e608052fdbfc392d93a57ebb34515ed
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823306"
---
# <a name="appendix---port-specific-examples"></a><span data-ttu-id="1fa14-103">Appendice-Esempi specifici della porta</span><span class="sxs-lookup"><span data-stu-id="1fa14-103">Appendix - Port-specific examples</span></span>

## <a name="arm11-processor"></a><span data-ttu-id="1fa14-104">Processore ARM11</span><span class="sxs-lookup"><span data-stu-id="1fa14-104">ARM11 processor</span></span>

### <a name="arm11-using-gcc"></a><span data-ttu-id="1fa14-105">ARM11 con GCC</span><span class="sxs-lookup"><span data-stu-id="1fa14-105">ARM11 using GCC</span></span>

#### <a name="module-preamble-for-arm11-using-gcc"></a><span data-ttu-id="1fa14-106">Preambolo del modulo per ARM11 con GCC</span><span class="sxs-lookup"><span data-stu-id="1fa14-106">Module preamble for ARM11 using GCC</span></span>

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

#### <a name="module-properties-for-arm11-using-gcc"></a><span data-ttu-id="1fa14-107">Proprietà dei moduli per ARM11 con GCC</span><span class="sxs-lookup"><span data-stu-id="1fa14-107">Module properties for ARM11 using GCC</span></span>

| <span data-ttu-id="1fa14-108">bit</span><span class="sxs-lookup"><span data-stu-id="1fa14-108">Bit</span></span> | <span data-ttu-id="1fa14-109">Valore</span><span class="sxs-lookup"><span data-stu-id="1fa14-109">Value</span></span> | <span data-ttu-id="1fa14-110">Significato</span><span class="sxs-lookup"><span data-stu-id="1fa14-110">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="1fa14-111">[23-0]</span><span class="sxs-lookup"><span data-stu-id="1fa14-111">[23-0]</span></span> | <span data-ttu-id="1fa14-112">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-112">0</span></span> | <span data-ttu-id="1fa14-113">Riservato</span><span class="sxs-lookup"><span data-stu-id="1fa14-113">Reserved</span></span>
| <span data-ttu-id="1fa14-114">[31-24]</span><span class="sxs-lookup"><span data-stu-id="1fa14-114">[31-24]</span></span> | <br /><span data-ttu-id="1fa14-115">0x00</span><span class="sxs-lookup"><span data-stu-id="1fa14-115">0x00</span></span><br /><span data-ttu-id="1fa14-116">0x01</span><span class="sxs-lookup"><span data-stu-id="1fa14-116">0x01</span></span><br /><span data-ttu-id="1fa14-117">0x02</span><span class="sxs-lookup"><span data-stu-id="1fa14-117">0x02</span></span> | <span data-ttu-id="1fa14-118">**ID compilatore**</span><span class="sxs-lookup"><span data-stu-id="1fa14-118">**Compiler ID**</span></span><br /><span data-ttu-id="1fa14-119">IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-119">IAR</span></span><br /><span data-ttu-id="1fa14-120">ARM</span><span class="sxs-lookup"><span data-stu-id="1fa14-120">ARM</span></span><br /><span data-ttu-id="1fa14-121">GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-121">GNU</span></span> |

#### <a name="module-linker-for-arm11-using-gcc"></a><span data-ttu-id="1fa14-122">Module linker per ARM11 con GCC</span><span class="sxs-lookup"><span data-stu-id="1fa14-122">Module linker for ARM11 using GCC</span></span>

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

#### <a name="building-modules-for-arm11-using-gcc"></a><span data-ttu-id="1fa14-123">Compilazione di moduli per ARM11 tramite GCC</span><span class="sxs-lookup"><span data-stu-id="1fa14-123">Building Modules for ARM11 using GCC</span></span>

<span data-ttu-id="1fa14-124">Un semplice esempio di riga di comando per la compilazione di un modulo ARM11 usando GCC:</span><span class="sxs-lookup"><span data-stu-id="1fa14-124">A simple command-line example for building an ARM11 module using GCC:</span></span>

```dos
arm-none-eabi-gcc -c -g -mcpu=arm1136j-s -msingle-pic-base -fPIC -mpic-register=r9 txm_module_preamble.S
arm-none-eabi-gcc -c -g -mcpu=arm1136j-s -msingle-pic-base -fPIC -mpic-register=r9 gcc_setup.S
arm-none-eabi-gcc -c -g -mcpu=arm1136j-s -msingle-pic-base -fPIC -mpic-register=r9 demo_threadx_module.c
arm-none-eabi-ld -A arm1136j-s -T demo_threadx_module.ld txm_module_preamble.o gcc_setup.o demo_threadx_module.o txm.a txm.a -o demo_threadx_module.out -M > demo_threadx_module.map
```

#### <a name="thread-extension-definition-for-arm11-using-gcc"></a><span data-ttu-id="1fa14-125">Definizione dell'estensione di thread per ARM11 con GCC</span><span class="sxs-lookup"><span data-stu-id="1fa14-125">Thread extension definition for ARM11 using GCC</span></span>

```c
#define TX_THREAD_EXTENSION_2   VOID    *tx_thread_module_instance_ptr;  \
                                VOID    *tx_thread_module_entry_info_ptr;
```

#### <a name="building-module-manager-for-arm11-using-gcc"></a><span data-ttu-id="1fa14-126">Compilazione di gestione moduli per ARM11 tramite GCC</span><span class="sxs-lookup"><span data-stu-id="1fa14-126">Building Module Manager for ARM11 using GCC</span></span>

<span data-ttu-id="1fa14-127">Non viene fornito alcun esempio.</span><span class="sxs-lookup"><span data-stu-id="1fa14-127">No example is provided.</span></span>

#### <a name="attributes-for-external-memory-enable-api-for-arm11-using-gcc"></a><span data-ttu-id="1fa14-128">Attributi per l'API External memory Enable per ARM11 con GCC</span><span class="sxs-lookup"><span data-stu-id="1fa14-128">Attributes for external memory enable API for ARM11 using GCC</span></span>

<span data-ttu-id="1fa14-129">Questa funzionalità non è abilitata su questa porta.</span><span class="sxs-lookup"><span data-stu-id="1fa14-129">This feature not enabled on this port.</span></span>

### <a name="arm11-using-ac5"></a><span data-ttu-id="1fa14-130">ARM11 con AC5</span><span class="sxs-lookup"><span data-stu-id="1fa14-130">ARM11 using AC5</span></span>

#### <a name="module-preamble-for-arm11-using-ac5"></a><span data-ttu-id="1fa14-131">Preambolo del modulo per ARM11 con AC5</span><span class="sxs-lookup"><span data-stu-id="1fa14-131">Module preamble for ARM11 using AC5</span></span>

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

#### <a name="module-properties-for-arm11-using-ac5"></a><span data-ttu-id="1fa14-132">Proprietà del modulo per ARM11 con AC5</span><span class="sxs-lookup"><span data-stu-id="1fa14-132">Module properties for ARM11 using AC5</span></span>

| <span data-ttu-id="1fa14-133">bit</span><span class="sxs-lookup"><span data-stu-id="1fa14-133">Bit</span></span> | <span data-ttu-id="1fa14-134">Valore</span><span class="sxs-lookup"><span data-stu-id="1fa14-134">Value</span></span> | <span data-ttu-id="1fa14-135">Significato</span><span class="sxs-lookup"><span data-stu-id="1fa14-135">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="1fa14-136">[23-0]</span><span class="sxs-lookup"><span data-stu-id="1fa14-136">[23-0]</span></span> | <span data-ttu-id="1fa14-137">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-137">0</span></span> | <span data-ttu-id="1fa14-138">Riservato</span><span class="sxs-lookup"><span data-stu-id="1fa14-138">Reserved</span></span>
| <span data-ttu-id="1fa14-139">[31-24]</span><span class="sxs-lookup"><span data-stu-id="1fa14-139">[31-24]</span></span> | <br /><span data-ttu-id="1fa14-140">0x00</span><span class="sxs-lookup"><span data-stu-id="1fa14-140">0x00</span></span><br /><span data-ttu-id="1fa14-141">0x01</span><span class="sxs-lookup"><span data-stu-id="1fa14-141">0x01</span></span><br /><span data-ttu-id="1fa14-142">0x02</span><span class="sxs-lookup"><span data-stu-id="1fa14-142">0x02</span></span> | <span data-ttu-id="1fa14-143">**ID compilatore**</span><span class="sxs-lookup"><span data-stu-id="1fa14-143">**Compiler ID**</span></span><br /><span data-ttu-id="1fa14-144">IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-144">IAR</span></span><br /><span data-ttu-id="1fa14-145">ARM</span><span class="sxs-lookup"><span data-stu-id="1fa14-145">ARM</span></span><br /><span data-ttu-id="1fa14-146">GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-146">GNU</span></span> |

#### <a name="module-linker-for-arm11-using-ac5"></a><span data-ttu-id="1fa14-147">Modulo linker per ARM11 con AC5</span><span class="sxs-lookup"><span data-stu-id="1fa14-147">Module linker for ARM11 using AC5</span></span>

<span data-ttu-id="1fa14-148">Compilato dalla riga di comando, nessun esempio di file del linker.</span><span class="sxs-lookup"><span data-stu-id="1fa14-148">Built on command-line, no linker file example.</span></span>

#### <a name="building-modules-for-arm11-using-ac5"></a><span data-ttu-id="1fa14-149">Compilazione di moduli per ARM11 con AC5</span><span class="sxs-lookup"><span data-stu-id="1fa14-149">Building Modules for ARM11 using AC5</span></span>

<span data-ttu-id="1fa14-150">Un semplice esempio di riga di comando per la compilazione di un modulo ARM11 usando AC5:</span><span class="sxs-lookup"><span data-stu-id="1fa14-150">A simple command-line example for building an ARM11 module using AC5:</span></span>

```dos
armasm -g --cpu ARM1136J-S --apcs /interwork --apcs /ropi --apcs /rwpi txm_module_preamble.s
armcc -g -c -O0 --cpu ARM1136J-S --apcs /interwork --apcs /ropi --apcs /rwpi demo_threadx_module.c
armlink -d -o demo_threadx_module.axf --elf --ro 0 --first txm_module_preamble.o(Init) --entry=_txm_module_thread_shell_entry --ropi --rwpi --remove --map --symbols --list demo_threadx_module.map txm_module_preamble.o demo_threadx_module.o txm.a
```

#### <a name="thread-extension-definition-for-arm11-using-ac5"></a><span data-ttu-id="1fa14-151">Definizione dell'estensione di thread per ARM11 con AC5</span><span class="sxs-lookup"><span data-stu-id="1fa14-151">Thread extension definition for ARM11 using AC5</span></span>

```c
#define TX_THREAD_EXTENSION_2   VOID    *tx_thread_module_instance_ptr;  \
                                VOID    *tx_thread_module_entry_info_ptr;
```

#### <a name="building-module-manager-for-arm11-using-ac5"></a><span data-ttu-id="1fa14-152">Compilazione di gestione moduli per ARM11 con AC5</span><span class="sxs-lookup"><span data-stu-id="1fa14-152">Building Module Manager for ARM11 using AC5</span></span>

<span data-ttu-id="1fa14-153">Semplice esempio di riga di comando per la compilazione di un gestore di moduli ARM11 usando AC5:</span><span class="sxs-lookup"><span data-stu-id="1fa14-153">A simple command-line example for building an ARM11 module manager using AC5:</span></span>

```dos
armasm -g --cpu ARM1136J-S --apcs /interwork tx_initialize_low_level.s
armcc -g -c -O2 --cpu ARM1136J-S --apcs /interwork demo_threadx_module_manager.c
armcc -g -c -O2 --cpu ARM1136J-S --apcs /interwork module_code.c
armlink -d -o demo_threadx_module_manager.axf --elf --ro 0 --first tx_initialize_low_level.o(Init) --remove --map --symbols --list demo_threadx_module_manager.map tx_initialize_low_level.o demo_threadx_module_manager.o module_code.o tx.a
```

#### <a name="attributes-for-external-memory-enable-api-for-arm11-using-ac5"></a><span data-ttu-id="1fa14-154">Attributi per la memoria esterna Abilita API per ARM11 con AC5</span><span class="sxs-lookup"><span data-stu-id="1fa14-154">Attributes for external memory enable API for ARM11 using AC5</span></span>

<span data-ttu-id="1fa14-155">Questa funzionalità non è abilitata su questa porta.</span><span class="sxs-lookup"><span data-stu-id="1fa14-155">This feature not enabled on this port.</span></span>

## <a name="cortex-a7-processor"></a><span data-ttu-id="1fa14-156">Processore Cortex-A7</span><span class="sxs-lookup"><span data-stu-id="1fa14-156">Cortex-A7 processor</span></span>

### <a name="cortex-a7-using-ac5"></a><span data-ttu-id="1fa14-157">Cortex-A7 con AC5</span><span class="sxs-lookup"><span data-stu-id="1fa14-157">Cortex-A7 using AC5</span></span>

#### <a name="module-preamble-for-cortex-a7-using-ac5"></a><span data-ttu-id="1fa14-158">Preambolo del modulo per Cortex-A7 con AC5</span><span class="sxs-lookup"><span data-stu-id="1fa14-158">Module preamble for Cortex-A7 using AC5</span></span>

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

#### <a name="module-properties-for-cortex-a7-using-ac5"></a><span data-ttu-id="1fa14-159">Proprietà dei moduli per Cortex-A7 con AC5</span><span class="sxs-lookup"><span data-stu-id="1fa14-159">Module properties for Cortex-A7 using AC5</span></span>

| <span data-ttu-id="1fa14-160">bit</span><span class="sxs-lookup"><span data-stu-id="1fa14-160">Bit</span></span> | <span data-ttu-id="1fa14-161">Valore</span><span class="sxs-lookup"><span data-stu-id="1fa14-161">Value</span></span> | <span data-ttu-id="1fa14-162">Significato</span><span class="sxs-lookup"><span data-stu-id="1fa14-162">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="1fa14-163">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-163">0</span></span> | <span data-ttu-id="1fa14-164">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-164">0</span></span><br /><span data-ttu-id="1fa14-165">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-165">1</span></span> | <span data-ttu-id="1fa14-166">Esecuzione in modalità privilegiata</span><span class="sxs-lookup"><span data-stu-id="1fa14-166">Privileged mode execution</span></span><br /><span data-ttu-id="1fa14-167">Esecuzione in modalità utente</span><span class="sxs-lookup"><span data-stu-id="1fa14-167">User mode execution</span></span> |
| <span data-ttu-id="1fa14-168">[23-1]</span><span class="sxs-lookup"><span data-stu-id="1fa14-168">[23-1]</span></span> | <span data-ttu-id="1fa14-169">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-169">0</span></span> | <span data-ttu-id="1fa14-170">Riservato</span><span class="sxs-lookup"><span data-stu-id="1fa14-170">Reserved</span></span>
| <span data-ttu-id="1fa14-171">[31-24]</span><span class="sxs-lookup"><span data-stu-id="1fa14-171">[31-24]</span></span> | <br /><span data-ttu-id="1fa14-172">0x00</span><span class="sxs-lookup"><span data-stu-id="1fa14-172">0x00</span></span><br /><span data-ttu-id="1fa14-173">0x01</span><span class="sxs-lookup"><span data-stu-id="1fa14-173">0x01</span></span><br /><span data-ttu-id="1fa14-174">0x02</span><span class="sxs-lookup"><span data-stu-id="1fa14-174">0x02</span></span> | <span data-ttu-id="1fa14-175">**ID compilatore**</span><span class="sxs-lookup"><span data-stu-id="1fa14-175">**Compiler ID**</span></span><br /><span data-ttu-id="1fa14-176">IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-176">IAR</span></span><br /><span data-ttu-id="1fa14-177">ARM</span><span class="sxs-lookup"><span data-stu-id="1fa14-177">ARM</span></span><br /><span data-ttu-id="1fa14-178">GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-178">GNU</span></span> |

#### <a name="module-linker-for-cortex-a7-using-ac5"></a><span data-ttu-id="1fa14-179">Module linker per Cortex-A7 con AC5</span><span class="sxs-lookup"><span data-stu-id="1fa14-179">Module linker for Cortex-A7 using AC5</span></span>

<span data-ttu-id="1fa14-180">Compilato dalla riga di comando, nessun esempio di file del linker.</span><span class="sxs-lookup"><span data-stu-id="1fa14-180">Built on command-line, no linker file example.</span></span>

#### <a name="building-modules-for-cortex-a7-using-ac5"></a><span data-ttu-id="1fa14-181">Compilazione di moduli per Cortex-A7 con AC5</span><span class="sxs-lookup"><span data-stu-id="1fa14-181">Building Modules for Cortex-A7 using AC5</span></span>

<span data-ttu-id="1fa14-182">Un semplice esempio di riga di comando per la compilazione di un modulo Cortex-A7 con AC5:</span><span class="sxs-lookup"><span data-stu-id="1fa14-182">A simple command-line example for building a Cortex-A7 module using AC5:</span></span>

```dos
armasm -g --cpu=cortex-a7.no_neon --fpu=softvfp --apcs=/interwork/ropi/rwpi txm_module_preamble.s
armcc  -g --cpu=cortex-a7.no_neon --fpu=softvfp -c --apcs=/interwork/ropi/rwpi --lower_ropi demo_threadx_module.c
armlink -d -o demo_threadx_module.axf --elf --ro 0 --first txm_module_preamble.o(Init) --entry=_txm_module_thread_shell_entry --ropi --rwpi --remove --map --symbols --list demo_threadx_module.map txm_module_preamble.o demo_threadx_module.o txm.a
```

#### <a name="thread-extension-definition-for-cortex-a7-using-ac5"></a><span data-ttu-id="1fa14-183">Definizione di estensione di thread per Cortex-A7 con AC5</span><span class="sxs-lookup"><span data-stu-id="1fa14-183">Thread extension definition for Cortex-A7 using AC5</span></span>

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

#### <a name="building-module-manager-for-cortex-a7-using-ac5"></a><span data-ttu-id="1fa14-184">Compilazione di Module Manager per Cortex-A7 con AC5</span><span class="sxs-lookup"><span data-stu-id="1fa14-184">Building Module Manager for Cortex-A7 using AC5</span></span>

<span data-ttu-id="1fa14-185">Semplice esempio di riga di comando per la compilazione di un modulo di gestione dei moduli Cortex-A7 con AC5:</span><span class="sxs-lookup"><span data-stu-id="1fa14-185">A simple command-line example for building a Cortex-A7 module manager using AC5:</span></span>

```dos
armasm -g --cpu=cortex-a7.no_neon --fpu=softvfp --apcs=interwork tx_initialize_low_level.s
armcc -g --cpu=cortex-a7.no_neon --fpu=softvfp -c demo_threadx_module_manager.c
armcc -g --cpu=cortex-a7.no_neon --fpu=softvfp -c module_code.c
armlink -d -o demo_threadx_module_manager.axf --elf --ro 0x80000000 --first tx_initialize_low_level.o(VECTORS) --remove --map --symbols --list demo_threadx_module_manager.map tx_initialize_low_level.o demo_threadx_module_manager.o module_code.o tx.a
```

#### <a name="attributes-for-external-memory-enable-api-for-cortex-a7-using-ac5"></a><span data-ttu-id="1fa14-186">Attributi per la memoria esterna Abilita API per Cortex-A7 con AC5</span><span class="sxs-lookup"><span data-stu-id="1fa14-186">Attributes for external memory enable API for Cortex-A7 using AC5</span></span>

<span data-ttu-id="1fa14-187">Per configurare le impostazioni di memoria condivisa, è possibile usare gli attributi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1fa14-187">The following attributes can be used to set up shared memory settings:</span></span>
| <span data-ttu-id="1fa14-188">Parametro attribute</span><span class="sxs-lookup"><span data-stu-id="1fa14-188">Attribute parameter</span></span> | <span data-ttu-id="1fa14-189">Significato</span><span class="sxs-lookup"><span data-stu-id="1fa14-189">Meaning</span></span> |
|---|---|
| <span data-ttu-id="1fa14-190">TXM_MMU_ATTRIBUTE_XN</span><span class="sxs-lookup"><span data-stu-id="1fa14-190">TXM_MMU_ATTRIBUTE_XN</span></span> | <span data-ttu-id="1fa14-191">Esegui mai</span><span class="sxs-lookup"><span data-stu-id="1fa14-191">Execute Never</span></span> |
| <span data-ttu-id="1fa14-192">TXM_MMU_ATTRIBUTE_B</span><span class="sxs-lookup"><span data-stu-id="1fa14-192">TXM_MMU_ATTRIBUTE_B</span></span> | <span data-ttu-id="1fa14-193">Impostazione B</span><span class="sxs-lookup"><span data-stu-id="1fa14-193">B setting</span></span> |
| <span data-ttu-id="1fa14-194">TXM_MMU_ATTRIBUTE_C</span><span class="sxs-lookup"><span data-stu-id="1fa14-194">TXM_MMU_ATTRIBUTE_C</span></span> | <span data-ttu-id="1fa14-195">Impostazione C</span><span class="sxs-lookup"><span data-stu-id="1fa14-195">C setting</span></span> |
| <span data-ttu-id="1fa14-196">TXM_MMU_ATTRIBUTE_AP</span><span class="sxs-lookup"><span data-stu-id="1fa14-196">TXM_MMU_ATTRIBUTE_AP</span></span> | <span data-ttu-id="1fa14-197">Impostazione AP</span><span class="sxs-lookup"><span data-stu-id="1fa14-197">AP setting</span></span> |
| <span data-ttu-id="1fa14-198">TXM_MMU_ATTRIBUTE_TEX</span><span class="sxs-lookup"><span data-stu-id="1fa14-198">TXM_MMU_ATTRIBUTE_TEX</span></span> | <span data-ttu-id="1fa14-199">Impostazione TEX</span><span class="sxs-lookup"><span data-stu-id="1fa14-199">TEX setting</span></span> |

<span data-ttu-id="1fa14-200">Per informazioni sulla configurazione di queste impostazioni, vedere la documentazione di ARM.</span><span class="sxs-lookup"><span data-stu-id="1fa14-200">See ARM documentation for how these settings are configured.</span></span>

## <a name="cortex-m3-processor"></a><span data-ttu-id="1fa14-201">Processore Cortex-M3</span><span class="sxs-lookup"><span data-stu-id="1fa14-201">Cortex-M3 processor</span></span>

### <a name="cortex-m3-using-ac5"></a><span data-ttu-id="1fa14-202">Cortex-M3 con AC5</span><span class="sxs-lookup"><span data-stu-id="1fa14-202">Cortex-M3 using AC5</span></span>

#### <a name="module-preamble-for-cortex-m3-using-ac5"></a><span data-ttu-id="1fa14-203">Preambolo del modulo per Cortex-M3 con AC5</span><span class="sxs-lookup"><span data-stu-id="1fa14-203">Module preamble for Cortex-M3 using AC5</span></span>

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

#### <a name="module-properties-for-cortex-m3-using-ac5"></a><span data-ttu-id="1fa14-204">Proprietà dei moduli per Cortex-M3 con AC5</span><span class="sxs-lookup"><span data-stu-id="1fa14-204">Module properties for Cortex-M3 using AC5</span></span>

| <span data-ttu-id="1fa14-205">bit</span><span class="sxs-lookup"><span data-stu-id="1fa14-205">Bit</span></span> | <span data-ttu-id="1fa14-206">Valore</span><span class="sxs-lookup"><span data-stu-id="1fa14-206">Value</span></span> | <span data-ttu-id="1fa14-207">Significato</span><span class="sxs-lookup"><span data-stu-id="1fa14-207">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="1fa14-208">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-208">0</span></span> | <span data-ttu-id="1fa14-209">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-209">0</span></span><br /><span data-ttu-id="1fa14-210">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-210">1</span></span> | <span data-ttu-id="1fa14-211">Esecuzione in modalità privilegiata</span><span class="sxs-lookup"><span data-stu-id="1fa14-211">Privileged mode execution</span></span><br /><span data-ttu-id="1fa14-212">Esecuzione in modalità utente</span><span class="sxs-lookup"><span data-stu-id="1fa14-212">User mode execution</span></span> |
| <span data-ttu-id="1fa14-213">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-213">1</span></span> | <span data-ttu-id="1fa14-214">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-214">0</span></span><br /><span data-ttu-id="1fa14-215">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-215">1</span></span> | <span data-ttu-id="1fa14-216">Nessuna protezione MPU</span><span class="sxs-lookup"><span data-stu-id="1fa14-216">No MPU protection</span></span><br /><span data-ttu-id="1fa14-217">Protezione MPU (è necessario selezionare la modalità utente)</span><span class="sxs-lookup"><span data-stu-id="1fa14-217">MPU protection (must have user mode selected)</span></span> |
| <span data-ttu-id="1fa14-218">2</span><span class="sxs-lookup"><span data-stu-id="1fa14-218">2</span></span> | <span data-ttu-id="1fa14-219">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-219">0</span></span><br /><span data-ttu-id="1fa14-220">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-220">1</span></span> | <span data-ttu-id="1fa14-221">Disabilitare l'accesso alla memoria condivisa/esterna</span><span class="sxs-lookup"><span data-stu-id="1fa14-221">Disable shared/external memory access</span></span><br /><span data-ttu-id="1fa14-222">Abilitare l'accesso alla memoria condivisa/esterna</span><span class="sxs-lookup"><span data-stu-id="1fa14-222">Enable shared/external memory access</span></span> |
| <span data-ttu-id="1fa14-223">[23-3]</span><span class="sxs-lookup"><span data-stu-id="1fa14-223">[23-3]</span></span> | <span data-ttu-id="1fa14-224">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-224">0</span></span> | <span data-ttu-id="1fa14-225">Riservato</span><span class="sxs-lookup"><span data-stu-id="1fa14-225">Reserved</span></span>
| <span data-ttu-id="1fa14-226">[31-24]</span><span class="sxs-lookup"><span data-stu-id="1fa14-226">[31-24]</span></span> | <br /><span data-ttu-id="1fa14-227">0x00</span><span class="sxs-lookup"><span data-stu-id="1fa14-227">0x00</span></span><br /><span data-ttu-id="1fa14-228">0x01</span><span class="sxs-lookup"><span data-stu-id="1fa14-228">0x01</span></span><br /><span data-ttu-id="1fa14-229">0x02</span><span class="sxs-lookup"><span data-stu-id="1fa14-229">0x02</span></span> | <span data-ttu-id="1fa14-230">**ID compilatore**</span><span class="sxs-lookup"><span data-stu-id="1fa14-230">**Compiler ID**</span></span><br /><span data-ttu-id="1fa14-231">IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-231">IAR</span></span><br /><span data-ttu-id="1fa14-232">ARM</span><span class="sxs-lookup"><span data-stu-id="1fa14-232">ARM</span></span><br /><span data-ttu-id="1fa14-233">GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-233">GNU</span></span> |

#### <a name="module-linker-for-cortex-m3-using-ac5"></a><span data-ttu-id="1fa14-234">Module linker per Cortex-M3 con AC5</span><span class="sxs-lookup"><span data-stu-id="1fa14-234">Module linker for Cortex-M3 using AC5</span></span>

<span data-ttu-id="1fa14-235">Nessun file del linker di esempio specificato. il collegamento viene eseguito sulla riga di comando.</span><span class="sxs-lookup"><span data-stu-id="1fa14-235">No example linker file is provided; linking is done on the command line.</span></span> <span data-ttu-id="1fa14-236">Vedere la sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="1fa14-236">See next section.</span></span>

#### <a name="building-modules-for-cortex-m3-using-ac5"></a><span data-ttu-id="1fa14-237">Compilazione di moduli per Cortex-M3 con AC5</span><span class="sxs-lookup"><span data-stu-id="1fa14-237">Building Modules for Cortex-M3 using AC5</span></span>

<span data-ttu-id="1fa14-238">Viene fornito uno script di compilazione di esempio:</span><span class="sxs-lookup"><span data-stu-id="1fa14-238">An example build script is provided:</span></span>

```dos
armasm -g --cpu=cortex-m3 --apcs=/interwork/ropi/rwpi txm_module_preamble.S
armcc  -g --cpu=cortex-m3 -c --apcs=/interwork/ropi/rwpi --lower_ropi -I../inc -I../../../../common_modules/inc -I../../../../common_modules/module_manager/inc -I../../../../common/inc sample_threadx_module.c
armlink -d -o sample_threadx_module.axf --elf --ro=0x30000 --rw=0x40000 --first txm_module_preamble.o(Init) --entry=_txm_module_thread_shell_entry --ropi --rwpi --remove --map --symbols --list sample_threadx_module.map txm_module_preamble.o sample_threadx_module.o txm.a
```

#### <a name="thread-extension-definition-for-cortex-m3-using-ac5"></a><span data-ttu-id="1fa14-239">Definizione di estensione di thread per Cortex-M3 con AC5</span><span class="sxs-lookup"><span data-stu-id="1fa14-239">Thread extension definition for Cortex-M3 using AC5</span></span>

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

#### <a name="building-module-manager-for-cortex-m3-using-ac5"></a><span data-ttu-id="1fa14-240">Compilazione di Module Manager per Cortex-M3 con AC5</span><span class="sxs-lookup"><span data-stu-id="1fa14-240">Building Module Manager for Cortex-M3 using AC5</span></span>

<span data-ttu-id="1fa14-241">Vedere build_threadx_module_manager_demo.bat di esempio:</span><span class="sxs-lookup"><span data-stu-id="1fa14-241">See example build_threadx_module_manager_demo.bat:</span></span>

```dos
armasm -g --cpu=cortex-m3 --apcs=interwork tx_initialize_low_level.S
armcc -g --cpu=cortex-m3 -c -I../inc -I../../../../common_modules/inc -I../../../../common_modules/module_manager/inc -I../../../../common/inc sample_threadx_module_manager.c
armlink -d -o sample_threadx_module_manager.axf --elf --ro 0x00000000 --first tx_initialize_low_level.o(RESET) --remove --map --symbols --list sample_threadx_module_manager.map tx_initialize_low_level.o sample_threadx_module_manager.o tx.a
```

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m3-using-ac5"></a><span data-ttu-id="1fa14-242">Attributi per la memoria esterna Abilita API per Cortex-M3 con AC5</span><span class="sxs-lookup"><span data-stu-id="1fa14-242">Attributes for external memory enable API for Cortex-M3 using AC5</span></span>

<span data-ttu-id="1fa14-243">Il modulo dispone sempre dell'accesso in lettura alla memoria condivisa.</span><span class="sxs-lookup"><span data-stu-id="1fa14-243">Module always has read access to shared memory.</span></span>
| <span data-ttu-id="1fa14-244">Parametro attribute</span><span class="sxs-lookup"><span data-stu-id="1fa14-244">Attribute parameter</span></span> | <span data-ttu-id="1fa14-245">Significato</span><span class="sxs-lookup"><span data-stu-id="1fa14-245">Meaning</span></span> |
|---|---|
| <span data-ttu-id="1fa14-246">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span><span class="sxs-lookup"><span data-stu-id="1fa14-246">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span></span> | <span data-ttu-id="1fa14-247">Accesso in scrittura</span><span class="sxs-lookup"><span data-stu-id="1fa14-247">Write access</span></span> |

### <a name="cortex-m3-using-ac6"></a><span data-ttu-id="1fa14-248">Cortex-M3 con AC6</span><span class="sxs-lookup"><span data-stu-id="1fa14-248">Cortex-M3 using AC6</span></span>

#### <a name="module-preamble-for-cortex-m3-using-ac6"></a><span data-ttu-id="1fa14-249">Preambolo del modulo per Cortex-M3 con AC6</span><span class="sxs-lookup"><span data-stu-id="1fa14-249">Module preamble for Cortex-M3 using AC6</span></span>

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

#### <a name="module-properties-for-cortex-m3-using-ac6"></a><span data-ttu-id="1fa14-250">Proprietà dei moduli per Cortex-M3 con AC6</span><span class="sxs-lookup"><span data-stu-id="1fa14-250">Module properties for Cortex-M3 using AC6</span></span>

| <span data-ttu-id="1fa14-251">bit</span><span class="sxs-lookup"><span data-stu-id="1fa14-251">Bit</span></span> | <span data-ttu-id="1fa14-252">Valore</span><span class="sxs-lookup"><span data-stu-id="1fa14-252">Value</span></span> | <span data-ttu-id="1fa14-253">Significato</span><span class="sxs-lookup"><span data-stu-id="1fa14-253">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="1fa14-254">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-254">0</span></span> | <span data-ttu-id="1fa14-255">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-255">0</span></span><br /><span data-ttu-id="1fa14-256">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-256">1</span></span> | <span data-ttu-id="1fa14-257">Esecuzione in modalità privilegiata</span><span class="sxs-lookup"><span data-stu-id="1fa14-257">Privileged mode execution</span></span><br /><span data-ttu-id="1fa14-258">Esecuzione in modalità utente</span><span class="sxs-lookup"><span data-stu-id="1fa14-258">User mode execution</span></span> |
| <span data-ttu-id="1fa14-259">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-259">1</span></span> | <span data-ttu-id="1fa14-260">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-260">0</span></span><br /><span data-ttu-id="1fa14-261">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-261">1</span></span> | <span data-ttu-id="1fa14-262">Nessuna protezione MPU</span><span class="sxs-lookup"><span data-stu-id="1fa14-262">No MPU protection</span></span><br /><span data-ttu-id="1fa14-263">Protezione MPU (è necessario selezionare la modalità utente)</span><span class="sxs-lookup"><span data-stu-id="1fa14-263">MPU protection (must have user mode selected)</span></span> |
| <span data-ttu-id="1fa14-264">2</span><span class="sxs-lookup"><span data-stu-id="1fa14-264">2</span></span> | <span data-ttu-id="1fa14-265">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-265">0</span></span><br /><span data-ttu-id="1fa14-266">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-266">1</span></span> | <span data-ttu-id="1fa14-267">Disabilitare l'accesso alla memoria condivisa/esterna</span><span class="sxs-lookup"><span data-stu-id="1fa14-267">Disable shared/external memory access</span></span><br /><span data-ttu-id="1fa14-268">Abilitare l'accesso alla memoria condivisa/esterna</span><span class="sxs-lookup"><span data-stu-id="1fa14-268">Enable shared/external memory access</span></span> |
| <span data-ttu-id="1fa14-269">[23-3]</span><span class="sxs-lookup"><span data-stu-id="1fa14-269">[23-3]</span></span> | <span data-ttu-id="1fa14-270">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-270">0</span></span> | <span data-ttu-id="1fa14-271">Riservato</span><span class="sxs-lookup"><span data-stu-id="1fa14-271">Reserved</span></span>
| <span data-ttu-id="1fa14-272">[31-24]</span><span class="sxs-lookup"><span data-stu-id="1fa14-272">[31-24]</span></span> | <br /><span data-ttu-id="1fa14-273">0x00</span><span class="sxs-lookup"><span data-stu-id="1fa14-273">0x00</span></span><br /><span data-ttu-id="1fa14-274">0x01</span><span class="sxs-lookup"><span data-stu-id="1fa14-274">0x01</span></span><br /><span data-ttu-id="1fa14-275">0x02</span><span class="sxs-lookup"><span data-stu-id="1fa14-275">0x02</span></span> | <span data-ttu-id="1fa14-276">**ID compilatore**</span><span class="sxs-lookup"><span data-stu-id="1fa14-276">**Compiler ID**</span></span><br /><span data-ttu-id="1fa14-277">IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-277">IAR</span></span><br /><span data-ttu-id="1fa14-278">ARM</span><span class="sxs-lookup"><span data-stu-id="1fa14-278">ARM</span></span><br /><span data-ttu-id="1fa14-279">GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-279">GNU</span></span> |

#### <a name="module-linker-for-cortex-m3-using-ac6"></a><span data-ttu-id="1fa14-280">Module linker per Cortex-M3 con AC6</span><span class="sxs-lookup"><span data-stu-id="1fa14-280">Module linker for Cortex-M3 using AC6</span></span>

<span data-ttu-id="1fa14-281">Non viene usato alcun file del linker.</span><span class="sxs-lookup"><span data-stu-id="1fa14-281">No linker file is used.</span></span> <span data-ttu-id="1fa14-282">Vedere Impostazioni progetto.</span><span class="sxs-lookup"><span data-stu-id="1fa14-282">See project settings.</span></span>

#### <a name="building-modules-for-cortex-m3-using-ac6"></a><span data-ttu-id="1fa14-283">Compilazione di moduli per Cortex-M3 con AC6</span><span class="sxs-lookup"><span data-stu-id="1fa14-283">Building Modules for Cortex-M3 using AC6</span></span>

<span data-ttu-id="1fa14-284">Viene fornita un'area di lavoro di esempio.</span><span class="sxs-lookup"><span data-stu-id="1fa14-284">An example workspace is provided.</span></span> <span data-ttu-id="1fa14-285">Compilare la libreria ThreadX, la libreria di moduli ThreadX, il progetto di modulo di esempio e il progetto di gestione moduli di esempio.</span><span class="sxs-lookup"><span data-stu-id="1fa14-285">Build the ThreadX library, ThreadX Modules library, sample module project, and sample module manager project.</span></span>

#### <a name="thread-extension-definition-for-cortex-m3-using-ac6"></a><span data-ttu-id="1fa14-286">Definizione di estensione di thread per Cortex-M3 con AC6</span><span class="sxs-lookup"><span data-stu-id="1fa14-286">Thread extension definition for Cortex-M3 using AC6</span></span>

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

#### <a name="building-module-manager-for-cortex-m3-using-ac6"></a><span data-ttu-id="1fa14-287">Compilazione di Module Manager per Cortex-M3 con AC6</span><span class="sxs-lookup"><span data-stu-id="1fa14-287">Building Module Manager for Cortex-M3 using AC6</span></span>

<span data-ttu-id="1fa14-288">Viene fornita un'area di lavoro di esempio.</span><span class="sxs-lookup"><span data-stu-id="1fa14-288">An example workspace is provided.</span></span> <span data-ttu-id="1fa14-289">Compilare la libreria ThreadX, la libreria di moduli ThreadX, il progetto di modulo di esempio e il progetto di gestione moduli di esempio.</span><span class="sxs-lookup"><span data-stu-id="1fa14-289">Build the ThreadX library, ThreadX Modules library, sample module project, and sample module manager project.</span></span>

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m3-using-ac6"></a><span data-ttu-id="1fa14-290">Attributi per la memoria esterna Abilita API per Cortex-M3 con AC6</span><span class="sxs-lookup"><span data-stu-id="1fa14-290">Attributes for external memory enable API for Cortex-M3 using AC6</span></span>

<span data-ttu-id="1fa14-291">Il modulo dispone sempre dell'accesso in lettura alla memoria condivisa.</span><span class="sxs-lookup"><span data-stu-id="1fa14-291">Module always has read access to shared memory.</span></span>
| <span data-ttu-id="1fa14-292">Parametro attribute</span><span class="sxs-lookup"><span data-stu-id="1fa14-292">Attribute parameter</span></span> | <span data-ttu-id="1fa14-293">Significato</span><span class="sxs-lookup"><span data-stu-id="1fa14-293">Meaning</span></span> |
|---|---|
| <span data-ttu-id="1fa14-294">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span><span class="sxs-lookup"><span data-stu-id="1fa14-294">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span></span> | <span data-ttu-id="1fa14-295">Accesso in scrittura</span><span class="sxs-lookup"><span data-stu-id="1fa14-295">Write access</span></span> |

### <a name="cortex-m3-using-gnu"></a><span data-ttu-id="1fa14-296">Cortex-M3 con GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-296">Cortex-M3 using GNU</span></span>

#### <a name="module-preamble-for-cortex-m3-using-gnu"></a><span data-ttu-id="1fa14-297">Preambolo del modulo per Cortex-M3 con GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-297">Module preamble for Cortex-M3 using GNU</span></span>

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

#### <a name="module-properties-for-cortex-m3-using-gnu"></a><span data-ttu-id="1fa14-298">Proprietà dei moduli per Cortex-M3 con GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-298">Module properties for Cortex-M3 using GNU</span></span>

| <span data-ttu-id="1fa14-299">bit</span><span class="sxs-lookup"><span data-stu-id="1fa14-299">Bit</span></span> | <span data-ttu-id="1fa14-300">Valore</span><span class="sxs-lookup"><span data-stu-id="1fa14-300">Value</span></span> | <span data-ttu-id="1fa14-301">Significato</span><span class="sxs-lookup"><span data-stu-id="1fa14-301">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="1fa14-302">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-302">0</span></span> | <span data-ttu-id="1fa14-303">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-303">0</span></span><br /><span data-ttu-id="1fa14-304">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-304">1</span></span> | <span data-ttu-id="1fa14-305">Esecuzione in modalità privilegiata</span><span class="sxs-lookup"><span data-stu-id="1fa14-305">Privileged mode execution</span></span><br /><span data-ttu-id="1fa14-306">Esecuzione in modalità utente</span><span class="sxs-lookup"><span data-stu-id="1fa14-306">User mode execution</span></span> |
| <span data-ttu-id="1fa14-307">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-307">1</span></span> | <span data-ttu-id="1fa14-308">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-308">0</span></span><br /><span data-ttu-id="1fa14-309">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-309">1</span></span> | <span data-ttu-id="1fa14-310">Nessuna protezione MPU</span><span class="sxs-lookup"><span data-stu-id="1fa14-310">No MPU protection</span></span><br /><span data-ttu-id="1fa14-311">Protezione MPU (è necessario selezionare la modalità utente)</span><span class="sxs-lookup"><span data-stu-id="1fa14-311">MPU protection (must have user mode selected)</span></span> |
| <span data-ttu-id="1fa14-312">2</span><span class="sxs-lookup"><span data-stu-id="1fa14-312">2</span></span> | <span data-ttu-id="1fa14-313">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-313">0</span></span><br /><span data-ttu-id="1fa14-314">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-314">1</span></span> | <span data-ttu-id="1fa14-315">Disabilitare l'accesso alla memoria condivisa/esterna</span><span class="sxs-lookup"><span data-stu-id="1fa14-315">Disable shared/external memory access</span></span><br /><span data-ttu-id="1fa14-316">Abilitare l'accesso alla memoria condivisa/esterna</span><span class="sxs-lookup"><span data-stu-id="1fa14-316">Enable shared/external memory access</span></span> |
| <span data-ttu-id="1fa14-317">[23-3]</span><span class="sxs-lookup"><span data-stu-id="1fa14-317">[23-3]</span></span> | <span data-ttu-id="1fa14-318">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-318">0</span></span> | <span data-ttu-id="1fa14-319">Riservato</span><span class="sxs-lookup"><span data-stu-id="1fa14-319">Reserved</span></span>
| <span data-ttu-id="1fa14-320">[31-24]</span><span class="sxs-lookup"><span data-stu-id="1fa14-320">[31-24]</span></span> | <br /><span data-ttu-id="1fa14-321">0x00</span><span class="sxs-lookup"><span data-stu-id="1fa14-321">0x00</span></span><br /><span data-ttu-id="1fa14-322">0x01</span><span class="sxs-lookup"><span data-stu-id="1fa14-322">0x01</span></span><br /><span data-ttu-id="1fa14-323">0x02</span><span class="sxs-lookup"><span data-stu-id="1fa14-323">0x02</span></span> | <span data-ttu-id="1fa14-324">**ID compilatore**</span><span class="sxs-lookup"><span data-stu-id="1fa14-324">**Compiler ID**</span></span><br /><span data-ttu-id="1fa14-325">IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-325">IAR</span></span><br /><span data-ttu-id="1fa14-326">ARM</span><span class="sxs-lookup"><span data-stu-id="1fa14-326">ARM</span></span><br /><span data-ttu-id="1fa14-327">GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-327">GNU</span></span> |

#### <a name="module-linker-for-cortex-m3-using-gnu"></a><span data-ttu-id="1fa14-328">Module linker per Cortex-M3 con GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-328">Module linker for Cortex-M3 using GNU</span></span>

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

#### <a name="building-modules-for-cortex-m3-using-gnu"></a><span data-ttu-id="1fa14-329">Compilazione di moduli per Cortex-M3 con GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-329">Building Modules for Cortex-M3 using GNU</span></span>

<span data-ttu-id="1fa14-330">Vedere build_threadx_module_sample.bat:</span><span class="sxs-lookup"><span data-stu-id="1fa14-330">See build_threadx_module_sample.bat:</span></span>

```dos
arm-none-eabi-gcc -c -g -mcpu=cortex-m3 -fpie -fno-plt -mpic-data-is-text-relative -msingle-pic-base txm_module_preamble.s
arm-none-eabi-gcc -c -g -mcpu=cortex-m3 -fpie -fno-plt -mpic-data-is-text-relative -msingle-pic-base gcc_setup.S
arm-none-eabi-gcc -c -g -mcpu=cortex-m3 -fpie -fno-plt -mpic-data-is-text-relative -msingle-pic-base -I..\inc -I..\..\..\..\common\inc -I..\..\..\..\common_modules\inc sample_threadx_module.c
arm-none-eabi-ld -A cortex-m3 -T sample_threadx_module.ld txm_module_preamble.o gcc_setup.o sample_threadx_module.o -e _txm_module_thread_shell_entry txm.a -o sample_threadx_module.axf -M > sample_threadx_module.map
```

#### <a name="thread-extension-definition-for-cortex-m3-using-gnu"></a><span data-ttu-id="1fa14-331">Definizione di estensione di thread per Cortex-M3 con GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-331">Thread extension definition for Cortex-M3 using GNU</span></span>

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

#### <a name="building-module-manager-for-cortex-m3-using-gnu"></a><span data-ttu-id="1fa14-332">Compilazione di gestione moduli per Cortex-M3 con GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-332">Building Module Manager for Cortex-M3 using GNU</span></span>

<span data-ttu-id="1fa14-333">Vedere build_threadx_module_manager_sample.bat:</span><span class="sxs-lookup"><span data-stu-id="1fa14-333">See build_threadx_module_manager_sample.bat:</span></span>

```dos
arm-none-eabi-gcc -c -g -mcpu=cortex-m3 -mthumb -I..\inc -I..\..\..\..\common\inc -I..\..\..\..\common_modules\inc sample_threadx_module_manager.c
arm-none-eabi-gcc -c -g -mcpu=cortex-m3 -mthumb tx_simulator_startup.S
arm-none-eabi-gcc -c -g -mcpu=cortex-m3 -mthumb cortexm_crt0.S
arm-none-eabi-ld -A cortex-m3 -ereset_handler -T sample_threadx.ld tx_simulator_startup.o cortexm_crt0.o sample_threadx_module_manager.o tx.a  libc.a -o sample_threadx_module_manager.axf -M > sample_threadx_module_manager.map
```

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m3-using-gnu"></a><span data-ttu-id="1fa14-334">Attributi per la memoria esterna Abilita API per Cortex-M3 con GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-334">Attributes for external memory enable API for Cortex-M3 using GNU</span></span>

<span data-ttu-id="1fa14-335">Il modulo dispone sempre dell'accesso in lettura alla memoria condivisa.</span><span class="sxs-lookup"><span data-stu-id="1fa14-335">Module always has read access to shared memory.</span></span>
| <span data-ttu-id="1fa14-336">Parametro attribute</span><span class="sxs-lookup"><span data-stu-id="1fa14-336">Attribute parameter</span></span> | <span data-ttu-id="1fa14-337">Significato</span><span class="sxs-lookup"><span data-stu-id="1fa14-337">Meaning</span></span> |
|---|---|
| <span data-ttu-id="1fa14-338">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span><span class="sxs-lookup"><span data-stu-id="1fa14-338">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span></span> | <span data-ttu-id="1fa14-339">Accesso in scrittura</span><span class="sxs-lookup"><span data-stu-id="1fa14-339">Write access</span></span> |

### <a name="cortex-m3-using-iar"></a><span data-ttu-id="1fa14-340">Cortex-M3 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-340">Cortex-M3 using IAR</span></span>

#### <a name="module-preamble-for-cortex-m3-using-iar"></a><span data-ttu-id="1fa14-341">Preambolo del modulo per Cortex-M3 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-341">Module preamble for Cortex-M3 using IAR</span></span>

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

#### <a name="module-properties-for-cortex-m3-using-iar"></a><span data-ttu-id="1fa14-342">Proprietà dei moduli per Cortex-M3 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-342">Module properties for Cortex-M3 using IAR</span></span>

| <span data-ttu-id="1fa14-343">bit</span><span class="sxs-lookup"><span data-stu-id="1fa14-343">Bit</span></span> | <span data-ttu-id="1fa14-344">Valore</span><span class="sxs-lookup"><span data-stu-id="1fa14-344">Value</span></span> | <span data-ttu-id="1fa14-345">Significato</span><span class="sxs-lookup"><span data-stu-id="1fa14-345">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="1fa14-346">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-346">0</span></span> | <span data-ttu-id="1fa14-347">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-347">0</span></span><br /><span data-ttu-id="1fa14-348">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-348">1</span></span> | <span data-ttu-id="1fa14-349">Esecuzione in modalità privilegiata</span><span class="sxs-lookup"><span data-stu-id="1fa14-349">Privileged mode execution</span></span><br /><span data-ttu-id="1fa14-350">Esecuzione in modalità utente</span><span class="sxs-lookup"><span data-stu-id="1fa14-350">User mode execution</span></span> |
| <span data-ttu-id="1fa14-351">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-351">1</span></span> | <span data-ttu-id="1fa14-352">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-352">0</span></span><br /><span data-ttu-id="1fa14-353">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-353">1</span></span> | <span data-ttu-id="1fa14-354">Nessuna protezione MPU</span><span class="sxs-lookup"><span data-stu-id="1fa14-354">No MPU protection</span></span><br /><span data-ttu-id="1fa14-355">Protezione MPU (è necessario selezionare la modalità utente)</span><span class="sxs-lookup"><span data-stu-id="1fa14-355">MPU protection (must have user mode selected)</span></span> |
| <span data-ttu-id="1fa14-356">2</span><span class="sxs-lookup"><span data-stu-id="1fa14-356">2</span></span> | <span data-ttu-id="1fa14-357">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-357">0</span></span><br /><span data-ttu-id="1fa14-358">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-358">1</span></span> | <span data-ttu-id="1fa14-359">Disabilitare l'accesso alla memoria condivisa/esterna</span><span class="sxs-lookup"><span data-stu-id="1fa14-359">Disable shared/external memory access</span></span><br /><span data-ttu-id="1fa14-360">Abilitare l'accesso alla memoria condivisa/esterna</span><span class="sxs-lookup"><span data-stu-id="1fa14-360">Enable shared/external memory access</span></span> |
| <span data-ttu-id="1fa14-361">[23-3]</span><span class="sxs-lookup"><span data-stu-id="1fa14-361">[23-3]</span></span> | <span data-ttu-id="1fa14-362">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-362">0</span></span> | <span data-ttu-id="1fa14-363">Riservato</span><span class="sxs-lookup"><span data-stu-id="1fa14-363">Reserved</span></span>
| <span data-ttu-id="1fa14-364">[31-24]</span><span class="sxs-lookup"><span data-stu-id="1fa14-364">[31-24]</span></span> | <br /><span data-ttu-id="1fa14-365">0x00</span><span class="sxs-lookup"><span data-stu-id="1fa14-365">0x00</span></span><br /><span data-ttu-id="1fa14-366">0x01</span><span class="sxs-lookup"><span data-stu-id="1fa14-366">0x01</span></span><br /><span data-ttu-id="1fa14-367">0x02</span><span class="sxs-lookup"><span data-stu-id="1fa14-367">0x02</span></span> | <span data-ttu-id="1fa14-368">**ID compilatore**</span><span class="sxs-lookup"><span data-stu-id="1fa14-368">**Compiler ID**</span></span><br /><span data-ttu-id="1fa14-369">IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-369">IAR</span></span><br /><span data-ttu-id="1fa14-370">ARM</span><span class="sxs-lookup"><span data-stu-id="1fa14-370">ARM</span></span><br /><span data-ttu-id="1fa14-371">GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-371">GNU</span></span> |

#### <a name="module-linker-for-cortex-m3-using-iar"></a><span data-ttu-id="1fa14-372">Module linker per Cortex-M3 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-372">Module linker for Cortex-M3 using IAR</span></span>

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

#### <a name="building-modules-for-cortex-m3-using-iar"></a><span data-ttu-id="1fa14-373">Compilazione di moduli per Cortex-M3 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-373">Building Modules for Cortex-M3 using IAR</span></span>

<span data-ttu-id="1fa14-374">Viene fornita un'area di lavoro di esempio.</span><span class="sxs-lookup"><span data-stu-id="1fa14-374">An example workspace is provided.</span></span> <span data-ttu-id="1fa14-375">Compilare la libreria ThreadX, la libreria di moduli ThreadX, il progetto del modulo demo e il progetto di gestione moduli dimostrativi.</span><span class="sxs-lookup"><span data-stu-id="1fa14-375">Build the ThreadX library, ThreadX Modules library, demo module project, and demo module manager project.</span></span>

#### <a name="thread-extension-definition-for-cortex-m3-using-iar"></a><span data-ttu-id="1fa14-376">Definizione dell'estensione di thread per Cortex-M3 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-376">Thread extension definition for Cortex-M3 using IAR</span></span>

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

#### <a name="building-module-manager-for-cortex-m3-using-iar"></a><span data-ttu-id="1fa14-377">Compilazione di Module Manager per Cortex-M3 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-377">Building Module Manager for Cortex-M3 using IAR</span></span>

<span data-ttu-id="1fa14-378">Viene fornita un'area di lavoro di esempio.</span><span class="sxs-lookup"><span data-stu-id="1fa14-378">An example workspace is provided.</span></span> <span data-ttu-id="1fa14-379">Compilare la libreria ThreadX, la libreria di moduli ThreadX, il progetto del modulo demo e il progetto di gestione moduli dimostrativi.</span><span class="sxs-lookup"><span data-stu-id="1fa14-379">Build the ThreadX library, ThreadX Modules library, demo module project, and demo module manager project.</span></span>

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m3-using-iar"></a><span data-ttu-id="1fa14-380">Attributi per la memoria esterna Abilita API per Cortex-M3 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-380">Attributes for external memory enable API for Cortex-M3 using IAR</span></span>

<span data-ttu-id="1fa14-381">Il modulo dispone sempre dell'accesso in lettura alla memoria condivisa.</span><span class="sxs-lookup"><span data-stu-id="1fa14-381">Module always has read access to shared memory.</span></span>
| <span data-ttu-id="1fa14-382">Parametro attribute</span><span class="sxs-lookup"><span data-stu-id="1fa14-382">Attribute parameter</span></span> | <span data-ttu-id="1fa14-383">Significato</span><span class="sxs-lookup"><span data-stu-id="1fa14-383">Meaning</span></span> |
|---|---|
| <span data-ttu-id="1fa14-384">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span><span class="sxs-lookup"><span data-stu-id="1fa14-384">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span></span> | <span data-ttu-id="1fa14-385">Accesso in scrittura</span><span class="sxs-lookup"><span data-stu-id="1fa14-385">Write access</span></span> |

## <a name="cortex-m33-processor"></a><span data-ttu-id="1fa14-386">Processore Cortex-M33</span><span class="sxs-lookup"><span data-stu-id="1fa14-386">Cortex-M33 processor</span></span>

### <a name="cortex-m33-using-ac6"></a><span data-ttu-id="1fa14-387">Cortex-M33 con AC6</span><span class="sxs-lookup"><span data-stu-id="1fa14-387">Cortex-M33 using AC6</span></span>

#### <a name="module-preamble-for-cortex-m33-using-ac6"></a><span data-ttu-id="1fa14-388">Preambolo del modulo per Cortex-M33 con AC6</span><span class="sxs-lookup"><span data-stu-id="1fa14-388">Module preamble for Cortex-M33 using AC6</span></span>

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

#### <a name="module-properties-for-cortex-m33-using-ac6"></a><span data-ttu-id="1fa14-389">Proprietà dei moduli per Cortex-M33 con AC6</span><span class="sxs-lookup"><span data-stu-id="1fa14-389">Module properties for Cortex-M33 using AC6</span></span>

| <span data-ttu-id="1fa14-390">bit</span><span class="sxs-lookup"><span data-stu-id="1fa14-390">Bit</span></span> | <span data-ttu-id="1fa14-391">Valore</span><span class="sxs-lookup"><span data-stu-id="1fa14-391">Value</span></span> | <span data-ttu-id="1fa14-392">Significato</span><span class="sxs-lookup"><span data-stu-id="1fa14-392">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="1fa14-393">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-393">0</span></span> | <span data-ttu-id="1fa14-394">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-394">0</span></span><br /><span data-ttu-id="1fa14-395">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-395">1</span></span> | <span data-ttu-id="1fa14-396">Esecuzione in modalità privilegiata</span><span class="sxs-lookup"><span data-stu-id="1fa14-396">Privileged mode execution</span></span><br /><span data-ttu-id="1fa14-397">Esecuzione in modalità utente</span><span class="sxs-lookup"><span data-stu-id="1fa14-397">User mode execution</span></span> |
| <span data-ttu-id="1fa14-398">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-398">1</span></span> | <span data-ttu-id="1fa14-399">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-399">0</span></span><br /><span data-ttu-id="1fa14-400">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-400">1</span></span> | <span data-ttu-id="1fa14-401">Nessuna protezione MPU</span><span class="sxs-lookup"><span data-stu-id="1fa14-401">No MPU protection</span></span><br /><span data-ttu-id="1fa14-402">Protezione MPU (è necessario selezionare la modalità utente)</span><span class="sxs-lookup"><span data-stu-id="1fa14-402">MPU protection (must have user mode selected)</span></span> |
| <span data-ttu-id="1fa14-403">2</span><span class="sxs-lookup"><span data-stu-id="1fa14-403">2</span></span> | <span data-ttu-id="1fa14-404">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-404">0</span></span><br /><span data-ttu-id="1fa14-405">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-405">1</span></span> | <span data-ttu-id="1fa14-406">Disabilitare l'accesso alla memoria condivisa/esterna</span><span class="sxs-lookup"><span data-stu-id="1fa14-406">Disable shared/external memory access</span></span><br /><span data-ttu-id="1fa14-407">Abilitare l'accesso alla memoria condivisa/esterna</span><span class="sxs-lookup"><span data-stu-id="1fa14-407">Enable shared/external memory access</span></span> |
| <span data-ttu-id="1fa14-408">[23-3]</span><span class="sxs-lookup"><span data-stu-id="1fa14-408">[23-3]</span></span> | <span data-ttu-id="1fa14-409">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-409">0</span></span> | <span data-ttu-id="1fa14-410">Riservato</span><span class="sxs-lookup"><span data-stu-id="1fa14-410">Reserved</span></span>
| <span data-ttu-id="1fa14-411">[31-24]</span><span class="sxs-lookup"><span data-stu-id="1fa14-411">[31-24]</span></span> | <br /><span data-ttu-id="1fa14-412">0x00</span><span class="sxs-lookup"><span data-stu-id="1fa14-412">0x00</span></span><br /><span data-ttu-id="1fa14-413">0x01</span><span class="sxs-lookup"><span data-stu-id="1fa14-413">0x01</span></span><br /><span data-ttu-id="1fa14-414">0x02</span><span class="sxs-lookup"><span data-stu-id="1fa14-414">0x02</span></span> | <span data-ttu-id="1fa14-415">**ID compilatore**</span><span class="sxs-lookup"><span data-stu-id="1fa14-415">**Compiler ID**</span></span><br /><span data-ttu-id="1fa14-416">IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-416">IAR</span></span><br /><span data-ttu-id="1fa14-417">ARM</span><span class="sxs-lookup"><span data-stu-id="1fa14-417">ARM</span></span><br /><span data-ttu-id="1fa14-418">GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-418">GNU</span></span> |

#### <a name="module-linker-for-cortex-m33-using-ac6"></a><span data-ttu-id="1fa14-419">Module linker per Cortex-M33 con AC6</span><span class="sxs-lookup"><span data-stu-id="1fa14-419">Module linker for Cortex-M33 using AC6</span></span>

<span data-ttu-id="1fa14-420">Non è necessario alcun file del linker per la Keil.</span><span class="sxs-lookup"><span data-stu-id="1fa14-420">No linker file needed for Keil toolchain.</span></span> <span data-ttu-id="1fa14-421">Vedere Impostazioni di compilazione nel progetto di esempio.</span><span class="sxs-lookup"><span data-stu-id="1fa14-421">See build settings in example project.</span></span>
<span data-ttu-id="1fa14-422">Di seguito sono elencate le opzioni importanti del linker:</span><span class="sxs-lookup"><span data-stu-id="1fa14-422">Important linker options are listed below:</span></span>

```c
--entry demo_module_start --first __txm_module_preamble
```

#### <a name="building-modules-for-cortex-m33-using-ac6"></a><span data-ttu-id="1fa14-423">Compilazione di moduli per Cortex-M33 con AC6</span><span class="sxs-lookup"><span data-stu-id="1fa14-423">Building Modules for Cortex-M33 using AC6</span></span>

<span data-ttu-id="1fa14-424">Impostazioni del compilatore:</span><span class="sxs-lookup"><span data-stu-id="1fa14-424">Compiler settings:</span></span>

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

#### <a name="thread-extension-definition-for-cortex-m33-using-ac6"></a><span data-ttu-id="1fa14-425">Definizione di estensione di thread per Cortex-M33 con AC6</span><span class="sxs-lookup"><span data-stu-id="1fa14-425">Thread extension definition for Cortex-M33 using AC6</span></span>

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

#### <a name="building-module-manager-for-cortex-m33-using-ac6"></a><span data-ttu-id="1fa14-426">Compilazione di Module Manager per Cortex-M33 con AC6</span><span class="sxs-lookup"><span data-stu-id="1fa14-426">Building Module Manager for Cortex-M33 using AC6</span></span>

<span data-ttu-id="1fa14-427">Viene fornita un'area di lavoro di esempio.</span><span class="sxs-lookup"><span data-stu-id="1fa14-427">An example workspace is provided.</span></span> <span data-ttu-id="1fa14-428">Compilare la libreria ThreadX, la libreria ThreadX Modules, il progetto sample_threadx_module e il progetto demo_threadx_non-secure_zone.</span><span class="sxs-lookup"><span data-stu-id="1fa14-428">Build the ThreadX library, ThreadX Modules library, sample_threadx_module project, and demo_threadx_non-secure_zone project.</span></span>

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m33-using-ac6"></a><span data-ttu-id="1fa14-429">Attributi per la memoria esterna Abilita API per Cortex-M33 con AC6</span><span class="sxs-lookup"><span data-stu-id="1fa14-429">Attributes for external memory enable API for Cortex-M33 using AC6</span></span>

| <span data-ttu-id="1fa14-430">Parametro attribute</span><span class="sxs-lookup"><span data-stu-id="1fa14-430">Attribute parameter</span></span> |
|---|
| <span data-ttu-id="1fa14-431">TXM_MODULE_ATTRIBUTE_NON_SHAREABLE</span><span class="sxs-lookup"><span data-stu-id="1fa14-431">TXM_MODULE_ATTRIBUTE_NON_SHAREABLE</span></span> |
| <span data-ttu-id="1fa14-432">TXM_MODULE_ATTRIBUTE_OUTER_SHAREABLE</span><span class="sxs-lookup"><span data-stu-id="1fa14-432">TXM_MODULE_ATTRIBUTE_OUTER_SHAREABLE</span></span> |
| <span data-ttu-id="1fa14-433">TXM_MODULE_ATTRIBUTE_INNER_SHAREABLE</span><span class="sxs-lookup"><span data-stu-id="1fa14-433">TXM_MODULE_ATTRIBUTE_INNER_SHAREABLE</span></span> |
| <span data-ttu-id="1fa14-434">TXM_MODULE_ATTRIBUTE_READ_WRITE</span><span class="sxs-lookup"><span data-stu-id="1fa14-434">TXM_MODULE_ATTRIBUTE_READ_WRITE</span></span> |
| <span data-ttu-id="1fa14-435">TXM_MODULE_ATTRIBUTE_READ_ONLY</span><span class="sxs-lookup"><span data-stu-id="1fa14-435">TXM_MODULE_ATTRIBUTE_READ_ONLY</span></span> |

### <a name="cortex-m33-using-gnu"></a><span data-ttu-id="1fa14-436">Cortex-M33 con GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-436">Cortex-M33 using GNU</span></span>

#### <a name="module-preamble-for-cortex-m33-using-gnu"></a><span data-ttu-id="1fa14-437">Preambolo del modulo per Cortex-M33 con GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-437">Module preamble for Cortex-M33 using GNU</span></span>

#### <a name="module-properties-for-cortex-m33-using-gnu"></a><span data-ttu-id="1fa14-438">Proprietà dei moduli per Cortex-M33 con GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-438">Module properties for Cortex-M33 using GNU</span></span>

| <span data-ttu-id="1fa14-439">bit</span><span class="sxs-lookup"><span data-stu-id="1fa14-439">Bit</span></span> | <span data-ttu-id="1fa14-440">Valore</span><span class="sxs-lookup"><span data-stu-id="1fa14-440">Value</span></span> | <span data-ttu-id="1fa14-441">Significato</span><span class="sxs-lookup"><span data-stu-id="1fa14-441">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="1fa14-442">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-442">0</span></span> | <span data-ttu-id="1fa14-443">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-443">0</span></span><br /><span data-ttu-id="1fa14-444">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-444">1</span></span> | <span data-ttu-id="1fa14-445">Esecuzione in modalità privilegiata</span><span class="sxs-lookup"><span data-stu-id="1fa14-445">Privileged mode execution</span></span><br /><span data-ttu-id="1fa14-446">Esecuzione in modalità utente</span><span class="sxs-lookup"><span data-stu-id="1fa14-446">User mode execution</span></span> |
| <span data-ttu-id="1fa14-447">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-447">1</span></span> | <span data-ttu-id="1fa14-448">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-448">0</span></span><br /><span data-ttu-id="1fa14-449">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-449">1</span></span> | <span data-ttu-id="1fa14-450">Nessuna protezione MPU</span><span class="sxs-lookup"><span data-stu-id="1fa14-450">No MPU protection</span></span><br /><span data-ttu-id="1fa14-451">Protezione MPU (è necessario selezionare la modalità utente)</span><span class="sxs-lookup"><span data-stu-id="1fa14-451">MPU protection (must have user mode selected)</span></span> |
| <span data-ttu-id="1fa14-452">2</span><span class="sxs-lookup"><span data-stu-id="1fa14-452">2</span></span> | <span data-ttu-id="1fa14-453">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-453">0</span></span><br /><span data-ttu-id="1fa14-454">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-454">1</span></span> | <span data-ttu-id="1fa14-455">Disabilitare l'accesso alla memoria condivisa/esterna</span><span class="sxs-lookup"><span data-stu-id="1fa14-455">Disable shared/external memory access</span></span><br /><span data-ttu-id="1fa14-456">Abilitare l'accesso alla memoria condivisa/esterna</span><span class="sxs-lookup"><span data-stu-id="1fa14-456">Enable shared/external memory access</span></span> |
| <span data-ttu-id="1fa14-457">[23-3]</span><span class="sxs-lookup"><span data-stu-id="1fa14-457">[23-3]</span></span> | <span data-ttu-id="1fa14-458">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-458">0</span></span> | <span data-ttu-id="1fa14-459">Riservato</span><span class="sxs-lookup"><span data-stu-id="1fa14-459">Reserved</span></span>
| <span data-ttu-id="1fa14-460">[31-24]</span><span class="sxs-lookup"><span data-stu-id="1fa14-460">[31-24]</span></span> | <br /><span data-ttu-id="1fa14-461">0x00</span><span class="sxs-lookup"><span data-stu-id="1fa14-461">0x00</span></span><br /><span data-ttu-id="1fa14-462">0x01</span><span class="sxs-lookup"><span data-stu-id="1fa14-462">0x01</span></span><br /><span data-ttu-id="1fa14-463">0x02</span><span class="sxs-lookup"><span data-stu-id="1fa14-463">0x02</span></span> | <span data-ttu-id="1fa14-464">**ID compilatore**</span><span class="sxs-lookup"><span data-stu-id="1fa14-464">**Compiler ID**</span></span><br /><span data-ttu-id="1fa14-465">IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-465">IAR</span></span><br /><span data-ttu-id="1fa14-466">ARM</span><span class="sxs-lookup"><span data-stu-id="1fa14-466">ARM</span></span><br /><span data-ttu-id="1fa14-467">GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-467">GNU</span></span> |

#### <a name="module-linker-for-cortex-m33-using-gnu"></a><span data-ttu-id="1fa14-468">Module linker per Cortex-M33 con GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-468">Module linker for Cortex-M33 using GNU</span></span>

#### <a name="building-modules-for-cortex-m33-using-gnu"></a><span data-ttu-id="1fa14-469">Compilazione di moduli per Cortex-M33 con GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-469">Building Modules for Cortex-M33 using GNU</span></span>

#### <a name="thread-extension-definition-for-cortex-m33-using-gnu"></a><span data-ttu-id="1fa14-470">Definizione di estensione di thread per Cortex-M33 con GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-470">Thread extension definition for Cortex-M33 using GNU</span></span>

#### <a name="building-module-manager-for-cortex-m33-using-gnu"></a><span data-ttu-id="1fa14-471">Compilazione di Module Manager per Cortex-M33 con GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-471">Building Module Manager for Cortex-M33 using GNU</span></span>

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m33-using-gnu"></a><span data-ttu-id="1fa14-472">Attributi per la memoria esterna Abilita API per Cortex-M33 con GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-472">Attributes for external memory enable API for Cortex-M33 using GNU</span></span>

| <span data-ttu-id="1fa14-473">Parametro attribute</span><span class="sxs-lookup"><span data-stu-id="1fa14-473">Attribute parameter</span></span> |
|---|
| <span data-ttu-id="1fa14-474">TXM_MODULE_ATTRIBUTE_NON_SHAREABLE</span><span class="sxs-lookup"><span data-stu-id="1fa14-474">TXM_MODULE_ATTRIBUTE_NON_SHAREABLE</span></span> |
| <span data-ttu-id="1fa14-475">TXM_MODULE_ATTRIBUTE_OUTER_SHAREABLE</span><span class="sxs-lookup"><span data-stu-id="1fa14-475">TXM_MODULE_ATTRIBUTE_OUTER_SHAREABLE</span></span> |
| <span data-ttu-id="1fa14-476">TXM_MODULE_ATTRIBUTE_INNER_SHAREABLE</span><span class="sxs-lookup"><span data-stu-id="1fa14-476">TXM_MODULE_ATTRIBUTE_INNER_SHAREABLE</span></span> |
| <span data-ttu-id="1fa14-477">TXM_MODULE_ATTRIBUTE_READ_WRITE</span><span class="sxs-lookup"><span data-stu-id="1fa14-477">TXM_MODULE_ATTRIBUTE_READ_WRITE</span></span> |
| <span data-ttu-id="1fa14-478">TXM_MODULE_ATTRIBUTE_READ_ONLY</span><span class="sxs-lookup"><span data-stu-id="1fa14-478">TXM_MODULE_ATTRIBUTE_READ_ONLY</span></span> |

### <a name="cortex-m33-using-iar"></a><span data-ttu-id="1fa14-479">Cortex-M33 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-479">Cortex-M33 using IAR</span></span>

#### <a name="module-preamble-for-cortex-m33-using-iar"></a><span data-ttu-id="1fa14-480">Preambolo del modulo per Cortex-M33 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-480">Module preamble for Cortex-M33 using IAR</span></span>

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

#### <a name="module-properties-for-cortex-m33-using-iar"></a><span data-ttu-id="1fa14-481">Proprietà dei moduli per Cortex-M33 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-481">Module properties for Cortex-M33 using IAR</span></span>

| <span data-ttu-id="1fa14-482">bit</span><span class="sxs-lookup"><span data-stu-id="1fa14-482">Bit</span></span> | <span data-ttu-id="1fa14-483">Valore</span><span class="sxs-lookup"><span data-stu-id="1fa14-483">Value</span></span> | <span data-ttu-id="1fa14-484">Significato</span><span class="sxs-lookup"><span data-stu-id="1fa14-484">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="1fa14-485">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-485">0</span></span> | <span data-ttu-id="1fa14-486">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-486">0</span></span><br /><span data-ttu-id="1fa14-487">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-487">1</span></span> | <span data-ttu-id="1fa14-488">Esecuzione in modalità privilegiata</span><span class="sxs-lookup"><span data-stu-id="1fa14-488">Privileged mode execution</span></span><br /><span data-ttu-id="1fa14-489">Esecuzione in modalità utente</span><span class="sxs-lookup"><span data-stu-id="1fa14-489">User mode execution</span></span> |
| <span data-ttu-id="1fa14-490">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-490">1</span></span> | <span data-ttu-id="1fa14-491">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-491">0</span></span><br /><span data-ttu-id="1fa14-492">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-492">1</span></span> | <span data-ttu-id="1fa14-493">Nessuna protezione MPU</span><span class="sxs-lookup"><span data-stu-id="1fa14-493">No MPU protection</span></span><br /><span data-ttu-id="1fa14-494">Protezione MPU (è necessario selezionare la modalità utente)</span><span class="sxs-lookup"><span data-stu-id="1fa14-494">MPU protection (must have user mode selected)</span></span> |
| <span data-ttu-id="1fa14-495">2</span><span class="sxs-lookup"><span data-stu-id="1fa14-495">2</span></span> | <span data-ttu-id="1fa14-496">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-496">0</span></span><br /><span data-ttu-id="1fa14-497">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-497">1</span></span> | <span data-ttu-id="1fa14-498">Disabilitare l'accesso alla memoria condivisa/esterna</span><span class="sxs-lookup"><span data-stu-id="1fa14-498">Disable shared/external memory access</span></span><br /><span data-ttu-id="1fa14-499">Abilitare l'accesso alla memoria condivisa/esterna</span><span class="sxs-lookup"><span data-stu-id="1fa14-499">Enable shared/external memory access</span></span> |
| <span data-ttu-id="1fa14-500">[23-3]</span><span class="sxs-lookup"><span data-stu-id="1fa14-500">[23-3]</span></span> | <span data-ttu-id="1fa14-501">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-501">0</span></span> | <span data-ttu-id="1fa14-502">Riservato</span><span class="sxs-lookup"><span data-stu-id="1fa14-502">Reserved</span></span>
| <span data-ttu-id="1fa14-503">[31-24]</span><span class="sxs-lookup"><span data-stu-id="1fa14-503">[31-24]</span></span> | <br /><span data-ttu-id="1fa14-504">0x00</span><span class="sxs-lookup"><span data-stu-id="1fa14-504">0x00</span></span><br /><span data-ttu-id="1fa14-505">0x01</span><span class="sxs-lookup"><span data-stu-id="1fa14-505">0x01</span></span><br /><span data-ttu-id="1fa14-506">0x02</span><span class="sxs-lookup"><span data-stu-id="1fa14-506">0x02</span></span> | <span data-ttu-id="1fa14-507">**ID compilatore**</span><span class="sxs-lookup"><span data-stu-id="1fa14-507">**Compiler ID**</span></span><br /><span data-ttu-id="1fa14-508">IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-508">IAR</span></span><br /><span data-ttu-id="1fa14-509">ARM</span><span class="sxs-lookup"><span data-stu-id="1fa14-509">ARM</span></span><br /><span data-ttu-id="1fa14-510">GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-510">GNU</span></span> |

#### <a name="module-linker-for-cortex-m33-using-iar"></a><span data-ttu-id="1fa14-511">Module linker per Cortex-M33 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-511">Module linker for Cortex-M33 using IAR</span></span>

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

#### <a name="building-modules-for-cortex-m33-using-iar"></a><span data-ttu-id="1fa14-512">Compilazione di moduli per Cortex-M33 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-512">Building Modules for Cortex-M33 using IAR</span></span>

#### <a name="thread-extension-definition-for-cortex-m33-using-iar"></a><span data-ttu-id="1fa14-513">Definizione di estensione di thread per Cortex-M33 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-513">Thread extension definition for Cortex-M33 using IAR</span></span>

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

#### <a name="building-module-manager-for-cortex-m33-using-iar"></a><span data-ttu-id="1fa14-514">Compilazione di Module Manager per Cortex-M33 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-514">Building Module Manager for Cortex-M33 using IAR</span></span>

<span data-ttu-id="1fa14-515">Non è ancora disponibile un'area di lavoro di esempio.</span><span class="sxs-lookup"><span data-stu-id="1fa14-515">An example workspace is not yet provided.</span></span> <span data-ttu-id="1fa14-516">Presto disponibile.</span><span class="sxs-lookup"><span data-stu-id="1fa14-516">Coming soon.</span></span>

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m33-using-iar"></a><span data-ttu-id="1fa14-517">Attributi per la memoria esterna Abilita API per Cortex-M33 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-517">Attributes for external memory enable API for Cortex-M33 using IAR</span></span>

| <span data-ttu-id="1fa14-518">Parametro attribute</span><span class="sxs-lookup"><span data-stu-id="1fa14-518">Attribute parameter</span></span> |
|---|
| <span data-ttu-id="1fa14-519">TXM_MODULE_ATTRIBUTE_NON_SHAREABLE</span><span class="sxs-lookup"><span data-stu-id="1fa14-519">TXM_MODULE_ATTRIBUTE_NON_SHAREABLE</span></span> |
| <span data-ttu-id="1fa14-520">TXM_MODULE_ATTRIBUTE_OUTER_SHAREABLE</span><span class="sxs-lookup"><span data-stu-id="1fa14-520">TXM_MODULE_ATTRIBUTE_OUTER_SHAREABLE</span></span> |
| <span data-ttu-id="1fa14-521">TXM_MODULE_ATTRIBUTE_INNER_SHAREABLE</span><span class="sxs-lookup"><span data-stu-id="1fa14-521">TXM_MODULE_ATTRIBUTE_INNER_SHAREABLE</span></span> |
| <span data-ttu-id="1fa14-522">TXM_MODULE_ATTRIBUTE_READ_WRITE</span><span class="sxs-lookup"><span data-stu-id="1fa14-522">TXM_MODULE_ATTRIBUTE_READ_WRITE</span></span> |
| <span data-ttu-id="1fa14-523">TXM_MODULE_ATTRIBUTE_READ_ONLY</span><span class="sxs-lookup"><span data-stu-id="1fa14-523">TXM_MODULE_ATTRIBUTE_READ_ONLY</span></span> |

## <a name="cortex-m4-processor"></a><span data-ttu-id="1fa14-524">Processore Cortex-M4</span><span class="sxs-lookup"><span data-stu-id="1fa14-524">Cortex-M4 processor</span></span>

### <a name="cortex-m4-using-ac5"></a><span data-ttu-id="1fa14-525">Cortex-M4 con AC5</span><span class="sxs-lookup"><span data-stu-id="1fa14-525">Cortex-M4 using AC5</span></span>

#### <a name="module-preamble-for-cortex-m4-using-ac5"></a><span data-ttu-id="1fa14-526">Preambolo del modulo per Cortex-M4 con AC5</span><span class="sxs-lookup"><span data-stu-id="1fa14-526">Module preamble for Cortex-M4 using AC5</span></span>

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

#### <a name="module-properties-for-cortex-m4-using-ac5"></a><span data-ttu-id="1fa14-527">Proprietà dei moduli per Cortex-M4 con AC5</span><span class="sxs-lookup"><span data-stu-id="1fa14-527">Module properties for Cortex-M4 using AC5</span></span>

| <span data-ttu-id="1fa14-528">bit</span><span class="sxs-lookup"><span data-stu-id="1fa14-528">Bit</span></span> | <span data-ttu-id="1fa14-529">Valore</span><span class="sxs-lookup"><span data-stu-id="1fa14-529">Value</span></span> | <span data-ttu-id="1fa14-530">Significato</span><span class="sxs-lookup"><span data-stu-id="1fa14-530">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="1fa14-531">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-531">0</span></span> | <span data-ttu-id="1fa14-532">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-532">0</span></span><br /><span data-ttu-id="1fa14-533">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-533">1</span></span> | <span data-ttu-id="1fa14-534">Esecuzione in modalità privilegiata</span><span class="sxs-lookup"><span data-stu-id="1fa14-534">Privileged mode execution</span></span><br /><span data-ttu-id="1fa14-535">Esecuzione in modalità utente</span><span class="sxs-lookup"><span data-stu-id="1fa14-535">User mode execution</span></span> |
| <span data-ttu-id="1fa14-536">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-536">1</span></span> | <span data-ttu-id="1fa14-537">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-537">0</span></span><br /><span data-ttu-id="1fa14-538">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-538">1</span></span> | <span data-ttu-id="1fa14-539">Nessuna protezione MPU</span><span class="sxs-lookup"><span data-stu-id="1fa14-539">No MPU protection</span></span><br /><span data-ttu-id="1fa14-540">Protezione MPU (è necessario selezionare la modalità utente)</span><span class="sxs-lookup"><span data-stu-id="1fa14-540">MPU protection (must have user mode selected)</span></span> |
| <span data-ttu-id="1fa14-541">2</span><span class="sxs-lookup"><span data-stu-id="1fa14-541">2</span></span> | <span data-ttu-id="1fa14-542">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-542">0</span></span><br /><span data-ttu-id="1fa14-543">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-543">1</span></span> | <span data-ttu-id="1fa14-544">Disabilitare l'accesso alla memoria condivisa/esterna</span><span class="sxs-lookup"><span data-stu-id="1fa14-544">Disable shared/external memory access</span></span><br /><span data-ttu-id="1fa14-545">Abilitare l'accesso alla memoria condivisa/esterna</span><span class="sxs-lookup"><span data-stu-id="1fa14-545">Enable shared/external memory access</span></span> |
| <span data-ttu-id="1fa14-546">[23-3]</span><span class="sxs-lookup"><span data-stu-id="1fa14-546">[23-3]</span></span> | <span data-ttu-id="1fa14-547">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-547">0</span></span> | <span data-ttu-id="1fa14-548">Riservato</span><span class="sxs-lookup"><span data-stu-id="1fa14-548">Reserved</span></span>
| <span data-ttu-id="1fa14-549">[31-24]</span><span class="sxs-lookup"><span data-stu-id="1fa14-549">[31-24]</span></span> | <br /><span data-ttu-id="1fa14-550">0x00</span><span class="sxs-lookup"><span data-stu-id="1fa14-550">0x00</span></span><br /><span data-ttu-id="1fa14-551">0x01</span><span class="sxs-lookup"><span data-stu-id="1fa14-551">0x01</span></span><br /><span data-ttu-id="1fa14-552">0x02</span><span class="sxs-lookup"><span data-stu-id="1fa14-552">0x02</span></span> | <span data-ttu-id="1fa14-553">**ID compilatore**</span><span class="sxs-lookup"><span data-stu-id="1fa14-553">**Compiler ID**</span></span><br /><span data-ttu-id="1fa14-554">IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-554">IAR</span></span><br /><span data-ttu-id="1fa14-555">ARM</span><span class="sxs-lookup"><span data-stu-id="1fa14-555">ARM</span></span><br /><span data-ttu-id="1fa14-556">GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-556">GNU</span></span> |

#### <a name="module-linker-for-cortex-m4-using-ac5"></a><span data-ttu-id="1fa14-557">Module linker per Cortex-M4 con AC5</span><span class="sxs-lookup"><span data-stu-id="1fa14-557">Module linker for Cortex-M4 using AC5</span></span>

<span data-ttu-id="1fa14-558">Nessun file del linker di esempio specificato. il collegamento viene eseguito sulla riga di comando.</span><span class="sxs-lookup"><span data-stu-id="1fa14-558">No example linker file is provided; linking is done on the command line.</span></span> <span data-ttu-id="1fa14-559">Vedere la sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="1fa14-559">See next section.</span></span>

#### <a name="building-modules-for-cortex-m4-using-ac5"></a><span data-ttu-id="1fa14-560">Compilazione di moduli per Cortex-M4 con AC5</span><span class="sxs-lookup"><span data-stu-id="1fa14-560">Building Modules for Cortex-M4 using AC5</span></span>

<span data-ttu-id="1fa14-561">Vedere build_threadx_module_demo.bat di esempio:</span><span class="sxs-lookup"><span data-stu-id="1fa14-561">See example build_threadx_module_demo.bat:</span></span>

```dos
armasm -g --cpreproc --cpu=cortex-m4 --fpu=vfpv4 --apcs=/interwork/ropi/rwpi txm_module_preamble.S
armcc  -g --cpu=cortex-m4 --fpu=vfpv4 -c --apcs=/interwork/ropi/rwpi --lower_ropi -I../inc -I../../../../common_modules/inc -I../../../../common_modules/module_manager/inc -I../../../../common/inc sample_threadx_module.c
armlink -d -o sample_threadx_module.axf --elf --ro=0x30000 --rw=0x40000 --first txm_module_preamble.o(Init) --entry=_txm_module_thread_shell_entry --ropi --rwpi --remove --map --symbols --list sample_threadx_module.map txm_module_preamble.o sample_threadx_module.o txm.a
```

#### <a name="thread-extension-definition-for-cortex-m4-using-ac5"></a><span data-ttu-id="1fa14-562">Definizione dell'estensione di thread per Cortex-M4 con AC5</span><span class="sxs-lookup"><span data-stu-id="1fa14-562">Thread extension definition for Cortex-M4 using AC5</span></span>

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

#### <a name="building-module-manager-for-cortex-m4-using-ac5"></a><span data-ttu-id="1fa14-563">Compilazione di Module Manager per Cortex-M4 con AC5</span><span class="sxs-lookup"><span data-stu-id="1fa14-563">Building Module Manager for Cortex-M4 using AC5</span></span>

<span data-ttu-id="1fa14-564">Vedere build_threadx_module_manager_demo.bat di esempio:</span><span class="sxs-lookup"><span data-stu-id="1fa14-564">See example build_threadx_module_manager_demo.bat:</span></span>

```dos
armasm -g --cpreproc --cpu=cortex-m4 --fpu=vfpv4 --apcs=/interwork tx_initialize_low_level.S
armcc -g --cpu=cortex-m4 --fpu=vfpv4 -c -I../inc -I../../../../common_modules/inc -I../../../../common_modules/module_manager/inc -I../../../../common/inc sample_threadx_module_manager.c
armlink -d -o sample_threadx_module_manager.axf --elf --ro 0x00000000 --first tx_initialize_low_level.o(RESET) --remove --map --symbols --list sample_threadx_module_manager.map tx_initialize_low_level.o sample_threadx_module_manager.o tx.a
```

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m4-using-ac5"></a><span data-ttu-id="1fa14-565">Attributi per la memoria esterna Abilita API per Cortex-M4 con AC5</span><span class="sxs-lookup"><span data-stu-id="1fa14-565">Attributes for external memory enable API for Cortex-M4 using AC5</span></span>

<span data-ttu-id="1fa14-566">Il modulo dispone sempre dell'accesso in lettura alla memoria condivisa.</span><span class="sxs-lookup"><span data-stu-id="1fa14-566">Module always has read access to shared memory.</span></span>
| <span data-ttu-id="1fa14-567">Parametro attribute</span><span class="sxs-lookup"><span data-stu-id="1fa14-567">Attribute parameter</span></span> | <span data-ttu-id="1fa14-568">Significato</span><span class="sxs-lookup"><span data-stu-id="1fa14-568">Meaning</span></span> |
|---|---|
| <span data-ttu-id="1fa14-569">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span><span class="sxs-lookup"><span data-stu-id="1fa14-569">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span></span> | <span data-ttu-id="1fa14-570">Accesso in scrittura</span><span class="sxs-lookup"><span data-stu-id="1fa14-570">Write access</span></span> |

### <a name="cortex-m4-using-ac6"></a><span data-ttu-id="1fa14-571">Cortex-M4 con AC6</span><span class="sxs-lookup"><span data-stu-id="1fa14-571">Cortex-M4 using AC6</span></span>

#### <a name="module-preamble-for-cortex-m4-using-ac6"></a><span data-ttu-id="1fa14-572">Preambolo del modulo per Cortex-M4 con AC6</span><span class="sxs-lookup"><span data-stu-id="1fa14-572">Module preamble for Cortex-M4 using AC6</span></span>

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

#### <a name="module-properties-for-cortex-m4-using-ac6"></a><span data-ttu-id="1fa14-573">Proprietà dei moduli per Cortex-M4 con AC6</span><span class="sxs-lookup"><span data-stu-id="1fa14-573">Module properties for Cortex-M4 using AC6</span></span>

| <span data-ttu-id="1fa14-574">bit</span><span class="sxs-lookup"><span data-stu-id="1fa14-574">Bit</span></span> | <span data-ttu-id="1fa14-575">Valore</span><span class="sxs-lookup"><span data-stu-id="1fa14-575">Value</span></span> | <span data-ttu-id="1fa14-576">Significato</span><span class="sxs-lookup"><span data-stu-id="1fa14-576">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="1fa14-577">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-577">0</span></span> | <span data-ttu-id="1fa14-578">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-578">0</span></span><br /><span data-ttu-id="1fa14-579">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-579">1</span></span> | <span data-ttu-id="1fa14-580">Esecuzione in modalità privilegiata</span><span class="sxs-lookup"><span data-stu-id="1fa14-580">Privileged mode execution</span></span><br /><span data-ttu-id="1fa14-581">Esecuzione in modalità utente</span><span class="sxs-lookup"><span data-stu-id="1fa14-581">User mode execution</span></span> |
| <span data-ttu-id="1fa14-582">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-582">1</span></span> | <span data-ttu-id="1fa14-583">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-583">0</span></span><br /><span data-ttu-id="1fa14-584">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-584">1</span></span> | <span data-ttu-id="1fa14-585">Nessuna protezione MPU</span><span class="sxs-lookup"><span data-stu-id="1fa14-585">No MPU protection</span></span><br /><span data-ttu-id="1fa14-586">Protezione MPU (è necessario selezionare la modalità utente)</span><span class="sxs-lookup"><span data-stu-id="1fa14-586">MPU protection (must have user mode selected)</span></span> |
| <span data-ttu-id="1fa14-587">2</span><span class="sxs-lookup"><span data-stu-id="1fa14-587">2</span></span> | <span data-ttu-id="1fa14-588">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-588">0</span></span><br /><span data-ttu-id="1fa14-589">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-589">1</span></span> | <span data-ttu-id="1fa14-590">Disabilitare l'accesso alla memoria condivisa/esterna</span><span class="sxs-lookup"><span data-stu-id="1fa14-590">Disable shared/external memory access</span></span><br /><span data-ttu-id="1fa14-591">Abilitare l'accesso alla memoria condivisa/esterna</span><span class="sxs-lookup"><span data-stu-id="1fa14-591">Enable shared/external memory access</span></span> |
| <span data-ttu-id="1fa14-592">[23-3]</span><span class="sxs-lookup"><span data-stu-id="1fa14-592">[23-3]</span></span> | <span data-ttu-id="1fa14-593">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-593">0</span></span> | <span data-ttu-id="1fa14-594">Riservato</span><span class="sxs-lookup"><span data-stu-id="1fa14-594">Reserved</span></span>
| <span data-ttu-id="1fa14-595">[31-24]</span><span class="sxs-lookup"><span data-stu-id="1fa14-595">[31-24]</span></span> | <br /><span data-ttu-id="1fa14-596">0x00</span><span class="sxs-lookup"><span data-stu-id="1fa14-596">0x00</span></span><br /><span data-ttu-id="1fa14-597">0x01</span><span class="sxs-lookup"><span data-stu-id="1fa14-597">0x01</span></span><br /><span data-ttu-id="1fa14-598">0x02</span><span class="sxs-lookup"><span data-stu-id="1fa14-598">0x02</span></span> | <span data-ttu-id="1fa14-599">**ID compilatore**</span><span class="sxs-lookup"><span data-stu-id="1fa14-599">**Compiler ID**</span></span><br /><span data-ttu-id="1fa14-600">IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-600">IAR</span></span><br /><span data-ttu-id="1fa14-601">ARM</span><span class="sxs-lookup"><span data-stu-id="1fa14-601">ARM</span></span><br /><span data-ttu-id="1fa14-602">GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-602">GNU</span></span> |

#### <a name="module-linker-for-cortex-m4-using-ac6"></a><span data-ttu-id="1fa14-603">Module linker per Cortex-M4 con AC6</span><span class="sxs-lookup"><span data-stu-id="1fa14-603">Module linker for Cortex-M4 using AC6</span></span>

<span data-ttu-id="1fa14-604">Non viene usato alcun file del linker.</span><span class="sxs-lookup"><span data-stu-id="1fa14-604">No linker file is used.</span></span> <span data-ttu-id="1fa14-605">Vedere Impostazioni progetto.</span><span class="sxs-lookup"><span data-stu-id="1fa14-605">See project settings.</span></span>

#### <a name="building-modules-for-cortex-m4-using-ac6"></a><span data-ttu-id="1fa14-606">Compilazione di moduli per Cortex-M4 con AC6</span><span class="sxs-lookup"><span data-stu-id="1fa14-606">Building Modules for Cortex-M4 using AC6</span></span>

<span data-ttu-id="1fa14-607">Viene fornita un'area di lavoro di esempio.</span><span class="sxs-lookup"><span data-stu-id="1fa14-607">An example workspace is provided.</span></span> <span data-ttu-id="1fa14-608">Compilare la libreria ThreadX, la libreria di moduli ThreadX, il progetto di modulo di esempio e il progetto di gestione moduli di esempio.</span><span class="sxs-lookup"><span data-stu-id="1fa14-608">Build the ThreadX library, ThreadX Modules library, sample module project, and sample module manager project.</span></span>

#### <a name="thread-extension-definition-for-cortex-m4-using-ac6"></a><span data-ttu-id="1fa14-609">Definizione dell'estensione di thread per Cortex-M4 con AC6</span><span class="sxs-lookup"><span data-stu-id="1fa14-609">Thread extension definition for Cortex-M4 using AC6</span></span>

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

#### <a name="building-module-manager-for-cortex-m4-using-ac6"></a><span data-ttu-id="1fa14-610">Compilazione di Module Manager per Cortex-M4 con AC6</span><span class="sxs-lookup"><span data-stu-id="1fa14-610">Building Module Manager for Cortex-M4 using AC6</span></span>

<span data-ttu-id="1fa14-611">Viene fornita un'area di lavoro di esempio.</span><span class="sxs-lookup"><span data-stu-id="1fa14-611">An example workspace is provided.</span></span> <span data-ttu-id="1fa14-612">Compilare la libreria ThreadX, la libreria di moduli ThreadX, il progetto di modulo di esempio e il progetto di gestione moduli di esempio.</span><span class="sxs-lookup"><span data-stu-id="1fa14-612">Build the ThreadX library, ThreadX Modules library, sample module project, and sample module manager project.</span></span>

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m4-using-ac6"></a><span data-ttu-id="1fa14-613">Attributi per la memoria esterna Abilita API per Cortex-M4 con AC6</span><span class="sxs-lookup"><span data-stu-id="1fa14-613">Attributes for external memory enable API for Cortex-M4 using AC6</span></span>

<span data-ttu-id="1fa14-614">Il modulo dispone sempre dell'accesso in lettura alla memoria condivisa.</span><span class="sxs-lookup"><span data-stu-id="1fa14-614">Module always has read access to shared memory.</span></span>
| <span data-ttu-id="1fa14-615">Parametro attribute</span><span class="sxs-lookup"><span data-stu-id="1fa14-615">Attribute parameter</span></span> | <span data-ttu-id="1fa14-616">Significato</span><span class="sxs-lookup"><span data-stu-id="1fa14-616">Meaning</span></span> |
|---|---|
| <span data-ttu-id="1fa14-617">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span><span class="sxs-lookup"><span data-stu-id="1fa14-617">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span></span> | <span data-ttu-id="1fa14-618">Accesso in scrittura</span><span class="sxs-lookup"><span data-stu-id="1fa14-618">Write access</span></span> |

### <a name="cortex-m4-using-gnu"></a><span data-ttu-id="1fa14-619">Cortex-M4 con GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-619">Cortex-M4 using GNU</span></span>

#### <a name="module-preamble-for-cortex-m4-using-gnu"></a><span data-ttu-id="1fa14-620">Preambolo del modulo per Cortex-M4 con GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-620">Module preamble for Cortex-M4 using GNU</span></span>

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

#### <a name="module-properties-for-cortex-m4-using-gnu"></a><span data-ttu-id="1fa14-621">Proprietà dei moduli per Cortex-M4 con GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-621">Module properties for Cortex-M4 using GNU</span></span>

| <span data-ttu-id="1fa14-622">bit</span><span class="sxs-lookup"><span data-stu-id="1fa14-622">Bit</span></span> | <span data-ttu-id="1fa14-623">Valore</span><span class="sxs-lookup"><span data-stu-id="1fa14-623">Value</span></span> | <span data-ttu-id="1fa14-624">Significato</span><span class="sxs-lookup"><span data-stu-id="1fa14-624">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="1fa14-625">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-625">0</span></span> | <span data-ttu-id="1fa14-626">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-626">0</span></span><br /><span data-ttu-id="1fa14-627">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-627">1</span></span> | <span data-ttu-id="1fa14-628">Esecuzione in modalità privilegiata</span><span class="sxs-lookup"><span data-stu-id="1fa14-628">Privileged mode execution</span></span><br /><span data-ttu-id="1fa14-629">Esecuzione in modalità utente</span><span class="sxs-lookup"><span data-stu-id="1fa14-629">User mode execution</span></span> |
| <span data-ttu-id="1fa14-630">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-630">1</span></span> | <span data-ttu-id="1fa14-631">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-631">0</span></span><br /><span data-ttu-id="1fa14-632">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-632">1</span></span> | <span data-ttu-id="1fa14-633">Nessuna protezione MPU</span><span class="sxs-lookup"><span data-stu-id="1fa14-633">No MPU protection</span></span><br /><span data-ttu-id="1fa14-634">Protezione MPU (è necessario selezionare la modalità utente)</span><span class="sxs-lookup"><span data-stu-id="1fa14-634">MPU protection (must have user mode selected)</span></span> |
| <span data-ttu-id="1fa14-635">2</span><span class="sxs-lookup"><span data-stu-id="1fa14-635">2</span></span> | <span data-ttu-id="1fa14-636">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-636">0</span></span><br /><span data-ttu-id="1fa14-637">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-637">1</span></span> | <span data-ttu-id="1fa14-638">Disabilitare l'accesso alla memoria condivisa/esterna</span><span class="sxs-lookup"><span data-stu-id="1fa14-638">Disable shared/external memory access</span></span><br /><span data-ttu-id="1fa14-639">Abilitare l'accesso alla memoria condivisa/esterna</span><span class="sxs-lookup"><span data-stu-id="1fa14-639">Enable shared/external memory access</span></span> |
| <span data-ttu-id="1fa14-640">[23-3]</span><span class="sxs-lookup"><span data-stu-id="1fa14-640">[23-3]</span></span> | <span data-ttu-id="1fa14-641">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-641">0</span></span> | <span data-ttu-id="1fa14-642">Riservato</span><span class="sxs-lookup"><span data-stu-id="1fa14-642">Reserved</span></span>
| <span data-ttu-id="1fa14-643">[31-24]</span><span class="sxs-lookup"><span data-stu-id="1fa14-643">[31-24]</span></span> | <br /><span data-ttu-id="1fa14-644">0x00</span><span class="sxs-lookup"><span data-stu-id="1fa14-644">0x00</span></span><br /><span data-ttu-id="1fa14-645">0x01</span><span class="sxs-lookup"><span data-stu-id="1fa14-645">0x01</span></span><br /><span data-ttu-id="1fa14-646">0x02</span><span class="sxs-lookup"><span data-stu-id="1fa14-646">0x02</span></span> | <span data-ttu-id="1fa14-647">**ID compilatore**</span><span class="sxs-lookup"><span data-stu-id="1fa14-647">**Compiler ID**</span></span><br /><span data-ttu-id="1fa14-648">IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-648">IAR</span></span><br /><span data-ttu-id="1fa14-649">ARM</span><span class="sxs-lookup"><span data-stu-id="1fa14-649">ARM</span></span><br /><span data-ttu-id="1fa14-650">GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-650">GNU</span></span> |

#### <a name="module-linker-for-cortex-m4-using-gnu"></a><span data-ttu-id="1fa14-651">Module linker per Cortex-M4 con GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-651">Module linker for Cortex-M4 using GNU</span></span>

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

#### <a name="building-modules-for-cortex-m4-using-gnu"></a><span data-ttu-id="1fa14-652">Compilazione di moduli per Cortex-M4 con GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-652">Building Modules for Cortex-M4 using GNU</span></span>

<span data-ttu-id="1fa14-653">Vedere build_threadx_module_sample.bat:</span><span class="sxs-lookup"><span data-stu-id="1fa14-653">See build_threadx_module_sample.bat:</span></span>

```dos
arm-none-eabi-gcc -c -g -mcpu=cortex-m4 -mfloat-abi=hard -mfpu=vfpv4 -fpie -fno-plt -mpic-data-is-text-relative -msingle-pic-base txm_module_preamble.s
arm-none-eabi-gcc -c -g -mcpu=cortex-m4 -mfloat-abi=hard -mfpu=vfpv4 -fpie -fno-plt -mpic-data-is-text-relative -msingle-pic-base gcc_setup.S
arm-none-eabi-gcc -c -g -mcpu=cortex-m4 -mfloat-abi=hard -mfpu=vfpv4 -fpie -fno-plt -mpic-data-is-text-relative -msingle-pic-base -I..\inc -I..\..\..\..\common\inc -I..\..\..\..\common_modules\inc sample_threadx_module.c
arm-none-eabi-ld -A cortex-m4 -T sample_threadx_module.ld txm_module_preamble.o gcc_setup.o sample_threadx_module.o -e _txm_module_thread_shell_entry txm.a -o sample_threadx_module.axf -M > sample_threadx_module.map
```

#### <a name="thread-extension-definition-for-cortex-m4-using-gnu"></a><span data-ttu-id="1fa14-654">Definizione di estensione di thread per Cortex-M4 con GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-654">Thread extension definition for Cortex-M4 using GNU</span></span>

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

#### <a name="building-module-manager-for-cortex-m4-using-gnu"></a><span data-ttu-id="1fa14-655">Compilazione di Module Manager per Cortex-M4 con GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-655">Building Module Manager for Cortex-M4 using GNU</span></span>

<span data-ttu-id="1fa14-656">Vedere build_threadx_module_manager_sample.bat:</span><span class="sxs-lookup"><span data-stu-id="1fa14-656">See build_threadx_module_manager_sample.bat:</span></span>

```dos
arm-none-eabi-gcc -c -g -mcpu=cortex-m4 -mfloat-abi=hard -mfpu=vfpv4 -mthumb cortexm_vectors.S
arm-none-eabi-gcc -c -g -mcpu=cortex-m4 -mfloat-abi=hard -mfpu=vfpv4 -mthumb cortexm_crt0.S
arm-none-eabi-gcc -c -g -mcpu=cortex-m4 -mfloat-abi=hard -mfpu=vfpv4 -mthumb tx_initialize_low_level.S
arm-none-eabi-gcc -c -g -mcpu=cortex-m4 -mfloat-abi=hard -mfpu=vfpv4 -mthumb -I..\inc -I..\..\..\..\common\inc -I..\..\..\..\common_modules\inc sample_threadx_module_manager.c
arm-none-eabi-gcc -g -mcpu=cortex-m4 -mfloat-abi=hard -mfpu=vfpv4 -mthumb -T sample_threadx.ld -ereset_handler -nostartfiles -o sample_threadx_module_manager.out -Wl,-Map=sample_threadx_module_manager.map cortexm_vectors.o cortexm_crt0.o tx_initialize_low_level.o sample_threadx_module_manager.o tx.a
```

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m4-using-gnu"></a><span data-ttu-id="1fa14-657">Attributi per la memoria esterna Abilita API per Cortex-M4 con GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-657">Attributes for external memory enable API for Cortex-M4 using GNU</span></span>

<span data-ttu-id="1fa14-658">Il modulo dispone sempre dell'accesso in lettura alla memoria condivisa.</span><span class="sxs-lookup"><span data-stu-id="1fa14-658">Module always has read access to shared memory.</span></span>
| <span data-ttu-id="1fa14-659">Parametro attribute</span><span class="sxs-lookup"><span data-stu-id="1fa14-659">Attribute parameter</span></span> | <span data-ttu-id="1fa14-660">Significato</span><span class="sxs-lookup"><span data-stu-id="1fa14-660">Meaning</span></span> |
|---|---|
| <span data-ttu-id="1fa14-661">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span><span class="sxs-lookup"><span data-stu-id="1fa14-661">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span></span> | <span data-ttu-id="1fa14-662">Accesso in scrittura</span><span class="sxs-lookup"><span data-stu-id="1fa14-662">Write access</span></span> |

### <a name="cortex-m4-using-iar"></a><span data-ttu-id="1fa14-663">Cortex-M4 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-663">Cortex-M4 using IAR</span></span>

#### <a name="module-preamble-for-cortex-m4-using-iar"></a><span data-ttu-id="1fa14-664">Preambolo del modulo per Cortex-M4 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-664">Module preamble for Cortex-M4 using IAR</span></span>

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

#### <a name="module-properties-for-cortex-m4-using-iar"></a><span data-ttu-id="1fa14-665">Proprietà dei moduli per Cortex-M4 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-665">Module properties for Cortex-M4 using IAR</span></span>

| <span data-ttu-id="1fa14-666">bit</span><span class="sxs-lookup"><span data-stu-id="1fa14-666">Bit</span></span> | <span data-ttu-id="1fa14-667">Valore</span><span class="sxs-lookup"><span data-stu-id="1fa14-667">Value</span></span> | <span data-ttu-id="1fa14-668">Significato</span><span class="sxs-lookup"><span data-stu-id="1fa14-668">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="1fa14-669">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-669">0</span></span> | <span data-ttu-id="1fa14-670">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-670">0</span></span><br /><span data-ttu-id="1fa14-671">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-671">1</span></span> | <span data-ttu-id="1fa14-672">Esecuzione in modalità privilegiata</span><span class="sxs-lookup"><span data-stu-id="1fa14-672">Privileged mode execution</span></span><br /><span data-ttu-id="1fa14-673">Esecuzione in modalità utente</span><span class="sxs-lookup"><span data-stu-id="1fa14-673">User mode execution</span></span> |
| <span data-ttu-id="1fa14-674">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-674">1</span></span> | <span data-ttu-id="1fa14-675">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-675">0</span></span><br /><span data-ttu-id="1fa14-676">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-676">1</span></span> | <span data-ttu-id="1fa14-677">Nessuna protezione MPU</span><span class="sxs-lookup"><span data-stu-id="1fa14-677">No MPU protection</span></span><br /><span data-ttu-id="1fa14-678">Protezione MPU (è necessario selezionare la modalità utente)</span><span class="sxs-lookup"><span data-stu-id="1fa14-678">MPU protection (must have user mode selected)</span></span> |
| <span data-ttu-id="1fa14-679">2</span><span class="sxs-lookup"><span data-stu-id="1fa14-679">2</span></span> | <span data-ttu-id="1fa14-680">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-680">0</span></span><br /><span data-ttu-id="1fa14-681">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-681">1</span></span> | <span data-ttu-id="1fa14-682">Disabilitare l'accesso alla memoria condivisa/esterna</span><span class="sxs-lookup"><span data-stu-id="1fa14-682">Disable shared/external memory access</span></span><br /><span data-ttu-id="1fa14-683">Abilitare l'accesso alla memoria condivisa/esterna</span><span class="sxs-lookup"><span data-stu-id="1fa14-683">Enable shared/external memory access</span></span> |
| <span data-ttu-id="1fa14-684">[23-3]</span><span class="sxs-lookup"><span data-stu-id="1fa14-684">[23-3]</span></span> | <span data-ttu-id="1fa14-685">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-685">0</span></span> | <span data-ttu-id="1fa14-686">Riservato</span><span class="sxs-lookup"><span data-stu-id="1fa14-686">Reserved</span></span>
| <span data-ttu-id="1fa14-687">[31-24]</span><span class="sxs-lookup"><span data-stu-id="1fa14-687">[31-24]</span></span> | <br /><span data-ttu-id="1fa14-688">0x00</span><span class="sxs-lookup"><span data-stu-id="1fa14-688">0x00</span></span><br /><span data-ttu-id="1fa14-689">0x01</span><span class="sxs-lookup"><span data-stu-id="1fa14-689">0x01</span></span><br /><span data-ttu-id="1fa14-690">0x02</span><span class="sxs-lookup"><span data-stu-id="1fa14-690">0x02</span></span> | <span data-ttu-id="1fa14-691">**ID compilatore**</span><span class="sxs-lookup"><span data-stu-id="1fa14-691">**Compiler ID**</span></span><br /><span data-ttu-id="1fa14-692">IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-692">IAR</span></span><br /><span data-ttu-id="1fa14-693">ARM</span><span class="sxs-lookup"><span data-stu-id="1fa14-693">ARM</span></span><br /><span data-ttu-id="1fa14-694">GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-694">GNU</span></span> |

#### <a name="module-linker-for-cortex-m4-using-iar"></a><span data-ttu-id="1fa14-695">Module linker per Cortex-M4 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-695">Module linker for Cortex-M4 using IAR</span></span>

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

#### <a name="building-modules-for-cortex-m4-using-iar"></a><span data-ttu-id="1fa14-696">Compilazione di moduli per Cortex-M4 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-696">Building Modules for Cortex-M4 using IAR</span></span>

<span data-ttu-id="1fa14-697">Viene fornita un'area di lavoro di esempio.</span><span class="sxs-lookup"><span data-stu-id="1fa14-697">An example workspace is provided.</span></span> <span data-ttu-id="1fa14-698">Compilare la libreria ThreadX, la libreria di moduli ThreadX, il progetto del modulo demo e il progetto di gestione moduli dimostrativi.</span><span class="sxs-lookup"><span data-stu-id="1fa14-698">Build the ThreadX library, ThreadX Modules library, demo module project, and demo module manager project.</span></span>

#### <a name="thread-extension-definition-for-cortex-m4-using-iar"></a><span data-ttu-id="1fa14-699">Definizione di estensione di thread per Cortex-M4 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-699">Thread extension definition for Cortex-M4 using IAR</span></span>

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

#### <a name="building-module-manager-for-cortex-m4-using-iar"></a><span data-ttu-id="1fa14-700">Compilazione di Module Manager per Cortex-M4 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-700">Building Module Manager for Cortex-M4 using IAR</span></span>

<span data-ttu-id="1fa14-701">Viene fornita un'area di lavoro di esempio.</span><span class="sxs-lookup"><span data-stu-id="1fa14-701">An example workspace is provided.</span></span> <span data-ttu-id="1fa14-702">Compilare la libreria ThreadX, la libreria di moduli ThreadX, il progetto del modulo demo e il progetto di gestione moduli dimostrativi.</span><span class="sxs-lookup"><span data-stu-id="1fa14-702">Build the ThreadX library, ThreadX Modules library, demo module project, and demo module manager project.</span></span>

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m4-using-iar"></a><span data-ttu-id="1fa14-703">Attributi per la memoria esterna Abilita API per Cortex-M4 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-703">Attributes for external memory enable API for Cortex-M4 using IAR</span></span>

<span data-ttu-id="1fa14-704">Il modulo dispone sempre dell'accesso in lettura alla memoria condivisa.</span><span class="sxs-lookup"><span data-stu-id="1fa14-704">Module always has read access to shared memory.</span></span>
| <span data-ttu-id="1fa14-705">Parametro attribute</span><span class="sxs-lookup"><span data-stu-id="1fa14-705">Attribute parameter</span></span> | <span data-ttu-id="1fa14-706">Significato</span><span class="sxs-lookup"><span data-stu-id="1fa14-706">Meaning</span></span> |
|---|---|
| <span data-ttu-id="1fa14-707">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span><span class="sxs-lookup"><span data-stu-id="1fa14-707">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span></span> | <span data-ttu-id="1fa14-708">Accesso in scrittura</span><span class="sxs-lookup"><span data-stu-id="1fa14-708">Write access</span></span> |

## <a name="cortex-m7-processor"></a><span data-ttu-id="1fa14-709">Processore Cortex-M7</span><span class="sxs-lookup"><span data-stu-id="1fa14-709">Cortex-M7 processor</span></span>

### <a name="cortex-m7-using-ac5"></a><span data-ttu-id="1fa14-710">Cortex-M7 con AC5</span><span class="sxs-lookup"><span data-stu-id="1fa14-710">Cortex-M7 using AC5</span></span>

#### <a name="module-preamble-for-cortex-m7-using-ac5"></a><span data-ttu-id="1fa14-711">Preambolo del modulo per Cortex-M7 con AC5</span><span class="sxs-lookup"><span data-stu-id="1fa14-711">Module preamble for Cortex-M7 using AC5</span></span>

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

#### <a name="module-properties-for-cortex-m7-using-ac5"></a><span data-ttu-id="1fa14-712">Proprietà dei moduli per Cortex-M7 con AC5</span><span class="sxs-lookup"><span data-stu-id="1fa14-712">Module properties for Cortex-M7 using AC5</span></span>

| <span data-ttu-id="1fa14-713">bit</span><span class="sxs-lookup"><span data-stu-id="1fa14-713">Bit</span></span> | <span data-ttu-id="1fa14-714">Valore</span><span class="sxs-lookup"><span data-stu-id="1fa14-714">Value</span></span> | <span data-ttu-id="1fa14-715">Significato</span><span class="sxs-lookup"><span data-stu-id="1fa14-715">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="1fa14-716">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-716">0</span></span> | <span data-ttu-id="1fa14-717">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-717">0</span></span><br /><span data-ttu-id="1fa14-718">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-718">1</span></span> | <span data-ttu-id="1fa14-719">Esecuzione in modalità privilegiata</span><span class="sxs-lookup"><span data-stu-id="1fa14-719">Privileged mode execution</span></span><br /><span data-ttu-id="1fa14-720">Esecuzione in modalità utente</span><span class="sxs-lookup"><span data-stu-id="1fa14-720">User mode execution</span></span> |
| <span data-ttu-id="1fa14-721">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-721">1</span></span> | <span data-ttu-id="1fa14-722">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-722">0</span></span><br /><span data-ttu-id="1fa14-723">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-723">1</span></span> | <span data-ttu-id="1fa14-724">Nessuna protezione MPU</span><span class="sxs-lookup"><span data-stu-id="1fa14-724">No MPU protection</span></span><br /><span data-ttu-id="1fa14-725">Protezione MPU (è necessario selezionare la modalità utente)</span><span class="sxs-lookup"><span data-stu-id="1fa14-725">MPU protection (must have user mode selected)</span></span> |
| <span data-ttu-id="1fa14-726">2</span><span class="sxs-lookup"><span data-stu-id="1fa14-726">2</span></span> | <span data-ttu-id="1fa14-727">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-727">0</span></span><br /><span data-ttu-id="1fa14-728">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-728">1</span></span> | <span data-ttu-id="1fa14-729">Disabilitare l'accesso alla memoria condivisa/esterna</span><span class="sxs-lookup"><span data-stu-id="1fa14-729">Disable shared/external memory access</span></span><br /><span data-ttu-id="1fa14-730">Abilitare l'accesso alla memoria condivisa/esterna</span><span class="sxs-lookup"><span data-stu-id="1fa14-730">Enable shared/external memory access</span></span> |
| <span data-ttu-id="1fa14-731">[23-3]</span><span class="sxs-lookup"><span data-stu-id="1fa14-731">[23-3]</span></span> | <span data-ttu-id="1fa14-732">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-732">0</span></span> | <span data-ttu-id="1fa14-733">Riservato</span><span class="sxs-lookup"><span data-stu-id="1fa14-733">Reserved</span></span>
| <span data-ttu-id="1fa14-734">[31-24]</span><span class="sxs-lookup"><span data-stu-id="1fa14-734">[31-24]</span></span> | <br /><span data-ttu-id="1fa14-735">0x00</span><span class="sxs-lookup"><span data-stu-id="1fa14-735">0x00</span></span><br /><span data-ttu-id="1fa14-736">0x01</span><span class="sxs-lookup"><span data-stu-id="1fa14-736">0x01</span></span><br /><span data-ttu-id="1fa14-737">0x02</span><span class="sxs-lookup"><span data-stu-id="1fa14-737">0x02</span></span> | <span data-ttu-id="1fa14-738">**ID compilatore**</span><span class="sxs-lookup"><span data-stu-id="1fa14-738">**Compiler ID**</span></span><br /><span data-ttu-id="1fa14-739">IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-739">IAR</span></span><br /><span data-ttu-id="1fa14-740">ARM</span><span class="sxs-lookup"><span data-stu-id="1fa14-740">ARM</span></span><br /><span data-ttu-id="1fa14-741">GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-741">GNU</span></span> |

#### <a name="module-linker-for-cortex-m7-using-ac5"></a><span data-ttu-id="1fa14-742">Module linker per Cortex-M7 con AC5</span><span class="sxs-lookup"><span data-stu-id="1fa14-742">Module linker for Cortex-M7 using AC5</span></span>

<span data-ttu-id="1fa14-743">Compilato dalla riga di comando, nessun esempio di file del linker.</span><span class="sxs-lookup"><span data-stu-id="1fa14-743">Built on command-line, no linker file example.</span></span>

#### <a name="building-modules-for-cortex-m7-using-ac5"></a><span data-ttu-id="1fa14-744">Compilazione di moduli per Cortex-M7 con AC5</span><span class="sxs-lookup"><span data-stu-id="1fa14-744">Building Modules for Cortex-M7 using AC5</span></span>

<span data-ttu-id="1fa14-745">Un semplice esempio di riga di comando per la compilazione di un modulo Cortex-M7 con AC5:</span><span class="sxs-lookup"><span data-stu-id="1fa14-745">A simple command-line example for building a Cortex-M7 module using AC5:</span></span>

```dos
armasm -g --cpu=cortex-m7 --fpu=softvfp --apcs=/interwork/ropi/rwpi txm_module_preamble.s
armcc  -g --cpu=cortex-m7 --fpu=softvfp -c --apcs=/interwork/ropi/rwpi --lower_ropi -I../inc -I../../../../common_modules/inc -I../../../../common_modules/module_manager/inc -I../../../../common/inc sample_threadx_module.c
armlink -d -o sample_threadx_module.axf --elf --ro 0 --first txm_module_preamble.o(Init) --entry=_txm_module_thread_shell_entry --ropi --rwpi --remove --map --symbols --list sample_threadx_module.map txm_module_preamble.o sample_threadx_module.o txm.a
```

#### <a name="thread-extension-definition-for-cortex-m7-using-ac5"></a><span data-ttu-id="1fa14-746">Definizione di estensione di thread per Cortex-M7 con AC5</span><span class="sxs-lookup"><span data-stu-id="1fa14-746">Thread extension definition for Cortex-M7 using AC5</span></span>

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

#### <a name="building-module-manager-for-cortex-m7-using-ac5"></a><span data-ttu-id="1fa14-747">Compilazione di Module Manager per Cortex-M7 con AC5</span><span class="sxs-lookup"><span data-stu-id="1fa14-747">Building Module Manager for Cortex-M7 using AC5</span></span>

<span data-ttu-id="1fa14-748">Semplice esempio di riga di comando per la compilazione di un gestore di moduli Cortex-M7 con AC5:</span><span class="sxs-lookup"><span data-stu-id="1fa14-748">A simple command-line example for building a Cortex-M7 module manager using AC5:</span></span>

```dos
armasm -g --cpu=cortex-m7 --fpu=softvfp --apcs=interwork tx_initialize_low_level.s
armcc -g --cpu=cortex-m7 --fpu=softvfp -c demo_threadx_module_manager.c
armcc -g --cpu=cortex-m7 --fpu=softvfp -c module_code.c
armlink -d -o demo_threadx_module_manager.axf --elf --ro 0x00000000 --first tx_initialize_low_level.o(RESET) --remove --map --symbols --list demo_threadx_module_manager.map tx_initialize_low_level.o demo_threadx_module_manager.o module_code.o tx.a
```

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m7-using-ac5"></a><span data-ttu-id="1fa14-749">Attributi per la memoria esterna Abilita API per Cortex-M7 con AC5</span><span class="sxs-lookup"><span data-stu-id="1fa14-749">Attributes for external memory enable API for Cortex-M7 using AC5</span></span>

### <a name="cortex-m7-using-ac6"></a><span data-ttu-id="1fa14-750">Cortex-M7 con AC6</span><span class="sxs-lookup"><span data-stu-id="1fa14-750">Cortex-M7 using AC6</span></span>

#### <a name="module-properties-for-cortex-m7-using-ac6"></a><span data-ttu-id="1fa14-751">Proprietà dei moduli per Cortex-M7 con AC6</span><span class="sxs-lookup"><span data-stu-id="1fa14-751">Module properties for Cortex-M7 using AC6</span></span>

| <span data-ttu-id="1fa14-752">bit</span><span class="sxs-lookup"><span data-stu-id="1fa14-752">Bit</span></span> | <span data-ttu-id="1fa14-753">Valore</span><span class="sxs-lookup"><span data-stu-id="1fa14-753">Value</span></span> | <span data-ttu-id="1fa14-754">Significato</span><span class="sxs-lookup"><span data-stu-id="1fa14-754">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="1fa14-755">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-755">0</span></span> | <span data-ttu-id="1fa14-756">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-756">0</span></span><br /><span data-ttu-id="1fa14-757">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-757">1</span></span> | <span data-ttu-id="1fa14-758">Esecuzione in modalità privilegiata</span><span class="sxs-lookup"><span data-stu-id="1fa14-758">Privileged mode execution</span></span><br /><span data-ttu-id="1fa14-759">Esecuzione in modalità utente</span><span class="sxs-lookup"><span data-stu-id="1fa14-759">User mode execution</span></span> |
| <span data-ttu-id="1fa14-760">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-760">1</span></span> | <span data-ttu-id="1fa14-761">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-761">0</span></span><br /><span data-ttu-id="1fa14-762">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-762">1</span></span> | <span data-ttu-id="1fa14-763">Nessuna protezione MPU</span><span class="sxs-lookup"><span data-stu-id="1fa14-763">No MPU protection</span></span><br /><span data-ttu-id="1fa14-764">Protezione MPU (è necessario selezionare la modalità utente)</span><span class="sxs-lookup"><span data-stu-id="1fa14-764">MPU protection (must have user mode selected)</span></span> |
| <span data-ttu-id="1fa14-765">2</span><span class="sxs-lookup"><span data-stu-id="1fa14-765">2</span></span> | <span data-ttu-id="1fa14-766">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-766">0</span></span><br /><span data-ttu-id="1fa14-767">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-767">1</span></span> | <span data-ttu-id="1fa14-768">Disabilitare l'accesso alla memoria condivisa/esterna</span><span class="sxs-lookup"><span data-stu-id="1fa14-768">Disable shared/external memory access</span></span><br /><span data-ttu-id="1fa14-769">Abilitare l'accesso alla memoria condivisa/esterna</span><span class="sxs-lookup"><span data-stu-id="1fa14-769">Enable shared/external memory access</span></span> |
| <span data-ttu-id="1fa14-770">[23-3]</span><span class="sxs-lookup"><span data-stu-id="1fa14-770">[23-3]</span></span> | <span data-ttu-id="1fa14-771">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-771">0</span></span> | <span data-ttu-id="1fa14-772">Riservato</span><span class="sxs-lookup"><span data-stu-id="1fa14-772">Reserved</span></span>
| <span data-ttu-id="1fa14-773">[31-24]</span><span class="sxs-lookup"><span data-stu-id="1fa14-773">[31-24]</span></span> | <br /><span data-ttu-id="1fa14-774">0x00</span><span class="sxs-lookup"><span data-stu-id="1fa14-774">0x00</span></span><br /><span data-ttu-id="1fa14-775">0x01</span><span class="sxs-lookup"><span data-stu-id="1fa14-775">0x01</span></span><br /><span data-ttu-id="1fa14-776">0x02</span><span class="sxs-lookup"><span data-stu-id="1fa14-776">0x02</span></span> | <span data-ttu-id="1fa14-777">**ID compilatore**</span><span class="sxs-lookup"><span data-stu-id="1fa14-777">**Compiler ID**</span></span><br /><span data-ttu-id="1fa14-778">IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-778">IAR</span></span><br /><span data-ttu-id="1fa14-779">ARM</span><span class="sxs-lookup"><span data-stu-id="1fa14-779">ARM</span></span><br /><span data-ttu-id="1fa14-780">GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-780">GNU</span></span> |

#### <a name="module-linker-for-cortex-m7-using-ac6"></a><span data-ttu-id="1fa14-781">Module linker per Cortex-M7 con AC6</span><span class="sxs-lookup"><span data-stu-id="1fa14-781">Module linker for Cortex-M7 using AC6</span></span>

<span data-ttu-id="1fa14-782">Non viene usato alcun file del linker.</span><span class="sxs-lookup"><span data-stu-id="1fa14-782">No linker file is used.</span></span> <span data-ttu-id="1fa14-783">Vedere Impostazioni progetto.</span><span class="sxs-lookup"><span data-stu-id="1fa14-783">See project settings.</span></span>

#### <a name="building-modules-for-cortex-m7-using-ac6"></a><span data-ttu-id="1fa14-784">Compilazione di moduli per Cortex-M7 con AC6</span><span class="sxs-lookup"><span data-stu-id="1fa14-784">Building Modules for Cortex-M7 using AC6</span></span>

<span data-ttu-id="1fa14-785">Viene fornita un'area di lavoro di esempio.</span><span class="sxs-lookup"><span data-stu-id="1fa14-785">An example workspace is provided.</span></span> <span data-ttu-id="1fa14-786">Compilare la libreria ThreadX, la libreria di moduli ThreadX, il progetto di modulo di esempio e il progetto di gestione moduli di esempio.</span><span class="sxs-lookup"><span data-stu-id="1fa14-786">Build the ThreadX library, ThreadX Modules library, sample module project, and sample module manager project.</span></span>

#### <a name="thread-extension-definition-for-cortex-m7-using-ac6"></a><span data-ttu-id="1fa14-787">Definizione di estensione di thread per Cortex-M7 con AC6</span><span class="sxs-lookup"><span data-stu-id="1fa14-787">Thread extension definition for Cortex-M7 using AC6</span></span>

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

#### <a name="building-module-manager-for-cortex-m7-using-ac6"></a><span data-ttu-id="1fa14-788">Compilazione di Module Manager per Cortex-M7 con AC6</span><span class="sxs-lookup"><span data-stu-id="1fa14-788">Building Module Manager for Cortex-M7 using AC6</span></span>

<span data-ttu-id="1fa14-789">Viene fornita un'area di lavoro di esempio.</span><span class="sxs-lookup"><span data-stu-id="1fa14-789">An example workspace is provided.</span></span> <span data-ttu-id="1fa14-790">Compilare la libreria ThreadX, la libreria di moduli ThreadX, il progetto di modulo di esempio e il progetto di gestione moduli di esempio.</span><span class="sxs-lookup"><span data-stu-id="1fa14-790">Build the ThreadX library, ThreadX Modules library, sample module project, and sample module manager project.</span></span>

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m7-using-ac6"></a><span data-ttu-id="1fa14-791">Attributi per la memoria esterna Abilita API per Cortex-M7 con AC6</span><span class="sxs-lookup"><span data-stu-id="1fa14-791">Attributes for external memory enable API for Cortex-M7 using AC6</span></span>

<span data-ttu-id="1fa14-792">Il modulo dispone sempre dell'accesso in lettura alla memoria condivisa.</span><span class="sxs-lookup"><span data-stu-id="1fa14-792">Module always has read access to shared memory.</span></span>
| <span data-ttu-id="1fa14-793">Parametro attribute</span><span class="sxs-lookup"><span data-stu-id="1fa14-793">Attribute parameter</span></span> | <span data-ttu-id="1fa14-794">Significato</span><span class="sxs-lookup"><span data-stu-id="1fa14-794">Meaning</span></span> |
|---|---|
| <span data-ttu-id="1fa14-795">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span><span class="sxs-lookup"><span data-stu-id="1fa14-795">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span></span> | <span data-ttu-id="1fa14-796">Accesso in scrittura</span><span class="sxs-lookup"><span data-stu-id="1fa14-796">Write access</span></span> |

### <a name="cortex-m7-using-gnu"></a><span data-ttu-id="1fa14-797">Cortex-M7 con GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-797">Cortex-M7 using GNU</span></span>

#### <a name="module-properties-for-cortex-m7-using-gnu"></a><span data-ttu-id="1fa14-798">Proprietà dei moduli per Cortex-M7 con GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-798">Module properties for Cortex-M7 using GNU</span></span>

| <span data-ttu-id="1fa14-799">bit</span><span class="sxs-lookup"><span data-stu-id="1fa14-799">Bit</span></span> | <span data-ttu-id="1fa14-800">Valore</span><span class="sxs-lookup"><span data-stu-id="1fa14-800">Value</span></span> | <span data-ttu-id="1fa14-801">Significato</span><span class="sxs-lookup"><span data-stu-id="1fa14-801">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="1fa14-802">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-802">0</span></span> | <span data-ttu-id="1fa14-803">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-803">0</span></span><br /><span data-ttu-id="1fa14-804">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-804">1</span></span> | <span data-ttu-id="1fa14-805">Esecuzione in modalità privilegiata</span><span class="sxs-lookup"><span data-stu-id="1fa14-805">Privileged mode execution</span></span><br /><span data-ttu-id="1fa14-806">Esecuzione in modalità utente</span><span class="sxs-lookup"><span data-stu-id="1fa14-806">User mode execution</span></span> |
| <span data-ttu-id="1fa14-807">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-807">1</span></span> | <span data-ttu-id="1fa14-808">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-808">0</span></span><br /><span data-ttu-id="1fa14-809">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-809">1</span></span> | <span data-ttu-id="1fa14-810">Nessuna protezione MPU</span><span class="sxs-lookup"><span data-stu-id="1fa14-810">No MPU protection</span></span><br /><span data-ttu-id="1fa14-811">Protezione MPU (è necessario selezionare la modalità utente)</span><span class="sxs-lookup"><span data-stu-id="1fa14-811">MPU protection (must have user mode selected)</span></span> |
| <span data-ttu-id="1fa14-812">2</span><span class="sxs-lookup"><span data-stu-id="1fa14-812">2</span></span> | <span data-ttu-id="1fa14-813">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-813">0</span></span><br /><span data-ttu-id="1fa14-814">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-814">1</span></span> | <span data-ttu-id="1fa14-815">Disabilitare l'accesso alla memoria condivisa/esterna</span><span class="sxs-lookup"><span data-stu-id="1fa14-815">Disable shared/external memory access</span></span><br /><span data-ttu-id="1fa14-816">Abilitare l'accesso alla memoria condivisa/esterna</span><span class="sxs-lookup"><span data-stu-id="1fa14-816">Enable shared/external memory access</span></span> |
| <span data-ttu-id="1fa14-817">[23-3]</span><span class="sxs-lookup"><span data-stu-id="1fa14-817">[23-3]</span></span> | <span data-ttu-id="1fa14-818">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-818">0</span></span> | <span data-ttu-id="1fa14-819">Riservato</span><span class="sxs-lookup"><span data-stu-id="1fa14-819">Reserved</span></span>
| <span data-ttu-id="1fa14-820">[31-24]</span><span class="sxs-lookup"><span data-stu-id="1fa14-820">[31-24]</span></span> | <br /><span data-ttu-id="1fa14-821">0x00</span><span class="sxs-lookup"><span data-stu-id="1fa14-821">0x00</span></span><br /><span data-ttu-id="1fa14-822">0x01</span><span class="sxs-lookup"><span data-stu-id="1fa14-822">0x01</span></span><br /><span data-ttu-id="1fa14-823">0x02</span><span class="sxs-lookup"><span data-stu-id="1fa14-823">0x02</span></span> | <span data-ttu-id="1fa14-824">**ID compilatore**</span><span class="sxs-lookup"><span data-stu-id="1fa14-824">**Compiler ID**</span></span><br /><span data-ttu-id="1fa14-825">IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-825">IAR</span></span><br /><span data-ttu-id="1fa14-826">ARM</span><span class="sxs-lookup"><span data-stu-id="1fa14-826">ARM</span></span><br /><span data-ttu-id="1fa14-827">GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-827">GNU</span></span> |

#### <a name="module-linker-for-cortex-m7-using-gnu"></a><span data-ttu-id="1fa14-828">Module linker per Cortex-M7 con GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-828">Module linker for Cortex-M7 using GNU</span></span>

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

#### <a name="building-modules-for-cortex-m7-using-gnu"></a><span data-ttu-id="1fa14-829">Compilazione di moduli per Cortex-M7 con GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-829">Building Modules for Cortex-M7 using GNU</span></span>

<span data-ttu-id="1fa14-830">Vedere build_threadx_module_sample.bat:</span><span class="sxs-lookup"><span data-stu-id="1fa14-830">See build_threadx_module_sample.bat:</span></span>

```dos
arm-none-eabi-gcc -c -g -mcpu=cortex-m7 -mfloat-abi=hard -mfpu=fpv5-d16 -fpie -fno-plt -mpic-data-is-text-relative -msingle-pic-base txm_module_preamble.s
arm-none-eabi-gcc -c -g -mcpu=cortex-m7 -mfloat-abi=hard -mfpu=fpv5-d16 -fpie -fno-plt -mpic-data-is-text-relative -msingle-pic-base gcc_setup.S
arm-none-eabi-gcc -c -g -mcpu=cortex-m7 -mfloat-abi=hard -mfpu=fpv5-d16 -fpie -fno-plt -mpic-data-is-text-relative -msingle-pic-base -I..\inc -I..\..\..\..\common\inc -I..\..\..\..\common_modules\inc sample_threadx_module.c
arm-none-eabi-ld -A cortex-m7 -T sample_threadx_module.ld txm_module_preamble.o gcc_setup.o sample_threadx_module.o -e _txm_module_thread_shell_entry txm.a -o sample_threadx_module.axf -M > sample_threadx_module.map
```

#### <a name="thread-extension-definition-for-cortex-m7-using-gnu"></a><span data-ttu-id="1fa14-831">Definizione di estensione di thread per Cortex-M7 con GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-831">Thread extension definition for Cortex-M7 using GNU</span></span>

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

#### <a name="building-module-manager-for-cortex-m7-using-gnu"></a><span data-ttu-id="1fa14-832">Compilazione di Module Manager per Cortex-M7 con GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-832">Building Module Manager for Cortex-M7 using GNU</span></span>

<span data-ttu-id="1fa14-833">Vedere build_threadx_module_manager_sample.bat:</span><span class="sxs-lookup"><span data-stu-id="1fa14-833">See build_threadx_module_manager_sample.bat:</span></span>

```dos
arm-none-eabi-gcc -c -g -mcpu=cortex-m7 -mfloat-abi=hard -mfpu=fpv5-d16 -mthumb -I..\inc -I..\..\..\..\common\inc -I..\..\..\..\common_modules\inc sample_threadx_module_manager.c
arm-none-eabi-gcc -c -g -mcpu=cortex-m7 -mfloat-abi=hard -mfpu=fpv5-d16 -mthumb tx_simulator_startup.S
arm-none-eabi-gcc -c -g -mcpu=cortex-m7 -mfloat-abi=hard -mfpu=fpv5-d16 -mthumb cortexm_crt0.S
arm-none-eabi-gcc -g -mcpu=cortex-m7 -mfloat-abi=hard -mfpu=fpv5-d16 -mthumb -nostartfiles -ereset_handler -T sample_threadx.ld tx_simulator_startup.o cortexm_crt0.o sample_threadx_module_manager.o tx.a -o sample_threadx_module_manager.axf -Wl,-Map=sample_threadx_module_manager.map
```

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m7-using-gnu"></a><span data-ttu-id="1fa14-834">Attributi per la memoria esterna Abilita API per Cortex-M7 con GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-834">Attributes for external memory enable API for Cortex-M7 using GNU</span></span>

<span data-ttu-id="1fa14-835">Il modulo dispone sempre dell'accesso in lettura alla memoria condivisa.</span><span class="sxs-lookup"><span data-stu-id="1fa14-835">Module always has read access to shared memory.</span></span>
| <span data-ttu-id="1fa14-836">Parametro attribute</span><span class="sxs-lookup"><span data-stu-id="1fa14-836">Attribute parameter</span></span> | <span data-ttu-id="1fa14-837">Significato</span><span class="sxs-lookup"><span data-stu-id="1fa14-837">Meaning</span></span> |
|---|---|
| <span data-ttu-id="1fa14-838">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span><span class="sxs-lookup"><span data-stu-id="1fa14-838">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span></span> | <span data-ttu-id="1fa14-839">Accesso in scrittura</span><span class="sxs-lookup"><span data-stu-id="1fa14-839">Write access</span></span> |

### <a name="cortex-m7-using-iar"></a><span data-ttu-id="1fa14-840">Cortex-M7 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-840">Cortex-M7 using IAR</span></span>

#### <a name="module-preamble-for-cortex-m7-using-iar"></a><span data-ttu-id="1fa14-841">Preambolo del modulo per Cortex-M7 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-841">Module preamble for Cortex-M7 using IAR</span></span>

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

#### <a name="module-properties-for-cortex-m7-using-iar"></a><span data-ttu-id="1fa14-842">Proprietà dei moduli per Cortex-M7 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-842">Module properties for Cortex-M7 using IAR</span></span>

| <span data-ttu-id="1fa14-843">bit</span><span class="sxs-lookup"><span data-stu-id="1fa14-843">Bit</span></span> | <span data-ttu-id="1fa14-844">Valore</span><span class="sxs-lookup"><span data-stu-id="1fa14-844">Value</span></span> | <span data-ttu-id="1fa14-845">Significato</span><span class="sxs-lookup"><span data-stu-id="1fa14-845">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="1fa14-846">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-846">0</span></span> | <span data-ttu-id="1fa14-847">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-847">0</span></span><br /><span data-ttu-id="1fa14-848">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-848">1</span></span> | <span data-ttu-id="1fa14-849">Esecuzione in modalità privilegiata</span><span class="sxs-lookup"><span data-stu-id="1fa14-849">Privileged mode execution</span></span><br /><span data-ttu-id="1fa14-850">Esecuzione in modalità utente</span><span class="sxs-lookup"><span data-stu-id="1fa14-850">User mode execution</span></span> |
| <span data-ttu-id="1fa14-851">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-851">1</span></span> | <span data-ttu-id="1fa14-852">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-852">0</span></span><br /><span data-ttu-id="1fa14-853">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-853">1</span></span> | <span data-ttu-id="1fa14-854">Nessuna protezione MPU</span><span class="sxs-lookup"><span data-stu-id="1fa14-854">No MPU protection</span></span><br /><span data-ttu-id="1fa14-855">Protezione MPU (è necessario selezionare la modalità utente)</span><span class="sxs-lookup"><span data-stu-id="1fa14-855">MPU protection (must have user mode selected)</span></span> |
| <span data-ttu-id="1fa14-856">2</span><span class="sxs-lookup"><span data-stu-id="1fa14-856">2</span></span> | <span data-ttu-id="1fa14-857">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-857">0</span></span><br /><span data-ttu-id="1fa14-858">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-858">1</span></span> | <span data-ttu-id="1fa14-859">Disabilitare l'accesso alla memoria condivisa/esterna</span><span class="sxs-lookup"><span data-stu-id="1fa14-859">Disable shared/external memory access</span></span><br /><span data-ttu-id="1fa14-860">Abilitare l'accesso alla memoria condivisa/esterna</span><span class="sxs-lookup"><span data-stu-id="1fa14-860">Enable shared/external memory access</span></span> |
| <span data-ttu-id="1fa14-861">[23-3]</span><span class="sxs-lookup"><span data-stu-id="1fa14-861">[23-3]</span></span> | <span data-ttu-id="1fa14-862">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-862">0</span></span> | <span data-ttu-id="1fa14-863">Riservato</span><span class="sxs-lookup"><span data-stu-id="1fa14-863">Reserved</span></span>
| <span data-ttu-id="1fa14-864">[31-24]</span><span class="sxs-lookup"><span data-stu-id="1fa14-864">[31-24]</span></span> | <br /><span data-ttu-id="1fa14-865">0x00</span><span class="sxs-lookup"><span data-stu-id="1fa14-865">0x00</span></span><br /><span data-ttu-id="1fa14-866">0x01</span><span class="sxs-lookup"><span data-stu-id="1fa14-866">0x01</span></span><br /><span data-ttu-id="1fa14-867">0x02</span><span class="sxs-lookup"><span data-stu-id="1fa14-867">0x02</span></span> | <span data-ttu-id="1fa14-868">**ID compilatore**</span><span class="sxs-lookup"><span data-stu-id="1fa14-868">**Compiler ID**</span></span><br /><span data-ttu-id="1fa14-869">IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-869">IAR</span></span><br /><span data-ttu-id="1fa14-870">ARM</span><span class="sxs-lookup"><span data-stu-id="1fa14-870">ARM</span></span><br /><span data-ttu-id="1fa14-871">GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-871">GNU</span></span> |

#### <a name="module-linker-for-cortex-m7-using-iar"></a><span data-ttu-id="1fa14-872">Module linker per Cortex-M7 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-872">Module linker for Cortex-M7 using IAR</span></span>

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

#### <a name="building-modules-for-cortex-m7-using-iar"></a><span data-ttu-id="1fa14-873">Compilazione di moduli per Cortex-M7 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-873">Building Modules for Cortex-M7 using IAR</span></span>

<span data-ttu-id="1fa14-874">Viene fornita un'area di lavoro di esempio.</span><span class="sxs-lookup"><span data-stu-id="1fa14-874">An example workspace is provided.</span></span> <span data-ttu-id="1fa14-875">Compilare la libreria ThreadX, la libreria di moduli ThreadX, il progetto del modulo demo e il progetto di gestione moduli dimostrativi.</span><span class="sxs-lookup"><span data-stu-id="1fa14-875">Build the ThreadX library, ThreadX Modules library, demo module project, and demo module manager project.</span></span>

#### <a name="thread-extension-definition-for-cortex-m7-using-iar"></a><span data-ttu-id="1fa14-876">Definizione di estensione di thread per Cortex-M7 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-876">Thread extension definition for Cortex-M7 using IAR</span></span>

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

#### <a name="building-module-manager-for-cortex-m7-using-iar"></a><span data-ttu-id="1fa14-877">Compilazione di Module Manager per Cortex-M7 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-877">Building Module Manager for Cortex-M7 using IAR</span></span>

<span data-ttu-id="1fa14-878">Viene fornita un'area di lavoro di esempio.</span><span class="sxs-lookup"><span data-stu-id="1fa14-878">An example workspace is provided.</span></span> <span data-ttu-id="1fa14-879">Compilare la libreria ThreadX, la libreria di moduli ThreadX, il progetto del modulo demo e il progetto di gestione moduli dimostrativi.</span><span class="sxs-lookup"><span data-stu-id="1fa14-879">Build the ThreadX library, ThreadX Modules library, demo module project, and demo module manager project.</span></span>

#### <a name="attributes-for-external-memory-enable-api-for-cortex-m7-using-iar"></a><span data-ttu-id="1fa14-880">Attributi per la memoria esterna Abilita API per Cortex-M7 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-880">Attributes for external memory enable API for Cortex-M7 using IAR</span></span>

<span data-ttu-id="1fa14-881">Il modulo dispone sempre dell'accesso in lettura alla memoria condivisa.</span><span class="sxs-lookup"><span data-stu-id="1fa14-881">Module always has read access to shared memory.</span></span>
| <span data-ttu-id="1fa14-882">Parametro attribute</span><span class="sxs-lookup"><span data-stu-id="1fa14-882">Attribute parameter</span></span> | <span data-ttu-id="1fa14-883">Significato</span><span class="sxs-lookup"><span data-stu-id="1fa14-883">Meaning</span></span> |
|---|---|
| <span data-ttu-id="1fa14-884">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span><span class="sxs-lookup"><span data-stu-id="1fa14-884">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span></span> | <span data-ttu-id="1fa14-885">Accesso in scrittura</span><span class="sxs-lookup"><span data-stu-id="1fa14-885">Write access</span></span> |

## <a name="cortex-r4-processor"></a><span data-ttu-id="1fa14-886">Processore Cortex-R4</span><span class="sxs-lookup"><span data-stu-id="1fa14-886">Cortex-R4 processor</span></span>

### <a name="cortex-r4-using-ac6"></a><span data-ttu-id="1fa14-887">Cortex-R4 con AC6</span><span class="sxs-lookup"><span data-stu-id="1fa14-887">Cortex-R4 using AC6</span></span>

#### <a name="module-preamble-for-cortex-r4-using-ac6"></a><span data-ttu-id="1fa14-888">Preambolo del modulo per Cortex-R4 con AC6</span><span class="sxs-lookup"><span data-stu-id="1fa14-888">Module preamble for Cortex-R4 using AC6</span></span>

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

#### <a name="module-properties-for-cortex-r4-using-ac6"></a><span data-ttu-id="1fa14-889">Proprietà dei moduli per Cortex-R4 con AC6</span><span class="sxs-lookup"><span data-stu-id="1fa14-889">Module properties for Cortex-R4 using AC6</span></span>

| <span data-ttu-id="1fa14-890">bit</span><span class="sxs-lookup"><span data-stu-id="1fa14-890">Bit</span></span> | <span data-ttu-id="1fa14-891">Valore</span><span class="sxs-lookup"><span data-stu-id="1fa14-891">Value</span></span> | <span data-ttu-id="1fa14-892">Significato</span><span class="sxs-lookup"><span data-stu-id="1fa14-892">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="1fa14-893">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-893">0</span></span> | <span data-ttu-id="1fa14-894">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-894">0</span></span><br /><span data-ttu-id="1fa14-895">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-895">1</span></span> | <span data-ttu-id="1fa14-896">Esecuzione in modalità privilegiata</span><span class="sxs-lookup"><span data-stu-id="1fa14-896">Privileged mode execution</span></span><br /><span data-ttu-id="1fa14-897">Esecuzione in modalità utente</span><span class="sxs-lookup"><span data-stu-id="1fa14-897">User mode execution</span></span> |
| <span data-ttu-id="1fa14-898">[23-1]</span><span class="sxs-lookup"><span data-stu-id="1fa14-898">[23-1]</span></span> | <span data-ttu-id="1fa14-899">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-899">0</span></span> | <span data-ttu-id="1fa14-900">Riservato</span><span class="sxs-lookup"><span data-stu-id="1fa14-900">Reserved</span></span>
| <span data-ttu-id="1fa14-901">[31-24]</span><span class="sxs-lookup"><span data-stu-id="1fa14-901">[31-24]</span></span> | <br /><span data-ttu-id="1fa14-902">0x00</span><span class="sxs-lookup"><span data-stu-id="1fa14-902">0x00</span></span><br /><span data-ttu-id="1fa14-903">0x01</span><span class="sxs-lookup"><span data-stu-id="1fa14-903">0x01</span></span><br /><span data-ttu-id="1fa14-904">0x02</span><span class="sxs-lookup"><span data-stu-id="1fa14-904">0x02</span></span> | <span data-ttu-id="1fa14-905">**ID compilatore**</span><span class="sxs-lookup"><span data-stu-id="1fa14-905">**Compiler ID**</span></span><br /><span data-ttu-id="1fa14-906">IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-906">IAR</span></span><br /><span data-ttu-id="1fa14-907">ARM</span><span class="sxs-lookup"><span data-stu-id="1fa14-907">ARM</span></span><br /><span data-ttu-id="1fa14-908">GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-908">GNU</span></span> |

#### <a name="module-linker-for-cortex-r4-using-ac6"></a><span data-ttu-id="1fa14-909">Module linker per Cortex-R4 con AC6</span><span class="sxs-lookup"><span data-stu-id="1fa14-909">Module linker for Cortex-R4 using AC6</span></span>

<span data-ttu-id="1fa14-910">Compilato dalla riga di comando, nessun esempio di file del linker.</span><span class="sxs-lookup"><span data-stu-id="1fa14-910">Built on command-line, no linker file example.</span></span>

#### <a name="building-modules-for-cortex-r4-using-ac6"></a><span data-ttu-id="1fa14-911">Compilazione di moduli per Cortex-R4 con AC6</span><span class="sxs-lookup"><span data-stu-id="1fa14-911">Building Modules for Cortex-R4 using AC6</span></span>

<span data-ttu-id="1fa14-912">Un semplice esempio di riga di comando per la compilazione di un modulo Cortex-R4 con AC6:</span><span class="sxs-lookup"><span data-stu-id="1fa14-912">A simple command-line example for building a Cortex-R4 module using AC6:</span></span>

```dos
armclang -c -g -fropi -frwpi --target=arm-arm-none-eabi -mcpu=cortex-r4 demo_threadx_module.c
armclang -c -g -fropi -frwpi --target=arm-arm-none-eabi -mcpu=cortex-r4 txm_module_preamble.S
armclang -c -g -fropi -frwpi --target=arm-arm-none-eabi -mcpu=cortex-r4 semihosting.c
armlink -d -o demo_threadx_module.axf --elf --ro 0x00100000 --first txm_module_preamble.o --entry=_txm_module_thread_shell_entry --ropi --rwpi --remove --map --symbols --datacompressor=off --list demo_threadx_module.map txm_module_preamble.o demo_threadx_module.o semihosting.o txm.a
```

#### <a name="thread-extension-definition-for-cortex-r4-using-ac6"></a><span data-ttu-id="1fa14-913">Definizione dell'estensione di thread per Cortex-R4 con AC6</span><span class="sxs-lookup"><span data-stu-id="1fa14-913">Thread extension definition for Cortex-R4 using AC6</span></span>

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

#### <a name="building-module-manager-for-cortex-r4-using-ac6"></a><span data-ttu-id="1fa14-914">Compilazione di Module Manager per Cortex-R4 con AC6</span><span class="sxs-lookup"><span data-stu-id="1fa14-914">Building Module Manager for Cortex-R4 using AC6</span></span>

<span data-ttu-id="1fa14-915">Un semplice esempio di riga di comando per la creazione di un modulo di gestione dei moduli Cortex-R4 con AC6:</span><span class="sxs-lookup"><span data-stu-id="1fa14-915">A simple command-line example for building a Cortex-R4 module manager using AC6:</span></span>

```dos
armclang -c -g --target=arm-arm-none-eabi -mcpu=cortex-r4 demo_threadx_module_manager.c
armclang -c -g --target=arm-arm-none-eabi -mcpu=cortex-r4 timer.c
armclang -c -g --target=arm-arm-none-eabi -mcpu=cortex-r4 gic.c
armclang -c -g --target=arm-arm-none-eabi -mcpu=cortex-r4 tx_initialize_low_level.S
armclang -c -g --target=arm-arm-none-eabi -mcpu=cortex-r4 startup.S
armlink -d -o demo_threadx_module_manager.axf --elf --scatter=demo_threadx.scat --remove --map --symbols --list demo_threadx_module_manager.map startup.o timer.o gic.o demo_threadx_module_manager.o tx_initialize_low_level.o tx.a
```

#### <a name="attributes-for-external-memory-enable-api-for-cortex-r4-using-ac6"></a><span data-ttu-id="1fa14-916">Attributi per la memoria esterna Abilita API per Cortex-R4 con AC6</span><span class="sxs-lookup"><span data-stu-id="1fa14-916">Attributes for external memory enable API for Cortex-R4 using AC6</span></span>

<span data-ttu-id="1fa14-917">Il modulo dispone sempre dell'accesso in lettura alla memoria condivisa.</span><span class="sxs-lookup"><span data-stu-id="1fa14-917">Module always has read access to shared memory.</span></span>
| <span data-ttu-id="1fa14-918">Parametro attribute</span><span class="sxs-lookup"><span data-stu-id="1fa14-918">Attribute parameter</span></span> | <span data-ttu-id="1fa14-919">Significato</span><span class="sxs-lookup"><span data-stu-id="1fa14-919">Meaning</span></span> |
|---|---|
| <span data-ttu-id="1fa14-920">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span><span class="sxs-lookup"><span data-stu-id="1fa14-920">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span></span> | <span data-ttu-id="1fa14-921">Accesso in scrittura</span><span class="sxs-lookup"><span data-stu-id="1fa14-921">Write access</span></span> |

### <a name="cortex-r4-using-iar"></a><span data-ttu-id="1fa14-922">Cortex-R4 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-922">Cortex-R4 using IAR</span></span>

#### <a name="module-preamble-for-cortex-r4-using-iar"></a><span data-ttu-id="1fa14-923">Preambolo del modulo per Cortex-R4 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-923">Module preamble for Cortex-R4 using IAR</span></span>

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

#### <a name="module-properties-for-cortex-r4-using-iar"></a><span data-ttu-id="1fa14-924">Proprietà dei moduli per Cortex-R4 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-924">Module properties for Cortex-R4 using IAR</span></span>

| <span data-ttu-id="1fa14-925">bit</span><span class="sxs-lookup"><span data-stu-id="1fa14-925">Bit</span></span> | <span data-ttu-id="1fa14-926">Valore</span><span class="sxs-lookup"><span data-stu-id="1fa14-926">Value</span></span> | <span data-ttu-id="1fa14-927">Significato</span><span class="sxs-lookup"><span data-stu-id="1fa14-927">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="1fa14-928">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-928">0</span></span> | <span data-ttu-id="1fa14-929">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-929">0</span></span><br /><span data-ttu-id="1fa14-930">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-930">1</span></span> | <span data-ttu-id="1fa14-931">Esecuzione in modalità privilegiata</span><span class="sxs-lookup"><span data-stu-id="1fa14-931">Privileged mode execution</span></span><br /><span data-ttu-id="1fa14-932">Esecuzione in modalità utente</span><span class="sxs-lookup"><span data-stu-id="1fa14-932">User mode execution</span></span> |
| <span data-ttu-id="1fa14-933">[23-1]</span><span class="sxs-lookup"><span data-stu-id="1fa14-933">[23-1]</span></span> | <span data-ttu-id="1fa14-934">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-934">0</span></span> | <span data-ttu-id="1fa14-935">Riservato</span><span class="sxs-lookup"><span data-stu-id="1fa14-935">Reserved</span></span>
| <span data-ttu-id="1fa14-936">[31-24]</span><span class="sxs-lookup"><span data-stu-id="1fa14-936">[31-24]</span></span> | <br /><span data-ttu-id="1fa14-937">0x00</span><span class="sxs-lookup"><span data-stu-id="1fa14-937">0x00</span></span><br /><span data-ttu-id="1fa14-938">0x01</span><span class="sxs-lookup"><span data-stu-id="1fa14-938">0x01</span></span><br /><span data-ttu-id="1fa14-939">0x02</span><span class="sxs-lookup"><span data-stu-id="1fa14-939">0x02</span></span> | <span data-ttu-id="1fa14-940">**ID compilatore**</span><span class="sxs-lookup"><span data-stu-id="1fa14-940">**Compiler ID**</span></span><br /><span data-ttu-id="1fa14-941">IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-941">IAR</span></span><br /><span data-ttu-id="1fa14-942">ARM</span><span class="sxs-lookup"><span data-stu-id="1fa14-942">ARM</span></span><br /><span data-ttu-id="1fa14-943">GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-943">GNU</span></span> |

#### <a name="module-linker-for-cortex-r4-using-iar"></a><span data-ttu-id="1fa14-944">Module linker per Cortex-R4 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-944">Module linker for Cortex-R4 using IAR</span></span>

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

#### <a name="building-modules-for-cortex-r4-using-iar"></a><span data-ttu-id="1fa14-945">Compilazione di moduli per Cortex-R4 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-945">Building Modules for Cortex-R4 using IAR</span></span>

<span data-ttu-id="1fa14-946">Viene fornita un'area di lavoro di esempio.</span><span class="sxs-lookup"><span data-stu-id="1fa14-946">An example workspace is provided.</span></span> <span data-ttu-id="1fa14-947">Compilare la libreria ThreadX, la libreria di moduli ThreadX, il progetto del modulo demo e il progetto di gestione moduli dimostrativi.</span><span class="sxs-lookup"><span data-stu-id="1fa14-947">Build the ThreadX library, ThreadX Modules library, demo module project, and demo module manager project.</span></span>

#### <a name="thread-extension-definition-for-cortex-r4-using-iar"></a><span data-ttu-id="1fa14-948">Definizione dell'estensione di thread per Cortex-R4 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-948">Thread extension definition for Cortex-R4 using IAR</span></span>

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

#### <a name="building-module-manager-for-cortex-r4-using-iar"></a><span data-ttu-id="1fa14-949">Compilazione di Module Manager per Cortex-R4 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-949">Building Module Manager for Cortex-R4 using IAR</span></span>

<span data-ttu-id="1fa14-950">Viene fornita un'area di lavoro di esempio.</span><span class="sxs-lookup"><span data-stu-id="1fa14-950">An example workspace is provided.</span></span> <span data-ttu-id="1fa14-951">Compilare la libreria ThreadX, la libreria di moduli ThreadX, il progetto del modulo demo e il progetto di gestione moduli dimostrativi.</span><span class="sxs-lookup"><span data-stu-id="1fa14-951">Build the ThreadX library, ThreadX Modules library, demo module project, and demo module manager project.</span></span>

#### <a name="attributes-for-external-memory-enable-api-for-cortex-r4-using-iar"></a><span data-ttu-id="1fa14-952">Attributi per la memoria esterna Abilita API per Cortex-R4 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-952">Attributes for external memory enable API for Cortex-R4 using IAR</span></span>

<span data-ttu-id="1fa14-953">Il modulo dispone sempre dell'accesso in lettura alla memoria condivisa.</span><span class="sxs-lookup"><span data-stu-id="1fa14-953">Module always has read access to shared memory.</span></span>
| <span data-ttu-id="1fa14-954">Parametro attribute</span><span class="sxs-lookup"><span data-stu-id="1fa14-954">Attribute parameter</span></span> | <span data-ttu-id="1fa14-955">Significato</span><span class="sxs-lookup"><span data-stu-id="1fa14-955">Meaning</span></span> |
|---|---|
| <span data-ttu-id="1fa14-956">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span><span class="sxs-lookup"><span data-stu-id="1fa14-956">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span></span> | <span data-ttu-id="1fa14-957">Accesso in scrittura</span><span class="sxs-lookup"><span data-stu-id="1fa14-957">Write access</span></span> |

## <a name="mcf544xx-processor"></a><span data-ttu-id="1fa14-958">Processore MCF544xx</span><span class="sxs-lookup"><span data-stu-id="1fa14-958">MCF544xx processor</span></span>

### <a name="mcf544xx-using-ghs"></a><span data-ttu-id="1fa14-959">MCF544xx con GHS</span><span class="sxs-lookup"><span data-stu-id="1fa14-959">MCF544xx using GHS</span></span>

#### <a name="module-preamble-for-mcf544xx-using-ghs"></a><span data-ttu-id="1fa14-960">Preambolo del modulo per MCF544xx con GHS</span><span class="sxs-lookup"><span data-stu-id="1fa14-960">Module preamble for MCF544xx using GHS</span></span>

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

#### <a name="module-properties-for-mcf544xx-using-ghs"></a><span data-ttu-id="1fa14-961">Proprietà del modulo per MCF544xx con GHS</span><span class="sxs-lookup"><span data-stu-id="1fa14-961">Module properties for MCF544xx using GHS</span></span>

| <span data-ttu-id="1fa14-962">bit</span><span class="sxs-lookup"><span data-stu-id="1fa14-962">Bit</span></span> | <span data-ttu-id="1fa14-963">Valore</span><span class="sxs-lookup"><span data-stu-id="1fa14-963">Value</span></span> | <span data-ttu-id="1fa14-964">Significato</span><span class="sxs-lookup"><span data-stu-id="1fa14-964">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="1fa14-965">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-965">0</span></span> | <span data-ttu-id="1fa14-966">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-966">0</span></span><br /><span data-ttu-id="1fa14-967">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-967">1</span></span> | <span data-ttu-id="1fa14-968">Esecuzione in modalità privilegiata</span><span class="sxs-lookup"><span data-stu-id="1fa14-968">Privileged mode execution</span></span><br /><span data-ttu-id="1fa14-969">Esecuzione in modalità utente</span><span class="sxs-lookup"><span data-stu-id="1fa14-969">User mode execution</span></span> |
| <span data-ttu-id="1fa14-970">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-970">1</span></span> | <span data-ttu-id="1fa14-971">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-971">0</span></span><br /><span data-ttu-id="1fa14-972">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-972">1</span></span> | <span data-ttu-id="1fa14-973">Nessuna protezione da MMU</span><span class="sxs-lookup"><span data-stu-id="1fa14-973">No MMU protection</span></span><br /><span data-ttu-id="1fa14-974">Protezione da MMU (è necessario selezionare la modalità utente)</span><span class="sxs-lookup"><span data-stu-id="1fa14-974">MMU protection (must have user mode selected)</span></span> |
| <span data-ttu-id="1fa14-975">2</span><span class="sxs-lookup"><span data-stu-id="1fa14-975">2</span></span> | <span data-ttu-id="1fa14-976">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-976">0</span></span><br /><span data-ttu-id="1fa14-977">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-977">1</span></span> | <span data-ttu-id="1fa14-978">Disabilitare l'accesso alla memoria condivisa/esterna</span><span class="sxs-lookup"><span data-stu-id="1fa14-978">Disable shared/external memory access</span></span><br /><span data-ttu-id="1fa14-979">Abilitare l'accesso alla memoria condivisa/esterna</span><span class="sxs-lookup"><span data-stu-id="1fa14-979">Enable shared/external memory access</span></span> |
| <span data-ttu-id="1fa14-980">[23-3]</span><span class="sxs-lookup"><span data-stu-id="1fa14-980">[23-3]</span></span> | <span data-ttu-id="1fa14-981">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-981">0</span></span> | <span data-ttu-id="1fa14-982">Riservato</span><span class="sxs-lookup"><span data-stu-id="1fa14-982">Reserved</span></span>
| <span data-ttu-id="1fa14-983">[31-24]</span><span class="sxs-lookup"><span data-stu-id="1fa14-983">[31-24]</span></span> | <br /><span data-ttu-id="1fa14-984">0x03</span><span class="sxs-lookup"><span data-stu-id="1fa14-984">0x03</span></span> | <span data-ttu-id="1fa14-985">**ID compilatore**</span><span class="sxs-lookup"><span data-stu-id="1fa14-985">**Compiler ID**</span></span><br /><span data-ttu-id="1fa14-986">GHS</span><span class="sxs-lookup"><span data-stu-id="1fa14-986">GHS</span></span> |

#### <a name="module-linker-for-mcf544xx-using-ghs"></a><span data-ttu-id="1fa14-987">Modulo linker per MCF544xx con GHS</span><span class="sxs-lookup"><span data-stu-id="1fa14-987">Module linker for MCF544xx using GHS</span></span>

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

#### <a name="building-modules-for-mcf544xx-using-ghs"></a><span data-ttu-id="1fa14-988">Compilazione di moduli per MCF544xx con GHS</span><span class="sxs-lookup"><span data-stu-id="1fa14-988">Building Modules for MCF544xx using GHS</span></span>

<span data-ttu-id="1fa14-989">Viene fornita un'area di lavoro di esempio.</span><span class="sxs-lookup"><span data-stu-id="1fa14-989">An example workspace is provided.</span></span> <span data-ttu-id="1fa14-990">Compilare la libreria ThreadX, la libreria di moduli ThreadX, il progetto del modulo demo e il progetto di gestione moduli dimostrativi.</span><span class="sxs-lookup"><span data-stu-id="1fa14-990">Build the ThreadX library, ThreadX Modules library, demo module project, and demo module manager project.</span></span>

#### <a name="thread-extension-definition-for-mcf544xx-using-ghs"></a><span data-ttu-id="1fa14-991">Definizione dell'estensione di thread per MCF544xx con GHS</span><span class="sxs-lookup"><span data-stu-id="1fa14-991">Thread extension definition for MCF544xx using GHS</span></span>

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

#### <a name="building-module-manager-for-mcf544xx-using-ghs"></a><span data-ttu-id="1fa14-992">Compilazione di gestione moduli per MCF544xx con GHS</span><span class="sxs-lookup"><span data-stu-id="1fa14-992">Building Module Manager for MCF544xx using GHS</span></span>

<span data-ttu-id="1fa14-993">Viene fornita un'area di lavoro di esempio.</span><span class="sxs-lookup"><span data-stu-id="1fa14-993">An example workspace is provided.</span></span> <span data-ttu-id="1fa14-994">Compilare la libreria ThreadX, la libreria di moduli ThreadX, il progetto del modulo demo e il progetto di gestione moduli dimostrativi.</span><span class="sxs-lookup"><span data-stu-id="1fa14-994">Build the ThreadX library, ThreadX Modules library, demo module project, and demo module manager project.</span></span>

#### <a name="attributes-for-external-memory-enable-api-for-mcf544xx-using-ghs"></a><span data-ttu-id="1fa14-995">Attributi per la memoria esterna Abilita API per MCF544xx con GHS</span><span class="sxs-lookup"><span data-stu-id="1fa14-995">Attributes for external memory enable API for MCF544xx using GHS</span></span>

<span data-ttu-id="1fa14-996">Questa funzionalità non è abilitata in MCF544xx.</span><span class="sxs-lookup"><span data-stu-id="1fa14-996">This feature not enabled on MCF544xx.</span></span>

## <a name="rx63-processor"></a><span data-ttu-id="1fa14-997">Processore RX63</span><span class="sxs-lookup"><span data-stu-id="1fa14-997">RX63 processor</span></span>

### <a name="rx63-using-iar"></a><span data-ttu-id="1fa14-998">RX63 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-998">RX63 using IAR</span></span>

#### <a name="module-preamble-for-rx63-using-iar"></a><span data-ttu-id="1fa14-999">Preambolo del modulo per RX63 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-999">Module preamble for RX63 using IAR</span></span>

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

#### <a name="module-properties-for-rx63-using-iar"></a><span data-ttu-id="1fa14-1000">Proprietà del modulo per RX63 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-1000">Module properties for RX63 using IAR</span></span>

| <span data-ttu-id="1fa14-1001">bit</span><span class="sxs-lookup"><span data-stu-id="1fa14-1001">Bit</span></span> | <span data-ttu-id="1fa14-1002">Valore</span><span class="sxs-lookup"><span data-stu-id="1fa14-1002">Value</span></span> | <span data-ttu-id="1fa14-1003">Significato</span><span class="sxs-lookup"><span data-stu-id="1fa14-1003">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="1fa14-1004">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-1004">0</span></span> | <span data-ttu-id="1fa14-1005">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-1005">0</span></span><br /><span data-ttu-id="1fa14-1006">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-1006">1</span></span> | <span data-ttu-id="1fa14-1007">Esecuzione in modalità privilegiata</span><span class="sxs-lookup"><span data-stu-id="1fa14-1007">Privileged mode execution</span></span><br /><span data-ttu-id="1fa14-1008">Esecuzione in modalità utente</span><span class="sxs-lookup"><span data-stu-id="1fa14-1008">User mode execution</span></span> |
| <span data-ttu-id="1fa14-1009">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-1009">1</span></span> | <span data-ttu-id="1fa14-1010">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-1010">0</span></span><br /><span data-ttu-id="1fa14-1011">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-1011">1</span></span> | <span data-ttu-id="1fa14-1012">Nessuna protezione MPU</span><span class="sxs-lookup"><span data-stu-id="1fa14-1012">No MPU protection</span></span><br /><span data-ttu-id="1fa14-1013">Protezione MPU (è necessario selezionare la modalità utente)</span><span class="sxs-lookup"><span data-stu-id="1fa14-1013">MPU protection (must have user mode selected)</span></span> |
| <span data-ttu-id="1fa14-1014">2</span><span class="sxs-lookup"><span data-stu-id="1fa14-1014">2</span></span> | <span data-ttu-id="1fa14-1015">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-1015">0</span></span><br /><span data-ttu-id="1fa14-1016">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-1016">1</span></span> | <span data-ttu-id="1fa14-1017">Disabilitare l'accesso alla memoria condivisa/esterna</span><span class="sxs-lookup"><span data-stu-id="1fa14-1017">Disable shared/external memory access</span></span><br /><span data-ttu-id="1fa14-1018">Abilitare l'accesso alla memoria condivisa/esterna</span><span class="sxs-lookup"><span data-stu-id="1fa14-1018">Enable shared/external memory access</span></span> |
| <span data-ttu-id="1fa14-1019">[23-3]</span><span class="sxs-lookup"><span data-stu-id="1fa14-1019">[23-3]</span></span> | <span data-ttu-id="1fa14-1020">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-1020">0</span></span> | <span data-ttu-id="1fa14-1021">Riservato</span><span class="sxs-lookup"><span data-stu-id="1fa14-1021">Reserved</span></span>
| <span data-ttu-id="1fa14-1022">[31-24]</span><span class="sxs-lookup"><span data-stu-id="1fa14-1022">[31-24]</span></span> | <br /><span data-ttu-id="1fa14-1023">0x00</span><span class="sxs-lookup"><span data-stu-id="1fa14-1023">0x00</span></span><br /><span data-ttu-id="1fa14-1024">0x02</span><span class="sxs-lookup"><span data-stu-id="1fa14-1024">0x02</span></span> | <span data-ttu-id="1fa14-1025">**ID compilatore**</span><span class="sxs-lookup"><span data-stu-id="1fa14-1025">**Compiler ID**</span></span><br /><span data-ttu-id="1fa14-1026">IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-1026">IAR</span></span><br /><span data-ttu-id="1fa14-1027">GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-1027">GNU</span></span> |

#### <a name="module-linker-for-rx63-using-iar"></a><span data-ttu-id="1fa14-1028">Modulo linker per RX63 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-1028">Module linker for RX63 using IAR</span></span>

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

#### <a name="building-modules-for-rx63-using-iar"></a><span data-ttu-id="1fa14-1029">Compilazione di moduli per RX63 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-1029">Building Modules for RX63 using IAR</span></span>

<span data-ttu-id="1fa14-1030">Viene fornita un'area di lavoro di esempio.</span><span class="sxs-lookup"><span data-stu-id="1fa14-1030">An example workspace is provided.</span></span> <span data-ttu-id="1fa14-1031">Compilare la libreria ThreadX, la libreria di moduli ThreadX, il progetto del modulo demo e il progetto di gestione moduli dimostrativi.</span><span class="sxs-lookup"><span data-stu-id="1fa14-1031">Build the ThreadX library, ThreadX Modules library, demo module project, and demo module manager project.</span></span>

#### <a name="thread-extension-definition-for-rxrx635n-using-iar"></a><span data-ttu-id="1fa14-1032">Definizione dell'estensione di thread per RXRX635N con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-1032">Thread extension definition for RXRX635N using IAR</span></span>

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

#### <a name="building-module-manager-for-rx63-using-iar"></a><span data-ttu-id="1fa14-1033">Compilazione di Module Manager per RX63 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-1033">Building Module Manager for RX63 using IAR</span></span>

<span data-ttu-id="1fa14-1034">Viene fornita un'area di lavoro di esempio.</span><span class="sxs-lookup"><span data-stu-id="1fa14-1034">An example workspace is provided.</span></span> <span data-ttu-id="1fa14-1035">Compilare la libreria ThreadX, la libreria di moduli ThreadX, il progetto del modulo demo e il progetto di gestione moduli dimostrativi.</span><span class="sxs-lookup"><span data-stu-id="1fa14-1035">Build the ThreadX library, ThreadX Modules library, demo module project, and demo module manager project.</span></span>

#### <a name="attributes-for-external-memory-enable-api-for-rx63-using-iar"></a><span data-ttu-id="1fa14-1036">Attributi per l'API External memory Enable per RX63 con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-1036">Attributes for external memory enable API for RX63 using IAR</span></span>

| <span data-ttu-id="1fa14-1037">Parametro attributo</span><span class="sxs-lookup"><span data-stu-id="1fa14-1037">Attribute Parameter</span></span> | <span data-ttu-id="1fa14-1038">Significato</span><span class="sxs-lookup"><span data-stu-id="1fa14-1038">Meaning</span></span> |
|---|---|
| <span data-ttu-id="1fa14-1039">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_EXECUTE</span><span class="sxs-lookup"><span data-stu-id="1fa14-1039">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_EXECUTE</span></span> | <span data-ttu-id="1fa14-1040">Esegui codice</span><span class="sxs-lookup"><span data-stu-id="1fa14-1040">Execute code</span></span> |
| <span data-ttu-id="1fa14-1041">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span><span class="sxs-lookup"><span data-stu-id="1fa14-1041">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span></span> | <span data-ttu-id="1fa14-1042">Accesso in scrittura</span><span class="sxs-lookup"><span data-stu-id="1fa14-1042">Write access</span></span> |
| <span data-ttu-id="1fa14-1043">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_READ</span><span class="sxs-lookup"><span data-stu-id="1fa14-1043">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_READ</span></span> | <span data-ttu-id="1fa14-1044">accesso in lettura</span><span class="sxs-lookup"><span data-stu-id="1fa14-1044">Read access</span></span> |

## <a name="rx65n-processor"></a><span data-ttu-id="1fa14-1045">Processore RX65N</span><span class="sxs-lookup"><span data-stu-id="1fa14-1045">RX65N processor</span></span>

### <a name="rx65n-using-iar"></a><span data-ttu-id="1fa14-1046">RX65N con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-1046">RX65N using IAR</span></span>

#### <a name="module-preamble-for-rx65n-using-iar"></a><span data-ttu-id="1fa14-1047">Preambolo del modulo per RX65N con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-1047">Module preamble for RX65N using IAR</span></span>

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

#### <a name="module-properties-for-rx65n-using-iar"></a><span data-ttu-id="1fa14-1048">Proprietà del modulo per RX65N con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-1048">Module properties for RX65N using IAR</span></span>

| <span data-ttu-id="1fa14-1049">bit</span><span class="sxs-lookup"><span data-stu-id="1fa14-1049">Bit</span></span> | <span data-ttu-id="1fa14-1050">Valore</span><span class="sxs-lookup"><span data-stu-id="1fa14-1050">Value</span></span> | <span data-ttu-id="1fa14-1051">Significato</span><span class="sxs-lookup"><span data-stu-id="1fa14-1051">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="1fa14-1052">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-1052">0</span></span> | <span data-ttu-id="1fa14-1053">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-1053">0</span></span><br /><span data-ttu-id="1fa14-1054">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-1054">1</span></span> | <span data-ttu-id="1fa14-1055">Esecuzione in modalità privilegiata</span><span class="sxs-lookup"><span data-stu-id="1fa14-1055">Privileged mode execution</span></span><br /><span data-ttu-id="1fa14-1056">Esecuzione in modalità utente</span><span class="sxs-lookup"><span data-stu-id="1fa14-1056">User mode execution</span></span> |
| <span data-ttu-id="1fa14-1057">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-1057">1</span></span> | <span data-ttu-id="1fa14-1058">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-1058">0</span></span><br /><span data-ttu-id="1fa14-1059">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-1059">1</span></span> | <span data-ttu-id="1fa14-1060">Nessuna protezione MPU</span><span class="sxs-lookup"><span data-stu-id="1fa14-1060">No MPU protection</span></span><br /><span data-ttu-id="1fa14-1061">Protezione MPU (è necessario selezionare la modalità utente)</span><span class="sxs-lookup"><span data-stu-id="1fa14-1061">MPU protection (must have user mode selected)</span></span> |
| <span data-ttu-id="1fa14-1062">2</span><span class="sxs-lookup"><span data-stu-id="1fa14-1062">2</span></span> | <span data-ttu-id="1fa14-1063">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-1063">0</span></span><br /><span data-ttu-id="1fa14-1064">1</span><span class="sxs-lookup"><span data-stu-id="1fa14-1064">1</span></span> | <span data-ttu-id="1fa14-1065">Disabilitare l'accesso alla memoria condivisa/esterna</span><span class="sxs-lookup"><span data-stu-id="1fa14-1065">Disable shared/external memory access</span></span><br /><span data-ttu-id="1fa14-1066">Abilitare l'accesso alla memoria condivisa/esterna</span><span class="sxs-lookup"><span data-stu-id="1fa14-1066">Enable shared/external memory access</span></span> |
| <span data-ttu-id="1fa14-1067">[23-3]</span><span class="sxs-lookup"><span data-stu-id="1fa14-1067">[23-3]</span></span> | <span data-ttu-id="1fa14-1068">0</span><span class="sxs-lookup"><span data-stu-id="1fa14-1068">0</span></span> | <span data-ttu-id="1fa14-1069">Riservato</span><span class="sxs-lookup"><span data-stu-id="1fa14-1069">Reserved</span></span>
| <span data-ttu-id="1fa14-1070">[31-24]</span><span class="sxs-lookup"><span data-stu-id="1fa14-1070">[31-24]</span></span> | <br /><span data-ttu-id="1fa14-1071">0x00</span><span class="sxs-lookup"><span data-stu-id="1fa14-1071">0x00</span></span><br /><span data-ttu-id="1fa14-1072">0x02</span><span class="sxs-lookup"><span data-stu-id="1fa14-1072">0x02</span></span> | <span data-ttu-id="1fa14-1073">**ID compilatore**</span><span class="sxs-lookup"><span data-stu-id="1fa14-1073">**Compiler ID**</span></span><br /><span data-ttu-id="1fa14-1074">IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-1074">IAR</span></span><br /><span data-ttu-id="1fa14-1075">GNU</span><span class="sxs-lookup"><span data-stu-id="1fa14-1075">GNU</span></span> |

#### <a name="module-linker-for-rx65n-using-iar"></a><span data-ttu-id="1fa14-1076">Modulo linker per RX65N con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-1076">Module linker for RX65N using IAR</span></span>

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

#### <a name="building-modules-for-rx65n-using-iar"></a><span data-ttu-id="1fa14-1077">Compilazione di moduli per RX65N con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-1077">Building Modules for RX65N using IAR</span></span>

<span data-ttu-id="1fa14-1078">Viene fornita un'area di lavoro di esempio.</span><span class="sxs-lookup"><span data-stu-id="1fa14-1078">An example workspace is provided.</span></span> <span data-ttu-id="1fa14-1079">Compilare la libreria ThreadX, la libreria di moduli ThreadX, il progetto del modulo demo e il progetto di gestione moduli dimostrativi.</span><span class="sxs-lookup"><span data-stu-id="1fa14-1079">Build the ThreadX library, ThreadX Modules library, demo module project, and demo module manager project.</span></span>

#### <a name="thread-extension-definition-for-rx65n-using-iar"></a><span data-ttu-id="1fa14-1080">Definizione dell'estensione di thread per RX65N con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-1080">Thread extension definition for RX65N using IAR</span></span>

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

#### <a name="building-module-manager-for-rx65n-using-iar"></a><span data-ttu-id="1fa14-1081">Compilazione di Module Manager per RX65N con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-1081">Building Module Manager for RX65N using IAR</span></span>

<span data-ttu-id="1fa14-1082">Viene fornita un'area di lavoro di esempio.</span><span class="sxs-lookup"><span data-stu-id="1fa14-1082">An example workspace is provided.</span></span> <span data-ttu-id="1fa14-1083">Compilare la libreria ThreadX, la libreria di moduli ThreadX, il progetto del modulo demo e il progetto di gestione moduli dimostrativi.</span><span class="sxs-lookup"><span data-stu-id="1fa14-1083">Build the ThreadX library, ThreadX Modules library, demo module project, and demo module manager project.</span></span>

#### <a name="attributes-for-external-memory-enable-api-for-rx65n-using-iar"></a><span data-ttu-id="1fa14-1084">Attributi per l'API External memory Enable per RX65N con IAR</span><span class="sxs-lookup"><span data-stu-id="1fa14-1084">Attributes for external memory enable API for RX65N using IAR</span></span>

| <span data-ttu-id="1fa14-1085">Parametro attributo</span><span class="sxs-lookup"><span data-stu-id="1fa14-1085">Attribute Parameter</span></span> | <span data-ttu-id="1fa14-1086">Significato</span><span class="sxs-lookup"><span data-stu-id="1fa14-1086">Meaning</span></span> |
|---|---|
| <span data-ttu-id="1fa14-1087">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_EXECUTE</span><span class="sxs-lookup"><span data-stu-id="1fa14-1087">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_EXECUTE</span></span> | <span data-ttu-id="1fa14-1088">Esegui codice</span><span class="sxs-lookup"><span data-stu-id="1fa14-1088">Execute code</span></span> |
| <span data-ttu-id="1fa14-1089">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span><span class="sxs-lookup"><span data-stu-id="1fa14-1089">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_WRITE</span></span> | <span data-ttu-id="1fa14-1090">Accesso in scrittura</span><span class="sxs-lookup"><span data-stu-id="1fa14-1090">Write access</span></span> |
| <span data-ttu-id="1fa14-1091">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_READ</span><span class="sxs-lookup"><span data-stu-id="1fa14-1091">TXM_MODULE_MANAGER_SHARED_ATTRIBUTE_READ</span></span> | <span data-ttu-id="1fa14-1092">accesso in lettura</span><span class="sxs-lookup"><span data-stu-id="1fa14-1092">Read access</span></span> |
