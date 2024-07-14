---
title: Ottimizzazione delle prestazioni del server AEM Forms
description: Affinché AEM Forms possa funzionare in modo ottimale, puoi ottimizzare le impostazioni della cache e i parametri JVM. Inoltre, l’utilizzo di un server web può migliorare le prestazioni dell’implementazione di AEM Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
role: Admin,User
exl-id: 22926757-9cdb-4f8a-9bd9-16ddbc3f954a
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 0%

---

# Ottimizzazione delle prestazioni del server AEM Forms{#performance-tuning-of-aem-forms-server}

Questo articolo illustra strategie e best practice da implementare per ridurre i colli di bottiglia e ottimizzare le prestazioni dell’implementazione di AEM Forms.

## Impostazioni cache {#cache-settings}

Puoi configurare e controllare la strategia di caching per AEM Forms utilizzando il componente **Configurazioni Forms mobile** nella console di configurazione Web AEM all&#39;indirizzo:

* (AEM Forms su OSGi) `https://'[server]:[port]'/system/console/configMgr`
* (AEM Forms su JEE) `https://'[server]:[port]'/lc/system/console/configMgr`

Le opzioni disponibili per il caching sono le seguenti:

* **Nessuno**: Impone di non memorizzare in cache alcun artefatto. In pratica, questo rallenterà le prestazioni e richiederà un’elevata disponibilità di memoria a causa dell’assenza di cache.
* **Conservativo**: detta di memorizzare in cache solo gli artefatti intermedi generati prima del rendering del modulo, ad esempio un modello contenente frammenti e immagini in linea.
* **Aggressivo**: impone di memorizzare in cache quasi tutto ciò che può essere memorizzato in cache, incluso il contenuto HTML sottoposto a rendering oltre a tutti gli artefatti del livello di memorizzazione in cache conservativa. Offre le migliori prestazioni ma consuma anche più memoria per l’archiviazione degli artefatti memorizzati nella cache. Una strategia di caching aggressiva consente di ottenere prestazioni di tempo costanti nel rendering di un modulo quando il contenuto sottoposto a rendering viene memorizzato nella cache.

Le impostazioni predefinite della cache per AEM Forms potrebbero non essere sufficienti per ottenere prestazioni ottimali. Pertanto, si consiglia di utilizzare le seguenti impostazioni:

* **Strategia cache**: aggressiva
* **Dimensione cache** (in termini di numero di moduli): come richiesto
* **Dimensione massima oggetto**: come richiesto

![Configurazioni Forms mobile](assets/snap.png)

>[!NOTE]
>
>Se utilizzi AEM Dispatcher per memorizzare in cache i moduli adattivi, questo memorizza in cache anche i moduli contenenti dati precompilati. Se tali moduli vengono forniti dalla cache Dispatcher dell’AEM, ciò può portare a fornire agli utenti dati precompilati o non aggiornati. Pertanto, utilizza AEM Dispatcher per memorizzare nella cache i moduli adattivi che non utilizzano dati precompilati. Inoltre, una cache di Dispatcher non annulla automaticamente la validità dei frammenti memorizzati in cache. Pertanto, non utilizzarlo per memorizzare in cache i frammenti di modulo. Per questi moduli e frammenti, utilizza [Cache moduli adattivi](../../forms/using/configure-adaptive-forms-cache.md).

## Parametri JVM {#jvm-parameters}

Per prestazioni ottimali, si consiglia di utilizzare i seguenti argomenti JVM `init` per configurare `Java heap` e `PermGen`.

```shell
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -Xms8192m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -Xmx8192m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -XX:PermSize=256m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -XX:MaxPermSize=1024m
```

>[!NOTE]
>
>Le impostazioni consigliate sono per Windows 2008 R2 8 Core e Oracle HotSpot 1.7 (64 bit) JDK e devono essere scalate verso l&#39;alto o verso il basso in base alla configurazione del sistema.

## Utilizzo di un server web {#using-a-web-server}

I moduli adattivi e i moduli HTML5 vengono riprodotti in formato HTML5. L’output risultante potrebbe essere grande a seconda di fattori quali le dimensioni del modulo e le immagini nel modulo. Per ottimizzare il trasferimento di dati, l’approccio consigliato consiste nel comprimere la risposta del HTML utilizzando il server web da cui viene trasmessa la richiesta. Questo approccio riduce le dimensioni della risposta, il traffico di rete e il tempo necessario per lo streaming dei dati tra server e client.

Ad esempio, per abilitare la compressione sul server web Apache 2.0 a 32 bit con JBoss, effettua le seguenti operazioni®:

>[!NOTE]
>
>Le istruzioni seguenti non sono valide per i server diversi da Apache Web Server 2.0 a 32 bit. Per i passaggi specifici di qualsiasi altro server, consulta la relativa documentazione di prodotto.

I passaggi seguenti illustrano le modifiche necessarie per abilitare la compressione con il server web Apache

**Ottenere il software del server web Apache applicabile al sistema operativo**

* Windows: scarica il server web Apache dal sito del progetto Apache HTTP Server.
* Solaris™ a 64 bit: scarica il server web Apache dal sito web Sunfreeware for Solaris™.
* Linux®: il server web Apache è preinstallato su un sistema Linux®.

Apache può comunicare con CRX utilizzando il protocollo HTTP. Le configurazioni sono ottimizzate tramite HTTP.

1. Rimuovere il commento dalle seguenti configurazioni del modulo nel file `APACHE_HOME/conf/httpd.conf`.

   ```shell
   LoadModule proxy_balancer_module modules/mod_proxy.so
   LoadModule proxy_balancer_module modules/mod_proxy_http.so
   LoadModule deflate_module modules/mod_deflate.so
   ```

   >[!NOTE]
   >
   >Per Linux®, il valore predefinito `APACHE_HOME` è `/etc/httpd/`.

1. Configura il proxy sulla porta 4502 di crx.
Aggiungi la seguente configurazione nel file di configurazione `APACHE_HOME/conf/httpd.conf`.

   ```shell
   ProxyPass / https://<server>:4502/
   ProxyPassReverse / https://<server>:4502/
   ```

1. Abilita Compressione. Aggiungi la seguente configurazione nel file di configurazione `APACHE_HOME/conf/httpd.conf`.

   **Per moduli HTML5**

   ```xml
   <Location /content/xfaforms>
       <IfModule mod_deflate.c>
           SetOutputFilter DEFLATE
           #Do not compress
           SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
           SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
           #Dealing with proxy servers
               <IfModule mod_headers.c>
                   Header append Vary User-Agent
               </IfModule>
       </IfModule>
   </Location>
   ```

   **Per moduli adattivi**

   ```xml
   <Location /content/forms/af>
       <IfModule mod_deflate.c>
           SetOutputFilter DEFLATE
           #Do not compress
           SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
           SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
           #Dealing with proxy servers
               <IfModule mod_headers.c>
                   Header append Vary User-Agent
               </IfModule>
       </IfModule>
   </Location>
   ```

   Per accedere al server crx, utilizzare `https://'server':80`, dove `server` è il nome del server in cui è in esecuzione il server Apache.

## Utilizzo di un antivirus su un server che esegue AEM Forms {#using-an-antivirus-on-server-running-aem-forms}

È possibile riscontrare un rallentamento delle prestazioni sui server che eseguono un software antivirus. Un software antivirus sempre attivo (scansione all&#39;accesso) esegue la scansione di tutti i file di un sistema. Può rallentare il server e influire sulle prestazioni dell’AEM Forms.

Per migliorare le prestazioni, è possibile indirizzare il software antivirus per escludere i seguenti file e cartelle di AEM Forms dalla scansione sempre attiva (all&#39;accesso):

* Directory di installazione AEM. Se non è possibile escludere la directory completa, escludere quanto segue:

   * [Directory di installazione AEM]\crx-repository\temp
   * [Directory di installazione AEM]\crx-repository\repository
   * [Directory di installazione AEM]\crx-repository\launchpad

* Directory temporanea del server applicazioni. La posizione predefinita è:

   * (JBoss®) [Directory di installazione AEM]\jboss\standalone\tmp
   * (WebLogic) \Oracle\Middleware\user_projects\domains\LCDomain\servers\LCServer1\tmp
   * (WebSphere®) \Programma Files\IBM\WebSphere\AppServer\profiles\AppSrv01\temp

* **(solo AEM Forms su JEE)** directory Global Document Storage (GDS). La posizione predefinita è:

   * (JBoss®) [radice server applicazioni]/server/&#39;server&#39;/svcnative/DocumentStorage
   * (WebLogic) [appserverdomain]/&#39;server&#39;/adobe/LiveCycleServer/DocumentStorage
   * (WebSphere®) [radice del server applicazioni]/installApps/adobe/&#39;server&#39;/DocumentStorage

* **(solo AEM Forms su JEE)** registri di AEM Forms Server e directory temporanea. La posizione predefinita è:

   * Registri del server - [Directory di installazione di AEM Forms]\Adobe\AEM forms\[app-server]\server\all\logs
   * Directory temporanea - [Directory di installazione di AEM Forms]\temp

>[!NOTE]
>
>* Se utilizzi una posizione diversa per GDS e la directory temporanea, apri AdminUI in `https://'[server]:[port]'/adminui`, passa a **Home > Impostazioni > Impostazioni sistema core > Configurazioni core** per confermare la posizione in uso.
>
* Se il server AEM Forms funziona lentamente anche dopo l’esclusione delle directory suggerite, escludi anche il file eseguibile Java™ (java.exe).
>
