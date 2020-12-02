---
title: Configurazione dell’utilizzo dei cookie
seo-title: Configurazione dell’utilizzo dei cookie
description: AEM fornisce un servizio che consente di configurare e controllare in che modo i cookie vengono utilizzati con le pagine Web
seo-description: AEM fornisce un servizio che consente di configurare e controllare in che modo i cookie vengono utilizzati con le pagine Web
uuid: 10d95176-0a56-41f1-9d36-01dbdac757d4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 5773ec1a-f15b-462d-8f9f-54ee1d7ead44
translation-type: tm+mt
source-git-commit: f64eb57a69f2124523bd6eaed3e2f58a54c1ea8e
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 3%

---


# Configurazione utilizzo cookie{#configuring-cookie-usage}

AEM fornisce un servizio che consente di configurare e controllare in che modo i cookie vengono utilizzati con le pagine Web:

* Un servizio lato server configurabile mantiene un elenco di cookie utilizzabili.
* Un&#39;API javascript consente al codice javascript di verificare che sia possibile utilizzare un cookie.

Utilizzate questa funzione per assicurarvi che le pagine siano conformi al consenso degli utenti in merito all&#39;utilizzo dei cookie.

## Configurazione dei cookie consentiti {#configuring-allowed-cookies}

Configurate il  Adobe Granite Opt-Out Service per specificare in che modo i cookie vengono utilizzati nelle pagine Web. La tabella seguente descrive le proprietà che puoi configurare.

Per configurare il servizio, è possibile utilizzare la [console Web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) o [aggiungere una configurazione OSGi all&#39;archivio](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository). Nella tabella seguente sono descritte le proprietà necessarie per entrambi i metodi. Per una configurazione OSGi, il servizio PID è `com.adobe.granite.optout`.

| Nome proprietà (console Web) | Nome proprietà OSGi | Descrizione |
|---|---|---|
| Cookie di rifiuto | optout.cookies | I nomi dei cookie che indicano, se presenti sul dispositivo dell&#39;utente, che l&#39;utente non ha acconsentito all&#39;uso dei cookie. |
| Intestazioni HTTP di rifiuto | optout.headers | I nomi delle intestazioni HTTP che indicano, se presenti, che l&#39;utente non ha acconsentito all&#39;uso dei cookie. |
| Cookie elenco bianco | optout.whitelist.cookies | Un elenco di cookie che sono essenziali per il funzionamento del sito Web e che possono essere utilizzati senza il consenso dell&#39;utente. |

## Convalida dell&#39;utilizzo del cookie {#validating-cookie-usage}

Utilizzate JavaScript lato client per chiamare  Adobe Granite Opt-Out Service per verificare che sia possibile utilizzare un cookie. Utilizzare l&#39;oggetto javascript Granite.OptOutUtil per eseguire una delle seguenti operazioni:

* Ottenete un elenco di nomi di cookie che indicano che l&#39;utente non accetta di utilizzare i cookie a scopo di tracciamento.
* Ottenere un elenco di cookie che possono essere utilizzati.
* Determinare se il browser Web contiene un cookie che indica che l&#39;utente non accetta l&#39;uso dei cookie per il tracciamento.
* Determinare se è possibile utilizzare un cookie specifico.

La cartella della libreria client granite.utils [](/help/sites-developing/clientlibs.md#referencing-client-side-libraries) fornisce l&#39;oggetto Granite.OptOutUtil. Aggiungi il codice seguente al codice JSP dell&#39;intestazione della pagina per includere un collegamento alla libreria javascript:

`<ui:includeClientLib categories="granite.utils" />`

Ad esempio, la seguente funzione javascript determina se il cookie COOKIE_NAME può essere utilizzato prima di scriverlo:

```
function writeCookie(value){
   if (!Granite.OptOutUtil.maySetCookie("COOKIE_NAME"))
      return;
   if (value) {
      value = encodeURIComponent(value);
      document.cookie = "COOKIE_NAME=" + value;
   }
}
```

## L&#39;oggetto Granite.OptOutUtil Javascript {#the-granite-optoututil-javascript-object}

Granite.OptOutUtil consente di determinare se l&#39;utilizzo dei cookie è consentito.

### funzione getCookieNames() {#getcookienames-function}

Restituisce i nomi dei cookie che, se presenti, indicano che l&#39;utente non ha dato il consenso all&#39;uso dei cookie.

**Parametri**

Nessuno.

**Valore restituito**

Un array di nomi di cookie.

#### funzione getWhitelistCookieNames() {#getwhitelistcookienames-function}

Restituisce i nomi dei cookie che possono essere utilizzati indipendentemente dal consenso dell&#39;utente.

**Parametri**

Nessuno.

**Valore restituito**

Un array di nomi di cookie.

#### isOptedOut(), funzione {#isoptedout-function}

Determina se il browser dell&#39;utente contiene cookie che indicano che non è stato dato il consenso all&#39;utilizzo dei cookie.

**Parametri**

Nessuno.

**Valore restituito**

Un valore booleano di `true` se viene trovato un cookie che indica l&#39;assenza di consenso e un valore di `false` se nessun cookie indica l&#39;assenza di consenso.

### funzione MaySetCookie(cookieName) {#maysetcookie-cookiename-function}

Determina se un cookie specifico può essere utilizzato nel browser dell&#39;utente. Questa funzione equivale a utilizzare la funzione `isOptedOut` insieme a determinare se il cookie specificato è incluso nell&#39;elenco restituito dalla funzione `getWhitelistCookieNames`.

**Parametri**

* cookieName: Stringa. Nome del cookie.

**Valore restituito**

Un valore booleano di `true` se è possibile utilizzare `cookieName` oppure un valore di `false` se non è possibile utilizzare `cookieName`.
