---
title: Come creare un modulo adattivo
description: Scopri come creare un modulo adattivo utilizzando [!DNL Experience Manager Forms]. I moduli adattivi sono moduli HTML5 reattivi che semplificano la raccolta e l’elaborazione delle informazioni. Approfondisci le modalità di creazione di un modulo adattivo basato su un modello di dati del modulo, un modello di modulo XFA e uno schema XML o JSON.
feature: Adaptive Forms
role: User, Developer
level: Beginner
exl-id: 2c25a8b7-73f7-40fb-a303-9446a708c8eb
source-git-commit: 654dcb7c9bbb73420df7494b21fddb8cb4fdd39a
workflow-type: tm+mt
source-wordcount: '1936'
ht-degree: 1%

---

# Creazione di un modulo adattivo {#creating-an-adaptive-form}

<span class="preview"> L’Adobe consiglia di utilizzare l’acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [creazione di un nuovo Forms adattivo](/help/forms/using/create-an-adaptive-form-core-components.md) o [aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html?lang=it) |
| AEM 6.5 | Questo articolo |

## Creare un modulo adattivo {#strong-create-an-adaptive-form-strong}

Per creare un modulo adattivo, segui la procedura riportata di seguito.

1. Accesso [!DNL Experience Manager Forms] Istanza di authoring in `https://'[server]:[port]'/<custom-context-if-any>.`

1. Immetti le credenziali nella pagina di accesso di Experience Manager.

   Dopo aver effettuato l’accesso, nell’angolo in alto a sinistra tocca **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.

   >[!NOTE]
   >
   >Per un’installazione predefinita, l’accesso è `admin` e la password è `admin`.

1. Tocca **[!UICONTROL Crea]** e seleziona **[!UICONTROL Modulo adattivo]**.
1. Viene visualizzata un&#39;opzione per selezionare un modello. Per ulteriori informazioni sui modelli, consulta [Modelli di modulo adattivo](creating-adaptive-form.md#p-adaptive-form-templates-p). Tocca un modello per selezionarlo, quindi tocca Avanti.
1. Viene visualizzata un&#39;opzione per &quot;Aggiungi proprietà&quot;. Specificare i valori per i seguenti campi proprietà. I campi Titolo e Nome sono obbligatori:

   * **[!UICONTROL Titolo:]** Specifica il nome visualizzato del modulo. Il titolo consente di identificare il modulo nel [!DNL Experience Manager Forms] dell&#39;utente.
   * **[!UICONTROL Nome:]** Specifica il nome del modulo. Nell&#39;archivio viene creato un nodo con il nome specificato. Quando si inizia a digitare un titolo, il valore del campo del nome viene generato automaticamente. Puoi modificare il valore suggerito. Il campo del nome può contenere solo caratteri alfanumerici, trattini e trattini bassi. Tutti gli input non validi vengono sostituiti da un trattino.
   * **[!UICONTROL Descrizione:]** Specifica le informazioni dettagliate sul modulo.
   * **[!UICONTROL Tag:]** Specifica i tag per identificare in modo univoco il modulo adattivo. Aiuto sui tag nella ricerca nel modulo. Per creare i tag, digita i nuovi nomi dei tag nel **[!UICONTROL Tag]** casella.

1. Puoi creare un modulo adattivo basato su uno dei seguenti modelli di modulo:

   * [Modello dati modulo](#fdm)
   * [Modello di modulo XFA](#create-an-adaptive-form-based-on-an-xfa-form-template)
   * [Schema XML o JSON](#create-an-adaptive-form-based-on-xml-or-json-schema)
   * Nessuno o senza modello modulo

   Puoi configurarli dalla sezione **[!UICONTROL Modello modulo]** scheda della **[!UICONTROL Aggiungi proprietà]** pagina. Per impostazione predefinita, il modello di modulo selezionato è **[!UICONTROL Nessuno]**.

1. Tocca **[!UICONTROL Crea]**. Viene creato un modulo adattivo e viene visualizzata una finestra di dialogo per aprire il modulo per la modifica.

   Dopo aver specificato tutte le proprietà, fare clic su **[!UICONTROL Crea]**. Viene creato un modulo adattivo e viene visualizzata una finestra di dialogo per aprire il modulo per la modifica.

   Dopo aver specificato tutte le proprietà, fare clic su **[!UICONTROL Crea]**. Viene creato un modulo adattivo e viene visualizzata una finestra di dialogo per aprire il modulo per la modifica.

1. Tocca **[!UICONTROL Apri]** per aprire il modulo appena creato in una nuova scheda. Il modulo si apre per la modifica e visualizza il contenuto disponibile nel modello. Viene inoltre visualizzata la barra laterale per personalizzare il modulo appena creato in base alle esigenze.

   In base al tipo di modulo adattivo, gli elementi del modulo presenti nel modello di modulo XFA, nello schema XML o nello schema JSON associato vengono visualizzati nel **[!UICONTROL Oggetti modello dati]** scheda di **[!UICONTROL Browser contenuti]** nella barra laterale. Puoi anche trascinare questi elementi per creare il modulo adattivo.

   Per informazioni sull’interfaccia di authoring di moduli adattivi e sui componenti disponibili, consulta [Introduzione all’authoring di moduli adattivi](introduction-forms-authoring.md).

   >[!NOTE]
   >
   >Consenti alle finestre popup nel browser di aprire il modulo appena creato in una nuova scheda.

## Creare un modulo adattivo basato su un modello di dati del modulo {#fdm}

[[!DNL Experience Manager Forms] integrazione dei dati](data-integration.md) consente di integrare più origini dati e di unire le rispettive entità e servizi per creare un modello di dati modulo. Si tratta di un’estensione dello schema JSON. Puoi utilizzare un modello dati modulo per creare un modulo adattivo. Le entità o gli oggetti modello dati configurati in un modello dati modulo sono disponibili come oggetti modello dati per la creazione di moduli. Sono associati alle rispettive origini dati e utilizzati per precompilare un modulo e riscrivere i dati inviati alle rispettive origini dati. È inoltre possibile chiamare i servizi configurati in un modello di dati del modulo utilizzando le regole del modulo adattivo.

Per utilizzare un modello di dati modulo per creare un modulo adattivo:

1. Nella scheda Modello modulo della schermata Aggiungi proprietà, seleziona **[!UICONTROL Modello dati modulo]** nel **[!UICONTROL Seleziona da]** elenco a discesa.

   ![create-af-1-1](assets/create-af-1-1.png)

1. Tocca per espandere **[!UICONTROL Seleziona modello dati modulo]**. Sono elencati tutti i modelli di dati dei moduli disponibili.

   Seleziona un dal modello dati.

   ![create-af-2-1](assets/create-af-2-1.png)

>[!NOTE]
>
>È inoltre possibile modificare il modello dati del modulo per un modulo adattivo. Per i passaggi dettagliati, consulta [Modificare le proprietà di un modello di modulo adattivo](#edit-form-model).

## Creare un modulo adattivo basato su un modello di modulo XFA {#create-an-adaptive-form-based-on-an-xfa-form-template}

Puoi riutilizzare i modelli di modulo XFA per creare moduli adattivi. Per riutilizzare, carica e associa un modello di modulo XFA a un modulo adattivo. Gli elementi del modello di modulo (modulo XFA) sono resi disponibili per l’utilizzo nel Finder di contenuti al momento dell’authoring dei moduli adattivi. Da Content Finder è possibile trascinare gli elementi del modello di modulo nel modulo.

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

## Creare un modulo adattivo basato su schema XML o JSON {#create-an-adaptive-form-based-on-xml-or-json-schema}

Gli schemi XML e JSON rappresentano la struttura in cui i dati vengono prodotti o utilizzati dal sistema back-end dell’organizzazione. È possibile associare uno schema a un modulo adattivo e utilizzarne gli elementi per aggiungere contenuto dinamico al modulo adattivo. Gli elementi dello schema sono disponibili nella scheda Oggetto modello dati del browser dei contenuti per la creazione di moduli adattivi. Puoi trascinare gli elementi dello schema per creare il modulo.

Consulta i seguenti documenti per comprendere come progettare schemi XML o JSON per la creazione di moduli adattivi.

* [Creazione di moduli adattivi tramite schema XML](adaptive-form-xml-schema-form-model.md)
* [Creazione di moduli adattivi tramite schema JSON](adaptive-form-json-schema-form-model.md)

Per utilizzare uno schema XML o JSON come modello di modulo per un modulo adattivo, effettua le seguenti operazioni:

1. Il giorno **[!UICONTROL Aggiungi proprietà]** passaggio della pagina di creazione di moduli adattivi, tocca il **[!UICONTROL Modello modulo]** scheda.
1. Nella scheda Modello modulo, seleziona **[!UICONTROL Schema]** dal **[!UICONTROL Seleziona da]** campo a discesa.

1. Tocca **[!UICONTROL Seleziona schema]** ed effettuare una delle seguenti operazioni:

   * **[!UICONTROL Carica da disco]** - Seleziona questa opzione e tocca Carica definizione schema per sfogliare e caricare uno schema XML o JSON dal file system. Il file dello schema caricato risiede con il modulo e non è accessibile ad altri moduli adattivi.
   * **[!UICONTROL Cerca nel repository]** - Selezionare questa opzione per effettuare una selezione dall&#39;elenco dei file di definizione dello schema disponibili nel repository. Seleziona il file di schema XML o JSON come modello del modulo. Lo schema selezionato è associato al modulo per riferimento ed è accessibile per l’utilizzo in altri moduli adattivi.

   >[!CAUTION]
   >
   >Assicurati che il nome file dello schema JSON termini con **.schema.json**. Ad esempio: mySchema.schema.json

   ![Selezione dello schema XML o JSON](assets/upload-schema.png)
   **Figura:** *Selezione dello schema XML o JSON*

1. (Solo per schema XML) Dopo aver selezionato o caricato uno schema XML, specifica un elemento principale del file XSD selezionato da mappare al modulo adattivo.

   ![Selezione dell’elemento principale XSD](assets/xsd-root-element.png)
   **Figura:** *Selezione dell’elemento principale XSD*

>[!NOTE]
>
>È inoltre possibile modificare lo schema per un modulo adattivo. Per i passaggi dettagliati, consulta [Modificare le proprietà di un modello di modulo adattivo](#edit-form-model).

## Modelli di modulo adattivo {#adaptive-form-templates}

Un modello fornisce una struttura di base e definisce l’aspetto (layout e stili) di un modulo adattivo. Include componenti preformattati contenenti determinate proprietà e struttura del contenuto. <!-- Out of the box, AEM Forms provides some adaptive form templates. To get the complete template package including advanced templates, you need to install the AEM Forms add-on package. For more information, see [Installing AEM Forms add-on package](installing-configuring-aem-forms-osgi.md).-->

Inoltre, puoi utilizzare l’editor modelli per creare modelli personalizzati. Per ulteriori informazioni sull&#39;utilizzo dei modelli, vedere [Modelli di modulo adattivo](template-editor.md).

>[!NOTE]
>
>Quando apri un modulo adattivo creato utilizzando il modello avanzato per la modifica, viene visualizzato un messaggio di errore. Il modello avanzato include un componente Passaggio di firma per il quale Adobe Sign è abilitato per impostazione predefinita. Crea e seleziona un [Configurazione cloud Adobe Sign](adobe-sign-integration-adaptive-forms.md) e [configurare un firmatario](working-with-adobe-sign.md#addsignerstoanadaptiveform) per risolvere l&#39;errore.

## Modificare le proprietà di un modello di modulo adattivo {#edit-form-model}

I moduli adattivi vengono creati senza un modello di modulo (utilizzando l’opzione Nessuno per il modello di modulo) o utilizzando un modello di modulo come un modello di modulo, uno schema XML o uno schema JSON o un modello di dati del modulo. È possibile modificare il modello di modulo per un modulo adattivo da Nessuno a un altro modello di modulo. Per i moduli adattivi basati su un modello di modulo, è possibile scegliere un altro modello di modulo, uno schema XML, uno schema JSON o un altro modello di dati del modulo per lo stesso modello di modulo. Non è tuttavia possibile passare da un modello di modulo a un altro.

1. Seleziona il modulo adattivo e tocca il **Proprietà** icona.
1. Apri **[!UICONTROL Modello modulo]** ed effettuare una delle seguenti operazioni.

   * Se il modulo adattivo non dispone di un modello di modulo, puoi scegliere un altro modello di modulo e di conseguenza selezionare un modello di modulo, uno schema XML o JSON o un modello di dati del modulo.
   * Se il modulo adattivo è basato su un modello di modulo, è possibile scegliere un altro modello di modulo, uno schema XML o JSON o un modello di dati del modulo per lo stesso modello di modulo.

1. Tocca **[!UICONTROL Salva]** per salvare le proprietà.

## Salvataggio automatico di un modulo adattivo {#auto-save-an-adaptive-form}

Per impostazione predefinita, il contenuto di un modulo adattivo viene salvato durante un’azione dell’utente, ad esempio premendo il pulsante Salva. Puoi anche configurare un modulo adattivo in modo che inizi automaticamente a salvare il contenuto in base a un evento o a un intervallo di tempo. L’opzione di salvataggio automatico è utile in:

* Salvataggio automatico del contenuto per utenti anonimi e connessi
* Salvataggio del contenuto di un modulo senza o con un intervento minimo da parte dell&#39;utente
* Iniziare a salvare il contenuto di un modulo basato su un evento utente
* Salvataggio ripetuto del contenuto di un modulo dopo un intervallo di tempo specificato

### Abilita salvataggio automatico per un modulo adattivo {#enable-auto-save-for-an-adaptive-form}

Per impostazione predefinita, l’opzione di salvataggio automatico non è abilitata. Puoi abilitare l’opzione salvataggio automatico dalla scheda Salvataggio automatico di un modulo adattivo. La scheda Salvataggio automatico fornisce anche diverse altre opzioni di configurazione. Per abilitare e configurare l’opzione di salvataggio automatico per un modulo adattivo, effettua le seguenti operazioni:

1. Per accedere alla sezione di salvataggio automatico nelle proprietà, seleziona un componente, quindi tocca ![a livello di campo](assets/field-level.png) > **[!UICONTROL Contenitore modulo adattivo]**, quindi tocca ![cmppr](assets/cmppr.png).
1. In **[!UICONTROL Salvataggio automatico]** sezione, **[!UICONTROL Abilita]** opzione di salvataggio automatico.
1. In **[!UICONTROL Evento modulo adattivo]** , specificare 1 o TRUE per iniziare automaticamente a salvare il modulo al caricamento nel browser. È inoltre possibile specificare un&#39;espressione condizionale per un evento che, quando viene attivato e restituisce true, inizia a salvare il contenuto del modulo.
1. Specifica il trigger. Il salvataggio automatico viene attivato in base alla configurazione. Le opzioni disponibili sono:

   * **[!UICONTROL Basato su tempo:]** Seleziona l’opzione per iniziare a salvare il contenuto in base a un intervallo di tempo specifico.
   * **[!UICONTROL Basato su evento:]** Seleziona l’opzione per iniziare a salvare il contenuto in base a quando viene attivato un evento.

   Quando si seleziona un trigger, la casella Configurazione strategia (Strategy Configuration) viene attivata. La casella Configurazione strategia (Strategy Configuration) consente di:

   * Specifica un intervallo di tempo se selezioni **[!UICONTROL Basato su tempo]** trigger.
   * Specifica un nome evento se selezioni **[!UICONTROL Basato su evento]** trigger.

   <!-- You can also create and add your own custom strategy to the list. For details, see [Implement a custom strategy to autosave the forms](auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p). -->

1. (Solo salvataggio automatico basato sul tempo) Per configurare le opzioni per il salvataggio automatico basato sul tempo, effettuare le seguenti operazioni.

   1. In **[!UICONTROL Salva automaticamente in questo intervallo]** , specificare l&#39;intervallo di tempo in secondi. Il modulo viene salvato ripetutamente allo scadere del numero di secondi specificato nella casella Intervallo.

1. (Solo salvataggio automatico basato su eventi) Per configurare le opzioni per il salvataggio automatico basato su eventi, effettuare le seguenti operazioni.

   1. In **[!UICONTROL Salva automaticamente dopo questo evento]** , specificare un [GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html) evento. Il modulo viene salvato ogni volta che l’espressione restituisce TRUE.

1. (Facoltativo) Per salvare automaticamente il contenuto per gli utenti anonimi, seleziona la **[!UICONTROL Abilita salvataggio automatico per utenti anonimi]** e fai clic su **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >Affinché l&#39;opzione di salvataggio automatico funzioni per gli utenti anonimi, accertati di configurare il servizio Configurazione comune di Forms per consentire a tutti gli utenti di visualizzare in anteprima, verificare e firmare i moduli.
   >
   >Per configurare il servizio, vai alla pagina di configurazione della console web di Adobe Experience Manager all’indirizzo `https://'[server]:[port]'system/console/configMgr` e modificare il **[!UICONTROL Servizio di configurazione comune di Forms]** per scegliere **[!UICONTROL Tutti gli utenti]** opzione in **[!UICONTROL Consenti]** e salva la configurazione.
