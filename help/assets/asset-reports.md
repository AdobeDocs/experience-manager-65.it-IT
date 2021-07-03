---
title: Rapporti sull’utilizzo e la condivisione delle risorse
description: Rapporti sulle risorse in [!DNL Adobe Experience Manager Assets] per comprendere l’utilizzo, l’attività e la condivisione delle risorse digitali.
contentOwner: AG
role: User, Admin
feature: Rapporti sulle risorse,Gestione delle risorse
exl-id: b4963a03-3496-4c6c-9d30-8812304d0e9f
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 9%

---

# Rapporti sulle risorse {#asset-reports}

Il reporting delle risorse consente di valutare l’utilità della distribuzione [!DNL Adobe Experience Manager Assets]. Con [!DNL Assets] puoi generare vari rapporti per le risorse digitali. I rapporti forniscono informazioni utili sull’utilizzo del sistema, su come gli utenti interagiscono con le risorse e quali risorse vengono scaricate e condivise.

Utilizza le informazioni contenute nei rapporti per derivare le metriche di successo chiave per misurare l’adozione di [!DNL Assets] all’interno dell’azienda e da parte dei clienti.

Il framework di reporting [!DNL Assets] utilizza [!DNL Sling] processi per elaborare in modo asincrono le richieste di report in modo ordinato. È scalabile per archivi di grandi dimensioni. L’elaborazione asincrona dei rapporti aumenta l’efficienza e la velocità con cui vengono generati i rapporti.

L’interfaccia di gestione dei rapporti è intuitiva e include opzioni e controlli a grana fine per accedere ai rapporti archiviati e visualizzare gli stati di esecuzione dei rapporti (con esito positivo, non riuscito e in coda).

Quando viene generato un rapporto, riceverai una notifica tramite e-mail (opzionale) e una notifica tramite una casella in entrata. Puoi visualizzare, scaricare o eliminare un rapporto dalla pagina di elenco dei rapporti, in cui vengono visualizzati tutti i rapporti generati in precedenza.

## Prerequisito {#prerequisite-for-reporting}

Per generare rapporti, procedi come segue:

* Attiva il servizio [!UICONTROL Day CQ DAM Event Recorder] da **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console Web]**.
* Seleziona le attività o gli eventi sui quali desideri creare rapporti. Ad esempio, per generare un rapporto sulle risorse scaricate, seleziona [!UICONTROL Risorsa scaricata (DOWNLOADED)].

![Abilitare il reporting delle risorse nella console Web](assets/reports-config-day-cq-dam-event-recorder.png)

## Genera report {#generate-reports}

[!DNL Experience Manager Assets] genera i seguenti rapporti standard:

* Carica
* Scarica
* Scadenza
* Modifiche
* Pubblicazione
* [!DNL Brand Portal] pubblicazione
* Utilizzo disco
* File
* Condivisione collegamenti

[!DNL Adobe Experience Manager] gli amministratori possono generare e personalizzare facilmente questi rapporti per la tua implementazione. Un amministratore può seguire questi passaggi per generare un rapporto:

1. Nell&#39;interfaccia [!DNL Experience Manager] fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Rapporti]**.

   ![Pagina degli strumenti per navigare nel rapporto delle risorse](assets/AssetsReportNavigation.png)

1. Nella pagina [!UICONTROL Rapporti su risorse], fai clic su **[!UICONTROL Crea]** nella barra degli strumenti.
1. Dalla pagina **[!UICONTROL Crea rapporto]**, scegli il rapporto che desideri creare e fai clic su **[!UICONTROL Avanti]**.

   ![Seleziona tipo di rapporto](assets/choose_report.png)

   >[!NOTE]
   >
   >Per impostazione predefinita, i frammenti di contenuto e le condivisioni di collegamento sono inclusi nel rapporto Risorsa [!UICONTROL Scarica] . Seleziona l’opzione appropriata per creare un rapporto di condivisioni di collegamenti o per escludere frammenti di contenuto dal rapporto di download.

   >[!NOTE]
   >
   >Il rapporto [!UICONTROL Download] visualizza i dettagli solo delle risorse scaricate dopo la selezione singolarmente o scaricate tramite Azione rapida. Tuttavia, non include i dettagli delle risorse che si trovano all’interno di una cartella scaricata.

1. Configura i dettagli del rapporto come titolo, descrizione, miniatura e percorso della cartella nell&#39;archivio CRX in cui è memorizzato il rapporto. Per impostazione predefinita, il percorso della cartella è `/content/dam`. È possibile specificare un percorso diverso.

   ![Pagina per aggiungere i dettagli del rapporto](assets/report_configuration.png)

   Scegli l’intervallo di date per il rapporto.

   Puoi scegliere di generare il rapporto ora o in una data e in un’ora future.

   >[!NOTE]
   >
   >Se scegli di pianificare il rapporto in un secondo momento, accertati di specificare la data e l’ora nei campi Data e ora. Se non si specifica alcun valore, il motore di report lo considera come un report da generare immediatamente.

   I campi di configurazione possono variare a seconda del tipo di rapporto creato. Ad esempio, il rapporto **[!UICONTROL Utilizzo del disco]** fornisce opzioni per includere le rappresentazioni delle risorse nel calcolo dello spazio su disco utilizzato dalle risorse. È possibile scegliere di includere o escludere le risorse nelle sottocartelle per il calcolo dell’utilizzo del disco.

   >[!NOTE]
   >
   >Il rapporto **[!UICONTROL Utilizzo spazio su disco]** non include campi intervallo di date, poiché indica solo l’utilizzo attuale dello spazio.

   ![Pagina dei dettagli del rapporto Utilizzo disco](assets/disk_usage_configuration.png)

   Quando crei il rapporto **[!UICONTROL File]**, puoi includere o escludere le sottocartelle. Tuttavia, non puoi includere rappresentazioni di risorse per questo rapporto.

   ![Pagina dei dettagli del rapporto File](assets/files_report.png)

   Il rapporto **[!UICONTROL Condivisione collegamenti]** visualizza gli URL delle risorse condivise con utenti esterni da [!DNL Assets]. Include gli ID e-mail dell’utente che ha condiviso le risorse, gli ID e-mail degli utenti con cui le risorse sono condivise, la data di condivisione e la data di scadenza del collegamento. Le colonne non sono personalizzabili.

   Il rapporto **[!UICONTROL Condivisione collegamenti]** non include opzioni per le sottocartelle e i rendering, in quanto pubblica semplicemente gli URL condivisi visualizzati in `/var/dam/share`.

   ![Pagina dei dettagli del rapporto Condivisione collegamenti](assets/link_share.png)

1. Fare clic su **[!UICONTROL Avanti]** nella barra degli strumenti.

1. Nella pagina **[!UICONTROL Configura colonne]**, alcune colonne sono selezionate per essere visualizzate nel rapporto per impostazione predefinita. Puoi selezionare più colonne. Annulla la selezione di una colonna per escluderla nel rapporto.

   ![Selezionare o annullare la selezione delle colonne del rapporto](assets/configure_columns.png)

   Per visualizzare un nome di colonna personalizzato o un percorso di proprietà, configura le proprietà per il binario di risorsa sotto il nodo `jcr:content` in CRX. In alternativa, aggiungilo tramite il selettore del percorso della proprietà.

   ![Selezionare o annullare la selezione delle colonne del rapporto](assets/custom_columns.png)

1. Fai clic su **[!UICONTROL Crea]** nella barra degli strumenti. Un messaggio notifica l’avvio della generazione del rapporto.
1. Nella pagina [!UICONTROL Rapporti su risorse], lo stato di generazione del rapporto si basa sullo stato corrente del processo di rapporto, ad esempio [!UICONTROL Success], [!UICONTROL Failed], [!UICONTROL Queued] o [!UICONTROL Scheduled]. Lo stesso stato viene visualizzato nella casella in entrata delle notifiche.Per visualizzare la pagina del rapporto, fare clic sul collegamento del rapporto. In alternativa, seleziona il rapporto e fai clic su **[!UICONTROL Visualizza]** nella barra degli strumenti.

   ![Un rapporto generato](assets/report_page.png)

   Fai clic su **[!UICONTROL Scarica]** dalla barra degli strumenti per scaricare il rapporto in formato CSV.

## Aggiungi colonne personalizzate {#add-custom-columns}

Puoi aggiungere colonne personalizzate ai seguenti rapporti per visualizzare più dati per le tue esigenze personalizzate:

* Carica
* Scarica
* Scadenza
* Modifiche
* Pubblicazione
* [!DNL Brand Portal] pubblicazione
* File

Per aggiungere colonne personalizzate a questi rapporti, effettua le seguenti operazioni:

1. In [!DNL Manager interface], fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Rapporti]**.
1. Nella pagina [!UICONTROL Rapporti su risorse], fai clic su **[!UICONTROL Crea]** nella barra degli strumenti.

1. Dalla pagina **[!UICONTROL Crea rapporto]**, scegli il rapporto che desideri creare e fai clic su **[!UICONTROL Avanti]**.
1. Configura i dettagli del rapporto come titolo, descrizione, miniatura, percorso della cartella e intervallo di date, a seconda delle necessità.

1. Per visualizzare una colonna personalizzata, specificane il nome in **[!UICONTROL Colonne personalizzate]**.

   ![Specifica il nome della colonna del report personalizzata](assets/custom_columns-1.png)

1. Aggiungi il percorso della proprietà sotto il nodo `jcr:content` in CRXDE utilizzando il selettore del percorso della proprietà. In alternativa, digitare il percorso nel campo percorso della proprietà.

   ![Mappa il percorso della proprietà dai percorsi in jcr:content](assets/property_picker.png)

   Per aggiungere altre colonne personalizzate, fai clic su **[!UICONTROL Aggiungi]** e ripeti i passaggi 5 e 6.

1. Fai clic su **[!UICONTROL Crea]** nella barra degli strumenti. Un messaggio notifica l’avvio della generazione del rapporto.

## Configurare il servizio di eliminazione {#configure-purging-service}

Per rimuovere i rapporti non più necessari, configura il servizio di eliminazione dei rapporti DAM dalla console Web per eliminare i rapporti esistenti in base alla loro quantità ed età.

1. Accedi alla console Web (gestione della configurazione) da `https://[aem_server]:[port]/system/console/configMgr`.
1. Apri la configurazione **[!UICONTROL DAM Report Purge Service]** .
1. Specifica la frequenza (intervallo di tempo) del servizio di eliminazione nel campo `scheduler.expression.name` . Puoi anche configurare la soglia di età e quantità per i rapporti.
1. Salva le modifiche.

## Informazioni, suggerimenti e limitazioni sulla risoluzione dei problemi {#best-practices-and-limitations}

* Se alcuni rapporti o numeri nei rapporti non sono disponibili o come previsto, assicurati che il servizio [!UICONTROL Day CQ DAM Event Recorder] sia abilitato.

* Rimuovi i rapporti non più necessari. Utilizza le opzioni di configurazione nel servizio di eliminazione dei rapporti DAM per configurare i criteri per l’eliminazione dei rapporti.

* Se il rapporto sull&#39;utilizzo del disco non viene generato e si utilizza [!DNL Dynamic Media], verificare che tutte le risorse procedano correttamente. Per risolvere il problema, rielabora le risorse e quindi genera di nuovo il rapporto.
