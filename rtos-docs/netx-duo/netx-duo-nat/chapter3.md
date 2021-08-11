---
title: Capitolo 3 - Opzioni di configurazione NAT
description: L'elenco seguente include tutte le opzioni e la relativa funzione descritte in dettaglio
author: philmea
ms.author: philmea
ms.date: 07/14/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 8c7f2de88b5d70646284d946fdb6fbc743f08b3486430befb4fcda1d7e23e9b9
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116797281"
---
# <a name="chapter-3---nat-configuration-options"></a>Capitolo 3 - Opzioni di configurazione NAT

Le opzioni configurabili per l'API NAT di NetX Duo sono disponibili in *nx_nat.h,* ad eccezione del primo, **NX_DISABLE_ERROR_CHECKING** disponibile in *nx_nat.c*. L'elenco seguente include tutte le opzioni e la relativa funzione descritte in dettaglio:

- **NX_NAT_DISABLE_ERROR_CHECKING** Questa opzione, se definita, rimuove il controllo degli errori NAT di base. Viene in genere usato dopo il debug dell'applicazione. Lo stato NAT predefinito di NetX Duo è definito (abilitato).
- **NX_NAT_ENABLE_REPLACEMENT** Questa opzione, se definita, abilita la sostituzione automatica quando la cache NAT è piena.
  > [!NOTE]
  > Sostituire solo la sessione non TCP meno recente.
- **NX_NAT_MIN_ENTRY_COUNT** Questa opzione imposta il conteggio minimo per la voce di traduzione. Il conteggio predefinito è 3.
- **NX_NAT_TCP_SESSION_TIMEOUT** Questa opzione imposta il timeout per la voce di conversione per le sessioni TCP. Il timeout predefinito è 24 ore.
- **NX_NAT_NON_TCP_SESSION_TIMEOUT** Questa opzione imposta il timeout per la voce di conversione per le sessioni non TCP. Il timeout predefinito è 240 secondi.
- **NX_NAT_START_TCP_PORT** Questa opzione imposta il valore iniziale per trovare una porta TCP inutilizzata per assegnare un pacchetto TCP in uscita. The default value is 20000.
- **NX_NAT_END_TCP_PORT** Questa opzione imposta il limite superiore della porta TCP per assegnare un pacchetto TCP in uscita. Il valore predefinito è 30000.
- **NX_NAT_START_UDP_PORT** Questa opzione imposta il valore iniziale per trovare una porta UDP inutilizzata per assegnare un pacchetto UDP in uscita. The default value is 20000.
- **NX_NAT_END_UDP_PORT** Questa opzione imposta il limite superiore della porta UDP per assegnare un pacchetto UDP in uscita. Il valore predefinito è 30000.
- **NX_NAT_START_ICMP_QUERY_ID** Questa opzione imposta il valore iniziale per trovare un ID di query inutilizzato per assegnare un pacchetto di query ICMP in uscita. The default value is 20000.
- **NX_NAT_END_ICMP_QUERY_ID** Questa opzione imposta il limite superiore degli ID di query per assegnare un pacchetto di query ICMP in uscita. Il valore predefinito è 30000.
