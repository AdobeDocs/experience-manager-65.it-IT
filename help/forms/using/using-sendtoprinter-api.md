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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 516393bc-fa69-5e74-a04e-f7ec9ffe2c5e
    internal-label: APIs & Integrations
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: f19cff18-c8cc-4a4b-adad-85dd2fa3dbe2
    internal-label: Document Services
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 16%
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
  * **CIFS**: il servizio di output supporta il protocollo CIFS (Common Internet File System).

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
| CIFS | Non valido | Qualsiasi | errore sconosciuto durante la stampa con CIFS. |
| CIFS | Vuoto | Qualsiasi | eccezione che indica che l&#39;argomento obbligatorio sPrintServerUri non può essere vuoto. |

## Supporto per l’autenticazione {#authentication-support}

L&#39;autenticazione è supportata solo per la stampa CIFS. Per eseguire l&#39;autenticazione, specificare il nome utente/password/dominio in PrinterSpec. È possibile crittografare una password utilizzando il servizio AEM Granite CyprtoSupport eseguendo le seguenti operazioni:

1. Visitare il sito Web all&#39;indirizzo https://&lt;server>:&lt;porta>/system/console.

1. Vai a **[!UICONTROL Principale]** > **[!UICONTROL Supporto crittografia]**.

1. Immettere testo normale e fare clic su **[!UICONTROL Proteggi]**.
