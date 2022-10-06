---
title: Funzionalità dei flussi di attività
seo-title: Activity Streams Feature
description: Attività di un membro della comunità firmato
seo-description: Activities of a signed-in community member
uuid: decd2d6c-4d4b-4698-a92c-2b5b441458cf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 89f3630f-c01a-4dc0-9ff5-169785f22c01
docset: aem65
exl-id: 2b2a5de0-e7c7-4417-a217-4b929bc7dcfb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 4%

---

# Funzionalità dei flussi di attività {#activity-streams-feature}

## Introduzione {#introduction}

Le attività di un membro della comunità firmato, come il post su un forum o blog, vengono raccolte in un flusso che può essere filtrato e visualizzato in vari modi attraverso la configurazione del `Activity Streams` componente.

La possibilità di seguire aggiunge un altro punto di vista sulle attività quando i membri della comunità seguono posizioni di interesse o seguono le attività di altri membri della comunità.

Il documento descrive:

* Aggiunta del componente Flussi attività a un sito AEM
* Impostazioni di configurazione per il componente Flussi attività

### Aggiunta di flussi di attività a una pagina {#adding-activity-streams-to-a-page}

Se desideri aggiungere un `Activity Streams` componente per una pagina in modalità di creazione, usate il browser componenti per individuare

* `Communities / Activity Streams`

e trascinalo nella posizione di una pagina in cui dovrebbero essere visualizzati i flussi di attività.

Per le informazioni necessarie, visita [Nozioni di base sui componenti di Communities](/help/communities/basics.md).

Quando il [librerie lato client richieste](/help/communities/essentials-activities.md#essentials-for-client-side) sono inclusi, è così che `Activity Streams` apparirà il componente :

![flussi di attività](assets/activity-component.png)

### Configurazione dei flussi di attività {#configuring-activity-streams}

Seleziona il `Activity Streams` per accedere e selezionare il `Configure` che apre la finestra di dialogo di modifica.

![configurare](assets/configure-new.png)

Sotto la **Attività utente** , specifica le attività da visualizzare :

![attività utente](assets/user-activities.png)

* **Numero massimo di attività**

   Il numero di attività da visualizzare

* **Percorso risorsa del flusso**

   Lascia vuoto per impostazione predefinita sul sito community o sul gruppo community. Il percorso della risorsa del flusso identifica l&#39;origine delle attività. Il valore predefinito è vuoto.

* **Visualizza la vista Attività utente**

   Se questa opzione è selezionata, la pagina delle attività includerà una scheda che filtra le attività in base a quelle generate all’interno della community dal membro corrente. Il valore predefinito è selezionato.

* **Visualizza la vista Tutte le attività**

   Se questa opzione è selezionata, la pagina attività includerà una scheda che include tutte le attività generate all’interno della community a cui il membro corrente ha accesso. Il valore predefinito è selezionato.

* **Visualizza la vista Segui**

   Se questa opzione è selezionata, la pagina attività includerà una scheda che filtra le attività in base a quelle che il membro corrente sta seguendo. Il valore predefinito è selezionato.

### Visualizzazione seguente {#following-view}

I componenti devono essere configurati per abilitare quanto segue. Funzioni che consentono quanto segue: [blog](/help/communities/blog-feature.md), [forum](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [calendario](/help/communities/calendar.md), [filelibrio](/help/communities/file-library.md)e [commenti](/help/communities/comments.md).

![visualizzazione a seguire](assets/following-activities.png)

La **Segui** pulsante fornisce un mezzo per seguire le voci come attività, [Notifiche](/help/communities/notifications.md)oppure [abbonamenti](/help/communities/subscriptions.md). Ogni volta che **Segui** è selezionato, è possibile attivare o disattivare una selezione. La `Email Subscriptions` la selezione è presente solo se configurata.

Se è selezionato un metodo di seguito, il testo del pulsante diventa **Seguente**. Per comodità, è possibile selezionare `Unfollow All` per disattivare tutti i metodi.

La **Segui** apparirà il pulsante:

* Visualizzazione del profilo di un altro membro.
* In una pagina con funzioni principali, ad esempio forum, QnA e blog.

   * Segue tutta l’attività per quella funzione generale.

* Per un post specifico, ad esempio un argomento del forum, una domanda QnA o un articolo di blog.

   * Segue tutte le attività per quella voce specifica.

### Informazioni aggiuntive {#additional-information}

Per ulteriori informazioni, consulta [Nozioni di base sui flussi di attività](/help/communities/essentials-activities.md) per sviluppatori.
