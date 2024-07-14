---
title: Abilitazione delle conversioni di file multithread
description: Scopri come abilitare le conversioni di file multithread.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: 402c1fd4-c6c8-494e-b452-b56a91c4a397
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 0%

---

# Abilitazione delle conversioni di file multithread {#enabling-multi-threaded-file-conversions}

PDF Generator consente di abilitare le conversioni di file con più thread per alcuni tipi di file. La conversione di file multithreading migliora le prestazioni di PDF Generator consentendogli di eseguire più conversioni contemporaneamente.

## Abilitazione delle conversioni di file multithread per i documenti di OpenOffice, Word e PowerPoint {#enabling-multi-threaded-file-conversions-for-openoffice-word-and-powerpoint-documents}

Per impostazione predefinita, PDF Generator può convertire un solo documento OpenOffice, Microsoft® Word o PowerPoint alla volta. Se si abilitano conversioni multithread, PDF Generator può convertire più di uno dei documenti contemporaneamente. PDF Generator avvia più istanze di OpenOffice o PDFMaker (utilizzate per eseguire le conversioni di Word e PowerPoint).

>[!NOTE]
>
>Le conversioni di file multithread non sono supportate in Microsoft® Word 2003 e PowerPoint 2003. Per abilitare le conversioni di file multithread, eseguire l&#39;aggiornamento a Microsoft® Word 2007 e PowerPoint 2007 o Microsoft® Word 2010 e PowerPoint 2010.

>[!NOTE]
>
>Le conversioni di file multithread non sono supportate in Microsoft® Excel, Microsoft® Visio, Microsoft® Project o Microsoft® Publisher.

Ogni istanza di OpenOffice o PDFMaker viene avviata utilizzando un account utente separato. Ogni account utente aggiunto deve essere un utente valido con privilegi amministrativi nel computer Forms Server. In un ambiente cluster, lo stesso insieme di utenti deve essere valido per tutti i nodi del cluster.

Nella pagina Account utente della console di amministrazione è possibile specificare gli account utente da utilizzare per le conversioni di file multithread. È possibile aggiungere, eliminare o modificare le password degli account. Se si esegue PDF Generator in Windows Server 2003 o Windows Server 2008, aggiungere almeno tre account utente con privilegi di amministratore.

Quando si aggiungono utenti per OpenOffice, Microsoft® Word o Microsoft® PowerPoint su Windows Server 2003 o 2008 oppure per OpenOffice su Linux® o Sun™ Solaris™, chiudere le finestre di dialogo di attivazione iniziali per tutti gli utenti.

### Aggiungi il diritto di sostituire il token a livello di processo {#add-the-right-to-replace-the-process-level-token}

In un sistema operativo Windows, gli account utente dell&#39;amministratore utilizzati per la conversione PDF (utenti PDFG) devono sostituire i privilegi dei token a livello di processo. È possibile aggiungere questo diritto utilizzando Editor Criteri di gruppo:

1. Nel menu Start di Windows fare clic su Esegui e quindi immettere gpedit.msc.
1. Fare clic su Criteri computer locale > Configurazione computer > Impostazioni di Windows > Impostazioni protezione > Criteri locali > Assegnazione diritti utente. Modifica il criterio *Sostituisci un token a livello di processo* per includere il gruppo Administrators.
1. Aggiungere l&#39;utente alla voce Sostituisci token a livello di processo.

### Configurazione aggiuntiva necessaria per OpenOffice, Microsoft® Word e Microsoft® PowerPoint su Windows Server 2008 {#additional-configuration-required-for-openoffice-microsoft-word-and-microsoft-powerpoint-on-windows-server-2008}

Se si esegue OpenOffice, Microsoft® Word o Microsoft® PowerPoint su Windows Server 2008, disattivare Controllo dell&#39;account utente per ogni utente aggiunto.

1. Fare clic su Pannello di controllo Campaign > Account utente > Attiva o disattiva Controllo account utente.
1. Deselezionare la casella &quot;Utilizzare Controllo account utente per proteggere il computer&quot; e fare clic su OK.
1. Riavviare il computer per rendere effettive le impostazioni.

### Configurazione aggiuntiva richiesta per OpenOffice su Linux® o Solaris™ {#additional-configuration-required-for-openoffice-on-linux-or-solaris}

1. Aggiungere account utente. (Vedi [Aggiungere un account utente](enabling-multi-threaded-file-conversions.md#add-a-user-account).)
1. Successivamente, è necessario modificare il file /etc/sudoers. L&#39;autorizzazione predefinita per questo file è 440. Cambia l&#39;autorizzazione per questo file in scrivibile.
1. Aggiungere voci per altri utenti (diversi dall&#39;amministratore che esegue Forms Server) nel file /etc/sudoers. Ad esempio, se si eseguono moduli AEM come un utente denominato lcadm e un server denominato myhost e si desidera rappresentare user1 e user2, aggiungere le seguenti voci a /etc/sudoers:

   ```shell
    lcadm myhost=(user1) NOPASSWD: ALL
    lcadm myhost=(user2) NOPASSWD: ALL
   ```

   Questa configurazione consente a lcadm di eseguire qualsiasi comando sull&#39;host &#39;myhost&#39; come &#39;user1&#39; o &#39;user2&#39; senza richiedere una password.

   >[!NOTE]
   >
   >Assicurati di aver assegnato i ruoli utente del sistema e utente PDFG a &quot;utente1&quot; e &quot;utente2&quot;. Per assegnare un ruolo PDFG a un utente, vedere [Aggiungere un account utente](enabling-multi-threaded-file-conversions.md#add-a-user-account)

1. Inoltre, nel file /etc/sudoers, individua e commenta questa riga aggiungendo un cancelletto (#) all’inizio della riga:

   ```shell
   Defaults requiretty
   ```

   Questo consente di aggiungere utenti Linux®.

1. Modifica l’autorizzazione per il file etc/sudoers riportandola a 440.
1. Consenti a tutti gli utenti aggiunti tramite [Aggiungi un account utente](enabling-multi-threaded-file-conversions.md#add-a-user-account) di effettuare connessioni al server Forms. Ad esempio, per consentire a un utente locale denominato user1 l&#39;autorizzazione di effettuare la connessione al server Forms, utilizzare il comando seguente

   `xhost +local:user1@`

   Per ulteriori dettagli, consulta la documentazione sui comandi xhost.

1. Riavviare il server.

>[!NOTE]
>
>OpenOffice deve essere installato in una directory accessibile a tutti gli utenti PDFG. Per verificare questo aspetto, accedi come utente PDFG e verifica se è possibile avviare OpenOffice senza problemi.

### Aggiungere un account utente {#add-a-user-account}

1. Nella console di amministrazione, fai clic su Servizi > PDF Generator > Account utente.
1. Fare clic su Aggiungi e immettere il nome utente e la password di un utente che dispone di privilegi amministrativi sul server Forms. Se si configurano gli utenti per OpenOffice, chiudere le finestre di dialogo iniziali di attivazione di OpenOffice.

   >[!NOTE]
   >
   >Se si configurano gli utenti per OpenOffice, il numero di istanze di OpenOffice non può essere maggiore del numero di account utente specificato in questo passaggio.

1. Riavviare Forms Server.

### Rimuovere un utente dall&#39;elenco utilizzato per le conversioni di file multithread {#remove-a-user-from-the-list-used-for-multi-threaded-file-conversions}

1. Nella console di amministrazione, fai clic su Servizi > PDF Generator > Account utente.
1. Selezionare la casella di controllo accanto all&#39;utente che si desidera rimuovere e fare clic su Elimina.
1. Nella pagina di conferma, fai clic su Elimina.
1. Riavviare Forms Server.

### Modificare la password di un account {#change-the-password-for-an-account}

1. Nella console di amministrazione, fai clic su Servizi > PDF Generator > Account utente.
1. Fai clic sul nome utente, quindi immetti e conferma la nuova password. Questa password deve corrispondere alla password di sistema dell&#39;utente.
