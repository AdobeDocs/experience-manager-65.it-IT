---
title: Configurazione di ContextHub
seo-title: Configurazione di ContextHub
description: Scopri come configurare Context Hub.
seo-description: Scopri come configurare Context Hub.
uuid: f2988bb9-6878-42a2-bb51-c3f8683248c5
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
translation-type: tm+mt
source-git-commit: a8ba56849f6bb9f0cf6571fc51f4b5cae71620e0
workflow-type: tm+mt
source-wordcount: '1850'
ht-degree: 1%

---


# Configurazione di ContextHub {#configuring-contexthub}

ContextHub è un framework per la memorizzazione, la manipolazione e la presentazione dei dati contestuali. Per ulteriori informazioni su ContextHub, consulta la documentazione [per](/help/sites-developing/contexthub.md)gli sviluppatori. ContextHub sostituisce Client Context [](/help/sites-administering/client-context.md) nell&#39;interfaccia utente touch.

Configurate la barra degli strumenti [ContextHub](/help/sites-developing/contexthub.md) per controllare se viene visualizzata in modalità Anteprima, per creare store ContextHub e aggiungere moduli di interfaccia tramite l’interfaccia utente ottimizzata per il tocco.

## Disattivazione di ContextHub {#disabling-contexthub}

Per impostazione predefinita, ContextHub è attivato in un&#39;installazione AEM. ContextHub può essere disattivato per impedire il caricamento di js/css e l&#39;inizializzazione. Esistono due opzioni per disabilitare ContextHub:

* Modificate la configurazione di ContextHub e verificate l&#39;opzione **Disattiva ContextHub**

   1. Nella barra laterale fate clic o toccate **Strumenti > Siti > ContextHub**
   1. Tocca o fai clic sul contenitore **di configurazione predefinito**
   1. Selezionate la configurazione **** ContextHub e toccate o fate clic su **Modifica elemento selezionato**
   1. Tocca o fai clic su **Disattiva ContextHub** e tocca o fai clic su **Salva**

o

* Utilizzare CRXDE Lite per impostare la proprietà `disabled` su **true** in `/libs/settings/cloudsettings`

>[!NOTE]
>
>[A causa della ristrutturazione del repository in AEM 6.4,](/help/sites-deploying/repository-restructuring.md) la posizione delle configurazioni ContextHub è cambiata da `/etc/cloudsettings` a:
>
> * `/libs/settings/cloudsettings`
> * `/conf/global/settings/cloudsettings`
> * `/conf/<tenant>/settings/cloudsettings`


## Visualizzazione e disattivazione dell’interfaccia utente ContextHub {#showing-and-hiding-the-contexthub-ui}

Configurate il servizio OSGi  Adobe di Granite ContextHub per mostrare o nascondere l’interfaccia utente [](/help/sites-authoring/ch-previewing.md) ContextHub sulle pagine. Il PID di questo servizio è `com.adobe.granite.contexthub.impl.ContextHubImpl.`

Per configurare il servizio è possibile utilizzare la console [](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) Web o utilizzare un nodo [JCR nell&#39;archivio](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository):

* **Console Web:** Per visualizzare l&#39;interfaccia utente, selezionare la proprietà Mostra interfaccia utente. Per nascondere l&#39;interfaccia utente, deselezionare la proprietà Nascondi interfaccia utente.
* **Nodo JCR:** Per visualizzare l&#39;interfaccia utente, impostare la `com.adobe.granite.contexthub.show_ui` proprietà booleana su `true`. Per nascondere l’interfaccia utente, impostare la proprietà su `false`.

Quando viene visualizzata l’interfaccia utente ContextHub, questa viene visualizzata solo sulle pagine AEM istanze dell’autore. L’interfaccia utente non viene visualizzata sulle pagine delle istanze pubblicate.

## Aggiunta di modalità e moduli dell’interfaccia utente ContextHub {#adding-contexthub-ui-modes-and-modules}

Configurare le modalità e i moduli dell’interfaccia utente visualizzati nella barra degli strumenti ContextHub in modalità Anteprima:

* Modalità interfaccia utente: Gruppi di moduli correlati
* Moduli: Widget che espongono i dati contestuali da uno store e consentono agli autori di manipolare il contesto

Le modalità di interfaccia utente sono visualizzate come una serie di icone sul lato sinistro della barra degli strumenti. Quando è selezionata questa opzione, i moduli di una modalità di interfaccia vengono visualizzati a destra.

![chlimage_1-319](assets/chlimage_1-319.png)

Le icone sono riferimenti dalla libreria delle icone [Coral UI (interfaccia utente Coral)](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons).

### Aggiunta di una modalità di interfaccia {#adding-a-ui-mode}

Aggiungere una modalità di interfaccia utente ai moduli ContextHub correlati al gruppo. Quando create la modalità di interfaccia utente, fornite il titolo e l’icona che vengono visualizzati nella barra degli strumenti ContextHub.

1. Nella barra  Experience Manager, fai clic o tocca Strumenti > Siti > Context Hub.
1. Tocca o fai clic sul contenitore di configurazione predefinito.
1. Tocca o fai clic su Configurazione Context Hub.
1. Tocca o fai clic sul pulsante Crea, quindi tocca o fai clic su Modalità interfaccia utente Context Hub.

   ![chlimage_1-320](assets/chlimage_1-320.png)

1. Immettete i valori per le seguenti proprietà:

   * Titolo modalità interfaccia utente: Titolo che identifica la modalità di interfaccia
   * Icona modalità: Selettore per l’icona [dell’interfaccia](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons) Coral da usare, ad esempio `coral-Icon--user`
   * Abilitato: Selezionate questa opzione per visualizzare la modalità dell’interfaccia utente nella barra degli strumenti ContextHub

1. Tocca o fai clic su Salva.

### Aggiunta di un modulo dell&#39;interfaccia utente {#adding-a-ui-module}

Aggiungete un modulo dell’interfaccia utente ContextHub a una modalità dell’interfaccia utente in modo che venga visualizzato nella barra degli strumenti ContextHub per visualizzare l’anteprima del contenuto della pagina. Quando si aggiunge un modulo dell&#39;interfaccia utente, si sta creando un&#39;istanza di un tipo di modulo registrato con ContextHub. Per aggiungere un modulo dell&#39;interfaccia utente, è necessario conoscere il nome del tipo di modulo associato.

AEM fornisce un tipo di modulo dell&#39;interfaccia utente di base e diversi tipi di moduli dell&#39;interfaccia utente di esempio sui quali è possibile basare un modulo dell&#39;interfaccia utente. Nella tabella seguente è riportata una breve descrizione di ciascuno di essi. Per informazioni sullo sviluppo di un modulo di interfaccia utente personalizzato, consultate [Creazione di moduli](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types)di interfaccia utente ContextHub.

Le proprietà del modulo dell&#39;interfaccia utente includono una configurazione di dettaglio in cui è possibile specificare i valori per le proprietà specifiche del modulo. Fornite la configurazione dei dettagli in formato JSON. La colonna Tipo di modulo nella tabella contiene collegamenti verso informazioni sul codice JSON richiesto per ciascun tipo di modulo dell’interfaccia utente.

| Tipo modulo | Descrizione | Store |
|---|---|---|
| [contexthub.base](/help/sites-developing/ch-samplemodules.md#contexthub-base-ui-module-type) | Tipo di modulo interfaccia utente generico | Configurate nelle proprietà del modulo dell&#39;interfaccia utente |
| [contexthub.browserinfo](/help/sites-developing/ch-samplemodules.md#contexthub-browserinfo-ui-module-type) | Visualizza informazioni sul browser | surferinfo |
| [contexthub.datetime](/help/sites-developing/ch-samplemodules.md#contexthub-datetime-ui-module-type) | Visualizza informazioni su data e ora | datetime |
| [contexthub.device](/help/sites-developing/ch-samplemodules.md#contexthub-device-ui-module-type) | Visualizzare il dispositivo client | emulatori |
| [contexthub.location](/help/sites-developing/ch-samplemodules.md#contexthub-location-ui-module-type) | Visualizza la latitudine e la longitudine del client, nonché la posizione su una mappa. Consente di cambiare la posizione. | geolocalizzazione |
| [contexthub.screen-orientation](/help/sites-developing/ch-samplemodules.md#contexthub-screen-orientation-ui-module-type) | Visualizza l&#39;orientamento dello schermo del dispositivo (orizzontale o verticale) | emulatori |
| [contexthub.tagcloud](/help/sites-developing/ch-samplemodules.md#contexthub-tagcloud-ui-module-type) | Visualizza statistiche sui tag pagina | tagcloud |
| [granite.profile](/help/sites-developing/ch-samplemodules.md#granite-profile-ui-module-type) | Visualizza le informazioni del profilo per l’utente corrente, inclusi AuthorizableID, displayName e familyName. È possibile modificare il valore di displayName e familyName. | profilo |

1. Nella barra  Experience Manager, fai clic o tocca Strumenti > Siti > ContextHub.
1. Tocca o fai clic sul Contenitore di configurazione al quale vuoi aggiungere un modulo di interfaccia utente.
1. Fate clic o digitate la configurazione ContextHub alla quale desiderate aggiungere il modulo dell&#39;interfaccia utente.
1. Tocca o fai clic sulla modalità dell’interfaccia a cui stai aggiungendo il modulo dell’interfaccia utente.
1. Tocca o fai clic sul pulsante Crea, quindi tocca o fai clic su Modulo interfaccia utente ContextHub (generico).

   ![chlimage_1-321](assets/chlimage_1-321.png)

1. Immettete i valori per le seguenti proprietà:

   * Titolo modulo interfaccia utente: Titolo che identifica il modulo dell&#39;interfaccia utente
   * Tipo di modulo: Tipo di modulo
   * Abilitato: Selezionare questa opzione per visualizzare il modulo dell&#39;interfaccia utente nella barra degli strumenti ContextHub

1. (Facoltativo) Per ignorare la configurazione predefinita dello store, immettete un oggetto JSON per configurare il modulo dell&#39;interfaccia utente.
1. Tocca o fai clic su Salva.

## Creazione di un archivio ContextHub {#creating-a-contexthub-store}

Create un archivio Context Hub per mantenere i dati utente e accedere ai dati in base alle esigenze. Gli store ContextHub si basano sui candidati store registrati. Quando create lo store, è necessario il valore di storeType con cui è stato registrato il candidato. Consultate [Creazione di candidati](/help/sites-developing/ch-extend.md#creating-custom-store-candidates)store personalizzati.

### Configurazione dettagliata dello store {#detailed-store-configuration}

Quando configurate uno store, la proprietà Configurazione dettagli consente di fornire valori per proprietà specifiche dello store. Il valore si basa sul `config` parametro della `init` funzione dello store. Pertanto, la necessità di fornire questo valore e il formato del valore dipende dallo store.

Il valore della proprietà Configurazione dettagli è un `config` oggetto in formato JSON.

### Candidati store di esempio {#sample-store-candidates}

AEM fornisce i seguenti esempi di store candidati ai quali potete basare uno store.

| Tipo di archivio | Descrizione |
|---|---|
| [aem.segmentation](/help/sites-developing/ch-samplestores.md#aem-segmentation-sample-store-candidate) | Memorizzazione per segmenti ContextHub risolti e non risolti. Recupera automaticamente i segmenti da ContextHub SegmentManager |
| [aem.resolvedsegment](/help/sites-developing/ch-samplestores.md#aem-resolvedsegments-sample-store-candidate) | Memorizza i segmenti attualmente risolti. Ascolta il servizio ContextHub SegmentManager per aggiornare automaticamente lo store |
| [contexthub.geolocation](/help/sites-developing/ch-samplestores.md#contexthub-geolocation-sample-store-candidate) | Memorizza la latitudine e la longitudine della posizione del browser. |
| [contexthub.datetime](/help/sites-developing/ch-samplestores.md#contexthub-datetime-sample-store-candidate) | Memorizza la data, l&#39;ora e la stagione correnti per la posizione del browser |
| [granite.emulators](/help/sites-developing/ch-samplestores.md#granite-emulators-sample-store-candidate) | Definisce proprietà e funzionalità per un certo numero di dispositivi e rileva il dispositivo client corrente |
| [contexthub.Generic-jsonp](/help/sites-developing/ch-samplestores.md#contexthub-generic-jsonp-sample-store-candidate) | Recupera e memorizza i dati da un servizio JSONP |
| [granite.profile](/help/sites-developing/ch-samplestores.md#granite-profile-sample-store-candidate) | Memorizza i dati del profilo per l&#39;utente corrente |
| [contexthub.surferinfo](/help/sites-developing/ch-samplestores.md#contexthub-surferinfo-sample-store-candidate) | Memorizza informazioni sul client, quali informazioni sul dispositivo, tipo di browser e orientamento della finestra |
| [contexthub.tagcloud](/help/sites-developing/ch-samplestores.md#contexthub-tagcloud-sample-data-store) | Memorizza i tag e i conteggi dei tag delle pagine |

1. Nella barra  Experience Manager, fai clic o tocca Strumenti > Siti > ContextHub.
1. Tocca o fai clic sul contenitore di configurazione predefinito.
1. Tocca o fai clic su Configurazione contestub
1. Per aggiungere uno store, tocca o fai clic sull&#39;icona Crea, quindi tocca o fai clic su Configurazione store ContexHub.

   ![chlimage_1-322](assets/chlimage_1-322.png)

1. Immettete i valori per le proprietà di configurazione di base, quindi fate clic o toccate Avanti:

   * **Titolo configurazione:** Titolo che identifica lo store
   * **Tipo store:** Il valore della proprietà storeType del candidato store su cui basare lo store
   * **Obbligatorio:** Select
   * **Abilitato:** Selezionare per abilitare lo store

1. (Facoltativo) Per ignorare la configurazione predefinita dello store, immettete un oggetto JSON nella casella Configurazione dettagli (JSON).
1. Tocca o fai clic su Salva.

## Esempio: Utilizzo di un servizio JSONP  {#example-using-a-jsonp-service}

Questo esempio illustra come configurare uno store e visualizzare i dati in un modulo dell&#39;interfaccia utente. In questo esempio, il servizio MD5 del sito jsontest.com viene utilizzato come origine dati per uno store. Il servizio restituisce il codice hash MD5 di una stringa specificata, in formato JSON.

Un archivio contestexthub.Generic-jsonp è configurato in modo da memorizzare i dati per la chiamata al servizio `https://md5.jsontest.com/?text=%22text%20to%20md5%22`. Il servizio restituisce i seguenti dati visualizzati in un modulo dell&#39;interfaccia utente:

```xml
{
   "md5": "919a56ab62b6d5e1219fe1d95248a2c5",
   "original": "\"text to md5\""
}
```

### Creazione di un archivio contestexthub.Generic-jsonp {#creating-a-contexthub-generic-jsonp-store}

Il candidato per l&#39;archivio di esempio contexthub.Generic-jsonp consente di recuperare dati da un servizio JSONP o da un servizio Web che restituisce dati JSON. Per questo store candidato, utilizzate la configurazione dello store per fornire dettagli sul servizio JSONP da utilizzare.

La funzione [init](/help/sites-developing/contexthub-api.md#init-name-config) della classe `ContextHub.Store.JSONPStore` Javascript definisce un `config` oggetto che inizializza il candidato store. L&#39; `config` oggetto contiene un `service` oggetto che include dettagli sul servizio JSONP. Per configurare lo store, fornite l&#39; `service` oggetto in formato JSON come valore per la proprietà Configurazione dettagli.

Per salvare i dati dal servizio MD5 del sito jsontest.com, utilizzate la procedura descritta in [Creazione di uno store](/help/sites-developing/ch-configuring.md#creating-a-contexthub-store) ContextHub con le seguenti proprietà:

* **Titolo configurazione:** md5
* **Tipo store:** contexthub.Generic-jsonp
* **Obbligatorio:** Select
* **Abilitato:** Select
* **Configurazione dettagli (JSON):**

   ```xml
   {
    "service": {
    "jsonp": false,
    "timeout": 1000,
    "ttl": 1800000,
    "secure": false,
    "host": "md5.jsontest.com",
    "port": 80,
    "params":{
    "text":"text to md5"
        }
      }
    }
   ```

### Aggiunta di un modulo dell’interfaccia utente per i dati md5 {#adding-a-ui-module-for-the-md-data}

Aggiungete un modulo dell’interfaccia utente alla barra degli strumenti ContextHub per visualizzare i dati memorizzati nell’archivio di esempio di md5. In questo esempio, il modulo contexthub.base viene utilizzato per generare il seguente modulo dell’interfaccia utente:

![chlimage_1-323](assets/chlimage_1-323.png)

Utilizzate la procedura descritta in [Aggiunta di un modulo](#adding-a-ui-module) dell&#39;interfaccia utente per aggiungere il modulo dell&#39;interfaccia utente a una modalità dell&#39;interfaccia utente esistente, ad esempio la modalità dell&#39;interfaccia utente di Perona. Per il modulo dell&#39;interfaccia utente, utilizzate i seguenti valori delle proprietà:

* **Titolo modulo interfaccia utente:** MD5
* **Tipo di modulo:** contexthub.base
* **Configurazione dettagli (JSON):**

   ```xml
   {
    "icon": "coral-Icon--data",
    "title": "MD5 Converstion",
    "storeMapping": { "md5": "md5" },
    "template": "<p> {{md5.original}}</p>;
                 <p>{{md5.md5}}</p>"
   }
   ```

## Debug di ContextHub {#debugging-contexthub}

È possibile abilitare una modalità di debug per ContextHub per consentire la risoluzione dei problemi. La modalità di debug può essere abilitata tramite la configurazione ContextHub o tramite CRXDE.

### Tramite la configurazione {#via-the-configuration}

Modificare la configurazione di ContextHub e selezionare l&#39;opzione **Debug**

1. Nella barra laterale fate clic o toccate **Strumenti > Siti > ContextHub**
1. Tocca o fai clic sul contenitore **di configurazione predefinito**
1. Selezionate la configurazione **** ContextHub e toccate o fate clic su **Modifica elemento selezionato**
1. Tocca o fai clic su **Debug** e tocca o fai clic su **Salva**

### Via CRXDE {#via-crxde}

Utilizzare CRXDE Lite per impostare la proprietà `debug` su **true** in:

* `/conf/global/settings/cloudsettings` o
* `/conf/<tenant>/settings/cloudsettings`

>[!NOTE]
>
>Per le configurazioni ContextHub ancora presenti nei percorsi legacy, la posizione da impostare `debug property` è `/libs/settings/cloudsettings/legacy/contexthub`.

### Modalità silenziosa {#silent-mode}

La modalità silenziosa sopprime tutte le informazioni di debug. A differenza della normale opzione di debug, che può essere impostata in modo indipendente per ogni configurazione ContextHub, la modalità silenziosa è un&#39;impostazione globale che ha precedenza rispetto a qualsiasi impostazione di debug a livello di configurazione ContextHub.

Questa funzione è utile per l’istanza di pubblicazione, in cui non sono necessarie informazioni di debug. Poiché è un’impostazione globale, è abilitata tramite OSGi.

1. Apri la configurazione **della console Web di** Adobe Experience Manager in `http://<host>:<port>/system/console/configMgr`
1. Ricerca **Adobe Granite ContextHub**
1. Fai clic sulla configurazione **Adobe Granite ContextHub** per modificarne le proprietà
1. Selezionate l’opzione Modalità **** invisibile e fate clic su **Salva**

## Ripristino delle configurazioni ContextHub dopo l&#39;aggiornamento {#recovering-contexthub-configurations-after-upgrading}

Quando si esegue un [aggiornamento a AEM](/help/sites-deploying/upgrade.md) , le configurazioni ContextHub vengono sottoposte a backup e memorizzate in una posizione sicura. Durante l&#39;aggiornamento, vengono installate le configurazioni ContextHub predefinite, sostituendo le configurazioni esistenti. Il backup è necessario per mantenere eventuali modifiche o aggiunte apportate.

Le configurazioni ContextHub sono memorizzate in una cartella denominata `contexthub` sotto i nodi seguenti:

* `/conf/global/settings/cloudsettings`
* `/conf/<tenant>/settings/cloudsettings`

Dopo un aggiornamento, il backup viene memorizzato in una cartella denominata `contexthub` sotto il nodo denominato:

`/conf/global/settings/cloudsettings/default-pre-upgrade_yyyymmdd_xxxxxxx` o
`/conf/<tenant>/settings/cloudsettings/default-pre-upgrade_yyyymmdd_xxxxxxx`

La `yyyymmdd` parte del nome del nodo è la data in cui è stato eseguito l&#39;aggiornamento.

Per ripristinare le configurazioni ContextHub, utilizza il CRXDE Lite per copiare i nodi che rappresentano i tuoi store, le modalità di interfaccia utente e i moduli di interfaccia dall&#39;area sotto il `default-pre-upgrade_yyyymmdd_xxxxxx` nodo al di sotto:

* `/conf/global/settings/cloudsettings` o
* `/conf/<tenant>/settings/cloudsettings`
