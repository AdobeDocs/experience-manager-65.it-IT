---
title: Ottimizzazione delle prestazioni del server AEM Forms
seo-title: Ottimizzazione delle prestazioni del server AEM Forms
description: Affinché AEM Forms funzioni in modo ottimale, puoi regolare con precisione le impostazioni della cache e i parametri JVM. Inoltre, l’utilizzo di un server web può migliorare le prestazioni della distribuzione AEM Forms.
seo-description: Affinché AEM Forms funzioni in modo ottimale, puoi regolare con precisione le impostazioni della cache e i parametri JVM. Inoltre, l’utilizzo di un server web può migliorare le prestazioni della distribuzione AEM Forms.
uuid: bf23b62c-7559-4726-8f4e-cc8b1457e501
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 38c0ec46-5686-4656-bfb4-7125ec194673
docset: aem65
role: Admin
exl-id: 22926757-9cdb-4f8a-9bd9-16ddbc3f954a
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 1%

---

# Ottimizzazione delle prestazioni del server AEM Forms{#performance-tuning-of-aem-forms-server}

Questo articolo illustra le strategie e le best practice che puoi implementare per ridurre i colli di bottiglia e ottimizzare le prestazioni della distribuzione AEM Forms.

## Impostazioni cache {#cache-settings}

Puoi configurare e controllare la strategia di caching per AEM Forms utilizzando il componente **Configurazioni Forms mobili** nella console Configurazione web AEM all&#39;indirizzo:

* (AEM Forms su OSGi) `https://'[server]:[port]'/system/console/configMgr`
* (AEM Forms su JEE) `https://'[server]:[port]'/lc/system/console/configMgr`

Le opzioni disponibili per la memorizzazione in cache sono le seguenti:

* **Nessuno**: Impone di non memorizzare in cache alcun artefatto. In pratica, ciò rallenta le prestazioni e richiede un&#39;elevata disponibilità di memoria a causa dell&#39;assenza di cache.
* **Conservatore**: Consente di memorizzare nella cache solo gli artefatti intermedi generati prima del rendering del modulo, ad esempio un modello contenente frammenti e immagini in linea.
* **Aggressivo**: Impone di memorizzare in cache quasi tutto ciò che può essere memorizzato in cache, incluso il contenuto HTML di cui è stato eseguito il rendering oltre a tutti gli artefatti dal livello di memorizzazione in cache conservativa. Consente di ottenere le migliori prestazioni, ma consuma anche più memoria per memorizzare gli artefatti memorizzati nella cache. La strategia di caching aggressiva consente di ottenere prestazioni a tempo costante nel rendering di un modulo mentre il contenuto di cui è stato eseguito il rendering viene memorizzato nella cache.

Le impostazioni di cache predefinite per AEM Forms potrebbero non essere sufficienti per ottenere prestazioni ottimali. Pertanto, si consiglia di utilizzare le seguenti impostazioni:

* **Strategia** cache: Aggressivo
* **Dimensione della cache**  (in termini di numero di moduli): Come richiesto
* **Dimensione** massima dell&#39;oggetto: Come richiesto

![Configurazioni Forms per dispositivi mobili](assets/snap.png)

>[!NOTE]
>
>Se utilizzi AEM Dispatcher per memorizzare nella cache i moduli adattivi, questo memorizza anche nella cache i moduli adattivi che contengono moduli con dati precompilati. Se tali moduli vengono serviti dalla cache AEM Dispatcher, potrebbe portare a fornire agli utenti dati precompilati o non aggiornati. Utilizza quindi AEM Dispatcher per memorizzare nella cache i moduli adattivi che non utilizzano dati precompilati. Inoltre, una cache del dispatcher non annulla automaticamente la validità dei frammenti memorizzati nella cache. Pertanto, non utilizzarlo per memorizzare nella cache i frammenti di modulo. Per tali moduli e frammenti, utilizza la [cache dei moduli adattivi](../../forms/using/configure-adaptive-forms-cache.md).

## Parametri JVM {#jvm-parameters}

Per ottenere prestazioni ottimali, si consiglia di utilizzare i seguenti argomenti JVM `init` per configurare i valori `Java heap` e `PermGen`.

```shell
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -Xms8192m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -Xmx8192m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -XX:PermSize=256m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -XX:MaxPermSize=1024m
```

>[!NOTE]
>
>Le impostazioni consigliate sono per Windows 2008 R2 8 Core e Oracle HotSpot 1.7 (64-bit) JDK e devono essere potenziate o ridotte in base alla configurazione del sistema.

## Utilizzo di un server web {#using-a-web-server}

Il rendering dei moduli adattivi e dei moduli HTML5 è in formato HTML5. L’output risultante potrebbe essere grande a seconda di fattori quali le dimensioni del modulo e le immagini nel modulo. Per ottimizzare il trasferimento dei dati, l’approccio consigliato consiste nel comprimere la risposta HTML utilizzando il server web da cui viene trasmessa la richiesta. Questo approccio riduce le dimensioni di risposta, il traffico di rete e il tempo necessario per lo streaming dei dati tra server e computer client.

Ad esempio, esegui i seguenti passaggi per abilitare la compressione su Apache Web Server 2.0 a 32 bit con JBoss:

>[!NOTE]
>
>Le istruzioni seguenti non si applicano ad alcun server diverso da Apache Web Server 2.0 a 32 bit. Per i passaggi specifici per qualsiasi altro server, consulta la documentazione di prodotto corrispondente.

I passaggi seguenti mostrano le modifiche necessarie per abilitare la compressione con Apache Web Server

**Ottieni il software del server web Apache applicabile al tuo sistema operativo**

* Windows: scarica il server web Apache dal sito Apache HTTP Server Project.
* Solaris a 64 bit: scaricare il server web Apache dal sito web Sunfreeware for Solaris.
* Linux: il server web Apache viene preinstallato su un sistema Linux.

Apache può comunicare con CRX utilizzando il protocollo HTTP. Le configurazioni sono per l’ottimizzazione tramite HTTP.

1. Rimuovi il commento alle seguenti configurazioni del modulo nel file `APACHE_HOME/conf/httpd.conf` .

   ```shell
   LoadModule proxy_balancer_module modules/mod_proxy.so
   LoadModule proxy_balancer_module modules/mod_proxy_http.so
   LoadModule deflate_module modules/mod_deflate.so
   ```

   >[!NOTE]
   >
   >Per Linux, il valore predefinito `APACHE_HOME` è `/etc/httpd/`.

1. Configura il proxy sulla porta 4502 di crx.
Aggiungi la seguente configurazione nel file di configurazione `APACHE_HOME/conf/httpd.conf` .

   ```shell
   ProxyPass / https://<server>:4502/
   ProxyPassReverse / https://<server>:4502/
   ```

1. Abilita compressione. Aggiungi la seguente configurazione nel file di configurazione `APACHE_HOME/conf/httpd.conf` .

   **Per i moduli HTML5**

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

   Per accedere al server crx, utilizza `https://'server':80`, dove `server` è il nome del server su cui è in esecuzione il server Apache.

## Utilizzo di un antivirus sul server che esegue AEM Forms {#using-an-antivirus-on-server-running-aem-forms}

È possibile riscontrare prestazioni lente sui server che eseguono un software antivirus. Un software sempre su antivirus (on-access scansione) scansiona tutti i file di un sistema. Può rallentare il server e le prestazioni di AEM Forms sono interessate.

Per migliorare le prestazioni, è possibile indirizzare il software antivirus per escludere i seguenti file e cartelle AEM Forms dalla scansione sempre attiva (all&#39;accesso):

* Directory di installazione AEM. Se non è possibile escludere la directory completa, escludi quanto segue:

   * [Directory di installazione AEM]\crx-repository\temp
   * [Directory di installazione AEM]\crx-repository\repository
   * [Directory di installazione AEM]\crx-repository\launchpad

* Directory temporanea del server applicazioni. Il percorso predefinito è:

   * (Jboss) [AEM directory di installazione]\jboss\standalone\tmp
   * (Weblogic) \Oracle\Middleware\user_projects\domains\LCDomain\servers\LCServer1\tmp
   * (Websphere) \Program Files\IBM\WebSphere\AppServer\profiles\AppSrv01\temp

* **(Solo per AEM Forms su JEE)** Directory Global Document Storage (GDS). Il percorso predefinito è:

   * (JBoss) [root appserver]/server/&#39;server&#39;/svcnative/DocumentStorage
   * (WebLogic) [appserverdomain]/&#39;server&#39;/adobe/LiveCycleServer/DocumentStorage
   * (WebSphere) [root dell&#39;appserver]/installApps/adobe/&#39;server&#39;/DocumentStorage

* **(Solo AEM Forms su JEE)** Registri del server AEM Forms e directory temporanea. Il percorso predefinito è:

   * Log del server - [Directory di installazione di AEM Forms]\Adobe\AEM forms\[app-server]\server\all\logs
   * Directory temporanea - [Directory di installazione AEM Forms]\temp

>[!NOTE]
>
>* Se utilizzi una posizione diversa per GDS e la directory temporanea, apri AdminUI in `https://'[server]:[port]'/adminui`, vai a **Home > Impostazioni > Impostazioni del sistema di base > Configurazioni di base** per confermare la posizione in uso.

* Se il server AEM Forms esegue lentamente anche dopo aver escluso le directory suggerite, escludere anche il file eseguibile Java (java.exe).


