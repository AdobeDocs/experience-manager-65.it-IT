---
title: Creazione di gruppi nidificati
seo-title: Creazione di gruppi nidificati
description: Creazione di gruppi nidificati
seo-description: Creazione di gruppi nidificati
uuid: b377dc1b-bbb6-41c9-b0fc-8281e1410685
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 752235d2-21ac-46d2-82ed-5fec09c645e9
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Creazione di gruppi nidificati{#authoring-nested-groups}

## Creazione di gruppi sull&#39;autore {#creating-groups-on-author}

Nell&#39;istanza di AEM Author, dalla navigazione globale:

* Selezionare** Community, Siti.**
* Selezionate **la cartella** di coinvolgimento per aprirla.
* Selezionate la scheda per il sito **Guida introduttiva all&#39;esercitazione** inglese.

   * Selezionate l&#39;immagine della scheda.
   * Non *selezionate* un&#39;icona.

Il risultato è di raggiungere la console [](/help/communities/groups.md)Gruppi:

![chlimage_1-91](assets/chlimage_1-91.png)

La funzione dei gruppi verrà visualizzata come una cartella in cui vengono create le istanze dei gruppi. Selezionate la cartella Gruppi per aprirla. Il gruppo creato al momento della pubblicazione è visibile.

![chlimage_1-92](assets/chlimage_1-92.png)

## Crea gruppo di arti principali {#create-main-arts-group}

Questo gruppo può essere creato perché la struttura del sito per il coinvolgimento include una funzione di gruppi. Per impostazione predefinita, la configurazione della funzione nel sito `Reference Template` consente di selezionare qualsiasi modello di gruppo abilitato. Pertanto, il modello scelto per questo nuovo gruppo è il `Reference Group`.

Queste console sono simili alla console Siti community.

* Selezionate **Crea gruppo.**
* **Modello per gruppo community**:

   * Titolo gruppo community: Arti.
   * Descrizione gruppo community: Un gruppo padre per vari gruppi artistici.
   * Radice gruppo community: *lasciate impostato come predefinito.*
   * Lingue aggiuntive disponibili per il gruppo di community: utilizzate il menu a discesa per selezionare le lingue dei gruppi di community disponibili. Nel menu vengono visualizzate tutte le lingue in cui viene creato il sito community principale. Gli utenti possono selezionare una di queste lingue per creare gruppi in più lingue in questo singolo passaggio. Lo stesso gruppo viene creato in più lingue specificate nella console Gruppi dei rispettivi siti della community.
   * Nome gruppo community: arti.
   * Modello: a discesa per selezionare `Reference Group.`
   * `Select Next.`

![Gruppi di community nidificati](assets/parent-to-nestedgroup.png)

Proseguite attraverso gli altri pannelli con le seguenti impostazioni:

* **Progettazione**

   * Modificate la progettazione o consentite la progettazione predefinita del sito padre.
   * Seleziona **Avanti.**

* **Impostazioni**

   * **Moderazione**

      * lasciate vuoto (ereditate dal sito padre).
   * **Iscrizione**

      * use default `Optional Membership.`
   * **Miniatura**

      * `*optional.*`
   * `Select Next.`




* Seleziona **Crea.**

### Nidificazione di gruppi all&#39;interno del gruppo Arti {#nesting-groups-within-arts-group}

La `groups` cartella ora contiene due gruppi (aggiorna la pagina).

![Nidificazione dei gruppi](assets/create-community-group.png)

#### Pubblica gruppo{#publish-group}

Prima di creare gruppi nidificati all’interno del `arts`gruppo, passate il mouse sulla `arts` scheda e selezionate l’icona Pubblica per pubblicarla.

![chlimage_1-93](assets/chlimage_1-93.png)

Attendete la conferma della pubblicazione del gruppo.

![chlimage_1-94](assets/chlimage_1-94.png)

Il `arts` gruppo deve contenere anche una `groups` cartella, ma vuota e in cui è possibile creare nuovi gruppi. Andate alla cartella del gruppo di arti e create 3 gruppi nidificati, ciascuno con un&#39;impostazione di appartenenza diversa:

1. Visuale

   * Titolo: `Visual Arts`
   * Nome: `visual`
   * Modello: `Reference Group`
   * iscrizione: selezionate `Optional Membership`un gruppo pubblico, aprite a tutti i membri

1. Auditory

   * Titolo: `Auditory Arts`
   * Nome: `auditory`
   * Modello: `Reference Group`
   * iscrizione: selezionate `Required Membership`un gruppo aperto, disponibile per i membri a partecipare

1. Storia

   * Titolo: `Art History`
   * Nome: `history`
   * Modello: `Reference Group`
   * iscrizione: selezionate `Restricted Membership`un gruppo segreto, visibile solo ai membri invitati come esempio, invitate un utente [](/help/communities/tutorials.md#demo-users) demo `emily.andrews@mailinator.com`

Aggiornate la pagina per visualizzare tutti e tre i gruppi nidificati (sottocomunità).

Per accedere ai gruppi nidificati dalla console Siti community:

* seleziona cartella di coinvolgimento
* seleziona scheda Esercitazione iniziale
* seleziona cartella Gruppi
* seleziona scheda grafica
* seleziona cartella Gruppi

![chlimage_1-95](assets/chlimage_1-95.png)

## Pubblicazione di gruppi {#publishing-groups}

![chlimage_1-96](assets/chlimage_1-96.png)

Dopo la pubblicazione del sito della community principale:

* pubblicare ciascun gruppo singolarmente

   * in attesa della conferma della pubblicazione del gruppo

* pubblica gruppo padre prima di pubblicare qualsiasi gruppo nidificato all’interno di

   * tutti i gruppi devono essere pubblicati in modo top-down.

![chlimage_1-97](assets/chlimage_1-97.png)

## Esperienza su Pubblica {#experience-on-publish}

È possibile utilizzare i diversi gruppi al momento dell&#39;accesso, ad esempio con gli utenti [](/help/communities/tutorials.md#demo-users) demo utilizzati per

* Membro del gruppo Art/History: emily.andrews@mailinator.com/password

   * il gruppo limitato (segreto), arti/storia è visibile
   * può visualizzare i gruppi facoltativi (pubblici)
   * può partecipare a gruppi limitati (aperti)

* Manager gruppo: aaron.mcdonald@mailinator.com/password

   * può visualizzare i gruppi facoltativi (pubblici)
   * può partecipare a gruppi limitati (aperti)
   * impossibile visualizzare i gruppi con restrizioni (segreti)

Accedete alle console [Membri e Gruppi della community](/help/communities/members.md) sull’autore per aggiungere altri utenti a vari gruppi di membri che corrispondono ai gruppi della community.

