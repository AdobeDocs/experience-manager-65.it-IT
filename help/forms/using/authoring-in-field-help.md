---
title: Authoring della guida contestuale per i campi del modulo
seo-title: Authoring della guida contestuale per i campi del modulo
description: ' AEM Forms consente di aggiungere aiuto contestuale a campi e pannelli di moduli adattivi, come testo o contenuti multimediali avanzati, compresi i video.'
seo-description: ' AEM Forms consente di aggiungere aiuto contestuale a campi e pannelli di moduli adattivi, come testo o contenuti multimediali avanzati, compresi i video.'
uuid: 1865bf7b-66fc-4f89-bd98-904daa409320
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 78000342-a6a7-4c2e-acab-a88851b82c2a
docset: aem65
translation-type: tm+mt
source-git-commit: 8bc99ed3817398ae358d439a5c1fcc90bbd24327
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 1%

---


# Authoring della guida contestuale per i campi modulo{#authoring-in-context-help-for-form-fields}

## Introduzione {#introduction}

In alcuni casi, gli utenti finali che compilano un modulo non sono sicuri di come compilare i dettagli in un particolare campo del modulo. Per risolvere tali problemi, i moduli adattivi supportano l&#39;aggiunta di testo o di informazioni dettagliate nel contesto a un campo del modulo. Consente di migliorare l&#39;esperienza di compilazione del modulo ed evitare ogni ambiguità per gli utenti finali.

In questo articolo viene illustrato in che modo gli autori dei moduli possono aggiungere la guida contestuale durante la creazione di Forms adattivo.

## Aggiungi aiuto contestuale {#add-in-context-help}

Potete specificare la guida contestuale utilizzando le seguenti opzioni nella sezione Contenuto della Guida della scheda Proprietà nella barra laterale.

* [Breve descrizione](../../forms/using/authoring-in-field-help.md#p-short-description-p)
* [Descrizione lunga](../../forms/using/authoring-in-field-help.md#p-long-description-p)

![Guida contestuale per i campi modulo](assets/descriptions.png)

>[!NOTE]
>
>La descrizione lunga sostituisce la descrizione breve. Se avete specificato entrambi, verrà visualizzata solo la descrizione lunga.

### Breve descrizione {#short-description}

Il campo Descrizione breve fornisce suggerimenti rapidi e brevi sulla compilazione di un campo del modulo. Il testo specificato nel campo Descrizione breve viene visualizzato come suggerimento quando si passa il mouse sul campo.

![Breve descrizione dell&#39;aggiunta della guida contestuale per i campi modulo](assets/tooltip.png)

>[!NOTE]
>
>Selezionare **Mostra sempre una breve descrizione** per visualizzare in modo permanente il testo della guida sotto il campo.

![Guida contestuale permanente breve sotto il campo](assets/short1.png)

### Descrizione lunga {#long-description}

Potete utilizzare il campo Descrizione lunga per specificare testo lungo o incorporare contenuti multimediali avanzati, inclusi video, come guida contestuale. Ad esempio, l’immagine seguente mostra come incorporare un video come guida contestuale.

![Aggiunta di contenuti multimediali avanzati come aiuto contestuale per i campi modulo](assets/long-descriptions.png)

Se si aggiunge una descrizione lunga, viene visualizzata una **?** accanto al campo. Facendo clic sull&#39;icona viene visualizzato il contenuto aggiunto nella sezione di descrizione lunga.

![Esempio di aiuto contestuale per i rich media](assets/photoshop.png)

### Guida a livello di pannello {#panel-level-help}

Oltre alla guida contestuale per i campi modulo, è possibile specificare la guida a livello di pannello nella scheda del contenuto della Guida della finestra di dialogo di modifica del pannello.

![Aggiunta della guida contestuale a un pannello del modulo](assets/panel-level-help.png)

Aggiungendo aiuto per il pannello viene visualizzato un **?** accanto alla descrizione del pannello. Facendo clic sull’icona viene visualizzato il contenuto aggiunto nella sezione Contenuto della guida della finestra di dialogo di modifica del pannello.

![Esempio di aiuto contestuale a livello di pannello del modulo](assets/photoshop-1.png)

