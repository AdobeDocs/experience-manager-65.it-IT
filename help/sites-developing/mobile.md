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

---


# Creazione di siti per dispositivi mobili{#creating-sites-for-mobile-devices}

>[!NOTE]
>
>Adobe consiglia di utilizzare SPA Editor per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

La creazione di un sito mobile è simile alla creazione di un sito standard, ma richiede anche la creazione di modelli e componenti. Per ulteriori dettagli sulla creazione di modelli e componenti, consulta le pagine seguenti: [Modelli](/help/sites-developing/templates.md), [componenti](/help/sites-developing/components.md) e [guida introduttiva allo sviluppo di siti](/help/sites-developing/getting-started.md)AEM. La differenza principale consiste nell’abilitare le funzionalità mobili integrate di AEM all’interno del sito. Viene ottenuto creando un modello basato sul componente Pagina mobile.

È inoltre consigliabile utilizzare la progettazione [](/help/sites-developing/responsive.md)reattiva, creando un unico sito in grado di contenere più dimensioni di schermo.

Per iniziare, consultate il sito dimostrativo **We.Retail Mobile** disponibile in AEM.

Per creare un sito mobile, effettuate le seguenti operazioni:

1. Creare il componente Pagina:

   * Imposta la `sling:resourceSuperType` proprietà su `wcm/mobile/components/page`In questo modo il componente si basa sul componente Pagina mobile.

   * Crea il progetto `body.jsp` con la logica specifica del progetto.

1. Create il modello di pagina:

   * Impostare la `sling:resourceType` proprietà sul componente pagina appena creato.
   * Impostare la `allowedPaths` proprietà.

1. Create la pagina di progettazione per il sito.
1. Crea la pagina principale del sito sotto il `/content` nodo:

   * Impostare la `cq:allowedTemplates` proprietà.
   * Impostare la `cq:designPath` proprietà.

1. Nelle proprietà della pagina principale del sito, impostate i gruppi di dispositivi nella scheda **Mobile** .
1. Create le pagine del sito utilizzando il nuovo modello.

Il componente Pagina mobile ( `/libs/wcm/mobile/components/page`):

* Aggiunge la scheda **Mobile** alla finestra di dialogo delle proprietà della pagina.
* Tramite `head.jsp`, recupera il gruppo di dispositivi mobili corrente dalla richiesta e, se viene trovato un gruppo di dispositivi, utilizza il `drawHead()` metodo del gruppo per includere il componente init dell&#39;emulatore associato del gruppo di dispositivi (solo in modalità di creazione) e il CSS di rendering del gruppo di dispositivi.

>[!NOTE]
>
>La pagina principale del sito mobile deve trovarsi al livello 1 della gerarchia dei nodi e si consiglia di trovarsi sotto il nodo /content.

## Creazione di un sito mobile con Multi Site Manager {#creating-a-mobile-site-with-the-multi-site-manager}

Multi Site Manager (MSM) consente di creare una Live Copy mobile da un sito standard. Il sito standard viene automaticamente trasformato in un sito mobile: il sito mobile presenta tutte le funzioni dei siti mobili (ad es. edizione all’interno di un emulatore) e può essere gestito in sincronia con il sito standard. Consultate la sezione [Creazione di una Live Copy per diversi canali](/help/sites-administering/msm.md) nella pagina Gestione multisito.

## API mobile lato server {#server-side-mobile-api}

I pacchetti Java contenenti le classi mobili sono:

* [com.day.cq.wcm.mobile.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html) - definisce MobileConstants.
* [com.day.cq.wcm.mobile.api.device](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/package-summary.html) - definisce Device, DeviceGroup e DeviceGroupList.
* [com.day.cq.wcm.mobile.api.device.functionality](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html) - definisce DeviceCapability.
* [com.day.cq.wcm.mobile.api.wurfl](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/api/package-summary.html) - definisce WurflQueryEngine.
* [com.day.cq.wcm.mobile.core](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/core/package-summary.html) - definisce MobileUtil, che fornisce vari metodi di utilità ruotanti attorno a WCM Mobile.

### Componenti per dispositivi mobili {#mobile-components}

Il sito dimostrativo **We.Retail Mobile** utilizza i seguenti componenti mobili che si trovano sotto `/libs/foundation/components`:

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
   <td>- in base al componente<br /> Image foundation - esegue il rendering di un'immagine se il dispositivo è in grado di<br /> </td>
  </tr>
  <tr>
   <td>mobilista</td>
   <td>Mobile</td>
   <td>- in base al componente<br /> list foundation - listitem_teaser.jsp esegue il rendering di un'immagine se il dispositivo è in grado di<br /> </td>
  </tr>
  <tr>
   <td>mobilelogo</td>
   <td>nascosto</td>
   <td>- basato sul componente<br /> logo foundation - esegue il rendering di un'immagine se il dispositivo è in grado di<br /> </td>
  </tr>
  <tr>
   <td>mobilereferenza</td>
   <td>Mobile</td>
   <td><p>- simile al componente Base riferimento</p> <p>- mappatura di un componente di testo su un modello mobile e di un componente immagine su un’immagine mobile</p> </td>
  </tr>
  <tr>
   <td>mobiletextimage</td>
   <td>Mobile</td>
   <td>- in base al componente<br /> textimage foundation - esegue il rendering di un'immagine se il dispositivo è in grado di</td>
  </tr>
  <tr>
   <td>mobiletopnav</td>
   <td>nascosto</td>
   <td><p>- in base al componente di base nav superiore</p> <p>- esegue solo il rendering del testo</p> </td>
  </tr>
 </tbody>
</table>

#### Creazione di un componente mobile {#creating-a-mobile-component}

Il framework AEM Mobile consente di sviluppare componenti sensibili al dispositivo che emette la richiesta. Gli esempi di codice seguenti mostrano come utilizzare l&#39;API AEM Mobile in un&#39;app componente e in particolare come:

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
   `if MobileUtil.hasCapability(request, DeviceCapability.CAPABILITY_IMAGES) {`
...

>[!NOTE]
>
>In un jsp, `slingRequest` è disponibile tramite il `<sling:defineObjects>` tag e `currentPage` il `<cq:defineObjects>` tag .

### Emulatori {#emulators}

L’authoring basato su emulatore offre agli autori gli strumenti per creare pagine di contenuto destinate ai client mobili. La creazione di contenuti per dispositivi mobili segue lo stesso principio della modifica WYSIWYG locale. Affinché gli autori possano percepire l’aspetto della pagina su un dispositivo mobile, una pagina di contenuto mobile viene modificata utilizzando un emulatore di dispositivo.

Gli emulatori dei dispositivi mobili si basano sul framework emulatore generico. Per ulteriori dettagli, consultare la pagina [Emulatori](/help/sites-developing/emulators.md) .

L&#39;emulatore del dispositivo visualizza il dispositivo mobile sulla pagina, mentre la modifica standard (parsys, components) avviene all&#39;interno dello schermo del dispositivo. L&#39;emulatore del dispositivo dipende dai gruppi di dispositivi configurati per il sito. Diversi emulatori possono essere assegnati a un gruppo di dispositivi. Tutti gli emulatori sono quindi disponibili nella pagina del contenuto. Per impostazione predefinita viene visualizzato il primo emulatore assegnato al primo gruppo di dispositivi assegnato al sito. Gli emulatori possono essere attivati tramite il carosello emulatore nella parte superiore della pagina o tramite il pulsante di modifica della barra laterale.

**Creazione di un emulatore**

Per creare un emulatore, consultare la sezione [Creazione di un emulatore](/help/sites-developing/emulators.md) mobile personalizzato nella pagina emulatori generici.

**Caratteristiche principali degli emulatori mobili**

* Un gruppo di dispositivi è composto da uno o più emulatori: la pagina di configurazione del gruppo di dispositivi, ad esempio /etc/mobile/groups/touch, contiene la `emulators` proprietà sotto il `jcr:content` nodo.
Nota: anche se è possibile che lo stesso emulatore appartenga a diversi gruppi di dispositivi, non ha molto senso.

* Tramite la finestra di dialogo di configurazione del gruppo di dispositivi, la `emulators` proprietà viene impostata con il percorso dell&#39;emulatore o degli emulatori desiderati. Esempio: `/libs/wcm/mobile/components/emulators/iPhone4`.

* Componenti dell’emulatore (ad esempio `/libs/wcm/mobile/components/emulators/iPhone4`) estendere il componente emulatore mobile di base ( `/libs/wcm/mobile/components/emulators/base`).

* Ogni componente che estende l’emulatore mobile di base è disponibile per la selezione quando si configura un gruppo di dispositivi. Gli emulatori personalizzati possono essere facilmente creati o estesi.
* Al momento della richiesta in modalità di modifica, l&#39;implementazione dell&#39;emulatore viene utilizzata per eseguire il rendering della pagina.
* Quando il modello della pagina si basa sul componente della pagina mobile, le funzionalità dell’emulatore vengono automaticamente integrate nella pagina (tramite il componente `head.jsp` della pagina mobile).

### Gruppi dispositivo {#device-groups}

I gruppi di dispositivi mobili forniscono la segmentazione dei dispositivi mobili in base alle funzionalità del dispositivo. Un gruppo di dispositivi fornisce le informazioni necessarie per l’authoring basato sull’emulatore nell’istanza di creazione e per il corretto rendering del contenuto nell’istanza di pubblicazione: dopo che gli autori hanno aggiunto contenuto alla pagina mobile e l’hanno pubblicata, la pagina può essere richiesta nell’istanza di pubblicazione. Qui, invece della visualizzazione di modifica dell&#39;emulatore, viene eseguito il rendering della pagina del contenuto utilizzando uno dei gruppi di dispositivi configurati. La selezione del gruppo di dispositivi avviene in base al rilevamento [dei dispositivi](#devicedetection)mobili. Il gruppo di dispositivi corrispondente fornisce quindi le informazioni di stile necessarie.

I gruppi di dispositivi sono definiti come pagine di contenuto sotto `/etc/mobile/devices` e utilizzano il modello Gruppo **di dispositivi** mobili. Il modello per gruppi di dispositivi funge da modello di configurazione per le definizioni dei gruppi di dispositivi nel modulo delle pagine di contenuto. Le sue caratteristiche principali sono:

* Posizione: `/libs/wcm/mobile/templates/devicegroup`
* Percorso consentito: `/etc/mobile/groups/*`
* Componente pagina: `wcm/mobile/components/devicegroup`

#### Assegnazione di gruppi di dispositivi al sito {#assigning-device-groups-to-your-site}

Quando create un sito mobile, dovete assegnare gruppi di dispositivi al sito. AEM offre tre gruppi di dispositivi a seconda delle capacità di rendering HTML e JavaScript del dispositivo:

* **Caratteristica** per dispositivi quali Sony Ericsson W800 con supporto per HTML di base ma nessun supporto per immagini e JavaScript.
* **Smartphone** , per dispositivi come Blackberry con supporto per HTML e immagini di base, ma senza supporto per JavaScript.

* **Smartphone touch** , per dispositivi come l’iPad con supporto completo per HTML, immagini, JavaScript e rotazione del dispositivo.

Poiché gli emulatori possono essere associati a un gruppo di dispositivi (consultate la sezione [Creazione di un gruppo](#creating-a-device-group)di dispositivi), l&#39;assegnazione di un gruppo di dispositivi a un sito consente agli autori di selezionare tra gli emulatori associati al gruppo di dispositivi per modificare la pagina.

Per assegnare un gruppo di dispositivi al sito:

1. Nel browser, passate alla console **Site Admin** (Amministrazione sito).
1. Aprite la pagina principale del sito mobile sotto **Siti Web**.
1. Aprire le proprietà della pagina.
1. Select the **Mobile** tab:

   * Definite i gruppi di dispositivi.
   * Fai clic su **OK**. 

>[!NOTE]
>
>Quando i gruppi di dispositivi sono stati definiti per un sito, vengono ereditati da tutte le pagine del sito.

#### Filtri per gruppo dispositivo {#device-group-filters}

I filtri per gruppi di dispositivi definiscono criteri basati sulle funzionalità per determinare se un dispositivo appartiene al gruppo. Quando create un gruppo di dispositivi, potete selezionare i filtri da utilizzare per valutare i dispositivi.

In fase di esecuzione, quando AEM riceve una richiesta HTTP da un dispositivo, ogni filtro associato a un gruppo confronta le funzionalità del dispositivo con criteri specifici. Il dispositivo è considerato appartenente al gruppo quando dispone di tutte le funzionalità richieste dai filtri. Le funzionalità vengono recuperate dal database WURFL™.

I gruppi di dispositivi possono utilizzare zero o più filtri per il rilevamento delle funzionalità. È inoltre possibile utilizzare un filtro con più gruppi di dispositivi. AEM fornisce un filtro predefinito che determina se il dispositivo dispone delle funzionalità selezionate per un gruppo:

* CSS
* Immagini JPG e PNG
* JavaScript
* Rotazione dispositivo

Se il gruppo di dispositivi non utilizza un filtro, le funzionalità selezionate configurate per il gruppo sono le uniche che un dispositivo richiede.

Per ulteriori informazioni, consulta [Creazione di filtri](/help/sites-developing/groupfilters.md)per gruppi di dispositivi.

#### Creazione di un gruppo di dispositivi {#creating-a-device-group}

Crea un gruppo di dispositivi quando i gruppi installati da AEM non soddisfano i tuoi requisiti.

1. In your browser, go to the **Tools** console.
1. Crea una nuova pagina in **Strumenti** > **Mobile** > Gruppi **di** dispositivi. Nella finestra di dialogo **Crea pagina** :

   * Come **Titolo** immettete `Special Phones`.

   * Come **Nome** immettete `special`.

   * Selezionate il modello **del gruppo di dispositivi** mobili.
   * Fai clic su **Crea**. 

1. In CRXDE, aggiungete un file **static.css** contenente gli stili per il gruppo di dispositivi sotto il `/etc/mobile/groups/special` nodo.

1. Aprite la pagina **Telefoni** speciali.
1. Per configurare il gruppo di dispositivi, fate clic sul pulsante **Modifica** accanto a **Impostazioni**.
Nella scheda **Generale** :

   * **Titolo**: il nome del gruppo del dispositivo mobile.
   * **Descrizione**: descrizione del gruppo.
   * **Agente** utente: stringa agente utente con cui viene confrontata la corrispondenza tra i dispositivi. È opzionale e può essere un regex. Esempio: `BlackBerryZ10`
   * **Funzionalità**: definisce se il gruppo può gestire immagini, CSS, JavaScript o rotazione del dispositivo.
   * **Larghezza** e altezza minima **dello schermo**
   * **Disattiva emulatore**: per attivare/disattivare l&#39;emulatore durante la modifica del contenuto.
   Nella scheda **Emulatori** :

   * **Emulatori**: selezionare gli emulatori assegnati a questo gruppo di dispositivi.
   Nella scheda **Filtri** :

   * Per aggiungere un filtro, fate clic su Aggiungi elemento e selezionate un filtro dall’elenco a discesa.
   * I filtri vengono valutati nell&#39;ordine in cui appaiono. Quando un dispositivo non soddisfa i criteri di un filtro, i filtri successivi nell&#39;elenco non vengono valutati.



1. Fate clic su OK.

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

Per informazioni, andate a [Creazione di filtri](/help/sites-developing/groupfilters.md)per gruppi di dispositivi.

### Utilizzo del database WURFL™ {#using-the-wurfl-database}

AEM utilizza una versione troncata del database [WURFL](https://wurfl.sourceforge.net/)™ per eseguire query sulle funzionalità dei dispositivi, come la risoluzione dello schermo o il supporto JavaScript, in base all&#39;agente utente del dispositivo.

Il codice XML del database WURFL™ è rappresentato come nodi di seguito `/var/mobile/devicespecs` analizzando il `wurfl.xml`file in `/libs/wcm/mobile/devicespecs/wurfl.xml.` L&#39;espansione ai nodi si verifica la prima volta che il `cq-mobile-core` bundle viene avviato.

Le funzionalità dei dispositivi sono memorizzate come proprietà dei nodi e i nodi rappresentano modelli di dispositivi. Potete utilizzare le query per recuperare le funzionalità di un dispositivo o agente utente.

Poiché il database WURFL™ si sta evolvendo, potrebbe essere necessario personalizzarlo o sostituirlo. Per aggiornare il database dei dispositivi mobili sono disponibili le seguenti opzioni:

* Se disponete di una licenza che consente tale utilizzo, sostituite il file con la versione più recente. Vedere Installazione di un altro database WURFL.
* Utilizzate la versione disponibile in AEM e configurate un regexp che corrisponda alle stringhe Agente-utente e punti a un dispositivo WURFL™ esistente. Consultate [Aggiunta di un abbinamento](#adding-a-regexp-based-user-agent-matching)utente-agente basato su regexp.

#### Verifica della mappatura di un agente utente alle funzionalità WURFL™ {#testing-the-mapping-of-a-user-agent-to-wurfl-capabilities}

Quando un dispositivo accede al sito mobile, AEM rileva il dispositivo, lo mappa a un gruppo di dispositivi in base alle sue capacità e invia una visualizzazione della pagina che corrisponde al gruppo di dispositivi. Il gruppo di dispositivi corrispondente fornisce le informazioni di stile necessarie. Le mappature possono essere testate nella pagina di test dell&#39;agente utente mobile:

`https://localhost:4502/etc/mobile/useragent-test.html`

#### Installazione di un database WURFL™ diverso {#installing-a-different-wurfl-database}

Il database WURFL™ troncato installato con AEM è una versione precedente al 30 agosto 2011. Se la vostra versione del WURFL è stata rilasciata dopo il 30 agosto 2011, accertatevi che l&#39;utilizzo sia conforme alla licenza.

Per installare un database WURFL™:

1. In CRXDE Lite, create la seguente cartella: `/apps/wcm/mobile/devicespecs`
1. Copiate il file WURFL™ nella cartella.
1. Rinominare il file come `wurfl.xml`.

AEM analizza automaticamente il `wurfl.xml` file e aggiorna i nodi sottostanti `/var/mobile/devicespecs`.

>[!NOTE]
>
>Quando il database WURFL™ completo è abilitato, l&#39;analisi e l&#39;attivazione potrebbero richiedere alcuni minuti. È possibile controllare i registri per informazioni sull’avanzamento.

#### Aggiunta di una corrispondenza agente utente basata su regexp {#adding-a-regexp-based-user-agent-matching}

Aggiungi un agente utente come espressione regolare di seguito /apps/wcm/mobile/devicspecs/wurfl/regexp per puntare a un tipo di dispositivo WURFL™ esistente.

1. In **CRXDE Lite**, create un nodo sotto /apps/wcm/mobile/devicspecs/regexp, ad esempio apple_ipad_ver1.
1. Aggiungi le seguenti proprietà al nodo:

   * **regexp**: espressione regolare che definisce gli agenti utente, ad esempio: .*Mozilla.*iPad.*AppleWebKit.*Safari.*
   * **deviceId**: l’ID dispositivo come definito nel file wurfl.xml, ad esempio: apple_ipad_ver1

La configurazione precedente causa la mappatura dei dispositivi per i quali l&#39;agente utente corrisponde all&#39;espressione regolare fornita all&#39;ID dispositivo apple_ipad_ver1 WURFL™, se esistente.

## Rilevamento dispositivo lato client {#client-side-device-detection}

Questa sezione descrive come utilizzare il rilevamento lato client del dispositivo di AEM per ottimizzare il rendering della pagina o fornire al client versioni alternative del sito Web.

AEM supporta il rilevamento lato client del dispositivo in base a `BrowserMap`. `BrowserMap` viene fornito in AEM come libreria client in `/etc/clientlibs/browsermap`.

`BrowserMap` fornisce tre strategie che potete utilizzare per fornire un sito Web alternativo a un cliente, che vengono utilizzate nel seguente ordine:

1. [Collegamenti alternativi](#providing-alternate-links)
1. [URL specifico per il gruppo di dispositivi](#definingdevicegroupspecificurl)
1. [URL basato su selettore](#defining-selector-based-urls)

>[!NOTE]
>
>Per ulteriori informazioni sull&#39;integrazione con la libreria client, consultate la sezione [Utilizzo delle librerie](/help/sites-developing/clientlibs.md) HTML lato client.

### Collegamenti Alternativi {#providing-alternate-links}

Il servizio `PageVariantsProvider` OSGi è in grado di generare collegamenti alternativi per siti appartenenti alla stessa famiglia. Per configurare i siti da prendere in considerazione dal servizio, è necessario aggiungere un `cq:siteVariant` nodo al `jcr:content` nodo dalla radice del sito.

Il `cq:siteVariant` nodo deve avere le seguenti proprietà:

* `cq:childNodesMapTo` - determina a quale attributo dell&#39;elemento di collegamento saranno mappati i nodi secondari; si consiglia di organizzare il contenuto del sito Web in modo che gli elementi secondari del nodo principale rappresentino la radice di una variante della lingua del sito Web globale (ad esempio `/content/mysite/en`, `/content/mysite/de`), nel qual caso il valore del `cq:childNodesMapTo` prodotto deve essere `hreflang`;
* `cq:variantDomain` - indica quale `Externalizer` dominio verrà utilizzato per generare gli URL assoluti delle varianti di pagina; se questo valore non è impostato, le varianti di pagina verranno generate utilizzando collegamenti relativi;
* `cq:variantFamily` - indica a quale famiglia di siti web appartiene questo sito; più rappresentazioni per dispositivo dello stesso sito web dovrebbero appartenere alla stessa famiglia;
* `media` - memorizza i valori dell&#39;attributo media dell&#39;elemento link; si consiglia di utilizzare il nome della `BrowserMap` libreria registrata `DeviceGroups``BrowserMap` , in modo che possa inoltrare automaticamente i client alla variante corretta del sito Web.

#### PageVariantsProvider ed Externalizer {#pagevariantsprovider-and-externalizer}

Quando il valore della `cq:variantDomain` proprietà di un `cq:siteVariant` nodo non è vuoto, il `PageVariantsProvider` servizio genererà collegamenti assoluti utilizzando questo valore come dominio configurato per il `Externalizer` servizio. Accertatevi di configurare il `Externalizer` servizio in modo che rifletta la configurazione.

>[!NOTE]
>
>When working with AEM there are several methods of managing the configuration settings for such services; see [Configuring OSGi](/help/sites-deploying/configuring-osgi.md) for more details and the recommended practices.

### Definizione di un URL specifico per un gruppo di dispositivi {#defining-a-device-group-specific-url}

Se non desiderate utilizzare collegamenti alternativi, potete configurare un URL globale per ciascuno di essi `DeviceGroup`. È consigliabile creare una libreria client personalizzata che incorpora la libreria `browsermap.standard` client e ridefinisca i gruppi di dispositivi.

BrowserMap è progettato in modo tale che le definizioni dei gruppi di dispositivi possano essere ignorate creando e aggiungendo un nuovo gruppo di dispositivi con lo stesso nome all&#39; `BrowserMap` oggetto dalla libreria client personalizzata.

>[!NOTE]
>
>Per ulteriori dettagli, consulta la sezione [Personalizzato BrowserMap](#creatingacustomisedbrowsermap) .

### Definizione degli URL basati su selettore {#defining-selector-based-urls}

Se non è stato utilizzato nessuno dei meccanismi precedenti per indicare un sito alternativo per `BrowserMap`, i selettori che utilizzeranno i nomi dei `DeviceGroups` verranno aggiunti agli `URL`s, nel qual caso dovreste fornire i vostri servlet che gestiranno le richieste.

Ad esempio, una ricerca per dispositivi `www.example.com/index.html` identificata come `smartphone` da BrowserMap viene inoltrata a `www.example.com/index.smartphone.html.`

### Utilizzo di BrowserMap sulle pagine {#using-browsermap-on-your-pages}

Per utilizzare la libreria client BrowserMap standard in una pagina, è necessario includere il `/libs/wcm/core/browsermap/browsermap.jsp` file utilizzando un `cq:include`tag nella `head` sezione della pagina.

```xml
<cq:include script="/libs/wcm/core/browsermap/browsermap.jsp" />
```

Oltre ad aggiungere la libreria `BrowserMap` client nei `JSP` file, è anche necessario aggiungere una proprietà `cq:deviceIdentificationMode` String impostata `client-side` al `jcr:content` nodo sotto la radice del sito Web.

### Ignorare il comportamento predefinito di BrowserMap {#overriding-browsermap-s-default-behaviour}

Se desiderate personalizzare `BrowserMap` - ignorando `DeviceGroups` o aggiungendo più sonde - dovete creare una vostra libreria client-side in cui incorporate la libreria lato `browsermap.standard`client.

Inoltre, è necessario chiamare manualmente il `BrowserMap.forwardRequest()` metodo nel `JavaScript` codice.

>[!NOTE]
>
>Per ulteriori informazioni sull&#39;integrazione con la libreria client, consultate la sezione [Utilizzo delle librerie](/help/sites-developing/clientlibs.md) HTML lato client.

Dopo aver creato la libreria `BrowserMap` client personalizzata, consigliamo il seguente approccio:

1. Creare un `browsermap.jsp` file nell’applicazione

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

1. Includete il `broswermap.jsp` file nella sezione head.

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

In questo modo lo `/libs/wcm/core/browsermap/browsermap.jsp` script aggiungerà un tag meta alla pagina che non eseguirà `BrowserMap` alcuna rilevazione:

```xml
<meta name="browsermap.enabled" content="false">
```

### Verifica di una versione specifica di un sito Web {#testing-a-specific-version-of-a-web-site}

Normalmente, lo script BrowserMap reindirizzerà sempre i visitatori alla versione più adatta del sito Web, in genere reindirizzando i visitatori al desktop o al sito mobile quando necessario.

Potete forzare il dispositivo di qualsiasi richiesta per testare una versione specifica di un sito Web aggiungendo il `device` parametro all’URL. Nell’URL riportato di seguito viene visualizzata la versione mobile del sito Web Geometrixx Outdoors.

`https://localhost:4502/content/geometrixx-outdoors/en.html?wcmmode=disabled&device=smartphone`

>[!NOTE]
>
>Il `wcmmode` parametro è impostato `disabled` per simulare il comportamento di un’istanza di pubblicazione.

Il valore del dispositivo ignorato viene memorizzato in un cookie in modo da poter esplorare il sito Web senza aggiungere il `device` parametro a ciascuno di essi `URL`.

Di conseguenza, è necessario chiamare lo stesso `URL` con il `device` set `browser` per tornare alla versione desktop del sito Web.

>[!NOTE]
>
>BrowserMap memorizza il valore del dispositivo ignorato in un cookie denominato `BMAP_device`. Se eliminate questo cookie, CQ distribuirà la versione appropriata del sito Web in base al dispositivo corrente (ad esempio, desktop o mobile).

## Elaborazione richiesta mobile {#mobile-request-processing}

AEM elabora una richiesta emessa da un dispositivo mobile appartenente al gruppo di dispositivi touch come segue:

1. Un iPad invia una richiesta all’istanza di pubblicazione AEM, ad esempio `https://localhost:4503/content/geometrixx_mobile/en/products.html`
1. AEM determina se il sito della pagina richiesta è un sito mobile (verificando se la pagina di primo livello `/content/geometrixx_mobile` estende il componente della pagina mobile). In caso affermativo:
1. AEM cerca le funzionalità del dispositivo in base all’agente utente nell’intestazione della richiesta.
1. AEM mappa le funzionalità del dispositivo al gruppo di dispositivi e le imposta `touch` come selettore del gruppo di dispositivi.
1. AEM reindirizza la richiesta a `https://localhost:4503/content/geometrixx_mobile/en/products.touch.html.`
1. AEM invia la risposta all’iPad:

   * `products.touch.html` è rappresentato nel modo usuale ed è memorizzabile nella cache.
   * I componenti di rendering utilizzano i selettori per adattare la presentazione.
   * AEM aggiunge automaticamente il selettore mobile a tutti i collegamenti interni nella pagina.

### Statistiche {#statistics}

Puoi ottenere alcune statistiche sul numero di richieste inviate al server AEM da dispositivi mobili. È possibile suddividere il numero di richieste:

* per gruppo di dispositivi e dispositivo
* anno, mese e giorno

Per visualizzare le statistiche:

1. Go to the **Tools** console.
1. Aprite la pagina Statistiche **** dispositivo in **Strumenti** > **Mobile**.
1. Fate clic sul collegamento per visualizzare le statistiche relative a un anno, mese o giorno specifico.

La pagina **Statistiche** si presenta come segue:

![screen_shot_2012-02-01at24353pm](assets/screen_shot_2012-02-01at24353pm.png)

>[!NOTE]
>
>La pagina **Statistiche** viene creata la prima volta che un dispositivo mobile accede ad AEM e viene rilevata. Prima di questo, non è disponibile.

Per generare una voce nelle statistiche, è possibile procedere come segue:

1. Usate un dispositivo mobile o un emulatore (ad esempio https://chrispederick.com/work/user-agent-switcher/ su Firefox).
1. Richiedete una pagina mobile nell’istanza di creazione disattivando la modalità di authoring, ad esempio:
   `https://localhost:4502/content/geometrixx_mobile/en/products.html?wcmmode=disabled`

È ora disponibile la pagina **Statistiche** .

### Memorizzazione nella cache delle pagine per i collegamenti &quot;Invia collegamento a un amico&quot; {#supporting-page-caching-for-send-link-to-a-friend-links}

Le pagine mobili sono generalmente memorizzabili nella cache del dispatcher, perché le pagine di cui viene eseguito il rendering per un gruppo di dispositivi sono distinte nell&#39;URL della pagina dal selettore del gruppo di dispositivi, ad esempio `/content/mobilepage.touch.html`. Una richiesta a una pagina mobile senza un selettore non viene mai memorizzata nella cache, come in questo caso, il rilevamento del dispositivo funziona e alla fine viene reindirizzato al gruppo di dispositivi corrispondente (o alla &quot;copia&quot; in quel caso). Il rendering di una pagina mobile con un selettore di gruppi di dispositivi viene elaborato dalla riscrittura dei collegamenti, che riscrive tutti i collegamenti all&#39;interno della pagina per contenere anche il selettore di gruppi di dispositivi, impedendo la ripetizione del rilevamento dispositivi per ogni clic su una pagina già qualificata.

Di conseguenza, si potrebbe verificare il seguente scenario:

L&#39;utente Alice viene reindirizzato a `coolpage.feature.html`, e invia l&#39;URL a un amico Bob che accede con un altro client appartenente al gruppo `touch` del dispositivo.

Se `coolpage.feature.html` viene distribuito da una cache front-end, AEM non ha la possibilità di analizzare la richiesta per scoprire che il selettore mobile non corrisponde al nuovo agente utente e Bob riceve la rappresentazione sbagliata.

Per risolverlo, puoi includere una semplice interfaccia utente di selezione nelle pagine, in cui gli utenti finali possono ignorare il gruppo di dispositivi selezionato da AEM. Nell&#39;esempio precedente, un collegamento (o un&#39;icona) sulla pagina consente all&#39;utente finale di passare a `coolpage.touch.html` se ritiene che il dispositivo sia sufficientemente adatto.
