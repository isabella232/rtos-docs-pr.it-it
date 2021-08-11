---
title: Capitolo 3 - Componenti funzionali dello stack host USBX
description: Questo capitolo contiene una descrizione dello stack host USB incorporato USBX ad alte prestazioni dal punto di vista funzionale.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: a3cbbb2e26d66d3db26144a47a1b6cbb11387c7b5b2ba5e19d35df026e5e3598
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116790889"
---
# <a name="chapter-3---functional-components-of-usbx-host-stack"></a>Capitolo 3 - Componenti funzionali dello stack host USBX

Questo capitolo contiene una descrizione dello stack host USB incorporato USBX ad alte prestazioni dal punto di vista funzionale.

## <a name="execution-overview"></a>Panoramica dell'esecuzione

USBX è costituito da diversi componenti:

- Inizializzazione
- Chiamate all'interfaccia dell'applicazione
- Hub radice
- Classe Hub
- Classi host
- USB Host Stack
- Controller host

Il diagramma seguente illustra lo stack host USBX.

![USBX Host Stack](./media/usbx-host-stack/usbx-host-stack.png)

### <a name="initialization"></a>Inizializzazione

Per attivare USBX, è necessario chiamare la funzione ***ux_system_initialize*** chiamata. Questa funzione inizializza le risorse di memoria di USBX.

Per attivare le funzionalità host USBX, è necessario ***chiamare*** ux_host_stack_initialize funzione. Questa funzione a sua volta inizializza tutte le risorse usate dallo stack host USBX, ad esempio thread ThreadX, mutex e semafori.

L'inizializzazione dell'applicazione deve attivare almeno un controller host USB e una o più classi USB. Quando le classi sono state registrate nello stack e la funzione di inizializzazione dei controller host è stata chiamata il bus è attivo e l'individuazione dei dispositivi può essere avviata. Se l'hub radice del controller host rileva un dispositivo collegato, il thread di enumerazione USB responsabile della topologia USB verrà riattivato e procederà all'enumerazione dei dispositivi.

È possibile, a causa della natura dell'hub radice e degli hub downstream, che tutti i dispositivi USB collegati non siano stati configurati completamente al termine della funzione di inizializzazione del controller host. L'enumerazione di tutti i dispositivi USB può richiedere alcuni secondi, soprattutto se sono presenti uno o più hub tra l'hub radice e i dispositivi USB.

### <a name="application-interface-calls"></a>Chiamate all'interfaccia dell'applicazione

Esistono due livelli di API in USBX.

- API dello stack di host USB
- API della classe host USB

In genere, un'applicazione USBX non deve chiamare alcuna funzione api dello stack di host USB. La maggior parte delle applicazioni accederà solo alle funzioni dell'API classe USB.

### <a name="usb-host-stack-apis"></a>API dello stack di host USB

Le funzioni API dello stack host sono responsabili della registrazione dei componenti USBX (classi host e controller host), della configurazione dei dispositivi e delle richieste di trasferimento per gli endpoint dispositivo disponibili.

### <a name="usb-host-class-api"></a>API della classe host USB

Le API di classe sono molto specifiche per ogni classe USB. La maggior parte delle funzioni API comuni per le classi USB fornisce servizi come l'apertura/chiusura di un dispositivo e la lettura e la scrittura in un dispositivo.

### <a name="root-hub"></a>Hub radice

Ogni istanza del controller host ha uno o più hub radice USB. Il numero di hub radice è determinato dalla natura del controller o può essere recuperato leggendo registri specifici dal controller.

### <a name="hub-class"></a>Classe Hub

La classe hub è responsabile della guida degli hub USB. Un hub USB può essere un hub autonomo o come parte di un dispositivo composto, ad esempio una tastiera o un monitor. Un hub può essere autoalimentato o basato su bus. Gli hub basati su bus hanno un massimo di quattro porte downstream e possono consentire solo la connessione di dispositivi con alimentazione autonoma o con bus che usano meno di 100 mA di potenza. Gli hub possono essere propagati a catena. È possibile collegare fino a cinque hub.

### <a name="usb-host-stack"></a>USB Host Stack

Lo stack host USB è il fulcro di USBX. Ha tre funzioni principali.

- Gestire la topologia dell'USB.
- Associare un dispositivo USB a una o più classi.
- Fornire un'API alle classi per eseguire l'interrogatorio del descrittore del dispositivo e i trasferimenti USB.

### <a name="topology-manager"></a>Gestione topologia

Il thread della topologia dello stack USB viene generato quando un nuovo dispositivo è connesso o quando un dispositivo è stato disconnesso. L'hub radice o un hub normale può accettare le connessioni del dispositivo. Dopo che un dispositivo è stato connesso all'USB, il gestore della topologia recupererà il descrittore del dispositivo. Questo descrittore conterrà il numero di possibili configurazioni disponibili per questo dispositivo. La maggior parte dei dispositivi ha una sola configurazione. Alcuni dispositivi possono funzionare in modo diverso in base all'alimentazione disponibile sulla porta in cui è connesso. In questo caso, il dispositivo avrà più configurazioni che possono essere selezionate a seconda della potenza disponibile. Quando il dispositivo viene configurato dal gestore della topologia, è quindi consentito disegnare la quantità di alimentazione specificata nel descrittore di configurazione.

## <a name="usb-class-binding"></a>Associazione di classi USB

Quando il dispositivo è configurato, gestione topologia consente al gestore di classi di continuare l'individuazione del dispositivo esaminando i descrittori dell'interfaccia del dispositivo. Un dispositivo può avere uno o più descrittori di interfaccia.

Un'interfaccia rappresenta una funzione in un dispositivo. Ad esempio, un altoparlante USB ha tre interfacce, una per lo streaming audio, una per il controllo audio e una per gestire i vari pulsanti del parlante.

Il gestore di classi ha due meccanismi per unire le interfacce del dispositivo a una o più classi. Può usare la combinazione di PID/VID (ID prodotto e ID fornitore) presenti nel descrittore di interfaccia o la combinazione di Classe/Sottoclasse/Protocollo.

La combinazione PID/VID è valida per le interfacce che non possono essere guidate da una classe generica. La combinazione Classe/Sottoclasse/Protocollo viene usata dalle interfacce che appartengono a una classe certificata USB-IF, ad esempio una stampante, un hub, un archivio, audio o HID.

Il gestore di classi contiene un elenco di classi registrate dall'inizializzazione di USBX. Il gestore di classi chiamerà ogni classe una alla volta finché una classe non accetta di gestire l'interfaccia per il dispositivo. Una classe può gestire una sola interfaccia. Per l'esempio dell'altoparlante audio USB, il gestore di classi chiamerà tutte le classi per ognuna delle interfacce.

Quando una classe accetta un'interfaccia, viene creata una nuova istanza di tale classe. Il gestore di classi cerca quindi l'impostazione alternativa predefinita per l'interfaccia. Un dispositivo può avere una o più impostazioni alternative per ogni interfaccia. L'impostazione alternativa 0 sarà l'oggetto utilizzato per impostazione predefinita fino a quando una classe non decide di modificarla.

Per l'impostazione alternativa predefinita, il gestore di classi monta tutti gli endpoint contenuti nell'impostazione alternativa. Se il montaggio di ogni endpoint ha esito positivo, il gestore di classi completerà il processo tornando alla classe che completerà l'inizializzazione dell'interfaccia.

### <a name="usbx-apis"></a>API USBX

Lo stack USB esporta un certo numero di API per le classi USB per eseguire l'interrogatorio sul dispositivo e i trasferimenti USB su endpoint specifici. Queste funzioni API sono descritte in dettaglio in questo manuale di riferimento.

### <a name="host-controller"></a>Host Controller

Il driver del controller host è responsabile della guida di un tipo specifico di controller USB. Un controller host USB può avere più controller all'interno. Ad esempio, alcuni chipset Intel PC contengono due controller UHCI. Alcuni controller USB 2.0 contengono più istanze di un controller OHCI oltre a un'istanza del controller EHCI.

Il controller host gestirà solo più istanze dello stesso controller. Per guidare la maggior parte dei controller host USB 2.0, sarà necessario inizializzare sia il controller OCHI che il controller EHCI durante l'inizializzazione di USBX.

Il controller host è responsabile della gestione di quanto segue.

- Hub radice
- Risparmio energia
- Endpoint
- Trasferimenti

### <a name="root-hub"></a>Hub radice

La gestione dell'hub radice è responsabile dell'accensione di ogni porta del controller e di determinare se è stato inserito o meno un dispositivo. Questa funzionalità viene usata dall'hub radice generico USBX per interrogare le porte downstream del controller.

### <a name="power-management"></a>Risparmio energia

L'elaborazione del risparmio energia consente di gestire i segnali di sospensione/ripresa in modalità banda, interessando quindi tutte le porte downstream del controller contemporaneamente o singolarmente se il controller offre questa funzionalità.

### <a name="endpoints"></a>Endpoint

La gestione degli endpoint consente la creazione o la distruzione di endpoint fisici al controller. Gli endpoint fisici sono entità di memoria analizzate dal controller se il controller supporta DMA master o scritte nel controller. Gli endpoint fisici contengono informazioni sulle transazioni che devono essere eseguite dal controller.

### <a name="transfers"></a>Trasferimenti

La gestione dei trasferimenti consente a una classe di eseguire una transazione in ognuno degli endpoint creati. Ogni endpoint logico contiene un componente denominato TRANSFER REQUEST per le richieste di trasferimento USB. TRANSFER REQUEST viene usato dallo stack per descrivere la transazione. Questa RICHIESTA DI TRASFERIMENTO viene quindi passata al controller e nello stack, che può essere suddivisa in diverse transazioni secondarie a seconda delle funzionalità del controller.

## <a name="usb-device-framework"></a>Framework di dispositivi USB

Un dispositivo USB è rappresentato da un albero di descrittori. Esistono sei tipi principali di descrittori.

- Descrittori del dispositivo
- Descrittori di configurazione
- Descrittori di interfaccia
- Descrittori di endpoint
- Descrittori di stringa
- Descrittori funzionali

Un dispositivo USB può avere una descrizione molto semplice e ha un aspetto simile al seguente.
![Dispositivo USB semplice](./media/usbx-host-stack/usb-device-simple.png)

Nella figura precedente il dispositivo ha una sola configurazione. A questa configurazione è collegata una singola interfaccia, che indica che il dispositivo ha una sola funzione e ha un solo endpoint. Collegato al descrittore del dispositivo è un descrittore di stringa che fornisce un'identificazione visibile del dispositivo.

Tuttavia, un dispositivo può essere più complesso e può apparire come segue.

![Dispositivo USB complesso](./media/usbx-host-stack/usb-device-complex.png)

Nella figura precedente il dispositivo ha due descrittori di configurazione collegati al descrittore del dispositivo. Questo dispositivo può indicare che ha due modalità di alimentazione o può essere guidato da classi standard o classi proprietarie.

Alla prima configurazione sono associate due interfacce che indicano che il dispositivo ha due funzioni logiche. La prima funzione ha 3 descrittori di endpoint e un descrittore funzionale. Il descrittore funzionale può essere usato dalla classe responsabile di guidare l'interfaccia per ottenere altre informazioni su questa interfaccia normalmente non trovate da un descrittore generico.

### <a name="device-descriptors"></a>Descrittori di dispositivo

Ogni dispositivo USB ha un singolo descrittore di dispositivo. Questo descrittore contiene l'identificazione del dispositivo, il numero di configurazioni supportate e le caratteristiche dell'endpoint di controllo predefinito usato per la configurazione del dispositivo.

| Offset | Campo              | Dimensione | Valore    | Descrizione                             |
| ------ | ------------------ | ---- | -------- | --------------------------------------- |
| 0      | BLength            | 1    | Numero   | Dimensioni del descrittore in byte |
| 1      | bDescriptorType    | 1    | Costante | Tipo di descrittore DEVICE |
| 2      | bcdUSB             | 2    | Bcd      | Numero di versione della specifica USB in BinaryCoded Dec<br />Esempio: 2.10 equivale a 0x210. Questo campo identifica il rilascio della specifica USB con cui il dispositivo e i relativi descrittori sono conformi. |
| 4      | bDeviceClass       | 1    | Classe    | Codice di classe (assegnato da USB-IF).<br />Se questo campo viene reimpostato su 0, ogni interfaccia all'interno di una configurazione specifica le proprie informazioni sulla classe e le varie interfacce operano in modo indipendente.<br />Se questo campo è impostato su un valore compreso tra 1 e 0xFE, il dispositivo supporta specifiche di classe diverse su interfacce diverse e le interfacce potrebbero non funzionare in modo indipendente. Questo valore identifica la definizione di classe usata per le interfacce di aggregazione.<br />Se questo campo è impostato su 0xFF, la classe del dispositivo è specifica del fornitore. |
| 5      | bDeviceSubClass    | 1    | Sottoclasse | Codice di sottoclasse (assegnato da USB-IF).<br />Questi codici sono qualificati dal valore del campo bDeviceClass. Se il campo bDeviceClass viene reimpostato su 0, anche questo campo deve essere reimpostato su 0. Se il campo bDeviceClass non è impostato su 0xFF, tutti i valori sono riservati per l'assegnazione tramite USB. |
| 6      | bDeviceProtocol    | 1    | Protocollo | Codice del protocollo (assegnato da USB-IF).<br />Questi codici sono qualificati dal valore dei campi bDeviceClass e bDeviceSubClass. Se un dispositivo supporta protocolli specifici della classe in base al dispositivo anziché a una base di interfaccia, questo codice identifica i protocolli che il dispositivo usa come definito dalla specifica della classe del dispositivo. Se questo campo viene reimpostato su 0, il dispositivo non usa protocolli specifici della classe in base al dispositivo.<br />Tuttavia, può usare protocolli specifici della classe su base di interfaccia.<br />Se questo campo è impostato su 0xFF, il dispositivo usa un protocollo specifico del fornitore in base al dispositivo. |
| 7      | bMaxPacketSize0    | 1    | Numero   | Dimensioni massime del pacchetto per l'endpoint zero (sono valide solo dimensioni in byte pari a 8, 16, 32 o 64) |
| 8      | idVendor           | 2    | ID       | ID fornitore (assegnato da USB-IF) |
| 10     | idProduct          | 2    | ID       | ID prodotto (assegnato dal produttore) |
| 12     | bcdDevice          | 2    | Bcd      | Numero di versione del dispositivo in formato decimale codificato binario |
| 14     | iManufacturer      | 1    | Indice    | Indice del descrittore di stringa che descrive il produttore |
| 15     | iProduct           | 1    | Indice    | Indice del descrittore di stringa che descrive il prodotto |
| 16     | iSerialNumbe       | 1    | Indice    | Indice del descrittore di stringa che descrive il numero di serie del dispositivo |
| 17     | bNumConfigurations | 1    | Numero   | Numero di configurazioni possibili |

USBX definisce un descrittore di dispositivo USB come segue:

```c
typedef struct UX_DEVICE_DESCRIPTOR_STRUCT
{
    UINT      bLength;
    UINT      bDescriptorType;
    USHORT    bcdUSB;
    UINT      bDeviceClass;
    UINT      bDeviceSubClass;
    UINT      bDeviceProtocol;
    UINT      bMaxPacketSize0;
    USHORT    idVendor;
    USHORT    idProduct;
    USHORT    bcdDevice;
    UINT      iManufacturer;
    UINT      iProduct;
    UINT      iSerialNumber;
    UINT      bNumConfigurations;
} UX_DEVICE_DESCRIPTOR;
```

Il descrittore del dispositivo USB fa parte di un contenitore di dispositivi descritto come:

```c
typedef struct UX_DEVICE_STRUCT
{
    ULONG ux_device_handle;
    ULONG ux_device_type;
    ULONG ux_device_state;
    ULONG ux_device_address;
    ULONG ux_device_speed;
    ULONG ux_device_port_location;
    ULONG ux_device_max_power;
    ULONG ux_device_power_source;
    UINT ux_device_current_configuration;

    TX_SEMAPHORE ux_device_protection_semaphore;
    struct UX_DEVICE_STRUCT *ux_device_parent; 
    struct UX_HOST_CLASS_STRUCT *ux_device_class; 
    VOID *ux_device_class_instance;
    struct UX_HCD_STRUCT *ux_device_hcd;
    struct UX_CONFIGURATION_STRUCT *ux_device_first_configuration; 
    struct UX_DEVICE_STRUCT *ux_device_next_device;
    struct UX_DEVICE_DESCRIPTOR_STRUCT ux_device_descriptor;
    struct UX_ENDPOINT_STRUCT ux_device_control_endpoint;
    struct UX_HUB_TT_STRUCT ux_device_hub_tt[UX_MAX_TT];
} UX_DEVICE;
```

- **ux_device_handle:** handle del dispositivo. Si tratta in genere dell'indirizzo dell'istanza di questa struttura per il dispositivo.
- **ux_device_type:** valore obsoleto. Non utilizzato.
- **ux_device_state:** Stato del dispositivo, che può avere uno dei valori seguenti:
    - **UX_DEVICE_RESET**                0
    - **UX_DEVICE_ATTACHED**             1
    - **UX_DEVICE_ADDRESSED**            2
    - **UX_DEVICE_CONFIGURED**           3
    - **UX_DEVICE_SUSPENDED**            4
    - **UX_DEVICE_RESUMED**              5
    - **UX_DEVICE_SELF_POWERED_STATE**   6
    - **UX_DEVICE_SELF_POWERED_STATE**   7
    - **UX_DEVICE_REMOTE_WAKEUP**        8
    - **UX_DEVICE_BUS_RESET_COMPLETED**  9
    - **UX_DEVICE_REMOVED**              10
    - **UX_DEVICE_FORCE_DISCONNECT**     11
- **ux_device_address**: indirizzo del dispositivo dopo **l'accettazione SET_ADDRESS** comando di configurazione (da 1 a 127).
- **ux_device_speed**: Velocità del dispositivo:
    - **UX_LOW_SPEED_DEVICE**      0
    - **UX_FULL_SPEED_DEVICE**     1
    - **UX_HIGH_SPEED_DEVICE**     2
- **ux_device_port_location:** indice della porta del dispositivo padre (hub radice o hub).
- **ux_device_max_power:** potenza massima in mA che il dispositivo può assumere nella configurazione selezionata.
- **ux_device_power_source**: può essere uno dei due valori seguenti:
    - **UX_DEVICE_BUS_POWERED**     1
    - **UX_DEVICE_SELF_POWERED**    2
- **ux_device_current_configuration**: indice della configurazione corrente usata dal dispositivo.
- **ux_device_parent:** puntatore del contenitore del dispositivo dell'elemento padre del dispositivo. Se il puntatore è Null, l'elemento padre è l'hub radice del controller.
- **ux_device_class**: puntatore al tipo di classe proprietario del dispositivo.
- **ux_device_class_instance**: puntatore all'istanza della classe proprietaria del dispositivo.
- **ux_device_hcd:** Istanza del controller host USB in cui è collegato il dispositivo.
- **ux_device_first_configuration:** puntatore al primo contenitore di configurazione per questo dispositivo.
- **ux_device_next_device:** puntatore al dispositivo successivo nell'elenco dei dispositivi rilevati da USBX.
- **ux_device_descriptor:** descrittore del dispositivo USB.
- **ux_device_control_endpoint**: descrittore dell'endpoint di controllo predefinito usato da questo dispositivo.
- **ux_device_hub_tt:** Matrice di TT hub per il dispositivo

### <a name="configuration-descriptors"></a>Descrittori di configurazione

Il descrittore di configurazione descrive le informazioni su una configurazione specifica del dispositivo. Un dispositivo USB può contenere uno o più descrittori di configurazione. Il **campo bNumConfigurations** nel descrittore di dispositivo indica il numero di descrittori di configurazione. Il descrittore contiene un campo **bConfigurationValue** con un valore che, se usato come parametro per la richiesta Set Configuration, fa sì che il dispositivo presupponga la configurazione descritta.

Il descrittore descrive il numero di interfacce fornite dalla configurazione. Ogni interfaccia rappresenta una funzione logica all'interno del dispositivo e può funzionare in modo indipendente. Ad esempio, un altoparlante audio USB può avere tre interfacce, una per lo streaming audio, una per il controllo audio e un'interfaccia HID per gestire i pulsanti dell'altoparlante.

Quando l'host esegue una GET_DESCRIPTOR richiesta per il descrittore di configurazione, vengono restituiti tutti i descrittori di interfaccia e endpoint correlati.

| Offset | Campo               | Dimensione | Valore    | Descrizione                       |
| ------ | ------------------- | ---- | -------- | --------------------------------- |
| 0      | bLength             | 1    | Numero   | Dimensione del descrittore in byte. |
| 1      | bDescriptorType     | 1    | Costante | CONFIGURATION                     |
| 2      | wTotalLength        | 2    | Numero   | Lunghezza totale dei dati restituiti per questa configurazione. Include la lunghezza combinata di tutti i descrittori (configurazione, interfaccia, endpoint e classe o fornitore specifici) restituiti per questa configurazione. |
| 4      | bNumInterfaces      | 1    | Numero   | Numero di interfacce supportate da questa configurazione. |
| 5      | bConfigurationValue | 1    | Numero   | Valore da utilizzare come argomento di Set<br/>Configurazione per selezionare questa configurazione. |
| 6      | iConfiguration      | 1    | Indice    | Indice del descrittore di stringa che descrive questa configurazione. |
| 7      | bMAttributes        | 1    | Bitmap   | Caratteristiche di configurazione basate su bus D7<br />D6 self-powered<br />Riattivazione remota D5<br />D4. 0 Riservato (reimpostato su 0)<br />Una configurazione del dispositivo che usa l'alimentazione dal bus e un'origine locale imposta sia D7 che D6. L'origine di alimentazione effettiva in fase di esecuzione può essere determinata usando la richiesta del dispositivo Ottieni stato.<br />Se una configurazione del dispositivo supporta la riattivazione remota, D5 è impostato su 1. |
| 8      | MaxPower            | 1    | mA       | Consumo massimo di energia del dispositivo USB dal bus in questa configurazione specifica quando il dispositivo è completamente operativo.<br />Espresso in 2 unità mA (ad esempio, 50 = 100 mA).<br />Nota: la configurazione di un dispositivo indica se la configurazione è basata su bus o autonoma.<br />Lo stato del dispositivo indica se il dispositivo è attualmente alimentato autonomamente. Se un dispositivo è disconnesso dalla relativa fonte di alimentazione esterna, aggiorna lo stato del dispositivo per indicare che non è più alimentato autonomamente. |

USBX definisce un descrittore di configurazione USB come indicato di seguito.

```c
typedef struct UX_CONFIGURATION_DESCRIPTOR_STRUCT
{
    UINT bLength;
    UINT bDescriptorType;
    USHORT wTotalLength;
    UINT bNumInterfaces;
    UINT bConfigurationValue;
    UINT iConfiguration;
    UINT bmAttributes;
    UINT MaxPower;
} UX_CONFIGURATION_DESCRIPTOR;
```

Il descrittore di configurazione USB fa parte di un contenitore di configurazione descritto di seguito.

```c
typedef struct UX_CONFIGURATION_STRUCT
{
    ULONG ux_configuration_handle;
    ULONG ux_configuration_state;
    struct UX_CONFIGURATION_DESCRIPTOR_STRUCT ux_configuration_descriptor;
    struct UX_INTERFACE_STRUCT *ux_configuration_first_interface;
    struct UX_CONFIGURATION_STRUCT *ux_configuration_next_configuration;
    struct UX_DEVICE_STRUCT *ux_configuration_device;
} UX_CONFIGURATION;
```

- **ux_configuration_handle**: gestire la configurazione. Questo è in genere l'indirizzo dell'istanza di questa struttura per la configurazione.
- **ux_configuration_state**: stato della configurazione.
- **ux_configuration_descriptor**: descrittore del dispositivo USB.
- **ux_configuration_first_interface:** puntatore alla prima interfaccia per questa configurazione.
- **ux_configuration_next_configuration:** puntatore alla configurazione successiva per lo stesso dispositivo.
- **ux_configuration_device:** puntatore al proprietario del dispositivo di questa configurazione.

### <a name="interface-descriptors"></a>Descrittori di interfaccia

Il descrittore di interfaccia descrive un'interfaccia specifica all'interno di una configurazione. Un'interfaccia è una funzione logica all'interno di un dispositivo USB. Una configurazione fornisce una o più interfacce, ognuna con zero o più descrittori di endpoint che descrivono un set univoco di endpoint all'interno della configurazione. Quando una configurazione supporta più interfacce, i descrittori di endpoint per una particolare interfaccia  seguono il descrittore di interfaccia nei dati restituiti dalla richiesta GET_DESCRIPTOR per la configurazione specificata.

Un descrittore di interfaccia viene sempre restituito come parte di un descrittore di configurazione. Un descrittore di interfaccia non può accedere direttamente da una GET_DESCRIPTOR richiesta.

Un'interfaccia può includere impostazioni alternative che consentono di variare gli endpoint e/o le relative caratteristiche dopo la configurazione del dispositivo. L'impostazione predefinita per un'interfaccia è sempre l'impostazione alternativa zero. Una classe può scegliere di modificare l'impostazione alternativa corrente per modificare il comportamento dell'interfaccia e le caratteristiche degli endpoint associati. La SET_INTERFACE richiesta viene usata per selezionare un'impostazione alternativa o per tornare all'impostazione predefinita.

Le impostazioni alternative consentono di variare una parte della configurazione del dispositivo mentre altre interfacce rimangono in funzione. Se per una configurazione sono disponibili impostazioni alternative per una o più interfacce, per ogni impostazione vengono inclusi un descrittore di interfaccia separato e gli endpoint associati.

Se una configurazione del dispositivo contiene una singola interfaccia con due impostazioni alternative, la richiesta GET_DESCRIPTOR per la configurazione restituirà il descrittore di configurazione, il descrittore di interfaccia con i campi **bInterfaceNumber** e **bAlternateSetting** impostati su zero e quindi i descrittori dell'endpoint per tale impostazione, seguiti da un altro descrittore di interfaccia e dai descrittori di endpoint associati. Anche il campo **bInterfaceNumber** del secondo descrittore di interfaccia verrebbe impostato su zero, ma il campo **bAlternateSetting** del secondo descrittore di interfaccia verrebbe impostato su 1 a indicare che questa impostazione alternativa appartiene alla prima interfaccia.

A un'interfaccia non possono essere associati endpoint, nel qual caso solo l'endpoint di controllo predefinito è valido per tale interfaccia.

Le impostazioni alternative vengono usate principalmente per modificare la larghezza di banda richiesta per gli endpoint periodici associati all'interfaccia. Ad esempio, un'interfaccia di streaming di altoparlanti USB deve avere la prima impostazione alternativa con una richiesta di larghezza di banda 0 sull'endpoint isocrono. Altre impostazioni alternative possono selezionare requisiti di larghezza di banda diversi a seconda della frequenza di streaming audio.

Il descrittore USB per l'interfaccia è il seguente:

| Offset | Campo              | Dimensione | Valore     | Descrittore                              |
| ------ | ------------------ | ---- | --------- | --------------------------------------- |
| 0      | bLength            | 1    | Numero    | Dimensioni del descrittore in byte.       |
| 1      | bDescriptorType    | 1    | Costante  | Tipo di descrittore INTERFACE               |
| 2      | bInterfaceNumber   | 1    | Numero    | Numero di interfacce. Valore in base zero che identifica l'indice nella matrice di interfacce simultanee supportate da questa configurazione. |
| 3      | bAltenateSetting   | 1    | Numero    | Valore utilizzato per selezionare un'impostazione alternativa per l'interfaccia identificata nel campo precedente. |
| 4      | bNumEndpoints      | 1    | Numero    | Numero di endpoint usati da questa interfaccia (escluso l'endpoint zero). Se questo valore è 0, questa interfaccia usa solo l'endpoint zero. |
| 5      | bInterfaceClass    | 1    | Classe     | Codice di classe (assegnato da USB)<br />Se questo campo viene reimpostato su 0, l'interfaccia non appartiene ad alcuna classe di dispositivo specificata da USB.<br />Se questo campo è impostato su 0xFF, la classe di interfaccia è specifica del fornitore.<br />Tutti gli altri valori sono riservati per l'assegnazione tramite USB. |
| 6      | bInterfaceSubClass | 1    | Sottoclasse  | Codice sottoclasse (assegnato da USB).<br />Questi codici sono qualificati dal valore del campo bInterfaceClass. Se il campo bInterfaceClass viene reimpostato su 0, anche questo campo deve essere reimpostato su 0. Se il campo bInterfaceClass non è impostato su 0xFF, tutti i valori sono riservati per l'assegnazione tramite USB. |
| 7      | bInterfaceProtocol | 1    | Protocollo  | Codice del protocollo (assegnato da USB). Questi codici sono qualificati dal valore dei campi bInterfaceClass e bInterfaceSubClass. Se un'interfaccia supporta richieste specifiche della classe, questo codice identifica i protocolli utilizzati dal dispositivo come definito dalla specifica della classe di dispositivo.<br />Se questo campo viene reimpostato su 0, il dispositivo non usa un protocollo specifico della classe su questa interfaccia. Se questo campo è impostato su 0xFF, il dispositivo usa un protocollo specifico del fornitore per questa interfaccia. |
| 8      | Interfaccia iInterface         | 1    | Indice     | Indice del descrittore di stringa che descrive questa interfaccia. |

USBX definisce un descrittore di interfaccia USB come indicato di seguito.

```c
typedef struct UX_INTERFACE_DESCRIPTOR_STRUCT
{
    UINT bLength;
    UINT bDescriptorType;
    UINT bInterfaceNumber;
    UINT bAlternateSetting;
    UINT bNumEndpoints;
    UINT bInterfaceClass
    UINT bInterfaceSubClass;
    UINT bInterfaceProtocol;
    UINT iInterface;
} UX_INTERFACE_DESCRIPTOR;
```

Il descrittore di interfaccia USB fa parte di un contenitore di interfacce descritto di seguito.

```c
typedef struct UX_INTERFACE_STRUCT
{
    ULONG ux_interface_handle;
    ULONG ux_interface_state;
    ULONG ux_interface_current_alternate_setting;
    struct UX_INTERFACE_DESCRIPTOR_STRUCT ux_interface_descriptor;
    struct UX_HOST_CLASS_STRUCT    *ux_interface_class;
    VOID    *ux_interface_class_instance;
    struct UX_ENDPOINT_STRUCT    *ux_interface_first_endpoint;
    struct UX_INTERFACE_STRUCT    *ux_interface_next_interface;
    struct UX_CONFIGURATION_STRUCT    *ux_interface_configuration;
} UX_INTERFACE;
```

- **ux_interface_handle**: handle dell'interfaccia. Si tratta in genere dell'indirizzo dell'istanza di questa struttura per l'interfaccia .
- **ux_interface_state:** stato dell'interfaccia.
- **ux_interface_descriptor:** descrittore di interfaccia USB.
- **ux_interface_class**: puntatore al tipo di classe proprietario di questa interfaccia.
- **ux_interface_class_instance**: puntatore all'istanza della classe proprietaria di questa interfaccia.
- **ux_interface_first_endpoint**: puntatore al primo endpoint registrato con questa interfaccia.
- **ux_interface_next_interface**: puntatore all'interfaccia successiva associata alla configurazione.
- **ux_interface_configuration**: puntatore al proprietario della configurazione di questa interfaccia.

### <a name="endpoint-descriptors"></a>Descrittori di endpoint

Ogni endpoint associato a un'interfaccia ha un proprio descrittore di endpoint. Questo descrittore contiene le informazioni richieste dallo stack host per determinare i requisiti di larghezza di banda di ogni endpoint, il payload massimo associato all'endpoint, la periodicità e la direzione. Un descrittore di endpoint viene sempre restituito da un comando GET_DESCRIPTOR per la configurazione.

L'endpoint di controllo predefinito associato al descrittore del dispositivo non viene conteggiato come parte degli endpoint associati all'interfaccia e pertanto non viene restituito in questo descrittore.

Quando il software host richiede una modifica dell'impostazione alternativa per un'interfaccia, tutti gli endpoint associati e le relative risorse USB vengono modificati in base alla nuova impostazione alternativa.

Ad eccezione degli endpoint di controllo predefiniti, gli endpoint non possono essere condivisi tra interfacce.

| Offset | Campo            | Dimensione | Valore    | Descrizione                       |
| ------ | ---------------- | ---- | -------- | --------------------------------- |
| 0      | bLength          | 1    | Numero   | Dimensione del descrittore in byte. |
| 1      | bDescriptorType  | 1    | Costante | Tipo di descrittore ENDPOINT. |
| 2      | bEndpointAddress | 1    | Endpoint | Indirizzo dell'endpoint nel dispositivo USB descritto da questo descrittore. L'indirizzo viene codificato come segue:<br />Bit 3...0: numero dell'endpoint<br />Bit 6...4: Riservato, reimposta su zero<br />Bit 7: Direzione, ignorata per gli endpoint di controllo<br />0 = Endpoint OUT<br />1 = Endpoint IN |
| 3      | bmAttributes     | 1    | Bitmap   | Questo campo descrive gli attributi dell'endpoint quando viene configurato usando il **campo bConfigurationValue.** Bit 1..0: tipo di trasferimento<br />00 = Controllo<br />01 = Isocrono<br />10 = In blocco<br />11 = Interrupt<br />Se non è un endpoint isocrono, i bit 5..2 sono riservati e devono essere impostati su zero. Se isocrono, vengono definiti come segue:<br />Bits 3..2: tipo di sincronizzazione<br />00 = Nessuna sincronizzazione<br />01 = Asincrono<br />10 = Adattivo<br />11 = Sincrono<br />Bit 5..4: Tipo di utilizzo<br />00 = Endpoint dati<br />01 = Endpoint di feedback<br />10 = Endpoint dati di feedback implicito<br />11 = Riservato |
| 4      | wMaxPacketSize   | 2    | Numero   | Dimensioni massime del pacchetto che questo endpoint è in grado di inviare o ricevere quando questa configurazione è selezionata.<br />Per gli endpoint isocroni, questo valore viene usato per riservare l'ora del bus nella pianificazione, necessaria per i payload di dati per frame. La pipe può, su base continuativa, usare una larghezza di banda inferiore rispetto a quella riservata. Il dispositivo segnala, se necessario, la larghezza di banda effettiva usata tramite i normali meccanismi non definiti da USB.<br />Per tutti gli endpoint, i bit 10..0 specificano le dimensioni massime del pacchetto (in byte).<br />Per endpoint isocroni e interrupt ad alta velocità:<br />I bit 12..11 specificano il numero di opportunità di transazione aggiuntive per microframe: 00 = Nessuna (1 transazione per microframe)<br />01 = 1 aggiuntivo (2 per microframe)<br />10 = 2 aggiuntivi (3 per microframe)<br />11 = Riservato<br />I bit 15..13 sono riservati e devono essere impostati su zero. |
| 6      | bInterval        | 1     | Numero   | Intervallo di numeri per l'endpoint di polling per i trasferimenti di dati.<br />Espresso in fotogrammi o microframe a seconda della velocità operativa del dispositivo (ad esempio, 1 millisecondo o 125 unità μs).<br />Per gli endpoint isocroni a velocità elevata/completa, questo valore deve essere compreso nell'intervallo da 1 a 16. **BInterval viene** usato come esponente per un valore 2bInterval-1. Ad esempio, **bInterval** 4 indica un periodo di 8 (24-1).<br />Per gli endpoint di interrupt full-/low-speed, il valore di questo campo può essere compreso tra 1 e 255.<br />Per gli endpoint di interrupt ad alta velocità, **bInterval** viene usato come esponente per un valore 2bInterval-1. Ad esempio, **bInterval** 4 indica un periodo di 8 (24-1). Questo valore deve essere compreso tra 1 e 16.<br />Per gli endpoint OUT in blocco/controllo ad alta velocità, **bInterval** specifica la velocità NAK massima dell'endpoint. Il valore 0 indica che l'endpoint non ha mai naK. Altri valori indicano al massimo un NAK ogni **bInterval** di microframe.<br />Questo valore deve essere compreso nell'intervallo da 0 a 255. |

USBX definisce un descrittore di endpoint USB come segue:

```c
typedef struct UX_ENDPOINT_DESCRIPTOR_STRUCT
{
    UINT bLength;
    UINT bDescriptorType;
    UINT bEndpointAddress;
    UINT bmAttributes;
    USHORT wMaxPacketSize;
    UINT bInterval;
} UX_ENDPOINT_DESCRIPTOR;
```

Il descrittore dell'endpoint USB fa parte di un contenitore di endpoint, come descritto di seguito.

```c
typedef struct UX_ENDPOINT_STRUCT {
    ULONG    ux_endpoint_handle;
    ULONG    ux_endpoint_state;
    VOID    *ux_endpoint_ed;
    struct UX_ENDPOINT_DESCRIPTOR_STRUCT    ux_endpoint_descriptor;
    struct UX_ENDPOINT_STRUCT    *ux_endpoint_next_endpoint;
    struct UX_INTERFACE_STRUCT    *ux_endpoint_interface;
    struct UX_DEVICE_STRUCT    *ux_endpoint_device;
    struct UX_TRANSFER REQUEST_STRUCT    ux_endpoint_transfer request;
} UX_ENDPOINT;

```

- **ux_endpoint_handle**: handle dell'endpoint. Si tratta in genere dell'indirizzo dell'istanza di questa struttura per l'endpoint.
- **ux_endpoint_state:** stato dell'endpoint.
- **ux_endpoint_ed:** puntatore all'endpoint fisico a livello del controller host.
- **ux_endpoint_descriptor:** descrittore dell'endpoint USB.
- **ux_endpoint_next_endpoint**: puntatore all'endpoint successivo che appartiene alla stessa interfaccia.
- **ux_endpoint_interface**: puntatore all'interfaccia proprietaria di questa interfaccia endpoint.
- **ux_endpoint_device:** puntatore al contenitore del dispositivo padre.
- **ux_endpoint_transfer richiesta:** richiesta di trasferimento USB usata per inviare/ricevere dati da/verso il dispositivo.

### <a name="string-descriptors"></a>Descrittori di stringa

I descrittori di stringa sono facoltativi. Se un dispositivo non supporta i descrittori di stringa, tutti i riferimenti ai descrittori di stringa all'interno dei descrittori di dispositivo, configurazione e interfaccia devono essere reimpostati su zero.

I descrittori di stringa usano la codifica UNICODE, consentendo così il supporto per diversi set di caratteri. Le stringhe in un dispositivo USB possono supportare più lingue. Quando si richiede un descrittore di stringa, il richiedente specifica la lingua desiderata usando un ID lingua definito da USB-IF. L'elenco dei LANGID USB attualmente definiti è disponibile nell'appendice USBX ??.
L'indice di stringa zero per tutte le lingue restituisce un descrittore di stringa che contiene una matrice di codici LANGID a due byte supportati dal dispositivo. Si noti che la stringa UNICODE non termina con 0. Al contrario, le dimensioni della matrice di stringhe vengono calcolate sottraendo due dalla dimensione della matrice contenuta nel primo byte del descrittore.

Il descrittore di stringa USB 0 viene codificato come segue.

| Offset | Campo           | Dimensione | Valore    | Descrizione                      |
| ------ | --------------- | ---- | -------- | -------------------------------- |
| 0      | bLength         | 1    | N+2      | Dimensioni del descrittore in byte |
| 1      | bDescriptorType | 1    | Costante | Tipo di descrittore STRING           |
| 2      | wLANGID[0]      | 2    | Numero   | Codice LANGID 0                    |
| ...    | ...]            | ...  | ...      | ...                              |
| N      | wLANGID[n]      | 2    | Numero   | Codice LANGID n                    |

Altri descrittori di stringa USB vengono codificati come indicato di seguito.

| Offset | Campo           | Dimensione | Valore    | Descrizione                      |
| ------ | --------------- | ---- | -------- | -------------------------------- |
| 0      | bLength         | 1    | Numero   | Dimensioni del descrittore in byte |
| 1      | bDescriptorType | 1    | Costante | Tipo di descrittore STRING           |
| 2      | bString         | n    | Numero   | Stringa con codifica UNICODE           |

USBX definisce un descrittore di stringa USB di lunghezza diverso da zero come segue:

```c
typedef struct UX_STRING_DESCRIPTOR_STRUCT
{
    UINT bLength;
    UINT bDescriptorType;
    USHORT bString[1];
} UX_STRING_DESCRIPTOR;
```

### <a name="functional-descriptors"></a>Descrittori funzionali

I descrittori funzionali sono noti anche come descrittori specifici della classe. In genere usano le stesse strutture di base dei descrittori generici e consentono la disponibilità di informazioni aggiuntive per la classe. Ad esempio, nel caso dell'altoparlante audio USB, i descrittori specifici della classe consentono alla classe audio di recuperare per ogni impostazione alternativa il tipo di frequenza audio supportato.

### <a name="usbx-device-descriptor-framework-in-memory"></a>USBX Device Descriptor Framework in Memory

USBX mantiene la maggior parte dei descrittori di dispositivo in memoria, ad eccezione della stringa e dei descrittori funzionali. Il diagramma seguente illustra come questi descrittori vengono archiviati e correlati.

![USBX Device Descriptor Framework in Memory](./media/usbx-host-stack/usbx-device-descriptor-framework.png)
