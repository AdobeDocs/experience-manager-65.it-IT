---
title: Giorno Duro
seo-title: Giorno Duro
description: Il test Tough Day simula il carico giornaliero di circa 1000 autori in uno scenario peggiore, con tutte le operazioni in corso contemporaneamente.
seo-description: Il test Tough Day simula il carico giornaliero di circa 1000 autori in uno scenario peggiore, con tutte le operazioni in corso contemporaneamente.
uuid: 1b672182-40f5-4580-b038-2e3c8fbfb8b7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: ea6b40fe-b6e1-495c-b34f-8815a4e2e42e
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5
workflow-type: tm+mt
source-wordcount: '1909'
ht-degree: 2%

---


# Giorno duro{#tough-day}

## Che cosa è difficile giorno 2 {#what-is-tough-day}

&quot;Tough Day 2&quot; è un&#39;applicazione che consente di sottoporre a stress test i limiti dell&#39;istanza AEM. Può essere eseguito con la suite di test predefinita oppure può essere configurato in base alle esigenze di test. È possibile guardare [questa registrazione](https://docs.adobe.com/ddc/en/gems/Toughday2---A-new-and-improved-stress-testing-and-benchmarking-tool.html) per una presentazione dell&#39;applicazione.

## Come eseguire il difficile giorno 2 {#how-to-run-tough-day}

Scaricate l&#39;ultima versione di Tough Day 2 dall&#39;archivio [ Adobi](https://repo.adobe.com/nexus/content/repositories/releases/com/adobe/qe/toughday2/). Dopo aver scaricato l&#39;applicazione, è possibile eseguirla fornendo il parametro `host`. Nell&#39;esempio seguente, l&#39;istanza AEM viene eseguita localmente, in modo che venga utilizzato il valore `localhost`:

```xml
java -jar toughday2.jar --host=localhost
```

La suite predefinita che viene eseguita dopo l&#39;aggiunta dei parametri è denominata `toughday`. Contiene i seguenti casi di utilizzo:

* Creazione di pagine e Live Copy per esse (inclusi i rollout)
* Get Homepage
* Eseguire query in querybuilder
* Creare gerarchie di risorse
* Eliminare le risorse

La suite contiene azioni di scrittura del 15% e azioni di lettura dell&#39;85%.

Per eseguire i test della suite, Tough Day 2 installerà il pacchetto di contenuto predefinito. Questo può essere evitato impostando il parametro `installsamplecontent`su `false`, ma è necessario anche modificare i percorsi predefiniti per i test che si intende eseguire. Se il jar viene eseguito senza parametri, Tough Day 2 visualizza le informazioni della Guida [](/help/sites-developing/tough-day.md#getting-help).

Come regola generale, è possibile utilizzare l&#39;applicazione seguendo questo pattern:

```xml
java -jar toughday2.jar [--help | --help_full | --help_tests | --help_publish]  [<global arguments> | <actions> | --runmode | --publishmode]
```

>[!NOTE]
>
>Tough Day 2 non ha un passo di pulizia. Di conseguenza, si consiglia di eseguire Tough Day 2 su un&#39;istanza di staging clonata e non sull&#39;istanza di produzione principale. L&#39;istanza di staging deve essere eliminata dopo i test.


### Assistenza {#getting-help}

Il Giorno 2 intensivo offre un&#39;ampia gamma di opzioni di aiuto accessibili dalla riga di comando. Esempio:

```xml
java -jar toughday2.jar --help_full
```

Nella tabella seguente sono riportati i parametri della guida pertinenti.

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
   <td>—help_ests</td>
   <td>Stampa le classi di test e la relativa descrizione.</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_full</td>
   <td>Stampa tutti i componenti di cui sopra, oltre a test, editori e suite.</td>
   <td> </td>
  </tr>
  <tr>
   <td> —help —runmode/publishmode type=&lt;Modalità&gt;</td>
   <td>Elenca le informazioni sulla modalità di esecuzione o pubblicazione specificata.</td>
   <td><p>java -jar toughday2.jar —help —runmode type=costantload</p> <p>java -jar toughday2.jar —help —publishmode type=intervalli</p> </td>
  </tr>
  <tr>
   <td>—help —suite=&lt;SuiteName&gt;</td>
   <td>Elenca tutti i test di una determinata suite e le relative proprietà configurabili.</td>
   <td><br /> java -jar toughday2.jar —help —suite=get_ests</td>
  </tr>
  <tr>
   <td> —help —tag=&lt;tag&gt;</td>
   <td><br /> Elenca tutti gli elementi con il tag specificato.</td>
   <td>java -jar toughday2.jar —help —tag=publish</td>
  </tr>
  <tr>
   <td>—help &lt;TestClass/PublisherClass&gt;</td>
   <td><br /> Elenca tutte le proprietà configurabili per il test o l'editore specificato.</td>
   <td><p>java -jar toughday2.jar —help UploadPDFTest</p> <p>java -jar toughday2.jar —help CSVPublisher</p> </td>
  </tr>
 </tbody>
</table>

### Parametri globali {#global-parameters}

Tough Day 2 offre parametri globali che impostano o modificano l&#39;ambiente per i test. Questi includono l&#39;host di destinazione, il numero della porta, il protocollo utilizzato, l&#39;utente e la password per l&#39;istanza e molti altri. Esempio:

```xml
java -jar toughday2.jar --host=host --protocol=https --port=4502 --duration=30m --dryrun=true
```

I parametri pertinenti sono elencati di seguito:

| **Parametro** | **Descrizione** | **Valore predefinito** | **Valori possibili** |
|---|---|---|---|
| `--installsamplecontent=<Val>` | Installate o saltate il pacchetto di contenuto predefinito &quot;Giorno difficile 2&quot;. | vero | true o false |
| `--protocol=<Val>` | Il protocollo utilizzato per l&#39;host. | Http | http o https |
| `--host=<Val>` | Il nome host o l&#39;IP di destinazione. |  |  |
| `--port=<Val>` | La porta dell&#39;host. | 4502 |  |
| `--user=<Val>` | Nome utente per l’istanza. | admin |  |
| `--password=<Val>` | Password per l’utente specificato. | admin |  |
| `--duration=<Val>` | Durata delle prove. Può essere espresso in (**s**) secondi, (**m**) minuti, (**h**) ore e (**d**) giorni. | 1d |  |
| `--timeout=<Val>` | Il tempo di esecuzione di un test prima che venga interrotto e contrassegnato come non riuscito. Espresso in secondi. | 180 |  |
| `--suite=<Val>` | Il valore può essere uno o un elenco (separato da virgole) di suite di test predefinite. | giorno difficile |  |
| `--configfile=<Val>` | Il file di configurazione dello yaml di destinazione. |  |  |
| `--contextpath=<Val>` | Percorso del contesto dell&#39;istanza. |  |  |
| `--loglevel=<Val>` | Livello di registro per il motore Tough Day 2. | INFO | ALL, DEBUG, INFO, AVVERTENZA, ERRORE, FATTO, OFF |
| `--dryrun=<Val>` | Se true, stampa la configurazione risultante e non esegue alcun test. | false | true o false |

## Personalizzazione di {#customizing}

La personalizzazione può essere realizzata in due modi: parametri della riga di comando o file di configurazione dello stile. **I file di configurazione vengono generalmente utilizzati per le suite personalizzate di grandi dimensioni e ignorano i parametri predefiniti del Giorno 2 Tough. I parametri della riga di comando ignorano sia i file di configurazione che i parametri predefiniti.**

L&#39;unico modo per salvare una configurazione di prova è copiarla in formato yaml. Per ulteriori dettagli, consultate questa [configurazione giorno.yaml](https://repo.adobe.com/nexus/service/local/repositories/releases/content/com/adobe/qe/toughday2/0.2.1/toughday2-0.2.1.yaml) e gli esempi di configurazione dello yaml nelle sezioni seguenti.

### Aggiunta di un nuovo test {#adding-a-new-test}

Se non si desidera utilizzare la suite `toughday` predefinita, è possibile aggiungere un test di scelta utilizzando il parametro `add`. Gli esempi seguenti mostrano come aggiungere il test `CreateAssetTreeTest` utilizzando i parametri della riga di comando o un file di configurazione del modello.

Utilizzando i parametri della riga di comando:

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest
```

Utilizzando un file di configurazione del modello:

```xml
globals:
  host : localhost
tests:
  - add : CreateAssetTreeTest
```

### Aggiunta di più istanze dello stesso test {#adding-multiple-instances-of-the-same-test}

Potete anche aggiungere ed eseguire più istanze dello stesso test, ma ciascuna di esse deve avere un nome univoco. Gli esempi seguenti mostrano come aggiungere due istanze dello stesso test utilizzando i parametri della riga di comando o un file di configurazione del modello.

Utilizzando i parametri della riga di comando:

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest name=FirstAssetTree --add CreateAssetTreeTest name=SecondAssetTree
```

Utilizzando un file di configurazione del modello:

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

Se è necessario modificare una o più proprietà di test, è possibile aggiungere tale proprietà alla riga di comando o al file di configurazione del modello. Per visualizzare tutte le proprietà di test disponibili, aggiungete il parametro `--help <TestClass/PublisherClass>` alla riga di comando, ad esempio:

```xml
java -jar toughday2.jar --help CreatePageTreeTest
```

Tenete presente che i file di configurazione dello yaml sovrascriveranno i parametri predefiniti di Tough Day 2 e che i parametri della riga di comando sovrascriveranno sia i file di configurazione che i valori predefiniti.

Gli esempi seguenti mostrano come modificare la proprietà `template` per il test `CreatePageTreeTest` utilizzando i parametri della riga di comando o un file di configurazione del modello.

Utilizzando i parametri della riga di comando:

```xml
java -jar toughday2.jar --host=localhost --add CreatePageTreeTest template=/conf/toughday-templates/settings/wcm/templates/toughday-template
```

Utilizzando un file di configurazione del modello:

```xml
globals:
  host : localhost
tests:
  - add : CreatePageTreeTest
    properties:
      template : /conf/toughday-templates/settings/wcm/templates/toughday-template
```

### Utilizzo di suite di test predefinite {#working-with-predefined-test-suites}

Gli esempi seguenti mostrano come aggiungere un test a una suite prestabilita e come riconfigurare ed escludere un test esistente da una suite predefinita.

Potete aggiungere un nuovo test a una suite predefinita utilizzando il parametro `add` e specificando la suite predefinita di destinazione.

Utilizzando i parametri della riga di comando:

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest
```

Utilizzando un file di configurazione del modello:

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - add : CreatePageTreeTest
```

I test esistenti in una determinata suite possono essere riconfigurati utilizzando il parametro `config`* *. È inoltre necessario specificare il nome della suite e il nome effettivo del test (non il nome della classe di test). Il nome del test è disponibile nella proprietà `name` della classe Test. Per ulteriori dettagli su come trovare le proprietà di test, consultare la sezione [Changing Test Properties](/help/sites-developing/tough-day.md#changing-the-test-properties) (Modifica delle proprietà di test).

Nell&#39;esempio seguente, il titolo della risorsa predefinita per `CreatePageTreeTest` (denominato `UploadAsset`) viene modificato in &quot;NewAsset&quot;.

Utilizzando i parametri della riga di comando:

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --config UploadAsset title=NewAsset
```

Utilizzando un file di configurazione del modello:

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - config : UploadAsset
    properties :
      title : NewAsset
```

Inoltre, con il parametro `exclude` è possibile rimuovere i test da suite o editori predefiniti dalla configurazione predefinita. È inoltre necessario specificare il nome della suite e il nome effettivo del test (non il nome del test C `lass`). Il nome del test è disponibile nella proprietà `name` della classe test. Nell&#39;esempio seguente, il test `CreatePageTreeTest` (denominato `UploadAsset`) viene rimosso dalla suite per giorni di prova.

Utilizzando i parametri della riga di comando:

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --exclude UploadAsset
```

Utilizzando un file di configurazione del modello:

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - exclude : UploadAsset
```

### Modalità di esecuzione {#run-modes}

Il Giorno 2 duro può essere eseguito in una delle seguenti modalità: **normale** e **carico costante**.

La modalità di esecuzione **normal** ha due parametri:

* `concurrency` - la concurrency rappresenta il numero di thread che verrà creato nel Giorno 2 per l&#39;esecuzione del test. Su questi thread, i test verranno eseguiti fino a quando la durata non sarà terminata o non saranno più eseguiti test.

* `waittime` - il tempo di attesa tra due esecuzioni di test consecutive sullo stesso thread. Il valore deve essere espresso in millisecondi.

L&#39;esempio seguente mostra come aggiungere i parametri utilizzando una riga di comando:

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest --runmode=normal concurrency=20
```

o utilizzando un file di configurazione del modello:

```xml
runmode:
  type : normal
  waittime : 300
  concurrency : 200
```

La modalità di esecuzione **carico costante** è diversa dalla modalità di esecuzione normale generando un numero costante di esecuzioni di prova avviate, anziché un numero costante di thread. Potete impostare il caricamento utilizzando il parametro della modalità di esecuzione con lo stesso nome.

### Selezione test {#test-selection}

Il processo di selezione del test è lo stesso per entrambe le modalità di esecuzione ed è il seguente: tutti i test dispongono di una proprietà `weight` che determina la probabilità di esecuzione in un thread. Ad esempio, se abbiamo due test, uno con un peso di 5 e l&#39;altro con un peso di 10, è probabile che vengano eseguiti due volte di più rispetto al primo.

Inoltre, i test possono avere una proprietà `count`, che limita il numero di esecuzioni a un dato numero. Dopo il superamento di questo numero, non si verificheranno ulteriori esecuzioni del test. Tutte le istanze di test già in esecuzione termineranno l&#39;esecuzione come configurata. L&#39;esempio seguente mostra come aggiungere questi parametri alla riga di comando o utilizzando un file di configurazione del modello.

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest weight=5 --add CreatePageTreeTest weight=10 count=100 --runmode=normal concurrency=20
```

o

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
>A causa di esecuzioni parallele, il numero effettivo di esecuzioni di test non sarà esattamente la quantità configurata nel parametro `count`. Si prevede una deviazione proporzionale al numero di filetti in esecuzione (controllati da `concurrency parameter`).

### Prova {#dry-run}

Una prova a secco analizza tutti i dati immessi (parametri della riga di comando o file di configurazione), unendoli con i valori predefiniti, quindi genera i risultati. Non esegue nessuno dei test.

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest --dryrun=true
```

## Output {#output}

Il Giorno 2 difficile produce sia metriche di test che registri. Per ulteriori dettagli, consultare le sezioni seguenti.

### Metriche di test {#test-metrics}

Il Giorno 2 intensivo attualmente segnala 9 metriche di test misurabili. Le metriche con il simbolo ***** vengono riportate solo dopo l&#39;esecuzione corretta:

| **Nome** | **Descrizione** |
|---|---|
| Timestamp | Timestamp dell&#39;ultima esecuzione del test completata. |
| Passato | Numero di esecuzioni riuscite. |
| Non riuscito | Numero di esecuzioni non riuscite. |
| Min* | Durata minima dell&#39;esecuzione del test. |
| Max* | Durata massima dell&#39;esecuzione del test. |
| Mediana* | Durata media calcolata di tutte le esecuzioni del test. |
| Media* | Durata media calcolata di tutte le esecuzioni del test. |
| StdDev* | La deviazione standard. |
| 90p* | 90 percentile. |
| 99p* | 99 percentile. |
| 99,9p* | 99,9 percentile. |
| Throughput reale* | Numero di esecuzioni divise per il tempo di esecuzione trascorso. |

Queste metriche vengono scritte con l&#39;aiuto di editori che possono essere aggiunti con il parametro `add` (in modo simile all&#39;aggiunta di test). Al momento sono disponibili due opzioni:

* **CSVPublisher** : l’output è un file CSV.
* **ConsolePublisher** : l&#39;output viene visualizzato nella console.

Per impostazione predefinita, entrambi gli editori sono abilitati.

Inoltre, esistono due modalità in cui vengono riportate le metriche:

* La **semplice** modalità di pubblicazione - riporta i risultati dall&#39;inizio dell&#39;esecuzione fino al momento della pubblicazione.
* La modalità di pubblicazione **intervalli** segnala i risultati in un determinato intervallo di tempo. Potete impostare l&#39;intervallo di tempo con il parametro della modalità di pubblicazione **interval**.

L&#39;esempio seguente mostra come configurare il parametro `intervals` sia alla riga di comando che utilizzando un file di configurazione del modello.

Utilizzando i parametri della riga di comando:

```xml
java -jar toughday2.jar --host=localhost --add CreatePageTreeTest --publishmode type=intervals interval=10s
```

Utilizzando un file di configurazione del modello:

```xml
publishmode:
     type : intervals
     interval : 10s
     tests:
        -add : CreatePageTreeTest
```

### Registrazione {#logging}

Tough Day 2 crea una cartella di file di registro nella stessa directory in cui hai eseguito Tough Day 2. Questa cartella contiene due tipi di file di registro:

* **toughday.log**: contiene messaggi relativi allo stato dell&#39;applicazione, alle informazioni di debug e ai messaggi globali.
* **toughday_&lt;testname>.log**: messaggi relativi al test specificato.

I registri non vengono sovrascritti, le esecuzioni successive aggiungeranno messaggi ai registri esistenti. I file di registro hanno diversi livelli. Per ulteriori informazioni, vedere ` [loglevel parameter](/help/sites-developing/tough-day.md#global-parameters)`.

#### Esempio di utilizzo {#example-usage}

#### Problemi noti {#known-issues}

[Ottieni file](assets/toughday-6_1.jar)
