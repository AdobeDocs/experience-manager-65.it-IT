---
title: Visualizzazione dei componenti in base al modello utilizzato
seo-title: Visualizzazione dei componenti in base al modello utilizzato
description: Quando si crea un modulo, è possibile apprendere come abilitare i componenti nella barra laterale in base al modello selezionato.
seo-description: Quando si crea un modulo, è possibile apprendere come abilitare i componenti nella barra laterale in base al modello selezionato.
uuid: 790d201b-318d-4d02-9bc5-9d6bc41d057a
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
content-type: reference
discoiquuid: f658da57-0134-4458-9ef9-a99787b66742
docset: aem65
translation-type: tm+mt
source-git-commit: 76908a565bf9e6916db39d7db23c04d2d40b3247
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 1%

---


# Visualizzazione dei componenti in base al modello utilizzato{#displaying-components-based-on-the-template-used}

Quando un autore crea un modulo adattivo utilizzando un [modello](../../forms/using/template-editor.md), l&#39;autore del modulo può visualizzare e utilizzare componenti specifici in base ai criteri per i modelli. È possibile specificare un criterio per il contenuto del modello che consente di scegliere un gruppo di componenti che l&#39;autore del modulo vede al momento della creazione del modulo.

## Modifica dei criteri di contenuto di un modello {#changing-the-content-policy-of-a-template}

Quando create un modello, questo viene creato in `/conf` nell&#39;archivio dei contenuti. In base alle cartelle create nella directory `/conf`, il percorso del modello è: `/conf/<your-folder>/settings/wcm/templates/<your-template>`.

Effettuate le seguenti operazioni per mostrare i componenti nella barra laterale in base ai criteri di contenuto di un modello:

1. Aprire CRXDE lite.\
   URL: `https://<server>:<port>/crx/de/index.jsp`
1. In CRXDE, individuate la cartella in cui viene creato il modello.

   Esempio: `/conf/<your-folder>/`

1. In CRXDE, passa a: `/conf/<your-folder>/settings/wcm/policies/fd/af/layouts/gridFluidLayout/`

   Per selezionare un gruppo di componenti, è necessario un nuovo criterio di contenuto. Per creare un nuovo criterio, copiate e incollate il criterio predefinito, quindi rinominatelo.

   Percorso del criterio contenuto predefinito: `/conf/<your-folder>/settings/wcm/policies/fd/af/layouts/gridFluidLayout/default`

   Nella cartella `gridFluidLayout`, copiate e incollate il criterio predefinito, quindi rinominatelo. Esempio, `myPolicy`.

   ![Copia dei criteri predefiniti](assets/crx-default1.png)

1. Selezionate il nuovo criterio creato e selezionate la proprietà **components** nel pannello a destra con il tipo `string[]`.

   Quando si seleziona e si apre la proprietà Components (Componenti), viene visualizzata la finestra di dialogo Edit components (Modifica componenti). La finestra di dialogo Modifica componenti consente di aggiungere o rimuovere gruppi di componenti utilizzando i pulsanti **+** e **-**. È possibile aggiungere un gruppo di componenti che include i componenti per il modulo che gli autori desiderano utilizzare.

   ![Aggiunta o rimozione di componenti nel criterio](assets/add-components-list1.png)

   Dopo aver aggiunto un gruppo di componenti, fare clic su **OK** per aggiornare l&#39;elenco, quindi fare clic su **Salva tutto** sopra la barra degli indirizzi CRXDE e aggiornare.

1. Nel modello, modificate il criterio del contenuto da predefinito al nuovo criterio creato. ( `myPolicy` in questo esempio.)

   Per modificare il criterio, in CRXDE, passare a `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/guideContainer/rootPanel/items`.

   Nella proprietà `cq:policy`, cambiare `default` nel nuovo nome del criterio ( `myPolicy`).

   ![Aggiornamento dei criteri per il contenuto dei modelli](assets/updated-policy.png)

   Quando si crea un modulo creato utilizzando il modello, è possibile vedere i componenti aggiunti nella barra laterale.

