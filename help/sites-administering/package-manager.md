---
title: Come lavorare con i pacchetti
seo-title: Come lavorare con i pacchetti
description: Scopri le basi dell'utilizzo dei pacchetti in AEM.
seo-description: Scopri le basi dell'utilizzo dei pacchetti in AEM.
uuid: cba76a5f-5d75-4d63-a0f4-44c13fa1baf2
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 6694a135-d1e1-4afb-9f5b-23991ee70eee
docset: aem65
translation-type: tm+mt
source-git-commit: 03967fcdc9685c9a8bf1dead4bd5e389603ff91b
workflow-type: tm+mt
source-wordcount: '3934'
ht-degree: 1%

---


# Come utilizzare i pacchetti{#how-to-work-with-packages}

I pacchetti consentono di importare ed esportare il contenuto del repository. Ad esempio, potete utilizzare i pacchetti per installare nuove funzionalità, trasferire contenuti tra le istanze e eseguire il backup del contenuto del repository.

È possibile accedere ai pacchetti e/o mantenerli nelle pagine seguenti:

* [Gestione](#package-manager) pacchetti, che consente di gestire i pacchetti nell&#39;istanza AEM locale.

* [Distribuzione](#software-distribution) software, un server centralizzato che contiene sia i pacchetti disponibili al pubblico che quelli privati per la società. I pacchetti pubblici possono contenere hotfix, nuove funzionalità, documentazione, ecc.

È possibile trasferire i pacchetti tra il gestore pacchetti, la distribuzione software e il file system.

## Che cosa sono i pacchetti? {#what-are-packages}

Un pacchetto è un file zip che contiene il contenuto del repository sotto forma di serializzazione del file system (chiamata serializzazione &quot;vault&quot;). Questo fornisce una rappresentazione semplice da usare e modificare di file e cartelle.

I pacchetti includono il contenuto, sia contenuto della pagina che contenuto relativo al progetto, selezionato utilizzando i filtri.

Un pacchetto contiene anche metadati di archivio, comprese le definizioni dei filtri e le informazioni di configurazione dell&#39;importazione. Nel pacchetto possono essere incluse ulteriori proprietà di contenuto (non utilizzate per l&#39;estrazione del pacchetto), ad esempio una descrizione, un&#39;immagine visiva o un&#39;icona; queste proprietà sono riservate al consumatore del pacchetto di contenuti e sono riservate solo a scopo informativo.

>[!NOTE]
>
>I pacchetti rappresentano la versione corrente del contenuto al momento della creazione del pacchetto. Non includono versioni precedenti del contenuto che AEM conservato nella directory archivio.

Potete eseguire le azioni seguenti su o con i pacchetti:

* Creare nuovi pacchetti; definizione delle impostazioni e dei filtri del pacchetto come richiesto
* Anteprima del contenuto del pacchetto (prima della creazione)
* Creare pacchetti
* Visualizzazione delle informazioni sul pacchetto
* Visualizzare il contenuto del pacchetto (dopo la creazione)
* Modificare la definizione dei pacchetti esistenti
* Ricreare i pacchetti esistenti
* Riavvolgere i pacchetti
* Scaricare pacchetti da AEM al file system
* Caricare i pacchetti dal file system nell’istanza AEM locale
* Convalida del contenuto del pacchetto prima dell&#39;installazione
* Eseguire un&#39;installazione a prova di secco
* Installare i pacchetti (AEM non installa automaticamente i pacchetti dopo il caricamento)
* Eliminare i pacchetti
* Scaricare pacchetti, come hotfix, dalla libreria Distribuzione software
* Caricare i pacchetti nella sezione interna della società della libreria Distribuzione software

## Informazioni pacchetto {#package-information}

Una definizione di pacchetto è composta da vari tipi di informazioni:

* [Impostazioni pacchetto](#package-settings)
* [Filtri pacchetto](#package-filters)
* [Schermate pacchetto](#package-screenshots)
* [Icone pacchetto](#package-icons)

### Impostazioni pacchetto {#package-settings}

Potete modificare diverse impostazioni del pacchetto per definire aspetti quali la descrizione del pacchetto, i bug correlati, le dipendenze e le informazioni sul fornitore.

La finestra di dialogo **Impostazioni pacchetto** è disponibile tramite il pulsante **Modifica** quando [create](#creating-a-new-package) o [editing](#viewing-and-editing-package-information) un pacchetto e fornisce tre schede per la configurazione. Dopo aver apportato le modifiche, fare clic su **OK** per salvarle.

![packagesedit](assets/packagesedit.png)

| **Campo** | **Descrizione** |
|---|---|
| Nome | Nome del pacchetto. |
| Gruppo | Nome del gruppo a cui aggiungere il pacchetto per organizzare i pacchetti. Digitate il nome di un nuovo gruppo o selezionate un gruppo esistente. |
| Versione | Testo da utilizzare per la versione personalizzata. |
| Descrizione | Breve descrizione del pacchetto. È possibile utilizzare i tag HTML per la formattazione. |
| Miniatura  | Icona visualizzata con l&#39;elenco dei pacchetti. Fate clic su Sfoglia per selezionare un file locale. |

![chlimage_1-108](assets/chlimage_1-108.png)

<table>
 <tbody>
  <tr>
   <th><strong>Campo</strong></th>
   <th><strong>Descrizione</strong></th>
   <th><strong>Formato/Esempio</strong></th>
  </tr>
  <tr>
   <td>Nome</td>
   <td>Nome del provider.</td>
   <td><em>Geometrixx AEM<br /> </em></td>
  </tr>
  <tr>
   <td>URL</td>
   <td>URL del provider.</td>
   <td><em>https://www.aem-geometrixx.com</em></td>
  </tr>
  <tr>
   <td>Collegamento</td>
   <td>Collegamento specifico al pacchetto a una pagina del fornitore.</td>
   <td><em>https://www.aem-geometrixx.com/mypackage.html</em></td>
  </tr>
  <tr>
   <td>Richiede<br /> </td>
   <td>
    <ul>
     <li>Amministratore: Selezionate quando il pacchetto può essere installato solo da un account con privilegi di amministratore.</li>
     <li>Riavvia: Selezionate quando il server deve essere riavviato dopo l'installazione del pacchetto.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Gestione AC</td>
   <td><p>Specificate come vengono gestite le informazioni sul controllo di accesso definite nel pacchetto quando il pacchetto viene importato:</p>
    <ul>
     <li><strong>Ignora</strong></li>
     <li><strong>Sovrascrivi</strong></li>
     <li><strong>Unisci</strong></li>
     <li><strong>Cancella</strong></li>
     <li><strong>MergePreserve</strong></li>
    </ul> <p>Il valore predefinito è <strong>Ignore</strong>.</p> </td>
   <td>
    <ul>
     <li><strong>Ignora</strong> : mantiene gli ACL nell'archivio</li>
     <li><strong>Sovrascrivi</strong> : sovrascrivi ACL nell'archivio</li>
     <li><strong>Unisci</strong> : unisci entrambi i set di ACL</li>
     <li><strong>Cancella</strong>  - ACL trasparenti</li>
     <li><strong>MergePreserve</strong> : consente di unire il controllo di accesso nel contenuto con quello fornito con il pacchetto aggiungendo le voci di controllo di accesso delle entità non presenti nel contenuto</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

![packagesdipendenze](assets/packagesdependencies.png)

| **Campo** | **Descrizione** | **Formato/Esempio** |
|---|---|---|
| Test con | Il nome e la versione del prodotto a cui è destinato il pacchetto o con cui è compatibile. | *AEM 6* |
| Bug/Problemi risolti | Campo di testo che consente di elencare i dettagli dei bug corretti con questo pacchetto. Elenca ciascun bug su una riga separata. | riepilogo bug-nr |
| Dipende da | Elenca le informazioni sulle dipendenze che devono essere rispettate ogni volta che sono necessari altri pacchetti per consentire l&#39;esecuzione del pacchetto corrente come previsto. Questo campo è importante quando si utilizzano gli hotfix. | groupId:name:version |
| Sostituisce | Un elenco di pacchetti obsoleti che il pacchetto sostituisce. Prima di eseguire l&#39;installazione, verificate che il pacchetto includa tutto il contenuto necessario dai pacchetti obsoleti, in modo da non sovrascrivere il contenuto. | groupId:name:version |

### Filtri pacchetto {#package-filters}

I filtri identificano i nodi del repository da includere nel pacchetto. A **Filter Definition** specifica le informazioni seguenti:

* Il **percorso principale** del contenuto da includere.
* **Regole** che includono o escludono nodi specifici sotto il percorso principale.

I filtri possono includere zero o più regole. Quando non sono definite regole, il pacchetto contiene tutto il contenuto al di sotto del percorso principale.

Potete definire una o più definizioni di filtro per un pacchetto. Utilizzate più di un filtro per includere il contenuto proveniente da più percorsi principali.

![chlimage_1-109](assets/chlimage_1-109.png)

Nella tabella seguente sono descritte le regole e sono riportati alcuni esempi:

<table>
 <tbody>
  <tr>
   <th> Tipo di regola</th>
   <th>Descrizione </th>
   <th>Esempio </th>
  </tr>
  <tr>
   <td> includi</td>
   <td>È possibile definire un percorso o utilizzare un'espressione regolare per specificare tutti i nodi che si desidera includere.<br /> <br /> Includendo una directory:
    <ul>
     <li>includere la directory <i>e</i> tutti i file e le cartelle presenti in tale directory (ovvero l'intera sottostruttura)</li>
     <li><strong>non </strong> includere altri file o cartelle dal percorso principale specificato</li>
    </ul> </td>
   <td>/libs/sling/install(/.*)? </td>
  </tr>
  <tr>
   <td> escludi</td>
   <td>È possibile specificare un percorso o utilizzare un'espressione regolare per specificare tutti i nodi da escludere.<br /> <br /> Escludendo una directory, tale directory  <i></i> e tutti i file e le cartelle presenti in tale directory (ovvero l’intera sottostruttura) verranno esclusi.<br /> </td>
   <td>/libs/wcm/foundation/components(/.*)?</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Un pacchetto può contenere più definizioni di filtro, in modo che i nodi di diverse ubicazioni possano essere facilmente combinati in un unico pacchetto.

I filtri pacchetto vengono definiti più spesso quando [create il pacchetto](#creating-a-new-package), ma possono essere modificati anche in un secondo momento (dopodiché il pacchetto deve essere rigenerato).

### Schermate pacchetto {#package-screenshots}

Potete allegare schermate al pacchetto per fornire una rappresentazione visiva dell&#39;aspetto del contenuto; ad esempio, fornendo schermate di nuove funzionalità.

### Icone pacchetto {#package-icons}

Potete anche allegare un’icona al pacchetto per fornire una rappresentazione visiva di riferimento rapido del contenuto del pacchetto. Questo viene visualizzato nell&#39;elenco dei pacchetti e può essere utile per identificare facilmente il pacchetto o la classe del pacchetto.

Poiché un pacchetto può contenere un&#39;icona, per i pacchetti ufficiali vengono utilizzate le seguenti convenzioni:

>[!NOTE]
>
>Per evitare confusione, usate un’icona descrittiva per il pacchetto e non usate una delle icone ufficiali.

Pacchetto Hotfix ufficiale:

![](do-not-localize/chlimage_1-28.png)

Pacchetto di installazione o estensione AEM ufficiale:

Pacchetti di funzioni ufficiali:

![](do-not-localize/chlimage_1-29.png)

## Gestione pacchetti {#package-manager}

Gestione pacchetti gestisce i pacchetti nell&#39;installazione AEM locale. Dopo aver [assegnato le autorizzazioni necessarie](#permissions-needed-for-using-the-package-manager) potete utilizzare Gestione pacchetti per diverse azioni, tra cui la configurazione, la creazione, il download e l&#39;installazione dei pacchetti. Gli elementi chiave da configurare sono:

* [Impostazioni pacchetto](#package-settings)
* [Filtri pacchetto](#package-filters)

### Autorizzazioni necessarie per l&#39;utilizzo di Package Manager {#permissions-needed-for-using-the-package-manager}

Per concedere agli utenti il diritto di creare, modificare, caricare e installare pacchetti, dovete concedere loro le autorizzazioni appropriate nei seguenti percorsi:

* **/etc/packages** (diritti completi esclusa l’eliminazione)
* il nodo che contiene il contenuto del pacchetto

Per istruzioni sulla modifica delle autorizzazioni, vedere [Impostazione delle autorizzazioni](/help/sites-administering/security.md#setting-page-permissions).

### Creazione di un nuovo pacchetto {#creating-a-new-package}

Per creare una nuova definizione di pacchetto:

1. Nella schermata di benvenuto AEM, fate clic su **Pacchetti** oppure, dalla console **Strumenti**, fate doppio clic su **Pacchetti**.

1. Selezionate quindi **Gestione pacchetti**.
1. Fare clic su **Crea pacchetto**.

   >[!NOTE]
   >
   >Se l’istanza include molti pacchetti, potrebbe essere presente una struttura di cartelle, in modo da poter passare alla cartella di destinazione richiesta prima di creare il nuovo pacchetto.

1. Nella finestra di dialogo:

   ![packagesnew](assets/packagesnew.png)

   Immettere:

   * **Nome gruppo**

      Nome del gruppo di destinazione (o cartella). I gruppi sono destinati all’organizzazione dei pacchetti.

      Se il gruppo non esiste già, viene creata una cartella. Se lasciate vuoto il nome del gruppo, verrà creato il pacchetto nell&#39;elenco dei pacchetti principali (Home > Pacchetti).

   * **Nome pacchetto**

      Nome del nuovo pacchetto. Selezionate un nome descrittivo per identificare facilmente i contenuti del pacchetto.

   * **Versione**

      Campo di testo per indicare una versione. Questo verrà aggiunto al nome del pacchetto per formare il nome del file zip.
   Fate clic su **OK** per creare il pacchetto.

1. AEM elenca il nuovo pacchetto nella cartella del gruppo appropriata.

   ![packagesitem](assets/packagesitem.png)

   Fate clic sull&#39;icona o sul nome del pacchetto da aprire.

   ![packagesitemcliccato](assets/packagesitemclicked.png)

   >[!NOTE]
   >
   >Se necessario, potete tornare a questa pagina in un secondo momento.

1. Fare clic su **Modifica** per modificare le impostazioni [del pacchetto](#package-settings).

   Qui è possibile aggiungere informazioni e/o definire determinate impostazioni; ad esempio, questi includono una descrizione, l&#39; [icona](#package-icons), i bug correlati e aggiungere i dettagli del fornitore.

   Fare clic su **OK** al termine della modifica delle impostazioni.

1. Aggiungete **[Screenshots](#package-screenshots)** al pacchetto come necessario. Quando viene creato il pacchetto, è disponibile un&#39;istanza; se necessario, aggiungete altro utilizzando **Package Screenshot** dalla barra laterale.

   Aggiungete l&#39;immagine effettiva facendo doppio clic sul componente immagine nell&#39;area **Screenshots**, aggiungendo un&#39;immagine e facendo clic su **OK**.

1. Definite i **[filtri pacchetto](#package-filters)** trascinando le istanze del **filtro definizione** dalla barra laterale, quindi fate doppio clic per aprire la finestra di modifica:

   ![packagesfilter](assets/packagesfilter.png)

   Specifica:

   * **Percorso**
radice: il contenuto da includere nel pacchetto; può essere la radice di un sottoalbero.
   * ****
RulesRules sono facoltative; per le definizioni di pacchetti semplici, non è necessario specificare regole di inclusione o esclusione.

      Se necessario, potete definire [**Includi** o **Escludi** regole](#package-filters) per definire esattamente il contenuto del pacchetto.

      Aggiungete le regole utilizzando il simbolo **+**, in alternativa rimuovete le regole utilizzando il simbolo **-**. Le regole vengono applicate in base al loro ordine, in modo da posizionarle come necessario utilizzando i pulsanti **Su** e **Giù**.
   Fare clic su **OK** per salvare il filtro.

   >[!NOTE]
   >
   >Puoi utilizzare tutte le definizioni di filtro necessarie, ma devi fare attenzione a non creare conflitti. Utilizzate **Preview** per confermare quali saranno i contenuti del pacchetto.

1. Per confermare il contenuto del pacchetto, potete utilizzare **Preview**. Questo esegue una prova a secco del processo di compilazione ed elenca tutti gli elementi che verranno aggiunti al pacchetto quando viene effettivamente costruito.
1. Ora è possibile [Generare](#building-a-package) il pacchetto.

   >[!NOTE]
   >
   >Non è obbligatorio costruire il pacchetto a questo punto, può essere fatto in un momento successivo.

### Creazione di un pacchetto {#building-a-package}

Spesso un pacchetto viene creato contemporaneamente alla [creazione della definizione del pacchetto](#creating-a-new-package), ma potete tornare in un momento successivo per creare o ricreare il pacchetto. Questo può essere utile se il contenuto all’interno della directory archivio è stato modificato.

>[!NOTE]
>
>Prima di creare il pacchetto può essere utile visualizzare in anteprima il contenuto del pacchetto. Fare clic su **Anteprima**.

1. Aprite la definizione del pacchetto da **Gestione pacchetti** (fate clic sull&#39;icona o sul nome del pacchetto).

1. Fare clic su **Build**. Viene visualizzata una finestra di dialogo con richiesta di conferma per confermare la creazione del pacchetto.

   >[!NOTE]
   >
   >Questo è particolarmente importante quando si sta ricreando un pacchetto in quanto il contenuto del pacchetto verrà sovrascritto.

1. Fai clic su **OK**. AEM creare il pacchetto, elencando tutti i contenuti aggiunti al pacchetto così come lo è. Al termine del AEM viene visualizzata una conferma che il pacchetto è stato creato e (quando chiudete la finestra di dialogo) aggiorna le informazioni dell’elenco dei pacchetti.

### Rewrapping di un pacchetto {#rewrapping-a-package}

Una volta creato, un pacchetto può essere reinserito, se necessario.

Il rewrapping modifica le informazioni sul pacchetto - *senza* modificare il contenuto del pacchetto. Le informazioni sul pacchetto sono la miniatura, la descrizione, ecc., in altre parole tutto ciò che è possibile modificare con la finestra di dialogo **Impostazioni pacchetto** (per aprire questo clic **Modifica**).

Un caso di utilizzo importante per il rewrapping è durante la preparazione di un pacchetto. Ad esempio, potreste avere un pacchetto esistente e decidere di condividerlo con altri utenti. Per aggiungere una miniatura, aggiungere una descrizione. Invece di ricreare l&#39;intero pacchetto con tutte le sue funzionalità (che potrebbero richiedere un po&#39; di tempo e comporta il rischio che il pacchetto non sia più identico all&#39;originale) potete reinserirlo e aggiungere semplicemente la miniatura e la descrizione.

1. Aprite la definizione del pacchetto da **Gestione pacchetti** (fate clic sull&#39;icona o sul nome del pacchetto).

1. Fare clic su **Modifica** e aggiornare le impostazioni **[Package Settings](#package-settings)** come necessario. Fate clic su **OK** per salvare. 

1. Fare clic su **Rewrapper**. Viene visualizzata una finestra di dialogo per richiedere una conferma.

### Visualizzazione e modifica delle informazioni sul pacchetto {#viewing-and-editing-package-information}

Per visualizzare o modificare le informazioni sulla definizione di un pacchetto:

1. In Gestione pacchetti, andate al pacchetto da visualizzare.
1. Fate clic sull&#39;icona del pacchetto da visualizzare. Viene aperta la pagina del pacchetto in cui sono elencate le informazioni sulla definizione del pacchetto:

   ![packagesitemclicked-1](assets/packagesitemclicked-1.png)

   >[!NOTE]
   >
   >Potete anche modificare ed eseguire determinate azioni sul pacchetto da questa pagina.
   >
   >I pulsanti disponibili dipendono dal fatto che il pacchetto sia già stato creato o meno.

1. Se il pacchetto è già stato creato, fate clic su **Contents**, si aprirà una finestra con l&#39;elenco completo del contenuto del pacchetto:

### Visualizzazione del contenuto del pacchetto e installazione di test {#viewing-package-contents-and-testing-installation}

Dopo aver creato un pacchetto, potete visualizzare i contenuti:

1. In Gestione pacchetti, andate al pacchetto da visualizzare.
1. Fate clic sull&#39;icona del pacchetto da visualizzare. Viene aperta la pagina del pacchetto con le informazioni sulla definizione del pacchetto.

1. Per visualizzare il contenuto fare clic su **Contents**, si apre una finestra con l&#39;elenco completo del contenuto del pacchetto:

   ![packgescontents](assets/packgescontents.png)

1. Per eseguire una prova a secco dell&#39;installazione, fare clic su **Test Installation**. Dopo aver confermato l’azione, si apre una finestra in cui sono elencati i risultati come se l’installazione fosse stata eseguita:

   ![packagestestinstall](assets/packagestestinstall.png)

### Download dei pacchetti nel file system {#downloading-packages-to-your-file-system}

Questa sezione descrive come scaricare un pacchetto da AEM al file system utilizzando **Package Manager**.

1. Nella schermata di benvenuto AEM, fate clic su **Packages**, quindi selezionate **Package Manager**.
1. Passate al pacchetto da scaricare.

   ![packagesdownload](assets/packagesdownload.png)

1. Fate clic sul collegamento formato dal nome del file ZIP (sottolineato) per il pacchetto da scaricare; ad esempio `export-for-offline.zip`.

   AEM scarica il pacchetto sul computer (utilizzando una finestra di dialogo di download standard del browser).

### Caricamento di pacchetti dal file system {#uploading-packages-from-your-file-system}

Il caricamento di un pacchetto consente di caricare un pacchetto dal file system in AEM Package Manager.
Per caricare un pacchetto:

1. Andate alla **Gestione pacchetti**. Quindi nella cartella del gruppo in cui desiderate caricare il pacchetto.

   ![packagesuploadbutton](assets/packagesuploadbutton.png)

1. Fate clic su **Carica pacchetto**.

   ![packagesuploaddialog](assets/packagesuploaddialog.png)

   * **File**

      È possibile digitare direttamente il nome del file oppure utilizzare il percorso **Sfoglia...** finestra di dialogo per selezionare il pacchetto richiesto dal file system locale (dopo la selezione fare clic su **OK**).

   * **Forza caricamento**

      Se esiste già un pacchetto con questo nome, potete fare clic su di esso per forzare il caricamento (e sovrascrivere il pacchetto esistente).
   Fate clic su **OK** in modo che il nuovo pacchetto venga caricato ed elencato nell&#39;elenco Gestione pacchetti.

   >[!NOTE]
   >
   >Per rendere il contenuto disponibile a AEM, [installate il pacchetto](#installing-packages).

### Convalida dei pacchetti {#validating-packages}

Prima di installare un pacchetto, potreste desiderare verificarne il contenuto. Poiché i pacchetti possono modificare i file sovrapposti in `/apps` e/o aggiungere, modificare e rimuovere ACL, spesso è utile convalidare queste modifiche prima dell&#39;installazione.

#### Opzioni di convalida {#validation-options}

Il meccanismo di convalida può controllare le seguenti caratteristiche del pacchetto:

* Importazioni pacchetti OSGi
* Sovrapposizioni
* ACL

Queste opzioni sono descritte di seguito.

* **Convalida importazioni di pacchetti OSGi**

   **Elementi controllati**

   Questa convalida esamina il pacchetto per tutti i file JAR (bundle OSGi), ne estrae i `manifest.xml` (che contiene le dipendenze con le versioni su cui si basa il bundle OSGi) e verifica che l&#39;istanza AEM esporta tali dipendenze con le versioni corrette.

   **Come viene segnalato**

   Tutte le dipendenze con versione che non possono essere soddisfatte dall&#39;istanza AEM sono elencate nel **log attività** di Package Manager.

   **Stati di errore**

   Se le dipendenze non sono soddisfatte, i bundle OSGi nel pacchetto con tali dipendenze non verranno avviati. Ciò comporta l’interruzione della distribuzione dell’applicazione in quanto tutto ciò che si basa sul bundle OSGi non avviato non funzionerà a sua volta correttamente.

   **Risoluzione errori**

   Per risolvere gli errori dovuti ai bundle OSGi non soddisfatti, è necessario modificare la versione della dipendenza nel bundle con importazioni non soddisfatte.

* **Convalida sovrapposizioni**

   **Elementi controllati**

   Questa convalida determina se il pacchetto installato contiene un file già sovrapposto nell&#39;istanza AEM di destinazione.

   Ad esempio, data una sovrapposizione esistente in `/apps/sling/servlet/errorhandler/404.jsp`, un pacchetto che contiene `/libs/sling/servlet/errorhandler/404.jsp`, in modo da modificare il file esistente in `/libs/sling/servlet/errorhandler/404.jsp`.

   **Come viene segnalato**

   Tali sovrapposizioni sono descritte nel **Registro attività** di Gestione pacchetti.

   **Stati di errore**

   Uno stato di errore indica che il pacchetto sta tentando di distribuire un file già sovrapposto, pertanto le modifiche nel pacchetto verranno sostituite (e quindi &quot;nascoste&quot;) dalla sovrapposizione e non avranno effetto.

   **Risoluzione errori**

   Per risolvere questo problema, il gestore del file di sovrapposizione in `/apps` deve rivedere le modifiche apportate al file di sovrapposizione in `/libs` e incorporare le modifiche necessarie nella sovrapposizione ( `/apps`), quindi ridistribuire il file di sovrapposizione.

   >[!NOTE]
   >
   >Il meccanismo di convalida non può essere conciliato se il contenuto sovrapposto è stato correttamente incorporato nel file della sovrapposizione. Pertanto, tale convalida continuerà a segnalare i conflitti anche dopo che saranno state apportate le necessarie modifiche.

* **Convalida ACL**

   **Elementi controllati**

   Questa convalida verifica quali autorizzazioni vengono aggiunte, come verranno gestite (unione/sostituzione) e se le autorizzazioni correnti verranno interessate.

   **Come viene segnalato**

   Le autorizzazioni sono descritte in **Activity Log** di Package Manager.

   **Stati di errore**

   Non è possibile fornire errori espliciti. La convalida indica semplicemente se le nuove autorizzazioni ACL verranno aggiunte o influenzate dall&#39;installazione del pacchetto.

   **Risoluzione errori**

   Utilizzando le informazioni fornite dalla convalida, i nodi interessati possono essere revisionati in CRXDE e gli ACL possono essere regolati nel pacchetto in base alle esigenze.

   >[!CAUTION]
   >
   >Come procedura ottimale, si consiglia di evitare che i pacchetti influenzino gli ACL forniti AEM, in quanto ciò potrebbe causare un comportamento inatteso del prodotto.

#### Esecuzione della convalida {#performing-validation}

La convalida dei pacchetti può essere eseguita in due modi diversi:

* Tramite l’interfaccia utente di Gestione pacchetti
* Tramite richiesta POST HTTP, ad esempio con cURL

>[!NOTE]
>
>La convalida deve sempre verificarsi dopo il caricamento del pacchetto ma prima di installarlo.

**Convalida del pacchetto tramite Gestione pacchetti**

1. Apri Gestione pacchetti in `https://<server>:<port>/crx/packmgr`
1. Selezionate il pacchetto nell&#39;elenco, quindi selezionate il menu a discesa **Altro** dall&#39;intestazione e quindi **Convalida** dal menu a discesa.

   >[!NOTE]
   >
   >Questa operazione deve essere eseguita dopo il caricamento del pacchetto di contenuto, ma prima di installare il pacchetto.

1. Nella finestra di dialogo modale visualizzata, utilizzare le caselle di controllo per selezionare i tipi di convalida e iniziare la convalida facendo clic su **Validate**. In alternativa, fare clic su **Annulla**.

1. Le convalida scelte vengono quindi eseguite. I risultati vengono visualizzati nel registro attività di Gestione pacchetti.

**Convalida del pacchetto tramite richiesta POST HTTP**

La richiesta POST è costituita dal seguente modulo.

```
https://<host>:<port>/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls
```

>[!NOTE]
>
>Il parametro `type` può essere un qualsiasi elenco non ordinato separato da virgole composto da:
>
>* `osgiPackageImports`
>* `overlays`
>* `acls`

>
>
Se non viene passato, il valore di `type` viene impostato come predefinito su `osgiPackageImports`.

Di seguito è riportato un esempio di utilizzo di cURL per eseguire la convalida di un pacchetto.

1. Se utilizzate cURL, eseguite un&#39;istruzione simile a quella riportata di seguito:

   ```shell
   curl -v -X POST --user admin:admin -F file=@/Users/SomeGuy/Desktop/core.wcm.components.all-1.1.0.zip 'http://localhost:4502/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls'
   ```

1. La convalida richiesta viene eseguita e la risposta viene restituita come oggetto JSON.

>[!NOTE]
>
>La risposta a una richiesta di POST HTTP di convalida sarà un oggetto JSON con i risultati della convalida.

### Installazione di pacchetti {#installing-packages}

Dopo aver caricato un pacchetto, dovete installare il contenuto. Per avere installato e funzionante il contenuto del pacchetto, è necessario che sia:

* caricato in AEM ([caricato dal file system](#uploading-packages-from-your-file-system) o scaricato da [Distribuzione software](#software-distribution))

* installati

>[!CAUTION]
>
>L&#39;installazione di un pacchetto può sovrascrivere o eliminare il contenuto esistente. Caricate un pacchetto solo se siete certi che non eliminerà o sovrascriverà il contenuto necessario.
>
>Per visualizzare il contenuto o l’impatto di un pacchetto, potete effettuare le seguenti operazioni:
>
>* Eseguite un&#39;installazione di prova del pacchetto senza modificare il contenuto:
   >  Aprite il pacchetto (fate clic sull&#39;icona o sul nome del pacchetto) e fate clic su **Test Install**.
   >
   >
* Consultate un elenco dei contenuti del pacchetto:
   >  Aprite il pacchetto e fate clic su **Contents**.

>



>[!NOTE]
>
>Immediatamente prima dell&#39;installazione del pacchetto, viene creato un pacchetto di snapshot che contiene il contenuto che verrà sovrascritto.
>
>Lo snapshot verrà reinstallato se/quando disinstallate il pacchetto.

>[!CAUTION]
>
>Se state installando delle risorse digitali, dovete:
>
>* Innanzitutto, disattivate WorkflowLauncher.
   >  Utilizzate l&#39;opzione di menu Componenti della console OSGi per disattivare `com.day.cq.workflow.launcher.impl.WorkflowLauncherImpl`.
   >
   >
* Al termine dell&#39;installazione, riattivate WorkflowLauncher.
>
>
La disattivazione di WorkflowLauncher assicura che il framework di Importazione risorse non modifichi (in modo involontario) le risorse al momento dell’installazione.

1. In Gestione pacchetti, andate al pacchetto da installare.

   Un pulsante **Install** viene visualizzato sul lato dei pacchetti che non sono ancora stati installati.

   >[!NOTE]
   >
   >In alternativa, potete aprire il pacchetto facendo clic sulla relativa icona per accedere al pulsante **Install**.

1. Fare clic su **Installa** per avviare l&#39;installazione. Viene visualizzata una finestra di dialogo con richiesta di conferma e con l’elenco di tutte le modifiche in corso. Al termine, fare clic su **Chiudi** nella finestra di dialogo.

   La parola **Installed** viene visualizzata accanto al pacchetto dopo che è stato installato.

### Caricamento e installazione basati su file system {#file-system-based-upload-and-installation}

Esiste un metodo alternativo per caricare e installare i pacchetti nell’istanza. Nel file system è presente una cartella `crx-quicksart` con il file jar e `license.properties`. È necessario creare una cartella denominata `install` in `crx-quickstart`. Avrete quindi qualcosa di simile a questo: `<aem_home>/crx-quickstart/install`

In questa cartella di installazione, potete aggiungere direttamente i pacchetti. Saranno automaticamente caricati e installati nell’istanza. Al termine, potete visualizzare i pacchetti in Gestione pacchetti.

Se l&#39;istanza è in esecuzione, l&#39;aggiunta di un pacchetto alla cartella `install` avvierà direttamente il caricamento e l&#39;installazione nell&#39;istanza. Se l&#39;istanza non è in esecuzione, i pacchetti inseriti nella cartella `install` verranno installati all&#39;avvio in ordine alfabetico.

>[!NOTE]
>
>È inoltre possibile eseguire questa operazione prima ancora di avviare l&#39;istanza per la prima volta. A tal fine, è necessario creare manualmente la cartella `crx-quickstart`, creare la cartella `install` al suo interno e inserire i pacchetti. Al primo avvio dell&#39;istanza, i pacchetti verranno installati in ordine alfabetico.

### Disinstallazione di pacchetti {#uninstalling-packages}

AEM consente di disinstallare i pacchetti. Questa azione consente di ripristinare i contenuti del repository interessati dallo snapshot creato immediatamente prima dell&#39;installazione del pacchetto.

>[!NOTE]
>
>Al momento dell&#39;installazione, viene creato un pacchetto di snapshot contenente il contenuto che verrà sovrascritto.
>
>Il pacchetto verrà reinstallato quando disinstallate il pacchetto.

1. In Gestione pacchetti, andate al pacchetto da disinstallare.
1. Fate clic sull&#39;icona del pacchetto da disinstallare.
1. Fate clic su **Disinstalla** per rimuovere il contenuto del pacchetto dall&#39;archivio. Viene visualizzata una finestra di dialogo con richiesta di conferma e con l’elenco di tutte le modifiche in corso. Al termine, fare clic su **Chiudi** nella finestra di dialogo.

### Eliminazione di pacchetti {#deleting-packages}

Per eliminare un pacchetto dagli elenchi Gestione pacchetti:

>[!NOTE]
>
>I file/nodi installati dal pacchetto sono **non** eliminati.

1. Nella console **Strumenti**, espandete la cartella **Packages** per visualizzare il pacchetto nel riquadro a destra.

1. Fate clic sul pacchetto da eliminare in modo che sia evidenziato e quindi:

   * Fare clic su **Elimina** nel menu della barra degli strumenti.
   * Fare clic con il pulsante destro del mouse e selezionare **Elimina**.

   ![packagesdelete](assets/packagesdelete.png)

1. AEM richiede la conferma dell’eliminazione del pacchetto. Fare clic su **OK** per confermare l&#39;eliminazione.

>[!CAUTION]
>
>Se il pacchetto è già stato installato, il contenuto *installato* **non** verrà eliminato.

### Replica di pacchetti {#replicating-packages}

Replicate il contenuto di un pacchetto per installarlo nell&#39;istanza di pubblicazione:

1. In **Gestione pacchetti**, andate al pacchetto da replicare.

1. Fate clic sull&#39;icona o sul nome del pacchetto da replicare per espanderlo.
1. Nel menu a discesa **Altro** della barra degli strumenti, selezionare **Replica**.

## Condivisione pacchetti {#package-share}

Package Share era un server centralizzato reso disponibile al pubblico per la condivisione di pacchetti di contenuti.

È stato sostituito da [Distribuzione software](#software-distribution).

## Distribuzione software {#software-distribution}

[La ](https://downloads.experiencecloud.adobe.com) distribuzione software è la nuova interfaccia utente progettata per semplificare la ricerca e il download di pacchetti AEM.

Per ulteriori informazioni, consultare la [Documentazione sulla distribuzione del software](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html).

>[!CAUTION]
>
>AEM gestione pacchetti non è utilizzabile con la distribuzione software per il momento, si scarica i pacchetti sul disco locale.

