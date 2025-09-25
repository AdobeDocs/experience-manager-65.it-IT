---
title: L’editor universale
description: Scopri la flessibilità dell’editor universale e come può aiutare a potenziare le esperienze headless utilizzando AEM 6.5.
feature: Developing
role: Developer
exl-id: 7bdf1fcc-02b9-40bc-8605-e6508a84d249
source-git-commit: 9f91063e51aa599ef48967f832aa359ecf100fc2
workflow-type: ht
source-wordcount: '1183'
ht-degree: 100%

---


# L’editor universale {#universal-editor}

Scopri la flessibilità dell’editor universale e come può aiutare a potenziare le esperienze headless utilizzando AEM 6.5.

## Panoramica {#overview}

L’editor universale è un editor visivo versatile che fa parte di Adobe Experience Manager Sites. Consente ai creatori di contenuti di modificare gli elementi di WYSIWYG (what-you-see-is-what-you-get) di qualsiasi esperienza headless.

* Gli autori traggono vantaggio dalla flessibilità dell’editor universale in quanto supporta le stesse modifiche visive coerenti per tutte le forme di contenuti headless AEM.
* Gli sviluppatori traggono vantaggio dalla versatilità dell’editor universale, che supporta un vero e proprio disaccoppiamento dell’implementazione. Consente agli sviluppatori di utilizzare virtualmente qualsiasi framework o architettura a loro scelta, senza imporre alcun vincolo di SDK o tecnologia.

Per maggiori dettagli, consulta la [documentazione di AEM as a Cloud Service nell&#39;editor universale](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction).

## Architettura {#architecture}

L’editor universale è un servizio che funziona insieme ad AEM per creare contenuti in modo headless.

* L&#39;editor universale è ospitato in `https://experience.adobe.com/#/aem/editor/canvas` e può modificare le pagine sottoposte al rendering da parte di AEM 6.5.
* La pagina AEM viene letta dall’editor universale tramite Dispatcher partendo dall’istanza di authoring di AEM.
* Il servizio Editor universale, che viene eseguito sullo stesso host di Dispatcher, riscrive le modifiche nell’istanza di authoring di AEM.

![Flusso di creazione di contenuti con l’editor universale](assets/author-flow.png)

## Requisiti {#requirements}

L’editor universale è supportato da:

* AEM 6.5
   * Sono supportati sia l’hosting locale che l’hosting AMS.
* [AEM 6.5 LTS](https://experienceleague.adobe.com/it/docs/experience-manager-65-lts/content/implementing/developing/headless/universal-editor/introduction)
   * Sono supportati sia l’hosting locale che l’hosting AMS.
* [AEM as a Cloud Service](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction)

Questo documento è incentrato sul supporto di AEM 6.5 dell’editor universale. Per utilizzare l’editor universale con AEM 6.5, è necessario avere:

* AEM 6.5 con service pack 23 o successivo
   * I Service Pack 21 e 22 sono supportati anche da [un Feature Pack.](https://experience.adobe.com/#/downloads/content/software-distribution/it/aem.html?package=/content/software-distribution/it/details.html/content/dam/aem/public/cq-6.5.21-universal-editor-1.0.0.zip).
* Dispatcher configurato correttamente

## Configurazione {#setup}

Per testare l’editor universale è necessario:

1. [Configurare un servizio di editor universale locale.](#set-up-ue)
1. [Modificare Dispatcher per consentire il servizio di editor universale.](#update-dispatcher)

Dopo aver completato la configurazione, puoi [dotare le applicazioni per l’uso dell’editor universale.](#instrumentation)

### Configurare i servizi {#configure-services}

L’editor universale sfrutta diversi pacchetti per i quali è necessaria una configurazione aggiuntiva.

#### Imposta l’attributo SameSite per il cookie `login-token`. {#samesite-attribute}

1. Apri Configuration Manager.
   * `http://<host>:<port>/system/console/configMgr`
1. Individua la voce **Adobe Granite Token Authentication Handler** nell’elenco e fai clic su **Modifica i valori di configurazione**
1. Nella finestra di dialogo, modifica l’**attributo SameSite per il cookie del token di accesso** (`token.samesite.cookie.attr`) in `Partitioned`.
1. Fai clic su **Salva**.

#### Rimuovi l’opzione X-Frame delle intestazioni `SAMEORIGIN`. {#sameorigin}

1. Apri Configuration Manager.
   * `http://<host>:<port>/system/console/configMgr`
1. Individua il **servlet principale di Apache Sling** nell’elenco e fai clic su **Modifica i valori di configurazione**.
1. Elimina il valore `X-Frame-Options=SAMEORIGIN` dall’attributo **Altre intestazioni di risposta** (`sling.additional.response.headers`) se esistente.
1. Fai clic su **Salva**.

#### Configura il gestore di autenticazione dei parametri di query di Adobe Granite. {#query-parameter}

1. Apri Configuration Manager.
   * `http://<host>:<port>/system/console/configMgr`
1. Individua il **Gestore di autenticazione dei parametri di query di Adobe Granite** nell’elenco e fai clic su **Modifica i valori di configurazione**.
1. Nel campo **Percorso** (`path`), aggiungi `/` per abilitare.
   * Un valore vuoto disattiva il gestore di autenticazione.
1. Fai clic su **Salva**.

#### Definisci i percorsi di contenuto o `sling:resourceTypes` per cui aprire l’editor universale. {#paths}

1. Apri Configuration Manager.
   * `http://<host>:<port>/system/console/configMgr`
1. Individua **Servizio URL editor universale** nell’elenco e fai clic su **Modifica i valori di configurazione**.
1. Definisci i percorsi di contenuto o `sling:resourceTypes` per cui aprire l’editor universale.
   * Nel campo **Mappatura apertura editor universale**, specifica i percorsi per i quali è aperto l’editor universale.
   * Nel campo **Sling:resourceTypes che verrà aperto dall’editor universale**, fornisci un elenco di risorse aperte direttamente dall’editor universale.
1. Fai clic su **Salva**.
1. Controlla la [configurazione di esternalizzazione](/help/sites-developing/externalizer.md) e assicurati di disporre quantomeno degli ambienti locali, di authoring e di pubblicazione impostati come nell’esempio seguente.

   ```text
   "local $[env:AEM_EXTERNALIZER_LOCAL;default=http://localhost:4502]",
   "author $[env:AEM_EXTERNALIZER_AUTHOR;default=http://localhost:4502]",
   "publish $[env:AEM_EXTERNALIZER_PUBLISH;default=http://localhost:4503]"
   ```

Una volta completati questi passaggi di configurazione, AEM aprirà l’editor universale per le pagine nell’ordine seguente.

1. AEM controllerà le mappature in `Universal Editor Opening Mapping` e se il contenuto si trova in uno dei percorsi qui definiti, verrà aperto l’editor universale.
1. Per il contenuto non incluso nei percorsi definiti in `Universal Editor Opening Mapping`, AEM verifica se il `resourceType` dei contenuti corrispondono a quelli definiti in **Sling:resourceTypes che verranno aperti dall’editor universale**; se il contenuto corrisponde a uno di questi tipi, l’editor universale verrà aperto in `${author}${path}.html`.
1. In caso contrario, AEM apre l’editor di pagine.

Per definire le mappature sono disponibili le seguenti variabili in `Universal Editor Opening Mapping`.

* `path`: percorso del contenuto della risorsa da aprire
* `localhost`: voce di Esternalizzazione per `localhost` senza schema, ad esempio `localhost:4502`
* `author`: voce di Esternalizzazione per authoring senza schema, ad esempio `localhost:4502`
* `publish`: voce di Esternalizzazione per pubblicazione senza schema, ad esempio `localhost:4503`
* `preview`: voce di Esternalizzazione per anteprima senza schema, ad esempio `localhost:4504`
* `env`: `prod`, `stage`, `dev` in base alle modalità di esecuzione di Sling definite
* `token`: token di query richiesto per `QueryTokenAuthenticationHandler`

Esempi di mappature:

* Apri tutte le pagine in `/content/foo` in AEM Author:
   * `/content/foo:${author}${path}.html?login-token=${token}`
   * Questo comporta l’apertura di `https://localhost:4502/content/foo/x.html?login-token=<token>`
* Apri tutte le pagine in `/content/bar` su un server NextJS remoto, fornendo come informazioni tutte le variabili
   * `/content/bar:nextjs.server${path}?env=${env}&author=https://${author}&publish=https://${publish}&login-token=${token}`
   * Questo comporta l’apertura di `https://nextjs.server/content/bar/x?env=prod&author=https://localhost:4502&publish=https://localhost:4503&login-token=<token>`

### Configurare il servizio editor universale {#set-up-ue}

Con AEM aggiornato e configurato, puoi impostare un servizio editor universale locale per le attività locali di sviluppo e testing.

1. Installa Node.js versione >=20.
1. Scarica e decomprimi il servizio editor universale più recente da [Distribuzione del software](https://experienceleague.adobe.com/it/docs/experience-cloud/software-distribution/home)
1. Configura il servizio editor universale tramite variabili di ambiente o un file `.env`.
   * [Per informazioni dettagliate, consulta la documentazione dell’editor universale di AEM as a Cloud Service.](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/local-dev#setting-up-service)
   * Nota che potresti dover utilizzare l’opzione `UES_MAPPING` se è richiesta la riscrittura interna dell’IP.
1. Eseguire `universal-editor-service.cjs`

### Aggiornare Dispatcher {#update-dispatcher}

Se AEM è configurato ed è in esecuzione un servizio editor universale locale, sarà necessario consentire un proxy inverso per il nuovo servizio [ in Dispatcher.](https://experienceleague.adobe.com/it/docs/experience-manager-dispatcher/using/dispatcher)

1. Modifica il file vhost dell’istanza di authoring in modo da includere un proxy inverso.

   ```html
   <IfModule mod_proxy.c>
    ProxyPass "/universal-editor" "http://localhost:8080"
    ProxyPassReverse "/universal-editor" "http://localhost:8080"
   </IfModule>
   ```

   >[!NOTE]
   >
   >La porta predefinita è 8080. Se hai modificato questo elemento usando il parametro `UES_PORT` nel [tuo file`.env`,](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/local-dev#setting-up-service) devi modificare di conseguenza il valore della porta qui.

1. Riavvia Apache.

## Dotare di strumenti l’app {#instrumentation}

Con AEM aggiornato e un servizio editor universale locale in esecuzione, puoi iniziare a modificare contenuti headless utilizzando l’editor universale.

L’app deve essere dotata di strumenti che consentano di sfruttare i vantaggi dell’editor universale. Questo comporta l’inclusione di tag meta per indicare all’editor come e dove mantenere il contenuto. I dettagli di questa dotazione di strumenti sono disponibili nella [documentazione dell’editor universale per AEM as a Cloud Service.](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/getting-started#instrument-page)

Nella documentazione dell’editor universale per AEM as a Cloud Service vanno applicate le seguenti modifiche per l’utilizzo con AEM 6.5.

* Il protocollo nel tag meta deve essere `aem65` invece di `aem`.

  ```html
  <meta name="urn:adobe:aue:system:aemconnection" content={`aem65:${getAuthorHost()}`}/>
  ```

* L’endpoint del servizio editor universale deve essere annunciato tramite un tag meta.

  ```html
  <meta name="urn:adobe:aue:config:service" content={`${getAuthorHost()}/universal-editor`}/>
  ```

* Nella sezione `plugins` della definizione dei componenti, è necessario utilizzare `aem65` invece di `aem`.

>[!TIP]
>
>Per una guida completa per gli sviluppatori su come iniziare a utilizzare l’editor universale, consulta il documento [Panoramica dell’editor universale per gli sviluppatori AEM](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/developer-overview) nella documentazione di AEM as a Cloud Service, tenendo presenti le modifiche necessarie per il supporto di AEM 6.5 indicate in questa sezione.

## Differenze tra AEM 6.5 e AEM as a Cloud Service {#differences}

L’editor universale in AEM 6.5 funziona in generale come in AEM as a Cloud Service, inclusa l’interfaccia utente e gran parte della configurazione. Esistono tuttavia differenze da sottolineare.

* L’editor universale nella versione 6.5 supporta solo il caso d’uso headless.
* La configurazione dell’editor universale varia leggermente per la versione 6.5 ([come descritto](#setup) nel documento corrente).
* L’editor universale nella versione 6.5 utilizza un selettore di risorse e un selettore di frammenti di contenuto diversi rispetto a AEM as a Cloud Service.
