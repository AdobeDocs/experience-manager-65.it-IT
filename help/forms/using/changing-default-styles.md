---
title: Modifica degli stili predefiniti dei moduli HTML5
seo-title: Modifica degli stili predefiniti dei moduli HTML5
description: Lo stile dei moduli HTML5 è basato su CSS. È possibile modificare gli stili predefiniti del modulo.
seo-description: Lo stile dei moduli HTML5 è basato su CSS. È possibile modificare gli stili predefiniti del modulo.
uuid: 5e23237d-42d8-4d29-b79e-4dc276ef65ff
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 582b0fe8-a92b-4a1d-b859-57f13f53d0d8
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---


# Modifica degli stili predefiniti dei moduli HTML5{#changing-default-styles-of-html-forms}

Il rendering dei moduli HTML5 viene eseguito utilizzando le funzionalità HTML5 e lo stile del modulo di cui è stato effettuato il rendering viene applicato tramite CSS. L&#39;aspetto predefinito di un modulo HTML5 è simile alla rappresentazione PDF. Gli sviluppatori possono utilizzare CSS personalizzato per modificare l&#39;aspetto predefinito dei moduli HTML5.

Questo articolo fornisce informazioni dettagliate sulla modifica dello stile di un modulo HTML5 e l&#39;articolo [Introduzione agli stili](/help/forms/using/css-styles.md) contiene informazioni dettagliate sui vari aspetti degli stili dei moduli HTML5. Prima di eseguire i passaggi indicati in questo articolo, leggete Introduzione agli stili.

Le due immagini seguenti mostrano la differenza tra gli stili predefiniti e personalizzati.

![picture-002-small](assets/pictures-002-small.png)

## Stile dei moduli {#style-your-forms}

1. **Scegliere un profilo per aggiungere stili personalizzati**

   Accedete all&#39;interfaccia CRX DE all&#39;URL: **https://&lt;server>:&lt;porta>/crx/de** e crea un profilo o scegli un profilo esistente. Per informazioni su come creare un profilo, vedere [Creazione di un nuovo profilo](/help/forms/using/custom-profile.md)

1. **Creare un foglio di stile CSS per la formattazione dei moduli HTML5**

   Passare alla cartella in cui è stato creato il renderer del profilo e creare un file foglio di stile CSS. I passaggi da seguire sono:

   1. Fare clic con il pulsante destro del mouse sulla cartella e selezionare **create** > **create File** dal menu

   1. Nella finestra di dialogo Crea file, immettere il nome del foglio di stile. Accertatevi di utilizzare l&#39;estensione .css (ad esempio, stylesheet.css)
   1. Dal riquadro di navigazione, aprite il file CSS creato.
   1. Definire le classi CSS dei componenti che si desidera personalizzare e aggiungere stili in tali classi.

   Per sapere quali classi CSS creare per un particolare componente nei moduli HTML5, vedere [Introduzione agli stili](/help/forms/using/css-styles.md).

1. **Includi il foglio di stile nel renderer del profilo**

   Aprite la pagina Profile Renderer (file jsp) in CRX DE e includete il file CSS nella pagina immediatamente sotto la libreria client XFA. Effettuate le seguenti operazioni per includere il file CSS nel profilo.

   1. Nella pagina del renderer, cercate la riga seguente:

      &lt;cq:includeclientlib categories=&quot;xfaforms.profile&quot; />

   1. Inserire quanto segue sotto la riga sopra per includere il foglio di stile:

      &lt;link href=&quot;/path/to/stylesheet&quot; rel=&quot;stylesheet&quot; type=&quot;text/css&quot; />

   1. Salvate il file.
