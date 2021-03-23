---
title: Capitolo 3-opzioni di configurazione NAT
description: Nell'elenco seguente sono incluse tutte le opzioni e le relative funzioni descritte in dettaglio
author: philmea
ms.author: philmea
ms.date: 07/14/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 9c10d6f0d2f36d2794ab1229081799f0032cada8
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821764"
---
# <a name="chapter-3---nat-configuration-options"></a>Capitolo 3-opzioni di configurazione NAT

Le opzioni configurabili per l'API NAT NetX Duo sono disponibili in *nx_nat. h* , ad eccezione del primo, **NX_DISABLE_ERROR_CHECKING** presente in *nx_nat. c*. Nell'elenco seguente sono incluse tutte le opzioni e le relative funzioni descritte in dettaglio:

- **NX_NAT_DISABLE_ERROR_CHECKING** Questa opzione se definito rimuove il controllo degli errori NAT di base. Viene in genere usato dopo il debug dell'applicazione. Lo stato NAT NetX Duo predefinito è definito (abilitato).
- **NX_NAT_ENABLE_REPLACEMENT** Questa opzione, se definita, consente la sostituzione automatica quando la cache NAT è piena.
  > [!NOTE]
  > Sostituire solo la sessione non TCP meno recente.
- **NX_NAT_MIN_ENTRY_COUNT** Questa opzione consente di impostare il numero minimo per la voce di traduzione. Il numero predefinito è 3.
- **NX_NAT_TCP_SESSION_TIMEOUT** Questa opzione imposta il timeout per la voce di traduzione per le sessioni TCP. Il timeout predefinito è 24 ore.
- **NX_NAT_NON_TCP_SESSION_TIMEOUT** Questa opzione imposta il timeout per la voce di traduzione per le sessioni non TCP. Il timeout predefinito è di 240 secondi.
- **NX_NAT_START_TCP_PORT** Questa opzione imposta il valore iniziale per la ricerca di una porta TCP non utilizzata per l'assegnazione di un pacchetto TCP in uscita. The default value is 20000.
- **NX_NAT_END_TCP_PORT** Questa opzione imposta il UpperLimit della porta TCP per l'assegnazione di un pacchetto TCP in uscita. Il valore predefinito è 30000.
- **NX_NAT_START_UDP_PORT** Questa opzione imposta il valore iniziale per la ricerca di una porta UDP non utilizzata per l'assegnazione di un pacchetto UDP in uscita. The default value is 20000.
- **NX_NAT_END_UDP_PORT** Questa opzione imposta il UpperLimit della porta UDP per assegnare un pacchetto UDP in uscita. Il valore predefinito è 30000.
- **NX_NAT_START_ICMP_QUERY_ID** Questa opzione imposta il valore iniziale per la ricerca di un ID di query non usato per assegnare un pacchetto di query ICMP in uscita. The default value is 20000.
- **NX_NAT_END_ICMP_QUERY_ID** Questa opzione imposta il UpperLimit di ID query per assegnare un pacchetto di query ICMP in uscita. Il valore predefinito è 30000.
