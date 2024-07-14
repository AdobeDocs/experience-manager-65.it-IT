---
title: Guida di riferimento per il processo dei flusso di lavoro
description: Consulta questo riferimento di processo per i flussi di lavoro in Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: a9de8ec6-6948-4643-89c3-62d9b1f6293a
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 1%

---

# Guida di riferimento per il processo dei flusso di lavoro{#workflow-process-reference}

L’AEM fornisce diverse fasi del processo che possono essere utilizzate per creare modelli di flusso di lavoro. È inoltre possibile aggiungere passaggi di processo personalizzati per attività non incluse nei passaggi predefiniti (vedere [Creazione di modelli di flussi di lavoro](/help/sites-developing/workflows-models.md)).

## Caratteristiche del processo {#process-characteristics}

Per ogni fase del processo, vengono descritte le seguenti caratteristiche.

### Java™ Class o percorso ECMA {#java-class-or-ecma-path}

I passaggi del processo sono definiti da una classe Java™ o da un ECMAScript.

* Per i processi di classe Java™, viene fornito il nome completo della classe.
* Per i processi ECMAScript, viene fornito il percorso dello script.

### Payload {#payload}

Il payload è l’entità su cui agisce un’istanza del flusso di lavoro. Il payload viene selezionato in modo implicito dal contesto all’interno del quale viene avviata un’istanza di flusso di lavoro.

Ad esempio, se un flusso di lavoro viene applicato a una pagina AEM *P*, *P* viene passato da un passaggio all&#39;altro con l&#39;avanzare del flusso di lavoro, con ogni passaggio che può facoltativamente agire su *P* in qualche modo.

Nel caso più comune, il payload è un nodo JCR nell’archivio (ad esempio, una pagina o una risorsa AEM). Un payload del nodo JCR viene passato come stringa costituita da un percorso JCR o da un identificatore JCR (UUID). A volte il payload può essere una proprietà JCR (passata come percorso JCR), un URL, un oggetto binario o un oggetto Java™ generico. Singoli passaggi del processo che agiscono sul payload solitamente si aspettano un payload di un determinato tipo, oppure agiscono in modo diverso a seconda del tipo di payload. Per ogni processo descritto di seguito, viene descritto il tipo di payload previsto, se presente.

### Argomenti {#arguments}

Alcuni processi di workflow accettano gli argomenti specificati dall&#39;amministratore durante la configurazione del passaggio del workflow.

Gli argomenti vengono immessi come stringa singola nella proprietà **Argomenti processo** nel riquadro **Proprietà** dell&#39;editor del flusso di lavoro. Per ogni processo descritto di seguito, il formato della stringa di argomento è descritto in una semplice grammatica EBNF. Ad esempio, quanto segue indica che la stringa dell’argomento è costituita da una o più coppie delimitate da virgole, in cui ogni coppia è costituita da un nome (che è una stringa) e da un valore, separati da due punti:

```
    args := name '::' value [',' name '::' value]*
    name := /* A string */
    value := /* A string */
```


### Timeout {#timeout}

Dopo questo periodo di timeout, il passaggio del flusso di lavoro non è più operativo. Alcuni processi del flusso di lavoro rispettano il timeout, mentre per altri non si applica e viene ignorato.

### Autorizzazioni {#permissions}

La sessione passata a `WorkflowProcess` è supportata dall&#39;utente del servizio per il servizio del processo del flusso di lavoro, che dispone delle seguenti autorizzazioni nella radice dell&#39;archivio:

* `jcr:read`
* `rep:write`
* `jcr:versionManagement`
* `jcr:lockManagement`
* `crx:replicate`

Se tale set di autorizzazioni non è sufficiente per l&#39;implementazione di `WorkflowProcess`, è necessario utilizzare una sessione con le autorizzazioni richieste.

A tale scopo, si consiglia di utilizzare un utente del servizio creato con il sottoinsieme di autorizzazioni necessario, ma minimo.

>[!CAUTION]
>
>Se aggiorni una versione precedente a AEM 6.2, potrebbe essere necessario aggiornare l’implementazione.
>
>Nelle versioni precedenti, la sessione di amministrazione è stata passata alle implementazioni `WorkflowProcess` e potrebbe quindi avere accesso completo all&#39;archivio senza dover definire ACL specifici.
>
>Le autorizzazioni sono ora definite come sopra ([Autorizzazioni](#permissions)). Come è il metodo consigliato per aggiornare l’implementazione.
>
>Una soluzione a breve termine è disponibile anche per motivi di compatibilità con le versioni precedenti quando non è possibile apportare modifiche al codice:
>
>* Utilizzo della console Web ( `/system/console/configMgr` individuare il **servizio di configurazione del flusso di lavoro Adobe Granite**
>
>* abilita la modalità legacy del processo di **flusso di lavoro**
>
>Viene ripristinato il precedente comportamento, ovvero fornire una sessione di amministrazione all&#39;implementazione `WorkflowProcess` e fornire nuovamente l&#39;accesso illimitato all&#39;intero archivio.

## Processi di controllo del flusso di lavoro {#workflow-control-processes}

I processi seguenti non eseguono alcuna azione sul contenuto. Servono a controllare il comportamento del flusso di lavoro stesso.

### AbsoluteTimeAutoAdvancer (Avanzamento automatico tempo assoluto) {#absolutetimeautoadvancer-absolute-time-auto-advancer}

Il processo `AbsoluteTimeAutoAdvancer` (Avanzamento automatico tempo assoluto) si comporta in modo identico a **Avanzamento automatico**, tranne per il fatto che si interrompe in un determinato momento e in una data specificata, anziché dopo un determinato periodo di tempo.

* **Classe Java™**: `com.adobe.granite.workflow.console.timeout.autoadvance.AbsoluteTimeAutoAdvancer`
* **Payload**: nessuno.
* **Argomenti**: nessuno.
* **Timeout**: timeout del processo quando vengono raggiunte l&#39;ora e la data impostate.

### Avanzamento automatico (Avanzamento automatico) {#autoadvancer-auto-advancer}

Il processo `AutoAdvancer` avanza automaticamente il flusso di lavoro al passaggio successivo. Se esiste più di un possibile passaggio successivo (ad esempio, se è presente una suddivisione OR), questo processo farà avanzare il flusso di lavoro lungo la *route predefinita*, se ne è stato specificato uno, altrimenti il flusso di lavoro non verrà avanzato.

* **Classe Java™**: `com.adobe.granite.workflow.console.timeout.autoadvance.AutoAdvancer`

* **Payload**: nessuno.
* **Argomenti**: nessuno.
* **Timeout**: timeout del processo dopo un periodo di tempo impostato.

### ProcessAssembler (Assemblatore processi) {#processassembler-process-assembler}

Il processo `ProcessAssembler` esegue più processi secondari in sequenza in un singolo passaggio del flusso di lavoro. Per utilizzare `ProcessAssembler`, creare un singolo passaggio di questo tipo nel flusso di lavoro e impostarne gli argomenti per indicare i nomi e gli argomenti dei processi secondari che si desidera eseguire.

* **Classe Java™**: `com.day.cq.workflow.impl.process.ProcessAssembler`

* **Payload**: una risorsa DAM, una pagina AEM o nessun payload (dipende dai requisiti dei sottoprocessi).
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

* **Timeout**: rispettato.

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
>Non modificare nulla nel percorso `/libs`.
>
>Il contenuto di `/libs` viene sovrascritto al successivo aggiornamento dell&#39;istanza e potrebbe essere sovrascritto quando si applica un hotfix o un feature pack.

### elimina {#delete}

L’elemento nel percorso specificato viene eliminato.

* **Percorso ECMAScript**: `/libs/workflow/scripts/delete.ecma`

* **Payload**: percorso JCR
* **Argomenti**: nessuno
* **Timeout**: ignorato

### noop {#noop}

Processo nullo. Non esegue alcuna operazione, ma registra un messaggio di debug.

* **Percorso ECMAScript**: `/libs/workflow/scripts/noop.ecma`

* **Payload**: nessuno
* **Argomenti**: nessuno
* **Timeout**: ignorato

### rule-false {#rule-false}

Processo null che restituisce `false` nel metodo `check()`.

* **Percorso ECMAScript**: `/libs/workflow/scripts/rule-false.ecma`

* **Payload**: nessuno
* **Argomenti**: nessuno
* **Timeout**: ignorato

### esempio {#sample}

Questo è un esempio di processo ECMAScript.

* **Percorso ECMAScript**: `/libs/workflow/scripts/sample.ecma`

* **Payload**: nessuno
* **Argomenti**: nessuno
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

* **Payload**: percorso JCR o UUID che fa riferimento a una pagina o a una risorsa DAM
* **Argomenti**: nessuno
* **Timeout**: rispettato
