---
title: Integrazione con Adobe Target
seo-title: Integrating with Adobe Target
description: Scopri come integrare AEM con Adobe Target.
seo-description: Learn about integrating AEM with Adobe Target.
uuid: b90346e8-9757-4272-a870-bbe5e647303f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 454854f8-6053-406c-888d-f427777bf570
exl-id: 2b17d8cd-a43c-4d54-b990-a6f0cb1db22b
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 63%

---

# Integrazione con Adobe Target{#integrating-with-adobe-target}

Come parte di Adobe Marketing Cloud, [Adobe Target](https://www.adobe.com/ro/solutions/testing-targeting/testandtarget.html) consente di aumentare la rilevanza dei contenuti mediante il targeting e la valutazione su tutti i canali. Adobe Target viene utilizzato dagli esperti di marketing per progettare ed eseguire test online, creare all’istante segmenti di pubblico (in base al comportamento) e automatizzare il targeting di contenuti ed esperienze online. AEM adottato il flusso di lavoro di targeting utilizzato in Adobe Target Standard. Se utilizzi Target, acquisisci familiarità con l’ambiente di modifica del targeting in AEM.

Integra i tuoi siti di AEM con Adobe Target per personalizzare i contenuti delle tue pagine:

* Implementa il targeting dei contenuti.
* Utilizza il pubblico di Target per creare esperienze personalizzate.
* Invia dati contestuali a Target quando i visitatori interagiscono con le tue pagine.
* Tieni traccia delle percentuali di conversione.

Per eseguire l’integrazione con Target, esegui le seguenti attività:

1. [Esegui attività preliminari](/help/sites-administering/target-requirements.md): registrati ad Adobe Target e configura alcuni aspetti dell’istanza di authoring AEM. Il tuo account Adobe Target deve disporre di autorizzazioni a livello di **approver **almeno. Inoltre, devi proteggere le impostazioni dell’attività sul nodo di pubblicazione in modo che sia inaccessibile agli utenti.

1. Effettua una delle seguenti operazioni:

   1. [Opt in Adobe Target](/help/sites-administering/opt-in.md): La procedura guidata di consenso prende le informazioni dell’account Target e crea una configurazione cloud di Adobe Target e un framework di Target. La procedura guidata associa inoltre i siti a Target Framework. Se la procedura guidata non è in grado di connettersi a Target, fare riferimento alla [risoluzione dei problemi di connessione](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems) sezione . È quindi possibile [Modifica le configurazioni cloud predefinite](/help/sites-administering/target-configuring.md#modifying-the-opt-in-wizard-configurations): Se necessario, modifica la configurazione e il framework cloud creati dalla procedura guidata di consenso. Ad esempio, modifica il framework per inviare dati di contesto aggiuntivi a Target. Se desideri utilizzare Adobe Analytics come origine per la generazione di rapporti per Adobe Target, devi modificare la configurazione cloud per puntare alla configurazione A4T.
   1. [Integrazione manuale con Adobe Target](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target).

1. [Configurare le attività](/help/sites-authoring/activitylib.md): associa le attività alla configurazione cloud di Target.

>[!NOTE]
>
>Vedi anche [Integrazione di AEM con Adobe Target e Adobe Analytics tramite DTM](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

>[!NOTE]
>
>Se utilizzi Target con una configurazione proxy personalizzata, devi impostare entrambe le configurazioni proxy del client HTTP, in quanto alcune funzionalità di AEM utilizzano le API 3.x e altre le API 4.x:
>
>* 3.x è configurato con [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x è configurato con [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>


>[!CAUTION]
>
>È necessario proteggere il nodo delle impostazioni delle attività **cq:ActivitySettings** sull&#39;istanza di pubblicazione in modo che sia inaccessibile agli utenti normali. Il nodo delle impostazioni delle attività deve essere accessibile solo al servizio che gestisce la sincronizzazione delle attività con Adobe Target.
>
>Consulta [Prerequisiti per l&#39;integrazione con Adobe Target](/help/sites-administering/target-requirements.md#securing-the-activity-settings-node) per informazioni dettagliate.

Una volta completata l’integrazione, puoi [contenuto mirato dell&#39;autore](/help/sites-authoring/content-targeting-touch.md) che invia i dati dei visitatori ad Adobe Target. I Componenti Pagina richiedono un codice specifico per abilitare il targeting dei contenuti. (Vedi [Sviluppo per contenuti mirati](/help/sites-developing/target.md).)

>[!NOTE]
>
>Quando esegui il targeting di un componente in AEM author, il componente effettua una serie di chiamate lato server ad Adobe Target per registrare la campagna, impostare le offerte e recuperare i segmenti Adobe Target (se configurati). Da AEM Publish ad Adobe Target non vengono effettuate chiamate lato server.

## Origini dell&#39;informazione di base {#background-information-sources}

L’integrazione di AEM con Adobe Target richiede la conoscenza di Adobe Target, la gestione delle attività di AEM e la gestione AEM audience. Devi avere familiarità con le seguenti informazioni:

* Adobe Target (consulta [Documentazione di Adobe Target](https://docs.adobe.com/content/help/en/target/using/target-home.html)).
* AEM console Attività (consulta [Gestione delle attività](/help/sites-authoring/activitylib.md)).
* Pubblico AEM (Vedi [Gestione dei tipi di pubblico](/help/sites-authoring/managing-audiences.md)).

>[!NOTE]
>
>Quando si lavora con Adobe Target, il numero massimo di artefatti consentiti in una campagna è il seguente:
>
>* 50 posizioni
>* 2.000 esperienze
>* 50 metriche
>* 50 segmenti di reporting
>

