---
title: Supporto di nuove impostazioni internazionali per la localizzazione di moduli adattivi
seo-title: Supporting new locales for adaptive forms localization
description: AEM Forms consente di aggiungere nuove impostazioni internazionali per la localizzazione di moduli adattivi. Le impostazioni internazionali supportate per impostazione predefinita sono inglese, francese, tedesco e giapponese.
seo-description: AEM Forms allows you to add new locales for localizing adaptive forms. The supported locales by default are English, French, German, and Japanese.
uuid: 7f9fab6b-8d93-46bb-8c7c-7b723d5159ea
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: d4e2acb0-8d53-4749-9d84-15b8136e610b
docset: aem65
feature: Adaptive Forms
role: Admin
exl-id: 2ed4d99e-0e90-4b21-ac17-aa6707a3ba7d
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 0%

---

# Supporto di nuove impostazioni internazionali per la localizzazione di moduli adattivi{#supporting-new-locales-for-adaptive-forms-localization}

## Informazioni sui dizionari internazionali {#about-locale-dictionaries}

La localizzazione dei moduli adattivi si basa su due tipi di dizionari locali:

**Dizionario specifico per il modulo** Contiene le stringhe utilizzate nei moduli adattivi. Ad esempio, etichette, nomi di campo, messaggi di errore, descrizioni della guida e così via. È gestito come un set di file XLIFF per ogni impostazione internazionale ed è possibile accedervi in `https://<host>:<port>/libs/cq/i18n/translator.html`.

**Dizionari globali** Ci sono due dizionari globali, gestiti come oggetti JSON, nella libreria client AEM. Questi dizionari contengono messaggi di errore predefiniti, nomi di mese, simboli di valuta, pattern di data e ora e così via. Puoi trovare questi dizionari in CRXDe Lite su /libs/fd/xfaforms/clientlibs/I18N. Queste posizioni contengono cartelle separate per ogni impostazione internazionale. Poiché i dizionari globali di solito non vengono aggiornati frequentemente, mantenere file JavaScript separati per ogni impostazione internazionale consente ai browser di memorizzarli nella cache e di ridurre l’utilizzo della larghezza di banda della rete quando si accede a diversi moduli adattivi sullo stesso server.

### Funzionamento della localizzazione dei moduli adattivi {#how-localization-of-adaptive-form-works}

Esistono due metodi per identificare le impostazioni internazionali del modulo adattivo. Quando viene eseguito il rendering di un modulo adattivo, identifica le impostazioni internazionali richieste da :

* guardando `[local]` nell’URL del modulo adattivo. Il formato dell’URL è `http://host:port/content/forms/af/[afName].[locale].html?wcmmode=disabled`. Utilizzo `[local]` Il selettore consente di memorizzare in cache un modulo adattivo.

* osservando i seguenti parametri nell’ordine specificato:

   * Parametro di richiesta `afAcceptLang`
Per ignorare le impostazioni internazionali del browser degli utenti, puoi trasmettere le 
`afAcceptLang` richiede il parametro per forzare le impostazioni internazionali. Ad esempio, con il seguente URL verrà eseguito il rendering del modulo nelle impostazioni internazionali giapponesi:
      `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

   * Le impostazioni internazionali del browser impostate per l’utente, specificate nella richiesta utilizzando `Accept-Language` intestazione.

   * Impostazione della lingua dell’utente specificata in AEM.

   * Per impostazione predefinita, le impostazioni internazionali del browser sono abilitate. Per modificare le impostazioni internazionali del browser,
      * Apri la gestione della configurazione. L’URL è `http://[server]:[port]/system/console/configMgr`
      * Individua e apri la **[!UICONTROL Canale web per moduli adattivi e comunicazioni interattive]** configurazione.
      * Cambia lo stato del **[!UICONTROL Usa impostazioni internazionali browser]** opzione e  **[!UICONTROL Salva]** la configurazione.

Una volta identificate le impostazioni internazionali, i moduli adattivi selezionano il dizionario specifico per il modulo. Se il dizionario specifico per il modulo per le impostazioni internazionali richieste non viene trovato, utilizza il dizionario per la lingua in cui è stato creato il modulo adattivo.

Se non sono presenti informazioni sulle impostazioni internazionali, il modulo adattivo viene distribuito nella lingua originale del modulo. La lingua originale è la lingua utilizzata durante lo sviluppo del modulo adattivo.

Se non esiste una libreria client per le impostazioni internazionali richieste, cerca in una libreria client il codice della lingua presente nelle impostazioni internazionali. Ad esempio, se le impostazioni internazionali richieste sono `en_ZA` (Inglese sudafricano) e la libreria client per `en_ZA` non esiste, il modulo adattivo utilizzerà la libreria client per `en` (Inglese), se esiste. Tuttavia, se non sono presenti, il modulo adattivo utilizza il dizionario per `en` locale.

## Aggiunta del supporto per la localizzazione per le impostazioni internazionali non supportate {#add-localization-support-for-non-supported-locales}

AEM Forms supporta attualmente la localizzazione di contenuti di moduli adattivi nelle impostazioni internazionali inglese (en), spagnolo (es), francese (fr), italiano (it), tedesco (de), giapponese (ja), portoghese-brasiliano (pt-BR), cinese (zh-CN), cinese-Taiwan (zh-TW) e coreano (ko-KR).

Per aggiungere il supporto per una nuova impostazione internazionale in fase di esecuzione dei moduli adattivi:

1. [Aggiungere un’impostazione internazionale al servizio GuideLocalizationService](../../forms/using/supporting-new-language-localization.md#p-add-a-locale-to-the-guide-localization-service-br-p)

1. [Aggiungere una libreria client XFA per le impostazioni internazionali](../../forms/using/supporting-new-language-localization.md#p-add-xfa-client-library-for-a-locale-br-p)

1. [Aggiungere una libreria client per moduli adattivi per le impostazioni internazionali](../../forms/using/supporting-new-language-localization.md#p-add-adaptive-form-client-library-for-a-locale-br-p)
1. [Aggiungere supporto per le impostazioni internazionali del dizionario](../../forms/using/supporting-new-language-localization.md#p-add-locale-support-for-the-dictionary-br-p)
1. [Riavvia il server](../../forms/using/supporting-new-language-localization.md#p-restart-the-server-p)

### Aggiungere un’impostazione internazionale al servizio Guide Localization {#add-a-locale-to-the-guide-localization-service-br}

1. Passa a `https://'[server]:[port]'/system/console/configMgr`.
1. Fai clic per modificare il **Servizio di localizzazione della guida** componente.
1. Aggiungi le impostazioni internazionali da aggiungere all’elenco delle impostazioni internazionali supportate.

![GuideLocalizationService](assets/configservice.png)

### Aggiungere una libreria client XFA per le impostazioni internazionali {#add-xfa-client-library-for-a-locale-br}

Crea un nodo di tipo `cq:ClientLibraryFolder` sotto `etc/<folderHierarchy>`, con categoria `xfaforms.I18N.<locale>`e aggiungi i seguenti file alla libreria client:

* **I18N.js** definizione `xfalib.locale.Strings` per `<locale>` come definito in `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`.

* **js.txt** contenenti:

```text
/libs/fd/xfaforms/clientlibs/I18N/Namespace.js
I18N.js
/etc/clientlibs/fd/xfaforms/I18N/LogMessages.js
```

### Aggiungere una libreria client per moduli adattivi per le impostazioni internazionali {#add-adaptive-form-client-library-for-a-locale-br}

Crea un nodo di tipo `cq:ClientLibraryFolder` sotto `etc/<folderHierarchy>`, con la categoria `guides.I18N.<locale>` e le dipendenze come `xfaforms.3rdparty`, `xfaforms.I18N.<locale>` e `guide.common`. &quot;

Aggiungi i seguenti file alla libreria client:

* **i18n.js** definizione `guidelib.i18n`, con pattern di &quot;calendarSymSymbol&quot;, `datePatterns`, `timePatterns`, `dateTimeSymbols`, `numberPatterns`, `numberSymbols`, `currencySymbols`, `typefaces` per `<locale>` secondo le specifiche XFA descritte in [Specifiche del set di impostazioni internazionali](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf). Puoi anche vedere come è definito per altre impostazioni internazionali supportate in `/etc/clientlibs/fd/af/I18N/fr/javascript/i18n.js`.
* **LogMessages.js** definizione `guidelib.i18n.strings` e `guidelib.i18n.LogMessages` per `<locale>` come definito in `/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`.
* **js.txt** contenenti:

```text
i18n.js
LogMessages.js
```

### Aggiungere supporto per le impostazioni internazionali del dizionario {#add-locale-support-for-the-dictionary-br}

Esegui questo passaggio solo se `<locale>` aggiungi non è tra `en`, `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`.

1. Crea un `nt:unstructured` nodo `languages` sotto `etc`, se non già presente.

1. Aggiungi una proprietà stringa con più valori `languages` al nodo, se non già presente.
1. Aggiungi il `<locale>` valori internazionali predefiniti `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`, se non già presente.

1. Aggiungi il `<locale>` ai valori del `languages` proprietà di `/etc/languages`.

La `<locale>` apparirà in `https://'[server]:[port]'/libs/cq/i18n/translator.html`.

### Riavvia il server {#restart-the-server}

Riavvia il server AEM per rendere effettive le impostazioni internazionali aggiunte.

## Librerie di esempio per aggiungere supporto per lo spagnolo {#sample-libraries-for-adding-support-for-spanish}

Librerie client di esempio per aggiungere supporto per lo spagnolo

[Ottieni file](assets/sample.zip)
