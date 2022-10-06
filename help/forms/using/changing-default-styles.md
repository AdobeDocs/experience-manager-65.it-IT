---
title: Modifica degli stili predefiniti dei moduli di HTML5
seo-title: Changing default styles of HTML5 forms
description: Lo stile dei moduli di HTML5 è basato su CSS. È possibile modificare gli stili predefiniti del modulo.
seo-description: HTML5 forms styling is based on CSS. You can change the default styles of the form.
uuid: 5e23237d-42d8-4d29-b79e-4dc276ef65ff
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 582b0fe8-a92b-4a1d-b859-57f13f53d0d8
docset: aem65
feature: Mobile Forms
exl-id: 4c84cfd1-50a4-416f-b4a5-7f2f4c7f10af
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---

# Modifica degli stili predefiniti dei moduli di HTML5{#changing-default-styles-of-html-forms}

Il rendering dei moduli di HTML5 viene eseguito utilizzando le funzionalità di HTML5 e lo stile del modulo di cui è stato effettuato il rendering viene eseguito utilizzando i CSS. L’aspetto predefinito di un modulo HTML5 è simile al rendering di PDF. Gli sviluppatori possono utilizzare CSS personalizzati per modificare l’aspetto predefinito dei moduli di HTML5.

Questo articolo fornisce informazioni dettagliate per modificare lo stile di un modulo HTML5 e [Introduzione agli stili](/help/forms/using/css-styles.md) questo articolo contiene informazioni dettagliate su vari aspetti dello stile dei moduli HTML5. Assicurati di aver letto Introduzione agli stili prima di eseguire i passaggi menzionati in questo articolo.

Le due immagini seguenti mostrano la differenza tra gli stili predefiniti e personalizzati.

![picture-002-small](assets/pictures-002-small.png)

## Personalizzare lo stile dei moduli {#style-your-forms}

1. **Scegliere un profilo per aggiungere stili personalizzati**

   Accedi all&#39;interfaccia CRX DE all&#39;URL: **https://&lt;server>:&lt;port>/crx/de** e crea un profilo o scegli un profilo esistente. Per informazioni su come creare un profilo, consulta [Creazione di un nuovo profilo](/help/forms/using/custom-profile.md)

1. **Creare un foglio di stile CSS per lo stile dei moduli HTML5**

   Passa alla cartella in cui hai creato il renderer del profilo e crea un file foglio di stile CSS. I passaggi da seguire sono

   1. Fai clic con il pulsante destro del mouse sulla cartella e seleziona **creare** > **crea file** dal menu

   1. Nella finestra di dialogo crea file, immettere il nome del foglio di stile. Assicurati di utilizzare l&#39;estensione .css (ad esempio stylesheet.css)
   1. Dal riquadro di navigazione, apri il file CSS creato.
   1. Definisci le classi CSS dei componenti che desideri assegnare agli stili e aggiungi stili in tali classi.

   Per sapere quali classi CSS creare per un particolare componente nei moduli di HTML5, consulta [Introduzione agli stili](/help/forms/using/css-styles.md).

1. **Includere il foglio di stile nel modulo di rendering del profilo**

   Apri la pagina Renderer di profilo (file jsp) in CRX DE e includi il file CSS nella pagina immediatamente sotto la libreria client XFA. Esegui questi passaggi per includere il file CSS nel profilo.

   1. Cerca nella pagina del renderer la seguente riga:

      &lt;cq:includeClientLib categories=&quot;xfaforms.profile&quot; />

   1. Inserire quanto segue sotto la riga precedente per includere il foglio di stile:

      &lt;link href=&quot;/path/to/stylesheet&quot; rel=&quot;stylesheet&quot; type=&quot;text/css&quot;/>

   1. Salva il file.
