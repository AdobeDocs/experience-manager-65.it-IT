---
title: Verifica dell’interfaccia utente
seo-title: Testing Your UI
description: AEM fornisce un framework per l’automazione dei test per l’interfaccia utente AEM
seo-description: AEM provides a framework for automating tests for your AEM UI
uuid: 408a60b5-cba9-4c9f-abd3-5c1fb5be1c50
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components, testing
discoiquuid: 938100ad-94f9-408a-819d-72657dc115f7
docset: aem65
exl-id: 2d28cee6-31b0-4288-bad3-4d2ecad7b626
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 2%

---

# Verifica dell’interfaccia utente{#testing-your-ui}

>[!NOTE]
>
>A partire da AEM 6.5, il framework di test dell’interfaccia utente hobbes.js è obsoleto. Adobe non prevede di apportare ulteriori miglioramenti e consiglia ai clienti di utilizzare l’automazione Selenium.
>
>Vedi [Funzioni obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

AEM fornisce un framework per l’automazione dei test per l’interfaccia utente AEM. Utilizzando il framework, puoi scrivere ed eseguire test di interfaccia utente direttamente in un browser web. Il framework fornisce un’API javascript per la creazione di test.

Il framework di test AEM utilizza Hobbes.js, una libreria di test scritta in Javascript. Il framework Hobbes.js è stato sviluppato per AEM di test nell’ambito del processo di sviluppo. Il framework è ora disponibile per l&#39;uso pubblico per il test delle applicazioni AEM.

>[!NOTE]
>
>Fai riferimento a Hobbes.js [documentazione](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/test-api/index.html) per informazioni complete sull’API.

## Struttura dei test {#structure-of-tests}

Quando si utilizzano test automatizzati in AEM, è importante comprendere i seguenti termini:

| Azione | Un **Azione** è un’attività specifica in una pagina web, ad esempio fare clic su un collegamento o un pulsante. |
|---|---|
| Caso di test | A **Caso di test** è una situazione specifica che può essere costituita da uno o più **Azioni**. |
| Suite di test | A **Suite di test** è un gruppo correlato **Casi di test** che testano insieme un caso d&#39;uso specifico. |

## Esecuzione di test {#executing-tests}

### Visualizzazione delle suite di test {#viewing-test-suites}

Apri la console Test per visualizzare le suite di test registrate. Il pannello Test contiene un elenco delle suite di test e dei relativi casi di test.

Passa alla console Strumenti tramite **Navigazione globale -> Strumenti > Operazioni -> Test**.

![chlimage_1-63](assets/chlimage_1-63.png)

All’apertura della console, le suite di test sono elencate a sinistra insieme a un’opzione per eseguirle tutte in sequenza. Lo spazio a destra visualizzato con uno sfondo a scacchi è un segnaposto per la visualizzazione del contenuto della pagina durante l’esecuzione dei test.

![chlimage_1-64](assets/chlimage_1-64.png)

### Esecuzione di una suite di test singola {#running-a-single-test-suite}

Le suite di test possono essere eseguite singolarmente. Quando esegui una suite di test, la pagina cambia man mano che vengono eseguiti i casi di test e le relative azioni e i risultati vengono visualizzati dopo il completamento del test. Le icone indicano i risultati.

Un’icona a forma di segno di spunta indica un test superato:

![](do-not-localize/chlimage_1-2.png)

Un&#39;icona &quot;X&quot; indica un test non riuscito:

![](do-not-localize/chlimage_1-3.png)

Per eseguire una suite di test:

1. Nel pannello Test , tocca o fai clic sul nome del Test Case da eseguire per espandere i dettagli delle azioni.

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. Tocca o fai clic su **Esegui test** pulsante .

   ![](do-not-localize/chlimage_1-4.png)

1. Il segnaposto viene sostituito con il contenuto della pagina durante l’esecuzione del test.

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. Rivedi i risultati del Test Case toccando o facendo clic sulla descrizione per aprire il **Risultato** pannello. Tocca o fai clic sul nome del Test Case nella **Risultato** mostra tutti i dettagli.

   ![chlimage_1-67](assets/chlimage_1-67.png)

### Esecuzione di più test {#running-multiple-tests}

Le suite di test vengono eseguite in sequenza nell’ordine in cui vengono visualizzate nella console. Puoi approfondire un test per visualizzare i risultati dettagliati.

![chlimage_1-68](assets/chlimage_1-68.png)

1. Nel pannello Test , tocca o fai clic sul pulsante **Esegui tutti i test** o **Eseguire test** sotto il titolo della suite di test che desideri eseguire.

   ![](do-not-localize/chlimage_1-5.png)

1. Per visualizzare i risultati di ogni test case, tocca o fai clic sul titolo del test case. Tocca o fai clic sul nome del test nella **Risultato** mostra tutti i dettagli.

   ![chlimage_1-69](assets/chlimage_1-69.png)

## Creazione e utilizzo di una suite di test semplice {#creating-and-using-a-simple-test-suite}

La procedura seguente illustra la procedura per creare ed eseguire una suite di test utilizzando [Contenuto We.Retail](/help/sites-developing/we-retail.md), ma puoi modificare facilmente il test per utilizzare una pagina web diversa.

Per informazioni complete sulla creazione di suite di test, consulta [Documentazione API di Hobbes.js](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/test-api/index.html).

1. Apri CRXDE Lite. ([https://localhost:4502/crx/de](https://localhost:4502/crx/de))
1. Fai clic con il pulsante destro del mouse sul pulsante `/etc/clientlibs` e fai clic su **Crea > Crea cartella**. Tipo `myTests` per il nome e fai clic su **OK**.
1. Fai clic con il pulsante destro del mouse sul pulsante `/etc/clientlibs/myTests` e fai clic su **Crea > Crea nodo**. Utilizza i seguenti valori di proprietà e fai clic su **OK**:

   * Nome: `myFirstTest`
   * Tipo: `cq:ClientLibraryFolder`

1. Aggiungi le seguenti proprietà al nodo myFirstTest:

   | Nome | Tipo | Valore |
   |---|---|---|
   | `categories` | Stringa[] | `granite.testing.hobbes.tests` |
   | `dependencies` | Stringa[] | `granite.testing.hobbes.testrunner` |

   >[!NOTE]
   >
   >**Solo AEM Forms**
   >
   >
   >Per testare i moduli adattivi, aggiungi i seguenti valori alle categorie e alle dipendenze. Esempio:
   >
   >
   >**categorie**: `granite.testing.hobbes.tests, granite.testing.hobbes.af.commons`
   >
   >
   >**dipendenze**: `granite.testing.hobbes.testrunner, granite.testing.hobbes.af`

1. Fai clic su **Salva tutto**.
1. Fai clic con il pulsante destro del mouse sul pulsante `myFirstTest` nodo e fai clic su **Crea > Crea file**. Denomina il file `js.txt` e fai clic su **OK**.
1. In `js.txt` file, immetti il testo seguente:

   ```
   #base=.
   myTestSuite.js
   ```

1. Fai clic su **Salva tutto** e quindi chiudere il `js.txt` file.
1. Fai clic con il pulsante destro del mouse sul pulsante `myFirstTest` nodo e fai clic su **Crea > Crea file**. Denomina il file `myTestSuite.js` e fai clic su **OK**.
1. Copia il seguente codice nel `myTestSuite.js` quindi salva il file:

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

1. Passa a **Test** per provare la suite di test.
