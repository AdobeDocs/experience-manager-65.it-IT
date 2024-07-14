---
title: Configurare la cache dei moduli adattivi
description: La cache dei moduli adattivi è progettata appositamente per i moduli e i documenti adattivi. Memorizza nella cache i moduli adattivi e i documenti adattivi con l’obiettivo di ridurre il tempo necessario per eseguire il rendering di un modulo o di un documento adattivo sul client.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
role: Admin,User
exl-id: 153986f0-b6ff-4278-8bb6-70c320a4e539
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Foundation Components
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 1%

---

# Configurare la cache dei moduli adattivi {#configure-adaptive-forms-cache}

La cache è un meccanismo che consente di ridurre i tempi di accesso ai dati, ridurre la latenza e migliorare le velocità di input/output (I/O). La cache dei moduli adattivi memorizza solo il contenuto HTML e la struttura JSON di un modulo adattivo senza salvare dati precompilati. Consente di ridurre il tempo necessario per il rendering di un modulo adattivo sul client. È progettato appositamente per i moduli adattivi.

## Configurare la cache dei moduli adattivi nelle istanze di authoring e pubblicazione {#configure-adaptive-forms-caching-at-author-and-publish-instances}

1. Passare a Gestione configurazione console Web AEM in `https://[server]:[port]/system/console/configMgr`.
1. Fai clic su **[!UICONTROL Configurazione modulo adattivo e canale web di comunicazione interattiva]** per modificarne i valori di configurazione.
1. Nella finestra di dialogo [!UICONTROL modifica valori configurazione], specifica il numero massimo di moduli o documenti, un&#39;istanza del server AEM [!DNL Forms] può memorizzare nella cache nel campo **[!UICONTROL Numero di Forms adattivi]**. Il valore predefinito è 100.

   >[!NOTE]
   >
   >Per disabilitare la cache, imposta il valore nel campo Numero di Forms adattivi su **0**. La cache viene reimpostata e tutti i moduli e i documenti vengono rimossi dalla cache quando si disattiva o si modifica la configurazione della cache.

   ![Finestra di dialogo di configurazione per la cache HTML dei moduli adattivi](assets/cache-configuration-edit.png)

1. Fai clic su **[!UICONTROL Salva]** per salvare la configurazione.

L’ambiente è configurato per l’utilizzo di moduli adattivi della cache e delle relative risorse.


## (Facoltativo) Configurazione della cache dei moduli adattivi in Dispatcher {#configure-the-cache}

Puoi anche configurare il caching dei moduli adattivi in Dispatcher per un ulteriore miglioramento delle prestazioni.

### Prerequisiti {#pre-requisites}

* Abilita l&#39;opzione [unione o precompilazione dei dati nel client](prepopulate-adaptive-form-fields.md#prefill-at-client). Consente di unire dati univoci per ogni istanza di un modulo precompilato.

### Considerazioni per la memorizzazione nella cache dei moduli adattivi su un Dispatcher {#considerations}

* Quando utilizzi la cache dei moduli adattivi, utilizza l’AEM [!DNL Dispatcher] per memorizzare nella cache le librerie client (CSS e JavaScript) di un modulo adattivo.
* Durante lo sviluppo di componenti personalizzati, nel server utilizzato per lo sviluppo, mantieni disabilitata la cache dei moduli adattivi.
* Gli URL senza estensione non vengono memorizzati in cache. Ad esempio, gli URL con pattern `/content/forms/[folder-structure]/[form-name].html` vengono memorizzati nella cache e la memorizzazione nella cache ignora gli URL con pattern `/content/dam/formsanddocument/[folder-name]/<form-name>/jcr:content`. Pertanto, utilizza gli URL con estensioni per sfruttare i vantaggi del caching.
* Considerazioni per i moduli adattivi localizzati:
   * Utilizza il formato URL `http://host:port/content/forms/af/<afName>.<locale>.html` per richiedere una versione localizzata di un modulo adattivo invece di `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`
   * [Disattivare utilizzando le impostazioni locali del browser](supporting-new-language-localization.md#how-localization-of-adaptive-form-works) per gli URL con formato `http://host:port/content/forms/af/<adaptivefName>.html`.
   * Quando si utilizza il formato URL `http://host:port/content/forms/af/<adaptivefName>.html` e **[!UICONTROL Usa impostazioni locali del browser]** in Gestione configurazione è disabilitato, viene distribuita la versione non localizzata del modulo adattivo. La lingua non localizzata è la lingua utilizzata durante lo sviluppo del modulo adattivo. Le impostazioni locali configurate per il browser (impostazioni locali del browser) non vengono considerate e viene distribuita una versione non localizzata del modulo adattivo.
   * Quando si utilizza il formato URL `http://host:port/content/forms/af/<adaptivefName>.html` e si attiva **[!UICONTROL Usa impostazioni locali browser]** in Gestione configurazione, viene distribuita una versione localizzata del modulo adattivo, se disponibile. La lingua del modulo adattivo localizzato si basa sulla lingua configurata per il browser (lingua del browser). Può causare il caching di [solo della prima istanza di un modulo adattivo]. Per evitare che il problema si verifichi nell&#39;istanza, vedere [risoluzione dei problemi](#only-first-insatnce-of-adptive-forms-is-cached).

### Abilita caching in Dispatcher

Per abilitare e configurare la memorizzazione in cache dei moduli adattivi su Dispatcher, effettua le seguenti operazioni:

1. Apri il seguente URL per ogni istanza di pubblicazione dell&#39;ambiente e [abilita l&#39;agente di svuotamento per le istanze di pubblicazione dell&#39;ambiente](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance):
   `http://[server]:[port]]/etc/replication/agents.publish/flush.html`

1. [Aggiungi quanto segue al file dispatcher.any](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#automatically-invalidating-cached-files):

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

   * Quando viene pubblicata una versione più recente di una risorsa a cui si fa riferimento in un modulo adattivo, i moduli adattivi interessati vengono automaticamente invalidati. Esistono alcune eccezioni all’annullamento automatico della validità delle risorse di riferimento. Per informazioni sulle eccezioni, vedere la sezione [risoluzione dei problemi](#troubleshooting).
1. [Aggiungi il seguente file di regole dispatcher.any o personalizzato](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#specifying-the-documents-to-cache). Sono esclusi gli URL che non supportano il caching. Ad esempio, la comunicazione interattiva.

   ```JSON
      /0000 {
            /glob "*"
            /type "allow"
      }
      ## Do not cache csrf login tokens
      /0001 {
            /glob "/libs/granite/csrf/token.json"
            /type "deny"
      }
      ## Do not cache IC - print channel
      /0002 {
            /glob "/content/forms/**/channels/print.html"
            /type "deny"
      }
      ## Do not cache IC - web channel
      /0003 {
            /glob "/content/forms/**/channels/web.html"
            /type "deny"
      }
   ```

1. [Aggiungere i seguenti parametri all&#39;elenco dei parametri URL da ignorare](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#ignoring-url-parameters):

   ```JSON
      /ignoreUrlParams {
      /0001 { /glob "*" /type "deny" }
      # added for AEM forms specific use cases.
      /0003 { /glob "dataRef" /type "allow" }
      }
   ```

L’ambiente AEM è configurato per memorizzare nella cache i moduli adattivi. Memorizza nella cache tutti i tipi di moduli adattivi. Se prima di distribuire la pagina memorizzata in cache è necessario verificare le autorizzazioni di accesso utente per una pagina, vedere [memorizzazione in cache del contenuto protetto](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=it).

## Risoluzione dei problemi {#troubleshooting}

### Alcuni moduli adattivi contenenti immagini o video non vengono invalidati automaticamente dalla cache di Dispatcher {#videos-or-images-not-auto-invalidated}

#### Problema   {#issue1}

Quando selezioni e aggiungi immagini o video tramite il browser di risorse a un modulo adattivo e tali immagini e video vengono modificati nell’editor di Assets, i moduli adattivi contenenti tali immagini non vengono invalidati automaticamente dalla cache di Dispatcher.

#### Soluzione {#Solution1}

Dopo aver pubblicato le immagini e il video, annulla esplicitamente la pubblicazione e pubblica i moduli adattivi che fanno riferimento a tali risorse.

### Solo la prima istanza di un modulo adattivo è memorizzata in cache {#only-first-instance-of-adaptive-forms-is-cached}

#### Problema   {#issue3}

Se l&#39;URL del modulo adattivo non dispone di informazioni sulla localizzazione e **[!UICONTROL Usa impostazioni locali browser]** nella gestione della configurazione è abilitato, viene distribuita una versione localizzata del modulo adattivo. Solo la prima istanza del modulo adattivo viene memorizzata in cache e distribuita a ogni utente successivo.

#### Soluzione {#Solution3}

Per risolvere il problema, effettuare le seguenti operazioni:

1. Apri il file conf.d/httpd-dispatcher.conf o qualsiasi altro file di configurazione configurato per il caricamento in fase di esecuzione.

1. Aggiungi il seguente codice al file e salvalo. Si tratta di un codice di esempio per modificarlo in base all’ambiente in uso.

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
