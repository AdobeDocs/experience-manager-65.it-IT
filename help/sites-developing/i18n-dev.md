---
title: Internazionalizzazione delle stringhe di interfaccia
seo-title: Internazionalizzazione delle stringhe di interfaccia
description: Le API Java e Javascript consentono di internazionalizzare le stringhe
seo-description: Le API Java e Javascript consentono di internazionalizzare le stringhe
uuid: 1cfa409f-9b1e-466f-8b03-5628db42bc57
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: 9da8823c-13a4-4244-bfab-a910a4fd44e7
translation-type: tm+mt
source-git-commit: b3e1493811176271ead54bae55b1cd0cf759fe71

---


# Internazionalizzazione delle stringhe di interfaccia {#internationalizing-ui-strings}

Le API Java e Javascript consentono di internazionalizzare le stringhe nei seguenti tipi di risorse:

* File Java sorgente.
* Script JSP.
* Javascript nelle librerie lato client o nell&#39;origine pagina.
* Valori delle proprietà del nodo JCR utilizzati nelle finestre di dialogo e nelle proprietà di configurazione del componente.

Per una panoramica del processo di internazionalizzazione e localizzazione, consulta [Internazionalizzazione dei componenti](/help/sites-developing/i18n.md).

## Internazionalizzazione delle stringhe in Java e codice JSP {#internationalizing-strings-in-java-and-jsp-code}

Il pacchetto `com.day.cq.i18n` Java consente di visualizzare stringhe localizzate nell’interfaccia utente. La `I18n` classe fornisce il `get` metodo che recupera le stringhe localizzate dal dizionario AEM. L&#39;unico parametro richiesto del `get` metodo è il valore letterale di stringa nella lingua inglese. L’inglese è la lingua predefinita per l’interfaccia utente. L&#39;esempio seguente localizza la parola `Search`:

`i18n.get("Search");`

L&#39;identificazione della stringa nella lingua inglese è diversa dai tipici framework di internazionalizzazione in cui un ID identifica una stringa e viene utilizzato per fare riferimento alla stringa in fase di esecuzione. L&#39;utilizzo del valore letterale di stringa inglese offre i seguenti vantaggi:

* Il codice è facile da capire.
* La stringa nella lingua predefinita è sempre disponibile.

### Determinazione della lingua dell&#39;utente {#determining-the-user-s-language}

Esistono due modi per determinare la lingua preferita dall&#39;utente:

* Per gli utenti autenticati, stabilite la lingua dalle preferenze nell&#39;account utente.
* Le impostazioni internazionali della pagina richiesta.

La proprietà language dell&#39;account utente è il metodo preferito perché è più affidabile. Tuttavia, l&#39;utente deve aver eseguito l&#39;accesso per utilizzare questo metodo.

#### Creazione dell&#39;oggetto Java I18n {#creating-the-i-n-java-object}

La classe I18n fornisce due costruttori. Il modo in cui viene determinato il linguaggio preferito dall&#39;utente determina il costruttore da utilizzare.

Per presentare la stringa nella lingua specificata nell&#39;account utente, utilizzate il seguente costruttore (dopo l&#39;importazione `com.day.cq.i18n.I18n)`:

```java
I18n i18n = new I18n(slingRequest);
```

Il costruttore utilizza il metodo `SlingHTTPRequest` per recuperare l&#39;impostazione della lingua dell&#39;utente.

Per utilizzare le impostazioni internazionali della pagina per determinare la lingua, è innanzitutto necessario ottenere ResourceBundle per la lingua della pagina richiesta:

```java
Locale pageLang = currentPage.getLanguage(false);
ResourceBundle resourceBundle = slingRequest.getResourceBundle(pageLang);
I18n i18n = new I18n(resourceBundle);
```

#### Internazionalizzazione di una stringa {#internationalizing-a-string}

Utilizzare il `get` metodo dell&#39; `I18n` oggetto per internazionalizzare una stringa. L&#39;unico parametro richiesto del `get` metodo è la stringa da internazionalizzare. La stringa corrisponde a una stringa in un dizionario di traduttori. Il metodo get cerca la stringa nel dizionario e restituisce la traduzione per la lingua corrente.

Il primo argomento del `get` metodo deve essere conforme alle seguenti regole:

* Il valore deve essere una stringa letterale. Variabile di tipo `String` non accettabile.
* La stringa letterale deve essere espressa su una sola riga.
* La stringa fa distinzione tra maiuscole e minuscole.

```xml
i18n.get("Enter a search keyword");
```

#### Utilizzo dei suggerimenti di traduzione {#using-translation-hints}

Specificare il [suggerimento](/help/sites-developing/i18n-translator.md#adding-changing-and-removing-strings) di traduzione della stringa internazionalizzata per distinguere tra stringhe duplicate nel dizionario. Utilizzate il secondo parametro opzionale del `get` metodo per fornire il suggerimento di conversione. Il suggerimento di traduzione deve corrispondere esattamente alla proprietà Commento dell&#39;elemento nel dizionario.

Ad esempio, il dizionario contiene la stringa `Request` due volte: una volta come verbo e una come sostantivo. Il codice seguente include il suggerimento di conversione come argomento nel `get` metodo:

```java
i18n.get("Request","A noun, as in a request for a web page");
```

#### Inclusione di variabili nelle frasi localizzate {#including-variables-in-localized-sentences}

Includi variabili nella stringa localizzata per creare un significato contestuale in una frase. Ad esempio, dopo aver effettuato l&#39;accesso a un&#39;applicazione Web, nella home page viene visualizzato il messaggio &quot;Benvenuti all&#39;amministratore. Hai 2 messaggi nella tua inbox.&quot; Il contesto della pagina determina il nome utente e il numero di messaggi.

[Nel dizionario](/help/sites-developing/i18n-translator.md#adding-changing-and-removing-strings), le variabili sono rappresentate in stringhe come indici tra parentesi. Specificare i valori delle variabili come argomenti del `get` metodo. Gli argomenti vengono inseriti dopo il suggerimento di traduzione e gli indici corrispondono all&#39;ordine degli argomenti:

```xml
i18n.get("Welcome back {0}. You have {1} messages.", "user name, number of messages", user.getDisplayName(), numItems);
```

La stringa internazionalizzata e il suggerimento di traduzione devono corrispondere esattamente alla stringa e al commento nel dizionario. Potete omettere il suggerimento di localizzazione fornendo un `null` valore come secondo argomento.

#### Utilizzo del metodo Get statico {#using-the-static-get-method}

La `I18N` classe definisce un `get` metodo statico che è utile quando è necessario localizzare un numero limitato di stringhe. Oltre ai parametri del `get` metodo di un oggetto, il metodo statico richiede l&#39; `SlingHttpRequest` oggetto o l&#39; `ResourceBundle` oggetto utilizzato, a seconda di come si determina la lingua preferita dell&#39;utente:

* Utilizzate le preferenze della lingua dell&#39;utente: Fornite SlingHttpRequest come primo parametro.

   `I18n.get(slingHttpRequest, "Welcome back {}. You have {} messages.", "user name, number of messages", user.getDisplayName(), numItems);`
* Utilizzate la lingua della pagina: Fornisci ResourceBundle come primo parametro.

   `I18n.get(resourceBundle,"Welcome back {}. You have {} messages.", "user name, number of messages", user.getDisplayName(), numItems);`

### Internazionalizzazione delle stringhe nel codice JavaScript {#internationalizing-strings-in-javascript-code}

L&#39;API Javascript consente di localizzare le stringhe sul client. Come per il codice [Java e JSP](#internationalizing-strings-in-java-and-jsp-code) , l&#39;API Javascript consente di identificare le stringhe da localizzare, fornire suggerimenti per la localizzazione e includere variabili nelle stringhe localizzate.

La cartella `granite.utils` della libreria [](/help/sites-developing/clientlibs.md) client fornisce l&#39;API Javascript. Per utilizzare l&#39;API, includete questa cartella libreria client nella pagina. Le funzioni di localizzazione utilizzano lo `Granite.I18n` spazio dei nomi.

Prima di presentare stringhe localizzate, è necessario impostare le impostazioni internazionali utilizzando la `Granite.I18n.setLocale` funzione. La funzione richiede il codice della lingua dell&#39;impostazione internazionale come argomento:

```
Granite.I18n.setLocale("fr");
```

Per presentare una stringa localizzata, utilizzare la `Granite.I18n.get` funzione:

```
Granite.I18n.get("string to localize");
```

L&#39;esempio seguente internazionalizza la stringa &quot;Welcome back&quot;:

```
Granite.I18n.setLocale("fr");
Granite.I18n.get("string to localize", [variables], "localization hint");
```

I parametri della funzione sono diversi dal metodo Java I18n.get:

* Il primo parametro è il valore letterale di stringa da localizzare.
* Il secondo parametro è una matrice di valori da inserire nella stringa letterale.
* Il terzo parametro è il suggerimento di localizzazione.

Nell&#39;esempio seguente viene utilizzato Javascript per localizzare &quot;Welcome back Administrator&quot;. Hai 2 messaggi nella tua inbox.&quot; frase:

```
Granite.I18n.setLocale("fr");
Granite.I18n.get("Welcome back {0}. You have {1} new messages in your inbox.", [username, numMsg], "user name, number of messages");
```

### Internazionalizzazione di stringhe dai nodi JCR {#internationalizing-strings-from-jcr-nodes}

Le stringhe dell&#39;interfaccia utente si basano spesso sulle proprietà dei nodi JCR. Ad esempio, la `jcr:title` proprietà di una pagina viene in genere utilizzata come contenuto dell&#39; `h1` elemento nel codice della pagina. La `I18n` classe fornisce il `getVar` metodo di localizzazione di queste stringhe.

Lo script JSP di esempio seguente recupera la `jcr:title` proprietà dall&#39;archivio e visualizza la stringa localizzata sulla pagina:

```java
<% title = properties.get("jcr:title", String.class);%>
<h1><%=i18n.getVar(title) %></h1>
```

#### Specifica dei suggerimenti di traduzione per i nodi JCR {#specifying-translation-hints-for-jcr-nodes}

Simili ai suggerimenti di [traduzione nell&#39;API](#using-translation-hints)Java, potete fornire suggerimenti di traduzione per distinguere le stringhe duplicate nel dizionario. Fornire il suggerimento di conversione come proprietà del nodo che contiene la proprietà internazionalizzata. Il nome della proprietà hint è composto dal nome della proprietà internazionalizzata con il `_commentI18n` suffisso:

`${prop}_commentI18n`

Ad esempio, un `cq:page` nodo include la proprietà jcr:title localizzata. L&#39;hint viene fornito come valore della proprietà denominata jcr:title_commentI18n.

### Verifica della copertura dell&#39;internazionalizzazione {#testing-internationalization-coverage}

Verificare se sono state internazionalizzate tutte le stringhe nell’interfaccia utente. Per vedere quali stringhe sono coperte, impostate la lingua utente su zz_ZZ e aprite l’interfaccia nel browser Web. Le stringhe internazionalizzate vengono visualizzate con una traduzione stub nel seguente formato:

`USR_*Default-String*_尠`

L’immagine seguente mostra la traduzione stub per la home page di AEM:

![chlimage_1](assets/chlimage_1a.jpeg)

Per impostare la lingua per l&#39;utente, configurate la proprietà della lingua del nodo delle preferenze per l&#39;account utente.

Il nodo delle preferenze di un utente ha un percorso simile al seguente:

`/home/users/<letter>/<hash>/preferences`

![chlimage_1-1](assets/chlimage_1-1a.jpeg)

