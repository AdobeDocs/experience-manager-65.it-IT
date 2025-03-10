---
title: Moderazione in contesto
description: Scopri come gli amministratori e i membri attendibili della community possono eseguire azioni di moderazione in Adobe Experience Manager Communities.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 47b3c19c-5228-4b72-b78c-7ed71b308921
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---

# Moderazione in contesto {#in-context-moderation}

Per AEM Communities, la moderazione può essere eseguita dagli amministratori e dai membri della community attendibile direttamente sulla pagina pubblicata in cui è stato pubblicato il contenuto della community.

Quando si utilizza una [console di moderazione](moderation.md), le informazioni visualizzate per il contenuto includono un collegamento alla pagina pubblicata per consentire l&#39;accesso alle azioni di moderazione aggiuntive disponibili durante la moderazione nel contesto.

## Azioni di moderazione {#moderation-actions}

Visita la panoramica moderazione per una descrizione di [azioni di moderazione](moderate-ugc.md#moderation-actions).

## Interfaccia utente di moderazione {#moderation-ui}

L&#39;interfaccia utente presentata al moderatore nell&#39;istanza di pubblicazione è contenuta nella finestra di dialogo per la pubblicazione e la gestione dei contenuti generati dagli utenti (UGC, User-Generated Content). Gli elementi dell’interfaccia utente dipendono dallo stato del visitatore del sito, che si tratti o meno di...

1. Membro che ha pubblicato il contenuto.
1. Un moderatore membro attendibile.
1. Un amministratore.
1. Accesso eseguito, ma nessun amministratore, moderatore o autore del contenuto.
1. Accesso non eseguito.

## Esempio {#example}

Utilizzando il sito [Geometrixx Engage](http://localhost:4503/content/sites/engage/en.html) creato durante la [Guida introduttiva ad AEM Communities](getting-started.md), è possibile impostare un thread in un forum su cui eseguire varie attività di moderazione nell&#39;ambiente Publish. Vedi sotto.

Aaron McDonald (`aaron.mcdonald@mailinator.com`) è stato identificato come membro attendibile della community aggiungendolo al gruppo community-engagement-moderators durante la creazione del sito.

Rebekah Larsen (`rebekah.larsen@trashymail.com`) può essere aggiunto come membro del gruppo community-engagement-members utilizzando la console [Members](members.md).

Per ulteriori informazioni sui gruppi di utenti della community, visita [Gestione di utenti e gruppi di utenti](users.md).

### Creare i post del forum {#create-the-forum-posts}

* Accedi come Rebekah Larsen (rebekah.larsen@trashymail.com)

   * Seleziona forum
   * Seleziona nuovo Post
   * Inserisci l’oggetto

     Quando cambiare il nettare in Alimentazione Uccelli Humming

   * Inserisci il corpo del testo

     Non ho avuto molto successo quando appendo un mangiatore di colibrì ogni anno. Sembra che arrivino un giorno o due, allora è tutto. Lo cambio una volta alla settimana è troppo lungo? Devo cambiarla prima?

   * Seleziona Post
   * Seleziona disconnessione

* Accedi come Aaron McDonald (aaron.mcdonald@mailinator.com)

   * Seleziona forum
   * Per l&#39;argomento Hummingbird, selezionare Ulteriori informazioni
   * Inserisci il commento per la risposta Post

     Cambio il mio una volta alla settimana e lo prendo da maggio a ottobre.

   * Seleziona risposta
   * Seleziona disconnessione

* Accedi come Andrew Schaeffer (andrew.schaeffer@trashymail.com)

   * Seleziona forum
   * Per l&#39;argomento Hummingbird, selezionare Ulteriori informazioni
   * Inserisci il commento per la risposta Post

     Vendo nettare e alimentatori - visita https://my.viral.url/

   * Seleziona risposta
   * Seleziona disconnessione

### Visitatore sito anonimo (#5) {#anonymous-site-visitor}

Di seguito è riportata una visualizzazione del forum visualizzata da un visitatore del sito che non ha effettuato l’accesso (5).

Un visitatore anonimo del sito può solo visualizzare il forum, ma non può pubblicare contenuti né eseguire azioni di moderazione.

![community-forum-visitor](assets/community-forum-visitor.png)

### Nuovo membro (#4) {#new-member}

All&#39;autore, accedi come amministratore e aggiungi Boyd Larsen (boyd.larsen@dodgit.com) come nuovo membro del gruppo community-engagement-members utilizzando la [console Members](members.md), quindi Esci.

Al momento della pubblicazione, accedi come Boyd Larsen e accedi al thread selezionando `Forum`, quindi `Read more` per il post su colibrì.

Avviso:

* Boyd non ha partecipato al forum.
* Boyd non può eliminare nulla.
* Boyd ha effettuato l&#39;accesso e può rispondere o contrassegnare il contenuto.

Chiedi a Boyd di selezionare Flag per segnalare il contenuto pubblicato da Andrew.

Disconnetti

![membro forum della community](assets/community-forum-member.png)

### Amministratore (#3) {#administrator}

Accedi come amministratore (admin) e accedi al thread selezionando Forum e quindi Leggi tutto per un post.

Avviso:

* L&#39;amministratore può contrassegnare, eliminare, modificare, negare, tagliare, chiudere, fissare, feature.
* L&#39;amministratore può selezionare Amministrazione per accedere alla console di moderazione.

![community-admin-forum](assets/community-admin-forum.png)

Selezionare la voce di menu Amministrazione per accedere alla [console di moderazione](moderation.md) dall&#39;ambiente Publish.

Tieni presente che, per un amministratore, tutto il contenuto moderabile è visibile, non solo il contenuto del sito della community Geometrixx Engage.

Il filtro di ricerca è un pannello laterale che consente di aprire o chiudere alternativamente.

Disconnetti.

![moderazione-console-publish](assets/moderation-console-publish.png)

### Moderatore community (#2) {#community-moderator}

Accedi come Aaron McDonald (`aaron.mcdonal@mailinator.com`), moderatore della community, quindi accedi al thread selezionando Forum e Leggi altro per il post su Hummingbird.

Avviso:

* Aaron può Rispondere, Eliminare, Modificare o Negare il proprio post.
* Aaron può anche Contrassegnare/Consentire, Rispondere, Eliminare, Modificare, Negare altri contenuti.
* Aaron può tagliare l&#39;argomento del forum per spostarlo in un altro forum per cui modera.
* Aaron può selezionare Amministrazione per accedere alla console di moderazione.

![community-forum-moderator](assets/community-forum-moderator.png)

Selezionare la voce di menu Amministrazione per accedere alla [console di moderazione](moderation.md) dall&#39;ambiente Publish.

Tieni presente che, per un moderatore della community, è visibile solo il contenuto moderabile del sito community di Geometrixx Engage.

Il moderatore della community dispone delle stesse opzioni dell’amministratore (l’immagine mostra la barra laterale di ricerca chiusa), ma non ha accesso ad altre console AEM.

Disconnetti.

![accesso moderatore](assets/moderator-access.png)

### Autore di contenuti (#1) {#content-author}

Accedere come Rebekah Larsen (`rebekah.larsen@mailinator.com`), un membro della comunità che ha avviato il thread e accedere al thread selezionando Forum e quindi Ulteriori informazioni per il post Hummingbird.

Avviso:

* Rebekah può cancellare o modificare il proprio post.
* Rebekah può anche Rispondere o Contrassegnare altri contenuti.
* Impossibile accedere alla console di moderazione.

![community-forum-author](assets/community-forum-author.png)
