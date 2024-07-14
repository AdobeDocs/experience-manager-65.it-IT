---
title: Lettori di schermi per moduli HTML5
description: Elenca gli assistenti vocali supportati con i moduli HTML5.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 53c57180-7004-4534-9146-603f7770a6fe
feature: HTML5 Forms,Mobile Forms
exl-id: 07d20c2f-7d13-48ac-8d58-b367eb194558
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# Lettori di schermi per moduli HTML5 {#screen-readers-for-html-forms}

I componenti dei moduli HTML5 eseguono il rendering del modello di modulo XFA in un formato HTML5. Tutti i browser standard che supportano HTML5 possono eseguire il rendering di questi moduli. Per supportare un’esperienza di acquisizione dati simile nei moduli PDF e HTML5, il layout dei PDF forms viene mantenuto nei moduli HTML5.

I moduli HTML5 utilizzano costrutti HTML standard che consentono di utilizzare con questi moduli strumenti di accessibilità regolari per HTML. Se un modulo è progettato in base alle best practice per i moduli accessibili, funziona con qualsiasi assistente vocale supportato. Inoltre, tali moduli sono abilitati per la navigazione da tastiera.

## Standard di accessibilità {#accessibility-standards}

I moduli HTML5 sono conformi alla sezione 508 per l’accessibilità, con eccezioni note. Per ulteriori informazioni, vedere [VPAT per i moduli HTML5](https://www.adobe.com/content/dam/cc1/en/accessibility/compliance/pdfs/adobe-livecycle-es4-section-508-vpat-portfolio.pdf).

## Lettori di schermate certificati per moduli HTML5 {#certified-screen-readers-for-html-forms}

* JAWS 14.0 su Microsoft® Windows
* VoiceOver su macOS X e iPad

### MASCELLE {#jaws}

Tutte le sequenze di tasti e le scelte rapide predefinite funzionano per i moduli di HTML5. Per ulteriori informazioni sull&#39;utilizzo di JAWS, visitare [https://www.freedomscientific.com/jaws-hq.asp](https://www.freedomscientific.com/jaws-hq.asp).

### VoiceOver {#voiceover}

I moduli di HTML5 supportano tutte le pressioni di tasti e i gesti predefiniti di Voice over. Per ulteriori informazioni sulla configurazione e l&#39;utilizzo di VoiceOver, vedere [https://www.apple.com/accessibility/vision/](https://www.apple.com/accessibility/vision/).

## Problemi noti {#known-issues}

* **(solo per Internal Explorer 9)** Nei moduli HTML5, le pagine vengono caricate su richiesta (in modo dinamico). Il caricamento della pagina su richiesta causa problemi con il funzionamento degli assistenti vocali. Quando lo stato attivo dell’assistente vocale si trova sull’ultimo campo della pagina e l’utente preme la scheda, l’assistente vocale ritorna attivo sul primo campo della prima pagina del modulo.
* **(solo per Internal Explorer 9)** Il controllo Selezione data nei moduli di HTML5 non è completamente accessibile tramite tastiera. Nel controllo Selezione data, se si premono più volte i tasti Su/Giù, il controllo Selezione data viene chiuso e lo stato attivo viene spostato sul campo successivo/ultimo.

* VoiceOver non è in grado di rilevare i tasti freccia sul widget della data su iPad safari.
