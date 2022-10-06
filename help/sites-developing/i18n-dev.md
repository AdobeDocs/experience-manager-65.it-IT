---
title: Internazionalizzazione delle stringhe di interfaccia utente
seo-title: Internationalizing UI Strings
description: Le API Java e JavaScript consentono di internazionalizzare le stringhe
seo-description: Java and Javascript APIs enable you to internationalize strings
uuid: 1cfa409f-9b1e-466f-8b03-5628db42bc57
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: 9da8823c-13a4-4244-bfab-a910a4fd44e7
exl-id: bc5b1cb7-a011-42fe-8759-3c7ee3068aad
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1100'
ht-degree: 0%

---

# Internazionalizzazione delle stringhe di interfaccia utente {#internationalizing-ui-strings}

Le API Java e JavaScript consentono di internazionalizzare le stringhe nei seguenti tipi di risorse:

* File di origine Java.
* Script JSP.
* Javascript nelle librerie lato client o nell’origine della pagina.
* Valori delle proprietà dei nodi JCR utilizzati nelle finestre di dialogo e nelle proprietà di configurazione dei componenti.

Per una panoramica del processo di internazionalizzazione e localizzazione, vedi [Componenti di internazionalizzazione](/help/sites-developing/i18n.md).

## Internazionalizzazione delle stringhe nel codice Java e JSP {#internationalizing-strings-in-java-and-jsp-code}

La `com.day.cq.i18n` Il pacchetto Java consente di visualizzare stringhe localizzate nell’interfaccia utente. La `I18n` la classe fornisce `get` metodo che recupera stringhe localizzate dal dizionario AEM. L&#39;unico parametro richiesto del `get` metodo è la stringa letterale nella lingua inglese. L’inglese è la lingua predefinita per l’interfaccia utente. L&#39;esempio seguente localizza la parola `Search`:

`i18n.get("Search");`

L’identificazione della stringa in lingua inglese è diversa dai framework di internazionalizzazione tipici, in cui un ID identifica una stringa e viene utilizzato per fare riferimento alla stringa in fase di esecuzione. L&#39;utilizzo del valore letterale stringa inglese fornisce i seguenti vantaggi:

* Il codice è facile da capire.
* La stringa nella lingua predefinita è sempre disponibile.

### Determinazione della lingua dell’utente {#determining-the-user-s-language}

Esistono due modi per determinare la lingua preferita dall’utente:

* Per gli utenti autenticati, determina la lingua dalle preferenze nell&#39;account utente.
* Impostazioni internazionali della pagina richiesta.

La proprietà language dell&#39;account utente è il metodo preferito perché è più affidabile. Tuttavia, per utilizzare questo metodo, è necessario che l’utente abbia effettuato l’accesso.

#### Creazione dell’oggetto Java I18n {#creating-the-i-n-java-object}

La classe I18n fornisce due costruttori. La modalità di determinazione della lingua preferita dell&#39;utente determina il costruttore da utilizzare.

Per presentare la stringa nella lingua specificata nell&#39;account utente, utilizzare il seguente costruttore (dopo l&#39;importazione `com.day.cq.i18n.I18n)`:

```java
I18n i18n = new I18n(slingRequest);
```

Il costruttore utilizza il `SlingHTTPRequest` per recuperare l’impostazione della lingua dell’utente.

Per utilizzare le impostazioni internazionali della pagina per determinare la lingua, è innanzitutto necessario ottenere il ResourceBundle per la lingua della pagina richiesta:

```java
Locale pageLang = currentPage.getLanguage(false);
ResourceBundle resourceBundle = slingRequest.getResourceBundle(pageLang);
I18n i18n = new I18n(resourceBundle);
```

#### Internazionalizzazione di una stringa {#internationalizing-a-string}

Utilizza la `get` metodo `I18n` oggetto per internazionalizzare una stringa. L&#39;unico parametro richiesto del `get` metodo è la stringa da internazionalizzare. La stringa corrisponde a una stringa in un dizionario di traduzione. Il metodo get cerca la stringa nel dizionario e restituisce la traduzione per la lingua corrente.

Il primo argomento del `get` il metodo deve rispettare le seguenti regole:

* Il valore deve essere un valore letterale stringa. Variabile di tipo `String` non è accettabile.
* Il valore letterale stringa deve essere espresso su una singola riga.
* Nella stringa viene fatta distinzione tra maiuscole e minuscole.

```xml
i18n.get("Enter a search keyword");
```

#### Utilizzo dei suggerimenti di traduzione {#using-translation-hints}

Specifica la [suggerimento per la traduzione](/help/sites-developing/i18n-translator.md#adding-changing-and-removing-strings) della stringa internazionalizzata per distinguere tra stringhe duplicate nel dizionario. Utilizza il secondo parametro opzionale del `get` per fornire il suggerimento di traduzione. L&#39;hint di traduzione deve corrispondere esattamente alla proprietà Commento dell&#39;elemento nel dizionario.

Ad esempio, il dizionario contiene la stringa `Request` due volte: una volta come verbo e una come sostantivo. Il codice seguente include il suggerimento di traduzione come argomento nel `get` metodo:

```java
i18n.get("Request","A noun, as in a request for a web page");
```

#### Inclusione di variabili nelle frasi localizzate {#including-variables-in-localized-sentences}

Includi le variabili nella stringa localizzata per creare un significato contestuale in una frase. Ad esempio, dopo aver effettuato l&#39;accesso a un&#39;applicazione Web, nella home page viene visualizzato il messaggio &quot;Bentornato Amministratore. Hai 2 messaggi nella tua casella in entrata.&quot; Il contesto della pagina determina il nome utente e il numero di messaggi.

[Nel dizionario](/help/sites-developing/i18n-translator.md#adding-changing-and-removing-strings), le variabili sono rappresentate in stringhe come indici tra parentesi. Specifica i valori delle variabili come argomenti del `get` metodo . Gli argomenti vengono inseriti seguendo il suggerimento di traduzione e gli indici corrispondono all&#39;ordine degli argomenti:

```xml
i18n.get("Welcome back {0}. You have {1} messages.", "user name, number of messages", user.getDisplayName(), numItems);
```

La stringa internazionalizzata e il suggerimento di traduzione devono corrispondere esattamente alla stringa e al commento nel dizionario. Puoi omettere l’hint di localizzazione fornendo un `null` come secondo argomento.

#### Utilizzo del metodo Get statico {#using-the-static-get-method}

La `I18N` la classe definisce un `get` , utile quando è necessario localizzare un numero limitato di stringhe. Oltre ai parametri di un oggetto `get` il metodo static richiede `SlingHttpRequest` o `ResourceBundle` in base a come si determina la lingua preferita dell’utente:

* Utilizza le preferenze linguistiche dell’utente: Fornisci SlingHttpRequest come primo parametro.

   `I18n.get(slingHttpRequest, "Welcome back {}. You have {} messages.", "user name, number of messages", user.getDisplayName(), numItems);`
* Utilizza la lingua della pagina: Fornisci ResourceBundle come primo parametro.

   `I18n.get(resourceBundle,"Welcome back {}. You have {} messages.", "user name, number of messages", user.getDisplayName(), numItems);`

### Internazionalizzazione delle stringhe nel codice JavaScript {#internationalizing-strings-in-javascript-code}

L’API Javascript ti consente di localizzare le stringhe sul client. Come con [Java e JSP](#internationalizing-strings-in-java-and-jsp-code) L’API Javascript ti consente di identificare le stringhe da localizzare, fornire suggerimenti di localizzazione e includere variabili nelle stringhe localizzate.

La `granite.utils` [cartella libreria client](/help/sites-developing/clientlibs.md) fornisce l&#39;API Javascript. Per utilizzare l’API, includi questa cartella della libreria client sulla pagina. Le funzioni di localizzazione utilizzano `Granite.I18n` spazio dei nomi.

Prima di presentare stringhe localizzate, è necessario impostare le impostazioni internazionali utilizzando `Granite.I18n.setLocale` funzione . La funzione richiede il codice della lingua delle impostazioni internazionali come argomento:

```
Granite.I18n.setLocale("fr");
```

Per presentare una stringa localizzata, utilizza la variabile `Granite.I18n.get` funzione:

```
Granite.I18n.get("string to localize");
```

L’esempio seguente internazionalizza la stringa &quot;Bentornato&quot;:

```
Granite.I18n.setLocale("fr");
Granite.I18n.get("string to localize", [variables], "localization hint");
```

I parametri della funzione sono diversi dal metodo Java I18n.get :

* Il primo parametro è il valore letterale stringa da localizzare.
* Il secondo parametro è una matrice di valori da inserire nella stringa letterale.
* Il terzo parametro è il suggerimento di localizzazione.

Nell&#39;esempio seguente viene utilizzato Javascript per localizzare &quot;Bentornato Amministratore. Hai 2 messaggi nella tua casella in entrata.&quot; frase:

```
Granite.I18n.setLocale("fr");
Granite.I18n.get("Welcome back {0}. You have {1} new messages in your inbox.", [username, numMsg], "user name, number of messages");
```

### Internazionalizzazione di stringhe dai nodi JCR {#internationalizing-strings-from-jcr-nodes}

Le stringhe di interfaccia utente si basano spesso sulle proprietà dei nodi JCR. Ad esempio, il `jcr:title` di una pagina viene in genere utilizzata come contenuto `h1` nel codice della pagina. La `I18n` la classe fornisce `getVar` metodo per localizzare queste stringhe.

Il seguente script JSP di esempio recupera il `jcr:title` dall&#39;archivio e visualizza la stringa localizzata sulla pagina:

```java
<% title = properties.get("jcr:title", String.class);%>
<h1><%=i18n.getVar(title) %></h1>
```

#### Specifica dei suggerimenti di traduzione per i nodi JCR {#specifying-translation-hints-for-jcr-nodes}

Simile a [suggerimenti di traduzione nell’API Java](#using-translation-hints), è possibile fornire suggerimenti di traduzione per distinguere le stringhe duplicate nel dizionario. Fornisci il suggerimento di traduzione come proprietà del nodo che contiene la proprietà internazionalizzata. Il nome della proprietà hint è composto dal nome del nome della proprietà internazionalizzata con il `_commentI18n` suffisso:

`${prop}_commentI18n`

Ad esempio, un `cq:page` node include la proprietà jcr:title in corso di localizzazione. L&#39;hint viene fornito come valore della proprietà denominata jcr:title_commentI18n.

### Verifica della copertura dell&#39;internazionalizzazione {#testing-internationalization-coverage}

Verifica di aver internazionalizzato tutte le stringhe nell’interfaccia utente. Per vedere quali stringhe sono coperte, imposta la lingua utente su zz_ZZ e apri l’interfaccia utente nel browser web. Le stringhe internazionalizzate appaiono con una traduzione stub nel seguente formato:

`USR_*Default-String*_尠`

L&#39;immagine seguente mostra la traduzione stub per la home page di AEM:

![chlimage_1](assets/chlimage_1a.jpeg)

Per impostare la lingua per l&#39;utente, configurare la proprietà della lingua del nodo delle preferenze per l&#39;account utente.

Il nodo delle preferenze di un utente ha un percorso come questo:

`/home/users/<letter>/<hash>/preferences`

![chlimage_1-1](assets/chlimage_1-1a.jpeg)
