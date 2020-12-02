---
title: Console per tag dell’interfaccia classica
seo-title: Console per tag dell’interfaccia classica
description: Scopri la console di assegnazione tag dell’interfaccia classica.
seo-description: Scopri la console di assegnazione tag dell’interfaccia classica.
uuid: 51e29422-f967-424b-a7fd-4ca2ddc6b8a3
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: b279c033-bc93-4e62-81ad-123c40b9fdd2
docset: aem65
translation-type: tm+mt
source-git-commit: 684d2d5f73d571a15c8155e7870134c28dc892b7
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 39%

---


# Console per tag dell’interfaccia classica{#classic-ui-tagging-console}

Questa sezione è dedicata alla console di assegnazione tag dell’interfaccia classica.

La console Tagging dell’interfaccia touch è [qui](/help/sites-administering/tags.md#tagging-console).

Per accedere alla console Tag dell’interfaccia classica:

* sull&#39;autore
* accesso con privilegi amministrativi
* passare alla console
ad esempio, [https://localhost:4502/tagging](https://localhost:4502/tagging)

![](assets/managing_tags_usingthetagasministrationconsole.png)

## Creazione di tag e namespace {#creating-tags-and-namespaces}

1. A seconda del livello di partenza, tramite **Nuovo** potete creare un tag o un namespace.

   Se selezionate **Tag**, potete creare un namespace:

   ![](assets/creating_tags_andnamespaces.png)

   Se selezionate un namespace (ad esempio **Demo**), potete creare un tag all’interno di tale namespace:

   ![](assets/creating_tags_andnamespacesinnewnamespace.png)

1. In entrambi i casi, immettere

   * **Titolo**
(
*Obbligatorio*) Titolo visualizzato per il tag . È possibile inserire qualsiasi carattere,
si consiglia di non utilizzare i seguenti caratteri speciali:

      * `colon (:)` - delimitatore dello spazio nomi
      * `forward slash (/)` - delimitatore di tag secondari

      Questi caratteri non verranno visualizzati se immessi.

   * **Nome**
(
*Obbligatorio*) Il nome del nodo per il tag.

   * **Descrizione**
(
*Facoltativo*) Una descrizione del tag.

   * selezionare **Crea**


## Modifica dei tag {#editing-tags}

1. Nel riquadro di destra selezionate il tag da modificare.
1. Fate clic su **Modifica**. 
1. Potete modificare il **Titolo** e la **Descrizione**.
1. Fate clic su **Salva** per chiudere la finestra di dialogo.

## Eliminazione dei tag {#deleting-tags}

1. Nel riquadro a destra, selezionate il tag da eliminare.
1. Fai clic su **Elimina**.
1. Fare clic su **Sì** per chiudere la finestra di dialogo.

   Il tag non deve più essere elencato.

## Attivazione e disattivazione dei tag {#activating-and-deactivating-tags}

1. Nel riquadro a destra, selezionate lo spazio nomi o il tag da attivare (pubblicare) o da disattivare (annullare la pubblicazione).
1. Fare clic su **Attiva** o su **Disattiva**, come necessario.

## Elenco - Indicazione di dove si trovano i riferimenti ai tag  {#list-showing-where-tags-are-referenced}

L’opzione **Elenco** consente di aprire una nuova finestra con i percorsi di tutte le pagine che usano il tag evidenziato:

![](assets/list_showing_wheretagsarereferenced.png)

## Spostamento dei tag {#moving-tags}

Per aiutare amministratori e sviluppatori di tag a ripulire la tassonomia o a rinominare un ID di tag, è possibile spostare un tag in una nuova posizione:

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
>Gli autori non devono spostare i tag o rinominare un ID di tag. Se necessario, gli autori devono modificare solo i titoli dei tag [a1/>.](#editing-tags)

## Unione dei tag {#merging-tags}

Se una tassonomia include duplicati, è possibile unire i tag. Se si unisce il tag A al tag B, tutte le pagine contrassegnate con il tag A vengono contrassegnate con il tag B e il tag A non è più disponibile agli autori.

Per unire un tag a un altro:

1. Aprite la console **Tagging**.
1. Selezionate il tag e fate clic su **Unisci** nella barra degli strumenti superiore o nel menu di scelta rapida.
1. Nella finestra di dialogo **Unisci tag** specificate:

   * Il nodo di destinazione nel campo **in**.

1. Fate clic su **Unisci**.

La finestra di dialogo **Unisci tag** si presenta come segue:

![](assets/mergetag.png)

## Conteggio dell’utilizzo dei tag {#counting-usage-of-tags}

Per verificare quante volte compare un determinato tag:

1. Aprite la console **Tagging**.
1. Fate clic su **Utilizzo conteggio** nella barra degli strumenti superiore. Il risultato viene visualizzato nella colonna Conteggio.

## Gestione dei tag in diverse lingue  {#managing-tags-in-different-languages}

La proprietà opzionale `title`di un tag può essere tradotta in più lingue. Il tag `titles` può quindi essere visualizzato in base alla lingua dell&#39;utente o alla lingua della pagina.

### Definizione dei titoli dei tag in diverse lingue {#defining-tag-titles-in-multiple-languages}

La procedura seguente illustra come tradurre il `title`del tag **Animals** in inglese, tedesco e francese:

1. Passate alla console **Tagging**.
1. Modificate il tag **Animals** sotto **Tags** > **Stock Photography**.
1. Aggiungete le traduzioni nelle lingue seguenti:

   * **Inglese**: Animals
   * **Tedesco**: Tiere
   * **Francese**: Animaux

1. Salva le modifiche.

La finestra di dialogo si presenta come segue:

![](assets/edit_tag.png)

La console Tagging utilizza l’impostazione della lingua utente, pertanto per il tag Animals viene visualizzato &quot;Animaux&quot; per un utente che imposta la lingua francese nelle proprietà dell’utente.

Per aggiungere una nuova lingua alla finestra di dialogo, fare riferimento alla sezione [Aggiunta di una nuova lingua alla finestra di dialogo Modifica tag](/help/sites-developing/building.md#adding-a-new-language-to-the-edit-tag-dialog) nella sezione **Assegnazione tag agli sviluppatori**.

### Visualizzazione dei titoli dei tag in Proprietà pagina in una lingua specifica {#displaying-tag-titles-in-page-properties-in-a-specified-language}

Per impostazione predefinita, il tag `titles`nelle proprietà della pagina viene visualizzato nella lingua della pagina. La finestra di dialogo dei tag nelle proprietà della pagina dispone di un campo della lingua che consente la visualizzazione del tag `titles`in una lingua diversa. La procedura seguente descrive come visualizzare il tag `titles`in francese:

1. Fare riferimento alla sezione precedente per aggiungere la traduzione francese alla **Animals** sotto **Tags** > **Stock Photography**.
1. Aprite le proprietà della pagina **Products** nel ramo inglese del sito **Geometrixx**.
1. Aprire la finestra di dialogo **Tag/Parole chiave** (selezionando il menu a discesa a destra dell&#39;area di visualizzazione Tag/Parole chiave) e selezionare la lingua **Francese** dal menu a discesa nell&#39;angolo in basso a destra.
1. Scorri utilizzando le frecce a sinistra fino a selezionare la scheda **Stock Photography**

   Selezionate il tag **Animals** (**Animaux**) e selezionate all&#39;esterno della finestra di dialogo per chiuderlo e aggiungere il tag alle proprietà della pagina.

   ![](assets/french_tag.png)

Per impostazione predefinita, nella finestra di dialogo Proprietà pagina viene visualizzato il tag `titles`in base alla lingua della pagina.

In generale, la lingua del tag viene presa dalla lingua della pagina, se disponibile. Quando si utilizza il widget [`tag` in altre situazioni (ad esempio nei moduli o nelle finestre di dialogo) la lingua del tag dipende dal contesto.](/help/sites-developing/building.md#tagging-on-the-client-side)

>[!NOTE]
>
>Il tag cloud e le parole chiave meta nel componente di pagina standard utilizzano il tag localizzato `titles`in base alla lingua della pagina, se disponibile.