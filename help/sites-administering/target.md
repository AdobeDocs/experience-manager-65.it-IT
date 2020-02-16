---
title: Integrazione con Adobe Target
seo-title: Integrazione con Adobe Target
description: Scopri come integrare AEM con Adobe Target.
seo-description: Scopri come integrare AEM con Adobe Target.
uuid: b90346e8-9757-4272-a870-bbe5e647303f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 454854f8-6053-406c-888d-f427777bf570
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Integrazione con Adobe Target{#integrating-with-adobe-target}

Come parte di Adobe Marketing Cloud, [Adobe Target](http://www.adobe.com/ro/solutions/testing-targeting/testandtarget.html) consente di aumentare la pertinenza dei contenuti attraverso il targeting e la misurazione su tutti i canali. Adobe Target è utilizzato dagli esperti di marketing per progettare ed eseguire test online, creare segmenti di pubblico pronti (basati sul comportamento) e automatizzare il targeting dei contenuti e delle esperienze online. AEM ha adottato il flusso di lavoro di targeting utilizzato in Adobe Target Standard. Se utilizzi Target, acquisisci familiarità con l’ambiente di modifica del targeting in AEM.

Integra i tuoi siti AEM con Adobe Target per personalizzare il contenuto delle tue pagine:

* Implementate il targeting dei contenuti.
* Utilizzate le audience di Target per creare esperienze personalizzate.
* Invia dati contestuali a Target quando i visitatori interagiscono con le tue pagine.
* Tenere traccia dei tassi di conversione.

Per effettuare l&#39;integrazione con Target, effettuate le seguenti operazioni:

1. [Eseguire le operazioni](/help/sites-administering/target-requirements.md)preliminari: Effettuate la registrazione con Adobe Target e configurate alcuni aspetti dell’istanza di creazione di AEM. L&#39;account Adobe Target deve disporre di autorizzazioni di livello **approver **almeno. Inoltre, è necessario proteggere le impostazioni dell&#39;attività sul nodo di pubblicazione in modo che sia inaccessibile agli utenti.

1. Effettua una delle seguenti operazioni:

   1. [Scegli Adobe Target](/help/sites-administering/opt-in.md): La procedura guidata di consenso prende in considerazione le informazioni sull&#39;account Target e crea una configurazione cloud Adobe Target e un framework di Target. La procedura guidata consente inoltre di associare i siti a Target Framework. Se la procedura guidata non è in grado di connettersi alla destinazione, fare riferimento alla sezione relativa ai problemi di [connessione durante la ripresa](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems) . Potete quindi [modificare le configurazioni](/help/sites-administering/target-configuring.md#modifying-the-opt-in-wizard-configurations)cloud predefinite: Se necessario, modificate la configurazione e il framework cloud creati dalla procedura guidata di consenso. Ad esempio, modificate il framework per inviare dati di contesto aggiuntivi a Target. Se desiderate utilizzare Adobe Analytics come origine di reporting per Adobe Target, dovete modificare la configurazione cloud per puntare alla configurazione A4T.
   1. [Integrazione manuale con Adobe Target](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target).

1. [Configura attività](/help/sites-authoring/activitylib.md): Associate le attività alla configurazione cloud di Target.

>[!NOTE]
>
>Consultate anche [Integrazione di AEM con Adobe Target e Adobe Analytics tramite DTM](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

>[!NOTE]
>
>Se utilizzate Target con una configurazione proxy personalizzata, dovete configurare sia le configurazioni proxy HTTP Client in quanto alcune funzionalità di AEM utilizzano le API 3.x, sia le API 4.x:
>
>* 3.x è configurato con [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x è configurato con [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>



>[!CAUTION]
>
>You must secure the activity settings node **cq:ActivitySettings** on the publish instance so that it is inaccessible to normal users. Il nodo delle impostazioni delle attività deve essere accessibile solo al servizio che gestisce la sincronizzazione delle attività con Adobe Target.
>
>See [Prerequisites for Integrating with Adobe Target](/help/sites-administering/target-requirements.md#securing-the-activity-settings-node) for detailed information.

Al termine dell&#39;integrazione, potete [creare contenuto](/help/sites-authoring/content-targeting-touch.md) mirato che invia i dati dei visitatori ad Adobe Target. I componenti della pagina richiedono codice specifico per abilitare il targeting dei contenuti. Consultate [Sviluppo per contenuti](/help/sites-developing/target.md)mirati.

>[!NOTE]
>
>Quando eseguite il targeting di un componente in AEM Author, il componente effettua una serie di chiamate server ad Adobe Target per registrare la campagna, impostare le offerte e recuperare i segmenti di Adobe Target (se configurato). Da AEM Publish ad Adobe Target non vengono effettuate chiamate lato server.

## Origini informazioni di base {#background-information-sources}

L&#39;integrazione di AEM con Adobe Target richiede la conoscenza di Adobe Target, la gestione delle attività AEM e la gestione dell&#39;audience AEM. È necessario avere familiarità con le seguenti informazioni:

* Adobe Target (consultate la documentazione [di](https://marketing.adobe.com/resources/help/en_US/target/)Adobe Target).
* Console Attività AEM (consultate [Gestione delle attività](/help/sites-authoring/activitylib.md)).
* AEM Audiences (consultate [Gestione dell&#39;audience](/help/sites-authoring/managing-audiences.md)).

>[!NOTE]
>
>Quando lavori con Adobe Target, è indicato il numero massimo di artefatti consentiti in una campagna:
>
>* 50 località
>* 2.000 esperienze
>* 50 metriche
>* 50 segmenti di reporting
>



