---
title: Creare un modulo adattivo utilizzando un set di moduli adattivi
seo-title: Creare un modulo adattivo utilizzando un set di moduli adattivi
description: 'Con AEM Forms, è possibile unire i moduli adattivi per creare un singolo modulo adattivo di grandi dimensioni e comprenderne le funzioni. '
seo-description: 'Con AEM Forms, è possibile unire i moduli adattivi per creare un singolo modulo adattivo di grandi dimensioni e comprenderne le funzioni. '
uuid: e52e4f90-8821-49ec-89ff-fbf07db69bd2
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 264aa8c0-ba64-4768-b3d1-1b9baa6b4d72
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 0%

---


# Creare un modulo adattivo utilizzando un set di moduli adattivi{#create-an-adaptive-form-using-a-set-of-adaptive-forms}

## Panoramica {#overview}

In un flusso di lavoro, ad esempio un’applicazione per l’apertura di un conto bancario, gli utenti compilano più moduli. Anziché chiedere loro di compilare un set di moduli, è possibile sovrapporre i moduli e creare un modulo di grandi dimensioni (modulo principale). Quando si aggiunge un modulo adattivo al modulo più grande, questo viene aggiunto come pannello (modulo figlio). Per creare un modulo principale è possibile aggiungere un set di moduli figlio. Puoi mostrare o nascondere i pannelli in base all’input dell’utente. I pulsanti del modulo principale, ad esempio invio e ripristino, sovrascrivono i pulsanti del modulo figlio. Per aggiungere un modulo adattivo nel modulo principale, puoi trascinare il modulo adattivo dal browser delle risorse (come i frammenti di modulo adattivo).

Le funzioni disponibili sono:

* Authoring indipendente
* Visualizzazione/eliminazione dei moduli appropriati
* Caricamento pigro

Funzioni quali authoring indipendente e caricamento lento migliorano le prestazioni rispetto all’utilizzo dei singoli componenti per creare il modulo principale.

>[!NOTE]
>
>Non è possibile utilizzare moduli/frammenti adattivi basati su XFA come moduli figlio o padre.

## Dietro le quinte {#behind-the-scenes}

È possibile aggiungere moduli adattivi basati su XSD e frammenti nel modulo principale. La struttura del modulo principale è la stessa di [qualsiasi modulo adattivo](../../forms/using/prepopulate-adaptive-form-fields.md). Quando si aggiunge un modulo adattivo come modulo secondario, questo viene aggiunto come pannello nel modulo principale. I dati di un modulo figlio associato sono memorizzati nella directory `data`principale della sezione `afBoundData` dello schema XML del modulo padre.

Ad esempio, i clienti compilano un modulo di richiesta. I primi due campi del modulo sono nome e identità. Il codice XML è:

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
        </data>
    </afBoundData>
</afData>
```

Nell’applicazione è aggiunto un altro modulo che consente ai clienti di compilare il proprio indirizzo dell’ufficio. La radice dello schema del modulo figlio è `officeAddress`. Applica `bindref` `/application/officeAddress` o `/officeAddress`. Se `bindref`non viene fornito, il modulo figlio viene aggiunto come sottoalbero `officeAddress`. Vedere l&#39;XML del modulo seguente:

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
            <officeAddress>
                <addressLine>1, Geometrixx City</addressLine>
                <zip>11111</zip>
            </officeAddress>
        </data>
    </afBoundData>
</afData>
```

Se si inserisce un altro modulo che consente ai clienti di fornire l&#39;indirizzo della casa, applicare `bindref` `/application/houseAddress or /houseAddress.`L&#39;XML è simile al seguente:

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
            <officeAddress>
                <addressLine>1, Geometrixx City</addressLine>
                <zip>11111</zip>
            </officeAddress>
            <houseAddress>
                <addressLine>2, Geometrixx City</addressLine>
                <zip>11111</zip>
            </houseAddress>
        </data>
    </afBoundData>
</afData>
```

Se desideri mantenere lo stesso nome della radice secondaria della directory principale dello schema ( `Address`in questo esempio), utilizza i binding indicizzati.

Ad esempio, applica i binari `/application/address[1]` o `/address[1]` e `/application/address[2]` o `/address[2]`. XML del modulo:

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
            <address>
                <addressLine>1, Geometrixx City</addressLine>
                <zip>11111</zip>
            </address>
            <address>
                <addressLine>2, Geometrixx City</addressLine>
                <zip>11111</zip>
            </address>
        </data>
    </afBoundData>
</afData>
```

È possibile modificare la struttura secondaria predefinita del modulo/frammento adattivo utilizzando la proprietà `bindRef` . La proprietà `bindRef` consente di specificare il percorso che punta a una posizione nella struttura ad albero dello schema XML.

Se il modulo figlio non è associato, i relativi dati vengono memorizzati nella directory principale `data`della sezione `afUnboundData` dello schema XML del modulo padre.

È possibile aggiungere più volte un modulo adattivo come modulo secondario. Assicurati che la `bindRef` sia modificata correttamente in modo che ogni istanza utilizzata del modulo adattivo punti a una sottoradice diversa sotto la radice dati.

>[!NOTE]
>
>Se diversi moduli/frammenti sono mappati sulla stessa radice secondaria, i dati vengono sovrascritti.

## Aggiunta di un modulo adattivo come modulo figlio tramite il browser Risorse {#adding-an-adaptive-form-as-a-child-form-using-asset-browser}

Esegui le seguenti operazioni per aggiungere un modulo adattivo come modulo figlio utilizzando il browser risorse.

1. Aprire il modulo principale in modalità di modifica.
1. Nella barra laterale, fai clic su **Risorse** ![risorse-browser](assets/assets-browser.png). In Risorse, seleziona **Modulo adattivo** dal menu a discesa.
   [ ![Selezione del modulo adattivo in Assets](assets/asset.png)](assets/asset-1.png)

1. Trascina il modulo adattivo da aggiungere come modulo figlio.
   [ ![Trascina il modulo adattivo nel ](assets/drag-drop.png)](assets/drag-drop-1.png)sitoIl modulo adattivo rilasciato viene aggiunto come modulo secondario.

