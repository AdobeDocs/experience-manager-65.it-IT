---
title: Configurazione endpoint di Gestione attività
description: Scopri come configurare gli endpoint di Gestione attività per richiamare il servizio. Sono necessarie impostazioni diverse per configurare gli endpoint di Gestione attività.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 8495a3d7-6ac9-41f5-b1f9-31decaba118a
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
source-wordcount: '245'
ht-degree: 100%
---
# Configurazione endpoint di Gestione attività {#configuring-task-manager-endpoints}

Gli endpoint di Gestione attività consentono agli utenti dell’area di lavoro di richiamare il servizio.

**Impostazioni endpoint di Gestione attività**

Utilizza le impostazioni seguenti per configurare un endpoint di Gestione attività.

**Nome:** (obbligatorio) identifica l’endpoint. Il nome viene visualizzato nella vista a schede in Workspace. Non includere un carattere &lt; o il nome visualizzato in Workspace verrà troncato. Se immetti un URL come nome dell’endpoint, accertati che sia conforme alle regole di sintassi specificate in RFC1738.

**Descrizione:** una descrizione dell’endpoint. Non includere un carattere &lt; o la descrizione visualizzata in Workspace verrà troncata.

**Istruzioni attività:** le istruzioni per l’utente che avvia il flusso di lavoro.

**Proprietario processo:** il nome dell’utente tipo responsabile del processo.

**L’utente può inoltrare l’attività:** consente all’utente di inoltrare l’attività iniziale.

**Mostra finestra allegato:** consente all’utente di visualizzare la finestra dell’allegato.

**Consenti aggiunta allegato:** consente all’utente di aggiungere allegati e note.

**Attività inizialmente bloccata:** blocca l’attività iniziale.

**Aggiungi ACL per le code condivise:** l’attività iniziale viene creata con ACL per gli utenti della coda condivisa.

**Categorizzazione:** (obbligatoria) la categoria in cui l’utente visualizzerà il modulo in Workspace. Seleziona una categoria dall’elenco oppure seleziona Nuova categoria per aggiungere una categoria.

**Nome operazione:** (obbligatorio) un elenco di operazioni che puoi assegnare all’endpoint.
