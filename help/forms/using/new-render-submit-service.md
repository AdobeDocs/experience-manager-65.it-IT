---
title: Nuovo servizio di rendering e invio
seo-title: New render and submit service
description: Definisci i servizi di rendering e invio in Workbench per eseguire il rendering del modulo XDP come HTML o PDF a seconda del dispositivo da cui si accede.
seo-description: Define render and submit services in Workbench to render XDP form as HTML or PDF depending on the device it is accessed from.
uuid: 7f8348a1-753c-4dab-87d5-4a4a301198dd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6a32d240-c6a6-4937-a31f-7a5ec3c60b1f
docset: aem65
exl-id: 46de0101-9607-4429-84c3-7c1f34d2da27
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 0%

---

# Nuovo servizio di rendering e invio{#new-render-and-submit-service}

## Introduzione {#introduction}

In Workbench, quando definisci un `AssignTask` specificare un modulo specifico (modulo XDP o PDF). Inoltre, specifica un set di servizi di rendering e invio tramite il profilo di azione.

È possibile eseguire il rendering di un file XDP come modulo PDF o HTML. Le nuove funzionalità includono la possibilità di:

* Eseguire il rendering e inviare un modulo XDP come HTML
* Eseguire il rendering e inviare un modulo XDP come PDF sul desktop e come HTML su dispositivi mobili (ad esempio, un iPad)

### Nuovo servizio HTML Forms {#new-html-forms-service}

Il nuovo servizio HTML Forms sfrutta la nuova funzione di Forms per supportare il rendering di moduli XDP come HTML. Il nuovo servizio HTML Forms espone i seguenti metodi:

```java
/*
 * Generates a URL (for the HTML Form) to be passed to client, given a TaskContext.
 * The output of this API is something like this - /lc/content/xfaforms/profiles/default.ws.html?ContentRoot=repository://Applications/MyApplication/MyFolder&template=MyForm.xdp
 * @param taskContext task context
 * @param profileName Forms servlet URL.
 * @return form URL string
 */
public String generateFormURL(TaskContext taskContext, String profileName);

/*
 * Render the XDP Form as HTML. Can be used directly for updating the runtimeMap in render.
 * It adds the following keys to the map -
 * hint:new html form = true
 * newHTMLFormURL = the URL returned after calling 'generateFormURL' API.
 * @param TaskContext taskContext
 * @param profileName Forms servlet URL.
 * @param runtimeMap runtime map<string,object> associated with form rendering.
 * return runtimeMap
 */
public Map<String, Object> renderHTMLForm (TaskContext taskContext, String profileName, Map<String,Object> runtimeMap);
```

Ulteriori informazioni sui profili dei moduli mobili sono disponibili all’indirizzo [Creazione di un profilo personalizzato](/help/forms/using/custom-profile.md).

## Nuovi processi di rendering e invio dei moduli di HTML {#new-html-form-render-amp-submit-processes}

Per ogni operazione &quot;AssignTask&quot;, specificare un processo Render e un processo Submit insieme al modulo. Questi processi vengono chiamati da TaskManager `renderForm`e `submitForm`API per consentire la gestione personalizzata. Semantiche di questi processi per il nuovo modulo HTML:

### Rendering di un nuovo modulo HTML {#render-a-new-html-form}

Il nuovo processo di rendering di HTML, come ogni processo di rendering, ha i seguenti parametri di I/O:

Input - `taskContext`

Output - `runtimeMap`

Output - `outFormDoc`

Questo metodo simula il comportamento esatto di `renderHTMLForm` API di NewHTMLFormsService. Chiama il `generateFormURL` API per ottenere l’URL per il rendering HTML del modulo. Quindi compila runtimeMap con la chiave o i valori seguenti:

nuovo modulo html = true

newHTMLFormURL = l&#39;URL restituito dopo la chiamata `generateFormURL` API.

### Invia un nuovo modulo HTML {#submit-a-new-html-form}

Questo processo per l’invio di un nuovo modulo HTML funziona con i seguenti parametri di I/O:

Input - `taskContext`

Output - `runtimeMap`

Output - `outputDocument`

Il processo imposta le `outputDocument`al `inputDocument`recuperato da `taskContext`.

## Processi di rendering o invio predefiniti e profili di azione {#default-render-or-submit-processes-and-action-profiles}

I servizi di rendering e invio predefiniti abilitano il supporto per il rendering di PDF su un desktop e HTML su dispositivi mobili (iPad).

### Modulo di rendering predefinito {#default-render-form}

Questo processo esegue il rendering di un modulo XDP su più piattaforme in modo semplice. Il processo recupera l&#39;agente utente da `taskContext`e utilizza i dati per chiamare il processo per eseguire il rendering di HTML o PDF.

![modulo di rendering predefinito](assets/default-render-form.png)

### Modulo di invio predefinito {#default-submit-form}

Questo processo consente di inviare un modulo XDP su più piattaforme senza soluzione di continuità. Recupera l&#39;agente utente da `taskContext`e utilizza i dati per chiamare il processo per inviare HTML o PDF.

![modulo di invio predefinito](assets/default-submit-form.png)

## Cambiare il rendering dei moduli per dispositivi mobili da PDF a HTML {#switch-the-rendering-of-mobile-forms-from-pdf-to-html}

I browser stanno gradualmente ritirando il supporto per i plug-in basati su NPAPI, inclusi i plug-in per Adobe Acrobat e Adobe Acrobat Reader. Per modificare il rendering dei moduli per dispositivi mobili da PDF a HTML, effettua le seguenti operazioni:

1. Accedi a Workbench come utente valido.
1. Seleziona **File** > **Ottieni applicazioni**.

   Viene visualizzata la finestra di dialogo Get Applications (Ottieni applicazioni).

1. Seleziona le applicazioni per le quali desideri modificare il rendering del modulo mobile e fai clic su **OK**.
1. Apri il processo di cui desideri modificare il rendering.
1. Apri il punto iniziale/attività di destinazione, passa alla sezione Presentazione e dati e fai clic su **Gestisci profili azioni**.

   Viene visualizzata la finestra di dialogo Gestisci profili azioni.
1. Modifica le configurazioni del profilo di rendering predefinito da PDF a HTML e fai clic su **OK**.
1. Controlla il processo.
1. Ripeti i passaggi per modificare il rendering per altri processi.
1. Distribuisci l&#39;applicazione pertinente ai processi modificati.

### Profilo azione predefinito {#default-action-profile}

Il profilo azione predefinito ha eseguito il rendering del modulo XDP come PDF. Questo comportamento è stato modificato in modo da utilizzare i processi Modulo di rendering predefinito e Modulo di invio predefinito.

Ecco alcune domande frequenti sui profili di azione:

![gen_query_b_20](assets/gen_question_b_20.png) **Quali processi di rendering/invio saranno disponibili?**

* Guida al rendering (le guide sono obsolete)
* Guida al modulo di rendering
* Modulo di rendering PDF
* Modulo di rendering HTML
* Rendering nuovo modulo HTML (nuovo)
* Modulo di rendering predefinito (nuovo)

E, processi di invio equivalenti.

![gen_query_b_20](assets/gen_question_b_20.png) **Quali profili di azione sono disponibili?**

Per XDP Forms:

* Predefinito (rendering/invio tramite i nuovi processi &quot;Default Render/Submit&quot;)

![gen_query_b_20](assets/gen_question_b_20.png) **Cosa deve essere fatto dal designer del processo per consentire il rendering del modulo in HTML su un dispositivo e in PDF su un desktop?**

Niente. Il profilo azione predefinito viene scelto automaticamente e anche la modalità di rendering viene gestita automaticamente.

![gen_query_b_20](assets/gen_question_b_20.png) **Cosa è necessario fare per abilitare il rendering del modulo in HTML su un desktop?**

L’utente deve selezionare il pulsante di scelta HTML per il profilo predefinito.

![gen_query_b_20](assets/gen_question_b_20.png) **Ci sarà un impatto di aggiornamento sulla modifica del comportamento del profilo di azione predefinito?**

Sì, poiché i servizi di rendering e invio precedenti associati al profilo di azione predefinito erano diversi, questi vengono trattati come una personalizzazione dei moduli esistenti. Al clic **Ripristina valori predefiniti**, vengono invece impostati i servizi di rendering e invio predefiniti.

Se hai modificato i servizi Render o Submit PDF Form esistenti o creato servizi personalizzati (ad esempio personalizzati1) e ora desideri utilizzare la stessa funzionalità per il rendering di HTML. È necessario replicare il nuovo servizio di rendering o invio (come ad esempio custom2) e applicare personalizzazioni simili a quelle. Ora, modifica il profilo di azione per il tuo XDP per iniziare a utilizzare i servizi personalizzati2, invece di custom1 per il rendering o l’invio.

Cosa deve essere fatto dal designer del processo per consentire il rendering del modulo in HTML su un dispositivo e in PDF su un desktop?
Cosa deve essere fatto dal designer del processo per consentire il rendering del modulo in HTML su un dispositivo e in PDF su un desktop?
