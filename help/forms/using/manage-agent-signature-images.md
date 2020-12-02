---
title: Gestire le immagini di firma dell'agente
seo-title: Gestire le immagini di firma dell'agente
description: Dopo aver creato un modello di lettera, è possibile utilizzarlo per creare la corrispondenza in  AEM Forms gestendo dati, contenuto e allegati.
seo-description: Dopo aver creato un modello di lettera, è possibile utilizzarlo per creare la corrispondenza in  AEM Forms gestendo dati, contenuto e allegati.
uuid: 48b2697e-6065-4e23-9aa8-333e7b11ede1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: a81cdd53-f0fb-4ac5-b2ec-c19aeee7186e
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 0%

---


# Gestione immagini firma agente{#manage-agent-signature-images}

## Panoramica {#overview}

In Gestione corrispondenza è possibile utilizzare un&#39;immagine per rappresentare la firma dell&#39;agente in lettere. Dopo aver impostato l&#39;immagine della firma dell&#39;agente, durante la creazione di una lettera è possibile renderizzare l&#39;immagine della firma dell&#39;agente nella lettera come firma dell&#39;agente mittente.

Il DDE agentSignatureImage è un DDE calcolato che rappresenta l&#39;immagine della firma dell&#39;agente. L&#39;espressione per questo DDE calcolato utilizza una nuova funzione personalizzata esposta dal blocco predefinito di Expression Manager. Questa funzione personalizzata prende agentID e agentFolder come parametri di input e raccoglie il contenuto dell’immagine in base a tali parametri. Il dizionario dati di sistema SystemContext fornisce alle lettere in Gestione corrispondenza l&#39;accesso alle informazioni nel contesto del sistema corrente. Il contesto del sistema include informazioni sui parametri di configurazione attiva e utente attualmente connessi.

Potete aggiungere delle immagini nella cartella cmuserroot. In [Proprietà di configurazione della gestione della corrispondenza](/help/forms/using/cm-configuration-properties.md), utilizzando la proprietà radice utente di CM è possibile modificare la cartella da cui viene prelevata l&#39;immagine della firma dell&#39;agente.

Il valore di agentFolder DDE viene ricavato dal parametro di configurazione CMUserRoot per le proprietà di configurazione della gestione della corrispondenza. Per impostazione predefinita, questo parametro di configurazione punta a/content/cmUserRoot nell’archivio CRX. È possibile modificare il valore della configurazione CMUserRoot nelle proprietà di configurazione.
È inoltre possibile ignorare la funzione personalizzata predefinita per definire la propria logica per il recupero dell&#39;immagine della firma utente.

## Aggiunta dell&#39;immagine firma agente {#adding-agent-signature-image}

1. Assicurarsi che l&#39;immagine firma agente abbia lo stesso nome del nome utente AEM dell&#39;utente. L’estensione non è necessaria per il nome del file immagine.
1. In CRX, create una cartella denominata `cmUserRoot` nella cartella del contenuto.

   1. Passa a `https://'[server]:[port]'/crx/de`. Se necessario, effettuate l’accesso come amministratore.

   1. Fare clic con il pulsante destro del mouse sulla cartella **content** e selezionare **Create** > **Create Folder**.

      ![Crea cartella](assets/1_createnode_cmuserroot.png)

   1. Nella finestra di dialogo Crea cartella, immettete il nome della cartella come `cmUserRoot`. Fare clic su **Salva tutto**.

      >[!NOTE]
      >
      >cmUserRoot è il percorso predefinito in cui AEM cercare l&#39;immagine della firma dell&#39;agente. È tuttavia possibile modificarlo modificando la proprietà radice utente di CM nelle proprietà di configurazione [Gestione corrispondenza](/help/forms/using/cm-configuration-properties.md).

1. In Content Explorer, andate alla cartella cmUserRoot e aggiungete l&#39;immagine della firma dell&#39;agente al suo interno.

   1. Passa a `https://'[server]:[port]'/crx/explorer/index.jsp`. Effettuate l&#39;accesso come amministratore, se necessario.
   1. Fare clic su **Content Explorer**. Content Explorer si apre in una nuova finestra.
   1. In Esplora contenuti, andate alla cartella cmUserRoot e selezionatela. Fare clic con il pulsante destro del mouse sulla cartella **cmUserRoot** e selezionare **Nuovo nodo**.

      ![Nuovo nodo in cmUserRoot](assets/2_cmuserroot_newnode.png)

      Immettere le seguenti voci nella riga per il nuovo nodo, quindi fare clic sul segno di spunta verde.

      **Nome:** JohnDoe (o il nome del file di firma dell&#39;agente)

      **Tipo:** nt:file

      Sotto la cartella `cmUserRoot` viene creata una nuova cartella denominata `JohnDoe` (o il nome specificato nel passaggio precedente).

   1. Fate clic sulla nuova cartella creata (qui `JohnDoe`). In Content Explorer il contenuto della cartella viene visualizzato in modo attenuato.

   1. Fare doppio clic sulla proprietà **jcr:content**, impostarne il tipo come **nt:resource**, quindi fare clic sul segno di spunta verde per salvare la voce.

      Se la proprietà non è presente, create prima una proprietà con nome jcr:content.

      ![jcr:proprietà content](assets/3_jcrcontentntresource.png)

      Tra le proprietà secondarie di jcr:content c&#39;è jcr:data, che è attenuato. Fate doppio clic su jcr:data. La proprietà diventa modificabile e nella voce viene visualizzato il pulsante Scegli file. Fare clic su **Scegli file** e selezionare il file immagine da utilizzare come logo. Il file immagine non deve avere un&#39;estensione.

      ![Dati JCR](assets/5_jcrdata.png)
   Fare clic su **Salva tutto**.

1. Verificare che il layout XDP\layout utilizzato nella lettera contenga un campo immagine in basso a sinistra (o in un&#39;altra posizione appropriata nel layout in cui si desidera eseguire il rendering della firma) per eseguire il rendering dell&#39;immagine della firma.
1. Durante la creazione della corrispondenza, nella scheda Dati selezionare un campo immagine per l&#39;immagine della firma utilizzando la procedura seguente:

   1. Selezionare Sistema dal menu a comparsa Tipo di collegamento nel riquadro a destra.

   1. Selezionare agentSignatureImage DDE dall&#39;elenco nel pannello Data Element per SystemContext DD.

   1. Salva la lettera.

1. Durante il rendering della lettera, è possibile visualizzare la firma nell’anteprima della lettera nel campo immagine in base al layout.

   ![Immagine firma agente nella lettera](assets/letterwithsignature.png)

