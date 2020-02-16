---
title: Report predefiniti in Process Reporting
seo-title: Report predefiniti in Process Reporting
description: Query per AEM Forms su dati del processo JEE per creare rapporti su processi in esecuzione a lungo termine, durata del processo e volume del flusso di lavoro
seo-description: Query per AEM Forms su dati del processo JEE per creare rapporti su processi in esecuzione a lungo termine, durata del processo e volume del flusso di lavoro
uuid: 704a8886-90ea-4793-a3fc-f998f878c928
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3d93375e-ec37-4445-96ea-d315676787b4
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# Report predefiniti in Process Reporting {#pre-defined-reports-in-process-reporting}

## Report predefiniti in Process Reporting {#pre-defined-reports-in-process-reporting-1}

AEM Forms Process Reporting viene fornito con i seguenti rapporti *out-of-the-box* :

* **[Processi](#long-running-processes)**Di Lunga Durata: Report di tutti i processi AEM Forms che richiedono più di un tempo specificato per il completamento
* **[Grafico](#process-duration-report)**durata processo: Report relativo a un determinato processo di AEM Forms per durata
* **[Volume](#workflow-volume-report)**flusso di lavoro: Report delle istanze in esecuzione e completate del processo specificato per data

## Processi a lunga esecuzione {#long-running-processes}

Il rapporto Processi con esecuzione prolungata visualizza i processi AEM Forms che hanno richiesto più di un tempo specificato per il completamento.

### Per eseguire un rapporto Processo di esecuzione prolungata {#to-execute-a-long-running-process-report}

1. Per visualizzare l&#39;elenco dei report predefiniti in Process Reporting (Generazione rapporti sui processi), nella visualizzazione struttura **Process Reporting** fare clic sul nodo **Reports **(Report*).
1. Fare clic sul nodo del rapporto Processi **** lunghi in esecuzione.

   ![long_run_node](assets/long_running_node.png)

   Quando selezionate un rapporto, il pannello Parametri **** rapporto viene visualizzato a destra della struttura ad albero.

   ![pannello parametri del rapporto processi lunghi](assets/report_parameters_panel.png)

   Parametri:

   * **Durata**(*obbligatorio*): Specificate una durata e un’unità di tempo. Visualizza tutti i processi AEM Forms eseguiti per più di una durata specificata.
   * **Avviato dopo** (*facoltativo*): Selezionare una data. Filtrare il rapporto per visualizzare le istanze del processo iniziate dopo la data specificata.
   * **Avviato prima** (*facoltativo*): Selezionare una data. Filtrare il rapporto per visualizzare le istanze del processo iniziate prima della data specificata.

1. Fate clic su **Vai** per eseguire il rapporto.

   Il rapporto viene visualizzato nel pannello **Report **a destra della finestra **Process Reporting (Generazione rapporti** processo).

   ![long_run_process](assets/long_running_processes.png)

   Utilizzate le opzioni nell&#39;angolo superiore destro del pannello **Report **per eseguire le seguenti operazioni sul report.

   * **Aggiorna**: Aggiorna il report con i dati più recenti presenti nello storage
   * **Cambia colore** legenda: Seleziona e modifica il colore della legenda del rapporto
   * **Esporta in CSV**: Esportare e scaricare i dati dal rapporto in un file separato da virgole

## Report Durata processo {#process-duration-report}

Il rapporto Durata processo visualizza il numero di istanze di un processo Forms per il numero di giorni di esecuzione di ciascuna istanza.

### Per eseguire un rapporto Durata processo {#to-execute-a-process-duration-report}

1. Per visualizzare i report predefiniti in Process Reporting (Generazione rapporti processo), nella visualizzazione struttura **Process Reporting** fare clic sul nodo **Reports **(Rapporti*).
1. Fare clic sul nodo del rapporto Durata **** processi.

   ![process_durata_node](assets/process_duration_node.png)

   Quando selezionate un rapporto, il pannello Parametri **** rapporto viene visualizzato a destra della struttura ad albero.

   ![pannello parametri del rapporto processi lunghi](assets/process_duration_params.png)

   Parametri:

   * **Seleziona processo **(*obbligatorio*): Selezionare un processo AEM Forms.

1. Fare clic su **Go **per eseguire il report.

   Il rapporto viene visualizzato nel pannello **Report **a destra della finestra Report processo.

   ![process_durata_report](assets/process_duration_report.png)

   Utilizzate le opzioni nell&#39;angolo superiore destro del pannello **Report **per eseguire le seguenti operazioni sul report.

   * **Aggiorna**: Aggiorna il report con i dati più recenti presenti nello storage
   * **Cambia colore** legenda: Seleziona e modifica il colore della legenda del rapporto
   * **Esporta in CSV**: Esportare e scaricare i dati dal rapporto in un file separato da virgole

## Report Volume flusso di lavoro {#workflow-volume-report}

Il rapporto Volume flusso di lavoro visualizza il numero di istanze attualmente in esecuzione e completate di un processo AEM Forms per giorno di calendario.

### Per eseguire un rapporto sul volume del flusso di lavoro {#to-execute-a-workflow-volume-report}

1. Per visualizzare i report predefiniti in Process Reporting (Generazione rapporti processo), nella vista ad albero **Process Reporting **fare clic sul nodo **Reports **(Rapporti **).
1. Fate clic sul nodo del rapporto Volume **** flusso di lavoro.

   ![workflow_volume_node](assets/workflow_volume_node.png)

   Quando selezionate un rapporto, il pannello Parametri **** rapporto viene visualizzato a destra della struttura ad albero.

   ![pannello parametri del rapporto processi lunghi](assets/workflow_volume_params.png)

   Parametri:

   * **Seleziona processo **(*obbligatorio*): Selezionare un processo AEM Forms.

   * **Avviato dopo** (*facoltativo*): Selezionare una data. Filtra il rapporto per visualizzare le istanze del processo iniziate dopo la data specificata.

   * **Avviato prima** (*facoltativo*): Selezionare una data. Filtra il rapporto per visualizzare le istanze del processo avviate prima della data specificata.

1. Fare clic su **Go **per eseguire il report.

   Il rapporto viene visualizzato nel pannello **Report **a destra della finestra **Process Reporting (Generazione rapporti** processo).

   ![workflow_volume_report](assets/workflow_volume_report.png)

   Utilizzate le opzioni nell&#39;angolo superiore destro del pannello **Report **per eseguire le seguenti operazioni sul report.

   * **Aggiorna**: Aggiorna il report con i dati più recenti presenti nello storage
   * **Cambia colore** legenda: Seleziona e modifica il colore della legenda del rapporto
   * **Esporta in CSV**: Esportare e scaricare i dati dal rapporto in un file separato da virgole

[Contattare il supporto](https://www.adobe.com/account/sign-in.supportportal.html)
