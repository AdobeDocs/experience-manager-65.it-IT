---
title: Candidati archivio ContextHub di esempio
description: ContextHub fornisce diversi esempi di store candidati che puoi utilizzare nelle tue soluzioni
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: d8d9a799-3e30-442a-843b-d4d7ba70c557
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 1%

---

# Candidati archivio ContextHub di esempio{#sample-contexthub-store-candidates}

ContextHub fornisce diversi esempi di store candidati che puoi utilizzare nelle soluzioni. Per ciascun campione vengono fornite le seguenti informazioni:

* Dove trovare il codice sorgente in modo da poterlo aprire a scopo di apprendimento.
* Come configurare i negozi creati dai candidati del negozio.
* Struttura dei dati di archivio in modo da potervi accedere.

>[!WARNING]
>
>I candidati per l’archivio di esempi vengono forniti come configurazioni di riferimento per aiutarti a creare una configurazione dedicata per il progetto. Non utilizzarle direttamente.

## Candidato per archivio campioni aem.segmentation {#aem-segmentation-sample-store-candidate}

Archivia per segmenti ContextHub risolti e non risolti. Recupera automaticamente i segmenti da ContextHub SegmentManager.

### Percorso di origine {#source-location-segmentation}

`/libs/settings/cloudsettings/legacy/contexthub/segmentation`

### Implementazione di base {#base-implementation-segmentation}

Il candidato per l’archivio aem.segmentation estende [`ContextHub.Store.PersistedJSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore).

### Configurazione {#configuration-segmentation}

Quando crei un archivio aem.segmentation, non devi fornire una configurazione dettagliata. La configurazione predefinita specifica la posizione delle definizioni dei segmenti ContextHub.

```xml
{
   "service":{
      "jsonp":false,
      "timeout":1000,
      "path":"/etc/segmentation/contexthub.segment.js"
   }
}
```

## contexthub.geolocation Sample Store Candidate {#contexthub-geolocation-sample-store-candidate}

Il candidato dell’archivio di esempio contexthub.geolocation utilizza Google Maps per ottenere e archiviare informazioni sulla posizione del client.

### Percorso di origine {#source-location-geolocation}

`/libs/settings/cloudsettings/legacy/contexthub/geolocation`

### Implementazione di base {#base-implementation-geolocation}

Il candidato dell’archivio contexthub.geolocation estende [`ContextHub.Store.PersistedJSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore).

### Configurazione {#configuration-geolocation}

La configurazione predefinita specifica informazioni sul servizio Google e le coordinate iniziali di latitudine e longitudine.

```xml
{
        "service": {
            "jsonp": false,
            "timeout": 1000,
            "ttl": 1800000,
            "secure": false,
            "host": "maps.googleapis.com",
            "port": 80,
            "path": "/maps/api/geocode/json"
        },

        "eventDeferring": 16,

        "html5coordinatesDiscoveryAPI": {
            "timeout": 30000,
            "ttl": 900000,
            "highAccuracy": false
        },

        "initialValues": {
            "latitude": 37.331375,
            "longitude": -121.893992
        }
    }
```

### Elementi dati {#data-items-geolocation}

L’archivio utilizza una struttura dati simile a quella del seguente esempio:

```xml
{
   "latitude":"37.331375",
   "longitude":"-121.893992"
}
```

>[!NOTE]
>
>Un criterio di sicurezza introdotto in Chrome 50.x richiede che tutte le chiamate relative alla geolocalizzazione vengano effettuate tramite una connessione protetta. Pertanto, l’AEM forza l’utilizzo di https per le chiamate API di geolocalizzazione se l’AEM è in esecuzione anche su https. Altrimenti http viene utilizzato per rispettare il criterio della stessa origine. Consulta [questo post di blog su Google](https://developers.google.com/web/updates/2016/04/geolocation-on-secure-contexts-only) per ulteriori dettagli sulla modifica in Chrome.

## contexthub.surferinfo Sample Store Candidate {#contexthub-surferinfo-sample-store-candidate}

Memorizza informazioni sull&#39;ambiente client corrente, ad esempio dispositivo, finestra, browser, data e ora.

### Percorso di origine {#source-location-surferinfo}

`/libs/settings/cloudsettings/legacy/contexthub/surferinfo`

### Implementazione di base {#base-implementation-surferinfo}

Il candidato dell’archivio contexthub.datetime estende [`ContextHub.Store.PersistedStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore).

### Configurazione {#configuration-surferinfo}

La configurazione predefinita viene ereditata da `ContextHub.Store.PersistedStore`.

### Elementi dati {#data-items-surferinfo}

Gli archivi che utilizzano questo candidato hanno una struttura dati simile a quella del seguente esempio:

```xml
{
   "display":{
      "resolution":{
         "width":1440,
         "height":900
      },
      "devicePixelRatio":1,
      "colorDepth":24,
      "nrOfColors":16777216,
      "pixelsPerInch":96,
      "orientation":{
         "mode":"landscape",
         "direction":"normal"
      }
   },
   "window":{
      "dimension":{
         "width":1395,
         "height":652
      },
      "percentageUsage":0.7
   },
   "browser":{
      "version":"39.0",
      "family":"Firefox",
      "userAgent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10.9; rv:39.0) Gecko/20100101 Firefox/39.0"
   },
   "device":{
      "category":"Desktop",
      "type":"Desktop",
      "model":"PC",
      "version":""
   },
   "isMobile":true,
   "os":{
      "name":"Mac OS X",
      "version":"10"
   },
   "year":2015,
   "month":7,
   "day":22,
   "hour":14,
   "minutes":1
}
```

## Candidato archivio esempi granite.emulators {#granite-emulators-sample-store-candidate}

L&#39;archivio di esempio granite.emulators memorizza le informazioni sui dispositivi client.

### Percorso di origine {#source-location-emulators}

`/libs/settings/cloudsettings/legacy/contexthub/emulators`

### Implementazione di base {#base-implementation-emulators}

Il candidato dell’archivio contexthub.geolocation estende [`ContextHub.Store.PersistedStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore).

### Configurazione {#configuration-emulators}

La configurazione predefinita include un array denominato `defaultEmulators` che contiene informazioni su dispositivi diversi. Quando crei un archivio, fornisci diversi profili dispositivo nella proprietà Configurazione dettagli, utilizzando il formato illustrato nell’esempio seguente:

```xml
{
   "defaultEmulators":[
        {
            "id": "iphone-6",
            "title": "iPhone 6",
            "type": "mobile",
            "platform": "iOS",
            "platformVersion": "8.1.3",
            "width": 750,
            "height": 1334,
            "canRotate": true,
            "orientation": "Portrait",
            "device-pixel-ratio": 2
        },
        {
            "id": "iphone-6-plus",
            "title": "iPhone 6 Plus",
            "type": "mobile",
            "platform": "iOS",
            "platformVersion": "8.1.3",
            "width": 1080,
            "height": 1920,
            "canRotate": true,
            "orientation": "Portrait",
            "device-pixel-ratio": 3
        },
        {
            "id": "galaxy-s4",
            "title": "Samsung Galaxy S4",
            "type": "mobile",
            "platform": "Android",
            "platformVersion": "4.4.2 KitKat",
            "width": 1080,
            "height": 1920,
            "canRotate": true,
            "orientation": "Portrait",
            "device-pixel-ratio": 3
        }
    ]
}
```

### Elementi dati {#data-items-emulators}

La struttura dati dell&#39;archivio è simile all&#39;esempio seguente:

```xml
{
   "devices":[
      {"id":"native",
      "title":"Native",
      "type":"screen",
      "width":1395,
      "height":374,
      "orientation":"Landscape",
      "platform":"Mac OS X",
      "platformVersion":"10",
      "canRotate":false
      },
      {"id":"ipad-3",
      "title":"iPad 3 / 4 / Air",
      "type":"tablet",
      "platform":"iOS",
      "platformVersion":"8.1.3",
      "width":1536,
      "height":2048,
      "canRotate":true,
      "orientation":"Portrait",
      "device-pixel-ratio":2
      },
      {"id":"iphone-6",
      "title":"iPhone 6",
      "type":"mobile",
      "platform":"iOS",
      "platformVersion":"8.1.3",
      "width":750,
      "height":1334,
      "canRotate":true,
      "orientation":"Portrait",
      "device-pixel-ratio":2
      },
      {"id":"galaxy-s4",
      "title":"Samsung Galaxy S4",
      "type":"mobile",
      "platform":"Android",
      "platformVersion":"4.4.2 KitKat",
      "width":1080,
      "height":1920,
      "canRotate":true,
      "orientation":"Portrait",
      "device-pixel-ratio":3
      }
   ],
   "currentDeviceId":"native",
   "orientations":[
      {"id":"landscape",
      "title":"Landscape"
      },
      {"id":"portrait",
       "title":"Portrait"
      }
   ],
   "currentDevice":{
      "id":"native",
      "title":"Native",
      "type":"screen",
      "width":1395,
      "height":374,
      "orientation":"Landscape",
      "platform":"Mac OS X",
      "platformVersion":"10",
      "canRotate":false
   }
}
```

## Candidato all’archivio di campioni di granite.profile {#granite-profile-sample-store-candidate}

Memorizza informazioni sull&#39;utente corrente.

### Percorso di origine {#source-location-profile}

`/libs/settings/cloudsettings/legacy/contexthub/profile`

### Implementazione di base {#base-implementation-profile}

Il candidato dell’archivio contexthub.datetime estende [`ContextHub.Store.PersistedJSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore).

### Configurazione {#configuration-profile}

Viene utilizzata la seguente configurazione predefinita. Non modificare questa configurazione.

```xml
{
   "service":{
      "jsonp":false,
      "timeout":1000,
      "path":"${contexthub:/store/profile/path}.infinity.json"
   },
   "initialValues":{"path":"/home/users/a/anonymous"}
}
```

### Elementi dati {#data-items-profile}

Gli archivi che utilizzano questo candidato hanno una struttura dati simile a quella del seguente esempio:

```xml
{
   "displayName":"anonymous",
   "path":"/home/users/6/6zavE_DGre6Ad9Y5E0Ba",
   "avatar":"/etc/designs/default/images/social/avatar.png",
   "authorizableId":"anonymous"
}
```
