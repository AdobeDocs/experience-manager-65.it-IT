---
title: Configurazione dell’utilizzo dei cookie
seo-title: Configuring Cookie Usage
description: AEM fornisce un servizio che consente di configurare e controllare il modo in cui i cookie vengono utilizzati con le pagine web
seo-description: AEM provides a service that enables you to configure and control how cookies are used with your web pages
uuid: 10d95176-0a56-41f1-9d36-01dbdac757d4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 5773ec1a-f15b-462d-8f9f-54ee1d7ead44
exl-id: 42e8d804-6b6a-432e-a651-940b9f45db4e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 5%

---

# Configurazione dell’utilizzo dei cookie{#configuring-cookie-usage}

AEM fornisce un servizio che consente di configurare e controllare il modo in cui i cookie vengono utilizzati con le pagine web:

* Un servizio lato server configurabile mantiene un elenco di cookie che possono essere utilizzati.
* Un&#39;API javascript abilita il codice javascript per verificare che possa essere utilizzato un cookie.

Utilizza questa funzione per assicurarti che le tue pagine siano conformi al consenso degli utenti per quanto riguarda l’utilizzo dei cookie.

## Configurazione dei cookie consentiti {#configuring-allowed-cookies}

Configura l&#39;Adobe Servizio di rinuncia di Granite per specificare il modo in cui i cookie vengono utilizzati nelle pagine web. La tabella seguente descrive le proprietà che puoi configurare.

Per configurare il servizio, puoi utilizzare la funzione [Console web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) o [aggiungi una configurazione OSGi all’archivio](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository). Nella tabella seguente sono descritte le proprietà necessarie per entrambi i metodi. Per una configurazione OSGi, il PID del servizio è `com.adobe.granite.optout`.

| Nome proprietà (console Web) | Nome proprietà OSGi | Descrizione |
|---|---|---|
| Cookie di rinuncia | optout.cookies | Nomi dei cookie che indicano, se presenti sul dispositivo dell&#39;utente, che l&#39;utente non ha acconsentito all&#39;uso dei cookie. |
| Intestazioni HTTP Opt-Out | optout.headers | I nomi delle intestazioni HTTP che indicano, se presenti, che l&#39;utente non ha acconsentito all&#39;uso dei cookie. |
| Cookie della whitelist | optout.whitelist.cookies | Un elenco di cookie essenziali per il funzionamento del sito web e utilizzabili senza il consenso dell&#39;utente. |

## Convalida dell’utilizzo dei cookie {#validating-cookie-usage}

Utilizza javascript lato client per chiamare Adobe Granite Opt-Out Service per verificare di poter utilizzare un cookie. Utilizzare l&#39;oggetto javascript Granite.OptOutUtil per eseguire una delle seguenti attività:

* Ottieni un elenco di nomi di cookie che indicano che l’utente non acconsente all’utilizzo dei cookie a scopo di tracciamento.
* Ottieni un elenco di cookie che possono essere utilizzati.
* Stabilisci se il browser web contiene un cookie che indica che l’utente non acconsente all’utilizzo di cookie per il tracciamento.
* Determina se è possibile utilizzare un cookie specifico.

Granite.utils [cartella libreria client](/help/sites-developing/clientlibs.md#referencing-client-side-libraries) fornisce l&#39;oggetto Granite.OptOutUtil . Aggiungi il seguente codice al tuo codice JSP per includere un collegamento alla libreria javascript:

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

## Oggetto Javascript Granite.OptOutUtil {#the-granite-optoututil-javascript-object}

Granite.OptOutUtil consente di determinare se l&#39;utilizzo dei cookie è consentito.

### funzione getCookieNames() {#getcookienames-function}

Restituisce i nomi dei cookie che, se presenti, indicano che l’utente non ha dato il consenso all’uso dei cookie.

**Parametri**

Nessuno.

**Valore restituito**

Matrice di nomi di cookie.

#### funzione getWhitelistCookieNames() {#getwhitelistcookienames-function}

Restituisce i nomi dei cookie che possono essere utilizzati indipendentemente dal consenso dell’utente.

**Parametri**

Nessuno.

**Valore restituito**

Matrice di nomi di cookie.

#### isOptedOut(), funzione {#isoptedout-function}

Determina se il browser dell&#39;utente contiene cookie che indicano che non è stato dato il consenso all&#39;utilizzo dei cookie.

**Parametri**

Nessuno.

**Valore restituito**

Un valore booleano di `true` se viene trovato un cookie che indica l’assenza di consenso e un valore di `false` se nessun cookie indica la mancata autorizzazione.

### funzione maySetCookie(cookieName) {#maysetcookie-cookiename-function}

Determina se è possibile utilizzare un cookie specifico nel browser dell&#39;utente. Equivale a utilizzare la funzione `isOptedOut` in combinazione con determinare se il cookie dato è incluso nell&#39;elenco che `getWhitelistCookieNames` restituisce la funzione .

**Parametri**

* cookieName: Stringa. Nome del cookie.

**Valore restituito**

Un valore booleano di `true` if `cookieName` può essere utilizzato, oppure un valore di `false` if `cookieName` non può essere utilizzato.
