---
title: Debug dei moduli di HTML5
seo-title: Debugging HTML5 forms
description: L'elenco dei documenti descrive i passaggi necessari per risolvere i vari problemi noti.
seo-description: The document list steps to troubleshoot various known issues.
uuid: df1835aa-6033-4ecb-97c8-4c3b7b96b943
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5260d981-da40-40ab-834e-88e091840813
feature: Mobile Forms
exl-id: 7330c03f-7102-43c0-aac6-825cce8a113d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 1%

---

# Debug dei moduli di HTML5 {#debugging-html-forms}

Questo documento include diversi scenari di risoluzione dei problemi. Per ogni scenario, vengono forniti alcuni passaggi per risolvere il problema. Segui questi passaggi e, se il problema persiste, configura il logger per ottenere e rivedere i registri in caso di errori/avvisi. Per ulteriori dettagli sulla registrazione dei moduli in HTML5, consulta [Generazione di registri per i moduli HTML5](/help/forms/using/enable-logs.md).

## Problema: Quando esegui il rendering del modulo, visualizzo la pagina di eccezione org.apache.sling.api.SlingException {#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page}

Nei dettagli dell&#39;eccezione, cerca la parola **causato da**.

È probabile che uno o più parametri nell’URL non siano corretti.

Verifica i seguenti parametri:

<table>
 <tbody>
  <tr>
   <td><strong>Parametro</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>template</td>
   <td>Il nome del file del modello</td>
  </tr>
  <tr>
   <td>contentRoot</td>
   <td>Percorso in cui risiedono il modello e le risorse associate</td>
  </tr>
  <tr>
   <td>dataRef</td>
   <td>Percorso assoluto del file di dati unito al modello.<br /> Nota: Il percorso definisce il percorso assoluto del file di dati.</td>
  </tr>
  <tr>
   <td>data</td>
   <td>Byte di dati codificati UTF-8 uniti al modello.</td>
  </tr>
 </tbody>
</table>

## Problema: Impossibile eseguire il rendering di un modulo (viene visualizzato un messaggio di errore) {#problem-unable-to-render-form}

1. Assicurati che i parametri specificati siano corretti. Per informazioni dettagliate sui parametri, vedi [Parametri di rendering](#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page).
1. Accedi a CRX Package Manager (all&#39;indirizzo https://)&lt;server>:&lt;port>/crx/packmgr/index.jsp) e controlla se i seguenti pacchetti sono installati correttamente:

   * adobe-lc-forms-content-pkg-&lt;version>.zip
   * adobe-lc-forms-runtime-pkg-&lt;version>.zip

1. Accedi alla console Web CQ (console Felix) all&#39;indirizzo https://&lt;server>:&lt;port>/system/console/bundles.

   Assicurati che lo stato dei seguenti bundle sia &quot;attivo&quot;:

   * scala-lang.bundle [osgi]

   (com.adobe.livecyclescala-lang.bundle)

   * Adobe XFA Forms Renderer

   (com.adobe.livecycle.adobe-lc-forms-core)

   * Connettore Adobe XFA Forms LC

   (com.adobe.livecycle.adobe-lc-forms-lc-connector)

## Problema: Rendering del modulo senza stili {#problem-form-renders-without-styles}

1. Nel browser, apri **Strumenti per gli sviluppatori**. Assicurati che profile.css sia disponibile.
1. Se il file profile.css non è disponibile, accedi a CRX DE all&#39;indirizzo https://&lt;server>:&lt;port>/crx/de.
1. Nella gerarchia delle cartelle a sinistra, vai a /etc/clientlibs/fd/xfaforms/. Apri i file css.txt elencati nelle cartelle.

   * profilo
   * runtime
   * scorrimento
   * toolbar
   * xfalib

1. Verifica che i file menzionati all&#39;interno di css.txt siano presenti in CRX DE lite in /libs/fd/xfaforms/clientlibs/xfalib/css.

   ```css
   #base=css
   application.css
   dialog.css
   datepicker.css
   scribble.css
   listboxwidget.css
   ```

1. Se i file menzionati non sono disponibili, installa adobe-lc-forms-runtime-pkg-&lt;version>pacchetto zip di nuovo.

### Problema: Errore imprevisto {#problem-unexpected-error-encountered}

1. Nell’URL del modulo, aggiungere un parametro di query debugClientLibs e impostarne il valore su true (ad esempio: https://&lt;server>:&lt;port>/content/xfaforms/profiles/test.html?contentRoot=&lt;some path=&quot;&quot;>&amp;template=&lt;name of=&quot;&quot; xdp=&quot;&quot; file=&quot;&quot;>&amp;log=1-a9-b9-c9&amp;debugClientLibs=true)
1. Nel browser desktop come chrome, vai a Strumenti per sviluppatori -> Console.
1. Apri i registri per identificare il tipo di errore. Per informazioni dettagliate sui registri, consulta [registri di HTML5 forms](/help/forms/using/enable-logs.md).
1. Vai a Strumenti per sviluppatori -> Console. Utilizza la traccia dello stack per individuare il codice che sta causando l’errore. Esegui il debug dell&#39;errore per risolvere il problema.

   >[!NOTE]
   >
   >Se si tratta di un errore di script, verificare se lo stesso problema si verifica anche durante il rendering del modulo in PDF. Se sì, si verifica un problema nella logica di script del modulo.

## Problema: Impossibile inviare il modulo {#problem-unable-to-submit-the-form}

1. Assicurati di disporre dei diritti per accedere al server AEM e di essere connesso al server.
1. Verifica che il parametro submitUrl sia corretto.
1. Abilita i registri lato client come indicato in [Registri per i moduli HTML5](/help/forms/using/enable-logs.md) utilizzo dell&#39;opzione di debug come **1-a5-b5-c5**. Quindi, esegui il rendering del modulo e fai clic su Invia. Apri la console di debug del browser e controlla se si verifica un errore.
1. Individua i registri del server come indicato in [Registri per i moduli HTML5](/help/forms/using/enable-logs.md). Controlla se si è verificato un errore nei log del server durante l&#39;invio.

## Problema: I messaggi di errore localizzati non vengono visualizzati {#problem-localized-error-messages-do-not-display}

1. Eseguire il rendering del modulo con un parametro di query aggiuntivo **debugClientLibs=true** nel browser desktop, quindi vai a Strumenti di sviluppo -> Risorse e controlla il file I18N.css.
1. Se il file non è disponibile, accedi a CRX DE all&#39;indirizzo https://&lt;server>:&lt;port>/crx/de.
1. Nella gerarchia delle cartelle a sinistra, vai a /libs/fd/xfaforms/clientlibs/I18N e assicurati che siano presenti i seguenti file e cartelle:

   * Namespace.js
   * LogMessages.js
   * Cartelle per le lingue

1. Se uno dei file o delle cartelle di cui sopra non esiste, installa il **adobe-lc-forms-runtime-pkg-&lt;version>.zip** di nuovo.
1. Passa alla cartella che ha lo stesso nome delle impostazioni internazionali e ne controlla il contenuto. La cartella deve contenere i file seguenti:

   * I18N.js
   * js.txt

1. Controlla il contenuto di js.txt e assicurati che contenga le seguenti voci.

   ```javascript
   ../Namespace.js
   I18N.js
   ../LogMessages.js
   ```

## Problema: Immagine non visualizzata {#problem-image-not-showing-up}

1. Assicurati che l&#39;URL dell&#39;immagine sia corretto.
1. Controlla se il browser supporta questo tipo di immagine.
1. Nei dettagli dell&#39;eccezione, cerca la parola **causato da**.

   È probabile che uno o più parametri nell’URL non siano corretti.

   Verifica i seguenti parametri: Testo del passaggio

<table>
 <tbody>
  <tr>
   <td><strong>Parametro</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>template</td>
   <td>Il nome del file del modello</td>
  </tr>
  <tr>
   <td>contentRoot</td>
   <td>Percorso in cui risiedono il modello e le risorse associate</td>
  </tr>
  <tr>
   <td>dataRef</td>
   <td>Percorso assoluto del file di dati unito al modello.<br /> Nota: Il percorso definisce il percorso assoluto del file di dati.</td>
  </tr>
  <tr>
   <td>data</td>
   <td>Byte di dati codificati UTF-8 uniti al modello.</td>
  </tr>
 </tbody>
</table>

1. Nel browser desktop, accedi a Strumenti per sviluppatori -> Risorse.

   Se l&#39;immagine viene visualizzata, seleziona il lato sinistro in Frame.
