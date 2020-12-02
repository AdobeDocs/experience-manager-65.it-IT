---
title: '"Esercitazione: Verifica del modulo adattivo"'
seo-title: '"Esercitazione: Verifica del modulo adattivo"'
description: Utilizzare il test automatico per sottoporre a test più moduli adattivi contemporaneamente.
seo-description: Utilizzare il test automatico per sottoporre a test più moduli adattivi contemporaneamente.
uuid: 6d182bbc-b47a-4c97-af70-c960b52fdfac
contentOwner: khsingh
discoiquuid: ecddb22e-c148-441f-9088-2e5b35c7021b
docset: aem65
translation-type: tm+mt
source-git-commit: 1a816672b3e97346f5a7a984fcb4dc0df1a5b0da
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 2%

---


# Esercitazione: Verifica del modulo adattivo {#tutorial-testing-your-adaptive-form}

![](do-not-localize/10-test-your-adaptive-form.png)

Questa esercitazione è un passaggio della serie [Crea il tuo primo modulo adattivo](https://helpx.adobe.com/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html). Si consiglia di seguire le serie in sequenza cronologica per comprendere, eseguire e dimostrare l&#39;uso completo dell&#39;esercitazione.

Una volta che il modulo adattivo è pronto, è importante verificare l&#39;adattivo prima di distribuirlo agli utenti finali. È possibile testare manualmente (test funzionale) ogni campo o automatizzare il test del modulo adattivo. In presenza di più moduli adattivi, il test manuale di tutti i campi di tutti i moduli adattivi diventa un&#39;attività scoraggiante.

AEM [!DNL Forms] fornisce un framework di test, Calvin, per automatizzare il test dei moduli adattivi. Utilizzando il framework, potete scrivere ed eseguire test di interfaccia direttamente in un browser Web. Il framework fornisce API JavaScript per la creazione di test. Il test automatizzato consente di verificare l&#39;esperienza di precompilazione di un modulo adattivo, inviare esperienze relative a un modulo adattivo, regole di espressione, da convalide, caricamento lento e interazioni dell&#39;interfaccia utente. Questa esercitazione illustra i passaggi necessari per creare ed eseguire test automatici su un modulo adattivo. Al termine di questa esercitazione, potrete:

* [Creare una suite di test per il modulo adattivo](../../forms/using/testing-your-adaptive-form.md#step-create-a-test-suite)
* [Creazione di test per il modulo adattivo](../../forms/using/testing-your-adaptive-form.md#step-create-a-test-case-to-prefill-values-in-an-adaptive-form)
* [Eseguire suite di test e test creati per il modulo adattivo](#step-run-all-the-tests-in-a-suite-or-individual-tests-cases)

## Passaggio 1: Creare una suite di test {#step-create-a-test-suite}

Le suite di test dispongono di una raccolta di casi di test. Potete avere più suite di test. È consigliabile disporre di una suite di test distinta per ciascun modulo. Per creare una suite di test:

1. Accedete a AEM l&#39;istanza di creazione [!DNL Forms] come amministratore. Aprire [!UICONTROL CRXDE Lite]. Toccate AEM Logo > **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL CRXDE Lite]** oppure aprite l&#39;URL [https://localhost:4502/crx/de/index.jsp](https://localhost:4502/crx/de/index.jsp) in un browser per aprire CRXDE Lite.

1. Andate a /etc/clientlibs in [!UICONTROL CRXDE Lite]. Fare clic con il pulsante destro del mouse sulla sottocartella /etc/clientlibs e scegliere **[!UICONTROL Crea]** > **[!UICONTROL Crea nodo]**. Nel campo **[!UICONTROL Name]** digitare **WeRetailFormTestCase**. Selezionare il tipo come **cq:ClientLibraryFolder** e fare clic su **[!UICONTROL OK]**. Crea un nodo. È possibile utilizzare qualsiasi nome al posto di `WeRetailFormTestCases`.
1. Aggiungete le seguenti proprietà al nodo `WeRetailFormTestCases` e toccate **[!UICONTROL Salva ALL]**.

   <table>
    <tbody>
     <tr>
      <td><strong>Proprietà</strong></td>
      <td><strong>Tipo</strong></td>
      <td><strong>Più</strong></td>
      <td><strong>Valore</strong></td>
     </tr>
     <tr>
      <td>categorie</td>
      <td>Stringa</td>
      <td>Abilitato</td>
      <td>
       <ul>
        <li>granite.testing.hobbes.tests<br /> </li>
        <li>granite.testing.calvin.tests</li>
       </ul> </td>
     </tr>
     <tr>
      <td>dipendenze</td>
      <td>Stringa</td>
      <td>Abilitato</td>
      <td>
       <ul>
        <li>granite.testing.hobbes.testrunner <br /> </li>
        <li>granite.testing.calvin <br /> </li>
        <li>apps.testframework.all</li>
       </ul> </td>
     </tr>
    </tbody>
   </table>

   Accertatevi che ciascuna proprietà sia aggiunta a una casella separata come illustrato di seguito:

   ![dipendenze](assets/dependencies.png)

1. Fare clic con il pulsante destro del mouse sul nodo **[!UICONTROL WeRetailFormTestCase]** fare clic su **[!UICONTROL Crea]** > **[!UICONTROL Crea file]**. Nel campo **[!UICONTROL Name]** digitare `js.txt` e fare clic su **[!UICONTROL OK]**.
1. Aprite il file js.txt per la modifica, aggiungete il codice seguente e salvate il file:

   ```text
   #base=.
    init.js
   ```

1. Create un file, init.js, nel nodo `WeRetailFormTestCases`. Aggiungete il codice seguente al file e toccate **[!UICONTROL Salva tutto]**.

   ```javascript
   (function(window, hobs) {
       'use strict';
       window.testsuites = window.testsuites || {};
     // Registering the test form suite to the sytem
     // If there are other forms, all registration should be done here
       window.testsuites.testForm3 = new hobs.TestSuite("We retail - Tests", {
           path: '/etc/clientlibs/WeRetailFormTestCases/init.js',
           register: true
       });
    // window.testsuites.testForm2 = new hobs.TestSuite("testForm2");
   }(window, window.hobs));
   ```

   Il codice riportato sopra crea una suite di test denominata **We retail - Tests**.

1. Aprite AEM interfaccia utente di test (AEM > **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Test]**). La suite di test - **We retail - Test** - è elencata nell&#39;interfaccia utente.

   ![we-retail-test-suite](assets/we-retail-test-suite.png)

## Passaggio 2: Creare un test case per precompilare i valori in un modulo adattivo {#step-create-a-test-case-to-prefill-values-in-an-adaptive-form}

Un test case è un insieme di azioni per testare una funzionalità specifica. Ad esempio, la precompilazione di tutti i campi di un modulo e la convalida di alcuni campi per garantire l&#39;immissione dei valori corretti.

Un&#39;azione è un&#39;attività specifica in un modulo adattivo, ad esempio fare clic su un pulsante. Per creare un caso di test e azioni per convalidare l’input dell’utente per ciascun campo modulo adattivo:

1. In [!UICONTROL CRXDE lite], passare alla cartella `/content/forms/af/create-first-adaptive-form`. Fare clic con il pulsante destro del mouse sul nodo di cartella **[!UICONTROL create-first-adaptive-form]** e scegliere **[!UICONTROL Crea]** **[!UICONTROL Crea file]**. Nel campo **[!UICONTROL Name]** digitare `prefill.xml` e fare clic su **[!UICONTROL OK]**. Aggiungi al file il codice seguente:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?><afData>
     <afUnboundData>
       <data>
         <customer_ID>371767</customer_ID>
         <customer_Name>John Jacobs</customer_Name>
         <customer_Shipping_Address>1657 1657 Riverside Drive Redding</customer_Shipping_Address>
         <customer_State>California</customer_State>
         <customer_ZIPCode>096001</customer_ZIPCode>
        </data>
     </afUnboundData>
     <afBoundData>
       <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/"/>
     </afBoundData>
   </afData>
   ```

1. Accedi a `/etc/clientlibs`. Fare clic con il pulsante destro del mouse sulla sottocartella `/etc/clientlibs` e scegliere **[!UICONTROL Crea]**> **[!UICONTROL Crea nodo]**.

   Nel campo **[!UICONTROL Name]** digitare `WeRetailFormTests`. Selezionare il tipo come `cq:ClientLibraryFolder` e fare clic su **[!UICONTROL OK]**.

1. Aggiungete le seguenti proprietà al nodo **[!UICONTROL WeRetailFormTest]**.

   <table>
    <tbody>
     <tr>
      <td><strong>Proprietà</strong></td>
      <td><strong>Tipo</strong></td>
      <td><strong>Più</strong></td>
      <td><strong>Valore</strong></td>
     </tr>
     <tr>
      <td>categorie</td>
      <td>Stringa</td>
      <td>Abilitato</td>
      <td>
       <ul>
        <li>granite.testing.hobbes.tests<br /> </li>
        <li>granite.testing.hobbes.tests.testForm</li>
       </ul> </td>
     </tr>
     <tr>
      <td>dipendenze</td>
      <td>Stringa</td>
      <td>Abilitato</td>
      <td>
       <ul>
        <li>granite.testing.calvin.tests</li>
       </ul> </td>
     </tr>
     </tbody>
   </table>

1. Create un file, js.txt, nel nodo **[!UICONTROL WeRetailFormTest]**. Aggiungete quanto segue al file:

   ```shell
   #base=.
   prefillTest.js
   ```

   Fare clic su **[!UICONTROL Salva tutto]**.

1. Create un file, `prefillTest.js`, nel nodo **[!UICONTROL WeRetailFormTest]**. Aggiungi il codice seguente al file. Il codice crea un test case. Il test case precompila tutti i campi di un modulo e convalida alcuni campi per garantire che vengano immessi valori corretti.

   ```javascript
   (function (window, hobs) {
       'use strict';
   
       var ts = new hobs.TestSuite("Prefill Test", {
           path: '/etc/clientlibs/WeRetailFormTests/prefillTest.js',
           register: false
       })
   
       .addTestCase(new hobs.TestCase("Prefill Test")
           // navigate to the testForm which is to be test
           .navigateTo("/content/forms/af/create-first-adaptive-form/shipping-address-add-update-form.html?wcmmode=disabled&dataRef=crx:///content/forms/af/create-first-adaptive-form/prefill.xml")
           // check if adaptive form is loaded
           .asserts.isTrue(function () {
               return calvin.isFormLoaded()
           })
           .asserts.isTrue(function () {
               return calvin.model("customer_ID").value == 371767;
           })
           .asserts.isTrue(function () {
               return calvin.model("customer_ZIPCode").value == 96001;
           })
       );
   
       // register the test suite with testForm
       window.testsuites.testForm3.add(ts);
   
   }(window, window.hobs));
   ```

   Il test case viene creato e pronto per essere eseguito. È possibile creare test case per convalidare vari aspetti di un modulo adattivo, ad esempio per controllare l&#39;esecuzione dello script calculate, convalidare i pattern e convalidare l&#39;esperienza di invio di un modulo adattivo. Per informazioni su vari aspetti del test dei moduli adattivi, vedere verifica automatica dei moduli adattivi.

## Passaggio 3: Eseguire tutti i test in una suite o singoli test case {#step-run-all-the-tests-in-a-suite-or-individual-tests-cases}

Una suite di test può contenere più casi di test. Potete eseguire tutti i casi di test in una suite di test contemporaneamente o singolarmente. Quando eseguite un test, le icone indicano i risultati:

* Un&#39;icona a forma di segno di spunta indica un test superato: ![save_icon](assets/save_icon.svg)
* Un&#39;icona &quot;X&quot; indica un test non riuscito: ![icona di chiusura](assets/close-icon.svg)

1. Passare all&#39;icona AEM > **[!UICONTROL Strumenti]** **[!UICONTROL Operazioni]**> **[!UICONTROL Test]**
1. Per eseguire tutti i test della suite di test:

   1. Nel pannello [!UICONTROL Test], toccare **[!UICONTROL Vendita al dettaglio - Test (1)]**. La suite si espande per visualizzare l&#39;elenco dei test.
   1. Toccate il pulsante **[!UICONTROL Esegui test]**. L&#39;area vuota sul lato destro dello schermo viene sostituita con un modulo adattivo durante l&#39;esecuzione del test.

      ![run-all-test](assets/run-all-test.png)

1. Per eseguire un singolo test dalla suite di test:

   1. Nel pannello Test, toccare **[!UICONTROL We retail - Test (1)]**. La suite si espande per visualizzare l&#39;elenco dei test.
   1. Toccate il tasto **[!UICONTROL Precompila test]** e toccate il pulsante **[!UICONTROL Esegui test]**. L&#39;area vuota sul lato destro dello schermo viene sostituita con un modulo adattivo durante l&#39;esecuzione del test.

1. Toccate il nome del test, Test di precompilazione, per esaminare i risultati del test case. Apre il pannello [!UICONTROL Risultato]. Toccate il nome del caso di test nel pannello [!UICONTROL Risultato] per visualizzare tutti i dettagli del test.

   ![review-Results](assets/review-results.png)

Ora il modulo adattivo è pronto per la pubblicazione.
