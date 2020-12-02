---
title: Moderazione In-Context
seo-title: Moderazione In-Context
description: Come eseguire azioni di moderatore
seo-description: Come eseguire azioni di moderatore
uuid: 282a8bea-2822-4e5c-b9f4-4d9a5380d895
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ee104f6f-123b-4a6e-9031-849fc1318cc5
translation-type: tm+mt
source-git-commit: 917fceffb58883df83e96f60da4769046a18f3c0
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 1%

---


# Moderazione contestuale {#in-context-moderation}

Per  AEM Communities, la moderazione può essere eseguita dagli amministratori e dai membri della community trusted direttamente sulla pagina pubblicata in cui è stato pubblicato il contenuto della community.

Quando si utilizza una [console di moderazione](moderation.md), le informazioni visualizzate per il contenuto includono un collegamento alla pagina pubblicata per consentire l&#39;accesso ad ulteriori azioni di moderazione disponibili durante la moderazione nel contesto.

## Azioni di moderazione {#moderation-actions}

Per una descrizione delle [azioni di moderazione](moderate-ugc.md#moderation-actions) visita la panoramica della moderazione.

## Interfaccia utente di moderazione {#moderation-ui}

L’interfaccia utente presentata al moderatore nell’istanza di pubblicazione è contenuta nella finestra di dialogo per la pubblicazione e la gestione del contenuto generato dall’utente (UGC). Gli elementi dell’interfaccia utente sono determinati dallo stato del visitatore del sito, a prescindere dal fatto che si tratti...

1. Il membro che ha pubblicato il contenuto.
1. Un moderatore membro affidabile.
1. Un amministratore.
1. Accesso, ma non amministratore, moderatore o autore del contenuto.
1. Accesso non effettuato.

## Esempio {#example}

Utilizzando il sito [Geometrixx Engage](http://localhost:4503/content/sites/engage/en.html) creato quando [Getting Started with  AEM Communities](getting-started.md), è possibile impostare rapidamente un thread in un forum in cui sperimentare varie attività di moderazione nell&#39;ambiente di pubblicazione, come illustrato di seguito.

Aaron McDonald (aaron.mcdonald@mailinator.com) è stato identificato come membro di fiducia della comunità aggiungendo lui al gruppo di moderatori-coinvolti nella comunità durante la creazione del sito.

Rebekah Larsen (rebekah.larsen@trashymail.com) può essere aggiunto come membro del gruppo di membri della comunità utilizzando la [console Membri](members.md).

Per ulteriori informazioni sui gruppi di utenti della community, visita [Gestione di utenti e gruppi di utenti](users.md).

### Creare i post del forum {#create-the-forum-posts}

* Effettuate l&#39;accesso come Rebekah Larsen (rebekah.larsen@trashymail.com)

   * Seleziona forum
   * Seleziona nuovo post
   * Immettere l&#39;oggetto

      Quando cambiare il nettare in Humming Bird Feeder

   * Immettete il testo del corpo

      Non ho avuto molto successo quando appendo un mangime per colibrì ogni anno. Sembra che arrivino un giorno o due allora è tutto. Lo cambio una volta alla settimana è troppo lungo? Devo cambiarla prima?

   * Seleziona post
   * Seleziona uscita

* Accedi come Aaron McDonald (aaron.mcdonald@mailinator.com)

   * Seleziona forum
   * Per l&#39;argomento Hummingbird, selezionate Leggi tutto
   * Inserite il commento per Rispondi al post

      Cambio il mio una volta alla settimana e li ricevo da maggio a ottobre.

   * Seleziona risposta
   * Seleziona uscita

* Accedete come Andrew Schaeffer (andrew.schaeffer@trashymail.com)

   * Seleziona forum
   * Per l&#39;argomento Hummingbird, selezionate Leggi tutto
   * Inserite il commento per Rispondi al post

      Vendo nettare e alimentatori - visitare il sito https://my.viral.url/

   * Seleziona risposta
   * Seleziona uscita

### Visitatore anonimo del sito (#5) {#anonymous-site-visitor}

Di seguito è riportata una visualizzazione del forum visualizzato da un visitatore del sito che non ha effettuato l’accesso (5).

Un visitatore anonimo del sito può solo visualizzare il forum, ma non può pubblicare alcun contenuto né eseguire azioni di moderazione.

![community-forum-visitor](assets/community-forum-visitor.png)

### Nuovo membro (#4) {#new-member}

All&#39;autore, accedete come amministratore e aggiungete Boyd Larsen (boyd.larsen@dodgit.com) come nuovo membro del gruppo di membri della community-interazione tramite la [console Membri](members.md), quindi disconnettetevi.

Al momento della pubblicazione, accedete come Boyd Larsen e accedete al thread selezionando `Forum`, quindi `Read more` per il post di colibrì.

Avviso:

* Boyd non ha partecipato al forum.
* Boyd non può eliminare nulla.
* Boyd è connesso e può rispondere o contrassegnare il contenuto.

Fate clic su Contrassegno corpo per contrassegnare il contenuto pubblicato da Andrew.

Disconnetti

![membro della community-forum](assets/community-forum-member.png)

### Amministratore (#3) {#administrator}

Accedete come amministratore (amministratore) e accedete al thread selezionando Forum, quindi Ulteriori informazioni su un post.

Avviso:

* L’Amministratore può contrassegnare, eliminare, modificare, rifiutare, tagliare, chiudere, fissare, feature.
* L&#39;amministratore può selezionare Amministrazione per accedere alla console di moderazione.

![community-admin-forum](assets/community-admin-forum.png)

Selezionate la voce di menu Amministrazione per accedere alla [console di moderazione](moderation.md) dall&#39;ambiente di pubblicazione.

Tenere presente che, per un amministratore, tutto il contenuto modificabile è visibile, non solo il contenuto del sito della community di Geometrixx Engage.

Il filtro di ricerca è un pannello laterale che attiva o disattiva l’apertura o la chiusura.

Disconnetti.

![moderation-console-publish](assets/moderation-console-publish.png)

### Moderatore community (#2) {#community-moderator}

Accedi come Aaron McDonald (aaron.mcdonal@mailinator.com), un moderatore della comunità, e accedere al thread selezionando Forum, quindi Leggi tutto per il post di colibrì.

Avviso:

* Aaron può rispondere, eliminare, modificare o rifiutare il proprio post.
* Aaron può anche contrassegnare/autorizzare, rispondere, eliminare, modificare, rifiutare altro contenuto.
* Aaron può tagliare l&#39;argomento del forum per spostarlo in un altro forum per il quale modera.
* Aaron può selezionare Amministrazione per accedere alla console di moderazione.

![community-forum-moderator](assets/community-forum-moderator.png)

Selezionate la voce di menu Amministrazione per accedere alla [console di moderazione](moderation.md) dall&#39;ambiente di pubblicazione.

Per un moderatore della community, è visibile solo il contenuto modificabile presente nel sito della community di Geometrixx Engage.

Notate che il moderatore della community dispone delle stesse opzioni dell&#39;amministratore (l&#39;immagine è con la barra laterale di ricerca attivata e disattivata), ma non ha accesso ad altre console AEM.

Disconnetti.

![moderatore-accesso](assets/moderator-access.png)

### Content Author (#1) {#content-author}

Accedete come Rebekah Larsen (rebekah.larsen@mailinator.com), membro della community che ha avviato il thread, e accedete al thread selezionando Forum, quindi Ulteriori informazioni sul post relativo al colibrì.

Avviso:

* Rebekah può eliminare o modificare il proprio post.
* Rebekah può anche rispondere o contrassegnare altri contenuti.
* Rebekah non può accedere alla console di moderazione.

![community-forum-author](assets/community-forum-author.png)

