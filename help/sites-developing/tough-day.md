---
title: Giorno difficile
seo-title: Tough Day
description: Il test Tough Day simula il carico giornaliero di circa 1000 autori in uno scenario peggiore con tutte le operazioni in corso allo stesso tempo.
seo-description: The Tough Day test simulates the daily load of around 1000 authors in a worst-case scenario with all the operations going on at the same time.
topic-tags: testing
content-type: reference
exl-id: ceb9671c-57f9-4d81-94c0-0dbccd4d90a2
source-git-commit: 0b1f28963d9294c7aa9ae45c6b9fc9a9b8b4f6e6
workflow-type: tm+mt
source-wordcount: '1879'
ht-degree: 2%

---

# Giorno difficile{#tough-day}

## Che cosa è difficile il giorno 2 {#what-is-tough-day}

&quot;Tough Day 2&quot; è un&#39;applicazione che ti consente di testare allo stress i limiti della tua istanza AEM. Può essere eseguito con la suite di test predefinita oppure può essere configurato per soddisfare le tue esigenze di test. Puoi guardare [questa registrazione](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-toughday2-stress-testing-benchmarking-tool.html) per la presentazione della domanda.

>[!CAUTION]
>
>Il difficile giorno 2 richiede Java 8.

## Come eseguire il giorno difficile 2 {#how-to-run-tough-day}

Scarica l&#39;ultima versione di Tough Day 2 dal [Archivio Adobe](https://repo1.maven.org/maven2/com/adobe/qe/toughday2/). Dopo aver scaricato l&#39;applicazione, è possibile eseguirla automaticamente fornendo `host` parametro . Nell&#39;esempio seguente, l&#39;istanza AEM viene eseguita localmente in modo che il `localhost` viene utilizzato il valore:

```xml
java -jar toughday2.jar --host=localhost
```

La suite predefinita che viene eseguita dopo l’aggiunta dei parametri è denominata `toughday`. Contiene i seguenti casi d’uso:

* Creare pagine e Live Copy per esse (inclusi i rollout)
* Pagina principale
* Esegui query in querybuilder
* Creare gerarchie di risorse
* Eliminare le risorse

La suite contiene 15% azioni di scrittura e 85% azioni di lettura.

Per eseguire i test della suite, Tough Day 2 installerà il suo pacchetto di contenuti predefinito. Per evitare questa situazione, imposta la variabile `installsamplecontent`parametro a `false`, ma ricorda che è necessario modificare anche i percorsi predefiniti per i test che intendi eseguire. Se il barattolo viene eseguito senza parametri, nel Giorno 2 viene visualizzato il valore [informazioni sulla guida](/help/sites-developing/tough-day.md#getting-help).

Come regola generale, è possibile utilizzare l&#39;applicazione seguendo questo pattern:

```xml
java -jar toughday2.jar [--help | --help_full | --help_tests | --help_publish]  [<global arguments> | <actions> | --runmode | --publishmode]
```

>[!NOTE]
>
>Il Duro Giorno 2 non ha un passo di pulizia. Di conseguenza, si consiglia di eseguire Tough Day 2 su un&#39;istanza di staging clonata e non sull&#39;istanza di produzione principale. L&#39;istanza di staging deve essere eliminata dopo i test.

### Assistenza {#getting-help}

Tough Day 2 offre un&#39;ampia gamma di opzioni di aiuto accessibili dalla riga di comando. Esempio:

```xml
java -jar toughday2.jar --help_full
```

Nella tabella seguente, puoi trovare i parametri della guida pertinenti.

<table>
 <tbody>
  <tr>
   <td><strong>Parametro</strong></td>
   <td><strong>Descrizione</strong></td>
   <td><strong>Esempio</strong></td>
  </tr>
  <tr>
   <td>--aiuto</td>
   <td>Stampa informazioni globali, ad esempio: le azioni disponibili, le suite predefinite, le modalità di esecuzione e i parametri globali.</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_publish</td>
   <td>Stampa tutti gli editori disponibili.</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_test</td>
   <td>Stampa le classi di test e la relativa descrizione.</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_full</td>
   <td>Stampa tutti gli elementi di cui sopra, oltre a test, editori e componenti della suite.</td>
   <td> </td>
  </tr>
  <tr>
   <td> —help —runmode/publishmode type=&lt;mode&gt;</td>
   <td>Elenca informazioni sulla modalità di esecuzione o pubblicazione specificata.</td>
   <td><p>java -jar toughday2.jar —help —runmode type=costantload</p> <p>java -jar toughday2.jar —help —publishmode type=ranges</p> </td>
  </tr>
  <tr>
   <td>—help —suite=&lt;suitename&gt;</td>
   <td>Elenca tutti i test di una determinata suite e le relative proprietà configurabili.</td>
   <td><br /> java -jar toughday2.jar —help —suite=get_test</td>
  </tr>
  <tr>
   <td> —help —tag=&lt;tag&gt;</td>
   <td><br /> Elenca tutti gli elementi con il tag specificato.</td>
   <td>java -jar toughday2.jar —help —tag=publish</td>
  </tr>
  <tr>
   <td>—help &lt;testclass publisherclass=""&gt;</td>
   <td><br /> Elenca tutte le proprietà configurabili per il test o l'editore specificato.</td>
   <td><p>java -jar toughday2.jar —help UploadPDFTest</p> <p>java -jar toughday2.jar —help CSVPublisher</p> </td>
  </tr>
 </tbody>
</table>

### Parametri globali {#global-parameters}

Il Dough Day 2 offre parametri globali che impostano o modificano l’ambiente per i test. Questi includono l&#39;host di destinazione, il numero di porta, il protocollo utilizzato, l&#39;utente e la password per l&#39;istanza e molti altri. Esempio:

```xml
java -jar toughday2.jar --host=host --protocol=https --port=4502 --duration=30m --dryrun=true
```

Puoi trovare i parametri rilevanti nell’elenco seguente:

| **Parametro** | **Descrizione** | **Valore predefinito** | **Valori possibili** |
|---|---|---|---|
| `--installsamplecontent=<Val>` | Installa o ignora il pacchetto di contenuto predefinito Tough Day 2. | vero | true o false |
| `--protocol=<Val>` | Il protocollo utilizzato per l&#39;host. | Http | http o https |
| `--host=<Val>` | Nome host o IP di destinazione. |  |  |
| `--port=<Val>` | La porta dell&#39;host. | 4502 |  |
| `--user=<Val>` | Il nome utente dell&#39;istanza. | admin |  |
| `--password=<Val>` | Password per l&#39;utente specificato. | admin |  |
| `--duration=<Val>` | Durata delle prove. Può essere espresso in (**s**)secondi, (**m**) minuti, (**h**)ours e (**d** Sì. | 1d |  |
| `--timeout=<Val>` | Per quanto tempo un test verrà eseguito prima che venga interrotto e contrassegnato come non riuscito. Espresso in secondi. | 180 |  |
| `--suite=<Val>` | Il valore può essere uno o un elenco (separato da virgole) di suite di test predefinite. | giorno difficile |  |
| `--configfile=<Val>` | Il file di configurazione dello yaml di destinazione. |  |  |
| `--contextpath=<Val>` | Percorso del contesto dell&#39;istanza. |  |  |
| `--loglevel=<Val>` | Livello di log per il motore Tough Day 2. | INFO | TUTTO, DEBUG, INFORMAZIONI, AVVERTENZA, ERRORE, GRASSETTO, DISATTIVATO |
| `--dryrun=<Val>` | Se true, stampa la configurazione risultante e non esegue alcun test. | false | true o false |

## Personalizzazione {#customizing}

La personalizzazione può essere ottenuta in due modi: parametri della riga di comando o file di configurazione dello stile. **I file di configurazione vengono generalmente utilizzati per le suite personalizzate di grandi dimensioni e sostituiranno i parametri predefiniti del Giorno 2 difficile. I parametri della riga di comando sostituiscono sia i file di configurazione che i parametri predefiniti.**

L’unico modo per salvare una configurazione di test è copiarla in formato yaml. Per ulteriori dettagli, consulta [giorno.yaml](https://repo.adobe.com/nexus/service/local/repositories/releases/content/com/adobe/qe/toughday2/0.2.1/toughday2-0.2.1.yaml) configurazione e gli esempi di configurazione dello schema nelle sezioni seguenti.

### Aggiunta di un nuovo test {#adding-a-new-test}

Se non desideri utilizzare il valore predefinito `toughday` puoi aggiungere un test a tua scelta utilizzando la `add` parametro . Gli esempi seguenti mostrano come aggiungere `CreateAssetTreeTest` eseguire il test utilizzando i parametri della riga di comando o un file di configurazione yaml.

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

Puoi anche aggiungere ed eseguire più istanze dello stesso test, ma ogni istanza deve avere un nome univoco. Gli esempi seguenti mostrano come aggiungere due istanze dello stesso test utilizzando i parametri della riga di comando o un file di configurazione dello stile.

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

Nel caso sia necessario modificare una o più proprietà di test, è possibile aggiungere tale proprietà alla riga di comando o al file di configurazione dello stile. Per visualizzare tutte le proprietà di test disponibili, aggiungi la `--help <TestClass/PublisherClass>` alla riga di comando, ad esempio:

```xml
java -jar toughday2.jar --help CreatePageTreeTest
```

Tieni presente che i file di configurazione yaml sovrascriveranno i parametri predefiniti di Tough Day 2 e i parametri della riga di comando sovrascriveranno sia i file di configurazione che i valori predefiniti.

Gli esempi seguenti mostrano come modificare il `template` per `CreatePageTreeTest` eseguire il test utilizzando i parametri della riga di comando o un file di configurazione yaml.

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

### Utilizzo di suite di test predefinite {#working-with-predefined-test-suites}

Gli esempi seguenti mostrano come aggiungere un test a una suite predefinita e come riconfigurare ed escludere un test esistente da una suite predefinita.

Puoi aggiungere un nuovo test a una suite predefinita utilizzando `add` e specifica la suite predefinita di destinazione.

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

I test esistenti in una determinata suite possono essere riconfigurati utilizzando `config`* *parametro. È inoltre necessario specificare il nome della suite e il nome effettivo del test (non il nome della classe di test). Puoi trovare il nome del test nella `name` della classe di test. Per ulteriori dettagli su come trovare le proprietà di test, consulta il [Modifica delle proprietà del test](/help/sites-developing/tough-day.md#changing-the-test-properties) sezione .

Nell’esempio sotto il titolo della risorsa predefinita per `CreatePageTreeTest` (denominato `UploadAsset`) viene modificato in &quot;NewAsset&quot;.

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

Inoltre, è possibile rimuovere i test da suite o editori predefiniti dalla configurazione predefinita utilizzando `exclude` parametro . È inoltre necessario specificare il nome della suite e il nome effettivo del test (non il Test C) `lass` nome). Puoi trovare il nome del test nella `name` della classe test. Nell’esempio seguente, la `CreatePageTreeTest` (denominato `UploadAsset`) viene rimosso dalla suite per giorni difficili.

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

Il Dough Day 2 può essere eseguito in una delle seguenti modalità: **normale** e **carico costante**.

La **normale** la modalità di esecuzione ha due parametri:

* `concurrency` - concurrency rappresenta il numero di thread che verranno creati per l&#39;esecuzione del test con il Tough Day 2. Su questi thread, i test verranno eseguiti fino a quando non viene eseguita la durata o non sono disponibili altri test da eseguire.

* `waittime` - il tempo di attesa tra due esecuzioni di prova consecutive sullo stesso thread. Il valore deve essere espresso in millisecondi.

L’esempio seguente mostra come aggiungere i parametri utilizzando una riga di comando:

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest --runmode=normal concurrency=20
```

o utilizzando un file di configurazione yaml:

```xml
runmode:
  type : normal
  waittime : 300
  concurrency : 200
```

La **carico costante** la modalità di esecuzione differisce dalla modalità di esecuzione normale generando un numero costante di esecuzioni di test avviate, anziché un numero costante di thread. Puoi impostare il caricamento utilizzando il parametro della modalità di esecuzione con lo stesso nome.

### Selezione del test {#test-selection}

Il processo di selezione del test è lo stesso per entrambe le modalità di esecuzione ed è il seguente: tutte le prove hanno `weight` , che determina la probabilità di esecuzione in un thread. Ad esempio, se disponiamo di due test, uno con un peso di 5 e l&#39;altro con un peso di 10, è due volte più probabile che vengano eseguiti rispetto al primo.

Inoltre, i test possono avere un `count` , che limita il numero di esecuzioni a un numero specifico. Una volta superato questo numero, non si verificheranno più esecuzioni del test. Tutte le istanze di test già in esecuzione termineranno l&#39;esecuzione come configurato. L&#39;esempio seguente mostra come aggiungere questi parametri alla riga di comando o utilizzando un file di configurazione yaml.

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
>A causa di esecuzioni parallele, il numero effettivo di esecuzioni di test non sarà esattamente la quantità configurata nel `count` parametro . Si prevede una deviazione proporzionale al numero di thread in esecuzione (controllati dal `concurrency parameter`).

### Prova {#dry-run}

Un&#39;esecuzione a secco analizza tutti gli input (parametri della riga di comando o file di configurazione), unendoli con i valori predefiniti e quindi genera i risultati. Non esegue nessuno dei test.

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest --dryrun=true
```

## Output {#output}

Il Dough Day 2 restituisce sia le metriche di test che i registri. Per ulteriori dettagli, consulta le sezioni seguenti.

### Metriche di test {#test-metrics}

Al momento il &quot;Dough Day 2&quot; indica 9 metriche di test che puoi valutare. Metriche con ***** i simboli vengono segnalati solo dopo l&#39;esecuzione corretta:

| **Nome** | **Descrizione** |
|---|---|
| Timestamp | Timestamp dell&#39;ultima esecuzione del test completata. |
| Passato | Numero di esecuzioni riuscite. |
| Non riuscito | Numero di esecuzioni non riuscite. |
| Min* | Durata inferiore dell’esecuzione del test. |
| Max* | Durata massima dell’esecuzione del test. |
| Mediana* | Durata media calcolata di tutte le esecuzioni dei test. |
| Media* | Durata media calcolata di tutte le esecuzioni dei test. |
| StdDev* | La deviazione standard. |
| 90p* | 90 percentile. |
| 99p* | 99 percentile. |
| 99,9p* | 99,9 percentile. |
| Throughput reale* | Numero di esecuzioni diviso per il tempo di esecuzione trascorso. |

Queste metriche vengono scritte con l’aiuto degli editori che possono essere aggiunti con `add` (simile all’aggiunta di test). Al momento sono disponibili due opzioni:

* **CSVPublisher** - l’output è un file CSV.
* **ConsoleEditore** - l&#39;output viene visualizzato nella console.

Per impostazione predefinita, entrambi gli editori sono abilitati.

Inoltre, esistono due modalità in cui le metriche vengono riportate:

* La **semplice** modalità di pubblicazione : riporta i risultati dall’inizio dell’esecuzione al momento della pubblicazione.
* La **intervalli** modalità di pubblicazione : riporta i risultati in un intervallo di tempo specificato. È possibile impostare l&#39;intervallo di tempo con il **intervallo** parametro della modalità di pubblicazione.

L’esempio seguente mostra come configurare il `intervals` nella riga di comando o utilizzando un file di configurazione yaml.

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

Tough Day 2 crea una cartella di log nella stessa directory in cui è stato eseguito Tough Day 2. Questa cartella contiene due tipi di registri:

* **toughday.log**: contiene messaggi relativi allo stato dell&#39;applicazione, alle informazioni di debug e ai messaggi globali.
* **giorni difficili_&lt;testname>.log**: messaggi relativi al test specificato.

I registri non vengono sovrascritti, le esecuzioni successive aggiungono messaggi ai registri esistenti. I registri hanno diversi livelli. Per ulteriori informazioni, consulta la sezione ` [loglevel parameter](/help/sites-developing/tough-day.md#global-parameters)`.

<!--
#### Example Usage {#example-usage}

#### Known Issues {#known-issues}

[Get File](assets/toughday-6_1.jar)
-->
