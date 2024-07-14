---
title: Giornata difficile
description: Il test Duro giorno simula il carico giornaliero di circa 1000 autori in uno scenario peggiore, con tutte le operazioni in corso nello stesso momento.
topic-tags: testing
content-type: reference
exl-id: ceb9671c-57f9-4d81-94c0-0dbccd4d90a2
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1825'
ht-degree: 1%

---

# Giornata difficile{#tough-day}

## Che cos’è il giorno difficile 2 {#what-is-tough-day}

&quot;Tough Day 2&quot; è un’applicazione che consente di sottoporre a test di stress i limiti dell’istanza di AEM. Può essere eseguita con la suite di test predefinita o configurata in base alle tue esigenze di test. Puoi guardare [questa registrazione](https://experienceleague.adobe.com/docs/events/experience-manager-gems-recordings/gems2017/aem-toughday2-stress-testing-benchmarking-tool.html) per una presentazione dell&#39;applicazione.

>[!CAUTION]
>
>Il Giorno 2 richiede Java™ 8.

## Come eseguire duro giorno 2 {#how-to-run-tough-day}

Scarica la versione più recente del secondo giorno rigido dall&#39;[archivio Adobe](https://repo1.maven.org/maven2/com/adobe/qe/toughday2/). Dopo aver scaricato l&#39;applicazione, è possibile eseguirla automaticamente fornendo il parametro `host`. Nell&#39;esempio seguente, l&#39;istanza AEM viene eseguita localmente in modo da utilizzare il valore `localhost`:

```xml
java -jar toughday2.jar --host=localhost
```

La suite predefinita eseguita dopo l&#39;aggiunta dei parametri è denominata `toughday`. Contiene i seguenti casi d’uso:

* Crea pagine e Live Copy per esse (inclusi i rollout)
* Ottieni homepage
* Eseguire query in querybuilder
* Creare gerarchie di risorse
* Eliminare risorse

La suite contiene il 15% di azioni di scrittura e l’85% di azioni di lettura.

Per eseguire i test delle suite, il Giorno difficile 2 installerà il pacchetto di contenuti predefinito. È possibile evitare questo inconveniente impostando il parametro `installsamplecontent` su `false`. È tuttavia necessario modificare anche i percorsi predefiniti per i test che si desidera eseguire. Se il file jar viene eseguito senza parametri, nel secondo giorno vengono visualizzate le [informazioni della Guida](/help/sites-developing/tough-day.md#getting-help).

Di regola, puoi utilizzare l’applicazione seguendo questo pattern:

```xml
java -jar toughday2.jar [--help | --help_full | --help_tests | --help_publish]  [<global arguments> | <actions> | --runmode | --publishmode]
```

>[!NOTE]
>
>Il Giorno 2 duro non ha un passaggio di pulizia. Di conseguenza, si consiglia di eseguire il Giorno 2 completo su un’istanza di staging clonata e non sull’istanza di produzione principale. L’istanza di staging deve essere rilasciata dopo i test.
>

### Ottenimento della Guida {#getting-help}

Duro Giorno 2 offre un&#39;ampia gamma di opzioni di aiuto accessibili dalla riga di comando. Ad esempio:

```xml
java -jar toughday2.jar --help_full
```

Nella tabella seguente sono disponibili i parametri della Guida pertinenti.

<table>
 <tbody>
  <tr>
   <td><strong>Parametro</strong></td>
   <td><strong>Descrizione</strong></td>
   <td><strong>Esempio</strong></td>
  </tr>
  <tr>
   <td>—aiuto</td>
   <td>Stampa informazioni globali, ad esempio le azioni disponibili, le suite predefinite, le modalità di esecuzione e i parametri globali.</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_publish</td>
   <td>Stampa tutti gli editori disponibili.</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_tests</td>
   <td>Stampa le classi di test e la relativa descrizione.</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_full</td>
   <td>Stampa tutte le informazioni precedenti, oltre a test, publisher e componenti delle suite.</td>
   <td> </td>
  </tr>
  <tr>
   <td> —help —runmode/publishmode type=&lt;Modalità&gt;</td>
   <td>Elenca le informazioni sulla modalità di esecuzione o di pubblicazione specificata.</td>
   <td><p>Java™ -jar toughday2.jar —help —runmode type=constantload</p> <p>Java™ -jar toughday2.jar —help —publishmode type=interval</p> </td>
  </tr>
  <tr>
   <td>—help —suite=&lt;NomeSuite&gt;</td>
   <td>Elenca tutti i test di una determinata suite e le rispettive proprietà configurabili.</td>
   <td><br /> Java™ -jar toughday2.jar —help —suite=get_tests</td>
  </tr>
  <tr>
   <td> —help —tag=&lt;Tag&gt;</td>
   <td><br /> Elenca tutti gli elementi con il tag specificato.</td>
   <td>Java™ -jar toughday2.jar —help —tag=publish</td>
  </tr>
  <tr>
   <td>—help &lt;TestClass/PublisherClass&gt;</td>
   <td><br /> Elenca tutte le proprietà configurabili per il test o l’editore specificato.</td>
   <td><p>Java™ -jar toughday2.jar —help UploadPDFTest</p> <p>Java™ -jar toughday2.jar —Aiuta CSVPublisher</p> </td>
  </tr>
 </tbody>
</table>

### Parametri globali {#global-parameters}

Il secondo giorno difficile offre parametri globali che impostano o modificano l’ambiente per i test. Questi includono l’host di destinazione, il numero di porta, il protocollo utilizzato, l’utente e la password per l’istanza e molti altri. Ad esempio:

```xml
java -jar toughday2.jar --host=host --protocol=https --port=4502 --duration=30m --dryrun=true
```

Puoi trovare i parametri rilevanti nell’elenco seguente:

| **Parametro** | **Descrizione** | **Valore predefinito** | **Valori Possibili** |
|---|---|---|---|
| `--installsamplecontent=<Val>` | Installa o salta il pacchetto di contenuti predefinito per il secondo giorno. | vero | true o false |
| `--protocol=<Val>` | Protocollo utilizzato per l&#39;host. | http | http o https |
| `--host=<Val>` | Il nome host o l’IP di destinazione. |  |  |
| `--port=<Val>` | La porta dell’host. | 4502 |  |
| `--user=<Val>` | Il nome utente dell’istanza. | admin |  |
| `--password=<Val>` | Password per l’utente specificato. | admin |  |
| `--duration=<Val>` | La durata dei test. Può essere espresso in **s** secondi, **m** minuti, **h** ore e **d** giorni. | 1d |  |
| `--timeout=<Val>` | Per quanto tempo un test verrà eseguito prima di essere interrotto e contrassegnato come non riuscito. Espresso in secondi. | 180 |  |
| `--suite=<Val>` | Il valore può essere uno o un elenco (separato da virgole) di suite di test predefinite. | giornata difficile |  |
| `--configfile=<Val>` | Il file di configurazione yaml di destinazione. |  |  |
| `--contextpath=<Val>` | Percorso di contesto dell’istanza. |  |  |
| `--loglevel=<Val>` | Livello di registro per il motore Tough Day 2. | INFO | TUTTI, DEBUG, INFORMAZIONI, AVVERTENZA, ERRORE, IRREVERSIBILE, DISATTIVATO |
| `--dryrun=<Val>` | Se true, stampa la configurazione risultante e non esegue alcun test. | false | true o false |

## Personalizzazione {#customizing}

La personalizzazione può essere ottenuta in due modi: tramite parametri della riga di comando o file di configurazione yaml. **I file di configurazione vengono utilizzati per le suite personalizzate di grandi dimensioni e sostituiscono i parametri predefiniti del giorno 2. I parametri della riga di comando sostituiscono sia i file di configurazione che i parametri predefiniti.**

L’unico modo per salvare una configurazione di test è copiarla in formato yaml.

### Aggiunta di un nuovo test {#adding-a-new-test}

Se non desideri utilizzare la suite `toughday` predefinita, puoi aggiungere un test scegliendo il parametro `add`. Gli esempi seguenti mostrano come aggiungere il test `CreateAssetTreeTest` utilizzando i parametri della riga di comando o un file di configurazione yaml.

Utilizzando i parametri della riga di comando:

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest
```

Utilizzando un file di configurazione yaml:

```xml
globals:
  host : localhost
tests:
  - add : CreateAssetTreeTest
```

### Aggiunta di più istanze dello stesso test  {#adding-multiple-instances-of-the-same-test}

Puoi anche aggiungere ed eseguire più istanze dello stesso test, ma ogni istanza deve avere un nome univoco. Gli esempi seguenti mostrano come aggiungere due istanze dello stesso test utilizzando parametri della riga di comando o un file di configurazione yaml.

Utilizzando i parametri della riga di comando:

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest name=FirstAssetTree --add CreateAssetTreeTest name=SecondAssetTree
```

Utilizzando un file di configurazione yaml:

```xml
globals:
  host : localhost
tests:
  - add : CreateAssetTreeTest
    properties:
      name : FirstAssetTree
  - add : CreateAssetTreeTest
    properties:
      name : SecondAssetTree
```

### Modifica delle proprietà del test {#changing-the-test-properties}

Se devi modificare una o più proprietà del test, puoi aggiungerle alla riga di comando o al file di configurazione yaml. Per visualizzare tutte le proprietà di test disponibili, aggiungere il parametro `--help <TestClass/PublisherClass>` alla riga di comando, ad esempio:

```xml
java -jar toughday2.jar --help CreatePageTreeTest
```

I file di configurazione yaml sovrascriveranno i parametri di default di Giorno 2 e i parametri della riga di comando sovrascriveranno sia i file di configurazione che i valori di default.

Negli esempi seguenti viene illustrato come modificare la proprietà `template` per il test `CreatePageTreeTest` utilizzando i parametri della riga di comando o un file di configurazione yaml.

Utilizzando i parametri della riga di comando:

```xml
java -jar toughday2.jar --host=localhost --add CreatePageTreeTest template=/conf/toughday-templates/settings/wcm/templates/toughday-template
```

Utilizzando un file di configurazione yaml:

```xml
globals:
  host : localhost
tests:
  - add : CreatePageTreeTest
    properties:
      template : /conf/toughday-templates/settings/wcm/templates/toughday-template
```

### Utilizzo delle suite di test predefinite {#working-with-predefined-test-suites}

Gli esempi seguenti mostrano come aggiungere un test a una suite predefinita e come riconfigurare ed escludere un test esistente da una suite predefinita.

È possibile aggiungere un nuovo test a una suite predefinita utilizzando il parametro `add` e specificando la suite predefinita di destinazione.

Utilizzando i parametri della riga di comando:

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest
```

Utilizzando un file di configurazione yaml:

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - add : CreatePageTreeTest
```

I test esistenti in una determinata suite possono essere riconfigurati utilizzando il parametro `config`* *. Specifica anche il nome della suite e il nome effettivo del test (non il nome della classe di test). È possibile trovare il nome del test nella proprietà `name` della classe del test. Per ulteriori dettagli su come trovare le proprietà dei test, leggere la sezione [Modifica delle proprietà dei test](/help/sites-developing/tough-day.md#changing-the-test-properties).

Nell&#39;esempio seguente il titolo predefinito della risorsa per `CreatePageTreeTest` (denominato `UploadAsset`) viene modificato in &quot;NewAsset&quot;.

Utilizzando i parametri della riga di comando:

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --config UploadAsset title=NewAsset
```

Utilizzando un file di configurazione yaml:

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - config : UploadAsset
    properties :
      title : NewAsset
```

È inoltre possibile rimuovere i test da suite o editori predefiniti dalla configurazione predefinita utilizzando il parametro `exclude`. Specificare inoltre il nome della suite e il nome effettivo del test (non il nome del test C `lass`). È possibile trovare il nome del test nella proprietà `name` della classe del test. Nell&#39;esempio seguente, il test `CreatePageTreeTest` (denominato `UploadAsset`) viene rimosso dalla suite di giorni duri.

Utilizzando i parametri della riga di comando:

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --exclude UploadAsset
```

Utilizzando un file di configurazione yaml:

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - exclude : UploadAsset
```

### Modalità di esecuzione {#run-modes}

Il giorno 2 può essere eseguito in una delle seguenti modalità: **normale** e **carico costante**.

La modalità di esecuzione **normale** ha due parametri:

* `concurrency` - la concorrenza rappresenta il numero di thread che verranno creati dal giorno 2 per l&#39;esecuzione del test. Su questi thread, i test verranno eseguiti fino a quando la durata non è terminata o non sono presenti altri test da eseguire.

* `waittime`: tempo di attesa tra due esecuzioni di test consecutive sullo stesso thread. Il valore deve essere espresso in millisecondi.

L’esempio seguente mostra come aggiungere i parametri utilizzando la riga di comando:

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest --runmode=normal concurrency=20
```

oppure utilizzando un file di configurazione yaml:

```xml
runmode:
  type : normal
  waittime : 300
  concurrency : 200
```

La modalità di esecuzione **caricamento costante** differisce dalla modalità di esecuzione normale in quanto genera un numero costante di esecuzioni di test avviate, anziché un numero costante di thread. È possibile impostare il carico utilizzando il parametro della modalità di esecuzione con lo stesso nome.

### Selezione test {#test-selection}

Il processo di selezione dei test è lo stesso per entrambe le modalità di esecuzione ed è il seguente: tutti i test hanno una proprietà `weight`, che determina la probabilità di esecuzione in un thread. Ad esempio, se disponi di due test, uno con un peso di 5 e l’altro con un peso di 10, è due volte più probabile che venga eseguito il secondo.

Inoltre, i test possono avere una proprietà `count`, che limita il numero di esecuzioni a un determinato numero. Una volta passato questo numero, non si verificheranno ulteriori esecuzioni del test. Tutte le istanze di test già in esecuzione finiranno l’esecuzione come configurato. Nell&#39;esempio seguente viene illustrato come aggiungere questi parametri nella riga di comando o utilizzando un file di configurazione yaml.

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest weight=5 --add CreatePageTreeTest weight=10 count=100 --runmode=normal concurrency=20
```

oppure

```xml
- add : CreateAssetTreeTest
    properties :
      name : UploadAsset
      weight : 5
      base : 3
      foldertitle : IAmAFolder
      assettitle : IAmAnAsset
      count : 100
```

>[!NOTE]
>
>A causa di esecuzioni parallele, il numero effettivo di esecuzioni dei test non corrisponderà esattamente alla quantità configurata nel parametro `count`. È prevista una deviazione proporzionale al numero di thread in esecuzione (controllati da `concurrency parameter`).

### Prova {#dry-run}

Un&#39;esecuzione a secco analizza tutti gli input forniti (parametri della riga di comando o file di configurazione), unendoli con i valori predefiniti e quindi restituisce i risultati. Non esegue nessuno dei test.

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest --dryrun=true
```

## Output {#output}

Il secondo giorno genera sia metriche di test che registri. Per ulteriori informazioni, leggere le sezioni seguenti.

### Metriche di test {#test-metrics}

Duro Giorno 2 attualmente riporta nove metriche di test che è possibile valutare. Le metriche con il simbolo **&#42;** vengono segnalate solo dopo esecuzioni riuscite:

| **Nome** | **Descrizione** |
|---|---|
| Marca temporale | Timestamp dell’ultima esecuzione di test completata. |
| Superata | Numero di esecuzioni riuscite. |
| Non riuscito | Numero di esecuzioni non riuscite. |
| Min&#42; | Durata minima dell’esecuzione del test. |
| Max&#42; | Durata massima dell’esecuzione del test. |
| Mediana&#42; | Durata mediana calcolata di tutte le esecuzioni di test. |
| Media&#42; | Durata media calcolata di tutte le esecuzioni di test. |
| DevStandard&#42; | La deviazione standard. |
| 90p&#42; | 90 percentile. |
| 99p&#42; | 99 percentile. |
| 99,9p&#42; | 99,9 percentile. |
| Throughput reale&#42; | Numero di esecuzioni diviso per il tempo di esecuzione trascorso. |

Queste metriche vengono scritte con l&#39;aiuto di editori che possono essere aggiunti con il parametro `add` (in modo simile all&#39;aggiunta di test). Attualmente sono disponibili due opzioni:

* **CSVPublisher** - l&#39;output è un file CSV.
* **ConsolePublisher** - l&#39;output viene visualizzato nella console.

Per impostazione predefinita, entrambi gli editori sono abilitati.

Inoltre, esistono due modalità in cui vengono riportate le metriche:

* Modalità di pubblicazione **simple**: riporta i risultati dall&#39;inizio dell&#39;esecuzione fino al punto di pubblicazione.
* Modalità di pubblicazione **intervalli**: riporta i risultati in un determinato intervallo di tempo. È possibile impostare l&#39;intervallo di tempo con il parametro della modalità di pubblicazione **interval**.

Nell&#39;esempio seguente viene illustrato come configurare il parametro `intervals` nella riga di comando o utilizzando un file di configurazione yaml.

Utilizzando i parametri della riga di comando:

```xml
java -jar toughday2.jar --host=localhost --add CreatePageTreeTest --publishmode type=intervals interval=10s
```

Utilizzando un file di configurazione yaml:

```xml
publishmode:
     type : intervals
     interval : 10s
     tests:
        -add : CreatePageTreeTest
```

### Registrazione {#logging}

Il giorno 2 crea una cartella dei registri nella stessa directory in cui è stato eseguito il giorno 2. Questa cartella contiene due tipi di registri:

* **toughday.log**: contiene messaggi relativi allo stato dell&#39;applicazione, alle informazioni di debug e ai messaggi globali.
* **toughday_&lt;testname>.log**: messaggi relativi al test specificato.

I registri non vengono sovrascritti, le esecuzioni successive aggiungono i messaggi ai registri esistenti. I registri hanno diversi livelli. Per ulteriori informazioni, vedere il parametro [loglevel.](#global-parameters).

<!--
#### Example Usage {#example-usage}

#### Known Issues {#known-issues}

[Get File](assets/toughday-6_1.jar)
-->
