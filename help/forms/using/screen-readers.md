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
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# assistenti vocali per moduli HTML5 {#screen-readers-for-html-forms}

I componenti per moduli HTML5 eseguono il rendering del modello di modulo XFA in un formato HTML5. Tutti i browser standard che supportano HTML5 possono eseguire il rendering di questi moduli. Per consentire un&#39;esperienza di acquisizione dei dati simile nei moduli PDF e HTML5, il layout dei moduli PDF viene mantenuto nei moduli HTML5.

I moduli HTML5 utilizzano costrutti HTML standard che consentono di utilizzare con tali moduli normali strumenti di accesso facilitato per HTML. Se un modulo è progettato in base alle procedure ottimali per i moduli con accesso facilitato, funziona con qualsiasi assistente vocale supportato. Inoltre, tali moduli sono abilitati per la navigazione tramite tastiera.

## Standard di accessibilità {#accessibility-standards}

I moduli HTML5 sono conformi alla sezione 508 per l’accessibilità, con eccezioni note. Per informazioni dettagliate, vedere [VPAT per i moduli](https://www.adobe.com/mena_en/accessibility/compliance/livecycle-mobile-forms-es4-section-508-vpat.html) HTML5.

## assistenti vocali certificati per moduli HTML5 {#certified-screen-readers-for-html-forms}

* JAWS 14.0 in Microsoft Windows
* VoiceOver su Mac OS X e iPad

### JAWS {#jaws}

Tutti i tasti e i collegamenti predefiniti funzionano per i moduli HTML5. Per ulteriori informazioni sull&#39;utilizzo di JAWS, visitate [https://www.freedomscientific.com/jaws-hq.asp](https://www.freedomscientific.com/jaws-hq.asp).

### VoiceOver {#voiceover}

I moduli HTML5 supportano tutti i tasti e i gesti predefiniti di Voice over. Per ulteriori informazioni sulla configurazione e l’uso di VoiceOver, vedete [https://www.apple.com/accessibility/voiceover/](https://www.apple.com/accessibility/voiceover/).

## Problemi noti {#known-issues}

* **(Solo Internal Explorer 9)** Nei moduli HTML5 le pagine vengono caricate su richiesta (in modo dinamico). Il caricamento su richiesta della pagina causa problemi con il funzionamento degli assistenti vocali. Quando l&#39;assistente vocale è attivo sull&#39;ultimo campo della pagina e l&#39;utente preme il tasto Tab, anziché impostare lo stato attivo sul primo campo della pagina successiva, l&#39;assistente vocale torna a essere attivo sul primo campo della prima pagina del modulo.
* **(Solo Internal Explorer 9)** Il controllo del selettore data nei moduli HTML5 non è completamente accessibile tramite tastiera. Nel controllo Selettore data, se si premono più volte i tasti Su/Giù, il controllo Selettore data si chiude e lo stato attivo si sposta sul campo Successivo/Ultimo.

* VoiceOver non è in grado di rilevare i tasti freccia sul widget data sul Safari iPad.

**[Contattare il supporto](https://www.adobe.com/account/sign-in.supportportal.html)**
