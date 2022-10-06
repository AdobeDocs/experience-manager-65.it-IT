---
title: Esternalizzazione degli URL
seo-title: Externalizing URLs
description: L’esternalizzatore è un servizio OSGI che consente di trasformare programmaticamente un percorso di risorsa in un URL esterno e assoluto
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

In AEM, il **Esternalizzatore** è un servizio OSGI che consente di trasformare programmaticamente un percorso di risorsa (ad es. `/path/to/my/page`) in un URL esterno e assoluto (ad esempio, `https://www.mycompany.com/path/to/my/page`) prefissando il percorso con un DNS preconfigurato.

Poiché un’istanza non può conoscere il suo URL visibile esternamente se è in esecuzione dietro un livello web e poiché a volte un collegamento deve essere creato al di fuori dell’ambito della richiesta, questo servizio fornisce una posizione centrale per configurare gli URL esterni e generarli.

Questa pagina spiega come configurare il **Esternalizzatore** e come usarlo. Per ulteriori informazioni, consulta la [Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html).

## Configurazione del servizio Externalizer {#configuring-the-externalizer-service}

La **Esternalizzatore** il servizio ti consente di definire centralmente più domini che possono essere utilizzati per prefisso programmaticamente i percorsi delle risorse. Ogni dominio è identificato da un nome univoco utilizzato per fare riferimento programmaticamente al dominio.

Per definire una mappatura del dominio per **Esternalizzatore** servizio:

1. Passa alla gestione della configurazione tramite **Strumenti**, quindi **Console web** oppure immetti:

   `https://<host>:<port>/system/console/configMgr`

1. Fai clic su **Day CQ Link Externalizer** per aprire la finestra di dialogo di configurazione.

   >[!NOTE]
   >
   >Il collegamento diretto alla configurazione è `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`

   ![aem-externalizer-01](assets/aem-externalizer-01.png)

1. Definire un **Domini** mappatura: una mappatura consiste in un nome univoco che può essere utilizzato nel codice per fare riferimento al dominio, a uno spazio e al dominio:

   `<unique-name> [scheme://]server[:port][/contextpath]`

   Dove:

   * **schema** di solito è http o https, ma può anche essere ftp, ecc.

      * utilizza https per applicare i collegamenti https, se necessario
      * viene utilizzato se il codice client non sostituisce lo schema quando si richiede l’esternalizzazione di un URL.
   * **server** è il nome host (può essere un nome di dominio o un indirizzo ip).
   * **porta** (facoltativo) è il numero di porta.
   * **contextpath** (facoltativo) è impostato solo se AEM è installato come applicazione web in un percorso contestuale diverso.

   Esempio: `production https://my.production.instance`

   I seguenti nomi di mappatura sono predefiniti e devono sempre essere impostati in base a AEM:

   * `local` - l&#39;istanza locale
   * `author` - DNS del sistema di authoring
   * `publish` - DNS del sito web pubblico

   >[!NOTE]
   >
   >Una configurazione personalizzata consente di aggiungere una nuova categoria, ad esempio `production`, `staging` o anche sistemi esterni non AEM quali `my-internal-webservice`. È utile evitare di codificare tali URL in posizioni diverse della codebase di un progetto.

1. Fai clic su **Salva** per salvare le modifiche.

>[!NOTE]
>
>L’Adobe consiglia di [aggiungi la configurazione al repository](/help/sites-deploying/configuring.md#addinganewconfigurationtotherepository).

### Utilizzo del servizio Externalizer {#using-the-externalizer-service}

Questa sezione mostra alcuni esempi di come **Esternalizzatore** è possibile utilizzare il servizio:

1. **Per ottenere il servizio Externalizer in un JSP:**

   ```java
   Externalizer externalizer = resourceResolver.adaptTo(Externalizer.class);
   ```

1. **Per esternalizzare un percorso con il dominio &quot;pubblica&quot;:**

   ```java
   String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
   ```

   Supponendo la mappatura del dominio:

   * `publish https://www.website.com`

   `myExternalizedUrl` termina con il valore:

   * `https://www.website.com/contextpath/my/page.html`


1. **Per esternalizzare un percorso con il dominio &quot;author&quot;:**

   ```java
   String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
   ```

   Supponendo la mappatura del dominio:

   * `author https://author.website.com`

   `myExternalizedUrl` termina con il valore:

   * `https://author.website.com/contextpath/my/page.html`


1. **Per esternalizzare un percorso con il dominio &quot;locale&quot;:**

   ```java
   String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
   ```

   Supponendo la mappatura del dominio:

   * `local https://publish-3.internal`

   `myExternalizedUrl` termina con il valore:

   * `https://publish-3.internal/contextpath/my/page.html`


1. Puoi trovare ulteriori esempi nella sezione [Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html).
