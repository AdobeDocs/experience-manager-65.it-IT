---
title: Verifica automatica dei moduli adattivi
seo-title: Verifica automatica dei moduli adattivi
description: Utilizzando Calvin è possibile creare casi di test in CRXDE ed eseguire i test dell’interfaccia utente direttamente nel browser web per testare a fondo i moduli adattivi.
seo-description: Utilizzando Calvin è possibile creare casi di test in CRXDE ed eseguire i test dell’interfaccia utente direttamente nel browser web per testare a fondo i moduli adattivi.
uuid: 7bf4fc8f-96df-4407-8d10-cf18880518bd
contentOwner: gtalwar
content-type: reference
topic-tags: adaptive_forms, develop
discoiquuid: 1cb54c8a-9322-4b5a-b5a7-0eef342cee54
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1285'
ht-degree: 1%

---


# Verifica automatica dei moduli adattivi{#automate-testing-of-adaptive-forms}

## Panoramica {#overview}

I moduli adattivi sono parte integrante delle interazioni dei clienti. È importante testare i moduli adattivi con ogni modifica apportata, ad esempio durante il rollout di un nuovo fix pack o la modifica di una regola nel modulo. Tuttavia, la verifica funzionale dei moduli adattivi e di tutti i campi in essi contenuti può risultare noiosa.

Calvin consente di automatizzare i test dei moduli adattivi nel browser web. Calvin utilizza l&#39;interfaccia utente di [Hobbes](/help/sites-developing/hobbes.md) per eseguire i test e fornisce i seguenti strumenti:

* API JavaScript per la creazione di test.
* Interfaccia utente per l’esecuzione di test.

Utilizzando Calvin, puoi creare casi di test in CRXDE ed eseguire i test dell’interfaccia utente direttamente nel browser web per testare a fondo i seguenti aspetti dei moduli adattivi:

<table>
 <tbody>
  <tr>
   <td><strong>Aspetto del modulo adattivo da testare</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>Precompilare l’esperienza di un modulo adattivo</td>
   <td>
    <ul>
     <li>Il modulo viene precompilato come previsto in base al tipo di modello dati?</li>
     <li>I valori predefiniti degli oggetti modulo vengono precompilati come previsto?</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Inviare l’esperienza di un modulo adattivo</td>
   <td>
    <ul>
     <li>I dati corretti vengono generati durante l’invio?</li>
     <li>Il modulo viene convalidato nuovamente sul server durante l’invio?</li>
     <li>L’azione di invio è configurata per il modulo in esecuzione?</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Regole di espressione</p> <p> </p> </td>
   <td>
    <ul>
     <li>Le espressioni associate agli oggetti modulo, come calculate, visibili, eseguono gli script dopo l'uscita da un campo, in esecuzione dopo aver eseguito le relative operazioni dell'interfaccia utente?<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>Convalida</td>
   <td>
    <ul>
     <li>Le convalide dei campi vengono eseguite come previsto dopo l’esecuzione delle operazioni?</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Caricamento pigro</p> <p> </p> </td>
   <td>
    <ul>
     <li>Quando si fa clic su schede (o su qualsiasi elemento di navigazione di un pannello), l’HTML viene recuperato dal server in base alla configurazione di caricamento pigro?</li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Interazione interfaccia</p> </td>
   <td>
    <ul>
     <li><a href="https://helpx.adobe.com/aem-forms/6-3/calvin-sdk-javascript-api/calvin.html#toc2__anchor" target="_blank">Verifica dell’interazione dell’interfaccia utente con gli oggetti modulo adattivo</a></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Prerequisiti {#prerequisites}

Prima di utilizzare questo articolo per creare i casi di test, è necessario conoscere quanto segue:

* Creazione di suite di test ed esecuzione di casi di test utilizzando [Hobbes](https://docs.adobe.com/docs/en/aem/6-3/develop/components/hobbes.html)
* [API JavaScript di Hobbes](https://docs.adobe.com/docs/en/aem/6-2/develop/ref/test-api/index.html)
* [API JavaScript di Calvin](https://helpx.adobe.com/aem-forms/6-3/calvin-sdk-javascript-api/calvin.html)

## Esempio: Crea una suite di test per un modulo adattivo utilizzando Hobbes come framework di test {#example-create-a-test-suite-for-an-adaptive-form-using-hobbes-as-testing-framework}

L’esempio seguente illustra la creazione di una suite di test per il test di più moduli adattivi. È necessario creare un test case separato per ciascun modulo da sottoporre a test. Seguendo passaggi simili a quelli seguenti e modificando il codice JavaScript al passaggio 11, puoi creare una tua suite di test per testare i moduli adattivi.

1. Passa a CRXDE Lite nel browser Web: `https://'[server]:[port]'/crx/de`.
1. Fai clic con il pulsante destro del mouse sulla sottocartella /etc/clientlibs e fai clic su **Crea** > **Crea nodo**. Immetti un nome (qui afTestRegistration), specifica il tipo di nodo come cq:ClientLibraryFolder, quindi fai clic su **OK.**

   La cartella clientlibs contiene l&#39;aspetto di registrazione dell&#39;applicazione (JS e Init). È consigliabile registrare tutti gli oggetti delle suite di test Hobbes specifici per un modulo nella cartella clientlibs.

1. Specifica i seguenti valori di proprietà nel nodo appena creato (qui afTestRegistration), quindi fai clic su **Salva tutto**. Queste proprietà consentono ad Hobbes di riconoscere la cartella come un test. Per riutilizzare questa libreria client come dipendenza in altre librerie client, denominala come granite.testing.calvin.test.

<table>
 <tbody>
  <tr>
   <td>Proprietà</td>
   <td>Tipo</td>
   <td>Valore</td>
  </tr>
  <tr>
   <td><p>categorie</p> </td>
   <td><p>Stringa[]</p> </td>
   <td><p>granite.testing.hobbes.test, granite.testing.calvin.test</p> </td>
  </tr>
  <tr>
   <td><p>dipendenze</p> </td>
   <td><p>Stringa[]</p> </td>
   <td><p>granite.testing.hobbes.testrunner, granite.testing.calvin, apps.testframework.all</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>La clientlib granite.testing.calvin.af contiene tutte le API dei moduli adattivi. Queste API fanno parte dello spazio dei nomi calvin.

![1_aftestregistration](assets/1_aftestregistration.png)

1. Fai clic con il pulsante destro del mouse sul nodo del test (qui **afTestRegistration)**, quindi fai clic su **Crea** > **Crea file**. Denomina il file js.txt e fai clic su **OK**.
1. Nel file js.txt, aggiungi il seguente testo:

   ```javascript
   #base=.
   js.txt
   ```

1. Fai clic su **Salva tutto**, quindi chiudi il file js.txt.
1. Fai clic con il pulsante destro del mouse sul nodo del test (qui **afTestRegistration)** e fai clic su **Crea** > **Crea file**. Denomina il file init.js e fai clic su **OK**.
1. Copia il seguente codice nel file init.js e fai clic su **Salva tutto**:

   ```javascript
   (function(window, hobs) {
       'use strict';
       window.testsuites = window.testsuites || {};
     // Registering the test form suite to the sytem
     // If there are other forms, all registration should be done here
       window.testsuites.testForm = new hobs.TestSuite("Adaptive Form - Demo Test", {
           path: '/etc/clientlibs/afTestRegistration/init.js',
           register: true
       });
    // window.testsuites.testForm1 = new hobs.TestSuite("testForm1");
   }(window, window.hobs));
   ```

   Il codice riportato sopra crea una suite di test denominata **Modulo adattivo - Test demo**. Per creare una suite di test con un nome diverso, modifica il nome di conseguenza.

1. Fai clic su **Crea** > **Crea nodo** per creare un nodo sotto la cartella clientlib per ciascun modulo da testare. Questo esempio utilizza un nodo denominato **testForm** per testare un modulo adattivo denominato **testForm**. Specifica le seguenti proprietà e fai clic su **OK**:

   * Nome: testForm (nome del modulo)
   * Tipo: cq:ClientLibraryFolder

1. Aggiungi le seguenti proprietà al nodo appena creato (qui testForm) per testare un modulo adattivo:

   | **Proprietà** | **Tipo** | **Valore** |
   |---|---|---|
   | categorie | Stringa[] | granite.testing.hobbes.test, granite.testing.hobbes.test.test.testForm |
   | dipendenze | Stringa[] | granite.testing.calvin.tests |

   >[!NOTE]
   >
   >In questo esempio viene utilizzata una dipendenza da client lib granite.testing.calvin.test per una migliore gestione. Questo esempio aggiunge anche una categoria client lib, &quot;granite.testing.hobbes.test.testForm&quot; per riutilizzare questa libreria client, se necessario.

   ![2_testformproperties](assets/2_testformproperties.png)

1. Fare clic con il pulsante destro del mouse sulla cartella creata per il modulo di test (qui testForm) e selezionare **Crea** > **Crea file**. Denomina il file scriptingTest.js e aggiungi il seguente codice al file, quindi fai clic su **Salva tutto.**

   Per utilizzare il codice seguente per testare un altro modulo adattivo, modifica il percorso e il nome del modulo in **navigaA** (righe 11, 36 e 62) e i rispettivi casi di test. Per ulteriori informazioni sulle API per il test di diversi aspetti dei moduli e degli oggetti modulo, vedere [API Calvin](https://helpx.adobe.com/aem-forms/6-3/calvin-sdk-javascript-api/calvin.html).

   ```javascript
   (function(window, hobs) {
       'use strict';
   
    var ts = new hobs.TestSuite("Script Test", {
           path: '/etc/clientlibs/testForm/scriptingTest.js',
     register: false
    })
   
       .addTestCase(new hobs.TestCase("Checking execution of calculate script")
           // navigate to the testForm which is to be tested
           .navigateTo("/content/forms/af/testForm.html?wcmmode=disabled")
           // check if adaptive form is loaded
           .asserts.isTrue(function () {
               return calvin.isFormLoaded()
           })
           .execSyncFct(function () {
               // create a spy before checking for the expression
               calvin.spyOnExpression("panel1.textbox1");
               // setValue would trigger enter, set the value and exit from the field
               calvin.setValueInDOM("panel1.textbox", "5");
           })
           // if the calculate expression was setting "textbox1" value to "5", let's also check that
           .asserts.isTrue(function () {
               return calvin.isExpressionExecuted("panel1.textbox1", "Calculate");
           })
           .execSyncFct(function () {
               calvin.destroySpyOnExpression("panel1.textbox1");
           })
           .asserts.isTrue(function () {
               return calvin.model("panel1.textbox1").value == "5"
           })
       )
   
       .addTestCase(new hobs.TestCase("Calculate script Test")
           // navigate to the testForm which is to be tested
           .navigateTo("/content/forms/af/cal/demoform.html?wcmmode=disabled&dataRef=crx:///content/forms/af/cal/prefill.xml")
           // check if adaptive form is loaded
           .asserts.isTrue(function () {
               return calvin.isFormLoaded()
           })
   
           .execSyncFct(function () {
               // create a spy before checking for the expression
               calvin.spyOnExpression("panel2.panel1488218690733.downPayment");
               // setValue would trigger enter, set the value and exit from the field
               calvin.setValueInDOM("panel2.panel1488218690733.priceProperty", "1000000");
           })
           .asserts.isTrue(function () {
               return calvin.isExpressionExecuted("panel2.panel1488218690733.downPayment", "Calculate");
           })
           .execSyncFct(function () {
               calvin.destroySpyOnExpression("panel2.panel1488218690733.downPayment");
           })
           .asserts.isTrue(function () {
               // if the calculate expression was setting "downPayment" value to "10000", let's also check that
      return calvin.model("panel2.panel1488218690733.downPayment").value == 10000
           })
       )
   
       .addTestCase(new hobs.TestCase("Checking execution of Value commit script")
           // navigate to the testForm which is to be tested
           .navigateTo("/content/forms/af/cal/demoform.html?wcmmode=disabled&dataRef=crx:///content/forms/af/cal/prefill.xml")
           // check if adaptive form is loaded
           .asserts.isTrue(function () {
               return calvin.isFormLoaded()
           })
   
           .execSyncFct(function () {
               // create a spy before checking for the expression
               calvin.spyOnExpression("panel2.panel1488218690733.priceProperty");
               // setValue would trigger enter, set the value and exit from the field
               calvin.setValueInDOM("panel2.panel1488218690733.priceProperty", "100");
           })
           .asserts.isTrue(function () {
               return calvin.isExpressionExecuted("panel2.panel1488218690733.priceProperty", "Value Commit");
           })
           .execSyncFct(function () {
               calvin.destroySpyOnExpression("panel2.panel1488218690733.priceProperty");
           })
           .asserts.isTrue(function () {
            // if the value commit expression was setting "textbox1488215618594" value to "0", let's also check that
               return calvin.model("panel2.panel1488218690733.textbox1488215618594").value == 0
           })
       );
   
    // register the test suite with testForm
     window.testsuites.testForm.add(ts);
   
    }(window, window.hobs));
   ```

   Viene creato il test case. Procedi con l’esecuzione del test case per testare i moduli adattivi tramite Hobbes. Per i passaggi per l’esecuzione dei casi di test, consulta [Esecuzione di test in Test della propria interfaccia utente tramite l’uso di test automatici](/help/sites-developing/hobbes.md).

Puoi anche installare il pacchetto nel file allegato SampleTestPackage.zip per ottenere gli stessi risultati dei passaggi descritti in Esempio: Crea una suite di test per un modulo adattivo utilizzando Hobbes come framework di test.

[Ottieni file](assets/sampletestpackage.zip)

## Test della vostra interfaccia utente tramite l&#39;uso di test automatici {#testing-your-ui-using-automated-tests}

### Esecuzione di una suite di test singola {#running-a-single-test-suite}

Le suite di test possono essere eseguite singolarmente. Quando esegui una suite di test, la pagina cambia man mano che vengono eseguiti i casi di test e le relative azioni e i risultati vengono visualizzati dopo il completamento del test. Le icone indicano i risultati.

Un’icona a forma di segno di spunta indica un test superato: ![segno di spunta](assets/checkmark.png)

Un&#39;icona &quot;X&quot; indica un test non riuscito: ![croce](assets/cross.png)

Per eseguire una suite di test:

1. Nel pannello Test , tocca o fai clic sul nome del Test Case da eseguire per espandere i dettagli delle azioni.

   ![1_tapnameoftestcase](assets/1_tapnameoftestcase.png)

1. Tocca o fai clic sul pulsante Esegui test . ![raccoglitore](assets/runtestcase.png)

   ![2_clickrun](assets/2_clickrun.png)

1. Il segnaposto viene sostituito con il contenuto della pagina durante l’esecuzione del test.

   ![3_pagecontent](assets/3_pagecontent.png)

1. Rivedi i risultati del Test Case toccando o facendo clic sulla descrizione per aprire il pannello Risultato. Per visualizzare tutti i dettagli, tocca o fai clic sul nome del test case nel pannello Risultato .

   ![4_risultati di revisione](assets/4_reviewresults.png)

I passaggi per testare i moduli adattivi AEM sono simili ai passaggi per testare l’interfaccia utente AEM. Per ulteriori informazioni sulla verifica dei moduli adattivi, consulta i seguenti argomenti in [Verifica dell&#39;interfaccia utente](https://helpx.adobe.com//experience-manager/6-3/help/sites-developing/hobbes.html):

* Visualizzazione delle suite di test
* Esecuzione di più test

## Glossario {#glossary}

<table>
 <tbody>
  <tr>
   <td><strong>Termine</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td><p>Suite di test</p> </td>
   <td><p>Una suite di test è una raccolta di casi di test correlati.</p> </td>
  </tr>
  <tr>
   <td><p>Caso di prova</p> </td>
   <td><p>Un test case rappresenta un'attività eseguita dall'utente utilizzando l'interfaccia utente. Aggiungi i casi di test alla suite di test per testare le attività eseguite dagli utenti.</p> </td>
  </tr>
  <tr>
   <td><p>Azioni</p> </td>
   <td><p>Le azioni sono metodi che eseguono un gesto nell’interfaccia utente, ad esempio fare clic su un pulsante o riempire una casella di input con un valore.</p> <p>I metodi delle classi hobs.actions.Asserts, hobs.actions.Core e hobs.utils.af sono azioni che puoi utilizzare nei test. Tutte le azioni vengono eseguite in modo sincrono.</p> </td>
  </tr>
  <tr>
   <td><p>Ambiente di authoring o pubblicazione</p> </td>
   <td><p>In generale, i moduli possono essere testati nell’ambiente di authoring o di pubblicazione. In caso di ambiente di pubblicazione, per impostazione predefinita, l’accesso per eseguire il test è limitato. Questo perché tutte le librerie client relative al runner di test si trovano all'interno di /libs nella struttura JCR.</p> </td>
  </tr>
 </tbody>
</table>

