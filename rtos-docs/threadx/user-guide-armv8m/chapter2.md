---
title: Capitolo 2-installazione del supporto ThreadX per ARMv8-M
description: Questo capitolo illustra come installare e usare il codice sorgente ThreadX per l'architettura ARMv8-M.
author: v-condav
ms.author: v-condav
ms.date: 03/04/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 303b83bcc92797314b764353b770965c0170fb99
ms.sourcegitcommit: d8edbb3207fe99f8afb431597dac063e73383e68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/05/2021
ms.locfileid: "106377592"
---
#  <a name="chapter-2--installing-threadx-support-for-armv8-m"></a>Capitolo 2 installazione del supporto ThreadX per ARMv8-M

Sono disponibili file di codice sorgente ThreadX aggiuntivi per supportare l'architettura ARMv8-M.

Se ThreadX deve essere eseguito in modalità protetta, questi file e API aggiuntivi non sono necessari. Per eseguire ThreadX in modalità protetta, definire il simbolo **TX_SECURE_EXECUTION** nella parte superiore di **_tx_port. h_*_ o nella riga di comando o nelle impostazioni del progetto. Assicurarsi che _* TX_SECURE_EXECUTION** sia definito per tutti i file c e assembly. ThreadX e l'applicazione utente vengono eseguiti in modalità protetta.

Per eseguire ThreadX e l'applicazione utente in modalità non protetta e supportare funzioni sicure richiamabili non sicure, effettuare le operazioni seguenti.

Il file ***tx_thread_secure_stack. c*** deve essere aggiunto all'applicazione protetta.

I file seguenti devono essere aggiunti alla libreria ThreadX.

- ***tx_secure_interface. h***
- ***txe_thread_secure_stack_allocate. c***
- ***txe_thread_secure_stack_free. c***
- ***tx_thread_secure_stack_allocate. s***
- ***tx_thread_secure_stack_free. s***

I due file seguenti sostituiscono i file generici nella libreria ThreadX.

- ***tx_thread_stack_error_handler. c***
- ***tx_thread_stack_error_notify. c***

## <a name="additional-threadx-sources-for-armv8-m"></a>Origini ThreadX aggiuntive per ARMv8-M

I file ThreadX aggiuntivi per l'architettura ARMv8-M TrustZone sono descritti di seguito.

  | **Nome file**                            | **Contents**                                                        |
  |------------------------------------------|---------------------------------------------------------------------|
  | ***tx_secure_interface. h***              | File di inclusione che definisce le funzioni chiamabili non sicure di ThreadX. |
  | ***txe_thread_secure_stack_allocate. c*** |  Errore durante il controllo del file per l'API di allocazione dello stack protetto. |
  | ***txe_thread_secure_stack_free. c***     |  Errore durante il controllo del file per l'API gratuita dello stack protetto. |
  | ***tx_thread_secure_stack_allocate. s***  |  Impiallacciatura non protetta per il servizio Secure stack allocate. |
  | ***tx_thread_secure_stack_free. s***      |  Impiallacciatura non sicura per il servizio Secure stack free. |
  | ***tx_thread_stack_error_handler. c***    |  Gestore per gli errori dello stack di thread. |
  | ***tx_thread_stack_error_notify. c***     |  Registra il callback di notifica per la gestione degli errori dello stack dei thread. |
