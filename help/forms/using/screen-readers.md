---
title: Assistente vocale per moduli HTML5
description: Elenca gli assistenti vocali supportati con i moduli HTML5.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 53c57180-7004-4534-9146-603f7770a6fe
feature: HTML5 Forms,Mobile Forms
exl-id: 07d20c2f-7d13-48ac-8d58-b367eb194558
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 3%
---
# Assistente vocale per moduli HTML5 {#screen-readers-for-html-forms}

I componenti dei moduli HTML5 eseguono il rendering del modello di modulo XFA in un formato HTML5. Tutti i browser standard che supportano HTML5 possono eseguire il rendering di questi moduli. Per supportare un’esperienza di acquisizione dati simile nei moduli PDF e HTML5, il layout di PDF forms viene mantenuto nei moduli HTML5.

I moduli HTML5 utilizzano costrutti HTML standard che consentono di utilizzare con questi moduli strumenti di accessibilità standard per HTML. Se un modulo è progettato in base alle best practice per i moduli accessibili, funziona con qualsiasi assistente vocale supportato. Inoltre, tali moduli sono abilitati per la navigazione da tastiera.

## Standard di accessibilità {#accessibility-standards}

I moduli HTML5 sono conformi alla sezione 508 per l’accessibilità, con eccezioni note. Per informazioni dettagliate, vedere [VPAT per HTML5 forms](https://www.adobe.com/content/dam/cc1/en/accessibility/compliance/pdfs/adobe-livecycle-es4-section-508-vpat-portfolio.pdf).

## Lettori di schermate certificati per HTML5 Forms {#certified-screen-readers-for-html-forms}

* JAWS 14.0 su Microsoft® Windows
* VoiceOver su macOS X e iPad

### MASCELLE {#jaws}

Tutte le sequenze di tasti e le scelte rapide predefinite funzionano per i moduli di HTML5. Per ulteriori informazioni sull&#39;utilizzo di JAWS, visitare [https://www.freedomscientific.com/jaws-hq.asp](https://www.freedomscientific.com/jaws-hq.asp).

### VoiceOver {#voiceover}

I moduli HTML5 supportano tutte le pressioni di tasti e i gesti predefiniti di Voice over. Per ulteriori informazioni sulla configurazione e l&#39;utilizzo di VoiceOver, vedere [https://www.apple.com/accessibility/vision/](https://www.apple.com/accessibility/vision/).

## Problemi noti {#known-issues}

* **(solo per Internal Explorer 9)** Nei moduli di HTML5, le pagine vengono caricate su richiesta (in modo dinamico). Il caricamento della pagina su richiesta causa problemi con il funzionamento degli assistenti vocali. Quando lo stato attivo dell’assistente vocale si trova sull’ultimo campo della pagina e l’utente preme la scheda, l’assistente vocale ritorna attivo sul primo campo della prima pagina del modulo.
* **(solo per Internal Explorer 9)** Il controllo Selezione data nei moduli di HTML5 non è completamente accessibile tramite tastiera. Nel controllo Selezione data, se si premono più volte i tasti Su/Giù, il controllo Selezione data viene chiuso e lo stato attivo viene spostato sul campo successivo/ultimo.

* VoiceOver non è in grado di rilevare i tasti freccia sul widget della data su iPad safari.
