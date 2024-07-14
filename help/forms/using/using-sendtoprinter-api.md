---
title: Utilizzo dell’API sendToPrinter
description: Utilizzo del servizio sendToPrinter per inviare un documento alla stampante.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
feature: Document Services,APIs & Integrations
exl-id: 585d4053-1056-4d2b-a9df-9516775afe50
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 14%

---

# Utilizzo dell’API sendToPrinter {#using-the-sendtoprinter-api}

## Panoramica {#overview}

In AEM Forms è possibile utilizzare il servizio SendToPrinter per inviare un documento alla stampante. Il servizio SendToPrinter supporta i seguenti meccanismi di accesso alla stampa:

* **Stampante con accesso diretto** `: A printer that is installed on the same computer is called a direct accessible printer, and the computer is named printer host. This type of printer can be a local printer that is connected to the computer directly.`

* **Stampante con accesso indiretto** `: The printer that is installed on a print server is accessed from other computers. Technologies such as the common UNIX® printing system (CUPS) and the Line Printer Daemon (LPD) protocol are available to connect to a network printer. To access an indirect accessible printer, specify the print server’s IP or host name. Using this mechanism, you can send a document to an LPD URI when the network has an LPD running. The mechanism lets you route the document to any printer that is connected to the network that has an LPD running.`

  Quando si invia un documento a una stampante, specificare uno dei seguenti protocolli di stampa:

   * **TAZZE** `: A printing protocol named common UNIX printing system. This protocol is used for UNIX operating systems and enables a computer to function as a print server. The print server accepts print requests from client applications, processes them, and sends them to configured printers. On the IBM AIX® operating system, usage of CUPS is not recommended.`
   * &quot;**DirectIP** `: A standard protocol for remote printing and managing print jobs. This protocol can be used locally or remotely. Print queues are not required.`
   * &quot;**LPD** `: A printing protocol named Line Printer Daemon protocol or Line Printer Remote (LPR) protocol. This protocol provides network print server functionality for UNIX-based systems.`
   * **SharedPrinter** `: A printing protocol that enables a computer to use a printer that is configured for that computer.`
   * **CIF**: il servizio di output supporta il protocollo di stampa CIF (Common Internet File System).

## Utilizzo del servizio SendToPrinter {#using-sendtoprinter-service}

La tabella seguente elenca:

* informazioni su printerName o printServer da utilizzare per vari protocolli.
* valore o eccezione restituita da una stampante per varie combinazioni di URI server della stampante e Nome della stampante

| Protocollo (meccanismo di accesso) | URI server di stampa (PrinterSpec.printServer) | Nome della stampante (PrinterSpec.printerName) | Risultato |
|--- |--- |--- |--- |
| SharedPrinter | Qualsiasi | Vuoto | Eccezione: l&#39;argomento obbligatorio sPrinterName non può essere vuoto. |
| SharedPrinter | Qualsiasi | Non valido | Un&#39;eccezione indica che non è possibile trovare la stampante. |
| SharedPrinter | Qualsiasi | Valido | Processo di stampa riuscito. |
| LPD | Vuoto | Qualsiasi | eccezione che indica che l&#39;argomento obbligatorio sPrintServerUri non può essere vuoto. |
| LPD | Non valido | Vuoto | eccezione che indica che l&#39;argomento obbligatorio sPrinterName non può essere vuoto. |
| LPD | Non valido | Non vuoto | eccezione che indica che sPrintServerUri non è stato trovato. |
| LPD | Valido | Non valido | eccezione che indica che la stampante non è stata trovata. |
| LPD | Valido | Valido | Processo di stampa riuscito. |
| CUPS | Vuoto | Qualsiasi | eccezione che indica che l&#39;argomento obbligatorio sPrintServerUri non può essere vuoto. |
| CUPS | Non valido | Qualsiasi | eccezione che indica che la stampante non è stata trovata. |
| CUPS | Valido | Qualsiasi | Processo di stampa riuscito. |
| DirectIP | Vuoto | Qualsiasi | eccezione che indica che l&#39;argomento obbligatorio sPrintServerUri non può essere vuoto. |
| DirectIP | Non valido | Qualsiasi | eccezione che indica che la stampante non è stata trovata. |
| DirectIP | Valido | Qualsiasi | Processo di stampa riuscito. |
| CIFS | Valido | Vuoto | Processo di stampa riuscito. |
| CIFS | Non valido | Qualsiasi | errore sconosciuto durante la stampa con CIF. |
| CIFS | Vuoto | Qualsiasi | eccezione che indica che l&#39;argomento obbligatorio sPrintServerUri non può essere vuoto. |

## Supporto per l’autenticazione {#authentication-support}

L&#39;autenticazione è supportata solo per la stampa CIF. Per eseguire l&#39;autenticazione, specificare il nome utente/password/dominio in PrinterSpec. È possibile crittografare una password utilizzando il servizio di supporto Cipro di AEM Granite eseguendo i seguenti passaggi:

1. Visitare il sito Web all&#39;indirizzo https://&lt;server>:&lt;porta>/system/console.

1. Vai a **[!UICONTROL Principale]** > **[!UICONTROL Supporto crittografia]**.

1. Immettere testo normale e fare clic su **[!UICONTROL Protect]**.
