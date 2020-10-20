---
title: Requisiti tecnici
seo-title: Requisiti tecnici
description: Elenco delle piattaforme client e server supportate per AEM.
seo-description: Elenco delle piattaforme client e server supportate per AEM.
uuid: 597f8fc1-9ac7-458d-a7c1-f576dd0f189b
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
discoiquuid: 16c7a97d-884a-447e-9aad-18a2db1bda1d
docset: aem65
translation-type: tm+mt
source-git-commit: 7065a6b984afb18c188acd848b9b77da7da67749
workflow-type: tm+mt
source-wordcount: '3118'
ht-degree: 1%

---


# Requisiti tecnici{#technical-requirements}

 Adobe supporta Adobe Experience Manager (AEM) sulle piattaforme come descritto nelle seguenti informazioni in questo documento.

Per eventuali problemi relativi alla piattaforma, contattate il fornitore della piattaforma.

>[!NOTE]
>
>A seconda della piattaforma su cui installate AEM, potrebbero essere presenti diversi set di requisiti per la gestione degli utenti.

## Prerequisiti {#prerequisites}

Requisiti minimi per l’installazione di Adobe Experience Manager:

* Piattaforma Java installata, JDK Standard Edition o altre macchine virtuali [Java supportate](#java-virtual-machines)
*  file Quickstart Experience Manager (JAR indipendente o WAR per la distribuzione di applicazioni Web)

### Requisiti minimi di dimensionamento {#minimum-sizing-requirements}

Requisiti minimi per l’esecuzione di Adobe Experience Manager:

* 5 GB di spazio libero su disco nella directory di installazione
* 2 GB di memoria

>[!NOTE]
>
>* I casi di utilizzo delle risorse digitali necessitano di una maggiore memoria di base. Per [informazioni dettagliate, consultate Implementazione e manutenzione](/help/sites-deploying/deploy.md#default-local-install) .
>* [pacchetto](/help/forms/using/installing-configuring-aem-forms-osgi.md) aggiuntivo AEM Forms richiede 15 GB di spazio temporaneo.

>



Per ulteriori informazioni, consultate le linee guida [sul ridimensionamento dell&#39;](/help/managing/hardware-sizing-guidelines.md)hardware.

### Livelli di supporto {#support-levels}

In questo documento sono elencate le piattaforme client e server supportate per Adobe Experience Manager.  Adobe offre diversi livelli di supporto, sia per le configurazioni consigliate che per altre configurazioni.

### Configurazioni supportate {#supported-configurations}

 Adobe consiglia queste configurazioni e fornisce supporto completo nell&#39;ambito del contratto standard di manutenzione del software.

<table>
 <tbody>
  <tr>
   <td>Livello di supporto</td>
   <td>Descrizione<br /> </td>
  </tr>
  <tr>
   <td><strong>A: Supportato</strong></td>
   <td> Adobe fornisce supporto e manutenzione completi per questa configurazione. Questa configurazione è coperta  processo  garanzia della qualità.</td>
  </tr>
  <tr>
   <td><strong>R: Supporto limitato</strong></td>
   <td>Per garantire il successo del progetto dei nostri clienti,  Adobe fornisce supporto completo nell'ambito di un programma di supporto limitato, che richiede il rispetto di condizioni specifiche. Il supporto a livello R richiede una richiesta formale del cliente e una conferma da parte  Adobe. Per ulteriori informazioni, contatta  Assistenza clienti di Adobe.</td>
  </tr>
 </tbody>
</table>

### Configurazioni non supportate {#unsupported-configurations}

| Livello di supporto | Descrizione |
|---|---|
| **Z: Non supportato** | La configurazione non è supportata.  Adobe non fornisce alcuna istruzione sul funzionamento della configurazione e non la supporta. |

## Piattaforme supportate {#supported-platforms}

### Java Virtual Machines {#java-virtual-machines}

L&#39;applicazione richiede l&#39;esecuzione di una macchina virtuale Java, fornita dalla distribuzione Java Development Kit (JDK).

Adobe Experience Manager funziona con le seguenti versioni di Java Virtual Machines:

>[!CAUTION]
>
>Si consiglia di tenere traccia dei bollettini sulla sicurezza dal fornitore Java per garantire la sicurezza degli ambienti di produzione e installare gli aggiornamenti Java più recenti.

<table>
 <tbody>
  <tr>
   <td>Platform</td>
   <td>Livello di supporto</td>
  </tr>
  <tr>
   <td>Oracle Java SE 12 JDK [1]</td>
   <td>Z: Non supportato </td>
  </tr>
  <tr>
   <td><strong>Oracle Java SE 11 JDK - 64 bit</strong></td>
   <td>A: Supportato</td>
  </tr>
  <tr>
   <td>Oracle Java SE 10 JDK [1]</td>
   <td>Z: Non supportato </td>
  </tr>
  <tr>
   <td>Oracle Java SE 9 JDK [1]</td>
   <td>Z: Non supportato</td>
  </tr>
  <tr>
   <td>Oracle Java SE 8 JDK - 64 bit</td>
   <td>A: Supportato [3]</td>
  </tr>
  <tr>
   <td>VM IBM J9 - build 2.9, JRE 1.8.0 [2]</td>
   <td>A: Supportato</td>
  </tr>
  <tr>
   <td>VM IBM J9 - build 2.8, JRE 1.8.0 [2]</td>
   <td>A: Supportato</td>
  </tr>
 </tbody>
</table>

1. Oracle è passato al modello “Long Term Support” (LTS) per i prodotti Oracle Java SE. Java 9, Java 10, and Java 12 are non-LTS releases by Oracle (see [Oracle Java SE support roadmap](https://www.oracle.com/technetwork/java/eol-135779.html)). Per distribuire AEM in ambiente di produzione,  Adobe fornisce supporto solo per le release LTS di Java.

1. IBM JRE è supportato solo insieme a WebSphere Application Server.
1. Il supporto e la distribuzione di Oracle Java SE JDK, compresi tutti gli aggiornamenti di manutenzione delle release LTS oltre la fine degli aggiornamenti pubblici, saranno supportati da  Adobe direttamente per tutti AEM clienti che utilizzano la tecnologia Oracle Java SE. Per ulteriori informazioni, vedere il supporto [Oracle Java per le domande e risposte](assets/adobe-oracle-java-license-agreement.pdf) di Adobe Experience Manager.

### Storage e persistenza {#storage-persistence}

Esistono diverse opzioni per distribuire l&#39;archivio di Adobe Experience Manager. Vedere l&#39;elenco seguente per le tecnologie supportate e le opzioni di storage.

| **Platform** | **Descrizione** | **Livello di supporto** |
|---|---|---|
| **File system con file TAR** `[1]` | Archivio | A: Supportato |
| **File system with Datastore** `[1]` | Binari | A: Supportato |
| Archiviare i file binari nei file TAR sul file system `[1]` | Binari | Z: Non supportato per la produzione |
|  Amazon S3 | Binari | A: Supportato |
| Archiviazione BLOB di Microsoft Azure | Binari | A: Supportato |
| MongoDB Enterprise 4.0 | Archivio | A: Supportato `[2, 3]` |
| MongoDB Enterprise 3.6 | Archivio | Z: Non supportato |
| MongoDB Enterprise 3.4 | Archivio | Z: Non supportato |
| IBM DB2 10.5 | Repository e database Forms | R: Supporto limitato `[4]` |
| Oracle Database 12c (12.1.x) | Repository e database Forms | R: Supporto limitato |
| Microsoft SQL Server 2016 | Database Forms | A: Supportato |
| **Apache Lucene (Introduzione rapida)** | Servizio di ricerca | A: Supportato |
| Apache Solr | Servizio di ricerca | A: Supportato |

1. Il file system include l&#39;archiviazione a blocchi conforme con POSIX. Ciò include la tecnologia di storage in rete. Tenere presente che le prestazioni del file system potrebbero variare e influenzare le prestazioni complessive. Si consiglia di caricare AEM di prova in combinazione con il file system di rete/remoto.
1. Lo Shopping MongoDB non è supportato in AEM.
1. MongoDB Storage Engine WiredTiger è supportato solo.
1. Supportato per  clienti AEM Forms. Non supportato per le nuove installazioni.

>[!NOTE]
>
>Consultate [Distribuzione di community](/help/communities/deploy-communities.md) per ulteriori informazioni sulla funzionalità di AEM Communities .

>[!NOTE]
>
>MongoDB è un software di terze parti e non è incluso nel pacchetto di licenze AEM. Per ulteriori informazioni, vedere la pagina relativa ai criteri [di licenza](https://www.mongodb.org/about/licensing/) MongoDB.
>
>Per ottenere il massimo dalla distribuzione AEM con MongoDB,  Adobe consiglia di concedere in licenza la versione Enterprise di MongoDB per beneficiare del supporto professionale. Per ulteriori informazioni, consultate [Implementazioni](/help/sites-deploying/recommended-deploys.md#prerequisites-and-recommendations-when-deploying-aem-with-mongomk) consigliate.
>
>La licenza include un set di repliche standard, composto da una delle istanze primarie e due secondarie che possono essere utilizzate per l&#39;autore o per le distribuzioni di pubblicazione.
>
>Se si desidera eseguire sia l&#39;autore che la pubblicazione su MongoDB, è necessario acquistare due licenze separate.
>
> Assistenza clienti di Adobe assisterà i problemi di qualificazione relativi all&#39;utilizzo di MongoDB con AEM.
>
>Per ulteriori informazioni, vedere la pagina [](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)MongoDB per Adobe Experience Manager.

>[!NOTE]
>
>I database relazionali supportati elencati sopra sono software di terze parti e non sono inclusi nel pacchetto di licenze AEM.
>
>Per eseguire AEM 6.5 con un database relazionale supportato, è necessario un contratto di assistenza separato con un fornitore di database.  Assistenza clienti di Adobe assisterà i problemi di qualificazione relativi all&#39;utilizzo di database relazionali con AEM 6.5.
>
>**La maggior parte dei database relazionali sono attualmente supportati all&#39;interno del livello R sul AEM 6.5, che include criteri di supporto e un programma di supporto come indicato nella descrizione di livello R precedente.**

### Motori Servlet / Server applicazioni {#servlet-engines-application-servers}

Adobe Experience Manager può essere eseguito come server autonomo (il file JAR di avvio rapido) o come applicazione Web all&#39;interno di un server applicazione di terze parti (il file WAR).

Versione minima dell&#39;API Servlet richiesta è Servlet 3.1

| Platform | Livello di supporto |
|---|---|
| **Motore Servlet integrato Quickstart (Jetty 9.4)** | A: Supportato |
| Oracle WebLogic Server 12.2 (12cR2) | Z: Non supportato |
| IBM WebSphere Application Server Continuous Delivery (LibertyProfile) con profilo Web 7.0 e IBM JRE 1.8 | R: Sostegno limitato per i nuovi contratti `[2]` |
| IBM WebSphere Application Server 9.0 e IBM JRE 1.8 | R: Sostegno limitato per i nuovi contratti `[1]` `[2]` |
| Apache Tomcat 8.5.x | R: Sostegno limitato per i nuovi contratti `[2]` |
| JBoss EAP 7.2.x con Application Server JBoss | Z: Non supportato |
| JBoss EAP 7.1.4 con Application Server JBoss | R: Sostegno limitato per i nuovi contratti `[1]` `[2]` |
| JBoss EAP 7.0.x con Application Server JBoss | Z: Non supportato |

1. Consigliato per le distribuzioni con  AEM Forms.
1. L&#39;avvio AEM distribuzioni 6.5 sui server applicazioni consente di passare al supporto limitato. I clienti esistenti possono effettuare l&#39;aggiornamento a AEM 6.5 e continuare a utilizzare i server delle applicazioni. Per i nuovi clienti è dotato di criteri di supporto e di un programma di supporto come indicato nella descrizione di livello R precedente.

### Sistemi operativi server {#server-operating-systems}

Adobe Experience Manager funziona con le seguenti piattaforme server per gli ambienti di produzione:

| **Platform** | **Livello di supporto** |
|---|---|
| **Linux, basato sulla distribuzione Red Hat** | A: Supportato `[1]` `[3]` |
| Linux, basato sulla distribuzione Debian incl. Ubuntu | A: Supportato `[2]` |
| Linux, basato sulla distribuzione SUSE | A: Supportato |
| Microsoft Windows Server 2019 `[4]` | R: Sostegno limitato per i nuovi contratti |
| Microsoft Windows Server 2016 `[4]` | R: Sostegno limitato per i nuovi contratti `[5]` |
| Microsoft Windows Server 2012 R2 | Z: Non supportato |
| Oracle Solaris 11 | Z: Non supportato |
| IBM AIX 7.2 | Z: Non supportato |

1. Linux Kernel 2.6, 3.x e 4.x include derivati dalla distribuzione Red Hat, tra cui Red Hat Enterprise Linux, CentOS, Oracle Linux e  Amazon Linux.  funzioni aggiuntive di AEM Forms sono supportate solo su CentOS 7 e Red Hat Enterprise Linux 7.
1.  AEM Forms è supportato solo su Ubuntu 16.04 LTS
1. Distribuzione Linux supportata da Adobe Managed Services
1. Le distribuzioni di produzione di Microsoft Windows sono supportate per i clienti che effettuano l&#39;aggiornamento alla versione 6.5 e per l&#39;utilizzo in modalità non di produzione. Le nuove distribuzioni sono su richiesta per  AEM Sites e Assets.
1.  AEM Forms è supportato su Microsoft Windows Server senza le restrizioni del livello di supporto R

### Ambienti di elaborazione virtuali e cloud {#virtual-cloud-computing-environments}

Adobe Experience Manager è supportato in esecuzione in una macchina virtuale in ambienti cloud computing, come Microsoft Azure e  Amazon Web Services (AWS), in conformità ai requisiti tecnici elencati in questa pagina e in base  termini di supporto standard del Adobe.

 Adobe consiglia di utilizzare Adobe Managed Services per distribuire AEM in Azure o AWS. Adobe Managed Services offre agli esperti esperienza e competenze per la distribuzione e il AEM operativo in questi ambienti cloud computing. Consulta la documentazione [aggiuntiva sui servizi](https://www.adobe.com/marketing-cloud/enterprise-content-management/managed-services-cloud-platform.html?aemClk=t)gestiti Adobe.

In tutti gli altri casi di implementazione di AEM in Azure o AWS, o in qualsiasi altro ambiente cloud computing, il supporto da  Adobe sarà contenuto nell&#39;ambiente di elaborazione virtuale in conformità alle specifiche tecniche elencate in questa pagina. Eventuali problemi segnalati relativi alle AEM in esecuzione in uno di questi ambienti cloud dovranno essere riproducibili indipendentemente da qualsiasi servizio cloud specifico per l&#39;ambiente cloud computing, a meno che il servizio cloud non sia specificamente supportato come parte dei requisiti tecnici elencati in questa pagina, ad esempio archiviazione Azure Blob o AWS S3.

Per raccomandazioni su come distribuire AEM su Azure o AWS, al di fuori dei servizi gestiti di Adobe,  Adobe consiglia vivamente di lavorare direttamente con il provider cloud o  partner di Adobe che supportano la distribuzione di AEM nell&#39;ambiente cloud di vostra scelta. Il fornitore o il partner cloud selezionato sarà responsabile delle specifiche di dimensionamento, della progettazione e dell&#39;implementazione dell&#39;architettura., per soddisfare i requisiti specifici di prestazioni, carico, scalabilità e sicurezza.

### Piattaforme Dispatcher (server Web) {#dispatcher-platforms-web-servers}

Il Dispatcher è il componente per il caching e il bilanciamento del carico. [Scarica la versione](https://helpx.adobe.com/experience-manager/dispatcher/release-notes.html)più recente del dispatcher.  Experience Manager 6.5 richiede il dispatcher versione 4.3.2 o successiva.

I seguenti server Web sono supportati per l’utilizzo con Dispatcher versione 4.3.2:

| Platform | Livello di supporto |
|---|---|
| **Apache httpd 2.4.x** `[1,2]` | A: Supportato |
| Microsoft IIS 10 (Internet Information Server) | A: Supportato |
| Microsoft IIS 8.5 (Internet Information Server) | Z: Non supportato |

1. I server Web basati sul codice sorgente httpd Apache avranno lo stesso livello di supporto della versione di httpd su cui si basa. In caso di dubbi, chiedere  Adobe la conferma del livello di supporto relativo al rispettivo prodotto server. Seguenti casi:

   1. Il server HTTP è stato creato utilizzando solo le distribuzioni di origine Apache ufficiali, oppure
   1. Il server HTTP è stato distribuito come parte del sistema operativo su cui è in esecuzione. Esempi: IBM HTTP Server, Oracle HTTP Server

1. Dispatcher non disponibile per Apache 2.4.x per i sistemi operativi Windows.

## Piattaforme client supportate {#supported-client-platforms}

### Browser supportati per l’authoring dell’interfaccia utente {#supported-browsers-for-authoring-user-interface}

L&#39;interfaccia utente di Adobe Experience Manager funziona con le seguenti piattaforme client. Tutti i browser vengono testati con il set predefinito di plug-in e componenti aggiuntivi.

L&#39;interfaccia utente AEM è ottimizzata per schermi più grandi (in genere notebook e computer desktop) e per fattori di forma per tablet (come Apple iPad o Microsoft Surface). Il fattore forma telefono non è supportato.

>[!NOTE]
>
>**Supporto per browser con cicli di rilascio rapidi:**
>
>Mozilla Firefox, Google Chrome e Microsoft Edge rilasciano aggiornamenti ogni pochi mesi.  Adobe si impegna a fornire aggiornamenti per Adobe Experience Manager per mantenere il livello di supporto come indicato di seguito con le prossime versioni di questi browser.

<table>
 <tbody>
  <tr>
   <td><strong>Browser</strong></td>
   <td><strong>Supporto per l'interfaccia utente<br /> </strong></td>
   <td><strong>Supporto per l’interfaccia classica</strong></td>
  </tr>
  <tr>
   <td><strong>Google Chrome (Evergreen)</strong></td>
   <td>A: Supportato</td>
   <td>A: Supportato</td>
  </tr>
  <tr>
   <td>Microsoft Edge (Evergreen)</td>
   <td>A: Supportato</td>
   <td>A: Supportato</td>
  </tr>
  <tr>
   <td>Microsoft Internet Explorer 11</td>
   <td>Z: Non supportato</td>
   <td>Z: Non supportato</td>
  </tr>
  <tr>
   <td>Mozilla Firefox (Evergreen)</td>
   <td>A: Supportato</td>
   <td>A: Supportato</td>
  </tr>
  <tr>
   <td>Mozilla Firefox ultimo ESR [1]</td>
   <td>A: Supportato</td>
   <td>A: Supportato</td>
  </tr>
  <tr>
   <td>Apple Safari su macOS (Evergreen)</td>
   <td>A: Supportato</td>
   <td>A: Supportato</td>
  </tr>
  <tr>
   <td>Apple Safari 11.x su macOS</td>
   <td>Z: Non supportato</td>
   <td>Z: Non supportato</td>
  </tr>
  <tr>
   <td>Apple Safari su iOS 12.x</td>
   <td>A: Supportato [2]</td>
   <td>Z: Non supportato</td>
  </tr>
  <tr>
   <td>Apple Safari su iOS 11.x</td>
   <td>Z: Non supportato</td>
   <td>Z: Non supportato</td>
  </tr>
 </tbody>
</table>

1. Versione estesa di supporto Firefox [Ulteriori informazioni su mozilla.org](https://www.mozilla.org/en-US/firefox/organizations/faq/)
1. supporto per Apple iPad

### Browser supportati per i siti Web {#supported-browsers-for-websites}

In genere, il supporto dei browser per i siti Web sottoposti a rendering da  AEM Sites dipende dall&#39;implementazione AEM modelli di pagina, dalla progettazione e dall&#39;output di componenti ed è pertanto a controllo dell&#39;implementazione di tali parti.

### Client WebDAV {#webdav-clients}

**Microsoft Windows 7+**

Per connettersi con Microsoft Windows 7+ a un&#39;istanza AEM non protetta con SSL, in Windows deve essere abilitata l&#39;autenticazione di base sulla rete non protetta. Ciò richiede una modifica nel Registro di sistema di Windows del WebClient:

1. Individuate la sottochiave del Registro di sistema:

   * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters

1. Aggiungete la voce del Registro di sistema BasicAuthLevel a questa sottochiave con un valore pari o superiore a 2.

Per migliorare la reattività del client WebDav in Windows - vedere [Supporto Microsoft KB 2445570](https://support.microsoft.com/kb/2445570)

## Note aggiuntive sulla piattaforma {#additional-platform-notes}

Questa sezione contiene note speciali e informazioni più dettagliate sull’esecuzione di Adobe Experience Manager e dei relativi componenti aggiuntivi.

### IPv4 e IPv6 {#ipv-and-ipv}

Tutti gli elementi di Adobe Experience Manager (Instance, Dispatcher) possono essere installati nelle reti IPv4 e IPv6.

L&#39;operazione è perfetta, in quanto non è necessaria alcuna configurazione speciale. Potete semplicemente specificare un indirizzo IP utilizzando il formato appropriato per il tipo di rete, se necessario.

Ciò significa che, quando è necessario specificare un indirizzo IP, è possibile selezionare (come richiesto) da:

* un indirizzo IPv6, ad esempio `https://[ab12::34c5:6d7:8e90:1234]:4502`

* un indirizzo IPv4, ad esempio `https://123.1.1.4:4502`

* un nome server, ad esempio, `https://www.yourserver.com:4502`

* il caso predefinito di `localhost` verrà interpretato per le installazioni di rete IPv4 e IPv6, ad esempio, `https://localhost:4502`

### Requisiti per AEM Dynamic Media Add-on {#requirements-for-aem-dynamic-media-add-on}

AEM Contenuti multimediali dinamici è disabilitato per impostazione predefinita. Per [abilitare gli elementi multimediali](/help/assets/config-dynamic.md#enabling-dynamic-media)dinamici, consulta la sezione.

Con l’opzione Contenuti multimediali dinamici attivata, sono applicabili i seguenti requisiti tecnici aggiuntivi.

>[!NOTE]
>
>Questi requisiti di sistema si applicano **solo** se si utilizza la modalità Dynamic Media - Hybrid; Elemento multimediale dinamico - La modalità ibrida dispone di un server di immagini incorporato, certificato solo in alcuni sistemi operativi.
>
>Per i clienti di Dynamic Media che eseguono Dynamic Media - Modalità Scene7 ( **** cioè, modalità runmode), non sono previsti requisiti di sistema aggiuntivi; solo gli stessi requisiti di sistema AEM. File multimediali dinamici - L’architettura in modalità Scene7 utilizza il servizio basato su cloud e non il servizio incorporato in AEM.

#### Hardware {#hardware}

I seguenti requisiti hardware sono applicabili sia per Linux che per Windows:

* CPU Intel Xeon o AMD Opteron con almeno 4 core
* Almeno 16 GB di RAM

#### Linux {#linux}

Se utilizzate Dynamic Media su Linux, è necessario soddisfare i seguenti prerequisiti:

* RedHat Enterprise 7 o CentOS 7 e versioni successive con patch di correzione più recenti
* Sistema operativo a 64 bit
* Scambio disattivato (consigliato)
* SELinux disabilitato (vedere la nota seguente)

>[!NOTE]
>
>Se le impostazioni internazionali sono impostate in modo tale che LC_CTYPE non sia uguale a `en_US.UTF-8`, impedisce il funzionamento di Dynamic Media. Per visualizzare il valore corrispondente al tipo &quot;locale&quot; al prompt dei comandi. Se non è impostato su tale valore, impostare la variabile di ambiente LC_CTYPE sulla stringa vuota digitando &quot;export LC_CTYPE=&quot; prima di eseguire AEM.

>[!NOTE]
>
>**Disattivazione di SELLinux:** Image Server non funziona con SELLinux attivato. Questa opzione è attivata per impostazione predefinita. Per risolvere questo problema, modificate il file **/etc/selLinux/config** e modificate il valore SELLinux da:
>
>`SELINUX=enforcing` **a** `SELINUX=disabled`

>[!NOTE]
>
>**Architettura NUMA:** I sistemi con processori con AMD64 e Intel EM64T sono generalmente configurati come piattaforme NUMA (non uniformi Memory Architecture), il che significa che il kernel costruisce più nodi di memoria in fase di avvio anziché costruire un singolo nodo di memoria.
>
>Il costrutto a più nodi può determinare l&#39;esaurimento della memoria su uno o più nodi prima che gli altri si esauriscano. Quando si verifica l’esaurimento della memoria, il kernel può decidere di interrompere i processi (ad esempio, Image Server o Platform Server) anche se è disponibile memoria.
>
>Pertanto,  Adobe consiglia che, se si esegue un sistema di questo tipo, si spenga NUMA utilizzando l&#39;opzione **numa=off** boot per evitare che il kernel uccida questi processi.

>[!NOTE]
>
>**Il nome host del server deve risolvere:** Verificate che il nome host del server sia risolvibile in un indirizzo IP. Se ciò non è possibile, aggiungete il nome host completo e l&#39;indirizzo IP agli **/etc/hosts**:
>
>`<ip address> <fully qualified hostname>`

#### Windows {#windows}

* Microsoft Windows Server 2016
* Spazio di scambio pari ad almeno il doppio della quantità di memoria fisica (RAM)

Per utilizzare i contenuti multimediali dinamici in Windows, installare i redistribuibili di Microsoft Visual Studio 2010, 2013 e 2015 per x64 e x86.

Per Windows x64:

* Ottenere Microsoft Visual Studio 2010 ridistribuibile all&#39;indirizzo [https://www.microsoft.com/en-us/download/details.aspx?id=13523](https://www.microsoft.com/en-us/download/details.aspx?id=13523)
* Ottenere Microsoft Visual Studio 2013 ridistribuibile all&#39;indirizzo [https://www.microsoft.com/en-us/download/details.aspx?id=40784](https://www.microsoft.com/en-us/download/details.aspx?id=40784)
* Ottenere Microsoft Visual Studio 2015 ridistribuibile all&#39;indirizzo [https://www.microsoft.com/en-us/download/details.aspx?id=48145](https://www.microsoft.com/en-us/download/details.aspx?id=48145)

Per Windows x86:

* Ottenere Microsoft Visual Studio 2010 ridistribuibile all&#39;indirizzo [https://www.microsoft.com/en-in/download/details.aspx?id=5555](https://www.microsoft.com/en-in/download/details.aspx?id=5555)
* Ottenere Microsoft Visual Studio 2013 ridistribuibile all&#39;indirizzo [https://www.microsoft.com/en-in/download/details.aspx?id=40769](https://www.microsoft.com/en-in/download/details.aspx?id=40769)
* Ottenere Microsoft Visual Studio 2015 ridistribuibile all&#39;indirizzo [https://www.microsoft.com/en-us/download/details.aspx?id=52685](https://www.microsoft.com/en-us/download/details.aspx?id=52685)

#### MacOS {#macos}

* 10.9.x e versioni successive
* Supportato solo a scopo di prova e demo

### Requisiti per  AEM Forms PDF Generator {#requirements-for-aem-forms-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>Prodotto</strong></p> </th>
   <th><p><strong>Formati supportati per la conversione in PDF</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2017 classic track</a> ultima versione</td>
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
>* PDF Generator richiede la versione a 32 bit di [Acrobat 2017 Classic track versione 17.011.30078 o successiva](https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html) per eseguire la conversione.
>* PDF Generator supporta solo la versione a 32 bit per la vendita al dettaglio di Microsoft Office Professional Plus e di altri software richiesti per la conversione.
>* PDF Generator non supporta Microsoft Office 365.
>* Le conversioni di PDF Generator per OpenOffice sono supportate solo in Windows e Linux.
>* Le funzioni PDF,  Optimize PDF e  Export PDF OCR sono supportate solo in Windows.
>* Una versione di  Acrobat viene fornita con  AEM Forms per abilitare la funzionalità PDF Generator. È consigliabile accedere alla versione bundle solo a livello di programmazione con  AEM Forms, per tutta la durata della licenza AEM Forms , da utilizzare con  AEM Forms PDF Generator. Per ulteriori informazioni, consultate  descrizione del prodotto AEM Forms come da distribuzione ([locale](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html) o [Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html))&quot;

   >
   >
* Il servizio PDF Generator non supporta Microsoft Windows 10.

>



### Requisiti per  riscrittura dei metadati XMP AEM Assets {#requirements-for-aem-assets-xmp-metadata-write-back}

XMP riscrittura è supportata e abilitata per le piattaforme e i formati file seguenti:

* **Sistemi operativi:**

   * Linux (supporto delle applicazioni a 32 bit e 32 bit su sistemi a 64 bit). Per informazioni sull&#39;installazione delle librerie client a 32 bit, vedere [Come abilitare l&#39;estrazione XMP e la riscrittura su RedHat Linux](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html)a 64 bit.

   * Windows Server
   * Mac OS X (64 bit)

* **Formati** file: JPEG, PNG, TIFF, PDF, INDD, AI ed EPS.

### Requisiti per  AEM Assets per l&#39;elaborazione di risorse con metadati pesanti su Linux {#assetsonlinux}

Il processo XMPFilesProcessor richiede il funzionamento della libreria GLIBC_2.14. Utilizzate un kernel Linux che contiene GLIBC_2.14, ad esempio il kernel Linux versione 3.1.x. Migliora le prestazioni per l’elaborazione di risorse contenenti una grande quantità di metadati, come i file PSD. L&#39;utilizzo di una versione precedente di GLIBC genera un errore nei registri a partire da `com.day.cq.dam.core.impl.handler.xmp.NCommXMPHandler Failed to read XMP`.
