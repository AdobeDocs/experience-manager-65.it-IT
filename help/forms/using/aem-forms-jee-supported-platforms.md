---
title: Piattaforme supportate per  AEM Forms su JEE
seo-title: Piattaforme supportate per  AEM Forms su JEE
description: Elenco dei componenti dell’infrastruttura richiesti e supportati per l’installazione  AEM Forms su JEE
seo-description: Elenco dei componenti dell’infrastruttura richiesti e supportati per l’installazione  AEM Forms su JEE
uuid: 777f943b-4cb4-444e-a036-8032b9fce5be
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: f777865e-d4a8-40ef-87b0-130c19eb1b91
docset: aem65
translation-type: tm+mt
source-git-commit: 4e1f5d549df1db28a8679296afb4b758051d8f6c
workflow-type: tm+mt
source-wordcount: '3298'
ht-degree: 0%

---


# Piattaforme supportate per  AEM Forms su JEE{#supported-platforms-for-aem-forms-on-jee}

## Piattaforme supportate {#supported-platforms}

### Livelli di supporto {#support-levels}

 AEM Forms su un server JEE può essere configurato utilizzando qualsiasi combinazione di sistemi operativi, server applicazioni, database, driver di database, JDK, server LDAP e server e-mail supportati.

In questo documento sono elencate le piattaforme client e server supportate per  AEM Forms su JEE.  Adobe offre diversi livelli di supporto, sia per le configurazioni consigliate che per altre configurazioni. Il documento elenca anche altri software supportati e la relativa versione, eccezioni, definizioni di patch e criteri di supporto per patch software di terze parti.

>[!NOTE]
>
>* Per un elenco completo delle eccezioni alle piattaforme server supportate, vedere [Eccezioni alle piattaforme server supportate](../../forms/using/aem-forms-jee-supported-platforms.md#p-exceptions-to-supported-server-platforms-p).
>*  AEM Forms su JEE supporta solo le versioni inglese, francese, tedesca e giapponese dei sistemi operativi e delle applicazioni supportati.
>



### Configurazioni consigliate {#recommendedconfigurations}

 Adobe consiglia queste configurazioni e fornisce supporto completo o limitato nell&#39;ambito del contratto standard di manutenzione del software:

<table>
 <tbody>
  <tr>
   <th>Livello di supporto</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>A: Supportato<br /> </td>
   <td> Adobe fornisce supporto e manutenzione completi per questa configurazione. Questa configurazione è coperta  processo  garanzia della qualità.</td>
  </tr>
  <tr>
   <td>R: Supporto limitato</td>
   <td> Adobe fornisce supporto completo per questa configurazione dopo il soddisfacimento di alcuni prerequisiti. Per informazioni sui prerequisiti e per richiedere assistenza, contattate  Adobe di assistenza Enterprise.</td>
  </tr>
  <tr>
   <td>L: Supporto limitato</td>
   <td> Adobe fornisce supporto e manutenzione completi per queste configurazioni dopo il soddisfacimento di determinati prerequisiti. Non tutte le funzionalità sono disponibili nella configurazione. Per informazioni sui prerequisiti e per ottenere una richiesta di assistenza, contattate  Adobe di assistenza enterprise.<br /> </td>
  </tr>
 </tbody>
</table>

### Configurazioni non supportate {#unsupported-configurations}

| Livello di supporto | Descrizione |
|---|---|
| E: Previsto per il lavoro | La configurazione dovrebbe funzionare e non ci sono rapporti al contrario. |
| Z: Non supportato | La configurazione non è supportata.  Adobe non fornisce alcuna istruzione sul funzionamento della configurazione e non la supporta. |

>[!NOTE]
>
>Per aiutare  clienti AEM Forms a ridurre i costi di proprietà, semplificare l&#39;architettura di distribuzione e modernizzare lo stack di sviluppo, la piattaforma Adobe Experience Manager Enterprise si sta allontanando dalle installazioni basate su server delle applicazioni a favore di installazioni standalone basate su OSGi.  Adobe continua a supportare lo stack AEM Forms JEE  con una matrice ridotta di componenti dell&#39;infrastruttura.
>
>Con il rilascio della versione 6.5, i componenti dell&#39;infrastruttura con l&#39;utilizzo più basso tra i clienti non sono più supportati, come segue:
>・ Database IBM DB2
>・ Sistemi operativi IBM AIX e Sun Solaris
>
>Per le nuove installazioni, si consiglia di implementare  AEM Forms nel moderno stack OSGi per sfruttare le ultime innovazioni su Forms adattivo reattivo per comunicazioni mobili, multi-canale, e integrazioni di dati back-end tramite Form Data Model.
>
>Riconosciamo che gli utenti esistenti devono continuare a distribuire  AEM Forms nello stack JEE. In tali scenari,  Adobe richiede la distribuzione di  AEM Forms JEE sull&#39;infrastruttura supportata come descritto in questa documentazione. Se state effettuando l&#39;aggiornamento a AEM 6.5 Forms e utilizzate una piattaforma non supportata nella precedente versione di AEM Forms , potete contattare  Supporto Adobe per assistenza sull&#39;aggiornamento a una piattaforma supportata.

### Java Virtual Machines (JVM) {#java-virtual-machines-jvm}

 Adobe Experience Manager Forms richiede l&#39;esecuzione di una macchina virtuale Java, fornita dalla distribuzione Java Development Kit (JDK). Adobe Experience Manager funziona con le seguenti versioni di Java Virtual Machines:

<table>
 <tbody>
  <tr>
   <th><p><strong>Platform</strong></p> </th>
   <th><p><strong>Livello di supporto</strong></p> </th>
   <th><p><strong>Definizioni di patch supportate</strong></p> </th>
  </tr>
  <tr>
   <td><p> Oracle Java™ SE 11 (64 bit)</p> </td>
   <td><p>Z: Non supportato</p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td> Oracle Java™ SE 8 (64 bit)</td>
   <td>A: Supportato</td>
   <td>Versioni e aggiornamenti secondari</td>
  </tr>
  <tr>
   <td>Macchina virtuale IBM® J9 (build 2.8, JRE 1.8.0)</td>
   <td>A: Supportato</td>
   <td>Versioni e aggiornamenti secondari</td>
  </tr>
  <tr>
   <td>Macchina virtuale IBM® J9 (build 2.9, JRE 1.8.0)<br /> </td>
   <td>A: Supportato</td>
   <td>Versioni e aggiornamenti secondari</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* Si consiglia di tenere traccia dei bollettini sulla sicurezza dal fornitore Java per garantire la sicurezza degli ambienti di produzione e installare gli aggiornamenti Java più recenti.
>*  AEM Forms su JEE supporta solo JVM a 64 bit in ambienti di produzione.


### Database e persistenza CRX {#databases-and-crx-persistence}

<table>
 <tbody>
  <tr>
   <td><p><strong>Piattaforma</strong></p> </td>
   <td><p><strong> Descrizione</strong></p> </td>
   <td><p><strong>Livello di supporto</strong></p> </td>
  </tr>
  <tr>
   <td><p>File system</p> </td>
   <td><p>Repository Microkernel (file TAR MK)</p> </td>
   <td><p>Supportato</p> </td>
  </tr>
  <tr>
   <td><p>MongoDB Enterprise 4.0 </p> </td>
   <td><p>Microkernel repository</p> </td>
   <td><p>Supportato</p> </td>
  </tr>
  <tr>
   <td><p> Oracle Database 12c Release 1</p> </td>
   <td><p>Microkernel repository</p> </td>
   <td><p>Supportato</p> </td>
  </tr>
   <tr>
   <td><p> Oracle Database 12c Release 2 (12.2.0.1.0)</p> </td>
   <td><p>Microkernel repository</p> </td>
   <td><p>Supportato</p> </td>
  </tr>
  <tr>
   <td> Oracle Database 18c </td>
   <td>Microkernel repository</td>
   <td>Supportato</td>
  </tr> 
   <tr>
   <td> Oracle Database 19c (versioni Standard, Real Application Clusters (RAC) ed Enterprise) </td>
   <td>Repository Microkeral </td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td><p>Microsoft SQL Server 2016</p> </td>
   <td><p>Microkernel repository</p> </td>
   <td><p>Supportato</p> </td>
  </tr>
  <tr>
   <td>IBM DB2 11.1</td>
   <td>Microkernel repository</td>
   <td>R: Supporto limitato</td>
  </tr>
    <tr>
   <td>MySQL 5.7.19 </td>
   <td>-</td>
   <td>R: Supporto limitato</td>
  </tr>
 </tbody>
</table>

* IBM DB2 non è supportato per le nuove installazioni. È supportato solo per i clienti esistenti che effettuano l’aggiornamento a AEM 6.5 Forms.
* MongoDB è un software di terze parti e non è incluso nel pacchetto di licenze AEM. Per ulteriori informazioni, vedere la pagina [Criteri di gestione licenze MongoDB](https://www.mongodb.org/about/licensing/).
* Per ottenere il massimo dalla distribuzione AEM,  Adobe consiglia di concedere in licenza la versione Enterprise di MongoDB per poter beneficiare del supporto professionale.
*  Assistenza clienti di Adobe assisterà i problemi di qualificazione relativi all&#39;utilizzo di MongoDB con AEM. Per ulteriori informazioni, vedere [MongoDB per Adobe Experience Manager page](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager).
* Il file system include l&#39;archiviazione a blocchi conforme con POSIX. Ciò include la tecnologia di storage in rete. Tenere presente che le prestazioni del file system potrebbero variare e influenzare le prestazioni complessive. Si consiglia di caricare AEM di prova in combinazione con il file system di rete/remoto.
* È supportato solo MongoDB Storage Engine WiredTiger.
* Lo Shopping MongoDB non è supportato in AEM.
*  AEM Forms su JEE non supporta MySQL per la persistenza RDBMK.
* Il modulo Document Security non utilizza l&#39;archivio dei contenuti. Ciò implica che, se si utilizza solo Document Security e non si intende utilizzare HTML Workspace, moduli HTML5 o moduli adattivi, non installare Content Repository.
*  AEM Forms su JEE non supporta l&#39;uso di MySQL per AEM repository persistente (CRX-Repository).


### Driver del database {#database-drivers}

<table>
 <tbody>
  <tr>
   <th>Database </th>
   <th><p><strong>Piattaforma</strong></p> </th>
   <th><p><strong>Definizioni di patch supportate</strong></p> </th>
  </tr>
  <tr>
   <td>MySQL</td>
   <td><p>Connettore MySQL/J 5.7</p> <p>mysql-Connector-java-5.1.44-bin.jar(versione 5.1.44)</p> </td>
   <td><p>Fornito con  AEM Forms sull'installazione JEE</p> </td>
  </tr>
  <tr>
   <td>Microsoft SQL Server<br /> </td>
   <td><p>Driver JDBC di Microsoft® SQL Server 6.2.1.0<br /> </p> <p>sqljdbc6.jar</p> </td>
   <td><p>Fornito con  AEM Forms sull'installazione JEE.</p> </td>
  </tr>
  <tr>
   <td> Oracle</td>
   <td><p> driver JDBC Oracle Database 19.3.0.0.0</p> <p>ojdbc8.jar (versione 19.3.0.0.0)<br /> </p> </td>
   <td><p>Scarica da <a href="https://www.oracle.com/technetwork/database/features/jdbc/jdbc-ucp-122-3110062.html"> sito Web Oracle</a>.</p> </td>
  </tr>
 </tbody>
</table>

### Server applicazioni {#application-servers}

<table>
 <tbody>
  <tr>
   <td><p><strong> Piattaforma</strong></p> </td>
   <td><p><strong>Livello di supporto</strong></p> </td>
   <td><p><strong>Definizioni di patch supportate</strong></p> </td>
  </tr>
  <tr>
   <td> Oracle WebLogic Server 12.2.1 (12c R2)</td>
   <td>A: Supportato</td>
   <td>Service Pack e aggiornamenti critici</td>
  </tr>
  <tr>
   <td>IBM® WebSphere® Application Server 9.0 <sup>[1] [4]</sup><br /> </td>
   <td>A: Supportato</td>
   <td>Service Pack e aggiornamenti critici</td>
  </tr>
  <tr>
   <td><p>JBoss® Enterprise Application Platform (EAP) 7.1.4 <sup>[2] [3] [7]</sup></p> </td>
   <td><p>A: Supportato</p> </td>
   <td><p>Patch e patch cumulative per la versione EAP supportata</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>I cluster IBM® WebSphere® sono supportati solo nelle edizioni di distribuzione in rete.

### Sistemi operativi server {#server-operating-systems}

#### Ambienti di produzione {#production-environments}

<table>
 <tbody>
  <tr>
   <th><p><strong> Piattaforma</strong></p> </th>
   <th><p><strong>Livello di supporto</strong></p> </th>
   <th><p><strong>Definizioni di patch supportate</strong></p> </th>
  </tr>
  <tr>
   <td>Microsoft Windows Server 2016 (64 bit)</td>
   <td>A: Supportato</td>
   <td>Service Pack e aggiornamenti critici</td>
  </tr>
  <tr>
   <td><p>Red Hat Enterprise Linux 7 (Kernel 3.x) (64 bit)</br><b>Nota:</b> <a href="https://access.redhat.com/articles/4665701">Red Hat Enterprise Linux 6</a> raggiunge la fase di fine manutenzione e le transizioni alla fase di supporto del ciclo di vita esteso il 30 novembre 2020.  Adobe consiglia Red Hat Enterprise Linux 7 per gli aggiornamenti e le nuove installazioni. Le installazioni esistenti possono utilizzare Red Hat Enterprise Linux 6 durante la fase di supporto del ciclo di vita esteso.</p> </td>
   <td><p>A: Supportato</p> </td>
   <td><p>Rilasci secondari, aggiornamenti cumulativi e aggiornamenti critici</p> </td>
  </tr>
  <tr>
   <td><p>SUSE® Linux® Enterprise Server 12 (64 bit)</p> </td>
   <td><p>A: Supportato</p> </td>
   <td><p>Service Pack, patch cumulative e aggiornamenti di sicurezza critici</p> </td>
  </tr>
  <tr>
   <td> Oracle Linux® 7 Update 3 (64 bit)</td>
   <td>A: Supportato</td>
   <td>Service Pack, patch cumulative e aggiornamenti di sicurezza critici</td>
  </tr>
  <tr>
   <td>CentOS 7 (64 bit)<sup> [6]</sup></td>
   <td>A: Supportato</td>
   <td>Service Pack, patch cumulative e aggiornamenti di sicurezza critici</td>
  </tr>
 </tbody>
</table>

#### Ambiente virtualizzato {#virtualized-environment}

È possibile eseguire  AEM Forms su JEE su una macchina fisica o su un ambiente virtuale. Tuttavia, se si verificano problemi con  AEM Forms in un ambiente virtuale, provare a replicare il problema su una macchina fisica. Se il problema persiste sul computer fisico, contattare  supporto del Adobe per una risoluzione. Per i problemi che non è possibile replicare su una macchina fisica, contattare il fornitore dell&#39;ambiente virtuale.

#### Ambienti di sviluppo {#development-environments}

<table>
 <tbody>
  <tr>
   <th><p><strong>Piattaforma (versione di base)</strong></p> </th>
   <th>Livello di supporto</th>
   <th><p><strong>Definizioni di patch supportate</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Windows® 10 a 64 bit</p> </td>
   <td>E: Previsto per il lavoro</td>
   <td><p>Service Pack e aggiornamenti critici</p> </td>
  </tr>
 </tbody>
</table>

### Eccezioni alle piattaforme server supportate {#exceptions-to-supported-server-platforms}

Considerate le seguenti eccezioni quando scegliete una piattaforma per configurare il vostro AEM Forms  sul server JEE.

1.  AEM Forms su JEE non supporta IBM® WebSphere® con MySQL.
1.  AEM Forms su JEE non supporta e JBoss su SUSE Linux Enterprise Server 12. Solo IBM WebSphere è supportato su SUSE Linux Enterprise Server 12.
1.  AEM Forms su JEE non supporta JDK con JBoss® diverso da  Oracle Java™ SE.
1.  AEM Forms su JEE non supporta JDK con IBM® WebSphere® diverso da IBM® JDK.
1. CRX-repository supporta la persistenza di tipo TarMK, MongoDB e database relazionali (RDBMK). Non è possibile avere due diversi sistemi di database tra il server applicazioni e il repository CRX. Tuttavia, in un AEM Forms  in ambiente JEE, è possibile utilizzare MongoMK con repository CRX e un database relazionale supportato con server applicazioni.
1.  AEM Forms su JEE non supporta il server applicazioni WebSphere su CentOS.
1.  AEM Forms su JEE non supporta il controllo degli accessi basato sui ruoli JBoss (RBAC).

Inoltre, considerate quanto segue durante la scelta del software per  Adobe  AEM Forms sulle distribuzioni JEE:

*  AEM Forms su JEE supporta aggiornamenti, patch e pacchetti di correzione sulla versione principale e secondaria specificata del software supportato. Tuttavia, l&#39;aggiornamento alla versione principale o secondaria successiva non è supportato a meno che non sia specificato.
* Le installazioni basate su cluster non supportano la persistenza TarMK. Per informazioni sulla persistenza supportata, vedere [Scelta di un tipo di persistenza per un&#39;installazione AEM Forms ](/help/forms/using/choosing-persistence-type-for-aem-forms.md).
*  AEM Forms su JEE supporta vari software di terze parti in base alla [Politica di supporto software di terze parti](../../forms/using/aem-forms-jee-supported-platforms.md#p-third-party-patch-support-policy-p).
*  AEM Forms su JEE supporta le piattaforme in base al supporto fornito da fornitori di terze parti. Alcune combinazioni possono non essere consentite da fornitori di terze parti. Ad esempio, molti fornitori non hanno certificato i propri server applicazioni con  Oracle. Di conseguenza, anche  AEM Forms su JEE non supporta queste combinazioni. Per essere certi di scegliere le versioni software supportate, controllate la matrice di supporto anche per i fornitori di terze parti.
*  AEM Forms su JEE non supporta TarMK Cold Standby.
*  AEM Forms su JEE non supporta il clustering verticale.
*  AEM Forms su JEE non supporta il database MySQL in un ambiente cluster.
* Per l&#39;elenco delle piattaforme rimosse o aggiornate, consultate il documento [AEM 6.5 Forms New Feature Summary](../../forms/using/whats-new.md).

### Server LDAP (facoltativi) {#ldap-servers-optional}

<table>
 <tbody>
  <tr>
   <th><p><strong>Prodotto (versione di base)</strong></p> </th>
   <th><p><strong>Definizioni di patch supportate</strong></p> </th>
  </tr>
  <tr>
   <td> Oracle Unified Directory (OUD) 11g Release 2</td>
   <td>Service Pack</td>
  </tr>
  <tr>
   <td>Microsoft Active Directory 2016</td>
   <td>Rilascio di manutenzione e pacchetti di correzione</td>
  </tr>
  <tr>
   <td><p>IBM® Tivoli Directory Server 6.4</p> </td>
   <td><p>Pacchetti di funzioni e correzioni intermedie</p> </td>
  </tr>
 </tbody>
</table>

### Server e-mail (facoltativo) {#email-servers-optional}

| Prodotto |
|---|
| IBM Lotus Domino 9.0 |
| Microsoft Exchange 2013 |
| Microsoft Office 365 |

### Content manager e connettori corrispondenti {#content-managers-and-corresponding-connectors}

<table>
 <tbody>
  <tr>
   <td><strong>Prodotto<br /> </strong></td>
   <td><strong>Versione</strong></td>
  </tr>
  <tr>
   <td>EMC Documentum</td>
   <td>7.3</td>
  </tr>
  <tr>
   <td>Filenet IBM</td>
   <td>5.2</td>
  </tr>
  <tr>
   <td>Filenet IBM</td>
   <td>5.5.2</td>
  </tr>
  <tr>
   <td>IBM Content Manager Server</td>
   <td>8.5 Fix pack 2</td>
  </tr>
  <tr>
   <td>Client IBM Content Manager</td>
   <td>8,5 </td>
  </tr>
  <tr>
   <td>Microsoft SharePoint</td>
   <td>2016<br /> </td>
  </tr>
 </tbody>
</table>

### Supporto per Cordova {#support-for-cordova}

 App AEM Forms ora supporta l&#39;Apache Cordova. Di seguito sono elencate le versioni di Cordova specifiche della piattaforma supportate:

* Apache Cordova 6.4.0
* Cordova iOS 4.3.0
* Cordova Android 6.0.0
* Cordova Windows 4.4.3

### Supporto software per PDF Generator {#software-support-for-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>Prodotto</strong></p> </th>
   <th><p><strong>Formati supportati per la conversione in PDF</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html"> Acrobat 2017 </a> trackeraggio classico versione più recente</td>
   <td>XPS, formati immagine (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, DWG, DXF e DWF</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2016</td>
   <td>DOC, DOCX, XLS, XLSX, PPT, PPTX, RTF e TXT</td>
  </tr>
  <tr>
   <td>WordPerfect X7</td>
   <td>WP, WPD</td>
  </tr>
  <tr>
   <td>Microsoft® Office Visio 2016<br /> </td>
   <td>VSD, VSDX</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2016<br /> </td>
   <td>PUB</td>
  </tr>
  <tr>
   <td>Microsoft® Project 2016<br /> </td>
   <td>MPP</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.2</td>
   <td>ODT, ODP, ODS, ODG, ODF, SXW, SXI, SXC, SXD, XLS, XLSX, DOC, DOCX, PPT, PPTX, formati immagine (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM RTF e TXT</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>PDF Generator supporta solo versioni in inglese, francese, tedesco e giapponese dei sistemi operativi e delle applicazioni supportati.
>
>Inoltre:
>
>* PDF Generator richiede la versione a 32 bit di [ Acrobat 2017 Classic track versione 17.011.30078 o successiva](https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html) per eseguire la conversione.
>* PDF Generator supporta solo la versione a 32 bit per la vendita al dettaglio di Microsoft Office Professional Plus e di altri software richiesti per la conversione.
>* PDF Generator non supporta Microsoft Office 365.
>* Le conversioni di PDF Generator per OpenOffice sono supportate solo in Windows e Linux.
>* Le funzioni PDF,  Optimize PDF e  Export PDF OCR sono supportate solo in Windows.
>* Una versione di  Acrobat viene fornita con  AEM Forms per abilitare la funzionalità PDF Generator. È consigliabile accedere alla versione bundle solo a livello di programmazione con  AEM Forms, per tutta la durata della licenza AEM Forms , da utilizzare con  AEM Forms PDF Generator. Per ulteriori informazioni, fare riferimento  descrizione del prodotto AEM Forms in base alla distribuzione ([In sede](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html) o [Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html))&quot;
   >
   >
* Il servizio PDF Generator non supporta Microsoft Windows 10.
>



### Eccezioni al supporto dell&#39;accessibilità {#exceptions-to-accessibility-support}

I seguenti sottosistemi di  AEM Forms non sono [508](https://www.section508.gov/) conformi:

* Interfaccia di authoring Forms adattiva
* Interfaccia utente di authoring di Forms Manager
* Interfaccia utente di authoring per la gestione della corrispondenza
* Interfaccia utente amministratore (interfaccia utente della console di amministrazione)

## Requisiti di sistema per  AEM Forms su JEE {#system-requirements-for-aem-forms-on-jee}

### Requisiti hardware minimi {#minimum-hardware-requirements}

<table>
 <tbody>
  <tr>
   <td>Piattaforma</td>
   <td>Requisiti hardware minimi</td>
  </tr>
  <tr>
   <td>Microsoft Windows Server</td>
   <td>Processore Intel® Xeon® E5-2680, a 2,4 GHz o equivalente<br /> VMWare ESX 5.1 o successivo<br /> RAM: 6 GB (sistema operativo a 64 bit con JVM a 64 bit)<br /> Spazio libero su disco: 15 GB di spazio temporaneo più 22 GB<br /> per  AEM Forms su JEE</td>
  </tr>
  <tr>
   <td>SUSE Linux Enterprise Server</td>
   <td>Intel Xeon E5-2670v2, 1 vCPU, processore da 2,5 GHz<br /> AWS m3.medium (3 ECU)<br /> RAM: 6 GB (sistema operativo a 64 bit con JVM a 64 bit)<br /> Spazio libero su disco: 6 GB di spazio temporaneo più 22 GB<br /> per  AEM Forms su JEE</td>
  </tr>
  <tr>
   <td>Red Hat Enterprise Linux</td>
   <td>Intel Xeon E5-2670v2, 1 vCPU, processore da 2,5 GHz<br /> AWS m3.medium (3 ECU)<br /> RAM: 6 GB (sistema operativo a 64 bit con JVM a 64 bit)<br /> Spazio libero su disco: 6 GB di spazio temporaneo più 22 GB<br /> per  AEM Forms su JEE<br /> </td>
  </tr>
  <tr>
   <td>Requisiti hardware per un ambiente di produzione di piccole dimensioni</td>
   <td>
    <ul>
     <li><strong>Ambiente</strong> con tecnologia Intel: Intel® Xeon® E5-2680, da 2,4 GHz o superiore. L'utilizzo di un processore dual core consente di migliorare ulteriormente le prestazioni</li>
     <li><strong>Memoria:  </strong>4 GB  <br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

Per ulteriori requisiti, consulta:

* [Requisiti di sistema per un singolo server  AEM Forms su distribuzione JEE](https://www.adobe.com/go/learn_aemforms_sysreq_single_63)
* [Requisiti di sistema per un  cluster AEM Forms su distribuzione JEE](https://www.adobe.com/go/learn_aemforms_sysreq_cluster_63)

## Client supportati per  AEM Forms su JEE {#supported-clients-for-aem-forms-on-jee}

### Workbench {#workbench}

<table>
 <tbody>
  <tr>
   <th><p><strong>Piattaforma</strong></p> </th>
   <th><p><strong>Definizioni di patch supportate</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Windows® 10 (Enterprise, Pro, Basic)</p> <p>Versione a 32 bit o a 64 bit</p> <p> </p> </td>
   <td>Service Pack e aggiornamenti critici</td>
  </tr>
  <tr>
   <td>Microsoft® Windows® 2016 Server</td>
   <td>Service Pack e aggiornamenti critici</td>
  </tr>
 </tbody>
</table>

* Spazio su disco per l&#39;installazione: 1,7 GB solo per Workbench, 2,7 GB su un&#39;unica unità per un&#39;installazione completa di Workbench, Designer e l&#39;assembly di esempi 400 MB per le directory di installazione temporanea: 200 MB nella directory temp dell&#39;utente e 200 MB nella directory temporanea di Windows. Se tutte queste posizioni si trovano su un&#39;unica unità, durante l&#39;installazione deve essere disponibile uno spazio di 1,5 GB. I file copiati nelle directory temporanee vengono eliminati al termine dell&#39;installazione.

* Memoria per l&#39;esecuzione di Workbench: 2 GB di RAM
* Requisiti hardware: Processore Intel® Pentium® 4 o AMD equivalente a 1 GHz
* Risoluzione minima del monitor 1024x768 pixel o superiore con colore a 16 bit o superiore
* Connessione di rete TCP/IPv4 o TCP/IPv6 all&#39;AEM Forms  sul server JEE
* Per installare Workbench in Windows è necessario disporre dei privilegi di amministratore. Se state installando un account non amministratore, il programma di installazione vi chiederà le credenziali per un account appropriato.

### Designer {#designer}

>[!NOTE]
>
>Per installare Designer in Windows, eseguire il programma di installazione con privilegi di amministratore.

* Microsoft® Windows® 2016 Server, Microsoft Windows 10

   * Processore da 1 GHz o più potente con supporto per PAE, NX e SSE2.
   * 1 GB di RAM per 32 bit o 2 GB di RAM per i sistemi operativi a 64 bit
   * 16 GB di spazio su disco per sistemi operativi a 64 bit o a 32 bit per uno spazio su disco da 20 GB

* Memoria grafica - 128 MB di GPU (consigliati 256 MB)
* 2,35 GB di spazio disponibile su disco rigido
* Unità DVD-ROM
* Internet Explorer 10 o 11; Firefox 45.x
* Risoluzione monitor 1024x768 pixel o superiore
* Accelerazione hardware video (opzionale)
* Acrobat Pro DC, Acrobat Standard DC o  Adobe Acrobat Reader DC.

###  Adobe Acrobat e  Adobe Reader {#adobe-acrobat-and-adobe-reader}

<table>
 <tbody>
  <tr>
   <th><p><strong> Acrobat e  Adobe Reader (base)</strong></p> </th>
   <th><p><strong>Definizioni di patch supportate</strong></p> </th>
  </tr>
  <tr>
   <td> Acrobat 2017 (modalità classica)</td>
   <td>Versione 17.011.30078 o successiva<br /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>La  famiglia di prodotti Acrobat DC presenta due tracce per  Acrobat e Reader, che sono essenzialmente prodotti diversi: &quot;Classic&quot; e &quot;Continuous&quot;. Per informazioni dettagliate e un confronto tra le due tracce, vedere [https://www.adobe.com/go/acrobatdctracks.](https://www.adobe.com/go/acrobatdctracks)

### Browser {#browsers}

#### Desktop {#desktops}

<table>
 <tbody>
  <tr>
   <th><p><strong>Browser (base)</strong></p> </th>
   <th><p><strong>Livello di supporto</strong></p> </th>
   <th><p><strong>Definizioni di patch supportate</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft Edge (Evergreen)</p> </td>
   <td><p>A: Supportato</p> </td>
   <td><p>Service Pack e aggiornamenti</p> </td>
  </tr>
  <tr>
   <td><p>Mozilla Firefox (Evergreen)</p> </td>
   <td><p>A: Supportato</p> </td>
   <td>Tutti gli aggiornamenti</td>
  </tr>
  <tr>
   <td>Microsoft Firefox ESR</td>
   <td>E: Previsto per il lavoro</td>
   <td> Tutti gli aggiornamenti</td>
  </tr>
  <tr>
   <td><p>Google Chrome (Evergreen)</p> </td>
   <td><p>A: Supportato</p> </td>
   <td>Tutti gli aggiornamenti</td>
  </tr>
  <tr>
   <td>Google Chrome e Firefox su MAC OS X</td>
   <td>A: Supportato<br /> <br /> </td>
   <td>Tutti gli aggiornamenti</td>
  </tr>
  <tr>
   <td>Apple Safari 11.x</td>
   <td>A: Supportato</td>
   <td>Tutti gli aggiornamenti</td>
  </tr>
  <tr>
   <td>Apple Safari 12.x<br /> <br /> </td>
   <td>A: Supportato</td>
   <td>Tutti gli aggiornamenti</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Alcune eccezioni relative al browser per i desktop sono le seguenti:
>
>* La maggior parte dei browser moderni non supporta più i plug-in basati su NPAPI. Per informazioni sull&#39;impatto  applicazioni e flussi di lavoro AEM Forms, vedere [Discontinuità dei plug-in del browser NPAPI e relativo impatto](https://helpx.adobe.com/aem-forms/kb/discontinuation-of-npapi-plugins-impact-on-aem-forms.html).
>* Safari è supportato solo su Macintosh OS X.
>* Workspace supporta Safari 5.1 su Macintosh OS X 10.6 e 10.7 con  Acrobat DC o versioni successive. Per ulteriori informazioni sulla compatibilità di Safari 5.1 con  Adobe Reader,  Acrobat, vedere [https://helpx.adobe.com/x-productkb/multi/safari-5-1-incompatible-reader.html](https://helpx.adobe.com/x-productkb/multi/safari-5-1-incompatible-reader.html).
>* La console di amministrazione non è supportata in Safari.
>* Gestione corrispondenza non supporta Windows® Internet Explorer 9.0 per i moduli AEM 6.1.
>* Il portale Forms supporta il software di lettura dello schermo JAWS 14.0 su Internet Explorer 11 per l&#39;accessibilità.
>



#### Client mobili {#mobile-clients}

<table>
 <tbody>
  <tr>
   <th><p><strong>Browser (base)</strong></p> </th>
   <th><p><strong>Definizioni di patch supportate</strong></p> </th>
  </tr>
  <tr>
   <td><p>Chrome su Android™ 4.1.2 e versioni successive</p> </td>
   <td><p>Tutti gli aggiornamenti</p> </td>
  </tr>
  <tr>
   <td>Safari su iOS 11.0 e versioni successive</td>
   <td>Tutti gli aggiornamenti</td>
  </tr>
  <tr>
   <td>Microsoft Edge<br /> </td>
   <td>Tutti gli aggiornamenti<br /> </td>
  </tr>
  <tr>
   <td>Browser Android nativo su Android™ 4.4 e versioni successive</td>
   <td>Tutti gli aggiornamenti</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* Forms Portal è supportato su Safari solo su iPad.
>



###  app AEM Forms {#aem-forms-workspace-app}

#### Supporto per dispositivi mobili {#mobile-device-support}

 app AEM Forms è disponibile sulle seguenti piattaforme:

| **Platform** | **Dispositivi supportati** |
|---|---|
| Apple iOS | Apple iPhone, iPad, iPad Air e iPad mini con iOS 12 e versioni successive. |
| Google Android | Android 5.1 e versioni successive.  app AEM Forms è certificato su 7- e 10-pollici Samsung Galaxy tablet e smartphone popolari. |
| Microsoft Windows | Dispositivi, tablet, notebook e desktop Microsoft Surface con sistema operativo Microsoft Windows 10. |

### Flash Player Adobe  {#adobe-flash-player}

<table>
 <tbody>
  <tr>
   <th><p><strong>Flash Player (base)</strong></p> </th>
   <th><p><strong>Definizioni di patch supportate</strong></p> </th>
  </tr>
  <tr>
   <td><p>Versione più recente di Flash Player</p> </td>
   <td><p>Versioni e aggiornamenti secondari</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
> Adobe [interromperà l&#39;aggiornamento e la distribuzione del Flash Player alla fine del 2020](https://theblog.adobe.com/adobe-flash-update/).

###  Adobe Document Security Extension for Microsoft Office {#adobe-rights-management-extension-for-microsoft-office}

Fate clic [qui](https://www.adobe.com/products/livecycle/rightsmanagement/extension/downloads.html) per visualizzare i requisiti di sistema per  Adobe Document Security Extension for Microsoft® Office.

### Eccezioni al supporto client {#exceptions-to-client-support}

 AEM Forms su JEE supporta aggiornamenti, patch e pacchetti di correzione sulla versione principale e secondaria specificata del software supportato. Tuttavia, l&#39;aggiornamento alla versione principale o secondaria successiva non è supportato a meno che non sia specificato.

## Criteri di supporto patch di terze parti {#third-party-patch-support-policy}

I requisiti software di terze parti per  AEM Forms su JEE sono documentati nella sezione &quot;Requisiti di sistema&quot; dei rispettivi documenti di prodotto. Tutta la documentazione è accessibile da [https://adobe.com/go/learn_aemforms_documentation_65](https://adobe.com/go/learn_aemforms_documentation_65) .

 AEM Forms sulle piattaforme di riferimento di terze parti di JEE indica il livello di patch specifico dell&#39;infrastruttura di terze parti che era in corso durante lo sviluppo e il rilascio di  AEM Forms su JEE, e dal livello di patch/service pack minimo dell&#39;infrastruttura supportata da quella versione di  AEM Forms su JEE.

 Adobe supporta patch urgenti o consigliate emesse da fornitori di terze parti al momento del rilascio, partendo dal presupposto che i fornitori di terze parti garantiscano la compatibilità con le versioni supportate da  AEM Forms su JEE.  Adobe supporterà solo le patch rilasciate dopo il livello di patch minimo indicato nell&#39;AEM Forms  nella documentazione JEE.

In alcuni casi,  Adobe non supporta gli aggiornamenti di terze parti che modificano le funzionalità principali, e quindi non supportano la compatibilità con le versioni precedenti. Per informazioni dettagliate sugli aggiornamenti supportati, vedere [Definizioni di patch supportate](https://helpx.adobe.com/aem-forms/aem-forms-third-party-software-patch.html) per prodotti fornitore specifici e i tipi di patch supportati  Adobe.

In circostanze che esulano  controllo del Adobe, le patch di terze parti che rivendicano la compatibilità con le versioni precedenti possono avere un impatto negativo sui prodotti del Adobe  o sugli ambienti dei clienti. In tali casi,  Adobe raccomanda ai clienti di valutare l&#39;impatto di eventuali patch urgenti di terzi prima di applicarle ai sistemi critici.  Adobe collaborerà con terzi utilizzando ragionevoli sforzi commerciali per risolvere tali problemi, sia attraverso normali programmi di sostegno  Adobe o da parte di terzi che porranno rimedio alla questione nella loro patch. Ciò non garantisce che una patch di terze parti appena rilasciata che sarà supportata dal Adobe  funzionerà come documentato dal fornitore o con  AEM Forms su JEE.

 Adobe si riserva il diritto di modificare le piattaforme di riferimento di terze parti supportate da un AEM Forms  sulla versione JEE e le relative definizioni di patch supportate in qualsiasi momento.

Per ulteriori informazioni sulle patch di terze parti, consultate anche il sito del supporto Enterprise  Adobe per gli articoli della knowledgebase relativi al prodotto.

## Cronologia revisioni {#revision-history}

* 09 settembre 2020
   * È stata modificata la versione supportata di iOS per  app AEM Forms in iOS 12. La versione precedente era iOS 11.
