---
title: Esternalizzazione degli URL
description: Externalizer è un servizio OSGI che consente di trasformare in modo programmatico un percorso di risorsa in un URL esterno e assoluto
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
exl-id: 971d6c25-1fbe-4c07-944e-be6b97a59922
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---

# Esternalizzazione degli URL{#externalizing-urls}

In Adobe Experience Manager (AEM), il **Esternalizzatore** è un servizio OSGI che consente di trasformare programmaticamente un percorso di risorsa (ad esempio, `/path/to/my/page`) in un URL esterno e assoluto (ad esempio, `https://www.mycompany.com/path/to/my/page`) inserendo un prefisso DNS nel percorso.

Poiché un’istanza non può conoscere il proprio URL visibile esternamente se è in esecuzione dietro un livello web e poiché a volte è necessario creare un collegamento al di fuori dell’ambito della richiesta, questo servizio fornisce una posizione centrale per configurare tali URL esterni e generarli.

Questa pagina spiega come configurare **Esternalizzatore** e come utilizzarlo. Per ulteriori informazioni, consultare [JavaScript](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/Externalizer.html).

## Configurazione del servizio Externalizer {#configuring-the-externalizer-service}

Il **Esternalizzatore** Il servizio consente di definire centralmente più domini che possono essere utilizzati per prefissare in modo programmatico i percorsi delle risorse. Ogni dominio è identificato da un nome univoco utilizzato per fare riferimento al dominio a livello di programmazione.

Per definire una mappatura di dominio per **Esternalizzatore** servizio:

1. Passa alla gestione della configurazione tramite **Strumenti**, quindi **Console web** o immetti:

   `https://<host>:<port>/system/console/configMgr`

1. Clic **Day CQ Link Externalizer** per aprire la finestra di dialogo configurazione.

   >[!NOTE]
   >
   >Il collegamento diretto alla configurazione è `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`

   ![aem-externalizer-01](assets/aem-externalizer-01.png)

1. Definisci un **Domini** mappatura: una mappatura è costituita da un nome univoco che può essere utilizzato nel codice per fare riferimento al dominio, a uno spazio e al dominio:

   `<unique-name> [scheme://]server[:port][/contextpath]`

   Dove:

   * **schema** è http o https, ma può anche essere ftp e così via.

      * se necessario, utilizza https per applicare i collegamenti https
      * viene utilizzato se il codice client non sostituisce lo schema quando viene richiesta l’esternalizzazione di un URL.

   * **server** è il nome host (può essere un nome di dominio o un indirizzo ip).
   * **porta** (facoltativo) è il numero della porta.
   * **contextpath** (facoltativo) è impostato solo se AEM è installato come app web in un percorso di contesto diverso.

   Esempio: `production https://my.production.instance`

   I seguenti nomi di mappatura sono predefiniti e devono essere impostati perché AEM si basa su di essi:

   * `local` : l’istanza locale
   * `author` - DNS del sistema di authoring
   * `publish` - il sito web pubblico DNS

   >[!NOTE]
   >
   >Una configurazione personalizzata consente di aggiungere una categoria, ad esempio `production`, `staging`, o anche sistemi esterni non AEM come `my-internal-webservice`. È utile evitare di codificare tali URL in posizioni diverse nella base di codice di un progetto.

1. Clic **Salva** per salvare le modifiche.

>[!NOTE]
>
>Adobe consiglia di: [aggiungi la configurazione all’archivio](/help/sites-deploying/configuring.md#addinganewconfigurationtotherepository).

### Utilizzo del servizio Externalizer {#using-the-externalizer-service}

Questa sezione mostra alcuni esempi di come **Esternalizzatore** Il servizio può essere utilizzato:

1. **Per ottenere il servizio Externalizer in una JSP:**

   ```java
   Externalizer externalizer = resourceResolver.adaptTo(Externalizer.class);
   ```

1. **Per esternalizzare un percorso con il dominio &quot;publish&quot;:**

   ```java
   String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
   ```

   Supponendo il mapping del dominio:

   * `publish https://www.website.com`

   `myExternalizedUrl` finisce con il valore:

   * `https://www.website.com/contextpath/my/page.html`

1. **Per esternalizzare un percorso con il dominio &quot;author&quot;:**

   ```java
   String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
   ```

   Supponendo il mapping del dominio:

   * `author https://author.website.com`

   `myExternalizedUrl` finisce con il valore:

   * `https://author.website.com/contextpath/my/page.html`

1. **Per esternalizzare un percorso con il dominio &quot;locale&quot;:**

   ```java
   String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
   ```

   Supponendo il mapping del dominio:

   * `local https://publish-3.internal`

   `myExternalizedUrl` finisce con il valore:

   * `https://publish-3.internal/contextpath/my/page.html`

1. Puoi trovare altri esempi nella sezione [JavaScript](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/Externalizer.html).
