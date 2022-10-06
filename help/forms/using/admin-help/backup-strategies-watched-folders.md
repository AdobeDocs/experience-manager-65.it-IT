---
title: Strategie di backup per le cartelle controllate
seo-title: Backup strategies for watched folders
description: Questo documento descrive come le cartelle controllate sono influenzate da diversi scenari di backup e ripristino, dai limiti e dai risultati di questi scenari e come ridurre al minimo la perdita di dati.
seo-description: This document describes how watched folders are affected by different backup and recovery scenarios, the limitations and outcomes of these scenarios, and how to minimize data loss.
uuid: c61997b8-6c36-4bd9-90e5-411841a6c176
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6f775933-e989-4456-ad01-9bdf5dee3dad
exl-id: 0d36160a-29fa-4cc4-a0ff-fc681d3e040e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1090'
ht-degree: 2%

---

# Strategie di backup per le cartelle controllate {#backup-strategies-for-watched-folders}

Questo contenuto descrive come le cartelle controllate sono influenzate da diversi scenari di backup e ripristino, dai limiti e dai risultati di questi scenari e come ridurre al minimo la perdita di dati.

*Cartella osservata* è un&#39;applicazione basata su file system che richiama le operazioni di servizio configurate che manipolano il file all&#39;interno di una delle seguenti cartelle nella gerarchia delle cartelle controllate:

* Input
* Area di visualizzazione
* Output
* Errore
* Mantieni

Un utente o un&#39;applicazione client rilascia prima il file o la cartella nella cartella di input. L’operazione del servizio quindi sposta il file nella cartella dell’area di visualizzazione per l’elaborazione. Dopo che il servizio esegue l&#39;operazione specificata, salva il file modificato nella cartella di output. I file di origine elaborati correttamente vengono spostati nella cartella di conservazione e i file di elaborazione non riusciti vengono spostati nella cartella di errore. Quando il `Preserve On Failure` l&#39;attributo per la cartella controllata è abilitato. I file di origine elaborati non riusciti vengono spostati nella cartella preserve. (Vedi [Configurazione degli endpoint della cartella controllati](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#configuring-watched-folder-endpoints).)

È possibile eseguire il backup delle cartelle controllate effettuando il backup del file system.

>[!NOTE]
>
>Questo backup è indipendente dal processo di backup e ripristino dello storage del database o del documento.

## Funzionamento delle cartelle controllate {#how-watched-folders-work}

Questo contenuto descrive il processo di manipolazione dei file delle cartelle controllate. È importante comprendere questo processo prima di sviluppare un piano di ripresa. In questo esempio, la `Preserve On Failure` l&#39;attributo per la cartella controllata è abilitato. I file vengono elaborati nell’ordine in cui arrivano.

La tabella seguente descrive la manipolazione dei file di cinque file di esempio (file1, file2, file3, file4, file5) durante l&#39;intero processo. Nella tabella, l&#39;asse x rappresenta il tempo, ad esempio il tempo 1 o T1, e l&#39;asse y rappresenta le cartelle all&#39;interno della gerarchia di cartelle controllata, ad esempio Input.

<table>
 <thead>
  <tr>
   <th><p>Cartella</p></th>
   <th><p>T1</p></th>
   <th><p>T2</p></th>
   <th><p>T3</p></th>
   <th><p>T4</p></th>
   <th><p>T5</p></th>
   <th><p>T6</p></th>
   <th><p>T7</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Ingresso</p></td>
   <td><p>file1, file2, file3, file4</p></td>
   <td><p>file2, file3, file4</p></td>
   <td><p>file3, file4</p></td>
   <td><p>file4</p></td>
   <td><p>vuoto</p></td>
   <td><p>file5</p></td>
   <td><p>vuoto</p></td>
  </tr>
  <tr>
   <td><p>Area di visualizzazione</p></td>
   <td><p>vuoto</p></td>
   <td><p>file1</p></td>
   <td><p>file2</p></td>
   <td><p>file3</p></td>
   <td><p>file4</p></td>
   <td><p>vuoto</p></td>
   <td><p>file5</p></td>
  </tr>
  <tr>
   <td><p>Uscita</p></td>
   <td><p>vuoto</p></td>
   <td><p>vuoto</p></td>
   <td><p>file1_out</p></td>
   <td><p>file1_out, file2_out</p></td>
   <td><p>file1_out, file2_out</p></td>
   <td><p>file1_out, file2_out, file4_out</p></td>
   <td><p>file1_out, file2_out, file4_out</p></td>
  </tr>
  <tr>
   <td><p>Errore</p></td>
   <td><p>vuoto</p></td>
   <td><p>vuoto</p></td>
   <td><p>vuoto</p></td>
   <td><p>vuoto</p></td>
   <td><p>file3_fail, file3 </p></td>
   <td><p>file3_fail, file3 </p></td>
   <td><p>file3_fail, file3 </p></td>
  </tr>
  <tr>
   <td><p>Mantieni</p></td>
   <td><p>vuoto</p></td>
   <td><p>vuoto</p></td>
   <td><p>file1 </p></td>
   <td><p>file1, file2 </p></td>
   <td><p>file1, file2 </p></td>
   <td><p>file1, file2, file4 </p></td>
   <td><p>file1, file2, file4 </p></td>
  </tr>
 </tbody>
</table>

Il testo seguente descrive ogni volta la manipolazione dei file:

**T1:** I quattro file di esempio vengono inseriti nella cartella di input.

**T2:** L&#39;operazione del servizio sposta il file1 nella cartella stage per la manipolazione.

**T3:** L&#39;operazione del servizio sposta il file2 nella cartella stage per la manipolazione. Posiziona i risultati di file1 nella cartella di output e sposta file1 nella cartella di conservazione.

**T4:** L&#39;operazione del servizio posiziona il file3 nella cartella stage per la manipolazione. Posiziona i risultati del file2 nella cartella di output e inserisce il file2 nella cartella di conservazione.

**T5:** L&#39;operazione del servizio colloca il file4 nella cartella stage per la manipolazione. La manipolazione del file3 non riesce e l&#39;operazione del servizio lo inserisce nella cartella degli errori.

**T6:** L&#39;operazione del servizio colloca il file5 nella cartella di input. Posiziona i risultati del file4 nella cartella di output, inserisce il file4 nella cartella di conservazione.

**T7:** L&#39;operazione del servizio colloca il file5 nella cartella stage per la manipolazione.

## Backup delle cartelle controllate {#backing-up-watched-folders}

Si consiglia di eseguire il backup dell&#39;intero file system di cartelle controllate su un altro file system.

## Ripristino delle cartelle controllate {#restoring-watched-folders}

Questa sezione descrive come ripristinare le cartelle controllate. Le cartelle visualizzate spesso richiamano processi di breve durata che vengono completati in un minuto. In questi casi, il ripristino della cartella controllata con un backup eseguito ogni ora non impedirà la perdita di dati.

Ad esempio, se un backup viene eseguito al momento T1 e il server non riesce a T7, allora file1, file2, file3 e file4 sono già manipolati. Il ripristino della cartella controllata con un backup eseguito a T1 non impedisce la perdita di dati.

Se è stato effettuato un backup più recente, è possibile ripristinare i file. Durante il ripristino dei file, considera in quale cartella della gerarchia cartelle controllata si trova il file corrente:

**Stage:** I file in questa cartella vengono elaborati nuovamente dopo il ripristino della cartella controllata.

**Ingresso:** I file in questa cartella vengono elaborati nuovamente dopo il ripristino della cartella controllata.

**Risultato:** I file in questa cartella non vengono elaborati.

**Uscita:** I file in questa cartella non vengono elaborati.

**Mantieni:** I file in questa cartella non vengono elaborati.

## Strategie per ridurre al minimo la perdita di dati {#strategies-to-minimize-data-loss}

Le seguenti strategie possono ridurre al minimo la perdita di dati della cartella di output e di input durante il ripristino di una cartella controllata:

* Esegui spesso il backup delle cartelle di output e di errore, ad esempio ogni ora, per evitare la perdita di file di risultato e di errore.
* Esegui il backup dei file di input in una cartella diversa da quella controllata. Questo garantisce la disponibilità dei file dopo il ripristino nel caso in cui non sia possibile trovare i file nella cartella di output o nella cartella di errore. Assicurati che lo schema di denominazione dei file sia coerente.

   Ad esempio, se salvi l’output con `%F.`*estensione*, il file di output avrà lo stesso nome del file di input. Questo consente di determinare quali file di input vengono manipolati e quali devono essere nuovamente inviati. Se nella cartella dei risultati vengono visualizzati solo file1_out e non file2_out, file3_out e file4_out, è necessario inviare nuovamente file2, file3 e file4.

* Se il backup della cartella controllata disponibile è più vecchio del tempo necessario per elaborare il processo, è necessario consentire al sistema di creare una nuova cartella controllata e inserire automaticamente i file nella cartella di input.
* Se l&#39;ultimo backup disponibile non è abbastanza recente, il tempo di backup è inferiore al tempo necessario per elaborare i file e la cartella controllata viene ripristinata, il file è stato manipolato in uno dei seguenti stadi diversi:

   * **Fase 1:** Nella cartella di input
   * **Fase 2:** Copiato nella cartella stage ma il processo non è ancora stato richiamato
   * **Fase 3:** Copiato nella cartella stage e il processo viene richiamato
   * **Fase 4:** Manipolazione in corso
   * **Fase 5:** Risultati restituiti

   Se i file si trovano nella fase 1, verranno manipolati. Se i file si trovano in fase 2 o 3, inseriscili nella cartella di input per eseguire nuovamente la manipolazione.

   >[!NOTE]
   >
   >Se la manipolazione di un file si verifica più di una volta, verrà evitata la perdita di dati, ma i risultati potrebbero essere duplicati.

## Conclusione {#conclusion}

A causa della natura dinamica e in continua evoluzione di una cartella controllata, il ripristino delle cartelle controllate dovrebbe essere fatto con i file che sono sottoposti a backup in un giorno. È consigliabile eseguire il backup dei risultati, memorizzare la cartella di input su un server e tenere traccia dei file di input in modo da poter inviare nuovamente il processo in caso di errore.
