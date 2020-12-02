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
source-git-commit: 5d196d1f6d5f94f2d3ef0d4461cfe38562f8ba8c
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 5%

---


# Authoring di gruppi nidificati{#authoring-nested-groups}

## Creazione di gruppi sull&#39;autore {#creating-groups-on-author}

Nell&#39;istanza di AEM Author, dalla navigazione globale:

* Selezionare **[!UICONTROL Communities]** > **[!UICONTROL Sites]**.
* Selezionare **[!UICONTROL cartella di coinvolgimento]** per aprirla.
* Selezionate la scheda per il sito **[!UICONTROL Guida introduttiva all&#39;esercitazione]** inglese.

   * Selezionate l&#39;immagine della scheda.
   * *not* selezionare un&#39;icona.

Il risultato è quello di raggiungere la [console Gruppi](/help/communities/groups.md):

![create-group](assets/create-group.png)

La funzione dei gruppi verrà visualizzata come una cartella in cui vengono create le istanze dei gruppi. Selezionate la cartella Gruppi per aprirla. Il gruppo creato al momento della pubblicazione è visibile.

![create-new-group](assets/create-new-group.png)

## Crea gruppo di arti principali {#create-main-arts-group}

Questo gruppo può essere creato perché la struttura del sito per il coinvolgimento include una funzione di gruppi. Per impostazione predefinita, la configurazione della funzione in `Reference Template` del sito consente la selezione di qualsiasi modello di gruppo abilitato. Pertanto, il modello scelto per questo nuovo gruppo è il `Reference Group`.

Queste console sono simili alla console Siti community.

* Selezionare **[!UICONTROL Crea gruppo]**.

* **Modello per gruppo community**:

   * **[!UICONTROL Titolo]** gruppo community: Arti.
   * **[!UICONTROL Descrizione]** gruppo community: Un gruppo padre per vari gruppi artistici.
   * **[!UICONTROL Radice]** gruppo community:  *lasciate come predefinito*.
   * **[!UICONTROL Lingue aggiuntive disponibili per i gruppi]** community: utilizzate il menu a discesa per selezionare le lingue dei gruppi di community disponibili. Nel menu vengono visualizzate tutte le lingue in cui viene creato il sito community principale. Gli utenti possono selezionare una di queste lingue per creare gruppi in più lingue in questo singolo passaggio. Lo stesso gruppo viene creato in più lingue specificate nella console Gruppi dei rispettivi siti della community.
   * **[!UICONTROL Nome]** gruppo community: arti.
   * **[!UICONTROL Modello]**: a discesa per selezionare  `Reference Group.`
   * Seleziona **[!UICONTROL Avanti]**.

![Gruppi di community nidificati](assets/parent-to-nestedgroup.png)

Proseguite attraverso gli altri pannelli con le seguenti impostazioni:

* **[!UICONTROL Progettazione]**

   * Modificate la progettazione o consentite la progettazione predefinita del sito padre.
   * Seleziona **[!UICONTROL Avanti]**.

* **[!UICONTROL Impostazioni]**

   * **[!UICONTROL Moderazione]**

      * Lasciate vuoto (ereditate dal sito padre).
   * **[!UICONTROL Iscrizione]**

      * Usa predefinito `Optional Membership.`

      * **[!UICONTROL Miniatura]**
         * `optional.*`
      * **[!UICONTROL Seleziona Avanti]**.



* Seleziona **[!UICONTROL Crea]**.

### Nidificazione di gruppi nel gruppo Arti {#nesting-groups-within-arts-group}

La cartella `groups` ora contiene due gruppi (aggiorna la pagina).

![Nidificazione dei gruppi](assets/create-community-group.png)

#### Pubblica gruppo{#publish-group}

Prima di creare gruppi nidificati all&#39;interno del gruppo `arts`, passate il puntatore del mouse sulla scheda `arts` e selezionate l&#39;icona di pubblicazione per pubblicarla.

![sito di pubblicazione](assets/publish-site.png)

Attendete la conferma della pubblicazione del gruppo.

![pubblicato in gruppo](assets/group-published.png)

Il gruppo `arts` deve contenere anche una cartella `groups`, ma vuota e in cui è possibile creare nuovi gruppi. Andate alla cartella del gruppo di arti e create 3 gruppi nidificati, ciascuno con un&#39;impostazione di appartenenza diversa:

1. **[!UICONTROL Visuale]**

   * Titolo: `Visual Arts`
   * Nome: `visual`
   * Modello: `Reference Group`
   * Appartenenza: selezionate `Optional Membership`, un gruppo pubblico, aperto a tutti i membri.

1. **[!UICONTROL Auditory]**

   * Titolo: `Auditory Arts`
   * Nome: `auditory`
   * Modello: `Reference Group`
   * Appartenenza: selezionate `Required Membership`, un gruppo aperto, disponibile per i membri a cui partecipare.

1. **[!UICONTROL Storia]**

   * Titolo: `Art History`
   * Nome: `history`
   * Modello: `Reference Group`
   * Appartenenza: selezionate `Restricted Membership`, un gruppo segreto, visibile solo ai membri invitati. Ad esempio, invitare [utente dimostrativo](/help/communities/tutorials.md#demo-users) `emily.andrews@mailinator.com`.

Aggiornate la pagina per visualizzare tutti e tre i gruppi nidificati (sottocomunità).

Per accedere ai gruppi nidificati dalla console Siti community:

* Selezionare **[!UICONTROL cartella di coinvolgimento]**
* Selezionare la **[!UICONTROL Guida introduttiva all&#39;esercitazione]**
* Selezionare la cartella **[!UICONTROL Groups]**
* Selezionare **[!UICONTROL scheda grafica]**
* Selezionare la cartella **[!UICONTROL Groups]**

![create-new-group2](assets/create-new-group2.png)

## Gruppi di pubblicazione {#publishing-groups}

![sito di pubblicazione](assets/publish-site.png)

Dopo la pubblicazione del sito della community principale:

* Pubblicate ciascun gruppo singolarmente:

   * In attesa della conferma della pubblicazione del gruppo.

* Pubblicare il gruppo principale prima di pubblicare qualsiasi gruppo nidificato all’interno di:

   * Tutti i gruppi devono essere pubblicati in modo top-down.

![pubblicato in gruppo](assets/group-published.png)

## Esperienza su Pubblica {#experience-on-publish}

È possibile provare i diversi gruppi al momento dell&#39;accesso, ad esempio con gli utenti [demo](/help/communities/tutorials.md#demo-users) utilizzati per:

* Membro del gruppo Art/History: emily.andrews@mailinator.com/password
   * Il gruppo limitato (segreto), arte/storia, è visibile:
   * Può visualizzare i gruppi facoltativi (pubblici).
   * Può partecipare a gruppi limitati (aperti).

* Manager gruppo: aaron.mcdonald@mailinator.com/password

   * Può visualizzare i gruppi facoltativi (pubblici).
   * Può partecipare a gruppi limitati (aperti).
   * Impossibile visualizzare i gruppi limitati (segreti).

Accedete alle console Community [Membri e gruppi](/help/communities/members.md) sull&#39;autore per aggiungere altri utenti a vari gruppi di membri che corrispondono ai gruppi della community.

