---
title: Abilitazione di conversioni di file multithread
seo-title: Abilitazione di conversioni di file multithread
description: Scoprite come abilitare le conversioni di file multithread.
seo-description: Scoprite come abilitare le conversioni di file multithread.
uuid: 830c78aa-4f68-4e01-8b24-69a0275689c7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 85d655bb-1b6b-4b4d-ae39-eca3ef9b7fd7
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '880'
ht-degree: 0%

---


# Abilitazione delle conversioni di file multithread {#enabling-multi-threaded-file-conversions}

PDF Generator consente di abilitare conversioni di file multithread per alcuni tipi di file. La conversione di file multithread migliora le prestazioni di PDF Generator consentendo a quest&#39;ultimo di eseguire più conversioni contemporaneamente.

## Abilitazione di conversioni di file multithread per documenti OpenOffice, Word e PowerPoint {#enabling-multi-threaded-file-conversions-for-openoffice-word-and-powerpoint-documents}

Per impostazione predefinita, PDF Generator può convertire un solo documento OpenOffice, Microsoft Word o PowerPoint alla volta. Se abilitate le conversioni multithread, PDF Generator può convertire simultaneamente più documenti. PDF Generator avvia più istanze di OpenOffice o PDFMaker (utilizzate per eseguire le conversioni di Word e PowerPoint).

>[!NOTE]
>
>Le conversioni di file multithread non sono supportate con Microsoft Word 2003 e PowerPoint 2003. Per abilitare le conversioni di file multithread, eseguire l&#39;aggiornamento a Microsoft Word 2007 e PowerPoint 2007 o Microsoft Word 2010 e PowerPoint 2010.

>[!NOTE]
>
>Le conversioni di file multithread non sono supportate con Microsoft Excel, Microsoft Visio, Microsoft Project o Microsoft Publisher.

Ogni istanza di OpenOffice o PDFMaker viene avviata utilizzando un account utente separato. Ogni account utente aggiunto deve essere un utente valido con privilegi amministrativi nel computer del server dei moduli. In un ambiente cluster, lo stesso set di utenti deve essere valido per tutti i nodi del cluster.

Nella pagina Account utente della console di amministrazione, potete specificare gli account utente da utilizzare per le conversioni di file multithread. Potete aggiungere account, eliminarli o cambiare le password dell&#39;account. Se PDF Generator è in esecuzione su Windows Server 2003 o Windows Server 2008, aggiungere almeno tre account utente con diritti di amministratore.

Quando si aggiungono utenti per OpenOffice, Microsoft Word o Microsoft PowerPoint su Windows Server 2003 o 2008, oppure per OpenOffice su Linux o Sun™ Solaris™, le finestre di dialogo di attivazione iniziali vengono chiuse per tutti gli utenti.

### Aggiungi il diritto per sostituire il token a livello di processo {#add-the-right-to-replace-the-process-level-token}

In un sistema operativo Windows, gli account utente amministratore utilizzati per la conversione PDF (utenti PDFG) dovranno sostituire i privilegi di token a livello di processo. È possibile aggiungere questo diritto utilizzando l&#39;Editor Criteri di gruppo:

1. Nel menu Start di Windows, fate clic su Esegui e immettete gpedit.msc.
1. Fate clic su Criteri computer locale > Configurazione computer > Impostazioni di Windows > Impostazioni di protezione > Criteri locali > Assegnazione diritti utente. Modificate il criterio *Sostituisci un token a livello di processo* per includere il gruppo Amministratori.
1. Aggiungete l&#39;utente alla voce Replace a Process Level Token (Sostituisci token a livello di processo).

### Configurazione aggiuntiva necessaria per OpenOffice, Microsoft Word e Microsoft PowerPoint in Windows Server 2008 {#additional-configuration-required-for-openoffice-microsoft-word-and-microsoft-powerpoint-on-windows-server-2008}

Se su Windows Server 2008 è in esecuzione OpenOffice, Microsoft Word o Microsoft PowerPoint, disattivate l&#39;account utente per ogni utente aggiunto.

1. Fate clic su Pannello di controllo Campaign > Account utente > Attiva o disattiva Controllo account utente.
1. Deselezionate la casella &quot;Usa controllo account utente (UAC) per proteggere il computer&quot; e fate clic su OK.
1. Riavviare il computer per rendere effettive le impostazioni.

### Configurazione aggiuntiva necessaria per OpenOffice su Linux o Solaris {#additional-configuration-required-for-openoffice-on-linux-or-solaris}

1. Aggiungete account utente. (Vedere [Aggiungere un account utente](enabling-multi-threaded-file-conversions.md#add-a-user-account).)
1. Quindi, verranno apportate modifiche al file /etc/sudoers. L&#39;autorizzazione predefinita per questo file è 440. Cambia l&#39;autorizzazione per questo file in scrivibile.
1. Aggiungere voci per altri utenti (diversi dall&#39;amministratore che esegue il server dei moduli) nel file /etc/sudoers. Ad esempio, se si esegue AEM moduli come utente denominato lcadm e server denominato myhost e si desidera rappresentare user1 e user2, aggiungere le seguenti voci a /etc/sudoers:

   ```shell
    lcadm myhost=(user1) NOPASSWD: ALL
    lcadm myhost=(user2) NOPASSWD: ALL
   ```

   Questa configurazione consente a lcadm di eseguire qualsiasi comando sull&#39;host &quot;myhost&quot; come &quot;user1&quot; o &quot;user2&quot; senza richiedere la password.

   >[!NOTE]
   >
   >Assicurarsi di aver assegnato i ruoli utente utente di sistema e PDFG a &quot;user1&quot; e &quot;user2&quot;. Per assegnare il ruolo PDFG a un utente, vedere [Aggiungi un account utente](enabling-multi-threaded-file-conversions.md#add-a-user-account)

1. Anche nel file /etc/sudoers, individuare e commentare questa riga aggiungendo un simbolo cancelletto (#) all&#39;inizio della riga:

   ```shell
   Defaults requiretty
   ```

   Questo consente di aggiungere utenti Linux.

1. Cambia l&#39;autorizzazione per il file etc/sudoers a 440.
1. Consentire a tutti gli utenti aggiunti tramite [Aggiungi un account utente](enabling-multi-threaded-file-conversions.md#add-a-user-account) di effettuare connessioni al server dei moduli. Ad esempio, per consentire a un utente locale denominato user1 di stabilire la connessione al server dei moduli, utilizzare il comando seguente

   `xhost +local:user1@`

   Per ulteriori informazioni, consultare la documentazione del comando xhost.

1. Riavviate il server.

>[!NOTE]
>
>OpenOffice deve essere installato in una directory accessibile a tutti gli utenti PDFG. È possibile verificare questa situazione effettuando l&#39;accesso come utente PDFG e verificando se è possibile avviare OpenOffice senza problemi.

### Aggiungere un account utente {#add-a-user-account}

1. Nella console di amministrazione, fare clic su Servizi > PDF Generator > Account utente.
1. Fare clic su Aggiungi e immettere il nome utente e la password di un utente che dispone dei privilegi di amministratore nel server dei moduli. Se state configurando gli utenti per OpenOffice, chiudete le finestre di dialogo di attivazione iniziali di OpenOffice.

   >[!NOTE]
   >
   >Se si configurano utenti per OpenOffice, il numero di istanze di OpenOffice non può essere maggiore del numero di account utente specificato in questo passaggio.

1. Riavviare il server dei moduli.

### Rimuovere un utente dall&#39;elenco utilizzato per le conversioni di file multithread {#remove-a-user-from-the-list-used-for-multi-threaded-file-conversions}

1. Nella console di amministrazione, fare clic su Servizi > PDF Generator > Account utente.
1. Fate clic sulla casella accanto all’utente che desiderate rimuovere e fate clic su Elimina.
1. Nella pagina di conferma, fate clic su Elimina.
1. Riavviare il server dei moduli.

### Modificare la password di un account {#change-the-password-for-an-account}

1. Nella console di amministrazione, fare clic su Servizi > PDF Generator > Account utente.
1. Fate clic sul nome utente, quindi immettete e confermate la nuova password. Questa password deve corrispondere alla password di sistema dell&#39;utente.

