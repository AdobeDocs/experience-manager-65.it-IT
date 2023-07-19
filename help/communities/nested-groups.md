---
title: Authoring di gruppi nidificati
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
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 4%

---

# Authoring di gruppi nidificati{#authoring-nested-groups}

## Creazione di gruppi durante la creazione {#creating-groups-on-author}

Nell’istanza di AEM Author, dalla navigazione globale:

* Seleziona **[!UICONTROL Community]** > **[!UICONTROL Sites]**.
* Seleziona **[!UICONTROL cartella di coinvolgimento]** per aprirlo.
* Seleziona la scheda per il **[!UICONTROL Tutorial introduttivo]** Sito in inglese.

   * Selezionare l&#39;immagine della scheda.
   * Esegui *non* seleziona un’icona.

Il risultato è quello di raggiungere [Console Gruppi](/help/communities/groups.md):

![create-group](assets/create-group.png)

La funzione gruppi viene visualizzata come una cartella in cui vengono create le istanze dei gruppi. Selezionare la cartella Gruppi per aprirla. Il gruppo creato al momento della pubblicazione è visibile.

![create-new-group](assets/create-new-group.png)

## Crea gruppo principale di arti {#create-main-arts-group}

Questo gruppo può essere creato perché la struttura del sito per il coinvolgimento include una funzione di gruppi. La configurazione della funzione nel `Reference Template` consente per impostazione predefinita la selezione di qualsiasi modello di gruppo abilitato. Pertanto, il modello scelto per questo nuovo gruppo è `Reference Group`.

Queste console sono simili alla console Siti di Communities.

* Seleziona **[!UICONTROL Crea gruppo]**

* **Modello per gruppo community**:

   * **[!UICONTROL Titolo gruppo community]**: Arti
   * **[!UICONTROL Descrizione gruppo community]**: gruppo principale per vari gruppi artistici
   * **[!UICONTROL Directory principale gruppo community]**: *lascia come predefinito*
   * **[!UICONTROL Lingue aggiuntive gruppo community disponibili]**: utilizza il menu a discesa per selezionare le lingue del gruppo community disponibili. Il menu visualizza tutte le lingue in cui viene creato il sito community principale. Gli utenti possono scegliere tra queste lingue per creare gruppi in più lingue in questo singolo passaggio. Lo stesso gruppo viene creato in più lingue specificate nella console Gruppi dei rispettivi siti community.
   * **[!UICONTROL Nome gruppo community]**: arti
   * **[!UICONTROL Modello]**: elenco a discesa per selezionare `Reference Group`
   * Seleziona **[!UICONTROL Avanti]**

![Gruppi community nidificati](assets/parent-to-nestedgroup.png)

Continua a scorrere gli altri pannelli con queste impostazioni:

* **[!UICONTROL Design]**

   * Modifica la progettazione o consenti la progettazione predefinita del sito padre.
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

### Nidificazione di gruppi all&#39;interno di Arts Group {#nesting-groups-within-arts-group}

Il `groups` La cartella ora contiene due gruppi (aggiorna la pagina).

![Nidificazione dei gruppi](assets/create-community-group.png)

#### Pubblica gruppo {#publish-group}

Prima di creare i gruppi nidificati all&#39;interno di `arts` gruppo, passa il puntatore del mouse sul `arts` e seleziona l’icona pubblica per pubblicarla.

![publish-site](assets/publish-site.png)

Attendi la conferma della pubblicazione del gruppo.

![pubblicato da gruppo](assets/group-published.png)

Il `arts` il gruppo deve contenere anche `groups` ma è vuota e consente di creare nuovi gruppi. Passare alla cartella dei gruppi di arti e creare 3 gruppi nidificati, ciascuno con un&#39;impostazione di appartenenza diversa:

1. **[!UICONTROL Visivo]**

   * Titolo: `Visual Arts`
   * Nome: `visual`
   * Modello: `Reference Group`
   * Appartenenza: seleziona `Optional Membership`, un gruppo pubblico, aperto a tutti i membri.

1. **[!UICONTROL Uditivo]**

   * Titolo: `Auditory Arts`
   * Nome: `auditory`
   * Modello: `Reference Group`
   * Appartenenza: seleziona `Required Membership`, un gruppo aperto, disponibile per l&#39;aggiunta dei membri.

1. **[!UICONTROL Storia]**

   * Titolo: `Art History`
   * Nome: `history`
   * Modello: `Reference Group`
   * Appartenenza: seleziona `Restricted Membership`, gruppo segreto, visibile solo ai membri invitati. Ad esempio, invita [utente demo](/help/communities/tutorials.md#demo-users) `emily.andrews@mailinator.com`.

Aggiorna la pagina per visualizzare tutti e tre i gruppi nidificati (comunità secondarie).

Per passare ai gruppi nidificati dalla console Siti community:

* Seleziona **[!UICONTROL cartella di coinvolgimento]**
* Seleziona **[!UICONTROL Guida introduttiva Scheda tutorial]**
* Seleziona **[!UICONTROL Gruppi]** cartella
* Seleziona **[!UICONTROL scheda arti]**
* Seleziona **[!UICONTROL Gruppi]** cartella

![create-new-group2](assets/create-new-group2.png)

## Gruppi di pubblicazione {#publishing-groups}

![publish-site](assets/publish-site.png)

Dopo la pubblicazione del sito principale della community:

* Pubblica ogni gruppo singolarmente:

   * In attesa di conferma della pubblicazione del gruppo.

* Pubblica il gruppo principale prima di pubblicare i gruppi nidificati in:

   * Tutti i gruppi devono essere pubblicati dall’alto verso il basso.

![pubblicato da gruppo](assets/group-published.png)

## Esperienza alla pubblicazione {#experience-on-publish}

È possibile avere un’idea dei diversi gruppi una volta effettuato l’accesso, ad esempio con [utenti demo](/help/communities/tutorials.md#demo-users) utilizzato per:

* Membro del gruppo artistico/storico: emily.andrews@mailinator.com/password
   * Il gruppo ristretto (segreto), arte/storia, è visibile:
   * Possono visualizzare gruppi facoltativi (pubblici).
   * Può unirsi a gruppi con restrizioni (aperti).

* Gestione gruppi: aaron.mcdonald@mailinator.com/password

   * Possono visualizzare gruppi facoltativi (pubblici).
   * Può unirsi a gruppi con restrizioni (aperti).
   * Impossibile visualizzare i gruppi con restrizioni (segreti).

Accedere alle community [Console membri e gruppi](/help/communities/members.md) all’autore di aggiungere altri utenti a vari gruppi di membri che corrispondono ai gruppi community.
