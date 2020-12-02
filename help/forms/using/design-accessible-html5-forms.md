---
title: Progettazione di moduli HTML5 con accesso facilitato
seo-title: Progettazione di moduli HTML5 con accesso facilitato
description: I moduli HTML5 utilizzano lo standard di accessibilità ARIA HTML5. Questi moduli supportano la navigazione a schede e sono certificati compatibili con gli assistenti vocali comuni.
seo-description: I moduli HTML5 utilizzano lo standard di accessibilità ARIA HTML5. Questi moduli supportano la navigazione a schede e sono certificati compatibili con gli assistenti vocali comuni.
uuid: 1ce5ba39-69ea-4d0e-96ea-e2a38b21d6b7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 8711ad33-396b-4572-b2ee-71e9f45f4ebe
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 0%

---


# Progettazione di moduli HTML5 con accesso facilitato {#designing-accessible-html-forms}

I moduli HTML5 utilizzano lo standard di accessibilità ARIA HTML5 per generare moduli HTML con accesso facilitato. Questi moduli supportano la navigazione a schede (ad eccezione di Mozilla FireFox) e sono certificati compatibili con gli assistenti vocali comuni. Per generare un modulo HTML5 con buone funzioni di accessibilità, progettare il modello di modulo XFA in base ad alcune linee guida di progettazione di base. Le linee guida della progettazione includono la configurazione dell&#39;ordine di tabulazione corretto e la fornitura del contenuto di testo parlato per ciascun controllo modulo.  AEM Forms Designer supporta l&#39;impostazione di questi attributi di controllo per generare un modulo PDF e HTML5 accessibile.

*Nota: la navigazione a schede non copre i campi protetti, ad esempio i campi di calcolo che mostrano la somma dei valori. Affinché l&#39;assistente vocale possa leggere il valore di un campo protetto, posizionare un campo di sola lettura vuoto sopra o accanto al campo protetto. Assegnare il valore del campo protetto al nuovo campo di sola lettura. L&#39;assistente vocale o la navigazione a schede può selezionare questo campo di sola lettura e parlare come il valore del campo protetto.*

 AEM Forms Designer include una serie di opzioni di testo parlato che possono essere trasmesse agli assistenti vocali. Per ciascun oggetto di un modulo, l&#39;utente può specificare una delle diverse impostazioni per il testo dell&#39;assistente vocale:

* Testo personalizzato dell&#39;assistente vocale, che può essere impostato utilizzando la palette Accessibilità. Gli autori possono annotare i nomi dei pulsanti e dei campi, nonché la loro funzione.
* Descrizioni comandi, che possono essere impostate nella palette Accessibilità.
* Didascalie per i campi del modulo.
* Nomi degli oggetti, come specificato nell&#39;opzione Nome della scheda Binding.

![accessibilità](assets/accessibility.png)

Quando in un controllo Modulo sono disponibili più opzioni come la descrizione comandi, il testo dell&#39;Reader dello schermo e la didascalia, l&#39;Reader dello schermo utilizza solo una di queste proprietà. L’ordine predefinito è Testo personalizzato Reader schermo, descrizione comandi, didascalia e nome. È possibile ignorare l&#39;ordine predefinito utilizzando l&#39;opzione Reader schermo **Precedenza** nella palette Accessibilità.
