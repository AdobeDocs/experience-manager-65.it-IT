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
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '180'
ht-degree: 100%

---

# Avviare e interrompere il server applicazioni WebSphere {#starting-and-stopping-websphere-application-server}

Varie procedure richiedono l’interruzione o l’avvio dell’istanza di WebSphere in cui vuoi distribuire i prodotti AEM Forms. Se non hai la certezza che il server applicazioni sia stato avviato, puoi innanzitutto visualizzare lo stato del server applicazioni WebSphere.

## Visualizzare lo stato del server applicazioni WebSphere {#view-the-status-of-websphere-application-server}

1. Dal prompt dei comandi passa alla directory `[appserver root]/bin`.
1. Immetti il comando seguente, sostituendo *nome_server* con il nome del server applicazioni WebSphere:

   * (Windows) `serverStatus.bat`*nome_server*
   * (Linux, UNIX)./ `serverStatus.sh`*nome_server*

## Avviare il server applicazioni WebSphere {#start-websphere-application-server}

1. Dal prompt dei comandi passa alla directory `[appserver root]/bin`.
1. Immetti il comando seguente, sostituendo *nome_server* con il nome del server applicazioni WebSphere:

   * (Windows) `startServer.bat`*nome_server*
   * (Linux, UNIX)./ `startServer.sh`*nome_server*

## Arrestare il server applicazioni WebSphere {#stop-websphere-application-server}

1. Dal prompt dei comandi passa alla directory `[appserver root]/bin`.
1. Immetti il comando seguente, sostituendo *nome_server* con il nome del server applicazioni WebSphere:

   * (Windows) `stopServer.bat`*nome_server*
   * (Linux, UNIX)./ `stopServer.sh`*nome_server*
