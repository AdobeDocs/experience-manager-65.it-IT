---
title: Creare una comunicazione interattiva
description: Crea una comunicazione interattiva utilizzando l’editor di comunicazione interattiva. Utilizza la funzionalità di trascinamento della selezione per creare la comunicazione interattiva e visualizzare in anteprima gli output di stampa e web su diversi tipi di dispositivi.
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
exl-id: 1f89c3bf-e67e-4d13-9285-3367be1ac8f8
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '6130'
ht-degree: 1%

---

# Creare una comunicazione interattiva{#create-an-interactive-communication}

## Panoramica {#overview}

Le comunicazioni interattive centralizzano e gestiscono la creazione, l’assemblaggio e la consegna di corrispondenze personalizzate e interattive. Utilizza stampa come canale principale per il web, puoi ridurre al minimo la duplicazione degli sforzi nella creazione dell’output web della comunicazione interattiva.

### Prerequisiti {#prerequisites}

Di seguito sono riportati i prerequisiti per la creazione di una comunicazione interattiva:

* Configura un [modello dati modulo](/help/forms/using/data-integration.md) contenente dati di test o con un&#39;origine dati effettiva, ad esempio un&#39;istanza di Microsoft® Dynamics.
* Assicurati di disporre dei [frammenti di documento](/help/forms/using/document-fragments.md).
* Assicurati di disporre di [modelli per il canale di stampa e web](/help/forms/using/web-channel-print-channel.md).
* Verifica di disporre del [tema](/help/forms/using/themes.md) richiesto per il canale Web.

## Crea comunicazione interattiva {#createic}

1. Accedi all&#39;istanza di creazione dell&#39;AEM e passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Seleziona **[!UICONTROL Crea]** e seleziona **[!UICONTROL Comunicazione interattiva]**. Viene visualizzata la pagina Crea comunicazione interattiva.

   ![create-interactive-communication](assets/create-interactive-communication.png)

1. Immettere le seguenti informazioni. :

   * **[!UICONTROL Titolo]**: immetti il titolo della comunicazione interattiva.
   * **[!UICONTROL Nome]**: il nome della comunicazione interattiva deriva dal titolo immesso. Se necessario, modificalo.
   * **[!UICONTROL Descrizione]**: immettere una descrizione della comunicazione interattiva.
   * **[!UICONTROL Modello dati modulo]**: sfogliare e selezionare il modello dati modulo. Per ulteriori informazioni sul modello dati modulo, vedere [Integrazione dati AEM Forms](/help/forms/using/data-integration.md).

   * **[!UICONTROL Servizio di precompilazione]**: selezionare il servizio di precompilazione per recuperare i dati e precompilare la comunicazione interattiva.
   * **[!UICONTROL Tipo di processo Post]**: è possibile selezionare il flusso di lavoro AEM o Forms da attivare quando viene inviata la comunicazione interattiva. Seleziona il tipo di flusso di lavoro da attivare.

   * **[!UICONTROL Processo Post]**: selezionare il nome del flusso di lavoro da attivare. Quando si seleziona un flusso di lavoro AEM, specificare Percorso allegato, Percorso layout, Percorso PDF, Percorso dati di stampa e Percorso dati Web.
   * **[!UICONTROL Tag]**: seleziona i tag da applicare alla comunicazione interattiva. Puoi anche immettere un nome di tag nuovo/personalizzato e premere Invio per crearlo.
   * **[!UICONTROL Autore]**: il nome dell&#39;autore viene ricavato automaticamente dal nome utente dell&#39;utente connesso.
   * **[!UICONTROL Data Publish:]** Immettere la data di pubblicazione della comunicazione interattiva.
   * **[!UICONTROL Data annullamento pubblicazione]**: immetti la data in cui annullare la pubblicazione della comunicazione interattiva.

1. Seleziona **[!UICONTROL Avanti]**. Viene visualizzata la schermata che consente di specificare i dettagli dei canali di stampa e web.
1. Immetti quanto segue:

   * **[!UICONTROL Stampa]**: selezionare questa opzione per generare il canale di stampa della comunicazione interattiva.
   * **[!UICONTROL Modello di stampa]**: sfoglia e seleziona un XDP come modello di stampa.
   * **[!UICONTROL Web]**: selezionare questa opzione per generare il canale Web o l&#39;output reattivo della comunicazione interattiva.
   * **[!UICONTROL Modello Web di comunicazione interattiva]**: sfogliare e selezionare il modello Web.
   * **[!UICONTROL Tema]** e **[!UICONTROL Seleziona tema]**: sfoglia e seleziona il tema per assegnare uno stile al canale web della comunicazione interattiva. Per ulteriori informazioni, vedere [Temi in AEM Forms](/help/forms/using/themes.md).

   * **[!UICONTROL Utilizza Stampa come master per il canale Web]**: selezionare questa opzione per creare il canale Web sincronizzato con il canale di stampa. L&#39;utilizzo del canale di stampa come master per il canale Web garantisce che il contenuto e l&#39;associazione dati del canale Web siano derivati dal canale di stampa e che le modifiche apportate al canale di stampa vengano applicate al canale Web quando si seleziona Sincronizza. Tuttavia, agli autori è consentito interrompere l’ereditarietà di componenti specifici nel canale web, in base alle esigenze. Per ulteriori informazioni, vedere [Sincronizzare canale Web con canale di stampa](../../forms/using/create-interactive-communication.md#synchronize).
Se si seleziona l&#39;opzione **[!UICONTROL Usa stampa come master per canale Web]**, è possibile selezionare una delle modalità seguenti per generare il canale Web:

      * **[!UICONTROL Layout automatico]**: selezionare questa modalità per generare automaticamente segnaposto, contenuto e associazione dati per il canale Web dal canale di stampa.
      * **[!UICONTROL Organizza manualmente]**: seleziona questa modalità per selezionare e aggiungere manualmente gli elementi del canale di stampa al canale Web utilizzando il contenuto principale disponibile nella scheda **[!UICONTROL Origini dati]**. Per ulteriori informazioni, vedere [Selezionare gli elementi del canale di stampa per creare il contenuto del canale Web](#selectprintchannelelements).

   Per ulteriori informazioni sul canale di stampa e sul canale Web, vedere [Canale di stampa e canale Web](/help/forms/using/web-channel-print-channel.md).

1. Seleziona **[!UICONTROL Crea]**. Viene creata la comunicazione interattiva e viene visualizzata una finestra di avviso. Selezionare **[!UICONTROL Modifica]** per iniziare a creare il contenuto della comunicazione interattiva come descritto in [Aggiungi contenuto tramite l&#39;interfaccia utente di creazione della comunicazione interattiva](#step2). In alternativa, è possibile selezionare **[!UICONTROL Fine]** e scegliere di modificare la comunicazione interattiva in un secondo momento.

## Aggiungere contenuto alla comunicazione interattiva {#step2}

Dopo aver creato una comunicazione interattiva, puoi utilizzare l’interfaccia di authoring di comunicazione interattiva per crearne il contenuto.

Per ulteriori informazioni sull&#39;interfaccia di creazione di comunicazioni interattive, vedere [Introduzione all&#39;authoring di comunicazioni interattive](/help/forms/using/introduction-interactive-communication-authoring.md).

1. L&#39;interfaccia di creazione della comunicazione interattiva viene avviata quando si seleziona Modifica come indicato in [Crea comunicazione interattiva](#createic). In alternativa, puoi passare a una risorsa di comunicazione interattiva esistente su AEM, selezionarla e selezionare **[!UICONTROL Modifica]** per avviare l&#39;interfaccia di creazione della comunicazione interattiva.

   Per impostazione predefinita, viene visualizzato il canale di stampa della comunicazione interattiva, a meno che la comunicazione interattiva non sia solo per il canale web. Il canale Stampa della comunicazione interattiva visualizza le aree di destinazione, come disponibili nel modello di canale XDP/stampa selezionato. In queste aree e questi campi di destinazione, puoi aggiungere componenti o risorse.

1. Con il canale di stampa selezionato, selezionare la scheda **[!UICONTROL Componenti]**. Nel canale di stampa sono disponibili i seguenti componenti:

   | **Component** | **Funzionalità** |
   |---|---|
   | Grafico | Aggiunge un grafico che è possibile utilizzare nella comunicazione interattiva per la rappresentazione visiva di dati bidimensionali recuperati da un insieme di modelli di dati del modulo. Per ulteriori informazioni, vedere [Utilizzo di grafici nelle comunicazioni interattive](/help/forms/using/chart-component-interactive-communications.md). |
   | Frammento di documento | Consente di aggiungere a una comunicazione interattiva un componente riutilizzabile, ad esempio testo, elenco o condizione. Il componente aggiunto può essere basato su un modello di dati modulo o senza un modello di dati modulo. |
   | Immagine | Consente di inserire un&#39;immagine. |

   Trascina i componenti nella comunicazione interattiva e configurali come richiesto.

   È inoltre possibile utilizzare le operazioni Annulla e Ripristina durante la creazione di una comunicazione interattiva sia per i canali di stampa che per quelli Web.

   Utilizzare l&#39;operazione Annulla per annullare l&#39;ultima azione eseguita e l&#39;operazione Ripeti per incorporare nuovamente l&#39;azione eliminata. Se, ad esempio, è stata inserita un&#39;immagine o creata un&#39;associazione dati in una comunicazione interattiva ed è necessario eliminarla, utilizzare l&#39;operazione Annulla.

   ![Azioni Annulla Ripristina](assets/undo_redo_actions_new.png)

   Le opzioni Annulla e Ripristina vengono visualizzate sulla barra degli strumenti della pagina dell’interfaccia utente di authoring. L&#39;opzione Annulla (Undo) viene visualizzata solo dopo aver eseguito un&#39;azione. L&#39;opzione Ripristina viene visualizzata sulla barra degli strumenti della pagina solo dopo l&#39;esecuzione di un&#39;operazione Annulla. Queste azioni vengono reimpostate all’aggiornamento della pagina.

1. Con il canale di stampa selezionato, passa alla scheda **[!UICONTROL Assets]** e applica il filtro per visualizzare solo le risorse che desideri visualizzare.

   Utilizzando il browser Assets, puoi anche trascinare e rilasciare direttamente le risorse nelle aree di destinazione della comunicazione interattiva.

   ![assets-docfragments](assets/assets-docfragments.png)

1. Trascinare i frammenti del documento nella comunicazione interattiva. Di seguito sono elencati i tipi di frammenti di documento che è possibile utilizzare nel canale di stampa della comunicazione interattiva.

<table>
 <tbody>
  <tr>
   <td><strong>Tipo frammento documento</strong></td>
   <td><strong>Scopo di esempio</strong></td>
  </tr>
  <tr>
   <td><a href="/help/forms/using/texts-interactive-communications.md" target="_blank">Testo</a></td>
   <td>Testo per aggiungere l’indirizzo, l’e-mail del destinatario e il corpo del testo della lettera </td>
  </tr>
  <tr>
   <td><a href="/help/forms/using/conditions-interactive-communications.md" target="_blank">Condizione</a></td>
   <td>Condizione per aggiungere l’immagine di intestazione appropriata alla comunicazione in base al tipo di criterio: Standard o Premium. <br /> </td>
  </tr>
  <tr>
   <td>Elenco</td>
   <td>Gruppo di frammenti di documenti, inclusi testo, condizioni, altri elenchi e immagini. <br /> </td>
  </tr>
 </tbody>
</table>

È inoltre possibile sostituire l&#39;associazione tra un&#39;area di destinazione e un frammento di documento rilasciando il nuovo frammento sull&#39;area di destinazione utilizzando la scheda **[!UICONTROL Assets]**. L’ombreggiatura blu dell’area di destinazione durante il trascinamento del frammento indica che il frammento di documento può essere rilasciato nell’area di destinazione.

Per ulteriori informazioni sui frammenti di documenti, vedere [Frammenti di documenti](/help/forms/using/document-fragments.md).

L’interfaccia di authoring consente di distinguere tra campi e variabili non associati e associati all’interno di una comunicazione interattiva. L’interfaccia evidenzia i campi e le variabili non associati utilizzando un bordo arancione.

![unbound_fields_variables_highlight_dc](assets/unbound_fields_variables_highlights_dc.jpg)

Inoltre, quando passi il mouse su questi elementi, viene visualizzata una descrizione con il messaggio Campo (non associato) o Variabile (non associato).

Talvolta, una variabile non associata utilizzata in un frammento di documento potrebbe non essere visualizzata nell’interfaccia di creazione. Può verificarsi a causa di una regola di testo in linea all’interno di un frammento di documento o se è presente un frammento di condizione. In questi casi, una descrizione, evidenziata in blu, viene visualizzata come parte del frammento di documento. Nella descrizione viene visualizzato il numero di variabili non associate utilizzate all’interno di un frammento di documento.

![Variabile non associata](assets/df_unbound_variable_new.png)

Seleziona il frammento di documento, fai clic su ![configure_icon](assets/configure_icon.png) (Configura), quindi seleziona **[!UICONTROL Proprietà]** dalla barra laterale della comunicazione interattiva. Nella sezione **[!UICONTROL Variabili e oggetti modello dati]** sono elencate le variabili, incluse le variabili nascoste, e gli oggetti modello dati utilizzati nei frammenti di documento. Utilizza l&#39;icona ![modifica](assets/edit.svg) (Modifica) accanto a ciascun oggetto o variabile del modello di dati per modificare le proprietà.

1. Per impostare l&#39;associazione delle variabili, selezionare una variabile, selezionare ![configure_icon](assets/configure_icon.png) (Configura), quindi impostare le proprietà di associazione nel pannello Proprietà nella barra laterale.

   * **Nessuno**: l&#39;agente compilerà il valore per la variabile.
   * **Frammento di testo**: se è selezionato, è possibile sfogliare e selezionare un frammento di documento di testo il cui contenuto viene renderizzato nel campo. Solo i frammenti di documenti di testo possono essere associati a variabili prive di variabili in.
   * **Oggetto modello dati**: selezionare una proprietà modello dati modulo il cui valore è popolato nel campo.
   * **Valore predefinito:** È possibile definire un valore predefinito per la variabile utilizzando questo campo. Il valore viene visualizzato quando visualizzi l’anteprima della comunicazione interattiva o nell’interfaccia utente dell’agente.
   * **Pattern di visualizzazione:** È inoltre possibile definire un formato di visualizzazione per una variabile. Selezionare una delle opzioni predefinite dall&#39;elenco a discesa **Tipo** per applicare un formato di visualizzazione a una variabile. Selezionare **Personalizzato** per definire un modello di visualizzazione non disponibile nell&#39;elenco. Per ulteriori informazioni, vedere [Modelli di visualizzazione dei dati](../../forms/using/create-interactive-communication.md#datadisplaypatterns).

   Passa a [Variabili e oggetti modello dati](../../forms/using/create-interactive-communication.md#hiddenvariables) per impostare l&#39;associazione delle variabili nascoste nel frammento di documento.

   È inoltre possibile trascinare elementi dell’origine dati o frammenti di documenti di testo per impostare l’associazione delle variabili.  Per creare un&#39;associazione con uno degli elementi dell&#39;origine dati, selezionare la scheda **Origini dati** e trascinare l&#39;elemento nel nome della variabile. L&#39;elemento e la variabile dell&#39;origine dati devono essere dello stesso tipo per impostare correttamente l&#39;associazione. Se trascini un elemento origine dati su una variabile già associata, il nuovo elemento sostituisce il precedente per creare un&#39;associazione con la variabile. Allo stesso modo, seleziona la scheda **Assets** e trascina il frammento del documento di testo sul nome della variabile per impostare l&#39;associazione tra di essi. Il frammento di documento di testo non deve contenere variabili.

1. Per aggiungere una tabella, con il canale di stampa selezionato, nella scheda **[!UICONTROL Assets]** applica il filtro per visualizzare solo i frammenti di layout. Trascina il frammento di layout richiesto nella comunicazione interattiva. Un frammento di layout è basato su un XDP e può essere utilizzato per creare layout grafici o tabelle statiche e dinamiche in Comunicazione interattiva che vengono compilate con dati dinamici.

   Esempio: una tabella di layout per visualizzare il premio lordo, la percentuale di sconto fedeltà e la disponibilità dell&#39;assistenza stradale di emergenza per i criteri vecchi e nuovi.

   Per ulteriori informazioni sui frammenti di layout, vedere [Frammenti di documento](/help/forms/using/document-fragments.md).

1. Con il canale di stampa selezionato, nella scheda **[!UICONTROL Assets]** applica il filtro alle immagini visualizzate. Trascina le immagini richieste nella comunicazione interattiva, ad esempio per il logo dell’azienda.

   Inoltre, gestisci quanto segue nella comunicazione interattiva:

   * [Aggiunta e configurazione di grafici](/help/forms/using/chart-component-interactive-communications.md)
   * [Sincronizzazione del canale web con il canale di stampa](../../forms/using/create-interactive-communication.md#synchronize)

      * Sincronizzazione automatica
      * Annulla ereditarietà
      * Riabilita ereditarietà
      * Sincronizza

   * [Allegati e accesso alla libreria](../../forms/using/create-interactive-communication.md#attachmentslibrary)
   * [Proprietà campo XDP/Layout](../../forms/using/create-interactive-communication.md#xdplayoutfieldproperties)
   * [Aggiungere regole ai componenti](../../forms/using/create-interactive-communication.md#rules)

1. Passa a **[!UICONTROL Canale Web]**. Il canale web viene visualizzato nell’editor di comunicazione interattiva. Quando si passa per la prima volta dal canale di stampa al canale Web, viene eseguita automaticamente la sincronizzazione. Per ulteriori informazioni, vedere [Sincronizzazione del canale Web dal canale di stampa](../../forms/using/create-interactive-communication.md#synchronize).

   Poiché in questo esempio viene utilizzato Stampa come master per il Web, i segnaposto del canale di stampa, il contenuto e l’associazione dati vengono sincronizzati nel canale web. Tuttavia, puoi modificare e personalizzare il contenuto specifico nel canale web. [Annulla ereditarietà](#cancelinheritance) per le aree di destinazione e le variabili generate utilizzando il canale di stampa per personalizzare il contenuto.

   ![webchannelassets](assets/webchannelassets.png)

   Seleziona il frammento di documento, fai clic su ![configure_icon](assets/configure_icon.png) (Configura), quindi seleziona **[!UICONTROL Proprietà]** dalla barra laterale della comunicazione interattiva. Nella sezione **[!UICONTROL Variabili e oggetti modello dati]** sono elencate le variabili, incluse le variabili nascoste, e gli oggetti modello dati utilizzati nei frammenti di documento. Utilizza l&#39;icona ![modifica](assets/edit.svg) (Modifica) accanto a ciascun oggetto o variabile del modello di dati per modificare le proprietà. Inoltre, per i frammenti di documento che sono stati [generati automaticamente](#synchronize) nel canale Web utilizzando il canale di stampa, utilizza l&#39;icona ![cancelinheritance](assets/cancelinheritance.png) (Annulla ereditarietà) accanto a ogni oggetto modello dati e variabile per [annullare ereditarietà](#cancelinheritance) e per essere in grado di modificarli.

1. Per aggiungere altri componenti nel canale Web, con il canale Web selezionato, selezionare **[!UICONTROL Componenti]**. Trascina i componenti nel canale web della comunicazione interattiva secondo le esigenze e procedi alla loro configurazione.

   | Componenti | Funzionalità |
   |---|---|
   | Grafico | Aggiunge un grafico che è possibile utilizzare nella comunicazione interattiva per la rappresentazione visiva di dati bidimensionali recuperati da un insieme di modelli di dati del modulo. Per ulteriori informazioni, vedere [Utilizzo del componente grafico](../../forms/using/chart-component-interactive-communications.md). |
   | Frammento di documento | Consente di aggiungere un componente, testo, elenco o condizione riutilizzabile a una comunicazione interattiva. Il componente riutilizzabile aggiunto a una comunicazione interattiva potrebbe essere basato su un modello di dati modulo o senza un modello di dati modulo. |
   | Immagine | Consente di inserire un&#39;immagine. |
   | Pannello | Consente di aggiungere un [pannello](../../forms/using/create-interactive-communication.md#add-panel-component-to-the-web-channel) alla comunicazione interattiva. |
   | Tabella | Aggiunge una tabella che consente di organizzare i dati in righe e colonne. |
   | Area di destinazione | Inserisce un&#39;area di destinazione in un canale web per organizzare i componenti specifici del canale web. L’area di destinazione è un contenitore semplice che consente di raggruppare componenti specifici per il canale web. |
   | Testo | Aggiunge testo formattato al canale web di una comunicazione interattiva. Il testo può inoltre utilizzare oggetti modello dati modulo per rendere dinamico il contenuto. |
   | Pulsante | Consente di aggiungere un [pulsante](../../forms/using/create-interactive-communication.md#add-button-component-to-the-web-channel) alla comunicazione interattiva. Puoi utilizzare il componente Pulsante per passare ad altre comunicazioni interattive, moduli adattivi, altre risorse come immagini o frammenti di documenti o un URL esterno. |
   | Separatore | Consente di inserire una linea orizzontale in una comunicazione interattiva. Utilizza questo componente per distinguere le sezioni in una corrispondenza. Ad esempio, è possibile utilizzare il componente Separatore per distinguere le sezioni Dettagli cliente e Dettagli carta di credito in un estratto conto relativo a una carta di credito. |

1. Se necessario, inserisci le risorse nel canale web.

   Puoi [visualizzare in anteprima la tua comunicazione interattiva](#previewic) per vedere come si presentano gli output di stampa e web della comunicazione interattiva e continuare ad apportare modifiche, come richiesto.

## Anteprima della comunicazione interattiva {#previewic}

È possibile utilizzare l&#39;opzione **Anteprima** per valutare l&#39;aspetto della comunicazione interattiva. Il canale web di comunicazione interattiva fornisce anche un’opzione per emulare l’esperienza di una comunicazione interattiva per vari dispositivi. Ad esempio, iPhone, iPad e Desktop. Puoi utilizzare entrambe le opzioni **Anteprima** e **Emulatore** ![righello](assets/ruler.png) insieme per visualizzare in anteprima gli output Web per dispositivi con dimensioni di schermo diverse. I dati di esempio nell’anteprima vengono compilati dal modello dati dei moduli specificato.

1. Seleziona il canale (stampa o web) per l’anteprima e seleziona anteprima. Viene visualizzata la comunicazione interattiva.

   >[!NOTE]
   >
   >L’anteprima viene compilata con i dati di esempio del modello dati del modulo specificato. Per ulteriori informazioni sulla visualizzazione in anteprima della comunicazione interattiva con altri dati o sull&#39;utilizzo del servizio di precompilazione, vedere [Utilizzare il modello dati del modulo](/help/forms/using/using-form-data-model.md) e [Utilizzare il modello dati del modulo](/help/forms/using/work-with-form-data-model.md).

1. Per il canale web, utilizza ![righello](assets/ruler.png) per visualizzare l&#39;aspetto della comunicazione interattiva su vari dispositivi.

   ![webchannelpreview](assets/webchannelpreview.png)

Inoltre, puoi [Preparare e inviare comunicazioni interattive utilizzando l&#39;interfaccia utente agente](/help/forms/using/prepare-send-interactive-communication.md).

## Configurare le proprietà nella comunicazione interattiva  {#configure-properties-in-interactive-communication}

### Allegati e accesso alla libreria {#attachmentslibrary}

Nel canale di stampa, puoi configurare gli allegati e l’accesso alla libreria per consentire all’agente di gestire gli allegati nell’interfaccia utente dell’agente per la comunicazione interattiva:

1. Nel canale di stampa, evidenziare Contenitore documenti e selezionare **Proprietà**.

   ![documentcontainerproperties](assets/documentcontainerproperties.png)

   Il pannello Proprietà viene visualizzato nella barra laterale.

   ![propertiestachments](assets/propertiesattachments.png)

1. Espandere **Allegati** e specificare le proprietà seguenti:

   * **[!UICONTROL Consenti accesso alla libreria]**: selezionare questa opzione per abilitare l&#39;accesso alla libreria per l&#39;agente nell&#39;interfaccia utente agente. Se questa opzione è abilitata, l’agente può aggiungere file dalla libreria durante la preparazione della comunicazione interattiva.
   * **[!UICONTROL Consenti riordinamento degli allegati]**: selezionare questa opzione per consentire all&#39;agente di riordinare gli allegati con la comunicazione interattiva.
   * **[!UICONTROL Numero massimo di allegati consentiti]**: specifica il numero massimo di allegati consentiti con la comunicazione interattiva.
   * **[!UICONTROL File da allegare]**: selezionare **[!UICONTROL Aggiungi]**, quindi selezionare i file da allegare e specificare quanto segue:

      * **[!UICONTROL Allega il file al documento per impostazione predefinita]**: è possibile modificare questa opzione se solo l&#39;allegato non è obbligatorio.
      * **[!UICONTROL Obbligatorio:]** l&#39;agente non sarà in grado di rimuovere l&#39;allegato nell&#39;interfaccia utente dell&#39;agente.

   ![file allegati](assets/attachfiles.png)

1. Seleziona **[!UICONTROL Fine]**.

### Proprietà campo XDP/Layout {#xdplayoutfieldproperties}

1. Durante la modifica del canale di stampa di una comunicazione interattiva, passa il cursore su un campo integrato nel modello del canale di stampa e seleziona ![configure_icon](assets/configure_icon.png) (Configura).

   La finestra di dialogo Proprietà viene visualizzata nella barra laterale.

   ![data_display_pattern_fields](assets/data_display_patterns_fields.jpg)

1. Specifica quanto segue:

   * **[!UICONTROL Nome]**: nome nodo JCR.
   * **[!UICONTROL Titolo]**: immetti un titolo che sarà visibile all&#39;agente nell&#39;interfaccia utente dell&#39;agente e nella struttura Contenitore documenti.
   * **[!UICONTROL Tipo di associazione]**: selezionare uno dei tipi di associazione seguenti per il campo.

      * Nessuno: l&#39;agente immetterà il valore della proprietà.
      * Frammento di testo: se selezionata, puoi sfogliare e selezionare un frammento di documento di testo il cui contenuto viene renderizzato nel campo. In alternativa, trascina il frammento del documento di testo sul nome del campo per impostare l’associazione tra di essi. Il frammento di documento di testo non deve contenere variabili.
      * Oggetto modello dati: selezionare una proprietà del modello dati del modulo il cui valore viene popolato nel campo. In alternativa, selezionare la scheda **Origini dati** e trascinare la proprietà nel campo.

   * **[!UICONTROL Valori predefiniti]**: il valore predefinito garantisce che il campo non sia vuoto se non è stato fornito alcun valore dall&#39;oggetto modello dati o dal frammento di testo specificato. Se il tipo di associazione dati è none, il valore predefinito viene precompilato nel campo.
   * **[!UICONTROL Pattern di visualizzazione]**: è inoltre possibile definire un formato di visualizzazione per un campo. Selezionare una delle opzioni predefinite dall&#39;elenco a discesa **Tipo** per applicare un formato di visualizzazione a un campo. Selezionare **Personalizzato** per definire un modello di visualizzazione non disponibile nell&#39;elenco. Per ulteriori informazioni, vedere [Modelli di visualizzazione dei dati](../../forms/using/create-interactive-communication.md#datadisplaypatterns)

   * **[!UICONTROL Modificabile dall&#39;agente]**: selezionare questa opzione per consentire all&#39;agente di modificare il valore nel campo dell&#39;interfaccia utente agente. Questa impostazione non è applicabile se il tipo di associazione è Frammento di testo.
   * **[!UICONTROL Etichetta]**: specificare una stringa di testo visualizzata con il campo per l&#39;agente nell&#39;interfaccia utente agente. Questa impostazione non è applicabile se il tipo di associazione è Frammento di testo.
   * **[!UICONTROL Descrizione]**: immetti una stringa di testo che sarà visibile al passaggio del mouse sull&#39;agente nell&#39;interfaccia utente agente. Questa impostazione non è applicabile se il tipo di associazione è Frammento di testo.
   * **[!UICONTROL Obbligatorio]**: selezionare questa opzione per rendere obbligatorio il campo per l&#39;agente. Questa impostazione non è applicabile se il tipo di associazione è Frammento di testo.
   * **[!UICONTROL Consenti più righe]**: selezionare questo campo per consentire l&#39;immissione di più righe di testo nel campo. Questa impostazione non è applicabile se il tipo di associazione è Frammento di testo.

1. Seleziona ![icona_completato](assets/done_icon.png).

### Modelli di visualizzazione dei dati {#datadisplaypatterns}

L’interfaccia di authoring consente di definire modelli di visualizzazione dei dati per campi, variabili ed elementi del modello dati del modulo disponibili durante la creazione di una comunicazione interattiva per i canali di stampa e web.

Per configurare il pattern di visualizzazione dei dati, seleziona l&#39;elemento, seleziona ![configure_icon](assets/configure_icon.png) (Configura) e imposta il pattern di visualizzazione nel pannello **[!UICONTROL Properties]** nella barra laterale. Selezionare un&#39;opzione predefinita dall&#39;elenco a discesa **[!UICONTROL Tipo]** per visualizzare il modello associato al tipo selezionato. Selezionare **[!UICONTROL Personalizzato]** dall&#39;elenco a discesa **[!UICONTROL Tipo]** per definire un modello non disponibile nell&#39;elenco. La modifica dei valori nel campo **[!UICONTROL Pattern]** comporta la modifica automatica del tipo in **[!UICONTROL Personalizzato]**.

Per applicare il modello di visualizzazione, il numero di caratteri o cifre definito nel campo Pattern deve corrispondere o superare i caratteri o le cifre definiti nel valore per campi, variabili ed elementi del modello dati del modulo. Per ulteriori informazioni, vedere [esempio](../../forms/using/create-interactive-communication.md#greaternumberofdigits).

![esempio_pattern_visualizzazione_dati](assets/data_display_patterns_ssn_new.png)

Puoi ridefinire il pattern di visualizzazione per un campo, una variabile o un elemento del modello dati del modulo dopo aver generato il contenuto web dal canale di stampa. Di conseguenza, un elemento può avere diversi modelli di visualizzazione definiti per la stampa e i canali web. Se non si definisce un modello di visualizzazione per un elemento nel canale di stampa e si genera automaticamente contenuto Web utilizzando il canale di stampa, l&#39;associazione dati definita per l&#39;elemento nel canale di stampa definisce le opzioni del modello di visualizzazione disponibili nell&#39;elenco a discesa **[!UICONTROL Tipo]**. Se non è stata definita alcuna associazione per l&#39;elemento, il tipo di dati dell&#39;elemento definisce le opzioni disponibili per il motivo di visualizzazione. Ad esempio, se si crea un&#39;associazione dati di tipo Number per un elemento nel canale di stampa, le opzioni del modello di visualizzazione disponibili nell&#39;elenco a discesa **[!UICONTROL Tipo]** sono di tipo Number in vari formati.

Passa alla modalità **Anteprima** o apri l&#39;interfaccia utente agente per visualizzare il modello di visualizzazione applicato a questi elementi.

Nella tabella seguente è riportato un esempio dei valori visualizzati in seguito all&#39;impostazione del modello di visualizzazione dei dati per una variabile:

| Tipo | Valore predefinito | Pattern di visualizzazione | Valore visualizzato | Descrizione |
|---|---|---|---|---|
| Codice fiscale | 123456789 | testo{999-99-9999} | 123 45 6789 | Il numero di cifre nel campo del valore predefinito corrisponde al numero di cifre nel campo Pattern. Il valore basato sul modello viene visualizzato correttamente. |
| Codice fiscale | 1234567 | testo{999-99-9999} | 1-23-4567 | Il numero di cifre nel campo del valore predefinito è inferiore al numero di cifre nel campo Pattern. Il modello si applica alle 7 cifre disponibili. |
| Codice fiscale | 1234567890 | testo{999-99-9999} | 1234567890 | Il numero di cifre nel campo del valore predefinito è maggiore del numero di cifre nel campo Pattern. Di conseguenza, il valore visualizzato non cambia. |

Se non viene specificato un modello di visualizzazione per una variabile o un elemento del modello dati del modulo, per impostazione predefinita viene utilizzata la [configurazione globale del frammento di documento](https://helpx.adobe.com/it//experience-manager/6-5/forms/using/interactive-communication-configuration-properties.html).

Se non si applica un motivo di visualizzazione a una variabile di tipo numerico, nell&#39;anteprima di stampa il motivo viene visualizzato in base alla configurazione globale del frammento di documento. Se si applicano modifiche alla configurazione globale predefinita del frammento di documento, il modello viene comunque visualizzato nell’interfaccia utente dell’agente in base ai separatori predefiniti definiti per le impostazioni internazionali.

Analogamente, per i campi, se non viene specificato un pattern di visualizzazione, al campo viene applicato il pattern definito durante la creazione del modello di stampa (XDP). Se non è presente alcun motivo durante la creazione del modello di stampa, ai campi vengono applicati i motivi predefiniti basati sulle specifiche XFA.

Inoltre, se il modello di visualizzazione specificato non è corretto o non può essere applicato, i modelli predefiniti basati sulle specifiche XFA vengono applicati ai campi, alle variabili o agli elementi del modello dati del modulo.

## Applicare le regole ai componenti di comunicazione interattiva {#rules}

Per condizionare componenti o contenuti nella comunicazione interattiva, seleziona il componente o la parte di contenuto e seleziona ![createruleicon](assets/createruleicon.png) (Crea regola) per avviare l&#39;editor di regole.

Per ulteriori informazioni, consulta:

* [Editor regole](/help/forms/using/rule-editor.md)
* [Introduzione all’authoring di comunicazioni interattive](/help/forms/using/introduction-interactive-communication-authoring.md)

## Utilizzo delle tabelle {#tables}

### Tabelle dinamiche nella comunicazione interattiva {#dynamic-tables-in-interactive-communication}

È possibile aggiungere tabelle dinamiche in Comunicazione interattiva utilizzando frammenti di layout. I passaggi seguenti utilizzano un esempio di estratto conto relativo a una carta di credito per illustrare l’utilizzo di un frammento di layout per la creazione di una tabella dinamica in una comunicazione interattiva.

1. Assicurati che il frammento di layout richiesto per la creazione della tabella sia disponibile in AEM.
1. Nel canale di stampa della comunicazione interattiva, trascina e rilascia un frammento di layout (con una tabella a più colonne) in un’area di destinazione dal browser Risorse.

   ![lf_dragdrop](assets/lf_dragdrop.png)

   Nell&#39;area di layout Comunicazione interattiva viene visualizzata una tabella.

   ![lf_dragdrop_table](assets/lf_dragdrop_table.png)

1. Specificare l&#39;associazione dati per ciascuna cella della tabella. Per creare una riga ripetibile, inserire le proprietà del modello dati del modulo nella riga che appartiene a una proprietà di raccolta comune.

   1. Selezionare una cella nella tabella e selezionare ![configure_icon](assets/configure_icon.png) (Configura).

      La finestra di dialogo Proprietà viene visualizzata nella barra laterale.

      ![lf_cell_properties](assets/lf_cell_properties.png)

   1. Configura le proprietà:

      * **[!UICONTROL Nome]**: nome nodo JCR.
      * **[!UICONTROL Titolo]**: immetti un titolo che sarà visibile nell&#39;editor di comunicazione interattiva.
      * **[!UICONTROL Tipo di associazione]**: selezionare uno dei tipi di associazione seguenti per il campo.

         * **[!UICONTROL Nessuno]**
         * **[!UICONTROL Oggetto modello dati]**: il valore di una proprietà modello dati modulo è popolato nel campo. In alternativa, selezionare la scheda **Origini dati** e trascinare la proprietà nel campo.

      * **[!UICONTROL Oggetto modello dati]**: proprietà del modello dati del modulo il cui valore è popolato nel campo.
      * **[!UICONTROL Valore predefinito]**: il valore predefinito garantisce che il campo non sia vuoto se non è stato fornito alcun valore dall&#39;oggetto modello dati specificato. Il valore predefinito viene inserito automaticamente nel campo.

      * **[!UICONTROL Modificabile dall&#39;agente]**: selezionare questa opzione per consentire all&#39;agente di modificare il valore nel campo dell&#39;interfaccia utente agente.

   1. Seleziona ![icona_completato](assets/done_icon.png).

1. Visualizza l’anteprima della comunicazione interattiva per visualizzare la tabella con i dati sottoposti a rendering.

   ![lf_preview](assets/lf_preview.png)

### Tabelle solo per canale web {#webchanneltables}

Selezionare il pannello principale nel modello Web e selezionare **+** per aggiungere un componente **Tabella** alla comunicazione interattiva. Nella comunicazione interattiva viene inserita una tabella comprendente due righe. La prima riga della tabella rappresenta l’intestazione della tabella.

#### Aggiungere righe e colonne alla tabella {#addrowscolumnstable}

**Per aggiungere o eliminare colonne:**

1. Seleziona la casella di testo predefinita nella riga di intestazione della tabella per visualizzare la barra degli strumenti del componente.
1. Selezionare **Aggiungi colonna** o **Elimina colonna** per aggiungere o eliminare le colonne della tabella.

![tabella_barra_degli_strumenti_componente1](assets/component_toolbar_table1.png)

**Per aggiungere o eliminare righe:**

1. Seleziona una delle righe della tabella per visualizzare la barra degli strumenti del componente. Puoi anche selezionare una riga di tabella utilizzando il Browser contenuto nella barra laterale della comunicazione interattiva.
1. Selezionare **Aggiungi riga** o **Elimina riga** per aggiungere o eliminare righe di tabella. Utilizza le opzioni **Sposta su** e **Sposta giù** disponibili nella barra degli strumenti per ridisporre le righe nella tabella.

![Barra degli strumenti del componente](assets/component_toolbar_table_row_new.png)

**A.** Aggiungi riga **B.** Elimina riga **C.** Sposta in alto **D.** Sposta in basso

#### Aggiungere o modificare testo nelle celle di tabella {#addedittexttable}

1. Selezionare la casella di testo predefinita nella cella della tabella e selezionare ![modifica](assets/edit.png) (Modifica).
1. Digita il testo nella cella della tabella e seleziona ![icona_fine](assets/done_icon.png) per salvarlo.

#### Creare un&#39;associazione tra celle di tabella ed elementi oggetto modello dati {#createbindingtablecells}

1. Selezionare la casella di testo predefinita nella riga di tabella e selezionare ![modifica](assets/edit.png) (Modifica).
1. Seleziona l’elenco a discesa Oggetti modello dati e fai clic sulla proprietà.
1. Selezionare questa opzione per salvare e creare un&#39;associazione tra la cella della tabella e la proprietà dell&#39;oggetto modello dati.

![Crea associazione dati](assets/create_data_binding_table_new.png)

#### Creare un collegamento ipertestuale per il testo nella cella della tabella {#createhyperlinktable}

1. Selezionare la casella di testo predefinita nella cella della tabella e selezionare ![modifica](assets/edit.svg) (Modifica).
1. Selezionare il testo nella cella della tabella e l&#39;icona Collegamento ipertestuale.
1. Specifica l&#39;URL nel campo **Percorso**.
1. Seleziona ![done_icon](assets/done_icon.png) per salvare le proprietà del collegamento ipertestuale.

![Crea collegamento ipertestuale](assets/create_hyperlink_table_new.png)

#### Creare tabelle dinamiche {#createdynamictables}

Puoi creare una tabella dinamica solo per il canale web in una comunicazione interattiva utilizzando una proprietà del modello di dati di tipo raccolta. Tale tabella rappresenta le proprietà figlio di una proprietà di insieme. È possibile modificare solo le proprietà di formattazione delle varie celle della tabella.

1. Passare al canale Web, quindi scegliere di visualizzare il browser Origini dati.
1. Trascinare una proprietà di raccolta in una sottomaschera. Viene creata una tabella nella sottomaschera.
1. Visualizza l’anteprima della tabella nell’anteprima web della comunicazione interattiva.

#### Ordinare le colonne in una tabella {#sortcolumns}

Nella comunicazione interattiva puoi ordinare i dati in base a qualsiasi colonna di una tabella. I valori nella colonna possono essere ordinati in ordine crescente o decrescente.

L’ordinamento può essere applicato alle colonne delle tabelle contenenti:

* Testo statico
* Proprietà oggetto modello dati
* Combinazione di testo statico e proprietà dell’oggetto modello dati

Per abilitare l&#39;ordinamento:

1. Selezionare la tabella e selezionare ![configure_icon](assets/configure_icon.png) (Configura). Puoi anche selezionare la tabella utilizzando il browser **Contenuto** nella barra laterale della comunicazione interattiva.
1. Seleziona **Abilita ordinamento.**
1. Seleziona ![done_icon](assets/done_icon.png) per salvare le proprietà della tabella. Le icone di ordinamento, frecce verso l’alto o il basso, nelle intestazioni di colonna indicano che l’ordinamento è stato abilitato.

   ![Abilita ordinamento](assets/enable_sorting_new-1.png)

1. Passa alla modalità **Anteprima** per visualizzare l&#39;output. La tabella viene ordinata automaticamente in base alla prima colonna della tabella.
1. Fai clic sull’intestazione della colonna per ordinare i valori in base alla colonna.

   Un’intestazione di colonna con una freccia su indica che:

   * tabella è ordinata in base a tale colonna.
   * i valori nella colonna vengono visualizzati in ordine crescente.

   ![Ordinamento crescente](assets/sorting_ascending_new-1.png)

   Analogamente, un&#39;intestazione di colonna con una freccia in giù indica che i valori nella colonna vengono visualizzati in ordine decrescente.

## Modificare le proprietà di comunicazione interattiva {#edit-interactive-communication-properties}

Dopo aver creato una comunicazione interattiva, puoi modificarne le proprietà in una fase successiva.

Utilizzare la pagina **Proprietà** per:

* Modifica i valori per i campi specificati durante la creazione della comunicazione interattiva, ad esempio Titolo e Descrizione.
* Aggiungi o elimina un canale web per una comunicazione interattiva esistente.
* Visualizzare in anteprima, scaricare o eliminare la comunicazione interattiva
* Apri l&#39;[interfaccia utente agente](/help/forms/using/prepare-send-interactive-communication.md).

Per accedere alla pagina **Proprietà**:

1. Accedi all&#39;istanza di creazione dell&#39;AEM e passa a **Adobe Experience Manager** > **Forms** > **Forms e documenti**.
1. Selezionare la comunicazione interattiva e selezionare **Proprietà**.
1. Selezionare la scheda **Generale** per modificare i campi **Titolo** e **Descrizione**.

### Aggiungere o eliminare il canale Web {#add-or-delete-the-web-channel}

Per aggiungere il canale web per una comunicazione interattiva esistente, effettua le seguenti operazioni:

1. Nella pagina **Proprietà** selezionare la scheda **Canali**.
1. Selezionare la casella di controllo **Web** e selezionare un modello per il canale Web.
1. Selezionare **Utilizza Stampa come master per il canale Web** per abilitare la sincronizzazione tra il canale Web e il canale di stampa.
1. Seleziona **Salva e chiudi** per salvare le modifiche.

   Analogamente, è possibile selezionare la casella di controllo **Web** nella scheda **Canali** per eliminare il canale Web dalla comunicazione interattiva.

## Aggiungi componente Pulsante al canale web {#add-button-component-to-the-web-channel}

Puoi aggiungere un pulsante come componente al canale web della comunicazione interattiva. Definisci le regole utilizzando l&#39;[editor di regole](../../forms/using/rule-editor.md) per passare ad altre comunicazioni interattive, moduli adattivi, altre risorse come immagini o frammenti di documenti oppure un URL esterno nella selezione del pulsante.

Per aggiungere un pulsante e definirne le regole:

1. Selezionare il pannello principale nel modello Web e selezionare **+** per aggiungere il componente **Button** alla comunicazione interattiva.
1. Seleziona il componente pulsante e seleziona ![edit-rules](assets/edit-rules.png) per definire le regole sulla selezione del pulsante.
1. Nella sezione **When**, seleziona **clicked** dallo stato dell&#39;elenco a discesa del pulsante.
1. Nella sezione **Then**:

   1. Seleziona un’azione dall’elenco a discesa. Selezionare ad esempio **Accedi a** come tipo di azione.

   1. Specifica l’URL della comunicazione interattiva, del modulo adattivo, di una risorsa o di una pagina web. Ad esempio, specifica l’URL nel formato seguente per passare a un’altra comunicazione interattiva: https://&lt;nome-server>:&lt;porta>/editor.html/content/forms/af/&lt;nome comunicazione interattiva>/channels/&lt;nome canale - print or web>.html
   1. Specifica l&#39;opzione per aprire la risorsa nella stessa scheda, nella nuova scheda o nella nuova finestra.
   1. Seleziona **Fine**, quindi seleziona **Chiudi** per salvare la regola.

   Allo stesso modo, puoi selezionare altre opzioni disponibili dall’elenco a discesa del tipo di azione, ad esempio Richiama servizio e Invia modulo. Per ulteriori informazioni, vedere [editor regole](../../forms/using/rule-editor.md).

1. Visualizzare l’anteprima della comunicazione interattiva e selezionare il pulsante per visualizzare la comunicazione interattiva, il modulo adattivo, una risorsa o una pagina web specificata al punto 4, lettera b).

## Aggiungi componente Pannello al canale web {#add-panel-component-to-the-web-channel}

Il componente Pannello è un segnaposto per raggruppare altri componenti e controlla il modo in cui un gruppo di componenti, come Pannello a soffietto e Schede, viene layout nella comunicazione interattiva. Un componente pannello consente inoltre di rendere un gruppo di componenti ripetibili per l’utente finale, ad esempio in più voci necessarie per compilare le credenziali educative.

Per aggiungere un componente Pannello al canale web, effettua le seguenti operazioni:

1. Inserire il componente **Pannello** nel canale Web utilizzando una delle opzioni seguenti:

   * Selezionare un componente, selezionare **+** e selezionare il componente **Pannello**.

   * Dal pannello del browser **Componente**, trascina il componente **Pannello** nella comunicazione interattiva.

   * Selezionare il **pannello** nel pannello del browser **Contenuto** e selezionare **Aggiungi pannello secondario**. Selezionando l&#39;opzione **Aggiungi pannello figlio** viene visualizzata la finestra di dialogo **Aggiungi pannello figlio**. Immetti il titolo e una descrizione e un nome facoltativi per il componente Pannello.

1. Selezionare il pannello dal browser **Contenuto** per eseguire azioni aggiuntive sul pannello, ad esempio configurare, modificare regole, copiare, eliminare e inserire componenti.

   Puoi anche trascinare un pannello all&#39;interno del browser **Contenuto** per riflettere la modifica nella struttura della comunicazione interattiva nel riquadro di destra.

## Sincronizzazione del canale web con il canale di stampa {#synchronize}

Quando si seleziona Stampa come master per un canale web durante la creazione di una comunicazione interattiva, il canale web viene creato in sincronia con il canale di stampa e il contenuto e l&#39;associazione dati del canale web derivano dal canale di stampa e le modifiche apportate al canale di stampa potrebbero riflettersi nel canale web quando si seleziona Sincronizza.

Tuttavia, agli autori è consentito interrompere l’ereditarietà dei componenti nel canale web in base alle esigenze.

![Crea master di stampa](assets/create_ic_print_master_new-1.png) ![Stampa Web master](assets/create_ic_print_master_web_new-1.png)

### Sincronizzazione automatica {#autosync}

Se si seleziona l&#39;opzione **[!UICONTROL Usa stampa come master per canale Web]**, è possibile selezionare una delle modalità seguenti per generare il canale Web:

* **[!UICONTROL Layout automatico]**: selezionare questa modalità per generare automaticamente segnaposto, contenuto e associazione dati per il canale Web dal canale di stampa.
* **[!UICONTROL Organizza manualmente]**: seleziona questa modalità per selezionare e aggiungere manualmente gli elementi del canale di stampa al canale Web utilizzando il contenuto principale disponibile nella scheda Origini dati. Per ulteriori informazioni, vedere [Selezionare gli elementi del canale di stampa per creare il contenuto del canale Web](#selectprintchannelelements).

![Crea opzioni IC](assets/create_ic_options_updated_new.png)

>[!NOTE]
>
>La sincronizzazione dei canali sincronizza solo i frammenti di documento, le immagini, le condizioni, gli elenchi e i frammenti di layout dal canale di stampa al canale web. I sottomoduli o i nodi principali che includono tali elementi non vengono sincronizzati.

### Seleziona Stampa elementi canale per creare contenuti canale web {#selectprintchannelelements}

Se si seleziona Stampa come master durante la creazione della comunicazione interattiva e non si seleziona l&#39;opzione di sincronizzazione automatica, è anche possibile trascinare gli elementi del canale di stampa nell&#39;interfaccia di creazione del canale Web.

Passa a **Origini dati** > **Contenuto principale** per visualizzare gli elementi del canale di stampa. Trascinare le aree di destinazione, i campi o le tabelle nell&#39;interfaccia di creazione del canale Web. Un&#39;icona blu accanto al nome dell&#39;elemento indica che l&#39;elemento Canale di stampa è già stato incluso nel canale Web.

![Contenuto principale](assets/master_content.png)

### Annulla ereditarietà {#cancelinheritance}

Nel canale web, i componenti sono incorporati nelle aree di destinazione.

Passa il puntatore del mouse sull&#39;area di destinazione o sulla variabile rilevante nel canale Web e seleziona ![cancella ereditarietà](assets/cancelinheritance.png) (Annulla ereditarietà), quindi nella finestra di dialogo Annulla ereditarietà seleziona **[!UICONTROL Sì]**.

L’ereditarietà dei componenti all’interno dell’area di destinazione viene annullata e ora puoi modificarli in base alle esigenze.

### Riabilita ereditarietà {#re-enable-inheritance}

Nel canale web, se hai annullato l’ereditarietà di un componente, puoi riabilitarlo. Per riabilitare l&#39;ereditarietà, passa il cursore del mouse sul limite dell&#39;area di destinazione pertinente, che include il componente, quindi seleziona ![reenableinheritance](assets/reenableinheritance.png).

Viene visualizzata la finestra di dialogo Ripristina ereditarietà.

![revertinheritance](assets/revertinheritance.png)

Se necessario, selezionare **[!UICONTROL Sincronizza la pagina dopo il ripristino dell&#39;ereditarietà]**. Selezionare questa opzione per sincronizzare l&#39;intera comunicazione interattiva. Se non selezioni questa opzione, al ripristino dell’ereditarietà viene sincronizzata solo l’area di destinazione pertinente.

Selezionare **[!UICONTROL Sì]**.

### Sincronizza {#synchronize-1}

Se si utilizza Stampa come master per il canale Web e si modifica il canale Stampa, è possibile sincronizzare il contenuto per apportare le modifiche appena apportate al canale Web.

1. Per sincronizzare il canale Web con il canale di stampa, passa al canale Web e seleziona l’icona Altre opzioni.

   ![Opzioni di sincronizzazione automatica](assets/auto_sync_options_new.png)

1. Selezionare una delle opzioni seguenti:

   * **[!UICONTROL Sincronizza con Stampa]**: sincronizza il contenuto solo per le aree di destinazione in cui l&#39;ereditarietà non viene annullata.
   * **[!UICONTROL Ripristina]**: sincronizza il contenuto del canale Web con il canale di stampa e ignora tutte le modifiche apportate al canale Web.

### Utilizza la barra degli strumenti del componente per eseguire azioni sui componenti ereditati {#componenttoolbar}

Dopo aver generato automaticamente il contenuto nel canale web utilizzando l’opzione Sincronizza, puoi eseguire più azioni sui componenti senza annullare l’ereditarietà.

![Barra degli strumenti del componente](assets/component_toolbar_inherited_web_new.png)

Seleziona il componente per visualizzare le seguenti opzioni:

* **Copia:** Copia un componente e incollalo in altre posizioni nella comunicazione interattiva.
* **Taglia:** Sposta un componente da una posizione all&#39;altra nella comunicazione interattiva.
* **Inserisci componente:** Inserire un componente sopra il componente selezionato.
* **Incolla:** Incolla il componente tagliato o copiato utilizzando le opzioni descritte in precedenza.
* **Gruppo:** Selezionare più componenti se si desidera tagliare, copiare o incollare insieme più componenti.
* **Elemento padre:** Selezionare il padre di un componente.
* **Visualizza espressione SOM:** Visualizza [espressione SOM](../../forms/using/using-som-expressions-adaptive-forms.md) per il componente.

* **Raggruppa oggetti nel pannello:** Raggruppa i componenti in un pannello per poter eseguire operazioni su tali componenti contemporaneamente. Per ulteriori dettagli, vedere [Raggruppa oggetti nel pannello](#groupobjectspanel).

* **Annulla ereditarietà:** [Annulla l&#39;ereditarietà](#cancelinheritance) dei componenti all&#39;interno dell&#39;area di destinazione per modificarli.

### Raggruppa oggetti nel pannello {#groupobjectspanel}

L’interfaccia di authoring del canale web semplifica il raggruppamento dei componenti in un pannello per consentire l’esecuzione simultanea di operazioni su tali componenti. Nella scheda **Contenuto** sono elencati i componenti raggruppati come elementi secondari del pannello nella struttura del contenuto.

1. Selezionare un componente e selezionare l&#39;operazione Gruppo ( ![gruppo](assets/group.jpg)).
1. Selezionare più componenti e selezionare **Raggruppa oggetti nel pannello**.

   ![Oggetti di gruppo](assets/component_toolbar_group_objects_new.png)

1. Nella finestra di dialogo **Raggruppa oggetti nel pannello** immettere un nome per il pannello.
1. Immetti un titolo e una descrizione facoltativi per il pannello.
1. Fai clic su ![punto_di controllo](assets/bullet_checkmark.png).

   I componenti raggruppati vengono visualizzati come elementi secondari del pannello nella struttura del contenuto.

   ![raggruppamento_struttura_contenuto](assets/content_tree_grouping.png)

## Formato di output per il canale di stampa {#output-format-print-channel}

Utilizza l’API PrintChannel per definire il formato di output per il canale di stampa di una comunicazione interattiva. Se non definite un formato di output, AEM Forms genera l&#39;output in formato PDF.

```javascript
//options for rendering print channel of a multi-channel document
PrintChannelRenderOptions renderOptions = new PrintChannelRenderOptions();
PrintDocument printDocument = printChannel.render(renderOptions);
```

Per generare l&#39;output in qualsiasi altro formato, specificate il tipo di formato di output. Per un elenco dei tipi di formato di output supportati, fare riferimento a [API PrintChannel](https://helpx.adobe.com/it/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/PrintConfig.html).

Ad esempio, potete utilizzare l&#39;esempio seguente per definire PCL come formato di output per una comunicazione interattiva:

```javascript
//options for rendering print channel of a multi-channel document
PrintChannelRenderOptions renderOptions = new PrintChannelRenderOptions();
renderOptions.setRenderFormat(PrintConfig.HP_PCL_5e);
PrintDocument printDocument = printChannel.render(renderOptions);
```
