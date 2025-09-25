---
title: Requisiti tecnici
description: Elenco delle piattaforme client e server supportate per Adobe Experience Manager.
topic-tags: platform
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
exl-id: 47529b9a-c4e5-434f-ac26-b01714ff863b
source-git-commit: 6fd6b5182dfb51fa0563c7eb191ba0d0cc85b113
workflow-type: tm+mt
source-wordcount: '3539'
ht-degree: 5%

---

# Requisiti tecnici{#technical-requirements}

Adobe supporta (AEM) Adobe Experience Manager sulle piattaforme come descritto nelle informazioni seguenti in questo documento.

Per qualsiasi problema relativo alla piattaforma, contatta il fornitore della piattaforma.

>[!NOTE]
>
>A seconda della piattaforma su cui installi AEM, potrebbero esserci diversi set di requisiti per la gestione degli utenti.

## Prerequisiti {#prerequisites}

Requisiti minimi per l&#39;installazione di Adobe Experience Manager:

* Installato Java™ Platform, Standard Edition JDK o altri [Java™ Virtual Machine](#java-virtual-machines) supportati
* File Experience Manager Quickstart (file JAR autonomo o WAR di implementazione di un’applicazione web)

### Requisiti di dimensionamento minimo {#minimum-sizing-requirements}

Requisiti minimi per l&#39;esecuzione di Adobe Experience Manager:

* 5 GB di spazio libero su disco nella directory di installazione
* 2 GB di memoria

>[!NOTE]
>
>* I casi di utilizzo di risorse digitali richiedono una maggiore quantità di memoria di base. Per ulteriori informazioni, vedere [Distribuzione e manutenzione](/help/sites-deploying/deploy.md#default-local-install).
>* [Il pacchetto del componente aggiuntivo AEM Forms](/help/forms/using/installing-configuring-aem-forms-osgi.md) richiede 15 GB di spazio temporaneo.
>

Per ulteriori informazioni, vedere le [linee guida per il dimensionamento hardware](/help/managing/hardware-sizing-guidelines.md).

### Livelli di supporto {#support-levels}

Questo documento elenca le piattaforme client e server supportate per Adobe Experience Manager. Adobe fornisce diversi livelli di supporto, sia per le configurazioni consigliate che per altre configurazioni.

### Configurazioni supportate {#supported-configurations}

Adobe consiglia queste configurazioni e fornisce supporto completo come parte del contratto standard di manutenzione software.

<table>
 <tbody>
  <tr>
   <td>Livello di supporto</td>
   <td>Descrizione<br /> </td>
  </tr>
  <tr>
   <td><strong>A: supportato</strong></td>
   <td>Adobe fornisce supporto e manutenzione completi per questa configurazione. Questa configurazione è coperta dal processo di controllo qualità di Adobe.</td>
  </tr>
  <tr>
   <td><strong>R: supporto limitato</strong></td>
   <td>Per garantire il successo dei progetti dei clienti, Adobe fornisce supporto completo nell’ambito di un programma di supporto limitato, che richiede il rispetto di condizioni specifiche. Il supporto a livello R richiede una richiesta formale del cliente e una conferma da parte di Adobe. Per ulteriori informazioni, contatta l’Assistenza clienti di Adobe.</td>
  </tr>
 </tbody>
</table>

### Configurazioni non supportate {#unsupported-configurations}

| Livello di supporto | Descrizione |
|---|---|
| **Z: non supportato** | La configurazione non è supportata. Adobe non fornisce istruzioni sul funzionamento o meno della configurazione e non la supporta. |

## Piattaforme supportate {#supported-platforms}

### Java™ Virtual Machine {#java-virtual-machines}

L’applicazione richiede una macchina virtuale Java™ da eseguire, fornita dalla distribuzione Java™ Development Kit (JDK).

Adobe Experience Manager funziona con le seguenti versioni di Java™ Virtual Machines:

>[!CAUTION]
>
>Monitora i bollettini sulla sicurezza dal fornitore Java™. In questo modo è possibile garantire la sicurezza degli ambienti di produzione. Inoltre, installa sempre gli aggiornamenti Java™ più recenti.

| **Piattaforma** | **Livello di supporto** | **Collegamento** |
|---|---|---|
| JDK per Oracle Java™ SE 21 | Z: Non supportato `[1]` |
| JDK per Oracle Java™ SE 17 | Z: Non supportato `[1]` |
| JDK Oracle Java™ SE 11 - 64 bit | R: Supportato `[1]` | [Download](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?fulltext=Oracle*+JDK*+11*&orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&orderby.sort=desc&layout=list&p.offset=0&p.limit=24<td>) |
| JDK Oracle Java™ SE 10 | Z: Non supportato `[1]` |
| JDK per Oracle Java™ SE 9 | Z: Non supportato `[1]` |
| JDK Oracle Java™ SE 8 a 64 bit | R: Supportato `[1]` | [Download](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?fulltext=Oracle*+JDK*+8*&orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&orderby.sort=desc&layout=list&p.offset=0&p.limit=10) |
| VM IBM® J9 - build 2.9, JRE 1.8.0 | R: Supportato `[2]` |
| VM IBM® J9 - build 2.8, JRE 1.8.0 | R: Supportato `[2]` |
| Azul Zulu OpenJDK 11 - 64 bit | R: Supportato `[3]` | |
| Azul Zulu OpenJDK 8 a 64 bit | R: Supportato `[3]` | |

1. Oracle è passato a un modello di &quot;supporto a lungo termine&quot; (LTS) per i prodotti Oracle Java™ SE. Java™ 9, Java™ 10 e Java™ 12 sono versioni non LTS di Oracle (consulta [Roadmap del supporto Java™ SE per Oracle](https://www.oracle.com/technetwork/java/eol-135779.html)). Per distribuire AEM in un ambiente di produzione, Adobe fornisce supporto solo per le versioni LTS di Java™. Il supporto e la distribuzione del JDK Java™ SE di Oracle, inclusi tutti gli aggiornamenti di manutenzione delle versioni LTS oltre la fine degli aggiornamenti pubblici, sono supportati direttamente da Adobe per tutti i clienti AEM che utilizzano la tecnologia Oracle Java™ SE. Vedere i criteri di supporto [Java™ per Adobe Experience Manager](assets/Java_Policy_for_Adobe_Experience_Manager.pdf).
   **Importante: Oracle Java™ 11 è supportato almeno fino a settembre 2026. Oracle Java™ 17 e 21 sono supportati in [AEM 6.5 LTS](https://experienceleague.adobe.com/it/docs/experience-manager-65-lts/content/implementing/deploying/introduction/technical-requirements).**

1. IBM® JRE è supportato solo insieme all&#39;Application Server WebSphere®.

1. Le versioni di Azul Zulu OpenJDK LTS sono supportate per le distribuzioni AEM locali a partire dalla versione 6.5 SP9. Il supporto e la distribuzione delle versioni Azul Zulu JDK LTS devono essere concessi in licenza direttamente da Azul dai clienti Adobe.


### Storage e persistenza {#storage-persistence}

Esistono diverse opzioni per distribuire l’archivio di Adobe Experience Manager. Consulta il seguente elenco per le tecnologie e le opzioni di archiviazione supportate.

| **Piattaforma** | **Descrizione** | **Livello di supporto** |
|---|---|---|
| **File system con file TAR** `[1]` | Archivio | A: supportato |
| **File system con archivio dati** `[1]` | Binari | A: supportato |
| Archivia file binari in file TAR nel file system `[1]` | Binari | Z: non supportato per la produzione |
| Amazon S3 | Binari | A: supportato |
| Archiviazione BLOB di Microsoft® Azure | Binari | A: supportato |
| MongoDB Enterprise 8.0 | Archivio | R: Supportato `[3, 4]` |
| MongoDB Enterprise 7.0 | Archivio | R: Supportato `[3, 4]` |
| MongoDB Enterprise 6.0 | Archivio | R: Supportato `[3, 4]` |
| MongoDB Enterprise 5.0 | Archivio | R: Supportato `[3, 4]` |
| MongoDB Enterprise 4.4 | Archivio | R: Supportato `[2, 3, 4, 7]` |
| MongoDB Enterprise 4.2 | Archivio | R: Supportato `[2, 3, 4, 7]` |
| MongoDB Enterprise 4.0 | Archivio | Z: non supportato |
| MongoDB Enterprise 3.6 | Archivio | Z: non supportato |
| MongoDB Enterprise 3.4 | Archivio | Z: non supportato |
| IBM® DB2® 10.5 | Archivio e database Forms | R: Supporto limitato `[5]` |
| Oracle Database 12c (12.1.x) | Archivio e database Forms | R: supporto limitato |
| Oracle Database 19c | Archivio e database Forms | R: supporto limitato |
| Microsoft® SQL Server 2016 | Database Forms | A: supportato |
| Microsoft® SQL Server 2019 (obsoleto) | Database Forms | A: supportato |
| Microsoft® SQL Server 2022 | Database Forms | A: supportato |
| **Apache Lucene (predefinito Quickstart)** | Servizio di ricerca | A: supportato |
| Apache Solr | Servizio di ricerca | A: supportato |

1. &#39;File system&#39; include l&#39;archiviazione dei blocchi compatibile con POSIX. Include la tecnologia di storage in rete. Tieni presente che le prestazioni del file system potrebbero variare e influenzare le prestazioni complessive. Caricare AEM di prova con il file system remoto/di rete.
2. Le versioni 4.2 e 4.4 di MongoDB Enterprise richiedono almeno AEM 6.5 SP9.
3. Il partizionamento MongoDB non è supportato in AEM.
4. MongoDB Storage Engine WiredTiger è supportato solo.
5. Supportato per i clienti con upgrade di AEM Forms. Non supportato per le nuove installazioni.
6. Applicabile solo ad AEM Forms:
   * Rimozione del supporto per Oracle Database 12c e aggiunta del supporto per Oracle Database 19c.
   * Rimozione del supporto per Microsoft® SQL Server 2016 e aggiunta del supporto per Microsoft® SQL Server 2019 e Microsoft® SQL Server 2022.

>[!NOTE]
>
>Per ulteriori informazioni sulla funzionalità AEM Communities, vedi [Distribuzione delle community](/help/communities/deploy-communities.md).

>[!NOTE]
>
>MongoDB è un programma software di terze parti e non è incluso nel pacchetto di licenze di AEM. Per ulteriori informazioni, vedere la pagina [Criteri di gestione licenze MongoDB](https://www.mongodb.com/licensing/server-side-public-license/faq).
>
>Per ottenere il massimo dall’implementazione di AEM con MongoDB, Adobe consiglia di concedere in licenza la versione Enterprise di MongoDB per usufruire di un supporto professionale. Per ulteriori informazioni, vedere [Distribuzioni consigliate](/help/sites-deploying/recommended-deploys.md#prerequisites-and-recommendations-when-deploying-aem-with-mongomk).
>
>La licenza include un set di repliche standard, composto da una istanza principale e due istanze secondarie che possono essere utilizzate per le distribuzioni di authoring o pubblicazione.
>
>Se desideri eseguire sia l’authoring che la pubblicazione su MongoDB, è necessario acquistare due licenze separate.
>
>L’Assistenza clienti di Adobe assiste i problemi di qualificazione relativi all’utilizzo di MongoDB con AEM.
>
>Per ulteriori informazioni, vedere la pagina [MongoDB per Adobe Experience Manager](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager).

<!--
>[!NOTE]
>
>Supported relational databases as listed above are third-party software and are not included in the AEM licensing package.
>
>To run AEM 6.5 with a supported relational database, a separate support contract with a database vendor is required. Adobe Customer Care assists qualifying issues related to the usage of relational databases with AEM 6.5.
>
>**Most relational databases are currently supported within Level-R on AEM 6.5, which comes with support criteria and a support program as stated in the Level-R description above.**-->

### Servlet Engine/Application Server {#servlet-engines-application-servers}

Adobe Experience Manager può essere eseguito come server autonomo (il file JAR quickstart) o come applicazione web all&#39;interno di un server applicazioni di terze parti (il file WAR).

La versione minima dell’API Servlet richiesta è Servlet 3.1

| Platform | Livello di supporto |
|---|---|
| **Motore servlet integrato Quickstart (Jetty 9.4)** | A: supportato |
| Server Oracle WebLogic 12.2 (12cR2) | Z: non supportato |
| IBM® WebSphere® Application Server Continuous Delivery (LibertyProfile) con Web Profile 7.0 e IBM® JRE 1.8 | R: Supporto limitato per i nuovi contratti `[2]` |
| IBM® WebSphere® Application Server 9.0 e IBM® JRE 1.8 | R: Supporto limitato per i nuovi contratti `[1]` `[2]` |
| Application server IBM® WebSphere® 9.0.0.10 | R: Supporto limitato per i nuovi contratti `[1]` `[2]` |
| Apache Tomcat 8.5.x | R: Supporto limitato per i nuovi contratti `[2]` |
| JBoss® EAP 7.2.x con JBoss® Application Server | Z: non supportato |
| JBoss® EAP 7.1.4 con JBoss® Application Server | R: Supporto limitato per i nuovi contratti `[1]` `[2]` |
| JBoss® EAP 7.0.x con JBoss® Application Server | Z: non supportato |
| JBoss® EAP 7.4 con JBoss® Application Server <sup>[2] [3] [7] | A: supportato |

1. Consigliato per le distribuzioni con AEM Forms.
2. L’avvio delle implementazioni di AEM 6.5 sui server applicazioni passa al Supporto con restrizioni. I clienti esistenti possono effettuare l’aggiornamento ad AEM 6.5 e continuare a utilizzare i server delle applicazioni. Per i nuovi clienti, include i criteri di supporto e un programma di supporto come indicato nella descrizione del livello R riportata sopra.
3. Applicabile solo AEM Forms:
   * Rimozione del supporto per JBoss® EAP 7.1.4 e aggiunta del supporto per JBoss® EAP 7.4.10.

### Sistemi operativi server {#server-operating-systems}

Adobe Experience Manager funziona con le seguenti piattaforme server per gli ambienti di produzione:

| **Piattaforma** | **Livello di supporto** |
|---|---|
| **Linux®, basato sulla distribuzione Red Hat®** | R: Supportato `[1]` `[3]` |
| Linux®, basato sulla distribuzione Debian incl. Ubuntu | R: Supportato `[1]` `[2]` |
| Linux®, basato sulla distribuzione SUSE® | R: Supportato `[1]` |
| Microsoft® Windows Server 2022 | R: supporto limitato |
| Microsoft® Windows Server 2019 `[4]` (obsoleto) | R: Supporto limitato per i nuovi contratti `[5]` |
| Microsoft® Windows Server 2016 `[4]` | R: Supporto limitato per i nuovi contratti `[5]` |
| Microsoft® Windows Server 2012 R2 | Z: non supportato |
| Oracle Solaris™ 11 | Z: non supportato |
| IBM® AIX® 7.2 | Z: non supportato |

1. Kernel Linux® 2.6, 3. x, 4. x, 5. x, 6. x e 9. x include derivati dalla distribuzione Red Hat®, tra cui Red Hat® Enterprise Linux®, Oracle Linux® e Amazon Linux®. Le funzioni del componente aggiuntivo AEM Forms sono supportate solo su Red Hat® Enterprise Linux® 7, Red Hat® Enterprise Linux® 8 e Red Hat® Enterprise Linux® 9.
2. AEM Forms è supportato su Ubuntu 20.04 e SUSE® Linux® Enterprise Server 15 SP6 (64 bit).
3. Distribuzione Linux® supportata da Adobe Managed Services.

   >[!NOTE]
   >
   >Per i server basati su Linux (stack OSGI e JEE), il componente aggiuntivo AEM Forms richiede dipendenze di runtime come:
   >* glibc.x86_64 (2,17-196)
   >* libX11.x86_64 (1.6.7-4)
   >* zlib.x86-64 (1.2.7-17)
   >* libxcb.x86_64 (1,13-1,el7)
   >* libXau.x86_64 (1.0.8-2.1.el7)
   >* glibc-locale.x86_64 (2.17 o versione successiva)
   >* OpenSSL 3 (richiesto nella posizione predefinita sul sistema operativo).

   *Per l&#39;installazione di OpenSSL 3: le librerie libcrypto.so.3 e libssl.so.3 devono essere disponibili nel percorso di libreria predefinito rappresentato dalla variabile di ambiente LD_LIBRARY_PATH. Se sono installati in un percorso non standard, assicurarsi che questo percorso venga aggiunto a LD_LIBRARY_PATH prima di avviare il server.*

4. Le distribuzioni di produzione di Microsoft® Windows sono supportate per i clienti che eseguono l’aggiornamento a 6.5 e per l’utilizzo non di produzione. Le nuove implementazioni sono su richiesta per AEM Sites e Assets.
5. AEM Forms è supportato su Microsoft® Window Server senza le restrizioni R di livello di supporto.
6. AEM Forms ha rimosso il supporto per Microsoft® Windows Server 2016.

>[!NOTE]
>
>Se stai installando AEM Forms 6.5, assicurati di aver installato il seguente Microsoft® Visual C++ a 32 bit ridistribuibile.
>
>* Microsoft® Visual C++ 2008 ridistribuibile
>* Microsoft® Visual C++ 2010 ridistribuibile
>* Microsoft® Visual C++ 2012 ridistribuibile
>* Microsoft® Visual C++ 2013 ridistribuibile
>* Microsoft® Visual C++ 2019 (VC14.28 o versione successiva) ridistribuibile


### Ambienti di elaborazione virtuali e cloud {#virtual-cloud-computing-environments}

Adobe Experience Manager è supportato in esecuzione in una macchina virtuale in ambienti di cloud computing. Questi ambienti includono as Microsoft® Azure e Amazon Web Services (AWS), in esecuzione in conformità ai requisiti tecnici elencati in questa pagina e ai termini di supporto standard di Adobe.

Per un ambiente nativo per il cloud, consulta l’offerta più recente della linea di prodotti AEM: Adobe Experience Manager as a Cloud Service. Per informazioni dettagliate, consulta la [documentazione di Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=it).

Adobe offre anche Adobe Managed Services per distribuire AEM su Azure o AWS. Adobe Managed Services offre agli esperti l’esperienza e le competenze necessarie per implementare e utilizzare AEM in questi ambienti di cloud computing. Consulta la [documentazione aggiuntiva su Adobe Managed Services](https://business.adobe.com/products/experience-manager/managed-services.html?aemClk=t).

In tutti gli altri casi di distribuzione di AEM in Azure, AWS o in qualsiasi altro ambiente di cloud computing, il supporto di Adobe è contenuto nell’ambiente di elaborazione virtuale. L’ambiente virtuale deve essere eseguito in conformità alle specifiche tecniche elencate in questa pagina. Qualsiasi problema relativo ad AEM in esecuzione in uno di questi ambienti cloud deve essere riproducibile indipendentemente da qualsiasi servizio cloud specifico per l’ambiente di cloud computing. Questo a meno che il servizio cloud non sia supportato come parte dei requisiti tecnici elencati in questa pagina, ad esempio archiviazione BLOB di Azure o AWS S3.

Per consigli su come distribuire AEM su Azure o AWS, al di fuori di Adobe Managed Services, Adobe consiglia di lavorare direttamente con il provider cloud. Oppure, in collaborazione con i partner Adobe che supportano l’implementazione di AEM nell’ambiente cloud desiderato. Il fornitore o partner cloud selezionato è responsabile delle specifiche di dimensionamento, della progettazione e dell&#39;implementazione dell&#39;architettura in modo da soddisfare specifici requisiti di prestazioni, carico, scalabilità e sicurezza.

### Piattaforme Dispatcher (server web) {#dispatcher-platforms-web-servers}

Dispatcher è il componente di caching e bilanciamento del carico. [Scarica la versione più recente di Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html?lang=it). Experience Manager 6.5 richiede Dispatcher versione 4.3.2 o successiva.

Con Dispatcher versione 4.3.2 sono supportati i seguenti server web:

| Platform | Livello di supporto |
|---|---|
| **Apache httpd 2.4.x** `[1,2]` | A: supportato |
| Microsoft® IIS 10 (Internet Information Server) | A: supportato |
| Microsoft® IIS 8.5 (Internet Information Server) | Z: non supportato |

1. I server web generati in base al codice sorgente httpd di Apache supportano sia la versione di httpd su cui si basa. In caso di dubbi, chiedere ad Adobe di confermare il livello di supporto relativo al rispettivo prodotto server. I seguenti casi:

   1. Il server HTTP è stato creato utilizzando solo le distribuzioni di origine ufficiali di Apache oppure
   1. Il server HTTP è stato distribuito come parte del sistema operativo in cui è in esecuzione. Esempi: IBM® HTTP Server, Oracle HTTP Server

1. Dispatcher non è disponibile per Apache 2.4.x per sistemi operativi Windows.

## Piattaforme client supportate {#supported-client-platforms}

### Browser supportati per l&#39;authoring dell&#39;interfaccia utente {#supported-browsers-for-authoring-user-interface}

L’interfaccia utente di Adobe Experience Manager funziona con le seguenti piattaforme client. Tutti i browser vengono testati con il set predefinito di plug-in e componenti aggiuntivi.

L’interfaccia utente di AEM è ottimizzata per schermi più grandi (in genere notebook e computer desktop) e per il fattore di forma del tablet (come Apple iPad o Microsoft® Surface). Il fattore di forma del telefono non è supportato.

>[!NOTE]
>
>**Supporto per browser con cicli di rilascio rapidi:**
>
>Mozilla Firefox, Google Chrome e Microsoft® Edge vengono rilasciati aggiornamenti ogni mese. Adobe si impegna a fornire aggiornamenti affinché Adobe Experience Manager mantenga il livello di supporto indicato di seguito con le prossime versioni di questi browser.

<table>
 <tbody>
  <tr>
   <td><strong>Browser</strong></td>
   <td><strong>Supporto per l’interfaccia utente<br /> </strong></td>
   <td><strong>Supporto per l’interfaccia classica</strong></td>
  </tr>
  <tr>
   <td><strong>Google Chrome (Evergreen)</strong></td>
   <td>A: supportato</td>
   <td>A: supportato</td>
  </tr>
  <tr>
   <td>Microsoft® Edge (Evergreen)</td>
   <td>A: supportato</td>
   <td>A: supportato</td>
  </tr>
  <tr>
   <td>Microsoft® Internet Explorer 11</td>
   <td>Z: non supportato</td>
   <td>Z: non supportato</td>
  </tr>
  <tr>
   <td>Mozilla Firefox (Evergreen)</td>
   <td>A: supportato</td>
   <td>A: supportato</td>
  </tr>
  <tr>
   <td>Mozilla Firefox ultimo ESR [1]</td>
   <td>A: supportato</td>
   <td>A: supportato</td>
  </tr>
  <tr>
   <td>Apple Safari su macOS (Evergreen)</td>
   <td>A: supportato</td>
   <td>A: supportato</td>
  </tr>
  <tr>
   <td>Apple Safari 11.x su macOS</td>
   <td>Z: non supportato</td>
   <td>Z: non supportato</td>
  </tr>
  <tr>
   <td>Apple Safari su iOS 12.x</td>
   <td>R: Supportato [2]</td>
   <td>Z: non supportato</td>
  </tr>
  <tr>
   <td>Apple Safari su iOS 11.x</td>
   <td>Z: non supportato</td>
   <td>Z: non supportato</td>
  </tr>
 </tbody>
</table>

1. Supporto esteso per Firefox [Ulteriori informazioni su mozilla.org](https://www.mozilla.org/it-IT/firefox/enterprise/)
1. supporto per Apple iPad

### Browser supportati per i siti Web {#supported-browsers-for-websites}

In genere, il supporto del browser per i siti web di cui è stato eseguito il rendering da AEM Sites dipende dall’implementazione dei modelli di pagina di AEM, dalla progettazione e dall’output dei componenti ed è quindi sotto il controllo della parte che implementa queste parti.

### Client WebDAV {#webdav-clients}

**Microsoft® Windows 7+**

Quando ci si connette con Microsoft® Windows 7+ a un&#39;istanza di AEM non protetta con SSL, è necessario abilitare l&#39;autenticazione di base su una rete non protetta. È necessaria una modifica nel Registro di sistema di Windows di WebClient:

1. Individuare la sottochiave del Registro di sistema:

   * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters

1. Aggiungere la voce del Registro di sistema BasicAuthLevel a questa sottochiave utilizzando un valore pari o superiore a 2.

## Note aggiuntive sulla piattaforma {#additional-platform-notes}

Questa sezione contiene note speciali e informazioni più dettagliate sull&#39;esecuzione di Adobe Experience Manager e dei relativi componenti aggiuntivi.

### IPv4 e IPv6 {#ipv-and-ipv}

Tutti gli elementi di Adobe Experience Manager (Instance, Dispatcher) possono essere installati nelle reti IPv4 e IPv6.

Il funzionamento è semplice in quanto non è richiesta alcuna configurazione particolare. Se necessario, specificare un indirizzo IP utilizzando il formato appropriato per il tipo di rete.

Quando è necessario specificare un indirizzo IP, è possibile selezionare (come richiesto) tra i seguenti:

* Un indirizzo IPv6. Ad esempio `https://[ab12::34c5:6d7:8e90:1234]:4502`

* Un indirizzo IPv4. Ad esempio `https://123.1.1.4:4502`

* Un nome di server. Ad esempio `https://www.yourserver.com:4502`

* Il caso predefinito di `localhost` viene interpretato per le installazioni di rete IPv4 e IPv6. Ad esempio `https://localhost:4502`

### Requisiti del componente aggiuntivo AEM Dynamic Media {#requirements-for-aem-dynamic-media-add-on}

AEM Dynamic Media è disabilitato per impostazione predefinita. Consulta qui per [abilitare Dynamic Media](/help/assets/config-dynamic.md#enabling-dynamic-media).

Con Dynamic Media abilitato, si applicano i seguenti requisiti tecnici aggiuntivi.

>[!NOTE]
>
>Questi requisiti di sistema **only** si applicano se si utilizza Dynamic Media - modalità ibrida; Dynamic Media - modalità ibrida dispone di un server immagini incorporato, certificato solo su alcuni sistemi operativi.
>
>Per i clienti Dynamic Media che eseguono la modalità Dynamic Media - Scene7 (ovvero la modalità di esecuzione **dynamicmedia_scene7**), non esistono requisiti di sistema aggiuntivi, ma solo gli stessi requisiti di sistema di AEM. Dynamic Media: l’architettura in modalità Scene7 utilizza il servizio per immagini basato su cloud e non il servizio incorporato in AEM.

#### Hardware {#hardware}

I seguenti requisiti hardware sono applicabili sia per Linux® che per Windows:

* CPU Intel Xeon® o AMD® Opteron con almeno quattro core
* Almeno 16 GB di RAM

#### Linux® {#linux}

Se utilizzi Dynamic Media su Linux®, è necessario soddisfare i seguenti prerequisiti:

* Red Hat® Enterprise 8 e versioni successive con le ultime patch di correzione
* Sistema operativo a 64 bit
* Scambio disabilitato (consigliato)
* SELinux disabilitato (vedi nota che segue)

>[!NOTE]
>
>Se le impostazioni locali sono impostate in modo che LC_CTYPE non sia uguale a `en_US.UTF-8`, Dynamic Media non potrà funzionare. Per visualizzare il valore, digitare &quot;locale&quot; al prompt dei comandi. Se non è impostata correttamente, impostare la variabile di ambiente LC_CTYPE sulla stringa vuota digitando &quot;export LC_CTYPE=&quot; prima di eseguire AEM.

>[!NOTE]
>
>**La disattivazione di SELinux:** Image Server non funziona se SELinux è attivato. Questa opzione è attivata per impostazione predefinita. Per risolvere il problema, modificare il file **/etc/selinux/config** e modificare il valore SELinux da:
>
>`SELINUX=enforcing` **a** `SELINUX=disabled`

>[!NOTE]
>
>**Architettura NUMA:** I sistemi con processori basati su AMD64 e Intel® EM64T sono generalmente configurati come piattaforme NUMA (non-Uniform Memory Architecture). In altre parole, il kernel costruisce più nodi di memoria in fase di avvio anziché costruire un singolo nodo di memoria.
>
>Il costrutto a più nodi può causare esaurimento della memoria su uno o più nodi prima che gli altri nodi si esauriscano. Quando si verifica esaurimento della memoria, il kernel può decidere di terminare i processi (ad esempio, il server immagini o il server di Platform) anche se è disponibile memoria.
>
>Pertanto, Adobe consiglia di disattivare NUMA utilizzando l&#39;opzione di avvio **numa=off** per evitare che il kernel uccida questi processi.

>[!NOTE]
>
>**Il nome host del server deve risolvere:** Verificare che il nome host del server sia risolvibile in un indirizzo IP. Se non è possibile, aggiungere il nome host completo e l&#39;indirizzo IP a **/etc/hosts**:
>
>`<ip address> <fully qualified hostname>`

#### Windows {#windows}

* Microsoft® Windows Server 2016
* Spazio di swap uguale ad almeno il doppio della quantità di memoria fisica (RAM)

Per utilizzare Dynamic Media su Windows, installare Microsoft® Visual Studio 2010, 2013 e 2015 ridistribuibile per x64 e x86.

Per Windows x64:

* Ottieni Microsoft® Visual Studio 2010 ridistribuibile in [https://www.microsoft.com/en-us/download/details.aspx?id=26999](https://www.microsoft.com/en-us/download/details.aspx?id=26999)
* Ottieni Microsoft® Visual Studio 2013 ridistribuibile in [https://www.microsoft.com/en-us/download/details.aspx?id=40784](https://www.microsoft.com/en-us/download/details.aspx?id=40784)
* Ottieni Microsoft® Visual Studio 2015 ridistribuibile in [https://www.microsoft.com/en-us/download/details.aspx?id=48145](https://www.microsoft.com/en-us/download/details.aspx?id=48145)

Per Windows x86:

* Ottieni Microsoft® Visual Studio 2010 ridistribuibile in [https://www.microsoft.com/en-us/download/details.aspx?id=26999](https://www.microsoft.com/en-us/download/details.aspx?id=26999)
* Ottieni Microsoft® Visual Studio 2013 ridistribuibile in [https://www.microsoft.com/en-in/download/details.aspx?id=40769](https://www.microsoft.com/en-in/download/details.aspx?id=40769)
* Ottieni Microsoft® Visual Studio 2015 ridistribuibile in [https://www.microsoft.com/en-us/download/details.aspx?id=52685](https://www.microsoft.com/en-us/download/details.aspx?id=52685)

#### macOS {#macos}

* 10.9.x e versioni successive
* Supportato solo a scopo di prova e dimostrazione

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
>* PDF Generator supporta solo le versioni in inglese, francese, tedesco e giapponese dei sistemi operativi e delle applicazioni supportati.
>* PDF Generator richiede Adobe Acrobat Pro DC (32 Bit) per eseguire la conversione.
>* PDF Generator supporta solo la versione a 32 bit di Microsoft® Office Professional Plus e di altro software necessario per la conversione.
>* Se un&#39;installazione di Microsoft® Office viene disattivata o priva di licenza per qualsiasi motivo, ad esempio se un&#39;installazione con licenza Volume License non è in grado di individuare un host KMS entro un determinato periodo di tempo, le conversioni potrebbero non riuscire fino a quando l&#39;installazione non viene rilasciata e riattivata.
>* PDF Generator non supporta Microsoft® Office 365.
>* Le conversioni PDF Generator per OpenOffice sono supportate solo su Windows e Linux®.
>* Le funzioni PDF, Ottimizza PDF e Export PDF di OCR sono supportate solo in Windows.
>* Una versione di Acrobat è inclusa in bundle con AEM Forms per abilitare le funzionalità di PDF Generator. Durante il periodo di validità della licenza di AEM Forms, è possibile accedere alla versione inclusa nel bundle solo a livello di programmazione con AEM Forms, utilizzabile solo con AEM Forms PDF Generator. Per ulteriori informazioni, consulta la descrizione del prodotto AEM Forms in base alla distribuzione ([On-Premise](https://helpx.adobe.com/it/legal/product-descriptions/adobe-experience-manager-on-premise.html) o [Managed Services](https://helpx.adobe.com/it/legal/product-descriptions/adobe-experience-manager-managed-services.html)).
>* Il servizio PDF Generator non supporta Microsoft® Windows 11.

### Requisiti per AEM Forms Designer {#requirements-for-aem-forms-designer}

* Microsoft® Windows® 2016 Server, Microsoft® Windows® 2019 Server, Microsoft® Windows® 10 o Windows® 11
* Processore da 1 GHz o superiore con supporto per PAE, NX e SSE2.
* 1 GB di RAM per 32 bit o 2 GB di RAM per sistema operativo a 64 bit
* 16 GB di spazio su disco per 32 bit o 20 GB di spazio su disco per sistema operativo a 64 bit
* Memoria grafica - 128 MB di GPU (consigliata 256 MB)
* 2,35 GB di spazio disponibile su disco rigido
* Risoluzione di 1024 X 768 pixel o superiore
* Accelerazione hardware video (opzionale)
* Acrobat Pro DC, Acrobat Standard DC o Adobe Acrobat Reader DC
* Privilegi amministrativi per l&#39;installazione di Designer
* Microsoft Visual C++ 2019 (VC 14.28 o versione successiva) Runtime a 32 bit per AEM Forms Designer a 32 bit
* Microsoft Visual C++ 2019 (VC 14.28 o versione successiva) Runtime a 64 bit per AEM Forms Designer a 64 bit (per gli stack OSGI e JEE)

[Installare e configurare AEM Forms Designer](/help/forms/using/installing-configuring-designer.md)

### Requisiti per il write-back dei metadati di AEM Assets XMP {#requirements-for-aem-assets-xmp-metadata-write-back}

La funzione di write-back di XMP è supportata e abilitata per le piattaforme e i formati di file seguenti:

* **Sistemi operativi:**

   * Linux® (supporto di applicazioni a 32 bit e 32 bit su sistemi a 64 bit).

   * Windows Server
   * macOS X (64 bit)

* **Formati file**: JPEG, PNG, TIFF, PDF, INDD, AI e EPS.

### Requisiti per AEM Assets per l’elaborazione di risorse contenenti metadati su Linux® {#assetsonlinux}

Il processo XMPFilesProcessor richiede il funzionamento della libreria GLIBC_2.14. Utilizzare un kernel Linux® che contiene GLIBC_2.14, ad esempio Linux® versione 3.1.x. Migliora le prestazioni per l’elaborazione delle risorse che contengono una grande quantità di metadati, come i file PSD. L&#39;utilizzo di una versione precedente di GLIBC genera un errore nei registri che iniziano con `com.day.cq.dam.core.impl.handler.xmp.NCommXMPHandler Failed to read XMP`.
