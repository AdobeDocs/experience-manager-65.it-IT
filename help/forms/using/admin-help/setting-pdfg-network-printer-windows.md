---
title: Configurazione di una stampante di rete PDFG (solo Windows)
seo-title: Configurazione di una stampante di rete PDFG (solo Windows)
description: Come impostare una stampante di rete PDFG (solo Windows)
seo-description: Come impostare una stampante di rete PDFG (solo Windows)
uuid: 13b8481e-5ef0-4a07-9602-7bc4d9e05dd4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7620e5e4-022e-49b2-8cfe-d5eec8ab99d7
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Configurazione di una stampante di rete PDFG (solo Windows) {#setting-up-a-pdfg-network-printer-windows-only}

La stampante di rete PDFG consente agli utenti di generare un documento PDF da qualsiasi applicazione che supporti la stampa. Dopo l&#39;installazione della stampante di rete PDFG da parte di un utente, nella sezione Stampanti del Pannello di controllo di Windows viene visualizzata una nuova stampante denominata *PDF generator* . Se esiste già una stampante con lo stesso nome, all&#39;utente viene richiesto di fornire un altro nome.

La stampa su questa stampante da qualsiasi applicazione invia il documento (in formato PostScript) a PDF Generator, che converte il file PostScript in PDF. A seconda della configurazione di PDF Generator, il documento PDF viene inviato all’utente come allegato a un messaggio e-mail, inviato a un determinato servizio o processo di moduli AEM, oppure viene eseguita entrambe le azioni.

Per configurare una stampante di rete PDFG è necessario effettuare le seguenti operazioni:

1. Configurare le impostazioni e-mail. (vedere [Configurare le impostazioni e-mail per la stampante](setting-pdfg-network-printer-windows.md#configure-email-settings-for-pdfg-network-printer)di rete PDFG).
1. Nella console di amministrazione, configurare le impostazioni della stampante di rete PDFG. (vedere [Configurare le impostazioni](setting-pdfg-network-printer-windows.md#configure-the-pdfg-network-printer-settings)della stampante di rete PDFG).
1. Verifica che i tuoi utenti siano configurati con un indirizzo e-mail valido nel database dei moduli AEM e assegna il PDFGUserPermission a ciascun utente. <!-- Fix broken link See Setting up and organizing users -->
1. Verificate che JRE6 a 32 bit sia installato sui computer degli utenti.
1. Installare la stampante sui computer degli utenti. (vedere [Installare la stampante di rete PDFG sul computer](setting-pdfg-network-printer-windows.md#install-pdfg-network-printer-on-a-user-s-computer)di un utente).

## Configurare le impostazioni e-mail per la stampante di rete PDFG {#configure-email-settings-for-pdfg-network-printer}

1. Nella console di amministrazione, fai clic su Servizi > Applicazioni e servizi > Gestione dei servizi.
1. Nella pagina Gestione dei servizi, fate clic su provider.email_sendmail_service, specificate le impostazioni SMTP e fate clic su Salva.

## Configurare le impostazioni della stampante di rete PDFG {#configure-the-pdfg-network-printer-settings}

1. Nella console di amministrazione, fare clic su Servizi > PDF Generator > PDFG Network Printer
1. Negli elenchi Impostazioni Adobe PDF e Impostazioni di protezione, selezionare le opzioni da applicare al PDF generato. Per informazioni dettagliate su queste impostazioni, consultate [Configurazione delle impostazioni](/help/forms/using/admin-help/configuring-pdf-settings.md#configuring-adobe-pdf-settings) Adobe PDF e [Configurazione delle impostazioni](/help/forms/using/admin-help/configuring-security-settings.md#configuring-security-settings)di protezione.
1. Per restituire i PDF convertiti agli utenti, selezionare l&#39;opzione Invia nuovamente all&#39;utente il file PDF convertito per e-mail e specificare le informazioni seguenti:

   * Indirizzo e-mail da utilizzare per inviare PDF agli utenti
   * Oggetto del messaggio e-mail
   * Intestazione, corpo e piè di pagina del messaggio e-mail. Nel messaggio e-mail, &lt;ricevitoreName> viene sostituito con il nome completo dell&#39;utente che ha stampato il documento.

1. Per inviare i PDF convertiti a un servizio o a un processo di elaborazione moduli AEM, selezionare l&#39;opzione Inoltra il PDF convertito al servizio o al processo moduli AEM specificato e specificare le informazioni seguenti:

   * Nome del servizio da richiamare
   * Nome dell&#39;operazione del servizio da richiamare
   * Il nome del parametro di input, come specificato nel file component.xml del servizio o del processo. Il documento PDF verrà utilizzato come valore per tale parametro di input.

1. Fate clic su Salva.

Per ripristinare il testo predefinito originale dell’e-mail, fare clic su Ripristina contenuto e-mail.

## Installare la stampante di rete PDFG sul computer di un utente {#install-pdfg-network-printer-on-a-user-s-computer}

Gli utenti che hanno il ruolo di amministratore PDFG o utente PDFG possono installare una stampante di rete PDFG. Sul computer deve essere installato un JDK a 32 bit.

1. (Amministratori PDFG) Nella console di amministrazione, fare clic su Servizi > Generatore PDF > Stampante di rete PDFG.

   (Utenti PDFG) Fare clic sul collegamento `http(s)://[host]:'port'/pdfgui` nella sezione Installazione della stampante di rete PDFG.

1. In Installazione stampante di rete PDFG fare clic sul collegamento. Quando viene richiesto di fornire informazioni sull&#39;account utente, specificate il nome utente e la password utilizzati al punto 1 per l&#39;accesso. Viene visualizzato un messaggio che indica che la stampante è stata installata correttamente.

   ***nota **: Se la password dell&#39;utente cambia, gli utenti dovranno reinstallare la stampante di rete PDFG sui propri computer. Non è possibile aggiornare la password dalla console di amministrazione.*

1. Fate clic su OK.

