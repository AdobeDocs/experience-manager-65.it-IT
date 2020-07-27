---
title: Ottimizzazione delle prestazioni del server AEM Forms
seo-title: Ottimizzazione delle prestazioni del server AEM Forms
description: Per ottimizzare le prestazioni degli AEM Forms, è possibile regolare le impostazioni della cache e i parametri JVM. Inoltre, l'utilizzo di un server Web può migliorare le prestazioni della distribuzione dei AEM Forms.
seo-description: Per ottimizzare le prestazioni degli AEM Forms, è possibile regolare le impostazioni della cache e i parametri JVM. Inoltre, l'utilizzo di un server Web può migliorare le prestazioni della distribuzione dei AEM Forms.
uuid: bf23b62c-7559-4726-8f4e-cc8b1457e501
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 38c0ec46-5686-4656-bfb4-7125ec194673
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---


# Ottimizzazione delle prestazioni del server AEM Forms{#performance-tuning-of-aem-forms-server}

Questo articolo illustra le strategie e le procedure ottimali che potete implementare per ridurre i colli di bottiglia e ottimizzare le prestazioni della distribuzione dei AEM Forms.

## Impostazioni cache {#cache-settings}

Puoi configurare e controllare la strategia di caching per i AEM Forms mediante il componente Configurazioni **di moduli** mobili nella console di configurazione Web di AEM all’indirizzo:

* (AEM Forms in OSGi) `https://'[server]:[port]'/system/console/configMgr`
* (AEM Forms on JEE) `https://'[server]:[port]'/lc/system/console/configMgr`

Le opzioni disponibili per il caching sono le seguenti:

* **Nessuno**: Impone di non memorizzare nella cache alcun artefatto. In pratica, ciò rallenta le prestazioni e richiede un&#39;elevata disponibilità di memoria a causa dell&#39;assenza di cache.
* **Conservatore**: Consente di memorizzare nella cache solo gli artefatti intermedi generati prima del rendering del modulo, ad esempio un modello contenente frammenti e immagini in linea.
* **Aggressivo**: Impone di memorizzare nella cache quasi tutto ciò che può essere memorizzato nella cache, incluso il contenuto HTML di cui è stato eseguito il rendering oltre a tutti gli artefatti del livello di memorizzazione nella cache conservativa. Le prestazioni risultano ottimali, ma viene utilizzata anche più memoria per memorizzare gli artefatti memorizzati nella cache. La strategia di caching aggressivo consente di ottenere prestazioni in tempo reale durante il rendering di un modulo durante la memorizzazione nella cache del contenuto di cui è stato eseguito il rendering.

Le impostazioni predefinite della cache per i AEM Forms potrebbero non essere sufficienti per ottenere prestazioni ottimali. Pertanto, si consiglia di utilizzare le seguenti impostazioni:

* **Strategia** cache: Aggressivo
* **Dimensione** cache (in termini di numero di moduli): Come richiesto
* **Dimensione** massima oggetto: Come richiesto

![Configurazioni di moduli mobili](assets/snap.png)

>[!NOTE]
>
>Se utilizzate AEM Dispatcher per memorizzare i moduli adattivi nella cache, questi vengono memorizzati anche nei moduli adattivi contenenti moduli con dati precompilati. Se tali moduli vengono memorizzati nella cache di AEM Dispatcher, potrebbe causare la trasmissione di dati precompilati o non aggiornati agli utenti. Utilizzate quindi AEM Dispatcher per memorizzare nella cache i moduli adattivi che non utilizzano dati precompilati. Inoltre, la cache del dispatcher non invalida automaticamente i frammenti memorizzati nella cache. Pertanto, non utilizzarlo per memorizzare nella cache i frammenti di modulo. Per tali moduli e frammenti, utilizzare la cache [dei moduli](../../forms/using/configure-adaptive-forms-cache.md)adattivi.

## Parametri JVM {#jvm-parameters}

Per ottenere prestazioni ottimali, si consiglia di utilizzare i seguenti `init` argomenti JVM per configurare il `Java heap` e `PermGen`.

```shell
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -Xms8192m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -Xmx8192m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -XX:PermSize=256m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -XX:MaxPermSize=1024m
```

>[!NOTE]
>
>Le impostazioni consigliate sono per Windows 2008 R2 8 Core e per Oracle HotSpot 1.7 (64 bit) JDK e devono essere ridimensionate in base alla configurazione del sistema.

## Utilizzo di un server Web {#using-a-web-server}

Il rendering dei moduli adattivi e dei moduli HTML5 è in formato HTML5. L&#39;output risultante potrebbe essere grande a seconda di fattori come la dimensione del modulo e le immagini nel modulo. Per ottimizzare il trasferimento dei dati, si consiglia di comprimere la risposta HTML utilizzando il server Web da cui viene distribuita la richiesta. Questo approccio riduce le dimensioni di risposta, il traffico di rete e il tempo necessario per lo streaming dei dati tra computer server e client.

Ad esempio, per abilitare la compressione su Apache Web Server 2.0 a 32 bit con JBoss, eseguire le operazioni seguenti:

>[!NOTE]
>
>Le seguenti istruzioni non si applicano ad alcun server diverso da Apache Web Server 2.0 a 32 bit. Per i passaggi specifici per qualsiasi altro server, consulta la documentazione di prodotto corrispondente.

I passaggi seguenti dimostrano le modifiche necessarie per abilitare la compressione con Apache Web Server

**Ottenete il software del server Web Apache applicabile al vostro sistema operativo**

* Windows: scaricate il server Web Apache dal sito Apache HTTP Server Project.
* Solaris a 64 bit: scaricate il server Web Apache dal sito Web Sunfreeware per Solaris.
* Linux: il server Web Apache è preinstallato in un sistema Linux.

Apache può comunicare con CRX utilizzando il protocollo HTTP. Le configurazioni sono per l&#39;ottimizzazione tramite HTTP.

1. Rimuovete il commento dalle seguenti configurazioni del modulo nel `APACHE_HOME/conf/httpd.conf` file.

   ```shell
   LoadModule proxy_balancer_module modules/mod_proxy.so
   LoadModule proxy_balancer_module modules/mod_proxy_http.so
   LoadModule deflate_module modules/mod_deflate.so
   ```

   >[!NOTE]
   >
   >Per Linux, il valore predefinito `APACHE_HOME` è `/etc/httpd/`.

1. Configurare il proxy sulla porta 4502 di crx.
Aggiungi la seguente configurazione nel file di `APACHE_HOME/conf/httpd.conf` configurazione.

   ```shell
   ProxyPass / https://<server>:4502/
   ProxyPassReverse / https://<server>:4502/
   ```

1. Abilita compressione. Aggiungi la seguente configurazione nel file di `APACHE_HOME/conf/httpd.conf` configurazione.

   **Per moduli HTML5**

   ```xml
   <Location /content/xfaforms>
       <IfModule mod_deflate.c>
           SetOutputFilter DEFLATE
           #Don’t compress
           SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
           SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
           #Dealing with proxy servers
               <IfModule mod_headers.c>
                   Header append Vary User-Agent
               </IfModule>
       </IfModule>
   </Location>
   ```

   **Per i moduli adattivi**

   ```xml
   <Location /content/forms/af>
       <IfModule mod_deflate.c>
           SetOutputFilter DEFLATE
           #Don’t compress
           SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
           SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
           #Dealing with proxy servers
               <IfModule mod_headers.c>
                   Header append Vary User-Agent
               </IfModule>
       </IfModule>
   </Location>
   ```

   Per accedere al server crx, utilizzate `https://'server':80`, dove `server` è il nome del server su cui è in esecuzione il server Apache.

## Utilizzo di un antivirus sul server in cui sono in esecuzione AEM Forms {#using-an-antivirus-on-server-running-aem-forms}

È possibile che sui server in cui è in esecuzione un software antivirus si verifichino rallentamenti delle prestazioni. Un software antivirus sempre su (scansione on-access) analizza tutti i file di un sistema. Può rallentare il server e le prestazioni degli AEM Forms sono influenzate.

Per migliorare le prestazioni, è possibile indirizzare il software antivirus per escludere i seguenti file di AEM Forms e cartelle dalla scansione sempre attiva (all&#39;accesso):

* Directory di installazione di AEM. Se non è possibile escludere la directory completa, escludere quanto segue:

   * [Directory]di installazione di AEM \crx-repository\temp
   * [Directory]di installazione di AEM \crx-repository\repository
   * [Directory]di installazione di AEM \crx-repository\launchpad

* Directory temporanea del server applicazioni. Il percorso predefinito è:

   * (Jboss) Directory di installazione di [AEM]\jboss\standalone\tmp
   * (Weblogic) \Oracle\Middleware\user_projects\domains\LCDomain\servers\LCServer1\tmp
   * (Sfera Web) \Program Files\IBM\WebSphere\AppServer\profiles\AppSrv01\temp

* **(solo AEM Forms su JEE)** Directory Global Document Storage (GDS). Il percorso predefinito è:

   * (JBoss) [appserver root]/server/&#39;server&#39;/svcnative/DocumentStorage
   * (WebLogic) [appserverdomain]/&#39;server&#39;/adobe/LiveCycleServer/DocumentStorage
   * (WebSphere) [appserver root]/installedApps/adobe/&#39;server&#39;/DocumentStorage

* **(solo AEM Forms su JEE)** registri del server AEM Forms e directory temporanea. Il percorso predefinito è:

   * Registri di server - [AEM Forms della directory di installazione]\Adobe\AEM forms\[app-server]\server\all\logs
   * Directory Temp - Directory di installazione [AEM Forms]\temp

>[!NOTE]
>
>* Se state utilizzando una posizione diversa per GDS e directory temporanea, aprite AdminUI in `https://'[server]:[port]'/adminui`, andate a **Home > Impostazioni > Impostazioni sistema di base > Configurazioni** di base per confermare la posizione in uso.

* Se il server AEM Forms viene eseguito lentamente anche dopo l&#39;esclusione delle directory suggerite, escludere anche il file eseguibile Java (java.exe).



