---
title: Eseguire il targeting dell’Adobe Campaign
description: Puoi creare esperienze mirate per Adobe Campaign dopo aver impostato la segmentazione.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
exl-id: fc6fccba-41c5-4c13-aac0-b4ef67767abe
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization,Integration
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 1%

---

# Targeting del tuo Adobe Campaign{#targeting-your-adobe-campaign}

Per eseguire il targeting della newsletter Adobe Campaign, devi prima impostare la segmentazione, che è disponibile solo nell’interfaccia classica (per il contesto client). Dopodiché puoi creare esperienze mirate per Adobe Campaign. Entrambi sono descritti in questa sezione.

## Impostazione della segmentazione nell’AEM {#setting-up-segmentation-in-aem}

Per impostare la segmentazione, è necessario utilizzare l’interfaccia classica. I passaggi rimanenti possono essere eseguiti nell’interfaccia utente standard.

L’impostazione della segmentazione include la creazione di segmenti, un marchio, una campagna e esperienze.

>[!NOTE]
>
>L’ID del segmento deve essere mappato a quello sul lato Adobe Campaign.

### Creazione di segmenti {#creating-segments}

Per creare segmenti:

1. Apri la [console di segmentazione](http://localhost:4502/miscadmin#/etc/segmentation) in **&lt;host>:&lt;port>/miscadmin#/etc/segmentation**.
1. Crea una pagina e immetti un titolo, ad esempio **Segmenti AC**, quindi seleziona il modello **Segmento (Adobe Campaign)**.
1. Selezionare la pagina creata nella struttura ad albero sul lato sinistro.
1. Crea un segmento, ad esempio quello destinato agli utenti maschi, creando una pagina sotto il segmento creato denominato Maschio e seleziona il modello **Segmento (Adobe Campaign)**.
1. Apri la pagina del segmento creato e trascina un **ID segmento** dalla barra laterale alla pagina.
1. Fai doppio clic sulla caratteristica, immetti l&#39;ID che rappresenta in questo caso il segmento maschile definito in Adobe Campaign, ad esempio **MALE**, e fai clic su **OK**. Dovrebbe apparire il seguente messaggio: *`targetData.segmentCode == "MALE"`*
1. Ripeti i passaggi per un altro segmento, ad esempio un segmento destinato a utenti di sesso femminile.

### Creazione di un marchio {#creating-a-brand}

Per creare un marchio:

1. In **Sites**, passa alla cartella **Campagne** (ad esempio, in We.Retail).
1. Fai clic su **Crea pagina** e immetti un titolo per la pagina, ad esempio Marchio We.Retail, quindi seleziona il modello **Marchio**.

### Creazione di una campagna {#creating-a-campaign}

Per creare una campagna:

1. Apri la pagina **Marchio** creata.
1. Fai clic su **Crea pagina** e immetti un titolo per la pagina, ad esempio We.Retail Campaign, quindi seleziona il modello **Campaign** e fai clic su **Crea**.

### Creazione di esperienze {#creating-experiences}

Per creare esperienze per i segmenti:

1. Apri la pagina **Campaign** creata.
1. Per creare esperienze per i segmenti, fai clic su **Crea pagina** e immetti un titolo per la pagina, ad esempio Maschio mentre crei un&#39;esperienza per il segmento Maschio, quindi seleziona il modello **Esperienza**.
1. Apri la pagina Esperienza creata.
1. Fai clic su **Modifica**, quindi sotto Segmenti fai clic su **Aggiungi elemento**.
1. Immetti il percorso del segmento maschile, ad esempio **/etc/segmentation/ac-segments/male** e fai clic su **OK**. Dovrebbe apparire il seguente messaggio: *Esperienza con destinazione: Maschio*
1. Ripeti i passaggi precedenti per creare un’esperienza per tutti i segmenti, ad esempio il target femminile.

## Creazione di una newsletter con contenuti mirati {#creating-a-newsletter-with-targeted-content}

Dopo aver creato segmenti, un marchio, una campagna e un’esperienza, puoi creare una newsletter con contenuti mirati. Dopo aver creato l’esperienza, puoi collegarla ai segmenti.

>[!NOTE]
>
>[Gli esempi di e-mail sono disponibili solo in Geometrixx](/help/sites-developing/we-retail.md). Scarica il contenuto di esempio di un Geometrixx da Condivisione pacchetti.

Per creare una newsletter con contenuti mirati:

1. Crea una newsletter con contenuti di destinazione: sotto Campagne e-mail in Geometrixx Outdoors, fai clic su **Crea** > **Pagina** e seleziona uno dei modelli di Adobe Campaign Mail.

   ![chlimage_1-188](assets/chlimage_1-188.png)

1. Nella newsletter, aggiungi un componente Testo e Personalization.
1. Aggiungi del testo al componente Testo e Personalization, ad esempio &quot;Impostazione predefinita&quot;.
1. Fai clic sulla freccia accanto a **Modifica** e seleziona **Targeting**.
1. Seleziona il marchio dal menu a discesa Marchio e fai clic sulla tua campagna. Questo è il marchio e la campagna che hai creato in precedenza.
1. Fare clic su **Inizia impostazione destinazione**. I segmenti vengono visualizzati nell’area Tipi di pubblico. L’esperienza predefinita viene utilizzata se nessuno dei segmenti definiti corrisponde a.

   >[!NOTE]
   >
   >Per impostazione predefinita, gli esempi e-mail inclusi nell’AEM utilizzano Adobe Campaign come motore di targeting. Per le newsletter personalizzate, potrebbe essere necessario selezionare Adobe Campaign come motore di targeting. Durante il targeting, fai clic su + nella barra degli strumenti, immetti un titolo per la nuova attività e seleziona **Adobe Campaign** come motore di targeting.

1. Fai clic su **Default**, quindi sul componente Testo e Personalization aggiunto e visualizzerai il bullseye con una freccia. Fai clic sull’icona per eseguire il targeting di questo componente.

   ![chlimage_1-189](assets/chlimage_1-189.png)

1. Passa a un altro segmento (maschile), fai clic su **Aggiungi offerta** e fai clic sull&#39;icona più +. Quindi modifica l’offerta.
1. Passa a un altro segmento (Femmina) e fai clic su **Aggiungi offerta** e sull&#39;icona più +. Quindi modifica questa offerta.
1. Fai clic su **Avanti** per visualizzare la mappatura, quindi fai clic su **Avanti** per visualizzare le impostazioni, che non si applicano ad Adobe Campaign, quindi fai clic su **Salva**.

   AEM genera automaticamente il codice di targeting corretto per Adobe Campaign quando il contenuto viene utilizzato in una consegna all’interno di Adobe Campaign

1. In Adobe Campaign, crea la consegna - seleziona **Consegna e-mail con contenuto AEM**, seleziona l&#39;account AEM locale, come appropriato, e conferma le modifiche.

   Nella vista HTML, le diverse esperienze dei componenti target sono racchiuse nel codice di targeting di Adobe Campaign.

   ![chlimage_1-190](assets/chlimage_1-190.png)

   >[!NOTE]
   >
   >Se imposti anche i segmenti in Adobe Campaign, facendo clic su **Anteprima** potrai visualizzare le esperienze per ciascun segmento.
