---
title: Configurare la cache dei moduli adattivi
seo-title: Configurare la cache dei moduli adattivi
description: 'La cache dei moduli adattivi è stata progettata specificamente per i moduli e i documenti adattivi. Memorizza nella cache moduli adattivi e documenti adattivi allo scopo di ridurre il tempo necessario per eseguire il rendering di un modulo o di un documento adattivo sul client. '
seo-description: 'La cache dei moduli adattivi è stata progettata specificamente per i moduli e i documenti adattivi. Memorizza nella cache moduli adattivi e documenti adattivi allo scopo di ridurre il tempo necessario per eseguire il rendering di un modulo o di un documento adattivo sul client. '
uuid: ba8f79fd-d8dc-4863-bc0d-7c642c45505c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 9fa6f761-58ca-4cd0-8992-b9337dc1a279
docset: aem65
translation-type: tm+mt
source-git-commit: d5a649337acdc01c58ecc473e7c919e06cbd0188
workflow-type: tm+mt
source-wordcount: '1022'
ht-degree: 1%

---


# Configurare la cache dei moduli adattivi {#configure-adaptive-forms-cache}

Una cache è un meccanismo per ridurre i tempi di accesso ai dati, ridurre la latenza e migliorare le velocità di ingresso/uscita (I/O). La cache dei moduli adattivi memorizza solo il contenuto HTML e la struttura JSON di un modulo adattivo senza salvare i dati precompilati. Consente di ridurre il tempo necessario per eseguire il rendering di un modulo adattivo sul client. È progettata specificatamente per i moduli adattivi.

## Configurare la cache dei moduli adattivi per le istanze di creazione e pubblicazione {#configure-adaptive-forms-caching-at-author-and-publish-instances}

1. Andate AEM console Web Configuration Manager all&#39;indirizzo `https://[server]:[port]/system/console/configMgr`.
1. Fate clic su Configurazione **[!UICONTROL canale Web per moduli]** adattivi e comunicazioni interattive per modificarne i valori di configurazione.
1. Nella finestra di dialogo [!UICONTROL Modifica valori] di configurazione, specificare il numero massimo di moduli o documenti che un&#39;istanza del [!DNL Forms] server AEM può memorizzare nella cache nel campo **[!UICONTROL Numero di Forms]** adattivi. Il valore predefinito è 100.

   >[!NOTE]
   >
   >Per disattivare la cache, impostate il valore nel campo Numero di Forms adattivo su **0**. La cache viene reimpostata e tutti i moduli e i documenti vengono rimossi dalla cache quando si disabilita o si modifica la configurazione della cache.

   ![Finestra di dialogo di configurazione per la cache HTML dei moduli adattivi](assets/cache-configuration-edit.png)

1. Click **[!UICONTROL Save]** to save the configuration.

L’ambiente è configurato per l’utilizzo della cache per moduli adattivi e risorse correlate.


## (Facoltativo) Configurare la cache dei moduli adattivi presso il dispatcher {#configure-the-cache}

È inoltre possibile configurare il caching dei moduli adattivi presso il dispatcher per un ulteriore miglioramento delle prestazioni.

### Prerequisiti {#pre-requisites}

* Abilitare l&#39;opzione di [unione o precompilazione dei dati in corrispondenza del client](prepopulate-adaptive-form-fields.md#prefill-at-client) . Consente di unire dati univoci per ogni istanza di un modulo precompilato.
* [Attivate l’agente di scaricamento per ogni istanza](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance)di pubblicazione. Consente di ottenere migliori prestazioni di memorizzazione nella cache per i moduli adattivi. L’URL predefinito degli agenti di scaricamento è `http://[server]:[port]]/etc/replication/agents.publish/flush.html`.

### Considerazioni sulla memorizzazione nella cache dei moduli adattivi in un dispatcher {#considerations}

* Quando si utilizza la cache dei moduli adattivi, utilizzare il AEM [!DNL Dispatcher] per memorizzare nella cache le librerie client (CSS e JavaScript) di un modulo adattivo.
* Durante lo sviluppo di componenti personalizzati, sul server utilizzato per lo sviluppo, mantenere disattivata la cache dei moduli adattivi.
* Gli URL senza estensione non vengono memorizzati nella cache. Ad esempio, gli URL con pattern`/content/forms/[folder-structure]/[form-name].html` vengono memorizzati nella cache e gli URL con pattern vengono ignorati dalla cache `/content/dam/formsanddocument/[folder-name]/<form-name>/jcr:content`. Utilizzate quindi gli URL con estensioni per sfruttare i vantaggi del caching.
* Considerazioni sui moduli adattivi localizzati:
   * Utilizzate il formato URL `http://host:port/content/forms/af/<afName>.<locale>.html` per richiedere una versione localizzata di un modulo adattivo anziché `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`
   * [Disattiva l’utilizzo delle impostazioni internazionali](supporting-new-language-localization.md#how-localization-of-adaptive-form-works) del browser per gli URL con formato `http://host:port/content/forms/af/<adaptivefName>.html`.
   * Se si utilizza il formato URL `http://host:port/content/forms/af/<adaptivefName>.html`e **[!UICONTROL l&#39;opzione Usa impostazioni internazionali]** browser in Gestione configurazione è disabilitata, viene servita la versione non localizzata del modulo adattivo. La lingua non localizzata è quella utilizzata per lo sviluppo del modulo adattivo. Le impostazioni internazionali configurate per il browser (impostazioni internazionali del browser) non vengono prese in considerazione e viene servita una versione non localizzata del modulo adattivo.
   * Se si utilizza il formato URL `http://host:port/content/forms/af/<adaptivefName>.html`e **[!UICONTROL l&#39;opzione Usa lingua]** browser in Gestione configurazione è abilitata, viene fornita una versione localizzata del modulo adattivo, se disponibile. La lingua del modulo adattivo localizzato si basa sulle impostazioni internazionali configurate per il browser in uso (impostazione internazionale del browser). Può causare il [caching solo della prima istanza di un modulo]adattivo. Per evitare che il problema si verifichi nell’istanza in uso, consultate [Risoluzione dei problemi](#only-first-insatnce-of-adptive-forms-is-cached).

### Attivazione della memorizzazione nella cache al dispatcher

Per attivare e configurare la memorizzazione nella cache dei moduli adattivi nel dispatcher, effettuare le operazioni riportate di seguito.

1. Aprite il seguente URL per ogni istanza di pubblicazione dell’ambiente e configurate l’agente di replica:
   `http://[server]:[port]]/etc/replication/agents.publish/flush.html`

1. [Aggiungi quanto segue al file](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#automatically-invalidating-cached-files)dispatcher.any:

   ```JSON
      /invalidate
      {
      /0000
      {
      /glob "*"
      /type "deny"
      }
      /0001
      {
      # Consider all HTML files stale after an activation.
      /glob "*.html"
      /type "allow"
      }
      /0002
      {
      # Exclude htmls present in AF directories
      /glob "/content/forms/**/*.html"
      /type "deny"
      }
   ```

   Quando aggiungete quanto sopra:

   * Un modulo adattivo rimane nella cache finché non viene pubblicata una versione aggiornata del modulo.

   * Quando viene pubblicata una nuova versione di risorse a cui viene fatto riferimento in un modulo adattivo, i moduli adattivi interessati vengono automaticamente invalidati. Esistono alcune eccezioni all&#39;annullamento automatico della convalida delle risorse di riferimento. Per una soluzione alternativa alle eccezioni, consultate la sezione [Risoluzione dei problemi](#troubleshooting) .
1. [Aggiungi il dispatcher delle regole riportato di seguito.any o il file](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#specifying-the-documents-to-cache)delle regole personalizzate. Sono esclusi gli URL che non supportano il caching. Ad esempio, Comunicazione interattiva.

   ```JSON
      /0000 {
            /glob "*"
            /type "allow"
      }
      ## Don't cache csrf login tokens
      /0001 {
            /glob "/libs/granite/csrf/token.json"
            /type "deny"
      }
      ## Don't cache IC - print channel
      /0002 {
            /glob "/content/forms/**/channels/print.html"
            /type "deny"
      }
      ## Don't cache IC - web channel
      /0003 {
            /glob "/content/forms/**/channels/web.html"
            /type "deny"
      }
   ```

1. [Aggiungete i seguenti parametri all’elenco](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#ignoring-url-parameters)dei parametri dell’URL di esclusione:

   ```JSON
      /ignoreUrlParams {
      /0001 { /glob "*" /type "deny" }
      # added for AEM forms specific use cases.
      /0003 { /glob "dataRef" /type "allow" }
      }
   ```

L&#39;ambiente AEM è configurato per memorizzare nella cache i moduli adattivi. Memorizza nella cache tutti i tipi di moduli adattivi. Se è necessario controllare le autorizzazioni di accesso degli utenti per una pagina prima di distribuire la pagina memorizzata nella cache, consultate [Memorizzazione nella cache del contenuto](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/permissions-cache.html)protetto.

## Risoluzione dei problemi {#troubleshooting}

### Alcuni moduli adattivi contenenti immagini o video non vengono automaticamente invalidati dalla cache del dispatcher {#videos-or-images-not-auto-invalidated}

#### Problema {#issue1}

Quando selezionate e aggiungete immagini o video tramite il browser risorse a un modulo adattivo e tali immagini e video vengono modificati nell’editor delle risorse, i moduli adattivi contenenti tali immagini non vengono invalidati automaticamente dalla cache del dispatcher.

#### Soluzione {#Solution1}

Dopo aver pubblicato le immagini e il video, annullate esplicitamente la pubblicazione e pubblicate i moduli adattivi che fanno riferimento a tali risorse.

### Alcuni moduli adattivi contenenti frammenti di contenuto o frammenti esperienza non vengono automaticamente invalidati dalla cache del dispatcher {#content-or-experience-fragment-not-auto-invalidated}

#### Problema {#issue2}

Quando si aggiunge un frammento di contenuto o un frammento esperienza a un modulo adattivo e queste risorse vengono modificate e pubblicate in modo indipendente, i moduli adattivi contenenti tali risorse non vengono invalidati automaticamente dalla cache del dispatcher.

#### Soluzione {#Solution2}

Dopo aver pubblicato un frammento di contenuto aggiornato o un frammento esperienza, è possibile annullare la pubblicazione in modo esplicito e pubblicare i moduli adattivi che utilizzano tali risorse.

### Nella cache viene memorizzata solo la prima istanza di un modulo adattivo{#only-first-insatnce-of-adptive-forms-is-cached}

#### Problema {#issue3}

Se l’URL del modulo adattivo non contiene informazioni sulla localizzazione e **[!UICONTROL l’opzione Usa impostazioni internazionali]** browser in Gestione configurazione è abilitata, viene distribuita una versione localizzata del modulo adattivo e viene memorizzata nella cache solo la prima istanza del modulo adattivo, che viene quindi inviata a ogni utente successivo.

#### Soluzione {#Solution3}

Per risolvere il problema, effettuate le seguenti operazioni:

1. Aprite il file conf.d/httpd-dispatcher.conf o qualsiasi altro file di configurazione configurato per il caricamento in fase di esecuzione.

1. Aggiungete il codice seguente al file e salvatelo. Si tratta di un codice di esempio che lo modifica per adattarlo al tuo ambiente.

```XML
   <VirtualHost *:80>
        # Set log level high during development / debugging and then turn it down to whatever is appropriate
    LogLevel rewrite:trace6
        # Start Rewrite Engine
    RewriteEngine On
        # Handle actual URL convention (just pass through)
        RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]
 
        # Handle selector based redirection basded on browser language
        # The Rewrite Cond(ition) is looking for the Accept-Lanague header and if found takes the first two character which most likely will be the desired language selector.
        RewriteCond %{HTTP:Accept-Language} ^(..).*$ [NC]
        RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
   </VirtualHost>
```
