---
title: Nuovo servizio di rendering e invio
description: Definisci i servizi di rendering e invio in Workbench per eseguire il rendering del modulo XDP come HTML o PDF a seconda del dispositivo da cui è accessibile.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 46de0101-9607-4429-84c3-7c1f34d2da27
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 0%

---

# Nuovo servizio di rendering e invio{#new-render-and-submit-service}

## Introduzione {#introduction}

In Workbench, quando definisci un’ `AssignTask` specifica un modulo specifico (XDP o PDF). Inoltre, specifica un set di servizi di rendering e invio tramite il profilo di azione.

È possibile eseguire il rendering di un XDP come modulo PDF o modulo HTML. Le nuove funzionalità includono la possibilità di:

* Rendering e invio di un modulo XDP come HTML
* Eseguire il rendering e inviare un modulo XDP come PDF su desktop e come HTML su dispositivi mobili (ad esempio, un iPad)

### Nuovo servizio HTML Forms {#new-html-forms-service}

Il nuovo servizio HTML Forms utilizza la nuova funzione di Forms per supportare il rendering del modulo XDP come HTML. Il nuovo servizio HTML Forms espone i seguenti metodi:

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

Ulteriori informazioni sui profili dei moduli per dispositivi mobili sono disponibili all’indirizzo [Creazione di un profilo personalizzato](/help/forms/using/custom-profile.md).

## Nuovi processi di rendering e invio di moduli HTML {#new-html-form-render-amp-submit-processes}

Per ogni operazione &#39;AssignTask&#39;, specificare un processo di rendering e un processo di invio con il modulo. Questi processi vengono chiamati da TaskManager `renderForm`e `submitForm`API per consentire la gestione personalizzata. Semantica di questi processi per il nuovo modulo HTML:

### Rendering di un nuovo modulo HTML {#render-a-new-html-form}

Il nuovo processo di rendering di HTML, come ogni processo di rendering, ha i seguenti parametri I/O:

Input - `taskContext`

Output - `runtimeMap`

Output - `outFormDoc`

Questo metodo simula il comportamento esatto di `renderHTMLForm` API di NewHTMLFormsService. Chiama il `generateFormURL` API per ottenere l’URL per la rappresentazione HTML del modulo. Quindi popola la mappa di runtime con la chiave o i valori seguenti:

nuovo modulo html = true

newHTMLFormURL = URL restituito dopo la chiamata `generateFormURL` API.

### Invia un nuovo modulo HTML {#submit-a-new-html-form}

Questo processo per inviare un nuovo modulo HTML funziona con i seguenti parametri di I/O:

Input - `taskContext`

Output - `runtimeMap`

Output - `outputDocument`

Il processo imposta `outputDocument`al `inputDocument`recuperato da `taskContext`.

## Processi predefiniti di rendering o invio e profili di azione {#default-render-or-submit-processes-and-action-profiles}

I servizi predefiniti di rendering e invio consentono di eseguire il rendering dei PDF su un desktop e di HTML su dispositivi mobili (iPad).

### Modulo di rendering predefinito {#default-render-form}

Questo processo esegue il rendering di un modulo XDP su più piattaforme in modo semplice. Il processo recupera l’agente utente da `taskContext`, e utilizza i dati per richiamare il processo per eseguire il rendering di HTML o PDF.

![default-render-form](assets/default-render-form.png)

### Modulo di invio predefinito {#default-submit-form}

Questo processo invia senza problemi un modulo XDP su più piattaforme. Recupera l’agente utente da `taskContext`e utilizza i dati per richiamare il processo per inviare HTML o PDF.

![default-submit-form](assets/default-submit-form.png)

## Passare dal rendering di moduli mobili da PDF a HTML {#switch-the-rendering-of-mobile-forms-from-pdf-to-html}

I browser stanno gradualmente ritirando il supporto per i plug-in basati su NPAPI, inclusi i plug-in per Adobe Acrobat e Adobe Acrobat Reader. Per cambiare il rendering dei moduli mobili da PDF a HTML, procedi come segue:

1. Accedi a Workbench come utente valido.
1. Seleziona **File** > **Ottieni applicazioni**.

   Viene visualizzata la finestra di dialogo Ottieni applicazioni.

1. Seleziona le applicazioni per le quali vuoi modificare il rendering dei moduli mobili e fai clic su **OK**.
1. Aprire il processo per il quale si desidera modificare il rendering.
1. Apri il punto d’inizio/l’attività target, passa alla sezione Presentazione e dati e fai clic su **Gestisci profili azione**.

   Viene visualizzata la finestra di dialogo Gestisci profili azione.
1. Cambia le configurazioni del profilo di rendering predefinito da PDF a HTML e fai clic su **OK**.
1. Archivia il processo.
1. Ripeti i passaggi per modificare il rendering per altri processi.
1. Distribuire l&#39;applicazione pertinente ai processi modificati.

### Profilo azione predefinito {#default-action-profile}

Il profilo azione predefinito ha eseguito il rendering del modulo XDP come PDF. Questo comportamento è stato modificato per utilizzare i processi Modulo di rendering predefinito e Modulo di invio predefinito.

Di seguito sono riportate alcune domande frequenti sui profili di azione:

![gen_question_b_20](assets/gen_question_b_20.png) **Quali processi di rendering/invio saranno disponibili come predefiniti?**

* Guida al rendering (Guide è obsoleto)
* Guida al rendering dei moduli
* Rendering modulo PDF
* Rendering modulo HTML
* Rendering nuovo modulo HTML (nuovo)
* Modulo di rendering predefinito (nuovo)

Processi di invio equivalenti.

![gen_question_b_20](assets/gen_question_b_20.png) **Quali profili di azione saranno disponibili come predefiniti?**

Per XDP Forms:

* Predefinito (rendering/invio con i nuovi processi di rendering/invio predefiniti)

![gen_question_b_20](assets/gen_question_b_20.png) **Cosa deve fare il progettista per consentire il rendering del modulo in HTML su un dispositivo e in PDF su un desktop?**

Niente. Il profilo di azione predefinito viene scelto automaticamente e viene gestita automaticamente anche la modalità di rendering.

![gen_question_b_20](assets/gen_question_b_20.png) **Cosa è necessario fare per abilitare il rendering del modulo in HTML su un desktop?**

L’utente deve selezionare il pulsante di opzione HTML per il profilo predefinito.

![gen_question_b_20](assets/gen_question_b_20.png) **L’aggiornamento influirà sulla modifica del comportamento predefinito del profilo di azione?**

Sì, poiché i precedenti servizi di rendering e invio associati al profilo di azione predefinito erano diversi, vengono trattati come una personalizzazione dei moduli esistenti. Al clic **Ripristina valori predefiniti**, vengono invece impostati i servizi predefiniti di rendering e invio.

Se hai modificato i servizi esistenti di Rendering o Invia modulo PDF o hai creato servizi personalizzati (ad esempio, personalizzato1) e ora desideri utilizzare la stessa funzionalità per il rendering HTML. È necessario replicare il nuovo servizio di rendering o invio (ad esempio, personalizzato2) e applicare personalizzazioni simili a tali servizi. Ora, modifica il profilo dell’azione per XDP in modo che inizi a utilizzare i servizi custom2, invece di custom1 per il rendering o l’invio.

Cosa deve fare il progettista per consentire il rendering del modulo in HTML su un dispositivo e in PDF su un desktop?
Cosa deve fare il progettista per consentire il rendering del modulo in HTML su un dispositivo e in PDF su un desktop?
