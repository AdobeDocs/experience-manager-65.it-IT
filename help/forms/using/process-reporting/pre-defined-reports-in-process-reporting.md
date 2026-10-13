---
title: Rapporti predefiniti in Rapporti sui processi
description: Eseguire una query per AEM Forms sui dati del processo JEE per creare rapporti su processi con tempi di esecuzione lunghi, durata del processo e volume del flusso di lavoro
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
exl-id: 34e55676-6332-4616-aecc-bcc8cc1e8a29
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 1%
---
# Rapporti predefiniti in Rapporti sui processi {#pre-defined-reports-in-process-reporting}

## Rapporti predefiniti nella generazione di rapporti {#pre-defined-reports-in-process-reporting-1}

AEM Forms Process Reporting viene fornito con i seguenti *report predefiniti*:

* **[Processi a esecuzione prolungata](#long-running-processes)**: un report di tutti i processi AEM Forms il cui completamento ha richiesto più di un tempo specificato
* **[Grafico durata processo](#process-duration-report)**: un report di un processo AEM Forms specificato per durata
* **[Volume flusso di lavoro](#workflow-volume-report)**: un report delle istanze in esecuzione e completate del processo specificato per data

## Processi a esecuzione prolungata {#long-running-processes}

Nel rapporto Processi a esecuzione prolungata vengono visualizzati i processi di AEM Forms il cui completamento ha richiesto più di un tempo specificato.

### Per eseguire un report di processi a esecuzione prolungata {#to-execute-a-long-running-process-report}

1. Per visualizzare l&#39;elenco dei report predefiniti in Process Reporting, nella visualizzazione struttura **Process Reporting** fare clic sul nodo **Reports**.
1. Fare clic sul nodo del report **Processi a esecuzione prolungata**.

   ![nodo_in_esecuzione](assets/long_running_node.png)

   Quando selezioni un report, il pannello **Parametri del report** viene visualizzato a destra della visualizzazione struttura.

   ![pannello parametri report processi a esecuzione prolungata](assets/report_parameters_panel.png)

   Parametri:

   * **Durata** (*obbligatoria*): specifica una durata e un&#39;unità di tempo. Visualizza tutti i processi AEM Forms eseguiti per una durata superiore a quella specificata.
   * **Iniziato dopo** (*facoltativo*): seleziona una data. Filtrare il report per visualizzare le istanze di processo avviate dopo la data specificata.
   * **Iniziato prima del** (*facoltativo*): seleziona una data. Filtrare il report per visualizzare le istanze di processo avviate prima della data specificata.

1. Fare clic su **Vai** per eseguire il report.

   Il report viene visualizzato nel pannello **Report** a destra della finestra **Report dei processi**.

   ![processi_in_esecuzione](assets/long_running_processes.png)

   Utilizzare le opzioni nell&#39;angolo superiore destro del pannello **Report** per eseguire le operazioni seguenti nel report.

   * **Aggiorna**: aggiorna il report con i dati più recenti presenti nell&#39;archivio
   * **Cambia colore legenda**: selezionare e modificare il colore della legenda del report
   * **Esporta in CSV**: esporta e scarica i dati dal report in un file separato da virgole

## Rapporto Durata processo  {#process-duration-report}

Nel rapporto Durata processo viene visualizzato il numero di istanze di un processo Forms per numero di giorni di esecuzione di ogni istanza.

### Per eseguire un report Durata processo {#to-execute-a-process-duration-report}

1. Per visualizzare i report predefiniti in Process Reporting, nella visualizzazione struttura **Process Reporting** fare clic sul nodo **Reports**.
1. Fare clic sul nodo del report **Durata processi**.

   ![process_duration_node](assets/process_duration_node.png)

   Quando selezioni un report, il pannello **Parametri del report** viene visualizzato a destra della visualizzazione struttura.

   ![pannello parametri report processi a esecuzione prolungata](assets/process_duration_params.png)

   Parametri:

   * **Seleziona processo** (*obbligatorio*): seleziona un processo AEM Forms.

1. Fare clic su **Vai** per eseguire il report.

   Il report viene visualizzato nel pannello **Report** a destra della finestra Report processi.

   ![report_durata_processo](assets/process_duration_report.png)

   Utilizzare le opzioni nell&#39;angolo superiore destro del pannello **Report** per eseguire le operazioni seguenti nel report.

   * **Aggiorna**: aggiorna il report con i dati più recenti presenti nell&#39;archivio
   * **Cambia colore legenda**: selezionare e modificare il colore della legenda del report
   * **Esporta in CSV**: esporta e scarica i dati dal report in un file separato da virgole

## Rapporto volume flusso di lavoro {#workflow-volume-report}

Nel rapporto Volume flusso di lavoro viene visualizzato il numero di istanze di un processo AEM Forms attualmente in esecuzione e completate per giorno di calendario.

### Per eseguire un report Volume flusso di lavoro {#to-execute-a-workflow-volume-report}

1. Per visualizzare i report predefiniti in Process Reporting, nella visualizzazione struttura **Process Reporting** fare clic sul nodo **Reports**.
1. Fare clic sul nodo del report **Volume flusso di lavoro**.

   ![nodo_volume_flusso di lavoro](assets/workflow_volume_node.png)

   Quando selezioni un report, il pannello **Parametri del report** viene visualizzato a destra della visualizzazione struttura.

   ![pannello parametri report processi a esecuzione prolungata](assets/workflow_volume_params.png)

   Parametri:

   * **Seleziona processo** (*obbligatorio*): seleziona un processo AEM Forms.

   * **Iniziato dopo** (*facoltativo*): seleziona una data. Filtra il report per visualizzare le istanze di processo avviate dopo la data specificata.

   * **Iniziato prima del** (*facoltativo*): seleziona una data. Filtra il report per visualizzare le istanze di processo avviate prima della data specificata.

1. Fare clic su **Vai** per eseguire il report.

   Il report viene visualizzato nel pannello **Report** a destra della finestra **Report dei processi**.

   ![workflow_volume_report](assets/workflow_volume_report.png)

   Utilizzare le opzioni nell&#39;angolo superiore destro del pannello **Report** per eseguire le operazioni seguenti nel report.

   * **Aggiorna**: aggiorna il report con i dati più recenti presenti nell&#39;archivio
   * **Cambia colore legenda**: selezionare e modificare il colore della legenda del report
   * **Esporta in CSV**: esporta e scarica i dati dal report in un file separato da virgole
