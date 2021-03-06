---
title: Configurare la cache dei moduli adattivi
seo-title: Configurare la cache dei moduli adattivi
description: 'La cache dei moduli adattivi è progettata appositamente per i moduli adattivi e i documenti. Memorizza in cache moduli adattivi e documenti adattivi allo scopo di ridurre il tempo necessario per eseguire il rendering di un modulo o di un documento adattivo sul client. '
seo-description: 'La cache dei moduli adattivi è progettata appositamente per i moduli adattivi e i documenti. Memorizza in cache moduli adattivi e documenti adattivi allo scopo di ridurre il tempo necessario per eseguire il rendering di un modulo o di un documento adattivo sul client. '
uuid: ba8f79fd-d8dc-4863-bc0d-7c642c45505c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 9fa6f761-58ca-4cd0-8992-b9337dc1a279
docset: aem65
role: Admin
exl-id: 153986f0-b6ff-4278-8bb6-70c320a4e539
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '934'
ht-degree: 1%

---

# Configurare la cache dei moduli adattivi {#configure-adaptive-forms-cache}

Una cache è un meccanismo per ridurre i tempi di accesso ai dati, ridurre la latenza e migliorare le velocità di input/output (I/O). La cache dei moduli adattivi memorizza solo il contenuto HTML e la struttura JSON di un modulo adattivo senza salvare dati precompilati. Consente di ridurre il tempo necessario per eseguire il rendering di un modulo adattivo sul client. È progettato specificatamente per i moduli adattivi.

## Configurare la cache dei moduli adattivi nelle istanze di creazione e pubblicazione {#configure-adaptive-forms-caching-at-author-and-publish-instances}

1. Vai AEM gestione della configurazione della console Web all&#39;indirizzo `https://[server]:[port]/system/console/configMgr`.
1. Fai clic su **[!UICONTROL Configurazione canale web per moduli adattivi e comunicazioni interattive]** per modificare i relativi valori di configurazione.
1. Nella finestra di dialogo [!UICONTROL modifica valori di configurazione], specifica il numero massimo di moduli o documenti che un&#39;istanza del server [!DNL Forms] AEM può memorizzare nella cache nel campo **[!UICONTROL Numero di Forms adattivo]**. Il valore predefinito è 100.

   >[!NOTE]
   >
   >Per disabilitare la cache, imposta il valore nel campo Numero di Forms adattivo su **0**. La cache viene reimpostata e tutti i moduli e i documenti vengono rimossi dalla cache quando si disabilita o si modifica la configurazione della cache.

   ![Finestra di dialogo di configurazione per la cache HTML dei moduli adattivi](assets/cache-configuration-edit.png)

1. Fai clic su **[!UICONTROL Salva]** per salvare la configurazione.

L’ambiente è configurato per l’utilizzo della cache dei moduli adattivi e delle relative risorse.


## (Facoltativo) Configura la cache del modulo adattivo sul dispatcher {#configure-the-cache}

Puoi anche configurare il caching dei moduli adattivi al dispatcher per ulteriori miglioramenti delle prestazioni.

### Prerequisiti {#pre-requisites}

* Abilita l&#39;opzione [unione o precompilazione dei dati in client](prepopulate-adaptive-form-fields.md#prefill-at-client) . Consente di unire dati univoci per ogni istanza di un modulo precompilato.

### Considerazioni sulla memorizzazione in cache dei moduli adattivi su un dispatcher {#considerations}

* Quando utilizzi la cache dei moduli adattivi, utilizza il AEM [!DNL Dispatcher] per memorizzare nella cache le librerie client (CSS e JavaScript) di un modulo adattivo.
* Durante lo sviluppo di componenti personalizzati, sul server utilizzato per lo sviluppo, tieni disabilitata la cache dei moduli adattivi.
* Gli URL senza estensione non vengono memorizzati nella cache. Ad esempio, gli URL con pattern`/content/forms/[folder-structure]/[form-name].html` vengono memorizzati nella cache e la memorizzazione in cache ignora gli URL con pattern `/content/dam/formsanddocument/[folder-name]/<form-name>/jcr:content`. Utilizza quindi gli URL con estensioni per sfruttare i vantaggi della memorizzazione in cache.
* Considerazioni sui moduli adattivi localizzati:
   * Utilizza il formato URL `http://host:port/content/forms/af/<afName>.<locale>.html` per richiedere una versione localizzata di un modulo adattivo invece di `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`
   * [Disabilita l’utilizzo ](supporting-new-language-localization.md#how-localization-of-adaptive-form-works) locale del browser per gli URL con formato  `http://host:port/content/forms/af/<adaptivefName>.html`.
   * Quando si utilizza il formato URL `http://host:port/content/forms/af/<adaptivefName>.html` e **[!UICONTROL Usa impostazione internazionale browser]** nel gestore della configurazione è disattivato, viene distribuita la versione non localizzata del modulo adattivo. La lingua non localizzata è la lingua utilizzata durante lo sviluppo del modulo adattivo. Le impostazioni internazionali configurate per il browser (impostazioni internazionali del browser) non vengono prese in considerazione e viene fornita una versione non localizzata del modulo adattivo.
   * Quando si utilizza il formato URL `http://host:port/content/forms/af/<adaptivefName>.html` e **[!UICONTROL Usa impostazione internazionale browser]** nel gestore della configurazione è abilitato, viene fornita una versione localizzata del modulo adattivo, se disponibile. La lingua del modulo adattivo localizzato si basa sulle impostazioni internazionali configurate per il browser (impostazioni internazionali del browser). Può causare la memorizzazione in cache solo della prima istanza di un modulo adattivo ]. [ Per evitare che il problema si verifichi sull&#39;istanza, consulta [risoluzione dei problemi](#only-first-insatnce-of-adptive-forms-is-cached).

### Abilita la memorizzazione in cache al dispatcher

Esegui i passaggi elencati di seguito per abilitare e configurare la memorizzazione in cache dei moduli adattivi sul dispatcher:

1. Apri il seguente URL per ogni istanza di pubblicazione dell&#39;ambiente e [abilita l&#39;agente di scaricamento per le istanze di pubblicazione dell&#39;ambiente](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance):
   `http://[server]:[port]]/etc/replication/agents.publish/flush.html`

1. [Aggiungi quanto segue al file](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#automatically-invalidating-cached-files) dispatcher.any:

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

   Quando aggiungi quanto sopra:

   * Un modulo adattivo rimane nella cache fino a quando non viene pubblicata una versione aggiornata del modulo.

   * Quando viene pubblicata una versione più recente della risorsa a cui viene fatto riferimento in un modulo adattivo, i moduli adattivi interessati vengono automaticamente invalidati. Sono presenti alcune eccezioni all’annullamento automatico della validità delle risorse di riferimento. Per la soluzione alle eccezioni, consulta la sezione [risoluzione dei problemi](#troubleshooting) .
1. [Aggiungi il seguente file](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#specifying-the-documents-to-cache) di regole dispatcher.any o personalizzato. Sono esclusi gli URL che non supportano la memorizzazione in cache. Ad esempio, la comunicazione interattiva.

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

1. [Aggiungi i seguenti parametri all’elenco](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#ignoring-url-parameters) dei parametri URL ignorati:

   ```JSON
      /ignoreUrlParams {
      /0001 { /glob "*" /type "deny" }
      # added for AEM forms specific use cases.
      /0003 { /glob "dataRef" /type "allow" }
      }
   ```

L’ambiente AEM è configurato per memorizzare nella cache i moduli adattivi. Memorizza in cache tutti i tipi di moduli adattivi. Se è necessario controllare le autorizzazioni di accesso utente per una pagina prima di distribuire la pagina in cache, consulta [memorizzazione in cache del contenuto protetto](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/permissions-cache.html).

## Risoluzione dei problemi {#troubleshooting}

### Alcuni moduli adattivi contenenti immagini o video non vengono invalidati automaticamente dalla cache del dispatcher {#videos-or-images-not-auto-invalidated}

#### Problema {#issue1}

Quando selezioni e aggiungi immagini o video tramite il browser risorse a un modulo adattivo e tali immagini e video vengono modificati nell’editor di Assets, i moduli adattivi contenenti tali immagini non vengono invalidati automaticamente dalla cache del dispatcher.

#### Soluzione {#Solution1}

Dopo aver pubblicato le immagini e il video, annulla esplicitamente la pubblicazione e pubblica i moduli adattivi che fanno riferimento a tali risorse.

### Solo la prima istanza di un modulo adattivo è memorizzata nella cache {#only-first-instance-of-adaptive-forms-is-cached}

#### Problema {#issue3}

Se l’URL del modulo adattivo non dispone di informazioni sulla localizzazione e **[!UICONTROL Use Browser Locale]** in configuration manager è abilitato, viene fornita una versione localizzata del modulo adattivo e viene memorizzata nella cache e distribuita solo la prima istanza del modulo adattivo a ogni utente successivo.

#### Soluzione {#Solution3}

Esegui i seguenti passaggi per risolvere il problema:

1. Apri conf.d/httpd-dispatcher.conf o qualsiasi altro file di configurazione configurato per il caricamento in fase di runtime.

1. Aggiungi il seguente codice al file e salvalo. Si tratta di un codice di esempio modificarlo in base all’ambiente.

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
