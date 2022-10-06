---
title: Creazione di siti per dispositivi mobili
seo-title: Creating Sites for Mobile Devices
description: La creazione di un sito mobile è simile alla creazione di un sito standard, in quanto comporta anche la creazione di modelli e componenti
seo-description: Creating a mobile site is similar to creating a standard site as it also involves creating templates and components
uuid: 6b19042c-03f1-4e33-970e-475f9fb8c5fb
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: 0aabfb0a-ef9c-4b06-b698-61cad101c3c1
docset: aem65
legacypath: /content/docs/en/aem/6-0/develop/mobile/mobile
exl-id: 21b2037a-685a-441d-aecd-865884253e03
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3840'
ht-degree: 1%

---

# Creazione di siti per dispositivi mobili{#creating-sites-for-mobile-devices}

>[!NOTE]
>
>Adobe consiglia di utilizzare l’editor di SPA per i progetti che richiedono il rendering lato client basato sul framework di un’applicazione a pagina singola (ad esempio, React). [Per saperne di più](/help/sites-developing/spa-overview.md).

La creazione di un sito mobile è simile alla creazione di un sito standard, in quanto comporta anche la creazione di modelli e componenti. Per ulteriori dettagli sulla creazione di modelli e componenti, consulta le pagine seguenti: [Modelli](/help/sites-developing/templates.md), [Componenti](/help/sites-developing/components.md) e [Guida introduttiva allo sviluppo per AEM Sites](/help/sites-developing/getting-started.md). La differenza principale consiste nell’abilitare le funzionalità mobili integrate AEM all’interno del sito. Viene ottenuto creando un modello basato sul componente della pagina mobile.

È inoltre consigliabile utilizzare [design dinamico](/help/sites-developing/responsive.md), creazione di un singolo sito che supporti diverse dimensioni dello schermo.

Per iniziare, puoi dare un&#39;occhiata al **Sito demo mobile We.Retail** disponibile in AEM.

Per creare un sito mobile, procedi come segue:

1. Crea il componente pagina:

   * Imposta la `sling:resourceSuperType` proprietà di `wcm/mobile/components/page`
In questo modo il componente si basa sul componente della pagina mobile.

   * Crea il `body.jsp` con la logica specifica del progetto.

1. Crea il modello di pagina:

   * Imposta la `sling:resourceType` al componente pagina appena creato.
   * Imposta la `allowedPaths` proprietà.

1. Crea la pagina di progettazione del sito.
1. Crea la pagina principale del sito sotto la `/content` nodo:

   * Imposta la `cq:allowedTemplates` proprietà.
   * Imposta la `cq:designPath` proprietà.

1. Nelle proprietà della pagina principale del sito, imposta i gruppi di dispositivi nella **Mobile** scheda .
1. Crea le pagine del sito utilizzando il nuovo modello.

Il componente Pagina mobile ( `/libs/wcm/mobile/components/page`):

* Aggiunge la **Mobile** nella finestra di dialogo delle proprietà della pagina.
* Attraverso le sue `head.jsp`, recupera il gruppo di dispositivi mobili corrente dalla richiesta e, se viene trovato un gruppo di dispositivi, utilizza il gruppo `drawHead()` per includere il componente init dell&#39;emulatore associato del gruppo di dispositivi (solo in modalità di authoring) e il CSS di rendering del gruppo di dispositivi.

>[!NOTE]
>
>La pagina principale del sito mobile deve essere al livello 1 della gerarchia dei nodi e si consiglia di essere al di sotto del nodo /content.

## Creazione di un sito mobile con Multi Site Manager {#creating-a-mobile-site-with-the-multi-site-manager}

Multi Site Manager (MSM) consente di creare una Live Copy mobile da un sito standard. Il sito standard viene automaticamente trasformato in un sito mobile: il sito mobile dispone di tutte le funzioni dei siti mobili (ad es. edizione all’interno di un emulatore) e può essere gestito in sincronia con il sito standard. Consulta la sezione . [Creazione di una Live Copy per canali diversi](/help/sites-administering/msm.md) nella pagina Multi Site Manager (Gestore siti multipli).

## API mobile lato server {#server-side-mobile-api}

I pacchetti Java contenenti le classi mobile sono:

* [com.day.cq.wcm.mobile.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html) - definisce MobileConstants.
* [com.day.cq.wcm.mobile.api.device](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/package-summary.html) - definisce Device, DeviceGroup e DeviceGroupList.
* [com.day.cq.wcm.mobile.api.device.funzionalità](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html) - definisce DeviceCapability.
* [com.day.cq.wcm.mobile.api.wurfl](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/api/package-summary.html) - definisce WurflQueryEngine.
* [com.day.cq.wcm.mobile.core](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/core/package-summary.html) - definisce MobileUtil, che fornisce vari metodi di utilità ruotanti intorno a WCM Mobile.

### Componenti per dispositivi mobili {#mobile-components}

La **Sito demo mobile We.Retail** utilizza i seguenti componenti mobili che si trovano di seguito `/libs/foundation/components`:

<table>
 <tbody>
  <tr>
   <td>Nome</td>
   <td>Gruppo</td>
   <td>Caratteristiche</td>
  </tr>
  <tr>
   <td>piè di pagina mobile</td>
   <td>nascosto</td>
   <td>- piè di pagina</td>
  </tr>
  <tr>
   <td>mobile</td>
   <td>Mobile</td>
   <td>- in base al componente di base dell’immagine<br /> - esegue il rendering di un'immagine se il dispositivo è in grado di<br /> </td>
  </tr>
  <tr>
   <td>mobilista</td>
   <td>Mobile</td>
   <td>- in base al componente di base dell'elenco<br /> - listitem_teaser.jsp esegue il rendering di un'immagine se il dispositivo è in grado di<br /> </td>
  </tr>
  <tr>
   <td>mobilelogo</td>
   <td>nascosto</td>
   <td>- basato sul componente di base del logo<br /> - esegue il rendering di un'immagine se il dispositivo è in grado di<br /> </td>
  </tr>
  <tr>
   <td>mobilità</td>
   <td>Mobile</td>
   <td><p>- simile al componente di base di riferimento</p> <p>- mappa un componente di testo in un modello mobile e un componente immagine in un elemento mobile</p> </td>
  </tr>
  <tr>
   <td>mobiletextimage</td>
   <td>Mobile</td>
   <td>- in base al componente di base del testo<br /> - esegue il rendering di un'immagine se il dispositivo è in grado di</td>
  </tr>
  <tr>
   <td>mobiletopnav</td>
   <td>nascosto</td>
   <td><p>- in base al componente di base della navigazione principale</p> <p>- esegue il rendering solo del testo</p> </td>
  </tr>
 </tbody>
</table>

#### Creazione di un componente mobile {#creating-a-mobile-component}

Il framework mobile AEM consente di sviluppare componenti sensibili al dispositivo che emette la richiesta. Gli esempi di codice seguenti mostrano come utilizzare l’API mobile AEM in un jsp componente e in particolare come:

* Ottieni il dispositivo dalla richiesta:
   `Device device = slingRequest.adaptTo(Device.class);`

* Ottieni il gruppo di dispositivi:
   `DeviceGroup deviceGroup = device.getDeviceGroup();`

* Ottieni le funzionalità del gruppo di dispositivi:
   `Collection<DeviceCapability> capabilities = deviceGroup.getCapabilities();`

* Ottenere gli attributi del dispositivo (chiave/valori di funzionalità non elaborati dal database WURFL):
   `Map<String,String> deviceAttributes = device.getAttributes();`

* Ottieni l&#39;agente utente del dispositivo:
   `String userAgent = device.getUserAgent();`

* Ottieni l’elenco dei gruppi di dispositivi (gruppi di dispositivi assegnati al sito dall’autore) dalla pagina corrente:
   `DeviceGroupList deviceGroupList = currentPage.adaptTo(DeviceGroupList.class);`

* Controlla se il gruppo di dispositivi supporta le immagini
   `if (deviceGroup.hasCapability(DeviceCapability.CAPABILITY_IMAGES)) {`
...
OPPURE

...   `if MobileUtil.hasCapability(request, DeviceCapability.CAPABILITY_IMAGES) {`
...

>[!NOTE]
>
>In un jsp, `slingRequest` è disponibile tramite `<sling:defineObjects>` tag e `currentPage` attraverso `<cq:defineObjects>` tag .

### Emulatori {#emulators}

L’authoring basato su emulatore offre agli autori gli strumenti per creare pagine di contenuto destinate ai clienti mobili. L’authoring dei contenuti mobili segue lo stesso principio dell’editing WYSIWYG sul posto. Affinché gli autori possano percepire l’aspetto della pagina su un dispositivo mobile, una pagina di contenuto mobile viene modificata utilizzando un emulatore del dispositivo.

Gli emulatori per dispositivi mobili si basano sul framework di emulatori generici. Per ulteriori informazioni, consulta la sezione [Emulatori](/help/sites-developing/emulators.md) pagina.

L’emulatore del dispositivo visualizza il dispositivo mobile sulla pagina, mentre la modifica standard (parsys, components) si verifica all’interno dello schermo del dispositivo. L’emulatore del dispositivo dipende dai gruppi di dispositivi configurati per il sito. È possibile assegnare più emulatori a un gruppo di dispositivi. Tutti gli emulatori sono quindi disponibili nella pagina del contenuto. Per impostazione predefinita viene visualizzato il primo emulatore assegnato al primo gruppo di dispositivi assegnato al sito. Gli emulatori possono essere attivati tramite il carosello dell’emulatore nella parte superiore della pagina o tramite il pulsante di modifica della barra laterale.

**Creazione di un emulatore**

Per creare un emulatore, fai riferimento al [Creazione di un emulatore mobile personalizzato](/help/sites-developing/emulators.md) nella pagina emulatori generici.

**Caratteristiche principali degli emulatori mobili**

* Un gruppo di dispositivi è composto da uno o più emulatori: la pagina di configurazione del gruppo di dispositivi, ad esempio /etc/mobile/groups/touch, contiene il `emulators` sotto la proprietà `jcr:content` nodo.
Nota: anche se è possibile che lo stesso emulatore appartenga a diversi gruppi di dispositivi, non ha molto senso.

* Tramite la finestra di dialogo di configurazione del gruppo di dispositivi, il `emulators` viene impostata con il percorso dell&#39;emulatore o degli emulatori desiderati. Esempio: `/libs/wcm/mobile/components/emulators/iPhone4`.

* Componenti dell’emulatore (ad es. `/libs/wcm/mobile/components/emulators/iPhone4`) estende il componente emulatore mobile di base ( `/libs/wcm/mobile/components/emulators/base`).

* Ogni componente che estende l’emulatore mobile di base è disponibile per la selezione durante la configurazione di un gruppo di dispositivi. Gli emulatori personalizzati possono quindi essere facilmente creati o estesi.
* Al momento della richiesta in modalità di modifica, l’implementazione dell’emulatore viene utilizzata per eseguire il rendering della pagina.
* Quando il modello della pagina si basa sul componente della pagina mobile, le funzionalità dell’emulatore vengono integrate automaticamente nella pagina (tramite il `head.jsp` del componente pagina mobile).

### Gruppi dispositivo {#device-groups}

I gruppi di dispositivi mobili forniscono la segmentazione dei dispositivi mobili in base alle funzionalità del dispositivo. Un gruppo di dispositivi fornisce le informazioni necessarie per l’authoring basato su emulatore sull’istanza di authoring e per il rendering corretto dei contenuti sull’istanza di pubblicazione: una volta che gli autori hanno aggiunto il contenuto alla pagina mobile e l’hanno pubblicata, la pagina può essere richiesta nell’istanza di pubblicazione. Qui, invece della visualizzazione di modifica dell’emulatore, la pagina di contenuto viene riprodotta utilizzando uno dei gruppi di dispositivi configurati. La selezione del gruppo di dispositivi si verifica in base a [rilevamento dispositivi mobili](#devicedetection). Il gruppo di dispositivi corrispondente fornisce quindi le informazioni sullo stile necessarie.

I gruppi di dispositivi sono definiti come pagine di contenuto sottostanti `/etc/mobile/devices` e utilizza **Gruppo di dispositivi mobili** modello. Il modello gruppo dispositivi funge da modello di configurazione per le definizioni dei gruppi di dispositivi sotto forma di pagine di contenuto. Le sue principali caratteristiche sono:

* Dove si trova: `/libs/wcm/mobile/templates/devicegroup`
* Percorso consentito: `/etc/mobile/groups/*`
* Componente Pagina: `wcm/mobile/components/devicegroup`

#### Assegnazione di gruppi di dispositivi al sito {#assigning-device-groups-to-your-site}

Quando crei un sito mobile, devi assegnare gruppi di dispositivi al sito. AEM fornisce tre gruppi di dispositivi a seconda delle capacità di rendering HTML e JavaScript del dispositivo:

* **Funzione** telefoni, per dispositivi con funzionalità quali Sony Ericsson W800 con supporto per HTML di base, ma senza supporto per immagini e JavaScript.
* **Smart** telefoni, per dispositivi come Blackberry con supporto per HTML e immagini di base, ma senza supporto per JavaScript.

* **Touch** telefoni, per dispositivi come iPad con supporto completo per HTML, immagini, JavaScript e rotazione dei dispositivi.

Poiché gli emulatori possono essere associati a un gruppo di dispositivi (consulta la sezione [Creazione di un gruppo di dispositivi](#creating-a-device-group)), l’assegnazione di un gruppo di dispositivi a un sito consente agli autori di selezionare tra gli emulatori associati al gruppo di dispositivi per modificare la pagina.

Per assegnare un gruppo di dispositivi al sito:

1. Nel browser, passate alla console **Site Admin** (Amministrazione sito).
1. Apri la pagina principale del tuo sito mobile qui sotto **Siti Web**.
1. Apri le proprietà della pagina.
1. Seleziona la **Mobile** scheda:

   * Definisci i gruppi di dispositivi.
   * Fai clic su **OK**.

>[!NOTE]
>
>I gruppi di dispositivi definiti per un sito vengono ereditati da tutte le pagine del sito.

#### Filtri per gruppo dispositivo {#device-group-filters}

I filtri per gruppi di dispositivi definiscono criteri basati sulle funzionalità per determinare se un dispositivo appartiene al gruppo. Quando crei un gruppo di dispositivi, puoi selezionare i filtri da utilizzare per la valutazione dei dispositivi.

In fase di esecuzione quando AEM ricevuto una richiesta HTTP da un dispositivo, ogni filtro associato a un gruppo confronta le funzionalità del dispositivo con criteri specifici. Il dispositivo è considerato appartenente al gruppo quando dispone di tutte le funzionalità richieste dai filtri. Le funzionalità vengono recuperate dal database WURFL™.

I gruppi di dispositivi possono utilizzare zero o più filtri per il rilevamento delle funzionalità. Inoltre, un filtro può essere utilizzato con più gruppi di dispositivi. AEM fornisce un filtro predefinito che determina se il dispositivo dispone delle funzionalità selezionate per un gruppo:

* CSS
* Immagini JPG e PNG
* JavaScript
* Rotazione dispositivo

Se il gruppo di dispositivi non utilizza un filtro, le funzionalità selezionate configurate per il gruppo sono le uniche funzionalità richieste da un dispositivo.

Per ulteriori informazioni, consulta [Creazione di filtri per i gruppi di dispositivi](/help/sites-developing/groupfilters.md).

#### Creazione di un gruppo di dispositivi {#creating-a-device-group}

Crea un gruppo di dispositivi quando i gruppi che AEM installati non soddisfano le tue esigenze.

1. Nel browser, vai alla pagina **Strumenti** console.
1. Crea una nuova pagina qui sotto **Strumenti** > **Mobile** > **Gruppi di dispositivi**. In **Crea pagina** finestra di dialogo:

   * Come **Titolo** enter `Special Phones`.

   * Come **Nome** enter `special`.

   * Seleziona la **Modello per gruppo di dispositivi mobili**.
   * Fai clic su **Crea**.

1. In CRXDE, aggiungi un **static.css** file contenente gli stili per il gruppo di dispositivi sotto il `/etc/mobile/groups/special` nodo.

1. Apri **Telefoni speciali** pagina.
1. Per configurare il gruppo di dispositivi, fai clic sul pulsante **Modifica** pulsante accanto **Impostazioni**.
Sulla **Generale** scheda:

   * **Titolo**: il nome del gruppo di dispositivi mobili.
   * **Descrizione**: descrizione del gruppo.
   * **Agente utente**: stringa dell&#39;agente utente con cui viene confrontata la corrispondenza dei dispositivi. È facoltativo e può essere un regex. Esempio: `BlackBerryZ10`
   * **Funzionalità**: definisce se il gruppo può gestire immagini, CSS, JavaScript o rotazione del dispositivo.
   * **Larghezza minima dello schermo** e **Altezza**
   * **Disattiva emulatore**: per abilitare/disabilitare l’emulatore durante la modifica del contenuto.

   Sulla **Emulatori** scheda:

   * **Emulatori**: selezionare gli emulatori assegnati a questo gruppo di dispositivi.

   Sulla **Filtri** scheda:

   * Per aggiungere un filtro, fai clic su Aggiungi elemento e seleziona un filtro dall’elenco a discesa.
   * I filtri vengono valutati nell’ordine in cui compaiono. Quando un dispositivo non soddisfa i criteri di un filtro, i filtri successivi nell’elenco non vengono valutati.



1. Fai clic su OK.

La finestra di dialogo di configurazione del gruppo di dispositivi mobili si presenta così:

![screen_shot_2012-02-01at22043pm](assets/screen_shot_2012-02-01at22043pm.png)

#### CSS personalizzati per gruppo di dispositivi {#custom-css-per-device-group}

Come descritto in precedenza, è possibile associare un CSS personalizzato a una pagina di gruppo di dispositivi, in modo analogo al CSS di una pagina di progettazione.Questo CSS viene utilizzato per influenzare il rendering specifico del gruppo di dispositivi del contenuto della pagina su autore e su pubblicazione.Questo CSS viene quindi incluso automaticamente:

* Nella pagina nell’istanza di authoring per ogni emulatore utilizzato da questo gruppo di dispositivi.
* Nella pagina dell’istanza di pubblicazione se l’agente utente della richiesta corrisponde a un dispositivo mobile in questo particolare gruppo di dispositivi.

## Rilevamento dei dispositivi lato server {#server-side-device-detection}

Utilizza i filtri e una libreria di specifiche del dispositivo per determinare le funzionalità del dispositivo che esegue la richiesta HTTP.

### Sviluppa filtri per i gruppi di dispositivi {#develop-device-group-filters}

Crea un filtro per gruppi di dispositivi per definire un set di requisiti di funzionalità per i dispositivi. Crea tutti i filtri necessari per eseguire il targeting dei gruppi di funzionalità del dispositivo necessari.

Progetta i filtri in modo da poter utilizzare combinazioni di questi per definire i gruppi di funzionalità. In genere, esiste una sovrapposizione delle funzionalità di diversi gruppi di dispositivi. Pertanto, puoi utilizzare alcuni filtri con più definizioni di gruppi di dispositivi.

Dopo aver creato un filtro, puoi utilizzarlo nella configurazione del gruppo.

Per informazioni, vai a [Creazione di filtri per i gruppi di dispositivi](/help/sites-developing/groupfilters.md).

### Utilizzo del database WURFL™ {#using-the-wurfl-database}

AEM utilizza una versione troncata del [WURFL](https://wurfl.sourceforge.net/)Database ™ per eseguire query sulle funzionalità dei dispositivi, ad esempio la risoluzione dello schermo o il supporto javascript, in base all&#39;User-Agent del dispositivo.

Il codice XML del database WURFL™ è rappresentato come nodi sotto `/var/mobile/devicespecs` analizzando le `wurfl.xml`file a `/libs/wcm/mobile/devicespecs/wurfl.xml.` L&#39;espansione ai nodi si verifica la prima volta che la `cq-mobile-core` bundle avviato.

Le funzionalità dei dispositivi sono memorizzate come proprietà dei nodi e i nodi rappresentano modelli di dispositivi. È possibile utilizzare le query per recuperare le funzionalità di un dispositivo o agente utente.

Poiché il database WURFL™ si sta evolvendo, potrebbe essere necessario personalizzarlo o sostituirlo. Per aggiornare il database dei dispositivi mobili sono disponibili le seguenti opzioni:

* Sostituisci il file con la versione più recente, se disponi di una licenza che consente questo utilizzo. Vedere Installazione di un database WURFL diverso.
* Utilizza la versione disponibile in AEM e configura un regexp che corrisponde alle stringhe Utente-Agente e punta a un dispositivo WURFL™ esistente. Vedi [Aggiunta di una corrispondenza utente-agente basata su regexp](#adding-a-regexp-based-user-agent-matching).

#### Verifica della mappatura di un agente utente alle funzionalità WURFL™ {#testing-the-mapping-of-a-user-agent-to-wurfl-capabilities}

Quando un dispositivo accede al sito mobile, AEM rileva il dispositivo, lo mappa a un gruppo di dispositivi in base alle sue funzionalità e invia una visualizzazione della pagina corrispondente al gruppo di dispositivi. Il gruppo di dispositivi corrispondente fornisce le informazioni sullo stile necessarie. Le mappature possono essere testate nella pagina di test dell’utente-agente mobile:

`https://localhost:4502/etc/mobile/useragent-test.html`

#### Installazione di un database WURFL™ diverso {#installing-a-different-wurfl-database}

Il database WURFL™ troncato installato con AEM è una versione precedente al 30 agosto 2011. Se la tua versione del WURFL è stata rilasciata dopo il 30 agosto 2011, assicurati che l’utilizzo sia conforme alla tua licenza.

Per installare un database WURFL™:

1. In CRXDE Lite, crea la cartella seguente: `/apps/wcm/mobile/devicespecs`
1. Copiare il file WURFL™ nella cartella.
1. Rinomina il file come `wurfl.xml`.

AEM analizza automaticamente le `wurfl.xml` e aggiorna i nodi sottostanti `/var/mobile/devicespecs`.

>[!NOTE]
>
>Quando il database WURFL™ completo è abilitato, l&#39;analisi e l&#39;attivazione potrebbero richiedere alcuni minuti. Per informazioni sull’avanzamento, puoi guardare i registri.

#### Aggiunta di una corrispondenza utente-agente basata su regexp {#adding-a-regexp-based-user-agent-matching}

Aggiungi un agente utente come espressione regolare sotto /apps/wcm/mobile/devicissues/wurfl/regexp per puntare a un tipo di dispositivo WURFL™ esistente.

1. In **CRXDE Lite**, crea un nodo sotto /apps/wcm/mobile/devicvisti/regexp, ad esempio apple_ipad_ver1.
1. Aggiungi le seguenti proprietà al nodo :

   * **rigexp**: espressione regolare che definisce gli agenti utente, ad esempio: .&#42;Mozilla.&#42;iPad.&#42;AppleWebKit.&#42;Safari.&#42;
   * **deviceId**: l&#39;ID dispositivo come definito nel wurfl.xml, ad esempio: apple_ipad_ver1

La configurazione di cui sopra fa sì che i dispositivi per i quali l&#39;utente-agente corrisponde all&#39;espressione regolare fornita siano mappati all&#39;ID dispositivo apple_ipad_ver1 WURFL™, se esiste.

## Rilevamento dei dispositivi lato client {#client-side-device-detection}

Questa sezione descrive come utilizzare il rilevamento lato client del dispositivo di AEM per ottimizzare il rendering della pagina o fornire al client versioni alternative del sito web.

AEM supporta il rilevamento lato client del dispositivo in base a `BrowserMap`. `BrowserMap` viene fornito in AEM come libreria client in `/etc/clientlibs/browsermap`.

`BrowserMap` fornisce tre strategie che è possibile utilizzare per fornire un sito web alternativo a un cliente, che vengono utilizzate nel seguente ordine:

1. [Collegamenti alternativi](#providing-alternate-links)
1. [URL specifico per il gruppo di dispositivi](#definingdevicegroupspecificurl)
1. [URL basato su selettore](#defining-selector-based-urls)

>[!NOTE]
>
>Per ulteriori informazioni sull’integrazione della libreria client, consulta la sezione [Utilizzo delle librerie HTML lato client](/help/sites-developing/clientlibs.md) sezione .

### Fornire collegamenti alternativi {#providing-alternate-links}

La `PageVariantsProvider` Il servizio OSGi è in grado di generare collegamenti alternativi per siti appartenenti alla stessa famiglia. Al fine di configurare i siti che devono essere presi in considerazione dal servizio, un `cq:siteVariant` deve essere aggiunto al `jcr:content` nodo dalla radice del sito.

La `cq:siteVariant` il nodo deve avere le seguenti proprietà:

* `cq:childNodesMapTo` - determina a quale attributo dell’elemento di collegamento saranno mappati i nodi figlio; si consiglia di organizzare il contenuto del sito web in modo che gli elementi secondari del nodo principale rappresentino la radice di una variante linguistica del sito web globale (ad esempio `/content/mysite/en`, `/content/mysite/de`), nel qual caso il valore del `cq:childNodesMapTo` devono `hreflang`;
* `cq:variantDomain` - indica cosa `Externalizer` viene utilizzato per generare gli URL assoluti delle varianti di pagina; se questo valore non è impostato, le varianti di pagina saranno generate utilizzando collegamenti relativi;
* `cq:variantFamily` - indica a quale famiglia di siti web appartiene questo sito; più rappresentazioni specifiche per dispositivo dello stesso sito web dovrebbero appartenere alla stessa famiglia;
* `media` - memorizza i valori dell&#39;attributo media dell&#39;elemento di collegamento; si consiglia di utilizzare il nome della `BrowserMap` registrato `DeviceGroups`, affinché `BrowserMap` la libreria può inoltrare automaticamente i client alla variante corretta del sito web.

#### PageVariantsProvider ed Externalizer {#pagevariantsprovider-and-externalizer}

Quando il valore di `cq:variantDomain` proprietà di un `cq:siteVariant` il nodo non è vuoto, il `PageVariantsProvider` il servizio genererà collegamenti assoluti utilizzando questo valore come dominio configurato per `Externalizer` servizio. Assicurati di configurare le `Externalizer` per riflettere la configurazione.

>[!NOTE]
>
>Quando si lavora con AEM esistono diversi metodi per gestire le impostazioni di configurazione di tali servizi; vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) per ulteriori dettagli e procedure consigliate.

### Definizione di un URL specifico per un gruppo di dispositivi {#defining-a-device-group-specific-url}

Se non desideri utilizzare collegamenti alternativi, puoi configurare un URL globale per ogni `DeviceGroup`. È consigliabile creare una libreria client personalizzata che incorpori le `browsermap.standard` libreria client, ma ridefinisce i gruppi di dispositivi.

BrowserMap è progettato in modo tale che le definizioni dei gruppi di dispositivi possano essere ignorate creando e aggiungendo un nuovo gruppo di dispositivi con lo stesso nome al gruppo di dispositivi `BrowserMap` dalla libreria client personalizzata.

>[!NOTE]
>
>Per ulteriori informazioni, consulta la sezione [BrowserMap personalizzato](#creatingacustomisedbrowsermap) sezione .

### Definizione degli URL basati su selettore {#defining-selector-based-urls}

Se non è stato utilizzato nessuno dei meccanismi precedenti per indicare un sito alternativo per `BrowserMap`, quindi selettori che utilizzeranno i nomi dei `DeviceGroups` verrà aggiunto al `URL`s, nel qual caso devi fornire i tuoi servlet che gestiranno le richieste.

Ad esempio, un browser `www.example.com/index.html` identificati come `smartphone` da BrowserMap è inoltrato a `www.example.com/index.smartphone.html.`

### Utilizzo di BrowserMap nelle pagine {#using-browsermap-on-your-pages}

Per utilizzare la libreria client BrowserMap standard in una pagina, è necessario includere il `/libs/wcm/core/browsermap/browsermap.jsp` file che utilizza un `cq:include`tag nella pagina `head` sezione .

```xml
<cq:include script="/libs/wcm/core/browsermap/browsermap.jsp" />
```

Oltre ad aggiungere `BrowserMap` libreria client nel `JSP` file, devi anche aggiungere un `cq:deviceIdentificationMode` Proprietà stringa impostata su `client-side` al `jcr:content` nodo sotto la radice del sito Web.

### Ignorare il comportamento predefinito di BrowserMap {#overriding-browsermap-s-default-behaviour}

Se desideri personalizzare `BrowserMap` - sovrascrivendo `DeviceGroups` o aggiungi più sonde, quindi devi creare una tua libreria lato client in cui incorporare il `browsermap.standard`libreria lato client.

Inoltre, devi chiamare manualmente il `BrowserMap.forwardRequest()` nel tuo `JavaScript` codice.

>[!NOTE]
>
>Per ulteriori informazioni sull’integrazione della libreria client, consulta la sezione [Utilizzo delle librerie HTML lato client](/help/sites-developing/clientlibs.md) sezione .

Una volta creato il tuo `BrowserMap` libreria client, ti suggeriamo il seguente approccio:

1. Crea un `browsermap.jsp` file nell&#39;applicazione

   ```xml
   <%@include file="/libs/foundation/global.jsp" %>
   <%@ taglib prefix="c" uri="https://java.sun.com/jsp/jstl/core" %>
   <%@ page import="
       com.day.cq.wcm.api.variants.PageVariant,
       com.day.cq.wcm.api.variants.PageVariantsProvider,
       com.day.cq.wcm.api.devicedetection.DeviceIdentificationMode,
       com.day.cq.wcm.api.WCMMode"
   %>
   <%
       final PageVariantsProvider p = sling.getService(PageVariantsProvider.class);
       if(p == null) {
           throw new IllegalStateException("Missing PageVariantsProvider service");
       }
       for(PageVariant v : p.getVariants(currentPage, slingRequest)) {
           final String curVar = v.getAttributes().get("data-current-variant");
           String media = v.getAttributes().get("media");
           if (media != null) {
               media = media.replaceAll(" ", "");
           }
   %>
       <link
           rel="alternate"
           data-cq-role="site.variant"
           title="<%= xssAPI.encodeForHTMLAttr(v.getTitle()) %>"
           hreflang="<%= xssAPI.encodeForHTMLAttr(v.getAttributes().get("hreflang")) %>"
           media="<%= xssAPI.encodeForHTMLAttr(media) %>"
           href="<%= xssAPI.getValidHref(v.getURL()) %>"
           <% if(curVar != null) { %> data-current-variant="<%= curVar %>"<% } %>
       />
   <%
       }
       Boolean browserMapEnabled = true;
       final DeviceIdentificationMode dim = sling.getService(DeviceIdentificationMode.class);
       String[] selectors  = slingRequest.getRequestPathInfo().getSelectors();
       boolean isPortletRequest = false;
       for (int i = 0; i < selectors.length; i++) {
           if ("portlet".equals(selectors[i])) {
               isPortletRequest = true;
               break;
           }
       }
       if (isPortletRequest) {
           log.debug("Request was made by a portlet container - BrowserMap will not be embedded");
       } else {
           final WCMMode wcmMode = WCMMode.fromRequest(slingRequest);
           boolean shouldIncludeClientLib = false;
           if (WCMMode.EDIT != wcmMode && WCMMode.PREVIEW != wcmMode && WCMMode.DESIGN != wcmMode) {
               if (dim != null) {
                   final String mode = dim.getDeviceIdentificationModeForPage(currentPage);
                   shouldIncludeClientLib = DeviceIdentificationMode.CLIENT_SIDE.equals(mode);
                   if (shouldIncludeClientLib) {
                       browserMapEnabled = (Boolean) request.getAttribute("browsermap.enabled");
                       if (browserMapEnabled == null) {
                           browserMapEnabled = true;
                       }
                   }
               }
           }
   %>
           <c:if test="<%= !browserMapEnabled %>">
               <meta name="browsermap.enabled" content="false">
           </c:if>
           <c:if test="<%= shouldIncludeClientLib %>">
               <meta name="viewport" content="width=device-width, initial-scale=1.0">
               <cq:includeClientLib categories="browsermap.custom"/>
           </c:if>
   <%
       }
   %>
   ```

1. Includi il `broswermap.jsp` nella sezione head.

   ```xml
   <cq:include script="browsermap.jsp" />
   ```

### Esclusione di BrowserMap da alcune pagine {#excluding-browsermap-from-certain-pages}

Se desideri escludere la libreria BrowserMap da alcune pagine in cui non è necessario il rilevamento del client, puoi aggiungere un attributo di richiesta:

```xml
<%
request.setAttribute("browsermap.enabled", false);
%>
```

In questo modo la `/libs/wcm/core/browsermap/browsermap.jsp` script per aggiungere alla pagina un tag meta che verrà creato `BrowserMap` per non eseguire alcun rilevamento:

```xml
<meta name="browsermap.enabled" content="false">
```

### Verifica di una versione specifica di un sito Web {#testing-a-specific-version-of-a-web-site}

Normalmente, lo script BrowserMap reindirizzerà sempre i visitatori alla versione più adatta del sito web, in genere reindirizzando i visitatori al desktop o al sito mobile quando necessario.

Puoi forzare il dispositivo di qualsiasi richiesta per testare una versione specifica di un sito web aggiungendo il `device` all&#39;URL. Il seguente URL esegue il rendering della versione mobile del sito Web Geometrixx Outdoors.

`https://localhost:4502/content/geometrixx-outdoors/en.html?wcmmode=disabled&device=smartphone`

>[!NOTE]
>
>La `wcmmode` è impostato su `disabled` per simulare il comportamento di un’istanza di pubblicazione.

Il valore del dispositivo ignorato viene memorizzato in un cookie per consentire di navigare nel sito Web senza aggiungere il `device` a ogni `URL`.

Di conseguenza, è necessario chiamare lo stesso `URL` con `device` impostato su `browser` per tornare alla versione desktop del sito web.

>[!NOTE]
>
>BrowserMap memorizza il valore del dispositivo ignorato in un cookie denominato `BMAP_device`. L’eliminazione di questo cookie assicurerà che CQ distribuisca la versione appropriata del sito web in base al dispositivo corrente (ad esempio, desktop o mobile).

## Elaborazione delle richieste mobile {#mobile-request-processing}

AEM elabora una richiesta emessa da un dispositivo mobile appartenente al gruppo di dispositivi touch come segue:

1. Un iPad invia una richiesta all’istanza di pubblicazione AEM, ad esempio `https://localhost:4503/content/geometrixx_mobile/en/products.html`
1. AEM determina se il sito della pagina richiesta è un sito mobile (verificando se la pagina di primo livello è `/content/geometrixx_mobile` estende il componente pagina mobile). In caso affermativo:
1. AEM controlla le funzionalità del dispositivo in base all’agente utente nell’intestazione della richiesta.
1. AEM mappa le funzionalità del dispositivo al gruppo di dispositivi e imposta `touch` come selettore del gruppo di dispositivi.
1. AEM reindirizza la richiesta a `https://localhost:4503/content/geometrixx_mobile/en/products.touch.html.`
1. AEM invia la risposta ad iPad:

   * `products.touch.html` viene riprodotto nel modo consueto ed è memorizzabile nella cache.
   * I componenti di rendering utilizzano i selettori per adattare la presentazione.
   * AEM aggiunge automaticamente il selettore mobile a tutti i collegamenti interni della pagina.

### Statistiche {#statistics}

Puoi ottenere alcune statistiche sul numero di richieste effettuate al server AEM da dispositivi mobili. È possibile suddividere il numero di richieste:

* per gruppo di dispositivi e dispositivo
* per anno, mese e giorno

Per visualizzare le statistiche:

1. Vai a **Strumenti** console.
1. Apri **Statistiche dispositivo** pagina sottostante **Strumenti** > **Mobile**.
1. Fai clic sul collegamento per visualizzare le statistiche relative a un anno, un mese o un giorno specifico.

La **Statistiche** si presenta così:

![screen_shot_2012-02-01at24353pm](assets/screen_shot_2012-02-01at24353pm.png)

>[!NOTE]
>
>La **Statistiche** viene creata la prima volta che un dispositivo mobile accede AEM e viene rilevato. Prima di questo, non è disponibile.

Se è necessario generare una voce nelle statistiche, è possibile procedere come segue:

1. Utilizza un dispositivo mobile o un emulatore (ad esempio https://chrispederick.com/work/user-agent-switcher/ su Firefox).
1. Richiedi una pagina mobile sull’istanza di authoring disattivando la modalità di authoring, ad esempio:
   `https://localhost:4502/content/geometrixx_mobile/en/products.html?wcmmode=disabled`

La **Statistiche** è ora disponibile.

### Memorizzazione in cache delle pagine per i collegamenti &quot;invia collegamento a un amico&quot; {#supporting-page-caching-for-send-link-to-a-friend-links}

Le pagine mobili sono generalmente memorizzabili nella cache in Dispatcher, perché le pagine di cui è stato effettuato il rendering per un gruppo di dispositivi sono distinte nell’URL della pagina dal selettore del gruppo di dispositivi, ad esempio `/content/mobilepage.touch.html`. Una richiesta a una pagina mobile senza un selettore non viene mai memorizzata nella cache, come in questo caso, il rilevamento del dispositivo funziona e infine reindirizza al gruppo di dispositivi corrispondente (o &quot;omatch&quot; per quel motivo). Una pagina mobile sottoposta a rendering con un selettore di gruppi di dispositivi viene elaborata dal rewriter di collegamento, che riscrive tutti i collegamenti all’interno della pagina per contenere anche il selettore di gruppi di dispositivi, impedendo la riesecuzione del rilevamento del dispositivo per ogni clic su una pagina già qualificata.

Pertanto, potresti riscontrare lo scenario seguente:

L&#39;utente Alice viene reindirizzato a `coolpage.feature.html`e invia l&#39;URL a un amico Bob che lo accede con un client diverso che rientra nel `touch` gruppo di dispositivi.

Se `coolpage.feature.html` viene servito da una cache front-end, AEM non ha la possibilità di analizzare la richiesta per scoprire che il selettore mobile non corrisponde al nuovo User-Agent e Bob riceve la rappresentazione sbagliata.

Per risolverlo, puoi includere una semplice interfaccia utente di selezione nelle pagine, in cui gli utenti finali possono ignorare il gruppo di dispositivi selezionato da AEM. Nell’esempio precedente, un collegamento (o un’icona) sulla pagina consente all’utente finale di passare a `coolpage.touch.html` se pensa che il suo dispositivo sia sufficiente.
