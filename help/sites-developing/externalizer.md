---
title: Esternalizzazione degli URL
seo-title: Externalizing URLs
description: Externalizer è un servizio OSGI che consente di trasformare in modo programmatico un percorso di risorsa in un URL esterno e assoluto
seo-description: The Externalizer is an OSGI service that allows you to programmatically transform a resource path into an external and absolute URL
uuid: 65bcc352-fc8c-4aa0-82fb-1321a035602d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 938469ad-f466-42f4-8b6f-bfc060ae2785
docset: aem65
exl-id: 971d6c25-1fbe-4c07-944e-be6b97a59922
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---

# Esternalizzazione degli URL{#externalizing-urls}

Nell&#39;AEM, la **Esternalizzatore** è un servizio OSGI che consente di trasformare in modo programmatico un percorso di risorsa (ad esempio, `/path/to/my/page`) in un URL esterno e assoluto (ad esempio, `https://www.mycompany.com/path/to/my/page`) inserendo un prefisso DNS nel percorso.

Poiché un’istanza non può conoscere il proprio URL visibile esternamente se è in esecuzione dietro un livello web e poiché a volte è necessario creare un collegamento al di fuori dell’ambito della richiesta, questo servizio fornisce una posizione centrale per configurare tali URL esterni e generarli.

Questa pagina spiega come configurare **Esternalizzatore** e come utilizzarlo. Per ulteriori informazioni, consultare [JavaScript](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html).

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

   * **schema** è solitamente http o https, ma può anche essere ftp, ecc.

      * utilizzare https per applicare i collegamenti https, se desiderato
      * verrà utilizzato se il codice client non sostituisce lo schema quando viene richiesta l’esternalizzazione di un URL.
   * **server** è il nome host (può essere un nome di dominio o un indirizzo ip).
   * **porta** (facoltativo) è il numero della porta.
   * **contextpath** (facoltativo) è impostato solo se AEM è installato come app web in un percorso di contesto diverso.

   Esempio: `production https://my.production.instance`

   I seguenti nomi di mappatura sono predefiniti e devono sempre essere impostati in quanto AEM si basa su di essi:

   * `local` : l’istanza locale
   * `author` - DNS del sistema di authoring
   * `publish` - il sito web pubblico DNS

   >[!NOTE]
   >
   >Una configurazione personalizzata consente di aggiungere una nuova categoria, ad esempio `production`, `staging` o anche sistemi esterni non AEM come `my-internal-webservice`. È utile evitare di codificare tali URL in posizioni diverse nella base di codice di un progetto.

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


1. Puoi trovare altri esempi nella sezione [JavaScript](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html).
