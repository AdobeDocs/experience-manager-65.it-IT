---
title: Creazione di gruppi nidificati
seo-title: Authoring Nested Groups
description: Creare gruppi nidificati
seo-description: Create nested groups
uuid: b377dc1b-bbb6-41c9-b0fc-8281e1410685
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 752235d2-21ac-46d2-82ed-5fec09c645e9
docset: aem65
exl-id: 55803b7a-9064-4392-9cc2-9f113fa8dc29
source-git-commit: 1074843a0105df39382b64defe66fc262986b9c9
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 5%

---

# Creazione di gruppi nidificati{#authoring-nested-groups}

## Creazione di gruppi sull’autore {#creating-groups-on-author}

Nell’istanza di AEM Author, dalla navigazione globale:

* Seleziona **[!UICONTROL Community]** > **[!UICONTROL Sites]**.
* Seleziona **[!UICONTROL cartella di interazione]** per aprirlo.
* Seleziona la scheda per la **[!UICONTROL Esercitazione introduttiva]** Sito inglese.

   * Seleziona l&#39;immagine della scheda.
   * Do *not* seleziona un’icona.

Il risultato è quello di raggiungere il [Console Gruppi](/help/communities/groups.md):

![create-group](assets/create-group.png)

La funzione gruppi verrà visualizzata come una cartella in cui vengono create le istanze dei gruppi. Selezionare la cartella Groups per aprirla. Il gruppo creato al momento della pubblicazione è visibile.

![create-new-group](assets/create-new-group.png)

## Crea gruppo di arti principali {#create-main-arts-group}

Questo gruppo può essere creato perché la struttura del sito per l&#39;interazione include una funzione di gruppi. Configurazione della funzione nel sito `Reference Template` consente per impostazione predefinita la selezione di qualsiasi modello di gruppo abilitato. Pertanto, il modello scelto per questo nuovo gruppo è il `Reference Group`.

Queste console sono simili alla console Sites di Communities.

* Seleziona **[!UICONTROL Crea gruppo]**

* **Modello per gruppo community**:

   * **[!UICONTROL Titolo gruppo community]**: Arti
   * **[!UICONTROL Descrizione gruppo community]**: Un gruppo di genitori per vari gruppi artistici
   * **[!UICONTROL Radice gruppo community]**: *lascia come predefinito*
   * **[!UICONTROL Lingue disponibili aggiuntive per i gruppi della community]**: utilizza il menu a discesa per selezionare le lingue del gruppo community disponibili. Nel menu vengono visualizzate tutte le lingue in cui viene creato il sito della community principale. In questo singolo passaggio gli utenti possono selezionare una di queste lingue per creare gruppi in più impostazioni internazionali. Lo stesso gruppo viene creato in più lingue specificate nella console Gruppi dei rispettivi siti della community.
   * **[!UICONTROL Nome gruppo community]**: arte
   * **[!UICONTROL Modello]**: menu a discesa per selezionare `Reference Group`
   * Seleziona **[!UICONTROL Avanti]**

![Gruppi community nidificati](assets/parent-to-nestedgroup.png)

Procedi attraverso gli altri pannelli con le seguenti impostazioni:

* **[!UICONTROL Design]**

   * Modificare la progettazione o consentire la progettazione predefinita del sito padre.
   * Seleziona **[!UICONTROL Avanti]**.

* **[!UICONTROL Impostazioni]**

   * **[!UICONTROL Moderazione]**

      * Lascia vuoto (eredita dal sito padre).
   * **[!UICONTROL Iscrizione]**

      * Usa predefinito `Optional Membership.`

      * **[!UICONTROL Miniatura]**
         * `optional.*`
      * **[!UICONTROL Seleziona Avanti]**.



* Seleziona **[!UICONTROL Crea]**.

### Nidificazione di gruppi nel gruppo Arti {#nesting-groups-within-arts-group}

La `groups` La cartella contiene ora due gruppi (aggiorna la pagina).

![Nidificazione dei gruppi](assets/create-community-group.png)

#### Pubblica gruppo {#publish-group}

Prima di creare gruppi nidificati all’interno di `arts` gruppo, passa il puntatore del mouse `arts` e seleziona l’icona pubblica per pubblicarla.

![sito di pubblicazione](assets/publish-site.png)

Attendi la conferma della pubblicazione del gruppo.

![pubblicato in gruppo](assets/group-published.png)

La `arts` il gruppo deve inoltre contenere `groups` ma è vuota e in cui è possibile creare nuovi gruppi. Passa alla cartella del gruppo di arti e crea 3 gruppi nidificati, ciascuno con un&#39;impostazione di appartenenza diversa:

1. **[!UICONTROL Visuale]**

   * Titolo: `Visual Arts`
   * Nome: `visual`
   * Modello: `Reference Group`
   * Iscrizione: select `Optional Membership`, un gruppo pubblico, aperto a tutti i membri.

1. **[!UICONTROL Auditor]**

   * Titolo: `Auditory Arts`
   * Nome: `auditory`
   * Modello: `Reference Group`
   * Iscrizione: select `Required Membership`, un gruppo aperto, disponibile per i membri a cui aderire.

1. **[!UICONTROL Storia]**

   * Titolo: `Art History`
   * Nome: `history`
   * Modello: `Reference Group`
   * Iscrizione: select `Restricted Membership`, un gruppo segreto, visibile solo ai membri invitati. Ad esempio, invita [utente dimostrativo](/help/communities/tutorials.md#demo-users) `emily.andrews@mailinator.com`.

Aggiorna la pagina per visualizzare tutti e tre i gruppi nidificati (sottocommunity).

Per passare ai gruppi nidificati dalla console Sites di Communities:

* Seleziona **[!UICONTROL cartella di interazione]**
* Seleziona **[!UICONTROL Scheda tutorial introduttiva]**
* Seleziona **[!UICONTROL Gruppi]** cartella
* Seleziona **[!UICONTROL carta d&#39;arte]**
* Seleziona **[!UICONTROL Gruppi]** cartella

![create-new-group2](assets/create-new-group2.png)

## Gruppi di pubblicazione {#publishing-groups}

![sito di pubblicazione](assets/publish-site.png)

Dopo aver pubblicato il sito principale della community:

* Pubblica ogni gruppo singolarmente:

   * In attesa di conferma della pubblicazione del gruppo.

* Pubblica il gruppo principale prima di pubblicare eventuali gruppi nidificati all’interno di:

   * Tutti i gruppi devono essere pubblicati in modo top-down.

![pubblicato in gruppo](assets/group-published.png)

## Esperienza su Publish {#experience-on-publish}

È possibile utilizzare i diversi gruppi al momento dell’accesso, ad esempio con [utenti dimostrativi](/help/communities/tutorials.md#demo-users) utilizzato per:

* Membro del gruppo Art/History: emily.andrews@mailinator.com/password
   * Il gruppo ristretto (segreto), arte/storia, è visibile:
   * Può visualizzare gruppi facoltativi (pubblici).
   * Possono partecipare a gruppi ristretti (aperti).

* Gestione dei gruppi: aaron.mcdonald@mailinator.com/password

   * Può visualizzare gruppi facoltativi (pubblici).
   * Possono partecipare a gruppi ristretti (aperti).
   * Impossibile visualizzare i gruppi con restrizioni (segreti).

Accesso alle community [Console Membri e gruppi](/help/communities/members.md) sull&#39;autore per aggiungere altri utenti a vari gruppi di membri che corrispondono ai gruppi della community.
