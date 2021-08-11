---
title: Appendice C - Utilità della riga di comando DOS
description: Sono disponibili tre utilità della riga di comando DOS nella sottodirectory Azure RTOS TraceX.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 1a89f8be7e21e416659b904f0ec5b2a3a8f666cdb9a861786e652a38564db48f
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116791551"
---
# <a name="appendix-c---dos-command-line-utilities"></a>Appendice C - Utilità della riga di comando DOS

Sono disponibili tre utilità della riga di comando DOS nell'installazione di TraceX nella ***sottodirectory Utilities.***

Le utilità fornite sono elencate di seguito:

| **Utilità**                              | **Scopo**                               | **Definizioni della riga di comando** |
| -------------------------------- | ----------------------------------------- | ---------------------------- |
| **ea2tracex.exe**                | Converte il file di traccia ea2tracex generato da ThreadX original_file associazione con gli strumenti GHS converted_file nel formato di file di traccia TraceX. Gli strumenti ThreadX per GHS producono un formato di traccia diverso da ThreadX per gli strumenti non GHS, motivo per cui è necessaria questa utilità di conversione. | ``` > eatracex original_file converted_file <cr> ``` | 
**hex2tracex.exe** | Converte un file di traccia generato da ThreadX ma scaricato dallo strumento di sviluppo in formato Intel HEX nel formato binario del file di traccia TraceX. TraceX V5 e successive possono aprire i file HEX senza convertirli. | ``` hex2tracex hex_file converted_file <cr> ``` | 
**mot2tracex.exe** | Converte un file di traccia generato da ThreadX ma di cui è stato scaricato il dump dallo strumento di sviluppo in formato Motorola S-Record nel formato binario del file di traccia TraceX. TraceX V5 e successive possono aprire i file S-Record senza convertirli. | ``` > mot2tracex mot_file converted_file <cr> ```|