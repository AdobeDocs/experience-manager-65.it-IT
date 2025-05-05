---
title: Facet di ricerca per filtrare i risultati della ricerca
description: Come creare, modificare e utilizzare i facet di ricerca in [!DNL Adobe Experience Manager].
contentOwner: AG
role: Admin, Developer
feature: Search
exl-id: acaf46e6-ff70-4825-8922-ce8f82905a92
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2411'
ht-degree: 15%

---

# Facet di ricerca {#search-facets}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/search-facets.html?lang=it) |
| AEM 6.5 | Questo articolo |

Una distribuzione a livello aziendale di [!DNL Adobe Experience Manager Assets] ha la capacità di archiviare molte risorse. Talvolta, trovare la risorsa giusta può essere difficile e richiedere tempo se si utilizzano solo le funzionalità di ricerca generiche di [!DNL Experience Manager].

Utilizza i facet di ricerca nel pannello Filtri per aggiungere maggiore granularità all’esperienza di ricerca e rendere la funzionalità di ricerca più efficiente e versatile. I facet di ricerca aggiungono più dimensioni (predicati) che consentono di eseguire ricerche più complesse. Il pannello Filtri include alcuni facet standard. Puoi anche aggiungere facet di ricerca personalizzati.

In sintesi, i facet di ricerca consentono di cercare le risorse in più modi anziché in un unico ordine tassonomico predeterminato. Per una ricerca più mirata, è possibile eseguire facilmente un drill-down al livello di dettaglio desiderato.

Ad esempio, se si sta cercando un&#39;immagine, è possibile scegliere se si desidera una bitmap o un&#39;immagine vettoriale. Puoi ridurre ulteriormente l’ambito della ricerca specificando il tipo MIME per l’immagine. Analogamente, durante la ricerca di documenti, è possibile specificare il formato, ad esempio PDF o MS Word.

## Aggiungi un predicato {#adding-a-predicate}

I facet di ricerca visualizzati nel pannello Filtri sono definiti nel modulo di ricerca sottostante utilizzando i predicati. Per visualizzare più facet o facet diversi, è possibile aggiungere predicati al modulo predefinito o utilizzare un modulo personalizzato che includa facet di propria scelta.

Per le ricerche full-text, aggiungi al modulo il predicato **[!UICONTROL Testo completo]**. Utilizza il predicato Proprietà per cercare le risorse che corrispondono a una singola proprietà specificata. Utilizza il predicato Options per cercare le risorse che corrispondono a uno o più valori per una particolare proprietà. Aggiungi il predicato Intervallo date per cercare le risorse create all’interno di un intervallo di date specificato.

1. Fare clic sul logo [!DNL Experience Manager], quindi passare a **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL Cerca in Forms]**.
1. Dalla pagina [!UICONTROL Cerca in Forms], seleziona **[!UICONTROL Barra di ricerca amministrazione Assets]**, quindi fai clic su **[!UICONTROL Modifica]** ![icona di modifica](assets/do-not-localize/aemassets_edit.png).

   >[!NOTE]
   >
   >Per utilizzare la funzionalità di ricerca delle cartelle della barra di ricerca dell&#39;amministratore [!DNL Assets] preconfigurata di una versione precedente, eseguire la procedura seguente:
   >
   >1. Passare a `/conf/global/settings/dam/search/facets/assets/jcr:content/items` in CRXDE.
   >1. Elimina il nodo `type`.
   >1. Dal percorso `/libs/settings/dam/search/facets/assets/jcr:content/items`, copiare i nodi `asset`, `directory`, `typeor`, `excludepaths` e `searchtype` nel percorso indicato nel passaggio 1.
   >1. Salva le modifiche.

1. Nella pagina [!UICONTROL Modifica Forms di ricerca], trascina un predicato dalla scheda **[!UICONTROL Seleziona predicato]** nel riquadro principale. Trascinare ad esempio **[!UICONTROL Predicato proprietà]**.

   ![Selezionare e spostare un predicato per personalizzare i filtri di ricerca](assets/drag_predicate.png)

   *Figura: selezionare e spostare un predicato per personalizzare i filtri di ricerca.*

1. Nella scheda [!UICONTROL Impostazioni] immettere un&#39;etichetta di campo, un testo segnaposto e una descrizione per il predicato. Specificare un nome valido per la proprietà di metadati che si desidera associare al predicato. L&#39;etichetta dell&#39;intestazione nella scheda [!UICONTROL Impostazioni] identifica il tipo di predicato selezionato.

1. Nel campo [!UICONTROL Nome proprietà], specifica un nome valido per la proprietà di metadati che vuoi associare al predicato. È il nome in base al quale viene eseguita la ricerca. Ad esempio, inserisci `jcr:content/metadata/dc:description` o `./jcr:content/metadata/dc:description`.

   Puoi anche selezionare un nodo esistente dalla finestra di dialogo di selezione.

   ![Associare una proprietà di metadati a un predicato nel campo Nome proprietà](assets/property_settings.png)

   Associare una proprietà di metadati a un predicato nel campo Nome proprietà

1. Fai clic sull&#39;**[!UICONTROL Anteprima]** ![anteprima](assets/do-not-localize/preview_icon.png) per generare un&#39;anteprima del pannello Filtri come appare dopo l&#39;aggiunta del predicato.
1. Rivedi il layout del predicato nella modalità Anteprima.

   ![Visualizza l&#39;anteprima del modulo di ricerca prima di inviare le modifiche](assets/preview-1.png)

   Visualizza l&#39;anteprima del modulo di ricerca prima di inviare le modifiche

1. Per chiudere l&#39;anteprima, fare clic su **[!UICONTROL Chiudi]** ![chiudi](assets/do-not-localize/close.png) nell&#39;angolo superiore destro dell&#39;anteprima.
1. Fai clic su **[!UICONTROL Fine]** per salvare le impostazioni.
1. Passare al pannello Ricerca nell&#39;interfaccia utente [!DNL Assets]. Il predicato Proprietà viene aggiunto al pannello.
1. Immetti una descrizione della risorsa da cercare nella casella di testo. Immettere ad esempio `Adobe`. Quando si esegue una ricerca, le risorse con descrizione corrispondente a `Adobe` sono elencate nei risultati della ricerca.

## Aggiungere un predicato Opzioni {#adding-an-options-predicate}

Il predicato Opzioni consente di aggiungere più opzioni di ricerca nel pannello Filtri. Per cercare le risorse, puoi selezionare una o più di queste opzioni nel pannello Filtri. Ad esempio, per cercare le risorse in base al tipo di file, configura opzioni quali Immagini, Multimedia, Documenti e Archivi nel modulo di ricerca. Dopo aver configurato queste opzioni, la ricerca viene eseguita sulle risorse di tipo GIF, JPEG, PNG e così via, quando selezioni l’opzione Immagini nel pannello Filtri.

Per mappare le opzioni alla rispettiva proprietà, crea una struttura di nodi per le opzioni e fornisci il percorso del nodo principale nella proprietà Nome proprietà del predicato Opzioni. Il nodo padre deve essere di tipo `sling`: `OrderedFolder`. Le opzioni devono essere di tipo `nt:unstructured`. I nodi delle opzioni devono avere le proprietà `jcr:title` e `value` configurate.

La proprietà `jcr:title` è un nome descrittivo per l&#39;opzione visualizzata nel pannello Filtri. Il campo `value` viene utilizzato nella query per corrispondere alla proprietà specificata.

Quando si seleziona un&#39;opzione, la ricerca viene eseguita in base alla proprietà `value` del nodo dell&#39;opzione e dei relativi nodi figlio, se presenti. L&#39;intera struttura sotto il nodo di opzione viene attraversata e la proprietà `value` di ciascun nodo figlio viene combinata utilizzando un&#39;operazione OR per creare la query di ricerca.

Ad esempio, se selezioni “Immagini” per i tipi di file, la query di ricerca per le risorse viene creata combinando la proprietà `value` utilizzando un’operazione OR. Ad esempio, la query di ricerca per le immagini è realizzata unendo i risultati di corrispondenza per *image/jpeg*, *image/gif*, *image/png*, *image/pjpeg* e *image/tiff* per la proprietà `jcr:content/metadata/dc:format` tramite un’operazione OR.

![La proprietà Value di un tipo di file, come visualizzata in CRXDE, viene utilizzata per il corretto funzionamento delle query di ricerca](assets/filetype-value-property.png)

La proprietà Value di un tipo di file, come mostrato in CRXDE, viene utilizzata per il funzionamento delle query di ricerca

Invece di creare manualmente una struttura di nodi per le opzioni nell’archivio CRXDE, puoi definire le opzioni in un file JSON, specificando le coppie chiave-valore corrispondenti. Nel campo **[!UICONTROL Nome proprietà]**, specifica il percorso del file JSON. Ad esempio, puoi definire le coppie chiave-valore, `image/bmp`, `image/gif`, `image/jpeg`, `image/png` e specificarne i valori, come mostrato nel seguente file JSON di esempio. Nel campo **[!UICONTROL Nome proprietà]** è possibile specificare il percorso CRXDE per il file.

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
>Il predicato Options è un wrapper personalizzato che include predicati di proprietà per dimostrare il comportamento descritto. Attualmente, non è disponibile alcun endpoint REST per supportare la funzionalità in modo nativo.

1. Fare clic sul logo [!DNL Experience Manager], quindi passare a **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL Cerca in Forms]**.
1. Dalla pagina **[!UICONTROL Cerca in Forms]**, seleziona **[!UICONTROL Barra di ricerca amministrazione Assets]**, quindi fai clic su **[!UICONTROL Modifica]**.
1. Nella pagina **[!UICONTROL Modifica modulo di ricerca]**, trascina **[!UICONTROL Predicato opzioni]** dalla scheda **[!UICONTROL Seleziona predicato]** al riquadro principale.
1. Nella scheda **[!UICONTROL Impostazioni]**, inserisci un’etichetta e un nome per la proprietà. Ad esempio, per cercare le risorse in base al loro formato, specifica un nome descrittivo per l&#39;etichetta, ad esempio **[!UICONTROL Tipo file]**. Specificare la proprietà in base alla quale eseguire la ricerca nel campo proprietà, ad esempio `jcr:content/metadata/dc:format.`
1. Effettua una delle operazioni seguenti:

   * Nel campo **[!UICONTROL Nome proprietà]**, indica il percorso del file JSON in cui si definiscono i nodi per le opzioni e specifica le coppie chiave-valore corrispondenti.
   * Fare clic sul simbolo `+` accanto al campo Opzioni per specificare il testo e il valore da visualizzare per le opzioni che si desidera specificare nel pannello Filtri. Per aggiungere un&#39;altra opzione, fare clic sul simbolo `+` e ripetere il passaggio.

1. Assicurati che l’opzione **[!UICONTROL Selezione singola]** sia deselezionata per consentire all’utente di scegliere più opzioni per volta per i tipi di file (ad esempio, Immagini, Documenti, Multimedia e Archivi). Se scegli **[!UICONTROL Selezione singola]**, l’utente può scegliere una sola opzione alla volta per i tipi di file.

   ![Campi disponibili nel predicato Opzioni](assets/options_predicate.png)

   Campi disponibili nel predicato Opzioni

1. Nel campo **[!UICONTROL Descrizione]** immettere una descrizione facoltativa e quindi fare clic su **[!UICONTROL Fine]**.
1. Passa al pannello Ricerca. Il predicato Options viene aggiunto al pannello **Search**. Le opzioni per **[!UICONTROL Tipo file]** sono visualizzate come caselle di controllo.

## Aggiungere un predicato di proprietà con più valori {#adding-a-multi-value-property-predicate}

Il predicato Proprietà con più valori consente di cercare le risorse per più valori. Considera uno scenario in cui si dispone di immagini di più prodotti in [!DNL Assets] e i metadati per ogni immagine includono un numero SKU associato al prodotto. Puoi utilizzare questo predicato per cercare immagini di prodotto in base a più numeri SKU.

1. Fare clic sul logo [!DNL Experience Manager], quindi passare a **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL Cerca in Forms]**.
1. Nella pagina Forms di ricerca, seleziona **[!UICONTROL Barra di ricerca amministrazione di Assets]**, quindi fai clic sull&#39;icona **[!UICONTROL Modifica]** ![Modifica](assets/do-not-localize/aemassets_edit.png).
1. Nella pagina Modifica modulo di ricerca, trascina il predicato **[!UICONTROL Proprietà con più valori]** dalla scheda **[!UICONTROL Seleziona predicato]** al riquadro principale.
1. Nella scheda **[!UICONTROL Impostazioni]**, immettere un&#39;etichetta e un testo segnaposto per il predicato. Specificare il nome della proprietà in base alla quale eseguire la ricerca nel campo proprietà, ad esempio `jcr:content/metadata/dc:value`. È inoltre possibile utilizzare la finestra di dialogo di selezione per selezionare un nodo.
1. Assicurati di aver selezionato **[!UICONTROL Supporto delimitatore]**. Specifica i delimitatori per separare i singoli valori nel campo **[!UICONTROL Delimitatori di input]**. Per impostazione predefinita, la virgola è indicata come delimitatore. È possibile specificare un delimitatore diverso.
1. Nel campo **Descrizione** immettere una descrizione facoltativa e quindi fare clic su **[!UICONTROL Fine]**.
1. Passare al pannello Filtri nell&#39;interfaccia utente [!DNL Assets]. Al pannello viene aggiunto il predicato **[!UICONTROL Proprietà con più valori]**.
1. Specificare più valori nel campo Multivalore separati dai delimitatori ed eseguire la ricerca. Il predicato recupera una corrispondenza di testo esatta per i valori specificati.

## Aggiungere un predicato Tag {#adding-a-tags-predicate}

Il predicato Tag consente di eseguire ricerche di risorse basate su tag. Per impostazione predefinita, [!DNL Assets] cerca le risorse per trovare uno o più tag corrispondenti in base ai tag specificati. In altre parole, la query di ricerca esegue un&#39;operazione OR utilizzando i tag specificati. Tuttavia, puoi utilizzare l’opzione abbina tutti i tag per cercare le risorse che includono tutti i tag specificati.

1. Fare clic sul logo [!DNL Experience Manager], quindi passare a **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL Cerca in Forms]**.
1. Dalla pagina Forms di ricerca, seleziona **[!UICONTROL Barra di ricerca amministrazione di Assets]**, quindi fai clic sull&#39;icona **[!UICONTROL Modifica]** ![Modifica](assets/do-not-localize/aemassets_edit.png).
1. Nella pagina Modifica modulo di ricerca, trascina **[!UICONTROL Predicato tag]** dalla scheda Seleziona predicato al riquadro principale.
1. Nella scheda Impostazioni, immettere un testo segnaposto per il predicato. Specifica il nome della proprietà in base alla quale eseguire la ricerca nel campo proprietà, ad esempio *jcr:content/metadata/cq:tags*. In alternativa, potete selezionare un nodo in CRXDE dalla finestra di dialogo di selezione.
1. Configurare la proprietà Percorso tag radice di questo predicato per popolare vari tag nell’elenco Tag.
1. Seleziona **[!UICONTROL Mostra opzione di corrispondenza con tutti i tag]** per cercare le risorse che includono tutti i tag specificati.

1. Nel campo **[!UICONTROL Descrizione]** immettere una descrizione facoltativa e quindi fare clic su **[!UICONTROL Fine]**.
1. Passa al pannello Ricerca. Il predicato **[!UICONTROL Tag]** è stato aggiunto al pannello di ricerca.
1. Specifica i tag in base ai quali desideri cercare le risorse o selezionarli dall’elenco dei suggerimenti.

1. Selezionare **[!UICONTROL Corrispondenza con tutti]** per cercare le corrispondenze che includono tutti i tag specificati.

## Aggiungi altri predicati {#adding-other-predicates}

Analogamente al modo in cui si aggiunge un predicato Proprietà o Opzioni, è possibile aggiungere i seguenti predicati aggiuntivi al pannello Ricerca:

| Nome predicato | Descrizione | Proprietà |
|---|---|---|
| [!UICONTROL Testo completo] | Predicato di ricerca per eseguire ricerche full-text su un intero nodo di risorsa. È mappato con l’operatore jcr:contains. Puoi specificare un percorso relativo se desideri eseguire una ricerca full-text su una parte specifica del nodo della risorsa. | <ul><li>Etichetta</li><li>Segnaposto</li><li>Nome proprietà</li><li>Descrizione</li></ul> |
| [!UICONTROL Browser Percorsi] | Predicato di ricerca per cercare le risorse in cartelle e sottocartelle in un percorso principale preconfigurato | <ul><li>Segnaposto</li><li>Percorso directory principale</li><li>Descrizione</li></ul> |
| [!UICONTROL Percorso] | Utilizzala per filtrare i risultati in base alla posizione. È possibile specificare percorsi diversi come opzioni. | <ul><li>Etichetta</li><li>Percorso</li><li>Descrizione</li></ul> |
| [!UICONTROL Stato Publish] | Cerca predicato per cercare le risorse in base al loro stato di pubblicazione | <ul><li>Etichetta</li><li>Nome proprietà</li><li>Descrizione</li></ul> |
| [!UICONTROL Data relativa] | Cerca predicato per cercare le risorse in base alla data relativa di creazione. Ad esempio, puoi configurare diverse opzioni, come 2 mesi fa, 3 settimane fa e così via. | <ul><li>Etichetta</li><li>Nome proprietà</li><li>Data relativa</li></ul> |
| [!UICONTROL Intervallo] | Predicato di ricerca per cercare le risorse che si trovano all’interno di un intervallo specificato. Nel pannello Ricerca, potete specificare i valori minimo e massimo per l&#39;intervallo. | <ul><li>Etichetta</li><li>Nome proprietà</li><li>Descrizione</li></ul> |
| [!UICONTROL Intervallo date] | Cerca predicato per cercare le risorse create all’interno di un intervallo specificato per una proprietà di data. Nel pannello Ricerca, potete specificare le date di inizio e di fine utilizzando gli strumenti di selezione delle date. | <ul><li>Etichetta</li><li>Segnaposto</li><li>Nome proprietà</li><li>Testo intervallo (Da)</li><li>Testo intervallo (A)</li><li>Descrizione</li></ul> |
| [!UICONTROL Data] | Predicato di ricerca per una ricerca di risorse basata su cursore e basata su una proprietà data. | <ul><li>Etichetta</li><li>Nome proprietà</li><li>Descrizione</li></ul> |
| [!UICONTROL Dimensione file] | Cerca predicato per cercare le risorse in base alle loro dimensioni. Si tratta di un predicato basato su silder in cui è possibile selezionare le opzioni del cursore da un nodo configurabile. Le opzioni predefinite sono definite in /libs/dam/options/predicates/filesize nell’archivio CRXDE. La dimensione del file è indicata in byte. | <ul><li>Etichetta</li><li>Nome proprietà</li><li>Percorso</li><li>Descrizione</li></ul> |
| [!UICONTROL Ultima modifica risorsa] | Cerca predicato per cercare le risorse modificate di recente | <ul><li>Nome proprietà</li><li>Valore proprietà</li><li>Descrizione</li></ul> |
| [!UICONTROL Stato Publish] | Cerca predicato per cercare le risorse in base al loro stato di pubblicazione | <ul><li>Etichetta</li><li>Nome proprietà</li><li>Descrizione</li></ul> |
| [!UICONTROL Valutazione] | Cerca predicato per cercare le risorse in base alla loro valutazione media | <ul><li>Etichetta</li><li>Nome proprietà</li><li>Percorso opzione</li><li>Descrizione</li></ul> |
| [!UICONTROL Stato scadenza] | Cerca predicato per cercare le risorse in base al loro stato di scadenza | <ul><li>Etichetta</li><li>Nome proprietà</li><li>Descrizione</li></ul> |
| [!UICONTROL Nascosto] | Predicato di ricerca che definisce una proprietà di campo nascosto per la ricerca di risorse | <ul><li>Nome proprietà</li><li>Valore proprietà</li><li>Descrizione</li></ul> |

## Ripristina facet di ricerca {#restoring-default-search-facets}

Per impostazione predefinita, un&#39;icona di blocco ![icona di blocco chiuso](assets/do-not-localize/lock_closed_icon.svg) viene visualizzata prima di **[!UICONTROL Barra di ricerca amministrazione Assets]** nella pagina **[!UICONTROL Cerca in Forms]**. Blocca l’icona rispetto a un’opzione nella pagina Forms di ricerca indica che le impostazioni predefinite sono intatte e non personalizzate. L&#39;icona ![blocca icona chiuso](assets/do-not-localize/lock_closed_icon.svg) scompare se si aggiungono al modulo facet di ricerca che indicano che il modulo predefinito è stato modificato.

![Icona Blocca](assets/locked_admin_rail.png)

Per ripristinare il facet di ricerca predefinito, effettuare le seguenti operazioni:

1. Selezionare **[!UICONTROL Barra di ricerca amministrazione Assets]** nella pagina **[!UICONTROL Cerca in Forms]**.
1. Fare clic su **[!UICONTROL Elimina]** ![elimina struttura](assets/do-not-localize/deleteoutline.png) nella barra degli strumenti.
1. Nella finestra di dialogo di conferma, fai clic su **[!UICONTROL Elimina]** per rimuovere le modifiche personalizzate.

   Dopo aver eliminato le modifiche personalizzate ai facet di ricerca, l&#39;icona del lucchetto ![icona del lucchetto chiuso](assets/do-not-localize/lock_closed_icon.svg) viene visualizzata nuovamente prima di **[!UICONTROL Barra di ricerca amministrazione Assets]** nella pagina **[!UICONTROL Cerca in Forms]**.

## Autorizzazioni utente {#user-permissions}

Se non ti è stato assegnato un ruolo di amministratore, ecco un elenco di autorizzazioni necessarie per eseguire le azioni di modifica, eliminazione e anteprima che coinvolgono i facet di ricerca.

| Azione | Autorizzazioni |
| ------------------- | ---------------------------------------------------------------- |
| [!UICONTROL Modifica] | Autorizzazioni di lettura e scrittura sul nodo `/apps` in CRXDE |
| [!UICONTROL Elimina] | Autorizzazioni di lettura, scrittura ed eliminazione per il nodo `/apps` in CRXDE |
| [!UICONTROL Anteprima] | Autorizzazioni di lettura, scrittura ed eliminazione per il nodo `/var/dam/content` in CRXDE. Inoltre, le autorizzazioni di lettura e scrittura sul nodo `/apps`. |

>[!MORELIKETHIS]
>
>* [Estendi funzionalità di ricerca risorse](searchx.md)
>* [Cercare risorse](search-assets.md)
