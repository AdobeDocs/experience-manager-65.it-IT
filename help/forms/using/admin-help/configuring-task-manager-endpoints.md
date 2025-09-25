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
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
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
