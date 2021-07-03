---
title: Usa tracciamento pagina e codice di incorporamento nelle pagine web
description: Scopri come includere il tracciamento pagina e i codici JavaScript da incorporare nel codice del sito web per consentire ad Adobe Analytics di acquisire i dati di utilizzo relativi alle risorse.
contentOwner: AG
role: Architect, Admin
feature: Rapporti su risorse
exl-id: 14d02015-df00-4566-a098-de76eaf42605
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 1%

---

# Utilizzare il tracciamento pagina e il codice di incorporamento nelle pagine web {#using-page-tracker-and-embed-code-in-web-pages}

Page Tracker è un pezzo di codice JavaScript che includi nel codice di siti web di terze parti per consentire ad Adobe Analytics di acquisire i dati di utilizzo intorno a [!DNL Adobe Experience Manager Assets] su questi siti web.

Per acquisire eventi, come clic e così via, specifici per le risorse, includi anche il codice di incorporamento nel codice dei siti web di terze parti.

Il seguente codice di esempio mostra l&#39;aspetto di una pagina web che contiene sia il codice di tracciamento pagina che il codice di incorporamento:

```html
<!DOCTYPE html>
<html>
    <head>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/sitecatalyst/appmeasurement.js"></script>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/assetinsights/pagetracker.js"></script>
            <script type="text/javascript">
                                assetAnalytics.attrTrackable = 'trackable';
                assetAnalytics.defaultTrackable = false;
                assetAnalytics.attrAssetID = 'aem-asset-id';
                assetAnalytics.assetImpressionPollInterval = 200; // interval in milliseconds
                assetAnalytics.charsLimitForGET = 2000; // bytes
                assetAnalytics.dispatcher.init("assetstesting","xxxx","xxx","list1","eVar3","event8","event7");
            </script>

    </head>

    <body>

                                <img
            src="https://10.41.52.147:4502/xxxx/content/dam/test/abc.jpg"
            data-aem-asset-id="aaid:a386f2cd78234becb66bd11575f9452d"
            data-trackable=true
            onload=assetAnalytics.core.assetLoaded(this)>

        <a
            href="https://www.adobe.com"

            onclick="assetAnalytics.core.assetClicked(this);return false">
                <img
                    src="http://localhost/xxxx/content/dam/test/xyz.jpg"
                    data-aem-asset-id="aaid:7fa01fce0ebe40268cd6dcf07e2d9cb1"
                    data-trackable=true
                    onload=assetAnalytics.core.assetLoaded(this)>
        </a>

    </body>
</html>
```

## Aggiungi codice di tracciamento pagina {#adding-page-tracker-code}

Puoi aggiungere il codice di tracciamento della pagina nella sezione di intestazione del codice del sito web. Il seguente frammento di codice mostra il codice Tracciamento pagina incluso in una pagina web di esempio:

```xml
 <head>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/sitecatalyst/appmeasurement.js"></script>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/foundation/assetinsights/pagetracker.js"></script>
            <script type="text/javascript">
                                assetAnalytics.attrTrackable = 'trackable';
                assetAnalytics.defaultTrackable = false;
                assetAnalytics.attrAssetID = 'aem-asset-id';
                assetAnalytics.assetImpressionPollInterval = 200; // interval in millis
                assetAnalytics.charsLimitForGET = 2000; // bytes
                assetAnalytics.dispatcher.init("assetstesting","abc.net","bee","list1","eVar3","event8","event7");
            </script>

 </head>
```

## Aggiungi codice di incorporamento {#add-embed-code}

Puoi aggiungere il codice di incorporamento all’interno del corpo del codice del sito web. Il seguente frammento di codice mostra il codice di incorporamento incluso in una pagina web di esempio:

```xml
<body>

      <img
            src="http://localhost:4502/xxxx/content/dam/test/xyz.jpg"
            data-aem-asset-id="aaid:a386f2cd78234becb66bd11575f9452d"
            data-trackable=true
            onload=assetAnalytics.core.assetLoaded(this)>

        <a
            href="https://www.adobe.com"

            onclick="assetAnalytics.core.assetClicked(this);return false">
           <img
                    src="http://localhost:4502/xxxx/content/dam/test/xyz.jpg"
                    data-aem-asset-id="aaid:7fa01fce0ebe40268cd6dcf07e2d9cb1"
                    data-trackable=true
                    onload=assetAnalytics.core.assetLoaded(this)>
        </a>

    </body>
```
