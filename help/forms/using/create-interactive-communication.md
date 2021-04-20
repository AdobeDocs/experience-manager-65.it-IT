---
title: Creare una comunicazione interattiva
seo-title: Creare una comunicazione interattiva
description: Crea una comunicazione interattiva utilizzando l’editor di comunicazioni interattive. Utilizza la funzionalità di trascinamento della selezione per creare la comunicazione interattiva e visualizzare in anteprima sia le uscite di stampa che quelle web su diversi tipi di dispositivi.
seo-description: Crea una comunicazione interattiva utilizzando l’editor di comunicazioni interattive. Utilizza la funzionalità di trascinamento della selezione per creare la comunicazione interattiva e visualizzare in anteprima sia le uscite di stampa che quelle web su diversi tipi di dispositivi.
uuid: d524a3de-00b4-444f-b3c7-be443fa24ec8
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f4d98cb9-84d8-4735-91d2-b9ceec861e5e
docset: aem65
feature: Interactive Communication
exl-id: 1f89c3bf-e67e-4d13-9285-3367be1ac8f8
translation-type: tm+mt
source-git-commit: 92092e1c050c9264c19e3cd9da9b240607af7bab
workflow-type: tm+mt
source-wordcount: '6212'
ht-degree: 1%

---

# Creare una comunicazione interattiva{#create-an-interactive-communication}

## Panoramica {#overview}

Le comunicazioni interattive centralizzano e gestiscono la creazione, l&#39;assemblaggio e la distribuzione di corrispondenze personalizzate e interattive. Utilizza la stampa come canale principale per il web, per ridurre al minimo le duplicazioni nella creazione dell&#39;output web della comunicazione interattiva.

### Prerequisiti {#prerequisites}

Di seguito sono riportati i prerequisiti per la creazione di una comunicazione interattiva:

* Imposta un [modello dati modulo](/help/forms/using/data-integration.md) contenente dati di prova o con un’origine dati effettiva, ad esempio un’istanza di Microsoft® Dynamics.
* Assicurati di disporre dei [Frammenti documento](/help/forms/using/document-fragments.md).
* Assicurati di disporre di [Modelli per la stampa e il canale web](/help/forms/using/web-channel-print-channel.md).
* Assicurati di disporre del [tema](/help/forms/using/themes.md) richiesto per il canale web.

## Crea comunicazione interattiva {#createic}

1. Accedi all&#39;istanza di authoring AEM e passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp; Documents]**.
1. Tocca **[!UICONTROL Crea]** e seleziona **[!UICONTROL Comunicazione interattiva]**. Viene visualizzata la pagina Crea comunicazione interattiva .

   ![create-interattivo-communication](assets/create-interactive-communication.png)

1. Inserite le seguenti informazioni. :

   * **[!UICONTROL Titolo]**: Inserisci il titolo della comunicazione interattiva.
   * **[!UICONTROL Nome]**: Il nome della comunicazione interattiva viene derivato dal titolo inserito. Se necessario, modificalo.
   * **[!UICONTROL Descrizione]**: Immettere una descrizione della comunicazione interattiva.
   * **[!UICONTROL Modello]** dati modulo: Individuare e selezionare il modello dati del modulo. Per ulteriori informazioni su Form Data Model, vedere [Integrazione dei dati di AEM Forms](/help/forms/using/data-integration.md).

   * **[!UICONTROL Servizio]** di precompilazione: Seleziona il servizio di precompilazione per recuperare i dati e precompilare la comunicazione interattiva.
   * **[!UICONTROL Tipo]** di post-processo: È possibile selezionare AEM o il flusso di lavoro Forms da attivare quando viene inviata la comunicazione interattiva. Seleziona il tipo di flusso di lavoro da attivare.

   * **[!UICONTROL Processo]** post: Seleziona il nome del flusso di lavoro da attivare. Quando si seleziona AEM flusso di lavoro, specificare Percorso allegato, Percorso layout, Percorso PDF, Percorso dati di stampa e Percorso dati Web.
   * **[!UICONTROL Tag]**: Selezionare i tag da applicare alla comunicazione interattiva. Puoi anche digitare un nome di tag nuovo/personalizzato e premere Invio per crearlo.
   * **[!UICONTROL Autore]**: il nome dell’autore viene automaticamente prelevato dal nome utente dell’utente connesso.
   * **[!UICONTROL Data di pubblicazione:]** immetti la data di pubblicazione della comunicazione interattiva.
   * **[!UICONTROL Data]** di annullamento pubblicazione: Immettere la data per annullare la pubblicazione della comunicazione interattiva.

1. Tocca **[!UICONTROL Avanti]**. Viene visualizzata la schermata per specificare i dettagli del canale web e di stampa.
1. Immetti quanto segue:

   * **[!UICONTROL Stampa]**: Selezionare questa opzione per generare il canale di stampa della comunicazione interattiva.
   * **[!UICONTROL Modello]** di stampa: Sfoglia e seleziona un XDP come modello di stampa.
   * **[!UICONTROL Web]**: Selezionare questa opzione per generare il canale web o l’output dinamico della comunicazione interattiva.
   * **[!UICONTROL Modello]** Web di comunicazione interattiva: Sfoglia e seleziona il modello web.
   * **** Tema e  **[!UICONTROL seleziona tema]**: Sfoglia e seleziona il tema per personalizzare lo stile del canale web della comunicazione interattiva. Per ulteriori informazioni, consulta [Temi in AEM Forms](/help/forms/using/themes.md).

   * **[!UICONTROL Utilizzare Stampa come master per il canale]** Web: Selezionare questa opzione per creare il canale web sincronizzato con il canale di stampa. L&#39;utilizzo del canale di stampa come master per il canale web assicura che il contenuto e il binding dei dati del canale web siano derivati dal canale di stampa e che le modifiche apportate al canale di stampa si riflettano nel canale web quando si tocca Sincronizza. Tuttavia, gli autori possono interrompere l’ereditarietà di componenti specifici nel canale web, a seconda delle necessità. Per ulteriori informazioni, vedere [Sincronizzare il canale Web con il canale di stampa](../../forms/using/create-interactive-communication.md#synchronize).
Se si seleziona l&#39;opzione **[!UICONTROL Usa stampa come master per il canale Web]**, è possibile selezionare una delle seguenti modalità per generare il canale Web:

      * **[!UICONTROL Layout]** automatico: Selezionare questa modalità per generare automaticamente segnaposti, contenuti e binding dei dati per il canale Web dal canale Stampa.
      * **[!UICONTROL Organizza]** manualmente: Selezionare questa modalità per selezionare e aggiungere manualmente gli elementi del canale Stampa al canale Web utilizzando il contenuto principale disponibile nella scheda  **[!UICONTROL Data]** Sourcestab. Per ulteriori informazioni, consulta [Selezionare gli elementi del canale di stampa per creare il contenuto del canale Web](#selectprintchannelelements).

   Per ulteriori informazioni sul canale di stampa e sul canale web, vedere [Canale di stampa e canale web](/help/forms/using/web-channel-print-channel.md).

1. Tocca **[!UICONTROL Crea]**. Viene creata la comunicazione interattiva e viene visualizzata una finestra di avviso. Tocca **[!UICONTROL Modifica]** per iniziare a creare il contenuto della comunicazione interattiva, come spiegato in [Aggiungi il contenuto utilizzando l&#39;interfaccia utente per l&#39;authoring delle comunicazioni interattive](#step2). In alternativa, è possibile toccare **[!UICONTROL Fine]** e scegliere di modificare la comunicazione interattiva in un secondo momento.

## Aggiungere contenuto alla comunicazione interattiva {#step2}

Dopo aver creato una comunicazione interattiva, puoi utilizzare l’interfaccia di creazione della comunicazione interattiva per crearne i contenuti.

Per ulteriori informazioni sull&#39;interfaccia di authoring delle comunicazioni interattive, vedere [Introduzione all&#39;authoring delle comunicazioni interattive](/help/forms/using/introduction-interactive-communication-authoring.md).

1. L&#39;interfaccia di creazione delle comunicazioni interattive viene avviata quando tocchi Modifica come indicato in [Crea comunicazione interattiva](#createic). In alternativa, puoi passare a una risorsa di comunicazione interattiva esistente su AEM, selezionarla e toccare **[!UICONTROL Modifica]** per avviare l’interfaccia di creazione di comunicazioni interattive.

   Per impostazione predefinita, viene visualizzato il canale di stampa della comunicazione interattiva, a meno che la comunicazione interattiva non sia solo un canale web. Il canale Stampa della comunicazione interattiva visualizza le aree di destinazione, come disponibile nel modello di canale XDP/print selezionato. In queste aree e campi di destinazione, puoi aggiungere componenti o risorse.

1. Con il canale di stampa selezionato, selezionare la scheda **[!UICONTROL Componenti]** . I seguenti componenti sono disponibili nel canale di stampa:

   | **Componente** | **Funzionalità** |
   |---|---|
   | Grafico | Aggiunge un grafico che è possibile utilizzare nella comunicazione interattiva per la rappresentazione visiva dei dati bidimensionali recuperati da una raccolta di modelli di dati del modulo. Per ulteriori informazioni, consulta [Uso dei grafici nelle comunicazioni interattive](/help/forms/using/chart-component-interactive-communications.md). |
   | Frammento di documento | Consente di aggiungere un componente riutilizzabile, ad esempio testo, elenco o condizione, a una comunicazione interattiva. Il componente aggiunto può essere basato su modelli di dati modulo o senza un modello di dati modulo. |
   | Immagine | Consente di inserire un’immagine. |

   Trascina i componenti nella comunicazione interattiva e configurali in base alle tue esigenze.

   È inoltre possibile utilizzare le operazioni Annulla e Ripristina durante la creazione di una comunicazione interattiva per i canali Stampa e Web.

   Utilizzare l’operazione di annullamento per eliminare l’ultima azione eseguita e l’operazione Ripristina per incorporare di nuovo l’azione scartata. Ad esempio, se hai inserito un’immagine o creato un binding di dati in una comunicazione interattiva e devi eliminarla, utilizza l’operazione di annullamento.

   ![Annulla Ripeti azioni](assets/undo_redo_actions_new.png)

   Le opzioni Annulla e Ripristina sono visualizzate nella barra degli strumenti dell’interfaccia utente di authoring. L’opzione Annulla viene visualizzata solo dopo l’esecuzione di un’azione. L’opzione Ripristina viene visualizzata sulla barra degli strumenti della pagina solo dopo un’operazione di annullamento. Queste azioni vengono reimpostate all’aggiornamento della pagina.

1. Con il canale di stampa selezionato, vai alla scheda **[!UICONTROL Risorse]** e applica il filtro per visualizzare solo le risorse che desideri visualizzare.

   Utilizzando il browser Risorse, puoi anche trascinare e rilasciare risorse direttamente nelle aree di destinazione di Comunicazione interattiva.

   ![assets-docfragments](assets/assets-docfragments.png)

1. Trascina i frammenti del documento nella comunicazione interattiva. Di seguito sono riportati i tipi di frammenti di documento che è possibile utilizzare nel canale di stampa della comunicazione interattiva.

<table>
 <tbody>
  <tr>
   <td><strong>Tipo frammento documento</strong></td>
   <td><strong>Scopo di esempio</strong></td>
  </tr>
  <tr>
   <td><a href="/help/forms/using/texts-interactive-communications.md" target="_blank">Testo</a></td>
   <td>Testo per aggiungere indirizzo, e-mail del destinatario e testo del corpo della lettera </td>
  </tr>
  <tr>
   <td><a href="/help/forms/using/conditions-interactive-communications.md" target="_blank">Condizione</a></td>
   <td>Condizione per aggiungere l’immagine di intestazione appropriata alla comunicazione in base al tipo di criterio: Standard o Premium. <br /> </td>
  </tr>
  <tr>
   <td>Elenco</td>
   <td>Gruppo di frammenti di documento, inclusi testo, condizioni, altri elenchi e immagini. <br /> </td>
  </tr>
 </tbody>
</table>

È inoltre possibile sostituire il binding tra un’area di destinazione e un frammento di documento rilasciando il nuovo frammento nell’area di destinazione utilizzando la scheda **[!UICONTROL Risorse]**. L’ombreggiatura blu dell’area di destinazione durante il trascinamento indica che il frammento di documento può essere rilasciato nell’area di destinazione.

Per ulteriori informazioni sui frammenti di documento, vedere [Frammenti di documento](/help/forms/using/document-fragments.md).

L’interfaccia di authoring consente di distinguere tra campi e variabili non associati e associati all’interno di una comunicazione interattiva. L’interfaccia evidenzia i campi e le variabili non associati utilizzando un bordo arancione.

![unbound_fields_variables_highlight_dc](assets/unbound_fields_variables_highlights_dc.jpg)

Inoltre, quando passi il mouse su questi elementi, viene visualizzata una descrizione comandi con il messaggio Campo (non associato) o Variabile (non associato).

È possibile che talvolta nell’interfaccia di authoring non venga visualizzata una variabile non associata utilizzata in un frammento di documento. Può verificarsi a causa di una regola di testo in linea all’interno di un frammento di documento o nel caso di un frammento di condizione. In questi casi, una descrizione comandi, evidenziata in blu, viene visualizzata come parte del frammento di documento. La descrizione comando visualizza il numero di variabili non associate utilizzate all’interno di un frammento di documento.

![Variabile non associata](assets/df_unbound_variable_new.png)

Toccare il frammento di documento, toccare ![configure_icon](assets/configure_icon.png) (Configura), quindi toccare **[!UICONTROL Properties]** dalla barra laterale della comunicazione interattiva. La sezione **[!UICONTROL Variabili e oggetti modello dati]** elenca le variabili, incluse le variabili nascoste, e gli oggetti modello dati utilizzati nei frammenti di documento. Utilizza l&#39;icona ![modifica](assets/edit.svg) (Modifica) accanto a ciascun oggetto o variabile del modello dati per modificare le proprietà.

1. Per impostare il binding delle variabili, toccare una variabile e selezionare ![configure_icon](assets/configure_icon.png) (Configura), quindi impostare le proprietà di binding nel pannello Proprietà nella barra laterale.

   * **Nessuno**: L&#39;agente compilerà il valore della variabile.
   * **Frammento** di testo: Se questa opzione è selezionata, è possibile sfogliare e selezionare un frammento di documento di testo il cui contenuto è sottoposto a rendering nel campo. Solo i frammenti di documento di testo possono essere associati a variabili prive di variabili.
   * **Oggetto** modello dati: Selezionare una proprietà del modello dati del modulo il cui valore viene compilato nel campo .
   * **Valore predefinito:** puoi definire un valore predefinito per la variabile utilizzando questo campo. Il valore viene visualizzato quando si visualizza l&#39;anteprima della comunicazione interattiva o nell&#39;interfaccia utente dell&#39;agente.
   * **Pattern di visualizzazione:** puoi anche definire un formato di visualizzazione per una variabile. Seleziona una delle opzioni predefinite dall&#39;elenco a discesa **Tipo** per applicare un formato di visualizzazione a una variabile. Selezionare **Personalizzato** per definire un pattern di visualizzazione non disponibile nell’elenco. Per ulteriori informazioni, vedere [Pattern di visualizzazione dei dati](../../forms/using/create-interactive-communication.md#datadisplaypatterns).

   Passa a [Variabili e oggetti modello dati](../../forms/using/create-interactive-communication.md#hiddenvariables) per impostare il binding di variabili nascoste nel frammento di documento.

   È inoltre possibile trascinare elementi di origine dati o frammenti di documento di testo per impostare il binding delle variabili.  Per creare un binding con uno qualsiasi degli elementi dell’origine dati, selezionare la scheda **Origini dati** e trascinare l’elemento nel nome della variabile. L&#39;elemento e la variabile dell&#39;origine dati devono essere dello stesso tipo per impostare correttamente il binding. Se trascini e rilascia un elemento dell’origine dati in una variabile già associata, il nuovo elemento sostituisce quello precedente per creare un nuovo binding con la variabile . Allo stesso modo, selezionare la scheda **Risorse** e trascinare il frammento di documento di testo sul nome della variabile per impostare il binding tra di essi. Il frammento di documento di testo non deve contenere variabili.

1. Per aggiungere una tabella con il canale di stampa selezionato, nella scheda **[!UICONTROL Risorse]** applicare il filtro per visualizzare solo i frammenti di layout. Trascina il frammento di layout desiderato nella comunicazione interattiva. Un frammento di layout è basato su un XDP e può essere utilizzato per creare layout grafici o tabelle statiche e dinamiche in Comunicazione interattiva che vengono popolate con dati dinamici.

   Esempio: Una tabella di layout per visualizzare il premio lordo, lo sconto fedeltà % e la disponibilità di assistenza stradale di emergenza per le politiche vecchie e nuove.

   Per ulteriori informazioni sui frammenti di layout, vedere [Frammenti documento](/help/forms/using/document-fragments.md).

1. Con il canale di stampa selezionato, nella scheda **[!UICONTROL Risorse]** applicare il filtro per visualizzare le immagini. Trascina le immagini richieste nella comunicazione interattiva, ad esempio per il logo aziendale.

   Inoltre, nella comunicazione interattiva, gestisci quanto segue:

   * [Aggiunta e configurazione di grafici](/help/forms/using/chart-component-interactive-communications.md)
   * [Sincronizzazione del canale web con il canale di stampa](../../forms/using/create-interactive-communication.md#synchronize)

      * Sincronizzazione automatica
      * Annulla ereditarietà
      * Riattiva ereditarietà
      * Sincronizza
   * [Allegati e accesso alla libreria](../../forms/using/create-interactive-communication.md#attachmentslibrary)
   * [Proprietà dei campi XDP/Layout](../../forms/using/create-interactive-communication.md#xdplayoutfieldproperties)
   * [Aggiungere regole ai componenti](../../forms/using/create-interactive-communication.md#rules)


1. Passa a **[!UICONTROL Canale Web]**. Il canale web viene visualizzato nell’editor di comunicazioni interattive. Quando si passa per la prima volta dal canale Stampa al canale Web, si verifica la sincronizzazione automatica. Per ulteriori informazioni, vedere [Sincronizzazione del canale Web dal canale di stampa](../../forms/using/create-interactive-communication.md#synchronize).

   Poiché in questo esempio utilizziamo Stampa come master per il web, i segnaposto del canale Stampa, il contenuto e il binding dei dati vengono sincronizzati sul canale Web. Tuttavia, puoi modificare e personalizzare il contenuto specifico nel canale web. [Annulla ](#cancelinheritance) ereditarietà per le aree di destinazione e le variabili generate utilizzando il canale di stampa per personalizzare il contenuto.

   ![webchannelassets](assets/webchannelassets.png)

   Toccare il frammento di documento, toccare ![configure_icon](assets/configure_icon.png) (Configura), quindi toccare **[!UICONTROL Properties]** dalla barra laterale della comunicazione interattiva. La sezione **[!UICONTROL Variabili e oggetti modello dati]** elenca le variabili, incluse le variabili nascoste, e gli oggetti modello dati utilizzati nei frammenti di documento. Utilizza l&#39;icona ![modifica](assets/edit.svg) (Modifica) accanto a ciascun oggetto o variabile del modello dati per modificare le proprietà. Inoltre, per i frammenti di documento che sono stati [generati automaticamente](#synchronize) nel canale Web utilizzando il canale Stampa, utilizzare l&#39;icona ![cancelinheritance](assets/cancelinheritance.png) (Annulla ereditarietà) accanto a ciascun oggetto del modello dati e la variabile su [Annulla ereditarietà](#cancelinheritance) per poterli modificare.

1. Per aggiungere altri componenti nel canale Web, con il canale Web selezionato, tocca **[!UICONTROL Componenti]**. Trascina i componenti nel canale web della comunicazione interattiva in base alle esigenze e procedi alla configurazione.

   | Componenti | Funzionalità |
   |---|---|
   | Grafico | Aggiunge un grafico che è possibile utilizzare nella comunicazione interattiva per la rappresentazione visiva dei dati bidimensionali recuperati da una raccolta di modelli di dati del modulo. Per ulteriori informazioni, vedere [Uso del componente grafico](../../forms/using/chart-component-interactive-communications.md). |
   | Frammento di documento | Consente di aggiungere un componente, un testo, un elenco o una condizione riutilizzabili a una comunicazione interattiva. Il componente riutilizzabile aggiunto a una comunicazione interattiva può essere basato su un modello di dati del modulo o senza un modello di dati del modulo. |
   | Immagine | Consente di inserire un’immagine. |
   | Pannello | Consente di aggiungere un [pannello](../../forms/using/create-interactive-communication.md#add-panel-component-to-the-web-channel) alla comunicazione interattiva. |
   | Tabella | Aggiunge una tabella che consente di organizzare i dati in righe e colonne. |
   | Area di destinazione | Inserisce un’area di destinazione in un canale web per organizzare i componenti specifici del canale web. L’area di destinazione è un contenitore semplice che consente di raggruppare componenti specifici per canale web. |
   | Testo | Aggiunge testo RTF al canale web di una comunicazione interattiva. Il testo può inoltre utilizzare gli oggetti del modello dati del modulo per rendere dinamico il contenuto. |
   | Pulsante | Consente di aggiungere un [pulsante](../../forms/using/create-interactive-communication.md#add-button-component-to-the-web-channel) alla comunicazione interattiva. Puoi utilizzare il componente Pulsante per passare ad altre comunicazioni interattive, moduli adattivi, altre risorse quali immagini o frammenti di documento o un URL esterno. |
   | Separatore | Consente di inserire una linea orizzontale all’interno di una comunicazione interattiva. Utilizza questo componente per distinguere tra le sezioni di una corrispondenza. Ad esempio, è possibile utilizzare il componente Separatore per distinguere tra le sezioni Dettagli cliente e Dettagli carta di credito in un rendiconto della carta di credito. |

1. Se necessario, inserisci le risorse nel canale web.

   È possibile [visualizzare in anteprima la comunicazione interattiva](#previewic) per verificare l&#39;aspetto delle uscite di stampa e web della comunicazione interattiva e continuare a apportare le modifiche necessarie.

## Anteprima della comunicazione interattiva {#previewic}

È possibile utilizzare l&#39;opzione **Anteprima** per valutare l&#39;aspetto della comunicazione interattiva. Il canale web della comunicazione interattiva offre inoltre la possibilità di emulare l’esperienza di una comunicazione interattiva per diversi dispositivi. Ad esempio, iPhone, iPad e Desktop. È possibile utilizzare le opzioni **Anteprima** e **Emulatore** ![righer](assets/ruler.png) insieme per visualizzare in anteprima le uscite web per dispositivi di diverse dimensioni dello schermo. I dati di esempio contenuti nell’anteprima vengono compilati dal modello dati dei moduli specificato.

1. Seleziona il canale (stampa o web) da visualizzare in anteprima e tocca anteprima. Viene visualizzata la comunicazione interattiva.

   >[!NOTE]
   >
   >L’anteprima viene compilata con i dati di esempio del modello dati del modulo specificato. Per ulteriori informazioni sull&#39;anteprima della comunicazione interattiva con altri dati o sull&#39;utilizzo del servizio di precompilazione, vedere [Utilizzare il modello dati del modulo](/help/forms/using/using-form-data-model.md) e [Utilizzare il modello dati del modulo](/help/forms/using/work-with-form-data-model.md).

1. Per il canale web, utilizza ![righer](assets/ruler.png) per visualizzare l&#39;aspetto della comunicazione interattiva su vari dispositivi.

   ![webchannelpreview](assets/webchannelpreview.png)

Inoltre, è possibile [Preparare e inviare comunicazioni interattive utilizzando l&#39;interfaccia utente dell&#39;agente](/help/forms/using/prepare-send-interactive-communication.md).

## Configurare le proprietà nella comunicazione interattiva {#configure-properties-in-interactive-communication}

### Allegati e accesso alla libreria {#attachmentslibrary}

Nel canale Stampa è possibile configurare gli allegati e l&#39;accesso alla libreria per consentire all&#39;agente di gestire gli allegati nell&#39;interfaccia utente dell&#39;agente per la comunicazione interattiva:

1. Nel canale Stampa, evidenzia il Contenitore documento e tocca **Proprietà**.

   ![documentcontainerproperties](assets/documentcontainerproperties.png)

   Il pannello Proprietà viene visualizzato nella barra laterale.

   ![proprietà](assets/propertiesattachments.png)

1. Espandi **Allegati** e specifica le seguenti proprietà:

   * **[!UICONTROL Consenti accesso]** libreria: Seleziona per abilitare l&#39;accesso alla libreria per l&#39;agente nell&#39;interfaccia utente dell&#39;agente. Se attivato, l’agente può aggiungere file dalla libreria durante la preparazione della comunicazione interattiva.
   * **[!UICONTROL Consenti Il Riordinamento Degli Allegati]**: Selezionare per abilitare l&#39;agente a riordinare gli allegati con la comunicazione interattiva.
   * **[!UICONTROL Numero Massimo Di Allegati Consentiti]**: Specifica il numero massimo di allegati consentiti con la comunicazione interattiva.
   * **[!UICONTROL File Da Allegare]**: Tocca  **** Aggiungi e sfoglia per selezionare i file da allegare e specificare quanto segue:

      * **[!UICONTROL Allega Questo File Al Documento Per Impostazione Predefinita]**: È possibile modificare questa opzione se solo l&#39;allegato non è obbligatorio.
      * **[!UICONTROL Obbligatorio:]** l&#39;agente non sarà in grado di rimuovere l&#39;allegato nell&#39;interfaccia utente dell&#39;agente.

   ![file allegati](assets/attachfiles.png)

1. Toccate **[!UICONTROL Chiudi]**.

### Proprietà dei campi XDP/Layout {#xdplayoutfieldproperties}

1. Durante la modifica del canale di stampa di una comunicazione interattiva, passa il cursore del mouse su un campo creato nel modello del canale di stampa e seleziona ![configure_icon](assets/configure_icon.png) (Configura).

   La finestra di dialogo Proprietà viene visualizzata nella barra laterale.

   ![data_display_patterns_fields](assets/data_display_patterns_fields.jpg)

1. Specifica quanto segue:

   * **[!UICONTROL Nome]**: Nome del nodo JCR.
   * **[!UICONTROL Titolo]**: Immettere un titolo che sarà visibile all&#39;agente nell&#39;interfaccia utente dell&#39;agente e nella struttura del contenitore del documento.
   * **[!UICONTROL Tipo]** di binding: Selezionare uno dei seguenti tipi di binding per il campo.

      * Nessuno: Il valore della proprietà verrà compilato dall&#39;agente.
      * Frammento di testo: Se questa opzione è selezionata, è possibile sfogliare e selezionare un frammento di documento di testo il cui contenuto è sottoposto a rendering nel campo. In alternativa, trascinare il frammento di documento di testo sul nome del campo per impostare il binding tra di essi. Il frammento di documento di testo non deve contenere variabili.
      * Oggetto modello dati: Selezionare una proprietà del modello dati del modulo il cui valore viene compilato nel campo . In alternativa, seleziona la scheda **Origini dati** e trascina la proprietà sul campo.
   * **[!UICONTROL Valori]** predefiniti: Il valore predefinito assicura che il campo non sia vuoto se non è presente alcun valore fornito dall’oggetto modello dati o dal frammento di testo specificato. Se il tipo di binding dei dati non è nessuno, il valore predefinito viene precompilato nel campo .
   * **[!UICONTROL Pattern]** di visualizzazione: È inoltre possibile definire un formato di visualizzazione per un campo. Seleziona una delle opzioni predefinite dall&#39;elenco a discesa **Tipo** per applicare un formato di visualizzazione a un campo. Selezionare **Personalizzato** per definire un pattern di visualizzazione non disponibile nell’elenco. Per ulteriori informazioni, vedere [Pattern di visualizzazione dei dati](../../forms/using/create-interactive-communication.md#datadisplaypatterns)

   * **[!UICONTROL Modificabile dall&#39;agente]**: Seleziona per consentire all’agente di modificare il valore nel campo nell’interfaccia utente dell’agente. Questa impostazione non è applicabile se il tipo di binding è Frammento di testo.
   * **[!UICONTROL Etichetta]**: Specifica una stringa di testo visualizzata con il campo nell&#39;interfaccia utente dell&#39;agente. Questa impostazione non è applicabile se il tipo di binding è Frammento di testo.
   * **[!UICONTROL Descrizione]**: Immettere una stringa di testo che sarà visibile al passaggio del mouse sull&#39;agente nell&#39;interfaccia utente dell&#39;agente. Questa impostazione non è applicabile se il tipo di binding è Frammento di testo.
   * **[!UICONTROL Obbligatorio]**: Selezionare questa opzione per rendere il campo obbligatorio per l&#39;agente. Questa impostazione non è applicabile se il tipo di binding è Frammento di testo.
   * **[!UICONTROL Consenti righe]** multiple: Selezionare questo campo per consentire più righe di testo come voce nel campo. Questa impostazione non è applicabile se il tipo di binding è Frammento di testo.


1. Tocca ![done_icon](assets/done_icon.png).

### Pattern di visualizzazione dei dati {#datadisplaypatterns}

L’interfaccia di authoring consente di definire pattern di visualizzazione dei dati per campi, variabili ed elementi del modello di dati del modulo disponibili durante la creazione di una comunicazione interattiva per la stampa e i canali web.

Per configurare il pattern di visualizzazione dei dati, tocca l’elemento, seleziona ![configure_icon](assets/configure_icon.png) (Configura) e imposta il pattern di visualizzazione nel pannello **[!UICONTROL Properties]** nella barra laterale. Seleziona un&#39;opzione predefinita dall&#39;elenco a discesa **[!UICONTROL Tipo]** per visualizzare il pattern associato al tipo selezionato. Selezionare **[!UICONTROL Personalizzato]** dall&#39;elenco a discesa **[!UICONTROL Tipo]** per definire un pattern non disponibile nell&#39;elenco. La modifica dei valori nel campo **[!UICONTROL Pattern]** modifica automaticamente il tipo in **[!UICONTROL Personalizzato]**.

Per applicare il pattern di visualizzazione, il numero di caratteri o cifre definito nel campo Pattern deve corrispondere o superare i caratteri o le cifre definiti nel valore per campi, variabili ed elementi del modello dati del modulo. Per ulteriori informazioni, consulta [esempio](../../forms/using/create-interactive-communication.md#greaternumberofdigits).

![data_display_pattern_example](assets/data_display_patterns_ssn_new.png)

È possibile ridefinire il pattern di visualizzazione per un campo, una variabile o un elemento del modello dati del modulo dopo la generazione del contenuto web dal canale di stampa. Di conseguenza, un elemento può avere diversi pattern di visualizzazione definiti per i canali web e di stampa. Se non si definisce un pattern di visualizzazione per un elemento nel canale di stampa e si genera automaticamente il contenuto web utilizzando il canale di stampa, il binding dei dati definito per l’elemento nel canale di stampa definisce le opzioni del pattern di visualizzazione disponibili nell’elenco a discesa **[!UICONTROL Tipo]** . Se non è definito alcun binding per l’elemento, il tipo di dati dell’elemento definisce le opzioni disponibili per il pattern di visualizzazione. Ad esempio, se si crea un binding dei dati di tipo Number per un elemento nel canale di stampa, le opzioni del pattern di visualizzazione disponibili nell’elenco a discesa **[!UICONTROL Tipo]** sono di tipo Number in vari formati.

Passa alla modalità **Anteprima** o apri l&#39;interfaccia utente dell&#39;agente per visualizzare il pattern di visualizzazione applicato a questi elementi.

Nella tabella seguente è riportato un esempio dei valori visualizzati in seguito all’impostazione del pattern di visualizzazione dei dati per una variabile:

| Tipo | Valore predefinito | Pattern di visualizzazione | Valore visualizzato | Descrizione |
|---|---|---|---|---|
| Codice fiscale | 123456789 | testo{999-99-9999} | 123-45-6789 | Il numero di cifre nel campo del valore predefinito corrisponde al numero di cifre nel campo Pattern. Il valore basato sul pattern viene visualizzato correttamente. |
| Codice fiscale | 1234567 | testo{999-99-9999} | 1-23-4567 | Il numero di cifre nel campo del valore predefinito è inferiore al numero di cifre nel campo Pattern. Il pattern si applica alle 7 cifre disponibili. |
| Codice fiscale | 1234567890 | testo{999-99-9999} | 1234567890 | Il numero di cifre nel campo del valore predefinito è maggiore del numero di cifre nel campo Pattern. Di conseguenza, non vi è alcuna modifica nel valore di visualizzazione. |

Se non viene specificato un pattern di visualizzazione per una variabile o un elemento del modello dati modulo, per impostazione predefinita viene utilizzata la [configurazione globale del frammento di documento](https://helpx.adobe.com//experience-manager/6-5/forms/using/interactive-communication-configuration-properties.html).

Se non si applica un pattern di visualizzazione a una variabile di tipo dati numero, nell’anteprima Stampa viene visualizzato il pattern in base alla configurazione del frammento di documento globale. Se si applicano modifiche alla configurazione di frammento di documento globale predefinita, l&#39;interfaccia utente agente visualizza comunque il pattern in base ai separatori predefiniti definiti per le impostazioni internazionali.

Analogamente, per i campi, se il pattern di visualizzazione non è specificato, al campo viene applicato il pattern definito durante la creazione del modello di stampa (XDP). Se non è presente alcun pattern durante la creazione del modello di stampa, i pattern predefiniti basati sulle specifiche XFA vengono applicati ai campi.

Inoltre, se il pattern di visualizzazione specificato non è corretto o non può essere applicato, i pattern predefiniti basati sulle specifiche XFA vengono applicati ai campi, alle variabili o agli elementi del modello dati del modulo.

## Applicare regole ai componenti di comunicazione interattiva {#rules}

Per condizionare componenti o contenuti nella comunicazione interattiva, tocca il componente o parte di contenuto e seleziona ![createruleicon](assets/createruleicon.png) (Crea regola) per avviare l’Editor regole.

Per ulteriori informazioni, vedere:

* [Editor regola](/help/forms/using/rule-editor.md)
* [Introduzione all’authoring delle comunicazioni interattive](/help/forms/using/introduction-interactive-communication-authoring.md)

## Uso delle tabelle {#tables}

### Tabelle dinamiche nella comunicazione interattiva {#dynamic-tables-in-interactive-communication}

È possibile aggiungere tabelle dinamiche nella comunicazione interattiva utilizzando frammenti di layout. I passaggi seguenti utilizzano un esempio di rendiconto della carta di credito per illustrare l’utilizzo di un frammento di layout per creare una tabella dinamica in una comunicazione interattiva.

1. Assicurati che il frammento di layout richiesto per la creazione della tabella sia disponibile in AEM.
1. Nel canale di stampa della comunicazione interattiva, trascina e rilascia un frammento di layout (con una tabella a più colonne) in un’area di destinazione dal browser Risorse.

   ![lf_dragdrop](assets/lf_dragdrop.png)

   Nell’area layout Comunicazione interattiva viene visualizzata una tabella.

   ![lf_dragdrop_table](assets/lf_dragdrop_table.png)

1. Specificare il binding dei dati per ciascuna cella della tabella. Per creare una riga ripetibile, inserire le proprietà del modello dati del modulo nella riga appartenente a una proprietà di raccolta comune.

   1. Tocca una cella nella tabella e seleziona ![configure_icon](assets/configure_icon.png) (Configura).

      La finestra di dialogo Proprietà viene visualizzata nella barra laterale.

      ![lf_cell_properties](assets/lf_cell_properties.png)

   1. Configura le proprietà:

      * **[!UICONTROL Nome]**: Nome del nodo JCR.
      * **[!UICONTROL Titolo]**: Immetti un titolo che sarà visibile nell’editor di comunicazioni interattive.
      * **[!UICONTROL Tipo]** di binding: Selezionare uno dei seguenti tipi di binding per il campo.

         * **[!UICONTROL Nessuna]**
         * **[!UICONTROL Oggetto]** del modello dati: Il valore della proprietà del modello dati modulo viene compilato nel campo . In alternativa, seleziona la scheda **Origini dati** e trascina la proprietà sul campo.
      * **[!UICONTROL Oggetto]** modello dati: Proprietà del modello dati del modulo il cui valore è popolato nel campo .
      * **[!UICONTROL Valore]** predefinito: Il valore predefinito assicura che il campo non sia vuoto se non è presente alcun valore fornito dall&#39;oggetto modello dati specificato. Il valore predefinito viene precompilato nel campo .

      * **[!UICONTROL Modificabile dall&#39;agente]**: Seleziona per consentire all’agente di modificare il valore nel campo nell’interfaccia utente dell’agente.
   1. Tocca ![done_icon](assets/done_icon.png).



1. Visualizza in anteprima la comunicazione interattiva per visualizzare la tabella rappresentata con i dati.

   ![lf_preview](assets/lf_preview.png)

### Tabelle solo per il canale web {#webchanneltables}

Toccare il pannello principale nel modello Web e toccare **+** per aggiungere un componente **Tabella** alla comunicazione interattiva. Nella comunicazione interattiva viene inserita una tabella contenente due righe. La prima riga della tabella rappresenta l’intestazione Tabella.

#### Aggiungi righe e colonne alla tabella {#addrowscolumnstable}

**Per aggiungere o eliminare colonne:**

1. Toccare la casella di testo predefinita nella riga di intestazione della tabella per visualizzare la barra degli strumenti del componente.
1. Selezionare **Aggiungi colonna** o **Elimina colonna** per aggiungere o eliminare rispettivamente le colonne della tabella.

![component_toolbar_table1](assets/component_toolbar_table1.png)

**Per aggiungere o eliminare righe:**

1. Tocca una delle righe della tabella per visualizzare la barra degli strumenti del componente. Puoi anche selezionare la riga della tabella utilizzando il browser Contenuto nella barra laterale della comunicazione interattiva.
1. Selezionare **Aggiungi riga** o **Elimina riga** per aggiungere o eliminare rispettivamente le righe della tabella. Utilizza le opzioni **Sposta su** e **Sposta giù** disponibili nella barra degli strumenti per ridisporre le righe nella tabella.

![Barra degli strumenti del componente](assets/component_toolbar_table_row_new.png)

**A.** Aggiungi riga  **B.** Elimina riga  **C.** Sposta su  **D.** Sposta giù

#### Aggiunta o modifica di testo nelle celle della tabella {#addedittexttable}

1. Seleziona la casella di testo predefinita nella cella della tabella e tocca ![modifica](assets/edit.png) (Modifica).
1. Digita il testo nella cella della tabella e tocca ![done_icon](assets/done_icon.png) per salvarlo.

#### Crea un binding tra celle di tabella ed elementi dell’oggetto del modello dati {#createbindingtablecells}

1. Seleziona la casella di testo predefinita nella riga della tabella e tocca ![modifica](assets/edit.png) (Modifica).
1. Toccare l’elenco a discesa Oggetti modello dati e selezionare la proprietà .
1. Toccare per salvare e creare un binding tra la cella della tabella e la proprietà dell’oggetto modello dati.

![Creazione del binding dei dati](assets/create_data_binding_table_new.png)

#### Crea un collegamento ipertestuale per il testo nella cella della tabella {#createhyperlinktable}

1. Seleziona la casella di testo predefinita nella cella della tabella e tocca ![modifica](assets/edit.svg) (Modifica).
1. Selezionare il testo nella cella della tabella e toccare l’icona Collegamento ipertestuale.
1. Specifica l&#39;URL nel campo **Percorso** .
1. Tocca ![done_icon](assets/done_icon.png) per salvare le proprietà dei collegamenti ipertestuali.

![Crea collegamento ipertestuale](assets/create_hyperlink_table_new.png)

#### Creare tabelle dinamiche {#createdynamictables}

È possibile creare una tabella dinamica solo per il canale web in una comunicazione interattiva utilizzando una proprietà del modello dati di raccolta di tipo . Una tabella di questo tipo rappresenta le proprietà secondarie di una proprietà di raccolta. È possibile modificare solo le proprietà di formattazione delle varie celle della tabella.

1. Passa al canale Web e scegli di visualizzare il browser Origini dati.
1. Trascinare una proprietà di raccolta in un sottomodulo. Nel sottomodulo viene creata una tabella.
1. Visualizzare l’anteprima della tabella nell’anteprima Web della comunicazione interattiva.

#### Ordinare le colonne in una tabella {#sortcolumns}

Puoi ordinare i dati in base a qualsiasi colonna di una tabella nella comunicazione interattiva. I valori della colonna possono essere ordinati in ordine crescente o decrescente.

L’ordinamento può essere applicato alle colonne delle tabelle contenenti:

* Testo statico
* Proprietà dell&#39;oggetto modello dati
* Combinazione delle proprietà dell’oggetto modello dati e testo statico

Per abilitare l’ordinamento:

1. Seleziona la tabella e tocca ![configure_icon](assets/configure_icon.png) (Configura). Puoi anche selezionare la tabella utilizzando il browser **Contenuto** nella barra laterale della comunicazione interattiva.
1. Selezionare **Abilita ordinamento.**
1. Tocca ![done_icon](assets/done_icon.png) per salvare le proprietà della tabella. Le icone di ordinamento, le frecce su e giù nelle intestazioni delle colonne indicano che l’ordinamento è stato attivato.

   ![Abilita ordinamento](assets/enable_sorting_new-1.png)

1. Passa alla modalità **Anteprima** per visualizzare l&#39;output. La tabella viene ordinata automaticamente in base alla prima colonna della tabella.
1. Fai clic sull’intestazione della colonna per ordinare i valori in base alla colonna.

   Un&#39;intestazione di colonna con una freccia su rappresenta che:

   * La tabella viene ordinata in base a tale colonna.
   * i valori nella colonna vengono visualizzati in ordine crescente.

   ![Ordinamento crescente](assets/sorting_ascending_new-1.png)

   Analogamente, un’intestazione di colonna con una freccia giù rappresenta la visualizzazione dei valori della colonna in ordine decrescente.

## Modifica proprietà di comunicazione interattiva {#edit-interactive-communication-properties}

Una volta creata una comunicazione interattiva, puoi modificarne le proprietà in un secondo momento.

Utilizzare la pagina **Proprietà** per:

* Modificare i valori per i campi specificati durante la creazione della comunicazione interattiva, ad esempio Titolo e Descrizione.
* Aggiungi o elimina un canale Web per una comunicazione interattiva esistente.
* Anteprima, download o eliminazione della comunicazione interattiva
* Apri l&#39; [Interfaccia utente agente](/help/forms/using/prepare-send-interactive-communication.md).

Per accedere alla pagina **Proprietà** :

1. Accedi all&#39;istanza di authoring AEM e passa a **Adobe Experience Manager** > **Forms** > **Forms &amp; Documents**.
1. Seleziona la comunicazione interattiva e tocca **Proprietà**.
1. Seleziona la scheda **Generale** per modificare i campi **Titolo** e **Descrizione** .

### Aggiungi o elimina il canale Web {#add-or-delete-the-web-channel}

Esegui i seguenti passaggi per aggiungere il canale Web per una comunicazione interattiva esistente:

1. Nella pagina **Proprietà**, seleziona la scheda **Canali** .
1. Selezionare la casella di controllo **Web** e selezionare un modello per il canale Web.
1. Selezionare **Usa stampa come master per il canale Web** per abilitare la sincronizzazione tra il canale Web e il canale Stampa.
1. Tocca **Salva e chiudi** per salvare le modifiche.

   Allo stesso modo, puoi toccare la casella di controllo **Web** nella scheda **Canali** per eliminare il canale Web dalla comunicazione interattiva.

## Aggiungi componente Pulsante al canale Web {#add-button-component-to-the-web-channel}

È possibile aggiungere un pulsante come componente al canale web della comunicazione interattiva. Definisci le regole utilizzando l’ [editor di regole](../../forms/using/rule-editor.md) per passare ad altre comunicazioni interattive, moduli adattivi, altre risorse come immagini o frammenti di documento, o un URL esterno toccando il pulsante .

Per aggiungere un pulsante e definirne le regole:

1. Toccare il pannello principale nel modello Web e toccare **+** per aggiungere il componente **Button** alla comunicazione interattiva.
1. Tocca il componente pulsante e tocca ![edit-rules](assets/edit-rules.png) per definire le regole toccando il pulsante.
1. Nella sezione **When** , seleziona **clicked** dallo stato dell’elenco a discesa del pulsante.
1. Nella sezione **Then** :

   1. Seleziona un’azione dall’elenco a discesa. Ad esempio, selezionare **Passa a** come tipo di azione.

   1. Specifica l’URL della comunicazione interattiva, del modulo adattivo, di una risorsa o di una pagina web. Ad esempio, specifica l’URL nel formato seguente per passare a un’altra comunicazione interattiva: https://&lt;server-name>:&lt;port>/editor.html/content/forms/af/&lt;Interactive Communication name>/channels/&lt;channel name - print or web>.html
   1. Specifica l’opzione per aprire la risorsa nella stessa scheda, nuova scheda o nuova finestra.
   1. Tocca **Fine**, quindi tocca **Chiudi** per salvare la regola.

   Allo stesso modo, è possibile selezionare altre opzioni disponibili dall’elenco a discesa del tipo di azione, ad esempio Invoke Service e Submit Form. Per ulteriori informazioni, consulta [editor di regole](../../forms/using/rule-editor.md).

1. Visualizza l’anteprima della comunicazione interattiva e tocca il pulsante per visualizzare la comunicazione interattiva, il modulo adattivo, una risorsa o una pagina web specificata al punto 4, lettera b).

## Aggiungi il componente Pannello al canale web {#add-panel-component-to-the-web-channel}

Il componente Pannello è un segnaposto per raggruppare altri componenti e controlla come un gruppo di componenti, come il pannello a soffietto e le schede, vengono disposti nella comunicazione interattiva. Un componente pannello consente inoltre di rendere ripetibile un gruppo di componenti per l’utente finale, ad esempio in più voci richieste per il riempimento delle credenziali educative.

Esegui i seguenti passaggi per aggiungere un componente Pannello al canale web:

1. Inserisci il componente **Pannello** nel canale web utilizzando una delle seguenti opzioni:

   * Tocca un componente, tocca **+** e seleziona il componente **Pannello**.

   * Dal pannello del browser **Componente**, trascina il componente **Pannello** nella comunicazione interattiva.

   * Tocca il **Pannello** nel pannello del browser **Contenuto** e tocca **Aggiungi pannello secondario**. Selezionando l&#39;opzione **Aggiungi pannello figlio** viene visualizzata la finestra di dialogo **Aggiungi pannello figlio**. Immetti il titolo e una descrizione facoltativa e il nome del componente Pannello.

1. Tocca il pannello dal browser **Contenuto** per eseguire azioni aggiuntive sul pannello, come configurare, modificare le regole, copiare, eliminare e inserire un componente.

   Puoi anche trascinare un pannello all’interno del browser **Contenuto** per riflettere la modifica nella struttura della comunicazione interattiva nel riquadro di destra.

## Sincronizzazione del canale web con il canale di stampa {#synchronize}

Quando si seleziona Stampa come master per il canale Web durante la creazione di una comunicazione interattiva, il canale Web viene creato in sincronia con il canale Stampa e il contenuto e il binding dei dati del canale Web viene derivato dal canale di stampa e le modifiche apportate nel canale di stampa potrebbero riflettersi nel canale Web quando si tocca Sincronizza.

Tuttavia, gli autori possono interrompere l’ereditarietà dei componenti nel canale web, a seconda delle necessità.

![Crea Stampa Web master ](assets/create_ic_print_master_new-1.png) ![MasterPrint](assets/create_ic_print_master_web_new-1.png)

### Sincronizzazione automatica {#autosync}

Se si seleziona l&#39;opzione **[!UICONTROL Usa stampa come master per il canale Web]**, è possibile selezionare una delle seguenti modalità per generare il canale Web:

* **[!UICONTROL Layout]** automatico: Selezionare questa modalità per generare automaticamente segnaposti, contenuti e binding dei dati per il canale Web dal canale Stampa.
* **[!UICONTROL Organizza]** manualmente: Selezionare questa modalità per selezionare e aggiungere manualmente gli elementi del canale Stampa al canale Web utilizzando il contenuto principale disponibile nella scheda Origini dati. Per ulteriori informazioni, consulta [Selezionare gli elementi del canale di stampa per creare il contenuto del canale Web](#selectprintchannelelements).

![Crea opzioni IC](assets/create_ic_options_updated_new.png)

>[!NOTE]
>
>La sincronizzazione dei canali sincronizza solo i frammenti di documento, le immagini, le condizioni, gli elenchi e i frammenti di layout dal canale di stampa al canale Web. I sottomoduli o i nodi padre che includono tali elementi non sono sincronizzati.

### Selezionare gli elementi del canale di stampa per creare il contenuto del canale Web {#selectprintchannelelements}

Se si seleziona Stampa come master durante la creazione della comunicazione interattiva e non si seleziona l&#39;opzione di sincronizzazione automatica, è inoltre possibile trascinare gli elementi del canale Stampa nell&#39;interfaccia di creazione del canale Web.

Passa a **Origini dati** > **Contenuto principale** per visualizzare gli elementi del canale di stampa. Trascinare le aree, i campi o le tabelle di destinazione nell&#39;interfaccia di authoring del canale Web. Un’icona a forma di cerchio blu accanto al nome dell’elemento indica che l’elemento Canale di stampa è già stato incluso nel canale Web.

![Contenuto principale](assets/master_content.png)

### Annulla ereditarietà {#cancelinheritance}

Nel canale web, i componenti sono incorporati nelle aree di destinazione.

Passa il puntatore del mouse sull&#39;area o sulla variabile di destinazione rilevante nel canale web e seleziona ![cancelinheritance](assets/cancelinheritance.png) (Annulla ereditarietà), quindi tocca **[!UICONTROL Sì]** nella finestra di dialogo Annulla ereditarietà.

L’ereditarietà dei componenti all’interno dell’area di destinazione viene annullata e ora è possibile modificarli in base alle esigenze.

### Riattiva ereditarietà {#re-enable-inheritance}

Nel canale Web, se hai annullato l’ereditarietà di un componente, puoi riabilitarlo. Per riabilitare l’ereditarietà, passa il cursore del mouse sul bordo dell’area di destinazione rilevante, che include il componente, e tocca ![reenableinheritance](assets/reenableinheritance.png).

Viene visualizzata la finestra di dialogo Ripristina ereditarietà.

![revertereditarietà](assets/revertinheritance.png)

Se necessario, seleziona **[!UICONTROL Sincronizza la pagina dopo aver ripristinato l&#39;ereditarietà]**. Seleziona questa opzione per sincronizzare l’intera comunicazione interattiva. Se non selezioni questa opzione, al momento del ripristino dell’ereditarietà viene sincronizzata solo l’area di destinazione interessata.

Toccare **[!UICONTROL Sì]**.

### Sincronizza {#synchronize-1}

Se si utilizza Stampa come master per il canale Web e si apportano modifiche al canale Stampa, è possibile sincronizzare il contenuto per apportare le modifiche appena apportate al canale Web.

1. Per sincronizzare il canale Web con il canale Stampa, passare al canale Web e toccare l&#39;icona Altre opzioni.

   ![Opzioni di sincronizzazione automatica](assets/auto_sync_options_new.png)

1. Toccate una delle seguenti opzioni:

   * **[!UICONTROL Sincronizza con stampa]**: Sincronizza il contenuto solo per le aree di destinazione in cui l’ereditarietà non viene annullata.
   * **[!UICONTROL Ripristina]**: Sincronizza il contenuto del canale Web con il canale Stampa ed elimina tutte le modifiche apportate al canale Web.

### Usa la barra degli strumenti del componente per eseguire azioni sui componenti ereditati {#componenttoolbar}

Dopo aver generato automaticamente il contenuto nel canale web utilizzando l’opzione Sincronizza, puoi eseguire più azioni sui componenti senza annullare l’ereditarietà.

![Barra degli strumenti del componente](assets/component_toolbar_inherited_web_new.png)

Toccate il componente per visualizzare le seguenti opzioni:

* **Copia:** copia un componente e incollalo in altre posizioni nella comunicazione interattiva.
* **Taglia:** sposta un componente da un punto all’altro nella comunicazione interattiva.
* **Inserisci componente:** inserisci un componente sopra il componente selezionato.
* **Incolla:** incolla il componente tagliato o copiato utilizzando le opzioni descritte in precedenza.
* **Gruppo:** selezionate più componenti per tagliarli, copiarli o incollarli insieme.
* **Elemento padre:** seleziona l’elemento principale di un componente.
* **Visualizza espressione SOM:** visualizza l’espressione  [SOM ](../../forms/using/using-som-expressions-adaptive-forms.md) per il componente.

* **Raggruppa oggetti nel pannello:**  Raggruppa i componenti in un pannello per eseguire le operazioni su tali componenti simultaneamente. Per ulteriori informazioni, vedere [Raggruppare gli oggetti nel pannello](#groupobjectspanel).

* **Annulla ereditarietà:** [Annulla l’](#cancelinheritance) ereditarietà dei componenti all’interno dell’area di destinazione per modificarli.

### Raggruppa oggetti nel pannello {#groupobjectspanel}

L’interfaccia di authoring dei canali web facilita il raggruppamento dei componenti in un pannello per eseguire le operazioni su tali componenti simultaneamente. La scheda **Contenuto** elenca i componenti raggruppati come elementi secondari del pannello nella struttura del contenuto.

1. Tocca un componente e seleziona l’operazione Gruppo ( ![gruppo](assets/group.jpg)).
1. Seleziona più componenti e tocca **Raggruppa oggetti nel pannello**.

   ![Raggruppa oggetti](assets/component_toolbar_group_objects_new.png)

1. Nella finestra di dialogo **Raggruppa oggetti nel pannello**, immettere un nome per il pannello.
1. Immetti un titolo e una descrizione facoltativi per il Pannello.
1. Fai clic su ![punto elenco_segno di spunta](assets/bullet_checkmark.png).

   I componenti raggruppati vengono visualizzati come elementi secondari del pannello nella struttura del contenuto.

   ![content_tree_group](assets/content_tree_grouping.png)

## Formato di uscita per il canale di stampa {#output-format-print-channel}

Utilizzare l&#39;API PrintChannel per definire il formato di output per il canale Stampa di una comunicazione interattiva. Se non si definisce un formato di output, AEM Forms genera l’output in formato PDF.

```javascript
//options for rendering print channel of a multi-channel document
PrintChannelRenderOptions renderOptions = new PrintChannelRenderOptions();
PrintDocument printDocument = printChannel.render(renderOptions);
```

Per generare l&#39;output in qualsiasi altro formato, specificare il tipo di formato di output. Fare riferimento a [API PrintChannel](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/PrintConfig.html) per l&#39;elenco dei tipi di formati di output supportati.

Ad esempio, è possibile utilizzare il seguente esempio per definire PCL come formato di output per una comunicazione interattiva:

```javascript
//options for rendering print channel of a multi-channel document
PrintChannelRenderOptions renderOptions = new PrintChannelRenderOptions();
renderOptions.setRenderFormat(PrintConfig.HP_PCL_5e);
PrintDocument printDocument = printChannel.render(renderOptions);
```
