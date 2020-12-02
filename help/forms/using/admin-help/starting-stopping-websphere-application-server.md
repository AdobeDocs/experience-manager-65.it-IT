---
title: Avvio e arresto di WebSphere Application Server
seo-title: Avvio e arresto di WebSphere Application Server
description: Diverse procedure richiedono l'arresto o l'avvio dell'istanza di WebSphere in cui si desidera distribuire i prodotti AEM moduli. Questo documento descrive come avviare e arrestare WebSphere Application Server.
seo-description: Diverse procedure richiedono l'arresto o l'avvio dell'istanza di WebSphere in cui si desidera distribuire i prodotti AEM moduli. Questo documento descrive come avviare e arrestare WebSphere Application Server.
uuid: e0373197-aa57-4087-933d-92a86840a11a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: bcd16691-67ab-4694-9e6b-c9d3e0c7bf0b
translation-type: tm+mt
source-git-commit: 67ea825215d1ca7cc2e350ed1c128c3146de45ec
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---


# Avvio e arresto di WebSphere Application Server {#starting-and-stopping-websphere-application-server}

Diverse procedure richiedono l&#39;arresto o l&#39;avvio dell&#39;istanza di WebSphere in cui si desidera distribuire i prodotti AEM moduli. Se non si è certi che il server applicazioni sia stato avviato, è prima possibile visualizzare lo stato di WebSphere Application Server.

## Visualizzare lo stato di WebSphere Application Server {#view-the-status-of-websphere-application-server}

1. Dal prompt dei comandi, andate alla directory `[appserver root]/bin`.
1. Digitate il comando seguente, sostituendo *server_name* con il nome del server applicazioni WebSphere:

   * (Windows) `serverStatus.bat`*nome_server*
   * (Linux, UNIX) ./ `serverStatus.sh`*nome_server*

## Avvia server applicazioni WebSphere {#start-websphere-application-server}

1. Dal prompt dei comandi, andate alla directory `[appserver root]/bin`.
1. Digitate il comando seguente, sostituendo *server_name* con il nome del server applicazioni WebSphere:

   * (Windows) `startServer.bat`*nome_server*
   * (Linux, UNIX) ./ `startServer.sh`*nome_server*

## Arresta server applicazione WebSphere {#stop-websphere-application-server}

1. Dal prompt dei comandi, andate alla directory `[appserver root]/bin`.
1. Digitate il comando seguente, sostituendo *server_name* con il nome del server applicazioni WebSphere:

   * (Windows) `stopServer.bat`*nome_server*
   * (Linux, UNIX) ./ `stopServer.sh`*nome_server*

