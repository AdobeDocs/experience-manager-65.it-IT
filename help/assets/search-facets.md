---
title: Facet di ricerca.
description: Come creare, modificare e utilizzare i facet di ricerca in  Adobe Experience Manager.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 8c481c9a5052ff057ae0857c2ac825cec2b26269
workflow-type: tm+mt
source-wordcount: '2515'
ht-degree: 18%

---


# Facet di ricerca {#search-facets}

L’implementazione a livello aziendale di  risorse di Adobe Experience Manager consente di archiviare molte risorse. A volte, trovare la risorsa giusta può essere difficile e richiede molto tempo se si utilizzano solo le funzionalità di ricerca generiche di  Experience Manager.

Usate i facet di ricerca nel pannello Filtri per aggiungere maggiore granularità all’esperienza di ricerca e rendere più efficiente e versatile la funzionalità di ricerca. I facet di ricerca aggiungono più dimensioni (predicati) che consentono di eseguire ricerche più complesse. Il pannello Filtri include alcuni facet standard. Potete inoltre aggiungere facet di ricerca personalizzati.

In sintesi, i facet di ricerca consentono di cercare le risorse in più modi anziché in un unico ordine tassonomico predeterminato. Potete facilmente approfondire fino al livello di dettaglio desiderato per una ricerca più mirata.

Ad esempio, se cercate un’immagine, potete scegliere se un elemento bitmap o un’immagine vettoriale deve essere selezionato. È possibile ridurre ulteriormente l&#39;ambito della ricerca specificando il tipo MIME per l&#39;immagine. Allo stesso modo, quando cercate documenti, potete specificare il formato, ad esempio PDF o MS Word.

## Aggiungere un predicato {#adding-a-predicate}

I facet di ricerca visualizzati nel pannello Filtri sono definiti nel modulo di ricerca sottostante utilizzando i predicati. Per visualizzare più facet o facet diversi, è possibile aggiungere predicati al modulo predefinito oppure utilizzare un modulo personalizzato che includa facet di propria scelta.

Per le ricerche full-text, aggiungere al modulo il predicato [!UICONTROL full-text] . Utilizzate il predicato Proprietà per cercare le risorse che corrispondono a una singola proprietà specificata. Utilizzate il predicato Opzioni per cercare le risorse che corrispondono a uno o più valori per una particolare proprietà. Aggiungi il predicato Intervallo date per cercare le risorse create entro un intervallo di date specificato.

1. Click the Experience Manager logo, and then go to **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL Search Forms]**.
1. From the Search Forms page, select **[!UICONTROL Assets Admin Search Rail]**, then click **[!UICONTROL Edit]** ![edit icon](assets/do-not-localize/aemassets_edit.png).

   ![Individua e seleziona la Barra di ricerca Amministratore risorse](assets/assets_admin_searchrail.png)

   >[!NOTE]
   >
   >Per utilizzare la funzionalità di ricerca delle cartelle dalla barra **di ricerca per l’amministratore delle** risorse preconfigurata, effettua le seguenti operazioni:
   >
   >1. Andate a */conf/global/settings/dam/search/facets/assets/jcr:content/items* in CRXDE.
   >1. Eliminare il nodo **del tipo** .
   >1. Dal percorso */libs/settings/dam/search/facets/assets/jcr:content/items*, copia i nodi **asset, directory, typeor, excludepaths** e **searchtype** nel percorso indicato al passaggio 1.
   >1. Salva le modifiche.


1. In the Edit Search Forms page, drag a predicate from the **[!UICONTROL Select Predicate]** tab to the main pane. Ad esempio, trascinare Predicato **[!UICONTROL proprietà]**.

   ![Premere e spostare un predicato per personalizzare i filtri di ricerca](assets/drag_predicate.png)

   *Figura: Premere e spostare un predicato per personalizzare i filtri di ricerca.*

1. Nella scheda Impostazioni, inserite un&#39;etichetta di campo, un testo segnaposto e una descrizione per il predicato. Specificate un nome valido per la proprietà di metadati che desiderate associare al predicato.

   L&#39;etichetta dell&#39;intestazione nella scheda Impostazioni identifica il tipo di predicato selezionato.

   ![Utilizzate la scheda Impostazioni per fornire le opzioni richieste per un predicato](assets/settings.png)

   Utilizzate la scheda Impostazioni per fornire le opzioni richieste per un predicato

1. Nel campo **[!UICONTROL Nome proprietà]**, specifica un nome valido per la proprietà di metadati che vuoi associare al predicato. È il nome in base al quale viene eseguita la ricerca. Ad esempio, inserisci `jcr:content/metadata/dc:description` o `./jcr:content/metadata/dc:description`.

   È inoltre possibile selezionare un nodo esistente dalla finestra di dialogo di selezione.

   ![Associare una proprietà di metadati a un predicato nel campo Nome proprietà](assets/property_settings.png)

   Associare una proprietà di metadati a un predicato nel campo Nome proprietà

1. Fate clic su **[!UICONTROL Anteprima]** ![anteprima](assets/do-not-localize/preview_icon.png) per generare un’anteprima del pannello Filtri così come appare dopo l’aggiunta del predicato.
1. Esaminate il layout del predicato in modalità Anteprima.

   ![Visualizzare l&#39;anteprima del modulo di ricerca prima di inviare le modifiche](assets/preview-1.png)

   Visualizzare l&#39;anteprima del modulo di ricerca prima di inviare le modifiche

1. Per chiudere l’anteprima, fate clic su **[!UICONTROL Chiudi]** ![chiudi](assets/do-not-localize/close.png) nell’angolo in alto a destra dell’anteprima.
1. Fate clic su **[!UICONTROL Fine]** per salvare le impostazioni.
1. Andate al pannello Ricerca nell’interfaccia utente Risorse. Il predicato Proprietà viene aggiunto al pannello.
1. Immettete una descrizione per la risorsa da cercare nella casella di testo. For example, enter `Adobe`. Quando eseguite una ricerca, nei risultati della ricerca `Adobe` vengono elencate le risorse con la descrizione corrispondente.

## Aggiunta di un predicato Opzioni {#adding-an-options-predicate}

Il predicato Opzioni consente di aggiungere più opzioni di ricerca nel pannello Filtri. Potete selezionare una o più di queste opzioni nel pannello Filtri per cercare le risorse. Ad esempio, per cercare le risorse in base al tipo di file, configurare le opzioni, quali Immagini, Multimedia, Documenti e Archivi, nel modulo di ricerca. Dopo aver configurato queste opzioni, la ricerca viene eseguita sulle risorse di tipo GIF, JPEG, PNG e così via, quando selezionate l’opzione Immagini nel pannello Filtri.

Per mappare le opzioni sulla rispettiva proprietà, create una struttura di nodi per le opzioni e fornite il percorso del nodo principale nella proprietà Nome proprietà del predicato Opzioni. Il nodo padre deve essere di tipo `sling`: `OrderedFolder`. Le opzioni devono essere di tipo `nt:unstructured`. I nodi di opzione devono avere le proprietà `jcr:title` e `value` configurate.

La `jcr:title` proprietà rappresenta un nome semplice per l&#39;opzione visualizzata nel pannello Filtri. Il `value` campo viene utilizzato nella query per corrispondere alla proprietà specificata.

Quando si seleziona un&#39;opzione, la ricerca viene eseguita in base alla `value` proprietà del nodo dell&#39;opzione e degli eventuali nodi secondari. L&#39;intera struttura sotto il nodo dell&#39;opzione viene attraversata e la `value` proprietà di ciascun nodo secondario viene combinata utilizzando un&#39;operazione OR per formare la query di ricerca.

Ad esempio, se selezioni “Immagini” per i tipi di file, la query di ricerca per le risorse viene creata combinando la proprietà `value` utilizzando un’operazione OR. Ad esempio, la query di ricerca per le immagini è realizzata unendo i risultati di corrispondenza per *image/jpeg*, *image/gif*, *image/png*, *image/pjpeg* e *image/tiff* per la proprietà `jcr:content/metadata/dc:format` tramite un’operazione OR.

![La proprietà Value di un tipo di file, come visualizzata in CRXDE, viene utilizzata per il funzionamento delle query di ricerca](assets/filetype-value-property.png)

La proprietà Value di un tipo di file, come visualizzata in CRXDE, viene utilizzata per il funzionamento delle query di ricerca

Invece di creare manualmente una struttura di nodi per le opzioni nell&#39;archivio CRXDE, potete definire le opzioni in un file JSON specificando le coppie chiave-valore corrispondenti. Nel campo **[!UICONTROL Nome proprietà]**, specifica il percorso del file JSON. Ad esempio, puoi definire le coppie chiave-valore, `image/bmp`, `image/gif`, `image/jpeg`, `image/png` e specificarne i valori, come mostrato nel seguente file JSON di esempio. In the **[!UICONTROL Property Name]** field, you can specify the CRXDE path for this file.

```json
{
    "options" :
 [
          {"value" : "image/bmp","text" : "BMP"},
          {"value" : "image/gif","text" : "GIF"},
          {"value" : "image/jpeg","text" : "JPEG"},
          {"value" : "image/png","text" : "PNG"}
 ]
}
```

Se si desidera utilizzare un nodo esistente, specificarlo utilizzando la finestra di dialogo di selezione.

>[!NOTE]
>
>Il predicato Options è un wrapper personalizzato che include i predicati delle proprietà per illustrare il comportamento descritto. Al momento non è disponibile alcun endpoint REST per supportare la funzionalità in modo nativo.

1. Click the Experience Manager logo, and then go to **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL Search Forms]**.
1. From the **[!UICONTROL Search Forms]** page, select **[!UICONTROL Assets Admin Search Rail]**, then click **[!UICONTROL Edit]**.
1. Nella pagina **[!UICONTROL Modifica modulo di ricerca]**, trascina **[!UICONTROL Predicato opzioni]** dalla scheda **[!UICONTROL Seleziona predicato]** al riquadro principale.
1. Nella scheda **[!UICONTROL Impostazioni]**, inserisci un’etichetta e un nome per la proprietà. Ad esempio, per cercare le risorse in base al loro formato, specifica un nome descrittivo per l’etichetta, ad esempio **[!UICONTROL Tipo file]**. Specifica la proprietà in base alla quale eseguire la ricerca nel campo apposito, ad esempio `jcr:content/metadata/dc:format.`
1. Effettua una delle operazioni seguenti:

   * In the **[!UICONTROL Property Name]** field, mention the path of the JSON file where you define the nodes for the options and specify corresponding key-value pairs.
   * Fare clic sul `+` simbolo accanto al campo Opzioni per specificare il testo e il valore di visualizzazione per le opzioni che si desidera fornire nel pannello Filtri. Per aggiungere un’altra opzione, fate clic sul `+` simbolo e ripetete il passaggio.

1. Assicurati che l’opzione **[!UICONTROL Selezione singola]** sia deselezionata per consentire all’utente di scegliere più opzioni per volta per i tipi di file (ad esempio, Immagini, Documenti, Multimedia e Archivi). Se scegli **[!UICONTROL Selezione singola]**, l’utente può scegliere una sola opzione alla volta per i tipi di file.

   ![Campi disponibili nel predicato Opzioni](assets/options_predicate.png)

   Campi disponibili nel predicato Opzioni

1. Nel campo **[!UICONTROL Descrizione]** , immettete una descrizione facoltativa e fate clic su **[!UICONTROL Fine]**.
1. Andate al pannello Ricerca. Il predicato Opzioni viene aggiunto al pannello **Ricerca** . Le opzioni per Tipo **[!UICONTROL di]** file sono visualizzate come caselle di controllo.

## Aggiunta di un predicato di proprietà con più valori {#adding-a-multi-value-property-predicate}

Il predicato Proprietà multivalore consente di cercare risorse per più valori. Considerate uno scenario in cui sono presenti immagini di più prodotti in Risorse e i metadati di ciascuna immagine includono un numero SKU associato al prodotto. Potete usare questo predicato per cercare immagini di prodotto basate su più numeri SKU.

1. Click the Experience Manager logo, and then go to **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL Search Forms]**.
1. Nella pagina Ricerca in Forms, seleziona Barra di ricerca **[!UICONTROL Amministratore]** risorse e fai clic sull’icona **[!UICONTROL Modifica]** ![modifica](assets/do-not-localize/aemassets_edit.png).
1. Nella pagina Modifica modulo di ricerca, trascina il predicato **[!UICONTROL Proprietà con più valori]** dalla scheda **[!UICONTROL Seleziona predicato]** al riquadro principale.
1. In the **[!UICONTROL Settings]** tab, enter a label and placeholder text for the predicate. Specify the property name based on which the search is to be performed in the property field, for example `jcr:content/metadata/dc:value`. È inoltre possibile utilizzare la finestra di dialogo di selezione per selezionare un nodo.
1. Assicurati di aver selezionato **[!UICONTROL Supporto delimitatore]**. Specifica i delimitatori per separare i singoli valori nel campo **[!UICONTROL Delimitatori di input]**. Per impostazione predefinita, la virgola è indicata come delimitatore. È possibile specificare un delimitatore diverso.
1. Nel campo **Descrizione** , immettete una descrizione facoltativa e fate clic su **[!UICONTROL Fine]**.
1. Nell’interfaccia utente Assets, vai al pannello Filtri. Al pannello viene aggiunto il predicato **[!UICONTROL Proprietà con più valori]**.
1. Specificate più valori nel campo Valore multiplo separati dai delimitatori ed eseguite la ricerca. Il predicato recupera una corrispondenza di testo esatta per i valori specificati.

## Aggiunta di un predicato Tag {#adding-a-tags-predicate}

Il predicato Tag consente di eseguire ricerche basate su tag per le risorse. Per impostazione predefinita, Risorse cerca nelle risorse una o più corrispondenze di tag in base ai tag specificati. In altre parole, la query di ricerca esegue un&#39;operazione OR utilizzando i tag specificati. Tuttavia, potete usare l’opzione corrispondenza con tutti i tag per cercare le risorse che includono tutti i tag specificati.

1. Click the Experience Manager logo, and then go to **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL Search Forms]**.
1. From the Search Forms page, select **[!UICONTROL Assets Admin Search Rail]** and then click **[!UICONTROL Edit]** ![edit icon](assets/do-not-localize/aemassets_edit.png).
1. In the Edit Search Form page, drag **[!UICONTROL Tags Predicate]** from the Select Predicate tab to the main pane.
1. Nella scheda Impostazioni, inserite un testo segnaposto per il predicato. Specify the property name based on which the search is to be performed in the property field, for example *jcr:content/metadata/cq:tags*. In alternativa, è possibile selezionare un nodo in CRXDE dalla finestra di dialogo di selezione.
1. Configurate la proprietà del percorso dei tag radice di questo predicate per popolare i vari tag nell&#39;elenco Tag.
1. Seleziona **[!UICONTROL Mostra opzione di corrispondenza con tutti i tag]** per cercare le risorse che includono tutti i tag specificati.

   ![Impostazioni tipiche del predicato Tag](assets/tags_predicate.png)

   Impostazioni tipiche del predicato Tag

1. Nel campo **[!UICONTROL Descrizione]** , immettete una descrizione facoltativa e fate clic su **[!UICONTROL Fine]**.
1. Andate al pannello Ricerca. Il **[!UICONTROL predicato Tag]** viene aggiunto al pannello Ricerca.
1. Specificate i tag in base ai quali desiderate effettuare ricerche nelle risorse o selezionarli dall’elenco dei suggerimenti.

   ![suggerimento fornito dal Experience Manager durante la digitazione del nome del tag](assets/tag-suggestion.png)

   *Figura:  suggerimento fornito dal Experience Manager durante la digitazione del nome del tag.*

1. Select **[!UICONTROL Match all]** to search for matches that include all tags that you specify.

## Aggiungere altri predicati {#adding-other-predicates}

Analogamente al modo in cui aggiungete un predicato Proprietà o un predicato Opzioni, potete aggiungere al pannello di ricerca i seguenti predicati aggiuntivi:

| Nome predicato | Descrizione | Proprietà |
|---|---|---|
| [!UICONTROL Testo completo] | Eseguire un predicato di ricerca per eseguire la ricerca full text su un intero nodo di risorsa. Viene mappato con l&#39;operatore jcr:contains. Potete specificare un percorso relativo se desiderate eseguire una ricerca full text su una parte specifica del nodo della risorsa. | <ul><li>Etichetta</li><li>Segnaposto</li><li>Nome proprietà</li><li>Descrizione</li></ul> |
| [!UICONTROL Browser Percorsi] | Cerca predicato per cercare le risorse in cartelle e sottocartelle in un percorso principale preconfigurato | <ul><li>Segnaposto</li><li>Percorso directory principale</li><li>Descrizione</li></ul> |
| [!UICONTROL Percorso] | Utilizzatelo per filtrare i risultati in base alla posizione. Potete specificare percorsi diversi come opzioni. | <ul><li>Etichetta</li><li>Percorso</li><li>Descrizione</li></ul> |
| [!UICONTROL Stato pubblicazione] | Cercare il predicato per cercare le risorse in base al loro stato di pubblicazione | <ul><li>Etichetta</li><li>Nome proprietà</li><li>Descrizione</li></ul> |
| [!UICONTROL Data relativa] | Consente di cercare le risorse in base alla data relativa della loro creazione. Ad esempio, potete configurare opzioni come 2 mesi fa, 3 settimane fa e così via. | <ul><li>Etichetta</li><li>Nome proprietà</li><li>Data relativa</li></ul> |
| [!UICONTROL Intervallo] | Cercare il predicato per cercare risorse che si trovano all’interno di un intervallo specificato. Nel pannello Ricerca, potete specificare i valori minimo e massimo per l’intervallo. | <ul><li>Etichetta</li><li>Nome proprietà</li><li>Descrizione</li></ul> |
| [!UICONTROL Intervallo date] | Cerca predicato per cercare le risorse create all’interno di un intervallo specificato per una proprietà data. Nel pannello Ricerca, potete specificare le date di inizio e fine utilizzando i selettori data. | <ul><li>Etichetta</li><li>Segnaposto</li><li>Nome proprietà</li><li>Testo intervallo (Da)</li><li>Testo intervallo (A)</li><li>Descrizione</li></ul> |
| [!UICONTROL Data] | Consente di eseguire una ricerca basata sul cursore delle risorse in base a una proprietà data. | <ul><li>Etichetta</li><li>Nome proprietà</li><li>Descrizione</li></ul> |
| [!UICONTROL Dimensione file] | Cercare un predicato per cercare le risorse in base alla loro dimensione. Si tratta di un predicato basato su silder in cui potete selezionare le opzioni del cursore da un nodo configurabile. Le opzioni predefinite sono definite in /libs/dam/options/predicates/filesize nel repository CRXDE. Le dimensioni del file sono espresse in byte. | <ul><li>Etichetta</li><li>Nome proprietà</li><li>Percorso</li><li>Descrizione</li></ul> |
| [!UICONTROL Ultima modifica risorsa] | Predicato di ricerca per cercare le risorse modificate di recente | <ul><li>Nome proprietà</li><li>Valore proprietà</li><li>Descrizione</li></ul> |
| [!UICONTROL Stato pubblicazione] | Cerca predicato per cercare le risorse in base al loro stato di pubblicazione | <ul><li>Etichetta</li><li>Nome proprietà</li><li>Descrizione</li></ul> |
| [!UICONTROL Valutazione] | Cerca predicato per cercare le risorse in base alla loro valutazione media | <ul><li>Etichetta</li><li>Nome proprietà</li><li>Percorso opzione</li><li>Descrizione</li></ul> |
| [!UICONTROL Stato scadenza] | Cerca predicato per cercare le risorse in base al loro stato di scadenza | <ul><li>Etichetta</li><li>Nome proprietà</li><li>Descrizione</li></ul> |
| [!UICONTROL Nascosto] | predicato di ricerca che definisce una proprietà campo nascosta per la ricerca delle risorse | <ul><li>Nome proprietà</li><li>Valore proprietà</li><li>Descrizione</li></ul> |

## Ripristina facet di ricerca {#restoring-default-search-facets}

Per impostazione predefinita, l’icona ![a forma di lucchetto chiuso viene visualizzata](assets/do-not-localize/lock_closed_icon.svg) prima della Barra **[!UICONTROL di ricerca Amministratore]** risorse nella pagina **[!UICONTROL Cerca Forms]** . L’icona Blocca rispetto a un’opzione nella pagina Cerca Forms indica che le impostazioni predefinite sono intatte e non sono personalizzate. Se al modulo si aggiungono facet di ricerca per indicare che il modulo predefinito è stato modificato, l&#39;icona ![Blocca](assets/do-not-localize/lock_closed_icon.svg) chiuso scompare.

![L’icona Blocca rispetto a un’opzione nella pagina Cerca Forms indica che le impostazioni predefinite sono intatte e non sono personalizzate.](assets/locked_admin_rail.png)

Per ripristinare il facet di ricerca predefinito, effettuare le seguenti operazioni:

1. Seleziona Barra di ricerca amministratore **[!UICONTROL risorse]** nella pagina **[!UICONTROL Cerca in Forms]** .
1. Fare clic su **[!UICONTROL Elimina]** ![elimina il contorno](assets/do-not-localize/deleteoutline.png) nella barra degli strumenti.
1. Nella finestra di dialogo di conferma, fate clic su **[!UICONTROL Elimina]** per rimuovere le modifiche personalizzate.

   After you delete the custom changes to search facets, the lock icon ![lock closed icon](assets/do-not-localize/lock_closed_icon.svg) reappears before **[!UICONTROL Assets Admin Search Rail]** in the **[!UICONTROL Search Forms]** page.

## User permissions {#user-permissions}

Se non vi è stato assegnato un ruolo di amministratore, ecco un elenco di autorizzazioni necessarie per eseguire azioni di modifica, eliminazione e anteprima che coinvolgono facet di ricerca.

| Azione | Autorizzazioni  |
| ------------------- | ---------------------------------------------------------------- |
| [!UICONTROL Modifica] | Autorizzazioni di lettura e scrittura sul `/apps` nodo in CRXDE |
| [!UICONTROL Elimina] | Autorizzazioni di lettura, scrittura ed eliminazione sul `/apps` nodo in CRXDE |
| [!UICONTROL Anteprima] | Autorizzazioni di lettura, scrittura ed eliminazione sul `/var/dam/content` nodo in CRXDE. Inoltre, le autorizzazioni di lettura e scrittura sul `/apps` nodo. |

>[!MORELIKETHIS]
>
>* [Estendere la funzionalità di ricerca delle risorse](searchx.md)
>* [Cercare risorse](search-assets.md)

