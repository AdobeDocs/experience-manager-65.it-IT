---
title: Scadenza degli oggetti statici
seo-title: Scadenza degli oggetti statici
description: Scoprite come configurare AEM in modo che gli oggetti statici non scadano (per un periodo di tempo ragionevole).
seo-description: Scoprite come configurare AEM in modo che gli oggetti statici non scadano (per un periodo di tempo ragionevole).
uuid: ee019a3d-4133-4d40-98ec-e0914b751fb3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 73f37b3c-5dbe-4132-bb60-daa8de871884
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---


# Scadenza di oggetti statici{#expiration-of-static-objects}

Gli oggetti statici (ad esempio, le icone) non vengono modificati. Pertanto, il sistema deve essere configurato in modo che non scada (per un periodo di tempo ragionevole) e quindi riduca il traffico inutile.

Questo ha il seguente impatto:

* Consente di scaricare le richieste dall&#39;infrastruttura del server.
* Aumenta le prestazioni di caricamento della pagina, man mano che il browser memorizza nella cache gli oggetti.

Le scadenze sono specificate dallo standard HTTP per quanto riguarda la &quot;scadenza&quot; dei file (vedere, ad esempio, il capitolo 14.21 di [RFC 2616](https://www.ietf.org/rfc/rfc2616.txt) &quot; Hypertext Transfer Protocol — HTTP 1.1&quot;). Questo standard utilizza l’intestazione per consentire ai client di memorizzare gli oggetti nella cache fino a quando non vengono considerati obsoleti; tali oggetti vengono memorizzati nella cache per il periodo di tempo specificato senza che venga eseguito il controllo dello stato sul server di origine.

>[!NOTE]
>
>Questa configurazione è completamente separata dal Dispatcher (e non funziona per esso).
>
>Lo scopo del Dispatcher è quello di memorizzare i dati nella cache davanti a AEM.

Tutti i file, che non sono dinamici e che non subiscono modifiche nel tempo, possono e devono essere memorizzati nella cache. La configurazione per il server Apache HTTPD potrebbe essere simile a una delle seguenti, a seconda dell&#39;ambiente:

>[!CAUTION]
>
>È necessario prestare attenzione quando si definisce il periodo di tempo durante il quale un oggetto viene considerato aggiornato. Poiché *nessun controllo fino alla scadenza del periodo di tempo specificato*, il client può presentare il contenuto precedente dalla cache.

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

   Questo consente alla cache intermedia (ad esempio, la cache del browser) di memorizzare i file CSS, Javascript, PNG e GIF per un massimo di un mese, fino alla scadenza. Ciò significa che non devono essere richiesti da AEM o dal server Web, ma possono rimanere nella cache del browser.

   Altre sezioni del sito non devono essere memorizzate nella cache in un’istanza di authoring, in quanto sono soggette a modifiche in qualsiasi momento.

1. **Per un’istanza Pubblica:**

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

   Questo consente alla cache intermedia (ad esempio, la cache del browser) di memorizzare i file CSS, Javascript, PNG e GIF per un massimo di un giorno nelle cache client. Anche se questo esempio illustra le impostazioni globali per tutti gli elementi inferiori a `/content` e `/etc/designs`, è necessario renderli più granulari.

   A seconda della frequenza con cui il sito viene aggiornato, è anche possibile memorizzare nella cache le pagine HTML. Un periodo di tempo ragionevole sarebbe di 1 ora:

   ```xml
   <Location /content>
     ExpiresByType text/html "access plus 1 hour"
   </Location>
   ```

Dopo aver configurato gli oggetti statici, eseguire la scansione `request.log`, selezionando le pagine che contengono tali oggetti, per confermare che non è stata eseguita alcuna richiesta (non necessaria) per gli oggetti statici.
