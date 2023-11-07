---
title: Strumento Server proxy (proxy.jar)
description: Scopri lo strumento Server proxy (proxy.jar) in Adobe Experience Manager.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: 3df50303-5cdd-4df0-abec-80831d2ccef7
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 0%

---

# Strumento Server proxy (proxy.jar){#proxy-server-tool-proxy-jar}

Il server proxy funge da server intermedio che inoltra le richieste tra un client e un server. Il server proxy tiene traccia di tutte le interazioni client-server e genera un registro dell&#39;intera comunicazione TCP. Questo consente di monitorare esattamente ciò che sta accadendo, senza dover accedere al server principale.

Il server proxy si trova nella cartella di installazione appropriata:

* &lt;cq_install_path>/opt/helpers/proxy.jar
* &lt;crx_install_path>/opt/helpers/proxy.jar

È possibile utilizzare il server proxy per monitorare tutte le interazioni client-server, indipendentemente dal protocollo di comunicazione sottostante. Ad esempio, puoi monitorare i seguenti protocolli:

* HTTP per pagine Web
* HTTPS per pagine Web protette
* SMTP per i messaggi e-mail
* LDAP per la gestione degli utenti

Ad esempio, è possibile posizionare il server proxy tra due applicazioni che comunicano tramite una rete TCP/IP, ad esempio un browser Web e l&#39;AEM. Questo consente di monitorare esattamente cosa accade quando si richiede una pagina AEM.

## Avvio dello strumento Server proxy {#starting-the-proxy-server-tool}

Lo strumento si trova nella cartella /opt/helpers dell’installazione dell’AEM. Per avviarlo, digita:

```xml
java -jar proxy.jar <host> <remoteport> <localport> [options]
```

### Opzioni {#options}

* **q (modalità non interattiva)** Non scrive le richieste nella finestra della console. Utilizzare questa opzione se non si desidera rallentare la connessione o se si registra l&#39;output in un file (vedere l&#39;opzione -logfile ).
* **b (modalità binaria)** Se stai cercando combinazioni di byte specifiche nel traffico, abilita la modalità binaria. L’output contiene l’output esadecimale e dei caratteri.
* **t (voci di registro timestamp)** Aggiunge una marca temporale a ciascun output del registro. La marca temporale è in secondi, pertanto potrebbe non essere adatta per il controllo di singole richieste. Utilizzalo per individuare gli eventi che si sono verificati in un momento specifico se utilizzi il server proxy per un periodo di tempo più lungo.
* **logfile &lt;filename> (scrittura su file di log)** Scrive la conversazione client-server in un file di log. Questo parametro funziona anche in modalità silenziosa.
* **i &lt;numindentions> (aggiungi rientro)** Per una migliore leggibilità, a ogni connessione attiva viene applicato un rientro. Il valore predefinito è 16 livelli. (Novità della versione 1.16 di proxy.jar).

## Utilizzo dello strumento Server proxy {#uses-of-the-proxy-server-tool}

Gli scenari seguenti illustrano alcuni degli scopi per i quali è possibile utilizzare lo strumento Proxy Server:

**Verifica la presenza di cookie e relativi valori**

L’esempio di voce di registro seguente mostra tutti i cookie e i relativi valori inviati dal client alla sesta connessione aperta dall’avvio del proxy:

```xml
C-6-#000635 -> [Cookie: cq3session=7e39bc51-ac72-3f48-88a9-ed80dbac0693; Show=ShowMode; JSESSIONID=68d78874-cabf-9444-84a4-538d43f5064d ]
```

**Verifica delle intestazioni e dei relativi valori** L&#39;esempio di voce di registro seguente mostra che il server è in grado di creare una connessione keep-alive e che l&#39;intestazione della lunghezza del contenuto è stata impostata correttamente:

```xml
S-7-#000017 -> [Connection: Keep-Alive ]
...
S-7-#000107 -> [Content-Length: 124 ]
```

**Verifica del funzionamento di Keep-Alive**

**Keep-Alive** indica che un client riutilizza la connessione al server per trasportare più file (codice della pagina, immagini, fogli di stile e così via). Senza keep-alive, il client deve stabilire una nuova connessione per ogni richiesta.

Per verificare se keep-alive funziona:

1. Avviare il server proxy.
1. Richiedi una pagina.

* Se keep-alive funziona, il contatore di connessione non deve mai superare le 5-10 connessioni.
* Se keep-alive non funziona, il contatore di connessione aumenta rapidamente.

**Ricerca di richieste perse**

Se perdi le richieste in un’impostazione server complessa, ad esempio con un firewall e un Dispatcher, puoi utilizzare il server proxy per scoprire dove è stata persa la richiesta. Se è presente un firewall:

1. Avviare un proxy prima di un firewall
1. Avvia un altro proxy dopo un firewall
1. Utilizza questi per vedere a che punto si trovano le richieste.

**Richieste bloccate**

Se si verificano di tanto in tanto richieste in sospeso:

1. Avvia un proxy.jar.
1. Attendere o scrivere il log degli accessi in un file, con ogni voce con una marca temporale.
1. Quando la richiesta inizia a bloccarsi, puoi vedere quante connessioni erano aperte e quale richiesta sta causando problemi.

## Formato dei messaggi di registro {#the-format-of-log-messages}

Le voci di registro prodotte da proxy.jar hanno tutte il seguente formato:

```xml
[timestamp (optional)] [<b>C</b>lient|<b>S</b>erver]-[ConnectionNumber]-[BytePosition] ->[Character Stream]
```

Ad esempio, una richiesta per una pagina Web può avere il seguente aspetto:

```xml
C-0-#000000 -> [GET /author/prox.html?CFC_cK=1102938422341 HTTP/1.1 ]
```

* C significa che questa voce proviene dal client (si tratta di una richiesta per una pagina Web)
* 0 è il numero di connessione (il contatore di connessione inizia da 0)
* #00000 l&#39;offset nel flusso di byte. Questa è la prima voce, quindi l&#39;offset è 0.
* [GET &lt;?>] è il contenuto della richiesta, nell’esempio una delle intestazioni HTTP (url).

Quando una connessione viene chiusa, vengono registrate le seguenti informazioni:

```xml
C-6-Finished: 758 bytes (1.0 kb/s)
S-6-Finished: 665 bytes (1.0 kb/s)
```

Mostra il numero di byte passati tra client e server alla sesta connessione e alla velocità media.

## Esempio di output del registro {#an-example-of-log-output}

Rivedi un modello semplice che, se richiesto, genera il seguente codice:

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

Se l&#39;AEM è in esecuzione su localhost:4303, avviare il server proxy come indicato di seguito:

```xml
java -jar proxy.jar localhost 4303 4444 -logfile test.log
```

È possibile accedere al server (`localhost:4303`) senza il server proxy, ma se vi accedi tramite `localhost:4444`, il server proxy registra la comunicazione. Apri un browser e accedi a una pagina creata con il modello precedente. In seguito, controlla il file di registro.

>[!NOTE]
>
>Fino alla versione 1.14 di proxy.jar, le voci di registro di una connessione non sono sincronizzate, il che significa che le voci di registro di una connessione client/server non sono necessarie nell&#39;ordine sequenziale corretto. Questo problema non si verifica nelle versioni più recenti (>=1.14) del server proxy.

All’avvio, nel registro vengono scritte le seguenti informazioni:

```xml
starting proxy for localhost:4303 on port 4444
using logfile: C:\CQUnify355default\opt\helpers\test.log
```

I seguenti campi di intestazione sono elencati all’inizio della prima connessione (0), che richiede la pagina HTML principale:

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

Il server proxy è uno strumento utile per verificare se i cookie sono impostati correttamente o meno. Qui puoi vedere quanto segue:

* Cookie cq3session generato da AEM
* il cookie del commutatore della modalità di visualizzazione generato dal CFC
* un cookie denominato JSESSIONID; viene creato automaticamente da JSP se non viene disattivato esplicitamente utilizzando &lt;%@ page session=&quot;false&quot; %>:

```xml
C-0-#000393 -> [Cookie: Show=ShowMode; cq3session=3bce15cf-1575-1b4e-8ea6-0d1a0c64738e; JSESSIONID=4161a56b-f193-d748-88a5-e09c5ff7ef2a ]
C-0-#000514 -> [ ]
S-0-#000000 -> [HTTP/1.0 200 OK ]
```

Il server chiuderà la connessione 0 dopo la richiesta. Keep-alive non è possibile perché la richiesta ha un punto interrogativo. Ciò significa che il server non può restituire una versione memorizzata nella cache e pertanto non può determinare la lunghezza del contenuto a questo punto, necessaria per una connessione keep-alive.

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

La connessione 0 si chiude immediatamente dopo che il file HTML è stato distribuito:

```xml
C-0-Finished: 516 bytes (0.0 kb/s)
S-0-Finished: 374 bytes (0.0 kb/s)
```

Ora l’output inizia per la connessione 1, che scarica l’immagine contenuta nel codice HTML:

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

Per la connessione 1, il server può fornire keep-alive, perché l&#39;immagine è statica e pertanto è nota la lunghezza del contenuto.

```xml
S-1-#000017 -> [Connection: Keep-Alive ]
S-1-#000041 -> [Server: Communique Servlet Engine/3.5.5 ]
S-1-#000082 -> [Content-Type: image/gif ]
```

Il server restituisce la lunghezza del contenuto dell&#39;immagine nella connessione 1:

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

Una volta raggiunto il timeout keep-alive, si chiude anche la connessione 1:

```xml
S-1-Finished: 291 bytes (0.0 kb/s)
C-1-Finished: 403 bytes (0.0 kb/s)
```

L’esempio precedente è relativamente semplice, perché le due connessioni si verificano in sequenza:

* in primo luogo, il server restituisce il codice HTML
* quindi il browser richiede l’immagine e apre una nuova connessione

In pratica, una pagina può generare molte richieste parallele per immagini, fogli di stile, file JavaScript e così via. Ciò significa che i registri presentano voci sovrapposte di connessioni aperte parallele. In tal caso, l’Adobe consiglia di utilizzare l’opzione -i per migliorare la leggibilità.
