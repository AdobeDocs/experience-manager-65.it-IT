---
title: assistenti vocali per moduli HTML5
seo-title: assistenti vocali per moduli HTML5
description: Elenca gli assistenti vocali supportati con i moduli HTML5.
seo-description: Elenca gli assistenti vocali supportati con i moduli HTML5.
uuid: 035354e2-957f-4eb6-bc16-4ca96ec7ac74
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 53c57180-7004-4534-9146-603f7770a6fe
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 1%

---


# Assistenti vocali per moduli HTML5 {#screen-readers-for-html-forms}

I componenti dei moduli HTML5 eseguono il rendering del modello di modulo XFA in un formato HTML5. Tutti i browser standard che supportano HTML5 possono eseguire il rendering di questi moduli. Per supportare un’esperienza di acquisizione dei dati simile nei moduli PDF e HTML5, il layout dei PDF forms viene mantenuto nei moduli HTML5.

I moduli HTML5 utilizzano costrutti HTML standard che consentono l’utilizzo di normali strumenti di accesso facilitato per l’HTML con questi moduli. Se un modulo è progettato in base alle best practice per i moduli con accesso facilitato, funziona con qualsiasi assistente vocale supportato. Inoltre, tali moduli sono abilitati per la navigazione da tastiera.

## Standard di accessibilità {#accessibility-standards}

I moduli HTML5 sono conformi alla sezione 508 per l’accessibilità con eccezioni note. Per ulteriori informazioni, vedere [VPAT for HTML5 forms](https://www.adobe.com/mena_en/accessibility/compliance/livecycle-mobile-forms-es4-section-508-vpat.html) .

## assistenti vocali certificati per moduli HTML5 {#certified-screen-readers-for-html-forms}

* JAWS 14.0 su Microsoft Windows
* VoiceOver su Mac OS X e iPad

### JAWS {#jaws}

Tutti i tasti di scelta rapida predefiniti funzionano per i moduli HTML5. Per ulteriori informazioni sull&#39;utilizzo di JAWS, visita [https://www.freedomscientific.com/jaws-hq.asp](https://www.freedomscientific.com/jaws-hq.asp).

### VoiceOver {#voiceover}

I moduli HTML5 supportano tutti i tasti e i gesti predefiniti di Voice over. Per ulteriori informazioni sull&#39;impostazione e l&#39;utilizzo di VoiceOver, vedere [https://www.apple.com/accessibility/voiceover/](https://www.apple.com/accessibility/voiceover/).

## Problemi noti {#known-issues}

* **(Solo per Internal Explorer 9)** Nei moduli HTML5, le pagine vengono caricate su richiesta (in modo dinamico). Il caricamento della pagina su richiesta causa problemi con il funzionamento degli assistenti vocali. Quando l’assistente vocale si trova sull’ultimo campo della pagina e l’utente preme il tasto Tab, anziché impostare lo stato attivo sul primo campo della pagina successiva, l’assistente vocale torna a essere attivo sul primo campo della prima pagina del modulo.
* **(Solo per Internal Explorer 9)** Il controllo Selezione data nei moduli HTML5 non è completamente accessibile tramite tastiera. Nel controllo Selettore data, se si premono più volte i tasti Su/Giù, il controllo Selettore data si chiude e lo stato attivo si sposta al campo successivo/ultimo.

* VoiceOver non è in grado di rilevare i tasti freccia sul widget data su iPad safari.
