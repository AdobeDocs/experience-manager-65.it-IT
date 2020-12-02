---
title: Gestione del lavoro e limitazione
seo-title: Gestione del lavoro e limitazione
description: Questo documento fornisce informazioni di base su Work Manager e istruzioni sulla configurazione delle opzioni di limitazione di Work Manager.
seo-description: Questo documento fornisce informazioni di base su Work Manager e istruzioni sulla configurazione delle opzioni di limitazione di Work Manager.
uuid: b90998bc-e3d4-493a-9371-55ccb44da20d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9a8b4e3a-f416-4dc6-a90a-9018df5c844e
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '1044'
ht-degree: 0%

---


# Gestione del lavoro e limitazione{#work-manager-and-throttling}

AEM moduli (e versioni precedenti) utilizzavano code JMS per eseguire le operazioni in modo asincrono. Nei AEM moduli, le code JMS sono state sostituite da Work Manager. Questo documento fornisce informazioni di base su Work Manager e istruzioni sulla configurazione delle opzioni di limitazione di Work Manager.

## Informazioni sulle operazioni longeve (asincrone) {#about-long-lived-asynchronous-operations}

Nei AEM moduli, le operazioni eseguite dai servizi possono essere di breve durata (sincrona) o di lunga durata (asincrona). Le operazioni di breve durata vengono completate in modo sincrono sullo stesso thread da cui sono state richiamate. Queste operazioni attendono una risposta prima di continuare.

Le operazioni di lunga durata possono estendersi anche oltre l&#39;organizzazione, ad esempio quando un cliente deve completare e inviare un modulo di richiesta di prestito come parte di una soluzione più ampia che integra molteplici attività automatizzate e umane. Tali operazioni devono proseguire in attesa di una risposta. Le operazioni di lunga durata eseguono il lavoro sottostante in modo asincrono, consentendo il coinvolgimento delle risorse in attesa del completamento. A differenza di un&#39;operazione di breve durata, Work Manager non considera un&#39;operazione di lunga durata completata una volta richiamata. Per completare l&#39;operazione, è necessario che venga eseguito un trigger esterno, ad esempio un sistema che richiede un&#39;altra operazione sullo stesso servizio o un utente che invia un modulo.

## Informazioni su Work Manager {#about-work-manager}

AEM moduli (e versioni precedenti) utilizzavano code JMS per eseguire le operazioni in modo asincrono. AEM moduli utilizza Work Manager per pianificare ed eseguire operazioni asincrone tramite thread gestiti.

Le operazioni asincrone vengono gestite in questo modo:

1. Work Manager riceve un elemento di lavoro per l&#39;esecuzione.
1. Work Manager memorizza l&#39;elemento di lavoro in una tabella di database e assegna un identificatore univoco all&#39;elemento di lavoro. Il record del database contiene tutte le informazioni necessarie per eseguire l&#39;elemento di lavoro.
1. I thread di Work Manager estraggono gli elementi di lavoro quando i thread diventano gratuiti. Prima di eseguire il pulling degli elementi di lavoro, i thread possono verificare se i servizi richiesti sono stati avviati, se la dimensione dell&#39;heap è sufficiente per eseguire il pulling dell&#39;elemento di lavoro successivo e se sono disponibili cicli CPU sufficienti per elaborare l&#39;elemento di lavoro. Work Manager valuta anche gli attributi dell&#39;elemento di lavoro (ad esempio la sua priorità) quando ne pianifica l&#39;esecuzione.

AEM gli amministratori dei moduli possono utilizzare il monitoraggio integrità per controllare le statistiche di Work Manager, ad esempio il numero di elementi di lavoro nella coda e i relativi stati. È inoltre possibile utilizzare Health Monitor per mettere in pausa, riprendere, riprovare o eliminare elementi di lavoro. (Vedere [Visualizzare le statistiche relative a Work Manager](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager).)

## Configurazione delle opzioni di limitazione di Work Manager {#configuring-work-manager-throttling-options}

È possibile configurare la limitazione per Work Manager in modo che gli elementi di lavoro siano pianificati solo quando sono disponibili risorse di memoria sufficienti. È possibile configurare la limitazione impostando le seguenti opzioni JVM nel server dell&#39;applicazione.

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
   <td><p>Specifica l'intervallo di tempo, in millisecondi, utilizzato da Work Manager per verificare la presenza di nuovi elementi nella coda.</p><p>Il valore di questa opzione è un numero intero. Il valore predefinito è <code>1000</code> millisecondi (1 secondo). </p><p>Se il volume delle chiamate asincrone è basso, potete aumentare questo valore. Ad esempio, potete aumentare il valore in un intervallo compreso tra 2000 e 5000 (da 2 a 5 secondi). </p><p>Se il volume delle chiamate asincrone è elevato, il valore predefinito deve essere sufficiente, ma se necessario potete utilizzare un valore inferiore. Se si riduce troppo questo valore (ad esempio, al di sotto di 50, con una frequenza di sondaggio di 20 volte al secondo), si verifica un sovraccarico notevole del sistema.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.debug-mode-enabled</code></td>
   <td><p>Impostate questa opzione su <code>true</code> per abilitare la modalità di debug o su false per disattivarla. </p><p>In modalità debug, i messaggi relativi alle violazioni dei criteri di Work Manager e alle azioni di pausa/ripresa di Work Manager vengono registrati. Impostate questa opzione su true solo per la risoluzione dei problemi.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.enabled</code></td>
   <td><p>Impostare questa opzione su <code>true</code> per abilitare la limitazione in base alle impostazioni del controllo della memoria descritte di seguito, oppure su <code>false</code> per disabilitare la limitazione.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.high-limit</code></td>
   <td><p>Specifica la percentuale massima di memoria che può essere utilizzata prima che Work Manager limiti i processi in arrivo.</p><p>Il valore predefinito per questa opzione è <code>95</code>. Questo valore deve essere valido per la maggior parte dei sistemi. Aumentarlo solo se il sistema deve raggiungere la capacità massima. Ma tenete presente che, aumentando questo valore, aumenta anche il rischio di problemi di memoria insufficiente.</p><p>Se si esegue AEM moduli in un ambiente cluster, è possibile impostare le impostazioni dei limiti di controllo della memoria in modo diverso su nodi diversi del cluster. Ad esempio, potete avere un limite massimo inferiore per i nodi A e B, programmati nel sistema di bilanciamento del carico per il lavoro interattivo. E si potrebbero impostare limiti più alti sui nodi C e D, che non vengono usati dal sistema di bilanciamento del carico, ma riservati al lavoro asincrono.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.low-limit</code></td>
   <td><p>Specifica la percentuale massima di memoria che può essere utilizzata prima che Work Manager interrompa la limitazione dei processi in arrivo.</p><p>Il valore predefinito per questa opzione è <code>20</code>. Questo valore deve essere valido per la maggior parte dei sistemi.</p></td>
  </tr>
  <tr>
   <td><code>Dadobe.workmanager.allocate.max-batch-size</code></td>
   <td><p>Specifica la dimensione batch massima per workmanager. La dimensione predefinita del batch è 10.</p><p>Se lo stato di un processo in workmanager non viene aggiornato anche dopo il completamento dell'attività, impostare la dimensione batch su 1.</p></td>
  </tr>
 </tbody>
</table>

**Aggiungere opzioni Java a JBoss**

1. Arrestate il server applicazioni JBoss.
1. Aprite la *[directory principale dell&#39;appserver]*/bin/run.bat (Windows) o run.sh (Linux o UNIX) in un editor e aggiungete le opzioni Java richieste nel formato `-Dproperty=value`.
1. Riavviate il server.

**Aggiunta di opzioni Java a WebLogic**

1. Avviate la console di amministrazione WebLogic digitando `https://[host name]:[port]/console` in un browser Web.
1. Digitare il nome utente e la password creati per il dominio WebLogic Server e fare clic su Log In Change Center, quindi fare clic su Lock &amp; Edit (Blocca e modifica).
1. In Struttura dominio, fare clic su Ambiente > Server e, nel riquadro a destra, fare clic sul nome del server gestito.
1. Nella schermata successiva, fate clic sulla scheda Configurazione > scheda Avvio server.
1. Nella casella Argomenti, aggiungere gli argomenti richiesti alla fine del contenuto corrente. Ad esempio, per disattivare il monitoraggio integrità, aggiungete:

   `-Dadobe.healthmonitor.enabled=false` disattiva il monitoraggio integrità.

1. Fate clic su Salva, quindi su Attiva modifiche.
1. Riavviare il server gestito WebLogic.

**Aggiungere opzioni Java a WebSphere**

1. Nella struttura di navigazione della console di amministrazione di WebSphere, fare clic su Server > Tipi di server > Server applicazioni WebSphere.
1. Nel riquadro a destra, fare clic sul nome del server.
1. In Infrastruttura server, fare clic su Flusso di lavoro Java e moduli > Definizione processo.
1. In Proprietà aggiuntive fare clic su Java Virtual Machine.
1. Nella casella Argomenti JVM generici, digitare gli argomenti richiesti.
1. Fate clic su OK o Applica, quindi fate clic su Salva direttamente nella configurazione principale.

