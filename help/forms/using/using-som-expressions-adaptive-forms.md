---
title: Utilizzo di espressioni SOM nei moduli adattivi
seo-title: Utilizzo di espressioni SOM nei moduli adattivi
description: Scoprite come estrarre le espressioni SOM da un pannello di un modulo adattivo.
seo-description: Scoprite come estrarre le espressioni SOM da un pannello di un modulo adattivo.
uuid: c5d55aff-fb69-4a1c-96ea-fb3f9322cbb0
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 13f00bb2-561f-4d64-8829-292c663abeab
docset: aem65
translation-type: tm+mt
source-git-commit: e5c2385c29e2d20d453e2d1496f7d459d1c55876
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---


# Utilizzo di espressioni SOM nei moduli adattivi{#using-som-expressions-in-adaptive-forms}

I moduli adattivi sono modellati come AEM pagina, rappresentata come struttura di contenuto JCR AEM repository. L&#39;elemento chiave della struttura del contenuto è il nodo guideContainer. Sotto guideContainer, è presente rootPanel che può contenere pannelli e campi nidificati.

È possibile utilizzare un modello di oggetto script (SOM) per fare riferimento a valori, proprietà e metodi all&#39;interno di un particolare modello di oggetto documento (DOM). Un DOM organizza gli oggetti di memoria e le proprietà in una gerarchia ad albero. Un&#39;espressione SOM fa riferimento a Campi/Disegno di elementi e pannelli.

Nell&#39;immagine seguente è illustrata una struttura di nodi a cui un modulo adattivo si traduce quando si aggiungono componenti a un modulo. Ad esempio, potete aggiungere un pannello al pannello principale e un pulsante di scelta nel pannello che viene trasformato in DOM in fase di esecuzione. L&#39;espressione SOM per il campo del pulsante di scelta in un modulo adattivo è specificata come `guide[0].guide1[0].guideRootPanel[0].panel1[0].radiobutton[0]`.

![Struttura DOM](assets/hierarchy.png)

Struttura DOM

Un&#39;espressione SOM per qualsiasi elemento in un modulo adattivo ha il prefisso `guide[0].guide1[0]`. La posizione di un componente nella gerarchia della struttura del nodo viene utilizzata per derivare la relativa espressione SOM.

![Struttura DOM con due pulsanti di scelta](assets/hierarchy_radio_button.png)

Struttura DOM con due pulsanti di scelta

L&#39;espressione SOM cambia quando si modifica la posizione dei pulsanti di scelta nel modulo adattivo. In modalità di authoring, è possibile visualizzare l&#39;espressione SOM di un campo o di un elemento in  AEM Forms utilizzando l&#39;opzione Visualizza espressione SOM. L’opzione viene visualizzata nel pannello e quando fate clic con il pulsante destro del mouse sul campo o sull’elemento.

![Estrazione di espressioni SOM in un modulo adattivo](assets/som-expressions.png)

Estrazione di espressioni SOM in un modulo adattivo

All’interno dei pannelli, potete accedere alla funzione dalla barra degli strumenti del pannello. Questa funzione facilita la creazione di script da parte di autori di moduli adattivi.

![Estrazione di espressioni SOM tramite la barra degli strumenti del pannello](assets/som-expression.png)

Estrazione di espressioni SOM tramite la barra degli strumenti del pannello

Alcune API elencate in [GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html) utilizzano l&#39;espressione SOM di un elemento. Ad esempio, per rendere attivo un particolare campo in un modulo adattivo, passare l&#39;espressione SOM corrispondente all&#39; `getFocus`API in `guideBridge`.
