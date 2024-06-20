---
title: Rapporti predefiniti nella generazione di rapporti sui processi
description: Eseguire una query per AEM Forms sui dati del processo JEE per creare rapporti su processi con tempi di esecuzione lunghi, durata del processo e volume del flusso di lavoro
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
exl-id: 34e55676-6332-4616-aecc-bcc8cc1e8a29
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 0%

---

# Rapporti predefiniti nella generazione di rapporti sui processi {#pre-defined-reports-in-process-reporting}

## Rapporti predefiniti nella generazione di rapporti {#pre-defined-reports-in-process-reporting-1}

AEM Forms Process Reporting viene fornito con *pronto all’uso* rapporti:

* **[Processi a esecuzione prolungata](#long-running-processes)**: report di tutti i processi di AEM Forms il cui completamento ha richiesto più di un tempo specificato
* **[Grafico durata processo](#process-duration-report)**: rapporto di un processo AEM Forms specificato per durata
* **[Volume flusso di lavoro](#workflow-volume-report)**: report delle istanze in esecuzione e completate del processo specificato per data

## Processi a esecuzione prolungata {#long-running-processes}

Nel rapporto Processi a esecuzione prolungata vengono visualizzati i processi di AEM Forms il cui completamento ha richiesto più di un tempo specificato.

### Per eseguire un report di processi a esecuzione prolungata {#to-execute-a-long-running-process-report}

1. Per visualizzare l&#39;elenco dei report predefiniti in Report processo, nella **Reporting sui processi** struttura, fare clic sul pulsante **Rapporti** nodo.
1. Fai clic su **Processi a esecuzione prolungata** nodo di report.

   ![long_running_node](assets/long_running_node.png)

   Quando selezioni un rapporto, il **Parametri del rapporto** viene visualizzato a destra della visualizzazione struttura.

   ![pannello parametri report processi a esecuzione prolungata](assets/report_parameters_panel.png)

   Parametri:

   * **Durata** (*obbligatorio*): specifica una durata e un’unità di tempo. Visualizza tutti i processi AEM Forms eseguiti per una durata superiore a quella specificata.
   * **Iniziato dopo** (*facoltativo*): seleziona una data. Filtrare il report per visualizzare le istanze di processo avviate dopo la data specificata.
   * **Iniziato prima di** (*facoltativo*): seleziona una data. Filtrare il report per visualizzare le istanze di processo avviate prima della data specificata.

1. Clic **Vai** per eseguire il report.

   Il rapporto viene visualizzato nel **Report** pannello a destra del **Reporting sui processi** finestra.

   ![long_running_PROCESSES](assets/long_running_processes.png)

   Utilizza le opzioni nell’angolo superiore destro della sezione **Report** per eseguire le seguenti operazioni sul rapporto.

   * **Aggiorna**: aggiorna il rapporto con i dati più recenti presenti nell’archiviazione
   * **Cambia colore legenda**: seleziona e modifica il colore della legenda del rapporto
   * **Esporta in CSV**: esporta e scarica i dati dal rapporto in un file separato da virgole

## Rapporto Durata processo  {#process-duration-report}

Nel rapporto Durata processo viene visualizzato il numero di istanze di un processo Forms per numero di giorni di esecuzione di ogni istanza.

### Per eseguire un report Durata processo {#to-execute-a-process-duration-report}

1. Per visualizzare i rapporti predefiniti in Report processo, nella **Reporting sui processi** struttura, fare clic sul pulsante **Rapporti** nodo.
1. Fai clic su **Durata processi** nodo di report.

   ![process_duration_node](assets/process_duration_node.png)

   Quando selezioni un rapporto, il **Parametri del rapporto** viene visualizzato a destra della visualizzazione struttura.

   ![pannello parametri report processi a esecuzione prolungata](assets/process_duration_params.png)

   Parametri:

   * **Seleziona processo** (*obbligatorio*): seleziona un processo AEM Forms.

1. Clic **Vai** per eseguire il report.

   Il rapporto viene visualizzato nel **Report** pannello a destra della finestra Report processo.

   ![process_duration_report](assets/process_duration_report.png)

   Utilizza le opzioni nell’angolo superiore destro della sezione **Report** per eseguire le seguenti operazioni sul rapporto.

   * **Aggiorna**: aggiorna il rapporto con i dati più recenti presenti nell’archiviazione
   * **Cambia colore legenda**: seleziona e modifica il colore della legenda del rapporto
   * **Esporta in CSV**: esporta e scarica i dati dal rapporto in un file separato da virgole

## Rapporto volume flusso di lavoro {#workflow-volume-report}

Nel rapporto Volume flusso di lavoro viene visualizzato il numero di istanze di un processo AEM Forms attualmente in esecuzione e completate per giorno di calendario.

### Per eseguire un report Volume flusso di lavoro {#to-execute-a-workflow-volume-report}

1. Per visualizzare i rapporti predefiniti in Report processo, nella **Reporting sui processi** struttura, fare clic sul pulsante **Rapporti** nodo.
1. Fai clic su **Volume flusso di lavoro** nodo di report.

   ![workflow_volume_node](assets/workflow_volume_node.png)

   Quando selezioni un rapporto, il **Parametri del rapporto** viene visualizzato a destra della visualizzazione struttura.

   ![pannello parametri report processi a esecuzione prolungata](assets/workflow_volume_params.png)

   Parametri:

   * **Seleziona processo** (*obbligatorio*): seleziona un processo AEM Forms.

   * **Iniziato dopo** (*facoltativo*): seleziona una data. Filtra il report per visualizzare le istanze di processo avviate dopo la data specificata.

   * **Iniziato prima di** (*facoltativo*): seleziona una data. Filtra il report per visualizzare le istanze di processo avviate prima della data specificata.

1. Clic **Vai** per eseguire il report.

   Il rapporto viene visualizzato nel **Report** pannello a destra del **Reporting sui processi** finestra.

   ![workflow_volume_report](assets/workflow_volume_report.png)

   Utilizza le opzioni nell’angolo superiore destro della sezione **Report** per eseguire le seguenti operazioni sul rapporto.

   * **Aggiorna**: aggiorna il rapporto con i dati più recenti presenti nell’archiviazione
   * **Cambia colore legenda**: seleziona e modifica il colore della legenda del rapporto
   * **Esporta in CSV**: esporta e scarica i dati dal rapporto in un file separato da virgole
