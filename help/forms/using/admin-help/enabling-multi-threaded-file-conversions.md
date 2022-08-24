---
title: Abilitazione delle conversioni di file multithread
seo-title: Enabling multi-threaded file conversions
description: Scopri come abilitare le conversioni di file multithread.
seo-description: Learn how to enable multi-threaded file conversions.
uuid: 830c78aa-4f68-4e01-8b24-69a0275689c7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 85d655bb-1b6b-4b4d-ae39-eca3ef9b7fd7
feature: PDF Generator
exl-id: 402c1fd4-c6c8-494e-b452-b56a91c4a397
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 0%

---

# Abilitazione delle conversioni di file multithread {#enabling-multi-threaded-file-conversions}

PDF Generator consente di abilitare conversioni di file multithread per determinati tipi di file. La conversione di file multithread migliora le prestazioni di PDF Generator consentendo a di eseguire più conversioni contemporaneamente.

## Abilitazione delle conversioni di file multithread per documenti OpenOffice, Word e PowerPoint {#enabling-multi-threaded-file-conversions-for-openoffice-word-and-powerpoint-documents}

Per impostazione predefinita, PDF Generator può convertire un solo documento OpenOffice, Microsoft Word o PowerPoint alla volta. Se si attivano conversioni multi-thread, PDF Generator può convertire contemporaneamente più di uno dei documenti. PDF Generator avvia più istanze di OpenOffice o PDFMaker (utilizzate per eseguire le conversioni di Word e PowerPoint).

>[!NOTE]
>
>Le conversioni di file multithread non sono supportate con Microsoft Word 2003 e PowerPoint 2003. Per abilitare le conversioni di file multithread, eseguire l&#39;aggiornamento a Microsoft Word 2007 e PowerPoint 2007 o Microsoft Word 2010 e PowerPoint 2010.

>[!NOTE]
>
>Le conversioni di file multithread non sono supportate con Microsoft Excel, Microsoft Visio, Microsoft Project o Microsoft Publisher.

Ogni istanza di OpenOffice o PDFMaker viene avviata utilizzando un account utente separato. Ogni account utente aggiunto deve essere un utente valido con privilegi amministrativi nel computer server dei moduli. In un ambiente cluster, lo stesso set di utenti deve essere valido per tutti i nodi del cluster.

Nella pagina Account utente della console di amministrazione, puoi specificare gli account utente da utilizzare per le conversioni di file multithread. È possibile aggiungere account, eliminarli o modificare le password dell&#39;account. Se si esegue PDF Generator su Windows Server 2003 o Windows Server 2008, aggiungere almeno tre account utente con privilegi di amministratore.

Quando si aggiungono utenti per OpenOffice, Microsoft Word o Microsoft PowerPoint su Windows Server 2003 o 2008 o per OpenOffice su Linux o Sun™ Solaris™, le finestre di dialogo di attivazione iniziali vengono ignorate per tutti gli utenti.

### Aggiungi il diritto di sostituire il token a livello di processo {#add-the-right-to-replace-the-process-level-token}

In un sistema operativo Windows, gli account utente amministratore utilizzati per la conversione PDF (utenti PDFG) dovranno sostituire i privilegi di token a livello di processo. Puoi aggiungere questo diritto utilizzando l’Editor Criteri di gruppo:

1. Nel menu Start di Windows, fare clic su Esegui e quindi immettere gpedit.msc.
1. Fare clic su Criteri computer locali > Configurazione computer > Impostazioni di Windows > Impostazioni protezione > Criteri locali > Assegnazione diritti utente. Modifica le *Sostituire un token a livello di processo* per includere il gruppo Administrators.
1. Aggiungi l’utente alla voce Replace a Process Level Token (Sostituisci token a livello di processo).

### Configurazione aggiuntiva necessaria per OpenOffice, Microsoft Word e Microsoft PowerPoint su Windows Server 2008 {#additional-configuration-required-for-openoffice-microsoft-word-and-microsoft-powerpoint-on-windows-server-2008}

Se si esegue OpenOffice, Microsoft Word o Microsoft PowerPoint su Windows Server 2008, disattivare l&#39;UAC per ogni utente aggiunto.

1. Fai clic su Pannello di controllo Campaign > Account utente > Attiva o disattiva il controllo dell&#39;account utente.
1. Deselezionare la casella &quot;Usa controllo account utente (UAC) per proteggere il computer&quot; e fare clic su OK.
1. Riavviare il computer per rendere effettive le impostazioni.

### Configurazione aggiuntiva necessaria per OpenOffice su Linux o Solaris {#additional-configuration-required-for-openoffice-on-linux-or-solaris}

1. Aggiungi account utente. (Vedi [Aggiungi un account utente](enabling-multi-threaded-file-conversions.md#add-a-user-account).)
1. Successivamente, apporti modifiche al file /etc/sudoers. L&#39;autorizzazione predefinita per questo file è 440. Modifica l&#39;autorizzazione per questo file in scrivibile.
1. Aggiungi voci per altri utenti (diversi dall’amministratore che esegue il server dei moduli) nel file /etc/sudoers. Ad esempio, se si esegue AEM moduli come utente denominato lcadm e un server denominato myhost e si desidera impersonare user1 e user2, aggiungere le seguenti voci a /etc/sudoers:

   ```shell
    lcadm myhost=(user1) NOPASSWD: ALL
    lcadm myhost=(user2) NOPASSWD: ALL
   ```

   Questa configurazione consente a lcadm di eseguire qualsiasi comando sull&#39;host &#39;myhost&#39; come &#39;user1&#39; o &#39;user2&#39; senza richiedere la password.

   >[!NOTE]
   >
   >Assicurati di aver assegnato i ruoli utente di sistema e utente PDFG a &quot;user1&quot; e &quot;user2&quot; . Per assegnare il ruolo PDFG a un utente, vedi [Aggiungi un account utente](enabling-multi-threaded-file-conversions.md#add-a-user-account)

1. Sempre nel file /etc/sudoers, individua e commenta questa riga aggiungendo un simbolo cancelletto (#) all&#39;inizio della riga:

   ```shell
   Defaults requiretty
   ```

   Questo consente di aggiungere utenti Linux.

1. Cambia di nuovo l&#39;autorizzazione per il file etc/sudoers a 440.
1. Consenti a tutti gli utenti aggiunti tramite [Aggiungi un account utente](enabling-multi-threaded-file-conversions.md#add-a-user-account) per effettuare connessioni al server dei moduli. Ad esempio, per consentire a un utente locale denominato user1 di eseguire la connessione al server dei moduli, utilizzare il comando seguente

   `xhost +local:user1@`

   Per ulteriori informazioni, consulta la documentazione del comando xhost .

1. Riavvia il server.

>[!NOTE]
>
>OpenOffice deve essere installato in un percorso di directory accessibile a tutti gli utenti PDFG. È possibile verificarlo accedendo come utente PDFG e verificando se è possibile avviare OpenOffice senza problemi.

### Aggiungi un account utente {#add-a-user-account}

1. Nella console di amministrazione, fare clic su Servizi > Generatore di PDF > Account utente.
1. Fare clic su Aggiungi e immettere il nome utente e la password di un utente con privilegi amministrativi nel server dei moduli. Se si configurano gli utenti per OpenOffice, ignorare le finestre di dialogo di attivazione iniziale di OpenOffice.

   >[!NOTE]
   >
   >Se si configurano utenti per OpenOffice, il numero di istanze di OpenOffice non può essere maggiore del numero di account utente specificato in questo passaggio.

1. Riavvia il server dei moduli.

### Rimuovere un utente dall’elenco utilizzato per le conversioni di file multithread {#remove-a-user-from-the-list-used-for-multi-threaded-file-conversions}

1. Nella console di amministrazione, fare clic su Servizi > Generatore di PDF > Account utente.
1. Fare clic sulla casella di controllo accanto all&#39;utente che si desidera rimuovere e fare clic su Elimina.
1. Nella pagina di conferma, fai clic su Elimina.
1. Riavvia il server dei moduli.

### Modificare la password di un account {#change-the-password-for-an-account}

1. Nella console di amministrazione, fare clic su Servizi > Generatore di PDF > Account utente.
1. Fare clic sul nome utente, quindi immettere e confermare la nuova password. Questa password deve corrispondere alla password di sistema dell’utente.
