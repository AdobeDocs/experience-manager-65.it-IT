---
title: Targeting con Adobe Campaign
seo-title: Targeting con Adobe Campaign
description: L’impostazione della segmentazione comprende la creazione di segmenti, di un marchio, di una campagna e delle esperienze.
seo-description: L’impostazione della segmentazione comprende la creazione di segmenti, di un marchio, di una campagna e delle esperienze.
uuid: 520cd006-0aa8-43f3-b754-efb7397bb92f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: bbc2aac9-ccf1-40c3-be4f-d59c2d0d8a6c
translation-type: tm+mt
source-git-commit: 016c705230dffec052c200b058a36cdbe0520fc4

---


# Targeting con Adobe Campaign{#targeting-your-adobe-campaign}

Per segmentare la newsletter Adobe Campaign, innanzitutto è necessario configurare la segmentazione, disponibile solo nell&#39;interfaccia classica. In seguito, è possibile creare esperienze mirate per Adobe Campaign.

## Impostazione della segmentazione con AEM {#setting-up-segmentation-in-aem}

L’impostazione della segmentazione comprende la creazione di segmenti, di un marchio, di una campagna e delle esperienze. È possibile creare i segmenti solo nell&#39;interfaccia classica. Puoi creare marchi, campagne ed esperienze nell’interfaccia touch.

>[!NOTE]
>
>L’ID del segmento deve essere associato a quello su Adobe Campaign.

### Creazione dei segmenti {#creating-segments}

Per creare i segmenti:

1. Open the [segmentation console](http://localhost:4502/miscadmin#/etc/segmentation) at **&lt;host>:&lt;port>/miscadmin#/etc/segmentation**.
1. Create a new page and enter a title - for example, **AC Segments** - and select the **Segment (Adobe Campaign)** template.
1. Seleziona la pagina creata nella struttura ad albero a sinistra.
1. Crea un segmento, ad esempio per utenti maschili, creando una nuova pagina chiamata Uomo sotto il segmento creato e seleziona il modello **Segmento (Adobe Campaign)**.
1. Apri la pagina dei segmenti creata e trascina sulla pagina l’**ID segmento** dalla finestra laterale.
1. Double-click the trait, enter the ID representing in this case, the male segment defined in Adobe Campaign - for example, **MALE** - and click **OK**. Dovrebbe comparire il seguente messaggio: `targetData.segmentCode == "MALE"`
1. Ripeti i passaggi per creare altri segmenti, ad esempio un segmento rivolto alle donne.

### Creazione di un marchio {#creating-a-brand}

Per creare un marchio:

1. In **Sites**, navigate to the **Campaigns** folder (for example in We.Retail).
1. Fai clic su **Crea pagina** e inserisci un titolo per la pagina, ad esempio We.Retail Brand, poi seleziona il modello **Marchio**.

### Creazione di una campagna {#creating-a-campaign}

Per creare una campagna:

1. Apri la pagina **Marchio** appena creata.
1. Fai clic su **Crea pagina** e inserisci un titolo per la pagina, ad esempio We.Retail Campaign, poi seleziona il modello di **Campagna** e fai clic su **Crea**.

### Creazione di esperienze {#creating-experiences}

Per creare delle esperienze per i segmenti:

1. Open the **Campaign** page you just created.
1. Create experiences for your segments by clicking **Create Page** and entering a title for your page, for example, Male as you are creating an experience for the Male segment, and select the **Experience** template.
1. Apri la pagina Esperienza creata.
1. Seleziona **Modifica**, vai in Segmenti e fai clic su **Aggiungi elemento**.
1. Enter the path to the male segment, for example `/etc/segmentation/ac-segments/male` and click **OK**. The following message should appear: *Experience is targeted at: Male*
1. Ripeti i passaggi precedenti per creare un&#39;esperienza per tutti i segmenti, ad esempio il target femminile.

## Creazione di una newsletter con contenuti di destinazione {#creating-a-newsletter-with-targeted-content}

Dopo aver creato i segmenti, un marchio, una campagna e un&#39;esperienza, puoi creare una newsletter con contenuti personalizzati. Dopo aver creato l&#39;esperienza, collega le esperienze ai tuoi segmenti.

Potete creare la newsletter con contenuti mirati nell’interfaccia touch e classica. Questo documento descrive la procedura per l’interfaccia touch.

Creare una newsletter con contenuti di destinazione:

1. Create a newsletter with targeted content: Below Email Campaigns in Geometrixx Outdoors, click or tap **Create** > **Page**, and select one of the Adobe Campaign Mail templates.

   >[!NOTE]
   >
   >[I modelli e-mail sono disponibili solo in Geometrixx](/help/sites-developing/we-retail.md#weretail). Scaricate un esempio di contenuto Geometrixx da Package Share.

1. Nella newsletter, aggiungi un componente Testo e personalizzazione.
1. Aggiungi il testo al componente Testo e personalizzazione, ad esempio “Questo è il valore predefinito”.
1. Click the arrow next to **Edit** and select **Targeting**.
1. Seleziona il tuo marchio dal menu a discesa Marchio e seleziona la tua Campagna. Si tratta del marchio e della campagna che hai creato in precedenza.
1. Fai clic su **Inizia impostazione destinazione**. I segmenti vengono visualizzati nell’area Tipi di pubblico. L&#39;esperienza predefinita viene utilizzata se nessuno dei segmenti definiti corrisponde.

   >[!NOTE]
   >
   >L&#39;impostazione predefinita prevede che le e-mail campione incluse in AEM utilizzino Adobe Campaign come motore di destinazione. Per le newsletter personalizzate, potrebbe essere necessario selezionare Adobe Campaign come motore di destinazione. Quando imposti la destinazione, tocca o fai clic su + nella barra degli strumenti, inserisci un titolo per la nuova attività e seleziona **Adobe Campaign** come motore di destinazione.

1. Fai clic su **Impostazione predefinita** e poi sul componente Testo e personalizzazione che hai aggiunto e vedrai l’icona bersaglio con una freccia. Fai clic sull’icona per impostare la destinazione per questo componente.

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. Passa a un altro segmento (ad esempio Uomo), fai clic su **Aggiungi offerta** e sull’icona +. Quindi modificate l’offerta.
1. Passa a un altro segmento (ad esempio Donna), fai clic su **Aggiungi offerta** e sull’icona +. Quindi, modifica l’offerta.
1. Click **Next** to see Mapping, then click **Next** to see Settings, which does not apply to Adobe Campaign, and click **Save**.

   AEM genera automaticamente il codice di impostazione della destinazione corretto per Adobe Campaign quando il contenuto viene utilizzato in una consegna in Adobe Campaign.

1. In Adobe Campaign, crea la consegna: seleziona **Invio e-mail con contenuto AEM**, se necessario seleziona l’account AEM locale e conferma le modifiche apportate.

   Nella visualizzazione HTML, le diverse esperienze dei componenti con destinazione sono racchiuse nell’apposito codice di Adobe Campaign.

   ![chlimage_1-166](assets/chlimage_1-166.png)

   >[!NOTE]
   >
   >Se imposti i segmenti anche in Adobe Campaign, facendo clic su **Anteprima** verranno mostrate le esperienze per ogni segmento.

