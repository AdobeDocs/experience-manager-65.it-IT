---
title: Configurazione degli endpoint di Task Manager
seo-title: Configuring Task Manager endpoints
description: Scopri come configurare gli endpoint di Task Manager.
seo-description: Learn how to configure Task Manager endpoints.
uuid: 07604b10-0bd7-4bce-9624-7ebac4754f56
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9c55feb9-23d8-4798-a3c5-70ec736df3ad
exl-id: 8495a3d7-6ac9-41f5-b1f9-31decaba118a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# Configurazione degli endpoint di Task Manager {#configuring-task-manager-endpoints}

Gli endpoint di Task Manager consentono agli utenti di Workspace di richiamare il servizio.

**Impostazioni endpoint di Task Manager**

Utilizza le seguenti impostazioni per configurare un endpoint di Task Manager.

**Nome:** (Obbligatorio) Identifica l&#39;endpoint. Il nome viene visualizzato nella vista a schede di Workspace. Non includere un carattere &lt; perché troncherà il nome visualizzato in Workspace. Se immetti un URL come nome dell’endpoint, accertati che sia conforme alle regole di sintassi specificate nella RFC1738.

**Descrizione:** Descrizione dell&#39;endpoint. Non includere un carattere &lt; perché troncherà la descrizione visualizzata in Workspace.

**Istruzioni attività:** Istruzioni per l’utente che avvia il flusso di lavoro.

**Proprietario del processo:** Nome della persona responsabile del processo.

**L&#39;Utente Può Inoltrare L&#39;Attività:** Consente all’utente di inoltrare l’attività iniziale.

**Mostra finestra allegato:** Consente all&#39;utente di visualizzare la finestra dell&#39;allegato.

**Consenti aggiunta allegati:** Consente all&#39;utente di aggiungere allegati e note.

**Attività inizialmente bloccata:** Blocca l&#39;attività iniziale.

**Aggiungi ACL per code condivise:** L&#39;attività iniziale viene creata con ACL per gli utenti della coda condivisa.

**Categorizzazione:** (Obbligatorio) La categoria in cui l’utente visualizza il modulo in Workspace. Selezionare una categoria dall’elenco oppure selezionare Nuova categoria per aggiungere una categoria.

**Nome operazione:** (Obbligatorio) Elenco di operazioni che possono essere assegnate al punto finale.
