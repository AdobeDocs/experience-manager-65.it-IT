---
title: Modifica delle impostazioni locali dell'interfaccia utente di AEM Forms Workspace
description: Come modificare l’area di lavoro di AEM Forms per localizzare testo, categorie compresse, code e processi e il selettore data sull’interfaccia.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 9a069486-02a8-4058-adfb-4e0e49d8c0cf
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 0%

---

# Modifica delle impostazioni locali dell&#39;interfaccia utente di AEM Forms Workspace{#changing-the-locale-of-aem-forms-workspace-user-interface}

AEM Forms Workspace offre supporto integrato per le lingue inglese, francese, tedesco e giapponese. Consente inoltre di localizzare l’interfaccia utente dell’area di lavoro di AEM Forms in qualsiasi altra lingua.

Per localizzare l’interfaccia utente dell’area di lavoro di AEM Forms nella lingua desiderata:

* Localizza il testo dell’area di lavoro di AEM Forms.
* Localizzare categorie, code e processi compressi.
* Selettore data localizzazione

Prima di eseguire i passaggi precedenti, assicurati di seguire i passaggi elencati in [Passaggi generici per la personalizzazione dell&#39;area di lavoro di AEM Forms](../../forms/using/generic-steps-html-workspace-customization.md).

>[!NOTE]
>
>Per modificare la lingua della schermata di accesso dell&#39;area di lavoro di AEM Forms, vedere [Creazione di una schermata di accesso](../../forms/using/creating-new-login-screen.md).

## Localizzazione del testo {#localizing-text}

Eseguire la procedura seguente per aggiungere il supporto per una lingua *New* e il codice delle impostazioni locali del browser *nw*.

1. Accedi a CRXDE Lite.
URL predefinito di CRXDE Lite: `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. Passare alla posizione `apps/ws/locales` e creare una cartella `nw.`
1. Copiare il file `translation.json` dal percorso `/apps/ws/locales/en-US` al percorso `/apps/ws/locales/nw`.
1. Passare a `/apps/ws/locales/nw` e aprire `translation.json` per la modifica. Apporta al file translation.json le modifiche specifiche per le impostazioni internazionali.

   Gli esempi seguenti contengono il file translation.json per le lingue inglese e francese dell’area di lavoro di AEM Forms.

   ![translation_json_in_en](assets/translation_json_in_en.png) ![translation_json_in_fr](assets/translation_json_in_fr.png)

## Localizzazione di categorie, code e processi compressi {#localizing-collapsed-categories-queues-and-processes}

AEM Forms Workspace utilizza le immagini per visualizzare intestazioni di categorie, code e processi. Per localizzare queste intestazioni è necessario un pacchetto di sviluppo. Per informazioni dettagliate sulla creazione di un pacchetto di sviluppo, vedere [Creazione del codice dell&#39;area di lavoro di AEM Forms.](introduction-customizing-html-workspace.md#building-html-workspace-code)

Nei passaggi seguenti si presume che i nuovi file immagine localizzati siano *Categories_nw.png*, *Queue_nw.png* e *Processes_nw.png*. La larghezza consigliata delle immagini deve essere impostata su 19 pixel.

>[!NOTE]
>
>Per trovare il codice di lingua del browser. Apri `https://'[server]:[port]'/lc/libs/ws/Locale.html`.

![immagine_pannelli_compressi](assets/collapsing_panels_image.png)

Per localizzare le immagini, effettuare le seguenti operazioni:

1. Utilizzando un client WebDAV, inserire i file immagine nella cartella */apps/ws/images*.
1. Passa a */apps/ws/css*. Apri *newStyle.css* per la modifica e aggiungi le seguenti voci:

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

1. Esegui tutte le modifiche semantiche elencate nell&#39;articolo [Personalizzazione Workspace](../../forms/using/introduction-customizing-html-workspace.md).
1. Passa alla cartella *js/runtime/utility* e apri il file *usersession.js* per la modifica.
1. Individua il codice elencato nel blocco di codice originale e aggiungi la condizione *lang!== &#39;nw&#39;* all&#39;istruzione if:

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

## Localizzazione selezione data {#localizing-date-picker}

È necessario un pacchetto di sviluppo per localizzare l&#39;API *datepicker*. Per informazioni dettagliate sulla creazione di un pacchetto di sviluppo, vedere [Creazione del codice dell&#39;area di lavoro di AEM Forms](introduction-customizing-html-workspace.md#building-html-workspace-code).

1. Scarica ed estrai il pacchetto dell&#39;interfaccia utente [jQuery](https://jqueryui.com/download/all/), passa a *&lt;pacchetto dell&#39;interfaccia utente jquery estratto>*\jquery-ui-1.10.2.zip\jquery-ui-1.10.2\ui\i18n.
1. Copia il file jquery.ui.datepicker-nw.js per il codice locale nw in apps/ws/js/libs/jqueryui e apporta al file le modifiche specifiche per la lingua.
1. Passare a `apps/ws/js` e aprire il file `jquery.ui.datepicker-nw.js` per la modifica.
1. Nel file main.js, creare un alias per `jquery.ui.datepicker-nw.js.` Il codice per creare un alias per il file `jquery.ui.datepicker-nw.js` è:

   ```javascript
   jqueryuidatepickernw : pathprefix + 'libs/jqueryui/jquery.ui.datepicker-nw'
   ```

1. Utilizzare l&#39;alias `jqueryuidatepickernw` per includere il file `jquery.ui.datepicker-nw.js` in tutti i file che utilizzano datepicker. Il datepicker viene utilizzato nei seguenti file:

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

1. In tutti i file che utilizzano l’API datepicker, modifica le impostazioni API predefinite di datepicker. L’API datepicker viene utilizzata nei seguenti file:

   * apps\ws\js\runtime\views\searchtemplatedetails.js
   * apps\ws\js\runtime\views\outofoffice.js

   Modifica il codice seguente per aggiungere la nuova lingua:

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
