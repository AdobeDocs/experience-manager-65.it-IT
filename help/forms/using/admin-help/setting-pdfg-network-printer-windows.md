---
title: Configurazione di una stampante di rete PDFG (solo Windows)
seo-title: Configurazione di una stampante di rete PDFG (solo Windows)
description: Informazioni su come impostare una stampante di rete PDFG ( solo Windows )
seo-description: Informazioni su come impostare una stampante di rete PDFG ( solo Windows )
uuid: 13b8481e-5ef0-4a07-9602-7bc4d9e05dd4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7620e5e4-022e-49b2-8cfe-d5eec8ab99d7
feature: PDF Generator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 0%

---


# Configurazione di una stampante di rete PDFG (solo Windows) {#setting-up-a-pdfg-network-printer-windows-only}

La stampante di rete PDFG consente agli utenti di generare un documento PDF da qualsiasi applicazione che supporti la stampa. Dopo che un utente installa la stampante di rete PDFG, nella sezione Stampanti del Pannello di controllo Campaign Windows viene visualizzata una nuova stampante denominata *PDF generator*. Se esiste già una stampante con lo stesso nome, all&#39;utente viene richiesto di fornire un altro nome.

La stampa su questa stampante da qualsiasi applicazione invia il documento (in formato PostScript) a PDF Generator, che converte il file PostScript in PDF. A seconda della configurazione di PDF Generator, il documento PDF viene inviato all’utente come allegato a un messaggio e-mail, inoltrato il documento PDF a uno specifico servizio o processo di moduli AEM o esegue entrambe le azioni.

Per configurare una stampante di rete PDFG sono necessari i seguenti passaggi:

1. Configura le impostazioni e-mail. (Consultare [Configurare le impostazioni e-mail per la stampante di rete PDFG](setting-pdfg-network-printer-windows.md#configure-email-settings-for-pdfg-network-printer).)
1. Nella console di amministrazione, configurare le impostazioni della stampante di rete PDFG. (Consultare [Configurare le impostazioni della stampante di rete PDFG](setting-pdfg-network-printer-windows.md#configure-the-pdfg-network-printer-settings).)
1. Verificare che gli utenti siano configurati con un indirizzo e-mail valido nel database dei moduli di AEM e assegnare il PDFGUserPermission a ciascun utente. <!-- Fix broken link See Setting up and organizing users -->
1. Assicurati che JRE6 a 32 bit sia installato sui computer degli utenti.
1. Installare la stampante sui computer degli utenti. (Consultare [Installare la stampante di rete PDFG sul computer di un utente](setting-pdfg-network-printer-windows.md#install-pdfg-network-printer-on-a-user-s-computer).)

## Configurare le impostazioni e-mail per la stampante di rete PDFG {#configure-email-settings-for-pdfg-network-printer}

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione dei servizi.
1. Nella pagina Gestione servizi fare clic su provider.email_sendmail_service, specificare le impostazioni SMTP e fare clic su Salva.

## Configurare le impostazioni della stampante di rete PDFG {#configure-the-pdfg-network-printer-settings}

1. Nella console di amministrazione, fare clic su Servizi > PDF Generator > PDFG Network Printer
1. Negli elenchi Impostazioni Adobe PDF e Impostazioni protezione , selezionare le opzioni da applicare al PDF generato. Per informazioni dettagliate su queste impostazioni, consulta [Configurazione delle impostazioni Adobe PDF](/help/forms/using/admin-help/configuring-pdf-settings.md#configuring-adobe-pdf-settings) e [Configurazione delle impostazioni di protezione](/help/forms/using/admin-help/configuring-security-settings.md#configuring-security-settings).
1. Per inviare nuovamente i PDF convertiti agli utenti, selezionare l’opzione Torna all’utente e-mail il file PDF convertito e specificare le seguenti informazioni:

   * Indirizzo e-mail da utilizzare per inviare PDF agli utenti
   * Oggetto del messaggio e-mail
   * Intestazione, corpo e piè di pagina del messaggio e-mail. Nel messaggio e-mail, &lt;ricevitoreName> viene sostituito con il nome completo dell&#39;utente che ha stampato il documento.

1. Per inviare i PDF convertiti a un servizio o a un processo di moduli AEM, selezionare l’opzione Inoltra il PDF convertito al servizio o al processo di moduli AEM specificati e specificare le informazioni seguenti:

   * Nome del servizio da richiamare
   * Nome dell&#39;operazione del servizio da richiamare
   * Il nome del parametro di input, come specificato nel file component.xml del servizio o del processo. Il documento PDF verrà utilizzato come valore per tale parametro di input.

1. Fai clic su Salva.

Se si desidera ripristinare il testo e-mail predefinito originale, fare clic su Ripristina contenuto e-mail.

## Installare la stampante di rete PDFG sul computer di un utente {#install-pdfg-network-printer-on-a-user-s-computer}

Gli utenti con il ruolo Amministratore PDFG o Utente PDFG possono installare una stampante di rete PDFG. Sul computer deve essere installato un JDK a 32 bit.

1. (Amministratori PDFG) Nella console di amministrazione, fare clic su Servizi > Generatore PDF > Stampante di rete PDFG.

   (Utenti PDFG) Vai a `http(s)://[host]:'port'/pdfgui` e fai clic sul collegamento in Installazione stampante di rete PDFG.

1. In Installazione stampante di rete PDFG fare clic sul collegamento. Quando viene richiesto di specificare le informazioni relative all&#39;account utente, specificare il nome utente e la password utilizzati al punto 1 per l&#39;accesso. Viene visualizzato un messaggio che indica che la stampante è stata installata correttamente.

   ***nota **: Se la password dell&#39;utente cambia, gli utenti dovranno reinstallare la stampante di rete PDFG sui propri computer. Non è possibile aggiornare la password dalla console di amministrazione.*

1. Fai clic su OK.

