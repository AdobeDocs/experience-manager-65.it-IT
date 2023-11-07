---
title: Eseguire il targeting dell’Adobe Campaign
description: Puoi creare esperienze mirate per Adobe Campaign dopo aver impostato la segmentazione.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
exl-id: fc6fccba-41c5-4c13-aac0-b4ef67767abe
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 0%

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

1. Apri [console di segmentazione](http://localhost:4502/miscadmin#/etc/segmentation) a **&lt;host>:&lt;port>/miscadmin#/etc/segmentation**.
1. Crea una pagina e immetti un titolo, ad esempio: **Segmenti AC**- e seleziona la **Segmento (Adobe Campaign)** modello.
1. Selezionare la pagina creata nella struttura ad albero sul lato sinistro.
1. Per creare un segmento, ad esempio quello destinato agli utenti maschi, crea una pagina sotto il segmento creato denominato Maschio e seleziona la **Segmento (Adobe Campaign)** modello.
1. Apri la pagina del segmento creato e trascina un **ID segmento** dalla barra laterale alla pagina.
1. Fai doppio clic sulla caratteristica, immetti l’ID che rappresenta in questo caso il segmento maschile definito in Adobe Campaign, ad esempio, **MASCHIO** - e fai clic su **OK**. Dovrebbe apparire il seguente messaggio: *`targetData.segmentCode == "MALE"`*
1. Ripeti i passaggi per un altro segmento, ad esempio un segmento destinato a utenti di sesso femminile.

### Creazione di un marchio {#creating-a-brand}

Per creare un marchio:

1. In entrata **Sites**, passare alla **Campagne** (ad esempio, in We.Retail).
1. Clic **Crea pagina** e inserisci un titolo per la pagina, ad esempio, Marchio We.Retail e seleziona il **Marchio** modello.

### Creazione di una campagna {#creating-a-campaign}

Per creare una campagna:

1. Apri **Marchio** pagina creata.
1. Clic **Crea pagina** e inserisci un titolo per la pagina, ad esempio We.Retail Campaign, e seleziona la **Campagna** e fai clic su **Crea**.

### Creazione di esperienze {#creating-experiences}

Per creare esperienze per i segmenti:

1. Apri **Campagna** pagina creata.
1. Creare esperienze per i segmenti facendo clic su **Crea pagina** e inserendo un titolo per la pagina, ad esempio Maschio durante la creazione di un&#39;esperienza per il segmento Maschio, quindi selezionare **Esperienza** modello.
1. Apri la pagina Esperienza creata.
1. Clic **Modifica**, quindi sotto Segmenti fai clic su **Aggiungi elemento**.
1. Immetti il percorso del segmento maschile, ad esempio: **/etc/segmentation/ac-segments/male** e fai clic su **OK**. Dovrebbe apparire il seguente messaggio: *Esperienza con destinazione: Maschio*
1. Ripeti i passaggi precedenti per creare un’esperienza per tutti i segmenti, ad esempio il target femminile.

## Creazione di una newsletter con contenuti mirati {#creating-a-newsletter-with-targeted-content}

Dopo aver creato segmenti, un marchio, una campagna e un’esperienza, puoi creare una newsletter con contenuti mirati. Dopo aver creato l’esperienza, puoi collegarla ai segmenti.

>[!NOTE]
>
>[Gli esempi di e-mail sono disponibili solo in Geometrixx](/help/sites-developing/we-retail.md). Scarica il contenuto di esempio di un Geometrixx da Condivisione pacchetti.

Per creare una newsletter con contenuti mirati:

1. Creare una newsletter con contenuti mirati: di seguito Campagne e-mail in Geometrixx Outdoors, tocca o fai clic su **Crea** > **Pagina** e selezionare uno dei modelli di Adobe Campaign Mail.

   ![chlimage_1-188](assets/chlimage_1-188.png)

1. Nella newsletter, aggiungi un componente Testo e personalizzazione.
1. Aggiungi del testo al componente Testo e personalizzazione, ad esempio &quot;Impostazione predefinita&quot;.
1. Fai clic sulla freccia accanto a **Modifica** e seleziona **Targeting**.
1. Seleziona il marchio dal menu a discesa Marchio e fai clic sulla tua campagna. Questo è il marchio e la campagna che hai creato in precedenza.
1. Clic **Inizia impostazione destinazione**. I segmenti vengono visualizzati nell’area Tipi di pubblico. L’esperienza predefinita viene utilizzata se nessuno dei segmenti definiti corrisponde a.

   >[!NOTE]
   >
   >Per impostazione predefinita, gli esempi e-mail inclusi nell’AEM utilizzano Adobe Campaign come motore di targeting. Per le newsletter personalizzate, potrebbe essere necessario selezionare Adobe Campaign come motore di targeting. Quando esegui il targeting, tocca o fai clic su + nella barra degli strumenti, immetti un titolo per la nuova attività e seleziona **Adobe Campaign** come motore di targeting.

1. Clic **Predefinito** e poi il componente Testo e personalizzazione aggiunto e vedete il bulletto con una freccia. Fai clic sull’icona per eseguire il targeting di questo componente.

   ![chlimage_1-189](assets/chlimage_1-189.png)

1. Passa a un altro segmento (maschile) e fai clic su **Aggiungi offerta** e fai clic sull’icona più +. Quindi modifica l’offerta.
1. Passa a un altro segmento (Femmina) e fai clic su **Aggiungi offerta** e l’icona più +. Quindi modifica questa offerta.
1. Clic **Successivo** per visualizzare la mappatura, fai clic su **Successivo** per visualizzare Impostazioni, che non si applica ad Adobe Campaign, quindi fai clic su **Salva**.

   AEM genera automaticamente il codice di targeting corretto per Adobe Campaign quando il contenuto viene utilizzato in una consegna all’interno di Adobe Campaign

1. In Adobe Campaign, crea la consegna - seleziona **Consegna e-mail con contenuti AEM** e seleziona l’account AEM locale, come appropriato, e conferma le modifiche.

   Nella vista HTML, le diverse esperienze dei componenti target sono racchiuse nel codice di targeting di Adobe Campaign.

   ![chlimage_1-190](assets/chlimage_1-190.png)

   >[!NOTE]
   >
   >Se imposti anche i segmenti in Adobe Campaign, fai clic su **Anteprima** ti mostrerà le esperienze per ogni segmento.
