---
title: Work Manager e limitazioni
description: Questo documento fornisce informazioni di base su Work Manager e istruzioni sulla relativa configurazione delle opzioni di limitazione.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1f765de2-1362-4318-9302-c5036e6fa7d6
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '1042'
ht-degree: 100%

---

# Work Manager e limitazioni{#work-manager-and-throttling}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

AEM Forms (e versioni precedenti) utilizzava code JMS per eseguire operazioni in modo asincrono. In AEM Forms, le code JMS sono state sostituite da Work Manager. Questo documento fornisce informazioni di base su Work Manager e istruzioni sulla relativa configurazione delle opzioni di limitazione.

## Informazioni sulle operazioni di lunga durata (asincrone) {#about-long-lived-asynchronous-operations}

Nei moduli di AEM, le operazioni eseguite dai servizi possono essere di breve durata (sincrone) o di lunga durata (asincrone). Operazioni di breve durata completate in modo sincrono sullo stesso thread da cui sono state richiamate. Queste operazioni attendono una risposta prima di continuare.

Le operazioni di lunga durata possono estendersi su più sistemi o anche oltre l’organizzazione, ad esempio quando un cliente deve completare e inviare un modulo di richiesta di prestito come parte di una soluzione più ampia che integra più attività automatizzate e umane. Tali operazioni devono continuare in attesa di una risposta. Le operazioni di lunga durata eseguono il lavoro sottostante in modo asincrono, consentendo alle risorse di essere altrimenti impegnate in attesa di completamento. A differenza di un’operazione di breve durata, Work Manager non considera completata un’operazione di lunga durata una volta richiamata. Per completare l’operazione è necessario che venga eseguito un trigger esterno, ad esempio un sistema che richiede un’altra operazione sullo stesso servizio o un utente che invia un modulo.

## Informazioni su Work Manager {#about-work-manager}

AEM Forms (e versioni precedenti) utilizzava code JMS per eseguire operazioni in modo asincrono. AEM Forms utilizza Work Manager per pianificare ed eseguire operazioni asincrone tramite thread gestiti.

Le operazioni asincrone vengono gestite in questo modo:

1. Work Manager riceve un elemento di lavoro per l’esecuzione.
1. Work Manager archivia l’elemento di lavoro in una tabella di database e assegna un identificatore univoco all’elemento di lavoro. Il record del database contiene tutte le informazioni necessarie per eseguire l’elemento di lavoro.
1. I thread di Work Manager acquisiscono gli elementi di lavoro quando diventano liberi. Prima di estrarre gli elementi di lavoro, i thread possono verificare se i servizi richiesti sono stati avviati, se la dimensione dell’heap disponibile è sufficiente per acquisire l’elemento di lavoro successivo e se il numero di cicli di CPU necessari per l’elaborazione dell’elemento di lavoro è sufficiente. Work Manager valuta anche gli attributi dell’elemento di lavoro (come la sua priorità) durante la pianificazione dell’esecuzione.

Gli amministratori di AEM Forms possono utilizzare Health Monitor per verificare le statistiche di Work Manager, ad esempio il numero di elementi di lavoro nella coda e i relativi stati. Puoi inoltre utilizzare Monitoraggio dello stato per sospendere, riprendere, riprovare o eliminare elementi di lavoro. Consulta [Visualizzare statistiche relative a Work Manager](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager).

## Configurazione delle opzioni di limitazione di Work Manager {#configuring-work-manager-throttling-options}

Puoi configurare la limitazione per Work Manager in modo che gli elementi di lavoro vengano pianificati solo quando sono disponibili risorse di memoria sufficienti. Puoi configurare la limitazione impostando le seguenti opzioni JVM nel server applicazioni.

<table>
 <thead>
  <tr>
   <th><p>Proprietà</p></th>
   <th><p>Descrizione</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><code> adobe.work-manager.queue-refill-interval</code></td>
   <td><p>Specifica l’intervallo di tempo, in millisecondi, utilizzato da Work Manager per il controllo di nuovi elementi nella coda.</p><p>Il valore di questa opzione è un numero intero. Il valore predefinito è pari a <code>1000</code> millisecondi (1 secondo). </p><p>Se il volume delle chiamate asincrone è basso, puoi aumentare questo valore. Ad esempio, è possibile aumentarlo tra 2000 e 5000 (2-5 secondi). </p><p>Se il volume delle chiamate asincrone è elevato, il valore predefinito dovrebbe essere sufficiente, ma se necessario è possibile utilizzare un valore inferiore. La riduzione eccessiva di questo valore (ad esempio, al di sotto di 50, che si traduce in una frequenza di polling di 20 volte al secondo) causa un notevole sovraccarico sul sistema.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.debug-mode-enabled</code></td>
   <td><p>Impostare questa opzione su <code>true</code> per abilitare la modalità di debug o su false per disabilitarla. </p><p>In modalità di debug, vengono registrati i messaggi relativi alle violazioni dei criteri di Work Manager e alle azioni di pausa/ripresa di Work Manager. Imposta questa opzione su true solo durante la risoluzione dei problemi.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.enabled</code></td>
   <td><p>Imposta questa opzione su <code>true</code> per abilitare la limitazione in base alle impostazioni di controllo della memoria descritte di seguito oppure su <code>false</code> per disabilitare la limitazione.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.high-limit</code></td>
   <td><p>Specifica la percentuale massima di memoria che può essere utilizzata prima che Work Manager limiti i processi in ingresso.</p><p>Il valore predefinito per questa opzione è <code>95</code>. Questo valore dovrebbe andare bene per la maggior parte dei sistemi. Aumentarla solo se il sistema deve raggiungere la capacità massima. Tuttavia, se si aumenta questo valore, aumenta anche il rischio di problemi di memoria insufficiente.</p><p>Se esegui AEM Forms in un ambiente cluster, puoi impostare i limiti di controllo della memoria in modo diverso su nodi diversi del cluster. Ad esempio, potresti avere un limite alto inferiore sui nodi A e B, che sono programmati nel load balancer per il lavoro interattivo. Inoltre, potresti impostare limiti alti più elevati sui nodi C e D, che non vengono utilizzati dal load balancer, ma sono riservati per il lavoro asincrono.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.low-limit</code></td>
   <td><p>Specifica la percentuale massima di memoria che può essere utilizzata prima che Work Manager interrompa la limitazione dei processi in ingresso.</p><p>Il valore predefinito per questa opzione è <code>20</code>. Questo valore dovrebbe andare bene per la maggior parte dei sistemi.</p></td>
  </tr>
  <tr>
   <td><code>Dadobe.workmanager.allocate.max-batch-size</code></td>
   <td><p>Specifica la dimensione batch massima per Work Manager. La dimensione dell’archivio per impostazione predefinita è 10.</p><p>Se lo stato di un processo in Work Manager non viene aggiornato anche dopo il completamento dell’operazione, imposta la dimensione batch su 1.</p></td>
  </tr>
 </tbody>
</table>

**Aggiungere opzioni Java a JBoss**

1. Arresta il server applicazioni di JBoss.
1. Apri la *[directory principale appserver]*/bin/run.bat (Windows) o run.sh (Linux o UNIX) in un editor e aggiungi le opzioni Java necessarie nel formato `-Dproperty=value`.
1. Riavvia il server.

**Aggiungere opzioni Java a WebLogic**

1. Avvia la console di amministrazione di WebLogic digitando `https://[host name]:[port]/console` in un browser web.
1. Digita il nome utente e la password creati per il dominio del server WebLogic e fai clic su Registra In Centro modifiche e su Blocca e modifica.
1. In Struttura dominio, fai clic su Ambiente > Server e nel riquadro di destra fai clic sul nome del server gestito.
1. Nella schermata successiva, fai clic sulla scheda Configurazione > scheda Avvio server.
1. Nella casella Argomenti, aggiungi gli argomenti necessari alla fine del contenuto corrente. Ad esempio, per disabilitare il Monitoraggio dello stato, aggiungi:

   `-Dadobe.healthmonitor.enabled=false` disabilita Monitoraggio dello stato.

1. Fai clic su Salva, quindi su Attiva modifiche.
1. Riavvia il server gestito da WebLogic.

**Aggiungere opzioni Java a WebSphere**

1. Nella struttura di navigazione della Console di amministrazione WebSphere, fai clic su Server > Tipi di server > Server applicazioni WebSphere.
1. Nel riquadro di destra, fai clic sul nome del server.
1. In Infrastruttura server fare fai clic su Java e Forms Workflow > Definizione processo.
1. In Proprietà aggiuntive, fai clic su Java Virtual Machine.
1. Nella casella Argomenti JVM generici digita gli argomenti richiesti.
1. Fai clic su OK o Applica e quindi su Salva direttamente nella configurazione principale.
