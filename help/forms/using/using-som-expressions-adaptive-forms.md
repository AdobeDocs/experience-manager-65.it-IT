---
title: Utilizzo di espressioni SOM nei moduli adattivi
seo-title: Utilizzo di espressioni SOM nei moduli adattivi
description: Scopri come estrarre le espressioni SOM di un pannello di un modulo adattivo.
seo-description: Scopri come estrarre le espressioni SOM di un pannello di un modulo adattivo.
uuid: c5d55aff-fb69-4a1c-96ea-fb3f9322cbb0
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 13f00bb2-561f-4d64-8829-292c663abeab
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---


# Utilizzo di espressioni SOM nei moduli adattivi{#using-som-expressions-in-adaptive-forms}

I moduli adattivi sono modellati come pagina AEM rappresentata come struttura di contenuto JCR nell’archivio AEM. L’elemento chiave della struttura del contenuto è il nodo guideContainer . Sotto guideContainer, è presente rootPanel che può contenere pannelli e campi nidificati.

È possibile utilizzare un modello di oggetto script (SOM) per fare riferimento a valori, proprietà e metodi all&#39;interno di un particolare modello di oggetto documento (DOM). Un DOM organizza gli oggetti e le proprietà di memoria in una gerarchia ad albero. Un&#39;espressione SOM fa riferimento a Campi/Disegno ed elementi.

Nell’immagine seguente viene illustrata una struttura di nodo a cui un modulo adattivo si traduce quando si aggiungono componenti a un modulo. Ad esempio, puoi aggiungere un pannello al pannello principale e un pulsante di scelta nel pannello che viene trasformato in DOM in fase di esecuzione. L’espressione SOM per il campo pulsante di scelta nel modulo adattivo è specificata come `guide[0].guide1[0].guideRootPanel[0].panel1[0].radiobutton[0]`.

![Struttura DOM](assets/hierarchy.png)

Struttura DOM

Un&#39;espressione SOM per qualsiasi elemento in un modulo adattivo è preceduta da `guide[0].guide1[0]`. La posizione di un componente nella gerarchia della struttura del nodo viene utilizzata per derivare la relativa espressione SOM.

![Struttura DOM con due pulsanti di scelta](assets/hierarchy_radio_button.png)

Struttura DOM con due pulsanti di scelta

L’espressione SOM cambia quando si modifica la posizione dei pulsanti di scelta nel modulo adattivo. In modalità di authoring, è possibile visualizzare l’espressione SOM di un campo o di un elemento in AEM Forms utilizzando l’opzione Visualizza espressione SOM. L’opzione viene visualizzata nel pannello e quando fai clic con il pulsante destro del mouse sul campo o sull’elemento.

![Estrazione di espressioni SOM in un modulo adattivo](assets/som-expressions.png)

Estrazione di espressioni SOM in un modulo adattivo

All’interno dei pannelli, potete accedere alla funzione dalla barra degli strumenti del pannello. Questa funzione facilita la creazione di script da parte degli autori di moduli adattivi.

![Estrazione di espressioni SOM tramite la barra degli strumenti del pannello](assets/som-expression.png)

Estrazione di espressioni SOM tramite la barra degli strumenti del pannello

Alcune API elencate in [GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html) utilizzano l&#39;espressione SOM di un elemento. Ad esempio, per attivare un particolare campo in un modulo adattivo, passa l’espressione SOM corrispondente all’ `getFocus`API in `guideBridge`.
