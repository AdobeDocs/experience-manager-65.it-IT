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
role: User,Admin,Developer
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 1%

---

# Targeting con Adobe Campaign{#targeting-your-adobe-campaign}

Per eseguire il targeting della newsletter Adobe Campaign, devi prima impostare la segmentazione, che è disponibile solo nell’interfaccia classica (per il contesto client). Dopodiché puoi creare esperienze mirate per Adobe Campaign. Entrambi sono descritti in questa sezione.

## Impostazione della segmentazione in AEM {#setting-up-segmentation-in-aem}

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
