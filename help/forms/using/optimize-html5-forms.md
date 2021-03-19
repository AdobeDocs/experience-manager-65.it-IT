---
title: Ottimizzazione dei moduli HTML5
seo-title: Ottimizzazione dei moduli HTML5
description: È possibile ottimizzare le dimensioni di output dei moduli HTML5.
seo-description: È possibile ottimizzare le dimensioni di output dei moduli HTML5.
uuid: 959f0b6a-9e4d-478a-afa8-4c39011fdf7a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bdb9edc2-6a37-4d3f-97d5-0fc5664316be
feature: Forms Mobile
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---


# Ottimizzazione dei moduli HTML5 {#optimizing-html-forms}

Nei moduli HTML5 viene eseguito il rendering dei moduli in formato HTML5. L’output risultante potrebbe essere grande a seconda di fattori quali le dimensioni del modulo e le immagini nel modulo. Per ottimizzare il trasferimento dei dati, l’approccio consigliato consiste nel comprimere la risposta HTML utilizzando il server web da cui viene distribuita la richiesta. Questo approccio riduce le dimensioni di risposta, il traffico di rete e il tempo necessario per lo streaming dei dati tra server e computer client.

Questo articolo descrive i passaggi necessari per abilitare la compressione per Apache Web Server 2.0 a 32 bit, con JBoss.

>[!NOTE]
>
>Le istruzioni seguenti non si applicano a server diversi da Apache Web Server 2.0 a 32 bit.

Ottieni il software del server web Apache applicabile al tuo sistema operativo:

* Per Windows, scarica il server web Apache dal sito Apache HTTP Server Project.
* Per Solaris a 64 bit, scaricare il server Web Apache dal sito Web Sunfreeware per Solaris.
* Per Linux, il server web Apache è preinstallato su un sistema Linux.

Apache può comunicare con JBoss utilizzando HTTP o il protocollo AJP.

1. Rimuovi il commento alle seguenti configurazioni del modulo nel file *APACHE_HOME/conf/httpd.conf* .

   ```java
   LoadModule proxy_balancer_module modules/mod_proxy.so
   LoadModule proxy_balancer_module modules/mod_proxy_http.so
   LoadModule deflate_module modules/mod_deflate.so
   ```

   >[!NOTE]
   >
   >Per Linux, la directory APACHE_HOME predefinita è /etc/httpd/.

1. Configura il proxy sulla porta 8080 di JBoss.

   Aggiungi la seguente configurazione al file di configurazione *APACHE_HOME/conf/httpd.conf* .

   ```java
   ProxyPass / https://<server_Name>:8080/
   ProxyPassReverse / https://<server_Name>:8080/
   ```

   >[!NOTE]
   >
   >Quando utilizzi un proxy, sono necessarie le seguenti modifiche di configurazione:
   >
   >* Accesso: *https://&lt;server>:&lt;port>/system/console/configMgr*
   * Modifica la configurazione per il filtro di riferimento Apache Sling
   * In Consenti host, aggiungi la voce per il server proxy


1. Abilita compressione.

   Aggiungi la seguente configurazione al file di configurazione *APACHE_HOME/conf/httpd.conf* .

   ```xml
   <Location /content/xfaforms>
     <IfModule mod_deflate.c>
        SetOutputFilter DEFLATE
        # Don’t compress
        SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
        SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
       #Dealing with proxy servers
   
        <IfModule mod_headers.c>
           Header append Vary User-Agent
        </IfModule>
     </IfModule>
   </Location>
   ```

1. Per accedere al server AEM, utilizza https://[Apache_server]:80.
