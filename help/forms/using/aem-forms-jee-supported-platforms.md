---
title: Piattaforme supportate per AEM Forms su JEE
description: Elenco dei componenti dell’infrastruttura richiesti e supportati per l’installazione di AEM Forms su JEE
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin
exl-id: 74d22cf4-56b2-48f5-92d9-928eaa134866
source-git-commit: 3d80ea6a6fbad05afcdd1f41f4b9de70921ab765
workflow-type: tm+mt
source-wordcount: '3684'
ht-degree: 1%

---


# Piattaforme supportate per AEM Forms su JEE {#supported-platforms-for-aem-forms-on-jee}

## Piattaforme supportate {#supported-platforms}

<div class="preview">

L’Adobe ha rilasciato un [programma di installazione completo](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) con AEM 6.5 Forms Service Pack 12 (6.5.12.0) su JEE insieme ai programmi di installazione delle patch. Il programma di installazione completo fornisce il supporto per le nuove piattaforme, mentre il programma di installazione delle patch include solo correzioni di bug.

Se stai eseguendo una nuova installazione o pianificando di utilizzare il software più recente per il tuo Forms AEM 6.5 in ambiente JEE, Adobe consiglia di utilizzare [Programma di installazione completo per Forms su JEE per AEM 6.5.12.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) rilasciato il 3 marzo 2022 invece del programma di installazione di Forms AEM 6.5 rilasciato l’8 aprile 2019.

</div>

### Livelli di supporto {#support-levels}

AEM Forms sul server JEE può essere configurato utilizzando qualsiasi combinazione di sistemi operativi, server applicazioni, database, driver di database, JDK, server LDAP e server e-mail supportati.

Questo documento elenca le piattaforme client e server supportate per AEM Forms su JEE. Adobe fornisce diversi livelli di supporto, sia per le configurazioni consigliate per Adobe che per altre configurazioni. Il documento elenca anche altri software supportati e le relative versioni, eccezioni, definizioni di patch e criteri di supporto delle patch software di terze parti.

>[!NOTE]
>
>- Per un elenco completo delle eccezioni alle piattaforme server supportate, vedere [Eccezioni alle piattaforme server supportate](../../forms/using/aem-forms-jee-supported-platforms.md#p-exceptions-to-supported-server-platforms-p).
>- AEM Forms su JEE supporta solo le versioni in inglese, francese, tedesco e giapponese dei sistemi operativi e delle applicazioni supportati.

### Configurazioni consigliate {#recommendedconfigurations}

L&#39;Adobe consiglia queste configurazioni e fornisce supporto completo o limitato come parte del contratto standard di manutenzione software:

<table>
 <tbody>
  <tr>
   <th>Livello di supporto</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>R: Supportato<br /> </td>
   <td>L'Adobe fornisce supporto e manutenzione completi per questa configurazione. Questa configurazione è coperta dal processo di controllo qualità di Adobe.</td>
  </tr>
  <tr>
   <td>R: Supporto limitato</td>
   <td>L’Adobe fornisce il supporto completo per questa configurazione dopo che sono stati soddisfatti alcuni prerequisiti. Contatta l’Adobe di supporto Enterprise per scoprire i prerequisiti e inoltrare una richiesta di supporto.</td>
  </tr>
  <tr>
   <td>L: Supporto limitato</td>
   <td>L'Adobe fornisce supporto e manutenzione completi per questa configurazione dopo che sono stati soddisfatti alcuni prerequisiti. Non tutte le funzionalità sono disponibili nella configurazione. Contatta l’Adobe di supporto Enterprise per scoprire i prerequisiti e inoltrare una richiesta di supporto.<br /> </td>
  </tr>
 </tbody>
</table>

### Configurazioni non supportata {#unsupported-configurations}

| Livello di supporto | Descrizione |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| E: Funzionamento previsto | La configurazione dovrebbe funzionare, e non ci sono report che indicano il contrario. |
| Z: non supportato | Configurazione non supportata. L’Adobe non fornisce alcuna istruzione sul funzionamento o meno della configurazione e non la supporta. |

>[!NOTE]
>
>Per aiutare i clienti AEM Forms a ridurre il costo di proprietà, semplificare l’architettura di distribuzione e modernizzare lo stack di sviluppo, la piattaforma aziendale Adobe Experience Manager si sta allontanando dalle implementazioni basate su server applicazioni a favore delle implementazioni autonome basate su OSGi. Adobe continua a supportare lo stack AEM Forms JEE con una matrice ridotta di componenti dell’infrastruttura.
>
>Con la versione 6.5, i componenti dell’infrastruttura che hanno il minore utilizzo tra i clienti Adobe non sono più supportati, come segue:
>
>- Database IBM® DB2®
- Sistemi operativi IBM® AIX® e Sun Solaris™
>
Per le nuove installazioni, ove possibile, si consiglia di implementare AEM Forms sul moderno stack OSGi per utilizzare le ultime innovazioni relative a Adaptive Forms per le integrazioni di dati mobili, interattivi multicanale e back-end tramite il modello dati del modulo.
>
Adobe riconosce che gli utenti esistenti devono continuare a distribuire AEM Forms sullo stack JEE. In tali scenari, Adobe richiede la distribuzione di AEM Forms JEE sull’infrastruttura supportata come descritto in questa documentazione. Se stai effettuando l’aggiornamento a Forms AEM 6.5 e utilizzi una piattaforma non supportata nella versione precedente di AEM Forms, puoi contattare il supporto di Adobe per assistenza sull’aggiornamento a una piattaforma supportata.

### Java™ Virtual Machine (JVM) {#java-virtual-machines-jvm}

Adobe Experience Manager Forms richiede una macchina virtuale Java™ da eseguire, fornita dalla distribuzione Java™ Development Kit (JDK). Adobe Experience Manager funziona con le seguenti versioni di Java™ Virtual Machines:

<table>
 <tbody>
  <tr>
   <th><p><strong>Platform</strong></p> </th>
   <th><p><strong>Livello di supporto</strong></p> </th>
   <th><p><strong>Definizioni di patch supportate</strong></p> </th>
  </tr>
  <tr> 
   <td><p>Oracle Java™ SE 11 (64 bit) <sup> [8] </sup> </p>  </td>
   <td><p>R: Supportato</p> </td>
   <td><p>Versioni minori e aggiornamenti </p> </td>
  </tr>
  <tr>
   <td>Azul Zulu OpenJDK 11 - 64 bit</td>
   <td>Z: non supportato</td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td>Azul Zulu OpenJDK 8 - 64 bit</td>
   <td>Z: non supportato</td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td>Oracle Java™ SE 8 (64 bit)</td>
   <td>R: Supportato</td>
   <td>Versioni minori e aggiornamenti</td>
  </tr>
  <tr>
   <td>Macchina virtuale IBM® J9 (build 2.9, JRE 1.8.0) IBM® JDK SR6-FP26<br /> </td>
   <td>R: Supportato</td>
   <td>Versioni minori e aggiornamenti</td>
  </tr>
  <tr>
   <td>IBM® JAVA1.8.0_291 (build 8.0.6.30)<br /> </td>
   <td>R: Supportato</td>
   <td>Versioni minori e aggiornamenti</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
- Monitora i bollettini sulla sicurezza del fornitore Java™ per garantire la sicurezza degli ambienti di produzione e installa gli aggiornamenti Java™ più recenti.
- AEM Forms su JEE supporta solo JVM a 64 bit negli ambienti di produzione.

### Database e persistenza CRX {#databases-and-crx-persistence}

<table>
 <tbody>
  <tr>
   <td><p><strong>Platform</strong></p> </td>
   <td><p><strong> Descrizione</strong></p> </td>
   <td><p><strong>Livello di supporto</strong></p> </td>
  </tr>
  <tr>
   <td><p>File system</p> </td>
   <td><p>Microkernel dell’archivio (file TAR MK)</p> </td>
   <td><p>Funzione supportata</p> </td>
  </tr>
  <tr>
   <td><p> MongoDB Enterprise 4.0 (obsoleto) </p> </td>
   <td><p>Microkernel archivio</p> </td>
   <td><p>Funzione supportata</p> </td>
  </tr>
  <tr>
   <td><p>MongoDB Enterprise 4.2 </p> </td>
   <td><p>Microkernel archivio</p> </td>
   <td><p>Funzione supportata</p> </td>
  </tr>
  <tr>
   <td><p>Database Oracle 12c versione 2 (12.2.0.1.0) (obsoleto)</p> </td>
   <td><p>Microkernel archivio</p> </td>
   <td><p>Funzione supportata</p> </td>
  </tr>
   <tr>
   <td>Oracle Database 19c (Standard, Real Application Clusters (RAC) ed Enterprise Edition) </td>
   <td>Archivio Microkernal </td>
   <td>Funzione supportata</td>
  </tr>
  <tr>
   <td><p>Microsoft® SQL Server 2016 (obsoleto)</p> </td>
   <td><p>Microkernel archivio</p> </td>
   <td><p>Funzione supportata</p> </td>
  </tr>
  <tr>
   <td><p>Microsoft® SQL Server 2019</p> </td>
   <td><p>Microkernel archivio</p> </td>
   <td><p>Funzione supportata</p> </td>
  </tr>
  <tr>
   <td>IBM® DB2® 11.1 (obsoleto)</td>
   <td>Microkernel archivio</td>
   <td>R: Supporto limitato</td>
  </tr>
  <tr>
   <td>MySQL 5.7.35 (obsoleto) </td>
   <td>-</td>
   <td>R: Supporto limitato</td>
  </tr>
  <tr>
   <td>MySQL 8.0.27</td>
   <td>-</td>
   <td>R: Supporto limitato</td>
  </tr>
 </tbody>
</table>

- IBM® DB2® non è supportato per le nuove installazioni. È supportato solo per i clienti esistenti che eseguono l’aggiornamento a Forms AEM 6.5.
- MongoDB è un software di terze parti e non è incluso nel pacchetto di licenze AEM. Per ulteriori informazioni, consulta [Criteri di licenza MongoDB](https://www.mongodb.org/about/licensing/).
- Per ottenere il massimo dall’implementazione dell’AEM, l’Adobe consiglia di concedere in licenza la versione Enterprise di MongoDB per beneficiare di un supporto professionale.
- L’Assistenza clienti Adobe fornirà assistenza per i problemi di qualificazione relativi all’utilizzo di MongoDB con AEM. Per ulteriori informazioni, vedere [Pagina MongoDB per Adobe Experience Manager](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager).
- &#39;File system&#39; include l&#39;archiviazione dei blocchi compatibile con POSIX. Ciò include la tecnologia di storage in rete. Tieni presente che le prestazioni del file system potrebbero variare e influenzare le prestazioni complessive. Si consiglia di caricare l&#39;AEM di prova con il file system di rete/remoto.
- È supportato solo MongoDB Storage Engine WiredTiger.
- Il partizionamento di MongoDB non è supportato in AEM.
- AEM Forms su JEE non supporta MySQL per la persistenza RDBMK.
- Il modulo Document Security non utilizza l’archivio dei contenuti. Ciò significa che, se utilizzi solo Document Security e non prevedi di utilizzare HTML Workspace, moduli HTML5 o moduli adattivi, non installare il Content Repository.
- AEM Forms su JEE non supporta l’utilizzo di MySQL per l’archivio AEM persistente (CRX-Repository).

### Driver di database {#database-drivers}

<table>
 <tbody>
  <tr>
   <th>Database </th>
   <th><p><strong>Platform</strong></p> </th>
   <th><p><strong>Definizioni di patch supportate</strong></p> </th>
  </tr>
  <tr>
   <td>MySQL</td>
   <td><p>Connettore MySQL/J 5.7</p> <p>mysql-connector-java-5.1.44-bin.jar(versione 5.1.44)</p> </td>
   <td><p>Fornito con l’installazione di AEM Forms su JEE</p> </td>
  </tr>
  <tr>
   <td>Microsoft® SQL Server<br /> </td>
   <td><p>Driver JDBC Microsoft® SQL Server 6.2.1.0 (obsoleto) <br /> </p> <p>sqljdbc6.jar</p> </td>
   <td><p>Fornito con l’installazione di AEM Forms su JEE.</p> </td>
  </tr>
    <tr>
   <td>Microsoft® SQL Server<br /> </td>
   <td><p>Driver JDBC Microsoft® SQL Server 6.2.2.0 <br /> </p> <p>sqljdbc6.jar</p> </td>
   <td><p>Fornito con l’installazione di AEM Forms su JEE.</p> </td>
  </tr>
  <tr>
   <td>Microsoft® SQL Server<br /> </td>
   <td><p>Driver JDBC Microsoft® SQL Server 8.2.2<br /> </p> <p>sqljdbc8.jar</p> </td>
   <td><p>Scarica dal sito web Microsoft®.</p> </td>
  </tr>
  <tr>
   <td>Oracle</td>
   <td><p>Driver JDBC Oracle Database 19.3.0.0.0</p> <p>ojdbc8.jar (versione 19.3.0.0.0)<br /> </p> </td>
   <td><p>Scarica da <a href="https://www.oracle.com/database/technologies/appdev/jdbc-ucp-19c-downloads.html">Sito Web Oracle</a>.</p> </td>
  </tr>
 </tbody>
</table>

### Server applicazioni {#application-servers}

<table>
 <tbody>
  <tr>
   <td><p><strong> Platform</strong></p> </td>
   <td><p><strong>Livello di supporto</strong></p> </td>
   <td><p><strong>Definizioni di patch supportate</strong></p> </td>
  </tr>
  <tr>
   <td>Oracle server WebLogic 12.2.1 (12c R2)</td>
   <td>R: Supportato</td>
   <td>Service Pack e aggiornamenti critici</td>
  </tr>
  <tr>
   <td>Application server IBM® WebSphere® 9.0.0.10 <sup>[1] [4]</sup><br /> </td>
   <td>R: Supportato</td>
   <td>Service Pack e aggiornamenti critici</td>
  </tr>
  <tr>
   <td><p>JBoss® Enterprise Application Platform (EAP) 7.1.4 <sup>[2] [3] [7]</sup> (Obsoleto) </p> </td>
   <td><p>R: Supportato</p> </td>
   <td><p>Patch e patch cumulative per la versione EAP supportata</p> </td>
  </tr>
  <tr>
   <td><p>JBoss® Enterprise Application Platform (EAP) 7.4 <sup>[2] [3] [7]</sup> </p> </td>
   <td><p>R: Supportato</p> </td>
   <td><p>Patch e patch cumulative per la versione EAP supportata</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
I cluster IBM® WebSphere® sono supportati solo nelle edizioni di distribuzione in rete.

### Sistemi operativi server {#server-operating-systems}

#### Ambienti di produzione {#production-environments}

<table>
 <tbody>
  <tr>
   <th><p><strong> Platform</strong></p> </th>
   <th><p><strong>Livello di supporto</strong></p> </th>
   <th><p><strong>Definizioni di patch supportate</strong></p> </th>
  </tr>
   <tr>
   <td>Microsoft® Windows Server 2019 (64 bit)</td>
   <td>R: Supportato</td>
   <td>Service Pack e aggiornamenti critici</td>
  </tr>
  <tr>
   <td>Ubuntu 20.04</td>
   <td>R: Supportato</td>
   <td>Service Pack e aggiornamenti critici</td>
  </tr>
  <tr>
   <td> Microsoft® Windows Server 2016 (64 bit) (obsoleto)</td>
   <td>R: Supportato</td>
   <td>Service Pack e aggiornamenti critici</td>
  </tr>
  <tr>
   <td><p>Red Hat® Enterprise Linux® 8 (Kernel 4.x) (64 bit)</p> </td>
   <td><p>R: Supportato</p> </td>
   <td><p>Versioni minori, aggiornamenti cumulativi e aggiornamenti critici</p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® Enterprise Linux® 7 (Kernel 3.x) (64 bit) (obsoleto)</td>
   <td><p>R: Supportato</p> </td>
   <td><p>Versioni minori, aggiornamenti cumulativi e aggiornamenti critici</p> </td>
  </tr>
  <tr>
   <td><p>SUSE® Linux® Enterprise Server 12 (64 bit)</p> </td>
   <td><p>R: Supportato</p> </td>
   <td><p>Service Pack, patch cumulative e aggiornamenti di sicurezza critici</p> </td>
  </tr>
  <tr>
   <td>Oracle Linux® 7 Aggiornamento 3 (64 bit)</td>
   <td>R: Supportato</td>
   <td>Service Pack, patch cumulative e aggiornamenti di sicurezza critici</td>
  </tr>
  <tr>
   <td>CentOS 7 (64 bit)<sup> [6]</sup></td>
   <td>R: Supportato</td>
   <td>Service Pack, patch cumulative e aggiornamenti di sicurezza critici</td>
  </tr>
 </tbody>
</table>

#### Ambiente virtualizzato {#virtualized-environment}

Puoi eseguire AEM Forms su JEE in un computer fisico o in un ambiente virtuale. Tuttavia, se riscontri problemi con AEM Forms in un ambiente virtuale, prova a replicare il problema su un computer fisico. Se il problema persiste sul computer fisico, contattare il supporto Adobe per una risoluzione. Per i problemi che non è possibile replicare su un computer fisico, contattare il fornitore dell&#39;ambiente virtuale.

#### Ambienti di sviluppo {#development-environments}

<table>
 <tbody>
  <tr>
   <th><p><strong>Piattaforma (versione base)</strong></p> </th>
   <th>Livello di supporto</th>
   <th><p><strong>Definizioni di patch supportate</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Windows® 10 a 64 bit</p> </td>
   <td>E: Funzionamento previsto</td>
   <td><p>Service Pack e aggiornamenti critici</p> </td>
  </tr>
 </tbody>
</table>

### Eccezioni alle piattaforme server supportate {#exceptions-to-supported-server-platforms}

Quando scegli una piattaforma per configurare il server AEM Forms su JEE, considera le seguenti eccezioni.

1. AEM Forms su JEE non supporta IBM® WebSphere® con MySQL.
1. AEM Forms su JEE non supporta e JBoss® su SUSE® Linux® Enterprise Server 12. Solo IBM® WebSphere® è supportato su SUSE® Linux® Enterprise Server 12.
1. AEM Forms su JEE non supporta JDK con JBoss® ad eccezione di Oracle Java™ SE.
1. AEM Forms su JEE non supporta JDK con IBM® WebSphere® eccetto IBM® JDK.
1. L’archivio CRX supporta la persistenza di tipi TarMK, MongoDB e database relazionali (RDBMK). Non è possibile avere due sistemi di database diversi tra il server applicazioni e l&#39;archivio CRX. Tuttavia, in un ambiente AEM Forms su JEE, puoi utilizzare MongoMK con l’archivio CRX e un database relazionale supportato con il server applicazioni.
1. AEM Forms su JEE non supporta il server applicazioni WebSphere® su CentOS.
1. AEM Forms su JEE non supporta JBoss® RBAC (role-based access control).
1. AEM Forms Oracle su JEE supporta l’SDK Java™ SE 11 (64 bit) per JBoss per application server® solo EAP 7.4.

Inoltre, nella scelta del software, considera i seguenti aspetti, ad Adobe le implementazioni di AEM Forms su JEE:

- AEM Forms su JEE supporta aggiornamenti, patch e fix pack oltre alla versione principale e secondaria specificata del software supportato. Tuttavia, l’aggiornamento alla versione principale o secondaria successiva non è supportato, a meno che non sia specificato.
- Le installazioni basate su cluster non supportano la persistenza TarMK. Per informazioni sulla persistenza supportata, consulta [Scelta di un tipo di persistenza per un’installazione di AEM Forms](/help/forms/using/choosing-persistence-type-for-aem-forms.md).
- AEM Forms su JEE supporta diversi software di terze parti in base ai Adobi [Criteri di supporto software di terze parti](../../forms/using/aem-forms-jee-supported-platforms.md#p-third-party-patch-support-policy-p).
- AEM Forms sulle piattaforme di supporto JEE in base al supporto fornito da fornitori terzi. Alcune combinazioni potrebbero non essere consentite da fornitori di terze parti. Molti fornitori, ad esempio, non hanno certificato i propri server applicazioni con Oracle. Di conseguenza, anche AEM Forms su JEE non supporta queste combinazioni. Per assicurarsi di scegliere le versioni del software supportate, consultare la matrice di supporto anche per i fornitori di terze parti.
- AEM Forms su JEE non supporta lo standby a freddo di TarMK.
- AEM Forms su JEE non supporta il clustering verticale.
- AEM Forms su JEE non supporta il database MySQL in un ambiente cluster.
- Per un elenco delle piattaforme rimosse o aggiornate, consulta [Riepilogo delle nuove funzioni di AEM 6.5 Forms](../../forms/using/whats-new.md) documento.

### Server LDAP (facoltativo) {#ldap-servers-optional}

<table>
 <tbody>
  <tr>
   <th><p><strong>Prodotto (versione base)</strong></p> </th>
   <th><p><strong>Definizioni di patch supportate</strong></p> </th>
  </tr>
  <tr>
   <td>Microsoft® Active Directory 2016</td>
   <td>Rilascio di manutenzione e pacchetti di correzione</td>
  </tr>
  <tr>
   <td><p>IBM® Tivoli Directory Server 6.4</p> </td>
   <td><p>Feature Pack e correzioni provvisorie</p> </td>
  </tr>
 </tbody>
</table>

### Server di posta elettronica (facoltativo) {#email-servers-optional}

| Prodotto |
| ----------------------- |
| Microsoft® Exchange 2013 |
| Microsoft® Office 365 |

### Gestione contenuti e connettori corrispondenti {#content-managers-and-corresponding-connectors}

<table>
 <tbody>
  <tr>
   <td><strong>Prodotto<br /> </strong></td>
   <td><strong>Versione</strong></td>
  </tr>
  <tr>
   <td>EMC Documentum®</td>
   <td>7.3</td>
  </tr>
  <tr>
   <td>IBM® FileNet</td>
   <td>5.5.2</td>
  </tr>
  <tr>
   <td>IBM® Content Manager Server (obsoleto) </td>
   <td>8.5 Fix pack 2</td>
  </tr>
  <tr>
   <td> Client IBM® Content Manager (obsoleto)</td>
   <td>8.5 </td>
  </tr>
  <tr>
   <td>Microsoft® Sharepoint </td>
   <td>2016 (obsoleto)<br /> </td>
  </tr>
  <tr>
   <td>Microsoft® Sharepoint </td>
   <td>2019<br /> </td>
  </tr>
 </tbody>
</table>

### Supporto per Cordova {#support-for-cordova}

L’app AEM Forms ora supporta Apache Cordova. Di seguito sono riportate le versioni di Cordova specifiche per piattaforma supportate:

- Apache Cordova 6.4.0
- Cordova iOS 4.3.0
- Cordova Android™ 6.0.0
- Cordova Windows 4.4.3

### Supporto software per PDF Generator {#software-support-for-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>Prodotto</strong></p> </th>
   <th><p><strong>Formati supportati per la conversione in PDF</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2020 classic track</a> ultima versione</td>
   <td>XPS, formati immagine (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, DWG, DXF e DWF</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2017 classic track</a> versione più recente (obsoleto)</td>
   <td>XPS, formati immagine (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, DWG, DXF e DWF</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2019</td>
   <td>DOC, DOCX, XLS, XLSX, PPT, PPTX, RTF e TXT</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2016 (obsoleto)</td>
   <td>DOC, DOCX, XLS, XLSX, PPT, PPTX, RTF e TXT</td>
  </tr>
  <tr>
   <td>WordPerfect 2020<br /> </td>
   <td>WP, WPD</td>
  </tr>
  <tr>
   <td>Microsoft® Office Visio 2016 (obsoleto)<br /> </td>
   <td>VSD, VSDX</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2019<br /> </td>
   <td>PUB</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2016 (obsoleto)<br /> </td>
   <td>PUB</td>
  </tr>
  <tr>
   <td>Microsoft® Project 2016 (obsoleto)<br /> </td>
   <td>MPP</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.10</td>
   <td>ODT, ODP, ODS, ODG, ODF, SXW, SXI, SXC, SXD, XLS, XLSX, DOC, DOCX, PPT, PPTX, formati immagine (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, RTF e TXT</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.2 (obsoleto)</td>
   <td>ODT, ODP, ODS, ODG, ODF, SXW, SXI, SXC, SXD, XLS, XLSX, DOC, DOCX, PPT, PPTX, formati immagine (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, RTF e TXT</td>
  </tr>  
 </tbody>
</table>

>[!NOTE]
>
PDF Generator supporta solo le versioni in inglese, francese, tedesco e giapponese dei sistemi operativi e delle applicazioni supportati.
>
Inoltre:
>
- PDF Generator richiede una versione a 32 bit di [Acrobat 2020 classic track versione 20.004.30006](https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html) o Acrobat 2017 versione 17.011.30078 per eseguire la conversione.
- PDF Generator supporta solo la versione a 32 bit di Microsoft® Office Professional Plus e altri software necessari per la conversione.
- PDF Generator non supporta Microsoft® Office 365.
- Le conversioni PDF Generator per OpenOffice sono supportate solo in Windows e Linux®.
- Le funzionalità PDF OCR, Optimize PDF e Export PDF sono supportate solo in Windows.
- Una versione di Acrobat è inclusa in bundle con AEM Forms per abilitare la funzionalità PDF Generator. È consigliabile accedere alla versione in bundle solo a livello di programmazione con AEM Forms, per l’utilizzo con AEM Forms PDF Generator, durante il periodo di validità della licenza di AEM Forms. Per ulteriori informazioni, consulta Descrizione del prodotto AEM Forms in base alla distribuzione ([On-Premise](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html) o [Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html))&quot;
>
- Il servizio PDF Generator non supporta Microsoft® Windows 10.
- PDF Generator non riesce a convertire i file in Microsoft® Visio 2019. È possibile continuare a utilizzare Microsoft® Visio 2016 per convertire i file VSD e VSDX.
- PDF Generator non riesce a convertire i file utilizzando Microsoft® Project 2019. È possibile continuare a utilizzare Microsoft® Project 2016 per convertire i file MPP.
>

### Eccezioni al supporto dell’accessibilità {#exceptions-to-accessibility-support}

I seguenti sottosistemi di AEM Forms non sono [508](https://www.section508.gov/) conforme:

- Interfaccia utente di authoring di Forms adattivo
- Interfaccia utente di authoring di Forms Manager
- Interfaccia utente di authoring di Gestione corrispondenza
- Interfaccia di amministrazione (interfaccia di Administration Console)

## Requisiti di sistema per AEM Forms su JEE {#system-requirements-for-aem-forms-on-jee}

### Requisiti hardware minimi {#minimum-hardware-requirements}

<table>
 <tbody>
  <tr>
   <td>Platform</td>
   <td>Requisiti hardware minimi</td>
  </tr>
  <tr>
   <td>Microsoft® Windows Server</td>
   <td>Processore Intel Xeon® E5-2680, 2,4 GHz o equivalente<br /> VMWare ESX 5.1 o versione successiva<br /> RAM: 6 GB (sistema operativo a 64 bit con JVM a 64 bit)<br /> Spazio libero su disco: 15 GB di spazio temporaneo più 22 GB<br /> per AEM Forms su JEE</td>
  </tr>
  <tr>
   <td>SUSE® Linux® Enterprise Server</td>
   <td>Intel Xeon® E5-2670v2, 1 vCPU, processore da 2,5 GHz<br /> AWS m3.medium (3 ECU)<br /> RAM: 6 GB (sistema operativo a 64 bit con JVM a 64 bit)<br /> Spazio libero su disco: 6 GB di spazio temporaneo più 22 GB<br /> per AEM Forms su JEE</td>
  </tr>
  <tr>
   <td>Red Hat® Enterprise Linux®</td>
   <td>Intel Xeon® E5-2670v2, 1 vCPU, processore da 2,5 GHz<br /> AWS m3.medium (3 ECU)<br /> RAM: 6 GB (sistema operativo a 64 bit con JVM a 64 bit)<br /> Spazio libero su disco: 6 GB di spazio temporaneo più 22 GB<br /> per AEM Forms su JEE<br /> </td>
  </tr>
  <tr>
   <td>Requisiti hardware per un ambiente di produzione di piccole dimensioni</td>
   <td>
    <ul>
     <li><strong>Ambiente basato su Intel®</strong>: Intel Xeon® E5-2680, 2,4 GHz o superiore. L'utilizzo di un processore dual-core migliorerà ulteriormente le prestazioni</li>
     <li><strong>Memoria: </strong>4 GB <br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

Per ulteriori informazioni, vedere:

- [Requisiti di sistema per un’implementazione AEM Forms su JEE per un singolo server](https://www.adobe.com/go/learn_aemforms_sysreq_single_65)
- [Requisiti di sistema per un’implementazione cluster di AEM Forms su JEE](https://www.adobe.com/go/learn_aemforms_sysreq_cluster_65)

## Client supportati per AEM Forms su JEE {#supported-clients-for-aem-forms-on-jee}

### Workbench {#workbench}

<table>
 <tbody>
  <tr>
   <th><p><strong>Platform</strong></p> </th>
   <th><p><strong>Definizioni di patch supportate</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Windows® 10 (Enterprise, Pro, Basic)</p> <p>Versione a 32 bit o a 64 bit</p> <p> </p> </td>
   <td>Service Pack e aggiornamenti critici</td>
  </tr>
  <tr>
   <td>Server Microsoft® Windows® 2016</td>
   <td>Service Pack e aggiornamenti critici</td>
  </tr>
 </tbody>
</table>

- Spazio su disco per l&#39;installazione: 1,7 GB solo per Workbench, 2,7 GB su un&#39;unica unità per un&#39;installazione completa di Workbench, Designer e l&#39;assembly di esempio 400 MB per le directory di installazione temporanee: 200 MB nella directory temporanea dell&#39;utente e 200 MB nella directory temporanea di Windows. Se tutte queste posizioni si trovano su un&#39;unica unità, durante l&#39;installazione devono essere disponibili 1,5 GB di spazio. I file copiati nelle directory temporanee vengono eliminati al termine dell&#39;installazione.

- Memoria per l&#39;esecuzione di Workbench: 2 GB di RAM
- Requisiti hardware: processore Intel® Pentium® 4 o AMD® equivalente a 1 GHz
- Risoluzione minima del monitor 1024 X 768 pixel o superiore con colore a 16 bit o superiore
- Connessione di rete TCP/IPv4 o TCP/IPv6 al server AEM Forms su JEE
- Per installare Workbench in Windows è necessario disporre dei privilegi di amministratore. Se si sta effettuando l&#39;installazione utilizzando un account non amministratore, il programma di installazione richiederà le credenziali per un account appropriato.

### Designer {#designer}

- Microsoft® Windows® 2016 Server, Microsoft® Windows® 2019 Server o Microsoft® Windows® 10
- Processore da 1 GHz o superiore con supporto per PAE, NX e SSE2.
- 1 GB di RAM per 32 bit o 2 GB di RAM per sistema operativo a 64 bit
- 16 GB di spazio su disco per 32 bit o 20 GB di spazio su disco per sistema operativo a 64 bit
- Memoria grafica - 128 MB di GPU (consigliata 256 MB)
- 2,35 GB di spazio disponibile su disco rigido
- Risoluzione di 1024 X 768 pixel o superiore
- Accelerazione hardware video (opzionale)
- Acrobat Pro DC, Acrobat Standard DC o Adobe Acrobat Reader DC.
- Privilegi amministrativi per installare Designer.

### ADOBE ACROBAT e ADOBE READER {#adobe-acrobat-and-adobe-reader}

<table>
 <tbody>
  <tr>
   <th><p><strong>Acrobat e Adobe Reader (base)</strong></p> </th>
   <th><p><strong>Definizioni di patch supportate</strong></p> </th>
  </tr>
  <tr>
   <td>Acrobat 2020 (brano classico)</td>
   <td>Versione 20.004.30006 o successiva<br /> </td>
  </tr>
  <tr>
   <td>Acrobat 2017 (brano classico) (obsoleto)</td>
   <td>Versione 17.011.30078 o successiva<br /> </td>
  </tr>

</tbody>
</table>

>[!NOTE]
>
La famiglia di prodotti Acrobat DC introduce due tracce per Acrobat e Reader che sono prodotti diversi: &quot;Classic&quot; e &quot;Continuous&quot;. Per maggiori dettagli e un confronto tra i due brani, vedere [https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/whatsnewdc.html](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/whatsnewdc.html).

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
   <td><p>Microsoft® Edge (Evergreen)</p> </td>
   <td><p>R: Supportato</p> </td>
   <td><p>Service Pack e aggiornamenti</p> </td>
  </tr>
  <tr>
   <td><p>Mozilla Firefox (Evergreen)</p> </td>
   <td><p>R: Supportato</p> </td>
   <td>Tutti gli aggiornamenti</td>
  </tr>
  <tr>
   <td>Mozilla Firefox ESR</td>
   <td>E: Funzionamento previsto</td>
   <td> Tutti gli aggiornamenti</td>
  </tr>
  <tr>
   <td><p>Google Chrome (Evergreen)</p> </td>
   <td><p>R: Supportato</p> </td>
   <td>Tutti gli aggiornamenti</td>
  </tr>
  <tr>
   <td>Apple Safari su macOS</td>
   <td>R: Supportato</td>
   <td>Tutti gli aggiornamenti</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
Di seguito sono riportate alcune eccezioni relative al browser per i desktop:
>
- Safari è supportato solo su Macintosh OS X.
- Workspace supporta Safari 5.1 su Macintosh OS X 10.6 e 10.7 con Acrobat DC o versioni successive. Per ulteriori informazioni sulla compatibilità di Safari 5.1 con Adobe Reader e Acrobat, consulta [https://helpx.adobe.com/x-productkb/multi/safari-5-1-incompatible-reader.html](https://helpx.adobe.com/x-productkb/multi/safari-5-1-incompatible-reader.html).
- La console di amministrazione non è supportata in Safari.
- Gestione corrispondenza non supporta Windows® Internet Explorer 9.0 per i moduli AEM 6.1.
- Forms Portal supporta il software JAWS 14.0 screen reader su Internet Explorer 11 per l&#39;accessibilità.

#### Client per dispositivi mobili {#mobile-clients}

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
   <td>Safari su iOS 15.1 e versioni successive</td>
   <td>Tutti gli aggiornamenti</td>
  </tr>
  <tr>
   <td>Microsoft® Edge<br /> </td>
   <td>Tutti gli aggiornamenti<br /> </td>
  </tr>
  <tr>
   <td>Browser nativo Android™ su Android™ 4.4 e versioni successive</td>
   <td>Tutti gli aggiornamenti</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
- Forms Portal è supportato su Safari solo su iPad.

### app AEM Forms {#aem-forms-workspace-app}

#### Supporto per dispositivi mobili {#mobile-device-support}

L’app AEM Forms è disponibile sulle seguenti piattaforme:

| **Platform** | **Dispositivi supportati** |
| ----------------- | ------------------------------------------------------------------------------------------------------------------- |
| Apple iOS | Apple iPhone, iPad, iPad Air e iPad mini con iOS 15.1 e versioni successive. |
| Google Android™ | Android™ 5.1 e versioni successive. L&#39;app AEM Forms è certificata su tablet Samsung Galaxy da 7 e 10 pollici e smartphone popolari. |
| Microsoft® Windows | Dispositivi Microsoft® Surface, tablet, notebook e desktop con sistema operativo Microsoft® Windows 10. |

### Adobe di Document Security Extension for Microsoft® Office {#adobe-rights-management-extension-for-microsoft-office}

Clic [qui](https://www.adobe.com/it/products/livecycle/rightsmanagement/extension/downloads.html) per visualizzare i requisiti di sistema per Adobe Document Security Extension for Microsoft® Office.

### Eccezioni al supporto client {#exceptions-to-client-support}

AEM Forms su JEE supporta aggiornamenti, patch e fix pack oltre alla versione principale e secondaria specificata del software supportato. Tuttavia, l’aggiornamento alla versione principale o secondaria successiva non è supportato, a meno che non sia specificato.

## Criteri di supporto delle patch di terze parti {#third-party-patch-support-policy}

I requisiti software di terze parti per AEM Forms su JEE sono documentati nella sezione &quot;Requisiti di sistema&quot; dei rispettivi documenti di prodotto. Accedi a tutta la documentazione da [https://adobe.com/go/learn_aemforms_documentation_65](https://adobe.com/go/learn_aemforms_documentation_65) .

AEM Forms sulle piattaforme di riferimento di terze parti di JEE indica il livello di patch specifico dell’infrastruttura di terze parti corrente durante lo sviluppo e il rilascio di AEM Forms su JEE e il livello minimo di patch/service pack dell’infrastruttura supportata da tale versione di AEM Forms su JEE.

Adobe supporta patch urgenti o consigliate rilasciate da fornitori di terze parti al momento del rilascio, presupponendo che i fornitori di terze parti garantiscano la compatibilità con le versioni supportate da AEM Forms su JEE. Adobe supporterà solo le patch rilasciate dopo il livello minimo di patch indicato nella documentazione di AEM Forms su JEE.

A volte, Adobe non supporta aggiornamenti di terze parti che modificano funzionalità principali e quindi non supportano la piena compatibilità con le versioni precedenti. Per informazioni dettagliate sugli aggiornamenti supportati, consulta [Definizioni di patch supportate](https://helpx.adobe.com/aem-forms/aem-forms-third-party-software-patch.html) per prodotti di fornitori specifici e i tipi di patch supportati dall’Adobe.

In circostanze che esulano dal controllo di Adobe, le patch di terze parti che rivendicano la compatibilità con le versioni precedenti possono avere un impatto negativo sui prodotti Adobe o sugli ambienti dei clienti. In questi casi, Adobe consiglia ai clienti di valutare l&#39;impatto di eventuali patch urgenti di terze parti prima di applicarle ai sistemi critici. Adobe collabora con terze parti utilizzando ragionevoli sforzi commerciali per risolvere tali problemi, sia attraverso normali programmi di supporto Adobe o da terze parti che rettificano il problema nella loro patch. Ciò non garantisce che una patch di terze parti appena rilasciata che sarà supportata da Adobe funzioni come documentato dal fornitore o con AEM Forms su JEE.

Adobe si riserva il diritto di modificare in qualsiasi momento le piattaforme di riferimento di terze parti supportate da una versione di AEM Forms su JEE e le relative definizioni di patch supportate.

Per ulteriori informazioni sulle patch di terze parti, visitare il sito di supporto Enterprise Adobe per trovare gli articoli della knowledgebase relativi al prodotto.

## Aggiornamenti della piattaforma {#platform-updates}

Le seguenti piattaforme sono contrassegnate come obsolete con la versione 6.5.13.0 di AEM Forms del 2 giugno 2022:

- Microsoft® SharePoint 2016

Le seguenti piattaforme sono contrassegnate come obsolete con la versione 6.5.12.0 di AEM Forms del 3 marzo 2022:

- MongoDB Enterprise 4.0
- IBM® DB2® 11.1
- Database Oracle 12c versione 2
- MySQL 5.7.35
- Driver JDBC Microsoft® SQL Server 6.2.1.0
- JBoss® Enterprise Application Platform (EAP) 7.1.4
- IBM® Content Manager Server 8.5 Fix Pack 2
- Client IBM® Content Manager 8.5
- Microsoft® SQL Server 2016

Le seguenti piattaforme sono contrassegnate come obsolete con la versione 6.5.10.0 di AEM Forms del 7 settembre 2021:

- Adobe Acrobat 2017 - [Il supporto di base per Adobe Acrobat 2017 termina il 6 giugno 2022](https://helpx.adobe.com/it/support/programs/eol-matrix.html).
- Microsoft® Windows Server 2016 (64 bit)
- Red Hat® Enterprise Linux® 7 (Kernel 3.x) (64 bit)
- Microsoft® Office 2016
- OpenOffice 4.1.2

>[!NOTE]
>
Piattaforme contrassegnate come [diventerà obsoleto il con AEM Forms 6.5.12.0 e 6.5.10.0 e rimarrà in supporto fino alla versione AEM Forms 6.5 Service Pack 18 (6.5.18.0)](https://helpx.adobe.com/it/support/programs/eol-matrix.html).

## Cronologia revisioni {#revision-history}

- 1 settembre 2022

   - È stato aggiunto il supporto per l’SDK Oracle Java™ SE 11 (64 bit) per il server applicazioni JBoss® EAP 7.4.

- 3 marzo 2022

   - È stato rimosso il supporto per i seguenti elementi:
      - Macchina virtuale IBM® J9 (build 2.8, JRE 1.8.0)
      - Database Oracle 12c versione 1
      - Database Oracle 18c
      - Oracle di directory unificata (OUD) 11g versione 2
      - IBM® Lotus Domino 9.0
      - IBM® FileNet 5.2
      - Flash Player Adobe

- 10 ottobre 2021

   - La versione supportata dell’app iOS for AEM Forms è stata modificata in iOS 15.1. La versione precedente era iOS 12.

- 7 settembre 2021
   - **Aggiornamenti della piattaforma**: [!DNL Adobe Experience Manager Forms] in JEE è stato aggiunto il supporto per le seguenti piattaforme:
      - [!DNL Adobe Acrobat 2020]
      - [!DNL Ubuntu 20.04]
      - [!DNL Open Office 4.1.10]
      - [!DNL Microsoft® Office 2019]
      - [!DNL Microsoft® Windows Server 2019]
      - [!DNL RHEL8]

- 3 dicembre 2020
   - È stato aggiunto il supporto per AEM Forms 6.5.7.0 o versione successiva per la seguente piattaforma:
      - [!DNL Microsoft® SQL Server 2019]

- 9 settembre 2020

   - La versione supportata dell’app iOS for AEM Forms è stata modificata in iOS 12. La versione precedente era iOS 11.

