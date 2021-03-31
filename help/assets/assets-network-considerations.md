---
title: Considerazioni e requisiti della rete
description: Esamina le considerazioni sulla rete durante la progettazione di una distribuzione [!DNL Adobe Experience Manager Assets] e
contentOwner: AG
role: Architetto, amministratore
feature: Strumenti per gli sviluppatori
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 0%

---


# [!DNL Assets] considerazioni sulla rete  {#assets-network-considerations}

Comprendere la rete è importante quanto capire [!DNL Adobe Experience Manager Assets]. La rete può influenzare le esperienze di caricamento, download e utente. Il diagramma della topologia di rete consente di identificare i punti di interruzione e le aree sottoottimizzate della rete che è necessario correggere per migliorare le prestazioni di rete e l&#39;esperienza utente.

Accertati di includere quanto segue nel diagramma di rete:

* Connettività dal dispositivo client (ad esempio computer, dispositivi mobili e tablet) alla rete.
* Topologia della rete aziendale.
* Eseguire l&#39;aggiornamento a Internet dalla rete aziendale e dall&#39;ambiente [!DNL Experience Manager].
* Topologia dell&#39;ambiente [!DNL Experience Manager].
* Consente di definire utenti simultanei dell&#39;interfaccia di rete [!DNL Experience Manager].
* Flussi di lavoro definiti per la distribuzione [!DNL Experience Manager].

## Connettività dal dispositivo client alla rete aziendale {#connectivity-from-the-client-device-to-the-corporate-network}

Per iniziare, è necessario creare un diagramma della connettività tra i singoli dispositivi client e la rete aziendale. In questa fase, identifica le risorse condivise, come le connessioni WiFi, in cui più utenti accedono allo stesso punto o switch ethernet per caricare e scaricare le risorse.

![chlimage_1-353](assets/chlimage_1-353.png)

I dispositivi client si collegano alla rete aziendale in vari modi, come WiFi condiviso, Ethernet a uno switch condiviso e VPN. L&#39;identificazione e la comprensione dei punti di blocco su questa rete è importante per la pianificazione [!DNL Assets] e per modificare la rete.

Nella parte superiore sinistra del diagramma, tre dispositivi sono rappresentati come condivisione di un punto di accesso WiFi a 48 Mbps. Se tutti i dispositivi vengono caricati contemporaneamente, la larghezza di banda della rete WiFi viene condivisa tra i dispositivi. Rispetto al sistema nel suo insieme, un utente può incontrare un punto di rottura diverso per i tre client su questo canale diviso.

È difficile misurare la velocità effettiva di una rete WiFi perché un dispositivo lento può influenzare altri clienti sul punto di accesso. Se prevedi di utilizzare WiFi per le interazioni delle risorse, esegui un test di velocità da più client simultaneamente per valutare il throughput.

Nella parte in basso a sinistra del diagramma sono rappresentati due dispositivi collegati alla rete aziendale attraverso canali indipendenti. Ogni dispositivo può quindi usufruire di una velocità minima di 10 Mbps e 100 Mbps.

Il computer visualizzato a destra ha un limite a monte della rete aziendale su una VPN con una velocità di 1 Mbps. L&#39;esperienza utente per la connessione a 1 Mbps è molto diversa dall&#39;esperienza utente sulla connessione a 1 Gb/s. A seconda delle dimensioni delle risorse con cui gli utenti interagiscono, il loro uplink VPN potrebbe essere inadeguato per l’attività.

## Topologia della rete aziendale {#topology-of-the-corporate-network}

![chlimage_1-354](assets/chlimage_1-354.png)

Il diagramma mostra velocità di uplink superiori all&#39;interno della rete aziendale rispetto a quelle generalmente utilizzate. Questi tubi sono risorse condivise. Se si prevede che lo switch condiviso gestisca 50 client, può potenzialmente essere un punto di rottura. Nel diagramma iniziale, solo due computer condividono la connessione specifica.

## Collegamento a Internet dalla rete aziendale e dall&#39; [!DNL Experience Manager] ambiente {#uplink-to-the-internet-from-the-corporate-network-and-aem-environment}

![chlimage_1-355](assets/chlimage_1-355.png)

È importante considerare fattori sconosciuti su Internet e la connessione VPC perché la larghezza di banda su Internet può essere compromessa a causa del picco di carico o di interruzioni del provider su larga scala. In generale, la connettività Internet è affidabile. Tuttavia, a volte può introdurre dei punti di ostinazione.

Dall&#39;uplink da una rete aziendale a Internet, possono esserci altri servizi che utilizzano la larghezza di banda. È importante comprendere quanto della larghezza di banda può essere dedicata o prioritaria ad Assets. Ad esempio, se un collegamento da 1 Gb/s è già utilizzato all&#39;80%, è possibile allocare solo un massimo del 20% della larghezza di banda per [!DNL Experience Manager Assets].

I firewall e i proxy aziendali possono inoltre modellare la larghezza di banda in molti modi diversi. Questo tipo di dispositivo può dare priorità alla larghezza di banda utilizzando la qualità del servizio, i limiti di larghezza di banda per utente o i limiti di bitrate per host. Si tratta di punti di interruzione importanti da esaminare in quanto possono avere un impatto significativo sull’ [!DNL Assets] esperienza utente.

In questo esempio, l&#39;azienda dispone di un uplink a 10 Gb/s. Deve essere sufficientemente grande per diversi client. Inoltre, il firewall impone un limite di velocità host di 10 Mbps. Questa limitazione può potenzialmente limitare il traffico a un singolo host a 10 Mbps, anche se l&#39;uplink a Internet è a 10 Gbps.

Questo è il punto di rottura più piccolo orientato al cliente. Tuttavia, è possibile valutare la presenza di una modifica o configurare un elenco Consentiti con il gruppo di operazioni di rete responsabile di questo firewall.

Dai diagrammi di esempio si può concludere che sei dispositivi condividono un canale concettuale a 10 Mbps. A seconda delle dimensioni delle risorse utilizzate, ciò potrebbe risultare inadeguato per soddisfare le aspettative degli utenti.

## Topologia dell’ ambiente [!DNL Experience Manager] {#topology-of-the-aem-environment}

![chlimage_1-356](assets/chlimage_1-356.png)

La progettazione della topologia dell&#39;ambiente [!DNL Experience Manager] richiede una conoscenza dettagliata della configurazione del sistema e del modo in cui la rete viene connessa all&#39;interno dell&#39;ambiente utente.

Lo scenario di esempio include una farm di pubblicazione con cinque server, un archivio binario S3 e Dynamic Media configurati.

Il dispatcher condivide la connessione a 100 Mbps con due entità, il mondo esterno e la distribuzione [!DNL Experience Manager]. Per le operazioni di caricamento e download simultanee, è necessario dividere questo numero per due. L&#39;archiviazione esterna collegata utilizza una connessione separata.

La distribuzione [!DNL Experience Manager] condivide la propria connessione a 1 Gb/s con più servizi. Dal punto di vista della topologia di rete, equivale a condividere un singolo canale con servizi diversi.

Esaminando la rete dal dispositivo client all&#39;implementazione [!DNL Experience Manager], il punto di interruzione più piccolo sembra essere la velocità del firewall Enterprise a 10 Mbit. Puoi utilizzare questi valori nel calcolatore delle dimensioni nella [Guida al dimensionamento delle risorse](assets-sizing-guide.md) per determinare l&#39;esperienza utente.

## Flussi di lavoro definiti per la distribuzione [!DNL Experience Manager] {#defined-workflows-of-the-aem-deployment}

Quando si considerano le prestazioni di rete, può essere importante considerare i flussi di lavoro e la pubblicazione che si verificheranno nel sistema. Inoltre, le richieste S3 o altro storage collegato di rete che si utilizzano e I/O richiedono una larghezza di banda di rete. Pertanto, anche in una rete completamente ottimizzata, le prestazioni possono essere limitate dall&#39;I/O del disco.

Per semplificare i processi relativi all’inserimento delle risorse (in particolare durante il caricamento di un numero elevato di risorse), esplora i flussi di lavoro delle risorse e ne scopri di più sulla loro configurazione.

Durante la valutazione della topologia del flusso di lavoro interno, è necessario analizzare quanto segue:

* Procedure per la scrittura di una risorsa
* Flussi di lavoro/eventi che si attivano quando la risorsa/i metadati vengono modificati
* Procedure per la lettura di una risorsa

Di seguito sono riportati alcuni elementi da considerare:

* Lettura/riscrittura dei metadati XMP
* Attivazione e replica automatiche
* Inserimento di filigrane
* Acquisizione di risorse secondarie/estrazione pagina
* Sovrapposizione dei flussi di lavoro.

Ecco un esempio di cliente per la definizione di un flusso di lavoro delle risorse.

![chlimage_1-357](assets/chlimage_1-357.png)
