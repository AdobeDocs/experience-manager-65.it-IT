---
title: Progettazione di moduli HTML5 con accesso facilitato
seo-title: Designing accessible HTML5 forms
description: I moduli di HTML5 utilizzano lo standard di accessibilità di ARIA HTML5. Questi moduli supportano la navigazione a schede e sono certificati compatibili con gli assistenti vocali comuni.
seo-description: HTML5 forms use the ARIA HTML5 accessibility standard. These forms support tabbed navigation and are certified to be compatible with common screen readers.
uuid: 1ce5ba39-69ea-4d0e-96ea-e2a38b21d6b7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 8711ad33-396b-4572-b2ee-71e9f45f4ebe
docset: aem65
feature: Mobile Forms
exl-id: fca2f9b2-11a2-4db0-a370-c4046f32be63
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---

# Progettazione di moduli HTML5 con accesso facilitato {#designing-accessible-html-forms}

I moduli di HTML5 utilizzano lo standard di accessibilità di ARIA HTML5 per generare moduli HTML accessibili. Questi moduli supportano la navigazione a schede (ad eccezione di Mozilla FireFox) e sono certificati compatibili con gli assistenti vocali comuni. Per generare un modulo HTML5 con buone funzioni di accesso facilitato, progettare il modello di modulo XFA in base ad alcune linee guida di progettazione di base. Le linee guida di progettazione includono la configurazione dell’ordine di tabulazione corretto e la fornitura del contenuto di testo parlato per ciascun controllo del modulo. AEM Forms Designer supporta l’impostazione di questi attributi di controllo del modulo per generare un modulo Accessible PDF e HTML5.

*Nota:la navigazione a schede non include campi protetti, ad esempio campi di calcolo che visualizzano la somma dei valori. Per consentire all’assistente vocale di leggere il valore di un campo protetto, posizionare un campo di sola lettura vuoto sopra o accanto al campo protetto. Assegnare il valore del campo protetto al nuovo campo di sola lettura. L’assistente vocale o la navigazione a schede possono scegliere questo campo di sola lettura e parlare il valore del campo protetto.*

AEM Forms Designer include diverse opzioni di testo parlato che possono essere passate agli assistenti vocali. Per ciascun oggetto di un modulo, l’utente può specificare una delle diverse impostazioni per il testo dell’assistente vocale:

* Testo personalizzato dell’assistente vocale, che può essere impostato utilizzando la palette Accessibilità. Gli autori possono annotare i nomi dei pulsanti e dei campi e il loro scopo.
* Le descrizioni comandi possono essere impostate nella palette Accessibilità.
* Sottotitoli per i campi del modulo.
* Nomi degli oggetti, come specificato nell’opzione Nome della scheda Binding.

![accessibilità](assets/accessibility.png)

Quando in un controllo Form sono disponibili più opzioni quali la descrizione comandi, il testo del Reader dello schermo e la didascalia, il Reader dello schermo utilizza solo una di queste proprietà. L’ordine predefinito è Testo personalizzato Reader schermo, descrizione comandi, Didascalia e Nome. È possibile ignorare l’ordine predefinito utilizzando il Reader Schermo **Precedenza** nella palette Accessibilità.
