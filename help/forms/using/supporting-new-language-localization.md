---
title: Supporto di nuove impostazioni internazionali per la localizzazione dei moduli adattivi
seo-title: Supporto di nuove impostazioni internazionali per la localizzazione dei moduli adattivi
description: AEM Forms consente di aggiungere nuove impostazioni internazionali per la localizzazione dei moduli adattivi. Le impostazioni internazionali supportate per impostazione predefinita sono Inglese, Francese, Tedesco e Giapponese.
seo-description: AEM Forms consente di aggiungere nuove impostazioni internazionali per la localizzazione dei moduli adattivi. Le impostazioni internazionali supportate per impostazione predefinita sono Inglese, Francese, Tedesco e Giapponese.
uuid: 7f9fab6b-8d93-46bb-8c7c-7b723d5159ea
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: d4e2acb0-8d53-4749-9d84-15b8136e610b
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---


# Supporto di nuove impostazioni internazionali per la localizzazione dei moduli adattivi{#supporting-new-locales-for-adaptive-forms-localization}

## Informazioni sui dizionari di lingua {#about-locale-dictionaries}

La localizzazione dei moduli adattivi si basa su due tipi di dizionari di lingua:

**Dizionario** specifico per il modulo Contiene le stringhe utilizzate nei moduli adattivi. Ad esempio, etichette, nomi di campi, messaggi di errore, descrizioni della guida e così via. Viene gestito come un set di file XLIFF per ogni lingua e potete accedervi in `https://<host>:<port>/libs/cq/i18n/translator.html`.

**Dizionari** globali Nella libreria client AEM sono presenti due dizionari globali, gestiti come oggetti JSON. Questi dizionari contengono messaggi di errore predefiniti, nomi dei mesi, simboli di valuta, pattern di data e ora e così via. Questi dizionari sono disponibili in CRXDe Lite all&#39;indirizzo /libs/fd/xfaforms/clientlibs/I18N. Questi percorsi contengono cartelle separate per ogni impostazione internazionale. Poiché in genere i dizionari globali non vengono aggiornati frequentemente, il mantenimento di file JavaScript separati per ciascuna lingua consente ai browser di memorizzarli nella cache e di ridurre l&#39;utilizzo della larghezza di banda di rete quando accedono a diversi moduli adattivi sullo stesso server.

### Funzionamento della localizzazione del modulo adattivo {#how-localization-of-adaptive-form-works}

Quando viene eseguito il rendering di un modulo adattivo, identifica le impostazioni internazionali richieste, esaminando i seguenti parametri nell&#39;ordine specificato:

* Parametro della richiesta `afAcceptLang`Per ignorare le impostazioni internazionali del browser degli utenti, puoi passare il 
`afAcceptLang` richiede il parametro per imporre l&#39;impostazione internazionale. Ad esempio, con il seguente URL sarà necessario eseguire il rendering del modulo in lingua giapponese:
   `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

* Le impostazioni internazionali del browser impostate per l’utente, specificate nella richiesta utilizzando l’ `Accept-Language` intestazione.

* Impostazione della lingua dell’utente specificata in AEM.

Una volta identificate le impostazioni internazionali, i moduli adattivi selezionano il dizionario specifico del modulo. Se il dizionario specifico del modulo per le impostazioni internazionali richieste non viene trovato, viene utilizzato il dizionario inglese (en).

Se non esiste una libreria client per l&#39;impostazione internazionale richiesta, essa cerca una libreria client per il codice della lingua presente nelle impostazioni internazionali. Ad esempio, se le impostazioni internazionali richieste sono `en_ZA` (Inglese sudafricano) e la libreria client per `en_ZA` non esiste, il modulo adattivo utilizzerà la libreria client per la lingua `en` (Inglese), se esiste. Tuttavia, se non ne esiste alcuna, il modulo adattivo utilizza il dizionario per le `en` impostazioni internazionali.

## Aggiunta del supporto per la localizzazione per le lingue non supportate {#add-localization-support-for-non-supported-locales}

AEM Forms attualmente supporta la localizzazione di contenuti di moduli adattivi in inglese (en), spagnolo (es), francese (fr), italiano (it), tedesco (de), giapponese (ja), portoghese-brasiliano (pt-BR), cinese (zh-CN), cinese-Taiwan (zh-TW) e coreano (ko-KR).

Per aggiungere il supporto per una nuova impostazione internazionale in fase di esecuzione dei moduli adattivi:

1. [Aggiunta di un&#39;impostazione internazionale al servizio GuideLocalizationService](../../forms/using/supporting-new-language-localization.md#p-add-a-locale-to-the-guide-localization-service-br-p)

1. [Aggiungere una libreria client XFA per una lingua](../../forms/using/supporting-new-language-localization.md#p-add-xfa-client-library-for-a-locale-br-p)

1. [Aggiunta di una libreria client di moduli adattivi per una lingua](../../forms/using/supporting-new-language-localization.md#p-add-adaptive-form-client-library-for-a-locale-br-p)
1. [Aggiunta del supporto per le impostazioni internazionali per il dizionario](../../forms/using/supporting-new-language-localization.md#p-add-locale-support-for-the-dictionary-br-p)
1. [Riavviare il server](../../forms/using/supporting-new-language-localization.md#p-restart-the-server-p)

### Aggiunta di un&#39;impostazione internazionale al servizio Guide Localization {#add-a-locale-to-the-guide-localization-service-br}

1. Passa a `https://'[server]:[port]'/system/console/configMgr`.
1. Fare clic per modificare il componente **Guide Localization Service** .
1. Aggiungere le impostazioni internazionali da aggiungere all&#39;elenco delle impostazioni internazionali supportate.

![GuideLocalizationService](assets/configservice.png)

### Aggiungere una libreria client XFA per una lingua {#add-xfa-client-library-for-a-locale-br}

Create un nodo di tipo `cq:ClientLibraryFolder` in `etc/<folderHierarchy>`, con categoria `xfaforms.I18N.<locale>`, e aggiungete i seguenti file alla libreria client:

* **I18N.js** che definisce `xfalib.locale.Strings` per il `<locale>` contenuto come definito in `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`.

* **js.txt** contenente quanto segue:

```text
/libs/fd/xfaforms/clientlibs/I18N/Namespace.js
I18N.js
/etc/clientlibs/fd/xfaforms/I18N/LogMessages.js
```

### Aggiunta di una libreria client di moduli adattivi per una lingua {#add-adaptive-form-client-library-for-a-locale-br}

Crea un nodo di tipo `cq:ClientLibraryFolder` in `etc/<folderHierarchy>`, con categoria come `guides.I18N.<locale>` e dipendenze come `xfaforms.3rdparty`, `xfaforms.I18N.<locale>` e `guide.common`. &quot;

Aggiungete i seguenti file alla libreria client:

* **i18n.js** che definisce `guidelib.i18n`, con pattern di &quot;CalendarSymsymbol&quot;, `datePatterns`, `timePatterns`, `dateTimeSymbols`, `numberPatterns`, `numberSymbols`, `currencySymbols`, `typefaces` per l&#39;interfaccia, `<locale>` [](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf)come indicato nelle specifiche XFA descritte in Specifiche per set di codici internazionali, Potete inoltre vedere come viene definito per altre impostazioni internazionali supportate in `/etc/clientlibs/fd/af/I18N/fr/javascript/i18n.js`.
* **LogMessages.js** che definisce `guidelib.i18n.strings` e `guidelib.i18n.LogMessages` per il `<locale>` file come definito in `/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`.
* **js.txt** contenente quanto segue:

```text
i18n.js
LogMessages.js
```

### Aggiunta del supporto per le impostazioni internazionali per il dizionario {#add-locale-support-for-the-dictionary-br}

Esegui questo passaggio solo se il `<locale>` contenuto aggiunto non è compreso tra `en`, `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja``ko-kr`.

1. Crea un `nt:unstructured` nodo `languages` sotto `etc`, se non già presente.

1. Aggiungi una proprietà stringa con più valori `languages` al nodo, se non già presente.
1. Aggiungete i valori `<locale>` di lingua predefiniti `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja``ko-kr`, se non già presenti.

1. Aggiungete i valori `<locale>` della `languages` proprietà di `/etc/languages`.

Il `<locale>` simbolo verrà visualizzato in `https://'[server]:[port]'/libs/cq/i18n/translator.html`.

### Restart the server {#restart-the-server}

Riavviate il server AEM per rendere effettive le impostazioni internazionali aggiunte.

## Librerie di esempio per aggiungere supporto per lo spagnolo {#sample-libraries-for-adding-support-for-spanish}

Esempi di librerie client per aggiungere supporto per lo spagnolo

[Ottieni file](assets/sample.zip)
