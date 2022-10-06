---
title: Gestire le immagini della firma dell’agente
seo-title: Manage agent signature images
description: Dopo aver creato un modello di lettera, è possibile utilizzarlo per creare la corrispondenza in AEM Forms gestendo dati, contenuto e allegati.
seo-description: After you have created a letter template, you can use it to create correspondence in AEM Forms by managing data, content, and attachments.
uuid: 48b2697e-6065-4e23-9aa8-333e7b11ede1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: a81cdd53-f0fb-4ac5-b2ec-c19aeee7186e
docset: aem65
feature: Correspondence Management
exl-id: f044ed75-bb72-4be1-aef6-2fb3b2a2697b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---

# Gestire le immagini della firma dell’agente{#manage-agent-signature-images}

## Panoramica {#overview}

In Gestione corrispondenza è possibile utilizzare un’immagine per eseguire il rendering della firma dell’agente in lettere. Dopo aver impostato l’immagine della firma dell’agente durante la creazione di una lettera, è possibile eseguire il rendering dell’immagine della firma dell’agente nella lettera come firma dell’agente mittente.

Il DDE agentSignatureImage è un DDE calcolato che rappresenta l&#39;immagine della firma dell&#39;agente. L&#39;espressione per questo DDE calcolato utilizza una nuova funzione personalizzata esposta dal blocco predefinito di Expression Manager. Questa funzione personalizzata prende agentID e agentFolder come parametri di input e recupera il contenuto dell’immagine in base a questi parametri. Il dizionario dati di sistema SystemContext consente alle lettere in Gestione corrispondenza di accedere alle informazioni nel contesto di sistema corrente. Il contesto del sistema include informazioni sull&#39;utente attualmente connesso e sui parametri di configurazione attivi.

È possibile aggiungere immagini nella cartella cmuserroot. In [Proprietà di configurazione della gestione della corrispondenza](/help/forms/using/cm-configuration-properties.md), utilizzando la proprietà User Root di CM è possibile modificare la cartella da cui viene prelevata l’immagine della firma dell’agente.

Il valore di agentFolder DDE viene ricavato dal parametro di configurazione CMUserRoot per le proprietà di configurazione di Gestione corrispondenza. Per impostazione predefinita, questo parametro di configurazione punta a/content/cmUserRoot nell’archivio CRX. Puoi modificare il valore della configurazione CMUserRoot nelle Proprietà di configurazione.
È inoltre possibile ignorare la funzione personalizzata predefinita per definire una logica personalizzata per il recupero dell’immagine della firma utente.

## Aggiunta dell’immagine della firma dell’agente {#adding-agent-signature-image}

1. Assicurarsi che l&#39;immagine della firma dell&#39;agente abbia lo stesso nome del nome utente AEM dell&#39;utente. (Estensione non necessaria per il nome del file immagine.)
1. In CRX, crea una cartella denominata `cmUserRoot` nella cartella del contenuto.

   1. Passa a `https://'[server]:[port]'/crx/de`. Se necessario, accedi come Amministratore.

   1. Fai clic con il pulsante destro del mouse sul pulsante **content** e seleziona **Crea** > **Crea cartella**.

      ![Crea cartella](assets/1_createnode_cmuserroot.png)

   1. Nella finestra di dialogo Crea cartella, immetti il nome della cartella come `cmUserRoot`. Fai clic su **Salva tutto**.

      >[!NOTE]
      >
      >cmUserRoot è la posizione predefinita in cui AEM cerca l’immagine della firma dell’agente. È tuttavia possibile modificarla modificando la proprietà Directory principale utente di CM nel [Proprietà di configurazione della gestione della corrispondenza](/help/forms/using/cm-configuration-properties.md).

1. In Content Explorer, passa alla cartella cmUserRoot e aggiungi l’immagine della firma dell’agente al suo interno.

   1. Passa a `https://'[server]:[port]'/crx/explorer/index.jsp`. Accedi come amministratore, se necessario.
   1. Fai clic su **Esplora contenuti**. Verrà visualizzata una nuova finestra di Esplora contenuti.
   1. In Content Explorer, accedi alla cartella cmUserRoot e selezionala. Fai clic con il pulsante destro del mouse sul pulsante **cmUserRoot** e seleziona **Nuovo nodo**.

      ![Nuovo nodo in cmUserRoot](assets/2_cmuserroot_newnode.png)

      Apporta le seguenti voci nella riga per il nuovo nodo, quindi fai clic sul segno di spunta verde.

      **Nome:** JohnDoe (o il nome del file di firma dell&#39;agente)

      **Tipo:** nt:file

      Sotto la `cmUserRoot` una nuova cartella denominata `JohnDoe` (o il nome specificato nel passaggio precedente) viene creato.

   1. Fai clic sulla nuova cartella creata (qui `JohnDoe`). In Esplora contenuti il contenuto della cartella viene visualizzato in grigio.

   1. Fai doppio clic sul pulsante **jcr:content** imposta il tipo come **nt:resource**, quindi fai clic sul segno di spunta verde per salvare la voce.

      Se la proprietà non è presente, crea innanzitutto una proprietà denominata jcr:content.

      ![jcr:content, proprietà](assets/3_jcrcontentntresource.png)

      Tra le sottoproprietà di jcr:content c&#39;è jcr:data, che è oscurato. Fai doppio clic su jcr:data. La proprietà diventa modificabile e nella voce viene visualizzato il pulsante Scegli file . Fai clic su **Scegli file** e selezionare il file immagine da utilizzare come logo. Il file immagine non deve avere un&#39;estensione.

      ![Dati JCR](assets/5_jcrdata.png)
   Fai clic su **Salva tutto**.

1. Per eseguire il rendering dell&#39;immagine firma, verificare che nella lettera sia presente un campo immagine in basso a sinistra (o in un altro punto appropriato del layout in cui si desidera eseguire il rendering della firma).
1. Durante la creazione della corrispondenza, nella scheda Dati selezionare un campo immagine per l’immagine della firma seguendo i seguenti passaggi:

   1. Selezionare Sistema dal menu a comparsa Tipo di collegamento nel riquadro a destra.

   1. Seleziona l&#39;agentSignatureImage DDE dall&#39;elenco nel pannello Elemento dati per SystemContext DD.

   1. Salva la lettera.

1. Durante il rendering della lettera, è possibile visualizzare la firma nell’anteprima della lettera nel campo immagine in base al layout.

   ![Immagine della firma dell’agente nella lettera](assets/letterwithsignature.png)
