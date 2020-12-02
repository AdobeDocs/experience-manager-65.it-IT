---
title: Utilizzo dell'API sendToPrinter
seo-title: Utilizzo dell'API sendToPrinter
description: Utilizzo del servizio sendToPrinter per inviare un documento alla stampante.
seo-description: Utilizzo del servizio sendToPrinter per inviare un documento alla stampante.
uuid: c6a3fe8d-ec19-4350-b4a6-4c3d1971b501
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: c2d564ba-fa5a-4130-b7fe-7e2c64d92170
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 13%

---


# Utilizzo dell&#39;API sendToPrinter {#using-the-sendtoprinter-api}

## Panoramica {#overview}

In  AEM Forms, è possibile utilizzare il servizio SendToPrinter per inviare un documento alla stampante. Il servizio SendToPrinter supporta i seguenti meccanismi di accesso alla stampa:

* **Stampante con accesso diretto** `: A printer that is installed on the same computer is called a direct accessible printer, and the computer is named printer host. This type of printer can be a local printer that is connected to the computer directly.`

* **Stampante con accesso indiretto** `: The printer that is installed on a print server is accessed from other computers. Technologies such as the common UNIX® printing system (CUPS) and the Line Printer Daemon (LPD) protocol are available to connect to a network printer. To access an indirect accessible printer, specify the print server’s IP or host name. Using this mechanism, you can send a document to an LPD URI when the network has an LPD running. The mechanism lets you route the document to any printer that is connected to the network that has an LPD running.`

   Quando si invia un documento a una stampante, specificare uno dei seguenti protocolli di stampa:

   * **CUPS** `: A printing protocol named common UNIX printing system. This protocol is used for UNIX operating systems and enables a computer to function as a print server. The print server accepts print requests from client applications, processes them, and sends them to configured printers. On the IBM AIX® operating system, usage of CUPS is not recommended.`
   * &quot;**DirectIP** `: A standard protocol for remote printing and managing print jobs. This protocol can be used locally or remotely. Print queues are not required.`
   * &quot;**LPD** `: A printing protocol named Line Printer Daemon protocol or Line Printer Remote (LPR) protocol. This protocol provides network print server functionality for UNIX-based systems.`
   * **SharedPrinter** `: A printing protocol that enables a computer to use a printer that is configured for that computer.`
   * **CIFS**: Il servizio Output supporta il protocollo CIFS (Common Internet File System) per la stampa.

## Utilizzo di SendToPrinter Service {#using-sendtoprinter-service}

La tabella seguente elenca:

* informazioni su printerName o printServer da utilizzare per vari protocolli.
* valore o eccezione restituito da una stampante per diverse combinazioni di URI Server stampante e Nome della stampante

| Protocollo (meccanismo di accesso) | URI del server di stampa (PrinterSpec.printServer) | Nome della stampante (PrinterSpec.printerName) | Risultato |
|--- |--- |--- |--- |
| SharedPrinter | Qualsiasi | Vuoto | Eccezione: L&#39;argomento richiesto sPrinterName non può essere vuoto. |
| SharedPrinter | Qualsiasi | Non valido | Un&#39;eccezione indica che la stampante non è stata trovata. |
| SharedPrinter | Qualsiasi | Valido | Processo di stampa completato. |
| LPD | Vuoto | Qualsiasi | un&#39;eccezione che indica che l&#39;argomento richiesto sPrintServerUri non può essere vuoto. |
| LPD | Non valido | Vuoto | un&#39;eccezione che indica che l&#39;argomento richiesto sPrinterName non può essere vuoto. |
| LPD | Non valido | Non vuoto | eccezione che indica che sPrintServerUri non è stato trovato. |
| LPD | Valido | Non valido | eccezione che indica che la stampante non è stata trovata. |
| LPD | Valido | Valido | Un processo di stampa di successo. |
| CUPS | Vuoto | Qualsiasi | un&#39;eccezione che indica che l&#39;argomento richiesto sPrintServerUri non può essere vuoto. |
| CUPS | Non valido | Qualsiasi | eccezione che indica che la stampante non è stata trovata. |
| CUPS | Valido | Qualsiasi | Processo di stampa completato. |
| DirectIP | Vuoto | Qualsiasi | un&#39;eccezione che indica che l&#39;argomento richiesto sPrintServerUri non può essere vuoto. |
| DirectIP | Non valido | Qualsiasi | eccezione che indica che la stampante non è stata trovata. |
| DirectIP | Valido | Qualsiasi | Processo di stampa completato. |
| CIFS | Valido | Vuoto | Processo di stampa completato. |
| CIFS | Non valido | Qualsiasi | errore sconosciuto durante la stampa tramite CIFS. |
| CIFS | Vuoto | Qualsiasi | un&#39;eccezione che indica che l&#39;argomento richiesto sPrintServerUri non può essere vuoto. |

## Supporto per l&#39;autenticazione {#authentication-support}

L&#39;autenticazione è supportata solo per la stampa CIFS. Per eseguire l&#39;autenticazione, specificare il nome utente/password/dominio in PrinterSpec. È possibile crittografare una password utilizzando AEM Granite CyprusSupport Service eseguendo i seguenti passaggi:

1. Andate a https://&lt;server>:&lt;porta>/sistema/console.

1. Andate a **[!UICONTROL Main]** > **[!UICONTROL Crypto Support]**.

1. Inserite del testo normale e fate clic su **[!UICONTROL Protect]**.

