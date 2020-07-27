---
title: Modifica delle impostazioni internazionali dell'interfaccia utente dell'area di lavoro AEM Forms
seo-title: Modifica delle impostazioni internazionali dell'interfaccia utente dell'area di lavoro AEM Forms
description: Come modificare l'area di lavoro AEM Forms per localizzare il testo, le categorie ridotte, le code e i processi e il selettore data sull'interfaccia.
seo-description: Come modificare l'area di lavoro AEM Forms per localizzare il testo, le categorie ridotte, le code e i processi e il selettore data sull'interfaccia.
uuid: c89ff150-a36e-45cc-99a6-8768dbe58eab
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 89f9d666-28e2-4201-8467-ae90693ca5d2
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 0%

---


# Modifica delle impostazioni internazionali dell&#39;interfaccia utente dell&#39;area di lavoro AEM Forms{#changing-the-locale-of-aem-forms-workspace-user-interface}

L&#39;area di lavoro AEM Forms fornisce supporto completo per le lingue inglese, francese, tedesco e giapponese. Consente inoltre di localizzare l’interfaccia utente dell’area di lavoro AEM Forms in qualsiasi altra lingua.

Per localizzare l’interfaccia utente dell’area di lavoro AEM Forms in base alla lingua desiderata:

* Localizzate il testo dell&#39;area di lavoro AEM Forms.
* Localizzare categorie, code e processi compressi.
* Localizza selettore data

Prima di eseguire i passaggi indicati sopra, accertatevi di seguire i passaggi elencati in [Generico per la personalizzazione](../../forms/using/generic-steps-html-workspace-customization.md)dell&#39;area di lavoro AEM Forms.

>[!NOTE]
>
>Per modificare la lingua della schermata di accesso dell’area di lavoro AEM Forms, consultate [Creazione di una nuova schermata](../../forms/using/creating-new-login-screen.md)di accesso.

## Localizzazione del testo {#localizing-text}

Effettuate le seguenti operazioni per aggiungere il supporto per una lingua *Nuovo* e il codice delle impostazioni internazionali del browser *ora*.

1. Accedete a CRXDE Lite.
L’URL predefinito di CRXDE Lite è `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. Andate alla posizione `apps/ws/locales` e create una nuova cartella `nw.`
1. Copiate il file `translation.json`dalla posizione `/apps/ws/locales/en-US` alla posizione `/apps/ws/locales/nw` .
1. Passate a `/apps/ws/locales/nw` e aprite `translation.json` per la modifica. Apportate modifiche specifiche alle impostazioni internazionali al file translate.json.

   Gli esempi seguenti contengono il file translate.json per le impostazioni internazionali Inglese e Francese dell&#39;area di lavoro AEM Forms.

   ![translate_json_in_it](assets/translation_json_in_en.png) ![translate_json_in_fr](assets/translation_json_in_fr.png)

## Localizzazione di categorie, code e processi compressi {#localizing-collapsed-categories-queues-and-processes}

L&#39;area di lavoro AEM Forms utilizza immagini per visualizzare intestazioni di categorie, code e processi. Per localizzare queste intestazioni è necessario un pacchetto di sviluppo. Per informazioni dettagliate sulla creazione del pacchetto di sviluppo, consultate Creazione del codice dell&#39;area di lavoro dei AEM Forms [Building.](introduction-customizing-html-workspace.md#building-html-workspace-code)

Nei passaggi seguenti, si presume che i nuovi file di immagine localizzati siano *Categories_nw.png*, *Queue_nw.png* e *Processes_nw.png*. La larghezza consigliata delle immagini è 19 px.

>[!NOTE]
>
>Per trovare il codice della lingua del browser in uso. Apri `https://'[server]:[port]'/lc/libs/ws/Locale.html`.

![comprimere_panel_image](assets/collapsing_panels_image.png)

Per localizzare le immagini, effettuate le seguenti operazioni:

1. Utilizzando un client WebDAV, inserite i file immagine nella cartella */apps/ws/images* .
1. Passa a */apps/ws/css*. Aprite *newStyle.css* per la modifica e aggiungete le seguenti voci:

   ```css
   #categoryListBar .content.nw {
        background: #3e3e3e url(../images/Categories_nw.png) no-repeat 10px 10px;
    }
   
   #filterListBar .content.nw {
       background: #3e3e3e url(../images/Queues_nw.png) no-repeat 10px 10px;
   }
   
   #processNameListBar .content.nw {
       background: #3e3e3e url(../images/Processes_nw.png) no-repeat 10px 10px;
   }
   ```

1. Effettuate tutte le modifiche semantiche elencate nell&#39;articolo Personalizzazione [di](../../forms/using/introduction-customizing-html-workspace.md) Workspace.
1. Andate alla cartella *js/runtime/utility* e aprite il file *usersession.js* per la modifica.
1. Individuare il codice elencato nel blocco di codice originale e aggiungere la condizione *lang !== &#39;nw&#39;* all&#39;istruzione if:

   ```javascript
   // Orignal code
   setLocale = function () {
           var lang = $.trim(i18n.lng());
           if (lang === null || lang === '' || (lang !== 'fr-FR' && lang !== 'de-DE' && lang !== 'ja-JP')) {
               window.lcWorkspace.locale = 'en-US';
           } else {
               window.lcWorkspace.locale = lang;
           }
       }
   ```

   ```javascript
   //new code
    setLocale = function () {
           var lang = $.trim(i18n.lng());
           if (lang === null || lang === '' || (lang !== 'fr-FR' && lang !== 'de-DE' && lang !== 'ja-JP' && lang !== 'nw')) {
               window.lcWorkspace.locale = 'en-US';
           } else {
               window.lcWorkspace.locale = lang;
           }
       }
   ```

## Localizzazione del selettore data {#localizing-date-picker}

È necessario un pacchetto di sviluppo per localizzare l&#39;API *datepicker* . Per informazioni dettagliate sulla creazione del pacchetto di sviluppo, consultate Creazione del codice [dell&#39;area di lavoro dei AEM Forms](introduction-customizing-html-workspace.md#building-html-workspace-code)Building.

1. Scaricate ed estraete il pacchetto [dell&#39;interfaccia utente](https://jqueryui.com/download/all/)jQuery, passate a *&lt;pacchetto dell&#39;interfaccia utente jquery estratto>*\jquery-ui-1.10.2.zip\jquery-ui-1.10.2\ui\i18n.
1. Copiate il file jquery.ui.datepicker-nw.js per il codice delle impostazioni internazionali ora in apps/ws/js/libs/jqueryui e apportate modifiche specifiche alle impostazioni internazionali del file.
1. Individuate `apps/ws/js` e aprite il `jquery.ui.datepicker-nw.js` file per la modifica.
1. Nel file main.js create un alias per `jquery.ui.datepicker-nw.js.` Il codice per creare un alias per il `jquery.ui.datepicker-nw.js` file è:

   ```javascript
   jqueryuidatepickernw : pathprefix + 'libs/jqueryui/jquery.ui.datepicker-nw'
   ```

1. Utilizzate l&#39;alias `jqueryuidatepickernw` per includere il `jquery.ui.datepicker-nw.js` file in tutti i file che utilizzano il datepicker. Il datepicker viene utilizzato nei file seguenti:

   * `js/runtime/views/outofoffice.js`
   * `js/runtime/views/searchtemplatedetails.js`

   Il codice di esempio seguente mostra come aggiungere la voce jquery.ui.datepicker-nw.js:

   ```json
   //Original Code
   define([
       'jquery',
       'underscore',
       'backbone',
       'jqueryui',
       'jqueryuidatepickerja',
       'jqueryuidatepickerde',
       'jqueryuidatepickerfr',
       'slimscroll',
       'usersearchview',
       'logmanagerutil',
       'loggerutil'
   ], function ($, _, Backbone, jQueryUI, jQueryUIDatePickerJA, jQueryUIDatePickerDE, jQueryUIDatePickerFR, slimScroll, UserSearch, LogManager, Logger) {
   ```

   ```json
   // Code with Date Picker alias for new language
   define([
       'jquery',
       'underscore',
       'backbone',
       'jqueryui',
       'jqueryuidatepickerja',
       'jqueryuidatepickerde',
       'jqueryuidatepickerfr',
       'jqueryuidatepickernw', // Date Picker alias
       'slimscroll',
       'usersearchview',
       'logmanagerutil',
       'loggerutil'
   ], function ($, _, Backbone, jQueryUI, jQueryUIDatePickerJA, jQueryUIDatePickerDE, jQueryUIDatePickerFR, jQueryUIDatePickerNW, slimScroll, UserSearch, LogManager, Logger) {
   ```

1. In tutti i file che utilizzano l&#39;API datepicker, modificate le impostazioni predefinite dell&#39;API datepicker. L&#39;API datepicker viene utilizzata nei file seguenti:

   * apps\ws\js\runtime\views\searchtemplatedetails.js
   * apps\ws\js\runtime\views\outofoffice.js

   Modificate il codice seguente per aggiungere la nuova impostazione internazionale:

   ```javascript
   if (locale === 'ja-JP') {
      $.datepicker.setDefaults($.datepicker.regional.ja);
   } else if (locale === 'de-DE') {
      $.datepicker.setDefaults($.datepicker.regional.de);
   } else if (locale === 'fr-FR') {
      $.datepicker.setDefaults($.datepicker.regional.fr);
   } else {
      $.datepicker.setDefaults($.datepicker.regional['']);
   }
   ```

   ```javascript
   if (locale === 'ja-JP') {
       $.datepicker.setDefaults($.datepicker.regional.ja);
   } else if (locale === 'de-DE') {
       $.datepicker.setDefaults($.datepicker.regional.de);
   } else if (locale === 'fr-FR') {
       $.datepicker.setDefaults($.datepicker.regional.fr);
   } else if (locale === 'nw') {
       $.datepicker.setDefaults($.datepicker.regional.nw);
   } else {
       $.datepicker.setDefaults($.datepicker.regional['']);
   }
   ```
