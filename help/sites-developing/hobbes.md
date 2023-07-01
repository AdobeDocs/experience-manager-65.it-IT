---
title: Verifica dell’interfaccia utente
description: AEM fornisce un framework per automatizzare i test per l’interfaccia utente dell’AEM
uuid: 408a60b5-cba9-4c9f-abd3-5c1fb5be1c50
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components, testing
discoiquuid: 938100ad-94f9-408a-819d-72657dc115f7
docset: aem65
exl-id: 2d28cee6-31b0-4288-bad3-4d2ecad7b626
source-git-commit: 4fd5e9a1bc603202ee52e85a1c09125b13cec315
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 2%

---

# Verifica dell’interfaccia utente{#testing-your-ui}

>[!NOTE]
>
>A partire da AEM 6.5, il framework di test dell’interfaccia utente hobbes.js è diventato obsoleto. Adobe non prevede di apportare ulteriori miglioramenti e consiglia ai clienti di utilizzare l’automazione Selenium.
>
>Consulta [Funzioni obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

L’AEM fornisce un framework per automatizzare i test per l’interfaccia utente dell’AEM. Utilizzando il framework, puoi scrivere ed eseguire test dell’interfaccia utente direttamente in un browser web. Il framework fornisce un’API JavaScript per la creazione di test.

Il framework di test AEM utilizza Hobbes.js, una libreria di test scritta in JavaScript. Il framework Hobbes.js è stato sviluppato per testare l&#39;AEM come parte del processo di sviluppo. Il framework è ora disponibile per l’uso pubblico per testare le applicazioni AEM.

>[!NOTE]
>
>Consulta Hobbes.js [documentazione](https://developer.adobe.com/experience-manager/reference-materials/6-5/test-api/index.html) per informazioni complete sull’API.

## Struttura delle prove {#structure-of-tests}

Quando si utilizzano test automatizzati all’interno dell’AEM, è importante comprendere i seguenti termini:

| Azione | Un **Azione** è un’attività specifica su una pagina web, ad esempio fare clic su un collegamento o su un pulsante. |
|---|---|
| Caso di prova | A **Caso di prova** è una situazione specifica che può essere costituita da uno o più **Azioni**. |
| Suite di test | A **Suite di test** è un gruppo di **Casi di test** che insieme testano un caso d’uso specifico. |

## Esecuzione dei test {#executing-tests}

### Visualizzazione delle suite di test {#viewing-test-suites}

Apri la console di test per visualizzare le suite di test registrate. Il pannello Test contiene un elenco di suite di test e dei relativi test case.

Passa alla console Strumenti tramite **Navigazione globale -> Strumenti > Operazioni -> Test**.

![chlimage_1-63](assets/chlimage_1-63.png)

All’apertura della console, le suite di test sono elencate a sinistra insieme a un’opzione per eseguirle tutte in sequenza. Lo spazio a destra mostrato con uno sfondo a quadretti è un segnaposto per la visualizzazione del contenuto della pagina durante l’esecuzione dei test.

![chlimage_1-64](assets/chlimage_1-64.png)

### Esecuzione di una singola suite di test {#running-a-single-test-suite}

Le suite di test possono essere eseguite singolarmente. Quando si esegue una suite di test, la pagina cambia quando vengono eseguiti i casi di test e le relative azioni e i risultati vengono visualizzati dopo il completamento del test. Le icone indicano i risultati.

Un’icona di spunta indica che il test è stato superato:

![Icona segno di spunta.](do-not-localize/chlimage_1-2.png)

Un’icona &quot;X&quot; indica un test non riuscito:

![Icona test non riuscito indicata da una X all&#39;interno di un cerchio.](do-not-localize/chlimage_1-3.png)

Per eseguire una suite di test:

1. Nel pannello Test, tocca o fai clic sul nome del Test Case che desideri eseguire per espandere i dettagli delle azioni.

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. Clic **Esegui test**.

   ![Immagine del pulsante Esegui test, indicata da un puntatore a destra all&#39;interno di un cerchio.](do-not-localize/chlimage_1-4.png)

1. Il segnaposto viene sostituito con il contenuto della pagina durante l’esecuzione del test.

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. Rivedi i risultati del test case toccando o facendo clic sulla descrizione per aprire il **Risultato** pannello. Toccando o facendo clic sul nome del test case nel **Risultato** mostra tutti i dettagli.

   ![chlimage_1-67](assets/chlimage_1-67.png)

### Esecuzione di più test {#running-multiple-tests}

Le suite di test vengono eseguite in sequenza nell’ordine in cui compaiono nella console. Puoi approfondire un test per visualizzare i risultati dettagliati.

![chlimage_1-68](assets/chlimage_1-68.png)

1. Nel pannello Test, tocca o fai clic su **Esegui tutti i test** o **Eseguire i test** sotto il titolo della suite di test che desideri eseguire.

   ![Immagine del pulsante Esegui tutti i test e del pulsante Esegui test, indicata da un puntatore a destra all&#39;interno di un cerchio.](do-not-localize/chlimage_1-5.png)

1. Per visualizzare i risultati di ogni test case, fare clic sul titolo del test case. Facendo clic sul nome del test in **Risultato** mostra tutti i dettagli.

   ![chlimage_1-69](assets/chlimage_1-69.png)

## Creazione e utilizzo di una suite di test semplice {#creating-and-using-a-simple-test-suite}

La procedura seguente illustra i passaggi della creazione ed esecuzione di una suite di test utilizzando [Contenuto We.Retail](/help/sites-developing/we-retail.md), ma puoi modificare facilmente il test per utilizzare una pagina web diversa.

Per informazioni dettagliate sulla creazione di suite di test personalizzate, vedi [Documentazione API di Hobbes.js](https://developer.adobe.com/experience-manager/reference-materials/6-5/test-api/index.html).

1. Apri CRXDE Lite. ([https://localhost:4502/crx/de](https://localhost:4502/crx/de))
1. Fare clic con il pulsante destro del mouse `/etc/clientlibs` cartella e fai clic su **Crea > Crea cartella**. Tipo `myTests` per il nome e fai clic su **OK**.
1. Fare clic con il pulsante destro del mouse `/etc/clientlibs/myTests` cartella e fai clic su **Crea > Crea nodo**. Utilizza i seguenti valori delle proprietà, quindi fai clic su **OK**:

   * Nome: `myFirstTest`
   * Tipo: `cq:ClientLibraryFolder`

1. Aggiungi le seguenti proprietà al nodo myFirstTest:

   | Nome | Tipo | Valore |
   |---|---|---|
   | `categories` | String[] | `granite.testing.hobbes.tests` |
   | `dependencies` | String[] | `granite.testing.hobbes.testrunner` |

   >[!NOTE]
   >
   >**Solo AEM Forms**
   >
   >
   >Per testare i moduli adattivi, aggiungi i seguenti valori alle categorie e alle dipendenze. Ad esempio:
   >
   >
   >**categorie**: `granite.testing.hobbes.tests, granite.testing.hobbes.af.commons`
   >
   >
   >**dipendenze**: `granite.testing.hobbes.testrunner, granite.testing.hobbes.af`

1. Clic **Salva tutto**.
1. Fare clic con il pulsante destro del mouse `myFirstTest` e fai clic su **Crea > Crea file**. Denomina il file `js.txt` e fai clic su **OK**.
1. In `js.txt` immetti il testo seguente:

   ```
   #base=.
   myTestSuite.js
   ```

1. Clic **Salva tutto** e quindi chiudere il `js.txt` file.
1. Fare clic con il pulsante destro del mouse `myFirstTest` e fai clic su **Crea > Crea file**. Denomina il file `myTestSuite.js` e fai clic su **OK**.
1. Copia il seguente codice in `myTestSuite.js` quindi salva il file:

   ```
   new hobs.TestSuite("Experience Content Test Suite", {path:"/etc/clientlibs/myTests/myFirstTest/myTestSuite.js"})
      .addTestCase(new hobs.TestCase("Navigate to Experience Content")
         .navigateTo("/content/we-retail/us/en/experience/arctic-surfing-in-lofoten.html")
      )
      .addTestCase(new hobs.TestCase("Hover Over Topnav")
         .mouseover("li.visible-xs")
      )
      .addTestCase(new hobs.TestCase("Click Topnav Link")
         .click("li.active a")
   );
   ```

1. Accedi a **Test** per provare la tua suite di test.
