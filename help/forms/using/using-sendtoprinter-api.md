---
title: Utilizzo dell'API sendToPrinter
seo-title: Using the sendToPrinter API
description: Utilizzo del servizio sendToPrinter per l'invio di un documento alla stampante.
seo-description: Using the sendToPrinter service to send a document to printer.
uuid: c6a3fe8d-ec19-4350-b4a6-4c3d1971b501
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: c2d564ba-fa5a-4130-b7fe-7e2c64d92170
exl-id: 5fb38afd-7517-494e-b084-1fdd4aef3ca4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 14%

---

# Utilizzo dell&#39;API sendToPrinter {#using-the-sendtoprinter-api}

## Panoramica {#overview}

In AEM Forms, è possibile utilizzare il servizio SendToPrinter per inviare un documento alla stampante. Il servizio SendToPrinter supporta i seguenti meccanismi di accesso alla stampa:

* **Stampante con accesso diretto** `: A printer that is installed on the same computer is called a direct accessible printer, and the computer is named printer host. This type of printer can be a local printer that is connected to the computer directly.`

* **Stampante con accesso indiretto** `: The printer that is installed on a print server is accessed from other computers. Technologies such as the common UNIX® printing system (CUPS) and the Line Printer Daemon (LPD) protocol are available to connect to a network printer. To access an indirect accessible printer, specify the print server’s IP or host name. Using this mechanism, you can send a document to an LPD URI when the network has an LPD running. The mechanism lets you route the document to any printer that is connected to the network that has an LPD running.`

   Quando si invia un documento a una stampante, specificare uno dei seguenti protocolli di stampa:

   * **CUPS** `: A printing protocol named common UNIX printing system. This protocol is used for UNIX operating systems and enables a computer to function as a print server. The print server accepts print requests from client applications, processes them, and sends them to configured printers. On the IBM AIX® operating system, usage of CUPS is not recommended.`
   * &quot;**DirectIP** `: A standard protocol for remote printing and managing print jobs. This protocol can be used locally or remotely. Print queues are not required.`
   * &quot;**LPD** `: A printing protocol named Line Printer Daemon protocol or Line Printer Remote (LPR) protocol. This protocol provides network print server functionality for UNIX-based systems.`
   * **SharedPrinter** `: A printing protocol that enables a computer to use a printer that is configured for that computer.`
   * **CIFS**: Il servizio Output supporta il protocollo di stampa CIFS (Common Internet File System).

## Utilizzo del servizio SendToPrinter {#using-sendtoprinter-service}

La tabella seguente elenca:

* informazioni su printerName o printServer da utilizzare per vari protocolli.
* valore o eccezione restituita da una stampante per diverse combinazioni di URI del server stampanti e Nome della stampante

| Protocollo (meccanismo di accesso) | URI server di stampa (PrinterSpec.printServer) | Nome della stampante (PrinterSpec.printerName) | Risultato |
|--- |--- |--- |--- |
| SharedPrinter | Qualsiasi | Vuoto | Eccezione: L&#39;argomento richiesto sPrinterName non può essere vuoto. |
| SharedPrinter | Qualsiasi | Non valido | Un&#39;eccezione indica che la stampante non è stata trovata. |
| SharedPrinter | Qualsiasi | Valido | Processo di stampa riuscito. |
| LPD | Vuoto | Qualsiasi | eccezione che indica che l&#39;argomento richiesto sPrintServerUri non può essere vuoto. |
| LPD | Non valido | Vuoto | un&#39;eccezione che indica che l&#39;argomento richiesto sPrinterName non può essere vuoto. |
| LPD | Non valido | Non vuoto | eccezione che indica che sPrintServerUri non è stato trovato. |
| LPD | Valido | Non valido | eccezione che indica che la stampante non è stata trovata. |
| LPD | Valido | Valido | Un processo di stampa riuscito. |
| CUPS | Vuoto | Qualsiasi | eccezione che indica che l&#39;argomento richiesto sPrintServerUri non può essere vuoto. |
| CUPS | Non valido | Qualsiasi | eccezione che indica che la stampante non è stata trovata. |
| CUPS | Valido | Qualsiasi | Processo di stampa riuscito. |
| DirectIP | Vuoto | Qualsiasi | eccezione che indica che l&#39;argomento richiesto sPrintServerUri non può essere vuoto. |
| DirectIP | Non valido | Qualsiasi | eccezione che indica che la stampante non è stata trovata. |
| DirectIP | Valido | Qualsiasi | Processo di stampa riuscito. |
| CIFS | Valido | Vuoto | Processo di stampa riuscito. |
| CIFS | Non valido | Qualsiasi | errore sconosciuto durante la stampa tramite CIFS. |
| CIFS | Vuoto | Qualsiasi | eccezione che indica che l&#39;argomento richiesto sPrintServerUri non può essere vuoto. |

## Supporto per l&#39;autenticazione {#authentication-support}

L&#39;autenticazione è supportata solo per la stampa CIFS. Per eseguire l&#39;autenticazione, specificare il nome utente/password/dominio in PrinterSpec. È possibile crittografare una password utilizzando AEM servizio Granite CyprusSupport eseguendo i seguenti passaggi:

1. Vai su https://&lt;server>:&lt;port>/system/console.

1. Vai a **[!UICONTROL Principale]** > **[!UICONTROL Supporto di Crypto]**.

1. Inserisci un testo normale e fai clic su **[!UICONTROL Protect]**.
