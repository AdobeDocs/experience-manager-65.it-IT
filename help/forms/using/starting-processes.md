---
title: Avvio dei processi
seo-title: Avvio dei processi
description: 'Come utilizzare l''area di lavoro di LiveCycle  AEM Forms: selezionare i processi, aggiungere note e allegati, salvare le copie delle bozze e aggiungere ai preferiti.'
seo-description: 'Come utilizzare l''area di lavoro di LiveCycle  AEM Forms: selezionare i processi, aggiungere note e allegati, salvare le copie delle bozze e aggiungere ai preferiti.'
uuid: a61da785-25b4-4482-bd72-02e250d35dc7
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c9d3f369-3744-41d5-b340-390ab7e03f36
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '1364'
ht-degree: 0%

---


# Avvio dei processi {#starting-processes}

&#39;area di lavoro di AEM Forms organizza i processi in base alle categorie configurate dall&#39;amministratore o dal progettista di processi. È inoltre possibile inserire nella categoria Preferiti i processi utilizzati frequentemente, in modo da poterli trovare rapidamente.

Quando si avvia un processo, potrebbe essere necessario compilare un modulo per avviare un processo aziendale che  controlli del flusso di lavoro AEM Forms. Se un modulo utilizza l&#39;opzione Prepara processo dati, alcune informazioni possono essere precompilate in un modulo vuoto quando viene avviato un nuovo processo.

Ad esempio, si desidera acquistare un nuovo monitor per computer e quindi avviare un processo denominato *Ordine di acquisto*. Quando si avvia il processo, viene aperto un modulo che richiede informazioni dettagliate sull&#39;elemento da ordinare. Il nome, il numero del dipendente e il nome del manager possono già essere precompilati nel modulo. Quando inviate la richiesta, viene avviato un processo aziendale. In base alla definizione del processo, il server invia automaticamente la richiesta al manager. L&#39;attività inizia a comparire nell&#39;elenco A-do del manager. Quando il manager approva la richiesta, il flusso di lavoro dei moduli indirizza la richiesta al reparto acquisti e invia una notifica e-mail.

## Selezione dei processi da avviare {#selecting-processes-to-start}

Potete selezionare un processo per avviarlo o visualizzare ulteriori informazioni.

Quando si seleziona un processo da avviare, potrebbe essere necessario compilare un modulo associato a tale processo. L&#39;invio del modulo avvia il processo.

Sono supportati Forms in diversi tipi di formati di file, inclusi  file Adobe PDF, HTML e SWF. Un modulo può avere l&#39;aspetto di un modulo tradizionale stampabile o basato su Web oppure può essere di aiuto tramite una serie di pannelli in stile procedura guidata per raccogliere informazioni.

Se il modulo e la procedura lo consentono, è anche possibile salvare il modulo offline, compilarlo e quindi inviarlo per completare l&#39;attività. Quando il modulo viene inviato, il client di posta elettronica viene avviato con l&#39;indirizzo e-mail del server appropriato, se è configurato il punto finale dell&#39;e-mail. È quindi possibile inviare il modulo compilato al server tramite e-mail.

Quando si seleziona un processo, vengono visualizzate le schede Modulo e Dettagli. Se la procedura consente di aggiungere note o allegati, vengono visualizzate anche le schede Allegati e Note. Se avete anche configurato l’URL di riepilogo con il processo, viene visualizzata anche la scheda Riepilogo. Nella scheda Forms viene visualizzato il modulo associato, mentre nella scheda Dettagli vengono visualizzate informazioni sull&#39;attività corrente e sul processo di cui fa parte.

### Avvio di un processo aziendale {#start-a-business-process}

1. Nella pagina Avvia processo, selezionate una categoria nell’elenco a sinistra. Tutti i processi a cui hai accesso nella categoria vengono visualizzati a destra.

   >[!NOTE]
   >
   >Se il riquadro Categorie è compresso, fare clic su &quot;Open Categories&quot; (Apri categorie), nell&#39;area in alto a sinistra dell&#39;area di lavoro AEM Forms , per aprire il riquadro.

1. Selezionate un processo facendo clic su un’attività. Il modulo associato al processo si apre nella scheda Modulo.

   Ogni modulo in un processo ha un URL univoco. Potete utilizzare l&#39;URL univoco per avviare direttamente l&#39;area di lavoro HTML con il processo e il modulo specifici. Il formato dell&#39;URL è https://&lt;server>:&lt;porta>/lc/libs/ws/index.html#/startprocess/&lt;ApplicationName>%2F&lt;ProcessName>. La stringa &lt;ApplicationName>%2F&lt;ProcessName> è sempre con codifica URL. Un URL di esempio è http://localhost:8080/lc/libs/ws/index.html#/startprocess/MyApplication%2FNewProcess. La stringa ApplicationName%2FProcessName nell&#39;esempio è codificata da un URL.

1. Compila il modulo secondo le istruzioni fornite. Se necessario, fare clic su **Ingrandisci** per aumentare l&#39;area visibile del modulo.
1. Se la scheda Allegati è disponibile, aggiungere gli allegati come necessario.
1. Se la scheda Note è disponibile, fornite le note necessarie.
1. Effettuare una delle seguenti operazioni:

   * Se il modulo dispone di un pulsante Invia, fare clic sul pulsante Invia.
   * Fare clic su Completa sotto il modulo, se il modulo non dispone di un pulsante Invia.

   Process Management avvia il processo e indirizza il modulo agli elenchi A-do delle persone appropriate che devono completare l&#39;attività successiva nel processo.

   Se è necessario chiudere un modulo prima di inviarlo e senza perdere i dati immessi, salvare una bozza e completarla successivamente, se il processo lo consente. Se il modulo e la procedura lo consentono, è possibile fare clic su **Offline** e successivamente inviarlo da  Adobe® Reader® o  Adobe®  Acrobat® Professional o  Acrobat Standard.

   >[!NOTE]
   >
   >L&#39;opzione offline è disponibile solo per i PDF forms.

## Aggiunta di note e allegati {#adding-notes-and-attachments}

È possibile aggiungere note e file allegati a un processo, se il processo lo consente. Potete fornire autorizzazioni ad altri utenti che partecipano al processo per visualizzare, aggiornare ed eliminare le note o gli allegati.

### Aggiungere una nota {#add-a-note}

Potete aggiungere più note, modificare le note scritte ed eliminarle. A ciascuna nota sono associati un titolo, una descrizione e un&#39;autorizzazione di accesso. Potete impostare una delle seguenti autorizzazioni di accesso su una nota:

* Sola lettura (autorizzazione predefinita)
* Lettura/Modifica/Elimina
* Lettura/Modifica
* Lettura/eliminazione
* Nessun accesso

1. Aprite un&#39;attività e fate clic sulla scheda **Note**, se il processo lo consente.
1. Digitare un titolo per la nota nella casella **Titolo** e digitare il testo della nota nella casella **Nota**.
1. Selezionate il livello **Autorizzazioni** per la nota relativa agli altri utenti che partecipano al processo.
1. Fai clic su **OK**. Un file di testo che contiene la nota viene allegato al modulo. Potete aggiornare una nota facendo clic su di essa e modificando direttamente il testo. Per eliminare una nota, fare clic sul pulsante **Elimina** ![Immagine di un cestino](assets/icondelete.png) accanto alla nota.

### Aggiungere un allegato {#add-an-attachment}

È inoltre possibile aggiungere commenti sull&#39;allegato. È possibile impostare una delle seguenti autorizzazioni di accesso su un allegato:

* Sola lettura (autorizzazione predefinita)
* Lettura/Modifica/Elimina
* Lettura/Modifica
* Lettura/eliminazione
* Nessun accesso

1. Fare clic sulla scheda **Allegati** e selezionare **Allegati**.
1. Fare clic su **Sfoglia** per selezionare il file da allegare.
1. Selezionare il livello **Autorizzazioni** per l&#39;allegato per gli altri utenti che partecipano al processo. Se si seleziona **Leggi**, altri utenti possono salvare il file localmente. Se si seleziona una delle autorizzazioni di modifica, altri utenti possono caricare un nuovo file per sostituire l&#39;allegato.
1. Fai clic su **OK**. Il file è allegato al modulo. Per eliminare un file, fare clic sul pulsante **Elimina** ![Immagine di un cestino](assets/icondelete.png) accanto all&#39;allegato.

## Salvataggio delle copie bozza dei moduli {#saving-draft-copies-of-forms}

Se è necessario completare e inviare un modulo in un secondo momento, è possibile salvare una bozza di copia del modulo in modo da non perdere il lavoro esistente. Le copie bozza vengono aggiunte alla categoria Bozze nella pagina Da fare.

Dopo aver riaperto e inviato una bozza di modulo, la bozza viene rimossa dalla categoria Bozze.

Inoltre, potete configurare l’area di lavoro in modo da salvare automaticamente le informazioni immesse da un utente come bozza. Per ulteriori informazioni, vedere [Gestione delle preferenze](/help/forms/using/getting-started-livecycle-html-workspace.md).

>[!NOTE]
>
>Il pulsante Salva non è disponibile per alcuni moduli, a seconda del processo a cui è associato.

### Salva una bozza di copia {#save-a-draft-copy}

1. Fare clic su **Salva** nell&#39;angolo inferiore sinistro di una scheda. Il modulo viene aggiunto alla categoria Bozze nella pagina Da fare. Tutte le modifiche apportate al modulo vengono salvate.

### Riaprire una copia bozza {#reopen-a-draft-copy}

1. Nella pagina Da fare, selezionare la coda **Bozze** e fare clic sulla copia bozza del modulo.

   Se il modulo contiene una serie di pannelli, potrebbe essere necessario passare al pannello in cui è terminata l’ultima sessione.

## Aggiunta di processi alla categoria Preferiti {#adding-processes-to-the-favorites-category}

È possibile aggiungere qualsiasi processo alla categoria Preferiti. Impostando i preferiti, potete raggruppare tutti i processi che si avviano frequentemente in una singola categoria in modo da poterli trovare rapidamente.

>[!NOTE]
>
>Se in genere si avviano i processi quando si utilizza &#39;area di lavoro di AEM Forms, è possibile impostare la preferenza Posizione iniziale in modo da visualizzare automaticamente la categoria Preferiti all&#39;avvio &#39;area di lavoro di AEM Forms. Per ulteriori dettagli, vedere Gestione delle preferenze in [Guida introduttiva &#39;area di lavoro AEM Forms](/help/forms/using/getting-started-livecycle-html-workspace.md).

Per contrassegnare un processo come preferito, selezionate l&#39;attività nella relativa categoria e fate clic sulla stella vuota. La stella diventa dorata. Per contrassegnare un processo come preferito, fate di nuovo clic sulla stella d&#39;oro.
