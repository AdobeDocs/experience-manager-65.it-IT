---
title: Requisiti tecnici
description: Elenco delle piattaforme client e server supportate per Adobe Experience Manager.
topic-tags: platform
exl-id: 47529b9a-c4e5-434f-ac26-b01714ff863b
source-git-commit: fbf056b6b7dcbfcaa27744672c45a87316c5f761
workflow-type: tm+mt
source-wordcount: '3642'
ht-degree: 1%

---

# Requisiti tecnici{#technical-requirements}

Adobe supporta (AEM) Adobe Experience Manager sulle piattaforme come descritto nelle seguenti informazioni in questo documento.

Per qualsiasi problema relativo alla piattaforma, contatta il fornitore della piattaforma.

>[!NOTE]
>
>A seconda della piattaforma su cui si installa AEM, potrebbero esistere diversi set di requisiti per la gestione degli utenti.

## Prerequisiti {#prerequisites}

Requisiti minimi per l&#39;installazione di Adobe Experience Manager:

* Piattaforma Java™, JDK Standard Edition o altro supporto installato [Java™ Virtual Machine](#java-virtual-machines)
* File Experience Manager Quickstart (file JAR autonomo o WAR di implementazione di un’applicazione web)

### Requisiti di dimensionamento minimo {#minimum-sizing-requirements}

Requisiti minimi per l&#39;esecuzione di Adobe Experience Manager:

* 5 GB di spazio libero su disco nella directory di installazione
* 2 GB di memoria

>[!NOTE]
>
>* I casi di utilizzo di risorse digitali richiedono una maggiore quantità di memoria di base. Consulta [Distribuzione e manutenzione](/help/sites-deploying/deploy.md#default-local-install) per i dettagli.
>* [Pacchetto del componente aggiuntivo AEM Forms](/help/forms/using/installing-configuring-aem-forms-osgi.md) richiede 15 GB di spazio temporaneo.
>

Per ulteriori informazioni, vedere [Linee guida per il dimensionamento dell&#39;hardware](/help/managing/hardware-sizing-guidelines.md).

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
   <td><strong>R: Supportato</strong></td>
   <td>L'Adobe fornisce supporto e manutenzione completi per questa configurazione. Questa configurazione è coperta dal processo di controllo qualità di Adobe.</td>
  </tr>
  <tr>
   <td><strong>R: Supporto limitato</strong></td>
   <td>Per garantire il successo dei progetti dei clienti, Adobe fornisce supporto completo nell’ambito di un programma di supporto limitato, che richiede il rispetto di condizioni specifiche. Il supporto a livello R richiede una richiesta formale del cliente e una conferma da parte dell’Adobe. Per ulteriori informazioni, contatta l’Assistenza clienti Adobe.</td>
  </tr>
 </tbody>
</table>

### Configurazioni non supportate {#unsupported-configurations}

| Livello di supporto | Descrizione |
|---|---|
| **Z: non supportato** | Configurazione non supportata. L’Adobe non fornisce istruzioni sul funzionamento o meno della configurazione e non la supporta. |

## Piattaforme supportate {#supported-platforms}

### Java™ Virtual Machine {#java-virtual-machines}

L’applicazione richiede una macchina virtuale Java™ da eseguire, fornita dalla distribuzione Java™ Development Kit (JDK).

Adobe Experience Manager funziona con le seguenti versioni di Java™ Virtual Machines:

>[!CAUTION]
>
>Monitora i bollettini sulla sicurezza dal fornitore Java™. In questo modo è possibile garantire la sicurezza degli ambienti di produzione. Inoltre, installa sempre gli aggiornamenti Java™ più recenti.

| **Piattaforma** | **Livello di supporto** | **Collegamento** |
|---|---|---|
| Oracle Java™ SE 17 JDK | Z: non supportato `[1]` |
| Oracle Java™ SE 11 JDK - 64 bit | R: Supportato `[1]` | [Download](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?fulltext=Oracle*+JDK*+11*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=24&lt;td>) |
| Oracle Java™ SE 10 JDK | Z: non supportato `[1]` |
| Oracle Java™ SE 9 JDK | Z: non supportato `[1]` |
| Oracle Java™ SE 8 JDK - 64 bit | R: Supportato `[1]` | [Download](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?fulltext=Oracle*+JDK*+8*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=10) |
| VM IBM® J9 - build 2.9, JRE 1.8.0 | R: Supportato `[2]` |
| VM IBM® J9 - build 2.8, JRE 1.8.0 | R: Supportato `[2]` |
| Azul Zulu OpenJDK 11 - 64 bit | R: Supportato `[3]` | |
| Azul Zulu OpenJDK 8 a 64 bit | R: Supportato `[3]` | |

1. Oracle è passato a un modello di &quot;supporto a lungo termine&quot; (LTS) per i prodotti Oracle Java™ SE. Java™ 9, Java™ 10 e Java™ 12 non sono versioni LTS per Oracle (vedi [Roadmap del supporto di Oracle Java™ SE](https://www.oracle.com/technetwork/java/eol-135779.html)). Per distribuire l’AEM in un ambiente di produzione, Adobe fornisce supporto solo per le versioni LTS di Java™. Il supporto e la distribuzione di Oracle Java™ SE JDK, inclusi tutti gli aggiornamenti di manutenzione delle versioni LTS oltre la fine degli aggiornamenti pubblici, sono supportati da Adobe direttamente per tutti i clienti AEM che utilizzano la tecnologia Oracle Java™ SE. Consulta la [Criteri di supporto Java™ per Adobe Experience Manager](assets/Java_Policy_for_Adobe_Experience_Manager.pdf).
   **Importante: Oracle Java™ 11 è supportato almeno fino a settembre 2026. È in preparazione il supporto per l’Oracle Java™ 17.**

1. IBM® JRE è supportato solo insieme all&#39;Application Server WebSphere®.

1. Le versioni di Azul Zulu OpenJDK LTS sono supportate per le distribuzioni AEM locali a partire dalla versione 6.5 SP9. Il supporto e la distribuzione delle versioni Azul Zulu JDK LTS devono essere concessi in licenza direttamente da Azul dai clienti Adobe.


### Storage e persistenza {#storage-persistence}

Esistono diverse opzioni per distribuire l’archivio di Adobe Experience Manager. Consulta il seguente elenco per le tecnologie e le opzioni di archiviazione supportate.

| **Piattaforma** | **Descrizione** | **Livello di supporto** |
|---|---|---|
| **File system con file TAR** `[1]` | Archivio | R: Supportato |
| **File system con archivio dati** `[1]` | Binari | R: Supportato |
| Memorizzare i file binari in file TAR nel file system `[1]` | Binari | Z: non supportato per la produzione |
| Amazon S3 | Binari | R: Supportato |
| Archiviazione BLOB di Microsoft® Azure | Binari | R: Supportato |
| MongoDB Enterprise 6.0 | Archivio | R: Supportato `[3, 4]` |
| MongoDB Enterprise 5.0 | Archivio | R: Supportato `[3, 4]` |
| MongoDB Enterprise 4.4 | Archivio | R: Supportato `[2, 3, 4, 7]` |
| MongoDB Enterprise 4.2 | Archivio | R: Supportato `[2, 3, 4, 7]` |
| MongoDB Enterprise 4.0 | Archivio | Z: non supportato |
| MongoDB Enterprise 3.6 | Archivio | Z: non supportato |
| MongoDB Enterprise 3.4 | Archivio | Z: non supportato |
| IBM® DB2® 10.5 | Archivio e database Forms | R: Supporto limitato `[5]` |
| Database Oracle 12c (12.1.x) | Archivio e database Forms | R: Supporto limitato |
| Microsoft® SQL Server 2016 | Database Forms | R: Supportato |
| **Apache Lucene (integrato con Quickstart)** | Servizio di ricerca | R: Supportato |
| Apache Solr | Servizio di ricerca | R: Supportato |

1. &#39;File system&#39; include l&#39;archiviazione dei blocchi compatibile con POSIX. Include la tecnologia di storage in rete. Tieni presente che le prestazioni del file system potrebbero variare e influenzare le prestazioni complessive. Caricare il test AEM con il file system remoto/di rete.
1. Le versioni 4.2 e 4.4 di MongoDB Enterprise richiedono come minimo AEM 6.5 SP9.
1. Il partizionamento di MongoDB non è supportato in AEM.
1. MongoDB Storage Engine WiredTiger è supportato solo.
1. Supportato per i clienti con upgrade di AEM Forms. Non supportato per le nuove installazioni.
1. Applicabile solo ad AEM Forms:
   * Rimozione del supporto per Oracle Database 12c e aggiunta del supporto per Oracle Database 19c.
   * Rimozione del supporto per Microsoft® SQL Server 2016 e aggiunta del supporto per Microsoft® SQL Server 2019.
1. Non supportato per AEM Forms.

>[!NOTE]
>
Consulta [Distribuzione delle community](/help/communities/deploy-communities.md) per ulteriori informazioni sulla funzionalità AEM Communities.

>[!NOTE]
>
MongoDB è un programma software di terze parti e non è incluso nel pacchetto di licenze AEM. Per ulteriori informazioni, vedere [Criteri di licenza MongoDB](https://www.mongodb.com/licensing/server-side-public-license/faq) pagina.
>
Per ottenere il massimo dall’implementazione AEM con MongoDB, l’Adobe consiglia di concedere in licenza la versione Enterprise di MongoDB per usufruire di un supporto professionale. Consulta [Distribuzioni consigliate](/help/sites-deploying/recommended-deploys.md#prerequisites-and-recommendations-when-deploying-aem-with-mongomk) per ulteriori informazioni.
>
La licenza include un set di repliche standard, composto da una istanza principale e due istanze secondarie che possono essere utilizzate per le distribuzioni di authoring o pubblicazione.
>
Se desideri eseguire sia l’authoring che la pubblicazione su MongoDB, è necessario acquistare due licenze separate.
>
L’Assistenza clienti Adobe assiste i problemi di qualificazione relativi all’utilizzo di MongoDB con AEM.
>
Per ulteriori informazioni, vedere la [pagina](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager) MongoDB per Adobe Experience Manager.

>[!NOTE]
>
I database relazionali supportati come sopra elencati sono software di terze parti e non sono inclusi nel pacchetto di licenze AEM.
>
Per eseguire AEM 6.5 con un database relazionale supportato, è necessario un contratto di supporto separato con un fornitore di database. L’Assistenza clienti Adobe assiste i problemi qualificati relativi all’utilizzo di database relazionali con AEM 6.5.
>
**La maggior parte dei database relazionali sono attualmente supportati al livello R su AEM 6.5, che viene fornito con criteri di supporto e un programma di supporto come indicato nella descrizione del livello R precedente.**

### Servlet Engine/Application Server {#servlet-engines-application-servers}

Adobe Experience Manager può essere eseguito come server autonomo (il file JAR quickstart) o come applicazione web all&#39;interno di un server applicazioni di terze parti (il file WAR).

La versione minima dell’API Servlet richiesta è Servlet 3.1

| Platform | Livello di supporto |
|---|---|
| **Motore servlet integrato Quickstart (Jetty 9.4)** | R: Supportato |
| Oracle Server WebLogic 12.2 (12cR2) | Z: non supportato |
| IBM® WebSphere® Application Server Continuous Delivery (LibertyProfile) con Web Profile 7.0 e IBM® JRE 1.8 | R: Supporto limitato per i nuovi contratti `[2]` |
| IBM® WebSphere® Application Server 9.0 e IBM® JRE 1.8 | R: Supporto limitato per i nuovi contratti `[1]` `[2]` |
| Apache Tomcat 8.5.x | R: Supporto limitato per i nuovi contratti `[2]` |
| JBoss® EAP 7.2.x con JBoss® Application Server | Z: non supportato |
| JBoss® EAP 7.1.4 con JBoss® Application Server | R: Supporto limitato per i nuovi contratti `[1]` `[2]` |
| JBoss® EAP 7.0.x con JBoss® Application Server | Z: non supportato |

1. Consigliato per le distribuzioni con AEM Forms.
1. A partire dalle implementazioni di AEM 6.5 sui server applicazioni, passa al Supporto con restrizioni. I clienti esistenti possono effettuare l&#39;aggiornamento a AEM 6.5 e continuare a utilizzare i server delle applicazioni. Per i nuovi clienti, include i criteri di supporto e un programma di supporto come indicato nella descrizione del livello R riportata sopra.
1. Applicabile solo AEM Forms:
   * Rimozione del supporto per JBoss® EAP 7.1.4 e aggiunta del supporto per JBoss® EAP 7.4.10.

### Sistemi operativi server {#server-operating-systems}

Adobe Experience Manager funziona con le seguenti piattaforme server per gli ambienti di produzione:

| **Piattaforma** | **Livello di supporto** |
|---|---|
| **Linux®, basato sulla distribuzione Red Hat®** | R: Supportato `[1]` `[3]` |
| Linux®, basato sulla distribuzione Debian incl. Ubuntu | R: Supportato `[1]` `[2]` |
| Linux®, basato sulla distribuzione SUSE® | R: Supportato `[1]` |
| Microsoft® Windows Server 2019 `[4]` | R: Supporto limitato per i nuovi contratti `[5]` |
| Microsoft® Windows Server 2016 `[4]` | R: Supporto limitato per i nuovi contratti `[5]` |
| Microsoft® Windows Server 2012 R2 | Z: non supportato |
| Oracle Solaris™ 11 | Z: non supportato |
| IBM® AIX® 7.2 | Z: non supportato |

1. Kernel Linux® 2.6, 3. x, 4. x e 5. x include derivati dalla distribuzione Red Hat®, tra cui Red Hat® Enterprise Linux®, CentOS, Oracle Linux® e Amazon Linux®. Le funzioni del componente aggiuntivo AEM Forms sono supportate solo su CentOS 7, Red Hat® Enterprise Linux® 7, Red Hat® Enterprise Linux® 8 e Red Hat® Enterprise Linux® 9.
1. AEM Forms è supportato su Ubuntu 20.04 LTS.
1. Distribuzione Linux® supportata da Adobe Managed Services.

   >[!NOTE]
   >
   Per i server basati su Linux (stack OSGI e JEE), il componente aggiuntivo AEM Forms richiede dipendenze di runtime come:
   * glibc.x86_64 (2,17-196)
   * libX11.x86_64 (1.6.7-4)
   * zlib.x86-64 (1.2.7-17)
   * libxcb.x86_64 (1.13-1.el7)
   * libXau.x86_64 (1.0.8-2.1.el7)

1. Le distribuzioni di produzione di Microsoft® Windows sono supportate per i clienti che eseguono l’aggiornamento a 6.5 e per l’utilizzo non di produzione. Le nuove implementazioni sono su richiesta per AEM Sites e Assets.
1. AEM Forms è supportato su Microsoft® Window Server senza le restrizioni R di livello di supporto.
1. AEM Forms ha rimosso il supporto per Microsoft® Windows Server 2016.

>[!NOTE]
>
Se stai installando AEM Forms 6.5, assicurati di aver installato il seguente Microsoft® Visual C++ a 32 bit ridistribuibile.
>
* Microsoft® Visual C++ 2008 ridistribuibile
* Microsoft® Visual C++ 2010 ridistribuibile
* Microsoft® Visual C++ 2012 ridistribuibile
* Microsoft® Visual C++ 2013 ridistribuibile
* Microsoft® Visual C++ 2019 (VC14.28 o versione successiva) ridistribuibile


### Ambienti di elaborazione virtuali e cloud {#virtual-cloud-computing-environments}

Adobe Experience Manager è supportato in esecuzione in una macchina virtuale in ambienti di cloud computing. Questi ambienti includono as Microsoft® Azure e Amazon Web Services (AWS), in esecuzione in conformità ai requisiti tecnici elencati in questa pagina e in base ai termini di supporto standard di Adobe.

Per un ambiente nativo per il cloud, consulta l’offerta più recente della linea di prodotti AEM: Adobe Experience Manager as a Cloud Service. Consulta [Documentazione di Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=it) per i dettagli.

Adobe offre anche Adobe Managed Services per distribuire l’AEM su Azure o AWS. Adobe Managed Services fornisce agli esperti l’esperienza e le competenze necessarie per implementare e utilizzare l’AEM in questi ambienti di cloud computing. Consulta [documentazione aggiuntiva su Adobe Managed Services](https://business.adobe.com/products/experience-manager/managed-services.html?aemClk=t).

In tutti gli altri casi di distribuzione di AEM in Azure, AWS o in qualsiasi altro ambiente di cloud computing, il supporto di Adobe è contenuto nell’ambiente di elaborazione virtuale. L’ambiente virtuale deve essere eseguito in conformità alle specifiche tecniche elencate in questa pagina. Qualsiasi problema relativo all’AEM in esecuzione in uno di questi ambienti cloud deve essere riproducibile indipendentemente da qualsiasi servizio cloud specifico per l’ambiente di cloud computing. Questo a meno che il servizio cloud non sia supportato come parte dei requisiti tecnici elencati in questa pagina, ad esempio archiviazione BLOB di Azure o AWS S3.

Per raccomandazioni su come distribuire l’AEM in Azure o AWS, al di fuori di Adobe Managed Services, Adobe consiglia di lavorare direttamente con il provider cloud. Oppure, collaborando con partner Adobi che supportano l’implementazione dell’AEM nell’ambiente cloud di tua scelta. Il fornitore o partner cloud selezionato è responsabile delle specifiche di dimensionamento, della progettazione e dell&#39;implementazione dell&#39;architettura in modo da soddisfare specifici requisiti di prestazioni, carico, scalabilità e sicurezza.

### Piattaforme di Dispatcher (server web) {#dispatcher-platforms-web-servers}

Dispatcher è il componente di caching e bilanciamento del carico. [Scarica la versione più recente di Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html). L’Experience Manager 6.5 richiede Dispatcher versione 4.3.2 o successiva.

I seguenti server web sono supportati per l’utilizzo con Dispatcher versione 4.3.2:

| Platform | Livello di supporto |
|---|---|
| **Apache httpd 2.4.x** `[1,2]` | R: Supportato |
| Microsoft® IIS 10 (Internet Information Server) | R: Supportato |
| Microsoft® IIS 8.5 (Internet Information Server) | Z: Non supportato |

1. I server Web costruiti sulla base del codice sorgente httpd di Apache hanno lo stesso supporto della versione di httpd su cui è basato. In caso di dubbi, chiedere all&#39;Adobe di confermare il livello di supporto relativo al rispettivo prodotto server. I seguenti casi:

   1. Il server HTTP è stato creato utilizzando solo le distribuzioni di origine ufficiali di Apache oppure
   1. Il server HTTP è stato distribuito come parte del sistema operativo in cui è in esecuzione. Esempi: IBM® HTTP Server, Oracle HTTP Server

1. Dispatcher non è disponibile per Apache 2.4.x per sistemi operativi Windows.

## Piattaforme client supportate {#supported-client-platforms}

### Browser supportati per l&#39;authoring dell&#39;interfaccia utente {#supported-browsers-for-authoring-user-interface}

L’interfaccia utente di Adobe Experience Manager funziona con le seguenti piattaforme client. Tutti i browser vengono testati con il set predefinito di plug-in e componenti aggiuntivi.

L’interfaccia utente AEM è ottimizzata per schermi più grandi (in genere notebook e computer desktop) e per il fattore di forma del tablet (come Apple iPad o Microsoft® Surface). Il fattore di forma del telefono non è supportato.

>[!NOTE]
>
**Supporto per browser con cicli di rilascio rapidi:**
>
Mozilla Firefox, Google Chrome e Microsoft® Edge vengono rilasciati aggiornamenti ogni pochi mesi. Adobe si impegna a fornire aggiornamenti affinché Adobe Experience Manager mantenga il livello di supporto indicato di seguito con le prossime versioni di questi browser.

<table>
 <tbody>
  <tr>
   <td><strong>Browser</strong></td>
   <td><strong>Supporto per l’interfaccia utente<br /> </strong></td>
   <td><strong>Supporto per l’interfaccia classica</strong></td>
  </tr>
  <tr>
   <td><strong>Google Chrome (Evergreen)</strong></td>
   <td>R: Supportato</td>
   <td>R: Supportato</td>
  </tr>
  <tr>
   <td>Microsoft® Edge (Evergreen)</td>
   <td>R: Supportato</td>
   <td>R: Supportato</td>
  </tr>
  <tr>
   <td>Microsoft® Internet Explorer 11</td>
   <td>Z: non supportato</td>
   <td>Z: non supportato</td>
  </tr>
  <tr>
   <td>Mozilla Firefox (Evergreen)</td>
   <td>R: Supportato</td>
   <td>R: Supportato</td>
  </tr>
  <tr>
   <td>Mozilla Firefox ultima ESR [1]</td>
   <td>R: Supportato</td>
   <td>R: Supportato</td>
  </tr>
  <tr>
   <td>Apple Safari su macOS (Evergreen)</td>
   <td>R: Supportato</td>
   <td>R: Supportato</td>
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

1. Supporto esteso per Firefox [Ulteriori informazioni su mozilla.org](https://www.mozilla.org/en-US/firefox/enterprise/)
1. supporto per Apple iPad

### Browser supportati per i siti Web {#supported-browsers-for-websites}

In genere, il supporto del browser per i siti web di cui è stato eseguito il rendering da AEM Sites dipende dall’implementazione dei modelli di pagina AEM, dalla progettazione e dall’output dei componenti ed è quindi sotto il controllo della parte che implementa queste parti.

### Client WebDAV {#webdav-clients}

**Microsoft® Windows 7+**

Quando ci si connette con Microsoft® Windows 7+ a un&#39;istanza AEM non protetta con SSL, è necessario abilitare l&#39;autenticazione di base su una rete non protetta. È necessaria una modifica nel Registro di sistema di Windows di WebClient:

1. Individuare la sottochiave del Registro di sistema:

   * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters

1. Aggiungere la voce del Registro di sistema BasicAuthLevel a questa sottochiave utilizzando un valore pari o superiore a 2.

## Note aggiuntive sulla piattaforma {#additional-platform-notes}

Questa sezione contiene note speciali e informazioni più dettagliate sull&#39;esecuzione di Adobe Experience Manager e dei relativi componenti aggiuntivi.

### IPv4 e IPv6 {#ipv-and-ipv}

Tutti gli elementi di Adobe Experience Manager (istanza, Dispatcher) possono essere installati sia nelle reti IPv4 che IPv6.

Il funzionamento è semplice in quanto non è richiesta alcuna configurazione speciale. Se necessario, specificare un indirizzo IP utilizzando il formato appropriato per il tipo di rete.

Quando è necessario specificare un indirizzo IP, è possibile selezionare (a seconda delle esigenze) una delle seguenti opzioni:

* Un indirizzo IPv6. Ad esempio `https://[ab12::34c5:6d7:8e90:1234]:4502`

* Un indirizzo IPv4. Ad esempio `https://123.1.1.4:4502`

* Un nome di server. Ad esempio `https://www.yourserver.com:4502`

* Il caso predefinito di `localhost` viene interpretato per le installazioni di rete IPv4 e IPv6. Ad esempio `https://localhost:4502`

### Requisiti del componente aggiuntivo Dynamic Medie per AEM {#requirements-for-aem-dynamic-media-add-on}

Il Dynamic Medie AEM è disattivato per impostazione predefinita. Consulta qui per [abilita Dynamic Medie](/help/assets/config-dynamic.md#enabling-dynamic-media).

Con Dynamic Medie abilitato, si applicano i seguenti requisiti tecnici aggiuntivi.

>[!NOTE]
>
Questi requisiti di sistema **solo** applicabile se si utilizza Dynamic Medie - Modalità ibrida; Dynamic Medie - Modalità ibrida dispone di un server immagini incorporato, certificato solo su alcuni sistemi operativi.
>
Per i clienti Dynamic Medie che eseguono Dynamic Medie in modalità Scene7 (ovvero **dynamicmedia_scene7** modalità di funzionamento), non vi sono requisiti di sistema aggiuntivi, ma solo gli stessi requisiti di sistema dell&#39;AEM. L’architettura della modalità Dynamic Medie - Scene7 utilizza il servizio per immagini basato su cloud e non il servizio incorporato nell’AEM.

#### Hardware {#hardware}

I seguenti requisiti hardware sono applicabili sia per Linux® che per Windows:

* CPU Intel Xeon® o AMD® Opteron con almeno quattro core
* Almeno 16 GB di RAM

#### Linux® {#linux}

Se utilizzi Dynamic Medie su Linux®, è necessario soddisfare i seguenti prerequisiti:

* Red Hat® Enterprise 7 o CentOS 7 e versioni successive con le ultime patch di correzione
* Sistema operativo a 64 bit
* Scambio disabilitato (consigliato)
* SELinux disabilitato (vedi nota che segue)

>[!NOTE]
>
Se la lingua è impostata in modo che LC_CTYPE non sia uguale a `en_US.UTF-8`, impedisce il funzionamento di Dynamic Medie. Per visualizzare il valore, digitare &quot;locale&quot; al prompt dei comandi. Se non è impostata correttamente, impostare la variabile di ambiente LC_CTYPE sulla stringa vuota digitando &quot;export LC_CTYPE=&quot; prima di eseguire AEM.

>[!NOTE]
>
**Disattivazione di SELinux:** Image Server non funziona con SELinux attivato. Questa opzione è attivata per impostazione predefinita. Per risolvere questo problema, modifica il **/etc/selinux/config** e modificare il valore SELinux da:
>
`SELINUX=enforcing` **a** `SELINUX=disabled`

>[!NOTE]
>
**Architettura NUMA:** i sistemi con processori con AMD64 e Intel® EM64T sono in genere configurati come piattaforme NUMA (Non-Uniform Memory Architecture). Cioè, il kernel costruisce più nodi di memoria al momento dell&#39;avvio piuttosto che costruire un singolo nodo di memoria.
>
Il costrutto a nodi multipli può causare l&#39;esaurimento della memoria su uno o più nodi prima che altri si esauriscano. Quando si verifica esaurimento della memoria, il kernel può decidere di terminare i processi (ad esempio, il server immagini o il server di Platform) anche se è disponibile memoria.
>
Pertanto, Adobe consiglia di disattivare NUMA utilizzando il **numa=off** opzione di avvio per evitare che il kernel uccida questi processi.

>[!NOTE]
>
**Il nome host del server deve risolvere:** Assicurarsi che il nome host del server sia risolvibile in un indirizzo IP. Se ciò non è possibile, aggiungere il nome host completo e l&#39;indirizzo IP a **/etc/hosts**:
>
`<ip address> <fully qualified hostname>`

#### Windows {#windows}

* Microsoft® Windows Server 2016
* Spazio di swap pari ad almeno il doppio della quantità di memoria fisica (RAM)

Per utilizzare Dynamic Medie su Windows, installare Microsoft® Visual Studio 2010, 2013 e 2015 ridistribuibile per x64 e x86.

Per Windows x64:

* Ottieni Microsoft® Visual Studio 2010 Redistributable at https://www.microsoft.com/en-us/download/details.aspx?id=26999 [](https://www.microsoft.com/en-us/download/details.aspx?id=26999)
* Ottieni Microsoft® Visual Studio 2013 Redistributable at https://www.microsoft.com/en-us/download/details.aspx?id=40784 [](https://www.microsoft.com/en-us/download/details.aspx?id=40784)
* Ottieni Microsoft® Visual Studio 2015 Redistributable su [https://www.microsoft.com/en-us/download/details.aspx?id=48145](https://www.microsoft.com/en-us/download/details.aspx?id=48145)

Per Windows x86:

* Ottieni Microsoft® Visual Studio 2010 ridistribuibile in [https://www.microsoft.com/en-us/download/details.aspx?id=26999](https://www.microsoft.com/en-us/download/details.aspx?id=26999)
* Ottieni Microsoft® Visual Studio 2013 ridistribuibile in [https://www.microsoft.com/en-in/download/details.aspx?id=40769](https://www.microsoft.com/en-in/download/details.aspx?id=40769)
* Ottieni Microsoft® Visual Studio 2015 ridistribuibile in [https://www.microsoft.com/en-us/download/details.aspx?id=52685](https://www.microsoft.com/en-us/download/details.aspx?id=52685)

#### macOS {#macos}

* 10.9.x e versioni successive
* Supportato solo a scopo di prova e dimostrazione

### Requisiti per i AEM Forms PDF Generator {#requirements-for-aem-forms-pdf-generator}

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
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2017 classic track</a> ultima versione (obsoleto)</td>
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
Inoltre,
>
* PDF Generator richiede una versione a 32 bit di [Acrobat 2020 classic track versione 20.004.30006](https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html) o Acrobat 2017 versione 17.011.30078 per eseguire la conversione.
* Le conversioni PDF Generator per OpenOffice sono supportate solo in Windows e Linux®.
* PDF Generator supporta solo la versione a 32 bit di Microsoft® Office Professional Plus e altri software necessari per la conversione nel sistema operativo Windows.
* PDF Generator supporta le versioni a 32 bit e a 64 bit di OpenOffice sul sistema operativo Linux®.
* PDF Generator non supporta Microsoft® Office 365.
* Le funzionalità PDF OCR, Optimize PDF e Export PDF sono supportate solo in Windows.
* Una versione di Acrobat è inclusa in bundle con AEM Forms per abilitare la funzionalità PDF Generator. Accedi in modo programmatico alla versione in bundle solo con AEM Forms, per l’utilizzo con AEM Forms PDF Generator, durante il periodo di validità della licenza di AEM Forms. Per ulteriori informazioni, consulta Descrizione del prodotto AEM Forms in base alla tua implementazione ([On-Premise](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html) o [Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html))
* Il servizio PDF Generator non supporta Microsoft® Windows 10.
* PDF Generator non riesce a convertire i file in Microsoft® Visio 2019. È possibile continuare a utilizzare Microsoft® Visio 2016 per la conversione `.VSD` e `.VSDX` file.
* PDF Generator non riesce a convertire i file utilizzando Microsoft® Project 2019. È possibile continuare a utilizzare Microsoft® Project 2016 per la conversione `.VSD` e `.VSDX` file.
>

### Requisiti di AEM Forms Designer {#requirements-for-aem-forms-designer}

* Microsoft Windows 2016 Server, Microsoft Windows 2019 Server o Microsoft®®® Windows®®® 10
* Processore da 1 GHz o superiore con supporto per PAE, NX e SSE2.
* 1 GB di RAM per 32 bit o 2 GB di RAM per sistema operativo a 64 bit
* 16 GB di spazio su disco per 32 bit o 20 GB di spazio su disco per sistema operativo a 64 bit
* Memoria grafica - 128 MB di GPU (consigliati 256 MB)
* 2,35 GB di spazio disponibile su disco rigido
* Risoluzione di 1024 X 768 pixel o superiore
* Accelerazione hardware video (opzionale)
* Acrobat Pro DC, Acrobat Standard DC o Adobe Acrobat Reader DC
* Privilegi amministrativi per installare Designer
* Microsoft Visual C++ 2019 (VC 14.28 o versione successiva) Runtime a 32 bit per AEM Forms Designer a 32 bit
* Microsoft Visual C++ 2019 (VC 14.28 o versione successiva) Runtime a 64 bit per AEM Forms Designer a 64 bit (per stack OSGI e JEE)

### Requisiti per il write-back dei metadati dell’XMP di AEM Assets {#requirements-for-aem-assets-xmp-metadata-write-back}

XMP write-back è supportato e abilitato per le piattaforme e i formati di file seguenti:

* **Sistemi operativi:**

   * Linux® (supporto di applicazioni a 32 bit e 32 bit su sistemi a 64 bit). Per informazioni sulla procedura di installazione delle librerie client a 32 bit, vedere [Come abilitare l&#39;estrazione e il write-back dell&#39;XMP su Red Hat® Linux a 64 bit®](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).

   * Windows Server
   * macOS X (64 bit)

* **Formati di file**: JPEG, PNG, TIFF, PDF, INDD, AI e EPS.

### Requisiti per AEM Assets per l’elaborazione di risorse contenenti metadati su Linux® {#assetsonlinux}

Il processo XMPFilesProcessor richiede il funzionamento di libreria GLIBC_2.14. Utilizzare un kernel Linux che contiene GLIBC_2.14, ad esempio il kernel Linux®® versione 3.1.x. Migliora le prestazioni per l&#39;elaborazione di risorse che contengono una grande quantità di file metadati like PSD. L&#39;utilizzo di una versione precedente di GLIBC porta a errori nei registri che iniziano con `com.day.cq.dam.core.impl.handler.xmp.NCommXMPHandler Failed to read XMP`.