---
title: Modifica delle impostazioni internazionali dell’interfaccia utente di AEM Forms Workspace
seo-title: Changing the locale of AEM Forms workspace user interface
description: Come modificare l’area di lavoro di AEM Forms per localizzare il testo, le categorie compresse, le code e i processi e il selettore data sull’interfaccia.
seo-description: How to modify the AEM Forms workspace to localize text, collapsed categories, queues, and processes, and the date picker on the interface.
uuid: c89ff150-a36e-45cc-99a6-8768dbe58eab
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 89f9d666-28e2-4201-8467-ae90693ca5d2
docset: aem65
exl-id: 9a069486-02a8-4058-adfb-4e0e49d8c0cf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 0%

---

# Modifica delle impostazioni internazionali dell’interfaccia utente di AEM Forms Workspace{#changing-the-locale-of-aem-forms-workspace-user-interface}

Lo spazio di lavoro di AEM Forms supporta le lingue inglese, francese, tedesco e giapponese. Fornisce inoltre la possibilità di localizzare l’interfaccia utente di AEM Forms Workspace in qualsiasi altra lingua.

Per localizzare l’interfaccia utente di AEM Forms Workspace nella lingua desiderata:

* Localizzare il testo dell’area di lavoro di AEM Forms.
* Localizzare categorie, code e processi compressi.
* Localizza selezione data

Prima di eseguire i passaggi precedenti, assicurati di seguire i passaggi elencati in [Passaggi generici per la personalizzazione dell’area di lavoro AEM Forms](../../forms/using/generic-steps-html-workspace-customization.md).

>[!NOTE]
>
>Per modificare la lingua della schermata di accesso di AEM Forms workspace, vedi [Creazione di una nuova schermata di accesso](../../forms/using/creating-new-login-screen.md).

## Localizzazione del testo {#localizing-text}

Esegui i seguenti passaggi per aggiungere il supporto per una lingua *Nuovo* e il codice internazionale del browser *nuovo*.

1. Accedi a CRXDE Lite.
L’URL predefinito di CRXDE Lite è `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. Passa alla posizione `apps/ws/locales` e crea una nuova cartella `nw.`
1. Copia il file `translation.json`dalla posizione `/apps/ws/locales/en-US` in posizione `/apps/ws/locales/nw` .
1. Passa a `/apps/ws/locales/nw` e aperto `translation.json` per la modifica. Apporta modifiche specifiche alle impostazioni internazionali del file translation.json.

   Gli esempi seguenti contengono il file translation.json per le impostazioni internazionali inglese e francese dell&#39;area di lavoro AEM Forms.

   ![translation_json_in_en](assets/translation_json_in_en.png) ![translation_json_in_fr](assets/translation_json_in_fr.png)

## Localizzazione di categorie, code e processi compressi {#localizing-collapsed-categories-queues-and-processes}

L’area di lavoro di AEM Forms utilizza immagini per visualizzare intestazioni di categorie, code e processi. Per localizzare queste intestazioni è necessario un pacchetto di sviluppo. Per informazioni dettagliate sulla creazione del pacchetto di sviluppo, vedi [Creazione del codice dell’area di lavoro di AEM Forms.](introduction-customizing-html-workspace.md#building-html-workspace-code)

Nei passaggi seguenti, si presume che i nuovi file di immagine localizzati siano *Categories_nw.png*, *Queue_nw.png* e *Processes_nw.png*. La larghezza consigliata delle immagini è 19 px.

>[!NOTE]
>
>Per trovare il codice internazionale della lingua del browser. Apri `https://'[server]:[port]'/lc/libs/ws/Locale.html`.

![comprimi_pannelli_immagine](assets/collapsing_panels_image.png)

Esegui i seguenti passaggi per localizzare le immagini:

1. Utilizzando un client WebDAV, inserire i file di immagine nel */apps/ws/images* cartella.
1. Passa a */apps/ws/css*. Apri *newStyle.css* per modificare e aggiungere le voci seguenti:

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

1. Esegui tutte le modifiche semantiche elencate nel [Personalizzazione di Workspace](../../forms/using/introduction-customizing-html-workspace.md) articolo.
1. Passa a *js/runtime/utility* e apri la *usersession.js* file da modificare.
1. Individua il codice elencato nel blocco di codice originale e aggiungi una condizione *lang!== &#39;nw&#39;* all’istruzione if:

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

È necessario un pacchetto di sviluppo per localizzare il *datepicker* API. Per informazioni dettagliate sulla creazione del pacchetto di sviluppo, vedi [Creazione del codice dell’area di lavoro di AEM Forms](introduction-customizing-html-workspace.md#building-html-workspace-code).

1. Scarica ed estrai [Pacchetto interfaccia utente jQuery](https://jqueryui.com/download/all/), passa a *&lt;extracted jquery=&quot;&quot; ui=&quot;&quot; package=&quot;&quot;>*\jquery-ui-1.10.2.zip\jquery-ui-1.10.2\ui\i18n.
1. Copia il file jquery.ui.datepicker-nw.js per il codice internazionale ora in apps/ws/js/libs/jqueryui e apporta modifiche specifiche alle impostazioni internazionali del file.
1. Passa a `apps/ws/js` e aprire `jquery.ui.datepicker-nw.js` file da modificare.
1. Nel file main.js crea un alias per `jquery.ui.datepicker-nw.js.` Codice per creare un alias per il `jquery.ui.datepicker-nw.js` file:

   ```javascript
   jqueryuidatepickernw : pathprefix + 'libs/jqueryui/jquery.ui.datepicker-nw'
   ```

1. Usa alias `jqueryuidatepickernw` per includere `jquery.ui.datepicker-nw.js` in tutti i file che utilizzano datepicker. Il datepicker viene utilizzato nei file seguenti:

   * `js/runtime/views/outofoffice.js`
   * `js/runtime/views/searchtemplatedetails.js`

   Il codice di esempio seguente mostra come aggiungere la voce di jquery.ui.datepicker-nw.js:

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

1. In tutti i file che utilizzano l’API datepicker, modifica le impostazioni predefinite dell’API datepicker. L’API del datepicker viene utilizzata nei file seguenti:

   * apps\ws\js\runtime\views\searchtemplatedetails.js
   * apps\ws\js\runtime\views\outofoffice.js

   Modifica il codice seguente per aggiungere le nuove impostazioni internazionali:

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
