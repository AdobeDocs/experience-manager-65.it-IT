---
title: Utilizzo di xtype (interfaccia classica)
seo-title: Using xtypes (Classic UI)
description: Scopri tutti gli xtype disponibili con AEM
seo-description: Learn about all the xtypes that are available with AEM
uuid: 6497caa4-2f9b-4f21-9023-88d485fd1d78
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: adb70b43-1b0b-4302-905a-c7612675dabb
exl-id: 06ca4e6d-9ab7-4c5b-905c-07c448632f2b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '6400'
ht-degree: 0%

---

# Utilizzo di xtype (interfaccia classica){#using-xtypes-classic-ui}

Questa pagina descrive tutti gli xtype disponibili con Adobe Experience Manager (AEM).

Nel linguaggio ExtJS, un xtype è un nome simbolico assegnato a una classe. È possibile leggere il paragrafo &quot;Tipi di testo componenti&quot; del [Panoramica di ExtJS 2](https://www.sencha.com/learn/overview-of-extjs-2) per una spiegazione dettagliata su cosa è un xtype e come può essere utilizzato.

Per informazioni complete su tutti i widget disponibili in AEM fare riferimento al [documentazione API per widget](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html).

Per scoprire in quali componenti viene utilizzato in AEM un xtype specifico, puoi utilizzare la seguente query Xpath in CRXDE sostituendo &quot;casella di controllo&quot; con l&#39;xtype interessato:

`//element(*, cq:Widget)[@xtype='checkbox']`

>[!NOTE]
>
>Questa pagina descrive l’utilizzo di xtype ExtJS nell’interfaccia classica.
>
>L’Adobe consiglia di sfruttare lo standard, moderno, [interfaccia touch](/help/sites-developing/touch-ui-concepts.md) basato su [Interfaccia Coral](/help/sites-developing/touch-ui-concepts.md#coral-ui) e [Interfaccia Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components).

## xtypes {#xtypes}

Di seguito è riportato un elenco degli xtype disponibili in Adobe Experience Manager:

* annotazione

   [CQ.wcm.Annotation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Annotation)

   La finestra di dialogo è un tipo speciale di finestra con un modulo nel corpo e un gruppo di pulsanti nel piè di pagina. In genere viene utilizzato per modificare i contenuti, ma può anche visualizzare solo le informazioni.

* arraystore

   [CQ.Ext.data.ArrayStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.ArrayStore)

   Precedentemente noto come &quot;SimpleStore&quot;.

   Classe helper piccola per creare [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)i dati di Array sono più semplici. Un ArrayStore viene configurato automaticamente con un [CQ.Ext.data.ArrayReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.ArrayReader).

* editor di risorse

   [CQ.dam.AssetEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.dam.AssetEditor)

   Editor risorse utilizzato nell’amministrazione DAM.

* assetreferencesearchedialogo

   [CQ.wcm.AssetReferenceSearchDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.AssetReferenceSearchDialog)

   La finestra di dialogo AssetReferenceSearchDialog è una finestra di dialogo che viene visualizzata nel caso in cui una pagina faccia riferimento a risorse o tag.

* blueprintconfig

   [CQ.wcm.msm.BlueprintConfig](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintConfig)

   BlueprintConfig fornisce un pannello per visualizzare le Live Copy di una Blueprint e modificare queste proprietà Blueprint ( trigger di sincronizzazione e azioni di sincronizzazione ).

* blueprintstatus

   [CQ.wcm.msm.BlueprintStatus](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintStatus)

   BlueprintStatus fornisce un pannello per visualizzare e modificare una Blueprint e le sue relazioni Live Copy. La navigazione viene effettuata attraverso un [CQ.wcm.msm.BlueprintStatus.Tree](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintStatus.Tree), edizione tramite [CQ.wcm.msm.BlueprintConfig](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintConfig) e a [CQ.wcm.msm.LiveCopyProperties](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.LiveCopyProperties).

* box

   [CQ.Ext.BoxComponent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.BoxComponent)

   Classe di base per qualsiasi [Componente](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component) che deve essere dimensionato come una scatola, utilizzando larghezza e altezza.

   BoxComponent fornisce le regolazioni automatiche del modello di box per il dimensionamento e il posizionamento e funzionerà correttamente all&#39;interno del modello di rendering del componente.

* browser, finestra di dialogo

   [CQ.BrowseDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.BrowseDialog)

   Il BrowseDialog consente all&#39;utente di navigare nel repository per selezionare un percorso. In genere viene utilizzato tramite un [SfogliaCampo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.BrowseField).

* campo

   [CQ.form.BrowseField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.BrowseField)

   **Obsoleto: Utilizzo [CQ.form.PathField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField) anziché**

* bulkeditor

   [CQ.wcm.BulkEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor)

   BulkEditor fornisce un motore di ricerca e una griglia per modificare i risultati della ricerca.

   È necessario inserire BulkEditor in un modulo HTML (richiesto dalla funzionalità di importazione). Questo funziona perfettamente con un [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog).

* bulkeditorform

   [CQ.wcm.BulkEditorForm](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditorForm)

   BulkEditorForm fornisce [CQ.wcm.BulkEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor) circondato da una forma HTML. Questa è la versione standalone del [CQ.wcm.BulkEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor), il modulo HTML è richiesto per il pulsante di importazione .

* pulsante

   [CQ.Ext.Button](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button)

   Classe Pulsante semplice

* gruppo pulsanti

   [CQ.Ext.ButtonGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ButtonGroup)

   Contenitore per un gruppo di pulsanti.

* grafico

   [CQ.Ext.Chart](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart)

   Il pacchetto CQ.Ext.Chart fornisce la capacità di visualizzare i dati con grafici basati su flash. Ogni grafico si lega direttamente a un CQ.Ext.data.Store abilitando gli aggiornamenti automatici del grafico. Per modificare l’aspetto di un grafico, vedi [ChartStyle](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart) e [extraStyle](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart) opzioni di configurazione.

* spunta

   [CQ.Ext.form.Checkbox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Checkbox)

   Campo casella di controllo singola. Può essere utilizzato come sostituzione diretta dei campi di controllo tradizionali.

* checkbox group

   [CQ.Ext.form.CheckboxGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.CheckboxGroup)

   Un contenitore di raggruppamento per [CQ.Ext.form.Checkbox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Checkbox) controlli.

* clearcombo

   [CQ.form.ClearableComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ClearableComboBox)

   ClearableComboBox è una casella combinata non modificabile con un trigger per cancellare il relativo valore.

* campo colorato

   [CQ.form.ColorField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ColorField)

   ColorField consente all&#39;utente di immettere un valore esadecimale del colore direttamente o utilizzando un [CQ.Ext.ColorMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorMenu).

* elenco a colori

   [CQ.form.ColorList](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ColorList)

   ColorList consente all&#39;utente di scegliere un colore da un elenco modificabile.

* colormenu

   [CQ.Ext.menu.ColorMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.ColorMenu)

   Un menu contenente un [CQ.Ext.ColorPalette](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorPalette) Componente.

* palette a colori

   [CQ.Ext.ColorPalette](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorPalette)

   Classe di palette di colori semplice per la scelta dei colori. È possibile eseguire il rendering della palette in qualsiasi contenitore.

* combo

   [CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)

   Controllo combobox con supporto per autocompletamento, caricamento remoto, paging e molte altre caratteristiche.

   Un controllo ComboBox funziona in modo simile a un HTML tradizionale &lt;select> campo . La differenza consiste nel sottomettere il [valueField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox), devi specificare un [hiddenName](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox) per creare un input nascosto.

* componente

   [CQ.Ext.Component](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component)

   Classe base per tutti i componenti Ext. Tutte le sottoclassi di Component possono partecipare al ciclo di vita del componente Ext automatizzato di creazione, rendering e distruzione fornito dalla [Contenitore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container) classe. I componenti possono essere aggiunti a un contenitore tramite [items](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container) opzione di configurazione al momento della creazione del contenitore.

* estrattore di componenti

   [CQ.wcm.ComponentExtractor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ComponentExtractor)

   ComponentExtractor consente all’utente di estrarre componenti da un sito Web o da una pagina.

* selettore componenti

   [CQ.form.ComponentSelector](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ComponentSelector)

   Selezione raggruppata e ordinata dei componenti disponibili.

* componentStyles

   [CQ.form.ComponentStyles](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ComponentStyles)

* compositore

   [CQ.form.CompositeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.CompositeField)

   Classe base per campi modulo complessi basati su pannelli che includono un campo modulo o un gruppo di campi modulo.

* container

   [CQ.Ext.Container](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container)

   Classe di base per qualsiasi [CQ.Ext.BoxComponent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.BoxComponent) che possono contenere altri componenti. I contenitori gestiscono il comportamento di base degli elementi contenenti, ovvero l’aggiunta, l’inserimento e la rimozione di elementi.

   Le classi Container più comunemente utilizzate sono [CQ.Ext.Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel), [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window) e [CQ.Ext.TabPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.TabPanel).

* contentfinder

   [CQ.wcm.ContentFinder](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder)

   ContentFinder è una colonna specializzata di due colonne [Viewport](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Viewport) che contiene l&#39;effettivo Content Finder a sinistra e la cornice contenuto a destra.

* contentfindertab

   [CQ.wcm.ContentFinderTab](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinderTab)

   ContentFinderTab è un pannello specializzato che fornisce le funzioni utilizzate nei pannelli delle schede [CQ.wcm.ContentFinder](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder). In genere, per visualizzare la ricerca è presente un modulo di ricerca, ovvero la Casella query, e una visualizzazione dati.

* cq.workflow.model.combo

   [CQ.wcm.WorkflowModelCombo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.WorkflowModelCombo)

   WorkflowModelCombo è un [CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox) mostra un elenco dei modelli di flusso di lavoro disponibili.

* cq.workflow.model.selector

   [CQ.wcm.WorkflowModelSelector](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.WorkflowModelSelector)

   WorkflowModelSelector combina un WorkflowModelCombo con un&#39;immagine in miniatura del flusso di lavoro e pulsanti per creare e modificare modelli di flusso di lavoro.

* createsitewcomunitari

   [CQ.wcm.CreateSiteWizard](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.CreateSiteWizard)

   CreateSiteWizard è una procedura guidata dettagliata per la creazione di siti (MSM).

* createversiondialog

   [CQ.wcm.CreateVersionDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.CreateVersionDialog)

   CreateVersionDialog è una finestra di dialogo che consente di creare una nuova versione di una pagina.

* customcontentpanel

   [CQ.CustomContentPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.CustomContentPanel)

   Il CustomContentPanel è un tipo speciale di pannello da utilizzare in [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog): Il relativo contenuto viene recuperato e inviato a un URL diverso rispetto agli altri campi della finestra di dialogo.

* ciclo

   [CQ.Ext.CycleButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.CycleButton)

   Un oggetto SplitButton specializzato contenente un menu di [CQ.Ext.menu.CheckItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.CheckItem) elementi. Il pulsante passa automaticamente in rassegna ogni voce del menu al momento del clic, sollevando il pulsante [cambiare](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.CycleButton) evento (o chiamata del pulsante [changeHandler](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.CycleButton) (se fornito) per la voce di menu attiva.

* visualizzazione dati

   [CQ.Ext.DataView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DataView)

   Meccanismo per la visualizzazione dei dati tramite modelli di layout personalizzati e la formattazione. DataView utilizza un [CQ.Ext.XTemplate](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.XTemplate) come meccanismo di template interno ed è vincolato a un [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store) in modo che, quando i dati nell&#39;archivio cambiano, la visualizzazione venga aggiornata automaticamente per riflettere le modifiche.

* datefield

   [CQ.Ext.form.DateField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField)

   Fornisce un campo di immissione data con un [CQ.Ext.DatePicker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker) a discesa e convalida automatica della data.

* datemenu

   [CQ.Ext.menu.DateMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.DateMenu)

   Un menu contenente un [CQ.Ext.DatePicker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker) Componente.

* datepicker

   [CQ.Ext.DatePicker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker)

   Selezione di una data a comparsa. Questa classe viene utilizzata dalla [DateField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField) per consentire la navigazione e la selezione di date valide.

* datetime

   [CQ.form.DateTime](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.DateTime)

   Il valore DateTime consente all&#39;utente di immettere una data e un&#39;ora combinando [CQ.Ext.form.DateField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField) e [CQ.Ext.form.TimeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TimeField).

* finestra di dialogo

   [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog)

   La finestra di dialogo è un tipo speciale di finestra con un modulo nel corpo e un gruppo di pulsanti nel piè di pagina. In genere viene utilizzato per modificare i contenuti, ma può anche visualizzare solo le informazioni.

* dialogfieldè

   [CQ.form.DialogFieldSet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.DialogFieldSet)

   DialogFieldSet è un [FieldSet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FieldSet) per l&#39;uso in [Finestre di dialogo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog).

* directstore

   [CQ.Ext.data.DirectStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.DirectStore)

   Classe helper piccola per creare un [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store) configurato con un [CQ.Ext.data.DirectProxy](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.DirectProxy) e [CQ.Ext.data.JsonReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonReader) per interagire con un [CQ.Ext.Direct](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Direct) Lato server [Provider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.direct.Provider) più facile.

* displayfield

   [CQ.Ext.form.DisplayField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DisplayField)

   Campo di testo di sola visualizzazione non convalidato e non inviato.

* barra editoriale

   [CQ.wcm.EditBar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditBar)

   La barra di modifica consente all&#39;utente di modificare il contenuto utilizzando i pulsanti di una barra.

   Sebbene non sia presente nell&#39;elenco, EditBar include tutti i membri di [CQ.wcm.EditBase](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditBase).

* editor

   [CQ.Ext.Editor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Editor)

   Campo dell’editor di base che gestisce la visualizzazione/l’eliminazione su richiesta e presenta alcune logiche di ridimensionamento e gestione degli eventi incorporate.

* griglia editorica

   [CQ.Ext.grid.EditorGridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.EditorGridPanel)

   Questa classe estende [Classe GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) per fornire la modifica della cella su selezionato [colonne](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.Column). Le colonne modificabili vengono specificate specificando un [editor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.ColumnModel) in [configurazione a colonne](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.Column).

* editrollover

   [CQ.wcm.EditRollover](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditRollover)

   Il pulsante Modifica consente all’utente di modificare il contenuto con un doppio clic e fornisce ulteriori azioni di modifica tramite un menu di scelta rapida. L’area modificabile viene indicata con un fotogramma quando il mouse passa sopra il contenuto.

* importatore

   [CQ.wcm.FeedImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.FeedImporter)

   FeedImporter consente all&#39;utente di importare feed RSS o Atom e creare pagine per ogni voce di feed.

* o in un altro campo

   [CQ.Ext.form.Field](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Field)

   Classe di base per i campi modulo che forniscono la gestione degli eventi, le dimensioni, la gestione dei valori e altre funzionalità predefinite.

* fielldità

   [CQ.Ext.form.FieldSet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FieldSet)

   Contenitore standard utilizzato per raggruppare gli elementi all’interno di un [modulo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FormPanel). ...

* fileuploaddialogbutton

   [CQ.form.FileUploadDialogButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.FileUploadDialogButton)

   FileUploadDialogButton crea un pulsante che apre una nuova finestra di dialogo per il caricamento di un file tramite FileUploadField. Può essere utilizzato all’interno di finestre di dialogo di modifica in cui il caricamento deve avvenire in un modulo separato.

* fileuploadfield

   [CQ.form.FileUploadField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.FileUploadField)

   FileUploadField consente all&#39;utente di selezionare un singolo file da caricare.

* findresegnaposto, finestra

   [CQ.wcm.FindReplaceDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.FindReplaceDialog)

   La finestra TrovaSostituisciFinestra di dialogo consente di trovare e sostituire i token in una pagina e nelle relative pagine figlie.

* flash

   [CQ.Ext.FlashComponent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.FlashComponent)

* griglia

   [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)

   Questa classe rappresenta l&#39;interfaccia primaria di un controllo griglia basato su componenti per rappresentare i dati in un formato tabulare di righe e colonne.

* groupingstore

   [CQ.Ext.data.GroupingStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.GroupingStore)

   Implementazione dell&#39;archivio specializzata che consente di raggruppare i record in base a uno dei campi disponibili. In genere viene utilizzato insieme a un [CQ.Ext.grid.GroupingView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GroupingView) provare il modello dati per un GridPanel raggruppato.

* dialogo celeste

   [CQ.wcm.HeavyMoveDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.HeavyMoveDialog)

   HeavyMoveDialog è una finestra di dialogo per lo spostamento di una pagina e delle relative pagine figlie, anche considerando la riattivazione di pagine precedentemente attivate (&quot;pesante&quot; spostamento).

* nascosto

   [CQ.Ext.form.Hidden](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Hidden)

   Campo nascosto di base per l’archiviazione dei valori nascosti nei moduli che devono essere passati all’interno dell’invio del modulo.

* storybutton

   [CQ.HistoryButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.HistoryButton)

   HistoryButton è una piccola classe di supporto per fornire facilmente i pulsanti indietro e avanti. Di solito sono necessarie due istanze correlate: L&#39;istanza del pulsante avanti è un semplice pulsante collegato all&#39;istanza del pulsante indietro che gestisce la cronologia.

* htmleditor

   [CQ.Ext.form.HtmlEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.HtmlEditor)

   Fornisce un componente leggero di HTML Editor. Alcune funzioni della barra degli strumenti non sono supportate da Safari e verranno nascoste automaticamente quando necessario. Se necessario, queste sono indicate nelle opzioni di configurazione.

   I pulsanti della barra degli strumenti dell’editor dispongono di descrizioni comandi definite in [buttonTips](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.HtmlEditor) proprietà.

* dialogo quadro

   [CQ.IframeDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.IframeDialog)

   Una finestra di dialogo semplice che mostra il contenuto di un iframe e consente la creazione di moduli in iframe.

* iframepanel

   [CQ.IframePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.IframePanel)

   Un pannello contenente un iframe. Consente di creare facilmente gli iframe, un evento di caricamento iframe e un facile accesso ai contenuti dell&#39;iframe.

* inlinetextfield

   [CQ.form.InlineTextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.InlineTextField)

   InlineField è un campo di testo visualizzato come etichetta quando non è attivo.

* jsonstore

   [CQ.Ext.data.JsonStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonStore)

   Classe helper piccola per creare [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)è più facile da usare per i dati JSON. Un JsonStore viene configurato automaticamente con un [CQ.Ext.data.JsonReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonReader).

* etichetta

   [CQ.Ext.form.Label](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Label)

   Campo Etichetta di base.

* languagecopydialog

   [CQ.wcm.LanguageCopyDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.LanguageCopyDialog)

   LanguageCopyDialog è una finestra di dialogo per la copia di strutture della lingua.

* linkchecker

   [CQ.wcm.LinkChecker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.LinkChecker)

   LinkChecker è uno strumento per controllare i collegamenti esterni in un sito.

* elenco

   [CQ.Ext.list.ListView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.ListView)

   CQ.Ext.list.ListView è un&#39;implementazione rapida e leggera di un [Griglia](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) come la vista.

* livecopyproperties

   [CQ.wcm.msm.LiveCopyProperties](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.LiveCopyProperties)

   LiveCopyProperties fornisce un pannello per visualizzare e modificare le proprietà Live Copy ( ereditarietà delle relazioni, attivatore di sincronizzazione e azioni di sincronizzazione ).

* lvbooleano

   [CQ.Ext.list.BooleanColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.BooleanColumn)

   Classe di definizione della colonna che esegue il rendering dei campi dati booleani. Consulta la sezione [xtype](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) opzione di configurazione [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) per ulteriori dettagli.

* lvcolumn

   [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column)

   Questa classe incapsula i dati di configurazione della colonna da utilizzare nell&#39;inizializzazione di un [ListView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.ListView).

* lvdatecolumn

   [CQ.Ext.list.DateColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.DateColumn)

   Una classe di definizione di colonna che esegue il rendering di una data passata in base alle impostazioni internazionali predefinite o di una [format](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.DateColumn). Consulta la sezione [xtype](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) opzione di configurazione [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) per ulteriori dettagli.

* lvnumbercolumn

   [CQ.Ext.list.NumberColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.NumberColumn)

   Classe di definizione di una colonna che esegue il rendering di un campo dati numerico in base a una [format](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.NumberColumn) stringa. Consulta la sezione [xtype](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) opzione di configurazione [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) per ulteriori dettagli.

* mediabrowsedialog

   [CQ.MediaBrowseDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.MediaBrowseDialog)

   **Obsoleto: Utilizzo [Content Finder](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder) per sfogliare invece i file multimediali.**

   MediaBrowseDialog è una finestra di dialogo per la navigazione nella libreria multimediale.

* menu

   [CQ.Ext.menu.Menu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Menu)

   Un oggetto menu. Questo è il contenitore a cui è possibile aggiungere voci di menu. Il menu può anche fungere da classe base quando si desidera un menu specializzato basato su un altro componente (come [CQ.Ext.menu.DateMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.DateMenu) ad esempio).

   I menu possono contenere [voci di menu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Item)o generale [Componente](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component)s.

* menubaseitem

   [CQ.Ext.menu.BaseItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.BaseItem)

   Classe base per tutti gli elementi di cui viene eseguito il rendering nei menu. BaseItem fornisce il rendering predefinito, la gestione dello stato attivato e le opzioni di configurazione di base condivise da tutti i componenti del menu.

* menucheckitem

   [CQ.Ext.menu.CheckItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.CheckItem)

   Aggiunge una voce di menu che contiene una casella di controllo per impostazione predefinita, ma che può anche far parte di un gruppo di pulsanti di scelta.

* menuitem

   [CQ.Ext.menu.Item](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Item)

   Una classe base per tutte le voci di menu che richiedono funzionalità correlate al menu (come i sottomenu) e non sono voci di visualizzazione statiche. L&#39;elemento estende la funzionalità di base di [CQ.Ext.menu.BaseItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.BaseItem) aggiungendo l’attivazione specifica del menu e facendo clic su gestione.

* menuseparatore

   [CQ.Ext.menu.Separator](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Separator)

   Aggiunge una barra di separazione a un menu, utilizzata per dividere gruppi logici di voci di menu. Generalmente aggiungi uno di questi utilizzando &quot;-&quot; nella chiamata a add() o nella configurazione degli elementi anziché crearne uno direttamente.

* menutextitem

   [CQ.Ext.menu.TextItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.TextItem)

   Aggiunge una stringa di testo statica a un menu, in genere utilizzato come separatore di intestazione o di gruppo.

* metadati

   [CQ.dam.form.Metadata](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.dam.form.Metadata)

   I metadati forniscono un set di campi per determinare le informazioni necessarie per un campo di metadati, come utilizzato ad esempio nelle pagine dell’editor risorse.

   Fornisce i campi seguenti:

* multicampo

   [CQ.form.MultiField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.MultiField)

   MultiField è un elenco modificabile di campi modulo per la modifica di proprietà multivalore.

* mvt

   [CQ.form.MVT](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.MVT)

   Il componente Test multivariato può essere utilizzato per definire e modificare un set di immagini presentate come banner alternativi. Le statistiche di click-through vengono raccolte per banner.

* notificationinbox

   [CQ.wcm.NotificationInbox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.NotificationInbox)

   La casella in entrata delle notifiche consente all’utente di sottoscrivere azioni WCM e gestire le notifiche.

* numberfield

   [CQ.Ext.form.NumberField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.NumberField)

   Campo di testo numerico che fornisce un filtro automatico per i tasti e una convalida numerica.

* offline importer

   [CQ.wcm.OfflineImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.OfflineImporter)

   OfflineImporter è uno strumento per importare e convertire documenti Microsoft Word in pagine AEM. Questa funzione consente di modificare il contenuto offline utilizzando un elaboratore di testi.

* possedere

   [CQ.form.OwnerDraw](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.OwnerDraw)

   Il OwnerDraw può contenere codice HTML personalizzato (immesso direttamente o recuperato da un URL).

* paging

   [CQ.Ext.PagingToolbar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.PagingToolbar)

   Man mano che aumenta la quantità di record, aumenta il tempo necessario al browser per eseguirne il rendering. Il paging consente di ridurre la quantità di dati scambiati con il cliente.

* pannello

   [CQ.Ext.Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel)

   Il pannello è un contenitore con funzionalità specifiche e componenti strutturali che lo rendono il componente di base ideale per le interfacce utente orientate alle applicazioni.

   I pannelli sono, in virtù della loro eredità da [CQ.Ext.Container](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container).

* paragrafo

   [CQ.form.ParagraphReference](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ParagraphReference)

   Il campo Riferimento paragrafo consente di sfogliare le pagine e selezionare uno dei paragrafi corrispondenti. È costituito da un campo di attivazione e da una finestra di dialogo di ricerca dei paragrafi associata.

* password

   [CQ.form.Password](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Password)

   La password è simile a una [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField) ma mantiene il suo valore privato, consentendo agli utenti di immettere dati sensibili.

* percorso

   [CQ.form.PathCompletion](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathCompletion)

   **Obsoleto: Utilizzo [CQ.form.PathField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField) anziché**

* pathfield

   [CQ.form.PathField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField)

   PathField è un campo di input progettato per i percorsi con completamento percorso e un pulsante per aprire un [CQ.BrowseDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.BrowseDialog) per esplorare l&#39;archivio server. Può anche sfogliare i paragrafi della pagina per la generazione avanzata di collegamenti.

* avanzamento

   [CQ.Ext.ProgressBar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ProgressBar)

   Componente di una barra di avanzamento aggiornabile. La barra di avanzamento supporta due modalità diverse: manuale e automatico.

   In modalità manuale, l’utente è responsabile della visualizzazione, dell’aggiornamento (tramite [updateProgress](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ProgressBar)) e cancella la barra di avanzamento in base alle esigenze dal codice. Questo metodo è più appropriato quando si desidera visualizzare l&#39;avanzamento.

* propertyGrid

   [CQ.Ext.grid.PropertyGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.PropertyGrid)

   Implementazione specializzata della griglia destinata a imitare la griglia delle proprietà tradizionale, come generalmente visto negli IDE di sviluppo. Ogni riga della griglia rappresenta una proprietà di un oggetto e i dati vengono memorizzati come un set di coppie nome/valore in [CQ.Ext.grid.PropertyRecord](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.PropertyRecord)s.

* propgrid

   [CQ.PropertyGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.PropertyGrid)

   PropertyGrid è una griglia generica utilizzata per visualizzare e modificare le proprietà degli oggetti.

* suggerimento rapido

   [CQ.Ext.QuickTip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTip)

   @xtype quicktip Classe di descrizioni comandi specializzate per le descrizioni comandi specificate nel markup e gestite automaticamente dal global [CQ.Ext.QuickTips](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTips) istanza. Per ulteriori dettagli ed esempi di utilizzo, consulta l’intestazione della classe QuickTips .

* radio

   [CQ.Ext.form.Radio](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Radio)

   Campo radio singolo. Come casella di controllo, ma fornita come comodità per impostare automaticamente il tipo di input. Il raggruppamento pulsanti di scelta viene gestito automaticamente dal browser se a ogni radio di un gruppo viene assegnato lo stesso nome.

* radiogroup

   [CQ.Ext.form.RadioGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.RadioGroup)

   Un contenitore di raggruppamento per [CQ.Ext.form.Radio](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Radio) controlli.

* riferimenti, finestra di dialogo

   [CQ.wcm.ReferencesDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ReferencesDialog)

   La finestra di dialogo Riferimenti è una finestra di dialogo per la visualizzazione di riferimenti su una pagina.

* restoretreedialog

   [CQ.wcm.RestoreTreeDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.RestoreTreeDialog)

   Il RestoreTreeDialog è una finestra di dialogo per il ripristino di una versione precedente di un albero.

* restoreversiondialog

   [CQ.wcm.RestoreVersionDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.RestoreVersionDialog)

   RestoreVersionDialog è una finestra di dialogo per il ripristino di una versione precedente di una pagina.

* richtext

   [CQ.form.RichText](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.RichText)

   RichText fornisce un campo modulo per la modifica di informazioni di testo formattate (RTF).

   Il componente RichText fornisce attualmente le seguenti funzionalità:

* piano di rotazione

   [CQ.wcm.msm.RolloutPlan](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutPlan)

   RolloutPlan fornisce una finestra di dialogo per visualizzare l’avanzamento del rollout della pagina. RolloutPlan viene avviato da un [CQ.wcm.msm.RolloutWizard](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutWizard).

* lucertola

   [CQ.wcm.msm.RolloutWizard](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutWizard)

   RolloutWizard fornisce una procedura guidata per il rollout di una pagina. RolloutWizard avvia un [CQ.wcm.msm.RolloutPlan](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutPlan).

* campo di ricerca

   [CQ.form.SearchField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SearchField)

   Il campo SearchField fornisce un campo di ricerca che fornisce i risultati in un elenco a discesa che può essere utilizzato per la ricerca nel repository.

* selezione

   [CQ.form.Selection](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Selection)

   La selezione consente all’utente di scegliere tra diverse opzioni. Le opzioni possono far parte della configurazione o essere caricate da una risposta JSON. È possibile eseguire il rendering della selezione come menu a discesa (selezione) o come casella di riepilogo a discesa (selezione con voce di testo libera).

* barra laterale

   [CQ.wcm.Sidekick](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Sidekick)

   La barra laterale è un supporto mobile che fornisce all’utente gli strumenti più comuni per la modifica delle pagine.

* siteadmin

   [CQ.wcm.SiteAdmin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.SiteAdmin)

   SiteAdmin è una console che fornisce funzioni di amministrazione WCM.

* siteimporter

   [CQ.wcm.SiteImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.SiteImporter)

   SiteImporter consente all’utente di importare siti web completi e creare progetti iniziali.

* sizefield

   [CQ.form.SizeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SizeField)

   SizeField consente all&#39;utente di immettere la larghezza e l&#39;altezza (ad esempio per un&#39;immagine).

* cursore

   [CQ.Ext.Slider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Slider)

   Slider che supporta l&#39;orientamento verticale o orizzontale, le regolazioni della tastiera, l&#39;aggancio configurabile, il clic sull&#39;asse e l&#39;animazione. Può essere aggiunto come elemento a qualsiasi contenitore. Esempio di utilizzo: ...

* presentazione

   [CQ.form.Slideshow](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Slideshow)

   La presentazione fornisce un componente che può essere utilizzato per definire e modificare un set di immagini e titoli di immagini che possono essere visualizzati come slideshow.

   Il componente Presentazione si basa sul [CQ.form.SmartImage](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartImage) componente.

* smartfile

   [CQ.form.SmartFile](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartFile)

   SmartFile è un caricatore di file intelligente.

   Se è installato un plug-in di Flash (versione >= 9), i caricamenti vengono eseguiti utilizzando la libreria SWFupload che offre un modo semplice per gestire i caricamenti.

* smartimage

   [CQ.form.SmartImage](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartImage)

   SmartImage è un caricatore di immagini intelligente. Fornisce gli strumenti per elaborare un&#39;immagine caricata, ad esempio uno strumento per definire mappe immagine e un ritaglio immagine.

   Il componente è progettato principalmente per l’uso in una scheda di dialogo separata.

* distanziatore

   [CQ.Ext.Spacer](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Spacer)

   Utilizzato per fornire uno spazio considerevole in un layout.

* spintore

   [CQ.form.Spinner](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Spinner)

   L’icona che ruota è un campo di attivazione per valori numerici, di data o di ora. Il valore può essere aumentato e diminuito utilizzando i trigger forniti, la rotellina di scorrimento o i tasti.

* pulsante

   [CQ.Ext.SplitButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.SplitButton)

   Pulsante di menu combinato che fornisce una freccia a discesa incorporata in grado di attivare un evento separatamente dall’evento di clic predefinito del pulsante. In genere viene utilizzato per visualizzare un menu a discesa che fornisce opzioni aggiuntive per l’azione del pulsante principale, ma qualsiasi gestore personalizzato può fornire l’implementazione del clic di freccia.

* statici

   [CQ.Static](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Static)

   Static può essere utilizzato per visualizzare testo arbitrario o HTML.

* statistiche

   [CQ.wcm.Statistics](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Statistics)

   Statistiche visualizza le impression della pagina sotto forma di grafico. Il widget consente di selezionare un periodo, le statistiche devono essere visualizzate per.

* archiviare

   [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)

   La classe Store incapsula una cache lato client di [Record](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Record) oggetti che forniscono dati di input per componenti quali [GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel), [ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)o [DataView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DataView).

* suggestivo

   [CQ.form.SuggestField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SuggestField)

   SuggestField fornisce all’utente suggerimenti basati sulla voce corrispondente.

* commutatore

   [CQ.Switcher](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Switcher)

   Il commutatore fornisce un gruppo di pulsanti per la barra dell’intestazione in una console per passare da Siti Web, Risorse digitali, Strumenti, Flusso di lavoro e Sicurezza.

* tableedit

   [CQ.form.TableEdit](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit)

   **Obsoleto: Utilizzo [CQ.form.TableEdit2](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit2) invece.**

* tableedit2

   [CQ.form.TableEdit2](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit2)

   TableEdit2 fornisce un widget per la creazione di tabelle.

* tavola

   [CQ.Ext.TabPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.TabPanel)

   Contenitore di schede di base. TabPanels può essere utilizzato esattamente come uno standard [CQ.Ext.Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel) a scopo di layout, ma dispongono anche di un supporto speciale per l’inclusione di componenti figlio ([`items`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container)).

* tag

   [CQ.tagging.TagInputField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.tagging.TagInputField)

   ```
   CQ.tagging.TagInputField
   ```

   è un widget modulo per l’immissione di tag. Dispone di un menu a comparsa per la selezione tra i tag esistenti, include il completamento automatico e molte altre funzioni.

* area di testo

   [CQ.Ext.form.TextArea](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextArea)

   Campo di testo a più righe. Può essere utilizzato come sostituzione diretta per i campi di testo tradizionali, oltre a supportare il ridimensionamento automatico.

* pulsante

   [CQ.TextButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.TextButton)

   TextButton fornisce un collegamento di testo con le funzionalità di un [CQ.Ext.Button](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button).

* campo di testo

   [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField)

   Campo di testo di base. Può essere utilizzato come sostituzione diretta per gli input di testo tradizionali o come classe base per controlli di input più sofisticati (come [CQ.Ext.form.TextArea](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextArea) e [CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)).

* miniatura

   [CQ.form.Thumbnail](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Thumbnail)

* campo temporale

   [CQ.Ext.form.TimeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TimeField)

   Fornisce un campo di immissione ora con un elenco a discesa e una convalida automatica dell’ora. Esempio di utilizzo: ...

* suggerimento

   [CQ.Ext.Tip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Tip)

   @xtype tip Questa è la classe base per [CQ.Ext.QuickTip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTip) e [CQ.Ext.Tooltip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Tooltip) che fornisce il layout e il posizionamento di base richiesti da tutte le classi basate su suggerimenti. Questa classe può essere utilizzata direttamente per suggerimenti semplici e a posizionamento statico.

* titleseparator

   [CQ.menu.TitleSeparator](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.menu.TitleSeparator)

   Aggiunge una barra di separazione a un menu, utilizzata per dividere gruppi logici di voci di menu. Il separatore può inoltre avere un titolo.

* toolbar

   [CQ.Ext.Toolbar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Toolbar)

   Classe Barra degli strumenti di base. Anche se la [`defaultType`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container) per la barra degli strumenti [`button`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button), gli elementi della barra degli strumenti (elementi secondari per il contenitore Barra degli strumenti) possono essere praticamente qualsiasi tipo di componente. Gli elementi della barra degli strumenti possono essere creati esplicitamente tramite i relativi costruttori.

* tooltip

   [CQ.Ext.ToolTip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ToolTip)

   Implementazione standard di descrizioni per fornire informazioni aggiuntive quando si passa il mouse su un elemento di destinazione. @xtype tooltip.

* burbero

   [CQ.tree.TreeGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.tree.TreeGrid)

   @xtype Treegrid

* treepanel

   [CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)

   TreePanel fornisce una rappresentazione dell&#39;interfaccia utente strutturata ad albero dei dati strutturati ad albero.

   [TreeNode](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreeNode)viene aggiunto al pannello ad albero, ciascuno dei quali può contenere i metadati utilizzati dall&#39;applicazione nella relativa [attributes](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreeNode) proprietà.

* attivare

   [CQ.Ext.form.TriggerField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField)

   Fornisce un wrapper pratico per TextFields che aggiunge un pulsante di attivazione cliccabile (assomiglia a una casella combinata per impostazione predefinita). Il trigger non ha un&#39;azione predefinita, pertanto devi assegnare una funzione per implementare il gestore di clic del trigger ignorando [onTriggerClick](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField). Puoi creare direttamente un oggetto TriggerField, in quanto esegue il rendering esattamente come una casella combinata.

* uploaddialog

   [CQ.UploadDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.UploadDialog)

   UploadDialog consente all&#39;utente di caricare i file nell&#39;archivio Crea una nuova finestra di dialogo UploadDialog.

* userinfo

   [CQ.UserInfo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.UserInfo)

   Elemento della barra degli strumenti per visualizzare il nome utente corrente e consentire azioni dell’utente come la modifica delle proprietà utente e la rappresentazione.

* viewport

   [CQ.Ext.Viewport](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Viewport)

   Un contenitore specializzato che rappresenta l&#39;area dell&#39;applicazione visualizzabile (la finestra del browser).

   Il riquadro di visualizzazione si riproduce al corpo del documento e si ridimensiona automaticamente alle dimensioni del riquadro di visualizzazione del browser e gestisce il ridimensionamento delle finestre. È possibile creare un solo riquadro di visualizzazione.

* finestra

   [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)

   Pannello specializzato destinato a essere utilizzato come finestra di un&#39;applicazione. Le finestre sono mobili, [ridimensionabile](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)e [trascinabile](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window) per impostazione predefinita. Windows può essere [massimizzato](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window) per riempire il riquadro di visualizzazione, ripristinato alle dimensioni precedenti, e può essere [minimizzare](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)d.

* xmlstore

   [CQ.Ext.data.XmlStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.XmlStore)

   Classe helper piccola per creare [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)è più semplice dai dati XML. Un XmlStore viene configurato automaticamente con un [CQ.Ext.data.XmlReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.XmlReader).

   **cqinclude** xtype di pseudo che include le definizioni di widget da un percorso diverso nell’archivio. Viene utilizzato più comunemente nelle finestre di dialogo delle pagine. Non esiste una classe di widget JavaScript effettiva per questo xtype. Viene elaborato dalla funzione formatData() della classe CQ.Util. Per ulteriori informazioni, consulta questo articolo della knowledge base.
