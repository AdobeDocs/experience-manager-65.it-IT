---
title: Utilizzo di xtypes (interfaccia classica)
description: Scopri tutti gli xtype disponibili con Adobe Experience Manager
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
exl-id: 06ca4e6d-9ab7-4c5b-905c-07c448632f2b
source-git-commit: 25c444e2093d118259925034e0d630ab0effc473
workflow-type: tm+mt
source-wordcount: '3865'
ht-degree: 0%

---

# Utilizzo di xtypes (interfaccia classica){#using-xtypes-classic-ui}

Questa pagina descrive tutti gli xtype disponibili con Adobe Experience Manager (AEM).

Nel linguaggio ExtJS, xtype è un nome simbolico assegnato a una classe. Puoi leggere il paragrafo &quot;Component XTypes&quot; (Tipi di Targeting esperienza componenti) della [Panoramica di ExtJS 2](https://www.sencha.com/learn/overview-of-extjs-2) per una spiegazione dettagliata su cosa è un xtype e come può essere utilizzato.

Per informazioni complete su tutti i widget disponibili in AEM, vedere [documentazione API widget](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html).

Per individuare i componenti in cui un determinato xtype viene utilizzato in AEM, è possibile utilizzare la seguente query Xpath in CRXDE sostituendo &#39;checkbox&#39; con l&#39;xtype desiderato:

`//element(*, cq:Widget)[@xtype='checkbox']`

>[!NOTE]
>
>Questa pagina descrive l’utilizzo di xtype ExtJS nell’interfaccia utente classica.
>
>L’Adobe consiglia di utilizzare il metodo standard, moderno, [interfaccia touch](/help/sites-developing/touch-ui-concepts.md) in base a [Coral UI](/help/sites-developing/touch-ui-concepts.md#coral-ui) e [Interfaccia utente Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components).

## xtypes {#xtypes}

Di seguito sono elencati gli xtype disponibili in Adobe Experience Manager:

* annotazione

  [CQ.wcm.Annotation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Annotation)

  La finestra di dialogo è un tipo speciale di finestra con una maschera nel corpo e un gruppo di pulsanti nel piè di pagina. In genere viene utilizzato per modificare il contenuto, ma può anche visualizzare solo le informazioni.

* array store

  [CQ.Ext.data.ArrayStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.ArrayStore)

  Precedentemente noto come &quot;SimpleStore&quot;.

  Piccola classe helper per creare [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)s da Dati array più semplice. Un ArrayStore viene configurato automaticamente con un [CQ.Ext.data.ArrayReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.ArrayReader).

* editor risorse

  [CQ.dam.AssetEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.dam.AssetEditor)

  Editor risorse utilizzato nell’amministrazione di DAM.

* assetreferencesearchdialog

  [CQ.wcm.AssetReferenceSearchDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.AssetReferenceSearchDialog)

  La finestra di dialogo AssetReferenceSearchDialog viene visualizzata quando una pagina fa riferimento a risorse o tag.

* blueprintconfig

  [CQ.wcm.msm.BlueprintConfig](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintConfig)

  BlueprintConfig fornisce un pannello per visualizzare le Live Copy di una blueprint e modificarne le proprietà ( attivazione di sincronizzazione e azioni di sincronizzazione ).

* blueprintstatus

  [CQ.wcm.msm.BlueprintStatus](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintStatus)

  BlueprintStatus fornisce un pannello per visualizzare e modificare una blueprint e le relative relazioni Live Copy. La navigazione viene eseguita tramite un [CQ.wcm.msm.BlueprintStatus.Tree](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintStatus.Tree), edizione tramite un [CQ.wcm.msm.BlueprintConfig](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintConfig) e un [CQ.wcm.msm.LiveCopyProperties](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.LiveCopyProperties).

* casella

  [CQ.Ext.BoxComponent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.BoxComponent)

  Classe base per qualsiasi [Componente](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component) che deve essere ridimensionata come una scatola, utilizzando larghezza e altezza.

  BoxComponent fornisce regolazioni automatiche del modello di box per il dimensionamento e il posizionamento e funziona correttamente all&#39;interno del modello di rendering del componente.

* browsedialog

  [CQ.BrowseDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.BrowseDialog)

  La finestra di dialogo Sfoglia consente all&#39;utente di sfogliare il repository per selezionare un percorso. Generalmente viene utilizzato tramite un [BrowseField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.BrowseField).

* browsefield

  [CQ.form.BrowseField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.BrowseField)

  **Obsoleto: usa [CQ.form.PathField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField) invece**

* bulkeditor

  [CQ.wcm.BulkEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor)

  BulkEditor fornisce un motore di ricerca e una griglia per modificare i risultati della ricerca.

  BulkEditor deve essere inserito in un modulo HTML (richiesto dalla funzionalità di importazione). Questo funziona perfettamente con [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog).

* bulkeditorform

  [CQ.wcm.BulkEditorForm](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditorForm)

  BulkEditorForm fornisce [CQ.wcm.BulkEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor) circondato da un modulo HTML. Questa è la versione autonoma del [CQ.wcm.BulkEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor), il modulo HTML è necessario per il pulsante Importa.

* pulsante

  [CQ.Ext.Button](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button)

  Classe Simple Button

* buttongroup

  [CQ.Ext.ButtonGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ButtonGroup)

  Contenitore per un gruppo di pulsanti.

* grafico

  [CQ.Ext.chart.Chart](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart)

  Il pacchetto CQ.Ext.chart fornisce la possibilità di visualizzare i dati con grafici basati su flash. Ogni grafico si associa direttamente a un CQ.Ext.data.Store abilitando gli aggiornamenti automatici del grafico. Per modificare l&#39;aspetto di un grafico, vedere [chartStyle](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart) e [extraStyle](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart) opzioni di configurazione.

* casella di controllo

  [CQ.Ext.form.Checkbox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Checkbox)

  Campo casella di controllo singola. Può essere utilizzata come sostituzione diretta dei campi delle caselle di controllo tradizionali.

* gruppo di caselle di controllo

  [CQ.Ext.form.CheckboxGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.CheckboxGroup)

  Un contenitore di raggruppamento per [CQ.Ext.form.Checkbox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Checkbox) controlli.

* clearcombo

  [CQ.form.ClearableComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ClearableComboBox)

  ClearableComboBox è una casella combinata non modificabile con un trigger che ne cancella il valore.

* colorfield

  [CQ.form.ColorField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ColorField)

  ColorField consente all&#39;utente di immettere un valore esadecimale colore direttamente o utilizzando un [CQ.Ext.ColorMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorMenu).

* colorlist

  [CQ.form.ColorList](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ColorList)

  ColorList consente all&#39;utente di scegliere un colore da un elenco modificabile.

* colormenu

  [CQ.Ext.menu.ColorMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.ColorMenu)

  Un menu contenente un [CQ.Ext.ColorPalette](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorPalette) Componente.

* colorpalette

  [CQ.Ext.ColorPalette](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorPalette)

  Classe semplice della tavolozza dei colori per la scelta dei colori. È possibile eseguire il rendering della palette in qualsiasi contenitore.

* combo

  [CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)

  Un controllo casella combinata con supporto per il completamento automatico, il caricamento remoto, il paging e molte altre funzioni.

  Un controllo ComboBox funziona in modo simile a un HTML tradizionale &lt;select> campo. La differenza è che per inviare il [valueField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox), è necessario specificare un [hiddenName](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox) per creare un input nascosto.

* componente

  [CQ.Ext.Component](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component)

  Classe base per tutti i componenti esterni. Tutte le sottoclassi di Component possono partecipare al ciclo di vita automatizzato di creazione, rendering e distruzione dei componenti Ext fornito da [Contenitore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container) classe. I componenti possono essere aggiunti a un Contenitore tramite [elementi](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container) al momento della creazione del contenitore.

* componentextractor

  [CQ.wcm.ComponentExtractor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ComponentExtractor)

  ComponentExtractor consente all&#39;utente di estrarre componenti da un sito Web o da una pagina.

* componentselector

  [CQ.form.ComponentSelector](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ComponentSelector)

  Una selezione raggruppata e ordinata dei Componenti disponibili.

* componentstyles

  [CQ.form.ComponentStyles](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ComponentStyles)

* compositefield

  [CQ.form.CompositeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.CompositeField)

  Classe base per campi modulo complessi basati su pannello che includono un campo modulo o un gruppo di campi modulo.

* contenitore

  [CQ.Ext.Container](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container)

  Classe base per qualsiasi [CQ.Ext.BoxComponent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.BoxComponent) che possono contenere altri Componenti. I contenitori gestiscono il comportamento di base degli elementi contenenti, ovvero l&#39;aggiunta, l&#39;inserimento e la rimozione di elementi.

  Le classi contenitore più comunemente utilizzate sono [CQ.Ext.Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel), [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window), e [CQ.Ext.TabPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.TabPanel).

* contentfinder

  [CQ.wcm.ContentFinder](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder)

  ContentFinder è un oggetto a due colonne specializzato [Viewport](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Viewport) che contiene il Content Finder effettivo a sinistra e il Content Frame a destra.

* contentfindertab

  [CQ.wcm.ContentFinderTab](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinderTab)

  ContentFinderTab è un pannello specializzato che fornisce le funzioni utilizzate nei pannelli delle schede di [CQ.wcm.ContentFinder](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder). In genere presenta un modulo di ricerca, la Casella di query, e una visualizzazione dati per visualizzare la ricerca.

* cq.workflow.model.combo

  [CQ.wcm.WorkflowModelCombo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.WorkflowModelCombo)

  WorkflowModelCombo è un componente personalizzato [CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox) che mostra un elenco di modelli di flusso di lavoro disponibili.

* cq.workflow.model.selector

  [CQ.wcm.WorkflowModelSelector](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.WorkflowModelSelector)

  WorkflowModelSelector combina WorkflowModelCombo con un&#39;immagine in miniatura del flusso di lavoro e i pulsanti per creare e modificare modelli di flusso di lavoro.

* createsitewizard

  [CQ.wcm.CreateSiteWizard](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.CreateSiteWizard)

  CreateSiteWizard è una procedura guidata dettagliata per la creazione di siti (MSM).

* createversiondialog

  [CQ.wcm.CreateVersionDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.CreateVersionDialog)

  CreateVersionDialog è una finestra di dialogo che consente di creare una versione di una pagina.

* customcontentpanel

  [CQ.CustomContentPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.CustomContentPanel)

  CustomContentPanel è un pannello speciale da utilizzare in [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog): il suo contenuto viene recuperato da e inviato a un URL diverso rispetto agli altri campi nella finestra di dialogo.

* ciclo

  [CQ.Ext.CycleButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.CycleButton)

  Un controllo SplitButton specializzato contenente un menu di [CQ.Ext.menu.CheckItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.CheckItem) elementi. Il pulsante scorre automaticamente ogni voce di menu al clic, facendo clic sul pulsante [modifica](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.CycleButton) (o richiamando il pulsante [changeHandler](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.CycleButton) (se in dotazione) per la voce di menu attiva.

* vista dati

  [CQ.Ext.DataView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DataView)

  Un meccanismo per visualizzare i dati utilizzando modelli di layout e formattazione personalizzati. DataView utilizza un [CQ.Ext.XTemplate](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.XTemplate) come meccanismo di modellazione interno ed è associato a un [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store) in modo che, quando i dati nell&#39;archivio cambiano, la visualizzazione venga automaticamente aggiornata per riflettere le modifiche.

* datefield

  [CQ.Ext.form.DateField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField)

  Fornisce un campo di immissione data con [CQ.Ext.DatePicker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker) a discesa e convalida automatica della data.

* datemenu

  [CQ.Ext.menu.DateMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.DateMenu)

  Un menu contenente un [CQ.Ext.DatePicker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker) Componente.

* datepicker

  [CQ.Ext.DatePicker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker)

  Un selettore di date a comparsa. Questa classe viene utilizzata da [DateField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField) classe per consentire la navigazione e la selezione di date valide.

* datetime

  [CQ.form.DateTime](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.DateTime)

  DateTime consente all&#39;utente di immettere una data e un&#39;ora combinando [CQ.Ext.form.DateField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField) e [CQ.Ext.form.TimeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TimeField).

* finestra di dialogo

  [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog)

  La finestra di dialogo è una finestra speciale con una maschera nel corpo e un gruppo di pulsanti nel piè di pagina. In genere viene utilizzato per modificare il contenuto, ma può anche visualizzare solo le informazioni.

* dialogfieldset

  [CQ.form.DialogFieldSet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.DialogFieldSet)

  DialogFieldSet è un [SetCampi](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FieldSet) da utilizzare in [Finestre di dialogo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog).

* directstore

  [CQ.Ext.data.DirectStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.DirectStore)

  Piccola classe helper per creare un [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store) configurato con un [CQ.Ext.data.DirectProxy](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.DirectProxy) e [CQ.Ext.data.JsonReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonReader) per fare in modo che interagisca con un [CQ.Ext.Direct](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Direct) Lato server [Provider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.direct.Provider) più facile.

* displayfield

  [CQ.Ext.form.DisplayField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DisplayField)

  Campo di testo di sola visualizzazione non convalidato e non inviato.

* editbar

  [CQ.wcm.EditBar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditBar)

  La barra di modifica consente all&#39;utente di modificare il contenuto utilizzando i pulsanti di una barra.

  Sebbene non sia elencato qui, EditBar ha tutti i membri di [CQ.wcm.EditBase](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditBase).

* editor

  [CQ.Ext.Editor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Editor)

  Campo dell’editor di base che gestisce la visualizzazione o l’hiding on-demand e che dispone di alcune logiche integrate di dimensionamento e gestione degli eventi.

* editorgrid

  [CQ.Ext.grid.EditorGridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.EditorGridPanel)

  Questa classe estende [Classe GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) per consentire la modifica delle celle su selezionati [colonne](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.Column). Le colonne modificabili vengono specificate fornendo un [editor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.ColumnModel) nel [configurazione colonna](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.Column).

* editrollover

  [CQ.wcm.EditRollover](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditRollover)

  L’oggetto EditRollover consente all’utente di modificare il contenuto con un doppio clic e fornisce ulteriori azioni di modifica tramite un menu di scelta rapida. L&#39;area modificabile viene indicata da una cornice quando si passa il mouse sul contenuto.

* feedimporter

  [CQ.wcm.FeedImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.FeedImporter)

  La funzione FeedImporter consente all&#39;utente di importare feed RSS o Atom e di creare pagine per ogni voce di feed.

* campo

  [CQ.Ext.form.Field](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Field)

  Classe di base per i campi modulo che fornisce la gestione degli eventi, il dimensionamento, la gestione dei valori e altre funzionalità predefinite.

* set di campi

  [CQ.Ext.form.FieldSet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FieldSet)

  Contenitore standard utilizzato per raggruppare gli elementi in una [modulo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FormPanel).

* fileuploaddialogbutton

  [CQ.form.FileUploadDialogButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.FileUploadDialogButton)

  FileUploadDialogButton crea un pulsante che apre una nuova finestra di dialogo per il caricamento di un file tramite FileUploadField. Può essere utilizzato all’interno di finestre di dialogo di modifica in cui il caricamento deve avvenire in un modulo separato.

* fileuploadfield

  [CQ.form.FileUploadField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.FileUploadField)

  FileUploadField consente all’utente di selezionare un singolo file da caricare.

* findreplacedialog

  [CQ.wcm.FindReplaceDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.FindReplaceDialog)

  FindReplaceDialog è una finestra di dialogo per la ricerca e la sostituzione di token in una pagina e nelle relative pagine figlie.

* flash

  [CQ.Ext.FlashComponent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.FlashComponent)

* griglia

  [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)

  Questa classe rappresenta l&#39;interfaccia principale di un controllo griglia basato su componenti per rappresentare i dati in un formato tabulare di righe e colonne.

* groupingstore

  [CQ.Ext.data.GroupingStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.GroupingStore)

  Implementazione di un negozio specializzato che consente di raggruppare i record in base a uno dei campi disponibili. Viene utilizzato con [CQ.Ext.grid.GroupingView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GroupingView) per provare il modello dati per un GridPanel raggruppato.

* finestra di dialogo

  [CQ.wcm.HeavyMoveDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.HeavyMoveDialog)

  HeavyMoveDialog è una finestra di dialogo per lo spostamento di una pagina e delle relative pagine figlie, che prende in considerazione anche la riattivazione di pagine attivate in precedenza (spostamento &quot;heavy&quot;).

* nascosto

  [CQ.Ext.form.Hidden](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Hidden)

  Campo nascosto di base per la memorizzazione di valori nascosti nei moduli che devono essere passati nell’invio del modulo.

* historybutton

  [CQ.HistoryButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.HistoryButton)

  HistoryButton è una piccola classe helper che fornisce pulsanti avanti e indietro. Di solito sono necessarie due istanze correlate: l’istanza del pulsante Avanti è un semplice pulsante collegato all’istanza del pulsante Indietro che gestisce la cronologia.

* htmleditor

  [CQ.Ext.form.HtmlEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.HtmlEditor)

  Fornisce un componente leggero dell’editor di HTML. Alcune funzioni della barra degli strumenti non sono supportate da Safari e vengono automaticamente nascoste quando necessario. Queste sono riportate nelle opzioni di configurazione, se necessario.

  I pulsanti della barra degli strumenti dell’editor presentano descrizioni comandi definite nel [buttonTips](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.HtmlEditor) proprietà.

* iframedialog

  [CQ.IframeDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.IframeDialog)

  Finestra di dialogo semplice che mostra il contenuto di un iframe e consente l’utilizzo di moduli negli iframe.

* iframepanel

  [CQ.IframePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.IframePanel)

  Pannello contenente un iframe. Semplifica la creazione di iframe, un evento di caricamento iframe e l’accesso ai relativi contenuti.

* inlinetextfield

  [CQ.form.InlineTextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.InlineTextField)

  InlineField è un campo di testo che viene visualizzato come etichetta quando non è attivo.

* jsonstore

  [CQ.Ext.data.JsonStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonStore)

  Piccola classe helper per creare [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)s da dati JSON più semplice. Un JsonStore viene configurato automaticamente con un [CQ.Ext.data.JsonReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonReader).

* etichetta

  [CQ.Ext.form.Label](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Label)

  Campo etichetta di base.

* languagecopydialog

  [CQ.wcm.LanguageCopyDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.LanguageCopyDialog)

  LanguageCopyDialog è una finestra di dialogo per la copia degli alberi del linguaggio.

* verifica collegamenti

  [CQ.wcm.LinkChecker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.LinkChecker)

  LinkChecker è uno strumento che consente di controllare i collegamenti esterni in un sito.

* listview

  [CQ.Ext.list.ListView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.ListView)

  CQ.Ext.list.ListView è un&#39;implementazione rapida e leggera di un [Simile a griglia](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) visualizzazione.

* livecopyproperties

  [CQ.wcm.msm.LiveCopyProperties](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.LiveCopyProperties)

  LiveCopyProperties fornisce un pannello per visualizzare e modificare le proprietà Live Copy ( ereditarietà delle relazioni, trigger di sincronizzazione e azioni di sincronizzazione ).

* lvbooleancolumn

  [CQ.Ext.list.BooleanColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.BooleanColumn)

  Classe di definizione della colonna che esegue il rendering dei campi dati booleani. Consulta la [xtype](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) opzione di configurazione di [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) per ulteriori dettagli.

* lvcolumn

  [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column)

  Questa classe racchiude i dati di configurazione delle colonne da utilizzare nell&#39;inizializzazione di un [ListView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.ListView).

* lvdatecolumn

  [CQ.Ext.list.DateColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.DateColumn)

  Classe Column definition che esegue il rendering di una data passata in base alle impostazioni internazionali predefinite o a una [formato](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.DateColumn). Consulta la [xtype](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) opzione di configurazione di [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) per ulteriori dettagli.

* lvnumcolumn

  [CQ.Ext.list.NumberColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.NumberColumn)

  Classe di definizione Column che esegue il rendering di un campo dati numerico in base a un [formato](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.NumberColumn) stringa. Consulta la [xtype](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) opzione di configurazione di [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) per ulteriori dettagli.

* mediabrowsedialog

  [CQ.MediaBrowseDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.MediaBrowseDialog)

  **Obsoleto: usa [Content Finder](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder) per sfogliare i file multimediali.**

  MediaBrowseDialog è una finestra di dialogo per la visualizzazione del Catalogo multimediale.

* menu

  [CQ.Ext.menu.Menu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Menu)

  Un oggetto menu. Questo è il contenitore al quale è possibile aggiungere voci di menu. Il menu può anche fungere da classe base quando si desidera un menu specializzato basato su un altro componente (ad esempio [CQ.Ext.menu.DateMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.DateMenu) ad esempio).

  I menu possono contenere [voci di menu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Item), o generale [Componente](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component)s.

* menubaseitem

  [CQ.Ext.menu.BaseItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.BaseItem)

  Classe di base per tutti gli elementi che vengono visualizzati nei menu. BaseItem fornisce il rendering predefinito, la gestione dello stato attivato e le opzioni di configurazione di base condivise da tutti i componenti del menu.

* menucheckitem

  [CQ.Ext.menu.CheckItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.CheckItem)

  Aggiunge una voce di menu che contiene una casella di controllo per impostazione predefinita, ma che può anche far parte di un gruppo di opzioni.

* menuitem

  [CQ.Ext.menu.Item](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Item)

  Classe di base per tutte le voci di menu che richiedono funzionalità relative ai menu (come i sottomenu) e non sono elementi di visualizzazione statici. Item estende la funzionalità di base di [CQ.Ext.menu.BaseItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.BaseItem) aggiungendo l’attivazione specifica del menu e facendo clic su gestione.

* menuseparator

  [CQ.Ext.menu.Separator](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Separator)

  Aggiunge una barra di separazione a un menu, utilizzata per dividere gruppi logici di voci di menu. In genere, puoi aggiungere uno di questi utilizzando &quot;-&quot; nella chiamata ad add() o nella configurazione degli elementi, anziché crearne uno direttamente.

* menutextitem

  [CQ.Ext.menu.TextItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.TextItem)

  Aggiunge una stringa di testo statica a un menu, utilizzata come separatore di intestazione o di gruppo.

* metadati

  [CQ.dam.form.Metadata](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.dam.form.Metadata)

  I metadati forniscono un set di campi per determinare le informazioni necessarie per un campo di metadati utilizzato, ad esempio, nelle pagine dell’Editor risorse.

  Fornisce i seguenti campi:

* multicampo

  [CQ.form.MultiField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.MultiField)

  MultiField è un elenco modificabile di campi modulo per la modifica di proprietà con più valori.

* MVT

  [CQ.form.MVT](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.MVT)

  Il componente Multivariate Testing può essere utilizzato per definire e modificare un set di immagini presentate come banner alternati. Le statistiche sui tassi di click-through vengono raccolte per banner.

* casella in entrata delle notifiche

  [CQ.wcm.NotificationInbox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.NotificationInbox)

  NotificationInbox consente all&#39;utente di sottoscrivere azioni WCM e di gestire le notifiche.

* campo numerico

  [CQ.Ext.form.NumberField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.NumberField)

  Campo di testo numerico che fornisce il filtro automatico della sequenza di tasti e la convalida numerica.

* offlineimporter

  [CQ.wcm.OfflineImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.OfflineImporter)

  OfflineImporter è uno strumento che consente di importare e convertire documenti di Microsoft® Word in pagine AEM. Questa funzione consente di modificare il contenuto offline utilizzando un elaboratore di testi.

* ownerdraw

  [CQ.form.OwnerDraw](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.OwnerDraw)

  OwnerDraw può contenere un codice HTML personalizzato (immesso direttamente o recuperato da un URL).

* paging

  [CQ.Ext.PagingToolbar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.PagingToolbar)

  Con l’aumento del numero di record, aumenta il tempo necessario al browser per eseguirne il rendering. Il paging viene utilizzato per ridurre la quantità di dati scambiati con il client.

* pannello

  [CQ.Ext.Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel)

  Il pannello è un contenitore con funzionalità specifiche e componenti strutturali che lo rendono il perfetto elemento di base per le interfacce utente orientate alle applicazioni.

  In virtù della loro ereditarietà da [CQ.Ext.Container](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container).

* riferimento paragrafo

  [CQ.form.ParagraphReference](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ParagraphReference)

  Il campo Riferimento paragrafo consente di sfogliare le pagine e selezionare uno dei relativi paragrafi. È costituito da un campo trigger e da una finestra di dialogo associata per l&#39;esplorazione dei paragrafi.

* password

  [CQ.form.Password](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Password)

  La password è simile a una [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField) ma mantiene privato il suo valore, consentendo agli utenti di immettere dati sensibili.

* pathcompletion

  [CQ.form.PathCompletion](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathCompletion)

  **Obsoleto: usa [CQ.form.PathField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField) invece**

* pathfield

  [CQ.form.PathField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField)

  PathField è un campo di input progettato per i percorsi con completamento del percorso e un pulsante per aprire un [CQ.BrowseDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.BrowseDialog) per la navigazione nell’archivio del server. Può anche sfogliare i paragrafi di pagina per la generazione avanzata di collegamenti.

* avanzamento

  [CQ.Ext.ProgressBar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ProgressBar)

  Componente barra di avanzamento aggiornabile. La barra di avanzamento supporta due diverse modalità: manuale e automatica.

  In modalità manuale, sei responsabile della visualizzazione e dell’aggiornamento (tramite [updateProgress](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ProgressBar)) e cancellando la barra di avanzamento in base alle esigenze dal codice. Questo metodo è più appropriato quando si desidera visualizzare l’avanzamento.

* propertygrid

  [CQ.Ext.grid.PropertyGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.PropertyGrid)

  Implementazione di una griglia specializzata progettata per simulare la griglia di proprietà tradizionale, come generalmente si vede negli IDE di sviluppo. Ogni riga della griglia rappresenta una proprietà di un oggetto e i dati vengono memorizzati come un insieme di coppie nome/valore in [CQ.Ext.grid.PropertyRecord](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.PropertyRecord)s.

* propgrid

  [CQ.PropertyGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.PropertyGrid)

  PropertyGrid è una griglia generica utilizzata per visualizzare e modificare le proprietà degli oggetti.

* suggerimento rapido

  [CQ.Ext.QuickTip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTip)

  suggerimento rapido @xtype classe di descrizioni comandi specifica per le descrizioni comandi che possono essere specificate nel markup e gestite automaticamente dal [CQ.Ext.QuickTips](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTips) dell&#39;istanza. Per ulteriori dettagli ed esempi sull&#39;utilizzo, vedere l&#39;intestazione della classe QuickTips.

* radio

  [CQ.Ext.form.Radio](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Radio)

  Campo radio singolo. Uguale a Casella di controllo, ma viene fornito per comodità per impostare automaticamente il tipo di input. Il raggruppamento delle radio viene gestito automaticamente dal browser se si assegna lo stesso nome a ogni radio di un gruppo.

* radiogroup

  [CQ.Ext.form.RadioGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.RadioGroup)

  Un contenitore di raggruppamento per [CQ.Ext.form.Radio](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Radio) controlli.

* referencesdialog

  [CQ.wcm.ReferencesDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ReferencesDialog)

  La finestra di dialogo Riferimenti (References)Finestra di dialogo consente di visualizzare i riferimenti in una pagina.

* restoreretredialog

  [CQ.wcm.RestoreTreeDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.RestoreTreeDialog)

  RestoreTreeDialog è una finestra di dialogo per il ripristino di una versione precedente di una struttura.

* restore eversiondialog

  [CQ.wcm.RestoreVersionDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.RestoreVersionDialog)

  RestoreVersionDialog è una finestra di dialogo per il ripristino di una versione precedente di una pagina.

* richtext

  [CQ.form.RichText](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.RichText)

  RichText fornisce un campo modulo per la modifica di informazioni di testo formattato (testo RTF).

  Il componente Rich Text offre attualmente le seguenti funzionalità:

* piano di aggregazione

  [CQ.wcm.msm.RolloutPlan](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutPlan)

  Il RolloutPlan fornisce una finestra di dialogo per monitorare l’avanzamento del rollout di una pagina. RolloutPlan è avviato da un [CQ.wcm.msm.RolloutWizard](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutWizard).

* rollout guidato

  [CQ.wcm.msm.RolloutWizard](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutWizard)

  Rollout guidato fornisce una procedura guidata per il rollout di una pagina. RolloutWizard avvia un [CQ.wcm.msm.RolloutPlan](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutPlan).

* searchfield

  [CQ.form.SearchField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SearchField)

  SearchField fornisce un campo di ricerca che fornisce i risultati in un elenco a discesa che può essere utilizzato per la ricerca nel repository.

* selezione

  [CQ.form.Selection](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Selection)

  La selezione consente all’utente di scegliere tra diverse opzioni. Le opzioni possono far parte della configurazione o essere caricate da una risposta JSON. È possibile eseguire il rendering della selezione come menu a discesa (seleziona) o come casella combinata (seleziona più voce di testo libero).

* barra laterale

  [CQ.wcm.Sidekick](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Sidekick)

  Il Sidekick è un supporto mobile che fornisce all’utente gli strumenti comuni per la modifica delle pagine.

* siteadmin

  [CQ.wcm.SiteAdmin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.SiteAdmin)

  SiteAdmin è una console che fornisce funzioni di amministrazione WCM.

* siteimporter

  [CQ.wcm.SiteImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.SiteImporter)

  SiteImporter consente all&#39;utente di importare siti Web completi e di creare progetti iniziali.

* sizefield

  [CQ.form.SizeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SizeField)

  La proprietà SizeField consente di immettere la larghezza e l&#39;altezza (ad esempio, per un&#39;immagine).

* cursore

  [CQ.Ext.Slider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Slider)

  Dispositivo di scorrimento che supporta l&#39;orientamento verticale o orizzontale, le regolazioni della tastiera, lo snap configurabile, il clic sull&#39;asse e l&#39;animazione. Può essere aggiunto come elemento a qualsiasi contenitore. Esempio: ...

* presentazione

  [CQ.form.Slideshow](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Slideshow)

  La presentazione fornisce un componente che può essere utilizzato per definire e modificare un set di immagini e titoli che possono essere visualizzati come presentazione.

  Il componente Presentazione è basato su [CQ.form.SmartImage](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartImage) componente.

* smartfile

  [CQ.form.SmartFile](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartFile)

  SmartFile è un caricatore di file intelligente.

  Se è installato un plug-in di Flash (versione >= 9), i caricamenti vengono eseguiti utilizzando la libreria SWFupload che offre un modo pratico per gestire i caricamenti.

* smartimage

  [CQ.form.SmartImage](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartImage)

  SmartImage è un caricatore di immagini intelligente. Fornisce strumenti per elaborare un’immagine caricata, ad esempio uno strumento per definire le mappe immagine e un ritaglio immagine.

  Il componente è progettato per essere utilizzato in una scheda di dialogo separata.

* distanziatore

  [CQ.Ext.Spacer](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Spacer)

  Utilizzato per fornire uno spazio considerevole in un layout.

* girare

  [CQ.form.Spinner](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Spinner)

  La casella di selezione è un campo trigger per valori numerici, di data o di ora. Il valore può essere aumentato e diminuito utilizzando i trigger su e giù forniti, la rotellina di scorrimento o i tasti.

* splitbutton

  [CQ.Ext.SplitButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.SplitButton)

  Pulsante diviso che fornisce una freccia a discesa incorporata che può attivare un evento separatamente dall&#39;evento clic predefinito del pulsante. In genere viene utilizzato per visualizzare un menu a discesa che fornisce opzioni aggiuntive all’azione del pulsante principale, ma qualsiasi gestore personalizzato può fornire l’implementazione con clic con freccia.

* statico

  [CQ.Static](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Static)

  Lo statico può essere utilizzato per visualizzare testo o HTML arbitrari.

* statistiche

  [CQ.wcm.Statistics](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Statistics)

  Le statistiche visualizzano le impression della pagina sotto forma di grafico. Il widget consente di selezionare un periodo per il quale visualizzare le statistiche.

* archiviare

  [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)

  La classe Store incapsula una cache lato client di [Registra](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Record) oggetti che forniscono dati di input per Componenti quali [GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel), il [CasellaCombinata](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)o [DataView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DataView).

* sugfield

  [CQ.form.SuggestField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SuggestField)

  SuggestField fornisce all&#39;utente suggerimenti in base alla voce immessa.

* commutatore

  [CQ.Switcher](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Switcher)

  Lo switcher fornisce un gruppo di pulsanti per la barra dell’intestazione in una console per passare da un sito Web all’altro, da Risorse digitali, Strumenti, Flusso di lavoro e Sicurezza.

* tableedit

  [CQ.form.TableEdit](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit)

  **Obsoleto: usa [CQ.form.TableEdit2](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit2) invece.**

* tableedit2

  [CQ.form.TableEdit2](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit2)

  TableEdit2 fornisce un widget per la creazione di tabelle.

* tabpanel

  [CQ.Ext.TabPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.TabPanel)

  Contenitore di schede di base. TabPanels può essere utilizzato esattamente come uno standard [CQ.Ext.Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel) per motivi di layout, ma dispongono anche di un supporto speciale per il contenimento dei componenti figlio ([`items`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container)).

* tag

  [CQ.tagging.TagInputField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.tagging.TagInputField)

  ```
  CQ.tagging.TagInputField
  ```

  è un widget di modulo per l’immissione di tag. Dispone di un menu a comparsa per selezionare da tag esistenti, include il completamento automatico e molte altre funzioni.

* textarea

  [CQ.Ext.form.TextArea](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextArea)

  Campo di testo a più righe. Può essere utilizzato come sostituzione diretta dei campi tradizionali dell’area di testo e aggiunge il supporto per il dimensionamento automatico.

* textbutton

  [CQ.TextButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.TextButton)

  Il controllo TextButton fornisce un collegamento di testo con le funzionalità di [CQ.Ext.Button](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button).

* textfield

  [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField)

  Campo di testo di base. Può essere utilizzata come sostituzione diretta degli input di testo tradizionali o come classe base per controlli di input più sofisticati (come [CQ.Ext.form.TextArea](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextArea) e [CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)).

* miniatura

  [CQ.form.Thumbnail](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Thumbnail)

* campo temporale

  [CQ.Ext.form.TimeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TimeField)

  Fornisce un campo di input dell’ora con un elenco a discesa dell’ora e una convalida automatica dell’ora. Esempio: ...

* suggerimento

  [CQ.Ext.Tip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Tip)

  Suggerimento @xtype Questa è la classe base per [CQ.Ext.QuickTip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTip) e [CQ.Ext.Tooltip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Tooltip) che fornisce il layout e il posizionamento di base necessari per tutte le classi basate su suggerimenti. Questa classe può essere utilizzata direttamente per semplici suggerimenti statici.

* titleseparator

  [CQ.menu.TitleSeparator](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.menu.TitleSeparator)

  Aggiunge una barra di separazione a un menu, utilizzata per dividere gruppi logici di voci di menu. Il separatore può anche contenere un titolo.

* barra strumenti

  [CQ.Ext.Toolbar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Toolbar)

  Classe della barra degli strumenti di base. Anche se il [`defaultType`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container) per la barra degli strumenti è [`button`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button), gli elementi della barra degli strumenti (elementi secondari per il contenitore Barra degli strumenti) possono essere virtualmente qualsiasi tipo di componente. Gli elementi della barra degli strumenti possono essere creati esplicitamente tramite i rispettivi costruttori.

* descrizione comando

  [CQ.Ext.ToolTip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ToolTip)

  Implementazione di una descrizione comando standard per fornire informazioni aggiuntive quando si passa il puntatore del mouse su un elemento target. Descrizione comando @xtype.

* treegrid

  [CQ.tree.TreeGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.tree.TreeGrid)

  @xtype treegrid

* treepanel

  [CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)

  Il controllo TreePanel fornisce una rappresentazione dell&#39;interfaccia utente con struttura ad albero dei dati con struttura ad albero.

  [TreeNode](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreeNode)possono contenere metadati utilizzati dall&#39;applicazione nel rispettivo [attributi](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreeNode) proprietà.

* trigger

  [CQ.Ext.form.TriggerField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField)

  Fornisce un comodo wrapper per TextFields che aggiunge un pulsante di attivazione cliccabile (per impostazione predefinita è simile a una casella combinata). Il trigger non ha un&#39;azione predefinita, pertanto devi assegnare una funzione per implementare il gestore di clic del trigger ignorando [onTriggerClick](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField). È possibile creare direttamente un TriggerField, poiché esegue il rendering esattamente come in una casella combinata.

* uploaddialog

  [CQ.UploadDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.UploadDialog)

  L&#39;oggetto UploadDialog consente all&#39;utente di caricare i file nel repository Crea un nuovo oggetto UploadDialog.

* userinfo

  [CQ.UserInfo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.UserInfo)

  Elemento della barra degli strumenti per visualizzare il nome utente corrente e consentire azioni dell’utente come la modifica delle proprietà e della rappresentazione dell’utente.

* viewport

  [CQ.Ext.Viewport](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Viewport)

  Contenitore specifico che rappresenta l’area di applicazione visualizzabile (il riquadro di visualizzazione del browser).

  Il riquadro di visualizzazione si riproduce nel corpo del documento, si ridimensiona automaticamente in base alle dimensioni del riquadro di visualizzazione del browser e gestisce il ridimensionamento delle finestre. È possibile creare un solo riquadro di visualizzazione.

* finestra

  [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)

  Pannello specializzato destinato a essere utilizzato come finestra di applicazione. Le finestre sono mobili, [ridimensionabile](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window), e [trascinabile](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window) per impostazione predefinita. Windows può essere [ingrandito](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window) per riempire il riquadro di visualizzazione, ripristinandone le dimensioni precedenti e può essere [ridurre a icona](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)d.

* xmlstore

  [CQ.Ext.data.XmlStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.XmlStore)

  Piccola classe helper per creare [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)s da dati XML semplificato. Un XmlStore viene configurato automaticamente con un [CQ.Ext.data.XmlReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.XmlReader).

  **cqinclude** Pseudo-tipo che include definizioni di widget da un percorso diverso nell’archivio. Viene utilizzato in genere nelle finestre di dialogo delle pagine. Non esiste alcuna classe widget JavaScript effettiva per questo xtype. Viene elaborata dalla funzione formatData() della classe CQ.Util. Per ulteriori informazioni, consulta questo articolo della knowledge base.
