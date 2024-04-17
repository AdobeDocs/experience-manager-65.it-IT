---
title: Console classica per l’assegnazione di tag dell’interfaccia utente
description: Scopri la console di assegnazione tag dell’interfaccia utente classica di Adobe Experience Manager.
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
docset: aem65
exl-id: 8c6ba22f-5555-4e3c-998a-9353bd44715b
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '887'
ht-degree: 1%

---


# Console classica per l’assegnazione di tag dell’interfaccia utente{#classic-ui-tagging-console}

Questa sezione è per la console di assegnazione tag dell’interfaccia classica.

La console di assegnazione tag dell’interfaccia touch è [qui](/help/sites-administering/tags.md#tagging-console).

Per accedere alla console di assegnazione tag dell’interfaccia classica:

* all’autore
* accedi con privilegi amministrativi
* ad esempio, passa alla console, [https://localhost:4502/tagging](https://localhost:4502/tagging)

![Finestra della console classica](assets/managing_tags_usingthetagasministrationconsole.png)

## Creazione di tag e spazi dei nomi {#creating-tags-and-namespaces}

1. A seconda del livello da cui stai iniziando, puoi creare un tag o uno spazio dei nomi utilizzando **Nuovo**:

   Se si seleziona **Tag** puoi creare uno spazio dei nomi:

   ![Creazione di una finestra di dialogo dello spazio dei nomi](assets/creating_tags_andnamespaces.png)

   Se selezioni uno spazio dei nomi (ad esempio, **Demo**) puoi creare un tag all’interno di tale spazio dei nomi:

   ![Creazione di una finestra di dialogo di tag](assets/creating_tags_andnamespacesinnewnamespace.png)

1. In entrambi i casi immettere:

   * **Titolo**
(*Obbligatorio*) Titolo da visualizzare per il tag. È possibile immettere qualsiasi carattere, ma si consiglia di non utilizzare i seguenti caratteri speciali:

      * `colon (:)` - delimitatore dello spazio dei nomi
      * `forward slash (/)` - delimitatore di tag secondari

     Questi caratteri non vengono visualizzati se vengono immessi.

   * **Nome**
(*Obbligatorio*) Nome del nodo del tag.

   * **Descrizione**
(*Facoltativo*) Descrizione del tag.

   * seleziona **Crea**

## Modifica dei tag {#editing-tags}

1. Nel riquadro di destra selezionare il tag che si desidera modificare.
1. Clic **Modifica**.
1. È possibile modificare **Titolo** e **Descrizione**.
1. Clic **Salva** per chiudere la finestra di dialogo

## Eliminazione dei tag {#deleting-tags}

1. Nel riquadro di destra selezionare il tag che si desidera eliminare.
1. Fai clic su **Elimina**.
1. Clic **Sì** per chiudere la finestra di dialogo

   Il tag non deve più essere elencato.

## Attivazione e disattivazione dei tag {#activating-and-deactivating-tags}

1. Nel riquadro di destra, seleziona lo spazio dei nomi o il tag che desideri attivare (pubblicare) o disattivare (annullare la pubblicazione).
1. Clic **Attiva** o **Disattiva** secondo necessità.

## Elenco: mostra dove si fa riferimento ai tag {#list-showing-where-tags-are-referenced}

**Elenco** apre una nuova finestra che mostra i percorsi di tutte le pagine che utilizzano il tag evidenziato:

![Ricerca di riferimenti ai tag](assets/list_showing_wheretagsarereferenced.png)

## Spostamento dei tag {#moving-tags}

Per aiutare gli amministratori e gli sviluppatori di tag a ripulire la tassonomia o a rinominare un ID tag, è possibile spostare un tag in una nuova posizione:

1. Apri **Assegnazione tag** console.
1. Seleziona il tag e fai clic su **Sposta...** nella barra degli strumenti superiore (o nel menu di scelta rapida).
1. In **Sposta tag** , definisci:

   * **a**, il nodo di destinazione.
   * **Rinomina in**, il nome del nuovo nodo.

1. Clic **Sposta**.

Il **Sposta tag** viene visualizzata come segue:

![Spostamento di un tag](assets/move_tag.png)

>[!NOTE]
>
>Gli autori non devono spostare o rinominare un ID tag. Quando necessario, gli autori devono solo [modificare i titoli dei tag](#editing-tags).

## Unione di tag {#merging-tags}

L’unione di tag può essere utilizzata quando una tassonomia presenta duplicati. Quando il tag A viene unito al tag B, tutte le pagine contrassegnate con il tag A vengono contrassegnate con il tag B e il tag A non è più disponibile per gli autori.

Per unire un tag in un altro:

1. Apri **Assegnazione tag** console.
1. Seleziona il tag e fai clic su **Unisci...** nella barra degli strumenti superiore (o nel menu di scelta rapida).
1. In **Unisci tag** , definisci:

   * **in**, il nodo di destinazione.

1. Clic **Unisci**.

Il **Unisci tag** viene visualizzata come segue:

![Unione di un tag](assets/mergetag.png)

## Conteggio dell’utilizzo dei tag {#counting-usage-of-tags}

Per vedere quante volte un tag viene utilizzato:

1. Apri **Assegnazione tag** console.
1. Clic **Utilizzo conteggio** nella barra degli strumenti superiore: la colonna Conteggio visualizza il risultato.

## Gestione dei tag in lingue diverse {#managing-tags-in-different-languages}

L&#39;opzione `title`di un tag può essere tradotta in più lingue. Tag `titles` può quindi essere visualizzata in base alla lingua utente o alla lingua della pagina.

### Definizione dei titoli di tag in più lingue {#defining-tag-titles-in-multiple-languages}

La procedura seguente illustra come tradurre il `title`del tag **Animali** in inglese, tedesco e francese:

1. Vai a **Assegnazione tag** console.
1. Modifica il tag **Animali** sotto **Tag** > **Foto d&#39;archivio**.
1. Aggiungi le traduzioni nelle seguenti lingue:

   * **Inglese**: Animali
   * **Tedesco**: Tiere
   * **Francese**: Animaux

1. Salva le modifiche.

La finestra di dialogo si presenta come segue:

![Modifica di un tag](assets/edit_tag.png)

La console Assegnazione tag utilizza l’impostazione della lingua utente, quindi per il tag Animal viene visualizzato &quot;Animaux&quot; per un utente che imposta la lingua sul francese nelle proprietà dell’utente.

Per aggiungere una nuova lingua alla finestra di dialogo, consulta la sezione [Aggiunta di una nuova lingua alla finestra di dialogo Modifica tag](/help/sites-developing/building.md#adding-a-new-language-to-the-edit-tag-dialog) nel **Assegnazione di tag per sviluppatori** sezione.

### Visualizzazione dei titoli di tag nelle proprietà della pagina in una lingua specificata {#displaying-tag-titles-in-page-properties-in-a-specified-language}

Per impostazione predefinita, il tag `titles`nella pagina, le proprietà vengono visualizzate nella lingua della pagina. La finestra di dialogo dei tag nelle proprietà della pagina ha un campo lingua che consente la visualizzazione dei tag `titles`in una lingua diversa. La procedura seguente descrive come visualizzare il tag `titles`in francese:

1. Consulta la sezione precedente per aggiungere la traduzione in francese al **Animali** sotto **Tag** > **Foto d&#39;archivio**.
1. Apri le proprietà della pagina di **Prodotti** pagina nel ramo inglese del **Geometrixx** sito.
1. Apri **Tag/Parole chiave** (selezionando il menu a discesa a destra dell&#39;area di visualizzazione Tag/Parole chiave) e selezionare **Francese** lingua dal menu a discesa nell’angolo in basso a destra.
1. Scorri utilizzando le frecce sinistra-destra fino a selezionare **Foto d&#39;archivio** scheda

   Seleziona la **Animali** (**Animaux**) e seleziona all’esterno della finestra di dialogo per chiuderla e aggiungere il tag alle proprietà della pagina.

   ![Modifica di un altro tag](assets/french_tag.png)

Per impostazione predefinita, nella finestra di dialogo Proprietà pagina viene visualizzato il tag `titles`in base alla lingua della pagina.

In generale, la lingua del tag viene presa dalla lingua della pagina se questa è disponibile. Quando [`tag` widget](/help/sites-developing/building.md#tagging-on-the-client-side) viene utilizzato in altri casi, ad esempio nei moduli o nelle finestre di dialogo, il linguaggio dei tag dipende dal contesto.

>[!NOTE]
>
>Il tag cloud e le parole chiave meta nel componente pagina standard utilizzano il tag localizzato `titles`in base alla lingua della pagina, se disponibile.
