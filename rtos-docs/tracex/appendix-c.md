---
title: Appendice C-DOS Utility della riga di comando
description: Sono disponibili tre utilità della riga di comando DOS nell'installazione di Azure RTO TraceX nella sottodirectory Utilities.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: e1ec852a97a6735a4a055706f55283950d3f8d6b
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823726"
---
# <a name="appendix-c---dos-command-line-utilities"></a>Appendice C-DOS Utility della riga di comando

Sono disponibili tre utilità della riga di comando DOS nell'installazione di TraceX nella sottodirectory ***Utilities*** .

Le utilità fornite sono elencate di seguito:

| **Utilità**                              | **Scopo**                               | **Definizioni della riga di comando** |
| -------------------------------- | ----------------------------------------- | ---------------------------- |
| **ea2tracex.exe**                | Converte il file di traccia ea2tracex generato da ThreadX nell'associazione original_file con gli strumenti GHS converted_file al formato del file di traccia TraceX. ThreadX per gli strumenti GHS produce un formato di traccia diverso da ThreadX per gli strumenti non GHS, motivo per cui questa utilità di conversione è necessaria. | ``` > eatracex original_file converted_file <cr> ``` | 
**hex2tracex.exe** | Converte un file di traccia generato da ThreadX, ma ne viene eseguito il dump dallo strumento di sviluppo in formato Intel HEX al formato del file di traccia TraceX binario. TraceX V5 e versioni successive possono aprire file ESADECIMALi senza convertirli. | ``` hex2tracex hex_file converted_file <cr> ``` | 
**mot2tracex.exe** | Converte un file di traccia generato da ThreadX, ma ne viene eseguito il dump dallo strumento di sviluppo nel formato di record Motorola S nel formato file di traccia TraceX binario. TraceX V5 e versioni successive possono aprire i file di record S senza convertirli. | ``` > mot2tracex mot_file converted_file <cr> ```|