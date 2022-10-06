---
title: Console per assegnazione tag dell’interfaccia classica
seo-title: Classic UI Tagging Console
description: Scopri la console Tagging dell’interfaccia utente classica.
seo-description: Learn about the Classic UI Tagging Console.
uuid: 51e29422-f967-424b-a7fd-4ca2ddc6b8a3
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: b279c033-bc93-4e62-81ad-123c40b9fdd2
docset: aem65
exl-id: 8c6ba22f-5555-4e3c-998a-9353bd44715b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 40%

---

# Console per assegnazione tag dell’interfaccia classica{#classic-ui-tagging-console}

Questa sezione è destinata alla console di assegnazione tag dell’interfaccia classica.

La console di assegnazione tag dell’interfaccia touch è [qui](/help/sites-administering/tags.md#tagging-console).

Per accedere alla console Tag dell’interfaccia classica :

* sull&#39;autore
* accesso con privilegi amministrativi
* ad esempio, passa alla console , [https://localhost:4502/tagging](https://localhost:4502/tagging)

![](assets/managing_tags_usingthetagasministrationconsole.png)

## Creazione di tag e namespace {#creating-tags-and-namespaces}

1. A seconda del livello di partenza, tramite **Nuovo** potete creare un tag o un namespace.

   Se selezionate **Tag**, potete creare un namespace:

   ![](assets/creating_tags_andnamespaces.png)

   Se selezionate un namespace (ad esempio **Demo**), potete creare un tag all’interno di tale namespace:

   ![](assets/creating_tags_andnamespacesinnewnamespace.png)

1. In entrambi i casi, inserisci

   * **Titolo**
(
*Obbligatorio*) Il titolo visualizzato del tag. Mentre è possibile immettere qualsiasi carattere, si consiglia di non utilizzare i seguenti caratteri speciali:

      * `colon (:)` - delimitatore dello spazio dei nomi
      * `forward slash (/)` - delimitatore di tag secondari

      Questi caratteri non verranno visualizzati se immessi.

   * **Nome**
(
*Obbligatorio*) Il nome del nodo del tag.

   * **Descrizione**
(
*Facoltativo*) Una descrizione del tag .

   * select **Crea**


## Modifica dei tag {#editing-tags}

1. Nel riquadro di destra selezionate il tag da modificare.
1. Fate clic su **Modifica**. 
1. Potete modificare il **Titolo** e la **Descrizione**.
1. Fate clic su **Salva** per chiudere la finestra di dialogo.

## Eliminazione dei tag {#deleting-tags}

1. Nel riquadro a destra, seleziona il tag da eliminare.
1. Fai clic su **Elimina**.
1. Fai clic su **Sì** per chiudere la finestra di dialogo.

   Il tag non deve più essere elencato.

## Attivazione e disattivazione dei tag {#activating-and-deactivating-tags}

1. Nel riquadro a destra, seleziona lo spazio dei nomi o il tag da attivare (pubblicare) o disattivare (annullare la pubblicazione).
1. Fare clic su **Attiva** o su **Disattiva**, come necessario.

## Elenco - Indicazione di dove si trovano i riferimenti ai tag {#list-showing-where-tags-are-referenced}

L’opzione **Elenco** consente di aprire una nuova finestra con i percorsi di tutte le pagine che usano il tag evidenziato:

![](assets/list_showing_wheretagsarereferenced.png)

## Spostamento dei tag {#moving-tags}

Per aiutare gli amministratori di tag e gli sviluppatori a ripulire la tassonomia o rinominare un ID tag, è possibile spostare un tag in una nuova posizione :

1. Aprite la console **Tagging**.
1. Selezionate il tag e fate clic su **Sposta** nella barra degli strumenti superiore o nel menu di scelta rapida.
1. Nella finestra di dialogo **Muovi tag** specificate:

   * Il nodo di destinazione nel campo **a**.
   * Il nome del nuovo nodo nel campo **Rinomina in**.

1. Fate clic su **Sposta**.

La finestra di dialogo **Muovi tag** si presenta così:

![](assets/move_tag.png)

>[!NOTE]
>
>Gli autori non devono spostare i tag o rinominarli. Se necessario, gli autori devono [modificare i titoli dei tag](#editing-tags).

## Unione dei tag {#merging-tags}

Se una tassonomia include duplicati, è possibile unire i tag. Se si unisce il tag A al tag B, tutte le pagine contrassegnate con il tag A vengono contrassegnate con il tag B e il tag A non è più disponibile agli autori.

Per unire un tag a un altro:

1. Aprite la console **Tagging**.
1. Selezionate il tag e fate clic su **Unisci** nella barra degli strumenti superiore o nel menu di scelta rapida.
1. Nella finestra di dialogo **Unisci tag** specificate:

   * Il nodo di destinazione nel campo **in**.

1. Fate clic su **Unisci**.

La **Unisci tag** la finestra di dialogo si presenta come segue:

![](assets/mergetag.png)

## Conteggio dell’utilizzo dei tag {#counting-usage-of-tags}

Per verificare quante volte compare un determinato tag:

1. Aprite la console **Tagging**.
1. Fate clic su **Utilizzo conteggio** nella barra degli strumenti superiore. Il risultato viene visualizzato nella colonna Conteggio.

## Gestione dei tag in diverse lingue {#managing-tags-in-different-languages}

L&#39;opzione `title`La proprietà di un tag può essere tradotta in più lingue. Tag `titles` possono quindi essere visualizzati in base alla lingua dell’utente o alla lingua della pagina.

### Definizione dei titoli dei tag in diverse lingue {#defining-tag-titles-in-multiple-languages}

La procedura seguente illustra come tradurre `title`del tag **Animali** in inglese, tedesco e francese:

1. Vai a **Assegnazione tag** console.
1. Modificare il tag **Animali** di seguito **Tag** > **Fotografia Stock**.
1. Aggiungete le traduzioni nelle lingue seguenti:

   * **Inglese**: Animals
   * **Tedesco**: Tiere
   * **Francese**: Animaux

1. Salva le modifiche.

La finestra di dialogo si presenta come segue:

![](assets/edit_tag.png)

La console Tagging utilizza l’impostazione della lingua utente, quindi per il tag Animals viene visualizzato &quot;Animaux&quot; per un utente che imposta la lingua in francese nelle proprietà dell’utente.

Per aggiungere una nuova lingua alla finestra di dialogo, consulta la sezione . [Aggiunta di una nuova lingua alla finestra di dialogo Modifica tag](/help/sites-developing/building.md#adding-a-new-language-to-the-edit-tag-dialog) in **Assegnazione tag per sviluppatori** sezione .

### Visualizzazione dei titoli dei tag nelle proprietà della pagina in una lingua specifica {#displaying-tag-titles-in-page-properties-in-a-specified-language}

Per impostazione predefinita, il tag `titles`nelle proprietà della pagina vengono visualizzate nella lingua della pagina. La finestra di dialogo dei tag nelle proprietà della pagina dispone di un campo della lingua che consente la visualizzazione del tag `titles`in una lingua diversa. La procedura seguente descrive come visualizzare il tag `titles`in francese:

1. Fai riferimento alla sezione precedente per aggiungere la traduzione francese al **Animali** di seguito **Tag** > **Fotografia Stock**.
1. Aprite le proprietà della pagina **Products** nel ramo inglese del sito **Geometrixx**.
1. Apri **Tag/Parole chiave** selezionando il menu a discesa a destra dell’area di visualizzazione Tag/Parole chiave e **Francese** dal menu a discesa nell&#39;angolo in basso a destra.
1. Scorri utilizzando le frecce sinistra-destra fino a selezionare la **Fotografia Stock** scheda

   Seleziona la **Animali** (**Animaux**) e seleziona all’esterno della finestra di dialogo per chiuderla e aggiungere il tag alle proprietà della pagina.

   ![](assets/french_tag.png)

Per impostazione predefinita, nella finestra di dialogo Proprietà pagina viene visualizzato il tag `titles`in base alla lingua della pagina.

In generale, la lingua del tag viene presa dalla lingua della pagina se la lingua della pagina è disponibile. Quando si utilizza il widget [`tag` in altre situazioni (ad esempio nei moduli o nelle finestre di dialogo) la lingua del tag dipende dal contesto.](/help/sites-developing/building.md#tagging-on-the-client-side)

>[!NOTE]
>
>Il tag cloud e le parole chiave meta nel componente pagina standard utilizzano il tag localizzato `titles`in base alla lingua della pagina, se disponibile.
