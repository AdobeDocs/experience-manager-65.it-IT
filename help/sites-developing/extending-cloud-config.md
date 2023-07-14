---
title: Configurazioni Cloud Service
description: Puoi estendere le istanze esistenti per creare configurazioni personalizzate
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 20a19ee5-7113-4aca-934a-a42c415a8d93
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 3%

---

# Configurazioni Cloud Service{#cloud-service-configurations}

Le configurazioni sono progettate per fornire la logica e la struttura per l’archiviazione delle configurazioni del servizio.

Puoi estendere le istanze esistenti per creare configurazioni personalizzate.

## Concetti {#concepts}

I principi utilizzati per lo sviluppo delle configurazioni si basano sui seguenti concetti:

* I servizi/adattatori vengono utilizzati per recuperare le configurazioni.
* Le configurazioni (ad esempio, proprietà/paragrafi) vengono ereditate dai padri.
* Riferito dai nodi di Analytics per percorso.
* Facilmente estensibile.
* Offre la flessibilità necessaria per gestire configurazioni più complesse, ad esempio [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics).
* Supporto per le dipendenze (ad esempio, [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics) i plug-in richiedono un [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics) ).

## Struttura {#structure}

Il percorso di base delle configurazioni è:

`/etc/cloudservices`.

Per ogni tipo di configurazione, viene fornito un modello e un componente. In questo modo è possibile disporre di modelli di configurazione in grado di soddisfare la maggior parte delle esigenze dopo la personalizzazione.

Per fornire una configurazione per i nuovi servizi, eseguire le operazioni seguenti:

* Creare una pagina di servizio in

  `/etc/cloudservices`

* Sotto questo:

   * un modello di configurazione
   * un componente di configurazione

Il modello e il componente devono ereditare il `sling:resourceSuperType` dal modello base:

`cq/cloudserviceconfigs/templates/configpage`

O componente base rispettivamente

`cq/cloudserviceconfigs/components/configpage`

Il fornitore di servizi deve inoltre fornire la pagina del servizio:

`/etc/cloudservices/<service-name>`

### Modello {#template}

Il modello estende il modello base:

`cq/cloudserviceconfigs/templates/configpage`

E definisci un `resourceType` che punta al componente personalizzato.

```xml
/libs/cq/analytics/templates/sitecatalyst
sling:resourceSuperType = cq/cloudserviceconfigs/templates/configpage
allowedChildren = /libs/cq/analytics/templates/sitecatalyst
allowedPaths = /etc/cloudservices/analytics/*, /etc/cloudservices/analytics/.*
componentReference = cq/analytics/components/sitecatalyst
jcr:content/
cq:designPath = /etc/designs/cloudservices
sling:resourceType = cq/analytics/components/sitecatalystpage

/libs/cq/analytics/templates/generictracker
sling:resourceSuperType = cq/cloudservices/templates/configpage
allowedChildren = /libs/cq/analytics/templates/generictracker
allowedPaths = /etc/cloudservices/analytics/*, /etc/cloudservices/analytics/.*
jcr:content/
cq:designPath = /etc/designs/cloudservices
sling:resourceType = cq/analytics/components/generictrackerpage
```

### Componenti {#components}

Il componente deve estendere il componente base:

`cq/cloudserviceconfigs/templates/configpage`

```xml
/libs/cq/analytics/components/sitecatalystpage

/libs/cq/analytics/components/generictrackerpage
```

Dopo aver configurato il modello e il componente, puoi aggiungere la configurazione aggiungendo pagine secondarie in:

`/etc/cloudservices/<service-name>`

### Modello di contenuto {#content-model}

Il modello di contenuto viene memorizzato come `cq:Page` in:

`/etc/cloudservices/<service-name>(/*)`

```xml
/etc/cloudservices
/etc/cloudservices/service-name
/etc/cloudservices/service-name/config
/etc/cloudservices/service-name/config/inherited-config
```

Le configurazioni vengono memorizzate nel sottonodo `jcr:content`.

* Le proprietà fisse, definite in una finestra di dialogo, devono essere memorizzate nel `jcr:node` direttamente.
* Elementi dinamici (utilizzando `parsys` o `iparsys`) utilizza un sottonodo per memorizzare i dati del componente.

```xml
/etc/cloudservices/service/config/jcr:content as nt:unstructured
propertyname
*
par/component/ as cq:Component
propertyname
*
```

### API {#api}

Per la documentazione di riferimento sull’API, consulta [com.day.cq.wcm.webservicesupport](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/webservicesupport/package-summary.html).

### Integrazione AEM {#aem-integration}

I servizi disponibili sono elencati nella **Cloud Services** scheda di **Proprietà pagina** (di qualsiasi pagina che eredita da `foundation/components/page` o `wcm/mobile/components/page`).

La scheda fornisce anche:

* un collegamento alla posizione in cui è possibile abilitare il servizio
* scegli una configurazione (sottonodo del servizio) da un campo percorso

#### Crittografia password {#password-encryption}

Quando si memorizzano le credenziali utente per il servizio, tutte le password devono essere crittografate.

Per ottenere questo risultato, aggiungi un campo modulo nascosto. Questo campo deve contenere l’annotazione `@Encrypted` nel nome della proprietà; ovvero, per `password` il nome sarà scritto come:

`password@Encrypted`

La proprietà verrà quindi crittografata automaticamente (utilizzando `CryptoSupport` servizio) da parte di `EncryptionPostProcessor`.

>[!NOTE]
>
>È simile allo standard ` [SlingPostServlet](https://sling.apache.org/site/manipulating-content-the-slingpostservlet-servletspost.html)` annotazioni.

>[!NOTE]
>
>Per impostazione predefinita, il `EcryptionPostProcessor` crittografa solo `POST` richieste effettuate a `/etc/cloudservices`.

#### Proprietà aggiuntive per i nodi jcr:content della pagina del servizio {#additional-properties-for-service-page-jcr-content-nodes}

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>componentReference</td>
   <td>Percorso di riferimento a un componente da includere automaticamente nella pagina.<br /> Viene utilizzato per funzionalità aggiuntive e inclusioni JS.<br /> Questo include il componente nella pagina in cui<br /> <code> cq/cloudserviceconfigs/components/servicecomponents</code><br /> (normalmente prima del <code>body</code> ).<br /> Nel caso di Adobe Analytics e Adobe Target, utilizziamo questo per includere funzionalità aggiuntive, come le chiamate JavaScript per monitorare il comportamento dei visitatori.</td>
  </tr>
  <tr>
   <td>descrizione</td>
   <td>Breve descrizione del servizio.<br /> </td>
  </tr>
  <tr>
   <td>descriptionExtended</td>
   <td>Descrizione estesa del servizio.</td>
  </tr>
  <tr>
   <td>classificazione</td>
   <td>Classificazione dei servizi da utilizzare nelle inserzioni.</td>
  </tr>
  <tr>
   <td>selectableChildren</td>
   <td>Filtro per la visualizzazione delle configurazioni nella finestra di dialogo delle proprietà della pagina.</td>
  </tr>
  <tr>
   <td>serviceUrl</td>
   <td>URL al sito Web del servizio.</td>
  </tr>
  <tr>
   <td>serviceUrlLabel</td>
   <td>Etichetta per l'URL del servizio.</td>
  </tr>
  <tr>
   <td>miniaturaPercorso</td>
   <td>Percorso della miniatura per il servizio.</td>
  </tr>
  <tr>
   <td>visibile</td>
   <td>Visibilità nella finestra di dialogo delle proprietà della pagina; visibile per impostazione predefinita (facoltativo)</td>
  </tr>
 </tbody>
</table>

### Casi d’uso {#use-cases}

Questi servizi sono forniti per impostazione predefinita:

* [Snippet tracker](/help/sites-administering/external-providers.md) (Google, WebTrends e così via)
* [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)
* [Test&amp;Target](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-target)
<!-- Search&Promote is end of life as of September 1, 2022 * [Search&Promote](/help/sites-administering/marketing-cloud.md#integrating-with-search-promote) -->
* [Dynamic Media](/help/sites-administering/marketing-cloud.md#integrating-with-scene)

>[!NOTE]
>
>Vedi anche [Creazione di un Cloud Service personalizzato](/help/sites-developing/extending-cloud-config-custom-cloud.md).
