---
title: Authoring di gruppi nidificati
description: Scopri come creare gruppi nidificati per un sito di Adobe Experience Manager Communities.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: 55803b7a-9064-4392-9cc2-9f113fa8dc29
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 1%

---

# Authoring di gruppi nidificati{#authoring-nested-groups}

## Creazione di gruppi durante la creazione {#creating-groups-on-author}

Nell’istanza Autore AEM, dalla navigazione globale:

* Seleziona **[!UICONTROL Community]** > **[!UICONTROL Siti]**.
* Seleziona **[!UICONTROL coinvolgi cartella]** per aprirla.
* Seleziona la scheda per il **[!UICONTROL tutorial introduttivo]** sito in inglese.

   * Selezionare l&#39;immagine della scheda.
   * *non* selezionare un&#39;icona.

Il risultato è quello di raggiungere la [console Gruppi](/help/communities/groups.md):

![crea-gruppo](assets/create-group.png)

La funzione gruppi viene visualizzata come una cartella in cui vengono create le istanze dei gruppi. Per aprirla, seleziona la cartella Gruppi. Il gruppo creato su Publish è visibile.

![create-new-group](assets/create-new-group.png)

## Crea gruppo principale di arti {#create-main-arts-group}

Questo gruppo può essere creato perché la struttura del sito per il coinvolgimento include la funzione di un gruppo. Per impostazione predefinita, la configurazione della funzione in `Reference Template` del sito consente la selezione di qualsiasi modello di gruppo abilitato. Pertanto, il modello scelto per questo nuovo gruppo è `Reference Group`.

Queste console sono simili alla console Siti di Communities.

* Seleziona **[!UICONTROL Crea gruppo]**

* **Modello per gruppo community**:

   * **[!UICONTROL Titolo gruppo community]**: arti
   * **[!UICONTROL Descrizione gruppo community]**: un gruppo padre per vari gruppi artistici
   * **[!UICONTROL Directory principale gruppo community]**: *lascia come predefinito*
   * **[!UICONTROL Lingue aggiuntive gruppo community disponibili]**: utilizzare il menu a discesa per selezionare le lingue disponibili per il gruppo community. Il menu visualizza tutte le lingue in cui viene creato il sito community principale. Gli utenti possono scegliere tra queste lingue per creare gruppi in più lingue in questo singolo passaggio. Lo stesso gruppo viene creato in più lingue specificate nella console Gruppi dei rispettivi siti community.
   * **[!UICONTROL Nome gruppo community]**: arts
   * **[!UICONTROL Modello]**: elenco a discesa per selezionare `Reference Group`
   * Seleziona **[!UICONTROL Avanti]**

![Gruppi community nidificati](assets/parent-to-nestedgroup.png)

Continua a scorrere gli altri pannelli con queste impostazioni:

* **[!UICONTROL Design]**

   * Modifica la progettazione o consenti la progettazione del sito padre predefinito.
   * Seleziona **[!UICONTROL Avanti]**.

* **[!UICONTROL Impostazioni]**

   * **[!UICONTROL Moderazione]**

      * Lascia vuoto (eredita dal sito padre).

   * **[!UICONTROL Appartenenza]**

      * Usa `Optional Membership.` predefinito

      * **[!UICONTROL Miniatura]**
         * `optional.*`

      * **[!UICONTROL Seleziona Successivo]**.

* Seleziona **[!UICONTROL Crea]**.

### Nidificazione di gruppi all&#39;interno di Arts Group {#nesting-groups-within-arts-group}

La cartella `groups` contiene ora due gruppi (aggiorna la pagina).

![Nidificazione dei gruppi](assets/create-community-group.png)

#### Gruppo Publish {#publish-group}

Prima di creare i gruppi nidificati nel gruppo `arts`, passa il cursore del mouse sulla scheda `arts` e seleziona l&#39;icona Pubblica per pubblicarla.

![sito di pubblicazione](assets/publish-site.png)

Attendi la conferma della pubblicazione del gruppo.

![gruppo-pubblicato](assets/group-published.png)

Il gruppo `arts` deve contenere anche una cartella `groups`, ma vuota e in cui è possibile creare nuovi gruppi. Passare alla cartella dei gruppi di arti e creare tre gruppi nidificati, ciascuno con un&#39;impostazione di appartenenza diversa:

1. **[!UICONTROL Visivo]**

   * Titolo: `Visual Arts`
   * Nome: `visual`
   * Modello: `Reference Group`
   * Appartenenza: selezionare `Optional Membership`, un gruppo pubblico, aperto a tutti i membri.

1. **[!UICONTROL Uditivo]**

   * Titolo: `Auditory Arts`
   * Nome: `auditory`
   * Modello: `Reference Group`
   * Appartenenza: selezionare `Required Membership`, un gruppo aperto, disponibile per l&#39;aggiunta dei membri.

1. **[!UICONTROL Cronologia]**

   * Titolo: `Art History`
   * Nome: `history`
   * Modello: `Reference Group`
   * Appartenenza: selezionare `Restricted Membership`, un gruppo segreto, visibile solo ai membri invitati. Ad esempio, invita [utente demo](/help/communities/tutorials.md#demo-users) `emily.andrews@mailinator.com`.

Aggiorna la pagina in modo da visualizzare tutti e tre i gruppi nidificati (sottocomunità).

Per passare ai gruppi nidificati dalla console Siti community:

* Seleziona la **[!UICONTROL cartella di coinvolgimento]**
* Seleziona **[!UICONTROL Scheda tutorial introduttivo]**
* Seleziona la cartella **[!UICONTROL Groups]**
* Seleziona **[!UICONTROL scheda arti]**
* Seleziona la cartella **[!UICONTROL Groups]**

![create-new-group2](assets/create-new-group2.png)

## Gruppi di pubblicazione {#publishing-groups}

![sito di pubblicazione](assets/publish-site.png)

Dopo la pubblicazione del sito principale della community:

* Publish ogni gruppo singolarmente:

   * In attesa di conferma della pubblicazione del gruppo.

* Prima di pubblicare i gruppi nidificati in, esegui il Publish del gruppo padre:

   * Tutti i gruppi devono essere pubblicati dall’alto verso il basso.

![gruppo-pubblicato](assets/group-published.png)

## Esperienza in Publish {#experience-on-publish}

È possibile provare i diversi gruppi quando si è connessi, ad esempio, con [utenti demo](/help/communities/tutorials.md#demo-users) utilizzati per:

* Membro gruppo artistico/storico: `emily.andrews@mailinator.com/password`
   * Il gruppo ristretto (segreto), arte/storia, è visibile:
   * In grado di visualizzare gruppi opzionali (pubblici).
   * Possibilità di partecipare a gruppi con restrizioni (aperti).

* Gestione gruppi: `aaron.mcdonald@mailinator.com/password`

   * In grado di visualizzare gruppi opzionali (pubblici).
   * Possibilità di partecipare a gruppi con restrizioni (aperti).
   * Impossibile visualizzare i gruppi con restrizioni (segreti).

Accedi alle console [Membri e gruppi](/help/communities/members.md) per aggiungere altri utenti ai vari gruppi di membri che corrispondono ai gruppi della community.
