---
title: Strategie di backup per le cartelle controllate
description: In questo documento viene descritto il modo in cui le cartelle controllate vengono influenzate da diversi scenari di backup e ripristino, le limitazioni e i risultati di tali scenari e come ridurre al minimo la perdita di dati.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0d36160a-29fa-4cc4-a0ff-fc681d3e040e
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '1080'
ht-degree: 100%

---

# Strategie di backup per le cartelle controllate {#backup-strategies-for-watched-folders}

In questo contenuto viene descritto il modo in cui le cartelle controllate vengono influenzate da diversi scenari di backup e ripristino, le limitazioni e i risultati di tali scenari e come ridurre al minimo la perdita di dati.

*Watched Folder* è un’applicazione basata su file system che richiama operazioni di servizio configurate che manipolano il file all’interno di una delle seguenti cartelle nella gerarchia di cartelle monitorata:

* Input
* Fase
* Output
* Errore
* Conservazione

Un utente o un’applicazione client rilascia prima il file o la cartella nella cartella di input. L’operazione di servizio quindi sposta il file nella cartella fase per l’elaborazione. Dopo aver eseguito l’operazione specificata, il servizio salva il file modificato nella cartella di output. I file di origine elaborati correttamente vengono spostati nella cartella di conservazione e i file di elaborazione non elaborati vengono spostati nella cartella errore. Quando l’attributo `Preserve On Failure` per la cartella monitorata è abilitato, i file di origine elaborati che presentano errori vengono spostati nella cartella di conservazione. (Consulta [Configurazione degli endpoint della cartella monitorata](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#configuring-watched-folder-endpoints).)

È possibile eseguire il backup delle cartelle controllate eseguendo il backup del file system.

>[!NOTE]
>
>Questo backup è indipendente dal processo di backup e ripristino del database o dell’archiviazione dei documenti.

## Funzionamento delle cartelle controllate {#how-watched-folders-work}

Questo contenuto descrive il processo di manipolazione dei file delle cartelle controllate. È importante comprendere questo processo prima di elaborare un piano di ripristino. In questo esempio, l’attributo `Preserve On Failure` per la cartella monitorata è abilitato. I file vengono elaborati nell’ordine di arrivo.

Nella tabella seguente viene descritta la manipolazione di cinque file di esempio (file1, file2, file3, file4, file5) durante l’intero processo. Nella tabella, l’asse x rappresenta la fase temporale del processo, ad esempio Fase temporale 1 o T1, e l’asse y rappresenta le cartelle all’interno della gerarchia delle cartelle controllate, ad esempio Input.

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
   <td><p>Input</p></td>
   <td><p>file1, file2, file3, file4</p></td>
   <td><p>file2, file3, file4</p></td>
   <td><p>file3, file4</p></td>
   <td><p>file4</p></td>
   <td><p>vuoto</p></td>
   <td><p>file5</p></td>
   <td><p>vuoto</p></td>
  </tr>
  <tr>
   <td><p>Fase</p></td>
   <td><p>vuoto</p></td>
   <td><p>file1</p></td>
   <td><p>file2</p></td>
   <td><p>file3</p></td>
   <td><p>file4</p></td>
   <td><p>vuoto</p></td>
   <td><p>file5</p></td>
  </tr>
  <tr>
   <td><p>Output</p></td>
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
   <td><p>Conservazione</p></td>
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

Il testo seguente descrive la manipolazione dei file per ogni occorrenza:

**T1:** i quattro file di esempio si trovano nella cartella di input.

**T2:** l’operazione di servizio sposta file1 nella cartella di fase per la modifica.

**T3:** l’operazione di servizio sposta file2 nella cartella di staging per la manipolazione. Inserisce i risultati di file1 nella cartella di output e sposta file1 nella cartella di salvataggio.

**T4:** l’operazione di servizio inserisce file3 nella cartella di staging per la manipolazione. Inserisce i risultati di file2 nella cartella di output e sposta file2 nella cartella di salvataggio.

**T5:** l’operazione di servizio inserisce file4 nella cartella di fase per la manipolazione. La manipolazione di file3 ha esito negativo e l’operazione di servizio lo inserisce nella cartella degli errori.

**T6:** l’operazione di servizio inserisce file5 nella cartella di input. Inserisce i risultati di file4 nella cartella di output e inserisce file4 nella cartella di conservazione.

**T7:** l’operazione di servizio inserisce file5 nella cartella di fase per la manipolazione.

## Backup delle cartelle controllate {#backing-up-watched-folders}

Si consiglia di eseguire il backup dell’intero file system della cartella controllata in un altro file system.

## Ripristino delle cartelle controllate {#restoring-watched-folders}

Questa sezione descrive come ripristinare le cartelle controllate. Le cartelle controllate spesso richiamano processi di breve durata che vengono completati in un minuto. In questi casi, il ripristino della cartella controllata con un backup eseguito ogni ora non impedisce la perdita di dati.

Ad esempio, se un backup viene eseguito al momento T1 e il server riscontra un errore in T7, file1, file2, file3 e file4 sono già manipolati. Il ripristino della cartella controllata con un backup eseguito in T1 non impedisce la perdita di dati.

Se è stato eseguito un backup più recente, è possibile ripristinare i file. Quando vengono ripristinati i file, considerare la cartella della gerarchia di cartelle controllate in cui si trova il file corrente:

**Fase:** i file in questa cartella vengono elaborati nuovamente dopo il ripristino della cartella controllata.

**Input:** i file in questa cartella vengono elaborati nuovamente dopo il ripristino della cartella controllata.

**Risultato:** i file di questa cartella non vengono elaborati.

**Output:** i file in questa cartella non vengono elaborati.

**Conservazione:** i file in questa cartella non vengono elaborati.

## Strategie per ridurre al minimo la perdita di dati {#strategies-to-minimize-data-loss}

Le seguenti strategie possono ridurre al minimo la perdita di dati di cartelle di output e di input durante il ripristino di una cartella controllata:

* Esegui frequentemente il backup delle cartelle di output e di errore, ad esempio ogni ora, per evitare la perdita di file di risultato e di errore.
* Esegui il backup dei file di input in una cartella diversa da quella controllata. Ciò garantisce la disponibilità dei file dopo il ripristino nel caso in cui non sia possibile trovare i file nella cartella di output o nella cartella di errore. Assicurati che lo schema di denominazione dei file sia coerente.

  Se, ad esempio, salvi l’output con `%F.`*estensione*, il file di output avrà lo stesso nome del file di input. Questo consente di determinare quali file di input vengono manipolati e quali devono essere inviati nuovamente. Se nella cartella dei risultati è presente solo file1_out e non file2_out, file3_out e file4_out, è necessario inviare nuovamente file2, file3 e file4.

* Se il backup della cartella controllata disponibile è precedente al tempo necessario per elaborare il processo, è necessario consentire al sistema di creare una cartella controllata e inserire automaticamente i file nella cartella di input.
* Se l’ultimo backup disponibile non è abbastanza recente, il tempo di backup è inferiore al tempo necessario per elaborare i file e la cartella controllata viene ripristinata, il file è stato manipolato in una delle seguenti fasi diverse:

   * **Fase 1:** nella cartella di input
   * **Fase 2:** copiato nella cartella di fase, ma il processo non è ancora stato richiamato
   * **Fase 3:** copiato nella cartella di fase e il processo è stato richiamato
   * **Fase 4:** manipolazione in corso
   * **Fase 5:** risultati restituiti

  Se i file sono nella Fase 1, verranno manipolati. Se i file sono nella Fase 2 o 3, inseriscili nella cartella di input in modo che la manipolazione possa aver luogo nuovamente.

  >[!NOTE]
  >
  >Se la manipolazione di un file si verifica più di una volta, la perdita di dati sarà evitata, ma i risultati potrebbero essere duplicati.

## Conclusione {#conclusion}

A causa della natura dinamica e in continua evoluzione di una cartella controllata, il ripristino delle cartelle controllate deve essere eseguito con i file di cui viene eseguito il backup in un giorno. È consigliabile eseguire il backup dei risultati, archiviare la cartella di input su un server e tenere traccia dei file di input in modo da poter inviare nuovamente il processo in caso di errore.
