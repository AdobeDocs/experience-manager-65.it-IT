---
title: Impostazione di una stampante di rete PDFG (solo Windows)
description: Scopri come impostare una stampante di rete PDFG (solo Windows)
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: c3fc159e-2677-4b71-b0b2-2feaf69e1a32
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '616'
ht-degree: 100%

---

# Impostazione di una stampante di rete PDFG (solo Windows) {#setting-up-a-pdfg-network-printer-windows-only}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

La stampante di rete PDFG consente agli utenti di generare un documento PDF da qualsiasi applicazione che supporti la stampa. Dopo l’installazione della stampante di rete PDFG da parte di un utente, nella sezione Stampanti del Pannello di controllo di Windows verrà visualizzata una nuova stampante denominata *PDF Generator*. Se esiste già una stampante con lo stesso nome, all’utente viene richiesto di specificare un altro nome.

La stampa su questa stampante da qualsiasi applicazione invia il documento (in formato PostScript) a PDF Generator, che converte il file PostScript in PDF. A seconda della configurazione di PDF Generator, il documento PDF viene inviato all’utente come allegato di un messaggio e-mail, inoltrato a un servizio o processo di AEM Forms specifico oppure vengono eseguite entrambe le azioni.

Per impostare una stampante di rete PDFG sono necessari i seguenti passaggi:

1. Configura le impostazioni e-mail. Consulta [Configurare le impostazioni e-mail per la stampante di rete PDFG](setting-pdfg-network-printer-windows.md#configure-email-settings-for-pdfg-network-printer).
1. Nella console di amministrazione, configura le impostazioni della stampante di rete PDFG. Consulta [Configurare le impostazioni della stampante di rete PDFG](setting-pdfg-network-printer-windows.md#configure-the-pdfg-network-printer-settings).
1. Assicurati che gli utenti siano configurati con un indirizzo e-mail valido nel database di AEM Forms e assegna PDFGUserPermission a ogni utente. <!-- Fix broken link See Setting up and organizing users -->
1. Verifica che JRE6 a 32 bit sia installato nei computer degli utenti.
1. Installa la stampante nei computer degli utenti. Consulta [Installare la stampante di rete PDFG sul computer di un utente](setting-pdfg-network-printer-windows.md#install-pdfg-network-printer-on-a-user-s-computer).

## Configurare le impostazioni e-mail per la stampante di rete PDFG {#configure-email-settings-for-pdfg-network-printer}

1. Nella console di amministrazione, fai clic su Servizi > Applicazioni e servizi > Gestione servizi.
1. Nella pagina Gestione servizi, fai clic su provider.email_sendmail_service, specifica le impostazioni SMTP e fai clic su Salva.

## Configurare le impostazioni della stampante di rete PDFG {#configure-the-pdfg-network-printer-settings}

1. Nella console di amministrazione, fai clic su Servizi > PDF Generator > Stampante di rete PDFG
1. Negli elenchi Impostazioni di Adobe PDF e Impostazioni di sicurezza, seleziona le opzioni da applicare al PDF generato. Per informazioni dettagliate su queste impostazioni, consulta [Configurazione delle impostazioni di Adobe PDF](/help/forms/using/admin-help/configuring-pdf-settings.md#configuring-adobe-pdf-settings) e [Configurazione delle impostazioni di sicurezza](/help/forms/using/admin-help/configuring-security-settings.md#configuring-security-settings).
1. Per inviare nuovamente i PDF convertiti agli utenti, seleziona l’opzione Restituisci all’utente il file PDF convertito e specifica le informazioni seguenti:

   * Indirizzo e-mail da utilizzare per inviare i PDF agli utenti
   * L’oggetto del messaggio e-mail
   * L’intestazione, corpo e piè di pagina del messaggio e-mail. Nel messaggio e-mail, &lt;receiverName> viene sostituito con il nome completo dell’utente che ha stampato il documento.

1. Per inviare i PDF convertiti a un servizio o processo di AEM Forms, seleziona l’opzione Inoltra PDF convertito al servizio o processo di AEM Forms specificato e specifica le informazioni seguenti:

   * Il nome del servizio da richiamare
   * Il nome dell’operazione del servizio da richiamare
   * Il nome del parametro di input, come specificato nel file component.xml del servizio o del processo. Il documento PDF viene utilizzato come valore per il parametro di input.

1. Fai clic su Salva.

Se desideri ripristinare il testo predefinito originale dell’e-mail, fai clic su Ripristina contenuti e-mail.

## Installare la stampante di rete PDFG sul computer di un utente {#install-pdfg-network-printer-on-a-user-s-computer}

Gli utenti che hanno il ruolo Amministratore PDFG o Utente PDFG possono installare una stampante di rete PDFG. Sul computer deve essere installato un JDK a 32 bit.

1. (Amministratori PDFG) Nella console di amministrazione, fai clic su Servizi > PDF Generator > Stampante di rete PDFG.

   (Utenti PDFG) Vai a `http(s)://[host]:'port'/pdfgui` e fai clic sul collegamento in Installazione stampante di rete PDFG.

1. In Installazione stampante di rete PDFG, fai clic sul collegamento. Quando vengono richieste informazioni sull’account utente, specifica il nome utente e la password utilizzati nel passaggio 1 per l’accesso. Viene visualizzato un messaggio che indica che la stampante è stata installata correttamente.

   ***nota **: se la password dell’utente cambia, gli utenti devono reinstallare la stampante di rete PDFG sui relativi computer. Non puoi aggiornare la password dalla console di amministrazione.*

1. Fai clic su OK.
