---
title: Come si creano o personalizzano i temi dei moduli adattivi?
description: Scopri come creare o personalizzare i temi per i componenti core Adaptive Forms utilizzando le specifiche BEM
keywords: crea tema dei componenti core per moduli adattivi, crea un nuovo tema, personalizza il tema, carica un nuovo tema, utilizza il tema nei moduli, elimina un tema, crea un tema nei moduli AEM 6.5
contentOwner: Khushwant Singh
topic-tags: Adaptive Forms
docset: aem65
role: Admin, Developer
feature: Adaptive Forms,Core Components
exl-id: 9f9b35a3-0479-4179-9fad-994a482c96b6
solution: Experience Manager, Experience Manager Forms
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1939'
ht-degree: 5%

---

# Creare o personalizzare un tema per moduli adattivi {#introduction-to-theme}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components.html?lang=it) |
| AEM 6.5 | Questo articolo |


<!--**Applies to:** ✅ Adaptive Form Core Components ❎ [Adaptive Form Foundation Components](/help/forms/using/create-adaptive-form.md).-->

In AEM Forms 6.5, un tema è una libreria client AEM che puoi utilizzare per definire gli stili (look and feel) di un modulo adattivo. Un tema contiene dettagli sullo stile dei componenti e dei pannelli. Gli stili includono proprietà quali i colori di sfondo, i colori degli stati, la trasparenza, l’allineamento e le dimensioni. Quando applichi un tema, lo stile specificato si riflette sui componenti corrispondenti. Un tema viene gestito in modo indipendente senza un riferimento a un modulo adattivo e può essere riutilizzato in più Forms adattivi.

## Temi disponibili {#available-theme}

L’ambiente AEM 6.5 fornisce i temi elencati di seguito per i Forms adattivi basati su Componenti core:

* [Tema Area di lavoro](https://github.com/adobe/aem-forms-theme-canvas)
* [Tema WKND](https://github.com/adobe/aem-forms-theme-wknd)
* [Tema EASEL](https://github.com/adobe/aem-forms-theme-easel)
* [Tema FSI](https://github.com/adobe/aem-forms-theme-fsi)
* [Tema assistenza sanitaria](https://github.com/adobe/aem-forms-theme-healthcare)
* [Tema pubblico](https://github.com/adobe/aem-forms-theme-public)
* [Tema produzione](https://github.com/adobe/aem-forms-theme-manufacturing)

## Struttura dei temi {#understanding-structure-of-theme}

Un tema è un pacchetto che include il file CSS, i file JavaScript e le risorse (come le icone) che definiscono lo stile del Forms adattivo. Un tema Modulo adattivo segue un’organizzazione specifica, costituita dai seguenti componenti:

* `src/theme.scss`: questa cartella include il file CSS che ha un ampio impatto sull&#39;intero tema. Funge da posizione centralizzata per definire e gestire lo stile e il comportamento del tema. Apportando modifiche a questo file, puoi apportare modifiche applicate universalmente a tutto il tema, influenzando l’aspetto e le funzionalità sia delle pagine Forms adattive che delle pagine AEM Sites.

* `src/site`: questa cartella contiene file CSS applicati alla pagina di un intero sito AEM. Questi file sono costituiti da codice e stili che influiscono sulle funzionalità e sul layout generali della pagina del sito AEM. Tutte le modifiche apportate qui vengono applicate a tutte le pagine del sito.

* `src/components`: i file CSS in questa cartella sono progettati per i singoli componenti core AEM. Ogni cartella dedicata per un componente include un file `.scss` con lo stile di quel particolare componente all&#39;interno di un modulo adattivo. Ad esempio, il file `/src/components/button/_button.scss` contiene informazioni sullo stile del componente Pulsante Forms adattivo.

  ![Struttura Tema Area Di Lavoro](/help/forms/using/assets/component-based-theme-folder-structure.png)

* `src/resources`: questa cartella contiene file statici come icone, loghi e font. Queste risorse vengono utilizzate per migliorare gli elementi visivi e la progettazione complessiva del tema.

## Creare un tema

AEM Forms 6.5 fornisce i temi elencati di seguito per i Componenti core basati su Adaptive Forms.

* [Tema Area di lavoro](https://github.com/adobe/aem-forms-theme-canvas)
* [Tema WKND](https://github.com/adobe/aem-forms-theme-wknd)
* [Tema EASEL](https://github.com/adobe/aem-forms-theme-easel)
* [Tema pubblico](https://github.com/adobe/aem-forms-theme-public)
* [Tema produzione](https://github.com/adobe/aem-forms-theme-manufacturing)

Puoi [personalizzare uno di questi temi per creare un tema](#customize-a-theme-core-components).

## Personalizzare un tema {#customize-a-theme-core-components-based-adaptive-forms}

La personalizzazione di un tema si riferisce al processo di modifica e personalizzazione dell’aspetto di un tema. Quando si personalizza un tema, è possibile modificarne gli elementi di progettazione, il layout, i colori, la composizione tipografica e, a volte, il codice sottostante. Questo consente di creare un aspetto univoco e personalizzato per il sito web o l’applicazione, mantenendo la struttura e le funzionalità di base fornite dal tema.

>[!NOTE]
>
> * Utilizza Gestione pacchetti per distribuire un tema in tutte le istanze di Author e Publish.
> * Una libreria client tema viene importata o esportata tramite Gestione pacchetti come qualsiasi altro pacchetto.

### Prerequisiti per personalizzare un tema {#prerequisites}

* [Abilita i componenti core adattivi di Forms](/help/forms/using/enable-adaptive-forms-core-components.md) per il tuo ambiente.

* Installa la versione più recente di [Apache Maven.](https://maven.apache.org/download.cgi) Apache Maven è uno strumento di automazione della build comunemente utilizzato per i progetti Java™. L’installazione della versione più recente garantisce che tu disponga delle dipendenze necessarie per la personalizzazione del tema.

* Scopri come creare una [libreria client in Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/clientlibs.html?lang=it). AEM fornisce librerie client che consentono di memorizzare il codice lato client nell’archivio, organizzarlo in categorie e definire quando e come ogni categoria di codice deve essere trasmessa al client.

* Installa un editor di testo normale. Microsoft® Visual Studio Code. L&#39;utilizzo di un editor di testo normale come Microsoft® Visual Studio Code fornisce un ambiente semplice per la modifica e la modifica dei file dei temi.

* Assicurati che l’ambiente AEM Forms sia operativo.

### Considerazioni per personalizzare un tema {#consideration}

* Assicurati di utilizzare [il progetto Archetipo utilizzato per abilitare i Componenti core adattivi di Forms](/help/forms/using/enable-adaptive-forms-core-components.md) nell&#39;ambiente per personalizzare i temi.

* Quando si pubblica un modulo adattivo, le librerie client non vengono pubblicate automaticamente nell’istanza di Publish. Assicurati di pubblicare manualmente negli ambienti Publish la libreria client a cui si fa riferimento in un modulo adattivo.

* L’Adobe consiglia di non modificare i nomi delle classi delle librerie client.

### Personalizzare un tema {#customize-a-theme-core-components}

La creazione o la personalizzazione di un tema è un processo in più fasi. Per creare/personalizzare il tema, effettua le seguenti operazioni:

1. [Clonare un tema](#clone-git-repo-of-theme)
1. [Personalizzare l&#39;aspetto del tema](#customize-the-theme)
1. [Pronto per la distribuzione locale](#generate-the-clientlib)
1. [Distribuisci il tema in un ambiente locale](#deploy-the-theme-on-a-local-environment)
1. [Distribuire il tema nell’ambiente di produzione](#5-deploy-a-theme-on-your-production-environment)

<!--
 ![Theme Customization workflow](/help/forms/using/assets/custom-theme-steps.png)
-->

Gli esempi forniti nel documento sono basati sul tema **Canvas**, ma è possibile clonare qualsiasi tema e personalizzarlo seguendo le stesse istruzioni. Queste istruzioni sono applicabili a qualsiasi tema, consentendo di modificare i temi in base alle esigenze specifiche.

#### 1. Clona l’archivio Git del tema {#clone-git-repo-of-theme}

Per clonare un tema per Forms adattivo basato su Componenti core, scegli uno dei seguenti temi:

* [Tema Area di lavoro](https://github.com/adobe/aem-forms-theme-canvas)
* [Tema WKND](https://github.com/adobe/aem-forms-theme-wknd)
* [Tema EASEL](https://github.com/adobe/aem-forms-theme-easel)

Per clonare un tema, esegui le seguenti istruzioni:

1. Apri il prompt dei comandi o la finestra del terminale nell’ambiente di sviluppo locale.

1. Eseguire il comando `git clone` per clonare un tema.

   ```
      git clone [Path of Git Repository of the theme]
   ```

   Sostituisci il [percorso dell&#39;archivio Git del tema] con l&#39;URL effettivo dell&#39;archivio Git corrispondente del tema

   Ad esempio, per clonare il tema Canvas, eseguire il comando seguente:

   ```
      git clone https://github.com/adobe/aem-forms-theme-canvas
   ```

1. Seleziona **Considera affidabili gli autori di tutti i file presenti nella cartella principale** e fai clic su **Sì, considero affidabili gli autori**.

Dopo aver eseguito correttamente il comando, nella cartella `aem-forms-theme-canvas` del computer è disponibile una copia locale del tema.

#### 2. Personalizzare il tema {#customize-the-theme}

Puoi personalizzare i singoli componenti o apportare modifiche a livello di tema utilizzando le variabili globali di un tema. La modifica delle variabili globali ha un effetto a cascata su tutti i singoli componenti. Ad esempio, puoi utilizzare le variabili globali per modificare il colore del bordo di tutti i componenti all’interno di un modulo adattivo o applicare un colore di riempimento vibrante ai pulsanti di invito all’azione (CTA). Operazioni disponibili:

* [Impostare gli stili del livello tema](#theme-customization-global-level)

* [Impostare gli stili a livello di componente](#component-based-customization)

##### Impostare gli stili del livello tema {#theme-customization-global-level}

Il file `variable.scss` contiene le variabili globali del tema. Aggiornando queste variabili, puoi apportare modifiche relative allo stile a livello di tema. Per applicare gli stili a livello di tema, effettua le seguenti operazioni:

1. Apri il file `<your-theme-sources>/src/site/_variables.scss` per la modifica.
1. Modifica il valore di qualsiasi proprietà. Ad esempio, il colore di errore predefinito è il rosso. Per modificare il colore dell&#39;errore da rosso a blu, modificare il codice esadecimale del colore della variabile `$error`. Esempio: `$error: #196ee5`.

   ![Esempio: colore dell&#39;errore impostato su blu](/help/forms/using/assets/theme-level-changes.png)

1. Salva e chiudi il file.


Analogamente, è possibile utilizzare il file `variable.scss` per impostare la famiglia e il tipo di carattere, i colori del tema e del carattere, la dimensione del carattere, la spaziatura del tema, l&#39;icona di errore, gli stili del bordo del tema e altre variabili che influiscono su più componenti del modulo adattivo.

##### Impostare gli stili a livello di componente {#component-based-customization}

È inoltre possibile personalizzare il carattere, il colore, le dimensioni e altre proprietà CSS di componenti core Modulo adattivo specifici, quali pulsanti, caselle di controllo, contenitori, piè di pagina e altro ancora. Modificando il file CSS associato al componente specifico, puoi allinearne lo stile al branding dell’organizzazione. Per personalizzare lo stile di un componente, effettua le seguenti operazioni:

1. Aprire il file `<your-theme-sources>/src/components/<component>/<component.scss>` per la modifica. Ad esempio, per modificare il colore del carattere del componente pulsante, aprire `<your-theme-sources>/src/components/button/button.scss`, file .
1. Modifica il valore di qualsiasi in base alle tue esigenze. Ad esempio, per cambiare il colore del componente Pulsante al passaggio del mouse su Verde, modificare il valore della proprietà `color: $white` nella classe `cmp-adaptiveform-button__widget:hover` in #12b453 di codice esadecimale o in qualsiasi altra tonalità di verde. Il codice finale è simile al seguente:

   ```
    .cmp-adaptiveform-button__widget:hover {
    background: $dark-gray;
    color: #12b453;
    }
   ```


1. Salva e chiudi il file.

<!--

   ![Example: Hover color set to green](/help/forms/using/assets/button-customization.png)

-->

>[!NOTE]
>
> Quando uno stile viene definito sia a livello di tema che a livello di componente, lo stile definito a livello di componente ha la priorità.

#### 3. Preparare il tema per la distribuzione {#generate-the-clientlib}

Per distribuire un tema in un’istanza AEM, è necessario convertirlo in una libreria client. Per convertire il tema in una libreria client, effettua le seguenti operazioni:

1. Apri il prompt dei comandi o la finestra del terminale.
1. Passare alla cartella `<your-theme-sources>`. Ad esempio `C:\aem-forms-theme-canvas`
1. Esegui il comando seguente:

   ```
      npm run create-clientlib --category=adaptiveform.theme.[yourtheme]
   ```

   Sostituisci `[yourtheme]` con il nome del tema personalizzato. Ad esempio, se il nome del tema personalizzato è `customcanvastheme`, eseguire il comando seguente

   ```
       npm run create-clientlib --category=adaptiveform.theme.customcanvastheme
   ```

   Se il comando viene eseguito correttamente, verrà creata una cartella della libreria client in `themerepo\theme-clientlibs\[yourtheme]`.

   ![Generazione libreria client](/help/forms/using/assets/clientlib_created.png)


   ![Percorso libreria client](/help/forms/using/assets/adaptiveform.theme.easel.png)

#### 4. Distribuire il tema in un ambiente locale {#deploy-the-theme-on-a-local-environment}

Per distribuire il tema nell’ambiente di sviluppo o di test locale, effettua le seguenti operazioni:

1. Copia la libreria client, creata nella sezione precedente, nel progetto Archetipo, nel percorso seguente:

   `/ui.apps/src/main/content/jcr_root/apps/[AEM Archetype Project Folder]/clientlibs/<yourtheme>`

1. Aprire il prompt dei comandi o il terminale.
1. Passa alla directory principale del progetto Archetipo AEM, il progetto utilizzato per abilitare i componenti core del modulo adattivo.
1. Esegui il comando seguente per distribuire il tema personalizzato nel tuo ambiente:

   `mvn clean install`

   ![Build libreria client](/help/forms/using/assets/mvndeploy.png)

<!--

#### 5. Test the theme with a local Adaptive Form {#test-the-theme-with-a-local-adaptive-form}

To apply and test the customized theme with an Adaptive Form:

**Apply theme while creating an Adaptive Form**

1. Log in to your AEM Forms author instance. 

1. Select **Adobe Experience Manager** > **Forms** > **Forms & Documents**.

1. Click **Create** > **Adaptive Forms**. The wizard for creating Adaptive Form opens.

1. Select the core component template in the **Source** tab.
1. Select the theme in the **Style** tab.
1. Click **Create**.

An Adaptive Form with the selected theme is created. 

**Apply theme to an existing Adaptive Form**

1. Log in to your AEM Forms author instance. 

1. Select **Adobe Experience Manager** > **Forms** > **Forms & Documents**.

1. Select an Adaptive Form and click Properties. 

1. For the **Theme Client Library** option, select the theme. 

1. Click **Save & Close**.

The selected theme is applied to the Adaptive Form. 
-->

#### 5. Distribuire un tema nell’ambiente di produzione {#deploy-theme}

Dopo aver testato correttamente il tema nell’ambiente di sviluppo locale, puoi procedere alla distribuzione del tema negli ambienti di produzione, incluse le istanze Author e Publish. Per distribuire il tema negli ambienti di produzione, effettua le seguenti operazioni:

1. Accedi all’ambiente AEM.
1. Apri Gestione pacchetti. URL predefinito: `https://localhost:4502/crx/packmgr/index.jsp`.
1. Fare clic su **Carica pacchetto** e quindi su **Sfoglia**.
1. Passare a `[AEM Archetype Project Folder]\all\target[appid].all-[version].zip` e selezionarlo. Fai clic su **Apri**.
1. Fai clic su Installa. Ripeti il passaggio in tutti gli ambienti di produzione.


Dopo l’installazione del pacchetto, il tema è disponibile per la selezione.

![Libreria client temi](/help/forms/using/assets/themeclientlibrary.png)

>[!NOTE]
>
>
> Se si verificano problemi durante l&#39;accesso alla finestra di dialogo di accesso in un&#39;istanza di pubblicazione per installare il pacchetto tramite Gestione pacchetti, provare ad accedere tramite il seguente URL: `http://[Publish Server URL]:[PORT]/system/console`. Questo consente di accedere all’istanza di Publish e di procedere con il processo di installazione.

## Applicare un tema a un modulo adattivo {#using-theme-in-adaptive-form}

I passaggi per applicare un tema a un modulo adattivo sono i seguenti:

1. Accedi all’istanza di authoring AEM locale.
1. Inserisci le credenziali nella pagina di accesso di Experience Manager. Seleziona **Adobe Experience Manager** > **Forms** > **Forms e documenti**.
1. Fai clic su **Crea** > **Forms adattivo**.
1. Seleziona un modello di Componenti core Forms adattivi e fai clic su **Avanti**. Viene visualizzato **Aggiungi proprietà**
1. Specifica il **Nome** per il modulo adattivo.


   >[!NOTE]
   >
   > * Per impostazione predefinita, il tema `adaptiveform.theme.canvas3` è selezionato.
   > * Puoi scegliere un tema diverso dal menu a discesa **Libreria client tema**.

1. Fai clic su **Crea**.

I temi per moduli adattivi vengono utilizzati come parte di un modello di modulo adattivo per definire lo stile durante la creazione di un modulo adattivo.

## Eliminare un tema {#delete-a-theme}

Per rimuovere i temi inutilizzati o indesiderati:

1. Accedi all’istanza di authoring.
1. Apri `http://[Publish Server URL]:[PORT]/crx/de/index.jsp`
1. Accedi a `apps/[AEM Archetype Project Folder]/clientlibs/[yourtheme]`.
1. Elimina la cartella dei temi e salva le modifiche.


## Domanda frequente {#faq}

**Q:** Quale personalizzazione ha priorità quando si eseguono personalizzazioni in una cartella dei temi a livello globale e di componente?

**Ans:** Quando uno stile viene definito sia a livello di tema che di componente, lo stile definito a livello di componente ha la precedenza.

**Q:** Quali passaggi è necessario eseguire se il tema personalizzato non è visibile nella **[!UICONTROL libreria client tema]**?

**Ans:** Se il tema personalizzato non viene visualizzato nel menu a discesa **[!UICONTROL Libreria client tema]**, eseguire la procedura seguente:

1. Passare alla posizione in cui è stata aggiunta la libreria client del tema personalizzata. Il percorso consigliato è `/ui.apps/src/main/content/jcr_root/apps[AEM Archetype Project Folder]/clientlibs/<yourtheme>`.

1. Aprire il file `.content.xml` e includere i metadati seguenti:

   ```
       formstheme:true
       allowproxy:true
   ```

1. Salva il file e ridistribuisci il tema.

## Consulta anche

* [Creare componenti core basati sul modulo adattivo](create-an-adaptive-form-core-components.md)
* [Utilizza l’editor di regole per aggiungere un comportamento dinamico al modulo](rule-editor.md)
* [Creazione o personalizzazione di temi per Forms adattivo basato su Componenti core](create-or-customize-themes-for-adaptive-forms-core-components.md)
* [Creazione di un modello per Forms adattivo basato su Componenti core](template-editor.md)
* [Creare o aggiungere un modulo adattivo a una pagina o a un frammento di esperienza di AEM Sites](create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [Modelli di temi di esempio e modelli di dati modulo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=it)
