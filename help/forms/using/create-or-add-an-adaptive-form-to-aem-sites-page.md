---
title: Creare o aggiungere un modulo adattivo alla pagina AEM Sites
description: Scopri come creare o aggiungere facilmente un modulo adattivo alla pagina AEM Sites. Scopri le tecniche e le best practice passo passo per integrare moduli dinamici e personalizzabili nel tuo sito web, ottimizzando le tue esperienze digitali per il massimo impatto.
Keywords: AEM Forms in sites, AF in Sites editor, af in aem sites, aem sites af, add af to a sites page, af aem sites, af sites, create af in a sites page, adaptive form in aem sites, forms aem sites, add form to a sites page, adaptive forms aem sites, add adaptive forms to aem page, create forms in an aem sites page
feature: Adaptive Forms,Foundation Components
exl-id: dcf023a1-8735-48cb-b3ea-d17357eeedaf
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2884'
ht-degree: 3%

---

# Creare o aggiungere un modulo adattivo alla pagina AEM Sites {#create-or-add-an-adaptive-form-to-aem-sites-page}

<span class="preview"> Adobe consiglia di utilizzare l&#39;acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [la creazione di un nuovo Forms adattivo](/help/forms/using/create-an-adaptive-form-core-components.md) o [l&#39;aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | Questo articolo |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/create-or-add-an-adaptive-form-to-aem-sites-page.html?lang=it) |

Con AEM Forms puoi incorporare facilmente i moduli adattivi nelle pagine web. Questo consente ai visitatori di compilare e inviare i moduli in modo comodo, senza mai uscire dalla pagina in cui si trovano. In questo modo, possono rimanere coinvolti senza difficoltà con altri elementi del sito web interagendo attivamente con il modulo.

È possibile utilizzare l’Editor pagina AEM per creare e aggiungere rapidamente più moduli alle pagine AEM Sites. L’editor di pagine AEM consente agli autori di contenuti di creare esperienze di acquisizione dati fluide all’interno di una pagina Sites, sfruttando la potenza dei componenti per moduli adattivi, tra cui comportamento dinamico, convalide, integrazione dei dati, generazione di documenti di record e automazione dei processi aziendali. Consente inoltre di utilizzare varie funzioni delle pagine AEM Sites, come controllo delle versioni, targeting, traduzione e gestione multisito.

AEM Forms fornisce i componenti Contenitore modulo adattivo e Forms adattivo - Incorpora. È possibile utilizzare il Contenitore di moduli adattivi per creare un modulo in un frammento di esperienza o in una pagina AEM Sites, mentre il componente Forms adattivo - Incorpora consente di aggiungere un modulo adattivo esistente o di creare un modulo utilizzando l’editor di Forms adattivo.

![Modulo adattivo nella pagina Sites](/help/forms/using/assets/adaptive-form-in-sites-page.png)

## Vantaggi dell’utilizzo del componente Contenitore modulo adattivo nell’Editor pagina o nel Frammento di esperienza AEM

L’utilizzo di Adaptive Form Container nell’editor di pagine AEM consente di creare esperienze di acquisizione dati fluide all’interno di una pagina Sites utilizzando la potenza dei componenti di Forms adattivi, tra cui comportamento dinamico, convalide, integrazione di dati, generazione di documenti di record e automazione dei processi aziendali. Consente inoltre di utilizzare varie funzioni delle pagine AEM Sites, come controllo delle versioni, targeting, traduzione e gestione multisito, migliorando l’esperienza complessiva di creazione e gestione dei moduli. Esaminiamo alcune di queste funzioni:

* **Controllo delle versioni:** le pagine AEM Sites offrono [solide funzionalità di controllo delle versioni](/help/sites-authoring/working-with-page-versions.md), che consentono di tenere traccia e gestire versioni diverse dei moduli. In questo modo è possibile apportare modifiche e miglioramenti ai moduli mantenendo la possibilità di ripristinare le versioni precedenti, se necessario. Il controllo delle versioni garantisce un approccio controllato e organizzato allo sviluppo e all’evoluzione dei moduli.
* **Targeting (integrazione con Adobe Target):** Con le funzionalità di targeting delle pagine di AEM Sites, puoi anche [personalizzare l&#39;esperienza del modulo per tipi di pubblico diversi](/help/sites-administering/target.md). Utilizzando i segmenti utente e i criteri di targeting, è possibile adattare il contenuto, la progettazione o il comportamento del modulo a specifici gruppi di utenti. Questo ti consente di fornire un’esperienza di modulo personalizzata e rilevante, aumentando i tassi di coinvolgimento e conversione.
* **Traduzione:** AEM Sites [integrazione perfetta con i servizi di traduzione](/help/sites-administering/translation.md), che consente di tradurre facilmente i moduli in più lingue. Questa funzione semplifica il processo di localizzazione, garantendo che i moduli siano accessibili a un pubblico globale. Puoi gestire le traduzioni in modo efficiente all’interno dei progetti di traduzione AEM, riducendo il tempo e l’impegno necessari per il supporto di moduli multilingue. Per ulteriori informazioni sulla traduzione, consulta la sezione delle considerazioni.
* **Gestione multisito e Live Copy:** AEM Sites fornisce [solide funzionalità di gestione multisito e Live Copy](/help/sites-administering/msm.md), che consentono di creare e gestire più siti Web in un unico ambiente. Questa funzione consente ora di riutilizzare i moduli in siti diversi, garantendo coerenza e riducendo le attività di duplicazione. Grazie al controllo e alla gestione centralizzati, è possibile gestire e aggiornare in modo efficiente i moduli su più siti Web.
* **Temi:** le pagine AEM Sites forniscono un framework per la progettazione e la gestione di stili visivi coerenti su più pagine Web. Questi definiscono colori, font, fogli di stile e altri elementi visivi che contribuiscono all’aspetto generale del sito web. [Puoi utilizzare i temi progettati per una pagina AEM Sites per un modulo adattivo, risparmiando tempo e fatica](/help/sites-authoring/style-system.md).
* **Assegnazione tag:** le pagine AEM Sites ti consentono di [assegnare tag o etichette a una pagina, una risorsa o altro contenuto](/help/sites-authoring/tags.md). I tag sono parole chiave o etichette di metadati che consentono di categorizzare e organizzare il contenuto in base a criteri specifici. Puoi assegnare uno o più tag a pagine, risorse o qualsiasi altro elemento di contenuto all’interno di AEM per migliorare la ricerca e classificare le risorse.
* **Blocco e sblocco del contenuto:** AEM Sites consente agli utenti di [controllare l&#39;accesso e le modifiche alle pagine](/help/sites-authoring/editing-content.md#locking-a-page-locking-a-page) nell&#39;ambiente AEM Sites. Quando una pagina viene bloccata, significa che è protetta da modifiche o modifiche non autorizzate da parte di altri utenti. Solo l’utente che ha bloccato il contenuto o un amministratore designato può sbloccarlo per consentire modifiche.


## Varie opzioni per aggiungere un modulo adattivo nell’editor di pagine AEM

Puoi sfruttare appieno questa funzione utilizzando le seguenti opzioni:

* **[Aggiungi un modulo adattivo personalizzato a una pagina di AEM Sites:](#create-an-adaptive-form-in-sites-editor)** Crea un nuovo modulo da zero, adattandolo in modo specifico alle tue esigenze e preferenze di progettazione.

* **[Aggiungi un modulo adattivo personalizzato a un frammento di esperienza:](#create-an-adaptive-form-in-experience-fragment)** Estendi la portata dei moduli aggiungendoli ai frammenti di esperienza AEM per consentirne il riutilizzo su più pagine o siti.

* **[Convertire un modulo adattivo in frammento di esperienza:](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment)** Convertire un modulo adattivo aggiunto a una pagina AEM Sites in un frammento di esperienza per riutilizzare il modulo in più pagine AEM Sites.

* **Creazione e aggiunta di moduli basati su modelli approvati a una pagina AEM Sites:** Sfrutta i modelli preapprovati per creare rapidamente moduli in linea con le linee guida di branding e gli standard di progettazione della tua organizzazione. L’opzione è disponibile solo per Forms adattivo creato con il componente Forms Editor adattivo o Forms adattivo - Incorpora.

* **Aggiungi moduli esistenti a una pagina di AEM Sites:** Integra facilmente i moduli già creati nei tuoi siti Web, consentendo ai visitatori di interagire direttamente con essi. L’opzione è disponibile solo per Forms adattivo creato con il componente Forms Editor adattivo o Forms adattivo - Incorpora.

* **Aggiungere più moduli a una pagina AEM Sites o a un frammento di esperienza:** Aggiungere più moduli a una pagina per fornire più scelte agli utenti in base alle loro preferenze e requisiti. Questi possono essere una combinazione di forme nuove di zecca da zero e moduli esistenti.

## Considerazioni {#consideration}

* Quando utilizzi il Contenitore di moduli adattivi per creare o aggiungere un modulo, i moduli vengono tradotti e localizzati attraverso il flusso di traduzione AEM Sites. Per ogni lingua viene generata una copia separata (copia per lingua) della pagina del sito e dei moduli corrispondenti e, quando un autore di contenuto modifica una regola in un modulo nella pagina padre, le stesse modifiche devono essere apportate in tutte le copie per lingua del modulo. Il Contenitore di moduli adattivi consente inoltre di utilizzare varie funzioni delle pagine AEM Sites, come controllo delle versioni, targeting, traduzione e gestione multisito.

* Quando crei o aggiungi un modulo utilizzando il componente di incorporamento modulo adattivo, i moduli vengono tradotti e localizzati utilizzando il flusso di traduzione AEM Forms. In questo caso, viene mantenuto un singolo modulo a cui viene fatto riferimento in tutte le copie in lingua delle pagine di Sites. Il componente per l’incorporamento di moduli adattivi non fornisce l’accesso a varie funzioni delle pagine AEM Sites come, controllo delle versioni, targeting, traduzione e gestione multisito.


## Prima di iniziare {#before-you-start}

+++  Abilitare i componenti core Forms adattivi per il tuo ambiente

Assicurati che i [Componenti core adattivi di Forms siano abilitati per il tuo ambiente](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/quick-setup/enable-headless-adaptive-forms-and-core-components.html?lang=it).

+++

+++  Aggiungere librerie client Forms adattive ai componenti della pagina AEM Sites e della pagina Frammento esperienza

Per abilitare la funzionalità completa del componente Contenitore Forms adattivo, aggiungi le librerie client Customheaderlibs e Customfooterlibs alla pagina AEM Sites utilizzando la pipeline di distribuzione. Per aggiungere le librerie:

1. Accedi all’istanza di authoring dell’AEM e apri CRX DE. L&#39;URL predefinito per un&#39;istanza Autore in esecuzione localmente è `http://localhost:4502/crx/de`.

1. Aprire il file `/apps/[your-sites-project]/components/page/customheaderlibs.html` e aggiungere il codice seguente al file:

   ```
       //Customheaderlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
       </sly> 
   ```

1. Aprire il file `/apps/[your-sites-project]/components/page/customfooterlibs.html` e aggiungere il codice seguente al file:

   ```
       //customfooterlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
       </sly> 
   ```

1. Aprire il file `/apps/[your-sites-project]/components/xfpage/customheaderlibs.html` e aggiungere il codice seguente al file:

   ```
       //Customheaderlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
       </sly> 
   ```

1. Aprire il file `/apps/[your-sites-project]/components/customfooterlibs.html` e aggiungere il codice seguente al file:

   ```
       //customfooterlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
       </sly> 
   ```

1. Ripeti i passaggi precedenti per tutte le istanze Author e Publish nell’ambiente.

+++

+++ Abilita contenitore Forms adattivo

Per abilitare il componente [!UICONTROL Contenitore Forms adattivo] nel criterio del modello, eseguire la procedura seguente:

1. Apri la pagina AEM Sites o il frammento di esperienza per la modifica. Per aprire la pagina per la modifica, selezionarla e fare clic su Modifica.
1. Apri il modello della pagina Sites o Frammento esperienza. Per aprire il modello, vai a [!UICONTROL Informazioni pagina] ![Informazioni pagina](/help/forms/using/assets/Smock_Properties_18_N.svg) > [!UICONTROL Modifica modello]. Apre il modello corrispondente nell’editor modelli.
1. Nella visualizzazione Struttura fare clic sull&#39;icona **[!UICONTROL Criteri]** ![Criteri](/help/forms/using/assets/Smock_FeedManagement_18_N.svg) nella barra dei menu. Nell&#39;elenco **[!UICONTROL Componenti consentiti]** e selezionare la casella di controllo **[!UICONTROL Contenitore Forms adattivo]** in **[Nome progetto Archetipo AEM] - Modulo adattivo**.
1. Fai clic su **[!UICONTROL Fine]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419370?quality=12&learn=on)

+++

## Creare un modulo adattivo {#create-an-adaptive-form-in-sites-editor-or-experience-fragment}

Puoi creare un nuovo modulo da zero, adattandolo in modo specifico ai tuoi requisiti e alle preferenze di progettazione, direttamente in una pagina di AEM Sites o in Frammento di esperienza. Per i moduli monouso, si consiglia di creare direttamente una pagina di AEM Sites, mentre i frammenti di esperienza sono ideali per i moduli che devono essere riutilizzati in più pagine del sito web.

* [Creare un modulo in una pagina di AEM Sites](#create-an-adaptive-form-in-sites-editor)
* [Creare un modulo in un frammento di esperienza](#create-an-adaptive-form-in-experience-fragment)
* [Convertire un modulo adattivo nella pagina di AEM Sites in un frammento di esperienza](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment)

### Creare un modulo in una pagina di AEM Sites {#create-an-adaptive-form-in-sites-editor}

Puoi utilizzare il componente Contenitore modulo adattivo nell’Editor pagina AEM per creare un modulo personalizzato. Il componente consente di creare un modulo trascinandone e rilasciandone i componenti. I componenti del modulo sono basati su Componenti core. Puoi personalizzarli facilmente in base alle esigenze della tua organizzazione.

>[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

Per creare un modulo adattivo in una pagina Sites:

1. Apri la pagina AEM Sites in modalità di modifica.
1. Trascina il componente **[!UICONTROL Contenitore Forms adattivo]** dal browser Componenti alla pagina Sites. Crea uno spazio nella pagina per il modulo. Puoi utilizzare la modalità layout per modificare la dimensione dello spazio del contenitore.
1. Trascina i componenti core modulo adattivo nello spazio contenitore per creare il modulo.
1. Aggiungi il pulsante Invia.

Successivamente, [impostare l&#39;azione di invio](#configure-submit-action-for-form) e le proprietà avanzate.

### Creare un modulo in un frammento esperienza {#create-an-adaptive-form-in-experience-fragment}

Puoi estendere la portata dei moduli aggiungendoli ai Frammenti esperienza AEM per consentirne il riutilizzo su più pagine o siti. Ad esempio, puoi includere un modulo di iscrizione a una newsletter all’interno di un frammento di esperienza. In questo modo è possibile riutilizzare il frammento in più pagine del sito Web, eliminando la necessità di ricreare ripetutamente il modulo. Eventuali aggiornamenti o modifiche apportate al modulo di iscrizione alla newsletter all’interno del frammento di esperienza vengono propagate automaticamente a tutte le pagine in cui viene utilizzato. Questo semplifica il processo e garantisce un’esperienza utente fluida, semplificando al contempo la gestione dei moduli del sito web.

Per creare un modulo adattivo in un frammento di esperienza:

1. Apri un frammento di esperienza.
1. Trascina il componente **[!UICONTROL Contenitore Forms adattivo]** dal browser Componenti al frammento di esperienza.
1. Per creare il modulo, trascina i componenti core modulo adattivo nello spazio contenitore nel frammento di esperienza.
1. Aggiungi il pulsante Invia.

Successivamente, [impostare l&#39;azione di invio](#configure-submit-action-for-form) e le proprietà avanzate.

### Convertire un modulo adattivo in una pagina di AEM Sites in un frammento di esperienza {#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment}

È possibile convertire un modulo adattivo esistente in un editor di pagine Sites in un frammento di esperienza per riutilizzare il modulo in più pagine o siti.

Per convertire un modulo adattivo nella pagina di AEM Sites in un frammento di esperienza:

1. Apri la pagina AEM Sites contenente il modulo adattivo (nel componente Contenitore Forms adattivo) in modalità di modifica.
1. Apri la Struttura contenuto e seleziona il **[!UICONTROL Contenitore Forms adattivo]** che ospita il modulo adattivo. Una pagina AEM Sites può ospitare più Forms adattivi. Quindi, seleziona con attenzione il contenitore Forms adattivo corretto.
1. Sulla barra dei menu, seleziona l&#39;icona ![Converti in variante di frammento di esperienza](/help/forms/using/assets/Smock_FilingCabinet_18_N.svg) Converti in variante di frammento di esperienza.
   ![Conversione di un modulo nella pagina Sites in un frammento esperienza](/help/forms/using/assets/convert-form-in-sites-page-to-an-experience-fragment.png)

   Viene visualizzata una finestra di dialogo per convertire il contenitore Moduli adattivi in un nuovo frammento di esperienza o aggiungerlo a un frammento di esperienza esistente
1. Nella finestra di dialogo Converti in variante di frammento di esperienza, imposta i valori per le seguenti opzioni:

   * **Azione:** Seleziona questa opzione per creare un frammento di esperienza o Aggiungi a un frammento di esperienza esistente.
   * **Percorso principale:** Specificare il percorso della cartella in cui ospitare il frammento di esperienza. L’opzione è disponibile solo per la creazione di un frammento di esperienza.
   * **Modello:** Specifica il percorso del modello Frammento esperienza. Se non disponi di un modello di Frammento esperienza, [crealo](/help/sites-developing/experience-fragments.md). L’opzione è disponibile solo per aggiungere un modulo adattivo a un frammento di esperienza esistente.
   * **Titolo frammento:** Specifica il titolo del frammento esperienza. Il titolo identifica in modo univoco un frammento esperienza


## Configurare l’azione di invio per il modulo {#configure-submit-action-for-form}

Un’azione di invio consente di scegliere la destinazione dei dati acquisiti tramite un modulo adattivo. Viene attivato quando un utente fa clic sul pulsante Invia in un modulo adattivo. I moduli adattivi includono alcune azioni di invio pronte all’uso. Puoi anche estendere un’azione di invio predefinita per creare un’azione di invio personalizzata. Per configurare un&#39;azione di invio per il modulo:

1. Apri l’Editor pagina AEM o il Frammento di esperienza che contiene il Modulo adattivo.
1. Apri la Struttura contenuto e seleziona il **[!UICONTROL Contenitore Forms adattivo]** che ospita il modulo adattivo. Una pagina AEM Sites può ospitare più Forms adattivi. Quindi, seleziona con attenzione il contenitore Forms adattivo corretto.
1. Fai clic sull&#39;icona Proprietà contenitore modulo adattivo ![Proprietà contenitore modulo adattivo](/help/forms/using/assets/configure-icon.svg). Viene visualizzata la finestra di dialogo Contenitore modulo adattivo con cui configurare le azioni di invio.
   ![Contenitore moduli adattivi](/help/forms/using/assets/adaptive-forms-container.png)
1. Seleziona e configura un’azione Invia in base alle tue esigenze. Per informazioni dettagliate sulle azioni di invio, consulta [Azione di invio modulo adattivo](configuring-submit-actions.md)


## Configurare uno schema o un modello dati modulo per un modulo {#configure-schema-or-data-model-for-form}

È possibile utilizzare il modello dati modulo per collegare un modulo a un’origine dati per inviare e ricevere dati in base alle azioni degli utenti. Puoi anche collegare un modulo a uno schema JSON per ricevere i dati inviati in un formato predefinito.

Prima di collegare un modulo a uno schema o a un modello di dati del modulo

* [Crea uno schema JSON e caricalo nell’ambiente](adaptive-form-json-schema-form-model.md)
* [Creare un modello dati modulo](create-form-data-models.md)

Per configurare uno schema JSON o un modello dati modulo per il modulo:

1. Apri l’Editor pagina AEM o il Frammento di esperienza che contiene il Modulo adattivo.
1. Apri la Struttura contenuto e seleziona il **[!UICONTROL Contenitore Forms adattivo]** che ospita il modulo adattivo. Una pagina AEM Sites può ospitare più Forms adattivi. Quindi, seleziona con attenzione il contenitore Forms adattivo corretto.
1. Fai clic sull&#39;icona Proprietà contenitore modulo adattivo ![Proprietà contenitore modulo adattivo](/help/forms/using/assets/configure-icon.svg). Viene visualizzata la finestra di dialogo Contenitore modulo adattivo per configurare i modelli dati.
   ![Contenitore moduli adattivi modello dati modulo](/help/forms/using/assets/form-data-model-adaptive-forms-container.png)
1. Seleziona e configura uno schema JSON o un modello dati modulo, in base ai requisiti. Per informazioni dettagliate sulle azioni di invio, vedere [Azione di invio modulo adattivo](configuring-submit-actions.md).

   * Quando si seleziona l&#39;opzione **[!UICONTROL Modello modulo]**, utilizzare l&#39;opzione **[!UICONTROL Seleziona modello dati modulo]** per selezionare un modello dati modulo preconfigurato.
   * Quando selezioni l&#39;opzione **[!UICONTROL Schema]**, utilizza l&#39;opzione **[!UICONTROL Schema]** per selezionare uno schema JSON per il modulo.

1. Fai clic su **[!UICONTROL Fine]**.

## Configurare un servizio di precompilazione per un modulo {#configure-prefill-service-for-form}

Puoi utilizzare il servizio di precompilazione per compilare automaticamente i campi di un modulo adattivo utilizzando dati esistenti. Quando un utente apre un modulo, i valori di tali campi vengono precompilati. Operazioni disponibili:

* [Creare un servizio di precompilazione personalizzato](prepopulate-adaptive-form-fields.md)
* [Usa servizio di precompilazione modello dati modulo](#fdm-prefill-service)

### Utilizza il servizio di precompilazione del modello dati del modulo {#fdm-prefill-service}

È possibile utilizzare il servizio di precompilazione del modello dati modulo per precompilare i campi di un modulo utilizzando un modello dati modulo configurato. Il servizio di precompilazione del modello dati modulo utilizza il servizio [Get Service del modello dati modulo configurato](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services) per recuperare i dati. Per utilizzare il servizio di precompilazione del modello dati modulo per un modulo adattivo:

1. Apri l’Editor pagina AEM o il Frammento di esperienza che contiene il Modulo adattivo.
1. Apri la Struttura contenuto e seleziona il **[!UICONTROL Contenitore Forms adattivo]** che ospita il modulo adattivo. Una pagina AEM Sites può ospitare più Forms adattivi. Quindi, seleziona con attenzione il contenitore Forms adattivo corretto.
1. Fai clic sull&#39;icona Proprietà contenitore modulo adattivo ![Proprietà contenitore modulo adattivo](/help/forms/using/assets/configure-icon.svg). Viene visualizzata la finestra di dialogo Contenitore modulo adattivo per configurare i modelli dati.
   ![Editor pagina per siti fdm aem del servizio di precompilazione](/help/forms/using/assets/prefill-service-fdm-aem-sites-page-editor.png)
1. Seleziona un modello di dati modulo. Apri la scheda **[!UICONTROL Base]**. Nel servizio di precompilazione, selezionare **[!UICONTROL Servizio di precompilazione bozza di Forms Portal]**.
1. Fai clic su **[!UICONTROL Fine]**.

## Reindirizza l’utente a un nuovo utente all’invio del modulo o mostra un messaggio di ringraziamento

All&#39;invio di un modulo è possibile reindirizzare l&#39;utente a un&#39;altra pagina Web o a un messaggio. Per reindirizzare l’utente o configurare il messaggio di ringraziamento:

1. Apri l’Editor pagina AEM o il Frammento di esperienza che contiene il Modulo adattivo.
1. Apri la Struttura contenuto e seleziona il **[!UICONTROL Contenitore Forms adattivo]** che ospita il modulo adattivo. Una pagina AEM Sites può ospitare più Forms adattivi. Quindi, seleziona con attenzione il contenitore Forms adattivo corretto.
1. Fai clic sull&#39;icona Proprietà contenitore modulo adattivo ![Proprietà contenitore modulo adattivo](/help/forms/using/assets/configure-icon.svg). Viene visualizzata la finestra di dialogo Contenitore modulo adattivo per configurare i modelli dati.
1. Apri la scheda **[!UICONTROL Invio]**.

   * Per configurare un URL di reindirizzamento, per l’opzione Invia seleziona l’opzione Reindirizza all’URL e specifica un indirizzo assoluto o un URL di reindirizzamento o un percorso relativo di una pagina AEM Sites.

   * Per configurare un messaggio personalizzato o di ringraziamento, per l’opzione Invia seleziona l’opzione Mostra messaggio e specifica un messaggio nella casella Contenuto messaggio. Si tratta di una casella di testo RTF, è possibile utilizzare l&#39;opzione a schermo intero per visualizzare tutti gli elementi RTF disponibili.

## Consulta anche {#see-also}

* [Creare un modulo adattivo basato su Componenti core autonomi](/help/forms/using/create-an-adaptive-form-core-components.md)
* [Creare stili o temi per i moduli](/help/forms/using/create-or-customize-themes-for-adaptive-forms-core-components.md)
