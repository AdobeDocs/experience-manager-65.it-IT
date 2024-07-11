---
title: Hotfix per AEM Forms
description: Informazioni su come scaricare e installare un hotfix per AEM Forms.
exl-id: 37287332-3c8d-4ddc-a77e-3c5ee332898b
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: fb689e86deaabcc4033ed75f615086b630a9a525
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 1%

---

# Hotfix per Adobe Experience Manager Forms{#aem-form-hotfix}

In questo articolo sono elencate le correzioni critiche implementate per risolvere problemi noti, migliorare la stabilità del sistema e migliorare le prestazioni complessive di AEM Forms.

>[!NOTE]
>
> Gli hotfix sono progettati per essere cumulativi e comprendono tutte le correzioni precedenti. Quando applichi l’aggiornamento rapido più recente a una versione, questo non solo risolve il problema più recente, ma incorpora anche tutte le correzioni di bug e i miglioramenti precedenti.

## Hotfix per Adaptive Forms {#hotfix-for-adaptive-forms}

<table>
  <tbody>
  <tr>
    <td><strong>Data</strong></td>
    <td><strong>Collegamento per il download degli hotfix (collegamento per la distribuzione di software AEM)</strong></td>
    <td><strong>Problemi risolti</strong></td>
  </tr>
  <tr>
    <td>giovedì 10 luglio 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/jboss/win/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-windows-jboss.zip.zip">Hotfix per AEM Service Pack 6.5.21.0 su Windows per il server JEE JBoss </a> </li>
      <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/jboss/linux/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-linux-jboss.tar.gz">Hotfix per AEM Service Pack 6.5.21.0 su Linux per il server JEE JBoss </a> </li>
       <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/websphere/win/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-windows-websphere.zip.zip">Hotfix per AEM Service Pack 6.5.21.0 su Windows per il server JEE di Webstore </a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/websphere/linux/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-linux-websphere.tar.gz">Hotfix per AEM Service Pack 6.5.21.0 su Linux per il server JEE di Webstore</a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/weblogic/win/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-windows-weblogic.zip.zip">Hotfix per AEM Service Pack 6.5.21.0 su Windows per il server JEE Weblogic </a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/weblogic/linux/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-linux-weblogic.tar.gz">Hotfix per AEM Service Pack 6.5.21.0 su Linux per il server JEE Weblogic</a> </li>
     </ul>
     </td>
    <td>
    <ul><li>Quando un utente si aggiorna a AEM Forms Service Pack 20 (6.5.20.0) sul server JEE e genera PDF utilizzando i servizi di output, i PDF presentano problemi di accessibilità. (LC-3922112)</li><li>I PDF con tag generati utilizzando il servizio di output su AEM Forms JEE mostrano un avviso di struttura inappropriata. (LC-3922038)</li><li>Quando un modulo viene inviato in AEM Forms JEE, le istanze di un elemento XML ripetuto vengono rimosse dai dati. (LC-3922017)</li><li>Quando un utente in un ambiente Linux esegue il rendering di un modulo adattivo (su JEE) in HTML, il rendering non riesce. (LC-3921957)</li><li>Quando un utente converte un file XTG in formato PostScript utilizzando il servizio di output in AEM Forms JEE, l’operazione non riesce e viene visualizzato l’errore: AEM_OUT_001_003: Eccezione imprevista: errore PAExecute: XFA_RENDER_FAILURE. (LC-3921720)</li><li>Dopo l’aggiornamento ad AEM Forms Service Pack 18 (6.5.18.0) sul server JEE, quando un utente invia un modulo, non riesce a eseguire il rendering di HTML5 o PDF forms e XMLFM si arresta. (LC-3921718)
    </ul>
    </td>    
  </tr>
  <tr>
    <td>sabato 21 giugno 2024</td>
     <td>
     <ul>
     <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">Hotfix per AEM Service Pack 6.5.21.0 sul server JEE JBoss </a> </li>
      <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">Hotfix per AEM Service Pack 6.5.21.0 nel server Weblogic JEE </a> </li>
       <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">Hotfix per AEM Service Pack 6.5.21.0 sul server WebShpere JEE </a> </li>
        <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">Hotfix per AEM Service Pack 6.5.21.0 sul server OSGi </a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li> Dopo l'aggiornamento a AEM Forms Service Pack 6.5.21.0, il servizio PaperCapture non è in grado di eseguire operazioni OCR (riconoscimento ottico dei caratteri) sui PDF. Per le istruzioni di installazione, consultare <a href="/help/forms/using/papercapture-service-resolution.md"> risoluzione dei problemi</a> articolo.(CQDOC-21680) </li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>sabato 21 giugno 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2Fccm-ccr-content-10.0.206.zip">Hotfix per AEM Service Pack 6.5.21.0 </a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>Le lettere bozza con dati XML si bloccano nello stato di caricamento durante l'anteprima. Per le istruzioni di download e installazione dell’hotfix, consulta<a href="#install-hotfix"> Scarica e installa l’hotfix per il problema della bozza di lettera</a> sezione.(FORMS-14521)</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>venerdì 16 maggio 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-win-pkg-6.0.1192-010.zip">Hotfix per AEM Service Pack 6.5.20.0 per Microsoft Windows</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1192-010.zip">Hotfix per AEM Service Pack 6.5.20.0 per Linux </a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-osx-pkg-6.0.1192-010.zip">Hotfix per AEM Service Pack 6.5.20.0 per Apple macOS</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>In un modulo adattivo basato su un XDP con script incorporati nelle caselle di controllo, gli script non vengono eseguiti per gli elementi che seguono tali caselle di controllo. Per questo problema è disponibile un hotfix. (FORMS-14244) </li>
     <li> Le righe nel widget del selettore data vengono troncate quando si attraversano i mesi nel widget popup per i campi con pattern di modifica/visualizzazione. Per questo problema è disponibile un hotfix. (FORMS-13620) </li>
     <li>L’invio dei moduli non riesce quando si tenta di utilizzare il servizio DOR (Document of Record) nel back-end. Messaggio di errore: "Impossibile completare l'azione di invio perché la risorsa del modulo non è assegnata correttamente". (FORMS-13798) </li>
     <li>Quando un modulo adattivo viene inviato da un’istanza di Adobe Experience Manager Publish a un flusso di lavoro di Adobe Experience Manager, il flusso di lavoro non riesce a salvare gli allegati.  (FORMS-14209) </li>
     <li> Durante l’installazione del pacchetto AEM 6.5 Forms Service Pack 20 (pacchetto del componente aggiuntivo AEM Forms per SP20), l’interfaccia utente di AEM Sites presenta un significativo deterioramento delle prestazioni.  (FORMS-13791) </li>
     <li>Il servizio di precompilazione ha esito negativo con un’eccezione NPE nelle comunicazioni interattive. (CQDOC-21355)</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>martedì 29 gennaio 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fforms-foundation-qs-content-4.0.170-FORMS-12692-B0001.zip">Hotfix per AEM Service Pack 6.5.19.0 per Windows sul server JEE</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>In AEM Forms sul server JEE, il Forms HTML5 che utilizza il percorso di contesto non riesce a eseguire il rendering. (FORMS-12485, FORMS-12691).</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>martedì 29 gennaio 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-win-pkg-6.0.1016-004.zip">Hotfix per AEM Service Pack 6.5.18.0 per Microsoft Windows</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-linux-pkg-6.0.1016-004.zip">Hotfix per AEM Service Pack 6.5.18.0 per Linux</a></li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-osx-pkg-6.0.1016-004.zip">Hotfix per AEM Service Pack 6.5.18.0 per Apple macOS</a></li>
     </ul>
     </td>
    <td>
    <ul>
    <li> Il componente preconfigurato Firma a mano non riesce a eseguire il rendering per un’anteprima in un modulo adattivo. (FORMS-12073)</li>
    </ul>
    </td>    
   </tr>
   <tr>
    <td>martedì 20 novembre 2023</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1016-002.zip">Hotfix per AEM Service Pack 6.5.18.0 per Linux</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-win-pkg-6.0.1016-002.zip">Hotfix per AEM Service Pack 6.5.18.0 per Microsoft Windows</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-osx-pkg-6.0.1016-002.zip">Hotfix per AEM Service Pack 6.5.18.0 per Apple macOS</a></li>
     </ul>
     </td>
    <td>
    <ul>
    <li>La firma in linea non funziona più quando viene impostato un URL di reindirizzamento nel contenitore della guida di un modulo adattivo. (FORMS-10493)</li>
    <li>Non è possibile pubblicare i modelli del documento record (DoR) per Adaptive Forms localizzato. (FORMS-10535)</li>
    <li>La comunicazione interattiva con immagini in linea di grandi dimensioni non si apre correttamente in modalità di modifica. (FORMS-10578)</li>
    </ul>
    </td>    
  </tr>
  <tbody>
</table>

## Scaricare e installare un Hotfix {#download-install-hotfix}

Per scaricare e installare l’Hotfix, effettua le seguenti operazioni:

1. Scarica [Hotfix](#hotfix-for-adaptive-forms) dal collegamento Software Distribution.
1. Estrai il file di archivio Hotfix per ottenere un pacchetto Experience Manager (.zip) e i file bundle (.jar).
1. Carica e installa il pacchetto (.zip) tramite [Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=es#accessing).
1. Apri i bundle di Gestione configurazione `https://server:host/system/console/bundles`, carica e installa il bundle (.jar). L&#39;aggiornamento rapido è installato.


## Scarica e installa l’hotfix per il problema della bozza di lettera {#install-hotfix}

Per risolvere il problema, effettuare le seguenti operazioni:

1. Scarica il file [hotfix](#hotfix-for-adaptive-forms) dal portale di distribuzione software.
2. Carica e installa il pacchetto (.zip) utilizzando [Gestione pacchetti CRX](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=es#accessing).