---
title: Piattaforme supportate per AEM Forms su JEE
description: Elenco dei componenti dell’infrastruttura richiesti e supportati per l’installazione di AEM Forms su JEE
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin
exl-id: 74d22cf4-56b2-48f5-92d9-928eaa134866
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on JEE,Platform Matrix
source-git-commit: 1d16a131bd185145d9ad55d88749535d7a2dd84a
workflow-type: tm+mt
source-wordcount: '4039'
ht-degree: 2%

---


# Piattaforme supportate per AEM Forms su JEE {#supported-platforms-for-aem-forms-on-jee}

## Piattaforme supportate {#supported-platforms}

<div class="preview">

Adobe ha rilasciato un [programma di installazione completo](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=it) con AEM 6.5 Forms Service Pack 18 (6.5.18.0) su JEE insieme ai programmi di installazione delle patch. Il programma di installazione completo supporta nuove piattaforme, mentre il programma di installazione delle patch include solo correzioni di bug.
Se stai eseguendo una nuova installazione o stai pianificando di utilizzare il software più recente per il tuo ambiente AEM 6.5 Forms su JEE, Adobe consiglia di utilizzare [il programma di installazione completo di AEM 6.5.18.0 Forms su JEE](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=it) rilasciato il 31 agosto 2023 invece del programma di installazione di AEM 6.5 Forms rilasciato l’8 aprile 2019 o di AEM 6.5.12 Forms Installer rilasciato il 3 marzo 2022.

</div>

### Livelli di supporto {#support-levels}

AEM Forms sul server JEE può essere configurato utilizzando qualsiasi combinazione di sistemi operativi, server applicazioni, database, driver di database, JDK, server LDAP e server e-mail supportati.

Questo documento elenca le piattaforme client e server supportate per AEM Forms su JEE. Adobe fornisce diversi livelli di supporto, sia per le configurazioni consigliate da Adobe che per altre configurazioni. Il documento elenca anche altri software supportati e le relative versioni, eccezioni, definizioni di patch e criteri di supporto delle patch software di terze parti.

>[!NOTE]
>
>- Per un elenco completo delle eccezioni alle piattaforme server supportate, vedere [Eccezioni alle piattaforme server supportate](../../forms/using/aem-forms-jee-supported-platforms.md#p-exceptions-to-supported-server-platforms-p).
>- AEM Forms su JEE supporta solo le versioni in inglese, francese, tedesco e giapponese dei sistemi operativi e delle applicazioni supportati.

### Criteri di aggiornamento e supporto

#### Installazione completa

- **Supporto dell&#39;aggiornamento per i programmi di installazione completi**: viene rilasciato un programma di installazione completo ogni sei versioni di AEM Service Pack. Ad esempio, è stato rilasciato un programma di installazione completo con 6.5.12.0 e 6.5.18.0 versioni SP. AEM Forms consente aggiornamenti diretti esclusivamente dagli ultimi due programmi di installazione completi. Ad esempio, AEM Forms semplifica gli aggiornamenti diretti alla versione 6.5.18.0 solo dagli ultimi due programmi di installazione completi, ovvero 6.5.12.0 e 6.5.6.0. Se è necessario eseguire l&#39;aggiornamento da un aggiornamento precedente, è possibile utilizzare un aggiornamento multi-hop per passare prima a una versione completa del programma di installazione supportata e quindi alla versione più recente.

- **Deprecazione e rimozione**: il supporto della piattaforma viene aggiornato a ogni versione completa del programma di installazione. Qualsiasi software contrassegnato come obsoleto nella matrice della piattaforma durante una versione con programma di installazione completo ha diritto a essere rimosso dalla matrice della piattaforma supportata in una versione successiva con programma di installazione completo, indicando la fine del supporto del software.

#### Service Pack

- **Copertura dei Service Pack**: Adobe fornisce supporto tecnico per gli ambienti AEM Forms che eseguono Service Pack rilasciati negli ultimi 18 mesi. Se la versione corrente non rientra in questa finestra di 18 mesi, Adobe consiglia vivamente di eseguire l’aggiornamento al service pack più recente per mantenere prestazioni, sicurezza e supporto continui ottimali.

- **Linee guida per l&#39;installazione delle patch**: quando si utilizzano i programmi di installazione delle patch per l&#39;aggiornamento, è fondamentale verificare che la versione completa del programma di installazione sottostante non sia precedente a più di due versioni. Ad esempio, durante l&#39;installazione del Service Pack 6.5.19.0, verificare che la versione del programma di installazione completo sottostante sia 6.5.18.0 o 6.5.12.0.

- **Supporto per l&#39;aggiornamento delle patch**: è possibile continuare l&#39;aggiornamento al service pack più recente fino a quando non si esegue l&#39;aggiornamento anche alle piattaforme supportate più recenti. Ad esempio, è possibile eseguire l&#39;aggiornamento dal service pack 6.5.12.0 a 6.5.19.0, purché si passi a una combinazione di piattaforme supportata per 6.5.19.0.

### Configurazioni consigliate {#recommendedconfigurations}

Adobe consiglia queste configurazioni e fornisce supporto completo o limitato come parte del contratto standard di manutenzione software:

<table>
 <tbody>
  <tr>
   <th>Livello di supporto</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>R: Supportato<br /> </td>
   <td>Adobe fornisce supporto e manutenzione completi per questa configurazione. Questa configurazione è coperta dal processo di controllo qualità di Adobe.</td>
  </tr>
  <tr>
   <td>R: supporto limitato</td>
   <td>Adobe fornisce il supporto completo per questa configurazione dopo aver soddisfatto alcuni prerequisiti. Contatta il supporto Enterprise di Adobe per scoprire i prerequisiti e inoltrare una richiesta di supporto.</td>
  </tr>
  <tr>
   <td>L: Supporto limitato</td>
   <td>Adobe fornisce supporto e manutenzione completi per questa configurazione dopo aver soddisfatto alcuni prerequisiti. Non tutte le funzionalità sono disponibili nella configurazione. Contatta il supporto Enterprise di Adobe per scoprire i prerequisiti e inoltrare una richiesta per il supporto.<br /> </td>
  </tr>
 </tbody>
</table>

### Configurazioni non supportata {#unsupported-configurations}

| Livello di supporto | Descrizione |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| E: Funzionamento previsto | La configurazione dovrebbe funzionare, e non ci sono report che indicano il contrario. |
| Z: non supportato | La configurazione non è supportata. Adobe non fornisce alcuna istruzione sul funzionamento o meno della configurazione e non la supporta. |

>[!NOTE]
>
>Per aiutare i clienti AEM Forms a ridurre il costo di proprietà, semplificare l’architettura di distribuzione e modernizzare lo stack di sviluppo, la piattaforma aziendale Adobe Experience Manager si sta allontanando dalle implementazioni basate su server applicazioni a favore delle implementazioni autonome basate su OSGi. Adobe continua a supportare lo stack AEM Forms JEE con una matrice ridotta di componenti dell’infrastruttura.
>
>Con il rilascio della versione 6.5, i componenti dell’infrastruttura che hanno l’utilizzo più basso tra i clienti di Adobe non sono più supportati, come segue:
>
>- Database IBM® DB2®
>- Sistemi operativi IBM® AIX® e Sun Solaris™
>
>Per le nuove installazioni, ove possibile, si consiglia di implementare AEM Forms sul moderno stack OSGi per utilizzare le ultime innovazioni relative a Adaptive Forms per le integrazioni di dati mobili, interattivi multicanale e back-end tramite il modello dati del modulo.
>
>Adobe riconosce che gli utenti esistenti devono continuare a distribuire AEM Forms sullo stack JEE. In tali scenari, Adobe richiede l’implementazione di AEM Forms JEE sull’infrastruttura supportata come descritto in questa documentazione. Se stai eseguendo l’aggiornamento a AEM 6.5 Forms e utilizzi una piattaforma non supportata nella versione precedente di AEM Forms, puoi contattare il supporto Adobe per assistenza sull’aggiornamento a una piattaforma supportata.

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
   <td><p>A: supportato</p> </td>
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
   <td>A: supportato</td>
   <td>Versioni minori e aggiornamenti</td>
  </tr>
  <tr>
   <td>Macchina virtuale IBM® J9 (build 2.9, JRE 1.8.0) IBM® JDK SR6-FP26<br /> </td>
   <td>A: supportato</td>
   <td>Versioni minori e aggiornamenti</td>
  </tr>
  <tr>
   <td>IBM® JAVA1.8.0_291(build 8.0.6.30)<br /> </td>
   <td>A: supportato</td>
   <td>Versioni minori e aggiornamenti</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>- Monitora i bollettini sulla sicurezza del fornitore Java™ per garantire la sicurezza degli ambienti di produzione e installa gli aggiornamenti Java™ più recenti.
>- AEM Forms su JEE supporta solo JVM a 64 bit negli ambienti di produzione.

### Persistenza di database e CRX {#databases-and-crx-persistence}

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
   <td><p> MongoDB Enterprise 5.0</p> </td>
   <td><p>Microkernel archivio</p> </td>
   <td><p>Funzione supportata</p> </td>
  </tr>
    <tr>
   <td><p> MongoDB Enterprise 6.0 </p> </td>
   <td><p>Microkernel archivio</p> </td>
   <td><p>Funzione supportata</p> </td>
  </tr>
   <tr>
   <td>Oracle Database 19c (Standard, Real Application Clusters (RAC) ed Enterprise Edition) </td>
   <td>Archivio Microkernal </td>
   <td>Funzione supportata</td>
  </tr>
  <tr>
   <td><p>Microkernel archivio</p> </td>
   <td><p>Funzione supportata</p> </td>
  </tr>
  <tr>
   <td><p>Microsoft® SQL Server 2019 </p> </td>
   <td><p>Microkernel archivio</p> </td>
   <td><p>Funzione supportata</p> </td>
  </tr>
  <tr>
   <td>IBM® DB2® 11.1 (obsoleto)</td>
   <td>Microkernel archivio</td>
   <td>R: supporto limitato</td>
  </tr>
  <tr>
  <tr>
   <td>MySQL 8.0.27</td>
   <td>-</td>
   <td>R: supporto limitato</td>
  </tr>
 </tbody>
</table>

- IBM® DB2® non è supportato per le nuove installazioni. È supportato solo per i clienti esistenti che eseguono l’aggiornamento ad AEM 6.5 Forms.
- MongoDB è un software di terze parti e non è incluso nel pacchetto di licenze di AEM. Per ulteriori informazioni, vedere [Criteri di gestione licenze MongoDB](https://www.mongodb.org/about/licensing/).
- Per ottenere il massimo dall’implementazione di AEM, Adobe consiglia di concedere la licenza per la versione Enterprise di MongoDB per usufruire di un supporto professionale.
- L’Assistenza clienti di Adobe assiste i problemi di qualificazione relativi all’utilizzo di MongoDB con AEM. Per ulteriori informazioni, vedere la pagina [MongoDB per Adobe Experience Manager](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager).
- &#39;File system&#39; include l&#39;archiviazione dei blocchi compatibile con POSIX. Ciò include la tecnologia di storage in rete. Tieni presente che le prestazioni del file system potrebbero variare e influenzare le prestazioni complessive. Si consiglia di caricare il test AEM con il file system di rete/remoto.
- È supportato solo MongoDB Storage Engine WiredTiger.
- Il partizionamento MongoDB non è supportato in AEM.
- AEM Forms su JEE non supporta MySQL per la persistenza RDBMK.
- Il modulo Document Security non utilizza l’archivio dei contenuti. Ciò significa che, se utilizzi solo Document Security e non prevedi di utilizzare HTML Workspace, HTML5 Forms o moduli adattivi, non installare il Content Repository.
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
   <td><p>Driver JDBC Microsoft® SQL Server 8.2.2<br /> </p> <p>sqljdbc8.jar</p> </td>
   <td><p>Scarica dal sito web Microsoft®.</p> </td>
  </tr>
  <tr>
   <td>Oracle</td>
   <td><p>Driver JDBC per Oracle Database 19.3.0.0.0</p> <p>ojdbc8.jar (versione 19.3.0.0.0)<br /> </p> </td>
   <td><p>Scarica dal <a href="https://www.oracle.com/database/technologies/appdev/jdbc-ucp-19c-downloads.html">sito Web Oracle</a>.</p> </td>
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
   <td>Server Oracle WebLogic 12.2.1 (12c R2) (obsoleto) <sup>[9]</sup></td>
   <td>A: supportato</td>
   <td>Service Pack e aggiornamenti critici</td>
  </tr>
  <tr>
   <td>Server Oracle WebLogic 14c <sup>[9]</sup></td>
   <td>A: supportato</td>
   <td>Service Pack e aggiornamenti critici</td>
  </tr>
  <tr>
   <td>Application Server IBM® WebSphere® 9.0.0.10 <sup>[1] [4]</sup><br /> </td>
   <td>A: supportato</td>
   <td>Service Pack e aggiornamenti critici</td>
  </tr>
  <tr>
   <td><p>JBoss® Enterprise Application Platform (EAP) 7.4 <sup>[2] [3] [7]</sup> </p> </td>
   <td><p>A: supportato</p> </td>
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
   <th><p><strong> Platform</strong></p> </th>
   <th><p><strong>Livello di supporto</strong></p> </th>
   <th><p><strong>Definizioni di patch supportate</strong></p> </th>
  </tr>
   <tr>
   <td>Microsoft® Windows Server 2019 (64 bit) (obsoleto)</td>
   <td>A: supportato</td>
   <td>Service Pack e aggiornamenti critici</td>
  </tr>
     <tr>
   <td>Microsoft® Windows Server 2022 (64 bit)</td>
   <td>A: supportato</td>
   <td>Service Pack e aggiornamenti critici</td>
  </tr>
  <tr>
   <td>Ubuntu 20.04</td>
   <td>A: supportato</td>
   <td>Service Pack e aggiornamenti critici</td>
  </tr>
  <tr>
   <td><p>Red Hat® Enterprise Linux® 9 (Kernel 4.x) (64 bit)</p> </td>
   <td><p>A: supportato</p> </td>
   <td><p>Versioni minori, aggiornamenti cumulativi e aggiornamenti critici</p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® Enterprise Linux® 8 (Kernel 4.x) (64 bit)</p> </td>
   <td><p>A: supportato</p> </td>
   <td><p>Versioni minori, aggiornamenti cumulativi e aggiornamenti critici</p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® Enterprise Linux® 7 (Kernel 3.x) (64 bit) (obsoleto)</td>
   <td><p>A: supportato</p> </td>
   <td><p>Versioni minori, aggiornamenti cumulativi e aggiornamenti critici</p> </td>
  </tr>
  <tr>
   <td><p>SUSE® Linux® Enterprise Server 12 (64 bit)</p> </td>
   <td><p>A: supportato</p> </td>
   <td><p>Service Pack, patch cumulative e aggiornamenti di sicurezza critici</p> </td>
  </tr>
  <tr>
   <td>Aggiornamento 3 di Oracle Linux® 7 (64 bit)</td>
   <td>A: supportato</td>
   <td>Service Pack, patch cumulative e aggiornamenti di sicurezza critici</td>
  </tr>
  <tr>
   <td>CentOS 7 (64 bit)<sup> [6]</sup></td>
   <td>A: supportato</td>
   <td>Service Pack, patch cumulative e aggiornamenti di sicurezza critici</td>
  </tr>
 </tbody>
</table>

#### Ambiente virtualizzato {#virtualized-environment}

Puoi eseguire AEM Forms su JEE in un computer fisico o in un ambiente virtuale. Tuttavia, se riscontri problemi con AEM Forms in un ambiente virtuale, prova a replicare il problema su un computer fisico. Se il problema persiste sul computer fisico, contatta il supporto Adobe per una risoluzione. Per i problemi che non è possibile replicare su un computer fisico, contattare il fornitore dell&#39;ambiente virtuale.

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
1. AEM Forms su JEE non supporta JDK con IBM® WebSphere® ad eccezione di IBM® JDK.
1. L’archivio CRX supporta la persistenza di tipi TarMK, MongoDB e database relazionali (RDBMK). Non è possibile avere due sistemi di database diversi tra il server applicazioni e il repository CRX. Tuttavia, in un ambiente AEM Forms su JEE, puoi utilizzare MongoMK con l’archivio CRX e un database relazionale supportato con il server applicazioni.
1. AEM Forms su JEE non supporta il server applicazioni WebSphere® su CentOS.
1. AEM Forms su JEE non supporta JBoss® RBAC (role-based access control).
1. AEM Forms su JEE supporta Oracle Java™ SE 11 (64 bit) SDK solo per il server applicazioni JBoss® EAP 7.4.
1. Le versioni JDK superiori a 1.8.0_281 non sono supportate per il server WebLogic. (FORMS-8498)
1. JDK 11.0.20 non è supportato per installare AEM Forms sul programma di installazione JEE. Per installare AEM Forms sul programma di installazione di JEE sono supportate solo JDK 11.0.19 o versioni precedenti.

<!-- 
1. [!DNL Microsoft&reg; Windows Server 2019] does not support [!DNL MySQL 5.7] and [!DNL JBoss&reg; EAP 7.1], [!DNL Microsoft&reg; Windows Server 2019] does not support turnkey installations for [!DNL Experience Manager Forms Service Pack 6.5.10.0 and later]. (CQDOC-18312) 
-->

Inoltre, considera i seguenti punti durante la scelta del software per le implementazioni Adobe AEM Forms su JEE:

- AEM Forms su JEE supporta aggiornamenti, patch e fix pack oltre alla versione principale e secondaria specificata del software supportato. Tuttavia, l’aggiornamento alla versione principale o secondaria successiva non è supportato, a meno che non sia specificato.
- Le installazioni basate su cluster non supportano la persistenza TarMK. Per informazioni sulla persistenza supportata, vedere [Scelta di un tipo di persistenza per un&#39;installazione di AEM Forms](/help/forms/using/choosing-persistence-type-for-aem-forms.md).
- AEM Forms su JEE supporta diversi software di terze parti in base ai [criteri di supporto software di terze parti](../../forms/using/aem-forms-jee-supported-platforms.md#p-third-party-patch-support-policy-p) di Adobe.
- AEM Forms sulle piattaforme di supporto JEE in base al supporto fornito da fornitori terzi. Alcune combinazioni potrebbero non essere consentite da fornitori di terze parti. Molti fornitori, ad esempio, non hanno certificato i propri server applicazioni con Oracle. Di conseguenza, anche AEM Forms su JEE non supporta queste combinazioni. Per assicurarsi di scegliere le versioni del software supportate, consultare la matrice di supporto anche per i fornitori di terze parti.
- AEM Forms su JEE non supporta lo standby a freddo di TarMK.
- AEM Forms su JEE non supporta il clustering verticale.
- AEM Forms su JEE non supporta il database MySQL in un ambiente cluster.
- Per l&#39;elenco delle piattaforme rimosse o aggiornate, vedere il documento [Riepilogo delle nuove funzioni di AEM 6.5 Forms](../../forms/using/whats-new.md).

### Server LDAP (facoltativo) {#ldap-servers-optional}

<table>
 <tbody>
  <tr>
   <th><p><strong>Prodotto (versione base)</strong></p> </th>
   <th><p><strong>Definizioni di patch supportate</strong></p> </th>
  </tr>
  <tr>
   <td>Microsoft® Active Directory 2016 (obsoleto)</td>
   <td>Rilascio di manutenzione e pacchetti di correzione</td>
  </tr>
  <tr>
   <td>Microsoft® Active Directory 2022</td>
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
   <td>7,3</td>
  </tr>
  <tr>
   <td>IBM® FileNet</td>
   <td>5.5.2.</td>
  </tr>
  <tr>
   <td>IBM® Content Manager Server (obsoleto) </td>
   <td>8.5 Fix pack 2</td>
  </tr>
  <tr>
   <td> Client IBM® Content Manager (obsoleto)</td>
   <td>8,5 </td>
  </tr>
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

### Considerazioni per PDF Generator {#software-support-for-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>Prodotto</strong></p> </th>
   <th><p><strong>Formati supportati per la conversione in PDF</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/it/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat Pro DC</a> ultima versione</td>
   <td>XPS, formati immagine (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML e HTM</td>
  </tr>

<tr>
   <td>Licenze Microsoft® Office 2021 Professional Plus, per vendite al dettaglio e volumi</td>
   <td>DOC, DOCX, XLS, XLSX, PPT, PPTX, RTF e TXT</td>
  </tr>
  <tr>
   <td>
    <strong>OpenOffice 4.1.15</strong>   </td>
   <td>
    ODT, ODP, ODS, ODG, ODF, SXW, SXI, SXC, SXD, XLS, XLSX, DOC, DOCX, PPT, PPTX, formati immagine (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, RTF e TXT<br>

</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
> - PDF Generator supporta solo le versioni in inglese, francese, tedesco e giapponese dei sistemi operativi e delle applicazioni supportati.
> - PDF Generator richiede Adobe Acrobat Pro DC (32 Bit) per eseguire la conversione.
> - PDF Generator supporta solo la versione a 32 bit di Microsoft® Office Professional Plus e di altro software necessario per la conversione.
> - Se un&#39;installazione di Microsoft® Office viene disattivata o priva di licenza per qualsiasi motivo, ad esempio se un&#39;installazione con licenza Volume License non è in grado di individuare un host KMS entro un determinato periodo di tempo, le conversioni potrebbero non riuscire fino a quando l&#39;installazione non viene rilasciata e riattivata.
> - PDF Generator non supporta Microsoft® Office 365.
> - Le conversioni PDF Generator per OpenOffice sono supportate solo su Windows e Linux®.
> - Le funzioni PDF, Ottimizza PDF e Export PDF di OCR sono supportate solo in Windows.
> - Una versione di Acrobat è inclusa in bundle con AEM Forms per abilitare le funzionalità di PDF Generator. Durante il periodo di validità della licenza di AEM Forms, è possibile accedere alla versione inclusa nel bundle solo a livello di programmazione con AEM Forms, utilizzabile solo con AEM Forms PDF Generator. Per ulteriori informazioni, consulta la descrizione del prodotto AEM Forms in base alla distribuzione ([On-Premise](https://helpx.adobe.com/it/legal/product-descriptions/adobe-experience-manager-on-premise.html) o [Managed Services](https://helpx.adobe.com/it/legal/product-descriptions/adobe-experience-manager-managed-services.html)).
> - Il servizio PDF Generator non supporta Microsoft® Windows 11.


<!-- Removed lines: >- PDF Generator fails to convert files using Microsoft&reg; Visio 2019. You can continue to use Microsoft&reg; Visio 2016 to convert .VSD and .VSDX files.
>- PDF Generator fails to convert files using Microsoft&reg; Project 2019. You can continue to use Microsoft&reg; Project 2016 to convert .MPP files.-->

### Eccezioni al supporto dell’accessibilità {#exceptions-to-accessibility-support}

I seguenti sottosistemi di AEM Forms non sono conformi a [508](https://www.section508.gov/):

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
   <td>Processore Intel Xeon® E5-2680, 2,4 GHz o equivalente<br /> VMWare ESX 5.1 o successivo<br /> RAM: 6 GB (sistema operativo a 64 bit con JVM a 64 bit)<br /> Spazio libero su disco: 15 GB di spazio temporaneo più 22 GB<br /> per AEM Forms su JEE</td>
  </tr>
  <tr>
   <td>SUSE® Linux® Enterprise Server</td>
   <td>Intel Xeon® E5-2670v2, 1 vCPU, processore 2,5 GHz<br /> AWS m3.medium (3 ECU)<br /> RAM: 6 GB (sistema operativo a 64 bit con JVM a 64 bit)<br /> Spazio libero su disco: 6 GB di spazio temporaneo più 22 GB<br /> per AEM Forms su JEE</td>
  </tr>
  <tr>
   <td>Red Hat® Enterprise Linux®</td>
   <td>Intel Xeon® E5-2670v2, 1 vCPU, processore 2,5 GHz<br /> AWS m3.medium (3 ECU)<br /> RAM: 6 GB (sistema operativo a 64 bit con JVM a 64 bit)<br /> Spazio libero su disco: 6 GB di spazio temporaneo più 22 GB<br /> per AEM Forms su JEE<br /> </td>
  </tr>
  <tr>
   <td>Requisiti hardware per un ambiente di produzione di piccole dimensioni</td>
   <td>
    <ul>
     <li><strong>Ambiente basato su Intel®</strong>: Intel Xeon® E5-2680 a 2,4 GHz o superiore. L'utilizzo di un processore dual-core migliorerà ulteriormente le prestazioni</li>
     <li><strong>Memoria: </strong>4 GB <br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

Per ulteriori informazioni, vedere:

- [Requisiti di sistema per una distribuzione AEM Forms su JEE per server singolo](https://www.adobe.com/go/learn_aemforms_sysreq_single_65_it)
- [Requisiti di sistema per una distribuzione AEM Forms in cluster su JEE](https://www.adobe.com/go/learn_aemforms_sysreq_cluster_65_it)

### Adobe Acrobat e Adobe Reader {#adobe-acrobat-and-adobe-reader}

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

</tbody>
</table>

>[!NOTE]
>
>La famiglia di prodotti Acrobat DC introduce due tracce per Acrobat e Reader, che sono prodotti diversi: &quot;Classic&quot; e &quot;Continuous&quot;. Per i dettagli e un confronto dei due brani, vedere [https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/whatsnewdc.html](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/whatsnewdc.html).

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
   <td>Server Microsoft® Windows® 2019 (obsoleto)</td>
   <td>Service Pack e aggiornamenti critici</td>
  </tr>
  <tr>
   <td>Server Microsoft® Windows® 2022</td>
   <td>Service Pack e aggiornamenti critici</td>
  </tr>
 </tbody>
</table>

- Spazio su disco per l&#39;installazione: 1,7 GB solo per Workbench, 2,7 GB su un&#39;unica unità per un&#39;installazione completa di Workbench, Designer e l&#39;assieme di esempio 400 MB per le directory di installazione temporanee: 200 MB nella directory temporanea dell&#39;utente e 200 MB nella directory temporanea di Windows. Se tutte queste posizioni si trovano su un&#39;unica unità, durante l&#39;installazione devono essere disponibili 1,5 GB di spazio. I file copiati nelle directory temporanee vengono eliminati al termine dell&#39;installazione.

- Memoria per l&#39;esecuzione di Workbench: 2 GB di RAM
- Requisiti hardware: processore Intel® Pentium® 4 o AMD® equivalente a 1 GHz
- Risoluzione minima del monitor 1024 X 768 pixel o superiore con colore a 16 bit o superiore
- Connessione di rete TCP/IPv4 o TCP/IPv6 al server AEM Forms su JEE
- Per installare Workbench in Windows è necessario disporre dei privilegi di amministratore. Se si sta effettuando l&#39;installazione utilizzando un account non amministratore, il programma di installazione richiederà le credenziali per un account appropriato.

### Designer {#designer}

- Microsoft® Windows® 2016 Server, Microsoft® Windows® 2019 Server, Microsoft® Windows® 10 o Windows® 11
- Processore da 1 GHz o superiore con supporto per PAE, NX e SSE2.
- 1 GB di RAM per 32 bit o 2 GB di RAM per sistema operativo a 64 bit
- 16 GB di spazio su disco per 32 bit o 20 GB di spazio su disco per sistema operativo a 64 bit
- Memoria grafica - 128 MB di GPU (consigliata 256 MB)
- 2,35 GB di spazio disponibile su disco rigido
- Risoluzione di 1024 X 768 pixel o superiore
- Accelerazione hardware video (opzionale)
- Acrobat Pro DC, Acrobat Standard DC o Adobe Acrobat Reader DC
- Privilegi amministrativi per l&#39;installazione di Designer
- Microsoft® Visual C++ 2019 (VC 14.28 o versione successiva), runtime a 32 bit

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
   <td><p>A: supportato</p> </td>
   <td><p>Service Pack e aggiornamenti</p> </td>
  </tr>
  <tr>
   <td><p>Mozilla Firefox (Evergreen)</p> </td>
   <td><p>A: supportato</p> </td>
   <td>Tutti gli aggiornamenti</td>
  </tr>
  <tr>
   <td>Mozilla Firefox ESR</td>
   <td>E: Funzionamento previsto</td>
   <td> Tutti gli aggiornamenti</td>
  </tr>
  <tr>
   <td><p>Google Chrome (Evergreen)</p> </td>
   <td><p>A: supportato</p> </td>
   <td>Tutti gli aggiornamenti</td>
  </tr>
  <tr>
   <td>Apple Safari su macOS</td>
   <td>A: supportato</td>
   <td>Tutti gli aggiornamenti</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Di seguito sono riportate alcune eccezioni relative al browser per i desktop:
>
>- Safari è supportato solo su Macintosh OS X.
>- Workspace supporta Safari 5.1 su Macintosh OS X 10.6 e 10.7 con Acrobat DC o versioni successive. Per ulteriori informazioni sulla compatibilità di Safari 5.1 con Acrobat Reader, vedi [https://helpx.adobe.com/x-productkb/multi/safari-5-1-incompatible-reader.html](https://helpx.adobe.com/x-productkb/multi/safari-5-1-incompatible-reader.html).
>- La console di amministrazione non è supportata in Safari.
>- Gestione corrispondenza non supporta Windows® Internet Explorer 9.0 per i moduli di AEM 6.1.
>- Forms Portal supporta il software JAWS 14.0 screen reader su Internet Explorer 11 per l&#39;accessibilità.

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
>- Forms Portal è supportato su Safari solo su iPad.

### app AEM Forms {#aem-forms-workspace-app}

#### Supporto per dispositivi mobili {#mobile-device-support}

L’app AEM Forms è disponibile sulle seguenti piattaforme:

| **Piattaforma** | **Dispositivi supportati** |
| ----------------- | ------------------------------------------------------------------------------------------------------------------- |
| Apple iOS | Apple iPhone, iPad, iPad Air e iPad mini con iOS 15.1 e versioni successive. |
| Google Android™ | Android™ 5.1 e versioni successive. L&#39;app AEM Forms è certificata su tablet Samsung Galaxy da 7 pollici e 10 pollici e smartphone popolari. |
| Microsoft® Windows | Dispositivi Microsoft® Surface, tablet, notebook e desktop con sistema operativo Microsoft® Windows 10. |

### Estensione Adobe Document Security per Microsoft® Office {#adobe-rights-management-extension-for-microsoft-office}

Fai clic [qui](https://www.adobe.com/it/products/livecycle/rightsmanagement/extension/downloads.html) per visualizzare i requisiti di sistema per Adobe Document Security Extension for Microsoft® Office.

### Eccezioni al supporto client {#exceptions-to-client-support}

AEM Forms su JEE supporta aggiornamenti, patch e fix pack oltre alla versione principale e secondaria specificata del software supportato. Tuttavia, l’aggiornamento alla versione principale o secondaria successiva non è supportato, a meno che non sia specificato.

## Criteri di supporto delle patch di terze parti {#third-party-patch-support-policy}

I requisiti software di terze parti per AEM Forms su JEE sono documentati nella sezione &quot;Requisiti di sistema&quot; dei rispettivi documenti di prodotto. Accedi a tutta la documentazione da [https://adobe.com/go/learn_aemforms_documentation_65_it](https://adobe.com/go/learn_aemforms_documentation_65_it) .

AEM Forms sulle piattaforme di riferimento di terze parti di JEE indica il livello di patch specifico dell’infrastruttura di terze parti corrente durante lo sviluppo e il rilascio di AEM Forms su JEE e il livello minimo di patch/service pack dell’infrastruttura supportata da tale versione di AEM Forms su JEE.

Adobe supporta patch urgenti o consigliate rilasciate da fornitori di terze parti al momento del rilascio, presupponendo che i fornitori di terze parti garantiscano la compatibilità con le versioni supportate da AEM Forms su JEE. Adobe supporterà solo le patch rilasciate dopo il livello minimo di patch indicato nella documentazione di AEM Forms su JEE.

A volte, Adobe non supporta aggiornamenti di terze parti che modificano funzionalità principali e quindi non supportano la piena compatibilità con le versioni precedenti. Per informazioni dettagliate sugli aggiornamenti supportati, vedere [Definizioni di patch supportate](https://helpx.adobe.com/aem-forms/aem-forms-third-party-software-patch.html) per prodotti specifici del fornitore e i tipi di patch supportati da Adobe.

In circostanze che esulano dal controllo di Adobe, le patch di terze parti che rivendicano la compatibilità con le versioni precedenti possono avere un impatto negativo sui prodotti Adobe o sugli ambienti dei clienti. In questi casi, Adobe consiglia ai clienti di valutare l’impatto di eventuali patch urgenti di terze parti prima di applicarle ai sistemi critici. Adobe collabora con terze parti utilizzando ragionevoli sforzi commerciali per risolvere tali problemi, sia tramite i normali programmi di supporto di Adobe che tramite terze parti che rettificano il problema nella loro patch. Ciò non garantisce che una patch di terze parti appena rilasciata che sarà supportata da Adobe funzioni come documentato dal fornitore o con AEM Forms su JEE.

Adobe si riserva il diritto di modificare in qualsiasi momento le piattaforme di riferimento di terze parti supportate da una versione di AEM Forms su JEE e le relative definizioni di patch supportate.

Per ulteriori informazioni sulle patch di terze parti, visitare il sito di assistenza Adobe Enterprise per trovare gli articoli della knowledge base relativi al prodotto.


>[!NOTE]
>
> Per qualsiasi query relativa ai formati o alle versioni della piattaforma supportati, contatta il supporto AEM Forms.


<!--

## Platform updates {#platform-updates}

The following platforms are marked as deprecated with AEM Forms 6.5.18.0 release on August 31, 2023:

- Microsoft&reg; Windows Server 2019 (64-bit)
- Microsoft&reg; Active Directory 2016

The following platforms are marked as deprecated with AEM Forms 6.5.13.0 release on June 2, 2022:
- Microsoft&reg; SharePoint 2016

The following platforms are marked as deprecated with AEM Forms 6.5.10.0 release on September 7, 2021:

- Adobe Acrobat 2017 - [Core support for Adobe Acrobat 2017 ends on June 6, 2022](https://helpx.adobe.com/it/support/programs/eol-matrix.html).
- Red Hat&reg; Enterprise Linux&reg; 7 (Kernel 3.x) (64-bit)
- Microsoft&reg; Windows Server 2016 (64-bit) 
- Microsoft&reg; Office 2016
- OpenOffice 4.1.2

-->


## Cronologia revisioni {#revision-history}

<!--

- 6.5.18.0 (Aug 31, 2023)
  - **Added support**: [!DNL Adobe Experience Manager Forms] on JEE has added support for the following platforms:
    - MongoDB Enterprise 4.4
    - Oracle WebLogic Server 14c
    - My SQL JDBC connector 8
    - Active Directory 2022
    - Microsoft&reg; Windows Server 2022 (64-bit)

  - **Removed support**: [!DNL Adobe Experience Manager Forms] on JEE has removed support for the following platforms:
    - Windows Server 2016 (64-bit)
    - MongoDB Enterprise 4.0
    - Oracle Database 12c Release 2 (12.2.0.1.0)
    - MySQL 5.7.35
    - Microsoft&reg; SQL Server 2016
    - JBoss&reg; EAP 7.1.4
    - My SQL JDBC connector 5.1.44
    - Microsoft&reg; SQL Server JDBC driver 6.2.1.0
    - Microsoft&reg; SQL Server JDBC driver 6.2.2.0
    - Microsoft&reg; JDBC Driver 8.x for SQL Server

    The release has also removed support for the following platforms for PDF Generator and in-general:
    - Microsoft&reg; Sharepoint 2016
    - Microsoft&reg; Office 2016
    - Microsoft&reg; Office Visio 2016 
    - Microsoft&reg; Publisher 2016
    - Microsoft&reg; Project 2016
    - OpenOffice 4.1.2
    - Acrobat 2017 (Classic track) Version 17.011.30078 or later

  - **Deprecated support**: [!DNL Adobe Experience Manager Forms] on JEE has deprecated the following platforms:
    - Microsoft&reg; Windows Server 2019 (64-bit)
    - Microsoft&reg; Active Directory 2016
    
- 6.5.13.0 (June 2, 2022)

  The following platforms are deprecated with AEM Forms 6.5.13.0 release on:
 
  - Microsoft&reg; SharePoint 2016

- 6.5.12.0 (March 3, 2022)

    - **Platform Updates**: [!DNL Adobe Experience Manager Forms] on JEE has removed support for the following platforms:
      - IBM&reg; J9 Virtual Machine (build 2.8, JRE 1.8.0)
      - Oracle Database 12c Release 1
      - Oracle Database 18c
      - Oracle Unified Directory (OUD) 11g Release 2
      - IBM&reg; Lotus Domino 9.0
      - IBM&reg; FileNet 5.2
      - Adobe Flash Player

    - **Platform Updates**: [!DNL Adobe Experience Manager Forms] on JEE has deprecated the following platforms:

      - MongoDB Enterprise 4.0
      - MongoDB Enterprise 4.2
      - IBM&reg; DB2&reg; 11.1
      - Oracle Database 12c Release 2
      - MySQL 5.7.35
      - Microsoft&reg; SQL Server JDBC driver 6.2.1.0
      - JBoss&reg; Enterprise Application Platform (EAP) 7.1.4
      - IBM&reg; Content Manager Server 8.5 Fix pack 2
      - IBM&reg; Content Manager Client 8.5
      - Microsoft&reg; SQL Server 2016

- 6.5.10.0 (Sep 01, 2022)

  - **Added support**: [!DNL Adobe Experience Manager Forms] on JEE has added support for the following platform:
  
    - Oracle Java&trade; SE 11 (64 bit) SDK for application server JBoss&reg; EAP 7.4.
  - **Deprecated support**: [!DNL Adobe Experience Manager Forms] on JEE has deprecated the following platforms:

    - Adobe Acrobat 2017 - [Core support for Adobe Acrobat 2017 ends on June 6, 2022](https://helpx.adobe.com/it/support/programs/eol-matrix.html).
    - Red Hat&reg; Enterprise Linux&reg; 7 (Kernel 3.x) (64-bit)
    - Microsoft&reg; Windows Server 2016 (64-bit) 
    - Microsoft&reg; Office 2016
    - OpenOffice 4.1.2


-->

### Versione 6.5.23.0 (luglio 2025)

| Supporto aggiunto | Supporto rimosso | Supporto obsoleto |
| -------------- | --------------- | ------------------- |
| Red Hat® Enterprise Linux® 9 (Kernel 4.x) (64 bit) |  |  |
| OpenOffice 4.1.15 | Microsoft Office 2019 |  |
| | Microsoft Publisher 2019 |  |
| | WordPerfect 2020 |  |
| | Microsoft Visio 2019 |  |
| | Microsoft Project 2019 |  |

### Versione 6.5.19.1 (15 dicembre 2023)

| Supporto aggiunto | Supporto rimosso | Supporto obsoleto |
| -------------- | --------------- | ------------------- |
| MongoDB Enterprise 6.0 | MongoDB Enterprise 4.4 |  |
| MongoDB Enterprise 5.0 |  |  |
|  | |  |

### Versione 6.5.18.0 (31 agosto 2023)

| Supporto aggiunto | Supporto rimosso | Supporto obsoleto |
| -------------- | --------------- | ------------------- |
| MongoDB Enterprise 4.4 | Windows Server 2016 (64 bit) | Microsoft® Windows Server 2019 (64 bit) |
| Server Oracle WebLogic 14c | MongoDB Enterprise 4.0 | Microsoft® Active Directory 2016 |
| Il mio connettore SQL JDBC 8 | Oracle Database 12c versione 2 (12.2.0.1.0) |  |
| Active Directory 2022 | MySQL 5.7.35 |  |
| Microsoft® Windows Server 2022 (64 bit) | Microsoft® SQL Server 2016 |  |
|  | JBoss® EAP 7.1.4 |  |
|  | Il mio connettore SQL JDBC 5.1.44 |  |
|  | Driver JDBC Microsoft® SQL Server 6.2.1.0 |  |
|  | Driver JDBC Microsoft® SQL Server 6.2.2.0 |  |
|  | Driver Microsoft® JDBC 8.x per SQL Server |  |
|  |  |  |
|  | **Supporto rimosso (PDF Generator e In generale):** |  |
|  | Microsoft® Sharepoint 2016 |  |
|  | Microsoft® Office 2016 |  |
|  | Microsoft® Office Visio 2016 |  |
|  | Microsoft® Publisher 2016 |  |
|  | Microsoft® Project 2016 |  |
|  | OpenOffice 4.1.2 |  |
|  | Acrobat 2017 (Classic track) versione 17.011.30078 o successiva |  |


### Versione 6.5.13.0 (2 giugno 2022)

| Supporto aggiunto | Supporto rimosso | Supporto obsoleto |
| -------------- | --------------- | ------------------- |
|  |  | Microsoft® SharePoint 2016 |


### Versione 6.5.12.0 (3 marzo 2022)

| Supporto aggiunto | Supporto rimosso | Supporto obsoleto |
| -------------- | --------------- | ------------------- |
|  | Macchina virtuale IBM® J9 (build 2.8, JRE 1.8.0) | MongoDB Enterprise 4.0 |
|  | Oracle Database 12c versione 1 | MongoDB Enterprise 4.2 |
|  | Oracle Database 18c | IBM® DB2® 11.1 |
|  | Oracle Unified Directory (OUD) 11g versione 2 | Oracle Database 12c versione 2 |
|  | IBM® Lotus Domino 9.0 | MySQL 5.7.35 |
|  | IBM® FileNet 5.2 | Driver JDBC Microsoft® SQL Server 6.2.1.0 |
|  | Adobe Flash Player | JBoss® Enterprise Application Platform (EAP) 7.1.4 |
|  | | IBM® Content Manager Server 8.5 Fix Pack 2 |
|  | | Client IBM® Content Manager 8.5 |
|  | | Microsoft® SQL Server 2016 |
|  | | Microsoft® Windows Server 2016 |

### Versione 6.5.10.0 (1 settembre 20222)

| Supporto aggiunto | Supporto rimosso | Supporto obsoleto |
| -------------- | --------------- | ------------------- |
| Oracle Java™ SE 11 (64 bit) SDK per il server applicazioni JBoss® EAP 7.4. | | [Adobe Acrobat 2017 - Il supporto di base per Adobe Acrobat 2017 termina il 6 giugno 2022.](https://helpx.adobe.com/it/support/programs/eol-matrix.html) |
|  | Red Hat® Enterprise Linux® 7 (Kernel 3.x) (64 bit) | |
|  | | Microsoft® Windows Server 2016 (64 bit) |
|  | | Microsoft® Office 2016 |
|  | | OpenOffice 4.1.2 |


>[!NOTE]
>
> Una piattaforma obsoleta continua a ricevere supporto fino alla prossima versione dell’installatore completo o, se precedente, fino a quando il supporto di terze parti non raggiunge la fine del ciclo di vita.

<!-- 
- Oct 10, 2021

  - Changed supported version of iOS for AEM Forms App to iOS 15.1. The previous version was iOS 12.

- Sep 07, 2021
  - **Platform Updates**: [!DNL Adobe Experience Manager Forms] on JEE has added support for the following platforms:
    - [!DNL Adobe Acrobat 2020]
    - [!DNL Ubuntu 20.04]
    - [!DNL Open Office 4.1.10]
    - [!DNL Microsoft&reg;&reg; Office 2016]
    - [!DNL Microsoft&reg;&reg; Windows Server 2016]
    - [!DNL RHEL8]

- Dec 03, 2020
  - Support added with AEM Forms 6.5.7.0 or later for the following platform:
    - [!DNL Microsoft&reg;&reg; SQL Server 2019]

- Sep 09, 2020

    - Changed supported version of iOS for AEM Forms App to iOS 12. The previous version was iOS 11.

    -->

