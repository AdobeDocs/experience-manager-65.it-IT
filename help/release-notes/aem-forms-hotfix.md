---
title: Hotfix per AEM Forms
description: Informazioni su come scaricare e installare un hotfix per AEM Forms.
exl-id: 37287332-3c8d-4ddc-a77e-3c5ee332898b
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 9d5ad43703d2fb3c1d40e10578f5289510a18230
workflow-type: tm+mt
source-wordcount: '1989'
ht-degree: 2%

---

# Hotfix per Adobe Experience Manager Forms{#aem-form-hotfix}

In questo articolo sono elencate le correzioni critiche implementate per risolvere problemi noti, migliorare la stabilità del sistema e migliorare le prestazioni complessive di AEM Forms.

>[!NOTE]
>
> Gli hotfix sono progettati per essere cumulativi e comprendono tutte le correzioni precedenti. Quando applichi l’aggiornamento rapido più recente a una versione, questo non solo risolve il problema più recente, ma incorpora anche tutte le correzioni di bug e i miglioramenti precedenti.

## Hotfix per AEM Forms {#hotfix-for-aem-forms}

<table>
  <tbody>
  <tr>
    <td><strong>Data</strong></td>
    <td><strong>Collegamento per il download degli hotfix (collegamento per la distribuzione di software AEM)</strong></td>
    <td><strong>Problemi risolti</strong></td>
  </tr>
  <tr>
    <td>
      <strong>14 ottobre 2025</strong><br>
      <em>Si applica a:</em> Errore di ImgToPdf con AEM Forms SP23 Jboss Hotfix3(109)<br>
    </td>
    <td>
    <ul> Per risolvere il problema, contattare [Supporto Adobe Experience Manager Forms](https://business.adobe.com/in/support/main.html)
    </ul>
    </td>
    <td>
    <ul>
    <li> <b>(FORMS-22029):</b> Migliora l'affidabilità della conversione di PDF risolvendo un problema in cui PDF Generator (PDFG) non riesce a convertire i file immagine in PDF dopo l'aggiornamento a SP23 con Hotfix 3, causando errori imprevisti di post-elaborazione.
      <ul>
  <tr>
    <td>
      <strong>23 settembre 2025</strong><br>
    </td>
    <td>
    <ul>
    <li><strong>Jboss:</strong></li>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-23-0-hotfix-3/jboss/adobe-aem-forms-jee-hotfix3-6.5.23.0-win-jboss.zip">Hotfix3 per AEM Service Pack 6.5.23.0 su Windows per il server JEE JBoss</a></li>
    <li>Linux- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-23-0-hotfix-3/jboss/adobe-aem-forms-jee-hotfix3-6.5.23.0-linux-jboss.tar.gz">Hotfix3 per AEM Service Pack 6.5.23.0 su Linux per il server JEE JBoss</a></li>
    <li><strong>Weblogic:</strong></li>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-23-0-hotfix-3/weblogic/adobe-aem-forms-jee-hotfix3-6.5.23.0-win-weblogic.zip">Hotfix3 per AEM Service Pack 6.5.23.0 su Windows per il server JEE Weblogic</a></li>
    <li>Linux- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-23-0-hotfix-3/weblogic/adobe-aem-forms-jee-hotfix3-6.5.23.0-linux-weblogic.tar.gz">Hotfix3 per AEM Service Pack 6.5.23.0 su Linux per il server JEE Weblogic</a></li>
    <li><strong>WebSphere:</strong></li>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-23-0-hotfix-3/websphere/adobe-aem-forms-jee-hotfix3-6.5.23.0-win-websphere.zip">Hotfix3 per AEM Service Pack 6.5.23.0 su Windows per il server WebSphere JEE</a></li>
    <li>Linux- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-23-0-hotfix-3/websphere/adobe-aem-forms-jee-hotfix3-6.5.23.0-linux-websphere.tar.gz">Hotfix3 per AEM Service Pack 6.5.23.0 su Linux per il server WebSphere JEE</a></li>
    </ul>
    </td>
    <td>
    <ul>
    <strong>Questo aggiornamento rapido corregge i seguenti problemi:</strong> 
    <li> <b>(FORMS-21378):</b> È stata migliorata l'affidabilità dell'invio dei moduli grazie alla risoluzione di un problema che impediva l'invio quando la convalida lato server (SSV) è abilitata e le informazioni di Meta calcolate sono vuote.

<li> <b>(FORMS-21721):</b> È stato risolto un problema che impediva le conversioni da PS a PDF e da HTML a PDF (WebKit) dopo la distribuzione dell'aggiornamento rapido 2 in data 6.5.23.0. 
    </li>
    </ul>
    </td>    
  </tr>
    </ul>
    </td>
  <tr>
    <td>
      <strong>5 agosto 2025</strong><br>
      <em>Si applica a:</em> AEM 6.5 Forms Service Pack 23<br>
      <em>Istruzioni di installazione:</em>
      <a href="/help/forms/using/mitigating-xxe-and-configuration-vulnerabilities-for-experience-manager-forms-jee.md#option-1-for-users-on-version-65230-install-latest-hotfix">
        Mitigazione delle vulnerabilità XXE, di configurazione e di esecuzione remota del codice (CVE-2025-49533) per AEM Forms su JEE
      </a>
    </td>
    <td>
    <ul>
    <li><strong>Jboss:</strong></li>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-02/jboss/adobe-aem-forms-jee-hotfix2-6.5.23.0-win-jboss.zip">Hotfix2 per AEM Service Pack 6.5.23.0 su Windows per il server JEE JBoss</a></li>
    <li>Linux- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-02/jboss/adobe-aem-forms-jee-hotfix2-6.5.23.0-linux-jboss.tar.gz">Hotfix2 per AEM Service Pack 6.5.23.0 su Linux per il server JEE JBoss</a></li>
    <li><strong>Weblogic:</strong></li>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-02/weblogic/adobe-aem-forms-jee-hotfix2-6.5.23.0-win-weblogic.zip">Hotfix2 per AEM Service Pack 6.5.23.0 su Windows per il server JEE Weblogic</a></li>
    <li>Linux- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-02/weblogic/adobe-aem-forms-jee-hotfix2-6.5.23.0-linux-weblogic.tar.gz">Hotfix2 per AEM Service Pack 6.5.23.0 su Linux per il server JEE Weblogic</a></li>
    <li><strong>WebSphere:</strong></li>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-02/websphere/adobe-aem-forms-jee-hotfix2-6.5.23.0-win-websphere.zip">Hotfix2 per AEM Service Pack 6.5.23.0 su Windows per il server WebSphere JEE</a></li>
    <li>Linux- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-02/websphere/adobe-aem-forms-jee-hotfix2-6.5.23.0-linux-websphere.zip">Hotfix2 per AEM Service Pack 6.5.23.0 su Linux per il server WebSphere JEE</a></li>
    </ul>
    </td>
    <td>
    <ul>
    <li>Maggiore sicurezza grazie alla risoluzione di una vulnerabilità RCE (Remote Code Execution) in Adobe Experience Manager (AEM) Forms. Il problema era relativo alla modalità di sviluppo Struts nell’interfaccia utente di amministrazione, che consentiva la valutazione arbitraria di Object-Graph Navigation Language (OGNL) tramite la funzionalità di debug. Questa correzione assicura che la modalità di sviluppo Struts sia disabilitata e che vengano applicati filtri di sicurezza appropriati per impedire l’accesso non autorizzato.</li>
    <li>È stata migliorata la protezione contro le vulnerabilità XXE (Extensible Markup Language) nel modulo EDC (Electronic Document Component) di Adobe Experience Manager (AEM) Forms. Le vulnerabilità erano dovute a una gestione impropria dei documenti XML senza protezioni XXE, che poteva portare alla lettura dei file locali. La correzione include:
      <ul>
        <li>Verificare che DocumentBuilderFactory utilizzato nella classe SecurityCheckHandler sia configurato per impedire attacchi XXE.</li>
        <li>Aggiornamento del servizio Web EDC per gestire i documenti XML in modo sicuro, impedendo l'accesso non autorizzato ai file locali.</li>
      </ul>
    </li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>
      <strong>5 agosto 2025</strong><br>
      <em>Si applica a:</em> AEM 6.5 Forms Service Pack 18 - 22<br>
      <em>Istruzioni di installazione:</em>
      <a href="/help/forms/using/mitigating-xxe-and-configuration-vulnerabilities-for-experience-manager-forms-jee.md#option-2-for-users-on-65180---65220-manual-hotfix-installation">
        Installazione manuale di hotfix per Service Pack 18-22
      </a>
    </td>
    <td>
    <ul>
    <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/adobe-xxe-configuration-hotfix.zip">Patch per AEM 6.5 Forms Service Pack 18 - AEM 6.5 Forms Service Pack 22 </a></li>
    </ul>
    </td>
    <td>
    <ul>
    <li>Maggiore sicurezza grazie alla risoluzione di una vulnerabilità RCE (Remote Code Execution) in Adobe Experience Manager (AEM) Forms. Il problema era relativo alla modalità di sviluppo Struts nell’interfaccia utente di amministrazione, che consentiva la valutazione arbitraria di Object-Graph Navigation Language (OGNL) tramite la funzionalità di debug. Questa correzione assicura che la modalità di sviluppo Struts sia disabilitata e che vengano applicati filtri di sicurezza appropriati per impedire l’accesso non autorizzato.</li>
    <li>È stata migliorata la protezione contro le vulnerabilità XXE (Extensible Markup Language) nel modulo Document Security di Adobe Experience Manager (AEM) Forms. Le vulnerabilità erano dovute a una gestione impropria dei documenti XML senza protezioni XXE, che poteva portare alla lettura dei file locali. La correzione include:
      <ul>
        <li>Verificare che DocumentBuilderFactory utilizzato nella classe SecurityCheckHandler sia configurato per impedire attacchi XXE.</li>
        <li>Aggiornamento del servizio Web Document Security per gestire i documenti XML in modo sicuro, impedendo l’accesso non autorizzato ai file locali.</li>
      </ul>
    </li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>10 luglio 2025-</td>
    <td>
    <ul>
    <li><strong>Jboss:</strong></li>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/jboss/adobe-aem-forms-jee-hotfix-6.5.23.0-win-jboss.zip">Hotfix per AEM Service Pack 6.5.23.0 su Windows per il server JEE JBoss</a></li>
    <li>Linux- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/jboss/adobe-aem-forms-jee-hotfix-6.5.23.0-linux-jboss.tar.gz">Hotfix per AEM Service Pack 6.5.23.0 su Linux per il server JEE JBoss</a></li>
    <li><strong>Weblogic:</strong></li>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/weblogic/adobe-aem-forms-jee-hotfix-6.5.23.0-win-weblogic.zip">Hotfix per AEM Service Pack 6.5.23.0 su Windows per il server JEE Weblogic</a></li>
    <li>Linux- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/weblogic/adobe-aem-forms-jee-hotfix-6.5.23.0-linux-weblogic.tar.gz">Hotfix per AEM Service Pack 6.5.23.0 su Linux per il server JEE Weblogic</a></li>
    <li><strong>WebSphere:</strong></li>
    <li>Windows: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/websphere/adobe-aem-forms-jee-hotfix-6.5.23.0-win-websphere.zip">Hotfix per AEM Service Pack 6.5.23.0 su Windows per il server WebSphere JEE</a></li>
    <li>Linux: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/websphere/adobe-aem-forms-jee-hotfix-6.5.23.0-linux-websphere.tar.gz">Hotfix per AEM Service Pack 6.5.23.0 su Linux per il server WebSphere JEE</a></li>
    </ul>
    </td>
    <td>
    <ul>
    <li><strong>Questo aggiornamento rapido corregge i seguenti problemi:</strong>
      <ul>
        <li><strong>FORMS-20533:</strong> AEM Forms ora include un aggiornamento della versione Struts da 2.5.33 a 6.x per il componente Forms. In questo modo si ottengono le modifiche Struts precedentemente mancate che non erano incluse in SP23. Il supporto è stato aggiunto tramite un Hotfix che è possibile scaricare e installare per aggiungere il supporto per la versione più recente di Struts.</li>
        <li><strong>FORMS-20532:</strong> AEM Forms ora include un aggiornamento della versione Struts da 2.5.33 a 6.x per il componente di output. In questo modo si ottengono le modifiche Struts precedentemente mancate che non erano incluse in SP23. Il supporto è stato aggiunto tramite un Hotfix che è possibile scaricare e installare per aggiungere il supporto per la versione più recente di Struts.</li>
        <li><strong>FORMS-20203:</strong> Quando un utente aggiorna Struts da AEM Service Pack 2.5.x ad AEM Forms Service Pack 6.x, nell'interfaccia utente dei criteri non vengono visualizzate tutte le configurazioni, ad esempio l'opzione per aggiungere una filigrana. Puoi scaricare e installare l’Hotfix per risolvere questo problema.</li>
        <li><strong>FORMS-20360:</strong> Dopo l'aggiornamento ad AEM Forms Service Pack 6.5.23.0, il servizio di conversione ImageToPDF non riesce e viene visualizzato l'errore:<br>
        <code>17:15:44,468 ERROR [com.adobe.pdfg.GeneratePDFImpl] (default task-49) ALC-PDG-001-000-ALC-PDG-011-028-Error occurred while converting the input image file to PDF. com/adobe/internal/pdftoolkit/core/encryption/EncryptionImp</code><br>
        Puoi scaricare e installare l’Hotfix per risolvere questo problema.</li>
      </ul>
    </li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>26 marzo 2025 </br> </br> Per installare questa correzione, segui le istruzioni <a href="/help/forms/using/mitigating-spring-framework-vulnerabilities-for-aem-forms-on-jee.md"> Mitigazione delle vulnerabilità Spring Framework per AEM Forms su JEE</a>.</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/jboss/adobe-aem-forms-jee-hotfix-6.5.22.0-win-jboss.tar.gz">Hotfix per AEM Service Pack 6.5.22.0 su Windows per il server JEE JBoss </a> </li>
      <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/jboss/adobe-aem-forms-jee-hotfix-6.5.22.0-linux-jboss.tar.gz">Hotfix per AEM Service Pack 6.5.22.0 su Linux per il server JEE JBoss </a> </li>
       <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/weblogic/adobe-aem-forms-jee-hotfix-6.5.22.0-win-weblogic.tar.gz">Hotfix per AEM Service Pack 6.5.22.0 in Windows per il server JEE Weblogic </a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/weblogic/adobe-aem-forms-jee-hotfix-6.5.22.0-linux-weblogic.tar.gz">Hotfix per AEM Service Pack 6.5.22.0 su Linux per il server JEE Weblogic</a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/websphere/adobe-aem-forms-jee-hotfix-6.5.22.0-win-websphere.tar.gz">Hotfix per AEM Service Pack 6.5.22.0 su Windows per il server WebSphere JEE </a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/websphere/adobe-aem-forms-jee-hotfix-6.5.22.0-linux-websphere.tar.gz">Hotfix per AEM Service Pack 6.5.22.0 su Linux per il server WebSphere JEE</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>Mitigazione delle vulnerabilità del framework Spring per AEM Forms su JEE</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>giovedì 10 luglio 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/jboss/win/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-windows-jboss.zip.zip">Hotfix per AEM Service Pack 6.5.21.0 su Windows per il server JEE JBoss </a> </li>
      <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/jboss/linux/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-linux-jboss.tar.gz">Hotfix per AEM Service Pack 6.5.21.0 su Linux per il server JEE JBoss </a> </li>
       <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/websphere/win/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-windows-websphere.zip.zip">Hotfix per AEM Service Pack 6.5.21.0 su Windows per il server WebShpere JEE </a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/websphere/linux/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-linux-websphere.tar.gz">Hotfix per AEM Service Pack 6.5.21.0 su Linux per il server WebShpere JEE</a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/weblogic/win/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-windows-weblogic.zip.zip">Hotfix per AEM Service Pack 6.5.21.0 in Windows per il server JEE Weblogic </a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/weblogic/linux/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-linux-weblogic.tar.gz">Hotfix per AEM Service Pack 6.5.21.0 su Linux per il server JEE Weblogic</a> </li>
     </ul>
     </td>
    <td>
    <ul><li>Quando un utente effettua l’aggiornamento ad AEM Forms Service Pack 20 (6.5.20.0) sul server JEE e genera PDF utilizzando i servizi di output, il rendering dei PDF presenta problemi di accessibilità. (LC-3922112)</li><li>I PDF con tag generati utilizzando il servizio di output su AEM Forms JEE mostrano l’avviso di struttura inappropriata. (LC-3922038)</li><li>Quando un modulo viene inviato in AEM Forms JEE, le istanze di un elemento XML ripetuto vengono rimosse dai dati. (LC-3922017)</li><li>Quando un utente in un ambiente Linux esegue il rendering di un modulo adattivo (su JEE) in HTML, il rendering non riesce. (LC-3921957)</li><li>Quando un utente converte un file XTG in formato PostScript utilizzando il servizio di output in AEM Forms JEE, l’operazione non riesce e viene visualizzato l’errore: AEM_OUT_001_003: Eccezione imprevista: errore PAExecute: XFA_RENDER_FAILURE. (LC-3921720)</li><li>Dopo l’aggiornamento ad AEM Forms Service Pack 18 (6.5.18.0) sul server JEE, quando un utente invia un modulo, non riesce a eseguire il rendering degli arresti anomali di HTML5 o PDF forms e XMLFM. (LC-3921718)
    </ul>
    </td>    
  </tr>
  <tr>
    <td>sabato 21 giugno 2024</td>
     <td>
     <ul>
     <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">Hotfix per AEM Service Pack 6.5.21.0 o AEM Forms Service Pack 6.5.22.0 sul server JEE JBoss </a> </li>
      <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">Hotfix per AEM Service Pack 6.5.21.0 o AEM Forms Service Pack 6.5.22.0 sul server JEE Weblogic </a> </li>
       <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">Hotfix per AEM Service Pack 6.5.21.0 o AEM Forms Service Pack 6.5.22.0 sul server WebShpere JEE </a> </li>
        <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">Hotfix per AEM Service Pack 6.5.21.0 o AEM Forms Service Pack 6.5.22.0 sul server OSGi </a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li> Dopo l'aggiornamento ad AEM Forms Service Pack 6.5.21.0 o AEM Forms Service Pack 6.5.22.0, il servizio PaperCapture non riesce a eseguire le operazioni OCR (Optical Character Recognition) sui PDF. Per le istruzioni di installazione, fare riferimento all'articolo <a href="/help/forms/using/papercapture-service-resolution.md"> sulla risoluzione dei problemi</a>.(CQDOC-21680) </li>
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
    <li>Le lettere bozza con dati XML si bloccano nello stato di caricamento durante l'anteprima. Per le istruzioni di download e installazione dell'hotfix, fare riferimento alla sezione <a href="#install-hotfix"> Download and install hotfix per bozza lettera problema</a>.(FORMS-14521)</li>
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
     <li>Quando un modulo adattivo viene inviato da un’istanza Adobe Experience Manager Publish a un flusso di lavoro Adobe Experience Manager, il flusso di lavoro non riesce a salvare gli allegati.  (FORMS-14209) </li>
     <li> Durante l’installazione del pacchetto AEM 6.5 Forms Service Pack 20 (pacchetto del componente aggiuntivo AEM Forms per SP20), l’interfaccia utente di AEM Sites presenta un significativo deterioramento delle prestazioni.  (FORMS-13791) </li>
     <li>Il servizio di precompilazione ha esito negativo con un’eccezione NPE nelle comunicazioni interattive. (CQDOC-21355)</li>
     <li>Le configurazioni che utilizzano il servizio cloud legacy per Adobe Analytics con autenticazione basata sulle credenziali utente non funzionano correttamente, causando l’errore di esecuzione delle regole di analisi. (FORMS-15428)
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

## Scaricare e installare un aggiornamento rapido OSGi {#download-install-hotfix}

Per scaricare e installare l’Hotfix, effettua le seguenti operazioni:

1. Scarica [Hotfix](#hotfix-for-adaptive-forms) dal collegamento Software Distribution.
1. Estrai il file di archivio Hotfix per ottenere un pacchetto Experience Manager (.zip) e i file bundle (.jar).
1. Carica e installa il pacchetto (.zip) tramite [Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=es#accessing).
1. Apri i bundle di Gestione configurazione `https://server:host/system/console/bundles`, carica e installa il bundle (.jar). L&#39;aggiornamento rapido è installato.

## Installare una patch JEE {#download-install-jee-patch}

Per istruzioni su come installare una patch JEE, consulta la [documentazione del programma di installazione di AEM Forms JEE Patch](/help/release-notes/jee-patch-installer-65.md).


## Scarica e installa l’hotfix per il problema della bozza di lettera {#install-hotfix}

Per risolvere il problema, effettuare le seguenti operazioni:

1. Scarica [hotfix](#hotfix-for-adaptive-forms) dal portale di distribuzione software.
2. Carica e installa il pacchetto (.zip) utilizzando [Gestione pacchetti CRX](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=es#accessing).
