---
title: Avviare e interrompere il server applicazioni WebSphere
description: Varie procedure richiedono l’interruzione o l’avvio dell’istanza di WebSphere in cui vuoi distribuire i prodotti AEM Forms. Questo documento descrive come avviare e arrestare il server applicazioni WebSphere.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1a4e8f20-0644-4c96-9f52-f7a59521eac9
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 95%
---
# Avviare e interrompere il server applicazioni WebSphere {#starting-and-stopping-websphere-application-server}

Varie procedure richiedono l’interruzione o l’avvio dell’istanza di WebSphere in cui vuoi distribuire i prodotti AEM Forms. Se non hai la certezza che il server applicazioni sia stato avviato, puoi innanzitutto visualizzare lo stato del server applicazioni WebSphere.

## Visualizzare lo stato del server applicazioni WebSphere {#view-the-status-of-websphere-application-server}

1. Dal prompt dei comandi passa alla directory `[appserver root]/bin`.
1. Immetti il comando seguente, sostituendo *nome_server* con il nome del server applicazioni WebSphere:

   * (Windows) `serverStatus.bat`*nome_server*
   * (Linux, UNIX) ./ `serverStatus.sh`*nome_server*

## Avviare il server applicazioni WebSphere {#start-websphere-application-server}

1. Dal prompt dei comandi passa alla directory `[appserver root]/bin`.
1. Immetti il comando seguente, sostituendo *nome_server* con il nome del server applicazioni WebSphere:

   * (Windows) `startServer.bat`*nome_server*
   * (Linux, UNIX) ./ `startServer.sh`*nome_server*

## Arrestare il server applicazioni WebSphere {#stop-websphere-application-server}

1. Dal prompt dei comandi passa alla directory `[appserver root]/bin`.
1. Immetti il comando seguente, sostituendo *nome_server* con il nome del server applicazioni WebSphere:

   * (Windows) `stopServer.bat`*nome_server*
   * (Linux, UNIX) ./ `stopServer.sh`*nome_server*
