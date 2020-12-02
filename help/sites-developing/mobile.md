---
title: Creazione di siti per dispositivi mobili
seo-title: Creazione di siti per dispositivi mobili
description: La creazione di un sito mobile è simile alla creazione di un sito standard e comporta anche la creazione di modelli e componenti
seo-description: La creazione di un sito mobile è simile alla creazione di un sito standard e comporta anche la creazione di modelli e componenti
uuid: 6b19042c-03f1-4e33-970e-475f9fb8c5fb
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: 0aabfb0a-ef9c-4b06-b698-61cad101c3c1
docset: aem65
legacypath: /content/docs/en/aem/6-0/develop/mobile/mobile
translation-type: tm+mt
source-git-commit: b3e1493811176271ead54bae55b1cd0cf759fe71
workflow-type: tm+mt
source-wordcount: '3864'
ht-degree: 1%

---


# Creazione di siti per dispositivi mobili{#creating-sites-for-mobile-devices}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;editor SPA per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

La creazione di un sito mobile è simile alla creazione di un sito standard, ma richiede anche la creazione di modelli e componenti. Per ulteriori dettagli sulla creazione di modelli e componenti, consulta le pagine seguenti: [Modelli](/help/sites-developing/templates.md), [Componenti](/help/sites-developing/components.md) e [Guida introduttiva allo sviluppo  AEM Sites](/help/sites-developing/getting-started.md). La differenza principale consiste nell&#39;abilitare le funzionalità mobili integrate AEM all&#39;interno del sito. Viene ottenuto creando un modello basato sul componente Pagina mobile.

È inoltre consigliabile utilizzare [responsive design](/help/sites-developing/responsive.md), creando un singolo sito che supporti diverse dimensioni di schermo.

Per iniziare, è possibile consultare il **Sito demo mobile We.Retail** disponibile in AEM.

Per creare un sito mobile, effettuate le seguenti operazioni:

1. Creare il componente Pagina:

   * Impostare la proprietà `sling:resourceSuperType` su `wcm/mobile/components/page`
In questo modo il componente si basa sul componente pagina mobile.

   * Create l&#39;elemento `body.jsp` con la logica specifica del progetto.

1. Create il modello di pagina:

   * Impostate la proprietà `sling:resourceType` sul componente pagina appena creato.
   * Impostare la proprietà `allowedPaths`.

1. Create la pagina di progettazione per il sito.
1. Crea la pagina principale del sito sotto il nodo `/content`:

   * Impostare la proprietà `cq:allowedTemplates`.
   * Impostare la proprietà `cq:designPath`.

1. Nelle proprietà della pagina principale del sito, impostare i gruppi di dispositivi nella scheda **Mobile**.
1. Create le pagine del sito utilizzando il nuovo modello.

Componente pagina mobile ( `/libs/wcm/mobile/components/page`):

* Aggiunge la scheda **Mobile** alla finestra di dialogo delle proprietà della pagina.
* Attraverso il suo `head.jsp`, recupera il gruppo di dispositivi mobili corrente dalla richiesta e, se viene trovato un gruppo di dispositivi, utilizza il metodo `drawHead()` del gruppo per includere il componente init dell&#39;emulatore associato del gruppo di dispositivi (solo in modalità di creazione) e il CSS di rendering del gruppo di dispositivi.

>[!NOTE]
>
>La pagina principale del sito mobile deve trovarsi al livello 1 della gerarchia dei nodi e si consiglia di trovarsi sotto il nodo /content.

## Creazione di un sito mobile con Multi Site Manager {#creating-a-mobile-site-with-the-multi-site-manager}

Multi Site Manager (MSM) consente di creare una Live Copy mobile da un sito standard. Il sito standard viene automaticamente trasformato in un sito mobile: il sito mobile presenta tutte le funzioni dei siti mobili (ad es. edizione all’interno di un emulatore) e può essere gestito in sincronia con il sito standard. Fare riferimento alla sezione [Creazione di una Live Copy per diversi canali](/help/sites-administering/msm.md) nella pagina Gestione multisito.

## API mobile lato server {#server-side-mobile-api}

I pacchetti Java contenenti le classi mobili sono:

* [com.day.cq.wcm.mobile.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html) - Definisce MobileConstants.
* [com.day.cq.wcm.mobile.api.device](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/package-summary.html) - definisce Device, DeviceGroup e DeviceGroupList.
* [com.day.cq.wcm.mobile.api.device.functionality](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html) - definisce DeviceCapability.
* [com.day.cq.wcm.mobile.api.wurfl](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/api/package-summary.html) - definisce WurflQueryEngine.
* [com.day.cq.wcm.mobile.core](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/core/package-summary.html) - definisce MobileUtil, che fornisce vari metodi di utilità ruotanti attorno a WCM Mobile.

### Componenti mobili {#mobile-components}

Il **sito dimostrativo We.Retail Mobile** utilizza i seguenti componenti mobili, che si trovano sotto `/libs/foundation/components`:

<table>
 <tbody>
  <tr>
   <td>Nome</td>
   <td>Gruppo</td>
   <td>Caratteristiche</td>
  </tr>
  <tr>
   <td>mobilepiè di pagina</td>
   <td>nascosto</td>
   <td>- piè di pagina</td>
  </tr>
  <tr>
   <td>mobileimage</td>
   <td>Mobile</td>
   <td>- basato sul componente base immagine<br /> - esegue il rendering di un'immagine se il dispositivo è in grado di eseguire il rendering<br /> </td>
  </tr>
  <tr>
   <td>mobilista</td>
   <td>Mobile</td>
   <td>- in base al componente di base dell'elenco<br /> - listitem_teaser.jsp esegue il rendering di un'immagine se il dispositivo è in grado<br /> </td>
  </tr>
  <tr>
   <td>mobilelogo</td>
   <td>nascosto</td>
   <td>- in base al componente di base del logo<br /> - esegue il rendering di un'immagine se il dispositivo è in grado di eseguire il rendering<br /> </td>
  </tr>
  <tr>
   <td>mobilereferenza</td>
   <td>Mobile</td>
   <td><p>- simile al componente Base riferimento</p> <p>- mappatura di un componente di testo su un modello mobile e di un componente immagine su un’immagine mobile</p> </td>
  </tr>
  <tr>
   <td>mobiletextimage</td>
   <td>Mobile</td>
   <td>- in base al componente di base del testo<br /> - esegue il rendering di un'immagine se il dispositivo è in grado di</td>
  </tr>
  <tr>
   <td>mobiletopnav</td>
   <td>nascosto</td>
   <td><p>- in base al componente di base nav superiore</p> <p>- esegue solo il rendering del testo</p> </td>
  </tr>
 </tbody>
</table>

#### Creazione di un componente mobile {#creating-a-mobile-component}

Il framework mobile AEM consente di sviluppare componenti sensibili al dispositivo che emette la richiesta. Gli esempi di codice riportati di seguito mostrano come utilizzare l&#39;API mobile AEM in un jsp componente e in particolare come:

* Ottenete il dispositivo dalla richiesta:
   `Device device = slingRequest.adaptTo(Device.class);`

* Ottenete il gruppo di dispositivi:
   `DeviceGroup deviceGroup = device.getDeviceGroup();`

* Ottenete le funzionalità del gruppo di dispositivi:
   `Collection<DeviceCapability> capabilities = deviceGroup.getCapabilities();`

* Ottenete gli attributi del dispositivo (chiave/valori della funzionalità non elaborati dal database WURFL):
   `Map<String,String> deviceAttributes = device.getAttributes();`

* Ottenere l’agente utente del dispositivo:
   `String userAgent = device.getUserAgent();`

* Ottenete l’elenco dei gruppi di dispositivi (gruppi di dispositivi assegnati al sito dall’autore) dalla pagina corrente:
   `DeviceGroupList deviceGroupList = currentPage.adaptTo(DeviceGroupList.class);`

* Verificate se il gruppo di dispositivi supporta le immagini
   `if (deviceGroup.hasCapability(DeviceCapability.CAPABILITY_IMAGES)) {`
...
OPPURE

...   `if MobileUtil.hasCapability(request, DeviceCapability.CAPABILITY_IMAGES) {`
...

>[!NOTE]
>
>In un jsp, `slingRequest` è disponibile tramite il tag `<sling:defineObjects>` e `currentPage` tramite il tag `<cq:defineObjects>`.

### Emulatori {#emulators}

L’authoring basato su emulatore offre agli autori gli strumenti per creare pagine di contenuto destinate ai client mobili. La creazione di contenuti per dispositivi mobili segue lo stesso principio della modifica WYSIWYG locale. Affinché gli autori possano percepire l’aspetto della pagina su un dispositivo mobile, una pagina di contenuto mobile viene modificata utilizzando un emulatore di dispositivo.

Gli emulatori dei dispositivi mobili si basano sul framework emulatore generico. Per ulteriori dettagli, fare riferimento alla pagina [Emulatori](/help/sites-developing/emulators.md).

L&#39;emulatore del dispositivo visualizza il dispositivo mobile sulla pagina, mentre la modifica standard (parsys, components) avviene all&#39;interno dello schermo del dispositivo. L&#39;emulatore del dispositivo dipende dai gruppi di dispositivi configurati per il sito. Diversi emulatori possono essere assegnati a un gruppo di dispositivi. Tutti gli emulatori sono quindi disponibili nella pagina del contenuto. Per impostazione predefinita viene visualizzato il primo emulatore assegnato al primo gruppo di dispositivi assegnato al sito. Gli emulatori possono essere attivati tramite il carosello emulatore nella parte superiore della pagina o tramite il pulsante di modifica della barra laterale.

**Creazione di un emulatore**

Per creare un emulatore, fare riferimento alla sezione [Creazione di un emulatore mobile personalizzato](/help/sites-developing/emulators.md) nella pagina Emulatori generici.

**Caratteristiche principali degli emulatori mobili**

* Un gruppo di dispositivi è composto da uno o più emulatori: la pagina di configurazione del gruppo di dispositivi, ad esempio /etc/mobile/groups/touch, contiene la proprietà `emulators` sotto il nodo `jcr:content`.
Nota: anche se è possibile che lo stesso emulatore appartenga a diversi gruppi di dispositivi, non ha molto senso.

* Tramite la finestra di dialogo di configurazione del gruppo di dispositivi, la proprietà `emulators` viene impostata con il percorso dell&#39;emulatore o degli emulatori desiderati. Esempio: `/libs/wcm/mobile/components/emulators/iPhone4`.

* Componenti dell’emulatore (ad esempio `/libs/wcm/mobile/components/emulators/iPhone4`) estendere il componente emulatore mobile di base ( `/libs/wcm/mobile/components/emulators/base`).

* Ogni componente che estende l’emulatore mobile di base è disponibile per la selezione quando si configura un gruppo di dispositivi. Gli emulatori personalizzati possono quindi essere facilmente creati o estesi.
* Al momento della richiesta in modalità di modifica, l&#39;implementazione dell&#39;emulatore viene utilizzata per eseguire il rendering della pagina.
* Quando il modello della pagina dipende dal componente della pagina mobile, le funzionalità dell&#39;emulatore vengono automaticamente integrate nella pagina (tramite `head.jsp` del componente della pagina mobile).

### Gruppi dispositivo {#device-groups}

I gruppi di dispositivi mobili forniscono la segmentazione dei dispositivi mobili in base alle funzionalità del dispositivo. Un gruppo di dispositivi fornisce le informazioni necessarie per l’authoring basato sull’emulatore nell’istanza di creazione e per il corretto rendering del contenuto nell’istanza di pubblicazione: dopo che gli autori hanno aggiunto contenuto alla pagina mobile e l’hanno pubblicata, la pagina può essere richiesta nell’istanza di pubblicazione. Qui, invece della visualizzazione di modifica dell&#39;emulatore, viene eseguito il rendering della pagina del contenuto utilizzando uno dei gruppi di dispositivi configurati. La selezione del gruppo di dispositivi avviene in base al [rilevamento dei dispositivi mobili](#devicedetection). Il gruppo di dispositivi corrispondente fornisce quindi le informazioni di stile necessarie.

I gruppi di dispositivi sono definiti come pagine di contenuto sotto `/etc/mobile/devices` e utilizzano il modello **Mobile Device Group**. Il modello per gruppi di dispositivi funge da modello di configurazione per le definizioni dei gruppi di dispositivi nel modulo delle pagine di contenuto. Le sue caratteristiche principali sono:

* Posizione: `/libs/wcm/mobile/templates/devicegroup`
* Percorso consentito: `/etc/mobile/groups/*`
* Componente pagina: `wcm/mobile/components/devicegroup`

#### Assegnazione di gruppi di dispositivi al sito {#assigning-device-groups-to-your-site}

Quando create un sito mobile, dovete assegnare gruppi di dispositivi al sito. AEM fornisce tre gruppi di dispositivi a seconda delle capacità di rendering HTML e JavaScript del dispositivo:

* **Caratteristiche** dei telefoni, per dispositivi quali Sony Ericsson W800 con supporto per HTML di base ma nessun supporto per immagini e JavaScript.
* **** Smartphone, per dispositivi come Blackberry con supporto per HTML e immagini di base, ma senza supporto per JavaScript.

* **** TouchPhone, per dispositivi come l’iPad con supporto completo per HTML, immagini, JavaScript e rotazione del dispositivo.

Poiché gli emulatori possono essere associati a un gruppo di dispositivi (vedere la sezione [Creazione di un gruppo di dispositivi](#creating-a-device-group)), l&#39;assegnazione di un gruppo di dispositivi a un sito consente agli autori di selezionare tra gli emulatori associati al gruppo di dispositivi per modificare la pagina.

Per assegnare un gruppo di dispositivi al sito:

1. Nel browser, passate alla console **Site Admin** (Amministrazione sito).
1. Aprite la pagina principale del sito mobile sotto **Siti Web**.
1. Aprite le proprietà della pagina.
1. Selezionate la scheda **Mobile**:

   * Definite i gruppi di dispositivi.
   * Fai clic su **OK**.

>[!NOTE]
>
>Quando i gruppi di dispositivi sono stati definiti per un sito, vengono ereditati da tutte le pagine del sito.

#### Filtri per gruppo dispositivo {#device-group-filters}

I filtri per gruppi di dispositivi definiscono criteri basati sulle funzionalità per determinare se un dispositivo appartiene al gruppo. Quando create un gruppo di dispositivi, potete selezionare i filtri da utilizzare per valutare i dispositivi.

In fase di esecuzione quando AEM ricevuto una richiesta HTTP da un dispositivo, ogni filtro associato a un gruppo confronta le funzionalità del dispositivo con criteri specifici. Il dispositivo è considerato appartenente al gruppo quando dispone di tutte le funzionalità richieste dai filtri. Le funzionalità vengono recuperate dal database WURFL™.

I gruppi di dispositivi possono utilizzare zero o più filtri per il rilevamento delle funzionalità. È inoltre possibile utilizzare un filtro con più gruppi di dispositivi. AEM fornisce un filtro predefinito che determina se il dispositivo dispone delle funzionalità selezionate per un gruppo:

* CSS
* Immagini JPG e PNG
* JavaScript
* Rotazione dispositivo

Se il gruppo di dispositivi non utilizza un filtro, le funzionalità selezionate configurate per il gruppo sono le uniche che un dispositivo richiede.

Per ulteriori informazioni, vedere [Creazione di filtri per gruppi di dispositivi](/help/sites-developing/groupfilters.md).

#### Creazione di un gruppo di dispositivi {#creating-a-device-group}

Crea un gruppo di dispositivi quando i gruppi che AEM installati non soddisfano i tuoi requisiti.

1. Nel browser, accedete alla console **Strumenti**.
1. Create una nuova pagina sotto **Strumenti** > **Mobile** > **Gruppi di dispositivi**. Nella finestra di dialogo **Crea pagina**:

   * Come **Title** immettere `Special Phones`.

   * Come **Nome** immettere `special`.

   * Selezionare il **Modello del gruppo di dispositivi mobili**.
   * Fai clic su **Crea**.

1. In CRXDE, aggiungete un file **static.css** contenente gli stili per il gruppo di dispositivi sotto il nodo `/etc/mobile/groups/special`.

1. Aprite la pagina **Telefoni speciali**.
1. Per configurare il gruppo di dispositivi, fare clic sul pulsante **Modifica** accanto a **Impostazioni**.
Nella scheda **Generale**:

   * **Titolo**: il nome del gruppo del dispositivo mobile.
   * **Descrizione**: descrizione del gruppo.
   * **Agente** utente: stringa agente utente con cui viene confrontata la corrispondenza tra i dispositivi. È opzionale e può essere un regex. Esempio: `BlackBerryZ10`
   * **Funzionalità**: definisce se il gruppo può gestire immagini, CSS, JavaScript o rotazione del dispositivo.
   * **Larghezza****e altezza minima dello schermo**
   * **Disattiva emulatore**: per attivare/disattivare l&#39;emulatore durante la modifica del contenuto.

   Nella scheda **Emulatori**:

   * **Emulatori**: selezionare gli emulatori assegnati a questo gruppo di dispositivi.

   Nella scheda **Filtri**:

   * Per aggiungere un filtro, fate clic su Aggiungi elemento e selezionate un filtro dall’elenco a discesa.
   * I filtri vengono valutati nell&#39;ordine in cui appaiono. Quando un dispositivo non soddisfa i criteri di un filtro, i filtri successivi nell&#39;elenco non vengono valutati.



1. Fai clic su OK.

La finestra di dialogo di configurazione del gruppo di dispositivi mobili si presenta come segue:

![screen_shot_2012-02-01at22043pm](assets/screen_shot_2012-02-01at22043pm.png)

#### CSS personalizzato per gruppo di dispositivi {#custom-css-per-device-group}

Come descritto in precedenza, è possibile associare un CSS personalizzato a una pagina di gruppo di dispositivi, proprio come il CSS di una pagina di progettazione.Questo CSS viene utilizzato per influenzare il rendering specifico del gruppo di dispositivi del contenuto della pagina sull&#39;autore e sulla pubblicazione.Questo CSS viene quindi incluso automaticamente:

* Nella pagina nell’istanza di creazione per ogni emulatore utilizzato da questo gruppo di dispositivi.
* Nella pagina dell’istanza di pubblicazione se l’agente utente della richiesta corrisponde a un dispositivo mobile in questo particolare gruppo di dispositivi.

## Rilevamento dispositivo lato server {#server-side-device-detection}

Utilizzate i filtri e una libreria di specifiche dispositivo per determinare le capacità del dispositivo che esegue la richiesta HTTP.

### Sviluppare filtri per gruppi di dispositivi {#develop-device-group-filters}

Create un filtro gruppo di dispositivi per definire un set di requisiti di funzionalità dei dispositivi. Create tutti i filtri necessari per eseguire il targeting dei gruppi necessari di funzionalità dei dispositivi.

Progettate i filtri in modo da poter utilizzare combinazioni di essi per definire i gruppi di funzionalità. In genere, esiste una sovrapposizione delle capacità di diversi gruppi di dispositivi. Di conseguenza, potete utilizzare alcuni filtri con più definizioni di gruppi di dispositivi.

Dopo aver creato un filtro, potete usarlo nella configurazione del gruppo.

Per ulteriori informazioni, vedere [Creazione di filtri per gruppi di dispositivi](/help/sites-developing/groupfilters.md).

### Utilizzo del database WURFL™ {#using-the-wurfl-database}

AEM utilizza una versione troncata del database [WURFL](https://wurfl.sourceforge.net/)™ per eseguire query sulle funzionalità dei dispositivi, come la risoluzione dello schermo o il supporto JavaScript, in base all&#39;agente utente del dispositivo.

Il codice XML del database WURFL™ è rappresentato come nodi sotto `/var/mobile/devicespecs` analizzando il file `wurfl.xml`in `/libs/wcm/mobile/devicespecs/wurfl.xml.` L&#39;espansione ai nodi si verifica la prima volta che viene avviato il bundle `cq-mobile-core`.

Le funzionalità dei dispositivi sono memorizzate come proprietà dei nodi e i nodi rappresentano modelli di dispositivi. Potete utilizzare le query per recuperare le funzionalità di un dispositivo o agente utente.

Poiché il database WURFL™ si sta evolvendo, potrebbe essere necessario personalizzarlo o sostituirlo. Per aggiornare il database dei dispositivi mobili sono disponibili le seguenti opzioni:

* Se disponete di una licenza che consente tale utilizzo, sostituite il file con la versione più recente. Vedere Installazione di un altro database WURFL.
* Utilizzate la versione disponibile in AEM e configurate un regexp che corrisponda alle stringhe Agente-utente e punti a un dispositivo WURFL™ esistente. Vedere [Aggiunta di una corrispondenza utente-agente basata su regexp](#adding-a-regexp-based-user-agent-matching).

#### Verifica della mappatura di un agente utente alle funzionalità WURFL™ {#testing-the-mapping-of-a-user-agent-to-wurfl-capabilities}

Quando un dispositivo accede al sito mobile, AEM rileva il dispositivo, lo mappa a un gruppo di dispositivi in base alle sue capacità e invia una visualizzazione della pagina che corrisponde al gruppo di dispositivi. Il gruppo di dispositivi corrispondente fornisce le informazioni di stile necessarie. Le mappature possono essere testate nella pagina di test dell&#39;agente utente mobile:

`https://localhost:4502/etc/mobile/useragent-test.html`

#### Installazione di un database WURFL™ diverso {#installing-a-different-wurfl-database}

Il database WURFL™ troncato installato con AEM è una versione precedente alle date
30 agosto 2011. Se la vostra versione del WURFL è stata rilasciata dopo il 30 agosto 2011, accertatevi che l&#39;utilizzo sia conforme alla licenza.

Per installare un database WURFL™:

1. In CRXDE Lite , create la seguente cartella: `/apps/wcm/mobile/devicespecs`
1. Copiate il file WURFL™ nella cartella.
1. Rinominare il file come `wurfl.xml`.

AEM automaticamente analizza il file `wurfl.xml` e aggiorna i nodi sottostanti `/var/mobile/devicespecs`.

>[!NOTE]
>
>Quando il database WURFL™ completo è abilitato, l&#39;analisi e l&#39;attivazione potrebbero richiedere alcuni minuti. È possibile controllare i registri per informazioni sull’avanzamento.

#### Aggiunta di una corrispondenza agente-utente basata su regexp {#adding-a-regexp-based-user-agent-matching}

Aggiungi un agente utente come espressione regolare di seguito /apps/wcm/mobile/devicspecs/wurfl/regexp per puntare a un tipo di dispositivo WURFL™ esistente.

1. In **CRXDE Lite**, create un nodo sotto /apps/wcm/mobile/devicspecs/regexp, ad esempio apple_ipad_ver1.
1. Aggiungi le seguenti proprietà al nodo:

   * **regexp**: espressione regolare che definisce gli agenti utente, ad esempio: .*Mozilla.*iPad.*AppleWebKit.*Safari.*
   * **deviceId**: l’ID dispositivo come definito nel file wurfl.xml, ad esempio: apple_ipad_ver1

La configurazione di cui sopra causa la mappatura dei dispositivi per i quali l&#39;agente utente corrisponde all&#39;espressione regolare fornita all&#39;ID dispositivo apple_ipad_ver1 WURFL™, se esistente.

## Rilevamento dispositivo lato client {#client-side-device-detection}

In questa sezione viene descritto come utilizzare il rilevamento lato client del dispositivo per AEM al fine di ottimizzare il rendering della pagina o per fornire al client versioni alternative del sito Web.

AEM supporta il rilevamento lato client del dispositivo in base a `BrowserMap`. `BrowserMap` viene spedito in AEM come libreria cliente in  `/etc/clientlibs/browsermap`.

`BrowserMap` fornisce tre strategie che potete utilizzare per fornire un sito Web alternativo a un cliente, che vengono utilizzate nel seguente ordine:

1. [Collegamenti alternativi](#providing-alternate-links)
1. [URL specifico per il gruppo di dispositivi](#definingdevicegroupspecificurl)
1. [URL basato su selettore](#defining-selector-based-urls)

>[!NOTE]
>
>Per ulteriori informazioni sull&#39;integrazione con la libreria client, consultare la sezione [Utilizzo delle librerie HTML lato client](/help/sites-developing/clientlibs.md).

### Collegamenti alternativi {#providing-alternate-links}

Il servizio `PageVariantsProvider` OSGi è in grado di generare collegamenti alternativi per siti appartenenti alla stessa famiglia. Per configurare i siti da prendere in considerazione dal servizio, è necessario aggiungere un nodo `cq:siteVariant` al nodo `jcr:content` dalla radice del sito.

Il nodo `cq:siteVariant` deve avere le seguenti proprietà:

* `cq:childNodesMapTo` - determina a quale attributo dell&#39;elemento di collegamento saranno mappati i nodi secondari; si consiglia di organizzare il contenuto del sito Web in modo che gli elementi secondari del nodo principale rappresentino la radice di una variante della lingua del sito Web globale (ad esempio  `/content/mysite/en`,  `/content/mysite/de`), nel qual caso il valore del  `cq:childNodesMapTo` prodotto deve essere  `hreflang`;
* `cq:variantDomain` - indica quale  `Externalizer` dominio verrà utilizzato per generare gli URL assoluti delle varianti di pagina; se questo valore non è impostato, le varianti di pagina verranno generate utilizzando collegamenti relativi;
* `cq:variantFamily` - indica a quale famiglia di siti web appartiene questo sito; più rappresentazioni specifiche per dispositivo dello stesso sito web dovrebbero appartenere alla stessa famiglia;
* `media` - memorizza i valori dell&#39;attributo media dell&#39;elemento link; si consiglia di utilizzare il nome della  `BrowserMap` registrazione  `DeviceGroups`, in modo che la  `BrowserMap` libreria possa inoltrare automaticamente i client alla variante corretta del sito Web.

#### PageVariantsProvider ed Externalizer {#pagevariantsprovider-and-externalizer}

Quando il valore della proprietà `cq:variantDomain` di un nodo `cq:siteVariant` non è vuoto, il servizio `PageVariantsProvider` genererà collegamenti assoluti utilizzando questo valore come dominio configurato per il servizio `Externalizer`. Accertatevi di configurare il servizio `Externalizer` in modo che rifletta la configurazione.

>[!NOTE]
>
>Quando lavorate con AEM esistono diversi metodi per gestire le impostazioni di configurazione di tali servizi; per ulteriori informazioni e procedure consigliate, vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md).

### Definizione di un URL specifico per un gruppo di dispositivi {#defining-a-device-group-specific-url}

Se non si desidera utilizzare collegamenti alternativi, è possibile configurare un URL globale per ogni `DeviceGroup`. È consigliabile creare una propria libreria client che incorpora la libreria client `browsermap.standard`, ma ridefinisce i gruppi di dispositivi.

BrowserMap è progettato in modo tale che le definizioni dei gruppi di dispositivi possano essere ignorate creando e aggiungendo un nuovo gruppo di dispositivi con lo stesso nome all&#39;oggetto `BrowserMap` dalla libreria client personalizzata.

>[!NOTE]
>
>Per ulteriori dettagli, consultare la sezione [BrowserMap](#creatingacustomisedbrowsermap) personalizzata.

### Definizione degli URL basati su selettore {#defining-selector-based-urls}

Se nessuno dei meccanismi precedenti è stato utilizzato per indicare un sito alternativo per `BrowserMap`, i selettori che utilizzeranno i nomi di `DeviceGroups` saranno aggiunti agli `URL`s, nel qual caso è necessario fornire i propri servlet che gestiranno le richieste.

Ad esempio, la ricerca di un dispositivo `www.example.com/index.html` identificata come `smartphone` da BrowserMap viene inoltrata a `www.example.com/index.smartphone.html.`

### Utilizzo di BrowserMap sulle pagine {#using-browsermap-on-your-pages}

Per utilizzare la libreria client BrowserMap standard in una pagina, è necessario includere il file `/libs/wcm/core/browsermap/browsermap.jsp` utilizzando un tag `cq:include`nella sezione `head` della pagina.

```xml
<cq:include script="/libs/wcm/core/browsermap/browsermap.jsp" />
```

Oltre ad aggiungere la `BrowserMap` libreria client nei file `JSP`, è necessario aggiungere anche una proprietà `cq:deviceIdentificationMode` String impostata su `client-side` al nodo `jcr:content` sotto la radice del sito Web.

### Ignorare il comportamento predefinito di BrowserMap {#overriding-browsermap-s-default-behaviour}

Se si desidera personalizzare `BrowserMap`, ignorando la `DeviceGroups` o aggiungendo più sonde, è necessario creare una propria libreria lato client in cui incorporare la `browsermap.standard`libreria lato client.

Inoltre, è necessario chiamare manualmente il metodo `BrowserMap.forwardRequest()` nel codice `JavaScript`.

>[!NOTE]
>
>Per ulteriori informazioni sull&#39;integrazione con la libreria client, consultare la sezione [Utilizzo delle librerie HTML lato client](/help/sites-developing/clientlibs.md).

Dopo aver creato la libreria client personalizzata `BrowserMap`, consigliamo il seguente approccio:

1. Creare un file `browsermap.jsp` nell&#39;applicazione

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

1. Includete il file `broswermap.jsp` nella sezione head.

   ```xml
   <cq:include script="browsermap.jsp" />
   ```

### Esclusione di BrowserMap da alcune pagine {#excluding-browsermap-from-certain-pages}

Se desiderate escludere la libreria BrowserMap da alcune pagine in cui non è necessario il rilevamento client, potete aggiungere un attributo di richiesta:

```xml
<%
request.setAttribute("browsermap.enabled", false);
%>
```

In questo modo lo script `/libs/wcm/core/browsermap/browsermap.jsp` aggiungerà un tag meta alla pagina che renderà `BrowserMap` non eseguibile il rilevamento:

```xml
<meta name="browsermap.enabled" content="false">
```

### Verifica di una versione specifica di un sito Web {#testing-a-specific-version-of-a-web-site}

Normalmente, lo script BrowserMap reindirizzerà sempre i visitatori alla versione più adatta del sito Web, in genere reindirizzando i visitatori verso il desktop o il sito mobile quando necessario.

Potete forzare il dispositivo di qualsiasi richiesta per testare una versione specifica di un sito Web aggiungendo il parametro `device` all&#39;URL. Il seguente URL renderà la versione mobile del sito Web Geometrixx Outdoors.

`https://localhost:4502/content/geometrixx-outdoors/en.html?wcmmode=disabled&device=smartphone`

>[!NOTE]
>
>Il parametro `wcmmode` è impostato su `disabled` per simulare il comportamento di un&#39;istanza di pubblicazione.

Il valore del dispositivo ignorato viene memorizzato in un cookie in modo da poter navigare nel sito Web senza aggiungere il parametro `device` a ogni elemento `URL`.

Di conseguenza, è necessario chiamare lo stesso `URL` con il `device` impostato su `browser` per tornare alla versione desktop del sito Web.

>[!NOTE]
>
>BrowserMap memorizza il valore del dispositivo ignorato in un cookie denominato `BMAP_device`. Se eliminate questo cookie, CQ distribuirà la versione appropriata del sito Web in base al dispositivo corrente (ad esempio, desktop o mobile).

## Elaborazione richiesta mobile {#mobile-request-processing}

AEM elabora una richiesta emessa da un dispositivo mobile appartenente al gruppo di dispositivi touch come segue:

1. Un iPad invia una richiesta all’istanza di pubblicazione AEM, ad esempio `https://localhost:4503/content/geometrixx_mobile/en/products.html`
1. AEM determina se il sito della pagina richiesta è un sito mobile (verificando se la pagina di primo livello `/content/geometrixx_mobile` estende il componente della pagina mobile). In caso affermativo:
1. AEM le funzionalità del dispositivo in base all&#39;agente utente nell&#39;intestazione della richiesta.
1. AEM mappa le funzionalità del dispositivo al gruppo di dispositivi e imposta `touch` come selettore del gruppo di dispositivi.
1. AEM reindirizzare la richiesta a `https://localhost:4503/content/geometrixx_mobile/en/products.touch.html.`
1. AEM invia la risposta all’iPad:

   * `products.touch.html` è rappresentato nel modo usuale ed è memorizzabile nella cache.
   * I componenti di rendering utilizzano i selettori per adattare la presentazione.
   * AEM aggiunge automaticamente il selettore mobile a tutti i collegamenti interni nella pagina.

### Statistiche {#statistics}

Potete ottenere alcune statistiche sul numero di richieste effettuate al server AEM dai dispositivi mobili. È possibile suddividere il numero di richieste:

* per gruppo di dispositivi e dispositivo
* anno, mese e giorno

Per visualizzare le statistiche:

1. Passate alla console **Strumenti**.
1. Aprite la pagina **Device Statistics** sotto **Tools** > **Mobile**.
1. Fate clic sul collegamento per visualizzare le statistiche relative a un anno, un mese o un giorno specifico.

La pagina **Statistics** si presenta come segue:

![screen_shot_2012-02-01at24353pm](assets/screen_shot_2012-02-01at24353pm.png)

>[!NOTE]
>
>La pagina **Statistics** viene creata la prima volta che un dispositivo mobile accede AEM e viene rilevata. Prima di questo, non è disponibile.

Per generare una voce nelle statistiche, è possibile procedere come segue:

1. Usate un dispositivo mobile o un emulatore (ad esempio https://chrispederick.com/work/user-agent-switcher/ su Firefox).
1. Richiedete una pagina mobile nell’istanza di creazione disattivando la modalità di authoring, ad esempio:
   `https://localhost:4502/content/geometrixx_mobile/en/products.html?wcmmode=disabled`

È ora disponibile la pagina **Statistiche**.

### Memorizzazione nella cache delle pagine di supporto per l&#39;invio di un collegamento a un amico. Collegamenti {#supporting-page-caching-for-send-link-to-a-friend-links}

Le pagine mobili sono generalmente memorizzabili nella cache del dispatcher, perché le pagine di cui viene eseguito il rendering per un gruppo di dispositivi vengono distinte nell&#39;URL della pagina dal selettore del gruppo di dispositivi, ad esempio `/content/mobilepage.touch.html`. Una richiesta a una pagina mobile senza un selettore non viene mai memorizzata nella cache, come in questo caso, il rilevamento del dispositivo funziona e alla fine viene reindirizzato al gruppo di dispositivi corrispondente (o alla &quot;copia&quot; in quel caso). Il rendering di una pagina mobile con un selettore di gruppi di dispositivi viene elaborato dalla riscrittura dei collegamenti, che riscrive tutti i collegamenti all&#39;interno della pagina per contenere anche il selettore di gruppi di dispositivi, impedendo la ripetizione del rilevamento dispositivi per ogni clic su una pagina già qualificata.

Di conseguenza, si potrebbe verificare il seguente scenario:

L&#39;utente Alice viene reindirizzato a `coolpage.feature.html` e invia l&#39;URL a un amico Bob che accede con un altro client appartenente al gruppo `touch` del dispositivo.

Se `coolpage.feature.html` viene distribuito da una cache front-end, AEM non ha la possibilità di analizzare la richiesta per scoprire che il selettore mobile non corrisponde al nuovo agente utente, e Bob riceve la rappresentazione sbagliata.

Per risolverlo, puoi includere una semplice interfaccia utente di selezione nelle pagine, in cui gli utenti finali possono ignorare il gruppo di dispositivi selezionato da AEM. Nell&#39;esempio precedente, un collegamento (o un&#39;icona) sulla pagina consente all&#39;utente finale di passare a `coolpage.touch.html` se ritiene che il dispositivo sia sufficientemente adatto.
