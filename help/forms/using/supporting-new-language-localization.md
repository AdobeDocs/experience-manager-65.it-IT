---
title: Supporto di nuove lingue per la localizzazione di moduli adattivi
description: AEM Forms consente di aggiungere nuove lingue per la localizzazione dei moduli adattivi. Le lingue supportate per impostazione predefinita sono inglese, francese, tedesco e giapponese.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
feature: Adaptive Forms,Foundation Components
role: Admin,User
exl-id: 2ed4d99e-0e90-4b21-ac17-aa6707a3ba7d
solution: Experience Manager, Experience Manager Forms
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 2%

---

# Supporto di nuove lingue per la localizzazione di moduli adattivi{#supporting-new-locales-for-adaptive-forms-localization}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/supporting-new-language-localization.html) |
| AEM 6.5 | Questo articolo |

## Informazioni sui dizionari delle impostazioni internazionali {#about-locale-dictionaries}

La localizzazione dei moduli adattivi si basa su due tipi di dizionari locali:

**Dizionario specifico per modulo** Contiene stringhe utilizzate nei moduli adattivi. Ad esempio, etichette, nomi dei campi, messaggi di errore, descrizioni della guida e così via. Viene gestito come un insieme di file XLIFF per ogni lingua e puoi accedervi all&#39;indirizzo `https://<host>:<port>/libs/cq/i18n/translator.html`.

**Dizionari globali** Nella libreria client AEM sono presenti due dizionari globali gestiti come oggetti JSON. Questi dizionari contengono messaggi di errore predefiniti, nomi dei mesi, simboli di valuta, modelli di data e ora e così via. Puoi trovare questi dizionari in CRXDe Lite su /libs/fd/xfaforms/clientlibs/I18N. Questi percorsi contengono cartelle separate per ogni lingua. Poiché i dizionari globali di solito non vengono aggiornati frequentemente, la separazione dei file JavaScript per ciascuna lingua consente ai browser di memorizzarli nella cache e di ridurre l’utilizzo della larghezza di banda di rete quando si accede a moduli adattivi diversi sullo stesso server.

### Come funziona la localizzazione dei moduli adattivi {#how-localization-of-adaptive-form-works}

Esistono due metodi per identificare le impostazioni locali del modulo adattivo. Quando viene eseguito il rendering di un modulo adattivo, questo identifica le impostazioni locali richieste tramite:

* visualizzazione del selettore `[local]` nell&#39;URL del modulo adattivo. Il formato dell&#39;URL è `http://host:port/content/forms/af/[afName].[locale].html?wcmmode=disabled`. Il selettore `[local]` consente di memorizzare nella cache un modulo adattivo.

* esaminare i seguenti parametri nell&#39;ordine specificato:

   * Parametro richiesta `afAcceptLang`
Per ignorare le impostazioni locali del browser degli utenti, è possibile passare il parametro di richiesta `afAcceptLang` per forzare le impostazioni locali. Ad esempio, il seguente URL è stato forzato a eseguire il rendering del modulo nelle impostazioni internazionali giapponesi:
     `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

   * Impostazioni locali del browser impostate per l&#39;utente, specificate nella richiesta utilizzando l&#39;intestazione `Accept-Language`.

   * Impostazione della lingua dell&#39;utente specificato nell&#39;AEM.

   * Le impostazioni locali del browser sono attivate per impostazione predefinita. Per modificare le impostazioni internazionali del browser:
      * Apri Gestione configurazione. URL: `http://[server]:[port]/system/console/configMgr`
      * Individua e apri la configurazione **[!UICONTROL Modulo adattivo e canale web di comunicazione interattiva]**.
      * Cambia lo stato dell&#39;opzione **[!UICONTROL Usa impostazioni internazionali del browser]** e **[!UICONTROL Salva]** la configurazione.

Una volta identificate le impostazioni locali, i moduli adattivi selezionano il dizionario specifico per il modulo. Se non viene trovato il dizionario specifico per la lingua richiesta, viene utilizzato il dizionario per la lingua in cui è stato creato il modulo adattivo.

Se non sono presenti informazioni sulle impostazioni internazionali, il modulo adattivo viene consegnato nella lingua originale del modulo. La lingua originale è la lingua utilizzata durante lo sviluppo del modulo adattivo.

Se non esiste una libreria client per le impostazioni locali richieste, verifica la presenza di una libreria client per il codice della lingua presente nelle impostazioni locali. Ad esempio, se le impostazioni locali richieste sono `en_ZA` (inglese sudafricano) e la libreria client per `en_ZA` non esiste, il modulo adattivo utilizzerà la libreria client per la lingua `en` (inglese), se esiste. Tuttavia, se non esiste nessuno di questi, il modulo adattivo utilizza il dizionario per le impostazioni locali di `en`.

## Aggiunta del supporto per la localizzazione per le lingue non supportate {#add-localization-support-for-non-supported-locales}

AEM Forms attualmente supporta la localizzazione dei contenuti dei moduli adattivi nelle lingue inglese (en), spagnolo (es), francese (fr), italiano (it), tedesco (de), giapponese (ja), portoghese-brasiliano (pt-BR), cinese (zh-CN), cinese-Taiwan (zh-TW) e coreano (ko-KR).

Per aggiungere il supporto per una nuova lingua in fase di esecuzione per moduli adattivi:

1. [Aggiungere una lingua al servizio GuideLocalizationService](../../forms/using/supporting-new-language-localization.md#p-add-a-locale-to-the-guide-localization-service-br-p)

1. [Aggiungere una libreria client XFA per una lingua](../../forms/using/supporting-new-language-localization.md#p-add-xfa-client-library-for-a-locale-br-p)

1. [Aggiungere una libreria client per moduli adattivi per una lingua](../../forms/using/supporting-new-language-localization.md#p-add-adaptive-form-client-library-for-a-locale-br-p)
1. [Aggiungere il supporto delle impostazioni locali per il dizionario](../../forms/using/supporting-new-language-localization.md#p-add-locale-support-for-the-dictionary-br-p)
1. [Riavvia il server](../../forms/using/supporting-new-language-localization.md#p-restart-the-server-p)

### Aggiungere una lingua al servizio Localizzazione guida {#add-a-locale-to-the-guide-localization-service-br}

1. Passa a `https://'[server]:[port]'/system/console/configMgr`.
1. Fare clic per modificare il componente **Servizio di localizzazione guida**.
1. Aggiungere le impostazioni locali da aggiungere all&#39;elenco delle impostazioni internazionali supportate.

![ServizioLocalizzazioneGuida](assets/configservice.png)

### Aggiungere una libreria client XFA per una lingua {#add-xfa-client-library-for-a-locale-br}

Creare un nodo di tipo `cq:ClientLibraryFolder` in `etc/<folderHierarchy>`, con categoria `xfaforms.I18N.<locale>`, e aggiungere i seguenti file alla libreria client:

* **I18N.js** che definisce `xfalib.locale.Strings` per `<locale>` come definito in `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`.

* **js.txt** contenente quanto segue:

```text
/libs/fd/xfaforms/clientlibs/I18N/Namespace.js
I18N.js
/etc/clientlibs/fd/xfaforms/I18N/LogMessages.js
```

### Aggiungere una libreria client per moduli adattivi per una lingua {#add-adaptive-form-client-library-for-a-locale-br}

Creare un nodo di tipo `cq:ClientLibraryFolder` in `etc/<folderHierarchy>`, con categoria come `guides.I18N.<locale>` e dipendenze come `xfaforms.3rdparty`, `xfaforms.I18N.<locale>` e `guide.common`. &quot;

Aggiungi i seguenti file alla libreria client:

* **i18n.js** che definisce `guidelib.i18n`, con pattern di &quot;calendarSymbols&quot;, `datePatterns`, `timePatterns`, `dateTimeSymbols`, `numberPatterns`, `numberSymbols`, `currencySymbols`, `typefaces` per `<locale>` in base alle specifiche XFA descritte in [Specifiche set di impostazioni locali](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf). È inoltre possibile vedere come viene definito per altre impostazioni internazionali supportate in `/etc/clientlibs/fd/af/I18N/fr/javascript/i18n.js`.
* **LogMessages.js** che definisce `guidelib.i18n.strings` e `guidelib.i18n.LogMessages` per `<locale>` come definito in `/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`.
* **js.txt** contenente quanto segue:

```text
i18n.js
LogMessages.js
```

### Aggiungere il supporto delle impostazioni locali per il dizionario {#add-locale-support-for-the-dictionary-br}

Eseguire questo passaggio solo se il `<locale>` che si sta aggiungendo non è tra `en`, `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`.

1. Creare un nodo `nt:unstructured` `languages` in `etc`, se non già presente.

1. Aggiungere una proprietà stringa multivalore `languages` al nodo, se non già presente.
1. Aggiungere i valori predefiniti delle impostazioni locali `<locale>` `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`, se non già presenti.

1. Aggiungere `<locale>` ai valori della proprietà `languages` di `/etc/languages`.

`<locale>` verrà visualizzato in `https://'[server]:[port]'/libs/cq/i18n/translator.html`.

### Riavvia il server {#restart-the-server}

Riavviare il server AEM per rendere effettive le impostazioni locali aggiunte.

>[!NOTE]
>
> Per riavviare l&#39;SDK, si consiglia di utilizzare il comando &#39;Ctrl + C&#39;. Il riavvio dell’SDK dell’AEM con metodi alternativi, ad esempio l’arresto dei processi Java, può causare incongruenze nell’ambiente di sviluppo dell’AEM.

## Librerie di esempio per l’aggiunta del supporto per lo spagnolo {#sample-libraries-for-adding-support-for-spanish}

Librerie client di esempio per aggiungere il supporto per la lingua spagnola

[Ottieni file](assets/sample.zip)
