---
title: Creazione di siti per dispositivi mobili
description: La creazione di un sito mobile è simile alla creazione di un sito standard, in quanto comporta anche la creazione di modelli e componenti
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
docset: aem65
legacypath: /content/docs/en/aem/6-0/develop/mobile/mobile
exl-id: 21b2037a-685a-441d-aecd-865884253e03
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '3701'
ht-degree: 0%

---

# Creazione di siti per dispositivi mobili{#creating-sites-for-mobile-devices}

{{ue-over-mobile}}

La creazione di un sito mobile è simile alla creazione di un sito standard, in quanto comporta anche la creazione di modelli e componenti. Per ulteriori dettagli sulla creazione di modelli e componenti, vedere le pagine seguenti: [Modelli](/help/sites-developing/templates.md), [Componenti](/help/sites-developing/components.md) e [Guida introduttiva allo sviluppo di AEM Sites](/help/sites-developing/getting-started.md). La differenza principale consiste nell’abilitare le funzionalità mobili integrate di Adobe Experience Manager (AEM) all’interno del sito. Ciò si ottiene creando un modello che si basa sul componente Pagina mobile.

È consigliabile utilizzare la [progettazione reattiva](/help/sites-developing/responsive.md), creando un singolo sito che supporta più dimensioni dello schermo.

Per iniziare, puoi dare un&#39;occhiata al **sito dimostrativo mobile We.Retail** disponibile in AEM.

Per creare un sito mobile, procedi come segue:

1. Creare il componente Pagina:

   * Imposta la proprietà `sling:resourceSuperType` su `wcm/mobile/components/page`
In questo modo il componente si basa sul componente Pagina mobile.

   * Crea `body.jsp` con la logica specifica del progetto.

1. Creare il modello di pagina:

   * Impostare la proprietà `sling:resourceType` sul componente pagina appena creato.
   * Impostare la proprietà `allowedPaths`.

1. Crea la pagina di progettazione per il sito.
1. Creare la pagina principale del sito sotto il nodo `/content`:

   * Impostare la proprietà `cq:allowedTemplates`.
   * Impostare la proprietà `cq:designPath`.

1. Nelle proprietà della pagina principale del sito, imposta i gruppi di dispositivi nella scheda **Mobile**.
1. Creare le pagine del sito utilizzando il nuovo modello.

Componente pagina mobile ( `/libs/wcm/mobile/components/page`):

* Aggiunge la scheda **Mobile** alla finestra di dialogo delle proprietà della pagina.
* Tramite il relativo `head.jsp`, recupera il gruppo di dispositivi mobili corrente dalla richiesta e, se viene trovato un gruppo di dispositivi, utilizza il metodo `drawHead()` del gruppo per includere il componente init dell&#39;emulatore associato al gruppo di dispositivi (solo in modalità di authoring) e il CSS di rendering del gruppo di dispositivi.

>[!NOTE]
>
>La pagina principale del sito mobile deve trovarsi al livello 1 della gerarchia dei nodi ed è consigliabile trovarsi al di sotto del nodo /content.

## Creazione di un sito mobile con Multi Site Manager {#creating-a-mobile-site-with-the-multi-site-manager}

Utilizza Multi Site Manager (MSM) per creare una Live Copy mobile da un sito standard. Il sito standard viene trasformato automaticamente in un sito mobile: il sito mobile dispone di tutte le funzioni dei siti mobili (ad esempio, l’edizione all’interno di un emulatore) e può essere gestito in sincronia con il sito standard. Consulta la sezione [Creazione di una Live Copy per canali diversi](/help/sites-administering/msm.md) nella pagina Multi Site Manager.

## API mobile lato server {#server-side-mobile-api}

I pacchetti Java™ contenenti le classi mobili sono:

* [com.day.cq.wcm.mobile.api](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html) - definisce MobileConstants.
* [com.day.cq.wcm.mobile.api.device](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/mobile/api/device/package-summary.html) - definisce Device, DeviceGroup e DeviceGroupList.
* [com.day.cq.wcm.mobile.api.device.capability](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html) - definisce DeviceCapability.
* [com.day.cq.wcm.mobile.api.wurfl](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/workflow/api/package-summary.html) - definisce WurflQueryEngine.
* [com.day.cq.wcm.mobile.core](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/mobile/core/package-summary.html) - definisce MobileUtil, che fornisce vari metodi di utilità che ruotano intorno a WCM Mobile.

### Componenti mobili {#mobile-components}

Il **sito di dimostrazione mobile We.Retail** utilizza i seguenti componenti mobili che si trovano sotto `/libs/foundation/components`:

<table>
 <tbody>
  <tr>
   <td>Nome</td>
   <td>Gruppo</td>
   <td>Caratteristiche</td>
  </tr>
  <tr>
   <td>mobilefooter</td>
   <td>nascosto</td>
   <td>- piè di pagina</td>
  </tr>
  <tr>
   <td>mobileimage</td>
   <td>Mobile</td>
   <td>- in base al componente image foundation <br /> - esegue il rendering di un'immagine se il dispositivo è in grado di eseguire il rendering<br /> </td>
  </tr>
  <tr>
   <td>mobilelist</td>
   <td>Mobile</td>
   <td>- in base al componente list foundation<br /> - listitem_teaser.jsp esegue il rendering di un'immagine se il dispositivo è in grado di eseguire il rendering<br /> </td>
  </tr>
  <tr>
   <td>mobilelogo</td>
   <td>nascosto</td>
   <td>- in base al componente di base logo<br /> - esegue il rendering di un'immagine se il dispositivo è in grado<br /> </td>
  </tr>
  <tr>
   <td>riferimento mobile</td>
   <td>Mobile</td>
   <td><p>- simile al componente base di riferimento</p> <p>: mappa un componente textimage su un elemento mobiletextimage 1 e un componente immagine su un elemento mobiletextimage 1</p> </td>
  </tr>
  <tr>
   <td>mobiletextimage</td>
   <td>Mobile</td>
   <td>- in base al componente di base textimage<br /> - esegue il rendering di un'immagine se il dispositivo è in grado di</td>
  </tr>
  <tr>
   <td>mobiletopnav</td>
   <td>nascosto</td>
   <td><p>- basato sul componente topnav foundation</p> <p>- esegue solo il rendering del testo</p> </td>
  </tr>
 </tbody>
</table>

#### Creazione di un componente mobile {#creating-a-mobile-component}

Il framework per dispositivi mobili AEM consente di sviluppare componenti sensibili al dispositivo che emette la richiesta. Gli esempi di codice seguenti mostrano come utilizzare l’API mobile dell’AEM in un componente jsp e in particolare come:

* Ottieni il dispositivo dalla richiesta:
  `Device device = slingRequest.adaptTo(Device.class);`

* Ottieni il gruppo di dispositivi:
  `DeviceGroup deviceGroup = device.getDeviceGroup();`

* Ottieni le funzionalità del gruppo di dispositivi:
  `Collection<DeviceCapability> capabilities = deviceGroup.getCapabilities();`

* Ottieni gli attributi del dispositivo (chiave/valori di capacità non elaborati dal database WURFL):
  `Map<String,String> deviceAttributes = device.getAttributes();`

* Ottieni l’agente utente del dispositivo:
  `String userAgent = device.getUserAgent();`

* Ottieni l’elenco dei gruppi di dispositivi (gruppi di dispositivi assegnati al sito dall’autore) dalla pagina corrente:
  `DeviceGroupList deviceGroupList = currentPage.adaptTo(DeviceGroupList.class);`

* Verifica se il gruppo di dispositivi supporta le immagini
  `if (deviceGroup.hasCapability(DeviceCapability.CAPABILITY_IMAGES)) {`
...
OPPURE
  `if MobileUtil.hasCapability(request, DeviceCapability.CAPABILITY_IMAGES) {`
...

>[!NOTE]
>
>In un JSP, `slingRequest` è disponibile tramite il tag `<sling:defineObjects>` e `currentPage` tramite il tag `<cq:defineObjects>`.

### Emulatori {#emulators}

L’authoring basato su emulatore consente agli autori di creare pagine di contenuti destinate ai clienti di dispositivi mobili. L’authoring dei contenuti per dispositivi mobili segue lo stesso principio dell’editing sul posto di WYSIWYG. Affinché gli autori possano percepire l’aspetto della pagina su un dispositivo mobile, una pagina di contenuto mobile viene modificata utilizzando un emulatore di dispositivo.

Gli emulatori per dispositivi mobili si basano sul framework dell’emulatore generico. Per ulteriori dettagli, vedi [Emulatori](/help/sites-developing/emulators.md).

L’emulatore del dispositivo visualizza il dispositivo mobile sulla pagina, mentre le normali modifiche (parsys, componenti) si verificano all’interno dello schermo del dispositivo. L’emulatore di dispositivi dipende dai gruppi di dispositivi configurati per il sito. È possibile assegnare diversi emulatori a un gruppo di dispositivi. Tutti gli emulatori sono quindi disponibili nella pagina del contenuto. Per impostazione predefinita, viene visualizzato il primo emulatore assegnato al primo gruppo di dispositivi assegnato al sito. Gli emulatori possono essere commutati tramite il carosello dell&#39;emulatore nella parte superiore della pagina o tramite il pulsante di modifica del Sidekick.

**Creazione di un emulatore**

Per creare un emulatore, vedere [Creazione di un emulatore mobile personalizzato](/help/sites-developing/emulators.md) nella pagina degli emulatori generici.

**Caratteristiche principali degli emulatori mobili**

* Un gruppo di dispositivi è composto da uno o più emulatori: la pagina di configurazione del gruppo di dispositivi, ad esempio /etc/mobile/groups/touch, contiene la proprietà `emulators` sotto il nodo `jcr:content`.
Nota: anche se è possibile che lo stesso emulatore appartenga a diversi gruppi di dispositivi, non ha molto senso.

* Tramite la finestra di dialogo di configurazione del gruppo di dispositivi, la proprietà `emulators` viene impostata con il percorso degli emulatori desiderati. Ad esempio: `/libs/wcm/mobile/components/emulators/iPhone4`.

* I componenti emulatore (ad esempio, `/libs/wcm/mobile/components/emulators/iPhone4`) estendono il componente emulatore mobile di base ( `/libs/wcm/mobile/components/emulators/base`).

* Ogni componente che estende l’emulatore mobile di base è disponibile per la selezione durante la configurazione di un gruppo di dispositivi. Gli emulatori personalizzati possono quindi essere facilmente creati o estesi.
* Al momento della richiesta in modalità di modifica, per eseguire il rendering della pagina viene utilizzata l’implementazione dell’emulatore.
* Quando il modello della pagina si basa sul componente Pagina mobile, le funzionalità dell’emulatore vengono integrate automaticamente nella pagina (tramite `head.jsp` del componente Pagina mobile).

### Gruppi dispositivo {#device-groups}

I gruppi di dispositivi mobili forniscono la segmentazione dei dispositivi mobili in base alle funzionalità del dispositivo. Un gruppo di dispositivi fornisce le informazioni necessarie per l’authoring basato su emulatori nell’istanza di authoring e per il rendering corretto dei contenuti nell’istanza di pubblicazione: una volta che gli autori hanno aggiunto contenuti alla pagina mobile e l’hanno pubblicata, la pagina può essere richiesta nell’istanza di pubblicazione. Al suo posto, la vista di modifica dell’emulatore riproduce la pagina di contenuto utilizzando uno dei gruppi di dispositivi configurati. La selezione del gruppo di dispositivi si verifica in base al [rilevamento dispositivi mobili](#devicedetection). Il gruppo di dispositivi corrispondente fornisce quindi le informazioni necessarie sullo stile.

I gruppi di dispositivi sono definiti come pagine di contenuto sotto `/etc/mobile/devices` e utilizzano il modello **Gruppo di dispositivi mobili**. Il modello gruppo di dispositivi funge da modello di configurazione per le definizioni dei gruppi di dispositivi sotto forma di pagine di contenuto. Le sue caratteristiche principali sono:

* Percorso: `/libs/wcm/mobile/templates/devicegroup`
* Percorso consentito: `/etc/mobile/groups/*`
* Componente pagina: `wcm/mobile/components/devicegroup`

#### Assegnazione di gruppi di dispositivi al sito {#assigning-device-groups-to-your-site}

Quando crei un sito mobile, devi assegnare gruppi di dispositivi al sito. L’AEM fornisce tre gruppi di dispositivi a seconda delle funzionalità di rendering HTML e JavaScript del dispositivo:

* **Telefoni Feature**, per dispositivi come Sony Ericsson W800 con supporto per HTML di base, ma senza supporto per immagini e JavaScript.
* **Telefoni Smart**, per dispositivi come BlackBerry® con supporto per HTML e immagini di base, ma senza supporto per JavaScript.

* **Telefoni touch**, per dispositivi come iPad con supporto completo per HTML, immagini, JavaScript e rotazione dei dispositivi.

Poiché gli emulatori possono essere associati a un gruppo di dispositivi (vedere la sezione [Creazione di un gruppo di dispositivi](#creating-a-device-group)), l&#39;assegnazione di un gruppo di dispositivi a un sito consente agli autori di selezionare tra gli emulatori associati al gruppo di dispositivi per modificare la pagina.

Per assegnare un gruppo di dispositivi al sito:

1. Nel browser, accedi alla console **Siteadmin**.
1. Apri la pagina root del tuo sito mobile sotto **Siti Web**.
1. Apri le proprietà della pagina.
1. Selezionare la scheda **Mobile**:

   * Definisci i gruppi di dispositivi.
   * Fai clic su **OK**.

>[!NOTE]
>
>Una volta definiti i gruppi di dispositivi per un sito, questi vengono ereditati da tutte le pagine del sito.

#### Filtri per gruppo dispositivo {#device-group-filters}

I filtri per gruppi di dispositivi definiscono criteri basati sulle funzionalità per determinare se un dispositivo appartiene al gruppo. Quando crei un gruppo di dispositivi, puoi selezionare i filtri da utilizzare per la valutazione dei dispositivi.

In fase di esecuzione, quando l’AEM riceve una richiesta HTTP da un dispositivo, ogni filtro associato a un gruppo confronta le funzionalità del dispositivo con criteri specifici. Il dispositivo viene considerato appartenente al gruppo quando dispone di tutte le funzionalità necessarie per i filtri. Le funzionalità vengono recuperate dal database WURFL™.

I gruppi di dispositivi possono utilizzare zero o più filtri per il rilevamento delle funzionalità. Inoltre, un filtro può essere utilizzato con più gruppi di dispositivi. L’AEM fornisce un filtro predefinito che determina se il dispositivo dispone delle funzionalità selezionate per un gruppo:

* CSS
* Immagini JPG-e PNG
* JavaScript
* Rotazione del dispositivo

Se il gruppo di dispositivi non utilizza un filtro, le funzionalità selezionate configurate per il gruppo sono le uniche necessarie per un dispositivo.

Per ulteriori informazioni, vedere [Creazione di filtri per gruppi di dispositivi](/help/sites-developing/groupfilters.md).

#### Creazione di un gruppo di dispositivi {#creating-a-device-group}

Creare un gruppo di dispositivi quando i gruppi installati da AEM non soddisfano le proprie esigenze.

1. Nel browser, accedi alla console **Strumenti**.
1. Crea una pagina sotto **Strumenti** > **Dispositivi mobili** > **Gruppi di dispositivi**. Nella finestra di dialogo **Crea pagina**:

   * Come **Titolo**, immetti `Special Phones`.

   * Come **Nome**, immetti `special`.

   * Selezionare il **modello gruppo dispositivi mobili**.
   * Fai clic su **Crea**.

1. In CRXDE, aggiungi un file **static.css** contenente gli stili per il gruppo di dispositivi sotto il nodo `/etc/mobile/groups/special`.

1. Apri la pagina **Telefoni speciali**.
1. Per configurare il gruppo di dispositivi, fare clic sul pulsante **Modifica** accanto a **Impostazioni**.
Nella scheda **Generale**:

   * **Titolo**: nome del gruppo di dispositivi mobili.
   * **Descrizione**: descrizione del gruppo.
   * **Agente-utente**: stringa agente-utente a cui corrispondono i dispositivi. È facoltativo e può essere un regex. Esempio: `BlackBerryZ10`
   * **Funzionalità**: definisce se il gruppo può gestire immagini, CSS, JavaScript o la rotazione del dispositivo.
   * **Larghezza minima dello schermo** e **altezza**
   * **Disabilita emulatore**: per attivare/disattivare l&#39;emulatore durante la modifica del contenuto.

   Nella scheda **Emulatori**:

   * **Emulatori**: selezionare gli emulatori assegnati a questo gruppo di dispositivi.

   Nella scheda **Filtri**:

   * Per aggiungere un filtro, fai clic su Aggiungi elemento, quindi seleziona un filtro dall’elenco a discesa.
   * I filtri vengono valutati nell’ordine in cui vengono visualizzati. Quando un dispositivo non soddisfa i criteri di un filtro, i filtri successivi nell’elenco non vengono valutati.

1. Fare clic su OK.

La finestra di dialogo per la configurazione del gruppo di dispositivi mobili si presenta così:

![schermata_shot_2012-02-01at22043pm](assets/screen_shot_2012-02-01at22043pm.png)

#### CSS personalizzato per gruppo di dispositivi {#custom-css-per-device-group}

Come descritto in precedenza, è possibile associare un CSS personalizzato a una pagina del gruppo di dispositivi, in modo analogo al CSS di una pagina di progettazione. Questo CSS viene utilizzato per influenzare il rendering specifico del gruppo di dispositivi del contenuto della pagina durante l’authoring e la pubblicazione. Questo CSS viene quindi incluso automaticamente:

* Nella pagina dell’istanza di authoring, per ogni emulatore utilizzato da questo gruppo di dispositivi.
* Nella pagina dell’istanza Publish, se l’agente utente della richiesta corrisponde a un dispositivo mobile di questo particolare gruppo di dispositivi.

## Rilevamento dispositivo lato server {#server-side-device-detection}

Utilizza i filtri e una libreria di specifiche del dispositivo per determinare le funzionalità del dispositivo che esegue la richiesta HTTP.

### Sviluppa filtri per gruppo di dispositivi {#develop-device-group-filters}

Crea un filtro per gruppi di dispositivi per definire un set di requisiti di funzionalità per dispositivi. Crea tutti i filtri necessari per eseguire il targeting dei gruppi necessari di funzionalità del dispositivo.

Progetta i filtri in modo da poterne utilizzare le combinazioni per definire i gruppi di funzionalità. In genere, le funzionalità dei diversi gruppi di dispositivi si sovrappongono. Pertanto, è possibile utilizzare alcuni filtri con più definizioni di gruppi di dispositivi.

Dopo aver creato un filtro, puoi utilizzarlo nella configurazione del gruppo.

Per informazioni, passare a [Creazione di filtri per gruppi di dispositivi](/help/sites-developing/groupfilters.md).

### Utilizzo del database WURFL™ {#using-the-wurfl-database}

L&#39;AEM utilizza una versione troncata del database [WURFL](https://wurfl.sourceforge.net/)™ per eseguire query sulle funzionalità del dispositivo, ad esempio la risoluzione dello schermo o il supporto di JavaScript, in base all&#39;agente utente del dispositivo.

Il codice XML del database WURFL™ è rappresentato come nodi al di sotto di `/var/mobile/devicespecs` analizzando il file `wurfl.xml` in `/libs/wcm/mobile/devicespecs/wurfl.xml.`. L&#39;espansione ai nodi viene eseguita al primo avvio del bundle `cq-mobile-core`.

Le funzionalità dei dispositivi sono memorizzate come proprietà dei nodi e i nodi rappresentano modelli di dispositivi. È possibile utilizzare le query per recuperare le funzionalità di un dispositivo o di un agente utente.

Con l&#39;evoluzione del database WURFL™, potrebbe essere necessario personalizzarlo o sostituirlo. Per aggiornare il database dei dispositivi mobili, sono disponibili le seguenti opzioni:

* Sostituisci il file con la versione più recente, se disponi di una licenza che consente questo utilizzo. Vedere Installazione di un altro database WURFL.
* Utilizza la versione disponibile in AEM e configura un regexp che corrisponda alle stringhe dell’agente utente e punti a un dispositivo WURFL™ esistente. Vedere [Aggiunta di una corrispondenza agente utente basata su regexp](#adding-a-regexp-based-user-agent-matching).

#### Verifica della mappatura di un agente utente sulle funzionalità WURFL™ {#testing-the-mapping-of-a-user-agent-to-wurfl-capabilities}

Quando un dispositivo accede al sito mobile, l’AEM rileva il dispositivo, lo mappa su un gruppo di dispositivi in base alle sue funzionalità e invia una visualizzazione della pagina che corrisponde al gruppo di dispositivi. Il gruppo di dispositivi corrispondente fornisce le informazioni necessarie sullo stile. Le mappature possono essere testate nella pagina di test agente utente mobile:

`https://localhost:4502/etc/mobile/useragent-test.html`

#### Installazione di un database WURFL™ diverso {#installing-a-different-wurfl-database}

Il database WURFL™ troncato installato con AEM è una versione precedente a quella
30 agosto 2011. Se la tua versione del WURFL è stata rilasciata dopo il 30 agosto 2011, assicurati che il tuo utilizzo sia conforme alla licenza.

Per installare un database WURFL™:

1. In CRXDE Lite, creare la cartella seguente: `/apps/wcm/mobile/devicespecs`
1. Copiare il file WURFL™ nella cartella.
1. Rinominare il file come `wurfl.xml`.

AEM analizza automaticamente il file `wurfl.xml` e aggiorna i nodi sottostanti `/var/mobile/devicespecs`.

>[!NOTE]
>
>Quando il database WURFL™ completo è attivato, l&#39;analisi e l&#39;attivazione potrebbero richiedere alcuni minuti. Puoi controllare i registri per informazioni sull’avanzamento.

#### Aggiunta di una corrispondenza agente utente basata su regexp {#adding-a-regexp-based-user-agent-matching}

Aggiungi user-agent come espressione regolare sotto /apps/wcm/mobile/devicespecs/wurfl/regexp per puntare a un tipo di dispositivo WURFL™ esistente.

1. In **CRXDE Lite**, creare un nodo sotto /apps/wcm/mobile/devicespecs/regexp, ad esempio, `apple_ipad_ver1`.
1. Aggiungi le seguenti proprietà al nodo:

   * **regexp**: espressione regolare che definisce gli user-agents, ad esempio.&#42;Mozilla.&#42;iPad.&#42;AppleWebKit.&#42;Safari.&#42;
   * **deviceId**: ID dispositivo definito nel file wurfl.xml, ad esempio `apple_ipad_ver1`

La configurazione precedente fa sì che i dispositivi per i quali l’agente utente corrisponde all’espressione regolare fornita vengano mappati sull’ID dispositivo apple_ipad_ver1 WURFL™, se presente.

## Rilevamento dispositivo lato client {#client-side-device-detection}

Questa sezione descrive come utilizzare il rilevamento dell’AEM lato client del dispositivo per ottimizzare il rendering della pagina o per fornire al client versioni alternative del sito web.

AEM supporta il rilevamento lato client del dispositivo basato su `BrowserMap`. `BrowserMap` è spedito in AEM come libreria client in `/etc/clientlibs/browsermap`.

`BrowserMap` offre tre strategie che è possibile utilizzare per fornire un sito Web alternativo a un cliente, che viene utilizzato nel seguente ordine:

1. [Collegamenti alternativi](#providing-alternate-links)
1. [URL specifico del gruppo di dispositivi](#definingdevicegroupspecificurl)
1. [URL basato su selettore](#defining-selector-based-urls)

>[!NOTE]
>
>Per ulteriori informazioni sull&#39;integrazione della libreria client, vedere [Utilizzo delle librerie HTML lato client](/help/sites-developing/clientlibs.md).

### Fornitura di collegamenti alternativi {#providing-alternate-links}

Il servizio OSGi `PageVariantsProvider` è in grado di generare collegamenti alternativi per i siti appartenenti alla stessa famiglia. Per configurare i siti da considerare dal servizio, è necessario aggiungere un nodo `cq:siteVariant` al nodo `jcr:content` dalla radice del sito.

Il nodo `cq:siteVariant` deve avere le seguenti proprietà:

* `cq:childNodesMapTo` - determina l&#39;attributo dell&#39;elemento di collegamento a cui verranno mappati i nodi figlio. Si consiglia di organizzare il contenuto del sito Web in modo che gli elementi figlio del nodo radice rappresentino la radice per una variante di lingua del sito Web globale (ad esempio, `/content/mysite/en`, `/content/mysite/de`), nel qual caso il valore di `cq:childNodesMapTo` dovrebbe essere `hreflang`;
* `cq:variantDomain` - indica il dominio `Externalizer` utilizzato per generare gli URL assoluti delle varianti di pagina. Se questo valore non è impostato, le varianti di pagina verranno generate utilizzando collegamenti relativi;
* `cq:variantFamily` - indica a quale famiglia di siti Web appartiene questo sito; più rappresentazioni specifiche per dispositivo dello stesso sito Web devono appartenere alla stessa famiglia;
* `media` - memorizza i valori dell&#39;attributo media dell&#39;elemento link. Si consiglia di utilizzare il nome dell&#39;elemento `DeviceGroups` registrato di `BrowserMap`, in modo che la libreria `BrowserMap` possa inoltrare automaticamente i client alla variante corretta del sito Web.

#### PageVariantsProvider ed Externalizer {#pagevariantsprovider-and-externalizer}

Quando il valore della proprietà `cq:variantDomain` di un nodo `cq:siteVariant` non è vuoto, il servizio `PageVariantsProvider` genera collegamenti assoluti utilizzando questo valore come dominio configurato per il servizio `Externalizer`. Assicurarsi di configurare il servizio `Externalizer` in modo che rifletta la configurazione.

>[!NOTE]
>
>Quando si lavora con AEM, esistono diversi metodi per gestire le impostazioni di configurazione per tali servizi; vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) per ulteriori dettagli e le procedure consigliate.

### Definizione di un URL specifico per un gruppo di dispositivi {#defining-a-device-group-specific-url}

Se non si desidera utilizzare collegamenti alternativi, è possibile configurare un URL globale per ogni `DeviceGroup`. Adobe consiglia di creare una libreria client personalizzata che incorpori la libreria client `browsermap.standard` ma ridefinisca i gruppi di dispositivi.

BrowserMap è progettato in modo che le definizioni dei gruppi di dispositivi possano essere ignorate creando e aggiungendo un gruppo di dispositivi con lo stesso nome all&#39;oggetto `BrowserMap` dalla libreria client personalizzata.

>[!NOTE]
>
>Per ulteriori dettagli, vedere [BrowserMap personalizzato](#creatingacustomisedbrowsermap).

### Definizione degli URL basati su selettori {#defining-selector-based-urls}

Se non è stato utilizzato nessuno dei meccanismi precedenti per indicare un sito alternativo per `BrowserMap`, i selettori che utilizzeranno i nomi di `DeviceGroups` verranno aggiunti ai `URL`, nel qual caso è necessario fornire i propri servlet che gestiranno le richieste.

Ad esempio, un dispositivo che esplora `www.example.com/index.html` identificato come `smartphone` da BrowserMap viene inoltrato a `www.example.com/index.smartphone.html.`

### Utilizzo di BrowserMap sulle pagine {#using-browsermap-on-your-pages}

Per utilizzare la libreria client BrowserMap standard in una pagina, è necessario includere il file `/libs/wcm/core/browsermap/browsermap.jsp` utilizzando un tag `cq:include` nella sezione `head` della pagina.

```xml
<cq:include script="/libs/wcm/core/browsermap/browsermap.jsp" />
```

Oltre ad aggiungere la libreria client `BrowserMap` nei file `JSP`, devi anche aggiungere una proprietà stringa `cq:deviceIdentificationMode` impostata su `client-side` al nodo `jcr:content` sotto la directory principale del sito Web.

### Sovrascrittura del comportamento predefinito di BrowserMap {#overriding-browsermap-s-default-behaviour}

Se desideri personalizzare `BrowserMap` - ignorando `DeviceGroups` o aggiungendo altri probe - devi creare la tua libreria lato client in cui incorporare la libreria lato client `browsermap.standard`.

Inoltre, devi chiamare manualmente il metodo `BrowserMap.forwardRequest()` nel codice `JavaScript`.

>[!NOTE]
>
>Per ulteriori informazioni sull&#39;integrazione della libreria client, vedere [Utilizzo delle librerie HTML lato client](/help/sites-developing/clientlibs.md).

Dopo aver creato la libreria client `BrowserMap` personalizzata, Adobe suggerisce il seguente approccio:

1. Crea un file `browsermap.jsp` nell&#39;applicazione

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

1. Includi il file `broswermap.jsp` nella sezione head.

   ```xml
   <cq:include script="browsermap.jsp" />
   ```

### Esclusione di BrowserMap da alcune pagine {#excluding-browsermap-from-certain-pages}

Se desideri escludere la libreria BrowserMap da alcune pagine in cui non è necessario il rilevamento client, puoi aggiungere un attributo di richiesta:

```xml
<%
request.setAttribute("browsermap.enabled", false);
%>
```

Verrà creato lo script `/libs/wcm/core/browsermap/browsermap.jsp` per aggiungere un tag meta alla pagina, in modo che `BrowserMap` non esegua alcun rilevamento:

```xml
<meta name="browsermap.enabled" content="false">
```

### Verifica di una versione specifica di un sito Web {#testing-a-specific-version-of-a-web-site}

Normalmente, lo script BrowserMap reindirizza sempre i visitatori alla versione più adatta del sito web, in genere reindirizzando i visitatori al desktop o al sito mobile quando necessario.

È possibile forzare il dispositivo di qualsiasi richiesta a testare una versione specifica di un sito Web aggiungendo il parametro `device` all&#39;URL. L’URL seguente esegue il rendering della versione mobile del sito web Geometrixx Outdoors.

`https://localhost:4502/content/geometrixx-outdoors/en.html?wcmmode=disabled&device=smartphone`

>[!NOTE]
>
>Il parametro `wcmmode` è impostato su `disabled` per simulare il comportamento di un&#39;istanza Publish.

Il valore del dispositivo di override è memorizzato in un cookie in modo da poter esplorare il sito Web senza aggiungere il parametro `device` a ogni `URL`.

Di conseguenza, è necessario chiamare lo stesso `URL` con `device` impostato su `browser` per tornare alla versione desktop del sito Web.

>[!NOTE]
>
>BrowserMap memorizza il valore del dispositivo di override in un cookie denominato `BMAP_device`. L’eliminazione di questo cookie assicura che CQ distribuisca la versione appropriata del sito web in base al dispositivo corrente (ad esempio desktop o mobile).

## Elaborazione di richieste mobili {#mobile-request-processing}

L’AEM elabora come segue una richiesta emessa da un dispositivo mobile che appartiene al gruppo di dispositivi touch:

1. Un iPad invia una richiesta all&#39;istanza di pubblicazione dell&#39;AEM, ad esempio `https://localhost:4503/content/geometrixx_mobile/en/products.html`
1. L&#39;AEM determina se il sito della pagina richiesta è un sito mobile (verificando se la pagina di primo livello `/content/geometrixx_mobile` estende il componente Pagina mobile). In caso affermativo:
1. AEM cerca le funzionalità del dispositivo in base all’agente utente nell’intestazione della richiesta.
1. AEM mappa le funzionalità del dispositivo al gruppo di dispositivi e imposta `touch` come selettore del gruppo di dispositivi.
1. AEM reindirizza la richiesta a `https://localhost:4503/content/geometrixx_mobile/en/products.touch.html.`
1. L’AEM invia la risposta all’iPad:

   * Il rendering di `products.touch.html` è eseguito nel modo consueto ed è memorizzabile in cache.
   * I componenti di rendering utilizzano i selettori per adattare la presentazione.
   * AEM aggiunge automaticamente il selettore mobile a tutti i collegamenti interni nella pagina.

### Statistiche {#statistics}

Puoi ottenere alcune statistiche sul numero di richieste effettuate al server AEM dai dispositivi mobili. Il numero di richieste può essere suddiviso:

* per gruppo di dispositivi e dispositivo
* all’anno, al mese e al giorno

Per visualizzare le statistiche:

1. Passa alla console **Strumenti**.
1. Apri la pagina **Statistiche dispositivo** sotto **Strumenti** > **Dispositivi mobili**.
1. Fare clic sul collegamento per visualizzare le statistiche relative a un anno, un mese o un giorno specifico.

L&#39;aspetto della pagina **Statistiche** è il seguente:

![schermata_shot_2012-02-01at24353pm](assets/screen_shot_2012-02-01at24353pm.png)

>[!NOTE]
>
>La pagina **Statistiche** viene creata la prima volta che un dispositivo mobile accede all&#39;AEM e viene rilevata. Prima di allora, non era disponibile.

Per generare una voce nelle statistiche, procedere come segue:

1. Utilizza un dispositivo mobile o un emulatore (come, ad esempio, https://chrispederick.com/work/user-agent-switcher/ su Firefox).
1. Richiedi una pagina mobile nell’istanza di authoring disabilitando la modalità di authoring, ad esempio:
   `https://localhost:4502/content/geometrixx_mobile/en/products.html?wcmmode=disabled`

La pagina **Statistiche** è ora disponibile.

### Supporto del caching delle pagine per i collegamenti &quot;Invia collegamento a un amico&quot; {#supporting-page-caching-for-send-link-to-a-friend-links}

Le pagine mobili possono essere memorizzate nella cache in Dispatcher perché le pagine sottoposte a rendering per un gruppo di dispositivi sono distinte nell&#39;URL della pagina dal selettore del gruppo di dispositivi, ad esempio `/content/mobilepage.touch.html`. Una richiesta a una pagina mobile senza un selettore non viene mai memorizzata nella cache, come in questo caso, il rilevamento del dispositivo funziona e infine viene reindirizzato al gruppo di dispositivi corrispondente (o &quot;nomatch&quot; per tale questione). Una pagina mobile di cui è stato eseguito il rendering con un selettore di gruppo dispositivo viene elaborata dal rewriter del collegamento, che riscrive tutti i collegamenti all’interno della pagina in modo da contenere anche il selettore di gruppo dispositivo, impedendo di rieseguire il rilevamento del dispositivo per ogni clic di una pagina già qualificata.

Pertanto, potresti incontrare lo scenario seguente:

L&#39;utente Alice viene reindirizzato a `coolpage.feature.html` e invia l&#39;URL a un amico Bob che vi accede con un client diverso che rientra nel gruppo di dispositivi `touch`.

Se `coolpage.feature.html` viene servito da una cache front-end, l&#39;AEM non ha la possibilità di analizzare la richiesta per scoprire che il selettore mobile non corrisponde al nuovo agente utente e Bob ottiene la rappresentazione errata.

Per risolverlo, puoi includere nelle pagine una semplice interfaccia utente di selezione, in cui gli utenti finali possono ignorare il gruppo di dispositivi selezionato dall’AEM. Nell&#39;esempio precedente, un collegamento (o un&#39;icona) nella pagina consente all&#39;utente finale di passare a `coolpage.touch.html` se ritiene che il dispositivo sia sufficiente.
