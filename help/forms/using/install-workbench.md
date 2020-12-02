---
title: Installazione workbench
seo-title: Installazione workbench
description: Installare Workbench.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '2246'
ht-degree: 0%

---


# Installazione di Workbench {#install-workbench}

Questo documento fornisce istruzioni per l&#39;installazione e la configurazione  AEM Forms Workbench. Il programma di installazione installa anche Forms Designer.

## Chi dovrebbe leggere questo documento? {#who-should-read-this-doc}

Questo documento è destinato agli amministratori o agli sviluppatori responsabili dell&#39;installazione, configurazione, amministrazione o implementazione di Workbench. Sono incluse anche le informazioni necessarie per configurare il sistema in modo da supportare i processi AEM Forms  aggiornati. Le informazioni fornite si basano sul presupposto che chiunque legga questo documento abbia familiarità con il sistema operativo Microsoft® Windows®.

## Informazioni aggiuntive {#additional-information}

Le risorse riportate in questa tabella sono utili per ottenere ulteriori informazioni e iniziare a utilizzare  AEM Forms.
<table>
 <tbody>
  <tr>
   <td><p><strong>Per informazioni su</strong></p> </td>
   <td><p><strong>Consulta</strong></p> </td>
  </tr>
  <tr>
   <td><p>Informazioni procedurali per Workbench</p> </td>
   <td><p><a href="https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf">Guida di Workbench</a><br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Informazioni generali su  AEM Forms e come si integra con altri prodotti  Adobe</p> </td>
   <td><p><a href="http://adobe.com/go/learn_aemforms_introduction_65"> Panoramica di AEM Forms</a><br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Tutta la documentazione disponibile per  AEM Forms</p> </td>
   <td><p><a href="http://adobe.com/go/learn_aemforms_introduction_65"> documentazione AEM Forms</a><br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Aggiornamenti patch, note tecniche e informazioni aggiuntive su questa versione del prodotto</p> </td>
   <td><p>Contatta  Adobe Enterprise Support</a><br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Flex Workspace è obsoleto per  AEM Forms. È disponibile per la versione  di AEM Forms.

## Prima di installare {#before-you-install}

### Panoramica sull&#39;installazione di Workbench {#workbench-installation-overview}

Workbench è un ambiente di sviluppo integrato (IDE) che gli sviluppatori e gli autori di moduli utilizzano per creare moduli e processi aziendali automatizzati. Viene inoltre utilizzata per gestire le risorse e i servizi utilizzati dai processi e dai moduli.

L&#39;illustrazione seguente illustra l&#39;installazione di Workbench, tra cui:
* Progettazione dei processi con Workbench
* Struttura del modulo con Designer

>[!NOTE]
>
>Il server AEM Forms  richiede un programma di installazione separato. Per ulteriori informazioni, consulta la documentazione di installazione  AEM Forms su JEE.

![default-rendering-form](assets/installing-workbench.png)

## Prerequisiti del sistema {#system-prerequisites}

Questa sezione descrive i requisiti hardware e software e le piattaforme supportate.

### Requisiti hardware e software minimi {#minimum-hardware-software-requirements}

****
WorkbenchCome minimo si consigliano i seguenti requisiti: Spazio su disco per l&#39;installazione:
* 680 MB solo per Workbench.
* 2,15 GB su un&#39;unica unità per l&#39;installazione completa di Workbench, Designer e dell&#39;assembly di esempio.
* 400 MB per le directory di installazione temporanea - 200 MB nella directory \temp dell&#39;utente e 200 MB nella directory temporanea di Windows.

>[!NOTE]
>
>Se tutte queste posizioni si trovano su un&#39;unica unità, durante l&#39;installazione deve essere disponibile uno spazio di 1,5 GB. I file copiati nelle directory temporanee vengono eliminati al termine dell&#39;installazione.

* Requisiti hardware: Processore Intel® Pentium® 4 o AMD equivalente, 1 GHz.
* Java™ Runtime Environment (JRE) 7.0 aggiorna 51 o versioni successive e aggiorna la versione 7.0.
* Risoluzione del monitor minima di 1024x768 pixel o superiore con colore a 16 bit o superiore.
* Connessione di rete TCP/IPv4 o TCP/IPv6 al server AEM Forms .
* Installate Visual C++ Redistributable Runtime Packages 2012 a 32 bit.
* Installate Visual C++ Redistributable Runtime Packages 2013 a 32 bit.

>[!NOTE]
>
>Per installare Workbench è necessario disporre dei privilegi di amministratore. Se state installando un account non amministratore, il programma di installazione vi chiederà le credenziali per un account appropriato.

### Piattaforme supportate {#supported-platforms}

Consultare l&#39;elenco completo delle piattaforme supportate per Workbench in [ piattaforme supportate da AEM Forms](http://adobe.com/go/learn_aemforms_supportedplatforms_65).

## Considerazioni sull&#39;installazione di Designer {#designer-installation-considerations}

Per impostazione predefinita, l&#39;installazione di Workbench include una versione di Designer in lingua solo inglese corrispondente. Se l&#39;applicazione di installazione di Workbench rileva una versione esistente di Designer sul computer in uso, l&#39;installazione potrebbe terminare e sarà necessario rimuovere la versione corrente di Designer prima di continuare.
Nella tabella seguente è riportato un elenco completo dei possibili scenari di installazione di Designer che è possibile incontrare durante l&#39;installazione di Workbench.

<table>
 <tbody>
  <tr>
   <td><p><strong>Versione di Designer attualmente installata</strong></p> </td>
   <td><p><strong>Azioni necessarie</strong></p> </td>
  </tr>
  <tr>
   <td><p> Acrobat Pro o  Acrobat Pro Extended (incluso Designer)</p> </td>
   <td><p>Nessuno.<br /> 
L'installazione di Workbench rileva nel computer un'istanza di Designer installata con  Acrobat Pro o  Acrobat Pro Extended.<br />
È possibile creare diverse versioni di Designer sullo stesso sistema, ad esempio Designer 6.4.x per Workbench 6.4 e Designer 6.5.0.x per Workbench 6.5. Non è necessario disinstallare la versione di Designer installata con  Acrobat 10 Pro o  Acrobat 10 Pro Extended o versioni successive.
<br /></p> </td>
  </tr>
  <tr>
   <td><p>Designer (autonomo)</p> </td>
   <td><p>Nessuno. <br />La versione di Designer inclusa in Workbench è disponibile solo in lingua inglese. <br />Il programma di installazione di Workbench non reinstallerà una nuova versione di Designer. Verrà invece applicata una patch a una versione aggiornata, inclusa nel programma di installazione di Workbench. È inoltre possibile utilizzare la versione localizzata di Designer all'interno di Workbench.<br /> </p> </td>
  </tr>
 </tbody>
</table>

### Disinstallazione di Designer (autonoma) in Windows 10 {#uninstall-designer-standalone-windows10}

1. Vai a **Pannello di controllo Campaign > Programmi > Programmi e funzionalità**
1. Nell&#39;elenco Programmi attualmente installati, selezionare **Designer Adobi**.
1. Fare clic su **Disinstalla**, quindi fare clic su **Sì**.

## Installazione di Workbench {#installing-workbench}

Questo capitolo descrive come installare Workbench.

### Installazione ed esecuzione di Workbench {#installing-and-running-workbench}

Prima di installare Workbench, è necessario assicurarsi che nell&#39;ambiente in uso siano inclusi il software e l&#39;hardware necessari per eseguire Workbench (vedere la sezione: **Prima di installare**).

**Per installare ed eseguire Workbench:**

1. Effettuare una delle seguenti operazioni:
   * Andate alla directory \workbench nel supporto di installazione e fate doppio clic sul file run_windows_installer.bat.
   * Scaricare e decomprimere Workbench nel file system. Dopo il download, andate alla directory \workbench e fate doppio clic sul file run_windows_installer.bat.

   >[!IMPORTANT]
   >
   >Il programma di installazione di Workbench viene eseguito solo da un&#39;unità locale. Non può essere eseguito da un sito remoto.

   >[!NOTE]
   >
   >Se si verifica un errore &quot;Impossibile creare la macchina virtuale Java&quot;, creare una variabile di ambiente denominata _JAVA_ OPTIONS con valore -Xmx512M ed eseguire il programma di installazione.

1. Nella schermata introduttiva, fate clic su Avanti.
1. Leggere il Contratto di Licenza del Prodotto, selezionare Accetto i termini del Contratto di Licenza, quindi fare clic su Avanti.
1. (Facoltativo) Selezionare Installa  Adobe Designer se è necessario questo strumento per creare e modificare i moduli.

   >[!NOTE]
   >
   >È possibile continuare a utilizzare Designer installato con  Acrobat 10 lasciando questa opzione deselezionata.

1. Accettare la directory predefinita come elencata oppure   fare clic su Scegli e passare alla directory in cui si installa Workbench, quindi fare clic su Avanti.

   >[!NOTE]
   >
   >Il percorso della directory di installazione non deve contenere caratteri # (sterline) e $ (dollari).

1. Esaminate il riepilogo della preinstallazione e fate clic su Installa. Il programma di installazione visualizza l&#39;avanzamento dell&#39;installazione.
1. Esaminate il riepilogo dell&#39;installazione. Selezionare Avvia  AEM Forms Workbench per avviare Workbench e fare clic su Avanti.
1. Esaminate le note sulla versione e fate clic su Fine.
1. I seguenti elementi sono ora installati nel computer:
   * **Workbench**: Per eseguire Workbench dal menu Start, selezionare Tutti i programmi >  AEM Forms > Workbench, se si desidera memorizzare la cartella dei collegamenti. Per informazioni,   consultare la documentazione di <a href="https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf">Utilizzo di Workbench</a>.
   * **Designer**: È possibile accedere a Designer dall&#39;interno di Workbench. Per ulteriori informazioni, vedere l&#39;argomento della Guida introduttiva nella Guida di <a href="https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/using-designer.pdf">Designer</a>.
   * **AEM Forms SDK**: Per ulteriori informazioni sull’utilizzo dell’SDK, consulta  <a href="http://www.adobe.com/go/learn_aemforms_programming_65">Programmazione con  AEM Forms</a>.

## Aggiornamento dei processi {#upgrading-processes}

 i processi AEM Forms su JEE possono essere aggiornati  applicazioni AEM Forms tramite l&#39;Aggiornamento guidato. Per ulteriori informazioni, vedere Aggiornamento della documentazione relativa agli artifact legacy nella Guida di Workbench.

### Configurazione e accesso a un server {#configuring-and-logging-server}

Per utilizzare Workbench, è necessario disporre di un&#39;istanza di  AEM Forms in esecuzione, in genere su un computer a parte. È necessario disporre di un nome utente e di una password per accedere a  AEM Forms, nonché dei dettagli sulla posizione del server.

>[!NOTE]
>
>Se si è configurato  AEM Forms per utilizzare il provider di repository EMC Documentum o IBM FileNet e si desidera accedere a un repository diverso da quello configurato come predefinito nella console di amministrazione AEM moduli, specificare il nome utente username@Repository.

### Configurazione delle impostazioni di timeout {#configuring-timeout-settings}

Per impostazione predefinita, Workbench si chiude dopo due ore, indipendentemente dall&#39;attività o dall&#39;inattività. Per modificare l&#39;impostazione del timeout, vedere &quot;Configuring User Management > Configure advanced system attribute&quot; (Configurazione di gestione utente > Configura attributi di sistema avanzati) nella <a href="https://docs.adobe.com/content/help/en/experience-manager-65/forms/administrator-help/configure-user-management/configure-advanced-system-attributes.html">Guida della console di amministrazione</a>.

### Configurazione di Workbench per la connessione mediante HTTPS {#configuring-workbench-to-connect-over-HTTPS}

Per connettere Workbench a un server AEM Forms  tramite HTTPS, è necessario assicurarsi che l&#39;autorità di certificazione (CA) che ha emesso la chiave pubblica sia riconosciuta come attendibile da Workbench. Se il certificato non viene riconosciuto come proveniente da un&#39;origine affidabile, è necessario aggiornare il file del certificato che si trova nella directory [Workbench_HOME]/workbench/jre/lib/security.

>[!NOTE]
>
>[Workbench_] HOMErappresenta la directory in cui è stato installato Workbench. Il percorso predefinito è C:\Program Files (x86)\Adobe Experience Manager Forms Workbench.

Assicuratevi di connettervi a HTTPS utilizzando il nome specificato nel certificato. Questo nome è in genere il nome host completo.

**Per aggiornare il file** cacert:
1. Accertatevi di disporre di una copia del certificato SSL (Secure Sockets Layer). Contattate l’amministratore che ha configurato il server SSL o esportate il certificato utilizzando un browser Web.

   >[!NOTE]
   >
   >Per esportare il certificato, aprire un browser Web e accedere alla console di amministrazione, installare il certificato nel browser, quindi esportare il certificato dal browser in una posizione di archiviazione temporanea (o direttamente nella directory [Workbench_HOME]/workbench/jre/lib/security).

1. Copiare il certificato nella directory [Workbench_HOME]/workbench/jre/lib/security.

1. Aprire una finestra del prompt dei comandi, passare a [Workbench_HOME]/workbench/jre/bin, quindi digitare il comando seguente:
   `keytool -import -storepass changeit -file [Workbench_HOME]\workbench\jre\lib\security\ssl_cert_for_certname.cer -keystore [Workbench_HOME]\workbench\jre\lib\security\cacerts -alias example`
Dove:
   * changeit è la password predefinita per l&#39;archivio di chiavi degli account.
   * certname è il certificato selezionato al punto 1.
   * esempio è l&#39;alias scelto per il certificato. Questo valore può essere modificato

1. Quando viene richiesto di rendere affidabile il certificato, digitare Sì e premere il tasto Invio. Il keytool prosegue con l&#39;importazione del file cacerts nella directory [Workbench_HOME]/workbench/jre/lib/security.

1. Chiudere e riavviare Workbench per applicare le modifiche.

### Configurazione delle impostazioni della cache per i modelli generati dinamicamente {#configuring-cache-settings-for-dynamically-generated-templates}

Se l&#39;applicazione genera al volo modelli univoci aggiornando automaticamente il contenuto XFA, è necessario considerare i seguenti aspetti del funzionamento della cache. In effetti, ogni transazione utilizza un nuovo modello univoco.

Quando il generatore di moduli o l&#39;output cerca o aggiorna voci nella cache per un modello di modulo specifico, utilizza diversi valori chiave per individuare la voce specifica della cache a cui si accede.

* **Nome** file modello: Posizione e nome file del modello utilizzato come identificatore univoco principale del modulo memorizzato nella cache.
* **Timestamp**: Il file modello contiene una marca temporale utilizzata per determinare l&#39;ora dell&#39;ultimo aggiornamento del modulo.
* **UUID** modello: Designer inserisce in ciascun modello un identificatore univoco (UUID) per il modulo e la relativa versione. Ogni volta che il modulo viene aggiornato, viene aggiornato l&#39;UUID incorporato. Ad esempio, un modello XDP potrebbe mostrare il contenuto seguente:

   `<?xml version="1.0" encoding="UTF-8"?>`
   `<?xfa generator="AdobeAEM formsDesignerES_V8.2" APIVersion="2.6.7185.0"?><xdp:xdp xmlns:xdp=http://ns.adobe.com/xdp/ timeStamp="2008-07-29T21:22:12Z" uuid="823e538f-ff6c-4961-b759-f7626978a223"><template xmlns="http://www.xfa.org/schema/xfa-template/2.6/">`

* **Opzioni** di rendering: All&#39;interno della cache del modulo di cui è stato effettuato il rendering, il contenuto della cache viene memorizzato separatamente per ciascun set di opzioni di rendering univoche.


Il servizio Forms riceve i modelli in base al nome del file o alla posizione del repository, oppure in base al valore, come oggetto XML in memoria.
* **Modelli passati tramite riferimento**: Utilizza il livello principale del contenuto e il nome del modulo. Se in ogni richiesta con questo metodo vengono passati modelli univoci con nomi di file diversi, la cache del disco si espanderà all’infinito e non verrà mai riutilizzata. Per evitare questo problema, è necessario trasmettere modelli univoci con lo stesso nome file per fare in modo che la stessa cache venga aggiornata per tutte le richieste.
* **Modelli passati per valore**: Utilizza i byte dei modelli passati insieme ai dati utilizzando il parametro theinDataDoc. Se si passano modelli univoci con UUID diversi con questo metodo, la cache del disco si espanderà all’infinito e non verrà mai riutilizzata. Per evitare questo problema, l&#39;attributo UUID deve essere rimosso da tutti i modelli per garantire che non venga creata alcuna cache per il modello. In alternativa, il passaggio dello stesso UUID non-null consente di creare gli oggetti della cache, ma assicura che la stessa cache venga aggiornata con ogni richiesta.

Per evitare che la cache cresca all&#39;infinito, prendete in considerazione i seguenti fattori per il rendering dei modelli generati dinamicamente tramite le nuove API AEM Forms , ovvero renderingHTMLForm2 e renderingPDFForm2.

Quando si utilizzano le nuove API, il modello viene passato come oggetto documento, che viene gestito nel servizio Forms a seconda che sia passivato o meno.

Per i documenti passivati in cui UUID e content root fungono da chiave di cache, tieni in considerazione i seguenti aspetti:
* La cache non viene creata per i modelli di input passivati senza UUID.
* Se vengono passati più modelli di input passivated con lo stesso UUID e la stessa directory principale del contenuto, la stessa cache viene sovrascritta.

Per i documenti non passivati in cui il nome del file e la radice del contenuto fungono da chiave della cache, considerate le seguenti proporzioni:
* Per i modelli di input non passivati, la memorizzazione nella cache dipende dalla radice del contenuto e dal nome del file da cui è stato generato il documento.
La stessa cache verrà utilizzata solo per le richieste con lo stesso nome file principale del contenuto e lo stesso nome file modello.
Le best practice seguenti garantiscono che la cache non si espanda all’infinito quando i modelli generati dinamicamente vengono passati al servizio Forms:
   * Eliminate l’UUID o passate lo stesso UUID in tutti i modelli generati in modo dinamico.
   * Generare il documento dai byte dei modelli o dallo stesso nome di file su disco.

### Disinstallazione di Workbench {#uninstalling-workbench}

Utilizzate la funzione Installazione applicazioni nel Pannello di controllo Campaign per avviare il programma di disinstallazione. Le applicazioni Workbench e Designer dispongono di programmi di disinstallazione separati.

## Configurazione  AEM Forms XDC Editor {#configuring-aem-forms-xdc-editor}

Utilizzando XDC Editor, gli amministratori della stampante di rete possono creare e modificare file XDC (XML Forms Architecture Device Configuration (XDC). I file XDC descrivono le caratteristiche delle stampanti, ad esempio il linguaggio di stampa o la correlazione tra il formato della carta e la posizione del vassoio.

Prima che l&#39;amministratore della stampante di rete utilizzi XDC Editor, è necessario riposizionare i file XDC di esempio e vedere Creazione di profili dispositivo tramite XDC Editor.

**Per ottenere i file** XDC di esempio:
1. Sul server AEM Forms , individuare la cartella XDC in [ radice AEM Forms]\sdk\samples\Output\IVS.
1. Copiare il contenuto di questa cartella in una directory accessibile da Workbench o dal sistema Eclipse.

**Per ottenere la Guida** di XDC Editor:
1. Visitate il sito Web della documentazione  AEM Forms.
1. Fare clic sulla scheda **Sviluppo** e passare a Creazione di profili dispositivo tramite XDC Editor. Scaricate il file xdc_editor_help_web.zip e installate i file della Guida seguendo le istruzioni fornite nel file Leggimi.

