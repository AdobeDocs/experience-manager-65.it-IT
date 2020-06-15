---
title: Importate ed esportate i metadati delle risorse in blocco.
description: Importazione ed esportazione in massa di metadati di risorse digitali.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9d6f9b8f8d49ae3322a6f5f677292afbd48beeda
workflow-type: tm+mt
source-wordcount: '808'
ht-degree: 5%

---


# Importare ed esportare in massa i metadati delle risorse {#import-and-export-asset-metadata-in-bulk}

[!DNL Adobe Experience Manager Assets] consente di importare in massa i metadati delle risorse mediante un file CSV. Potete eseguire aggiornamenti in blocco per le risorse caricate di recente o per le risorse esistenti importando un file CSV. Potete anche assimilare i metadati delle risorse in massa da sistemi di terze parti in formato CSV.

## Importare i metadati {#import-metadata}

L&#39;importazione dei metadati è asincrona e non ostacola le prestazioni del sistema. L’aggiornamento simultaneo dei metadati per più risorse può richiedere molte risorse a causa dell’attività di reinserimento XMP se è selezionato il flag del flusso di lavoro. Pianificate tale importazione durante l&#39;utilizzo di un server snello in modo che le prestazioni per altri utenti non vengano compromesse.

>[!NOTE]
>
>Per importare i metadati negli spazi dei nomi personalizzati, registrate prima gli spazi dei nomi.

1. Passate all’interfaccia [!DNL Assets] utente e fate clic su **[!UICONTROL Crea]** dalla barra degli strumenti.
1. Dal menu, selezionate **[!UICONTROL Metadati]**.
1. In the **[!UICONTROL Metadata Import]** page, click **[!UICONTROL Select File]**. Scegli il file CSV con i metadati.
1. Specificate i seguenti parametri. Consultate un file CSV di esempio in [metadata-import-sample-file.csv](assets/metadata-import-sample-file.csv).

   | Parametri di importazione metadati | Descrizione |
   |:---|:---|
   | [!UICONTROL Dimensione batch] | Numero di risorse in un batch per cui importare i metadati. Il valore predefinito è 50. Il valore massimo è 100. |
   | [!UICONTROL Separatore di campi] | Il valore predefinito è `,` (una virgola). È possibile specificare qualsiasi altro carattere. |
   | [!UICONTROL Delimitatore valori multipli] | Separatore per i valori dei metadati. Il valore predefinito è `|`. |
   | [!UICONTROL Avvia flussi di lavoro] | False per impostazione predefinita. Quando è impostata su `true` e le impostazioni predefinite di Launcher sono attive per il flusso di lavoro WriteBack [!UICONTROL metadati] DAM (che scrive i metadati nei dati XMP binari). L&#39;attivazione dei flussi di lavoro di avvio rallenta il sistema. |
   | [!UICONTROL Nome colonna percorso risorsa] | Definisce il nome della colonna per il file CSV con le risorse. |

1. Fate clic su **[!UICONTROL Importa]** dalla barra degli strumenti. Una volta importati i metadati, nella inbox delle [!UICONTROL notifiche] viene visualizzata una notifica.

1. Per verificare la corretta importazione, andate alla pagina [!UICONTROL Proprietà] di una risorsa e verificate i valori nei campi.

Per aggiungere data e marca temporale al momento dell’importazione dei metadati, utilizzate `YYYY-MM-DDThh:mm:ss.fff-00:00` il formato per la data e l’ora. Data e ora sono separate da `T`, `hh` è ore in formato 24 ore, `fff` è nanosecondi e `-00:00` è l’offset del fuso orario. Ad esempio, `2020-03-26T11:26:00.000-07:00` è il 26 marzo 2020 alle 11:26:00.000 ora di ora precedente.

>[!CAUTION]
>
>Se il formato della data non corrisponde, `YYYY-MM-DDThh:mm:ss.fff-00:00`i valori della data non vengono impostati. I formati data del file CSV dei metadati esportati sono nel formato `YYYY-MM-DDThh:mm:ss-00:00`. Se desiderate importarlo, convertitelo nel formato accettabile aggiungendo il valore nanosecondi indicato da `fff`.

## Export metadata {#export-metadata}

Potete esportare i metadati per più risorse in formato CSV. I metadati vengono esportati in modo asincrono e non influiscono sulle prestazioni del sistema. Per esportare i metadati, [!DNL Experience Manager] scorrono le proprietà del nodo della risorsa `jcr:content/metadata` e dei relativi nodi secondari ed esportano le proprietà dei metadati in un file CSV.

Alcuni esempi di utilizzo per l’esportazione di metadati in massa sono:

* Importate i metadati in un sistema di terze parti durante la migrazione delle risorse.
* Condividete i metadati delle risorse con un team di progetto più ampio.
* Verificate o verificate la conformità dei metadati.
* Esternalizzate i metadati per localizzarli separatamente.

1. Selezionate la cartella di risorse che contiene le risorse per le quali desiderate esportare i metadati. Dalla barra degli strumenti, selezionate **[!UICONTROL Esporta metadati]**.

1. Nella finestra di dialogo Esportazione  metadati, specificate un nome per il file CSV. Per esportare i metadati delle risorse nelle sottocartelle, selezionate **[!UICONTROL Includi risorse nelle sottocartelle]**.

   ![Interfaccia e opzioni per l’esportazione dei metadati di tutte le risorse di una](assets/export_metadata_page.png "cartellaInterfaccia e opzioni per l’esportazione dei metadati di tutte le risorse di una cartella")

1. Selezionate le opzioni desiderate. Specificare un nome di file e, se necessario, una data.

1. Nel campo **[!UICONTROL Proprietà da esportare]** , specificate se esportare tutte le proprietà o solo proprietà specifiche. Se scegliete le proprietà selettive da esportare, aggiungete le proprietà desiderate.

1. Dalla barra degli strumenti, fate clic su **[!UICONTROL Esporta]**. Viene visualizzato un messaggio di conferma dell’esportazione dei metadati. Chiudi il messaggio.

1. Apri la notifica della casella in entrata del processo di esportazione. Seleziona il processo e fai clic su **[!UICONTROL Apri]** nella barra degli strumenti. To download the CSV file with the metadata, click **[!UICONTROL CSV Download]** from the toolbar. Fai clic su **[!UICONTROL Chiudi]**.

   ![Finestra di dialogo per scaricare il file CSV contenente i metadati esportati in massa](assets/csv_download.png)

   *Figura: Finestra di dialogo per scaricare il file CSV contenente i metadati esportati in massa.*

## Best practice, limitazioni e suggerimenti {#best-practices-limitations-tips}

* Il file CSV per l’importazione dei metadati delle risorse è in un formato molto specifico. Per risparmiare tempo e sforzi ed evitare errori non intenzionali, potete iniziare a creare il CSV utilizzando il formato di un file CSV esportato.
* Quando importate dei metadati utilizzando un file CSV, il formato di data richiesto è `YYYY-MM-DDThh:mm:ss.fff-00:00`. Se viene utilizzato un altro formato, i valori data non vengono impostati. I formati data del file CSV dei metadati esportati sono nel formato `YYYY-MM-DDThh:mm:ss-00:00`. Se desiderate importarlo, convertitelo nel formato accettabile aggiungendo il valore nanosecondi indicato da `fff`.
* Per importare i metadati negli spazi dei nomi personalizzati, registrate prima gli spazi dei nomi.
* Il selettore proprietà visualizza le proprietà utilizzate negli editor di schemi e nei moduli di ricerca. Il selettore proprietà non seleziona le proprietà dei metadati da una risorsa.

>[!MORELIKETHIS]
>
>* [Importazione ed esportazione di metadati in Experience Manager Assets](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/metadata-import-feature-video-use.html)

