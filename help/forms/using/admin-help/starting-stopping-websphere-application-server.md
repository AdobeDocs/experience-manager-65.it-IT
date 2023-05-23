---
title: Avvio e arresto dell'Application Server WebSphere
seo-title: Starting and stopping WebSphere Application Server
description: Diverse procedure richiedono l'arresto o l'avvio dell'istanza di WebSphere in cui si desidera distribuire i prodotti AEM forms. Questo documento descrive come avviare e arrestare l'Application Server WebSphere.
seo-description: Several procedures require you to stop or start the instance of WebSphere where you want to deploy AEM forms products. This document describes how to start and stop the WebSphere Application Server.
uuid: e0373197-aa57-4087-933d-92a86840a11a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: bcd16691-67ab-4694-9e6b-c9d3e0c7bf0b
exl-id: 1a4e8f20-0644-4c96-9f52-f7a59521eac9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# Avvio e arresto dell&#39;Application Server WebSphere {#starting-and-stopping-websphere-application-server}

Diverse procedure richiedono l&#39;arresto o l&#39;avvio dell&#39;istanza di WebSphere in cui si desidera distribuire i prodotti AEM forms. Se non si è certi che il server applicazioni sia stato avviato, è innanzitutto possibile visualizzare lo stato dell&#39;Application Server WebSphere.

## Visualizzare lo stato dell&#39;Application Server WebSphere {#view-the-status-of-websphere-application-server}

1. Da un prompt dei comandi, passare al `[appserver root]/bin` directory.
1. Immetti il comando seguente, sostituendo *nome_server* con il nome dell&#39;Application Server WebSphere:

   * (Windows) `serverStatus.bat`*nome_server*
   * (Linux, UNIX)./ `serverStatus.sh`*nome_server*

## Avvia Application Server WebSphere {#start-websphere-application-server}

1. Da un prompt dei comandi, passare al `[appserver root]/bin` directory.
1. Immetti il comando seguente, sostituendo *nome_server* con il nome dell&#39;Application Server WebSphere:

   * (Windows) `startServer.bat`*nome_server*
   * (Linux, UNIX)./ `startServer.sh`*nome_server*

## Arresta server applicazioni WebSphere {#stop-websphere-application-server}

1. Da un prompt dei comandi, passare al `[appserver root]/bin` directory.
1. Immetti il comando seguente, sostituendo *nome_server* con il nome dell&#39;Application Server WebSphere:

   * (Windows) `stopServer.bat`*nome_server*
   * (Linux, UNIX)./ `stopServer.sh`*nome_server*
