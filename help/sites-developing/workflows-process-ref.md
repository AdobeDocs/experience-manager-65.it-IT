---
title: Guida di riferimento per il processo dei flusso di lavoro
seo-title: Guida di riferimento per il processo dei flusso di lavoro
description: Guida di riferimento per il processo dei flusso di lavoro
seo-description: 'null'
uuid: de367aa8-4580-4810-b665-2a7b521e36ca
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: dbdf981f-791b-4ff7-8ca8-039d0bdc9c92
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 2%

---


# Guida di riferimento per il processo dei flusso di lavoro{#workflow-process-reference}

AEM fornisce diversi passaggi del processo che possono essere utilizzati per creare modelli di flusso di lavoro. È inoltre possibile aggiungere passaggi di processo personalizzati per attività non coperte dai passaggi incorporati (consulta [Creazione di modelli di flusso di lavoro](/help/sites-developing/workflows-models.md)).

## Caratteristiche del processo {#process-characteristics}

Per ogni fase del processo sono descritte le seguenti caratteristiche.

### Percorso classe Java o ECMA {#java-class-or-ecma-path}

I passaggi del processo sono definiti da una classe Java o da un ECMAScript.

* Per i processi della classe Java, viene fornito il nome completo della classe.
* Per i processi ECMAScript viene fornito il percorso dello script.

### Payload {#payload}

Il payload è l’entità su cui agisce un’istanza di flusso di lavoro. Il payload viene selezionato implicitamente dal contesto in cui viene avviata un’istanza di flusso di lavoro.

Ad esempio, se un flusso di lavoro viene applicato a una pagina AEM *P*, *P* viene passato da un passaggio all&#39;altro mentre il flusso di lavoro avanza, con ogni passaggio che agisce facoltativamente su *P* in qualche modo.

Nel caso più comune, il payload è un nodo JCR nell’archivio (ad esempio, una pagina AEM o una risorsa). Un payload del nodo JCR viene passato come stringa che è un percorso JCR o un identificatore JCR (UUID). In alcuni casi il payload può essere una proprietà JCR (passata come percorso JCR), un URL, un oggetto binario o un oggetto Java generico. I singoli passaggi del processo che agiscono sul payload in genere si aspettano un payload di un determinato tipo o agiscono in modo diverso a seconda del tipo di payload. Per ogni processo descritto di seguito, viene descritto l’eventuale tipo di payload previsto.

### Argomenti {#arguments}

Alcuni processi del flusso di lavoro accettano gli argomenti specificati dall’amministratore durante la configurazione del passaggio del flusso di lavoro.

Gli argomenti vengono immessi come stringa singola nella proprietà **Argomenti processo** nel riquadro **Proprietà** dell&#39;editor del flusso di lavoro. Per ogni processo descritto di seguito, il formato della stringa dell&#39;argomento è descritto in una semplice grammatica EBNF. Ad esempio, quanto segue indica che la stringa dell&#39;argomento è costituita da una o più coppie delimitate da virgole, in cui ciascuna coppia è costituita da un nome (una stringa) e un valore, separati da due punti:

```
    args := name '::' value [',' name '::' value]*
    name := /* A string */
    value := /* A string */
```


### Timeout {#timeout}

Dopo questo periodo di timeout, il passaggio del flusso di lavoro non è più operativo. Alcuni processi del flusso di lavoro rispettano il timeout, mentre altri non lo applicano e vengono ignorati.

### Autorizzazioni  {#permissions}

La sessione passata a `WorkflowProcess` viene supportata dall&#39;utente del servizio per il servizio di processo del flusso di lavoro, che dispone delle seguenti autorizzazioni nella directory principale dell&#39;archivio:

* `jcr:read`
* `rep:write`
* `jcr:versionManagement`
* `jcr:lockManagement`
* `crx:replicate`

Se quel set di autorizzazioni non è sufficiente per l&#39;implementazione di `WorkflowProcess`, deve utilizzare una sessione con le autorizzazioni richieste.

Il modo consigliato per farlo è quello di utilizzare un utente di servizio creato con il sottoinsieme di autorizzazioni necessario, ma minimo, necessario.

>[!CAUTION]
>
>Se esegui l’aggiornamento da una versione precedente alla versione 6.2 di AEM, potrebbe essere necessario aggiornare l’implementazione.
>
>Nelle versioni precedenti, la sessione di amministrazione veniva passata alle `WorkflowProcess` implementazioni e poteva quindi avere accesso completo all&#39;archivio senza dover definire ACL specifici.
>
>Le autorizzazioni sono ora definite come sopra ([Autorizzazioni](#permissions)). Come indicato per l’aggiornamento dell’implementazione.
>
>Una soluzione a breve termine è disponibile anche a scopo di retrocompatibilità quando non è possibile modificare il codice:
>
>* Tramite la console Web ( `/system/console/configMgr` individuare il **servizio Adobe Granite Workflow Configuration**
   >
   >
* abilita la **modalità legacy del processo di workflow**
>
>
Questo tornerà al vecchio comportamento di fornire una sessione di amministrazione all’ `WorkflowProcess` implementazione e fornire nuovamente accesso illimitato all’intero archivio.

## Processi di controllo del flusso di lavoro {#workflow-control-processes}

I processi seguenti non eseguono alcuna azione sul contenuto. Servono a controllare il comportamento del flusso di lavoro stesso.

### AbsoluteTimeAutoAdvancer (Absolute Time Auto Advancer) {#absolutetimeautoadvancer-absolute-time-auto-advancer}

Il processo `AbsoluteTimeAutoAdvancer` (Absolute Time Auto Advancer) si comporta in modo identico a **AutoAdvancer**, tranne per il fatto che scade in una data e in un&#39;ora specificate, anziché dopo un determinato periodo di tempo.

* **Classe** Java:  `com.adobe.granite.workflow.console.timeout.autoadvance.AbsoluteTimeAutoAdvancer`
* **Payload**: Nessuno.
* **Argomenti**: Nessuno.
* **Timeout**: Il processo scade quando viene raggiunta l’ora e la data impostate.

### AutoAdvancer (Auto Advancer) {#autoadvancer-auto-advancer}

Il processo `AutoAdvancer` avanza automaticamente il flusso di lavoro al passaggio successivo. Se è possibile eseguire più di un passaggio successivo (ad esempio, se è presente una suddivisione OR), questo processo farà avanzare il flusso di lavoro lungo la *route predefinita*, se specificato, altrimenti il flusso di lavoro non verrà avanzato.

* **Classe** Java:  `com.adobe.granite.workflow.console.timeout.autoadvance.AutoAdvancer`

* **Payload**: Nessuno.
* **Argomenti**: Nessuno.
* **Timeout**: Il processo si interrompe una volta impostato il tempo.

### ProcessAssembler (Process Assembler) {#processassembler-process-assembler}

Il processo `ProcessAssembler` esegue più processi secondari in sequenza in un singolo passaggio del flusso di lavoro. Per utilizzare il `ProcessAssembler`, crea un singolo passaggio di questo tipo nel flusso di lavoro e imposta i relativi argomenti per indicare i nomi e gli argomenti dei processi secondari che desideri eseguire.

* **Classe** Java:  `com.day.cq.workflow.impl.process.ProcessAssembler`

* **Payload**: Una risorsa DAM, AEM pagina o nessun payload (a seconda dei requisiti dei sottoprocessi).
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

* Estrai i metadati dalla risorsa.
* Crea tre miniature delle tre dimensioni specificate.
* Crea un&#39;immagine JPEG dalla risorsa, partendo dal presupposto che la risorsa non sia originariamente né un file GIF né un file PNG (nel qual caso non viene creato alcun file JPEG).
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
>***Non è necessario*** modificare nulla nel percorso `/libs`.
>
>Questo perché il contenuto di `/libs` viene sovrascritto la prossima volta che aggiorni l&#39;istanza (e può essere sovrascritto quando applichi un hotfix o un feature pack).

### delete {#delete}

L&#39;elemento nel percorso specificato viene eliminato.

* **Percorso** ECMAScript:  `/libs/workflow/scripts/delete.ecma`

* **Payload**: Percorso JCR
* **Argomenti**: Nessuno
* **Timeout**: Ignorato

### noop {#noop}

Questo è il processo null. Non esegue alcuna operazione, ma registra un messaggio di debug.

* **Percorso** ECMAScript:  `/libs/workflow/scripts/noop.ecma`

* **Payload**: Nessuno
* **Argomenti**: Nessuno
* **Timeout**: Ignorato

### rule-false {#rule-false}

Si tratta di un processo null che restituisce `false` sul metodo `check()`.

* **Percorso** ECMAScript:  `/libs/workflow/scripts/rule-false.ecma`

* **Payload**: Nessuno
* **Argomenti**: Nessuno
* **Timeout**: Ignorato

### campione {#sample}

Questo è un esempio di processo ECMAScript.

* **Percorso** ECMAScript:  `/libs/workflow/scripts/sample.ecma`

* **Payload**: Nessuno
* **Argomenti**: Nessuno
* **Timeout**: Ignorato

### chiamante {#urlcaller}

Si tratta di un semplice processo di flusso di lavoro che chiama l’URL specificato. In genere l’URL è un riferimento a un JSP (o altro servlet equivalente) che esegue un’attività semplice. Questo processo deve essere utilizzato solo durante lo sviluppo e le dimostrazioni e non in un ambiente di produzione. Gli argomenti specificano l&#39;URL, il login e la password.

* **Percorso** ECMAScript:  `/libs/workflow/scripts/urlcaller.ecma`

* **Payload**: Nessuno
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

* **Payload:** JCR_PATH e JCR_UUID
* **Argomenti:** Nessuno
* **Timeout:** ignorato

Il passaggio non ha effetto nelle seguenti circostanze:

* Il payload è già bloccato
* Il nodo di payload non contiene un nodo figlio jcr:content

### Sblocca processo {#unlockprocess}

Sblocca il payload del flusso di lavoro.

* **Classe Java:** `com.day.cq.workflow.impl.process.UnlockProcess`

* **Payload:** JCR_PATH e JCR_UUID
* **Argomenti:** Nessuno
* **Timeout:** ignorato

Il passaggio non ha effetto nelle seguenti circostanze:

* Il payload è già sbloccato
* Il nodo di payload non contiene un nodo figlio jcr:content

## Processi di gestione delle versioni {#versioning-processes}

Il processo seguente esegue un’attività relativa alla versione.

### CreateVersionProcess {#createversionprocess}

Crea una nuova versione del payload del flusso di lavoro (AEM pagina o risorsa DAM).

* **Classe** Java:  `com.day.cq.wcm.workflow.process.CreateVersionProcess`

* **Payload**: Un percorso JCR o UID che fa riferimento a una pagina o a una risorsa DAM
* **Argomenti**: Nessuno
* **Timeout**: Rispettato

