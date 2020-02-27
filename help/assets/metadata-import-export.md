---
title: Importare ed esportare in massa i metadati delle risorse
description: Importare ed esportare in massa i metadati delle risorse
contentOwner: AG
translation-type: tm+mt
source-git-commit: 44daaa61f7328e79fd4e11a503b0eef3ff9ffb56

---


# Importare ed esportare in massa i metadati delle risorse {#import-and-export-asset-metadata-in-bulk}

Risorse AEM consente di importare i metadati delle risorse in blocco mediante un file CSV. Potete eseguire aggiornamenti in blocco per le risorse caricate di recente o per le risorse esistenti importando un file CSV. Potete anche assimilare i metadati delle risorse in massa da sistemi di terze parti in formato CSV.

## Importare i metadati {#import-metadata}

L&#39;importazione dei metadati è asincrona e non ostacola le prestazioni del sistema. L’aggiornamento simultaneo dei metadati per più risorse può richiedere molte risorse a causa dell’attività di reinserimento XMP se è selezionato il flag del flusso di lavoro. Pianificate tale importazione durante l&#39;utilizzo di un server snello in modo da non influenzare le prestazioni di altri utenti.

>[!NOTE]
>
>Per importare i metadati negli spazi dei nomi personalizzati, registrate prima gli spazi dei nomi.

1. Passa all’interfaccia utente Risorse e tocca o fai clic su **[!UICONTROL Crea]** dalla barra degli strumenti.
1. Dal menu, selezionate **[!UICONTROL Metadati]**.
1. Nella pagina **[!UICONTROL Importazione metadati]**, tocca o fai clic su **[!UICONTROL Seleziona un file]**. Scegli il file CSV con i metadati.
1. Specificate i seguenti parametri:

   | Parametri di importazione metadati | Descrizione |
   |:---|:---|
   | [!UICONTROL Dimensione batch] | Numero di risorse in un batch per cui importare i metadati. Il valore predefinito è 50. Il valore massimo è 100. |
   | [!UICONTROL Separatore di campi] | Il valore predefinito è `,` (una virgola). È possibile specificare qualsiasi altro carattere. |
   | [!UICONTROL Delimitatore valori multipli] | Separatore per i valori dei metadati. Il valore predefinito è `|`. |
   | [!UICONTROL Avvia flussi di lavoro] | False per impostazione predefinita. Quando è impostata su `true` e le impostazioni predefinite di Launcher sono attive per il flusso di lavoro di scrittura dei metadati DAM (che scrive i metadati nei dati XMP binari). L&#39;attivazione dei flussi di lavoro di avvio rallenta il sistema. |
   | [!UICONTROL Nome colonna percorso risorsa] | Definisce il nome della colonna per il file CSV con le risorse. |

1. Toccate o fate clic su **[!UICONTROL Importa]** dalla barra degli strumenti. Una volta importati i metadati, viene inviata una notifica alla inbox Notifica. Andate alla pagina delle proprietà della risorsa e verificate se i valori dei metadati sono stati importati correttamente per le risorse.

## Esporta metadati {#export-metadata}

Potete esportare i metadati per più risorse in formato CSV. I metadati vengono esportati in modo asincrono e non influiscono sulle prestazioni del sistema. Per esportare i metadati, AEM attraversa le proprietà del nodo della risorsa `jcr:content/metadata` e dei relativi nodi secondari ed esporta le proprietà dei metadati in un file CSV.

Alcuni esempi di utilizzo per l’esportazione di metadati in massa sono:

* Importate i metadati in un sistema di terze parti durante la migrazione delle risorse.
* Condividete i metadati delle risorse con un team di progetto più ampio.
* Verifica o verifica la conformità dei metadati.
* Esternalizzare i metadati per una localizzazione separata.

1. Selezionate la cartella di risorse che contiene le risorse per le quali desiderate esportare i metadati. Dalla barra degli strumenti, selezionate **[!UICONTROL Esporta metadati]**.
1. Nella finestra di dialogo Esportazione metadati, specificate un nome per il file CSV. Per esportare i metadati delle risorse nelle sottocartelle, selezionate **[!UICONTROL Includi risorse nelle sottocartelle]**.

   ![Interfaccia e opzioni per esportare i metadati di tutte le risorse di una](assets/export_metadata_page.png "cartellaInterfaccia e opzioni per esportare i metadati di tutte le risorse di una cartella")

1. Selezionate le opzioni desiderate. Specificare un nome di file e, se necessario, una data.

1. Nel campo **[!UICONTROL Proprietà da esportare]** , specificate se esportare tutte le proprietà o solo proprietà specifiche. Se scegliete le proprietà selettive da esportare, aggiungete le proprietà desiderate.

1. Dalla barra degli strumenti, toccate o fate clic su **[!UICONTROL Esporta]**. Viene visualizzato un messaggio di conferma dell’esportazione dei metadati. Chiudi il messaggio.
1. Apri la notifica della casella in entrata del processo di esportazione. Seleziona il processo e fai clic su **[!UICONTROL Apri]** nella barra degli strumenti. Per scaricare il file CSV con i metadati, tocca o fai clic su **[!UICONTROL Scarica CSV]** nella barra degli strumenti. Fai clic su **[!UICONTROL Chiudi]**.

   ![Finestra di dialogo per scaricare il file CSV contenente i metadati esportati in massa](assets/csv_download.png)

   *Figura: Finestra di dialogo per scaricare il file CSV contenente i metadati esportati in massa*

>[!MORELIKETHIS]
>
>* [Importazione ed esportazione di metadati in AEM Assets](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/metadata-import-feature-video-use.html)

