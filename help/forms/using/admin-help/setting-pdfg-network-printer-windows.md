---
title: Configurazione di una stampante di rete PDFG (solo Windows)
description: Scopri come configurare una stampante di rete PDFG ( solo Windows )
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: c3fc159e-2677-4b71-b0b2-2feaf69e1a32
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 0%

---

# Configurazione di una stampante di rete PDFG (solo Windows) {#setting-up-a-pdfg-network-printer-windows-only}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

La stampante di rete PDFG consente agli utenti di generare un documento PDF da qualsiasi applicazione che supporti la stampa. Dopo l&#39;installazione della stampante di rete PDFG da parte di un utente, nella sezione Stampanti del Pannello di controllo Campaign Windows verrà visualizzata una nuova stampante denominata *PDF generator*. Se esiste già una stampante con lo stesso nome, all&#39;utente viene richiesto di specificare un altro nome.

La stampa su questa stampante da qualsiasi applicazione invia il documento (in formato PostScript) a PDF Generator, che converte il file PostScript in PDF. A seconda della configurazione di PDF Generator, il documento PDF PDF viene inviato all&#39;utente come allegato di un messaggio e-mail, inoltrato a un servizio o processo AEM Forms specifico oppure vengono eseguite entrambe le azioni.

Per configurare una stampante di rete PDFG sono necessari i seguenti passaggi:

1. Configurare le impostazioni e-mail. (Vedi [Configurare le impostazioni e-mail per la stampante di rete PDFG](setting-pdfg-network-printer-windows.md#configure-email-settings-for-pdfg-network-printer).)
1. Nella console di amministrazione, configurare le impostazioni della stampante di rete PDFG. (Vedere [Configurare le impostazioni della stampante di rete PDFG](setting-pdfg-network-printer-windows.md#configure-the-pdfg-network-printer-settings).)
1. Assicurati che gli utenti siano configurati con un indirizzo e-mail valido nel database dei moduli AEM e assegna l’autorizzazione PDFGUser a ogni utente. <!-- Fix broken link See Setting up and organizing users -->
1. Verificare che JRE6 a 32 bit sia installato nei computer degli utenti.
1. Installare la stampante nei computer degli utenti. (Vedi [Installare la stampante di rete PDFG sul computer di un utente](setting-pdfg-network-printer-windows.md#install-pdfg-network-printer-on-a-user-s-computer).)

## Configura impostazioni e-mail per stampante di rete PDFG {#configure-email-settings-for-pdfg-network-printer}

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione servizi.
1. Nella pagina Gestione servizi fare clic su provider.email_sendmail_service, specificare le impostazioni SMTP e fare clic su Salva.

## Configurare le impostazioni della stampante di rete PDFG {#configure-the-pdfg-network-printer-settings}

1. Nella console di amministrazione, fare clic su Servizi > PDF Generator > Stampante di rete PDFG
1. Negli elenchi Impostazioni di Adobe PDF e Impostazioni di sicurezza, seleziona le opzioni da applicare al PDF generato. Per informazioni dettagliate su queste impostazioni, vedere [Configurazione delle impostazioni di Adobe PDF](/help/forms/using/admin-help/configuring-pdf-settings.md#configuring-adobe-pdf-settings) e [Configurazione delle impostazioni di sicurezza](/help/forms/using/admin-help/configuring-security-settings.md#configuring-security-settings).
1. Per inviare nuovamente i PDF convertiti agli utenti, selezionare l&#39;opzione Restituisci all&#39;utente il file di PDF convertito e specificare le informazioni seguenti:

   * Indirizzo e-mail da utilizzare per inviare PDF agli utenti
   * Oggetto del messaggio e-mail
   * Intestazione, corpo e piè di pagina del messaggio e-mail. Nel messaggio e-mail, &lt;receiverName> viene sostituito con il nome completo dell&#39;utente che ha stampato il documento.

1. Per inviare i PDF convertiti a un servizio o a un processo di AEM Forms, selezionare l&#39;opzione Inoltra il PDF convertito al servizio o processo di AEM Forms specificato e specificare le informazioni seguenti:

   * Nome del servizio da richiamare
   * Nome dell&#39;operazione del servizio da richiamare
   * Nome del parametro di input, come specificato nel file component.xml del servizio o del processo. Il documento PDF viene utilizzato come valore per il parametro di input.

1. Fai clic su Salva.

Se si desidera ripristinare il testo predefinito originale dell&#39;e-mail, fare clic su Ripristina contenuto posta elettronica.

## Installare la stampante di rete PDFG sul computer di un utente {#install-pdfg-network-printer-on-a-user-s-computer}

Gli utenti che hanno il ruolo Amministratore PDFG o Utente PDFG possono installare una stampante di rete PDFG. Sul computer deve essere installato un JDK a 32 bit.

1. (Amministratori PDFG) Nella console di amministrazione, fai clic su Servizi > PDF Generator > Stampante di rete PDFG.

   (Utenti PDFG) Andare a `http(s)://[host]:'port'/pdfgui` e fare clic sul collegamento in Installazione stampante di rete PDFG.

1. In Installazione stampante di rete PDFG, fare clic sul collegamento. Quando vengono richieste informazioni sull&#39;account utente, specificare il nome utente e la password utilizzati nel passaggio 1 per l&#39;accesso. Viene visualizzato un messaggio che indica che la stampante è stata installata correttamente.

   ***nota **: se la password dell&#39;utente cambia, gli utenti devono reinstallare la stampante di rete PDFG sui propri computer. Impossibile aggiornare la password dalla console di amministrazione.*

1. Fare clic su OK.
