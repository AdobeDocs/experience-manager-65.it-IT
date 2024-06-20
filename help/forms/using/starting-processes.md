---
title: Avvio dei processi
description: 'Come utilizzare LiveCycle AEM Forms Workspace: selezionare i processi, aggiungere note e allegati, salvare le bozze e aggiungerle ai preferiti.'
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: b2a6ba3a-0f4c-44b1-8f9a-c15c6fb8c305
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '1334'
ht-degree: 0%

---

# Avvio dei processi {#starting-processes}

AEM Forms workspace organizza i processi in base alle categorie impostate dall&#39;amministratore o dal designer processi. È inoltre possibile inserire i processi utilizzati di frequente nella categoria Preferiti in modo da poterli trovare rapidamente.

Quando si avvia un processo, potrebbe essere necessario compilare un modulo per avviare un processo aziendale controllato da AEM Forms workflow. Se un modulo utilizza il processo di preparazione dei dati, alcune informazioni possono essere precompilate in un modulo vuoto, quando viene avviato un nuovo processo.

Ad esempio, si desidera acquistare un nuovo monitor e quindi avviare un processo denominato *Ordine di acquisto*. Quando si avvia il processo, viene visualizzata una maschera in cui vengono richiesti i dettagli dell&#39;articolo da ordinare. Il nome, il numero del dipendente e il nome del responsabile possono già essere precompilati nel modulo. Quando si invia la richiesta, viene avviato un processo aziendale. In base alla definizione del processo, il server instrada automaticamente la richiesta al manager. L’attività inizia a comparire nell’elenco delle cose da fare del tuo manager. Quando il manager approva la richiesta, il flusso di lavoro Forms la indirizza al reparto acquisti e ti invia una notifica e-mail.

## Selezione dei processi da avviare {#selecting-processes-to-start}

È possibile selezionare un processo per avviarlo o per visualizzare ulteriori informazioni su di esso.

Quando si seleziona un processo da avviare, potrebbe essere necessario compilare un modulo associato a tale processo. L’invio del modulo avvia il processo.

Sono supportati i Forms in vari tipi di formati di file, tra cui Adobe PDF, HTML e SWF. Un modulo può avere l&#39;aspetto di un modulo tradizionale stampabile o basato su Web oppure può guidare l&#39;utente attraverso una serie di pannelli in stile procedura guidata per la raccolta di informazioni.

Se il modulo e il processo lo consentono, è inoltre possibile salvare il modulo in modalità non in linea, compilarlo e quindi inviarlo per completare l&#39;attività. Quando il modulo viene inviato, il client e-mail viene avviato con l’indirizzo e-mail del server appropriato, se è configurato l’endpoint e-mail. Puoi quindi inviare il modulo completato al server tramite e-mail.

Quando si seleziona un processo, vengono visualizzate le schede Modulo e Dettagli. Se il processo consente di aggiungere note o allegati, vengono visualizzate anche le schede Allegati e Note. Se hai anche configurato l’URL di riepilogo con il processo, viene visualizzata la scheda Riepilogo. Nella scheda Forms viene visualizzato il modulo associato, mentre nella scheda Dettagli vengono visualizzate informazioni sull&#39;attività corrente e sul processo di cui fa parte.

### Avviare un processo aziendale {#start-a-business-process}

1. Nella pagina Avvia processo selezionare una categoria nell&#39;elenco a sinistra. Tutti i processi a cui hai accesso nella categoria vengono visualizzati a destra.

   >[!NOTE]
   >
   >Se il riquadro Categorie è compresso, fare clic su Apri categorie nell&#39;area in alto a sinistra dell&#39;area di lavoro di AEM Forms per aprire il riquadro.

1. Selezionare un processo facendo clic su un&#39;attività. Il modulo associato al processo viene aperto nella scheda Modulo.

   Ogni modulo di un processo ha un URL univoco. Puoi utilizzare l’URL univoco per avviare direttamente HTML Workspace con il processo e il modulo specifici. Il formato dell’URL è https://&lt;server>:&lt;port>/lc/libs/ws/index.html#/startprocess/&lt;applicationname>%2F&lt;processname>. Il &lt;applicationname>%2F&lt;processname> La stringa è sempre codificata in URL. Un URL di esempio è http://localhost:8080/lc/libs/ws/index.html#/startprocess/MyApplication%2FNewProcess. La stringa ApplicationName%2FProcessName nell&#39;esempio è codificata in URL.

1. Compilare il modulo seguendo le istruzioni fornite. Se necessario, fai clic su **Ingrandisci** per aumentare l&#39;area visibile del modulo.
1. Se è disponibile la scheda Allegati, aggiungere gli allegati in base alle esigenze.
1. Se la scheda Note è disponibile, fornisci le note richieste.
1. Effettua una delle seguenti operazioni:

   * Fare clic sul pulsante Invia nel modulo, se il modulo include un pulsante Invia.
   * Se il modulo non dispone di un pulsante Invia, fare clic su Completa sotto il modulo.

   Gestione processi avvia il processo e indirizza il modulo agli elenchi Da fare delle persone appropriate che devono completare l&#39;attività successiva nel processo.

   Se è necessario chiudere un modulo prima di inviarlo e senza perdere i dati immessi, salvare una bozza e completarla in un secondo momento se il processo lo consente. Se il modulo e il processo lo consentono, è inoltre possibile fare clic su **Offline** e successivamente inviarlo da Adobe® Reader® o Adobe® Acrobat® Professional o Acrobat Standard.

   >[!NOTE]
   >
   >L’opzione offline è disponibile solo per i PDF forms.

## Aggiunta di note e allegati {#adding-notes-and-attachments}

Se il processo lo consente, è possibile aggiungere note e file allegati a un processo. È possibile concedere autorizzazioni ad altri utenti che partecipano al processo per visualizzare, aggiornare ed eliminare le note o gli allegati.

### Aggiungi una nota {#add-a-note}

Potete aggiungere più note, modificare le note scritte ed eliminarle. A ciascuna nota sono associati un titolo, una descrizione e un’autorizzazione di accesso. È possibile impostare una delle seguenti autorizzazioni di accesso per una nota:

* Sola lettura (autorizzazione predefinita)
* Lettura/Modifica/Elimina
* Lettura/Modifica
* Lettura/eliminazione
* Nessun accesso

1. Apri un’attività e fai clic su **Note** , se il processo lo consente.
1. Digita un titolo per la nota nella **Titolo** e digitare il testo della nota nella casella **Nota** casella.
1. Seleziona la **Autorizzazioni** livello della nota per gli altri utenti che partecipano al processo.
1. Clic **OK**. Al modulo viene allegato un file di testo contenente la nota. È possibile aggiornare una nota facendo clic su di essa e modificando direttamente il testo. È possibile eliminare una nota facendo clic sul pulsante **Elimina** pulsante ![Immagine di un cestino](assets/icondelete.png) accanto alla nota.

### Aggiungi un allegato {#add-an-attachment}

È inoltre possibile aggiungere commenti sull&#39;allegato. È possibile impostare una delle seguenti autorizzazioni di accesso per un allegato:

* Sola lettura (autorizzazione predefinita)
* Lettura/Modifica/Elimina
* Lettura/Modifica
* Lettura/eliminazione
* Nessun accesso

1. Fai clic su **Allegati** e seleziona **Allegato**.
1. Clic **Sfoglia** per selezionare il file da allegare.
1. Seleziona la **Autorizzazioni** livello dell&#39;allegato per altri utenti che partecipano al processo. Se si seleziona **Letto**, altri utenti possono salvare il file localmente. Se selezioni una delle autorizzazioni di modifica, anche altri utenti possono caricare un nuovo file per sostituire l’allegato.
1. Clic **OK**. Il file viene allegato al modulo. È possibile eliminare un file facendo clic sul pulsante **Elimina** pulsante ![Immagine di un cestino](assets/icondelete.png) accanto all&#39;allegato.

## Salvataggio delle bozze dei moduli {#saving-draft-copies-of-forms}

Se è necessario compilare e inviare un modulo in un secondo momento, è possibile salvare una bozza di copia di un modulo in modo da non perdere il lavoro esistente. Le bozze vengono aggiunte alla categoria Bozze nella pagina Da fare.

Dopo aver riaperto e inviato un modulo di bozza, la bozza viene rimossa dalla categoria Bozze.

Inoltre, puoi configurare l’area di lavoro in modo da salvare automaticamente le informazioni immesse da un utente come bozza. Per ulteriori informazioni, consulta [Gestione delle preferenze](/help/forms/using/getting-started-livecycle-html-workspace.md).

>[!NOTE]
>
>Il pulsante Salva non è disponibile per alcuni moduli, a seconda del processo a cui è associato.

### Salvare una bozza {#save-a-draft-copy}

1. Clic **Salva** nell’angolo in basso a sinistra di qualsiasi scheda. Il modulo viene aggiunto alla categoria Bozze della pagina Da fare. Tutte le modifiche apportate al modulo vengono salvate.

### Riaprire una bozza di copia {#reopen-a-draft-copy}

1. Nella pagina Da fare selezionare **Bozze** in coda e fare clic sulla bozza del modulo.

   Se il modulo contiene una serie di pannelli, potrebbe essere necessario passare al pannello in cui è stata terminata l&#39;ultima sessione.

## Aggiunta di processi alla categoria Preferiti {#adding-processes-to-the-favorites-category}

È possibile aggiungere qualsiasi processo alla categoria Preferiti. Impostando i preferiti, è possibile raggruppare tutti i processi che si avviano di frequente in un&#39;unica categoria in modo da poterli trovare rapidamente.

>[!NOTE]
>
>Se in genere si avviano i processi quando si utilizza l&#39;area di lavoro di AEM Forms, è possibile impostare la preferenza Posizione iniziale per visualizzare automaticamente la categoria Preferiti all&#39;avvio dell&#39;area di lavoro di AEM Forms. Per ulteriori dettagli, consulta Gestione delle preferenze in [Guida introduttiva all’area di lavoro di AEM Forms](/help/forms/using/getting-started-livecycle-html-workspace.md).

Per contrassegnare un processo come preferito, selezionare l&#39;attività nella relativa categoria e fare clic sulla stella vuota. La stella diventa dorata. Per annullare il contrassegno di un processo come preferito, fare di nuovo clic sulla stella d&#39;oro.
