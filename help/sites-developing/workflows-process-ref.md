---
title: Guida di riferimento per il processo dei flusso di lavoro
description: Consulta questo riferimento di processo per i flussi di lavoro in Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: a9de8ec6-6948-4643-89c3-62d9b1f6293a
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 1%

---

# Guida di riferimento per il processo dei flusso di lavoro{#workflow-process-reference}

L’AEM fornisce diverse fasi del processo che possono essere utilizzate per creare modelli di flusso di lavoro. È inoltre possibile aggiungere passaggi di processo personalizzati per attività non incluse nei passaggi incorporati (vedere [Creazione di modelli di flussi di lavoro](/help/sites-developing/workflows-models.md)).

## Caratteristiche del processo {#process-characteristics}

Per ogni fase del processo, vengono descritte le seguenti caratteristiche.

### Java™ Class o percorso ECMA {#java-class-or-ecma-path}

I passaggi del processo sono definiti da una classe Java™ o da un ECMAScript.

* Per i processi di classe Java™, viene fornito il nome completo della classe.
* Per i processi ECMAScript, viene fornito il percorso dello script.

### Payload {#payload}

Il payload è l’entità su cui agisce un’istanza del flusso di lavoro. Il payload viene selezionato in modo implicito dal contesto all’interno del quale viene avviata un’istanza di flusso di lavoro.

Ad esempio, se un flusso di lavoro viene applicato a una pagina AEM *P* allora *P* viene passato da un passaggio all’altro con l’avanzare del flusso di lavoro; ogni passaggio agisce facoltativamente su *P* in qualche modo.

Nel caso più comune, il payload è un nodo JCR nell’archivio (ad esempio, una pagina o una risorsa AEM). Un payload del nodo JCR viene passato come stringa costituita da un percorso JCR o da un identificatore JCR (UUID). A volte il payload può essere una proprietà JCR (passata come percorso JCR), un URL, un oggetto binario o un oggetto Java™ generico. Singoli passaggi del processo che agiscono sul payload solitamente si aspettano un payload di un determinato tipo, oppure agiscono in modo diverso a seconda del tipo di payload. Per ogni processo descritto di seguito, viene descritto il tipo di payload previsto, se presente.

### Argomenti {#arguments}

Alcuni processi di workflow accettano gli argomenti specificati dall&#39;amministratore durante la configurazione del passaggio del workflow.

Gli argomenti vengono immessi come una singola stringa nel **Argomenti processo** proprietà in **Proprietà** dell&#39;editor del flusso di lavoro. Per ogni processo descritto di seguito, il formato della stringa di argomento è descritto in una semplice grammatica EBNF. Ad esempio, quanto segue indica che la stringa dell’argomento è costituita da una o più coppie delimitate da virgole, in cui ogni coppia è costituita da un nome (che è una stringa) e da un valore, separati da due punti:

```
    args := name '::' value [',' name '::' value]*
    name := /* A string */
    value := /* A string */
```


### Timeout {#timeout}

Dopo questo periodo di timeout, il passaggio del flusso di lavoro non è più operativo. Alcuni processi del flusso di lavoro rispettano il timeout, mentre per altri non si applica e viene ignorato.

### Autorizzazioni {#permissions}

La sessione è stata passata al `WorkflowProcess` è supportato dall’utente del servizio per il servizio di elaborazione del flusso di lavoro, che dispone delle seguenti autorizzazioni nella directory principale dell’archivio:

* `jcr:read`
* `rep:write`
* `jcr:versionManagement`
* `jcr:lockManagement`
* `crx:replicate`

Se tale set di autorizzazioni non è sufficiente per `WorkflowProcess` , deve quindi utilizzare una sessione con le autorizzazioni necessarie.

A tale scopo, si consiglia di utilizzare un utente del servizio creato con il sottoinsieme di autorizzazioni necessario, ma minimo.

>[!CAUTION]
>
>Se aggiorni una versione precedente a AEM 6.2, potrebbe essere necessario aggiornare l’implementazione.
>
>Nelle versioni precedenti, la sessione di amministrazione è stata passata al `WorkflowProcess` implementazioni e potrebbero quindi avere accesso completo all’archivio senza dover definire ACL specifici.
>
>Le autorizzazioni sono ora definite come sopra ([Autorizzazioni](#permissions)). Come è il metodo consigliato per aggiornare l’implementazione.
>
>Una soluzione a breve termine è disponibile anche per motivi di compatibilità con le versioni precedenti quando non è possibile apportare modifiche al codice:
>
>* Utilizzo della console web ( `/system/console/configMgr` individuare **Servizio di configurazione del flusso di lavoro Adobe Granite**
>
>* abilita **Elaborazione flusso di lavoro in modalità legacy**
>
>In questo modo si torna al vecchio comportamento di fornire una sessione di amministrazione al `WorkflowProcess` e fornire nuovamente l’accesso illimitato a tutto l’archivio.

## Processi di controllo del flusso di lavoro {#workflow-control-processes}

I processi seguenti non eseguono alcuna azione sul contenuto. Servono a controllare il comportamento del flusso di lavoro stesso.

### AbsoluteTimeAutoAdvancer (Avanzamento automatico tempo assoluto) {#absolutetimeautoadvancer-absolute-time-auto-advancer}

Il `AbsoluteTimeAutoAdvancer` (Avanzamento automatico tempo assoluto) si comporta in modo identico a **Avanzamento automatico**, con la differenza che il timeout avviene in un determinato momento e in una data specificata, invece che dopo un determinato periodo di tempo.

* **Java™ Class**: `com.adobe.granite.workflow.console.timeout.autoadvance.AbsoluteTimeAutoAdvancer`
* **Payload**: nessuna.
* **Argomenti**: nessuna.
* **Timeout**: il processo scade quando vengono raggiunte l’ora e la data impostate.

### Avanzamento automatico (Avanzamento automatico) {#autoadvancer-auto-advancer}

Il `AutoAdvancer` Il processo porta automaticamente il flusso di lavoro al passaggio successivo. Se esiste più di un possibile passaggio successivo (ad esempio, in caso di suddivisione di un operatore OR), questo processo fa avanzare il flusso di lavoro lungo *ciclo di lavorazione predefinito*, se ne è stato specificato uno, altrimenti il flusso di lavoro non verrà avanzato.

* **Java™ Class**: `com.adobe.granite.workflow.console.timeout.autoadvance.AutoAdvancer`

* **Payload**: nessuna.
* **Argomenti**: nessuna.
* **Timeout**: timeout del processo dopo un periodo di tempo impostato.

### ProcessAssembler (Assemblatore processi) {#processassembler-process-assembler}

Il `ProcessAssembler` Il processo esegue più processi secondari in sequenza in un singolo passaggio del flusso di lavoro. Per utilizzare `ProcessAssembler`, creare un singolo passaggio di questo tipo nel flusso di lavoro e impostarne gli argomenti per indicare i nomi e gli argomenti dei sottoprocessi che si desidera eseguire.

* **Java™ Class**: `com.day.cq.workflow.impl.process.ProcessAssembler`

* **Payload**: risorsa DAM, pagina AEM o nessun payload (a seconda dei requisiti dei sottoprocessi).
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

Ad esempio:

* Estrai i metadati dalla risorsa.
* Crea tre miniature delle tre dimensioni specificate.
* Crea un’immagine JPEG dalla risorsa, supponendo che la risorsa non sia originariamente un GIF o un PNG (in tal caso non viene creato alcun JPEG).
* Imposta la data dell’ultima modifica sulla risorsa.

```shell
com.day.cq.dam.core.process.ExtractMetadataProcess,
    com.day.cq.dam.core.process.CreateThumbnailProcess::[140:100];[48:48];[319:319:false],
    com.day.cq.dam.core.process.CreateWebEnabledImageProcess::dimension:1280:1280;mimetype:image/jpeg,
    com.day.cq.dam.core.process.AssetSetLastModifiedProcess
```

## Processi di base {#basic-processes}

I processi seguenti eseguono attività semplici o fungono da esempi.

>[!CAUTION]
>
>Non modificare nulla nella `/libs` percorso.
>
>Questo perché il contenuto di `/libs` viene sovrascritto al successivo aggiornamento dell’istanza (e può essere sovrascritto quando si applica un hotfix o un feature pack).

### elimina {#delete}

L’elemento nel percorso specificato viene eliminato.

* **Percorso ECMAScript**: `/libs/workflow/scripts/delete.ecma`

* **Payload**: percorso JCR
* **Argomenti**: nessuna
* **Timeout**: ignorato

### noop {#noop}

Processo nullo. Non esegue alcuna operazione, ma registra un messaggio di debug.

* **Percorso ECMAScript**: `/libs/workflow/scripts/noop.ecma`

* **Payload**: nessuna
* **Argomenti**: nessuna
* **Timeout**: ignorato

### rule-false {#rule-false}

Si tratta di un processo nullo che restituisce `false` il `check()` metodo.

* **Percorso ECMAScript**: `/libs/workflow/scripts/rule-false.ecma`

* **Payload**: nessuna
* **Argomenti**: nessuna
* **Timeout**: ignorato

### esempio {#sample}

Questo è un esempio di processo ECMAScript.

* **Percorso ECMAScript**: `/libs/workflow/scripts/sample.ecma`

* **Payload**: nessuna
* **Argomenti**: nessuna
* **Timeout**: ignorato

### BloccaProcesso {#lockprocess}

Blocca il payload del workflow.

* **Classe Java™:** `com.day.cq.workflow.impl.process.LockProcess`

* **Payload:** JCR_PATH e JCR_UUID
* **Argomenti:** Nessuno
* **Timeout:** Ignorato

La fase non ha alcun effetto nelle seguenti circostanze:

* Il payload è già bloccato
* Il nodo payload non contiene un nodo figlio jcr:content

### UnlockProcess {#unlockprocess}

Sblocca il payload del flusso di lavoro.

* **Classe Java™:** `com.day.cq.workflow.impl.process.UnlockProcess`

* **Payload:** JCR_PATH e JCR_UUID
* **Argomenti:** Nessuno
* **Timeout:** Ignorato

La fase non ha alcun effetto nelle seguenti circostanze:

* Il payload è già sbloccato
* Il nodo payload non contiene un nodo figlio jcr:content

## Processi di controllo delle versioni {#versioning-processes}

Il processo seguente esegue un&#39;attività correlata alla versione.

### CreateVersionProcess {#createversionprocess}

Crea una versione del payload del flusso di lavoro (pagina AEM o risorsa DAM).

* **Classe Java™**: `com.day.cq.wcm.workflow.process.CreateVersionProcess`

* **Payload**: percorso JCR o UUID che fa riferimento a una pagina o una risorsa DAM
* **Argomenti**: nessuna
* **Timeout**: Rispettato
