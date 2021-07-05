---
title: Guida introduttiva all'estensione AEM per PWA Studi
description: Scopri come distribuire un progetto AEM headless Content and Commerce con PWA Studi.
topics: Commerce
feature: Commerce Integration Framework
thumbnail: 37843.jpg
source-git-commit: 247c521e93990df2c8026da5edd84d163d5d424b
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 1%

---


# Guida introduttiva all&#39;estensione AEM per PWA Studi {#getting-started-pwa}

PWA Studi si integra perfettamente con Adobe Commerce tramite GraphQL e offre opzioni illimitate per la creazione di vetrine innovative e coinvolgenti e di altre esperienze digitali.

I frammenti di contenuto sono parti di contenuto con una struttura predefinita che consente loro di essere utilizzate in modo headless utilizzando GraphQL come API in diversi formati (ad esempio JSON, Markdown) ed eseguirne il rendering indipendente. I frammenti di contenuto includono tutti i tipi di dati e i campi necessari per GraphQL per garantire che l’applicazione richieda solo ciò che è disponibile e riceva ciò che è previsto. La flessibilità che offrono in termini di struttura li rende perfetti per l&#39;utilizzo in più posizioni e su più canali.

La progettazione della struttura necessaria è semplice grazie all’Editor modelli di frammento di contenuto in Adobe Experience Manager. La sfida principale per integrare frammenti di contenuto Adobe Experience Manager (o qualsiasi altro dato) con l’applicazione PWA Studi è rappresentata dal recupero di dati da più endpoint GraphQL. Questo perché PWA Studi funziona con un singolo endpoint Commerce GraphQL di Adobe.

## Architettura {#architecture}

![Architettura headless PWA](/help/commerce/cif/assets/pwa-studio/PWA-Studio_Architecture.png)

## Configurazione PWA Studi {#setup-pwa}

Per configurare l’app PWA Studi, segui la documentazione Adobe Commerce [PWA Studi](https://magento.github.io/pwa-studio/tutorials/) .

Per collegare PWA Studi all’endpoint GraphQL di AEM, puoi utilizzare l’ [AEM Extension per PWA Studi](https://github.com/adobe/aem-pwa-studio-extensions).

1. Consulta il repository

1. Nell’applicazione PWA Studi, aggiungi l’estensione come dipendenza di sviluppo.

   ```javascript
   yarn add --dev file:{path-to-extension}/extension
   ```

1. Aggiungi il wrapper Apollo Link all’applicazione PWA Studi. In pwa-root/src/index.js, apporta le seguenti modifiche:

   ```javascript
     import { linkWrapper } from '@adobe/pwa-studio-aem-cfm-blog-extension';
   
   // ...
   
   <Adapter apiBase={apiBase} apollo={{ link: linkWrapper(apolloLink) }} store={store}>
   ```

   Per ulteriori dettagli sulla personalizzazione del client Apollo, consulta [linkWrapper.js](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/linkWrapper.js).

1. Per estendere il componente di navigazione con una voce Blog, aggiungi i seguenti adattamenti a pwa-root/local-intercept.js:

   ```javascript
   const addBlogToNavigation = require('@adobe/pwa-studio-aem-cfm-blog-extension/src/addBlogToNavigation');
   
   function localIntercept(targets) {
       addBlogToNavigation(targets);
   }    
   ```

   Per ulteriori informazioni sulla personalizzazione del componente Navigazione, consulta la documentazione [addBlogToNavigation.js](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/addBlogToNavigation.js) e la documentazione [Extensibility Framework](https://magento.github.io/pwa-studio/pwa-buildpack/extensibility-framework/) di PWA Studi.

1. Il client Apollo si aspetta l’endpoint GraphQL AEM in <https://pwa-studio/endpoint.js>. Per mappare l’endpoint a questa posizione, è necessario personalizzare la configurazione UPWARD dell’applicazione PWA Studi:
a) Aggiungi la variabile AEM_CFM_GRAPHQL a pwa-root/.env e adattala per puntare all’endpoint GraphQL dei frammenti di contenuto AEM.

   Esempio: AEM_CFM_GRAPHQL=<http://localhost:4503/content/graphql/global>

   b) Aggiungi un risolutore proxy alla tua configurazione UPWARD. Un esempio di configurazione UPWARD potrebbe essere il seguente:

```json
   response:
     resolver: conditional
     when:
       - matches: request.url.pathname
         pattern: ^/endpoint.json(/|$)
         use: aemProxy
     default: veniaResponse

   aemProxy:
     resolver: proxy
     target: env.AEM_CFM_GRAPHQL
     ignoreSSLErrors: true

   status: response.status
   headers: response.headers
   body: response.body
```

## AEM di installazione {#setup-aem}

Per impostare un endpoint GraphQL per il progetto AEM, segui la documentazione AEM Frammenti di contenuto . Inoltre, nel progetto AEM, aggiungi le seguenti configurazioni per consentire all’applicazione PWA Studi di accedere all’endpoint GraphQL:

* Criterio per la condivisione delle risorse tra le origini di Adobe Granite (com.adobe.granite.cors.impl.CORSPolicyImpl)

   Imposta la proprietà allowedorigin sull’hostname completo dell’applicazione PWA.

   Esempio:  <https://pwa-studio-test-vflyn.local.pwadev:9366>

* Filtro di riferimento Apache Sling (org.apache.sling.security.impl.ReferrerFilter.cfg.json)

   Imposta la proprietà allow.hosts sul nome host dell&#39;applicazione PWA.

   Esempio: pwa-studio-test-vflyn.local.pwadev

Puoi trovare esempi completi di entrambe le configurazioni qui: <https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension/aem/config/src/main/content/jcr_root/apps/blog-demo/config>.

Per mostrare l’endpoint GraphQL, abbiamo preparato alcuni modelli e dati di frammenti di contenuto di esempio tramite un pacchetto di contenuti. Questi funzionano bene insieme ai componenti React forniti con l’estensione PWA Studi.

## Guida all’uso {#how-to-use}

Questa estensione è considerata un esempio di implementazione di come collegare un’applicazione PWA Studi con AEM per recuperare ed eseguire il rendering del contenuto tramite GraphQL.

A seconda del caso d’uso, vuoi creare modelli di frammenti di contenuto personalizzati che generano uno schema GraphQL personalizzato che può essere utilizzato dai tuoi componenti React.

Le impostazioni di produzione possono variare in diversi aspetti.

* È possibile disporre di un singolo endpoint GraphQL federato che combina dati GraphQL AEM e Magento invece di personalizzare il client Apollo.
* L&#39;applicazione PWA Studi potrebbe utilizzare direttamente l&#39;URL dell&#39;endpoint GraphQL AEM, senza un proxy con UPWARD. Il proxy può anche essere spostato in un livello diverso (ad es. CDN).
* L’approccio più adatto alle tue esigenze dipende anche dalla modalità di distribuzione dell’applicazione PWA Studi all’utente finale.

Questa estensione include due esempi.

### Blog {#blog}

Visualizza i post di blog in base ad alcuni modelli di frammenti di contenuto. Inoltre, contiene esempi su come configurare il client Apollo in modo che funzioni con l’endpoint GraphQL AEM e come estendere il componente di navigazione in PWA Studi. Per ulteriori informazioni, consulta [GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension) .

### Arricchimento PDP {#pdp-enrichment}

Consente agli addetti al marketing di arricchire facilmente i PDP con contenuti aggiuntivi gestiti come frammenti di contenuto.  Per ulteriori informazioni, consulta [GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cif-product-page-extension) .
