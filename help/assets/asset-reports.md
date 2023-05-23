---
title: Rapporti sull’utilizzo e la condivisione delle risorse
description: Rapporti sulle risorse in [!DNL Adobe Experience Manager Assets] che ti aiutano a comprendere l’utilizzo, l’attività e la condivisione delle risorse digitali.
contentOwner: AG
role: User, Admin
feature: Asset Reports,Asset Management
exl-id: b4963a03-3496-4c6c-9d30-8812304d0e9f
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '1162'
ht-degree: 9%

---

# Rapporti sulle risorse {#asset-reports}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/asset-reports.html?lang=en) |
| AEM 6.5 | Questo articolo |

La generazione di rapporti sulle risorse consente di valutare l’utilità della [!DNL Adobe Experience Manager Assets] distribuzione. Con [!DNL Assets], puoi generare vari rapporti per le risorse digitali. I rapporti forniscono informazioni utili sull’utilizzo del sistema, sul modo in cui gli utenti interagiscono con le risorse e sulle risorse scaricate e condivise.

Utilizza le informazioni contenute nei rapporti per derivare le metriche di successo chiave con cui misurare l’adozione di [!DNL Assets] all&#39;interno dell&#39;azienda e dai clienti.

Il [!DNL Assets] utilizzo del framework di reporting [!DNL Sling] processi per elaborare in modo asincrono le richieste di rapporti in modo ordinato. È scalabile per archivi di grandi dimensioni. L’elaborazione asincrona dei rapporti aumenta l’efficienza e la velocità con cui vengono generati.

L’interfaccia di gestione dei rapporti è intuitiva e include opzioni e controlli dettagliati per accedere ai rapporti archiviati e visualizzare gli stati di esecuzione dei rapporti (operazione riuscita, non riuscita e in coda).

Quando viene generato un rapporto, l’utente riceve una notifica tramite e-mail (facoltativa) e una notifica nella casella in entrata. Puoi visualizzare, scaricare o eliminare un rapporto dalla pagina dell’elenco dei rapporti, in cui vengono visualizzati tutti i rapporti generati in precedenza.

## Prerequisito {#prerequisite-for-reporting}

Per generare i rapporti, effettuare le seguenti operazioni:

* Abilita [!UICONTROL Day CQ DAM Event Recorder] servizio da **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console web]**.
* Seleziona le attività o gli eventi per i quali desideri generare rapporti. Ad esempio, per generare un rapporto sulle risorse scaricate, seleziona [!UICONTROL Risorsa scaricata (DOWNLOADED)].

![Abilitare la generazione di rapporti sulle risorse nella console web](assets/reports-config-day-cq-dam-event-recorder.png)

## Generare rapporti {#generate-reports}

[!DNL Experience Manager Assets] genera automaticamente i seguenti rapporti standard:

* Caricare
* Scarica
* Scadenza
* Modifiche
* Pubblicazione
* [!DNL Brand Portal] pubblicazione
* Utilizzo disco
* File
* Condivisione collegamenti

[!DNL Adobe Experience Manager] gli amministratori possono generare e personalizzare facilmente questi rapporti per la tua implementazione. Per generare un rapporto, l’amministratore può effettuare le seguenti operazioni:

1. In entrata [!DNL Experience Manager] , fare clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Rapporti]**.

   ![Pagina Strumenti per passare al rapporto delle risorse](assets/AssetsReportNavigation.png)

1. Il giorno [!UICONTROL Rapporti su risorse] pagina, fai clic su **[!UICONTROL Crea]** dalla barra degli strumenti.
1. Dalla sezione **[!UICONTROL Crea rapporto]** , scegli il rapporto da creare e fai clic su **[!UICONTROL Successivo]**.

   ![Seleziona tipo di rapporto](assets/choose_report.png)

   >[!NOTE]
   >
   >Per impostazione predefinita, i frammenti di contenuto e le condivisioni di collegamenti sono inclusi nella risorsa [!UICONTROL Scarica] rapporto. Seleziona l’opzione appropriata per creare un rapporto sulle condivisioni di collegamenti o per escludere Frammenti di contenuto dal rapporto di download.

   >[!NOTE]
   >
   >Il [!UICONTROL Scarica] Il rapporto mostra i dettagli solo delle risorse che vengono scaricate dopo aver selezionato singolarmente o che vengono scaricate tramite Azione rapida. Tuttavia, non include i dettagli delle risorse all’interno di una cartella scaricata.

1. Configura i dettagli del rapporto come titolo, descrizione, miniatura e percorso della cartella nell’archivio CRX in cui è memorizzato il rapporto. Per impostazione predefinita, il percorso della cartella è `/content/dam`. È possibile specificare un percorso diverso.

   ![Pagina per aggiungere i dettagli del rapporto](assets/report_configuration.png)

   Scegli l’intervallo di date per il rapporto.

   Puoi scegliere di generare il rapporto ora o in una data e un’ora future.

   >[!NOTE]
   >
   >Se si sceglie di pianificare il rapporto in un secondo momento, assicurarsi di specificare la data e l&#39;ora nei campi Data e ora. Se non specifichi alcun valore, il motore di report lo tratta come un report che deve essere generato immediatamente.

   I campi di configurazione possono variare in base al tipo di rapporto creato. Ad esempio, il **[!UICONTROL Utilizzo disco]** Il rapporto fornisce opzioni per includere le rappresentazioni delle risorse durante il calcolo dello spazio su disco utilizzato dalle risorse. Puoi scegliere di includere o escludere le risorse nelle sottocartelle per il calcolo dell’utilizzo del disco.

   >[!NOTE]
   >
   >Il rapporto **[!UICONTROL Utilizzo spazio su disco]** non include campi intervallo di date, poiché indica solo l’utilizzo attuale dello spazio.

   ![Pagina Dettagli del report Utilizzo disco](assets/disk_usage_configuration.png)

   Quando crei il **[!UICONTROL File]** rapporto, puoi includere/escludere sottocartelle. Tuttavia, per questo rapporto non puoi includere rappresentazioni di risorse.

   ![Pagina Dettagli del rapporto File](assets/files_report.png)

   Il rapporto **[!UICONTROL Condivisione collegamenti]** visualizza gli URL delle risorse condivise con utenti esterni da [!DNL Assets]. Include gli ID e-mail dell’utente che ha condiviso le risorse, gli ID e-mail degli utenti con cui le risorse sono condivise, la data di condivisione e la data di scadenza del collegamento. Le colonne non sono personalizzabili.

   Il **[!UICONTROL Condivisione collegamenti]** , non include opzioni per sottocartelle e rappresentazioni, in quanto pubblica semplicemente gli URL condivisi visualizzati in `/var/dam/share`.

   ![Pagina dei dettagli del rapporto Condivisione collegamenti](assets/link_share.png)

1. Clic **[!UICONTROL Successivo]** dalla barra degli strumenti.

1. In **[!UICONTROL Configura colonne]** , alcune colonne vengono selezionate per essere visualizzate nel rapporto per impostazione predefinita. Puoi selezionare più colonne. Annulla la selezione di una colonna per escluderla nel rapporto.

   ![Seleziona o annulla la selezione delle colonne del rapporto](assets/configure_columns.png)

   Per visualizzare il nome di una colonna personalizzata o il percorso di una proprietà, configura le proprietà del binario della risorsa in `jcr:content` in CRX. In alternativa, aggiungilo tramite il selettore del percorso delle proprietà.

   ![Seleziona o annulla la selezione delle colonne del rapporto](assets/custom_columns.png)

1. Clic **[!UICONTROL Crea]** dalla barra degli strumenti. Un messaggio notifica che la generazione del rapporto è stata avviata.
1. Il giorno [!UICONTROL Rapporti su risorse] pagina, lo stato di generazione del rapporto si basa sullo stato corrente del processo di rapporto, ad esempio [!UICONTROL Completato], [!UICONTROL Non riuscito], [!UICONTROL In coda], o [!UICONTROL Pianificato]. Lo stesso stato viene visualizzato nella casella in entrata delle notifiche.Per visualizzare la pagina del report, fare clic sul collegamento al report. In alternativa, seleziona il rapporto e fai clic su **[!UICONTROL Visualizza]** dalla barra degli strumenti.

   ![Un rapporto generato](assets/report_page.png)

   Clic **[!UICONTROL Scarica]** dalla barra degli strumenti per scaricare il rapporto in formato CSV.

## Aggiungi colonne personalizzate {#add-custom-columns}

Puoi aggiungere colonne personalizzate ai seguenti rapporti per visualizzare più dati in base ai tuoi requisiti personalizzati:

* Caricare
* Scarica
* Scadenza
* Modifiche
* Pubblicazione
* [!DNL Brand Portal] pubblicazione
* File

Per aggiungere colonne personalizzate a questi rapporti, effettua le seguenti operazioni:

1. In [!DNL Manager interface], fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Rapporti]**.
1. Il giorno [!UICONTROL Rapporti su risorse] pagina, fai clic su **[!UICONTROL Crea]** dalla barra degli strumenti.

1. Dalla sezione **[!UICONTROL Crea rapporto]** , scegli il rapporto da creare e fai clic su **[!UICONTROL Successivo]**.
1. Configura i dettagli del rapporto come titolo, descrizione, miniatura, percorso della cartella e intervallo di date, a seconda dei casi.

1. Per visualizzare una colonna personalizzata, specificane il nome in **[!UICONTROL Colonne personalizzate]**.

   ![Specifica il nome per la colonna personalizzata del rapporto](assets/custom_columns-1.png)

1. Aggiungi il percorso della proprietà sotto `jcr:content` in CRXDE utilizzando il selettore del percorso delle proprietà. In alternativa, digita il percorso nel campo percorso proprietà.

   ![Mappare il percorso proprietà dai percorsi in jcr:content](assets/property_picker.png)

   Per aggiungere altre colonne personalizzate, fai clic su **[!UICONTROL Aggiungi]** e ripetere i passaggi 5 e 6.

1. Clic **[!UICONTROL Crea]** dalla barra degli strumenti. Un messaggio notifica che la generazione del rapporto è stata avviata.

## Configura servizio di eliminazione {#configure-purging-service}

Per rimuovere i rapporti che non sono più necessari, configura il servizio Rimozione rapporti DAM dalla console web per rimuovere i rapporti esistenti in base alla quantità e all’età.

1. Accedi alla console web (gestione configurazione) da `https://[aem_server]:[port]/system/console/configMgr`.
1. Apri **[!UICONTROL Servizio eliminazione report DAM]** configurazione.
1. Specificare la frequenza (intervallo di tempo) per il servizio di eliminazione in `scheduler.expression.name` campo. Puoi anche configurare la soglia di età e di quantità per i rapporti.
1. Salva le modifiche.

## Informazioni, suggerimenti e limitazioni per la risoluzione dei problemi {#best-practices-and-limitations}

* Se alcuni rapporti o numeri non sono disponibili o non sono conformi alle previsioni, assicurati che [!UICONTROL Day CQ DAM Event Recorder] il servizio è abilitato.

* Rimuovi i rapporti che non sono più necessari. Utilizza le opzioni di configurazione nel servizio Rimozione report DAM per configurare i criteri per l’eliminazione dei report.

* Se il Report utilizzo disco non viene generato e si utilizza [!DNL Dynamic Media], assicurati che tutte le risorse procedano correttamente. Per risolvere il problema, rielabora le risorse e quindi genera di nuovo il rapporto.
