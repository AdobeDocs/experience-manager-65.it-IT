---
title: Installare workbench
seo-title: Install workbench
description: Installare Workbench.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
role: Admin
exl-id: d530dbb9-f95e-4329-9665-37faf8f7931b
source-git-commit: 18cfefb794382b5314b18a62645f1fba28d314a2
workflow-type: tm+mt
source-wordcount: '2232'
ht-degree: 0%

---

# Installare Workbench {#install-workbench}

Questo documento fornisce istruzioni per l’installazione e la configurazione di AEM Forms Workbench. Il programma di installazione installa anche Forms Designer.

## Chi dovrebbe leggere questo documento? {#who-should-read-this-doc}

Questo documento è destinato agli amministratori o agli sviluppatori responsabili dell’installazione, della configurazione, dell’amministrazione o della distribuzione di Workbench. Sono incluse anche le informazioni per configurare il sistema in modo da supportare i processi AEM Forms aggiornati. Le informazioni fornite si basano sul presupposto che chiunque legga questo documento conosca il sistema operativo Microsoft® Windows®.

## Informazioni aggiuntive {#additional-information}

Le risorse presenti in questa tabella possono essere utili per ulteriori informazioni e per iniziare a utilizzare AEM Forms.
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
   <td><p>Informazioni generali su AEM Forms e su come si integra con altri prodotti Adobe</p> </td>
   <td><p><a href="https://experienceleague.adobe.com/docs/experience-manager-65/forms/getting-started/introduction-aem-forms.html?lang=en">Panoramica di AEM Forms</a><br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Tutta la documentazione disponibile per AEM Forms</p> </td>
   <td><p><a href="https://experienceleague.adobe.com/docs/experience-manager-65/forms/getting-started/introduction-aem-forms.html?lang=en">Documentazione di AEM Forms</a><br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Aggiornamenti patch, note tecniche e informazioni aggiuntive su questa versione del prodotto</p> </td>
   <td><p>Contatta l’Adobe di supporto Enterprise</a><br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Flex Workspace è obsoleto per AEM Forms. È disponibile per la versione AEM Forms.

## Prima dell’installazione {#before-you-install}

### Panoramica sull’installazione di Workbench {#workbench-installation-overview}

Workbench è un ambiente di sviluppo integrato (IDE, Integrated Development Environment) utilizzato dagli sviluppatori e dagli autori di moduli per creare processi e moduli aziendali automatizzati. Viene inoltre utilizzato per gestire le risorse e i servizi utilizzati dai processi e dai moduli.

L’illustrazione seguente illustra l’installazione di Workbench, tra cui:
* Progettazione processi tramite Workbench
* Progettazione moduli tramite Designer

>[!NOTE]
>
>Il server AEM Forms richiede un programma di installazione separato. Per ulteriori informazioni, consulta la documentazione sull’installazione di AEM Forms su JEE.

![default-render-form](assets/installing-workbench.png)

## Prerequisiti di sistema {#system-prerequisites}

Questa sezione descrive i requisiti hardware e software e le piattaforme supportate.

### Requisiti minimi hardware e software {#minimum-hardware-software-requirements}

**Workbench**
Si consigliano come minimo i seguenti requisiti: Spazio su disco per l&#39;installazione:
* 680 MB solo per Workbench.
* 2,15 GB su un&#39;unica unità per un&#39;installazione completa di Workbench, Designer e dell&#39;assieme samples.
* 400 MB per le directory di installazione temporanee - 200 MB nella directory utente \temp e 200 MB nella directory temporanea di Windows.

>[!NOTE]
>
>Se tutte queste posizioni si trovano su un&#39;unica unità, durante l&#39;installazione devono essere disponibili 1,5 GB di spazio. I file copiati nelle directory temporanee vengono eliminati al termine dell&#39;installazione.

* Requisiti hardware: processore Intel® Pentium® 4 o AMD® equivalente a 1 GHz.
* Java™ Runtime Environment (JRE) 7.0 aggiorna la versione 51 o successiva alla versione 7.0.
* Risoluzione minima del monitor 1024 X 768 pixel o superiore con colore a 16 bit o superiore.
* Connessione di rete TCP/IPv4 o TCP/IPv6 al server AEM Forms.
* Installare i pacchetti runtime ridistribuibili di Visual C++ 2012 a 32 bit.
* Installare i pacchetti runtime ridistribuibili di Visual C++ 2013 a 32 bit.

>[!NOTE]
>
>Per installare Workbench è necessario disporre dei privilegi di amministratore. Se si sta effettuando l&#39;installazione utilizzando un account non amministratore, il programma di installazione richiederà le credenziali per un account appropriato.

### Piattaforme supportate {#supported-platforms}

Consulta l’elenco completo delle piattaforme supportate per Workbench all’indirizzo [Piattaforme supportate da AEM Forms](https://www.adobe.com/go/learn_aemforms_supportedplatforms_65).

## Considerazioni sull’installazione di Designer {#designer-installation-considerations}

Per impostazione predefinita, l’installazione di Workbench include una versione di Designer corrispondente in lingua inglese. Se l&#39;applicazione di installazione di Workbench rileva una versione esistente di Designer nel computer, l&#39;installazione potrebbe terminare e prima di continuare è necessario rimuovere la versione corrente di Designer.
La tabella seguente contiene un elenco completo dei possibili scenari di installazione di Designer che possono verificarsi e delle azioni da intraprendere durante l’installazione di Workbench.

<table>
 <tbody>
  <tr>
   <td><p><strong>Versione di Designer attualmente installata</strong></p> </td>
   <td><p><strong>Azioni necessarie</strong></p> </td>
  </tr>
  <tr>
   <td><p>Acrobat Pro o Acrobat Pro Extended (include Designer)</p> </td>
   <td><p>Nessuno.<br /> 
L’installazione di Workbench rileva un’istanza di Designer sul computer installata con Acrobat Pro o Acrobat Pro Extended.<br />
Diverse versioni di Designer possono coesistere nello stesso sistema, ad esempio Designer 6.4.x per Workbench 6.4 e Designer 6.5.0.x per Workbench 6.5. Non è necessario disinstallare la versione di Designer installata con Acrobat 10 Pro o Acrobat 10 Pro Extended o versione successiva.
<br /></p> </td>
  </tr>
  <tr>
   <td><p>Designer (autonomo)</p> </td>
   <td><p>Nessuno. <br />La versione di Designer inclusa in Workbench è di sola inglese. <br />Il programma di installazione di Workbench non reinstallerà una nuova versione di Designer. Verrà invece applicata la patch a una versione aggiornata, inclusa nel pacchetto con il programma di installazione di Workbench. Questo consente anche di utilizzare la versione localizzata di Designer in Workbench.<br /> </p> </td>
  </tr>
 </tbody>
</table>

### Per disinstallare Designer (autonomo) su Windows 10 {#uninstall-designer-standalone-windows10}

1. Vai a **Pannello di controllo Campaign > Programmi > Programmi e funzionalità**
1. Nell&#39;elenco Programmi attualmente installati selezionare **Designer Adobe**.
1. Clic **Disinstalla** e quindi fare clic su **Sì**.

## Installazione di Workbench {#installing-workbench}

Questo capitolo descrive come installare Workbench.

### Installazione ed esecuzione di Workbench {#installing-and-running-workbench}

Prima di installare Workbench, è necessario assicurarsi che l&#39;ambiente includa il software e l&#39;hardware necessari per eseguirlo (vedere la sezione: **Prima dell’installazione**).

**Per installare ed eseguire Workbench:**

1. Eseguire una delle operazioni seguenti:
   * Passare alla directory \workbench sul supporto di installazione e fare doppio clic sul file run_windows_installer.bat.
   * Scarica e decomprimi Workbench nel file system. Dopo averlo scaricato, passare alla directory \workbench e fare doppio clic sul file run_windows_installer.bat.

   >[!IMPORTANT]
   >
   >Il programma di installazione di Workbench viene eseguito solo da un&#39;unità locale. Non può essere eseguito da un sito remoto.

   >[!NOTE]
   >
   >Se si verifica un errore di tipo &quot;Impossibile creare la Java™ Virtual Machine&quot;, creare una variabile di ambiente denominata _JAVA_OPTIONS con valore -Xmx512M ed eseguire il programma di installazione.

1. Nella schermata introduttiva, fai clic su Avanti.
1. Leggere il Contratto di Licenza del Prodotto, selezionare Accetto i termini del Contratto di Licenza e quindi fare clic su Avanti.
1. (Facoltativo) Se questo strumento è necessario per la creazione e la modifica di moduli, selezionare Installa Designer Adobi.

   >[!NOTE]
   Per continuare a utilizzare Designer installato con Acrobat 10, lascia deselezionata questa opzione.

1. Accettare la directory predefinita come elencato oppure fare clic su Scegli e passare alla directory in cui si desidera installare Workbench e quindi fare clic su Avanti.

   >[!NOTE]
   Il percorso della directory di installazione non può contenere i caratteri # (libbra) e $ (dollaro).

1. Rivedere il riepilogo della preinstallazione e fare clic su Installa. Il programma di installazione visualizza lo stato di avanzamento dell&#39;installazione.
1. Esaminare il riepilogo dell&#39;installazione. Seleziona Avvia AEM Forms Workbench per avviare Workbench e fai clic su Avanti.
1. Consulta le Note sulla versione e fai clic su Fine.
1. I seguenti elementi sono ora installati nel computer:
   * **Workbench**: per eseguire Workbench dal menu Start, selezionare Tutti i programmi > AEM Forms > Workbench, se si è scelto di memorizzare la cartella dei collegamenti. Per informazioni, vedere <a href="https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf">Utilizzo di Workbench</a> documentazione.
   * **Designer**: puoi accedere a Designer da Workbench. Per informazioni, consulta l’argomento Guida introduttiva in <a href="https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/using-designer.pdf">Guida di Designer</a>.
   * **SDK di AEM Forms**: per ulteriori informazioni sull’utilizzo dell’SDK, consulta <a href="https://helpx.adobe.com/pdf/aem-forms/6-3/programming-with-aem-forms.pdf">Programmazione con AEM Forms</a>.

## Aggiornamento dei processi {#upgrading-processes}

I processi AEM Forms su JEE possono essere aggiornati alle applicazioni AEM Forms utilizzando l’Aggiornamento guidato. Per ulteriori informazioni, consulta Aggiornamento della documentazione degli artefatti legacy nella Guida di Workbench.

### Configurazione e accesso a un server {#configuring-and-logging-server}

Per utilizzare Workbench, è necessario disporre di un&#39;istanza di AEM Forms in esecuzione, in genere su un computer separato. È necessario disporre di un nome utente e di una password per accedere ad AEM Forms, nonché di dettagli sulla posizione del server.

>[!NOTE]
Se AEM Forms è stato configurato per l&#39;utilizzo del provider di repository EMC Documentum® o IBM® FileNet e si desidera accedere a un repository diverso da quello configurato come predefinito nella console di amministrazione dei moduli AEM, specificare il nome utente come username@Repository.

### Configurazione delle impostazioni di timeout {#configuring-timeout-settings}

Per impostazione predefinita, Workbench riceve un timeout dopo due ore, indipendentemente dall’attività o dall’inattività. Per modificare l’impostazione di timeout, consulta &quot;Configurazione della gestione utente > Configurazione degli attributi di sistema avanzati&quot; in <a href="https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/configure-user-management/configure-advanced-system-attributes.html">Guida della console di amministrazione</a>.

### Configurazione di Workbench per la connessione tramite HTTPS {#configuring-workbench-to-connect-over-HTTPS}

Per connettere Workbench a un server AEM Forms tramite HTTPS, è necessario assicurarsi che l’autorità di certificazione (CA) che ha emesso la chiave pubblica venga riconosciuta come attendibile da Workbench. Se il certificato non viene riconosciuto come proveniente da una fonte attendibile, è necessario aggiornare il file cacert in [Workbench_HOME]directory /workbench/jre/lib/security.

>[!NOTE]
[Workbench_HOME] rappresenta la directory in cui è stato installato Workbench. Il percorso predefinito è C:\Program Files (x86)\Adobe Experience Manager Forms Workbench.

Assicurati di connetterti a HTTPS utilizzando il nome specificato nel certificato. Questo nome è in genere il nome host completo.

**Per aggiornare il file cacert**:
1. Verificare di disporre di una copia del certificato SSL (Secure Sockets Layer). Contatta l’amministratore che ha configurato il server SSL o esporta il certificato utilizzando un browser web.

   >[!NOTE]
   Per esportare il certificato, apri un browser web e accedi alla console di amministrazione, installa il certificato nel browser, quindi esportalo dal browser in un percorso di archiviazione temporaneo (o direttamente nel [Workbench_HOME]/workbench/jre/lib/security).

1. Copia il certificato in [Workbench_HOME]directory /workbench/jre/lib/security.

1. Aprire una finestra del prompt dei comandi, passare a [Workbench_HOME]/workbench/jre/bin, quindi digitare il comando seguente:
   `keytool -import -storepass changeit -file [Workbench_HOME]\workbench\jre\lib\security\ssl_cert_for_certname.cer -keystore [Workbench_HOME]\workbench\jre\lib\security\cacerts -alias example`
Dove:
   * `changeit` è la password predefinita per il keystore di cacerts.
   * certname è il certificato selezionato al passaggio 1.
   * esempio è l’alias scelto per il certificato. Questo valore può essere modificato.

1. Quando viene richiesto di considerare attendibile il certificato, digitare Sì e premere Invio. Lo strumento chiave procede con l&#39;importazione del file cacerts in [Workbench_HOME]directory /workbench/jre/lib/security.

1. Chiudere e riavviare Workbench per applicare le modifiche.

### Configurazione delle impostazioni della cache per i modelli generati in modo dinamico {#configuring-cache-settings-for-dynamically-generated-templates}

Se l’applicazione genera al volo modelli univoci aggiornando automaticamente il contenuto XFA, è necessario considerare i seguenti aspetti del funzionamento della cache. In effetti, ogni transazione utilizza un nuovo modello univoco.

Quando il generatore o l’output di Forms cerca o aggiorna voci nella cache per un modello di modulo specifico, utilizza diversi valori chiave per individuare la voce specifica nella cache a cui si accede.

* **Nome file modello**: posizione e nome del modello utilizzato come identificatore univoco principale del modulo memorizzato in cache.
* **Timestamp**: il file modello contiene una marca temporale utilizzata per determinare l’ora dell’ultimo aggiornamento del modulo.
* **UUID modello**: Designer inserisce in ogni modello un identificatore univoco (UUID) per il modulo e la relativa versione. Ogni volta che il modulo viene aggiornato, l’UUID incorporato viene aggiornato. Ad esempio, un modello XDP potrebbe mostrare il seguente contenuto:

   `<?xml version="1.0" encoding="UTF-8"?>`
   `<?xfa generator="AdobeAEM formsDesignerES_V8.2" APIVersion="2.6.7185.0"?><xdp:xdp xmlns:xdp=https://ns.adobe.com/xdp/ timeStamp="2008-07-29T21:22:12Z" uuid="823e538f-ff6c-4961-b759-f7626978a223"><template xmlns="https://www.xfa.org/schema/xfa-template/2.6/">`

* **Opzioni di rendering**: all’interno della cache dei moduli renderizzati, il contenuto della cache viene memorizzato separatamente per ogni set di opzioni di rendering univoche.


Il servizio Forms riceve i modelli in base al nome del file o alla posizione del repository oppure in base al valore come oggetto XML in memoria.
* **Modelli passati per riferimento**: utilizza la directory principale del contenuto e il nome del modulo. Se in ogni richiesta vengono passati modelli univoci con nomi di file diversi utilizzando questo metodo, la cache del disco cresce all&#39;infinito e non viene mai riutilizzata. Per evitare questo problema, è necessario trasmettere modelli univoci con lo stesso nome file per garantire che la stessa cache venga aggiornata per tutte le richieste.
* **Modelli passati per valore**: utilizza i byte dei modelli passati insieme ai dati utilizzando il parametro inDataDoc. Se vengono passati modelli univoci con UUID diversi utilizzando questo metodo, la cache del disco cresce all&#39;infinito e non verrà mai riutilizzata. Per evitare questo problema, l’attributo UUID deve essere rimosso da tutti i modelli per garantire che non venga creata alcuna cache per il modello. In alternativa, il passaggio dello stesso UUID non nullo consente di creare gli oggetti cache, ma assicura che la stessa cache venga aggiornata con ogni richiesta.

Per evitare che la cache cresca all’infinito, considera i seguenti fattori per il rendering dei modelli generati in modo dinamico utilizzando le nuove API di AEM Forms, ovvero renderHTMLForm2 e renderPDFForm2.

Quando si utilizzano le nuove API, il modello viene passato come oggetto documento, che viene gestito nel servizio Forms a seconda che sia passivo o meno.

Per i documenti passivi in cui l’UUID e la directory principale del contenuto fungono da chiave della cache, considera i seguenti aspetti:
* La cache non viene creata per i modelli di input passivati senza UUID.
* Se viene passato più di un modello di input passivo con lo stesso UUID e la stessa directory principale del contenuto, la stessa cache viene sovrascritta.

Per i documenti non passivi in cui il nome file e la radice del contenuto fungono da chiave della cache, considera il seguente aspetto:
* Per i modelli di input non passivi, la memorizzazione nella cache dipende dalla directory principale del contenuto e dal nome del file da cui è stato generato il documento.
La stessa cache viene utilizzata solo per le richieste con lo stesso nome file radice e modello di contenuto.
Le seguenti best practice garantiscono che la cache non aumenti all’infinito quando i modelli generati in modo dinamico vengono passati al servizio Forms:
   * Rimuovi l’UUID o passa lo stesso UUID in tutti i modelli generati in modo dinamico.
   * Generare il documento da byte modello o dallo stesso nome file su disco.

### Disinstallazione di Workbench {#uninstalling-workbench}

Utilizzare la funzione Installazione applicazioni nel Pannello di controllo Campaign per avviare il programma di disinstallazione. Le applicazioni Workbench e Designer dispongono di programmi di disinstallazione separati.

## Configurazione di AEM Forms XDC Editor {#configuring-aem-forms-xdc-editor}

Utilizzando l&#39;editor XDC, gli amministratori delle stampanti di rete possono creare e modificare i file XDC (XML Forms Architecture Device Configuration). I file XDC descrivono le funzionalità delle stampanti, ad esempio il linguaggio della stampante o la correlazione tra il formato della carta e la posizione del cassetto.

Prima che l&#39;amministratore della stampante di rete utilizzi l&#39;editor XDC, riposizionare i file XDC di esempio e vedere Creazione di profili di dispositivo con l&#39;editor XDC.

**Per ottenere i file XDC di esempio**:
1. Sul server AEM Forms, individua la cartella XDC in [Directory principale di AEM Forms]\sdk\samples\Output\IVS.
1. Copia il contenuto di questa cartella in una directory accessibile dal Workbench o dal sistema Eclipse.

**Per ottenere la Guida dell&#39;editor XDC**:
1. Vai al sito web della documentazione di AEM Forms.
1. Fai clic su **Sviluppa** e passa a Creazione di profili dispositivo tramite l’editor XDC. Scaricare il file xdc_editor_help_web.zip e installare i file della Guida seguendo le istruzioni fornite nel file Leggimi.
