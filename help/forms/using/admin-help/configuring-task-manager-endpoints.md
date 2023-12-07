---
title: Configurazione degli endpoint di Task Manager
description: Scopri come configurare gli endpoint di Task Manager per richiamare il servizio. Sono necessarie impostazioni diverse per configurare gli endpoint di Task Manager.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 8495a3d7-6ac9-41f5-b1f9-31decaba118a
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# Configurazione degli endpoint di Task Manager {#configuring-task-manager-endpoints}

Gli endpoint di Task Manager consentono agli utenti di Workspace di richiamare il servizio.

**Impostazioni endpoint di Task Manager**

Utilizzare le impostazioni seguenti per configurare un endpoint di Task Manager.

**Nome:** (Obbligatorio) Identifica l’endpoint. Il nome viene visualizzato nella vista a schede in Workspace. Non includere un carattere &lt; perché il nome visualizzato in Workspace verrà troncato. Se immetti un URL come nome dell’endpoint, accertati che sia conforme alle regole di sintassi specificate in RFC1738.

**Descrizione:** Descrizione dell&#39;endpoint. Non includere un carattere &lt; perché la descrizione visualizzata in Workspace verrà troncata.

**Istruzioni attività:** Istruzioni per l’utente che avvia questo flusso di lavoro.

**Proprietario processo:** Il nome della persona responsabile del processo.

**L’Utente Può Inoltrare L’Attività:** Consente all&#39;utente di inoltrare l&#39;attività iniziale.

**Mostra finestra allegato:** Consente all&#39;utente di visualizzare la finestra dell&#39;allegato.

**Consenti aggiunta allegato:** Consente all&#39;utente di aggiungere allegati e note.

**Attività inizialmente bloccata:** Blocca l&#39;attività iniziale.

**Aggiungi ACL per code condivise:** L&#39;operazione iniziale viene creata con ACL per gli utenti della coda condivisa.

**Categorizzazione:** (Obbligatorio) Categoria in cui l’utente visualizzerà il modulo in Workspace. Selezionare una categoria dall&#39;elenco oppure selezionare Nuova categoria per aggiungere una categoria.

**Nome operazione:** (Obbligatorio) Elenco di operazioni che possono essere assegnate all’endpoint.
