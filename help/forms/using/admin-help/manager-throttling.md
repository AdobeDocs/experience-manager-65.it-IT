---
title: Work Manager e limitazione
seo-title: Work Manager and throttling
description: Questo documento fornisce informazioni di base su Work Manager e fornisce istruzioni su come configurare le opzioni di limitazione di Work Manager.
seo-description: This document provides background information on Work Manager, and provides instructions on configuring Work Manager throttling options.
uuid: b90998bc-e3d4-493a-9371-55ccb44da20d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9a8b4e3a-f416-4dc6-a90a-9018df5c844e
exl-id: 1f765de2-1362-4318-9302-c5036e6fa7d6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 0%

---

# Work Manager e limitazione{#work-manager-and-throttling}

AEM forms (e versioni precedenti) utilizzavano code JMS per eseguire le operazioni in modo asincrono. Nei moduli AEM le code JMS sono state sostituite da Work Manager. Questo documento fornisce informazioni di base su Work Manager e fornisce istruzioni su come configurare le opzioni di limitazione di Work Manager.

## Informazioni sulle operazioni a lungo termine (asincrone) {#about-long-lived-asynchronous-operations}

In AEM forme, le operazioni eseguite dai servizi possono essere di breve durata (sincrona) o di lunga durata (asincrona). Operazioni di breve durata completate in modo sincrono sullo stesso thread da cui sono state richiamate. Queste operazioni attendono una risposta prima di continuare.

Le operazioni a lungo termine possono estendersi a sistemi o addirittura oltre l&#39;organizzazione, ad esempio quando un cliente deve completare e inviare un modulo di richiesta di prestito come parte di una soluzione più ampia che integra più attività automatizzate e umane. Tali operazioni devono continuare in attesa di una risposta. Le operazioni di lunga durata eseguono il lavoro sottostante in modo asincrono, consentendo l’utilizzo di risorse in altro modo in attesa del completamento. A differenza di un&#39;operazione di breve durata, Work Manager non considera un&#39;operazione di lunga durata completa una volta richiamata. Per completare l’operazione, è necessario che un trigger esterno, ad esempio un sistema che richiede un’altra operazione sullo stesso servizio o un utente che invia un modulo, si verifichi.

## Informazioni su Work Manager {#about-work-manager}

AEM forms (e versioni precedenti) utilizzavano code JMS per eseguire le operazioni in modo asincrono. AEM forms utilizza Work Manager per pianificare ed eseguire operazioni asincrone tramite thread gestiti.

Le operazioni asincrone vengono gestite in questo modo:

1. Work Manager riceve un elemento di lavoro da eseguire.
1. Work Manager memorizza l&#39;elemento di lavoro in una tabella di database e assegna un identificatore univoco all&#39;elemento di lavoro. Il record del database contiene tutte le informazioni necessarie per eseguire l&#39;elemento di lavoro.
1. I thread di Work Manager estraggono gli elementi di lavoro quando i thread diventano liberi. Prima di richiamare gli elementi di lavoro, i thread possono verificare se i servizi richiesti sono avviati, se vi sono dimensioni di heap sufficienti per richiamare l&#39;elemento di lavoro successivo e se ci sono abbastanza cicli CPU per elaborare l&#39;elemento di lavoro. Work Manager valuta anche gli attributi dell&#39;elemento di lavoro (ad esempio la sua priorità) quando ne pianifica l&#39;esecuzione.

AEM gli amministratori di moduli possono utilizzare Monitoraggio integrità per controllare le statistiche di Work Manager, ad esempio il numero di elementi di lavoro in coda e i relativi stati. È inoltre possibile utilizzare Health Monitor per mettere in pausa, riprendere, riprovare o eliminare elementi di lavoro. (Vedi [Visualizza le statistiche relative a Work Manager](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager).)

## Configurazione delle opzioni di limitazione di Work Manager {#configuring-work-manager-throttling-options}

È possibile configurare la limitazione per Work Manager in modo che gli elementi di lavoro vengano pianificati solo quando sono disponibili risorse di memoria sufficienti. Puoi configurare la limitazione impostando le seguenti opzioni JVM nel server delle applicazioni.

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
   <td><p>Specifica l'intervallo di tempo, in millisecondi, utilizzato da Work Manager per il controllo della presenza di nuovi elementi nella coda.</p><p>Il valore di questa opzione è un numero intero. Il valore predefinito è <code>1000</code> millisecondi (1 secondo). </p><p>Se il volume delle chiamate asincrone è basso, puoi aumentare questo valore. Ad esempio, puoi incrementarlo a un valore compreso tra 2000 e 5000 (da 2 a 5 secondi). </p><p>Se il volume delle chiamate asincrone è alto, il valore predefinito dovrebbe essere sufficiente, ma se necessario puoi utilizzare un valore inferiore. Diminuendo troppo questo valore (ad esempio, al di sotto di 50, che si traduce in una frequenza di sondaggio di 20 volte al secondo) si crea un notevole sovraccarico sul sistema.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.debug-mode-enabled</code></td>
   <td><p>Imposta questa opzione su <code>true</code> per abilitare la modalità di debug o su false per disattivarla. </p><p>In modalità di debug vengono registrati i messaggi relativi alle violazioni dei criteri di Work Manager e alle azioni di pausa/ripresa di Work Manager. Imposta questa opzione su true solo per la risoluzione dei problemi.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.enabled</code></td>
   <td><p>Imposta questa opzione su <code>true</code> per abilitare la limitazione in base alle impostazioni di controllo della memoria descritte di seguito, oppure <code>false</code> per disabilitare la limitazione.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.high-limit</code></td>
   <td><p>Specifica la percentuale massima di memoria che può essere utilizzata prima che Work Manager limiti i processi in arrivo.</p><p>Il valore predefinito per questa opzione è <code>95</code>. Questo valore deve essere valido per la maggior parte dei sistemi. Aumentalo solo se il sistema deve passare alla sua capacità massima. Ma si noti che aumentando questo valore, aumenta anche il rischio di problemi di memoria esaurita.</p><p>Se si eseguono AEM moduli in un ambiente cluster, è possibile impostare le impostazioni dei limiti di controllo della memoria in modo diverso su diversi nodi del cluster. Ad esempio, potresti avere un limite alto inferiore sui nodi A e B, che sono programmati nel load balancer per il lavoro interattivo. E si potrebbero impostare limiti massimi più alti sui nodi C e D, che non sono usati dal load balancer, ma riservati al lavoro asincrono.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.low-limit</code></td>
   <td><p>Specifica la percentuale massima di memoria che può essere utilizzata prima che Work Manager smetta di limitare i processi in arrivo.</p><p>Il valore predefinito per questa opzione è <code>20</code>. Questo valore deve essere valido per la maggior parte dei sistemi.</p></td>
  </tr>
  <tr>
   <td><code>Dadobe.workmanager.allocate.max-batch-size</code></td>
   <td><p>Specifica la dimensione batch massima per workmanager. La dimensione predefinita del batch è 10.</p><p>Se lo stato di un processo in workmanager non viene aggiornato anche dopo il completamento dell'attività, impostare la dimensione del batch su 1.</p></td>
  </tr>
 </tbody>
</table>

**Aggiungi opzioni Java a JBoss**

1. Arresta il server dell&#39;applicazione JBoss.
1. Apri *[root appserver]*/bin/run.bat (Windows) o run.sh (Linux o UNIX) in un editor e aggiungi una qualsiasi delle opzioni Java secondo necessità, nel formato `-Dproperty=value`.
1. Riavvia il server.

**Aggiungi opzioni Java a WebLogic**

1. Avvia la console di amministrazione di WebLogic digitando `https://[host name]:[port]/console` in un browser web.
1. Digita il nome utente e la password creati per il dominio del server WebLogic e fai clic su Log Under Change Center, quindi fai clic su Lock &amp; Edit.
1. In Struttura del dominio, fai clic su Ambiente > Server e, nel riquadro a destra, fai clic sul nome del server gestito.
1. Nella schermata successiva, fai clic sulla scheda Configurazione > Avvio server .
1. Nella casella Argomenti , aggiungi gli argomenti necessari alla fine del contenuto corrente. Ad esempio, per disabilitare Health Monitor, aggiungi:

   `-Dadobe.healthmonitor.enabled=false` disabilita Monitoraggio integrità.

1. Fare clic su Salva e quindi su Attiva modifiche.
1. Riavvia il server gestito WebLogic.

**Aggiungi opzioni Java a WebSphere**

1. Nella struttura di navigazione Console amministrativa WebSphere, fare clic su Server > Tipi di server > Server applicazioni WebSphere.
1. Nel riquadro a destra, fare clic sul nome del server.
1. In Infrastruttura server, fai clic su Flusso di lavoro Java e moduli > Definizione del processo.
1. In Proprietà aggiuntive fare clic su Java Virtual Machine.
1. Nella casella Argomenti JVM generici digitare gli argomenti necessari.
1. Fare clic su OK o Applica, quindi fare clic su Salva direttamente nella configurazione principale.
