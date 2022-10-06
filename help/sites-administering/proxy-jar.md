---
title: Strumento Proxy Server (proxy.jar)
seo-title: Proxy Server Tool (proxy.jar)
description: Scopri lo strumento Proxy Server in AEM.
seo-description: Learn about the Proxy Server Tool in AEM.
uuid: 2fc1df24-8d5a-4be7-83fa-238ae65591b0
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: ca98dc3c-7056-4cdc-b4d3-23e471da5730
docset: aem65
exl-id: 3df50303-5cdd-4df0-abec-80831d2ccef7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1161'
ht-degree: 0%

---

# Strumento Proxy Server (proxy.jar){#proxy-server-tool-proxy-jar}

Il server proxy funge da server intermedio che inoltra le richieste tra un client e un server. Il server proxy tiene traccia di tutte le interazioni client-server e genera un registro dell&#39;intera comunicazione TCP. Questo consente di monitorare esattamente ciò che accade, senza dover accedere al server principale.

Puoi trovare il server proxy nella cartella di installazione appropriata:

* &lt;cq_install_path>/opt/helpers/proxy.jar
* &lt;crx_install_path>/opt/helpers/proxy.jar

È possibile utilizzare il server proxy per monitorare tutte le interazioni client-server, indipendentemente dal protocollo di comunicazione sottostante. Ad esempio, puoi monitorare i seguenti protocolli:

* HTTP per pagine web
* HTTPS per pagine web sicure
* SMTP per i messaggi e-mail
* LDAP per la gestione degli utenti

Ad esempio, è possibile posizionare il server proxy tra due applicazioni che comunicano tramite una rete TCP/IP; Ad esempio, un browser web e AEM. Questo ti consente di monitorare esattamente ciò che accade quando richiedi una pagina AEM.

## Avvio dello strumento Proxy Server {#starting-the-proxy-server-tool}

Lo strumento si trova nella cartella /opt/helpers dell&#39;installazione AEM. Per iniziare, digitare:

```xml
java -jar proxy.jar <host> <remoteport> <localport> [options]
```

### Opzioni {#options}

* **q (modalità silenziosa)** Non scrive le richieste nella finestra della console. Utilizzalo se non desideri rallentare la connessione o se registri l&#39;output in un file (vedi opzione -logfile ).
* **b (modalità binaria)** Se cerchi combinazioni di byte specifiche nel traffico, abilita la modalità binaria. L&#39;output conterrà quindi l&#39;output esadecimale e di caratteri.
* **t (voci del registro delle marche temporali)** Aggiunge una marca temporale a ogni output di log. La marca temporale è in secondi, pertanto potrebbe non essere adatta per il controllo di singole richieste. Utilizzalo per individuare gli eventi che si sono verificati in un momento specifico se utilizzi il server proxy per un periodo di tempo più lungo.
* **file di registro &lt;filename> (scrivi nel file di registro)** Scrive la conversazione client-server in un file di registro. Questo parametro funziona anche in modalità silenziosa.
* **i &lt;numindentions> (aggiungere un rientro)** Ogni connessione attiva presenta un rientro per una migliore leggibilità. Il valore predefinito è 16 livelli. (Novità della versione 1.16 di proxy.jar).

## Utilizzo dello strumento Server proxy {#uses-of-the-proxy-server-tool}

Gli scenari seguenti illustrano alcuni degli scopi per cui è possibile utilizzare lo strumento Proxy Server:

**Verifica la presenza di cookie e dei relativi valori**

L&#39;esempio seguente della voce di registro mostra tutti i cookie e i relativi valori inviati dal client sulla 6a connessione aperta dall&#39;avvio del proxy:

```xml
C-6-#000635 -> [Cookie: cq3session=7e39bc51-ac72-3f48-88a9-ed80dbac0693; Show=ShowMode; JSESSIONID=68d78874-cabf-9444-84a4-538d43f5064d ]
```

**Verifica delle intestazioni e dei relativi valori** L’esempio seguente mostra che il server è in grado di effettuare una connessione keep-alive e che l’intestazione della lunghezza del contenuto è stata impostata correttamente:

```xml
S-7-#000017 -> [Connection: Keep-Alive ]
...
S-7-#000107 -> [Content-Length: 124 ]
```

**Verifica del funzionamento di Keep Alive**

**Mantieni vivo** significa che un client riutilizza la connessione al server per il trasporto di più file (codice pagina, immagini, fogli di stile e così via). Senza mantenere in vita, il cliente deve stabilire una nuova connessione per ogni richiesta.

Per verificare se keep-alive funziona:

1. Avvia il server proxy.
1. Richiedi una pagina.

* Se keep-alive funziona, il contatore di connessione non deve mai superare 5-10 connessioni.
* Se keep-alive non funziona, il contatore di connessione aumenta rapidamente.

**Ricerca di richieste perse**

Se perdi le richieste in un&#39;impostazione server complessa, ad esempio con un firewall e un dispatcher, puoi utilizzare il server proxy per scoprire dove la richiesta è stata persa. In caso di firewall:

1. Avviare un proxy prima di un firewall
1. Avvia un altro proxy dopo un firewall
1. Utilizza questi per vedere quanto tempo arrivano le richieste.

**Gestione delle richieste**

Se si verificano richieste appese di tanto in tanto:

1. Avvia un proxy.jar.
1. Attendi o scrivi il registro di accesso in un file , con ogni voce con una marca temporale.
1. Quando la richiesta inizia ad essere sospesa, puoi vedere quante connessioni erano aperte e quale richiesta causa problemi.

## Formato dei messaggi di log {#the-format-of-log-messages}

Le voci di registro prodotte da proxy.jar hanno tutti il seguente formato:

```xml
[timestamp (optional)] [<b>C</b>lient|<b>S</b>erver]-[ConnectionNumber]-[BytePosition] ->[Character Stream]
```

Ad esempio, una richiesta per una pagina Web potrebbe avere il seguente aspetto:

```xml
C-0-#000000 -> [GET /author/prox.html?CFC_cK=1102938422341 HTTP/1.1 ]
```

* C indica che questa voce proviene dal client (è una richiesta per una pagina Web)
* 0 è il numero di connessione (il contatore di connessione inizia da 0)
* # 00000 l&#39;offset nel flusso di byte. Questa è la prima voce, quindi l&#39;offset è 0.
* [GET &lt;?>] è il contenuto della richiesta, nell’esempio di una delle intestazioni HTTP (url).

Quando una connessione viene chiusa, vengono registrate le seguenti informazioni:

```xml
C-6-Finished: 758 bytes (1.0 kb/s)
S-6-Finished: 665 bytes (1.0 kb/s)
```

Mostra il numero di byte passati tra client e server alla 6a connessione e alla velocità media.

## Esempio di output di log {#an-example-of-log-output}

Rivediamo un semplice modello che produce il seguente codice quando richiesto:

```xml
<html>
  <head>
    <title>Welcome</title>
  </head>
  <body>
    Welcome to Playground<br>
    <img src="/logo.gif">
  </body>
</html>
```

Se AEM è in esecuzione su localhost:4303, avvia il server proxy come segue:

```xml
java -jar proxy.jar localhost 4303 4444 -logfile test.log
```

Puoi accedere al server (`localhost:4303`) senza il server proxy, ma se si accede tramite `localhost:4444`, il server proxy registra la comunicazione. Apri un browser e accedi a una pagina creata con il modello precedente. Dopo di che, guarda il file di log.

>[!NOTE]
>
>Fino alla versione 1.14 di proxy.jar, le voci di registro di una connessione non vengono sincronizzate, il che significa che le voci di registro di una connessione client/server non sono necessarie nell&#39;ordine sequenziale corretto. Le versioni più recenti (>=1.14) del server proxy non hanno questo problema.

All&#39;avvio, le seguenti informazioni vengono scritte nel registro:

```xml
starting proxy for localhost:4303 on port 4444
using logfile: C:\CQUnify355default\opt\helpers\test.log
```

I seguenti campi di intestazione sono elencati all’inizio della prima connessione (0), che richiede la pagina principale di HTML:

```xml
C-0-#000000 -> [GET /author/prox.html?CFC_cK=1102936796533 HTTP/1.1 ]
C-0-#000053 -> [Accept: image/gif, image/x-xbitmap, image/jpeg, image/pjpeg, application/vnd.ms-powerpoint, application/vnd.ms-excel, application/msword, appl]
C-0-#000194 -> [ication/x-shockwave-flash, */* ]
C-0-#000227 -> [Accept-Language: de-ch ]
C-0-#000251 -> [Accept-Encoding: gzip, deflate ]
C-0-#000283 -> [User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.0) ]
C-0-#000347 -> [Host: localhost:4444 ]
```

Il client richiede una connessione keep-alive, in modo che il server possa inviare più file tramite la stessa connessione:

```xml
C-0-#000369 -> [Connection: Keep-Alive ]
```

Il server proxy è uno strumento utile per verificare se i cookie sono impostati correttamente o meno. Qui vediamo:

* cookie cq3session generato da AEM
* il cookie di commutazione della modalità show generato dal CFC
* un cookie denominato JSESSIONID; questo viene creato automaticamente da JSP se non è esplicitamente disattivato utilizzando &lt;%@ page session=&quot;false&quot; %>:

```xml
C-0-#000393 -> [Cookie: Show=ShowMode; cq3session=3bce15cf-1575-1b4e-8ea6-0d1a0c64738e; JSESSIONID=4161a56b-f193-d748-88a5-e09c5ff7ef2a ]
C-0-#000514 -> [ ]
S-0-#000000 -> [HTTP/1.0 200 OK ]
```

Il server chiuderà la connessione 0 dopo la richiesta. Mantenere in vita non è possibile, perché la richiesta ha un punto interrogativo. Questo significa che il server non può restituire una versione cache e quindi non può determinare la lunghezza del contenuto a questo punto, che è necessaria per una connessione keep-alive.

```xml
S-0-#000017 -> [Connection: Close ]
S-0-#000036 -> [Server: Communique Servlet Engine/3.5.5 ]
S-0-#000077 -> [Content-Type: text/html;charset=iso-8859-1 ]
S-0-#000121 -> [Date: Tue, 14 Dec 2004 09:46:44 GMT ]
S-0-#000158 -> [Set-Cookie: JSESSIONID=4161a56b-f193-d8-88a5-e09c5ff7ef2a;Path=/author ]
S-0-#000232 -> [ ]
```

In questo caso, il server inizia a inviare il codice HTML alla connessione 0:

```xml
S-0-#000234 -> [<html> ]
S-0-#000242 -> [.<head> ]
S-0-#000251 -> [..<title>Welcome</title> ]
S-0-#000277 -> [.</head> ]
S-0-#000287 -> [.<body> ]
S-0-#000296 -> [..Welcome to Playground<br> ]
S-0-#000325 -> [..<img src="/author/logo.gif"> ]
S-0-#000357 -> [.</body> ]
S-0-#000367 -> [</html>]
```

La connessione 0 viene chiusa immediatamente dopo la distribuzione del file HTML:

```xml
C-0-Finished: 516 bytes (0.0 kb/s)
S-0-Finished: 374 bytes (0.0 kb/s)
```

Ora, l&#39;output inizia per la connessione 1, che scarica l&#39;immagine contenuta nel codice HTML:

```xml
C-1-#000000 -> [GET /author/logo.gif HTTP/1.1 ]
C-1-#000031 -> [Accept: */* ]
C-1-#000044 -> [Referer: http://localhost:4444/author/prox.html?CFC_cK=1102936796533 ]
C-1-#000114 -> [Accept-Language: de-ch ]
C-1-#000138 -> [Accept-Encoding: gzip, deflate ]
C-1-#000170 -> [User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.0) ]
C-1-#000234 -> [Host: localhost:4444 ]
```

Anche in questo caso, il client richiede una connessione keep-alive:

```xml
C-1-#000256 -> [Connection: Keep-Alive ]
C-1-#000280 -> [Cookie: Show=ShowMode; cq3session=3bce15cf-1575-1b4e-8ea6-0d1a0c64738e; JSESSIONID=4161a56b-f193-d748-88a5-e09c5ff7ef2a ]
C-1-#000401 -> [ ]
S-1-#000000 -> [HTTP/1.0 200 OK ]
```

Per la connessione 1, il server può fornire keep-alive, perché l&#39;immagine è statica e quindi la lunghezza del contenuto è nota.

```xml
S-1-#000017 -> [Connection: Keep-Alive ]
S-1-#000041 -> [Server: Communique Servlet Engine/3.5.5 ]
S-1-#000082 -> [Content-Type: image/gif ]
```

Il server restituisce la lunghezza del contenuto dell&#39;immagine alla connessione 1:

```xml
S-1-#000107 -> [Content-Length: 124 ]
S-1-#000128 -> [Date: Tue, 14 Dec 2004 09:46:44 GMT ]
S-1-#000165 -> [ ]
```

Una volta stabilita la lunghezza del contenuto, il server invia i dati immagine alla connessione 1:

```xml
S-1-#000167 -> [GIF87a..........................,.......
...I....0.A..8......YDA.W...1..`i.`..6...Z...$@.F..)`..f..A.....iu.........$..;]
```

Una volta raggiunto il timeout di conservazione, la connessione 1 si chiude anche:

```xml
S-1-Finished: 291 bytes (0.0 kb/s)
C-1-Finished: 403 bytes (0.0 kb/s)
```

L&#39;esempio precedente è relativamente semplice, perché le due connessioni si verificano in sequenza:

* prima il server restituisce il codice HTML
* il browser richiede l’immagine e apre una nuova connessione

In pratica, una pagina può generare molte richieste parallele per immagini, fogli di stile, file JavaScript, ecc. Ciò significa che i registri hanno voci sovrapposte di connessioni aperte parallele. In tal caso, si consiglia di utilizzare l’opzione -i per migliorare la leggibilità.
