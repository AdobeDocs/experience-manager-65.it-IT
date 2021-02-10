---
title: Come creare un modulo adattivo
description: 'Scoprite come creare un modulo adattivo utilizzando  [!DNL Experience Manager Forms]. I moduli adattivi sono moduli HTML5 reattivi che semplificano la raccolta e l’elaborazione delle informazioni. Approfondire la procedura di creazione di un modulo adattivo basato su un modello di dati del modulo, un modello di modulo XFA e uno schema XML o JSON. '
feature: Adaptive Forms
role: Business Practitioner, Developers
level: Beginner
translation-type: tm+mt
source-git-commit: 52fedc234b3edf581393bb42325902d2da3ab46e
workflow-type: tm+mt
source-wordcount: '1856'
ht-degree: 0%

---


# Creazione di un modulo adattivo {#creating-an-adaptive-form}

## <strong>Creare un modulo adattivo</strong> {#strong-create-an-adaptive-form-strong}

Per creare un modulo adattivo, procedere come segue.

1. Accedere all&#39;istanza di [!DNL Experience Manager Forms] Author in `https://'[server]:[port]'/<custom-context-if-any>.`

1. Immettete le credenziali nella pagina di login del Experience Manager .

   Dopo aver effettuato l&#39;accesso, nell&#39;angolo in alto a sinistra toccate **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp; Documents]**.

   >[!NOTE]
   >
   >Per un&#39;installazione predefinita, il login è `admin` e la password è `admin`.

1. Toccate **[!UICONTROL Crea]** e selezionate **[!UICONTROL Modulo adattivo]**.
1. Viene visualizzata un’opzione per selezionare un modello. Per ulteriori informazioni sui modelli, vedere [Modelli di moduli adattivi](creating-adaptive-form.md#p-adaptive-form-templates-p). Toccate un modello per selezionarlo e toccate Avanti.
1. Viene visualizzata l&#39;opzione &quot;Aggiungi proprietà&quot;. Specificare i valori per i seguenti campi di proprietà. I campi Titolo e Nome sono obbligatori:

   * **[!UICONTROL Titolo:]** specifica il nome visualizzato del modulo. Il titolo consente di identificare il modulo nell&#39;interfaccia utente [!DNL Experience Manager Forms].
   * **[!UICONTROL Nome:]** specifica il nome del modulo. Nella directory archivio viene creato un nodo con il nome specificato. Quando si inizia a digitare un titolo, viene automaticamente generato il valore relativo al campo del nome. È possibile modificare il valore suggerito. Il campo del nome può includere solo caratteri alfanumerici, trattini e caratteri di sottolineatura. Tutti gli input non validi vengono sostituiti con un trattino.
   * **[!UICONTROL Descrizione:]** specifica le informazioni dettagliate sul modulo.
   * **[!UICONTROL Tag:]** specifica i tag per identificare in modo univoco il modulo adattivo. I tag consentono di effettuare ricerche nel modulo. Per creare i tag, digitate nuovi nomi di tag nella casella **[!UICONTROL Tag]**.

1. È possibile creare un modulo adattivo basato su uno dei seguenti modelli di modulo:

   * [Modello dati modulo](#fdm)
   * [Modello di modulo XFA](#create-an-adaptive-form-based-on-an-xfa-form-template)
   * [Schema XML o JSON](#create-an-adaptive-form-based-on-xml-or-json-schema)
   * Nessuno o senza un modello di modulo

   È possibile configurarli dalla scheda **[!UICONTROL Modello modulo]** nella pagina **[!UICONTROL Aggiungi proprietà]**. Per impostazione predefinita, il modello di modulo selezionato è **[!UICONTROL None]**.

1. Toccate **[!UICONTROL Crea]**. Viene creato un modulo adattivo e viene visualizzata una finestra di dialogo per aprire il modulo per la modifica.

   Dopo aver specificato tutte le proprietà, fare clic su **[!UICONTROL Crea]**. Viene creato un modulo adattivo e viene visualizzata una finestra di dialogo per aprire il modulo per la modifica.

   Dopo aver specificato tutte le proprietà, fare clic su **[!UICONTROL Crea]**. Viene creato un modulo adattivo e viene visualizzata una finestra di dialogo per aprire il modulo per la modifica.

1. Toccate **[!UICONTROL Apri]** per aprire il modulo appena creato in una nuova scheda. Il modulo si apre per la modifica e visualizza il contenuto disponibile nel modello. Inoltre, consente di visualizzare la barra laterale per personalizzare il modulo appena creato in base alle esigenze.

   In base al tipo di modulo adattivo, gli elementi del modulo presenti nel modello di modulo XFA, nello schema XML o nello schema JSON associato vengono visualizzati nella scheda **[!UICONTROL Oggetti modello dati]** della barra laterale **[!UICONTROL Browser contenuti]**. Potete anche trascinare questi elementi per creare il modulo adattivo.

   Per informazioni sull&#39;interfaccia per la creazione di moduli adattivi e sui componenti disponibili, vedere [Introduzione alla creazione di moduli adattivi](introduction-forms-authoring.md).

   >[!NOTE]
   >
   >Consente alle finestre a comparsa del browser di aprire il modulo appena creato in una nuova scheda.

## Creare un modulo adattivo basato su un modello dati modulo {#fdm}

[[!DNL Experience Manager Forms] l&#39;](data-integration.md) integrazione dei dati consente di integrare più origini dati e di unire le relative entità e servizi per creare un modello dati del modulo. È un&#39;estensione dello schema JSON. È possibile utilizzare un modello dati modulo per creare un modulo adattivo. Le entità o gli oggetti del modello dati configurati in un modello dati del modulo sono disponibili come oggetti del modello dati per l&#39;authoring del modulo. Sono associati alle rispettive origini dati e utilizzati per precompilare un modulo e riscrittare i dati inviati alle rispettive origini dati. È inoltre possibile chiamare i servizi configurati in un modello dati del modulo utilizzando le regole del modulo adattivo.

Per utilizzare un modello dati modulo per la creazione di un modulo adattivo:

1. Nella scheda Modello modulo della schermata Aggiungi proprietà, selezionare **[!UICONTROL Modello dati modulo]** nell&#39;elenco a discesa **[!UICONTROL Seleziona da]**.

   ![create-af-1-1](assets/create-af-1-1.png)

1. Toccate per espandere **[!UICONTROL Seleziona modello dati modulo]**. Vengono elencati tutti i modelli di dati del modulo disponibili.

   Selezionare un modello dati da.

   ![create-af-2-1](assets/create-af-2-1.png)

>[!NOTE]
>
>È inoltre possibile modificare il modello dati del modulo per un modulo adattivo. Per i passaggi dettagliati, vedere [Modifica delle proprietà del modello di modulo di un modulo adattivo](#edit-form-model).

## Creare un modulo adattivo basato su un modello di modulo XFA {#create-an-adaptive-form-based-on-an-xfa-form-template}

È possibile riadattare i modelli di modulo XFA per creare moduli adattivi. Per riadattare, caricare e associare un modello di modulo XFA a un modulo adattivo. Gli elementi del modello di modulo (modulo XFA) sono disponibili per l&#39;uso in Content Finder al momento della creazione di moduli adattivi. Da Content Finder, è possibile trascinare gli elementi del modello di modulo sul modulo.

<!-- >>[!NOTE]
>
>[Upload the XFA Form Template](get-xdp-pdf-documents-aem.md) to AEM Forms before you start creating an adaptive form based on the form template.

Do the following to use an XFA form template as form model for your adaptive form:

1. On the **[!UICONTROL Add Properties]** page, open the **[!UICONTROL Form Model]** tab.
1. In the Form Model tab, from the drop-down list, select **[!UICONTROL Form Templates]**. All the form templates that are uploaded to the repository via AEM Forms UI are listed for selection. Select a template from the list.

   ![Associate XFA Form Template with an Adaptive Form](assets/form_model_xfa_associate.png)
**Figure:** *Selecting a form template*

   >[!NOTE]
   >
   >You can also change the form template for an adaptive form. For detailed steps, see [Edit Form Model properties of an adaptive form](#edit-form-model). -->

## Creare un modulo adattivo basato su uno schema XML o JSON {#create-an-adaptive-form-based-on-xml-or-json-schema}

Gli schemi XML e JSON rappresentano la struttura in cui i dati vengono prodotti o consumati dal sistema back-end della tua organizzazione. È possibile associare uno schema a un modulo adattivo e utilizzarne gli elementi per aggiungere contenuto dinamico al modulo adattivo. Gli elementi dello schema sono disponibili nella scheda Oggetto modello dati del browser del contenuto per la creazione di moduli adattivi. È possibile trascinare gli elementi dello schema per creare il modulo.

Per informazioni su come progettare lo schema XML o JSON per la creazione di moduli adattivi, vedere i documenti seguenti.

* [Creazione di moduli adattivi mediante lo schema XML](adaptive-form-xml-schema-form-model.md)
* [Creazione di moduli adattivi con lo schema JSON](adaptive-form-json-schema-form-model.md)

Per utilizzare lo schema XML o JSON come modello di modulo per un modulo adattivo, effettuate le seguenti operazioni:

1. Nel passaggio **[!UICONTROL Aggiungi proprietà]** della pagina di creazione del modulo adattivo, toccare la scheda **[!UICONTROL Modello modulo]**.
1. Nella scheda Modello modulo, selezionare **[!UICONTROL Schema]** dal campo a discesa **[!UICONTROL Seleziona da]**.

1. Toccate **[!UICONTROL Seleziona schema]** ed effettuate una delle seguenti operazioni:

   * **[!UICONTROL Carica da disco]** : selezionate questa opzione e toccate Carica definizione schema per sfogliare e caricare uno schema XML o JSON dal file system. Il file dello schema caricato risiede nel modulo e non è accessibile ad altri moduli adattivi.
   * **[!UICONTROL Ricerca nella directory archivio]** : selezionare questa opzione per selezionare dall&#39;elenco dei file di definizione dello schema disponibili nella directory archivio. Selezionare il file di schema XML o JSON come modello di modulo. Lo schema selezionato è associato al modulo tramite riferimento ed è accessibile per l&#39;uso in altri moduli adattivi.

   >[!CAUTION]
   >
   >Assicurarsi che il nome del file dello schema JSON termini con **.schema.json**. Ad esempio: mySchema.schema.json

   ![Selezione dello schema XML o JSON](assets/upload-schema.png)
   **Figura:** *Selezione dello schema XML o JSON*

1. (Solo per lo schema XML) Dopo aver selezionato o caricato uno schema XML, specificare un elemento principale del file XSD selezionato da mappare con il modulo adattivo.

   ![Selezione dell&#39;elemento principale XSD](assets/xsd-root-element.png)
   **Figura:** *Selezione dell&#39;elemento principale XSD*

>[!NOTE]
>
>È inoltre possibile modificare lo schema di un modulo adattivo. Per i passaggi dettagliati, vedere [Modifica delle proprietà del modello di modulo di un modulo adattivo](#edit-form-model).

## Modelli di modulo adattivo {#adaptive-form-templates}

Un modello fornisce una struttura di base e definisce l&#39;aspetto (layout e stili) di un modulo adattivo. Contiene componenti preformattati che contengono determinate proprietà e struttura del contenuto. <!-- Out of the box, AEM Forms provides some adaptive form templates. To get the complete template package including advanced templates, you need to install the AEM Forms add-on package. For more information, see [Installing AEM Forms add-on package](installing-configuring-aem-forms-osgi.md).-->

Inoltre, potete usare l’editor modelli per creare modelli personalizzati. Per ulteriori informazioni sull&#39;utilizzo dei modelli, vedere [Modelli di moduli adattivi](template-editor.md).

>[!NOTE]
>
>Quando si apre un modulo adattivo creato utilizzando il modello avanzato per la modifica, viene visualizzato un messaggio di errore. Il modello avanzato include un componente Fase firma e per impostazione predefinita  Adobe Sign è abilitato. Crea e seleziona una [ configurazione cloud Adobe Sign](adobe-sign-integration-adaptive-forms.md) e [configura un firmatario](working-with-adobe-sign.md#addsignerstoanadaptiveform) per risolvere l&#39;errore.

## Modificare le proprietà del modello di modulo di un modulo adattivo {#edit-form-model}

I moduli adattivi vengono creati senza un modello di modulo (utilizzando l&#39;opzione Nessuno per il modello di modulo) o utilizzando un modello di modulo, ad esempio un modello di modulo, uno schema XML, uno schema JSON o un modello di dati del modulo. È possibile modificare il modello di modulo per un modulo adattivo da Nessuno a un altro. Per i moduli adattivi basati su un modello di modulo, è possibile scegliere un altro modello di modulo, schema XML, schema JSON o modello di dati modulo per lo stesso modello di modulo. Tuttavia, non è possibile passare da un modello a un altro.

1. Selezionate il modulo adattivo e toccate l&#39;icona **Proprietà**.
1. Aprire la scheda **[!UICONTROL Modello modulo]** ed effettuare una delle seguenti operazioni.

   * Se il modulo adattivo non dispone di un modello di modulo, è possibile scegliere un altro modello di modulo e quindi selezionare un modello di modulo, uno schema XML o JSON o un modello di dati del modulo.
   * Se il modulo adattivo è basato su un modello di modulo, è possibile scegliere un altro modello di modulo, uno schema XML o JSON oppure un modello di dati modulo per lo stesso modello di modulo.

1. Toccate **[!UICONTROL Salva]** per salvare le proprietà.

## Salvataggio automatico di un modulo adattivo {#auto-save-an-adaptive-form}

Per impostazione predefinita, il contenuto di un modulo adattivo viene salvato in seguito a un&#39;azione dell&#39;utente, ad esempio premendo il pulsante Salva. È inoltre possibile configurare un modulo adattivo per avviare automaticamente il salvataggio del contenuto in base a un evento o a un intervallo di tempo. L’opzione di salvataggio automatico è utile in:

* Salvataggio automatico dei contenuti per utenti anonimi e connessi
* Salvataggio del contenuto di un modulo senza intervento da parte dell&#39;utente
* Avvio del salvataggio del contenuto di un modulo in base a un evento utente
* Salvataggio ripetuto del contenuto di un modulo dopo un intervallo di tempo specificato

### Abilita salvataggio automatico per un modulo adattivo {#enable-auto-save-for-an-adaptive-form}

Per impostazione predefinita, l&#39;opzione di salvataggio automatico non è abilitata. È possibile attivare l&#39;opzione di salvataggio automatico dalla scheda Salvataggio automatico di un modulo adattivo. La scheda Salvataggio automatico offre anche diverse altre opzioni di configurazione. Per attivare e configurare l’opzione di salvataggio automatico per un modulo adattivo, effettuate le seguenti operazioni:

1. Per accedere alla sezione di salvataggio automatico nelle proprietà, selezionare un componente, quindi toccare ![livello campo](assets/field-level.png) > **[!UICONTROL Contenitore modulo adattivo]**, quindi toccare ![cmppr](assets/cmppr.png).
1. Nella sezione **[!UICONTROL Salvataggio automatico]**, **[!UICONTROL Abilitare]** l&#39;opzione di salvataggio automatico.
1. Nella casella **[!UICONTROL Evento modulo adattivo]**, specificare 1 o TRUE per avviare automaticamente il salvataggio del modulo quando il modulo viene caricato nel browser. È inoltre possibile specificare un&#39;espressione condizionale per un evento che, quando viene attivato e restituisce true, inizia a salvare il contenuto del modulo.
1. Specifica l&#39;attivatore. Il salvataggio automatico viene attivato in base alla configurazione in uso. Le opzioni disponibili sono:

   * **[!UICONTROL Base temporale:]** selezionare l&#39;opzione per iniziare a salvare il contenuto in base a un intervallo di tempo specifico.
   * **[!UICONTROL Basato su evento:]** selezionare l&#39;opzione per avviare il salvataggio del contenuto in base all&#39;attivazione di un evento.

   Quando selezionate un attivatore, la casella Configurazione strategia è abilitata. La finestra Configurazione strategia consente di:

   * Specificare un intervallo di tempo se si seleziona il trigger **[!UICONTROL Time based]**.
   * Specificate un nome evento se selezionate l&#39;attivatore **[!UICONTROL basato sull&#39;evento]**.

   <!-- You can also create and add your own custom strategy to the list. For details, see [Implement a custom strategy to autosave the forms](auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p). -->

1. (Solo salvataggio automatico basato su tempo) Effettuate le seguenti operazioni per configurare le opzioni per l&#39;salvataggio automatico basato su tempo.

   1. Nella casella **[!UICONTROL Salvataggio automatico su questo intervallo]**, specificare l&#39;intervallo di tempo in secondi. Il modulo viene salvato ripetutamente dopo la scadenza del numero di secondi specificato nella casella di intervallo.

1. (Solo salvataggio automatico basato su eventi) Effettuate le seguenti operazioni per configurare le opzioni per il salvataggio automatico basato su eventi.

   1. Nella casella **[!UICONTROL Salvataggio automatico dopo questo evento]**, specificare un evento [GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html). Il modulo viene salvato ogni volta che l&#39;espressione restituisce TRUE.

1. (Facoltativo) Per salvare automaticamente il contenuto per gli utenti anonimi, selezionare l&#39;opzione **[!UICONTROL Abilita salvataggio automatico per utenti anonimi]**, quindi fare clic su **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >Affinché l&#39;opzione di salvataggio automatico funzioni correttamente per gli utenti anonimi, è necessario configurare il servizio di configurazione comune di Forms in modo da consentire a tutti gli utenti di visualizzare in anteprima, verificare e firmare i moduli.
   >
   >Per configurare il servizio, andate alla configurazione della console Web Adobe Experience Manager in `https://'[server]:[port]'system/console/configMgr` e modificate il **[!UICONTROL servizio di configurazione comune Forms]** per scegliere l&#39;opzione **[!UICONTROL Tutti gli utenti]** nel campo **[!UICONTROL Consenti]**, quindi salvate la configurazione.