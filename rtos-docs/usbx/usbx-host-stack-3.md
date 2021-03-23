---
title: Capitolo 3-componenti funzionali dello stack host USBX
description: Questo capitolo contiene una descrizione dello stack host USB incorporato USBX a prestazioni elevate dal punto di vista funzionale.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 17b8d884dd2c71d60e91f5fcec40c360060f4fe8
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104824272"
---
# <a name="chapter-3---functional-components-of-usbx-host-stack"></a>Capitolo 3-componenti funzionali dello stack host USBX

Questo capitolo contiene una descrizione dello stack host USB incorporato USBX a prestazioni elevate dal punto di vista funzionale.

## <a name="execution-overview"></a>Panoramica dell'esecuzione

USBX è costituito da diversi componenti:

- Inizializzazione
- Chiamate dell'interfaccia dell'applicazione
- Hub radice
- Classe Hub
- Classi host
- Stack host USB
- Controller host

Il diagramma seguente illustra lo stack host USBX.

![Stack host USBX](./media/usbx-host-stack/usbx-host-stack.png)

### <a name="initialization"></a>Inizializzazione

Per attivare USBX, è necessario chiamare la funzione ***ux_system_initialize*** . Questa funzione Inizializza le risorse di memoria di USBX.

Per attivare le funzionalità host USBX, è necessario chiamare la funzione ***ux_host_stack_initialize*** . Questa funzione inizializza a sua volta tutte le risorse usate dallo stack host USBX, ad esempio thread ThreadX, mutex e semafori.

L'inizializzazione dell'applicazione consente di attivare almeno un controller host USB e una o più classi USB. Quando le classi sono state registrate nello stack e la funzione di inizializzazione dei controller host è stata chiamata, il bus è attivo e l'individuazione del dispositivo può essere avviata. Se l'hub radice del controller host rileva un dispositivo collegato, il thread di enumerazione USB, responsabile della topologia USB, verrà riattivato e continuerà a enumerare i dispositivi.

È possibile, a causa della natura dell'hub radice e degli hub downstream, che tutti i dispositivi USB collegati potrebbero non essere stati configurati completamente quando la funzione di inizializzazione del controller host restituisce. L'enumerazione di tutti i dispositivi USB può richiedere alcuni secondi, soprattutto se sono presenti uno o più hub tra l'hub radice e i dispositivi USB.

### <a name="application-interface-calls"></a>Chiamate dell'interfaccia dell'applicazione

In USBX sono disponibili due livelli di API.

- API dello stack host USB
- API della classe host USB

In genere, un'applicazione USBX non deve chiamare alcuna delle funzioni API dello stack host USB. La maggior parte delle applicazioni accederà solo alle funzioni API della classe USB.

### <a name="usb-host-stack-apis"></a>API dello stack host USB

Le funzioni API dello stack host sono responsabili della registrazione dei componenti USBX (classi host e controller host), della configurazione dei dispositivi e delle richieste di trasferimento per gli endpoint di dispositivo disponibili.

### <a name="usb-host-class-api"></a>API della classe host USB

Le API della classe sono molto specifiche per ogni classe USB. La maggior parte delle funzioni API comuni per le classi USB fornisce servizi quali l'apertura e la chiusura di un dispositivo, la lettura e la scrittura in un dispositivo.

### <a name="root-hub"></a>Hub radice

Ogni istanza del controller host ha uno o più hub radice USB. Il numero di hub radice è determinato dalla natura del controller oppure può essere recuperato leggendo registri specifici dal controller.

### <a name="hub-class"></a>Classe Hub

La classe Hub è responsabile della Guida degli hub USB. Un hub USB può essere un hub autonomo o come parte di un dispositivo composto, ad esempio una tastiera o un monitor. Un hub può essere autoalimentato o alimentato da bus. Gli hub basati su bus hanno un massimo di quattro porte a valle e possono consentire solo la connessione di dispositivi che sono dispositivi autonomi o basati su bus che usano meno di 100. Gli hub possono essere a cascata. Fino a cinque hub possono essere connessi tra loro.

### <a name="usb-host-stack"></a>Stack host USB

Lo stack host USB è il fulcro di USBX. Sono disponibili tre funzioni principali.

- Gestire la topologia del dispositivo USB.
- Associare un dispositivo USB a una o più classi.
- Fornire un'API alle classi per eseguire l'interrogazione del descrittore del dispositivo e i trasferimenti USB.

### <a name="topology-manager"></a>Gestione topologia

Il thread della topologia dello stack USB viene riattivato quando si connette un nuovo dispositivo o quando un dispositivo è stato disconnesso. L'hub radice o un hub normale può accettare le connessioni del dispositivo. Dopo che un dispositivo è stato connesso al dispositivo USB, il descrittore del dispositivo viene recuperato da Gestione topologia. Questo descrittore conterrà il numero di configurazioni possibili disponibili per questo dispositivo. La maggior parte dei dispositivi ha una sola configurazione. Alcuni dispositivi possono funzionare in modo diverso in base alla potenza disponibile disponibile sulla porta in cui è connessa. In tal caso, il dispositivo disporrà di più configurazioni che possono essere selezionate a seconda della potenza disponibile. Quando il dispositivo è configurato da Gestione topologia, può quindi creare la quantità di energia specificata nel descrittore di configurazione.

## <a name="usb-class-binding"></a>Associazione di classe USB

Quando il dispositivo è configurato, Gestione topologia consente a gestione classi di continuare l'individuazione del dispositivo esaminando i descrittori di interfaccia del dispositivo. Un dispositivo può avere uno o più descrittori di interfaccia.

Un'interfaccia rappresenta una funzione in un dispositivo. Un altoparlante USB, ad esempio, dispone di tre interfacce, una per lo streaming audio, una per il controllo audio e una per la gestione dei diversi pulsanti del altoparlante.

Gestione classi dispone di due meccanismi per unire le interfacce del dispositivo a una o più classi. Può usare la combinazione di un PID/VID (ID prodotto e ID fornitore) trovato nel descrittore di interfaccia o nella combinazione di classe/sottoclasse/protocollo.

La combinazione PID/VID è valida per le interfacce che non possono essere gestite da una classe generica. La combinazione classe/sottoclasse/protocollo viene usata dalle interfacce che appartengono a una classe certificata USB-IF, ad esempio una stampante, un hub, un'archiviazione, un audio o una HID.

Gestione classi contiene un elenco di classi registrate dall'inizializzazione di USBX. Gestione classi chiamerà ogni classe uno alla volta finché una classe non accetta di gestire l'interfaccia per il dispositivo. Una classe può gestire solo un'interfaccia. Per l'esempio dell'altoparlante audio USB, gestione classi chiamerà tutte le classi per ciascuna interfaccia.

Una volta che una classe accetta un'interfaccia, viene creata una nuova istanza di tale classe. Gestione classi eseguirà quindi la ricerca dell'impostazione alternativa predefinita per l'interfaccia. Un dispositivo può avere una o più impostazioni alternative per ogni interfaccia. L'impostazione alternativa 0 sarà on utilizzata per impostazione predefinita fino a quando una classe non decide di modificarla.

Per l'impostazione alternativa predefinita, gestione classi monta tutti gli endpoint contenuti nell'impostazione alternativa. Se il montaggio di ogni endpoint ha esito positivo, il gestore delle classi completerà il processo restituendo alla classe che terminerà l'inizializzazione dell'interfaccia.

### <a name="usbx-apis"></a>API USBX

Lo stack USB esporta un certo numero di API per le classi USB per eseguire l'interrogazione sul dispositivo e sui trasferimenti USB su endpoint specifici. Queste funzioni API sono descritte in dettaglio in questo manuale di riferimento.

### <a name="host-controller"></a>Controller host

Il driver del controller host è responsabile della Guida di un tipo specifico di controller USB. Un controller host USB può avere più controller all'interno di. Ad esempio, alcuni chipset Intel PC contengono due controller UHCI. Alcuni controller USB 2,0 contengono più istanze di un controller OHCI, oltre a un'istanza del controller EHCI.

Il controller host gestirà più istanze dello stesso controller. Per poter gestire la maggior parte dei controller host USB 2,0, sarà necessario inizializzare sia il controller OCHI che il controller EHCI durante l'inizializzazione di USBX.

Il controller host è responsabile della gestione dei seguenti elementi.

- Hub radice
- Risparmio energia
- Endpoint
- Trasferimenti

### <a name="root-hub"></a>Hub radice

La gestione dell'hub radice è responsabile della potenza di ogni porta del controller e dell'eventuale inserimento di un dispositivo. Questa funzionalità viene usata dall'hub radice generico USBX per interrogare le porte downstream del controller.

### <a name="power-management"></a>Risparmio energia

L'elaborazione del risparmio energia consente di gestire i segnali di sospensione/ripresa in modalità Gang, interessando quindi tutte le porte downstream del controller allo stesso tempo oppure singolarmente se il controller offre questa funzionalità.

### <a name="endpoints"></a>Endpoint

La gestione degli endpoint consente la creazione o l'eliminazione di endpoint fisici nel controller. Gli endpoint fisici sono entità di memoria analizzate dal controller se il controller supporta il DMA master o scritti nel controller. Gli endpoint fisici contengono informazioni sulle transazioni che devono essere eseguite dal controller.

### <a name="transfers"></a>Trasferimenti

Gestione trasferimento consente a una classe di eseguire una transazione in ogni endpoint creato. Ogni endpoint logico contiene un componente denominato richiesta di trasferimento per le richieste di trasferimento USB. La richiesta di trasferimento viene utilizzata dallo stack per descrivere la transazione. Questa richiesta di trasferimento viene quindi passata allo stack e al controller, che può suddividerla in diverse transazioni secondarie a seconda delle funzionalità del controller.

## <a name="usb-device-framework"></a>Framework del dispositivo USB

Un dispositivo USB è rappresentato da un albero di descrittori. Sono disponibili sei tipi principali di descrittori.

- Descrittori del dispositivo
- Descrittori di configurazione
- Descrittori di interfaccia
- Descrittori di endpoint
- Descrittori di stringa
- Descrittori funzionali

Un dispositivo USB può avere una descrizione molto semplice e ha un aspetto simile al seguente.
![Dispositivo USB semplice](./media/usbx-host-stack/usb-device-simple.png)

Nella figura precedente, il dispositivo ha una sola configurazione. Una singola interfaccia è associata a questa configurazione, a indicare che il dispositivo ha una sola funzione e ha un solo endpoint. Il descrittore del dispositivo è associato a un descrittore di stringa che fornisce un'identificazione visibile del dispositivo.

Tuttavia, un dispositivo può essere più complesso e può apparire come segue.

![Dispositivo USB complesso](./media/usbx-host-stack/usb-device-complex.png)

Nella figura precedente, il dispositivo dispone di due descrittori di configurazione collegati al descrittore del dispositivo. Questo dispositivo può indicare che dispone di due modalità di risparmio energia o può essere gestito da classi standard o classi proprietarie.

Collegato alla prima configurazione sono disponibili due interfacce che indicano che il dispositivo ha due funzioni logiche. La prima funzione ha 3 descrittori di endpoint e un descrittore funzionale. Il descrittore funzionale può essere usato dalla classe responsabile dell'azionamento dell'interfaccia per ottenere ulteriori informazioni su questa interfaccia normalmente non trovata da un descrittore generico.

### <a name="device-descriptors"></a>Descrittori del dispositivo

Ogni dispositivo USB ha un singolo descrittore di dispositivo. Questo descrittore contiene l'identificazione del dispositivo, il numero di configurazioni supportate e le caratteristiche dell'endpoint di controllo predefinito usato per la configurazione del dispositivo.

| Offset | Campo              | Dimensione | Valore    | Descrizione                             |
| ------ | ------------------ | ---- | -------- | --------------------------------------- |
| 0      | BLength            | 1    | Number   | Dimensioni del descrittore in byte |
| 1      | bDescriptorType    | 1    | Costante | Tipo di descrittore del dispositivo |
| 2      | bcdUSB             | 2    | BCD      | Numero di versione delle specifiche USB in BinaryCoded Dec<br />Esempio: 2,10 è equivalente a 0x210. Questo campo identifica la versione della specifica USB per cui il dispositivo e i relativi descrittori sono conformi. |
| 4      | bDeviceClass       | 1    | Classe    | Codice di classe (assegnato da USB-IF).<br />Se questo campo viene reimpostato su 0, ogni interfaccia all'interno di una configurazione specifica le proprie informazioni sulla classe e le varie interfacce operano in modo indipendente.<br />Se questo campo è impostato su un valore compreso tra 1 e 0xFE, il dispositivo supporta specifiche di classe diverse su interfacce diverse e le interfacce potrebbero non funzionare in modo indipendente. Questo valore identifica la definizione della classe utilizzata per le interfacce di aggregazione.<br />Se questo campo è impostato su 0xFF, la classe Device è specifica del fornitore. |
| 5      | bDeviceSubClass    | 1    | Sottoclasse | Codice di sottoclasse (assegnato da USB-IF).<br />Questi codici sono qualificati dal valore del campo bDeviceClass. Se il campo bDeviceClass viene reimpostato su 0, è necessario reimpostare anche questo campo su 0. Se il campo bDeviceClass non è impostato su 0xFF, tutti i valori sono riservati per l'assegnazione tramite USB. |
| 6      | bDeviceProtocol    | 1    | Protocollo | Codice del protocollo (assegnato da USB-IF).<br />Questi codici sono qualificati dal valore dei campi bDeviceClass e bDeviceSubClass. Se un dispositivo supporta i protocolli specifici della classe su un dispositivo, anziché un'interfaccia, questo codice identifica i protocolli usati dal dispositivo come definito dalla specifica della classe del dispositivo. Se questo campo viene reimpostato su 0, il dispositivo non usa protocolli specifici di classe in base a un dispositivo.<br />Tuttavia, può usare protocolli specifici di classe in base a un'interfaccia.<br />Se questo campo è impostato su 0xFF, il dispositivo utilizza un protocollo specifico del fornitore in base a un dispositivo. |
| 7      | bMaxPacketSize0    | 1    | Number   | Dimensioni massime del pacchetto per l'endpoint zero (sono valide solo le dimensioni in byte di 8, 16, 32 o 64) |
| 8      | idVendor           | 2    | ID       | ID fornitore (assegnato da USB-IF) |
| 10     | idProduct          | 2    | ID       | ID prodotto (assegnato dal produttore) |
| 12     | bcdDevice          | 2    | BCD      | Numero di rilascio del dispositivo in formato decimale con codifica binaria |
| 14     | iManufacturer      | 1    | Indice    | Indice del descrittore di stringa che descrive il produttore |
| 15     | iProduct           | 1    | Indice    | Indice del descrittore di stringa che descrive il prodotto |
| 16     | iSerialNumbe       | 1    | Indice    | Indice del descrittore di stringa che descrive il numero di serie del dispositivo |
| 17     | bNumConfigurations | 1    | Number   | Numero di configurazioni possibili |

USBX definisce un descrittore di dispositivo USB nel modo seguente:

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

Il descrittore di dispositivo USB fa parte di un contenitore di dispositivi descritto di seguito:

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

- **ux_device_handle**: handle del dispositivo. Si tratta in genere dell'indirizzo dell'istanza di questa struttura per il dispositivo.
- **ux_device_type**: valore obsoleto. Non utilizzato.
- **ux_device_state**: stato del dispositivo, che può avere uno dei valori seguenti:
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
- **ux_device_address**: indirizzo del dispositivo dopo l'accettazione del comando **SET_ADDRESS** (da 1 a 127).
- **ux_device_speed**: velocità del dispositivo:
    - **UX_LOW_SPEED_DEVICE**      0
    - **UX_FULL_SPEED_DEVICE**     1
    - **UX_HIGH_SPEED_DEVICE**     2
- **ux_device_port_location**: indice della porta del dispositivo padre (hub radice o hub).
- **ux_device_max_power**: potenza massima in ma che il dispositivo può assumere nella configurazione selezionata.
- **ux_device_power_source**: può essere uno dei due valori seguenti:
    - **UX_DEVICE_BUS_POWERED**     1
    - **UX_DEVICE_SELF_POWERED**    2
- **ux_device_current_configuration**: indice della configurazione corrente usata dal dispositivo.
- **ux_device_parent**: puntatore del contenitore del dispositivo dell'elemento padre del dispositivo. Se il puntatore è null, l'elemento padre è l'hub radice del controller.
- **ux_device_class**: puntatore al tipo di classe proprietario del dispositivo.
- **ux_device_class_instance**: puntatore all'istanza della classe proprietaria del dispositivo.
- **ux_device_hcd**: istanza del controller host USB a cui è collegato il dispositivo.
- **ux_device_first_configuration**: puntatore al primo contenitore di configurazione per il dispositivo.
- **ux_device_next_device**: puntatore al dispositivo successivo nell'elenco del dispositivo su uno dei bus rilevati da USBX.
- **ux_device_descriptor**: descrittore dispositivo USB.
- **ux_device_control_endpoint**: descrittore dell'endpoint di controllo predefinito usato dal dispositivo.
- **ux_device_hub_tt**: matrice di TTs dell'hub per il dispositivo

### <a name="configuration-descriptors"></a>Descrittori di configurazione

Il descrittore di configurazione descrive le informazioni sulla configurazione di un dispositivo specifico. Un dispositivo USB può contenere uno o più descrittori di configurazione. Il campo **bNumConfigurations** nel descrittore del dispositivo indica il numero di descrittori di configurazione. Il descrittore contiene un campo **bConfigurationValue** con un valore che, se usato come parametro della richiesta di configurazione set, fa in modo che il dispositivo assuma la configurazione descritta.

Il descrittore descrive il numero di interfacce fornite dalla configurazione. Ogni interfaccia rappresenta una funzione logica all'interno del dispositivo e può funzionare in modo indipendente. Ad esempio, un altoparlante audio USB può avere tre interfacce, una per lo streaming audio, una per il controllo audio e un'interfaccia nascosta per gestire i pulsanti dell'altoparlante.

Quando l'host emette una richiesta GET_DESCRIPTOR per il descrittore della configurazione, vengono restituiti tutti i descrittori di interfaccia e di endpoint correlati.

| Offset | Campo               | Dimensione | Valore    | Descrizione                       |
| ------ | ------------------- | ---- | -------- | --------------------------------- |
| 0      | bLength             | 1    | Number   | Dimensioni in byte del descrittore. |
| 1      | bDescriptorType     | 1    | Costante | CONFIGURATION                     |
| 2      | wTotalLength        | 2    | Number   | Lunghezza totale dei dati restituiti per questa configurazione. Include la lunghezza combinata di tutti i descrittori (configurazione, interfaccia, endpoint e classe o specifico del fornitore) restituiti per questa configurazione. |
| 4      | bNumInterfaces      | 1    | Number   | Numero di interfacce supportate da questa configurazione. |
| 5      | bConfigurationValue | 1    | Number   | Valore da usare come argomento da impostare<br/>Configurazione per selezionare questa configurazione. |
| 6      | iConfiguration      | 1    | Indice    | Indice del descrittore di stringa che descrive questa configurazione. |
| 7      | bMAttributes        | 1    | Bitmap   | Caratteristiche di configurazione del bus D7 con tecnologia<br />D6 auto alimentato<br />Riattivazione remota D5<br />D4.. 0 riservato (Reimposta su 0)<br />Una configurazione del dispositivo che usa l'alimentazione dal bus e un'origine locale imposta sia D7 che D6. La fonte di alimentazione effettiva in fase di esecuzione può essere determinata usando la richiesta Get status Device.<br />Se una configurazione del dispositivo supporta la riattivazione remota, D5 è impostato su 1. |
| 8      | MaxPower            | 1    | mA       | Consumo di energia massimo del dispositivo USB dal bus in questa configurazione specifica quando il dispositivo è completamente operativo.<br />Espressa in unità di 2 mA (ad esempio, 50 = 100 mA).<br />Nota: una configurazione del dispositivo segnala se la configurazione è basata su bus o auto-alimentato.<br />Lo stato del dispositivo segnala se il dispositivo è attualmente autoalimentato. Se un dispositivo è disconnesso dalla fonte di alimentazione esterna, aggiorna lo stato del dispositivo per indicare che non è più autoalimentato. |

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

Il descrittore di configurazione USB fa parte di un contenitore di configurazione descritto come illustrato di seguito.

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

- **ux_configuration_handle**: handle della configurazione. Si tratta in genere dell'indirizzo dell'istanza di questa struttura per la configurazione.
- **ux_configuration_state**: stato della configurazione.
- **ux_configuration_descriptor**: descrittore dispositivo USB.
- **ux_configuration_first_interface**: puntatore alla prima interfaccia per questa configurazione.
- **ux_configuration_next_configuration**: puntatore alla configurazione successiva per lo stesso dispositivo.
- **ux_configuration_device**: puntatore al proprietario del dispositivo di questa configurazione.

### <a name="interface-descriptors"></a>Descrittori di interfaccia

Il descrittore di interfaccia descrive un'interfaccia specifica all'interno di una configurazione. Un'interfaccia è una funzione logica all'interno di un dispositivo USB. Una configurazione fornisce una o più interfacce, ognuna con zero o più descrittori di endpoint che descrivono un set univoco di endpoint all'interno della configurazione. Quando una configurazione supporta più interfacce, i descrittori di endpoint per una determinata interfaccia seguono il descrittore di interfaccia nei dati restituiti dalla richiesta **GET_DESCRIPTOR** per la configurazione specificata.

Un descrittore di interfaccia viene sempre restituito come parte di un descrittore di configurazione. Non è possibile accedere direttamente a un descrittore di interfaccia tramite una richiesta GET_DESCRIPTOR.

Un'interfaccia può includere impostazioni alternative che consentono di variare gli endpoint e/o le relative caratteristiche dopo la configurazione del dispositivo. L'impostazione predefinita per un'interfaccia è sempre un'impostazione alternativa zero. Una classe può scegliere di modificare l'impostazione alternativa corrente per modificare il comportamento dell'interfaccia e le caratteristiche degli endpoint associati. La richiesta SET_INTERFACE viene utilizzata per selezionare un'impostazione alternativa o per tornare all'impostazione predefinita.

Le impostazioni alternative consentono di variare una parte della configurazione del dispositivo mentre le altre interfacce restano in funzione. Se una configurazione presenta impostazioni alternative per una o più delle relative interfacce, per ogni impostazione viene incluso un descrittore di interfaccia separato e gli endpoint associati.

Se una configurazione del dispositivo contiene una singola interfaccia con due impostazioni alternative, la richiesta GET_DESCRIPTOR per la configurazione restituisce il descrittore di configurazione, quindi il descrittore di interfaccia con i campi **bInterfaceNumber** e **bAlternateSetting** impostati su zero e quindi i descrittori dell'endpoint per tale impostazione, seguiti da un altro descrittore di interfaccia e i descrittori di endpoint associati. Anche il campo **bInterfaceNumber** del secondo descrittore di interfaccia verrà impostato su zero, ma il campo **bAlternateSetting** del secondo descrittore di interfaccia verrà impostato su 1 per indicare che questa impostazione alternativa appartiene alla prima interfaccia.

A un'interfaccia non possono essere associati endpoint, nel qual caso solo l'endpoint di controllo predefinito è valido per tale interfaccia.

Le impostazioni alternative vengono utilizzate principalmente per modificare la larghezza di banda richiesta per gli endpoint periodici associati all'interfaccia. Ad esempio, un'interfaccia di streaming di altoparlanti USB deve avere la prima impostazione alternativa con una richiesta di larghezza di banda 0 sul relativo endpoint isocrono. Altre impostazioni alternative possono selezionare requisiti di larghezza di banda diversi a seconda della frequenza di streaming audio.

Il descrittore USB per l'interfaccia è il seguente:

| Offset | Campo              | Dimensione | Valore     | Descrittore                              |
| ------ | ------------------ | ---- | --------- | --------------------------------------- |
| 0      | bLength            | 1    | Number    | Dimensioni in byte del descrittore.       |
| 1      | bDescriptorType    | 1    | Costante  | Tipo di descrittore di interfaccia               |
| 2      | bInterfaceNumber   | 1    | Number    | Numero di interfaccia. Valore in base zero che identifica l'indice nella matrice di interfacce simultanee supportate da questa configurazione. |
| 3      | bAltenateSetting   | 1    | Number    | Valore utilizzato per selezionare l'impostazione alternativa per l'interfaccia identificata nel campo precedente. |
| 4      | bNumEndpoints      | 1    | Number    | Numero di endpoint utilizzati da questa interfaccia (escluso l'endpoint zero). Se questo valore è 0, questa interfaccia usa solo l'endpoint zero. |
| 5      | bInterfaceClass    | 1    | Classe     | Codice di classe (assegnato da USB)<br />Se questo campo viene reimpostato su 0, l'interfaccia non appartiene ad alcuna classe di dispositivo USB specificata.<br />Se questo campo è impostato su 0xFF, la classe di interfaccia è specifica del fornitore.<br />Tutti gli altri valori sono riservati per l'assegnazione tramite USB. |
| 6      | bInterfaceSubClass | 1    | Sottoclasse  | Codice di sottoclasse (assegnato da USB).<br />Questi codici sono qualificati dal valore del campo bInterfaceClass. Se il campo bInterfaceClass viene reimpostato su 0, è necessario reimpostare anche questo campo su 0. Se il campo bInterfaceClass non è impostato su 0xFF, tutti i valori sono riservati per l'assegnazione tramite USB. |
| 7      | bInterfaceProtocol | 1    | Protocollo  | Codice del protocollo (assegnato da USB). Questi codici sono qualificati dal valore dei campi bInterfaceClass e bInterfaceSubClass. Se un'interfaccia supporta richieste specifiche della classe, questo codice identifica i protocolli usati dal dispositivo come definito dalla specifica della classe del dispositivo.<br />Se questo campo viene reimpostato su 0, il dispositivo non usa un protocollo specifico della classe su questa interfaccia. Se questo campo è impostato su 0xFF, il dispositivo utilizza un protocollo specifico del fornitore per questa interfaccia. |
| 8      | iInterface         | 1    | Indice     | Indice del descrittore di stringa che descrive questa interfaccia. |

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

Il descrittore dell'interfaccia USB fa parte di un contenitore di interfaccia descritto di seguito.

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

- **ux_interface_handle**: handle dell'interfaccia. Si tratta in genere dell'indirizzo dell'istanza di questa struttura per l'interfaccia.
- **ux_interface_state**: stato dell'interfaccia.
- **ux_interface_descriptor**: descrittore dell'interfaccia USB.
- **ux_interface_class**: puntatore al tipo di classe a cui appartiene questa interfaccia.
- **ux_interface_class_instance**: puntatore all'istanza della classe a cui appartiene questa interfaccia.
- **ux_interface_first_endpoint**: puntatore al primo endpoint registrato con questa interfaccia.
- **ux_interface_next_interface**: puntatore alla successiva interfaccia associata alla configurazione.
- **ux_interface_configuration**: puntatore al proprietario della configurazione di questa interfaccia.

### <a name="endpoint-descriptors"></a>Descrittori di endpoint

Ogni endpoint associato a un'interfaccia ha il proprio descrittore dell'endpoint. Questo descrittore contiene le informazioni richieste dallo stack host per determinare i requisiti di larghezza di banda di ogni endpoint, il payload massimo associato all'endpoint, la periodicità e la direzione. Un descrittore dell'endpoint viene sempre restituito da un GET_DESCRIPTOR comando per la configurazione.

L'endpoint di controllo predefinito associato al descrittore del dispositivo non viene conteggiato come parte degli endpoint associati all'interfaccia e pertanto non viene restituito in questo descrittore.

Quando il software host richiede una modifica dell'impostazione alternativa per un'interfaccia, tutti gli endpoint associati e le relative risorse USB vengono modificati in base alla nuova impostazione alternativa.

Ad eccezione degli endpoint di controllo predefiniti, gli endpoint non possono essere condivisi tra le interfacce.

| Offset | Campo            | Dimensione | Valore    | Descrizione                       |
| ------ | ---------------- | ---- | -------- | --------------------------------- |
| 0      | bLength          | 1    | Number   | Dimensioni in byte del descrittore. |
| 1      | bDescriptorType  | 1    | Costante | Tipo di descrittore dell'ENDPOINT. |
| 2      | bEndpointAddress | 1    | Endpoint | Indirizzo dell'endpoint sul dispositivo USB descritto da questo descrittore. L'indirizzo è codificato come indicato di seguito:<br />Bit 3... 0: numero di endpoint<br />Bit 6... 4: riservato, reimpostazione a zero<br />Bit 7: direzione, ignorato per gli endpoint di controllo<br />0 = endpoint OUT<br />1 = IN endpoint |
| 3      | bmAttributes     | 1    | Bitmap   | Questo campo descrive gli attributi dell'endpoint quando viene configurato usando il campo **bConfigurationValue** . BITS 1.. 0: tipo di trasferimento<br />00 = controllo<br />01 = isocrono<br />10 = bulk<br />11 = interrupt<br />Se non si tratta di un endpoint isocrono, i bit 5.. 2 sono riservati e devono essere impostati su zero. Se isocrone, vengono definiti come segue:<br />BITS 3.. 2: tipo di sincronizzazione<br />00 = nessuna sincronizzazione<br />01 = asincrono<br />10 = adattivo<br />11 = sincrono<br />BITS 5.. 4: tipo di utilizzo<br />00 = endpoint dati<br />01 = endpoint feedback<br />10 = endpoint dati di commenti impliciti<br />11 = riservato |
| 4      | wMaxPacketSize   | 2    | Number   | Dimensioni massime pacchetti questo endpoint è in grado di inviare o ricevere quando viene selezionata questa configurazione.<br />Per gli endpoint isocroni, questo valore viene usato per riservare il tempo del bus nella pianificazione, necessario per i payload dei dati del frame per (micro). La pipe può, su base continuativa, usare effettivamente una larghezza di banda inferiore rispetto a quella riservata. Il dispositivo segnala, se necessario, la larghezza di banda effettiva utilizzata tramite i normali meccanismi non USB definiti.<br />Per tutti gli endpoint, bits 10.. 0 specifica la dimensione massima del pacchetto (in byte).<br />Per gli endpoint di interrupt e isocroni ad alta velocità:<br />BITS 12.. 11 specificare il numero di opportunità di transazione aggiuntive per microframe: 00 = None (1 transazione per microframe)<br />01 = 1 aggiuntivo (2 per microframe)<br />10 = 2 aggiuntivi (3 per microframe)<br />11 = riservato<br />Bits 15.. 13 sono riservati e devono essere impostati su zero. |
| 6      | bInterval        | 1     | Number   | Intervallo numerico per l'endpoint di polling per i trasferimenti di dati.<br />Espressa in frame o microframe, a seconda della velocità operativa del dispositivo (ad esempio, 1 millisecondo o 125 μs).<br />Per gli endpoint isocroni/High-Speed completi, questo valore deve essere compreso tra 1 e 16. **BInterval** viene usato come esponente per un valore 2bInterval-1; ad esempio, un **bInterval** 4 indica un periodo di 8 (24-1).<br />Per gli endpoint di interrupt/Low-Speed completi, il valore di questo campo può essere compreso tra 1 e 255.<br />Per gli endpoint di interrupt ad alta velocità, **bInterval** viene usato come esponente per un valore 2bInterval-1; ad esempio, un **bInterval** 4 indica un periodo di 8 (24-1). Questo valore deve essere compreso tra 1 e 16.<br />Per gli endpoint ad alta velocità in blocco o di controllo, **bInterval** specifica la frequenza massima di NAK dell'endpoint. Il valore 0 indica che l'endpoint non è mai NAKs. Altri valori indicano al massimo un NAK ogni **bInterval** di microframe.<br />Questo valore deve essere compreso tra 0 e 255. |

USBX definisce un descrittore dell'endpoint USB nel modo seguente:

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

Il descrittore dell'endpoint USB fa parte di un contenitore di endpoint, descritto di seguito.

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
- **ux_endpoint_state**: stato dell'endpoint.
- **ux_endpoint_ed**: puntatore all'endpoint fisico a livello del controller host.
- **ux_endpoint_descriptor**: descrittore dell'endpoint USB.
- **ux_endpoint_next_endpoint**: puntatore all'endpoint successivo che appartiene alla stessa interfaccia.
- **ux_endpoint_interface**: puntatore all'interfaccia a cui appartiene questa interfaccia endpoint.
- **ux_endpoint_device**: puntatore al contenitore del dispositivo padre.
- **ux_endpoint_transfer request**: richiesta di trasferimento USB usata per inviare/ricevere dati da e verso il dispositivo.

### <a name="string-descriptors"></a>Descrittori di stringa

I descrittori di stringa sono facoltativi. Se un dispositivo non supporta descrittori di stringa, tutti i riferimenti a descrittori di stringa nei descrittori di dispositivo, configurazione e interfaccia devono essere reimpostati su zero.

I descrittori di stringa utilizzano la codifica UNICODE, consentendo così il supporto di diversi set di caratteri. Le stringhe in un dispositivo USB possono supportare più lingue. Quando si richiede un descrittore di stringa, il richiedente specifica la lingua desiderata usando un ID lingua definito da USB-IF. L'elenco dei LANGIDs USB attualmente definiti è disponibile nell'appendice USBX??.
L'indice stringa zero per tutti i linguaggi restituisce un descrittore di stringa che contiene una matrice di codici LANGID a due byte supportati dal dispositivo. Si noti che la stringa UNICODE non è terminata con 0. Al contrario, le dimensioni della matrice di stringhe vengono calcolate sottraendo due dalla dimensione della matrice contenuta nel primo byte del descrittore.

Il descrittore di stringa USB 0 è codificato come indicato di seguito.

| Offset | Campo           | Dimensione | Valore    | Descrizione                      |
| ------ | --------------- | ---- | -------- | -------------------------------- |
| 0      | bLength         | 1    | N + 2      | Dimensioni del descrittore in byte |
| 1      | bDescriptorType | 1    | Costante | Tipo di descrittore di stringa           |
| 2      | wLANGID [0]      | 2    | Number   | Codice LANGID 0                    |
| ...    | ...]            | ...  | ...      | ...                              |
| N      | wLANGID [n]      | 2    | Number   | Codice LANGID n                    |

Gli altri descrittori di stringa USB sono codificati come indicato di seguito.

| Offset | Campo           | Dimensione | Valore    | Descrizione                      |
| ------ | --------------- | ---- | -------- | -------------------------------- |
| 0      | bLength         | 1    | Number   | Dimensioni del descrittore in byte |
| 1      | bDescriptorType | 1    | Costante | Tipo di descrittore di stringa           |
| 2      | bString         | n    | Number   | Stringa con codifica UNICODE           |

USBX definisce un descrittore di stringa USB di lunghezza diversa da zero, come indicato di seguito:

```c
typedef struct UX_STRING_DESCRIPTOR_STRUCT
{
    UINT bLength;
    UINT bDescriptorType;
    USHORT bString[1];
} UX_STRING_DESCRIPTOR;
```

### <a name="functional-descriptors"></a>Descrittori funzionali

I descrittori funzionali sono noti anche come descrittori specifici della classe. Usano normalmente le stesse strutture di base dei descrittori generici e consentono di rendere disponibili informazioni aggiuntive per la classe. Ad esempio, nel caso dell'altoparlante audio USB, i descrittori specifici della classe consentono alla classe audio di recuperare per ogni impostazione alternativa il tipo di frequenza audio supportata.

### <a name="usbx-device-descriptor-framework-in-memory"></a>USBX Framework descrittore dispositivi in memoria

USBX gestisce la maggior parte dei descrittori di dispositivo in memoria, ovvero tutti i descrittori ad eccezione dei descrittori di stringa e funzionali. Il diagramma seguente illustra come vengono archiviati e correlati tali descrittori.

![USBX Framework descrittore dispositivi in memoria](./media/usbx-host-stack/usbx-device-descriptor-framework.png)
