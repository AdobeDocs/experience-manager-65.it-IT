---
title: Nuovo servizio di rendering e invio
seo-title: Nuovo servizio di rendering e invio
description: In Workbench è possibile definire i servizi di rendering e invio per eseguire il rendering del modulo XDP come HTML o PDF a seconda del dispositivo di accesso.
seo-description: In Workbench è possibile definire i servizi di rendering e invio per eseguire il rendering del modulo XDP come HTML o PDF a seconda del dispositivo di accesso.
uuid: 7f8348a1-753c-4dab-87d5-4a4a301198dd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6a32d240-c6a6-4937-a31f-7a5ec3c60b1f
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 0%

---


# Nuovo servizio di rendering e invio{#new-render-and-submit-service}

## Introduzione {#introduction}

In Workbench, quando si definisce un&#39;operazione `AssignTask`, specificare un modulo specifico (modulo XDP o PDF). Inoltre, specificate un set di servizi di rendering e invio tramite il profilo azione.

È possibile eseguire il rendering di un file XDP come modulo PDF o HTML. Le nuove funzionalità includono la possibilità di:

* Eseguire il rendering e inviare un modulo XDP come HTML
* Eseguire il rendering e inviare un modulo XDP come PDF sul desktop e come HTML su dispositivi mobili (ad esempio, un iPad)

### Nuovo servizio Forms HTML {#new-html-forms-service}

Il nuovo servizio Forms HTML sfrutta la nuova funzione di Forms per supportare il rendering del modulo XDP come HTML. Il nuovo servizio HTML Forms espone i seguenti metodi:

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

Per ulteriori informazioni sui profili dei moduli per dispositivi mobili, vedere [Creazione di un profilo personalizzato](/help/forms/using/custom-profile.md).

## Nuovi processi di rendering e invio dei moduli HTML {#new-html-form-render-amp-submit-processes}

Per ogni operazione &#39;AssignTask&#39;, specificare un rendering e un processo di invio con il modulo. Tali processi vengono chiamati da TaskManager `renderForm`e `submitForm`API per consentire la gestione personalizzata. Semantica di questi processi per il nuovo modulo HTML:

### Eseguire il rendering di un nuovo modulo HTML {#render-a-new-html-form}

Il nuovo processo di rendering HTML, come ogni processo di rendering, presenta i seguenti parametri di I/O:

Input - `taskContext`

Output - `runtimeMap`

Output - `outFormDoc`

Questo metodo simula il comportamento esatto dell&#39;API `renderHTMLForm` di NewHTMLFormsService. Chiama l&#39;API `generateFormURL` per ottenere l&#39;URL per la rappresentazione HTML del modulo. Quindi compila runtimeMap con la chiave o i valori seguenti:

nuovo modulo HTML = true

newHTMLFormURL = l&#39;URL restituito dopo la chiamata dell&#39;API `generateFormURL`.

### Invia un nuovo modulo HTML {#submit-a-new-html-form}

Questo processo di invio di un nuovo modulo HTML funziona con i seguenti parametri di I/O:

Ingresso - `taskContext`

Output - `runtimeMap`

Output - `outputDocument`

Il processo imposta la `outputDocument`su `inputDocument`recuperata da `taskContext`.

## Processi di rendering o invio predefiniti e profili azione {#default-render-or-submit-processes-and-action-profiles}

I servizi di rendering e invio predefiniti supportano il rendering di PDF su computer desktop e di HTML su dispositivi mobili (iPad).

### Modulo di rendering predefinito {#default-render-form}

Questo processo esegue il rendering di un modulo XDP su più piattaforme senza soluzione di continuità. Il processo recupera l&#39;agente utente da `taskContext` e utilizza i dati per chiamare il processo per eseguire il rendering HTML o PDF.

![default-rendering-form](assets/default-render-form.png)

### Modulo di invio predefinito {#default-submit-form}

Questo processo consente di inviare un modulo XDP su più piattaforme senza problemi. Recupera l&#39;agente utente da `taskContext`e utilizza i dati per chiamare il processo per inviare HTML o PDF.

![default-submit-form](assets/default-submit-form.png)

## Conversione del rendering dei moduli per dispositivi mobili da PDF a HTML {#switch-the-rendering-of-mobile-forms-from-pdf-to-html}

I browser stanno gradualmente ritirando il supporto per i plug-in basati su NPAPI, inclusi i plug-in per  Adobe Acrobat e  Adobe Acrobat Reader. Per modificare il rendering dei moduli mobili da PDF a HTML, procedere come segue:

1. Accedere a Workbench come utente valido.
1. Selezionare **File** > **Get Applications**.

   Viene visualizzata la finestra di dialogo Acquisisci applicazioni.

1. Selezionare le applicazioni per le quali si desidera modificare il rendering del modulo mobile e fare clic su **OK**.
1. Aprite il processo per il quale desiderate modificare il rendering.
1. Aprite il punto di avvio/attività di destinazione, andate alla sezione Presentazione e dati e fate clic su **Gestisci profili azione**.

   Viene visualizzata la finestra di dialogo Gestisci profili azioni.
1. Modificate le configurazioni predefinite del profilo di rendering da PDF a HTML e fate clic su **OK**.
1. Eseguire il check-in del processo.
1. Ripetere i passaggi per modificare il rendering per altri processi.
1. Distribuire l&#39;applicazione relativa ai processi modificati.

### Profilo azione predefinito {#default-action-profile}

Il profilo azione predefinito ha rappresentato il modulo XDP come PDF. Questo comportamento è stato modificato per utilizzare i processi Modulo di rendering predefinito e Modulo di invio predefinito.

Seguono alcune domande frequenti sui profili di azione:

![gen_question_b_20](assets/gen_question_b_20.png) **Quali processi Render / Submit saranno disponibili?**

* Guida di rendering (guide non più utilizzate)
* Guida ai moduli di rendering
* Rendering del modulo PDF
* Rendering del modulo HTML
* Rendering nuovo modulo HTML (nuovo)
* Modulo di rendering predefinito (nuovo)

Inoltre, processi di invio equivalenti.

![gen_question_b_20](assets/gen_question_b_20.png) **Quali profili di azione saranno disponibili?**

Per Forms XDP:

* Valore predefinito (rendering/invio tramite i nuovi processi di rendering/invio predefiniti)

![gen_question_b_20](assets/gen_question_b_20.png) **Cosa deve essere fatto dal progettista di processi per consentire il rendering del modulo in HTML su un dispositivo e in PDF su un desktop?**

Niente. Il profilo azione predefinito viene scelto automaticamente e anche la modalità di rendering viene gestita automaticamente.

![gen_question_b_20](assets/gen_question_b_20.png) **Cosa è necessario fare per abilitare il rendering del modulo in HTML su un computer desktop?**

L&#39;utente deve selezionare il pulsante di scelta HTML per il profilo predefinito.

![gen_question_b_20](assets/gen_question_b_20.png) **Si verificherà un impatto di aggiornamento sulla modifica del comportamento del profilo di azione predefinito?**

Sì, poiché i servizi di rendering e invio precedenti associati al profilo di azione predefinito erano diversi, questi vengono trattati come una personalizzazione dei moduli esistenti. Facendo clic su **Ripristina predefiniti**, vengono impostati i servizi di rendering e invio predefiniti.

Se si sono modificati i servizi Render (Rendering) o Submit PDF Form esistenti o se sono stati creati servizi personalizzati (ad esempio, custom1), e si desidera utilizzare la stessa funzionalità per la rappresentazione HTML. È necessario replicare il nuovo servizio di rendering o di invio (come ad esempio custom2) e applicare a tali servizi personalizzazioni simili. A questo punto, modificate il profilo di azione per XDP in modo da iniziare a utilizzare i servizi personalizzati2, invece di custom1 per il rendering o l&#39;invio.

Cosa deve essere fatto dal progettista di processi per consentire il rendering del modulo in HTML su un dispositivo e in PDF su un desktop?
Cosa deve essere fatto dal progettista di processi per consentire il rendering del modulo in HTML su un dispositivo e in PDF su un desktop?
