---
title: Visualizzazione dei componenti in base al modello utilizzato
seo-title: Displaying components based on the template used
description: Quando crei un modulo, scopri come abilitare i componenti nella barra laterale in base al modello selezionato.
seo-description: When you create a form, learn how you can enable components in the sidebar based on the template selected.
uuid: 790d201b-318d-4d02-9bc5-9d6bc41d057a
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
content-type: reference
discoiquuid: f658da57-0134-4458-9ef9-a99787b66742
docset: aem65
exl-id: 1fc56829-db81-4450-b1d8-b4a31110199e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 1%

---

# Visualizzazione dei componenti in base al modello utilizzato{#displaying-components-based-on-the-template-used}

Quando un autore crea un modulo adattivo utilizzando un [template](../../forms/using/template-editor.md), l’autore del modulo può visualizzare e utilizzare componenti specifici in base ai criteri dei modelli. È possibile specificare un criterio per il contenuto del modello che consente di scegliere un gruppo di componenti che l’autore del modulo visualizza al momento della creazione del modulo.

## Modifica del criterio del contenuto di un modello {#changing-the-content-policy-of-a-template}

Quando crei un modello, questo viene creato in `/conf` nell’archivio dei contenuti. In base alle cartelle create in `/conf` directory, il percorso del modello è: `/conf/<your-folder>/settings/wcm/templates/<your-template>`.

Per visualizzare i componenti nella barra laterale in base al criterio del contenuto di un modello, effettua le seguenti operazioni:

1. Apri CRXDE lite.\
   URL: `https://<server>:<port>/crx/de/index.jsp`
1. In CRXDE, passa alla cartella in cui viene creato il modello.

   Esempio: `/conf/<your-folder>/`

1. In CRXDE, passa a: `/conf/<your-folder>/settings/wcm/policies/fd/af/layouts/gridFluidLayout/`

   Per selezionare un gruppo di componenti, è necessario un nuovo criterio per i contenuti. Per creare un nuovo criterio, copiare e incollare il criterio predefinito e rinominarlo.

   Percorso del criterio contenuto predefinito: `/conf/<your-folder>/settings/wcm/policies/fd/af/layouts/gridFluidLayout/default`

   In `gridFluidLayout` , copia e incolla il criterio predefinito e rinominalo. Esempio: `myPolicy`.

   ![Copia dei criteri predefiniti](assets/crx-default1.png)

1. Selezionare il nuovo criterio creato e selezionare il **componenti** nel pannello laterale destro con il tipo `string[]`.

   Quando selezioni e apri la proprietà dei componenti, viene visualizzata la finestra di dialogo Modifica componenti . La finestra di dialogo Modifica componenti consente di aggiungere o rimuovere gruppi di componenti utilizzando **+** e **-** pulsanti. È possibile aggiungere un gruppo di componenti che include i componenti modulo che gli autori devono utilizzare.

   ![Aggiungere o rimuovere componenti nel criterio](assets/add-components-list1.png)

   Dopo aver aggiunto un gruppo di componenti, fai clic su **OK** per aggiornare l&#39;elenco, quindi fare clic su **Salva tutto** sopra la barra degli indirizzi CRXDE e aggiornare.

1. Nel modello, modificare il criterio del contenuto da predefinito al nuovo criterio creato. ( `myPolicy` in questo esempio).

   Per modificare il criterio, in CRXDE, passa a `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/guideContainer/rootPanel/items`.

   In `cq:policy` proprietà, modifica `default` al nuovo nome del criterio ( `myPolicy`).

   ![Criterio del contenuto del modello aggiornato](assets/updated-policy.png)

   Quando si crea un modulo creato utilizzando il modello, è possibile visualizzare i componenti aggiunti nella barra laterale.
