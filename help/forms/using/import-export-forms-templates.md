---
title: Importazione ed esportazione di risorse in  AEM Forms
seo-title: Importazione ed esportazione di risorse in  AEM Forms
description: È possibile importare ed esportare moduli e modelli adattivi da e verso AEM istanze. In questo modo è possibile migrare i moduli o spostarli tra i diversi sistemi.
seo-description: È possibile importare ed esportare moduli e modelli adattivi da e verso AEM istanze. In questo modo è possibile migrare i moduli o spostarli tra i diversi sistemi.
uuid: 937daedd-56f3-4e02-b695-b194b494d9bf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 69210727-dde3-495a-87b7-2e8173e6b664
docset: aem65
translation-type: tm+mt
source-git-commit: 5035c9630b5e861f4386e1b5ab4f4ae7a8d26149
workflow-type: tm+mt
source-wordcount: '2548'
ht-degree: 1%

---


# Importazione ed esportazione di risorse in  AEM Forms{#importing-and-exporting-assets-to-aem-forms}

È possibile spostare moduli e risorse correlate, temi, dizionari di dati, frammenti di documento e lettere tra istanze AEM Forms  diverse. Tale spostamento è richiesto quando si migrano sistemi o si spostano moduli da un server di fase a un server di produzione. Per le risorse per le quali sono supportati il caricamento e l’importazione tramite l’interfaccia  di AEM Forms, si consiglia di usare l’interfaccia utente di Forms per l’esportazione o l’importazione. Non è consigliabile utilizzare AEM Package Manager per esportare o importare tali risorse.

>[!NOTE]
>
>* In Forms AEM 6.4, la struttura e i percorsi del repository crx sono cambiati. Se importate le risorse da una versione precedente a AEM 6.4 Forms e il modulo ha alcune dipendenze dalla struttura precedente, è necessario esportare manualmente le dipendenze. Per informazioni dettagliate sulle modifiche nella struttura e nei percorsi del repository, vedere [Ristrutturazione del repository in AEM](/help/sites-deploying/repository-restructuring.md).

>



## Scaricare o caricare risorse Forms e Documenti {#download-or-upload-forms-amp-documents-assets}

&#39;interfaccia utente di AEM Forms consente di esportare le risorse da un&#39;istanza AEM scaricandole come AEM pacchetto CRX o file binari. Potete quindi importare il AEM CRX-package scaricato o il file binario in un&#39;altra istanza AEM.

L&#39;esportazione e l&#39;importazione tramite &#39;interfaccia utente AEM Forms è supportata per tutte le risorse, ad eccezione dei modelli di modulo adattivo e dei criteri per il contenuto dei moduli adattivi. Pertanto, al momento dell&#39;esportazione di un modulo adattivo dall&#39; dell&#39;interfaccia utente di AEM Forms, il modello di modulo adattivo e i criteri di contenuto correlati non vengono esportati automaticamente come altre risorse correlate.

Per questi tipi di risorse, dovete usare AEM Package Manager per creare un pacchetto CRX sul server AEM di origine e installare il pacchetto sul server di destinazione. Per informazioni sulla creazione e l&#39;installazione di pacchetti, vedere [Utilizzo dei pacchetti](/help/sites-administering/package-manager.md).

### Scarica risorse Forms e Documenti {#download-forms-amp-documents-assets}

Per scaricare le risorse Forms e Documenti:

1. Effettuate l&#39;accesso all&#39;istanza AEM Forms .
1. Toccate  Experience Manager ![adobeexperience emanager](assets/adobeexperiencemanager.png) icona > navigazione ![bussola](assets/compass.png) icona> Forms > Forms &amp; Documents.
1. Selezionare le risorse dei moduli e toccare l&#39;icona **Scarica**.
1. In Scarica risorse, scegliete una delle seguenti opzioni e toccate **Scarica**.

   * **Scarica come pacchetto CRX:** utilizzate l&#39;opzione per scaricare e spostare tutte le risorse selezionate e le dipendenze correlate da un&#39;istanza di AEM Forms  a un&#39;altra. Consente di scaricare tutte le risorse e le cartelle come pacchetto crx. Tutte le risorse dei moduli, compresi i moduli creati in AEM (moduli adattivi, comunicazioni interattive e frammenti di moduli adattivi), set di moduli, modelli di moduli, documenti PDF e risorse (XSD, XFS, immagini), possono essere scaricate come pacchetti dallinterfaccia utente di AEM Forms.
Il vantaggio di scaricare come pacchetto le risorse è che vengono scaricate anche quelle usate dalla risorsa selezionata per il download. Ad esempio, se si dispone di un modulo adattivo che utilizza un modello di modulo, XSD e un&#39;immagine. Quando selezionate questo modulo adattivo e lo scaricate come pacchetto, il pacchetto scaricato contiene anche il modello di modulo, XSD e l&#39;immagine. Vengono scaricate anche tutte le proprietà di metadati (comprese le proprietà personalizzate) associate alla risorsa.

   * **Scaricate le risorse come file binari:** utilizzate l&#39;opzione per scaricare solo i modelli di modulo (XDP), gli PDF forms (PDF), il documento (PDF) e le risorse (immagini, schemi, fogli di stile). Potete modificare queste risorse con applicazioni esterne. Consente di scaricare come file .zip le risorse dei moduli che contengono file binari, come XSD, XDP, immagini, PDF e XDP.
Non è possibile scaricare moduli adattivi, comunicazioni interattive, frammenti di modulo adattivi, temi e set di moduli con l&#39;opzione **Scarica risorse come file binari**. Per scaricare queste risorse, utilizzate l&#39;opzione **Scarica come pacchetto CRX**.

   Le risorse selezionate vengono scaricate come archivio (file .zip).

   >[!NOTE]
   >
   >Sia AEM pacchetto che file binari vengono scaricati come archivio (file .zip). I modelli delle risorse non vengono scaricati insieme alle risorse. È necessario esportare i modelli di risorse separatamente.

### Caricare le risorse Forms e Documenti {#upload-forms-amp-documents-assets}

Per caricare le risorse Forms e Documenti:

>[!VIDEO](https://vimeo.com/)

1. Effettuate l&#39;accesso all&#39;istanza AEM Forms .
1. Toccate  Experience Manager ![adobeexperience emanager](assets/adobeexperiencemanager.png) icona > navigazione ![bussola](assets/compass.png) icona> Forms> Forms &amp; Documents.
1. Toccate **Crea** >**Caricamento file**. Viene visualizzata una finestra di dialogo per il caricamento di moduli o pacchetti.
1. Nella finestra di dialogo, individuate e selezionate il pacchetto o l&#39;archivio da importare. È inoltre possibile selezionare documenti PDF, file XSD, immagini, fogli di stile e moduli XDP. Toccate **Apri**. La cartella o il nome file selezionato non deve includere caratteri speciali.

   Nella finestra di dialogo, verificate i dettagli delle risorse caricate e toccate **Carica**.

   Se carichi una risorsa di modulo esistente, la risorsa viene aggiornata.

   >[!NOTE]
   >
   >Il caricamento di un pacchetto non sostituisce la gerarchia di cartelle esistente. Ad esempio, se disponete di un modulo adattivo denominato &quot;Training&quot; in corrispondenza della posizione /content/dam/formsanddocuments su un server. È possibile scaricare il modulo adattivo e caricarlo su un altro server. Il secondo server dispone inoltre di una cartella denominata &quot;Training&quot; nello stesso percorso /content/dam/formsanddocuments. Il caricamento non riesce.

## Download o caricamento di un tema {#downloading-or-uploading-a-theme}

Con  AEM Forms potete creare, scaricare o caricare i temi. Un tema viene creato come altre risorse come moduli, documenti e lettere. Potete creare un tema, scaricarlo e caricarlo in un&#39;istanza separata per riutilizzarlo. Per ulteriori informazioni sui temi, vedere [Temi in  AEM Forms](../../forms/using/themes.md).

### Download di un tema {#downloading-a-theme}

Potete esportare i temi in  AEM Forms da usare in altri progetti o istanze. AEM scaricare il tema come file zip, che potete caricare sull’istanza.

Per scaricare un tema:

1. Effettuate l&#39;accesso all&#39;istanza AEM Forms .
1. Toccate  Experience Manager ![adobeexperience emanager](assets/adobeexperiencemanager.png) icona > navigazione ![bussola](assets/compass.png) icona> Forms> Temi.
1. Selezionate il tema e toccate **Scarica**. Il tema viene scaricato come archivio (file .zip).

### Caricamento di un tema {#uploading-a-theme}

Potete usare i temi creati con i predefiniti di stile del progetto. Potete importare pacchetti di temi creati da altri utenti caricandoli nel progetto.

Per caricare un tema:

1. In  Experience Manager, passare a **Forms > Temi**.
1. Nella pagina Temi, fate clic su **Crea > Caricamento file**.
1. Nel prompt Caricamento file, individuate e selezionate un pacchetto di temi sul computer e fate clic su **Carica**.
Il tema caricato è disponibile nella pagina dei temi.

1. Effettuate l&#39;accesso all&#39;istanza AEM Forms .
1. Toccate  Experience Manager ![adobeexperience emanager](assets/adobeexperiencemanager.png) icona > navigazione ![bussola](assets/compass.png) icona> Forms> Temi.
1. fare clic su **Crea** > **Caricamento file**. Nel prompt Caricamento file, individuate e selezionate un pacchetto di temi sul computer e fate clic su **Carica**. Il tema viene caricato.

## Importazione ed esportazione di risorse in Gestione corrispondenza {#import-and-export-assets-in-correspondence-management}

Per condividere risorse, come dizionari di dati, lettere e frammenti di documento, tra due diverse implementazioni di Gestione corrispondenza, potete creare e condividere file .cmp. Un file .cmp può includere uno o più dizionari di dati, lettere, frammenti di documento e moduli.

### Esportare frammenti di documento, lettere e/o dizionari di dati {#export-document-fragments-letters-and-or-data-dictionaries}

1. Nelle pagine di lettere, frammenti di documento o del dizionario dati, toccate e selezionate le risorse da esportare in un singolo pacchetto, quindi toccate Coda per il download. Le risorse sono allineate per l’esportazione.
1. Come necessario, ripetere il passaggio precedente per aggiungere lettere, frammenti di documento e dizionari di dati.
1. Toccate **Scarica**.
1. Gestione corrispondenza visualizza la finestra di dialogo Scarica risorse con un elenco di risorse nell’elenco di esportazione.

   ![export](assets/export.png)

1. Per visualizzare le dipendenze esportate, toccate Risolvi. Oppure passate al passaggio successivo. Anche se non toccate resolve, le dipendenze vengono comunque esportate.
1. Per scaricare il file .cmp, toccate **OK**.
1. Gestione corrispondenza scarica un file .cmp sul computer.

   Il file .cmp include le risorse esportate. Potete condividere il file .cmp con altri utenti. Altri utenti possono importare il file .cmp in un server diverso per ottenere tutte le risorse nel nuovo server.

### Esportate tutte le risorse di Gestione corrispondenza come pacchetto {#export-all-the-correspondence-management-assets-as-a-package}

Utilizzate questa opzione per scaricare tutte le risorse Gestione corrispondenza e le dipendenze correlate come pacchetto da un&#39;istanza di modulo AEM.

Ad esempio, se Gestione corrispondenza ha una lettera che utilizza un&#39;immagine e un testo, il pacchetto scaricato contiene anche l&#39;immagine e il testo relativi alla lettera. Vengono scaricate anche tutte le proprietà di metadati (comprese le proprietà personalizzate) associate alla risorsa. Dopo aver scaricato il pacchetto (.cmp), potete [importare il pacchetto in un&#39;altra istanza  AEM Forms](../../forms/using/import-export-forms-templates.md#p-upload-forms-documents-assets-p).

Per scaricare come pacchetto tutte le risorse Gestione corrispondenza e le dipendenze correlate, effettua i seguenti passaggi:

1. Accedere  server AEM Forms come utente dei moduli.
1. Toccate **Adobe Experience Manager** nella barra di navigazione globale.
1. Toccate gli strumenti ( ![strumenti](assets/tools.png)), quindi toccate **Forms**.
1. Toccate **Esporta risorse di gestione della corrispondenza**.

   ![publish-cmp-assets-1](assets/publish-cmp-assets-1.png)

   &quot;Viene visualizzata la pagina Esporta tutte le risorse di gestione della corrispondenza, con le informazioni relative all’ultima volta che è stato tentato il processo di esportazione e un collegamento per scaricare l’ultimo pacchetto esportato correttamente.

   ![export-last-run-details](assets/export-last-run-details.png)

1. Toccate **Export** e, nel messaggio di conferma, toccate **OK**.

   Al termine di un processo batch, vengono aggiornati gli ultimi dettagli di esecuzione e il collegamento per scaricare il pacchetto. Questo include informazioni come il login dell&#39;amministratore e se il batch viene eseguito correttamente o con esito negativo. Le risorse vengono esportate in un pacchetto e viene visualizzato il collegamento Scarica pacchetto esportato.

   >[!NOTE]
   >
   >Il processo Esporta tutte le risorse non può essere annullato una volta avviato. Inoltre, mentre è in corso l’esportazione di tutte le operazioni, non create, eliminate, modificate o pubblicate risorse, né avviate il processo Pubblica tutte le risorse.a

1. Toccate il collegamento **Scarica pacchetto esportato** per scaricare il file del pacchetto.

   Per aggiungere le risorse del pacchetto a un&#39;altra istanza di Gestione corrispondenza, [importate il pacchetto in un&#39;istanza  AEM Forms](../../forms/using/import-export-forms-templates.md#p-upload-forms-documents-assets-p).

### Importa frammenti di documento, lettere e/o dizionari di dati in Gestione corrispondenza {#import-document-fragments-letters-and-or-data-dictionaries-into-correspondence-management}

Potete importare le risorse esportate in un file .cmp. Un file .cmp può contenere una o più lettere, dizionari di dati, frammenti di documento e risorse dipendenti.

>[!NOTE]
>
>Durante l&#39;importazione di vecchie risorse di Gestione della corrispondenza per la migrazione, effettuate l&#39;accesso con un account amministratore. Per ulteriori informazioni sulla migrazione delle risorse di gestione della corrispondenza precedente, vedere [Migra le risorse di gestione della corrispondenza AEM moduli 6.1](/help/forms/using/migration-utility.md).

1. Nella pagina del dizionario dati, delle lettere o dei frammenti di documento, toccare **Crea > Caricamento file** e selezionare il file .cmp.
1. Gestione corrispondenza visualizza la finestra di dialogo Importa risorse con l’elenco delle risorse importate. Toccate **Importa**.

   Dopo aver importato le risorse, vengono aggiornate le seguenti proprietà delle risorse, mentre le altre rimangono invariate:

   * Autore: Visualizza l’ID dell’utente che ha importato la risorsa nel server
   * Modificato: L’ora in cui la risorsa è stata importata nel server

   >[!NOTE]
   >
   >Per poter caricare gli XDP (come parte del file cmp o in altro modo), è necessario far parte del gruppo di utenti per l&#39;alimentazione dei moduli. Per i diritti di accesso, contattate l’amministratore.

## Esportare un&#39;applicazione di workflow {#export-a-workflow-application}

Potete usare AEM gestore pacchetti per esportare le applicazioni dei flussi di lavoro. La procedura è la seguente:

1. Aprite  gestione pacchetti AEM Forms. L&#39;URL del gestore pacchetti è https://&lt;server>:&lt;porta>/crx/packmgr.
1. Fare clic su **[!UICONTROL Crea pacchetto]**. Viene visualizzata la finestra di dialogo **[!UICONTROL Nuovo pacchetto]**.
1. Specificate nome, versione e gruppo per il pacchetto. Fai clic su **[!UICONTROL OK]**.
1. Fare clic su **[!UICONTROL Modifica]** e aprire la scheda **[!UICONTROL Filtri]**. Fare clic su **[!UICONTROL Aggiungi filtro]**. Specificate il percorso dell’applicazione del flusso di lavoro. Ad esempio, /etc/fd/dashboard/startpoints/homemortgage. Fare clic su **[!UICONTROL Aggiungi regola]**.

1. Apri la scheda **[!UICONTROL Avanzate.]** Selezionare **[!UICONTROL Merge]** o **[!UICONTROL Sovrascrivi]** nel campo Gestione ACL. Fai clic su **[!UICONTROL Salva]**.
1. Fate clic su **[!UICONTROL Build]** per creare il pacchetto.

   Dopo aver creato il pacchetto, potete scaricarlo e importarlo nell&#39;altro server. L&#39;applicazione del flusso di lavoro viene visualizzata sul server in cui viene caricato il pacchetto.

   >[!NOTE]
   >
   >Affinché l’applicazione del flusso di lavoro funzioni correttamente, è inoltre possibile esportare il modulo adattivo e il modello di flusso di lavoro corrispondenti con l’applicazione di lavoro.

## Cartelle e organizzazione delle risorse {#folders-and-organizing-assets}

&#39;interfaccia utente di AEM Forms utilizza le cartelle per disporre le risorse. Tali cartelle vengono utilizzate per disporre le risorse create all’interno ’interfaccia utente di AEM Forms. Potete rinominare, creare sottocartelle e archiviare risorse e documenti in queste cartelle. L’organizzazione di documenti e risorse in una cartella consente di raggruppare i file per facilitarne la gestione. Potete selezionare una cartella e scegliere se scaricarla o eliminarla.

Per creare una cartella, effettuate le seguenti operazioni:

### Crea una cartella . {#create-a-folder}

1. Accedete all&#39;interfaccia utente  AEM Forms all&#39;indirizzo `https://<server>:<port>/aem/forms.html`.
1. Andate alla posizione in cui desiderate creare una cartella.
1. Toccate Crea > Cartella.
1. Inserite i seguenti dettagli:

   * **Titolo:Nome** visualizzato per la cartella
   * **Nome:** *(obbligatorio)* Nome del nodo in cui si desidera memorizzare la cartella nell’archivio

   >[!NOTE]
   >
   >Per impostazione predefinita, il valore del campo nome viene compilato automaticamente dal titolo. Il nome può contenere solo caratteri alfanumerici, oppure caratteri speciali trattino (-) e carattere di sottolineatura (_). Eventuali altri caratteri speciali immessi nel titolo vengono sostituiti automaticamente con un trattino e viene richiesto di confermare il nuovo nome. Potete scegliere di continuare con il nome suggerito o di modificarlo ulteriormente.

1. Una nuova cartella con il titolo definito viene visualizzata nella posizione corrente nell’elenco delle risorse.

   Se esiste una cartella con il nome specificato, l&#39;invio non riesce con un errore. Per visualizzare il messaggio di errore, passare il puntatore del mouse sull&#39;icona di errore ![aem6forms_error_alert](assets/aem6forms_error_alert.png) visualizzata accanto al campo del nome.

   Potete toccare la cartella appena creata per entrare nella cartella e creare risorse o cartelle all’interno della cartella. Inoltre, potete selezionare una cartella e scegliere di accodarla per il download, eliminarla o modificarne il nome.

   ![editdelete edownloadafolder](assets/editdeletedownloadafolder.png)

### Creare copie di una o più risorse o lettere {#create-copies-of-one-or-more-assets-or-letters}

Potete usare risorse e lettere esistenti per creare rapidamente risorse e lettere con proprietà, contenuto e risorse ereditate simili. È possibile copiare e incollare dizionari di dati, frammenti di documento e lettere.

Per creare copie delle risorse e delle lettere, effettuate le seguenti operazioni:

1. Nella pagina Risorse o Lettere, seleziona una o più risorse/lettere. L’interfaccia utente presenta l’icona Copia.
1. Tocca Copia. Nell’interfaccia utente viene visualizzata l’icona Incolla. Potete anche scegliere di andare o navigare all’interno di una cartella prima di incollare. Cartelle diverse possono contenere risorse con gli stessi nomi. Per ulteriori informazioni sulle cartelle, consultate [Cartelle e organizzazione delle risorse](#folders-and-organizing-assets).
1. Toccate Incolla. Viene visualizzata la finestra di dialogo Incolla. Il sistema genera automaticamente nomi e titoli alle nuove copie di risorse/lettere, ma è possibile modificare titoli e nomi delle risorse/lettere.

   Se copiate e incollate le risorse/lettere nello stesso punto, al nome esistente della risorsa/lettera viene aggiunto il suffisso &quot;-CopyXX&quot;. Se non esiste alcun titolo per la risorsa o la lettera copiata, il campo del titolo generato automaticamente rimane vuoto.

1. Se necessario, modificate il Titolo e il Nome con cui desiderate salvare la copia della risorsa o della lettera.
1. Toccate Incolla. Vengono create nuove copie delle risorse copiate.

## Ricerca {#search-forms}

&#39;interfaccia utente di AEM Forms consente di effettuare ricerche nel contenuto. Utilizzando la barra superiore, potete toccare Cerca **[A]** per cercare nel contenuto risorse quali risorse e documenti.

Quando cercate le risorse,  AEM Forms visualizza il pannello laterale. Per richiamare il pannello laterale, potete anche toccare ![assets-browser-content-only](assets/assets-browser-content-only.png) > Filter **[B]**. Usando i vari filtri nel pannello laterale, potete restringere la ricerca. Il pannello laterale consente inoltre di salvare le ricerche.

![search_topbar](assets/search_topbar.png)

**A.** Search  **B.** Filter

![Pannello laterale - Filtri](assets/search_sidepanel.png)

Pannello laterale - Filtri

Nel pannello laterale potete usare quanto segue per limitare i risultati della ricerca:

* Directory di ricerca
* Tag
* Criteri di ricerca, ad esempio Data di modifica, Stato pubblicazione, Stato LiveCopy.

Il pannello laterale consente inoltre di salvare le impostazioni di ricerca con i nomi desiderati.

Per ulteriori informazioni e istruzioni sull&#39;uso di ricerca, filtri, ricerca salvata e pannello laterale, vedere [Ricerca](/help/sites-authoring/search.md).
