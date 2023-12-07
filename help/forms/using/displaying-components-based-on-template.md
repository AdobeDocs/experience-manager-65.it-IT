---
title: Visualizzazione dei componenti in base al modello utilizzato
description: Quando crei un modulo, scopri come abilitare i componenti nella barra laterale in base al modello selezionato.
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
content-type: reference
docset: aem65
exl-id: 1fc56829-db81-4450-b1d8-b4a31110199e
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 1%

---

# Visualizzazione dei componenti in base al modello utilizzato{#displaying-components-based-on-the-template-used}

Quando un autore di moduli crea un modulo adattivo utilizzando una [modello](../../forms/using/template-editor.md), l’autore del modulo può visualizzare e utilizzare componenti specifici basati sui criteri dei modelli. È possibile specificare un criterio per il contenuto dei modelli che consenta di scegliere un gruppo di componenti visualizzato dall&#39;autore del modulo durante la creazione del modulo.

## Modifica del criterio del contenuto di un modello {#changing-the-content-policy-of-a-template}

Quando si crea un modello, questo viene creato in `/conf` nell’archivio dei contenuti. In base alle cartelle create in `/conf` directory, il percorso del modello è: `/conf/<your-folder>/settings/wcm/templates/<your-template>`.

Per visualizzare i componenti nella barra laterale in base al criterio del contenuto di un modello, effettua le seguenti operazioni:

1. Apri CRXDE lite.\
   URL: `https://<server>:<port>/crx/de/index.jsp`
1. In CRXDE, passa alla cartella in cui è stato creato il modello.

   Esempio: `/conf/<your-folder>/`

1. In CRXDE, passa a: `/conf/<your-folder>/settings/wcm/policies/fd/af/layouts/gridFluidLayout/`

   Per selezionare un gruppo di componenti, è necessario un nuovo criterio per i contenuti. Per creare un criterio, copia e incolla il criterio predefinito e rinominalo.

   Il percorso del criterio contenuto predefinito è: `/conf/<your-folder>/settings/wcm/policies/fd/af/layouts/gridFluidLayout/default`

   In `gridFluidLayout` cartella, copia e incolla il criterio predefinito e rinominalo. Esempio: `myPolicy`.

   ![Copia dei criteri predefiniti](assets/crx-default1.png)

1. Seleziona il nuovo criterio creato e quindi fai clic su **componenti** proprietà nel pannello a destra con tipo `string[]`.

   Quando selezioni e apri la proprietà dei componenti, viene visualizzata la finestra di dialogo Modifica componenti. La finestra di dialogo Modifica componenti consente di aggiungere o rimuovere gruppi di componenti utilizzando **+** e **-** pulsanti. È possibile aggiungere un gruppo di componenti che includa i componenti che si desidera vengano utilizzati dagli autori.

   ![Aggiungere o rimuovere componenti nel criterio](assets/add-components-list1.png)

   Dopo aver aggiunto un gruppo di componenti, fai clic su **OK** per aggiornare l&#39;elenco, quindi fare clic su **Salva tutto** sopra la barra degli indirizzi CRXDE e aggiorna.

1. Nel modello, modifica il criterio del contenuto da predefinito al nuovo criterio creato. ( `myPolicy` in questo esempio.)

   Per modificare il criterio, in CRXDE, passa a `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/guideContainer/rootPanel/items`.

   In `cq:policy` proprietà, modifica `default` al nuovo nome del criterio ( `myPolicy`).

   ![Criterio contenuto modello aggiornato](assets/updated-policy.png)

   Quando crei un modulo utilizzando il modello, puoi visualizzare i componenti aggiunti nella barra laterale.
