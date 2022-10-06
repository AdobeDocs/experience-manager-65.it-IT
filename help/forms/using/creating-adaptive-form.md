---
title: Come creare un modulo adattivo
description: Scopri come creare un modulo adattivo utilizzando [!DNL Experience Manager Forms]. I moduli adattivi sono moduli HTML5 reattivi che semplificano la raccolta e l’elaborazione delle informazioni. Scopri come creare un modulo adattivo basato su un modello di dati modulo, un modello di modulo XFA e uno schema XML o JSON.
feature: Adaptive Forms
role: User, Developer
level: Beginner
exl-id: 2c25a8b7-73f7-40fb-a303-9446a708c8eb
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1856'
ht-degree: 0%

---

# Creazione di un modulo adattivo {#creating-an-adaptive-form}

## <strong>Creare un modulo adattivo</strong> {#strong-create-an-adaptive-form-strong}

Per creare un modulo adattivo, effettua le seguenti operazioni.

1. Accesso [!DNL Experience Manager Forms] Istanza autore in `https://'[server]:[port]'/<custom-context-if-any>.`

1. Immetti le credenziali nella pagina di accesso di Experience Manager.

   Dopo aver effettuato l’accesso, nell’angolo in alto a sinistra tocca **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.

   >[!NOTE]
   >
   >Per un&#39;installazione predefinita, l&#39;accesso è `admin` e la password è `admin`.

1. Tocca **[!UICONTROL Crea]** e seleziona **[!UICONTROL Modulo adattivo]**.
1. Viene visualizzata un’opzione per selezionare un modello. Per ulteriori informazioni sui modelli, consulta [Modelli di modulo adattivi](creating-adaptive-form.md#p-adaptive-form-templates-p). Toccare un modello per selezionarlo e toccare Avanti.
1. Viene visualizzata l’opzione &quot;Aggiungi proprietà&quot;. Specifica i valori per i seguenti campi di proprietà. I campi Titolo e Nome sono obbligatori:

   * **[!UICONTROL Titolo:]** Specifica il nome visualizzato del modulo. Il titolo consente di identificare il modulo nel [!DNL Experience Manager Forms] interfaccia utente.
   * **[!UICONTROL Nome:]** Specifica il nome del modulo. Nel repository viene creato un nodo con il nome specificato. Quando si inizia a digitare un titolo, il valore del campo nome viene generato automaticamente. È possibile modificare il valore suggerito. Il campo name può includere solo caratteri alfanumerici, trattini e caratteri di sottolineatura. Tutti gli input non validi vengono sostituiti con un trattino.
   * **[!UICONTROL Descrizione:]** Specifica le informazioni dettagliate sul modulo.
   * **[!UICONTROL Tag:]** Specifica i tag per identificare in modo univoco il modulo adattivo. I tag consentono di cercare il modulo. Per creare i tag, digitate nuovi nomi di tag nella sezione **[!UICONTROL Tag]** scatola.

1. È possibile creare un modulo adattivo basato su uno dei seguenti modelli di modulo:

   * [Modello dati modulo](#fdm)
   * [Modello di modulo XFA](#create-an-adaptive-form-based-on-an-xfa-form-template)
   * [Schema XML o JSON](#create-an-adaptive-form-based-on-xml-or-json-schema)
   * Nessuno o senza un modello di modulo

   Puoi configurarli dalla **[!UICONTROL Modello Modulo]** nella scheda **[!UICONTROL Aggiungi proprietà]** pagina. Per impostazione predefinita, il modello di modulo selezionato è **[!UICONTROL Nessuno]**.

1. Tocca **[!UICONTROL Crea]**. Viene creato un modulo adattivo e viene visualizzata una finestra di dialogo per aprire il modulo per la modifica.

   Una volta completata la specificazione di tutte le proprietà, fai clic su **[!UICONTROL Crea]**. Viene creato un modulo adattivo e viene visualizzata una finestra di dialogo per aprire il modulo per la modifica.

   Una volta completata la specificazione di tutte le proprietà, fai clic su **[!UICONTROL Crea]**. Viene creato un modulo adattivo e viene visualizzata una finestra di dialogo per aprire il modulo per la modifica.

1. Tocca **[!UICONTROL Apri]** per aprire il modulo appena creato in una nuova scheda. Il modulo viene aperto per la modifica e visualizza il contenuto disponibile nel modello. Visualizza inoltre la barra laterale per personalizzare il modulo appena creato in base alle esigenze.

   In base al tipo di modulo adattivo, gli elementi del modulo presenti nel modello di modulo XFA, nello schema XML o nello schema JSON associati vengono visualizzati nel **[!UICONTROL Oggetti del modello dati]** della scheda **[!UICONTROL Browser dei contenuti]** nella barra laterale. Puoi anche trascinare questi elementi per creare il modulo adattivo.

   Per informazioni sull’interfaccia per la creazione di moduli adattivi e sui componenti disponibili, consulta [Introduzione alla creazione di moduli adattivi](introduction-forms-authoring.md).

   >[!NOTE]
   >
   >Consente alle finestre a comparsa nel browser di aprire il modulo appena creato in una nuova scheda.

## Creare un modulo adattivo basato su un modello di dati modulo {#fdm}

[[!DNL Experience Manager Forms] integrazione dei dati](data-integration.md) consente di integrare più origini dati e di riunire le relative entità e servizi per creare un modello dati modulo. È un&#39;estensione dello schema JSON. È possibile utilizzare un modello dati modulo per creare un modulo adattivo. Le entità o gli oggetti modello dati configurati in un modello dati modulo sono disponibili come oggetti modello dati per la creazione di moduli. Sono associati alle rispettive origini dati e vengono utilizzati per precompilare un modulo e riscrivere i dati inviati alle rispettive origini dati. È inoltre possibile chiamare i servizi configurati in un modello dati modulo utilizzando regole del modulo adattive.

Per utilizzare un modello dati modulo per la creazione di un modulo adattivo:

1. Nella scheda Modello modulo della schermata Aggiungi proprietà, selezionare **[!UICONTROL Modello dati modulo]** in **[!UICONTROL Seleziona da]** elenco a discesa.

   ![create-af-1-1](assets/create-af-1-1.png)

1. Tocca per espandere **[!UICONTROL Seleziona modello dati modulo]**. Sono elencati tutti i modelli di dati modulo disponibili.

   Seleziona un modello dati da.

   ![create-af-2-1](assets/create-af-2-1.png)

>[!NOTE]
>
>È inoltre possibile modificare il modello dati del modulo per un modulo adattivo. Per i passaggi dettagliati vedi [Modificare le proprietà del modello di modulo di un modulo adattivo](#edit-form-model).

## Creare un modulo adattivo basato su un modello di modulo XFA {#create-an-adaptive-form-based-on-an-xfa-form-template}

È possibile riutilizzare i modelli di modulo XFA per creare moduli adattivi. Per riutilizzare, caricare e associare un modello di modulo XFA a un modulo adattivo. Gli elementi del modello di modulo (modulo XFA) sono resi disponibili per l’utilizzo in Content Finder al momento della creazione di moduli adattivi. Da Content Finder è possibile trascinare gli elementi del modello di modulo sul modulo.

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

Gli schemi XML e JSON rappresentano la struttura in cui i dati vengono prodotti o utilizzati dal sistema back-end della tua organizzazione. È possibile associare uno schema a un modulo adattivo e utilizzarne gli elementi per aggiungere contenuto dinamico al modulo adattivo. Gli elementi dello schema sono disponibili nella scheda Oggetto modello dati del browser del contenuto per la creazione di moduli adattivi. È possibile trascinare gli elementi dello schema per creare il modulo.

Per informazioni su come progettare uno schema XML o JSON per la creazione di moduli adattivi, consulta i documenti seguenti.

* [Creazione di moduli adattivi tramite schema XML](adaptive-form-xml-schema-form-model.md)
* [Creazione di moduli adattivi tramite lo schema JSON](adaptive-form-json-schema-form-model.md)

Per utilizzare lo schema XML o JSON come modello di modulo per un modulo adattivo, procedi come segue:

1. Sulla **[!UICONTROL Aggiungi proprietà]** passaggio della pagina di creazione di moduli adattivi, tocca **[!UICONTROL Modello Modulo]** scheda .
1. Nella scheda Modello di modulo, selezionare **[!UICONTROL Schema]** dal **[!UICONTROL Seleziona da]** campo a discesa.

1. Tocca **[!UICONTROL Seleziona schema]** ed effettuare una delle seguenti operazioni:

   * **[!UICONTROL Carica dal disco]** - Seleziona questa opzione e tocca Carica definizione schema per sfogliare e caricare uno schema XML o uno schema JSON dal file system. Il file di schema caricato si trova con il modulo e non è accessibile ad altri moduli adattivi.
   * **[!UICONTROL Cerca nell’archivio]** - Selezionare questa opzione per selezionare dall&#39;elenco dei file di definizione dello schema disponibili nel repository. Selezionare il file di schema XML o JSON come modello di modulo. Lo schema selezionato è associato al modulo tramite riferimento ed è accessibile per l’uso in altri moduli adattivi.

   >[!CAUTION]
   >
   >Assicurati che il nome del file dello schema JSON termini con **.schema.json**. Ad esempio: mySchema.schema.json

   ![Selezione dello schema XML o JSON](assets/upload-schema.png)
   **Figura:** *Selezione dello schema XML o JSON*

1. (Solo per schema XML) Dopo aver selezionato o caricato uno schema XML, specificare un elemento principale del file XSD selezionato da mappare con il modulo adattivo.

   ![Selezione dell&#39;elemento principale XSD](assets/xsd-root-element.png)
   **Figura:** *Selezione dell&#39;elemento principale XSD*

>[!NOTE]
>
>È inoltre possibile modificare lo schema di un modulo adattivo. Per i passaggi dettagliati vedi [Modificare le proprietà del modello di modulo di un modulo adattivo](#edit-form-model).

## Modelli di modulo adattivi {#adaptive-form-templates}

Un modello fornisce una struttura di base e definisce l’aspetto (layout e stili) di un modulo adattivo. Dispone di componenti preformattati contenenti determinate proprietà e struttura del contenuto. <!-- Out of the box, AEM Forms provides some adaptive form templates. To get the complete template package including advanced templates, you need to install the AEM Forms add-on package. For more information, see [Installing AEM Forms add-on package](installing-configuring-aem-forms-osgi.md).-->

Inoltre, puoi utilizzare l’editor modelli per creare modelli personalizzati. Per ulteriori informazioni sull’utilizzo dei modelli, consulta [Modelli di modulo adattivi](template-editor.md).

>[!NOTE]
>
>Quando si apre un modulo adattivo creato utilizzando il modello avanzato per la modifica, viene visualizzato un messaggio di errore. Il modello avanzato dispone di un componente Passaggio firma e Adobe Sign è abilitato per impostazione predefinita. Crea e seleziona un [Configurazione cloud di Adobe Sign](adobe-sign-integration-adaptive-forms.md) e [configurare un firmatario](working-with-adobe-sign.md#addsignerstoanadaptiveform) per risolvere l&#39;errore.

## Modificare le proprietà del modello di modulo di un modulo adattivo {#edit-form-model}

I moduli adattivi vengono creati senza un modello di modulo (utilizzando l’opzione Nessuno per il modello di modulo) o utilizzando un modello di modulo, ad esempio un modello di modulo, uno schema XML o uno schema JSON o un modello di dati modulo. È possibile modificare il modello di modulo per un modulo adattivo da Nessuno a un altro modello di modulo. Per i moduli adattivi basati su un modello di modulo, è possibile scegliere un altro modello di modulo, schema XML, schema JSON o modello di dati modulo per lo stesso modello di modulo. Tuttavia, non è possibile passare da un modello di modulo all’altro.

1. Seleziona il modulo adattivo e tocca il **Proprietà** icona.
1. Apri **[!UICONTROL Modello Modulo]** e effettuare una delle seguenti operazioni.

   * Se il modulo adattivo non dispone di un modello di modulo, è possibile scegliere un altro modello di modulo e quindi selezionare un modello di modulo, uno schema XML o JSON o un modello di dati modulo.
   * Se il modulo adattivo è basato su un modello di modulo, è possibile scegliere un altro modello di modulo, schema XML o JSON o modello di dati modulo per lo stesso modello di modulo.

1. Tocca **[!UICONTROL Salva]** per salvare le proprietà.

## Salvataggio automatico di un modulo adattivo {#auto-save-an-adaptive-form}

Per impostazione predefinita, il contenuto di un modulo adattivo viene salvato in seguito a un’azione dell’utente, ad esempio premendo il pulsante salva. È inoltre possibile configurare un modulo adattivo per iniziare automaticamente a salvare il contenuto in base a un evento o a un intervallo di tempo. L’opzione di salvataggio automatico è utile in:

* Salvataggio automatico del contenuto per utenti anonimi e connessi
* Salvataggio del contenuto di un modulo senza o con intervento minimo dell’utente
* Inizio del salvataggio del contenuto di un modulo in base a un evento utente
* Salvataggio ripetuto del contenuto di un modulo dopo un intervallo di tempo specificato

### Abilita salvataggio automatico per un modulo adattivo {#enable-auto-save-for-an-adaptive-form}

Per impostazione predefinita, l’opzione di salvataggio automatico non è abilitata. È possibile abilitare l’opzione di salvataggio automatico dalla scheda Salvataggio automatico di un modulo adattivo. La scheda Salvataggio automatico fornisce anche diverse altre opzioni di configurazione. Esegui i seguenti passaggi per abilitare e configurare l’opzione di salvataggio automatico per un modulo adattivo:

1. Per accedere alla sezione di salvataggio automatico nelle proprietà, seleziona un componente, quindi tocca ![a livello di campo](assets/field-level.png) > **[!UICONTROL Contenitore di moduli adattivi]**, quindi tocca ![cmppr](assets/cmppr.png).
1. In **[!UICONTROL Salvataggio automatico]** sezione **[!UICONTROL Abilita]** l’opzione di salvataggio automatico.
1. In **[!UICONTROL Evento modulo adattivo]** specificare 1 o TRUE per iniziare automaticamente a salvare il modulo quando il modulo viene caricato nel browser. È inoltre possibile specificare un&#39;espressione condizionale per un evento che, quando attivato e restituito vero, inizia a salvare il contenuto del modulo.
1. Specifica il trigger. Il salvataggio automatico viene attivato in base alla configurazione. Le opzioni disponibili sono:

   * **[!UICONTROL Basato sul tempo:]** Seleziona l’opzione per iniziare a salvare il contenuto in base a un intervallo di tempo specifico.
   * **[!UICONTROL Basato su evento:]** Seleziona l’opzione per iniziare a salvare il contenuto in base all’attivazione di un evento.

   Quando selezioni un trigger, la casella Configurazione strategia è abilitata. La casella Configurazione strategia consente di:

   * Specifica un intervallo di tempo se selezioni **[!UICONTROL Basato sul tempo]** attivatore.
   * Specifica un nome evento se selezioni **[!UICONTROL Basato su eventi]** attivatore.

   <!-- You can also create and add your own custom strategy to the list. For details, see [Implement a custom strategy to autosave the forms](auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p). -->

1. (Solo salvataggio automatico basato su tempo) Esegui i seguenti passaggi per configurare le opzioni per l’salvataggio automatico basato su tempo.

   1. In **[!UICONTROL Salvataggio automatico in questo intervallo]** specificare l&#39;intervallo di tempo in secondi. Il modulo viene salvato ripetutamente dopo la scadenza del numero di secondi specificato nella casella Intervallo.

1. (Solo salvataggio automatico basato su eventi) Esegui i seguenti passaggi per configurare le opzioni per il salvataggio automatico basato su eventi.

   1. In **[!UICONTROL Salvataggio automatico dopo questo evento]** specificare un [GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html) evento. Il modulo viene salvato ogni volta che l’espressione restituisce TRUE.

1. (Facoltativo) Per salvare automaticamente il contenuto per gli utenti anonimi, seleziona la **[!UICONTROL Abilita salvataggio automatico per utenti anonimi]** e fai clic su **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >Affinché l’opzione di salvataggio automatico funzioni per gli utenti anonimi, è necessario configurare il servizio di configurazione comune di Forms per consentire a tutti gli utenti di visualizzare in anteprima, verificare e firmare i moduli.
   >
   >Per configurare il servizio, passa alla configurazione della console Web Adobe Experience Manager all’indirizzo `https://'[server]:[port]'system/console/configMgr` e modifica le **[!UICONTROL Servizio di configurazione comune Forms]** per scegliere **[!UICONTROL Tutti gli utenti]** in **[!UICONTROL Consenti]** e salva la configurazione.
