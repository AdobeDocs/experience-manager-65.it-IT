---
title: Risoluzione dei problemi di Adobe Experience Manager
description: Scopri come risolvere alcuni problemi che potrebbero verificarsi con Adobe Experience Manager.
uuid: 72379531-915c-45d0-ba70-42b212665272
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6346cd93-1ca3-4510-9c31-a74c41017ddb
docset: aem65
exl-id: d2d351e7-87a5-4895-b4ec-391fb0b66798
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 4%

---

# Risoluzione dei problemi di Adobe Experience Manager {#troubleshooting-aem}

Nella sezione seguente vengono descritti alcuni problemi che possono verificarsi durante l’utilizzo di AEM (Adobe Experience Manager) e vengono proposte possibili soluzioni.

>[!NOTE]
>
>Se stai risolvendo problemi di authoring in AEM, consulta [Risoluzione dei problemi per gli autori.](/help/sites-authoring/troubleshooting.md)

>[!NOTE]
>
>Quando si verificano problemi, vale anche la pena controllare l’elenco di [Problemi noti](/help/release-notes/release-notes.md) per la tua istanza (release e service pack).

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

1. Apri **Console web AEM**; ad esempio, in `https://localhost:4502/system/console/`.
1. Seleziona la **Threads** in **Stato** scheda.

![screen_shot_2012-02-13at43925pm](assets/screen_shot_2012-02-13at43925pm.png)

### Utilizzo di jstack (riga di comando) {#using-jstack-command-line}

1. Trova il PID (ID processo) dell’istanza Java™ dell’AEM.

   Ad esempio, puoi utilizzare `ps -ef` o `jps`.

1. Esegui:

   `jstack <pid>`

1. Mostra l’immagine thread.

>[!NOTE]
>
>È possibile aggiungere le immagini thread a un file di registro utilizzando `>>` reindirizzamento output:
>
>`jstack <pid> >> /path/to/logfile.log`

Consulta la [Come prendere Thread Dumps da una JVM](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17452.html?lang=it) per ulteriori informazioni

### Verifica di sessioni JCR non chiuse {#checking-for-unclosed-jcr-sessions}

Quando viene sviluppata la funzionalità per AEM WCM, è possibile aprire le sessioni JCR (come per l’apertura di una connessione al database). Se le sessioni aperte non vengono mai chiuse, il sistema potrebbe presentare i seguenti sintomi:

* Il sistema diventa più lento.
* È possibile visualizzare gran parte di CacheManager: resizeAll voci nel file di registro; il seguente numero (size=&lt;x>) mostra il numero di cache, ogni sessione apre diverse cache.
* Di tanto in tanto il sistema esaurisce la memoria (dopo alcune ore, giorni o settimane, a seconda della gravità).

Per analizzare le sessioni non chiuse e individuare il codice che non chiude una sessione, vedere l&#39;articolo della Knowledge Base [Analizza sessioni non chiuse](https://helpx.adobe.com/experience-manager/kb/AnalyzeUnclosedSessions.html).

### Utilizzo della console Web di Adobe Experience Manager {#using-the-adobe-experience-manager-web-console}

Lo stato dei bundle OSGi può anche fornire un’indicazione anticipata di possibili problemi.

1. Apri **Console web AEM**; ad esempio, in `https://localhost:4502/system/console/`.
1. Seleziona **Bundle** in **OSGI** scheda.
1. Seleziona:

   * lo stato dei bundle. In caso contrario, prova ad arrestare e riavviare il bundle. Se il problema persiste, approfondisci ulteriormente utilizzando altri metodi.
   * se uno dei bundle presenta dipendenze mancanti. Per visualizzare tali dettagli, fai clic sul nome del singolo bundle, che è un collegamento (il seguente esempio non presenta alcun problema):

![screen_shot_2012-02-13at44706pm](assets/screen_shot_2012-02-13at44706pm.png)
