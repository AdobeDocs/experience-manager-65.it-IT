---
title: Rapporti sull’utilizzo e la condivisione delle risorse
description: Rapporti sulle risorse in [!DNL Adobe Experience Manager Assets] per comprendere l'utilizzo, l'attività e la condivisione delle risorse digitali.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 10%

---


# Rapporti su risorse {#asset-reports}

Il reporting delle risorse consente di valutare l&#39;utilità della distribuzione [!DNL Adobe Experience Manager Assets]. Con [!DNL Assets] potete generare vari rapporti per le risorse digitali. I rapporti forniscono informazioni utili sull’utilizzo del sistema, su come gli utenti interagiscono con le risorse e quali risorse vengono scaricate e condivise.

Utilizzate le informazioni contenute nei report per derivare le metriche di successo chiave per misurare l&#39;adozione di [!DNL Assets] all&#39;interno dell&#39;azienda e da parte dei clienti.

Il framework di report [!DNL Assets] utilizza i processi [!DNL Sling] per elaborare in modo asincrono le richieste di report in modo ordinato. È scalabile per archivi di grandi dimensioni. L&#39;elaborazione asincrona dei report aumenta l&#39;efficienza e la velocità con cui vengono generati i report.

L&#39;interfaccia di gestione dei report è intuitiva e include opzioni e controlli di granulometria per accedere ai report archiviati e visualizzare gli stati di esecuzione dei report (operazione riuscita, non riuscita e in coda).

Quando viene generato un rapporto, riceverete una notifica via e-mail (facoltativo) e una notifica nella inbox. Puoi visualizzare, scaricare o eliminare un rapporto dalla pagina di elenco dei rapporti, dove vengono visualizzati tutti i rapporti generati in precedenza.

## Prerequisito {#prerequisite-for-reporting}

Per generare i rapporti, effettuate le seguenti operazioni:

* Abilitare il servizio [!UICONTROL Giornata di registrazione eventi CQ DAM] da **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console Web]**.
* Selezionate le attività o gli eventi sui quali desiderate creare rapporti. Ad esempio, per generare un rapporto sulle risorse scaricate, selezionate [!UICONTROL Risorsa scaricata (DOWNLOADED)].

![Abilitare i rapporti sulle risorse nella console Web](assets/reports-config-day-cq-dam-event-recorder.png)

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

[!DNL Adobe Experience Manager] gli amministratori possono generare e personalizzare facilmente questi rapporti per la vostra implementazione. Per generare un rapporto, un amministratore può effettuare le seguenti operazioni:

1. Nell&#39;interfaccia [!DNL Experience Manager] fare clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Rapporti]**.

   ![Pagina degli strumenti per navigare nel rapporto delle risorse](assets/AssetsReportNavigation.png)

1. Nella pagina [!UICONTROL Report risorse], fate clic su **[!UICONTROL Crea]** nella barra degli strumenti.
1. Dalla pagina **[!UICONTROL Crea rapporto]**, scegliere il rapporto che si desidera creare e fare clic su **[!UICONTROL Avanti]**.

   ![Selezionare il tipo di rapporto](assets/choose_report.png)

   >[!NOTE]
   >
   >Per impostazione predefinita, i frammenti di contenuto e le condivisioni di collegamenti sono inclusi nel rapporto Risorse [!UICONTROL Scarica]. Selezionate l&#39;opzione appropriata per creare un rapporto delle condivisioni di collegamenti o per escludere i frammenti di contenuto dal rapporto di download.

   >[!NOTE]
   >
   >Il rapporto [!UICONTROL Download] visualizza i dettagli solo delle risorse che vengono scaricate dopo la selezione individuale o che vengono scaricate tramite la funzione Azione rapida. Tuttavia, non include i dettagli delle risorse che si trovano all’interno di una cartella scaricata.

1. Configurare i dettagli del rapporto come titolo, descrizione, miniatura e percorso della cartella nell&#39;archivio CRX in cui è memorizzato il rapporto. Per impostazione predefinita, il percorso della cartella è `/content/dam`. Potete specificare un percorso diverso.

   ![Pagina per aggiungere i dettagli del rapporto](assets/report_configuration.png)

   Scegli l&#39;intervallo di date per il rapporto.

   Puoi scegliere di generare il rapporto adesso o in una data e in un&#39;ora future.

   >[!NOTE]
   >
   >Se scegli di pianificare il rapporto in un secondo momento, accertati di specificare la data e l’ora nei campi Data e Ora. Se non si specifica alcun valore, il motore di report lo gestisce come un report da generare all&#39;istante.

   I campi di configurazione possono essere diversi in base al tipo di rapporto creato. Ad esempio, il rapporto **[!UICONTROL Uso del disco]** fornisce opzioni per includere le rappresentazioni delle risorse nel calcolo dello spazio su disco utilizzato dalle risorse. Potete scegliere di includere o escludere le risorse nelle sottocartelle per il calcolo dell’utilizzo del disco.

   >[!NOTE]
   >
   >Il rapporto **[!UICONTROL Utilizzo spazio su disco]** non include campi intervallo di date, poiché indica solo l’utilizzo attuale dello spazio.

   ![Pagina dei dettagli del rapporto Uso del disco](assets/disk_usage_configuration.png)

   Quando create il rapporto **[!UICONTROL File]**, potete includere o escludere sottocartelle. Tuttavia, non potete includere rappresentazioni delle risorse per questo rapporto.

   ![Pagina dei dettagli del rapporto sui file](assets/files_report.png)

   Il rapporto **[!UICONTROL Condivisione collegamenti]** visualizza gli URL delle risorse condivise con utenti esterni da [!DNL Assets]. Include gli ID e-mail dell’utente che ha condiviso le risorse, gli ID e-mail degli utenti con cui le risorse sono condivise, la data di condivisione e la data di scadenza del collegamento. Le colonne non sono personalizzabili.

   Il rapporto **[!UICONTROL Condivisione collegamenti]** non include opzioni per sottocartelle e rappresentazioni, perché pubblica semplicemente gli URL condivisi visualizzati in `/var/dam/share`.

   ![Pagina dei dettagli del rapporto Condivisione collegamenti](assets/link_share.png)

1. Fare clic su **[!UICONTROL Next]** dalla barra degli strumenti.

1. Nella pagina **[!UICONTROL Configura colonne]**, per impostazione predefinita nel rapporto vengono selezionate alcune colonne. È possibile selezionare più colonne. Deselezionate una colonna selezionata per escluderla nel rapporto.

   ![Seleziona o deseleziona le colonne del rapporto](assets/configure_columns.png)

   Per visualizzare un nome di colonna o un percorso di proprietà personalizzato, configura le proprietà per il binario della risorsa sotto il nodo `jcr:content` in CRX. In alternativa, aggiungetelo tramite il selettore del percorso della proprietà.

   ![Seleziona o deseleziona le colonne del rapporto](assets/custom_columns.png)

1. Fare clic su **[!UICONTROL Crea]** dalla barra degli strumenti. Un messaggio notifica che è stata avviata la generazione del report.
1. Nella pagina [!UICONTROL Report risorse], lo stato di generazione del rapporto è basato sullo stato corrente del processo del rapporto, ad esempio [!UICONTROL Success], [!UICONTROL Failed], [!UICONTROL Queued] o [!UICONTROL Scheduled]. Lo stesso stato viene visualizzato nella inbox delle notifiche.Per visualizzare la pagina del rapporto, fai clic sul collegamento del rapporto. In alternativa, selezionare il rapporto e fare clic su **[!UICONTROL Visualizza]** nella barra degli strumenti.

   ![Report generato](assets/report_page.png)

   Fate clic su **[!UICONTROL Scarica]** dalla barra degli strumenti per scaricare il rapporto in formato CSV.

## Aggiungi colonne personalizzate {#add-custom-columns}

Puoi aggiungere colonne personalizzate ai report seguenti per visualizzare più dati per i tuoi requisiti personalizzati:

* Carica
* Scarica
* Scadenza
* Modifiche
* Pubblicazione
* [!DNL Brand Portal] pubblicazione
* File

Per aggiungere colonne personalizzate a questi rapporti, procedere come segue:

1. In [!DNL Manager interface], fare clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Rapporti]**.
1. Nella pagina [!UICONTROL Report risorse], fate clic su **[!UICONTROL Crea]** nella barra degli strumenti.

1. Dalla pagina **[!UICONTROL Crea rapporto]**, scegliere il rapporto che si desidera creare e fare clic su **[!UICONTROL Avanti]**.
1. Configura i dettagli del rapporto come titolo, descrizione, miniatura, percorso della cartella e intervallo di date, a seconda delle necessità.

1. Per visualizzare una colonna personalizzata, specificane il nome in **[!UICONTROL Colonne personalizzate]**.

   ![Specificare il nome per la colonna personalizzata del rapporto](assets/custom_columns-1.png)

1. Aggiungete il percorso della proprietà sotto il nodo `jcr:content` in CRXDE utilizzando il selettore del percorso della proprietà. In alternativa, digitare il percorso nel campo percorso della proprietà.

   ![Mappare il percorso della proprietà dai percorsi in jcr:content](assets/property_picker.png)

   Per aggiungere altre colonne personalizzate, fare clic su **[!UICONTROL Aggiungi]** e ripetere i passaggi 5 e 6.

1. Fare clic su **[!UICONTROL Crea]** dalla barra degli strumenti. Un messaggio notifica che è stata avviata la generazione del report.

## Configurare il servizio di eliminazione {#configure-purging-service}

Per rimuovere i rapporti non più necessari, configura il servizio Rimozione rapporti DAM dalla console Web per eliminare i rapporti esistenti in base alla loro quantità e età.

1. Accedete alla console Web (Gestione configurazione) da `https://[aem_server]:[port]/system/console/configMgr`.
1. Aprire la configurazione **[!UICONTROL DAM Report Purge Service]**.
1. Specificare la frequenza (intervallo di tempo) per il servizio di eliminazione nel campo `scheduler.expression.name`. Puoi anche configurare la soglia di età e quantità per i rapporti.
1. Salva le modifiche.
