---
title: Utilizzo di xtype (interfaccia classica)
seo-title: Utilizzo di xtype (interfaccia classica)
description: Scopri tutti gli xtype disponibili con AEM
seo-description: Scopri tutti gli xtype disponibili con AEM
uuid: 6497caa4-2f9b-4f21-9023-88d485fd1d78
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: adb70b43-1b0b-4302-905a-c7612675dabb
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '6414'
ht-degree: 0%

---


# Utilizzo di xtype (interfaccia classica){#using-xtypes-classic-ui}

Questa pagina descrive tutti gli xtype disponibili con Adobe Experience Manager (AEM).

Nel linguaggio ExtJS, un xtype è un nome simbolico assegnato a una classe. È possibile leggere il paragrafo &quot;Component XTypes&quot; della [Overview of ExtJS 2](https://www.sencha.com/learn/overview-of-extjs-2) per una spiegazione dettagliata su cos&#39;è un xtype e come può essere utilizzato.

Per informazioni complete su tutti i widget disponibili in AEM fare riferimento alla [documentazione API dei widget](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html).

Per scoprire in quali componenti è utilizzato un dato xtype in AEM, è possibile utilizzare la seguente query Xpath in CRXDE sostituendo &#39;Casella di controllo&#39; con l&#39;xtype a cui si è interessati:

`//element(*, cq:Widget)[@xtype='checkbox']`

>[!NOTE]
>
>Questa pagina descrive l’utilizzo di xtype ExtJS nell’interfaccia classica.
>
> Adobe consiglia di utilizzare l&#39;interfaccia utente standard, moderna, [touch-enabled](/help/sites-developing/touch-ui-concepts.md) basata su [interfaccia utente Coral](/help/sites-developing/touch-ui-concepts.md#coral-ui) e [interfaccia utente Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components).

## xtype {#xtypes}

Di seguito è riportato un elenco degli xtype disponibili in Adobe Experience Manager:

* annotazione

   [CQ.wcm.Annotation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Annotation)

   La finestra di dialogo è un tipo speciale di finestra con un modulo nel corpo e un gruppo di pulsanti nel piè di pagina. Viene in genere utilizzato per modificare i contenuti, ma può anche visualizzare solo le informazioni.

* arraystore

   [CQ.Ext.data.ArrayStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.ArrayStore)

   Precedentemente noto come &quot;SimpleStore&quot;.

   Classe helper piccola per semplificare la creazione di [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)s dai dati dell&#39;array. Un ArrayStore verrà configurato automaticamente con un [CQ.Ext.data.ArrayReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.ArrayReader).

* asseteditor

   [CQ.dam.AssetEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.dam.AssetEditor)

   Editor risorse utilizzato in DAM Admin.

* assetreferencesearchionedialogo

   [CQ.wcm.AssetReferenceSearchDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.AssetReferenceSearchDialog)

   AssetReferenceSearchDialog è una finestra di dialogo che viene visualizzata se una pagina fa riferimento a risorse o tag.

* blueprintconfig

   [CQ.wcm.msm.BlueprintConfig](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintConfig)

   BlueprintConfig fornisce un pannello per visualizzare le Live Copy di una Blueprint e modificare queste proprietà Blueprint (attivatore di sincronizzazione e azioni di sincronizzazione).

* blueprintstatus

   [CQ.wcm.msm.BlueprintStatus](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintStatus)

   BlueprintStatus fornisce un pannello per visualizzare e modificare una Blueprint e le sue relazioni Live Copy. La navigazione viene eseguita tramite [CQ.wcm.msm.BlueprintStatus.Tree](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintStatus.Tree), l&#39;edizione viene realizzata tramite [CQ.wcm.msm.BlueprintConfig](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintConfig) e un [CQ.wcm.msm.LiveCopyProperties](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.LiveCopyProperties).

* box

   [CQ.Ext.BoxComponent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.BoxComponent)

   Classe di base per qualsiasi [Componente](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component) che deve essere ridimensionata come casella, utilizzando larghezza e altezza.

   BoxComponent fornisce regolazioni automatiche del modello di scatola per il ridimensionamento e il posizionamento e funzionerà correttamente all&#39;interno del modello di rendering del componente.

* browsefinestra di dialogo

   [CQ.BrowseDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.BrowseDialog)

   BrowseDialog consente all&#39;utente di sfogliare la directory archivio per selezionare un percorso. In genere viene utilizzato tramite un [BrowseField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.BrowseField).

* browsefield

   [CQ.form.BrowseField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.BrowseField)

   **Obsoleto: Utilizzare  [CQ.form.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField) PathField**

* bulkeditor

   [CQ.wcm.BulkEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor)

   BulkEditor fornisce un motore di ricerca e una griglia per modificare i risultati della ricerca.

   BulkEditor deve essere inserito in un modulo HTML (richiesto dalla funzionalità di importazione). Questo funziona perfettamente con un [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog).

* bulkeditorform

   [CQ.wcm.BulkEditorForm](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditorForm)

   BulkEditorForm fornisce [CQ.wcm.BulkEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor) circondato da un modulo HTML. Questa è la versione standalone del modulo [CQ.wcm.BulkEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor), HTML è richiesto per il pulsante di importazione.

* pulsante

   [CQ.Ext.Button](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button)

   Classe Button semplice

* buttongroup

   [CQ.Ext.ButtonGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ButtonGroup)

   Contenitore per un gruppo di pulsanti.

* grafico

   [CQ.Ext.chart.Chart](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart)

   Il pacchetto CQ.Ext.chart consente di visualizzare i dati con grafici basati su Flash. Ciascun grafico si collega direttamente a CQ.Ext.data.Store e consente di aggiornare automaticamente il grafico. Per modificare l&#39;aspetto di un grafico, vedere le opzioni di configurazione [chartStyle](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart) e [extraStyle](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart).

* Casella

   [CQ.Ext.form.Checkbox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Checkbox)

   Campo casella di controllo singola. Può essere utilizzato come sostituzione diretta per i campi di controllo tradizionali.

* checkboxgroup

   [CQ.Ext.form.CheckboxGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.CheckboxGroup)

   Contenitore di raggruppamento per i controlli [CQ.Ext.form.Checkbox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Checkbox).

* clear

   [CQ.form.ClearableComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ClearableComboBox)

   ClearableComboBox è una casella combinata non modificabile con un trigger per cancellare il valore.

* colorfield

   [CQ.form.ColorField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ColorField)

   ColorField consente all&#39;utente di immettere un valore esadecimale del colore direttamente o utilizzando un [CQ.Ext.ColorMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorMenu).

* colorlist

   [CQ.form.ColorList](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ColorList)

   ColorList consente all’utente di scegliere un colore da un elenco modificabile.

* colormenu

   [CQ.Ext.menu.ColorMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.ColorMenu)

   Un menu contenente un componente [CQ.Ext.ColorPalette](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorPalette).

* colorpalette

   [CQ.Ext.ColorPalette](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorPalette)

   Classe semplice della palette dei colori per la scelta dei colori. È possibile eseguire il rendering della palette in qualsiasi contenitore.

* combo

   [CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)

   Un controllo combobox con supporto per la compilazione automatica, il caricamento remoto, il paging e molte altre funzioni.

   Un controllo ComboBox funziona in modo simile a un campo HTML tradizionale &lt;select>. La differenza sta nel fatto che per inviare il [valueField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox), è necessario specificare un [hiddenName](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox) per creare un input nascosto.

* componente

   [CQ.Ext.Component](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component)

   Classe base per tutti i componenti Ext. Tutte le sottoclassi di Component possono partecipare al ciclo di vita automatizzato del componente Ext di creazione, rendering e distruzione fornito dalla classe [Container](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container). I componenti possono essere aggiunti a un contenitore tramite l&#39;opzione di configurazione [items](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container) al momento della creazione del contenitore.

* componentestraitore

   [CQ.wcm.ComponentExtender](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ComponentExtractor)

   ComponentExtrattore consente all’utente di estrarre componenti da un sito Web o da una pagina.

* componentSelector

   [CQ.form.ComponentSelector](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ComponentSelector)

   Una selezione raggruppata e ordinata di componenti disponibili.

* componentStyles

   [CQ.form.ComponentStyles](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ComponentStyles)

* compositefield

   [CQ.form.CompositeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.CompositeField)

   Classe base per campi modulo complessi e basati su pannelli che includono un campo modulo o un gruppo di campi modulo.

* container

   [CQ.Ext.Container](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container)

   Classe di base per qualsiasi [CQ.Ext.BoxComponent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.BoxComponent) che può contenere altri componenti. I contenitori consentono di gestire il comportamento di base degli elementi che contengono, ovvero aggiungere, inserire e rimuovere elementi.

   Le classi Container utilizzate più comunemente sono [CQ.Ext.Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel), [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window) e [CQ.Ext.TabPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.TabPanel).

* contentfinder

   [CQ.wcm.ContentFinder](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder)

   ContentFinder è una colonna specializzata di due colonne [Viewport](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Viewport) che contiene l&#39;effettivo Content Finder a sinistra e la cornice contenuto a destra.

* contentfindertab

   [CQ.wcm.ContentFinderTab](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinderTab)

   ContentFinderTab è un pannello specializzato che fornisce funzionalità utilizzate nei pannelli delle schede di [CQ.wcm.ContentFinder](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder). Generalmente, per visualizzare la ricerca sono disponibili un modulo di ricerca, la casella Query, e una visualizzazione dati.

* cq.workflow.model.combo

   [CQ.wcm.WorkflowModelCombo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.WorkflowModelCombo)

   WorkflowModelCombo è un [CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox) personalizzato che mostra un elenco di modelli di workflow disponibili.

* cq.workflow.model.selector

   [CQ.wcm.WorkflowModelSelector](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.WorkflowModelSelector)

   WorkflowModelSelector combina un WorkflowModelCombo con una miniatura del flusso di lavoro e pulsanti per creare e modificare modelli di workflow.

* createsitewcomunitari

   [CQ.wcm.CreateSiteWizard](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.CreateSiteWizard)

   CreateSiteWizard è una procedura guidata dettagliata per la creazione di siti (MSM).

* createeversiondialog

   [CQ.wcm.CreateVersionDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.CreateVersionDialog)

   CreateVersionDialog è una finestra di dialogo che consente di creare una nuova versione di una pagina.

* customcontentpanel

   [CQ.CustomContentPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.CustomContentPanel)

   CustomContentPanel è un tipo speciale di pannello da utilizzare in [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog): Il contenuto viene recuperato e inviato a un URL diverso rispetto agli altri campi della finestra di dialogo.

* cycle

   [CQ.Ext.CycleButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.CycleButton)

   Pulsante SplitButton specializzato contenente un menu di elementi [CQ.Ext.menu.CheckItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.CheckItem). Il pulsante passa automaticamente in rassegna ogni voce di menu quando si fa clic, sollevando l&#39;evento [change](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.CycleButton) del pulsante (o chiamando la funzione [changeHandler](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.CycleButton) del pulsante, se fornita) per la voce di menu attiva.

* dataView

   [CQ.Ext.DataView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DataView)

   Meccanismo per visualizzare i dati utilizzando modelli di layout e formattazione personalizzati. DataView utilizza un [CQ.Ext.XTemplate](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.XTemplate) come meccanismo di modellazione interno ed è associato a un [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store) in modo che, quando i dati nello store cambiano, la visualizzazione venga automaticamente aggiornata per riflettere le modifiche.

* datefield

   [CQ.Ext.form.DateField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField)

   Fornisce un campo di immissione data con un menu a discesa [CQ.Ext.DatePicker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker) e una convalida automatica della data.

* datemenu

   [CQ.Ext.menu.DateMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.DateMenu)

   Un menu contenente un componente [CQ.Ext.DatePicker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker).

* datepicker

   [CQ.Ext.DatePicker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker)

   Selettore data popup. Questa classe viene utilizzata dalla classe [DateField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField) per consentire la navigazione e la selezione di date valide.

* datetime

   [CQ.form.DateTime](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.DateTime)

   La proprietà DateTime consente all&#39;utente di immettere una data e un&#39;ora combinando [CQ.Ext.form.DateField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField) e [CQ.Ext.form.TimeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TimeField).

* finestra di dialogo

   [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog)

   La finestra di dialogo è un tipo speciale di finestra con un modulo nel corpo e un gruppo di pulsanti nel piè di pagina. Viene in genere utilizzato per modificare i contenuti, ma può anche visualizzare solo le informazioni.

* dialogfieldità

   [CQ.form.DialogFieldSet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.DialogFieldSet)

   DialogFieldSet è un [FieldSet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FieldSet) da utilizzare in [Dialogs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog).

* directstore

   [CQ.Ext.data.DirectStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.DirectStore)

   Classe helper piccola per creare un [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store) configurato con un [CQ.Ext.data.DirectProxy](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.DirectProxy) e [CQ.Ext.data.JsonReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonReader) per interagire con un [CQ.Ext.Direct](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Direct) lato server a8/>Provider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.direct.Provider) più semplice.[

* displayfield

   [CQ.Ext.form.DisplayField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DisplayField)

   Campo di testo di sola visualizzazione che non è convalidato e non è inviato.

* editbar

   [CQ.wcm.EditBar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditBar)

   EditBar consente all&#39;utente di modificare il contenuto utilizzando i pulsanti di una barra.

   Anche se non è elencato qui, EditBar dispone di tutti i membri di [CQ.wcm.EditBase](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditBase).

* editor

   [CQ.Ext.Editor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Editor)

   Campo dell&#39;editor di base che gestisce la visualizzazione/l&#39;occultamento su richiesta e che include una logica di ridimensionamento e gestione degli eventi integrata.

* editorgrid

   [CQ.Ext.grid.EditorGridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.EditorGridPanel)

   Questa classe estende la [GridPanel Class](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) per fornire la modifica delle celle sulle [colonne ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.Column) selezionate. Le colonne modificabili vengono specificate fornendo un [editor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.ColumnModel) nella [configurazione delle colonne](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.Column).

* editrollover

   [CQ.wcm.EditRollover](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditRollover)

   EditRollover permette all’utente di modificare il contenuto con un doppio clic e fornisce ulteriori azioni di modifica tramite un menu di scelta rapida. L&#39;area modificabile è indicata da un fotogramma quando il mouse passa il mouse sul contenuto.

* Feed

   [CQ.wcm.FeedImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.FeedImporter)

   FeedImporter consente all&#39;utente di importare feed RSS o Atom e creare pagine per ogni voce di feed.

* o in un altro campo

   [CQ.Ext.form.Field](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Field)

   Classe base per i campi modulo che forniscono la gestione degli eventi, il ridimensionamento, la gestione dei valori e altre funzionalità predefinite.

* fielabilità

   [CQ.Ext.form.FieldSet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FieldSet)

   Contenitore standard utilizzato per raggruppare gli elementi all&#39;interno di un [modulo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FormPanel). ...

* fileuploaddialogbutton

   [CQ.form.FileUploadDialogButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.FileUploadDialogButton)

   FileUploadDialogButton crea un pulsante che apre una nuova finestra di dialogo per il caricamento di un file tramite FileUploadField. Può essere utilizzato all’interno di finestre di dialogo di modifica, nelle quali il caricamento deve avvenire in un modulo separato.

* fileuploadfield

   [CQ.form.FileUploadField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.FileUploadField)

   FileUploadField consente all&#39;utente di selezionare un singolo file da caricare.

* findresegnaposto, finestra

   [CQ.wcm.FindReplaceDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.FindReplaceDialog)

   La finestra di dialogo TrovaSostituisci consente di trovare e sostituire i token in una pagina e nelle relative pagine figlie.

* flash

   [CQ.Ext.FlashComponent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.FlashComponent)

* griglia

   [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)

   Questa classe rappresenta l&#39;interfaccia principale di un controllo griglia basato su componente per rappresentare i dati in un formato tabulare di righe e colonne.

* groupingstore

   [CQ.Ext.data.GroupingStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.GroupingStore)

   Implementazione dell&#39;archivio specializzata che prevede il raggruppamento dei record in base a uno dei campi disponibili. Questa funzione è in genere utilizzata insieme a [CQ.Ext.grid.GroupingView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GroupingView) per dimostrare il modello dati per un gruppo GridPanel.

* Heymovedialog

   [CQ.wcm.HeavyMoveDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.HeavyMoveDialog)

   HeavyMoveDialog è una finestra di dialogo per lo spostamento di una pagina e delle relative pagine figlie, anche in considerazione della riattivazione di pagine precedentemente attivate (spostamento pesante).

* nascosto

   [CQ.Ext.form.Hidden](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Hidden)

   Campo nascosto di base per l&#39;archiviazione dei valori nascosti nei moduli che devono essere passati nell&#39;invio del modulo.

* storybutton

   [CQ.HistoryButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.HistoryButton)

   HistoryButton è una piccola classe helper che consente di fornire facilmente i pulsanti indietro e avanti. In genere sono necessarie due istanze correlate: L&#39;istanza del pulsante avanti è un semplice pulsante collegato all&#39;istanza del pulsante indietro che gestisce la cronologia.

* htmleditor

   [CQ.Ext.form.HtmlEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.HtmlEditor)

   Fornisce un componente Editor HTML leggero. Alcune funzioni della barra degli strumenti non sono supportate da Safari e saranno automaticamente nascoste quando necessario. Se necessario, tali opzioni sono riportate nelle opzioni di configurazione.

   I pulsanti della barra degli strumenti dell&#39;editor contengono descrizioni comandi definite nella proprietà [buttonTips](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.HtmlEditor).

* iframe dialog

   [CQ.IframeDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.IframeDialog)

   Una finestra di dialogo semplice che mostra il contenuto di un iframe e consente la creazione di moduli in iframe.

* iframepanel

   [CQ.IframePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.IframePanel)

   Pannello contenente un iframe. Fornisce la creazione semplice di iframe, un evento di caricamento iframe e un facile accesso ai contenuti dell&#39;iframe.

* inlinetextfield

   [CQ.form.InlineTextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.InlineTextField)

   InlineField è un campo di testo visualizzato come etichetta quando non è attivo.

* jsonstore

   [CQ.Ext.data.JsonStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonStore)

   Classe helper piccola per semplificare la creazione di [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)s dai dati JSON. Un oggetto JsonStore verrà configurato automaticamente con un [CQ.Ext.data.JsonReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonReader).

* label

   [CQ.Ext.form.Label](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Label)

   Etichetta di base.

* languagecopydialog

   [CQ.wcm.LanguageCopyDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.LanguageCopyDialog)

   LanguageCopyDialog è una finestra di dialogo per la copia delle strutture ad albero della lingua.

* linkchecker

   [CQ.wcm.LinkChecker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.LinkChecker)

   LinkChecker è uno strumento per controllare i collegamenti esterni in un sito.

* listview

   [CQ.Ext.list.ListView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.ListView)

   CQ.Ext.list.ListView è un&#39;implementazione rapida e leggera di una [Grid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) come la vista.

* livecopyproperties

   [CQ.wcm.msm.LiveCopyProperties](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.LiveCopyProperties)

   LiveCopyProperties offre un pannello per visualizzare e modificare le proprietà Live Copy (ereditarietà delle relazioni, attivatore di sincronizzazione e azioni di sincronizzazione).

* lvbooleancolumn

   [CQ.Ext.list.BooleanColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.BooleanColumn)

   Una classe di definizione delle colonne che esegue il rendering dei campi dati booleani. Per ulteriori informazioni, vedere l&#39;opzione di configurazione [xtype](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) di [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column).

* lvcolumn

   [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column)

   Questa classe racchiude i dati di configurazione delle colonne da utilizzare per l&#39;inizializzazione di una [ListView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.ListView).

* lvdatecolumn

   [CQ.Ext.list.DateColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.DateColumn)

   Una classe di definizione della colonna che esegue il rendering di una data passata in base alle impostazioni internazionali predefinite oppure un [formato ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.DateColumn) configurato. Per ulteriori informazioni, vedere l&#39;opzione di configurazione [xtype](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) di [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column).

* lvnumbercolumn

   [CQ.Ext.list.NumberColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.NumberColumn)

   Una classe di definizione delle colonne che esegue il rendering di un campo di dati numerici in base a una stringa [format](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.NumberColumn). Per ulteriori informazioni, vedere l&#39;opzione di configurazione [xtype](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) di [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column).

* mediabrowsedialog

   [CQ.MediaBrowseDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.MediaBrowseDialog)

   **Obsoleto: Utilizzate  [Content ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder) Finder per sfogliare i file multimediali.**

   MediaBrowseDialog è una finestra di dialogo che consente di esplorare la libreria multimediale.

* menu

   [CQ.Ext.menu.Menu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Menu)

   Un oggetto menu. Questo è il contenitore a cui è possibile aggiungere voci di menu. Il menu può essere utilizzato anche come classe base quando si desidera un menu specializzato basato su un altro componente (ad esempio [CQ.Ext.menu.DateMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.DateMenu)).

   I menu possono contenere [voci di menu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Item) o [Componente](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component)generale.

* menubaseitem

   [CQ.Ext.menu.BaseItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.BaseItem)

   La classe base per tutti gli elementi di cui viene eseguito il rendering nei menu. BaseItem fornisce il rendering predefinito, la gestione dello stato attivato e le opzioni di configurazione di base condivise da tutti i componenti del menu.

* menucheckitem

   [CQ.Ext.menu.CheckItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.CheckItem)

   Aggiunge una voce di menu che per impostazione predefinita contiene una casella di controllo, ma che può anche far parte di un gruppo di pulsanti di scelta.

* menuitem

   [CQ.Ext.menu.Item](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Item)

   Una classe base per tutte le voci di menu che richiedono funzionalità correlate ai menu (come i sottomenu) e non sono elementi di visualizzazione statici. L&#39;elemento estende la funzionalità di base di [CQ.Ext.menu.BaseItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.BaseItem) aggiungendo l&#39;attivazione specifica del menu e la gestione dei clic.

* menuseparatore

   [CQ.Ext.menu.Separator](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Separator)

   Aggiunge una barra di separazione a un menu, utilizzata per dividere i gruppi logici di voci di menu. In genere si aggiunge uno di questi utilizzando &quot;-&quot; nella chiamata a add() o nella configurazione degli elementi anziché crearne uno direttamente.

* menutextitem

   [CQ.Ext.menu.TextItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.TextItem)

   Aggiunge una stringa di testo statica a un menu, in genere utilizzata come separatore di intestazione o di gruppo.

* metadata

   [CQ.dam.form.Metadata](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.dam.form.Metadata)

   I metadati forniscono una serie di campi per determinare le informazioni richieste per un campo di metadati, come utilizzato ad esempio nelle pagine dell’editor di risorse.

   Contiene i campi seguenti:

* multifield

   [CQ.form.MultiField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.MultiField)

   MultiField è un elenco modificabile di campi modulo per la modifica di proprietà multivalore.

* mvt

   [CQ.form.MVT](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.MVT)

   Il componente Test multivariato può essere usato per definire e modificare un set di immagini presentate come banner alternativi. Le statistiche relative ai tassi di click-through vengono raccolte per banner.

* notificationinbox

   [CQ.wcm.NotificationInbox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.NotificationInbox)

   NotificationInbox consente all&#39;utente di iscriversi alle azioni WCM e gestire le notifiche.

* numberfield

   [CQ.Ext.form.NumberField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.NumberField)

   Campo di testo numerico che fornisce il filtraggio automatico dei tasti e la convalida numerica.

* offline importer

   [CQ.wcm.OfflineImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.OfflineImporter)

   OfflineImporter è uno strumento per importare e convertire documenti di Microsoft Word in pagine AEM. Questa funzione consente di modificare il contenuto offline utilizzando un elaboratore di testi.

* ownerdraw

   [CQ.form.OwnerDraw](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.OwnerDraw)

   OwnerDraw può contenere codice HTML personalizzato (immesso direttamente o recuperato da un URL).

* paging

   [CQ.Ext.PagingToolbar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.PagingToolbar)

   Con l&#39;aumentare della quantità di record, aumenta il tempo necessario al browser per eseguirne il rendering. La funzione di paging consente di ridurre la quantità di dati scambiati con il cliente.

* panel

   [CQ.Ext.Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel)

   Il pannello è un contenitore con funzionalità specifiche e componenti strutturali che lo rendono il perfetto componente di base per le interfacce utente orientate alle applicazioni.

   I pannelli sono, in virtù della loro ereditarietà da [CQ.Ext.Container](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container).

* paragraphreference

   [CQ.form.ParagraphReference](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ParagraphReference)

   Il campo Riferimento paragrafo consente di sfogliare le pagine e selezionare uno dei paragrafi corrispondenti. È costituito da un campo di attivazione e da una finestra di dialogo di ricerca paragrafo associata.

* password

   [CQ.form.Password](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Password)

   La password è simile a una [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField), ma ne mantiene il valore privato, consentendo agli utenti di immettere dati riservati.

* pathcompletion

   [CQ.form.PathCompletion](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathCompletion)

   **Obsoleto: Utilizzare  [CQ.form.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField) PathField**

* pathfield

   [CQ.form.PathField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField)

   PathField è un campo di input progettato per i percorsi con completamento del percorso e un pulsante per aprire un [CQ.BrowseDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.BrowseDialog) per esplorare l&#39;archivio del server. Può anche sfogliare i paragrafi della pagina per la generazione avanzata di collegamenti.

* avanzamento

   [CQ.Ext.ProgressBar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ProgressBar)

   Un componente della barra di avanzamento aggiornabile. La barra di avanzamento supporta due modalità diverse: manuale e automatico.

   In modalità manuale, è necessario visualizzare, aggiornare (tramite [updateProgress](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ProgressBar)) e cancellare la barra di avanzamento in base alle esigenze dal codice. Questo metodo è più adatto per mostrare l’avanzamento.

* propertyGrid

   [CQ.Ext.grid.PropertyGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.PropertyGrid)

   Un&#39;implementazione specializzata della griglia destinata a imitare la tradizionale griglia di proprietà, come si vede di solito negli IDE di sviluppo. Ogni riga della griglia rappresenta una proprietà di un oggetto e i dati vengono memorizzati come un insieme di coppie nome/valore in [CQ.Ext.grid.PropertyRecord](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.PropertyRecord)s.

* propgrid

   [CQ.PropertyGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.PropertyGrid)

   PropertyGrid è una griglia generica utilizzata per visualizzare e modificare le proprietà degli oggetti.

* descrizione rapida

   [CQ.Ext.QuickTip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTip)

   @xtype quicktip Una classe di descrizioni comandi specializzata per le descrizioni comandi che possono essere specificate nella marcatura e gestite automaticamente dall&#39;istanza globale [CQ.Ext.QuickTips](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTips). Per ulteriori dettagli sull&#39;utilizzo e per ulteriori esempi, consultate l&#39;intestazione della classe QuickTips.

* radio

   [CQ.Ext.form.Radio](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Radio)

   Campo di scelta singolo. Come casella di controllo, ma è utile per impostare automaticamente il tipo di input. I raggruppamenti di pulsanti di scelta vengono gestiti automaticamente dal browser se assegnate a ciascuna radio di un gruppo lo stesso nome.

* radiogroup

   [CQ.Ext.form.RadioGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.RadioGroup)

   Contenitore di raggruppamento per i controlli [CQ.Ext.form.Radio](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Radio).

* referencesdialog

   [CQ.wcm.ReferencesDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ReferencesDialog)

   La finestra di dialogo References (Riferimenti) è una finestra di dialogo che consente di visualizzare i riferimenti su una pagina.

* restoretredialog

   [CQ.wcm.RestoreTreeDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.RestoreTreeDialog)

   RestoreTreeDialog è una finestra di dialogo che consente di ripristinare una versione precedente di una struttura ad albero.

* restoreversiondialog

   [CQ.wcm.RestoreVersionDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.RestoreVersionDialog)

   RestoreVersionDialog è una finestra di dialogo che consente di ripristinare una versione precedente di una pagina.

* richtext

   [CQ.form.RichText](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.RichText)

   RichText fornisce un campo modulo per la modifica delle informazioni di testo formattate (RTF).

   Il componente RichText offre attualmente le seguenti funzioni:

* rolloutplan

   [CQ.wcm.msm.RolloutPlan](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutPlan)

   RolloutPlan offre una finestra di dialogo per visualizzare l’avanzamento dell’implementazione di una pagina. RolloutPlan viene avviato da un [CQ.wcm.msm.RolloutWizard](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutWizard).

* rolloutwycè

   [CQ.wcm.msm.RolloutWizard](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutWizard)

   RolloutWizard fornisce una procedura guidata per il rollout di una pagina. RolloutWizard avvia un [CQ.wcm.msm.RolloutPlan](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutPlan).

* search field

   [CQ.form.SearchField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SearchField)

   SearchField fornisce un campo di ricerca che fornisce i risultati in un elenco a discesa che può essere utilizzato per la ricerca nell&#39;archivio.

* selezione

   [CQ.form.Selection](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Selection)

   La selezione consente all&#39;utente di scegliere tra diverse opzioni. Le opzioni possono essere parte della configurazione o caricate da una risposta JSON. È possibile eseguire il rendering della selezione come menu a discesa (selezione) oppure come una casella di controllo (selezione più voci di testo gratuite).

* barra laterale

   [CQ.wcm.Sidekick](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Sidekick)

   La barra laterale è un assistente mobile che fornisce all’utente gli strumenti più comuni per la modifica delle pagine.

* siteadmin

   [CQ.wcm.SiteAdmin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.SiteAdmin)

   SiteAdmin è una console che fornisce funzioni di amministrazione WCM.

* siteimporter

   [CQ.wcm.SiteImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.SiteImporter)

   SiteImporter consente all&#39;utente di importare siti Web completi e creare progetti iniziali.

* sizefield

   [CQ.form.SizeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SizeField)

   Il campo SizeField consente all’utente di immettere la larghezza e l’altezza (ad esempio per un’immagine).

* cursore

   [CQ.Ext.Slider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Slider)

   Slider che supporta l&#39;orientamento verticale o orizzontale, le regolazioni della tastiera, l&#39;aggancio configurabile, il clic sull&#39;asse e l&#39;animazione. Può essere aggiunto come elemento a qualsiasi contenitore. Esempio di utilizzo: ...

* slideshow

   [CQ.form.Slideshow](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Slideshow)

   La presentazione fornisce un componente che può essere usato per definire e modificare un set di immagini e titoli di immagini da visualizzare come presentazione.

   Il componente Presentazione si basa sul componente [CQ.form.SmartImage](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartImage).

* smartfile

   [CQ.form.SmartFile](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartFile)

   SmartFile è un caricatore intelligente di file.

   Se è installato un plug-in di Flash (versione >= 9), i caricamenti vengono eseguiti utilizzando la libreria di caricamento SWF che fornisce un metodo pratico per gestire i caricamenti.

* smartphone

   [CQ.form.SmartImage](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartImage)

   SmartImage è un caricatore intelligente di immagini. Fornisce strumenti per elaborare un’immagine caricata, ad esempio uno strumento per definire mappe immagine e un ritaglio immagine.

   Il componente è destinato principalmente all’uso in una scheda di dialogo separata.

* distanziatore

   [CQ.Ext.Spacer](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Spacer)

   Utilizzato per fornire uno spazio di dimensioni in un layout.

* spinner

   [CQ.form.Spinner](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Spinner)

   Lo Spinner è un campo di attivazione per i valori numerici, di data o di ora. Il valore può essere aumentato e diminuito utilizzando i trigger forniti, la rotellina di scorrimento o i tasti.

* splitbutton

   [CQ.Ext.SplitButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.SplitButton)

   Un pulsante di divisione che fornisce una freccia a discesa incorporata in grado di attivare un evento separatamente dall&#39;evento clic predefinito del pulsante. In genere viene utilizzato per visualizzare un menu a discesa che fornisce opzioni aggiuntive per l&#39;azione del pulsante principale, ma qualsiasi gestore personalizzato può fornire l&#39;implementazione del clic freccia.

* statici

   [CQ.Static](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Static)

   Static può essere utilizzato per visualizzare testo arbitrario o HTML.

* statistica

   [CQ.wcm.Statistics](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Statistics)

   Statistiche visualizza le impression della pagina come grafico. Il widget consente di selezionare un periodo. Le statistiche devono essere visualizzate.

* store

   [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)

   La classe Store racchiude una cache lato client di oggetti [Record](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Record) che forniscono dati di input per componenti come [GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel), [ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox) o [DataView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DataView).

* suggestfield

   [CQ.form.SuggestField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SuggestField)

   Il campo SuggestField fornisce all&#39;utente suggerimenti basati sulla voce corrispondente.

* commutatore

   [CQ.Switcher](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Switcher)

   Lo switcher fornisce un gruppo di pulsanti per la barra dell’intestazione di una console che consente di passare da Siti Web, Risorse digitali, Strumenti, Flusso di lavoro e Sicurezza.

* tableedit

   [CQ.form.TableEdit](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit)

   **Obsoleto: Utilizzare  [CQ.form.TableEdit2](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit2) invece.**

* tableedit2

   [CQ.form.TableEdit2](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit2)

   TableEdit2 fornisce un widget per la creazione di tabelle.

* tabpanel

   [CQ.Ext.TabPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.TabPanel)

   Contenitore tabulazione di base. TabPanels può essere utilizzato esattamente come un [CQ.Ext.Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel) standard a scopo di layout, ma anche un supporto speciale per i componenti secondari contenenti componenti secondari ([`items`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container)).

* tag

   [CQ.tagging.TagInputField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.tagging.TagInputField)

   ```
   CQ.tagging.TagInputField
   ```

   è un widget modulo per l’immissione di tag. Dispone di un menu a comparsa per la selezione tra i tag esistenti, include il completamento automatico e molte altre funzioni.

* textarea

   [CQ.Ext.form.TextArea](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextArea)

   Campo di testo su più righe. Può essere utilizzato come sostituzione diretta per i campi di testo tradizionali, oltre a supportare il ridimensionamento automatico.

* textbutton

   [CQ.TextButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.TextButton)

   TextButton fornisce un collegamento di testo con le funzionalità di [CQ.Ext.Button](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button).

* textfield

   [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField)

   Campo di testo di base. Può essere utilizzato come sostituzione diretta per gli input di testo tradizionali o come classe base per controlli di input più sofisticati (come [CQ.Ext.form.TextArea](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextArea) e [CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)).

* thumbnail

   [CQ.form.Thumbnail](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Thumbnail)

* timefield

   [CQ.Ext.form.TimeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TimeField)

   Fornisce un campo di immissione dell&#39;ora con un menu a discesa e una convalida automatica dell&#39;ora. Esempio di utilizzo: ...

* tip

   [CQ.Ext.Tip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Tip)

   @xtype tip Questa è la classe base per [CQ.Ext.QuickTip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTip) e [CQ.Ext.Tooltip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Tooltip) che fornisce il layout di base e il posizionamento richiesti da tutte le classi basate su suggerimenti. Questa classe può essere utilizzata direttamente per suggerimenti semplici e statici.

* titleseparator

   [CQ.menu.TitleSeparator](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.menu.TitleSeparator)

   Aggiunge una barra di separazione a un menu, utilizzata per dividere i gruppi logici di voci di menu. Il separatore può inoltre avere un titolo.

* toolbar

   [CQ.Ext.Toolbar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Toolbar)

   Basic Toolbar, classe. Sebbene il [`defaultType`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container) per la barra degli strumenti sia [`button`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button), gli elementi della barra degli strumenti (elementi secondari per il contenitore della barra degli strumenti) possono essere praticamente qualsiasi tipo di componente. Gli elementi della barra degli strumenti possono essere creati in modo esplicito tramite i relativi costruttori.

* tooltip

   [CQ.Ext.ToolTip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ToolTip)

   Implementazione standard delle descrizioni comandi per fornire informazioni aggiuntive quando si passa il puntatore su un elemento di destinazione. @xtype tooltip.

* burbero

   [CQ.tree.TreeGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.tree.TreeGrid)

   @xtype Treegrid

* treppiede

   [CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)

   TreePanel offre una rappresentazione ad albero dell&#39;interfaccia utente dei dati ad albero.

   [I ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreeNode)TreeNodes aggiunti al pannello ad albero possono contenere i metadati utilizzati dall&#39;applicazione nella relativa proprietà  [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreeNode) attributesproperty.

* trigger

   [CQ.Ext.form.TriggerField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField)

   Fornisce un pratico wrapper per TextFields che aggiunge un pulsante di attivazione selezionabile (per impostazione predefinita è simile a una casella combinata). L&#39;attivatore non ha azioni predefinite, pertanto è necessario assegnare una funzione per implementare il gestore di clic attivatore sovrascrivendo [onTriggerClick](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField). È possibile creare un campo TriggerField direttamente, così come viene riprodotto esattamente come un combobox.

* uploaddialog

   [CQ.UploadDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.UploadDialog)

   La finestra di dialogo Carica consente all’utente di caricare i file nell’archivio. Crea una nuova finestra di dialogo Carica.

* userinfo

   [CQ.UserInfo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.UserInfo)

   Elemento della barra degli strumenti per visualizzare il nome utente corrente e consentire azioni da parte dell&#39;utente come la modifica delle proprietà utente e la rappresentazione.

* viewport

   [CQ.Ext.Viewport](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Viewport)

   Contenitore specializzato che rappresenta l&#39;area visibile dell&#39;applicazione (la finestra del browser).

   Il viewport esegue il rendering sul corpo del documento, si ridimensiona automaticamente alle dimensioni della finestra del browser e gestisce il ridimensionamento delle finestre. È possibile creare un solo visualizzatore.

* finestra

   [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)

   Pannello specializzato destinato a essere utilizzato come finestra dell’applicazione. Le finestre sono mobili, [ridimensionabili](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window) e [trascinabili](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window) per impostazione predefinita. Le finestre possono essere [ingrandite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window) per riempire la finestra, ripristinate alle dimensioni precedenti e possono essere [ridotte a icona](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)d.

* xmlstore

   [CQ.Ext.data.XmlStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.XmlStore)

   Classe helper piccola per semplificare la creazione di [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)s dai dati XML. Un XmlStore verrà configurato automaticamente con un [CQ.Ext.data.XmlReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.XmlReader).

   **** cqincludePseudo xtype che include definizioni di widget da un percorso diverso nell’archivio. Viene utilizzato più frequentemente nelle finestre di dialogo delle pagine. Nessuna classe widget JavaScript effettiva per questo xtype. Viene elaborata dalla funzione formatData() della classe CQ.Util. Per ulteriori informazioni, consultate questo articolo della knowledge base.
