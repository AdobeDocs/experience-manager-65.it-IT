---
title: L’editor universale
description: Scopri la flessibilità di Universal Editor e come può aiutare a potenziare le esperienze headless utilizzando AEM 6.5.
feature: Developing
role: Developer
exl-id: 7bdf1fcc-02b9-40bc-8605-e6508a84d249
source-git-commit: d3dd827e93549c558284be1c1991b4e003c9e0e8
workflow-type: tm+mt
source-wordcount: '1252'
ht-degree: 1%

---


# L’editor universale {#universal-editor}

Scopri la flessibilità di Universal Editor e come può aiutare a potenziare le esperienze headless utilizzando AEM 6.5.

## Panoramica {#overview}

Universal Editor è un editor visivo versatile che fa parte di Adobe Experience Manager Sites. Consente agli autori di modificare ciò che si vede è ciò che si ottiene (WYSIWYG) di qualsiasi esperienza headless.

* Gli autori traggono vantaggio dalla flessibilità di Universal Editor in quanto supporta lo stesso editing visivo coerente per tutte le forme di contenuti headless AEM.
* Gli sviluppatori traggono vantaggio dalla versatilità di Universal Editor in quanto supporta anche un vero e proprio disaccoppiamento dell’implementazione. Consente agli sviluppatori di utilizzare virtualmente qualsiasi framework o architettura a loro scelta, senza imporre alcun vincolo di SDK o tecnologia.

Per ulteriori informazioni, vedere la documentazione di [AEM as a Cloud Service nell&#39;editor universale](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction).

## Architettura {#architecture}

Universal Editor è un servizio che funziona insieme ad AEM per creare contenuti in modo headless.

* L&#39;editor universale è ospitato in `https://experience.adobe.com/#/aem/editor/canvas` e può modificare le pagine sottoposte a rendering da AEM 6.5.
* La pagina AEM viene letta dall’editor universale tramite Dispatcher dall’istanza di authoring di AEM.
* Il servizio Universal Editor, che viene eseguito sullo stesso host di Dispatcher, riscrive le modifiche nell&#39;istanza di authoring di AEM.

![Flusso di authoring con Universal Editor](assets/author-flow.png)

## Requisiti {#requirements}

L’editor universale è supportato da:

* AEM 6.5 (service pack 21 o 22 più un feature pack)
   * Sono supportati sia l’hosting locale che AMS.
* [AEM as a Cloud Service](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction) (versione `2023.8.13099` o successiva)

Questo documento si concentra sul supporto di AEM 6.5 di Universal Editor.

## Configurazione {#setup}

Per testare l’Editor universale è necessario:

1. [Aggiorna e configura l’istanza di authoring di AEM.](#update-configure-aem)
1. [Configurare un servizio Universal Editor locale.](#set-up-ue)
1. [Regola il dispatcher per consentire il servizio Universal Editor.](#update-dispatcher)

Dopo aver completato la configurazione, puoi [dotare le applicazioni dell&#39;editor universale.](#instrumentation)

### Aggiornare AEM {#update-aem}

Per poter utilizzare Universal Editor con AEM 6.5 sono necessari Service Pack 21 o 22 e un feature pack per AEM.

#### Applica Service Pack più recente {#latest}

Assicurati di eseguire almeno il service pack 21 o 22 per AEM 6.5. È possibile scaricare il service pack più recente da [Software Distribution.](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=it)

#### Installazione del Feature Pack di Universal Editor {#feature-pack}

Installa **Universal Editor Feature Pack per AEM 6.5** [disponibile in Software Distribution.](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/cq-6.5.21-universal-editor-1.0.0.zip)

Se è già in esecuzione il service pack 23 o versione successiva, il feature pack non è necessario.

### Configura servizi {#configure-services}

Il feature pack installa una serie di nuovi pacchetti per i quali è necessaria una configurazione aggiuntiva.

#### Impostare l&#39;attributo SameSite per il cookie `login-token`. {#samesite-attribute}

1. Apri Configuration Manager.
   * `http://<host>:<port>/system/console/configMgr`
1. Individua **Adobe Granite Token Authentication Handler** nell&#39;elenco e fai clic su **Modifica i valori di configurazione**.
1. Nella finestra di dialogo, modifica l&#39;attributo **SameSite per il cookie token di accesso** (`token.samesite.cookie.attr`) in `Partitioned`.
1. Fai clic su **Salva**.

#### Rimuovi l&#39;opzione X-Frame delle intestazioni `SAMEORIGIN`. {#sameorigin}

1. Apri Configuration Manager.
   * `http://<host>:<port>/system/console/configMgr`
1. Individua **Apache Sling Main Servlet** nell&#39;elenco e fai clic su **Modifica i valori di configurazione**.
1. Eliminare il valore `X-Frame-Options=SAMEORIGIN` dall&#39;attributo **Altre intestazioni di risposta** (`sling.additional.response.headers`) se esistente.
1. Fai clic su **Salva**.

#### Configura il gestore di autenticazione dei parametri di query di Adobe Granite. {#query-parameter}

1. Apri Configuration Manager.
   * `http://<host>:<port>/system/console/configMgr`
1. Individua **Adobe Granite Query Parameter Authentication Handler** nell&#39;elenco e fai clic su **Modifica i valori di configurazione**.
1. Nel campo **Percorso** (`path`), aggiungi `/` per abilitare.
   * Un valore vuoto disattiva il gestore di autenticazione.
1. Fai clic su **Salva**.

#### Definire i percorsi di contenuto o `sling:resourceTypes` per cui aprire l&#39;editor universale. {#paths}

1. Apri Configuration Manager.
   * `http://<host>:<port>/system/console/configMgr`
1. Individua **Servizio URL editor universale** nell&#39;elenco e fai clic su **Modifica i valori di configurazione**.
1. Definire i percorsi di contenuto o `sling:resourceTypes` per cui aprire l&#39;editor universale.
   * Nel campo **Mapping apertura editor universale**, specificare i percorsi per i quali è aperto l&#39;editor universale.
   * Nel campo **Sling:resourceTypes che deve essere aperto da Universal Editor**, fornire un elenco delle risorse aperte direttamente da Universal Editor.
1. Fai clic su **Salva**.
1. Controlla la [configurazione di Externalizer](/help/sites-developing/externalizer.md) e assicurati di disporre almeno degli ambienti locale, di authoring e di pubblicazione impostati come nell&#39;esempio seguente.

   ```text
   "local $[env:AEM_EXTERNALIZER_LOCAL;default=http://localhost:4502]",
   "author $[env:AEM_EXTERNALIZER_AUTHOR;default=http://localhost:4502]",
   "publish $[env:AEM_EXTERNALIZER_PUBLISH;default=http://localhost:4503]"
   ```

Una volta completati questi passaggi di configurazione, AEM aprirà l’Editor universale per le pagine nell’ordine seguente.

1. AEM controllerà le mappature in `Universal Editor Opening Mapping` e se il contenuto si trova in uno dei percorsi qui definiti, verrà aperto l&#39;Editor universale.
1. Per il contenuto non incluso nei percorsi definiti in `Universal Editor Opening Mapping`, AEM controlla se il `resourceType` del contenuto corrisponde a quelli definiti in **Sling:resourceTypes che verranno aperti da Universal Editor** e se il contenuto corrisponde a uno di questi tipi, l&#39;Editor universale verrà aperto in `${author}${path}.html`.
1. In caso contrario, AEM apre l’Editor pagina.

Per definire le mappature in `Universal Editor Opening Mapping` sono disponibili le seguenti variabili.

* `path`: percorso del contenuto della risorsa da aprire
* `localhost`: voce esternalizzatore per `localhost` senza schema, ad esempio `localhost:4502`
* `author`: voce esternalizzazione per autore senza schema, ad esempio `localhost:4502`
* `publish`: voce esternalizzatore per la pubblicazione senza schema, ad esempio `localhost:4503`
* `preview`: voce esternalizzatore per l&#39;anteprima senza schema, ad esempio `localhost:4504`
* `env`: `prod`, `stage`, `dev` in base alle modalità di esecuzione Sling definite
* `token`: token di query richiesto per `QueryTokenAuthenticationHandler`

Esempi di mappature:

* Apri tutte le pagine in `/content/foo` in AEM Author:
   * `/content/foo:${author}${path}.html?login-token=${token}`
   * Ciò comporta l&#39;apertura di `https://localhost:4502/content/foo/x.html?login-token=<token>`
* Apri tutte le pagine in `/content/bar` su un server NextJS remoto, fornendo come informazioni tutte le variabili
   * `/content/bar:nextjs.server${path}?env=${env}&author=https://${author}&publish=https://${publish}&login-token=${token}`
   * Ciò comporta l&#39;apertura di `https://nextjs.server/content/bar/x?env=prod&author=https://localhost:4502&publish=https://localhost:4503&login-token=<token>`

### Configurazione del servizio Editor universale {#set-up-ue}

Con AEM aggiornato e configurato, puoi impostare un servizio Universal Editor locale per le attività di sviluppo e test locali.

1. Installa Node.js versione >=20.
1. Scarica e decomprimi il servizio Universal Editor più recente da [Distribuzione software](https://experienceleague.adobe.com/it/docs/experience-cloud/software-distribution/home)
1. Configurare il servizio Universal Editor tramite variabili di ambiente o file `.env`.
   * [Per informazioni dettagliate, consulta la documentazione di AEM as a Cloud Service Universal Editor.](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/local-dev#setting-up-service)
   * Si noti che potrebbe essere necessario utilizzare l&#39;opzione `UES_MAPPING` se è richiesta la riscrittura interna dell&#39;IP.
1. Esegui `universal-editor-service.cjs`

### Aggiornare Dispatcher {#update-dispatcher}

Se AEM è configurato e un servizio Universal Editor locale è in esecuzione, sarà necessario consentire un proxy inverso per il nuovo servizio [nel dispatcher.](https://experienceleague.adobe.com/it/docs/experience-manager-dispatcher/using/dispatcher)

1. Regola il file vhost dell’istanza di authoring in modo da includere un proxy inverso.

   ```html
   <IfModule mod_proxy.c>
    ProxyPass "/universal-editor" "http://localhost:8080"
    ProxyPassReverse "/universal-editor" "http://localhost:8080"
   </IfModule>
   ```

   >[!NOTE]
   >
   >8080 è la porta predefinita. Se hai modificato questo usando il parametro `UES_PORT` in [il tuo file `.env`,](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/local-dev#setting-up-service) devi regolare di conseguenza il valore della porta qui.

1. Riavvia Apache.

## Strumentazione dell’app {#instrumentation}

Con AEM aggiornato e un servizio Universal Editor locale in esecuzione, puoi iniziare a modificare contenuti headless utilizzando Universal Editor.

Tuttavia, l’app deve essere dotata di strumenti che consentano di sfruttare i vantaggi dell’editor universale. Ciò comporta l’inclusione di metatag per indicare all’editor come e dove mantenere il contenuto. I dettagli di questa strumentazione sono disponibili nella [documentazione dell&#39;editor universale per AEM as a Cloud Service.](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/getting-started#instrument-page)

Quando si segue la documentazione di Universal Editor con AEM as a Cloud Service, vengono applicate le seguenti modifiche quando si utilizza con AEM 6.5.

* Il protocollo nel tag meta deve essere `aem65` invece di `aem`.

  ```html
  <meta name="urn:adobe:aue:system:aemconnection" content={`aem65:${getAuthorHost()}`}/>
  ```

* L&#39;endpoint del servizio Universal Editor deve essere annunciato tramite un tag meta.

  ```html
  <meta name="urn:adobe:aue:config:service" content={`${getAuthorHost()}/universal-editor`}/>
  ```

* Nella sezione `plugins` della definizione dei componenti, è necessario utilizzare `aem65` invece di `aem`.

>[!TIP]
>
>Per una guida completa per gli sviluppatori su come iniziare a utilizzare Universal Editor, consulta il documento [Panoramica di Universal Editor per sviluppatori AEM](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/developer-overview) nella documentazione di AEM as a Cloud Service, tenendo presente le modifiche necessarie per il supporto di AEM 6.5 come indicato in questa sezione.

## Differenze tra AEM 6.5 e AEM as a Cloud Service {#differences}

L’editor universale in AEM 6.5 funziona in generale come in AEM as a Cloud Service, inclusa l’interfaccia utente e gran parte della configurazione. Ci sono, tuttavia, delle differenze da notare.

* Universal Editor nella versione 6.5 supporta solo il caso d’uso headless.
* La configurazione dell&#39;editor universale varia leggermente per 6.5 ([come descritto](#setup) nel documento corrente).
* L’editor universale nella versione 6.5 utilizza un selettore di risorse diverso e un selettore di frammenti di contenuto diverso da AEM as a Cloud Service.
