---
title: Modifica degli stili predefiniti dei moduli HTML5
description: Lo stile dei moduli di HTML5 è basato su CSS. È possibile modificare gli stili predefiniti del modulo.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: 4c84cfd1-50a4-416f-b4a5-7f2f4c7f10af
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
source-wordcount: '369'
ht-degree: 4%
---
# Modifica degli stili predefiniti dei moduli HTML5{#changing-default-styles-of-html-forms}

I moduli HTML5 vengono sottoposti a rendering utilizzando le funzionalità di HTML5 e lo stile del modulo sottoposto a rendering viene eseguito utilizzando CSS. L&#39;aspetto predefinito dei moduli HTML5 è simile al rendering PDF. Gli sviluppatori possono utilizzare CSS personalizzati per modificare l&#39;aspetto predefinito dei moduli HTML5.

Questo articolo fornisce informazioni dettagliate per modificare lo stile di un modulo di HTML5 e [Introduzione agli stili](/help/forms/using/css-styles.md) contiene informazioni dettagliate su vari aspetti dello stile dei moduli di HTML5. Assicurati di aver letto l’articolo Introduzione agli stili prima di eseguire i passaggi menzionati in questo articolo.

Le due immagini seguenti mostrano la differenza tra gli stili predefiniti e personalizzati.

![immagini-002-small](assets/pictures-002-small.png)

## Personalizzare lo stile dei moduli {#style-your-forms}

1. **Scegliere un profilo per aggiungere stili personalizzati**

   Accedi all&#39;interfaccia di CRX DE all&#39;URL: **https://&lt;server>:&lt;port>/crx/de** e crea un profilo o scegli un profilo esistente. Per informazioni su come creare un profilo, vedere [Creazione di un profilo](/help/forms/using/custom-profile.md)

1. **Creare un foglio di stile CSS per la formattazione dei moduli HTML5**

   Passa alla cartella in cui hai creato il renderer del profilo e crea un file del foglio di stile CSS. I passaggi da seguire sono

   1. Fai clic con il pulsante destro del mouse sulla cartella e seleziona **crea** > **crea file** dal menu

   1. Nella finestra di dialogo Crea file immettere il nome del foglio di stile. Assicurati di utilizzare l’estensione .css (ad esempio, stylesheet.css)
   1. Dal riquadro di navigazione, apri il file CSS creato.
   1. Definisci le classi CSS dei componenti a cui vuoi applicare uno stile e aggiungi gli stili in tali classi.

   Per informazioni sulle classi CSS da creare per un particolare componente nei moduli HTML5, vedere [Introduzione agli stili](/help/forms/using/css-styles.md).

1. **Includi il foglio di stile nel modulo di rendering profili**

   Apri la pagina di rendering del profilo (file jsp) in CRX DE e includi il file CSS nella pagina appena sotto la libreria client XFA. Per includere il file CSS nel profilo, effettua le seguenti operazioni.

   1. Cerca nella pagina del renderer la seguente riga:

      &lt;cq:includeClientLib Categories=&quot;xfaforms.profile&quot; />

   1. Inserire quanto segue sotto la riga precedente per includere il foglio di stile:

      &lt;link href=&quot;/path/to/stylesheet&quot; rel=&quot;stylesheet&quot; type=&quot;text/css&quot;/>

   1. Salva il file.
