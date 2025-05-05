---
title: Risoluzione dei problemi di Adobe Experience Manager
description: Scopri come risolvere alcuni problemi che potrebbero verificarsi con Adobe Experience Manager.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: d2d351e7-87a5-4895-b4ec-391fb0b66798
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 2%

---

# Risoluzione dei problemi di Adobe Experience Manager {#troubleshooting-aem}

Nella sezione seguente vengono descritti alcuni problemi che possono verificarsi durante l’utilizzo di AEM (Adobe Experience Manager) e vengono proposte possibili soluzioni.

>[!NOTE]
>
>Se stai risolvendo problemi di authoring in AEM, consulta [Risoluzione dei problemi per gli autori.](/help/sites-authoring/troubleshooting.md)

>[!NOTE]
>
>In caso di problemi, vale la pena controllare anche l&#39;elenco di [problemi noti](/help/release-notes/release-notes.md) per la tua istanza (pacchetti di versioni e service pack).

## Risoluzione dei problemi relativi agli amministratori {#troubleshooting-scenarios-for-administrators}

La tabella seguente fornisce una panoramica dei problemi che gli amministratori possono risolvere:

<table>
 <tbody>
  <tr>
   <td><strong>Ruolo</strong></td>
   <td><strong>Problema </strong></td>
  </tr>
  <tr>
   <td>Amministratore di sistema</td>
   <td><p>Se si fa doppio clic sul file jar Quickstart, questo non ha alcun effetto o il file jar viene aperto con un altro programma (ad esempio, Archive Manager)</p> </td>
  </tr>
  <tr>
   <td><p>Amministratore di sistema</p> </td>
   <td><p>La mia applicazione in esecuzione su CRX genera errori di memoria insufficiente</p> </td>
  </tr>
  <tr>
   <td><p>Amministratore di sistema</p> </td>
   <td><p>La schermata iniziale dell’AEM non viene visualizzata nel browser dopo aver fatto doppio clic su AEM CM Quickstart</p> </td>
  </tr>
  <tr>
   <td><p>Amministratore di sistema</p> <p>utente amministratore</p> </td>
   <td><p>Creazione di un'immagine thread</p> </td>
  </tr>
  <tr>
   <td><p>Amministratore di sistema</p> <p>utente amministratore</p> </td>
   <td><p>Verifica di sessioni JCR non chiuse</p> </td>
  </tr>
 </tbody>
</table>

## Problemi di installazione {#installation-issues}

Consulta [Problemi comuni di installazione](/help/sites-deploying/troubleshooting.md#common-installation-issues) per informazioni sui seguenti scenari di risoluzione dei problemi:

* Il doppio clic sul file JAR Quickstart non ha alcun effetto o sul file JAR con un altro programma (ad esempio, Archive Manager).
* Le applicazioni in esecuzione su CRX generano errori di memoria insufficiente.
* La schermata iniziale dell’AEM non viene visualizzata nel browser dopo aver fatto doppio clic su AEM Quickstart.

## Metodi per la risoluzione dei problemi di analisi {#methods-for-troubleshooting-analysis}

### Creazione di un&#39;immagine thread {#making-a-thread-dump}

L’immagine thread è un elenco di tutti i thread Java™ attualmente attivi. Se l’AEM non risponde correttamente, l’immagine thread può aiutarti a identificare deadlock o altri problemi.

### Utilizzo di Sling Thread Dumper {#using-sling-thread-dumper}

1. Apri la **console Web AEM**, ad esempio in `https://localhost:4502/system/console/`.
1. Selezionare la scheda **Threads** in **Stato**.

![schermata_shot_2012-02-13alle43925pm](assets/screen_shot_2012-02-13at43925pm.png)

### Utilizzo di jstack (riga di comando) {#using-jstack-command-line}

1. Trova il PID (ID processo) dell’istanza Java™ dell’AEM.

   È possibile, ad esempio, utilizzare `ps -ef` o `jps`.

1. Esegui:

   `jstack <pid>`

1. Mostra l’immagine thread.

>[!NOTE]
>
>È possibile aggiungere le immagini thread a un file di registro utilizzando il reindirizzamento di output `>>`:
>
>`jstack <pid> >> /path/to/logfile.log`

Per ulteriori informazioni, consulta la [documentazione su come estrarre immagini thread da una JVM](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17452.html?lang=it)

### Verifica di sessioni JCR non chiuse {#checking-for-unclosed-jcr-sessions}

Quando viene sviluppata la funzionalità per AEM WCM, è possibile aprire le sessioni JCR (come per l’apertura di una connessione al database). Se le sessioni aperte non vengono mai chiuse, il sistema potrebbe presentare i seguenti sintomi:

* Il sistema diventa più lento.
* È possibile visualizzare gran parte di CacheManager: resizeAll voci nel file di registro; il seguente numero (size=&lt;x>) mostra il numero di cache, ogni sessione apre diverse cache.
* Di tanto in tanto il sistema esaurisce la memoria (dopo alcune ore, giorni o settimane, a seconda della gravità).

Per analizzare le sessioni non chiuse e individuare il codice che non chiude una sessione, vedere l&#39;articolo della Knowledge Base [Analisi delle sessioni non chiuse](https://helpx.adobe.com/experience-manager/kb/AnalyzeUnclosedSessions.html).

### Utilizzo della console Web di Adobe Experience Manager {#using-the-adobe-experience-manager-web-console}

Lo stato dei bundle OSGi può anche fornire un’indicazione anticipata di possibili problemi.

1. Apri la **console Web AEM**, ad esempio in `https://localhost:4502/system/console/`.
1. Seleziona **Bundle** nella scheda **OSGI**.
1. Seleziona:

   * lo stato dei bundle. In caso contrario, prova ad arrestare e riavviare il bundle. Se il problema persiste, approfondisci ulteriormente utilizzando altri metodi.
   * se uno dei bundle presenta dipendenze mancanti. Per visualizzare tali dettagli, fai clic sul nome del singolo bundle, che è un collegamento (il seguente esempio non presenta alcun problema):

![schermata_shot_2012-02-13alle44706pm](assets/screen_shot_2012-02-13at44706pm.png)
