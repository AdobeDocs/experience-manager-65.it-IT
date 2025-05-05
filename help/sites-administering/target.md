---
title: Integrazione con Adobe Target
description: Scopri come integrare Adobe Experience Manager con Adobe Target.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 2b17d8cd-a43c-4d54-b990-a6f0cb1db22b
solution: Experience Manager, Experience Manager Sites
feature: Administering,Personalization
role: Admin
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 65%

---

# Integrazione con Adobe Target{#integrating-with-adobe-target}

Come parte di Adobe Marketing Cloud, [Adobe Target](https://www.adobe.com/ro/solutions/testing-targeting/testandtarget.html) consente di aumentare la rilevanza dei contenuti mediante il targeting e la valutazione su tutti i canali. Adobe Target viene utilizzato dagli esperti di marketing per progettare ed eseguire test online, creare all’istante segmenti di pubblico (in base al comportamento) e automatizzare il targeting di contenuti ed esperienze online. L’AEM ha adottato il flusso di lavoro di targeting utilizzato in Adobe Target Standard. Se utilizzi Target, avrai familiarità con l’ambiente di modifica del targeting in AEM.

Integra i tuoi siti di AEM Sites con Adobe Target per personalizzare i contenuti delle tue pagine:

* Implementa il targeting dei contenuti.
* Utilizza il pubblico di Target per creare esperienze personalizzate.
* Invia dati contestuali a Target quando i visitatori interagiscono con le tue pagine.
* Tieni traccia delle percentuali di conversione.

Per eseguire l’integrazione con Target, esegui le seguenti attività:

1. [Esegui attività preliminari](/help/sites-administering/target-requirements.md): registrati ad Adobe Target e configura alcuni aspetti dell’istanza di authoring AEM. Il tuo account Adobe Target deve disporre almeno delle autorizzazioni **livello &#x200B;** approvatore&quot;. Inoltre, devi proteggere le impostazioni dell’attività sul nodo di pubblicazione in modo che sia inaccessibile agli utenti.

1. Effettua una delle seguenti operazioni:

   1. [Consenso ad Adobe Target](/help/sites-administering/opt-in.md): la procedura guidata consenso prende in considerazione le informazioni sull&#39;account Target e crea una configurazione cloud Adobe Target e un framework Target. La procedura guidata associa inoltre i siti al framework di Target. Se la procedura guidata non riesce a connettersi alla destinazione, vedere la sezione [risoluzione dei problemi di connessione](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems). È quindi possibile [Modificare le configurazioni cloud predefinite](/help/sites-administering/target-configuring.md#modifying-the-opt-in-wizard-configurations): se necessario, modificare la configurazione cloud e il framework creati dalla procedura guidata di consenso. Ad esempio, modifica il framework per inviare dati di contesto aggiuntivi a Target. Se desideri utilizzare Adobe Analytics come origine per la generazione di rapporti per Adobe Target, devi modificare la configurazione cloud in modo che punti alla configurazione A4T.
   1. [Integrazione manuale con Adobe Target](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target).

1. [Configurare le attività](/help/sites-authoring/activitylib.md): associa le attività alla configurazione cloud di Target.

>[!NOTE]
>
>Vedi anche [Integrazione dell&#39;AEM con Adobe Target e Adobe Analytics utilizzando DTM](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

>[!NOTE]
>
>Se utilizzi Target con una configurazione proxy personalizzata, devi impostare entrambe le configurazioni proxy del client HTTP, in quanto alcune funzionalità di AEM utilizzano le API 3.x e altre le API 4.x:
>
>* 3.x è configurato con [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x è configurato con [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>

>[!CAUTION]
>
>Proteggere il nodo delle impostazioni delle attività **cq:ActivitySettings** sull’istanza di pubblicazione, in modo che non sia accessibile agli utenti normali. Il nodo delle impostazioni delle attività deve essere accessibile solo al servizio che gestisce la sincronizzazione delle attività con Adobe Target.
>
>Consulta [Prerequisiti per l&#39;integrazione con Adobe Target](/help/sites-administering/target-requirements.md#securing-the-activity-settings-node) per informazioni dettagliate.

Una volta completata l’integrazione, puoi [contenuto mirato dell&#39;autore](/help/sites-authoring/content-targeting-touch.md) che invia i dati dei visitatori ad Adobe Target. I Componenti Pagina richiedono un codice specifico per abilitare il targeting dei contenuti. (Vedi [Sviluppo per contenuti di destinazione](/help/sites-developing/target.md).)

>[!NOTE]
>
>Quando esegui il targeting di un componente in AEM author, il componente effettua una serie di chiamate lato server ad Adobe Target per registrare la campagna, impostare le offerte e recuperare i segmenti Adobe Target (se configurati). Da AEM Publish ad Adobe Target non vengono effettuate chiamate lato server.

## Origini dell&#39;informazione di base {#background-information-sources}

L’integrazione dell’AEM con Adobe Target richiede una conoscenza approfondita di Adobe Target, AEM Activities management e AEM Audiences management. Devi avere familiarità con le seguenti informazioni:

* Adobe Target (consulta [Documentazione di Adobe Target](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=it)).
* Console Attività di AEM (consulta [Gestione delle attività](/help/sites-authoring/activitylib.md)).
* Tipi di pubblico di AEM (consulta [Gestione dei tipi di pubblico](/help/sites-authoring/managing-audiences.md)).

>[!NOTE]
>
>Quando si lavora con Adobe Target, il numero massimo di artefatti consentiti in una campagna è il seguente:
>
>* 50 posizioni
>* 2.000 esperienze
>* 50 metriche
>* 50 segmenti di reporting
>
