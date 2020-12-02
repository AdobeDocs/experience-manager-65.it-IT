---
title: Integrazione con Adobe Target
seo-title: Integrazione con Adobe Target
description: Scopri come integrare AEM con  Adobe Target.
seo-description: Scopri come integrare AEM con  Adobe Target.
uuid: b90346e8-9757-4272-a870-bbe5e647303f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 454854f8-6053-406c-888d-f427777bf570
translation-type: tm+mt
source-git-commit: 70b18dbe351901abb333d491dd06a6c1c1c569d6
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 5%

---


# Integrazione con Adobe Target{#integrating-with-adobe-target}

Come parte dell&#39;Adobe Marketing Cloud, [ Adobe Target](http://www.adobe.com/ro/solutions/testing-targeting/testandtarget.html) consente di aumentare la pertinenza dei contenuti attraverso il targeting e la misurazione su tutti i canali.  Adobe Target è utilizzato dagli esperti di marketing per progettare ed eseguire test online, creare segmenti di pubblico pronti (basati sul comportamento) e automatizzare il targeting dei contenuti e delle esperienze online. AEM adottato il flusso di lavoro di targeting utilizzato in  Adobe Target Standard. Se utilizzate Target, avrete familiarità con l&#39;ambiente di modifica del targeting in AEM.

Integra i tuoi siti AEM con  Adobe Target per personalizzare il contenuto delle tue pagine:

* Implementate il targeting dei contenuti.
* Utilizzate le audience di Target per creare esperienze personalizzate.
* Invia dati contestuali a Target quando i visitatori interagiscono con le tue pagine.
* Tenere traccia dei tassi di conversione.

Per effettuare l&#39;integrazione con Target, effettuate le seguenti operazioni:

1. [Eseguire le operazioni](/help/sites-administering/target-requirements.md) preliminari: Effettuate la registrazione con  Adobe Target e configurate alcuni aspetti dell’istanza AEM di creazione. Il tuo account Adobe Target  deve avere autorizzazioni di livello **approver **almeno. Inoltre, è necessario proteggere le impostazioni dell&#39;attività sul nodo di pubblicazione in modo che sia inaccessibile agli utenti.

1. Effettua una delle seguenti operazioni:

   1. [Scegliere  Adobe Target](/help/sites-administering/opt-in.md): La procedura guidata di consenso prende in considerazione le informazioni sull&#39;account Target e crea una configurazione cloud Adobe Target  e un framework di Target. La procedura guidata consente inoltre di associare i siti a Target Framework. Se la procedura guidata non è in grado di connettersi alla destinazione, fare riferimento alla sezione [problemi di connessione durante la ripresa](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems). È quindi possibile [Modificare le configurazioni cloud predefinite](/help/sites-administering/target-configuring.md#modifying-the-opt-in-wizard-configurations): Se necessario, modificate la configurazione e il framework cloud creati dalla procedura guidata di consenso. Ad esempio, modificate il framework per inviare dati di contesto aggiuntivi a Target. Se desiderate utilizzare  Adobe Analytics come origine di reporting per  Adobe Target, dovete modificare la configurazione cloud per puntare alla configurazione A4T.
   1. [Effettuare l&#39;integrazione manuale con  Adobe Target](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target).

1. [Configura attività](/help/sites-authoring/activitylib.md): Associate le attività alla configurazione cloud di Target.

>[!NOTE]
>
>Vedere anche [Integrazione AEM con  Adobe Target e  Adobe Analytics mediante DTM](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

>[!NOTE]
>
>Se utilizzate Target con una configurazione proxy personalizzata, è necessario configurare sia le configurazioni proxy HTTP Client in quanto alcune funzionalità di AEM utilizzano le API 3.x, sia quelle di 4.x:
>
>* 3.x è configurato con [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x è configurato con [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)

>



>[!CAUTION]
>
>È necessario proteggere il nodo delle impostazioni dell&#39;attività **cq:ActivitySettings** nell&#39;istanza di pubblicazione in modo che sia inaccessibile agli utenti normali. Il nodo delle impostazioni delle attività deve essere accessibile solo al servizio che gestisce la sincronizzazione delle attività con Adobe Target.
>
>Per informazioni dettagliate, consultate [Prerequisiti per l&#39;integrazione con  Adobe Target](/help/sites-administering/target-requirements.md#securing-the-activity-settings-node).

Una volta completata l&#39;integrazione, potete [creare contenuto di destinazione](/help/sites-authoring/content-targeting-touch.md) che invia i dati dei visitatori a  Adobe Target. I componenti della pagina richiedono codice specifico per abilitare il targeting dei contenuti. (Vedere [Sviluppo per contenuti mirati](/help/sites-developing/target.md).)

>[!NOTE]
>
>Quando eseguite il targeting di un componente in AEM autore, il componente effettua una serie di chiamate lato server  Adobe Target per registrare la campagna, impostare le offerte e recuperare  segmenti Adobe Target (se configurato). Nessuna chiamata lato server viene effettuata da AEM pubblicazione a  Adobe Target.

## Origini informazioni di base {#background-information-sources}

Per integrare AEM con  Adobe Target è necessario conoscere  Adobe Target, AEM gestione delle attività e AEM gestione dell&#39;audience. È necessario avere familiarità con le seguenti informazioni:

*  Adobe Target (vedere la [ documentazione Adobe Target](https://docs.adobe.com/content/help/en/target/using/target-home.html)).
* AEM console Attività (vedere [Gestione delle attività](/help/sites-authoring/activitylib.md)).
* AEM audience (vedere [Gestione dell&#39;audience](/help/sites-authoring/managing-audiences.md)).

>[!NOTE]
>
>Quando lavorate con  Adobe Target, quanto segue indica il numero massimo di artefatti consentiti in una campagna:
>
>* 50 località
>* 2.000 esperienze
>* 50 metriche
>* 50 segmenti di reporting

>



