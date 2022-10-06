---
title: Rapporti predefiniti in Process Reporting
seo-title: Pre-defined reports in Process Reporting
description: Query per AEM Forms sui dati del processo JEE per creare rapporti su processi a lungo termine, durata del processo e volume del flusso di lavoro
seo-description: Query for AEM Forms on JEE process data to create reports on long running processes, Process duration, and Workflow volume
uuid: 704a8886-90ea-4793-a3fc-f998f878c928
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3d93375e-ec37-4445-96ea-d315676787b4
docset: aem65
exl-id: 34e55676-6332-4616-aecc-bcc8cc1e8a29
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 0%

---

# Rapporti predefiniti in Process Reporting {#pre-defined-reports-in-process-reporting}

## Rapporti predefiniti nel reporting dei processi {#pre-defined-reports-in-process-reporting-1}

AEM Forms Process Reporting viene fornito con i seguenti *pronto all&#39;uso* rapporti:

* **[Processi a lunga esecuzione](#long-running-processes)**: Report di tutti i processi AEM Forms che richiedono più di un tempo specificato per il completamento
* **[Grafico a barre della durata del processo](#process-duration-report)**: Rapporto di un determinato processo AEM Forms per durata
* **[Volume del flusso di lavoro](#workflow-volume-report)**: Rapporto delle istanze in esecuzione e completate del processo specificato per data

## Processi a lunga esecuzione {#long-running-processes}

Il rapporto Processi a esecuzione lunga visualizza i processi AEM Forms che hanno richiesto più di un tempo specificato per il completamento.

### Per eseguire un rapporto sul processo a lungo termine {#to-execute-a-long-running-process-report}

1. Per visualizzare l&#39;elenco dei report predefiniti in Reporting dei processi, nella sezione **Reporting dei processi** visualizzazione struttura, fare clic sul pulsante **Rapporti** nodo.
1. Fai clic sul pulsante **Processi a lunga esecuzione** nodo del report.

   ![long_run_node](assets/long_running_node.png)

   Quando selezioni un rapporto, la **Parametri del rapporto** viene visualizzato a destra della vista ad albero.

   ![pannello dei parametri del rapporto dei processi a lungo termine](assets/report_parameters_panel.png)

   Parametri:

   * **Durata** (*obbligatorio*): Specifica una durata e un’unità di tempo. Visualizza tutti i processi AEM Forms eseguiti per più della durata specificata.
   * **Avviato dopo** (*facoltativo*): Seleziona una data. Filtra il rapporto per visualizzare le istanze del processo iniziate dopo la data specificata.
   * **Avviato prima** (*facoltativo*): Seleziona una data. Filtrare il rapporto per visualizzare le istanze del processo avviate prima della data specificata.

1. Fai clic su **Vai** per eseguire il report.

   Il rapporto viene visualizzato nel **Rapporto** pannello a destra **Reporting dei processi** finestra.

   ![long_run_process](assets/long_running_processes.png)

   Utilizza le opzioni nell’angolo superiore destro del **Rapporto** per eseguire le seguenti operazioni sul report.

   * **Aggiorna**: Aggiorna il report con i dati più recenti presenti nell&#39;archivio
   * **Cambia colore della legenda**: Selezionare e modificare il colore della legenda del rapporto
   * **Esportazione in formato CSV**: Esporta e scarica i dati dal rapporto in un file separato da virgole

## Rapporto sulla durata del processo  {#process-duration-report}

Il rapporto Durata processo visualizza il numero di istanze di un processo Forms per numero di giorni in cui ogni istanza è stata eseguita.

### Per eseguire un rapporto sulla durata del processo {#to-execute-a-process-duration-report}

1. Per visualizzare i report predefiniti in Reporting dei processi, nella sezione **Reporting dei processi** visualizzazione struttura, fare clic sul pulsante **Rapporti** nodo.
1. Fai clic sul pulsante **Durata dei processi** nodo del report.

   ![process_duration_node](assets/process_duration_node.png)

   Quando selezioni un rapporto, la **Parametri del rapporto** viene visualizzato a destra della vista ad albero.

   ![pannello dei parametri del rapporto dei processi a lungo termine](assets/process_duration_params.png)

   Parametri:

   * **Seleziona processo** (*obbligatorio*): Seleziona un processo AEM Forms.

1. Fai clic su **Vai** per eseguire il report.

   Il rapporto viene visualizzato nel **Rapporto** pannello a destra della finestra Reporting processi.

   ![process_duration_report](assets/process_duration_report.png)

   Utilizza le opzioni nell’angolo superiore destro del **Rapporto** per eseguire le seguenti operazioni sul report.

   * **Aggiorna**: Aggiorna il report con i dati più recenti presenti nell&#39;archivio
   * **Cambia colore della legenda**: Selezionare e modificare il colore della legenda del rapporto
   * **Esportazione in formato CSV**: Esporta e scarica i dati dal rapporto in un file separato da virgole

## Rapporto volume flusso di lavoro {#workflow-volume-report}

Il rapporto Volume flusso di lavoro visualizza il numero di istanze attualmente in esecuzione e completate di un processo AEM Forms per giorno di calendario.

### Per eseguire un rapporto sul volume di un flusso di lavoro {#to-execute-a-workflow-volume-report}

1. Per visualizzare i report predefiniti in Reporting dei processi, nella sezione **Reporting dei processi** visualizzazione struttura, fare clic sul pulsante **Rapporti** nodo.
1. Fai clic sul pulsante **Volume del flusso di lavoro** nodo del report.

   ![workflow_volume_node](assets/workflow_volume_node.png)

   Quando selezioni un rapporto, la **Parametri del rapporto** viene visualizzato a destra della vista ad albero.

   ![pannello dei parametri del rapporto dei processi a lungo termine](assets/workflow_volume_params.png)

   Parametri:

   * **Seleziona processo** (*obbligatorio*): Seleziona un processo AEM Forms.

   * **Avviato dopo** (*facoltativo*): Seleziona una data. Filtra il rapporto per visualizzare le istanze del processo iniziate dopo la data specificata.

   * **Avviato prima** (*facoltativo*): Seleziona una data. Filtra il rapporto per visualizzare le istanze del processo iniziate prima della data specificata.

1. Fai clic su **Vai** per eseguire il report.

   Il rapporto viene visualizzato nel **Rapporto** pannello a destra **Reporting dei processi** finestra.

   ![workflow_volume_report](assets/workflow_volume_report.png)

   Utilizza le opzioni nell’angolo superiore destro del **Rapporto** per eseguire le seguenti operazioni sul report.

   * **Aggiorna**: Aggiorna il report con i dati più recenti presenti nell&#39;archivio
   * **Cambia colore della legenda**: Selezionare e modificare il colore della legenda del rapporto
   * **Esportazione in formato CSV**: Esporta e scarica i dati dal rapporto in un file separato da virgole
