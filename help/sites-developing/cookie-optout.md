---
title: Configurazione dell’utilizzo dei cookie
description: AEM fornisce un servizio che consente di configurare e controllare il modo in cui i cookie vengono utilizzati con le pagine web.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 42e8d804-6b6a-432e-a651-940b9f45db4e
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 2%

---

# Configurazione dell’utilizzo dei cookie{#configuring-cookie-usage}

AEM fornisce un servizio che consente di configurare e controllare il modo in cui i cookie vengono utilizzati con le pagine web:

* Un servizio lato server configurabile mantiene un elenco di cookie che possono essere utilizzati.
* Un’API JavaScript consente al codice JavaScript di verificare che sia possibile utilizzare un cookie.

Utilizza questa funzione per assicurarti che le pagine siano conformi al consenso degli utenti per quanto riguarda l’utilizzo dei cookie.

## Configurazione dei cookie consentiti {#configuring-allowed-cookies}

Configura il servizio di rinuncia di Adobe Granite per specificare come vengono utilizzati i cookie sulle pagine web. Nella tabella seguente sono descritte le proprietà che è possibile configurare.

Per configurare il servizio, puoi utilizzare [Console web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) o [aggiungere una configurazione OSGi all’archivio](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository). Nella tabella seguente vengono descritte le proprietà necessarie per entrambi i metodi. Per una configurazione OSGi, il PID del servizio è `com.adobe.granite.optout`.

| Nome proprietà (console Web) | Nome proprietà OSGi | Descrizione |
|---|---|---|
| Cookie di rinuncia | optout.cookies | I nomi dei cookie che indicano, quando presenti sul dispositivo dell’utente, che quest’ultimo non ha acconsentito all’utilizzo dei cookie. |
| Intestazioni HTTP di rinuncia | optout.headers | I nomi delle intestazioni HTTP che indicano, se presenti, che l’utente non ha acconsentito all’utilizzo dei cookie. |
| Cookie della whitelist | optout.whitelist.cookies | Un elenco di cookie che sono essenziali per il funzionamento del sito web e possono essere utilizzati senza il consenso di un utente. |

## Convalida dell’utilizzo dei cookie {#validating-cookie-usage}

Utilizza JavaScript lato client per chiamare il servizio Opt-out di Adobe Granite e verificare che sia possibile utilizzare un cookie. Utilizzare l&#39;oggetto JavaScript Granite.OptOutUtil per eseguire una delle operazioni seguenti:

* Ottieni un elenco di nomi di cookie che indicano che l’utente non acconsente all’utilizzo dei cookie a scopo di tracciamento.
* Ottieni un elenco di cookie che possono essere utilizzati.
* Determina se il browser web contiene un cookie che indica che l’utente non acconsente all’utilizzo dei cookie per il tracciamento.
* Determina se è possibile utilizzare un cookie specifico.

Granite.utils [cartella della libreria client](/help/sites-developing/clientlibs.md#referencing-client-side-libraries) fornisce l&#39;oggetto Granite.OptOutUtil. Aggiungi il seguente codice all&#39;intestazione della pagina JSP per includere un collegamento alla libreria JavaScript:

`<ui:includeClientLib categories="granite.utils" />`

Ad esempio, la seguente funzione JavaScript determina se il cookie COOKIE_NAME può essere utilizzato prima di scrivervi:

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

## Oggetto JavaScript Granite.OptOutUtil {#the-granite-optoututil-javascript-object}

Granite.OptOutUtil consente di determinare se l&#39;utilizzo dei cookie è consentito.

### funzione getCookieNames() {#getcookienames-function}

I nomi dei cookie che, se presenti, indicano che l’utente non ha dato il consenso all’uso dei cookie.

**Parametri**

Nessuno.

**Restituisce**

Matrice di nomi di cookie.

#### funzione getWhitelistCookieNames() {#getwhitelistcookienames-function}

I nomi dei cookie che possono essere utilizzati indipendentemente dal consenso dell’utente.

**Parametri**

Nessuno.

**Restituisce**

Matrice di nomi di cookie.

#### isOptedOut(), funzione {#isoptedout-function}

Determina se il browser dell’utente contiene cookie che indicano che non è stato fornito il consenso all’utilizzo dei cookie.

**Parametri**

Nessuno.

**Restituisce**

Valore booleano di `true` se viene trovato un cookie che indica assenza di consenso e un valore di `false` se nessun cookie indica il mancato consenso.

### funzione maySetCookie(cookieName) {#maysetcookie-cookiename-function}

Determina se è possibile utilizzare un cookie specifico nel browser dell&#39;utente. Questa funzione equivale a utilizzare il `isOptedOut` per determinare se il cookie specificato è incluso nell’elenco che il cookie `getWhitelistCookieNames` restituisce.

**Parametri**

* cookieName: stringa. Nome del cookie.

**Restituisce**

Valore booleano di `true` se `cookieName` può essere utilizzato o un valore di `false` se `cookieName` non può essere utilizzato.
