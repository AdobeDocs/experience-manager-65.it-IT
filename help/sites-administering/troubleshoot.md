---
title: Risoluzione dei problemi AEM
seo-title: Risoluzione dei problemi AEM
description: Scopri come risolvere i problemi con AEM.
seo-description: Scopri come risolvere i problemi con AEM.
uuid: 72379531-915c-45d0-ba70-42b212665272
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6346cd93-1ca3-4510-9c31-a74c41017ddb
docset: aem65
translation-type: tm+mt
source-git-commit: 4b965d8f7814816126601f6366c1ba313e404538

---


# Risoluzione dei problemi AEM {#troubleshooting-aem}

La sezione seguente illustra alcuni problemi che potrebbero verificarsi durante l’utilizzo di AEM e suggerisce come risolvere eventuali problemi.

>[!NOTE]
>
>Se state risolvendo problemi di authoring in AEM, consultate Risoluzione dei [problemi per gli autori.](/help/sites-authoring/troubleshooting.md)

>[!NOTE]
>
>Quando si verificano problemi, è anche utile controllare l’elenco dei [Problemi noti](/help/release-notes/known-issues.md) per l’istanza (release e service pack).

## Scenari di risoluzione dei problemi per gli amministratori {#troubleshooting-scenarios-for-administrators}

La tabella seguente fornisce una panoramica dei problemi che gli amministratori possono dover risolvere:

<table>
 <tbody>
  <tr>
   <td><strong>Ruoli</strong></td>
   <td><strong>Problema </strong></td>
  </tr>
  <tr>
   <td>Amministratore di sistema</td>
   <td><p>Se si fa doppio clic sul file JAR non si verifica alcun effetto o si apre il file JAR con un altro programma (ad esempio, archive manager)</p> </td>
  </tr>
  <tr>
   <td><p>Amministratore di sistema</p> </td>
   <td><p>La mia applicazione in esecuzione su CRX genera errori di memoria insufficiente</p> </td>
  </tr>
  <tr>
   <td><p>Amministratore di sistema</p> </td>
   <td><p>La schermata introduttiva di AEM non viene visualizzata nel browser dopo aver fatto doppio clic su Avvio rapido di AEM CM</p> </td>
  </tr>
  <tr>
   <td><p>Amministratore di sistema</p> <p>admin, utente</p> </td>
   <td><p>Creazione di un dump del thread</p> </td>
  </tr>
  <tr>
   <td><p>Amministratore di sistema</p> <p>admin, utente</p> </td>
   <td><p>Verifica delle sessioni JCR non chiuse</p> </td>
  </tr>
 </tbody>
</table>

## Problemi di installazione {#installation-issues}

Consultate Problemi [](/help/sites-deploying/troubleshooting.md#common-installation-issues) comuni di installazione per informazioni sui seguenti scenari di risoluzione dei problemi:

* Un doppio clic sul jar Quickstart non ha alcun effetto oppure il file JAR viene aperto in un altro programma (ad esempio un gestore di archivi).
* Le applicazioni eseguite su CRX generano errori di esaurimento della memoria.
* La schermata di benvenuto di AEM non viene visualizzata nel browser quando si fa doppio clic su AEM Quickstart.

## Metodi per la risoluzione dei problemi di analisi {#methods-for-troubleshooting-analysis}

### Creazione di un dump del thread {#making-a-thread-dump}

Il dump del thread è un elenco di tutti i thread Java attualmente attivi. Se AEM non risponde correttamente, il dump del thread può aiutarti a identificare i punti critici o altri problemi.

### Utilizzo di Sling Thread Dumer {#using-sling-thread-dumper}

1. Aprite la console **Web di** AEM; ad esempio in `https://localhost:4502/system/console/`.
1. Selezionare i **thread** nella **scheda Stato** .

![screen_shot_2012-02-13at43925pm](assets/screen_shot_2012-02-13at43925pm.png)

### Utilizzo di jstack (riga di comando) {#using-jstack-command-line}

1. Individua il PID (ID processo) dell’istanza AEM Java.

   Ad esempio, potete utilizzare `ps -ef` o `jps`.

1. Esegui:

   `jstack <pid>`

1. Verrà visualizzato il dump del thread.

>[!NOTE]
>
>È possibile aggiungere i file di thread a un file di registro utilizzando il reindirizzamento `>>` di output:
>
>`jstack <pid> >> /path/to/logfile.log`

Per ulteriori informazioni, consulta [How to take Thread Dumps from a JVM](https://helpx.adobe.com/cq/kb/TakeThreadDump.html) documentation.

### Verifica delle sessioni JCR non chiuse {#checking-for-unclosed-jcr-sessions}

Quando vengono sviluppate funzionalità per AEM WCM, è possibile aprire le sessioni JCR (paragonabili all&#39;apertura di una connessione al database). Se le sessioni aperte non vengono mai chiuse, il sistema potrebbe presentare i seguenti sintomi:

* Il sistema diventa più lento.
* È possibile vedere molti CacheManager: ridimensionaTutte le voci nel file di registro; il numero seguente (size=&lt;x>) mostra il numero di cache, ogni sessione apre diverse cache.
* Di tanto in tanto il sistema non dispone di memoria sufficiente (dopo alcune ore, giorni o settimane, a seconda della gravità).

Per analizzare le sessioni non chiuse e scoprire quale codice non sta chiudendo una sessione, fare riferimento all&#39;articolo Knowledge Base [Analisi delle sessioni](https://helpx.adobe.com/crx/kb/AnalyzeUnclosedSessions.html)non chiuse.

### Utilizzo della console Web di Adobe Experience Manager {#using-the-adobe-experience-manager-web-console}

Lo stato dei bundle OSGi può anche fornire un&#39;indicazione tempestiva dei possibili problemi.

1. Aprite la console **Web di** AEM; ad esempio in `https://localhost:4502/system/console/`.
1. Selezionate **Bundle** nella scheda **OSGI** .
1. Seleziona:

   * lo stato dei bundle. Se sono inattivi o non soddisfatti, provare a arrestare e riavviare il bundle. Se il problema persiste, potrebbe essere necessario approfondire l&#39;analisi utilizzando altri metodi.
   * se uno dei bundle dispone di dipendenze mancanti. Tali dettagli possono essere visualizzati facendo clic sul singolo nome del bundle, che è un collegamento (l&#39;esempio seguente non presenta problemi):

![screen_shot_2012-02-13at44706pm](assets/screen_shot_2012-02-13at44706pm.png)

