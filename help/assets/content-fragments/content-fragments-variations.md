---
title: Varianti - Authoring dei contenuti di frammenti
seo-title: Varianti - Authoring dei contenuti di frammenti
description: Le varianti consentono di creare contenuti per il frammento, quindi di creare varianti di tali contenuti in base allo scopo (se necessario).
seo-description: Le varianti consentono di creare contenuti per il frammento, quindi di creare varianti di tali contenuti in base allo scopo (se necessario).
uuid: 0844f271-79bc-4f76-8031-d388b81d6feb
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: content-fragments
content-type: reference
discoiquuid: 324df1da-78fa-460f-a744-3504259f1d4a
docset: aem65
feature: Frammenti di contenuto
role: User, Admin
exl-id: ded05f24-ab5c-4195-b5c4-704a9fd93c7e
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1746'
ht-degree: 16%

---

# Varianti - Authoring dei contenuti di frammenti{#variations-authoring-fragment-content}

[](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) Le varianti sono una caratteristica significativa dei frammenti di contenuto, in quanto consentono di creare e modificare copie del contenuto principale da utilizzare su canali e/o scenari specifici.

Dalla scheda **Variazioni** è possibile:

* [Immettere il ](#authoring-your-content) contenuto del frammento
* [Creare e gestire ](#managing-variations) le varianti del contenuto  **** principale

Eseguire una serie di altre azioni a seconda del tipo di dati in corso di modifica; ad esempio:

* [Inserire risorse visive nel frammento](#inserting-assets-into-your-fragment)  (immagini)
* Seleziona tra [Rich Text](#rich-text), [Testo normale](#plain-text) e [Markdown](#markdown) per la modifica

* [Carica contenuto](#uploading-content)

* [Visualizzare le statistiche chiave](#viewing-key-statistics)  (informazioni sul testo su più righe)
* [Testo riepilogo](#summarizing-text)

* [Sincronizzare le varianti con il contenuto principale](#synchronizing-with-master)

>[!CAUTION]
>
>Dopo la pubblicazione e/o il riferimento a un frammento, AEM un avviso quando un autore riapre il frammento per la modifica. In questo modo si avverte che le modifiche al frammento avranno effetto anche sulle pagine a cui si fa riferimento.

## Authoring dei contenuti {#authoring-your-content}

Quando apri il frammento di contenuto per la modifica, la scheda **Variazioni** viene aperta per impostazione predefinita. Qui puoi creare il contenuto, per Master o qualsiasi variante disponibile. Operazioni disponibili:

* apportare modifiche direttamente nella scheda **Variazioni**
* apri l&#39; [editor a schermo intero](#full-screen-editor) per:

   * seleziona [Formato](#formats)
   * ulteriori opzioni di modifica (per il formato [Rich Text](#rich-text))

   * accedere a un intervallo di [azioni](#actions)

Esempio:

* Modifica di un frammento semplice

   Un frammento semplice è costituito da un campo di testo a più righe (è possibile aggiungere risorse visive dall’editor a schermo intero).

   ![cfm-6420-21](assets/cfm-6420-21.png)

* Modifica di un frammento con contenuto strutturato

   Un frammento strutturato contiene vari campi, di vari tipi di dati, definiti nel modello di contenuto. Per tutti i campi con più righe è disponibile l’ [editor a schermo intero](#full-screen-editor).

   ![cfm-6420-16](assets/cfm-6420-16.png)

### Editor a schermo intero {#full-screen-editor}

Quando modifichi un campo di testo su più righe puoi aprire l’editor a schermo intero:

![cf-fullscreeneditor-icon](assets/cf-fullscreeneditor-icon.png)

L’editor a schermo intero fornisce:

* Accesso a varie [azioni](#actions)
* A seconda del [formato](#formats), opzioni di formattazione aggiuntive ([Rich Text](#rich-text))

### Azioni {#actions}

Sono disponibili anche le seguenti azioni (per tutti i [formati](#formats)) quando è aperto l&#39;editor a schermo intero (cioè il testo su più righe):

* Seleziona il [formato](#formats) ([Rich Text](#rich-text), [Testo normale,](#plain-text) [Markdown](#markdown))

* [Mostra statistiche testo](#viewing-key-statistics)

* [Caricare contenuto](#uploading-content)
* [Sincronizza con principale](#synchronizing-with-master)  (durante la modifica di una variante)
* [Testo riepilogo](#summarizing-text)
* [](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment) Annotazione del testo

* [Inserire risorse visive nel frammento](#inserting-assets-into-your-fragment)  (immagini)

### Formati {#formats}

Le opzioni per la modifica del testo su più righe dipendono dal formato selezionato:

* [Formato RTF](#rich-text)
* [Testo normale](#plain-text)
* [Markdown](#markdown)

Il formato può essere selezionato quando si utilizza l’editor a schermo intero.

### Formato RTF {#rich-text}

La modifica Rich Text consente di formattare:

* Grassetto
* Corsivo
* Sottolineato
* Allineamento: sinistra, centro, destra
* Elenco puntato
* Elenco numerato
* Rientro: aumento, diminuzione
* Creare/interrompere collegamenti ipertestuali
* Apri l’editor a schermo intero, in cui sono disponibili le seguenti opzioni di formattazione:

   * Incolla testo/da Word
   * Inserire una tabella
   * Stile paragrafo: Paragrafo, Titolo 1/2/3
   * [Inserire risorse visive](#inserting-assets-into-your-fragment)
   * Ricerca
   * Trova/Sostituisci
   * Controllo ortografia
   * [Annotazioni](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)

Le [azioni](#actions) sono accessibili anche dall’editor a schermo intero.

### Testo normale {#plain-text}

Testo normale consente di inserire rapidamente i contenuti senza formattazione o informazioni di markdown. Puoi anche aprire l&#39;editor a schermo intero per ulteriori [azioni](#actions).

>[!CAUTION]
>
>Se selezioni **Testo normale**, potresti perdere la formattazione, le marcature e/o le risorse inserite in **Rich Text** o **Markdown**.

### Markdown {#markdown}

>[!NOTE]
>
>Per informazioni complete, consulta la documentazione [Markdown](/help/assets/content-fragments/content-fragments-markdown.md) .

Questo consente di formattare il testo utilizzando markdown. Puoi definire:

* Intestazioni
* Paragrafi e interruzioni di riga
* Collegamenti
* Immagini
* Virgolette a blocchi
* Elenchi
* Enfasi
* Blocchi di codice
* Espressioni barra rovesciata

Puoi anche aprire l&#39;editor a schermo intero per ulteriori [azioni](#actions).

>[!CAUTION]
>
>Se passi da **Rich Text** a **Markdown**, potresti riscontrare effetti imprevisti con Block Quotes (Citazioni) e Code Blocks (Blocchi di codice), in quanto questi due formati possono presentare differenze nelle modalità di gestione.

### Visualizzazione delle statistiche chiave {#viewing-key-statistics}

Quando l’editor a schermo intero è aperto, l’azione **Statistiche testo** visualizzerà una serie di informazioni sul testo. Esempio:

![cfx-6420-22](assets/cfx-6420-22.png)

### Caricamento del contenuto {#uploading-content}

Per facilitare il processo di creazione dei frammenti di contenuto, puoi caricare il testo, prepararlo in un editor esterno e aggiungerlo direttamente al frammento.

### Testo riepilogo {#summarizing-text}

Il testo di riepilogo è progettato per aiutare gli utenti a ridurre la lunghezza del testo a un numero predefinito di parole, mantenendo al tempo stesso i punti chiave e il significato generale.

>[!NOTE]
>
>A livello più tecnico, il sistema mantiene le frasi che valuta fornendo il *miglior rapporto di densità delle informazioni e di unicità* in base a specifici algoritmi.

>[!CAUTION]
>
>Il frammento di contenuto deve avere come predecessore una cartella di lingua (codice ISO) valida; viene utilizzato per determinare il modello di lingua da utilizzare.
>
>Ad esempio, `en/` come nel seguente percorso:
>
>`/content/dam/my-brand/en/path-down/my-content-fragment`

>[!CAUTION]
>
>L&#39;inglese è disponibile come standard.
>
>Altre lingue sono disponibili come Pacchetti modello lingua da Distribuzione software:
>
>* [Francese (fr) da Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)
>* [Tedesco (de) da Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-de)
>* [Italiano (it) da Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-it)
>* [Spagnolo (es) da Distribuzione di software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-es)

>



1. Selezionare **Master** o la variante richiesta.
1. Apri l’editor a schermo intero.

1. Seleziona **Riepiloga testo** dalla barra degli strumenti.

   ![cf-17](assets/cf-17.png)

1. Specifica il numero di parole desiderato e seleziona **Start**:
1. Il testo originale viene visualizzato affiancato al riepilogo proposto:

   * Tutte le frasi da eliminare sono evidenziate in rosso, con un click-through.
   * Fai clic su una frase evidenziata per mantenerla nel contenuto riepilogato.
   * Fai clic su una frase non evidenziata per eliminarla.

   ![cfm-6420-23](assets/cfm-6420-23.png)

1. Seleziona **Riepilogo** per confermare le modifiche.

### Aggiunta di annotazioni a un frammento di contenuto {#annotating-a-content-fragment}

Per annotare un frammento:

1. Selezionare **Master** o la variante richiesta.
1. Apri l’editor a schermo intero.
1. Seleziona del testo. L&#39;icona **Annota** diventa disponibile.

   ![cfm-6420-24](assets/cfm-6420-24.png)

1. Viene aperta una finestra di dialogo. Consente di inserire l’annotazione.

1. Chiudi l’editor a schermo intero e **Salva** il frammento.

### Visualizzazione, Modifica, Eliminazione Di Annotazioni {#viewing-editing-deleting-annotations}

Annotazioni:

* Sono evidenziati dal testo, sia in modalità a schermo intero che in modalità normale dell’editor. Per visualizzare, modificare e/o eliminare tutti i dettagli di un’annotazione, fate clic sul testo evidenziato per riaprire la finestra di dialogo.

   >[!NOTE]
   >
   >Se a un testo sono state applicate più annotazioni, viene fornito un selettore a discesa.

* Quando si elimina l’intero testo a cui è stata applicata l’annotazione, viene eliminata anche l’annotazione.

* Può essere elencato ed eliminato selezionando la scheda **Annotazioni** nell’editor frammenti.

   ![cfm-6420-25](assets/cfm-6420-25.png)

* Può essere visualizzato ed eliminato in [Timeline](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments) per il frammento selezionato.

### Inserimento di risorse nel frammento {#inserting-assets-into-your-fragment}

Per semplificare il processo di creazione dei frammenti di contenuto, puoi aggiungere direttamente [Risorse](/help/assets/manage-assets.md) (immagini) al frammento.

Vengono aggiunti alla sequenza di paragrafi del frammento senza formattazione; la formattazione può essere eseguita quando il frammento [viene utilizzato/a cui si fa riferimento in una pagina](/help/sites-authoring/content-fragments.md).

>[!CAUTION]
>
>Queste risorse non possono essere spostate o eliminate in una pagina di riferimento, ma devono essere eseguite nell’editor frammenti.
>
>Tuttavia, la formattazione della risorsa (ad esempio, le dimensioni) deve essere eseguita nell’ [editor di pagine](/help/sites-authoring/content-fragments.md). La rappresentazione della risorsa nell’editor frammenti è puramente per la creazione del flusso di contenuto.

>[!NOTE]
>
>Esistono vari metodi per aggiungere [immagini](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) al frammento e/o alla pagina.

1. Posiziona il cursore nel punto in cui vuoi aggiungere l’immagine.
1. Per aprire la finestra di dialogo di ricerca, utilizza l’icona **Inserisci risorsa**.

   ![cf-insertasset-icon](assets/cf-insertasset-icon.png)

1. Nella finestra di dialogo puoi effettuare le seguenti operazioni:

   * Passa alla risorsa richiesta in DAM
   * cerca la risorsa in DAM

   Una volta individuata la risorsa desiderata, fai clic sulla miniatura.

1. Utilizza **Seleziona** per aggiungere la risorsa al sistema paragrafo del frammento di contenuto nella posizione corrente.

   >[!CAUTION]
   >
   >Se, dopo aver aggiunto una risorsa, ne cambi il formato in:
   >
   >* **Testo normale**: la risorsa verrà persa completamente dal frammento.
   >* **Markdown**: la risorsa non sarà visibile, ma lo tornerà a essere quando tornerai a **Rich Text**.


## Gestione delle varianti {#managing-variations}

### Creazione di una variante {#creating-a-variation}

Le varianti ti consentono di prendere il contenuto **Master** e modificarlo in base allo scopo (se necessario).

Per creare una nuova variante:

1. Apri il frammento e accertati che il pannello laterale sia visibile.
1. Seleziona **Variazioni** dalla barra delle icone nel pannello laterale.
1. Seleziona **Crea variante**.
1. Viene aperta una finestra di dialogo in cui vengono specificati **Titolo** e **Descrizione** per la nuova variante.
1. Seleziona **Aggiungi**, il frammento **Master** verrà copiato nella nuova variante, che è ora aperta per la [modifica](#editing-a-variation).

   >[!NOTE]
   >
   >Quando crei una nuova variante, viene sempre copiata **Master** e non la variante attualmente aperta.

### Modifica di una variante {#editing-a-variation}

Puoi apportare modifiche al contenuto della variante dopo:

* [Creazione della variante](#creating-a-variation).
* Aprite un frammento esistente, quindi selezionate la variante desiderata dal pannello laterale.

![cfm-6420-26](assets/cfm-6420-26.png)

### Ridenominazione di una variante {#renaming-a-variation}

Per rinominare una variante esistente:

1. Apri il frammento e seleziona **Variazioni** dal pannello laterale.
1. Seleziona la variante desiderata.
1. Seleziona **Rinomina** dal menu a discesa **Azioni**.

1. Immetti il nuovo **Titolo** e/o **Descrizione** nella finestra di dialogo in questione.

1. Conferma l’azione **Rinomina**.

>[!NOTE]
>
>Questo influisce solo sulla variante **Titolo**.

### Eliminazione di una variante {#deleting-a-variation}

Per eliminare una variante esistente:

1. Apri il frammento e seleziona **Variazioni** dal pannello laterale.
1. Seleziona la variante desiderata.
1. Seleziona **Elimina** dal menu a discesa **Azioni**.

1. Conferma l’azione **Elimina** nella finestra di dialogo.

>[!NOTE]
>
>Non è possibile eliminare **Master**.

### Sincronizzazione con Master {#synchronizing-with-master}

**** Master è una parte integrale di un frammento di contenuto e, per definizione, contiene la copia master del contenuto, mentre le varianti contengono le singole versioni aggiornate e personalizzate del contenuto. Quando Master viene aggiornato, è possibile che queste modifiche siano pertinenti anche alle varianti e, pertanto, devono essere propagate a esse.

Quando modifichi una variante hai accesso all’azione per sincronizzare l’elemento corrente della variante con Master. Questo consente di copiare automaticamente le modifiche apportate a Master nella variante desiderata.

>[!CAUTION]
>
>La sincronizzazione è disponibile solo per copiare le modifiche *da **Master**alla variante*.
>
>Viene sincronizzato solo l’elemento corrente della variante.
>
>La sincronizzazione funziona solo sul tipo di dati **Testo su più righe**.
>
>Il trasferimento delle modifiche *da una variante a **Master*** non è disponibile come opzione.

1. Apri il frammento di contenuto nell’editor frammenti. Assicurati che il **Master** sia stato modificato.
1. Seleziona una variante specifica, quindi l’azione di sincronizzazione appropriata da:

   * selettore a discesa **Azioni** - **Sincronizza l&#39;elemento corrente con master**

   * la barra degli strumenti dell&#39;editor a schermo intero - **Sincronizza con master**

1. Master e la variante saranno mostrati uno accanto all’altro:

   * verde indica il contenuto aggiunto (alla variante)
   * il rosso indica il contenuto rimosso (dalla variante)

   ![cfm-6420-27](assets/cfm-6420-27.png)

1. Seleziona **Sincronizza**, la variante verrà aggiornata e visualizzata.
