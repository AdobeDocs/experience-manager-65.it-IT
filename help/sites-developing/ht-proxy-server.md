---
title: Come utilizzare lo strumento Proxy Server
seo-title: Come utilizzare lo strumento Proxy Server
description: Il server proxy funge da server intermedio che invia le richieste tra un client e un server
seo-description: Il server proxy funge da server intermedio che invia le richieste tra un client e un server
uuid: 30f4f46d-839e-4d23-a511-12f29b3cc8aa
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: dfbc1d2f-80c1-4564-a01c-a5028b7257d7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 0%

---


# Come utilizzare lo strumento Proxy Server{#how-to-use-the-proxy-server-tool}

Il server proxy funge da server intermedio che invia le richieste tra un client e un server. Il server proxy tiene traccia di tutte le interazioni client-server e genera un registro dell&#39;intera comunicazione TCP. Questo consente di monitorare esattamente ciò che sta accadendo, senza dover accedere al server principale.

Il server proxy è disponibile nell&#39;installazione AEM:

`crx-quickstart/opt/helpers/proxy-2.1.jar`

È possibile utilizzare il server proxy per monitorare tutte le interazioni client-server, indipendentemente dal protocollo di comunicazione sottostante. Ad esempio, potete monitorare i protocolli seguenti:

* HTTP per pagine Web
* HTTPS per pagine Web sicure
* SMTP per i messaggi e-mail
* LDAP per la gestione degli utenti

Ad esempio, è possibile posizionare il server proxy tra due applicazioni che comunicano tramite una rete TCP/IP; ad esempio un browser Web e AEM. Questo consente di monitorare esattamente ciò che accade quando si richiede una pagina CQ.

## Avvio dello strumento Proxy Server {#starting-the-proxy-server-tool}

Avviate il server dalla riga di comando:

`java -jar proxy-2.1.jar <host> <remoteport> <localport> [options]`

**Parametri**

`<host>`

Questo è l&#39;indirizzo host dell&#39;istanza CRX a cui si desidera connettersi. Se l&#39;istanza si trova nel computer locale, sarà `localhost`.

`<remoteport>`

Si tratta della porta host dell&#39;istanza CRX di destinazione. Ad esempio, il valore predefinito di una nuova installazione AEM è **`4502`** e il valore predefinito per una nuova istanza di creazione AEM installata è `4502`.

`<localport>`

Si tratta della porta del computer locale alla quale si desidera connettersi per accedere all&#39;istanza CRX tramite il proxy.

**Opzioni**

`-q` (modalità silenziosa)

Non scrive l&#39;output nella finestra della console. Utilizzate questa opzione se non desiderate rallentare la connessione o se registrate l&#39;output in un file (consultate l&#39;opzione -logfile).

`-b`(modalità binaria)

Se state cercando combinazioni di byte specifiche nel traffico, abilitate la modalità binaria. L&#39;output conterrà quindi l&#39;output esadecimale e il carattere.

`-t` (voci del registro di marca temporale)

Aggiunge una marca temporale a ciascun output del registro. La marca temporale è espressa in secondi, pertanto potrebbe non essere adatta per il controllo di singole richieste. Utilizzatelo per individuare gli eventi che si sono verificati in un momento specifico se utilizzate il server proxy per un periodo di tempo più lungo.

`-logfile <filename>`(scrivi nel file di registro)

Scrive la conversazione client-server in un file di registro. Questo parametro funziona anche in modalità silenziosa.

**`-i <numIndentions>`**(aggiungere un rientro)

Ogni connessione attiva è rientrata per una migliore leggibilità. Il valore predefinito è 16 livelli. Questa funzione è stata introdotta con `proxy.jar version 1.16`.

### Formato registro {#log-format}

Le voci di registro prodotte da proxy-2.1.jar hanno tutti il seguente formato:

`[timestamp (optional)] [Client|Server]-[ConnectionNumber]-[BytePosition] ->[Character Stream]`

Ad esempio, una richiesta per una pagina Web può essere visualizzata come segue:

`C-0-#000000 -> [GET /author/prox.html?CFC_cK=1102938422341 HTTP/1.1 ]`

* C significa che questa voce proviene dal client (è una richiesta per una pagina Web)
* 0 è il numero di connessione (il contatore di connessione inizia da 0)
* # 00000 l&#39;offset nel flusso di byte. Questa è la prima voce, quindi l&#39;offset è 0.
* `[GET <?>]` è il contenuto della richiesta, nell’esempio di una delle intestazioni HTTP (url).

Quando una connessione viene chiusa, vengono registrate le informazioni seguenti:

```
C-6-Finished: 758 bytes (1.0 kb/s)
S-6-Finished: 665 bytes (1.0 kb/s)
```

Questo mostra il numero di byte passati tra client ( `C`) e server ( `S`) sulla 6a connessione e alla velocità media.

**Esempio di output di registro**

Ad esempio, prendete in considerazione una pagina che produce il seguente codice quando richiesto:

### Esempio {#example}

Ad esempio, considerate un semplice documento HTML che si trova nella directory archivio all&#39;indirizzo

`/content/test.html`

accanto a un file di immagine che si trova in

`/content/test.jpg`

Il contenuto di `test.html` è:

```xml
<html>
<head>
    <title>Test</title>
</head>
<body>
    Test<br>
    <img src="test.jpg">
</body>
</html>
```

Presupponendo che l&#39;istanza AEM sia in esecuzione su `localhost:4502`, avvieremo il proxy come segue:

`java -jar proxy.jar localhost 4502 4444 -logfile test.log`

Ora è possibile accedere all&#39;istanza CQ/CRX tramite il proxy su `localhost:4444` e tutte le comunicazioni tramite questa porta sono registrate su `test.log`.

Se ora guardiamo l&#39;output del proxy, vedremo l&#39;interazione tra il browser e l&#39;istanza AEM.

All&#39;avvio, il proxy emette quanto segue:

```xml
starting proxy for localhost:4502 on port 4444
using logfile: <some-dir>/crx-quickstart/opt/helpers/test.log
```

Quindi aprite un browser e accedete alla pagina di test:

`http://localhost:4444/content/test.html`

e il browser effettua una `GET` richiesta per la pagina:

```shell
C-0-#000000 -> [GET /content/test.html HTTP/1.1 ]
C-0-#000033 -> [Host: localhost:4444 ]
C-0-#000055 -> [Connection: keep-alive ]
C-0-#000079 -> [User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_4) AppleWebKit/536.11 (KHTML, like Gecko) Chrome/20.0.1132.57 Safari/536.11 ]
C-0-#000212 -> [Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8 ]
C-0-#000285 -> [Accept-Encoding: gzip,deflate,sdch ]
C-0-#000321 -> [Accept-Language: en-US,en;q=0.8 ]
C-0-#000354 -> [Accept-Charset: ISO-8859-1,utf-8;q=0.7,*;q=0.3 ]
C-0-#000402 -> [Cookie: login-token=179ba6bd-e0a7-4909-a965-e11c7f2bc2fc%3a618bd8a8-fbaf-43c5-827d-c84c62248c5e_22ee860cc9036fee%3acrx.default%3b21148fb0-eb6c]
C-0-#000543 -> [-43c9-a2b9-c8d40618d8ae%3ad87a3d1a-5e9a-4d5a-bab1-0ee60ad6d8df_d0e4ddce0fcd84b6%3acrx.default%3b5cb95227-ea51-47bf-850b-68ad1dfd7297%3af3bbb6]
C-0-#000684 -> [59-7913-4285-8857-832c087bafd5_c484727d3b3665ad%3acrx.default; ys-cq-siteadmin-tree=o%3Awidth%3Dn%253A240%5EselectedPath%3Ds%253A/content ]
C-0-#000824 -> [ ]
```

L&#39;istanza AEM risponde con il contenuto del file `test.html`:

```shell
S-0-#000000 -> [HTTP/1.1 200 OK ]
S-0-#000017 -> [Connection: Keep-Alive ]
S-0-#000041 -> [Server: Day-Servlet-Engine/4.1.24  ]
S-0-#000077 -> [Content-Type: text/html;charset=utf-8 ]
S-0-#000116 -> [Content-Length: 104 ]
S-0-#000137 -> [Date: Mon, 16 Jul 2012 11:23:38 GMT ]
S-0-#000174 -> [Last-Modified: Mon, 16 Jul 2012 11:19:27 GMT ]
S-0-#000220 -> [ ]
S-0-#000222 -> [<html>]
S-0-#000229 -> [<head>]
S-0-#000236 -> [    <title>Test</title>]
S-0-#000260 -> [</head> ]
S-0-#000269 -> [<body>]
S-0-#000276 -> [ Test<br>]
S-0-#000286 -> [    <img src="test.jpg">]
S-0-#000311 -> [</body>]
S-0-#000319 -> [</html>]
```

### Uso del server proxy {#uses-of-the-proxy-server}

Gli scenari seguenti illustrano alcuni degli scopi per i quali il server proxy può essere utilizzato:

**Verifica cookie e relativi valori**

L&#39;esempio seguente mostra tutti i cookie e i relativi valori inviati dal client sulla sesta connessione aperta dall&#39;avvio del proxy:

`C-6-#000635 -> [Cookie: cq3session=7e39bc51-ac72-3f48-88a9-ed80dbac0693; Show=ShowMode; JSESSIONID=68d78874-cabf-9444-84a4-538d43f5064d ]`

**Verifica delle intestazioni e dei relativi valori**

L’esempio di voce di registro seguente mostra che il server è in grado di creare una connessione keep-alive e che l’intestazione della lunghezza del contenuto è stata impostata correttamente:

```
S-7-#000017 -> [Connection: Keep-Alive ]
 ...
 S-7-#000107 -> [Content-Length: 124 ]
```

**Verifica del funzionamento di Keep-Alive**

Keep-alive è una funzione di HTTP che consente al client di riutilizzare la connessione TCP al server per effettuare più richieste (per il codice della pagina, immagini, fogli di stile e così via). Senza keep-alive, il client deve stabilire una nuova connessione per ogni richiesta.

Per verificare se keep-alive funziona:

* Avviate il server proxy.
* Richiedete una pagina.
* Se keep-alive funziona, il contatore di connessione non deve mai superare 5-10 connessioni.
* Se keep-alive non funziona, il contatore di connessione aumenta rapidamente.

**Ricerca di richieste perse**

Se si perdono richieste in un server complesso, ad esempio con un firewall e un dispatcher, è possibile utilizzare il server proxy per scoprire dove la richiesta è stata persa. In caso di firewall:

* Avviare un proxy prima di un firewall
* Avviare un altro proxy dopo un firewall
* Utilizzate questi elementi per vedere fino a che punto sono arrivate le richieste.

**Gestione richieste**

Se si verificano richieste sporgenti di tanto in tanto:

* Avviate il proxy.
* Attendi o scrivi il registro di accesso in un file con ciascuna voce con una marca temporale.
* Quando la richiesta inizia con l’appesa, potete vedere quante connessioni erano aperte e quale è la richiesta che causa problemi.

