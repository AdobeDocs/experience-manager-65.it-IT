---
title: Debug di moduli HTML5
seo-title: Debug di moduli HTML5
description: L'elenco dei documenti consente di risolvere diversi problemi noti.
seo-description: L'elenco dei documenti consente di risolvere diversi problemi noti.
uuid: df1835aa-6033-4ecb-97c8-4c3b7b96b943
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5260d981-da40-40ab-834e-88e091840813
translation-type: tm+mt
source-git-commit: 998a127ce00c6cbb3db3a81d8a89d97ab9ef7469
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 1%

---


# Debug di moduli HTML5 {#debugging-html-forms}

Questo documento include diversi scenari di risoluzione dei problemi. Per ogni scenario, vengono forniti alcuni passaggi per risolvere il problema. Segui questi passaggi e, se il problema persiste, configura il logger per ottenere e rivedere i registri per individuare eventuali errori o avvisi. Per ulteriori dettagli sulla registrazione dei moduli HTML5, vedere [Generazione di registri per i moduli](/help/forms/using/enable-logs.md)HTML5.

## Problema: Quando si esegue il rendering del modulo, viene visualizzata la pagina di eccezione org.apache.sling.api.SlingException {#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page}

Nei dettagli dell&#39;eccezione, cercare la parola **causata da**.

È probabile che uno o più parametri nell’URL non siano corretti.

Controllate i seguenti parametri:

<table>
 <tbody>
  <tr>
   <td><strong>Parametro</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>template</td>
   <td>Nome del file del modello</td>
  </tr>
  <tr>
   <td>contentRoot</td>
   <td>Percorso in cui risiedono il modello e le risorse associate</td>
  </tr>
  <tr>
   <td>dataRef</td>
   <td>Percorso assoluto del file di dati unito al modello.<br /> Nota: Percorso definisce il percorso assoluto del file di dati.</td>
  </tr>
  <tr>
   <td>data</td>
   <td>Byte di dati codificati UTF-8 uniti al modello.</td>
  </tr>
 </tbody>
</table>

## Problema: Impossibile eseguire il rendering di un modulo (viene visualizzato un messaggio di errore) {#problem-unable-to-render-form}

1. Verificate che i parametri specificati siano corretti. Per informazioni dettagliate sui parametri, consultate Parametri di [rendering](#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page).
1. Accedete a CRX Package Manager (all&#39;indirizzo https://&lt;server>:&lt;porta>/crx/packmgr/index.jsp) e verificate che i pacchetti seguenti siano installati correttamente:

   * adobe-lc-forms-content-pkg-&lt;versione>.zip
   * adobe-lc-forms-runtime-pkg-&lt;versione>.zip

1. Accedete alla console Web di CQ (console Felix) all&#39;indirizzo https://&lt;server>:&lt;porta>/sistema/console/bundle.

   Verificate che lo stato dei seguenti bundle sia &quot;attivo&quot;:

   * scala-lang.bundle [osgi]

   (com.adobe.livecyclescala-lang.bundle)

   *  Modulo di rendering Forms XFA Adobe

   (com.adobe.livecycle.adobe-lc-forms-core)

   *  Adobe XFA Forms LC Connector

   (com.adobe.livecycle.adobe-lc-forms-lc-Connector)

## Problema: Rendering del modulo senza stili {#problem-form-renders-without-styles}

1. Nel browser, aprite **Strumenti** per sviluppatori. Verifica che profile.css sia disponibile.
1. Se il file profile.css non è disponibile, accedete a CRX DE all&#39;indirizzo https://&lt;server>:&lt;porta>/crx/de.
1. Nella gerarchia delle cartelle a sinistra, andate a /etc/clientlibs/fd/xfaforms/. Aprite i file css.txt elencati nelle cartelle.

   * profilo
   * runtime
   * scrollnav
   * toolbar
   * xfalib

1. Verificate che i file citati in css.txt siano presenti in CRX DE lite all&#39;indirizzo /libs/fd/xfaforms/clientlibs/xfalib/css.

   ```css
   #base=css
   application.css
   dialog.css
   datepicker.css
   scribble.css
   listboxwidget.css
   ```

1. Se i file indicati non sono disponibili, installate di nuovo il pacchetto adobe-lc-forms-runtime-pkg-&lt;versione>.zip.

### Problema: Errore imprevisto {#problem-unexpected-error-encountered}

1. Nell&#39;URL del modulo, aggiungere un parametro di query debugClientLibs e impostarne il valore su true (ad esempio: https://&lt;server>:&lt;porta>/content/xfaforms/profiles/test.html?contentRoot=&lt;percorso>&amp;template=&lt;nome del file xdp>&amp;log=1-a9-b9-c9&amp;debugClientLibs=true)
1. Nel browser desktop come Chrome, andate a Strumenti per sviluppatori -> Console.
1. Aprire i registri per identificare il tipo di errore. Per informazioni dettagliate sui registri, vedere [registri per i moduli](/help/forms/using/enable-logs.md)HTML5.
1. Vai a Strumenti per sviluppatori > Console. Utilizzare la traccia dello stack per individuare il codice che causa l&#39;errore. Eseguire il debug dell&#39;errore per risolvere il problema.

   >[!NOTE]
   >
   >Se si verifica un errore di script, verificare se lo stesso problema si verifica anche durante la rappresentazione PDF del modulo. In caso affermativo, la logica di script del modulo presenta un problema.

## Problema: Impossibile inviare il modulo {#problem-unable-to-submit-the-form}

1. Verificate di disporre dei diritti di accesso al server AEM e di essere connessi al server.
1. Verificate che il parametro submitUrl sia corretto.
1. Abilitare i registri lato client come indicato in [Registri per i moduli](/help/forms/using/enable-logs.md) HTML5 utilizzando l&#39;opzione di debug come **1-a5-b5-c5**. Quindi, eseguite il rendering del modulo e fate clic su Invia. Aprite la console di debug del browser e verificate se si è verificato un errore.
1. Individuare i registri del server come indicato in [Registri per i moduli](/help/forms/using/enable-logs.md)HTML5. Verificare se si è verificato un errore nei registri del server durante l&#39;invio.

## Problema: I messaggi di errore localizzati non vengono visualizzati {#problem-localized-error-messages-do-not-display}

1. Eseguire il rendering del modulo con il parametro di query aggiuntivo **debugClientLibs=true** nel browser desktop, quindi passare a Strumenti sviluppatore -> Risorse e verificare il file I18N.css.
1. Se il file non è disponibile, accedete a CRX DE all&#39;indirizzo https://&lt;server>:&lt;porta>/crx/de.
1. Nella gerarchia delle cartelle a sinistra, andate a /libs/fd/xfaforms/clientlibs/I18N e verificate che siano presenti i file e le cartelle seguenti:

   * Namespace.js
   * LogMessages.js
   * Cartelle per le lingue

1. Se uno dei file o delle cartelle di cui sopra non esiste, installate di nuovo il pacchetto **adobe-lc-forms-runtime-pkg-&lt;versione>.zip** .
1. Individuate la cartella che ha lo stesso nome delle impostazioni internazionali e verificarne il contenuto. La cartella deve contenere i file seguenti:

   * I18N.js
   * js.txt

1. Controllate il contenuto di js.txt e accertatevi che contenga le voci seguenti.

   ```javascript
   ../Namespace.js
   I18N.js
   ../LogMessages.js
   ```

## Problema: Immagine che non viene visualizzata {#problem-image-not-showing-up}

1. Accertatevi che l’URL dell’immagine sia corretto.
1. Verificate se il browser supporta questo tipo di immagine.
1. Nei dettagli dell&#39;eccezione, cercare la parola **causata da**.

   È probabile che uno o più parametri nell’URL non siano corretti.

   Controllate i seguenti parametri:
Testo del passaggio

<table>
 <tbody>
  <tr>
   <td><strong>Parametro</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>template</td>
   <td>Nome del file del modello</td>
  </tr>
  <tr>
   <td>contentRoot</td>
   <td>Percorso in cui risiedono il modello e le risorse associate</td>
  </tr>
  <tr>
   <td>dataRef</td>
   <td>Percorso assoluto del file di dati unito al modello.<br /> Nota: Percorso definisce il percorso assoluto del file di dati.</td>
  </tr>
  <tr>
   <td>data</td>
   <td>Byte di dati codificati UTF-8 uniti al modello.</td>
  </tr>
 </tbody>
</table>

1. Nel browser desktop, accedete a Strumenti per sviluppatori -> Risorse.

   Se l&#39;immagine viene visualizzata, selezionate Cornici a sinistra.
