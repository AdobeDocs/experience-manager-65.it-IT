---
title: Riferimento per il processo di workflow
seo-title: Riferimento per il processo di workflow
description: 'null'
seo-description: 'null'
uuid: de367aa8-4580-4810-b665-2a7b521e36ca
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: dbdf981f-791b-4ff7-8ca8-039d0bdc9c92
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 1%

---


# Riferimento processo flusso di lavoro{#workflow-process-reference}

AEM fornisce diversi passaggi di processo che possono essere utilizzati per creare modelli di workflow. Per le attività non incluse nei passaggi predefiniti è inoltre possibile aggiungere passaggi di processo personalizzati (vedere [Creazione di modelli di workflow](/help/sites-developing/workflows-models.md)).

## Caratteristiche del processo {#process-characteristics}

Per ogni fase del processo sono descritte le seguenti caratteristiche.

### Classe Java o percorso ECMA {#java-class-or-ecma-path}

I passaggi di processo sono definiti da una classe Java o ECMAScript.

* Per i processi di classe Java, viene fornito il nome completo della classe.
* Per i processi ECMAScript viene fornito il percorso dello script.

### Payload {#payload}

Il payload è l&#39;entità su cui agisce un&#39;istanza del flusso di lavoro. Il payload viene selezionato in modo implicito dal contesto in cui viene avviata un&#39;istanza del flusso di lavoro.

Ad esempio, se un flusso di lavoro viene applicato a una pagina AEM *P*, *P* viene passato da un passaggio all&#39;altro man mano che il flusso di lavoro avanza, con ogni passaggio che agisce facoltativamente su *P* in qualche modo.

Nel caso più comune, il payload è un nodo JCR nella directory archivio (ad esempio, una pagina o una risorsa AEM). Un payload del nodo JCR viene passato come una stringa che è un percorso JCR o un identificatore JCR (UUID). In alcuni casi, il payload può essere una proprietà JCR (passata come percorso JCR), un URL, un oggetto binario o un oggetto Java generico. I singoli passaggi del processo che agiscono sul payload in genere prevedono un payload di un certo tipo o agiscono in modo diverso a seconda del tipo di payload. Per ogni processo descritto di seguito, viene descritto l&#39;eventuale tipo di payload previsto.

### Argomenti {#arguments}

Alcuni processi del flusso di lavoro accettano argomenti specificati dall&#39;amministratore al momento della configurazione del passaggio del flusso di lavoro.

Gli argomenti vengono immessi come una singola stringa nella proprietà **Argomenti processo** nel riquadro **Proprietà** dell&#39;editor del flusso di lavoro. Per ogni processo descritto di seguito, il formato della stringa dell&#39;argomento è descritto in una semplice grammatica EBNF. Ad esempio, quanto segue indica che la stringa dell&#39;argomento è costituita da una o più coppie delimitate da virgole, in cui ciascuna coppia è costituita da un nome (una stringa) e un valore, separati da due punti:

```
    args := name '::' value [',' name '::' value]*
    name := /* A string */
    value := /* A string */
```


### Timeout {#timeout}

Dopo questo periodo di timeout, il passaggio del flusso di lavoro non è più operativo. Alcuni processi del flusso di lavoro rispettano il timeout, mentre altri non vengono applicati e vengono ignorati.

### Autorizzazioni  {#permissions}

La sessione passata al `WorkflowProcess` viene sostenuta dall&#39;utente del servizio per il servizio di elaborazione del flusso di lavoro, che dispone delle seguenti autorizzazioni alla radice del repository:

* `jcr:read`
* `rep:write`
* `jcr:versionManagement`
* `jcr:lockManagement`
* `crx:replicate`

Se tale insieme di autorizzazioni non è sufficiente per l&#39;implementazione `WorkflowProcess`, deve utilizzare una sessione con le autorizzazioni richieste.

Il modo consigliato per eseguire questa operazione è utilizzare un utente di servizio creato con il sottoinsieme necessario, ma minimo, di autorizzazioni.

>[!CAUTION]
>
>Se state effettuando l&#39;aggiornamento da una versione precedente alla AEM 6.2, potrebbe essere necessario aggiornare l&#39;implementazione.
>
>Nelle versioni precedenti, la sessione di amministrazione veniva passata alle `WorkflowProcess` implementazioni e poteva quindi avere accesso completo all&#39;archivio senza dover definire ACL specifici.
>
>Le autorizzazioni ora sono definite come sopra ([Autorizzazioni](#permissions)). Come indicato per aggiornare l’implementazione.
>
>Una soluzione a breve termine è disponibile anche a fini di compatibilità con le versioni precedenti quando non è possibile apportare modifiche al codice:
>
>* Utilizzando la console Web ( `/system/console/configMgr` individuare il **Adobe di configurazione del flusso di lavoro Granite**
   >
   >
* abilitare la **modalità legacy processo di workflow**
>
>
Questo tornerà al vecchio comportamento di fornire una sessione di amministrazione all&#39;implementazione `WorkflowProcess` e fornire l&#39;accesso illimitato all&#39;intero repository ancora una volta.

## Processi di controllo del flusso di lavoro {#workflow-control-processes}

I processi seguenti non eseguono alcuna azione sul contenuto. Servono a controllare il comportamento del flusso di lavoro stesso.

### AbsoluteTimeAutoAdvancer (Absolute Time Auto Advancer) {#absolutetimeautoadvancer-absolute-time-auto-advancer}

Il processo `AbsoluteTimeAutoAdvancer` (Absolute Time Auto Advancer) si comporta in modo identico a **AutoAdvancer**, ma si verifica un timeout in un dato momento e in una data, anziché dopo un determinato periodo di tempo.

* **Classe** Java:  `com.adobe.granite.workflow.console.timeout.autoadvance.AbsoluteTimeAutoAdvancer`
* **Payload**: Nessuno.
* **Argomenti**: Nessuno.
* **Timeout**: Timeout del processo quando vengono raggiunti l&#39;ora e la data impostate.

### AutoAdvancer (Auto Advancer) {#autoadvancer-auto-advancer}

Il processo `AutoAdvancer` sposta automaticamente il flusso di lavoro al passaggio successivo. Se è possibile eseguire più passaggi successivi (ad esempio, in presenza di una divisione OR), questo processo porterà avanti il flusso di lavoro lungo la route *predefinita*, se specificata, altrimenti il flusso di lavoro non verrà anticipato.

* **Classe** Java:  `com.adobe.granite.workflow.console.timeout.autoadvance.AutoAdvancer`

* **Payload**: Nessuno.
* **Argomenti**: Nessuno.
* **Timeout**: Timeout del processo dopo la durata impostata.

### ProcessAssembler (Process Assembler) {#processassembler-process-assembler}

Il processo `ProcessAssembler` esegue più processi secondari in sequenza in un singolo passaggio del flusso di lavoro. Per utilizzare il `ProcessAssembler`, create un singolo passaggio di questo tipo nel flusso di lavoro e impostate i relativi argomenti per indicare i nomi e gli argomenti dei processi secondari che desiderate eseguire.

* **Classe** Java:  `com.day.cq.workflow.impl.process.ProcessAssembler`

* **Payload**: Una risorsa DAM, AEM pagina o nessun payload (dipende dai requisiti dei sottoprocessi).
* **Argomenti**:

```
        args := arg [',' arg]
        arg := processname ['::' processargs]
        processname := /* A fully qualified Java Class or absolute
        repository path to an ECMAScript */
        processargs := processarg [';' processarg]*
        processarg := '[' nobracketprocessarg ']' | nobracketprocessarg
        nobracketprocessarg := listitem [':' listitem]*
        listitem := /* A string */
```

* **Timeout**: Rispettato.

Esempio:

* Estraete i metadati dalla risorsa.
* Create tre miniature delle tre dimensioni specificate.
* Create un’immagine JPEG dalla risorsa, partendo dal presupposto che la risorsa non sia originariamente né GIF né PNG (nel qual caso non viene creato alcun file JPEG).
* Imposta la data dell’ultima modifica sulla risorsa.

```shell
com.day.cq.dam.core.process.ExtractMetadataProcess,
    com.day.cq.dam.core.process.CreateThumbnailProcess::[140:100];[48:48];[319:319:false],
    com.day.cq.dam.core.process.CreateWebEnabledImageProcess::dimension:1280:1280;mimetype:image/jpeg,
    com.day.cq.dam.core.process.AssetSetLastModifiedProcess
```

## Processi di base {#basic-processes}

I processi seguenti eseguono operazioni semplici o fungono da esempi.

>[!CAUTION]
>
>***non è necessario*** modificare nulla nel percorso `/libs`.
>
>Questo perché il contenuto di `/libs` viene sovrascritto al successivo aggiornamento dell&#39;istanza (e potrebbe essere sovrascritto quando si applica un hotfix o un feature pack).

### delete {#delete}

L’elemento nel percorso specificato viene eliminato.

* **Percorso** ECMAScript:  `/libs/workflow/scripts/delete.ecma`

* **Payload**: Percorso JCR
* **Argomenti**: None
* **Timeout**: Ignorato

### noop {#noop}

Questo è il processo null. Non esegue alcuna operazione, ma registra un messaggio di debug.

* **Percorso** ECMAScript:  `/libs/workflow/scripts/noop.ecma`

* **Payload**: None
* **Argomenti**: None
* **Timeout**: Ignorato

### rule-false {#rule-false}

Si tratta di un processo null che restituisce `false` sul metodo `check()`.

* **Percorso** ECMAScript:  `/libs/workflow/scripts/rule-false.ecma`

* **Payload**: None
* **Argomenti**: None
* **Timeout**: Ignorato

### esempio {#sample}

Si tratta di un esempio di processo ECMAScript.

* **Percorso** ECMAScript:  `/libs/workflow/scripts/sample.ecma`

* **Payload**: None
* **Argomenti**: None
* **Timeout**: Ignorato

### urlcaller {#urlcaller}

Si tratta di un semplice processo di workflow che richiama l’URL specificato. In genere, l’URL è un riferimento a una JSP (o altro servlet equivalente) che esegue un’attività semplice. Questo processo dovrebbe essere utilizzato solo durante lo sviluppo e le dimostrazioni e non in un ambiente di produzione. Gli argomenti specificano l&#39;URL, il login e la password.

* **Percorso** ECMAScript:  `/libs/workflow/scripts/urlcaller.ecma`

* **Payload**: None
* **Argomenti**:

```
        args := url [',' login ',' password]
        url := /* The URL to be called */
        login := /* The login to access the URL */
        password := /* The password to access the URL */
```

Esempio: `http://localhost:4502/my.jsp, mylogin, mypassword`

* **Timeout**: Ignorato

### LockProcess {#lockprocess}

Blocca il payload del flusso di lavoro.

* **Classe Java:** `com.day.cq.workflow.impl.process.LockProcess`

* **Payload:** JCR_PATH e JCR_UID
* **Argomenti:** None
* **Timeout:** Ignorato

La fase non ha effetto nelle seguenti circostanze:

* Il payload è già bloccato
* Il nodo payload non contiene un nodo figlio jcr:content

### Sblocca processo {#unlockprocess}

Sblocca il payload del flusso di lavoro.

* **Classe Java:** `com.day.cq.workflow.impl.process.UnlockProcess`

* **Payload:** JCR_PATH e JCR_UID
* **Argomenti:** None
* **Timeout:** Ignorato

La fase non ha effetto nelle seguenti circostanze:

* Il payload è già sbloccato
* Il nodo payload non contiene un nodo figlio jcr:content

## Processi di gestione delle versioni {#versioning-processes}

Il seguente processo esegue un&#39;attività relativa alla versione.

### CreateVersionProcess {#createversionprocess}

Crea una nuova versione del payload del flusso di lavoro (AEM pagina o risorsa DAM).

* **Classe** Java:  `com.day.cq.wcm.workflow.process.CreateVersionProcess`

* **Payload**: Un percorso JCR o un UUID che fa riferimento a una pagina o a una risorsa DAM
* **Argomenti**: None
* **Timeout**: Rispettato

