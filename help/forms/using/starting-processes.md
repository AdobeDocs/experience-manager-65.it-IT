---
title: Avvio dei processi
seo-title: Starting processes
description: 'Come utilizzare l''area di lavoro di LiveCycle AEM Forms: seleziona i processi, aggiungi note e allegati, salva le copie delle bozze e aggiungi ai preferiti.'
seo-description: How to use LiveCycle AEM Forms workspace--select processes, add notes and attachments, save draft copies, and add to favorites.
uuid: a61da785-25b4-4482-bd72-02e250d35dc7
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c9d3f369-3744-41d5-b340-390ab7e03f36
exl-id: b2a6ba3a-0f4c-44b1-8f9a-c15c6fb8c305
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1343'
ht-degree: 0%

---

# Avvio dei processi {#starting-processes}

AEM Forms Workspace organizza i processi in base alle categorie configurate dall&#39;amministratore o dalla finestra di progettazione dei processi. È inoltre possibile inserire i processi utilizzati di frequente nella categoria Preferiti in modo da poterli trovare rapidamente.

Quando si avvia un processo, potrebbe essere necessario compilare un modulo per avviare un processo aziendale controllato dal flusso di lavoro AEM Forms. Se un modulo utilizza il processo di preparazione dei dati, alcune informazioni possono essere precompilate in un modulo vuoto quando viene avviato un nuovo processo.

Ad esempio, si desidera acquistare un nuovo monitor del computer e quindi avviare un processo denominato *Ordine di acquisto*. Quando si avvia il processo, viene visualizzato un modulo che richiede di specificare i dettagli dell&#39;elemento da ordinare. Il nome, il numero del dipendente e il nome del responsabile potrebbero essere già precompilati sul modulo. Quando si invia la richiesta, viene avviato un processo aziendale. In base alla definizione del processo, il server indirizza automaticamente la richiesta al tuo responsabile. L’attività inizia a comparire nell’elenco A-do del tuo responsabile. Quando il tuo responsabile approva la richiesta, il flusso di lavoro dei moduli indirizza la richiesta al reparto acquisti e invia una notifica e-mail.

## Selezione dei processi da avviare {#selecting-processes-to-start}

È possibile selezionare un processo per avviarlo o per visualizzare ulteriori informazioni.

Quando si seleziona un processo da avviare, potrebbe essere necessario compilare un modulo associato a tale processo. L’invio del modulo avvia il processo.

Sono supportati Forms in vari tipi di formati di file, inclusi i file Adobe PDF, HTML e SWF. Un modulo può avere l’aspetto di un modulo tradizionale stampabile o basato su web oppure può essere di aiuto nell’uso di una serie di pannelli in stile procedura guidata per raccogliere informazioni.

Se il modulo e la procedura lo consentono, è anche possibile salvare il modulo offline, compilarlo e quindi inviarlo per completare l&#39;attività. Quando il modulo viene inviato, il client e-mail viene avviato con l’indirizzo e-mail del server appropriato, se è configurato l’endpoint e-mail. Puoi quindi inviare il modulo completato al server tramite e-mail.

Quando si seleziona un processo, vengono visualizzate le schede Modulo e Dettagli . Se il processo consente di aggiungere note o allegati, vengono visualizzate anche le schede Allegati e Note . Se hai configurato anche l’url di riepilogo con il processo, viene visualizzata anche la scheda Riepilogo . Nella scheda Forms viene visualizzato il modulo associato e nella scheda Dettagli vengono visualizzate informazioni sull’attività corrente e sul processo di cui fa parte.

### Avviare un processo aziendale {#start-a-business-process}

1. Nella pagina Avvia processo selezionare una categoria nell’elenco a sinistra. Tutti i processi a cui hai accesso nella categoria vengono visualizzati a destra.

   >[!NOTE]
   >
   >Se il riquadro Categorie è compresso, fare clic su &#39;Apri categorie&#39; nell&#39;area in alto a sinistra dell&#39;area di lavoro AEM Forms per aprire il riquadro.

1. Selezionare un processo facendo clic su un&#39;attività. Il modulo associato al processo viene visualizzato nella scheda Modulo .

   Ogni modulo in un processo ha un URL univoco. Puoi utilizzare l’URL univoco per avviare direttamente HTML Workspace con il processo e il modulo specifici. Il formato dell’URL è https://&lt;server>:&lt;port>/lc/libs/ws/index.html#/startprocess/&lt;applicationname>%2F&lt;processname>. La &lt;applicationname>%2F&lt;processname> La stringa è sempre codificata in URL. Un esempio di URL è http://localhost:8080/lc/libs/ws/index.html#/startprocess/MyApplication%2FNewProcess. La stringa ApplicationName%2FProcessName nell&#39;esempio è codificata in URL.

1. Compila il modulo secondo le istruzioni fornite con esso. Se necessario, fai clic su **Massimizza** per aumentare l’area visibile del modulo.
1. Se la scheda Allegati è disponibile, aggiungere gli allegati come necessario.
1. Se la scheda Note è disponibile, fornisci eventuali note in base alle esigenze.
1. Esegui uno dei seguenti passaggi:

   * Se nel modulo è presente un pulsante Invia, fare clic sul pulsante Invia del modulo.
   * Fare clic su Completa sotto il modulo, se il modulo non dispone di un pulsante Invia.

   Process Management avvia il processo e indirizza il modulo agli elenchi To-do delle persone appropriate che devono completare l&#39;attività successiva nel processo.

   Se è necessario chiudere un modulo prima di inviarlo e senza perdere i dati immessi, salvare una bozza e completarla in un secondo momento, se il processo lo consente. Se il modulo e il processo lo consentono, è anche possibile fare clic su **Offline** e successivamente invialo da Adobe® Reader® o Adobe® Acrobat® Professional o Acrobat Standard.

   >[!NOTE]
   >
   >L’opzione offline è disponibile solo per i PDF forms.

## Aggiunta di note e allegati {#adding-notes-and-attachments}

È possibile aggiungere note e allegati a un processo se il processo lo consente. È possibile fornire autorizzazioni ad altri utenti che partecipano al processo per visualizzare, aggiornare ed eliminare le note o gli allegati.

### Aggiungi una nota {#add-a-note}

È possibile aggiungere più note, modificarle ed eliminarle. A ciascuna nota sono associati un titolo, una descrizione e un’autorizzazione di accesso. È possibile impostare una delle seguenti autorizzazioni di accesso su una nota:

* Sola lettura (autorizzazione predefinita)
* Lettura/Modifica/Elimina
* Lettura/Modifica
* Lettura/eliminazione
* Nessun accesso

1. Apri un’attività e fai clic su **Note** , se il processo lo consente.
1. Digita un titolo per la nota nella **Titolo** e digitare il testo della nota nella **Nota** scatola.
1. Seleziona la **Autorizzazioni** livello della nota per gli altri utenti che partecipano al processo.
1. Fai clic su **OK**. Al modulo viene allegato un file di testo contenente la nota. È possibile aggiornare una nota facendo clic su di essa e modificando direttamente il testo. Per eliminare una nota, fai clic sul pulsante **Elimina** pulsante ![Immagine di un cestino](assets/icondelete.png) accanto alla nota.

### Aggiungere un allegato {#add-an-attachment}

È inoltre possibile aggiungere i commenti relativi all&#39;allegato. È possibile impostare una delle seguenti autorizzazioni di accesso su un allegato:

* Sola lettura (autorizzazione predefinita)
* Lettura/Modifica/Elimina
* Lettura/Modifica
* Lettura/eliminazione
* Nessun accesso

1. Fai clic sul pulsante **Allegati** e seleziona **Allegato**.
1. Fai clic su **Sfoglia** per selezionare il file da allegare.
1. Seleziona la **Autorizzazioni** livello dell&#39;allegato per gli altri utenti che partecipano al processo. Se si seleziona **Leggi**, altri utenti possono salvare il file localmente. Se selezioni una delle autorizzazioni di modifica, altri utenti possono caricare anche un nuovo file per sostituire l&#39;allegato.
1. Fai clic su **OK**. Il file viene allegato al modulo. Per eliminare un file, fai clic sul pulsante **Elimina** pulsante ![Immagine di un cestino](assets/icondelete.png) accanto all&#39;attacco.

## Salvataggio delle copie in bozza dei moduli {#saving-draft-copies-of-forms}

Se in seguito è necessario completare e inviare un modulo, è possibile salvare una bozza di copia di un modulo in modo da non perdere il lavoro esistente. Le copie bozza vengono aggiunte alla categoria Bozze nella pagina Da fare.

Dopo aver riaperto e inviato una bozza di modulo, la bozza viene rimossa dalla categoria Bozze.

Inoltre, puoi configurare l’area di lavoro per salvare automaticamente le informazioni immesse da un utente come bozza. Per ulteriori informazioni, consulta [Gestione delle preferenze](/help/forms/using/getting-started-livecycle-html-workspace.md).

>[!NOTE]
>
>Il pulsante Salva non è disponibile per alcuni moduli, a seconda del processo a cui è associato.

### Salvare una bozza di copia {#save-a-draft-copy}

1. Fai clic su **Salva** nell’angolo in basso a sinistra di qualsiasi scheda. Il modulo viene aggiunto alla categoria Bozze nella pagina Da fare. Tutte le modifiche apportate al modulo vengono salvate.

### Riaprire una bozza di copia {#reopen-a-draft-copy}

1. Nella pagina Da fare, seleziona la **Bozze** accodare e fare clic sulla bozza di copia del modulo.

   Se il modulo contiene una serie di pannelli, potrebbe essere necessario passare al pannello in cui è stata terminata l’ultima sessione.

## Aggiunta di processi alla categoria Preferiti {#adding-processes-to-the-favorites-category}

È possibile aggiungere qualsiasi processo alla categoria Preferiti. Impostando i preferiti, puoi raggruppare tutti i processi che si iniziano frequentemente in una singola categoria in modo da poterli trovare rapidamente.

>[!NOTE]
>
>Se i processi vengono solitamente avviati quando si utilizza l&#39;area di lavoro AEM Forms, è possibile impostare la preferenza Posizione iniziale in modo da visualizzare automaticamente la categoria Preferiti all&#39;avvio dell&#39;area di lavoro AEM Forms. Per ulteriori dettagli, consulta Gestione delle preferenze in [Guida introduttiva all’area di lavoro di AEM Forms](/help/forms/using/getting-started-livecycle-html-workspace.md).

Per contrassegnare un processo come preferito, selezionalo nella relativa categoria e fai clic sulla stella vuota. La stella diventa dorata. Per contrassegnare un processo come preferito, fai di nuovo clic sulla stella dorata.
