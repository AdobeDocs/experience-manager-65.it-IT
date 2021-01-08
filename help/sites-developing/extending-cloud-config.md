---
title: Configurazioni Cloud Service
seo-title: Configurazioni Cloud Service
description: Potete estendere le istanze esistenti per creare configurazioni personalizzate
seo-description: Potete estendere le istanze esistenti per creare configurazioni personalizzate
uuid: 9d20c3a4-2a12-4d3c-80c3-fcac3137a675
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: d25c03bf-6eaa-45f4-ab60-298865935a62
translation-type: tm+mt
source-git-commit: 801d57bbe8a1bede6dcb4bf7884e5f71ddea1e83
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 4%

---


# Configurazioni Cloud Service{#cloud-service-configurations}

Le configurazioni sono progettate per fornire la logica e la struttura per la memorizzazione delle configurazioni del servizio.

Potete estendere le istanze esistenti per creare configurazioni personalizzate.

## Concetti {#concepts}

I principi utilizzati nello sviluppo delle configurazioni si sono basati sui seguenti concetti:

* I servizi/le schede di rete vengono utilizzati per recuperare le configurazioni.
* Le configurazioni (ad es. proprietà/paragrafi) vengono ereditate dagli elementi padre.
* Riferimento dai nodi di analisi per percorso.
* Facilmente estensibile.
* Offre la flessibilità necessaria per gestire configurazioni più complesse, ad esempio [ Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics).
* Supporto per dipendenze (ad es. [ i plug-in Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics) necessitano di una configurazione [ Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)).

## Struttura {#structure}

Il percorso di base delle configurazioni è:

`/etc/cloudservices`.

Per ogni tipo di configurazione verranno forniti un modello e un componente. Questo consente di disporre di modelli di configurazione in grado di soddisfare le esigenze più specifiche dopo essere stati personalizzati.

Per fornire una configurazione per un nuovo servizio è necessario:

* creare una pagina di servizio in

   `/etc/cloudservices`

* in questa sezione:

   * un modello di configurazione
   * un componente di configurazione

Il modello e il componente devono ereditare il simbolo `sling:resourceSuperType` dal modello di base:

`cq/cloudserviceconfigs/templates/configpage`

o componente di base

`cq/cloudserviceconfigs/components/configpage`

Il provider di servizi deve inoltre fornire la pagina del servizio:

`/etc/cloudservices/<service-name>`

### Modello {#template}

Il modello verrà esteso:

`cq/cloudserviceconfigs/templates/configpage`

e definire un `resourceType` che punti al componente personalizzato.

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

Il componente deve estendere il componente di base:

`cq/cloudserviceconfigs/templates/configpage`

```xml
/libs/cq/analytics/components/sitecatalystpage

/libs/cq/analytics/components/generictrackerpage
```

Dopo aver configurato il modello e il componente, puoi aggiungere la configurazione aggiungendo le sottopagine in:

`/etc/cloudservices/<service-name>`

### Modello di contenuto {#content-model}

Il modello di contenuto è memorizzato come `cq:Page` in:

`/etc/cloudservices/<service-name>(/*)`

```xml
/etc/cloudservices
/etc/cloudservices/service-name
/etc/cloudservices/service-name/config
/etc/cloudservices/service-name/config/inherited-config
```

Le configurazioni sono memorizzate nel nodo secondario `jcr:content`.

* Le proprietà fisse definite in una finestra di dialogo devono essere memorizzate direttamente in `jcr:node`.
* Gli elementi dinamici (che utilizzano `parsys` o `iparsys`) utilizzano un nodo secondario per memorizzare i dati del componente.

```xml
/etc/cloudservices/service/config/jcr:content as nt:unstructured
propertyname
*
par/component/ as cq:Component
propertyname
*
```

### API {#api}

Per la documentazione di riferimento sull&#39;API, vedete [com.day.cq.wcm.webservicesupport](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/webservicesupport/package-summary.html).

### Integrazione AEM {#aem-integration}

I servizi disponibili sono elencati nella scheda **Cloud Services** della finestra di dialogo **Proprietà pagina** (di qualsiasi pagina che eredita da `foundation/components/page` o `wcm/mobile/components/page`).

La scheda fornisce inoltre:

* un collegamento alla posizione in cui è possibile abilitare il servizio
* scegliere una configurazione (nodo secondario del servizio) da un campo percorso

#### Crittografia password {#password-encryption}

Quando si memorizzano le credenziali utente per il servizio, tutte le password devono essere crittografate.

A tal fine, è possibile aggiungere un campo modulo nascosto. Questo campo deve contenere l&#39;annotazione `@Encrypted` nel nome della proprietà; ad esempio, per il campo `password` il nome verrà scritto come segue:

`password@Encrypted`

La proprietà verrà quindi cifrata automaticamente (utilizzando il servizio `CryptoSupport`) dal `EncryptionPostProcessor`.

>[!NOTE]
>
>È simile alle annotazioni ` [SlingPostServlet](https://sling.apache.org/site/manipulating-content-the-slingpostservlet-servletspost.html)` standard.

>[!NOTE]
>
>Per impostazione predefinita, `EcryptionPostProcessor` codifica solo le richieste `POST` effettuate a `/etc/cloudservices`.

#### Proprietà aggiuntive per jcr pagina di servizio:nodi di contenuto {#additional-properties-for-service-page-jcr-content-nodes}

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>componentReference</td>
   <td>Percorso di riferimento per un componente da includere automaticamente nella pagina.<br /> Viene utilizzato per ulteriori funzionalità e inclusione JS.<br /> Questo include il componente sulla pagina <br /> <code> cq/cloudserviceconfigs/components/servicecomponents</code><br /> in cui è incluso (in genere prima del  <code>body</code> tag).<br /> Nel caso in cui Analytics e Target utilizzino questa funzionalità per includere funzionalità aggiuntive, come le chiamate JavaScript per monitorare il comportamento dei visitatori.</td>
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
   <td>classifica</td>
   <td>Classificazione del servizio per l'uso nelle inserzioni.</td>
  </tr>
  <tr>
   <td>selectChildren</td>
   <td>Filtro per la visualizzazione delle configurazioni nella finestra di dialogo delle proprietà della pagina.</td>
  </tr>
  <tr>
   <td>serviceUrl</td>
   <td>URL del sito Web del servizio.</td>
  </tr>
  <tr>
   <td>serviceUrlLabel</td>
   <td>Etichetta per l’URL del servizio.</td>
  </tr>
  <tr>
   <td>thumbnailPath</td>
   <td>Percorso della miniatura del servizio.</td>
  </tr>
  <tr>
   <td>visible</td>
   <td>Visibilità nella finestra di dialogo delle proprietà della pagina; visible per impostazione predefinita (facoltativo)</td>
  </tr>
 </tbody>
</table>

### Casi di utilizzo {#use-cases}

Questi servizi sono forniti per impostazione predefinita:

* [Snippet](/help/sites-administering/external-providers.md)  Tracker (Google, WebTrends, ecc.)
* [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)
* [Test&amp;Target](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-target)
* [Search&amp;Promote](/help/sites-administering/marketing-cloud.md#integrating-with-search-promote)
* [Dynamic Media](/help/sites-administering/marketing-cloud.md#integrating-with-scene)

>[!NOTE]
>
>Vedere anche [Creazione di un Cloud Service personalizzato](/help/sites-developing/extending-cloud-config-custom-cloud.md).

