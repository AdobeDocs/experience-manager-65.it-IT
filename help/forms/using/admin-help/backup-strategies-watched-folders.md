---
title: Strategie di backup per le cartelle esaminate
seo-title: Strategie di backup per le cartelle esaminate
description: Questo documento descrive come le cartelle esaminate siano influenzate da diversi scenari di backup e ripristino, dai limiti e dai risultati di questi scenari e come ridurre al minimo la perdita di dati.
seo-description: Questo documento descrive come le cartelle esaminate siano influenzate da diversi scenari di backup e ripristino, dai limiti e dai risultati di questi scenari e come ridurre al minimo la perdita di dati.
uuid: c61997b8-6c36-4bd9-90e5-411841a6c176
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6f775933-e989-4456-ad01-9bdf5dee3dad
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 2%

---


# Strategie di backup per le cartelle esaminate {#backup-strategies-for-watched-folders}

Questo contenuto descrive come le cartelle esaminate siano influenzate da diversi scenari di backup e ripristino, dai limiti e dai risultati di questi scenari e come ridurre al minimo la perdita di dati.

*Watched* Folderis è un&#39;applicazione basata su file system che richiama operazioni di servizio configurate che modificano il file all&#39;interno di una delle seguenti cartelle nella gerarchia delle cartelle esaminate:

* Input
* Area di visualizzazione
* Output
* Errore
* Mantieni

Un utente o un’applicazione client rilascia prima il file o la cartella nella cartella di input. L’operazione del servizio quindi sposta il file nella cartella dell’area di visualizzazione per l’elaborazione. Dopo che il servizio ha eseguito l&#39;operazione specificata, salva il file modificato nella cartella di output. I file sorgente elaborati correttamente vengono spostati nella cartella preserve e i file di elaborazione non riusciti vengono spostati nella cartella failure. Quando l&#39;attributo `Preserve On Failure` per la cartella esaminata è abilitato, i file sorgente elaborati non riusciti vengono spostati nella cartella preserve. (vedere [Configurazione degli endpoint delle cartelle esaminate](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#configuring-watched-folder-endpoints).)

È possibile eseguire il backup delle cartelle esaminate eseguendo il backup del file system.

>[!NOTE]
>
>Questo backup è indipendente dal processo di backup e ripristino del database o dell&#39;archivio documenti.

## Funzionamento delle cartelle esaminate {#how-watched-folders-work}

Questo contenuto descrive il processo di manipolazione dei file delle cartelle controllato. È importante comprendere questo processo prima di sviluppare un piano di ripresa. In questo esempio, l&#39;attributo `Preserve On Failure` per la cartella esaminata è abilitato. I file vengono elaborati nell&#39;ordine in cui arrivano.

La tabella seguente descrive la manipolazione dei file di cinque file di esempio (file1, file2, file3, file4, file5) durante l’intero processo. Nella tabella, l&#39;asse x rappresenta il tempo, ad esempio Tempo 1 o T1, e l&#39;asse y rappresenta le cartelle all&#39;interno della gerarchia delle cartelle guardata, come Input.

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
   <td><p>empty</p></td>
   <td><p>file5</p></td>
   <td><p>empty</p></td>
  </tr>
  <tr>
   <td><p>Area di visualizzazione</p></td>
   <td><p>empty</p></td>
   <td><p>file1</p></td>
   <td><p>file2</p></td>
   <td><p>file3</p></td>
   <td><p>file4</p></td>
   <td><p>empty</p></td>
   <td><p>file5</p></td>
  </tr>
  <tr>
   <td><p>Uscita</p></td>
   <td><p>empty</p></td>
   <td><p>empty</p></td>
   <td><p>file1_out</p></td>
   <td><p>file1_out, file2_out</p></td>
   <td><p>file1_out, file2_out</p></td>
   <td><p>file1_out, file2_out, file4_out</p></td>
   <td><p>file1_out, file2_out, file4_out</p></td>
  </tr>
  <tr>
   <td><p>Errore</p></td>
   <td><p>empty</p></td>
   <td><p>empty</p></td>
   <td><p>empty</p></td>
   <td><p>empty</p></td>
   <td><p>file3_fail, file3 </p></td>
   <td><p>file3_fail, file3 </p></td>
   <td><p>file3_fail, file3 </p></td>
  </tr>
  <tr>
   <td><p>Mantieni</p></td>
   <td><p>empty</p></td>
   <td><p>empty</p></td>
   <td><p>file1 </p></td>
   <td><p>file1, file2 </p></td>
   <td><p>file1, file2 </p></td>
   <td><p>file1, file2, file4 </p></td>
   <td><p>file1, file2, file4 </p></td>
  </tr>
 </tbody>
</table>

Il testo seguente descrive la manipolazione dei file per ogni volta:

**T1:** I quattro file di esempio vengono inseriti nella cartella di input.

**T2:** L&#39;operazione del servizio sposta file1 nella cartella dell&#39;area di visualizzazione per la manipolazione.

**T3:** L&#39;operazione del servizio sposta file2 nella cartella dell&#39;area di visualizzazione per la manipolazione. Posiziona i risultati di file1 nella cartella di output e sposta file1 nella cartella preserve.

**T4:** L&#39;operazione del servizio colloca file3 nella cartella dell&#39;area di visualizzazione per la manipolazione. Posiziona i risultati di file2 nella cartella di output e inserisce file2 nella cartella preserve.

**T5:** L’operazione del servizio colloca il file4 nella cartella dell’area di visualizzazione per la manipolazione. La manipolazione di file3 non riesce e l&#39;operazione del servizio lo inserisce nella cartella degli errori.

**T6:** L&#39;operazione del servizio colloca file5 nella cartella di input. Posiziona i risultati di file4 nella cartella di output, inserisce file4 nella cartella preserve.

**T7:** L’operazione del servizio colloca il file5 nella cartella dell’area di visualizzazione per la manipolazione.

## Backup delle cartelle esaminate {#backing-up-watched-folders}

Si consiglia di eseguire il backup dell&#39;intero file system delle cartelle controllato su un altro file system.

## Ripristino delle cartelle esaminate {#restoring-watched-folders}

Questa sezione descrive come ripristinare le cartelle esaminate. Le cartelle esaminate spesso richiamano processi di breve durata che vengono completati in un minuto. In tali casi, il ripristino della cartella esaminata con un backup eseguito ogni ora non impedisce la perdita di dati.

Ad esempio, se un backup viene eseguito al momento T1 e il server non riesce a T7, file1, file2, file3 e file4 sono già manipolati. Il ripristino della cartella esaminata con un backup eseguito a T1 non impedisce la perdita di dati.

Se è stato eseguito un backup più recente, è possibile ripristinare i file. Durante il ripristino dei file, individuare la cartella gerarchica delle cartelle esaminate in cui si trova il file corrente:

**Fase: i** file in questa cartella vengono elaborati di nuovo dopo il ripristino della cartella esaminata.

**Input:** I file in questa cartella vengono elaborati di nuovo dopo il ripristino della cartella controllata.

**Risultato:** i file in questa cartella non vengono elaborati.

**Output:** i file in questa cartella non vengono elaborati.

**Mantieni:** i file in questa cartella non vengono elaborati.

## Strategie per ridurre al minimo la perdita di dati {#strategies-to-minimize-data-loss}

Le seguenti strategie possono ridurre al minimo la perdita di dati delle cartelle di output e di input durante il ripristino di una cartella esaminata:

* Eseguire di frequente il backup delle cartelle di output e di errore, ad esempio ogni ora, per evitare la perdita di risultati e di file con errore.
* Esegui il backup dei file di input in una cartella diversa da quella esaminata. Questo garantisce la disponibilità dei file dopo il ripristino nel caso in cui non si possano trovare i file nella cartella di output o nella cartella degli errori. Accertatevi che lo schema di denominazione dei file sia coerente.

   Ad esempio, se si salva l&#39;output con `%F.`*extension*, il file di output avrà lo stesso nome del file di input. Questo consente di determinare quali file di input vengono manipolati e quali devono essere reinviati. Se nella cartella dei risultati viene visualizzato solo file1_out e non file2_out, file3_out e file4_out, è necessario reinviare file2, file3 e file4.

* Se il backup delle cartelle controllato disponibile è precedente al tempo necessario per l’elaborazione del processo, è necessario consentire al sistema di creare una nuova cartella esaminata e di inserire automaticamente i file nella cartella di input.
* Se l&#39;ultimo backup disponibile non è abbastanza recente, il tempo di backup è inferiore al tempo necessario per l&#39;elaborazione dei file e la cartella controllata viene ripristinata, il file è stato manipolato in uno dei seguenti passaggi:

   * **Fase 1:** nella cartella di input
   * **Fase 2:** Copiato nella cartella dell&#39;area di visualizzazione ma il processo non viene ancora richiamato
   * **Fase 3:** Copiato nella cartella stage e richiamato il processo
   * **Fase 4:** Manipolazione in corso
   * **Fase 5:** Risultati restituiti

   Se i file si trovano nella fase 1, verranno modificati. Se i file si trovano nella fase 2 o 3, inseriteli nuovamente nella cartella di input per la manipolazione.

   >[!NOTE]
   >
   >Se la manipolazione di un file si verifica più volte, la perdita di dati sarà evitata ma i risultati potrebbero essere duplicati.

## Conclusione {#conclusion}

A causa della natura dinamica e in continua evoluzione di una cartella esaminata, il ripristino delle cartelle esaminate dovrebbe essere effettuato con i file sottoposti a backup entro un giorno. È consigliabile eseguire il backup dei risultati, memorizzare la cartella di input su un server e tenere traccia dei file di input in modo da poter reinviare il processo in caso di errore.
