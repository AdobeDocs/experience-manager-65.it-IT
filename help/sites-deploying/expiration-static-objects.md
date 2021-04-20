---
title: Scadenza degli oggetti statici
seo-title: Scadenza degli oggetti statici
description: Scopri come configurare AEM in modo che gli oggetti statici non scadano (per un periodo di tempo ragionevole).
seo-description: Scopri come configurare AEM in modo che gli oggetti statici non scadano (per un periodo di tempo ragionevole).
uuid: ee019a3d-4133-4d40-98ec-e0914b751fb3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 73f37b3c-5dbe-4132-bb60-daa8de871884
feature: Configuring
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---


# Scadenza oggetti statici{#expiration-of-static-objects}

Gli oggetti statici (ad esempio, le icone) non cambiano. Pertanto, il sistema deve essere configurato in modo che non scadano (per un periodo di tempo ragionevole) e quindi riducano il traffico inutile.

Questo ha il seguente impatto:

* Consente di scaricare le richieste dall&#39;infrastruttura del server.
* Aumenta le prestazioni del caricamento della pagina, quando il browser memorizza in cache gli oggetti nella cache del browser.

Le scadenze sono specificate dallo standard HTTP per quanto riguarda la &quot;scadenza&quot; dei file (vedi, ad esempio, il capitolo 14.21 di [RFC 2616](https://www.ietf.org/rfc/rfc2616.txt) &quot; Hypertext Transfer Protocol — HTTP 1.1&quot;). Questo standard utilizza l’intestazione per consentire ai client di memorizzare in cache gli oggetti finché non vengono considerati obsoleti; tali oggetti vengono memorizzati nella cache per il periodo di tempo specificato senza che venga effettuato alcun controllo dello stato al server di origine.

>[!NOTE]
>
>Questa configurazione è completamente separata dal Dispatcher (e non funzionerà per).
>
>Lo scopo del Dispatcher è quello di memorizzare i dati nella cache di fronte a AEM.

Tutti i file che non sono dinamici e che non cambiano nel tempo possono e devono essere memorizzati nella cache. La configurazione per il server HTTPD di Apache potrebbe essere simile a una delle seguenti, a seconda dell’ambiente:

>[!CAUTION]
>
>È necessario prestare attenzione quando si definisce il periodo di tempo durante il quale un oggetto viene considerato aggiornato. Poiché non c&#39;è *nessun controllo finché il periodo di tempo specificato non è scaduto*, il client può finire per presentare il vecchio contenuto dalla cache.

1. **Per un&#39;istanza Author:**

   ```xml
   LoadModule expires_module modules/mod_expires.so
   <Location /libs>
     ExpiresByType text/css "access plus 1 month"
     ExpiresByType text/javascript "access plus 1 month"
     ExpiresByType image/png "access plus 1 month"
     ExpiresByType image/gif "access plus 1 month"
   </Location>
   ```

   Questo consente alla cache intermedia (ad esempio la cache del browser) di memorizzare i file CSS, Javascript, PNG e GIF per un massimo di un mese, fino alla scadenza. Ciò significa che non devono essere richiesti da AEM o dal server web, ma possono rimanere nella cache del browser.

   Altre sezioni del sito non devono essere memorizzate nella cache in un’istanza dell’autore, in quanto sono soggette a modifiche in qualsiasi momento.

1. **Per un&#39;istanza Publish:**

   ```xml
   LoadModule expires_module modules/mod_expires.so
   <Location /content>
     ExpiresByType text/css "access plus 1 day"
     ExpiresByType text/javascript "access plus 1 day"
     ExpiresByType image/png "access plus 1 day"
     ExpiresByType image/gif "access plus 1 day"
   </Location>
   <Location /etc/designs>
     ExpiresByType text/css "access plus 1 day"
     ExpiresByType text/javascript "access plus 1 day"
     ExpiresByType image/png "access plus 1 day"
     ExpiresByType image/gif "access plus 1 day"
   </Location>
   ```

   Questo consente alla cache intermedia (ad esempio la cache del browser) di memorizzare i file CSS, Javascript, PNG e GIF per un massimo di un giorno nelle cache client. Anche se questo esempio illustra le impostazioni globali per tutti gli elementi inferiori a `/content` e `/etc/designs`, è necessario renderli più granulari.

   A seconda della frequenza con cui il sito viene aggiornato, è anche possibile considerare la memorizzazione in cache delle pagine HTML. Un periodo di tempo ragionevole sarebbe di 1 ora:

   ```xml
   <Location /content>
     ExpiresByType text/html "access plus 1 hour"
   </Location>
   ```

Dopo aver configurato gli oggetti statici, eseguire la scansione `request.log`, selezionando le pagine che contengono tali oggetti, per confermare che non sono state effettuate richieste (non necessarie) per gli oggetti statici.
