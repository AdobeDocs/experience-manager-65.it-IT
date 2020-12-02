---
title: Targeting con Adobe Campaign
seo-title: Targeting con Adobe Campaign
description: Puoi creare esperienze mirate per Adobe Campaign dopo aver impostato la segmentazione.
seo-description: Puoi creare esperienze mirate per Adobe Campaign dopo aver impostato la segmentazione.
uuid: 8fcc9210-d8c5-44e3-8aa8-6c6db810c98e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: f1cb5e98-ccd1-4b2c-acca-2b3cc1b7ac5f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 74%

---


# Targeting con Adobe Campaign{#targeting-your-adobe-campaign}

Per segmentare la newsletter Adobe Campaign, devi innanzitutto configurare la segmentazione, disponibile solo nell&#39;interfaccia classica (per il ClientContext). Dopodiché, puoi creare esperienze mirate per Adobe Campaign. Entrambe le operazioni sono descritte in questa sezione.

## Impostazione della segmentazione con AEM {#setting-up-segmentation-in-aem}

Per impostare la segmentazione, è necessario utilizzare l’interfaccia classica per impostare i segmenti. I passaggi successivi possono essere eseguiti nell&#39;interfaccia utente standard.

L’impostazione della segmentazione comprende la creazione di segmenti, di un marchio, di una campagna e delle esperienze.

>[!NOTE]
>
>L’ID del segmento deve essere associato a quello su Adobe Campaign.

### Creazione dei segmenti {#creating-segments}

Per creare i segmenti:

1. Aprite la [console di segmentazione](Http://localhost:4502/miscadmin#/etc/segmentation) in **&lt;host>:&lt;porta>/miscadmin#/etc/segmentation**.
1. Create una nuova pagina e immettete un titolo, ad esempio **Segmenti CA**, quindi selezionate il modello **Segmento ( Adobe Campaign)**.
1. Seleziona la pagina creata nella struttura ad albero a sinistra.
1. Crea un segmento, ad esempio per utenti maschili, creando una nuova pagina chiamata Uomo sotto il segmento creato e seleziona il modello **Segmento (Adobe Campaign)**.
1. Apri la pagina dei segmenti creata e trascina sulla pagina l’**ID segmento** dalla finestra laterale.
1. Fare doppio clic sulla caratteristica, inserire l&#39;ID che rappresenta in questo caso il segmento maschile definito in  Adobe Campaign, ad esempio **MASCHIO**, quindi fare clic su **OK**. Dovrebbe comparire il seguente messaggio: *`targetData.segmentCode == "MALE"`*
1. Ripeti i passaggi per creare altri segmenti, ad esempio un segmento rivolto alle donne.

### Creazione di un marchio  {#creating-a-brand}

Per creare un marchio:

1. In **Siti**, andate alla cartella **Campagne** (ad esempio in We.Retail).
1. Fai clic su **Crea pagina** e inserisci un titolo per la pagina, ad esempio We.Retail Brand, poi seleziona il modello **Marchio**.

### Creazione di una campagna {#creating-a-campaign}

Per creare una campagna:

1. Apri la pagina **Marchio** appena creata.
1. Fai clic su **Crea pagina** e inserisci un titolo per la pagina, ad esempio We.Retail Campaign, poi seleziona il modello di **Campagna** e fai clic su **Crea**.

### Creazione di esperienze  {#creating-experiences}

Per creare delle esperienze per i segmenti:

1. Aprite la pagina **Campaign** appena creata.
1. Per creare esperienze per i segmenti, fai clic su **Crea pagina** e immetti un titolo per la pagina, ad esempio Maschio mentre crei un&#39;esperienza per il segmento Maschio, quindi seleziona il modello **Esperienza**.
1. Apri la pagina Esperienza creata.
1. Seleziona **Modifica**, vai in Segmenti e fai clic su **Aggiungi elemento**.
1. Inserite il percorso del segmento maschile, ad esempio **/etc/segmentation/ac-segment/maschio** e fate clic su **OK**. Dovrebbe comparire il seguente messaggio: *L&#39;esperienza è destinata a: Maschio*
1. Ripeti i passaggi precedenti per creare un&#39;esperienza per tutti i segmenti, ad esempio il target femminile.

## Creazione di una newsletter con contenuti di destinazione  {#creating-a-newsletter-with-targeted-content}

Dopo aver creato i segmenti, un marchio, una campagna e un&#39;esperienza, puoi creare una newsletter con contenuti personalizzati. Dopo aver creato l&#39;esperienza, collega le esperienze ai tuoi segmenti.

>[!NOTE]
>
>[I modelli e-mail sono disponibili solo in Geometrixx](/help/sites-developing/we-retail.md). Scaricate contenuti di Geometrixx di esempio da Package Share.

Creare una newsletter con contenuti di destinazione:

1. Create una newsletter con contenuti mirati: Sotto Campagne e-mail in Geometrixx Outdoors, fare clic o toccare **Crea** > **Pagina**, quindi selezionare uno dei  modelli di Adobe Campaign Mail.

   ![chlimage_1-188](assets/chlimage_1-188.png)

1. Nella newsletter, aggiungi un componente Testo e personalizzazione.
1. Aggiungi il testo al componente Testo e personalizzazione, ad esempio “Questo è il valore predefinito”.
1. Fare clic sulla freccia accanto a **Modifica** e selezionare **Targeting**.
1. Seleziona il tuo marchio dal menu a discesa Marchio e seleziona la tua Campagna. Si tratta del marchio e della campagna che hai creato in precedenza.
1. Fai clic su **Inizia impostazione destinazione**. I segmenti vengono visualizzati nell’area Tipi di pubblico. L&#39;esperienza predefinita viene utilizzata se nessuno dei segmenti definiti corrisponde.

   >[!NOTE]
   >
   >L&#39;impostazione predefinita prevede che le e-mail campione incluse in AEM utilizzino Adobe Campaign come motore di destinazione. Per le newsletter personalizzate, potrebbe essere necessario selezionare Adobe Campaign come motore di destinazione. Quando imposti la destinazione, tocca o fai clic su + nella barra degli strumenti, inserisci un titolo per la nuova attività e seleziona **Adobe Campaign** come motore di destinazione.

1. Fai clic su **Impostazione predefinita** e poi sul componente Testo e personalizzazione che hai aggiunto e vedrai l’icona bersaglio con una freccia. Fai clic sull’icona per impostare la destinazione per questo componente.

   ![chlimage_1-189](assets/chlimage_1-189.png)

1. Passa a un altro segmento (ad esempio Uomo), fai clic su **Aggiungi offerta** e sull’icona +. Quindi modificate l’offerta.
1. Passa a un altro segmento (ad esempio Donna), fai clic su **Aggiungi offerta** e sull’icona +. Quindi, modifica l’offerta.
1. Fare clic su **Next** per visualizzare la mappatura, quindi fare clic su **Next** per visualizzare le impostazioni, che non si applicano a  Adobe Campaign, e fare clic su **Save**.

   AEM genera automaticamente il codice di impostazione della destinazione corretto per Adobe Campaign quando il contenuto viene utilizzato in una consegna in Adobe Campaign.

1. In Adobe Campaign, crea la consegna: seleziona **Invio e-mail con contenuto AEM**, se necessario seleziona l’account AEM locale e conferma le modifiche apportate.

   Nella visualizzazione HTML, le diverse esperienze dei componenti con destinazione sono racchiuse nell’apposito codice di Adobe Campaign.

   ![chlimage_1-190](assets/chlimage_1-190.png)

   >[!NOTE]
   >
   >Se imposti i segmenti anche in Adobe Campaign, facendo clic su **Anteprima** verranno mostrate le esperienze per ogni segmento.

