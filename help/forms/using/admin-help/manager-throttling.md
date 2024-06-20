---
title: Gestione del lavoro e limitazione
description: Questo documento fornisce informazioni di base su Work Manager e istruzioni sulla configurazione delle opzioni di limitazione di Work Manager.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1f765de2-1362-4318-9302-c5036e6fa7d6
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1030'
ht-degree: 0%

---

# Gestione del lavoro e limitazione{#work-manager-and-throttling}

I moduli AEM (e versioni precedenti) utilizzavano code JMS per eseguire operazioni in modo asincrono. Nei moduli AEM, le code JMS sono state sostituite da Work Manager. Questo documento fornisce informazioni di base su Work Manager e istruzioni sulla configurazione delle opzioni di limitazione di Work Manager.

## Informazioni sulle operazioni di lunga durata (asincrone) {#about-long-lived-asynchronous-operations}

Nelle forme AEM, le operazioni eseguite dai servizi possono essere di breve durata (sincrone) o di lunga durata (asincrone). Operazioni di breve durata completate in modo sincrono sullo stesso thread da cui sono state richiamate. Queste operazioni attendono una risposta prima di continuare.

Le operazioni di lunga durata possono estendersi su più sistemi o anche oltre l&#39;organizzazione, ad esempio quando un cliente deve completare e inviare un modulo di richiesta di prestito come parte di una soluzione più ampia che integra più attività automatizzate e umane. Tali operazioni devono continuare in attesa di una risposta. Le operazioni di lunga durata eseguono il lavoro sottostante in modo asincrono, consentendo alle risorse di essere altrimenti impegnate in attesa di completamento. A differenza di un’operazione di breve durata, una volta richiamata, Work Manager non considera completata un’operazione di lunga durata. Per completare l&#39;operazione è necessario che venga eseguito un trigger esterno, ad esempio un sistema che richiede un&#39;altra operazione sullo stesso servizio o un utente che invia un modulo.

## Informazioni su Work Manager {#about-work-manager}

I moduli AEM (e versioni precedenti) utilizzavano code JMS per eseguire operazioni in modo asincrono. I moduli AEM utilizzano Work Manager per pianificare ed eseguire operazioni asincrone tramite thread gestiti.

Le operazioni asincrone vengono gestite in questo modo:

1. Work Manager riceve un elemento di lavoro per l&#39;esecuzione.
1. Work Manager memorizza l&#39;elemento di lavoro in una tabella di database e assegna un identificatore univoco all&#39;elemento di lavoro. Il record del database contiene tutte le informazioni necessarie per eseguire l&#39;elemento di lavoro.
1. I thread di Work Manager estraggono gli elementi di lavoro quando diventano liberi. Prima di estrarre gli elementi di lavoro, i thread possono verificare se i servizi richiesti sono stati avviati, se sono presenti dimensioni heap sufficienti per estrarre l&#39;elemento di lavoro successivo e se sono presenti cicli di CPU sufficienti per elaborare l&#39;elemento di lavoro. Work Manager valuta anche gli attributi dell’elemento di lavoro (come la sua priorità) durante la pianificazione dell’esecuzione.

Gli amministratori di moduli AEM possono utilizzare Monitoraggio integrità per verificare le statistiche di Gestione lavoro, ad esempio il numero di elementi di lavoro nella coda e i relativi stati. È inoltre possibile utilizzare Health Monitor per sospendere, riprendere, riprovare o eliminare elementi di lavoro. (vedere [Visualizzare le statistiche relative a Work Manager](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager).)

## Configurazione delle opzioni di limitazione di Work Manager {#configuring-work-manager-throttling-options}

È possibile configurare la limitazione per Work Manager in modo che gli elementi di lavoro vengano pianificati solo quando sono disponibili risorse di memoria sufficienti. Puoi configurare la limitazione impostando le seguenti opzioni JVM nel server applicazioni.

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
   <td><p>Specifica l'intervallo di tempo, in millisecondi, utilizzato da Work Manager per il controllo di nuovi elementi nella coda.</p><p>Il valore di questa opzione è un numero intero. Il valore predefinito è <code>1000</code> millisecondi (1 secondo). </p><p>Se il volume delle chiamate asincrone è basso, puoi aumentare questo valore. Ad esempio, è possibile aumentarlo tra 2000 e 5000 (2-5 secondi). </p><p>Se il volume delle chiamate asincrone è elevato, il valore predefinito dovrebbe essere sufficiente, ma se necessario è possibile utilizzare un valore inferiore. La riduzione eccessiva di questo valore (ad esempio, al di sotto di 50, che si traduce in una frequenza di polling di 20 volte al secondo) causa un notevole sovraccarico sul sistema.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.debug-mode-enabled</code></td>
   <td><p>Imposta questa opzione su <code>true</code> per attivare la modalità di debug o su false per disattivarla. </p><p>In modalità di debug, vengono registrati i messaggi relativi alle violazioni dei criteri di Work Manager e alle azioni di pausa/ripresa di Work Manager. Impostare questa opzione su true solo durante la risoluzione dei problemi.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.enabled</code></td>
   <td><p>Imposta questa opzione su <code>true</code> per abilitare la limitazione in base alle impostazioni di controllo della memoria descritte di seguito, oppure per <code>false</code> per disattivare la limitazione.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.high-limit</code></td>
   <td><p>Specifica la percentuale massima di memoria che può essere utilizzata prima che Work Manager limiti i processi in ingresso.</p><p>Il valore predefinito per questa opzione è <code>95</code>. Questo valore dovrebbe andare bene per la maggior parte dei sistemi. Aumentarla solo se il sistema deve raggiungere la capacità massima. Tuttavia, se si aumenta questo valore, aumenta anche il rischio di problemi di memoria insufficiente.</p><p>Se si eseguono moduli AEM in un ambiente cluster, è possibile impostare in modo diverso i limiti di controllo della memoria su nodi diversi del cluster. Ad esempio, potresti avere un limite alto inferiore sui nodi A e B, che sono programmati nel load balancer per il lavoro interattivo. E si potrebbero impostare limiti alti più alti sui nodi C e D, che non vengono utilizzati dal load balancer, ma sono riservati per il lavoro asincrono.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.low-limit</code></td>
   <td><p>Specifica la percentuale massima di memoria che può essere utilizzata prima che Work Manager interrompa la limitazione dei processi in ingresso.</p><p>Il valore predefinito per questa opzione è <code>20</code>. Questo valore dovrebbe andare bene per la maggior parte dei sistemi.</p></td>
  </tr>
  <tr>
   <td><code>Dadobe.workmanager.allocate.max-batch-size</code></td>
   <td><p>Specifica la dimensione batch massima per workmanager. La dimensione predefinita del batch è 10.</p><p>Se lo stato di un processo in Workmanager non viene aggiornato anche dopo il completamento dell'operazione, impostare la dimensione batch su 1.</p></td>
  </tr>
 </tbody>
</table>

**Aggiungere opzioni Java a JBoss**

1. Arresta il server applicazioni JBoss.
1. Apri *[directory principale del server applicazioni]*/bin/run.bat (Windows) o run.sh (Linux o UNIX) in un editor e aggiungi una qualsiasi delle opzioni Java necessarie, nel formato `-Dproperty=value`.
1. Riavviare il server.

**Aggiungere opzioni Java a WebLogic**

1. Avviare la console di amministrazione WebLogic digitando `https://[host name]:[port]/console` in un browser web.
1. Digitare il nome utente e la password creati per il dominio del server WebLogic e fare clic su Registra In Centro modifiche fare clic su Blocca e modifica.
1. In Struttura dominio fare clic su Ambiente > Server e nel riquadro di destra fare clic sul nome del server gestito.
1. Nella schermata successiva, fai clic sulla scheda Configurazione > scheda Avvio server.
1. Nella casella Argomenti aggiungere gli argomenti necessari alla fine del contenuto corrente. Ad esempio, per disabilitare Health Monitor, aggiungere:

   `-Dadobe.healthmonitor.enabled=false` disabilita Health Monitor.

1. Fai clic su Salva, quindi su Attiva modifiche.
1. Riavviare il server gestito WebLogic.

**Aggiungere opzioni Java a WebSphere**

1. Nella struttura di navigazione della Console di amministrazione WebSphere, fare clic su Server > Tipi di server > Application Server WebSphere.
1. Nel riquadro di destra fare clic sul nome del server.
1. In Infrastruttura server fare clic su Java e su Flusso di lavoro moduli > Definizione processo.
1. In Proprietà aggiuntive fare clic su Java Virtual Machine.
1. Nella casella Argomenti JVM generici digitare gli argomenti richiesti.
1. Fare clic su OK o Applica e quindi su Salva direttamente nella configurazione principale.
