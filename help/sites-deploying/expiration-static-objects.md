---
title: Scadenza degli oggetti statici
description: Scopri come configurare Adobe Experience Manager in modo che gli oggetti statici non scadano (per un periodo di tempo ragionevole).
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: bfd5441c-19cc-4fa8-b597-b1221465f75d
source-git-commit: 3885cc51f7e821cdb352737336a29f9c4f0c2f41
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---

# Scadenza degli oggetti statici{#expiration-of-static-objects}

Gli oggetti statici, ad esempio le icone, non vengono modificati. Pertanto, il sistema deve essere configurato in modo che non scadano (per un periodo di tempo ragionevole) e in modo da ridurre il traffico non necessario.

Questo ha il seguente impatto:

* Ripartisce il carico delle richieste dall&#39;infrastruttura del server.
* Aumenta le prestazioni di caricamento della pagina, poiché il browser memorizza nella cache gli oggetti nel browser.

Le scadenze sono specificate dallo standard HTTP relativo alla &quot;scadenza&quot; dei file (ad esempio, vedi il capitolo 14.21 del [RFC 2616](https://www.ietf.org/rfc/rfc2616.txt) &quot; Hypertext Transfer Protocol — HTTP 1.1&quot;). Questo standard utilizza l’intestazione per consentire ai client di memorizzare in cache gli oggetti fino a quando non vengono considerati obsoleti; tali oggetti vengono memorizzati in cache per il periodo di tempo specificato senza che venga eseguito alcun controllo dello stato sul server di origine.

>[!NOTE]
>
>Questa configurazione è separata (e non funzionerà) da Dispatcher.
>
>Lo scopo del Dispatcher è quello di memorizzare in cache i dati prima di Adobe Experience Manager (AEM).

Tutti i file non dinamici che non cambiano nel tempo possono e devono essere memorizzati in cache. A seconda dell’ambiente, la configurazione del server HTTPD Apache potrebbe essere simile a una delle seguenti:

>[!CAUTION]
>
>È necessario prestare attenzione quando si definisce il periodo di tempo durante il quale un oggetto viene considerato aggiornato. Dato che *nessun controllo fino alla scadenza del periodo di tempo specificato*, il client può finire per presentare contenuti obsoleti dalla cache.

1. **Per un’istanza Autore:**

   ```xml
   LoadModule expires_module modules/mod_expires.so
   <Location /libs>
     ExpiresByType text/css "access plus 1 month"
     ExpiresByType text/javascript "access plus 1 month"
     ExpiresByType image/png "access plus 1 month"
     ExpiresByType image/gif "access plus 1 month"
   </Location>
   ```

   Questo consente alla cache intermedia (ad esempio, la cache del browser) di memorizzare file CSS, JavaScript, PNG e GIF per un massimo di un mese, fino alla scadenza. Ciò significa che non devono essere richieste dall’AEM o dal server web, ma possono rimanere nella cache del browser.

   Le altre sezioni del sito non devono essere memorizzate nella cache in un’istanza Autore, in quanto sono soggette a modifiche in qualsiasi momento.

1. **Per un’istanza Publish:**

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

   Questo consente alla cache intermedia (ad esempio, la cache del browser) di memorizzare file CSS, JavaScript, PNG e GIF per un massimo di un giorno nelle cache client. Anche se questo esempio illustra le impostazioni globali per tutto ciò che segue `/content` e `/etc/designs`, dovresti renderlo più granulare.

   A seconda della frequenza con cui il sito viene aggiornato, puoi anche considerare la memorizzazione in cache delle pagine di HTML. Un periodo di tempo ragionevole è di un’ora:

   ```xml
   <Location /content>
     ExpiresByType text/html "access plus 1 hour"
   </Location>
   ```

Dopo aver configurato gli oggetti statici, eseguire la scansione `request.log`, durante la selezione delle pagine che contengono tali oggetti, per confermare che non vengono effettuate richieste (non necessarie) per gli oggetti statici.
