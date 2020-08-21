---
title: Funzionalità Flussi di attività
seo-title: Funzionalità Flussi di attività
description: Attività di un membro della community che ha effettuato l'accesso
seo-description: Attività di un membro della community che ha effettuato l'accesso
uuid: decd2d6c-4d4b-4698-a92c-2b5b441458cf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 89f3630f-c01a-4dc0-9ff5-169785f22c01
docset: aem65
translation-type: tm+mt
source-git-commit: fcdae5363e7a0070b5d6b76227e5c65efb71bc03
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 4%

---


# Funzionalità Flussi di attività {#activity-streams-feature}

## Introduzione {#introduction}

Le attività di un membro della comunità firmato, come l&#39;invio a un forum o blog, vengono raccolte in un flusso che può essere filtrato e visualizzato in vari modi attraverso la configurazione del `Activity Streams` componente.

La possibilità di seguire aggiunge un&#39;altra visione delle attività quando i membri della comunità seguono i post di interesse o seguono le attività di altri membri della comunità.

Il documento descrive:

* Aggiunta del componente Activity Streams a un sito AEM
* Impostazioni di configurazione per il componente Activity Streams

### Aggiunta di flussi di attività a una pagina {#adding-activity-streams-to-a-page}

Se si desidera aggiungere un `Activity Streams` componente a una pagina in modalità di creazione, utilizzare il browser Componenti per individuare

* `Communities / Activity Streams`

e trascinatelo nella stessa posizione in una pagina in cui dovrebbero essere visualizzati i flussi di attività.

Per le informazioni necessarie, consulta [Community Components Basics](/help/communities/basics.md).

Quando sono incluse le librerie [lato client](/help/communities/essentials-activities.md#essentials-for-client-side) richieste, verrà visualizzato il `Activity Streams` componente:

![activity-streams](assets/activity-component.png)

### Configurazione dei flussi di attività {#configuring-activity-streams}

Selezionate il `Activity Streams` componente inserito a cui accedere e selezionate l’ `Configure` icona che apre la finestra di dialogo di modifica.

![configure](assets/configure-new.png)

Nella scheda Attività **** utente, specificate le attività da visualizzare:

![attività degli utenti](assets/user-activities.png)

* **Numero massimo di attività**

   Numero di attività da visualizzare

* **Percorso risorsa del flusso**

   Lasciate vuoto il campo predefinito per il sito community o il gruppo community. Il percorso della risorsa del flusso identifica l&#39;origine delle attività. Il valore predefinito è vuoto.

* **Visualizza la vista Attività utente**

   Se questa opzione è attivata, la pagina delle attività includerà una scheda che filtra le attività in base a quelle generate all&#39;interno della community dal membro corrente. Il valore predefinito è selezionato.

* **Visualizza la vista Tutte le attività**

   Se questa opzione è attivata, la pagina delle attività includerà una scheda che include tutte le attività generate all&#39;interno della comunità a cui il membro corrente ha accesso. Il valore predefinito è selezionato.

* **Visualizza la vista Segui**

   Se questa opzione è selezionata, la pagina delle attività includerà una scheda che filtra le attività in base a quelle che il membro corrente sta seguendo. Il valore predefinito è selezionato.

### Visualizzazione seguente {#following-view}

I componenti devono essere configurati per abilitare quanto segue. Le funzioni che consentono di seguire sono [blog](/help/communities/blog-feature.md), [forum](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [calendario](/help/communities/calendar.md), [filibreria](/help/communities/file-library.md)[](/help/communities/comments.md), commenti.

![visualizzazione](assets/following-activities.png)

Il pulsante **Segui** consente di seguire le voci come attività, [notifiche](/help/communities/notifications.md)o [iscrizioni](/help/communities/subscriptions.md). Ogni volta che si seleziona il pulsante **Segui** , è possibile attivare o disattivare una selezione. La `Email Subscriptions` selezione è presente solo se configurata.

Se è selezionato un metodo di seguito, il testo del pulsante diventa **Seguente**. Per comodità, è possibile selezionare `Unfollow All` per disattivare tutti i metodi.

Verrà visualizzato il pulsante **Segui** :

* Visualizzando il profilo di un altro membro.
* In una pagina delle funzioni principali, ad esempio forum, QnA e blog.

   * Segue tutta l&#39;attività per quella funzione generale.

* Per un post specifico, ad esempio un argomento del forum, una domanda QnA o un articolo di blog.

   * Segue tutta l&#39;attività per quella voce specifica.

### Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili nella pagina [Activity Streams Essentials](/help/communities/essentials-activities.md) per gli sviluppatori.
