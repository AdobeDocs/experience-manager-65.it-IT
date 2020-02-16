---
title: Come utilizzare i pacchetti
seo-title: Come utilizzare i pacchetti
description: Scopri le basi dell’utilizzo dei pacchetti in AEM.
seo-description: Scopri le basi dell’utilizzo dei pacchetti in AEM.
uuid: cba76a5f-5d75-4d63-a0f4-44c13fa1baf2
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 6694a135-d1e1-4afb-9f5b-23991ee70eee
docset: aem65
translation-type: tm+mt
source-git-commit: 5e10ddb0e5cf24e1915d0840cd380520374e93ea

---


# How to Work With Packages{#how-to-work-with-packages}

I pacchetti consentono di importare ed esportare il contenuto del repository. Ad esempio, potete utilizzare i pacchetti per installare nuove funzionalità, trasferire contenuti tra le istanze e eseguire il backup del contenuto del repository.

È possibile accedere ai pacchetti e/o mantenerli nelle pagine seguenti:

* [Package Manager](#package-manager), che consente di gestire i pacchetti nell’istanza locale di AEM.

* [Package Share](#package-share), un server centralizzato che contiene sia i pacchetti disponibili pubblicamente che quelli privati per la società. I pacchetti pubblici possono contenere hotfix, nuove funzionalità, documentazione, ecc.

Potete trasferire i pacchetti tra Package Manager, Package Share e il file system.

## Che cosa sono i pacchetti? {#what-are-packages}

Un pacchetto è un file zip che contiene il contenuto del repository sotto forma di serializzazione del file system (chiamata serializzazione &quot;vault&quot;). Questo fornisce una rappresentazione semplice da usare e modificare di file e cartelle.

I pacchetti includono il contenuto, sia contenuto della pagina che contenuto relativo al progetto, selezionato utilizzando i filtri.

Un pacchetto contiene anche metadati di archivio, comprese le definizioni dei filtri e le informazioni sulla configurazione di importazione. Nel pacchetto possono essere incluse ulteriori proprietà di contenuto (non utilizzate per l&#39;estrazione del pacchetto), come una descrizione, un&#39;immagine visiva o un&#39;icona; queste proprietà sono riservate al consumatore del pacchetto di contenuti e sono riservate solo a scopo informativo.

>[!NOTE]
>
>I pacchetti rappresentano la versione corrente del contenuto al momento della creazione del pacchetto. Non includono versioni precedenti del contenuto memorizzato nella directory archivio da AEM.

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
* Scaricare pacchetti, come hotfix, dalla libreria Condivisione pacchetti
* Caricare i pacchetti nella sezione interna della società della libreria Package Share

## Informazioni pacchetto {#package-information}

Una definizione di pacchetto è composta da vari tipi di informazioni:

* [Impostazioni pacchetto](#package-settings)
* [Filtri pacchetto](#package-filters)
* [Schermate pacchetto](#package-screenshots)
* [Icone pacchetto](#package-icons)

### Impostazioni pacchetto {#package-settings}

Potete modificare diverse impostazioni del pacchetto per definire aspetti quali la descrizione del pacchetto, i bug correlati, le dipendenze e le informazioni sul fornitore.

La finestra di dialogo Impostazioni **** pacchetto è disponibile tramite il pulsante **Modifica** al momento della [creazione](#creating-a-new-package) o della [modifica](#viewing-and-editing-package-information) di un pacchetto e fornisce tre schede per la configurazione. Dopo aver apportato le modifiche, fare clic su **OK** per salvarle.

![packagesedit](assets/packagesedit.png)

| **Campo** | **Descrizione** |
|---|---|
| Nome | Nome del pacchetto. |
| Gruppo | Nome del gruppo a cui aggiungere il pacchetto per organizzare i pacchetti. Digitate il nome di un nuovo gruppo o selezionate un gruppo esistente. |
| Versione | Testo da utilizzare per la versione personalizzata. |
| Descrizione | Breve descrizione del pacchetto. È possibile utilizzare i tag HTML per la formattazione. |
| Miniatura | Icona visualizzata con l&#39;elenco dei pacchetti. Fate clic su Sfoglia per selezionare un file locale. |

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
   <td><em>AEM Geometrixx<br /> </em></td>
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
    </ul> <p>The default value is <strong>Ignore</strong>.</p> </td>
   <td>
    <ul>
     <li><strong>Ignora</strong> - Conserva gli ACL nell'archivio</li>
     <li><strong>Sovrascrivi</strong> - sovrascrivi ACL nell'archivio</li>
     <li><strong>Unisci</strong> - unisci entrambi i set di ACL</li>
     <li><strong>Cancella</strong> - cancella ACL</li>
     <li><strong>MergePreserve</strong> : consente di unire il controllo di accesso nel contenuto a quello fornito con il pacchetto aggiungendo le voci di controllo di accesso delle entità non presenti nel contenuto</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

![packagesdipendenze](assets/packagesdependencies.png)

| **Campo** | **Descrizione** | **Formato/Esempio** |
|---|---|---|
| Test con | Il nome e la versione del prodotto a cui è destinato il pacchetto o con cui è compatibile. | *AEM6* |
| Bug/Problemi risolti | Campo di testo che consente di elencare i dettagli dei bug corretti con questo pacchetto. Elenca ciascun bug su una riga separata. | riepilogo bug-nr |
| Dipende da | Elenca le informazioni sulle dipendenze che devono essere rispettate ogni volta che sono necessari altri pacchetti per consentire l&#39;esecuzione del pacchetto corrente come previsto. Questo campo è importante quando si utilizzano gli hotfix. | groupId:name:version |
| Sostituisce | Un elenco di pacchetti obsoleti che il pacchetto sostituisce. Prima di eseguire l&#39;installazione, verificate che il pacchetto includa tutto il contenuto necessario dai pacchetti obsoleti, in modo da non sovrascrivere il contenuto. | groupId:name:version |

### Filtri pacchetto {#package-filters}

I filtri identificano i nodi del repository da includere nel pacchetto. Una definizione **di** filtro specifica le informazioni seguenti:

* Percorso **** principale del contenuto da includere.
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
     <li>includi tale directory <i>e tutti</i> i file e le cartelle presenti in tale directory (ovvero l’intera sottostruttura)</li>
     <li><strong>non</strong> includere altri file o cartelle nel percorso principale specificato</li>
    </ul> </td>
   <td>/libs/sling/install(/.*)? </td>
  </tr>
  <tr>
   <td> escludi</td>
   <td>È possibile specificare un percorso o utilizzare un'espressione regolare per specificare tutti i nodi da escludere.<br /> <br /> Escludendo una directory, tale directory <i>e tutti</i> i file e le cartelle in essa contenuti (ovvero l’intera sottostruttura) verranno esclusi.<br /> </td>
   <td>/libs/wcm/foundation/components(/.*)?</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Un pacchetto può contenere più definizioni di filtro, in modo che i nodi di diverse ubicazioni possano essere facilmente combinati in un unico pacchetto.

I filtri pacchetto vengono definiti più spesso quando [create il pacchetto](#creating-a-new-package)per la prima volta, ma possono essere modificati anche in un secondo momento (dopodiché il pacchetto deve essere rigenerato).

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

Package Manager gestisce i pacchetti nell’installazione locale di AEM. Dopo aver [assegnato le autorizzazioni](#permissions-needed-for-using-the-package-manager) necessarie potete utilizzare Gestione pacchetti per diverse azioni, tra cui la configurazione, la creazione, il download e l&#39;installazione dei pacchetti. Gli elementi chiave da configurare sono:

* [Impostazioni pacchetto](#package-settings)
* [Filtri pacchetto](#package-filters)

### Autorizzazioni necessarie per l&#39;utilizzo di Gestione pacchetti {#permissions-needed-for-using-the-package-manager}

Per concedere agli utenti il diritto di creare, modificare, caricare e installare pacchetti, dovete concedere loro le autorizzazioni appropriate nei seguenti percorsi:

* **/etc/packages** (diritti completi esclusa l’eliminazione)
* il nodo che contiene il contenuto del pacchetto

Consultate [Impostazione delle autorizzazioni](/help/sites-administering/security.md#setting-page-permissions) per le istruzioni sulla modifica delle autorizzazioni.

### Creazione di un nuovo pacchetto {#creating-a-new-package}

Per creare una nuova definizione di pacchetto:

1. Nella schermata introduttiva di AEM, fate clic su **Pacchetti** (oppure, nella console **Strumenti** , fate doppio clic su **Pacchetti**).

1. Selezionate quindi Gestione **** pacchetti.
1. Fate clic su **Crea pacchetto**.

   >[!NOTE]
   >
   >Se l’istanza include molti pacchetti, potrebbe essere presente una struttura di cartelle, per cui potete passare alla cartella di destinazione richiesta prima di creare il nuovo pacchetto.

1. Nella finestra di dialogo:

   ![packagesnew](assets/packagesnew.png)

   Inserire:

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

1. Fate clic su **Modifica** per modificare le impostazioni [del](#package-settings)pacchetto.

   Qui è possibile aggiungere informazioni e/o definire determinate impostazioni; ad esempio, questi includono una descrizione, l&#39; [icona](#package-icons), i bug correlati e aggiungere i dettagli del fornitore.

   Dopo aver modificato le impostazioni, fate clic su **OK** .

1. Aggiungete **[schermate](#package-screenshots)**al pacchetto come necessario. Quando viene creato il pacchetto, è disponibile un&#39;istanza; se necessario, aggiungete altro utilizzando **Package Screenshot**dalla barra laterale.

   Aggiungete l’immagine effettiva facendo doppio clic sul componente immagine nell’area **Screenshots** , aggiungendo un’immagine e facendo clic su **OK**.

1. Per definire i filtri **[](#package-filters)**pacchetto, trascinate le istanze della definizione **del**filtro dalla barra laterale, quindi fate doppio clic per aprire la finestra di modifica:

   ![packagesfilter](assets/packagesfilter.png)

   Specificate:

   * **Percorso** radice Il contenuto da includere nel pacchetto; può essere la radice di un sottoalbero.
   * **Le regole** sono facoltative; per le definizioni di pacchetti semplici, non è necessario specificare regole di inclusione o esclusione.

      Se necessario, potete definire regole [****Includi** o **Escludi](#package-filters)per definire esattamente il contenuto del pacchetto.

      Aggiungete le regole utilizzando il simbolo **+** , in alternativa rimuovete le regole utilizzando il **-** simbolo. Le regole vengono applicate in base al loro ordine, in modo da posizionarle come necessario utilizzando i pulsanti **Su** e **Giù** .
   Fate clic su **OK** per salvare il filtro.

   >[!NOTE]
   >
   >Puoi utilizzare tutte le definizioni di filtro necessarie, ma devi fare attenzione a non creare conflitti. Usate **Anteprima** per confermare il contenuto del pacchetto.

1. Per confermare il contenuto del pacchetto, potete utilizzare **Anteprima**. Questo esegue una prova a secco del processo di compilazione ed elenca tutti gli elementi che verranno aggiunti al pacchetto quando viene effettivamente costruito.
1. Ora potete [creare](#building-a-package) il pacchetto.

   >[!NOTE]
   >
   >Non è obbligatorio costruire il pacchetto a questo punto, può essere fatto in un momento successivo.

### Creazione di un pacchetto {#building-a-package}

Spesso un pacchetto viene creato contemporaneamente alla [creazione della definizione](#creating-a-new-package)del pacchetto, ma potete tornare in un momento successivo per creare o ricreare il pacchetto. Questo può essere utile se il contenuto all’interno della directory archivio è stato modificato.

>[!NOTE]
>
>Prima di creare il pacchetto può essere utile visualizzare in anteprima il contenuto del pacchetto. A questo scopo, fate clic su **Anteprima**.

1. Aprite la definizione del pacchetto da Gestione **** pacchetti (fate clic sull&#39;icona o sul nome del pacchetto).

1. Fate clic su **Genera**. Viene visualizzata una finestra di dialogo con richiesta di conferma per confermare la creazione del pacchetto.

   >[!NOTE]
   >
   >Questo è particolarmente importante quando si sta ricreando un pacchetto in quanto il contenuto del pacchetto verrà sovrascritto.

1. Fai clic su **OK**. AEM crea il pacchetto, elencando tutti i contenuti aggiunti al pacchetto così come lo fa. Quando AEM è completo, viene visualizzata una conferma che il pacchetto è stato creato e (quando si chiude la finestra di dialogo) vengono aggiornate le informazioni dell&#39;elenco dei pacchetti.

### Rewrapping di un pacchetto {#rewrapping-a-package}

Una volta creato, un pacchetto può essere reinserito, se necessario.

Il rewrapping modifica le informazioni sul pacchetto *senza* modificarne il contenuto. Le informazioni sul pacchetto sono la miniatura, la descrizione e così via, ovvero tutto ciò che è possibile modificare con la finestra di dialogo Impostazioni **** pacchetto (per aprire questo clic su **Modifica**).

Un caso di utilizzo principale per il rewrapping è la preparazione di un pacchetto per la condivisione del pacchetto. Ad esempio, potreste avere un pacchetto esistente e decidere di condividerlo con altri. Per aggiungere una miniatura, aggiungere una descrizione. Invece di ricreare l&#39;intero pacchetto con tutte le sue funzionalità (che potrebbero richiedere un po&#39; di tempo e comporta il rischio che il pacchetto non sia più identico all&#39;originale) potete reinserirlo e aggiungere semplicemente la miniatura e la descrizione.

1. Aprite la definizione del pacchetto da Gestione **** pacchetti (fate clic sull&#39;icona o sul nome del pacchetto).

1. Fate clic su **Modifica** e aggiornate le impostazioni **[del](#package-settings)**pacchetto come necessario. Fate clic su **OK**per salvare.

1. Fate clic su **Rewrapper**. Viene visualizzata una finestra di dialogo con richiesta di conferma.

### Visualizzazione e modifica delle informazioni sul pacchetto {#viewing-and-editing-package-information}

Per visualizzare o modificare le informazioni sulla definizione di un pacchetto:

1. In Gestione pacchetti, andate al pacchetto da visualizzare.
1. Fate clic sull&#39;icona del pacchetto da visualizzare. Viene aperta la pagina del pacchetto con le informazioni sulla definizione del pacchetto:

   ![packagesitemclicked-1](assets/packagesitemclicked-1.png)

   >[!NOTE]
   >
   >Potete anche modificare ed eseguire determinate azioni sul pacchetto da questa pagina.
   >
   >I pulsanti disponibili dipendono dal fatto che il pacchetto sia già stato creato o meno.

1. Se il pacchetto è già stato creato, fate clic su **Contenuto**, si aprirà una finestra con l’elenco completo del contenuto del pacchetto:

### Visualizzazione del contenuto del pacchetto e verifica dell’installazione {#viewing-package-contents-and-testing-installation}

Dopo aver creato un pacchetto, potete visualizzare i contenuti:

1. In Gestione pacchetti, andate al pacchetto da visualizzare.
1. Fate clic sull&#39;icona del pacchetto da visualizzare. Viene aperta la pagina del pacchetto con le informazioni sulla definizione del pacchetto.

1. Per visualizzare il contenuto fate clic su **Sommario**, si apre una finestra con l’elenco completo del contenuto del pacchetto:

   ![packgescontents](assets/packgescontents.png)

1. Per eseguire una prova a secco dell&#39;installazione, fate clic su **Test di installazione**. Dopo aver confermato l’azione, si apre una finestra in cui sono elencati i risultati come se l’installazione fosse stata eseguita:

   ![packagestestinstall](assets/packagestestinstall.png)

### Download dei pacchetti nel file system {#downloading-packages-to-your-file-system}

Questa sezione descrive come scaricare un pacchetto da AEM al file system utilizzando **Package Manager**.

>[!NOTE]
>
>Consultate Condivisione [](#package-share) pacchetti per informazioni sul download di hotfix, pacchetti di funzionalità e pacchetti dall&#39;area pubblica e dall&#39;area interna della condivisione di pacchetti della vostra azienda.
>
>Da Condivisione pacchetti potete:
>
>* scarica i pacchetti da [Package Share direttamente nella tua istanza](#downloading-and-installing-packages-from-package-share)AEM locale.
   >  Al momento del download, il pacchetto viene importato nella directory archivio, dopodiché potete installarlo immediatamente nell&#39;istanza locale tramite **Gestione** pacchetti. Questi pacchetti includono hotfix e altri pacchetti condivisi.
   >
   >
* scaricare pacchetti da [Package Share nel file system](#downloading-packages-to-your-file-system-from-package-share).
>



1. Nella schermata introduttiva di AEM, fate clic su **Pacchetti**, quindi selezionate Gestione **** pacchetti.
1. Passate al pacchetto da scaricare.

   ![packagesdownload](assets/packagesdownload.png)

1. Fate clic sul collegamento formato dal nome del file ZIP (sottolineato) per il pacchetto da scaricare; ad esempio `export-for-offline.zip`.

   AEM scarica il pacchetto nel computer (utilizzando una finestra di dialogo di download standard del browser).

### Caricamento di pacchetti dal file system {#uploading-packages-from-your-file-system}

Il caricamento di un pacchetto consente di caricare un pacchetto dal file system in AEM Package Manager.

>[!NOTE]
>
>Consultate [Caricamento di pacchetti nella condivisione](#uploading-packages-to-the-company-internal-package-share) di pacchetti interna della società per caricare un pacchetto nell’area privata della società di Package Share.

Per caricare un pacchetto:

1. Passate a Gestione **pacchetti**. Quindi nella cartella del gruppo in cui desiderate caricare il pacchetto.

   ![packagesuploadbutton](assets/packagesuploadbutton.png)

1. Fate clic su **Carica pacchetto**.

   ![packagesuploaddialog](assets/packagesuploaddialog.png)

   * **File**

      **È possibile digitare direttamente il nome del file oppure utilizzare** Sfoglia. per selezionare il pacchetto desiderato dal file system locale (dopo aver selezionato, fare clic su **OK**).

   * **Forza caricamento**

      Se esiste già un pacchetto con questo nome, potete fare clic su di esso per forzare il caricamento (e sovrascrivere il pacchetto esistente).
   Fate clic su **OK** in modo che il nuovo pacchetto venga caricato ed elencato nell&#39;elenco Gestione pacchetti.

   >[!NOTE]
   >
   >Per rendere il contenuto disponibile ad AEM, accertatevi di [installare il pacchetto](#installing-packages).

### Convalida dei pacchetti {#validating-packages}

Prima di installare un pacchetto, potreste desiderare verificarne il contenuto. Poiché i pacchetti possono modificare i file sovrapposti in `/apps` e/o aggiungere, modificare e rimuovere ACL, è spesso utile convalidare queste modifiche prima dell&#39;installazione.

#### Opzioni di convalida {#validation-options}

Il meccanismo di convalida può controllare le seguenti caratteristiche del pacchetto:

* Importazioni pacchetti OSGi
* Sovrapposizioni
* ACL

Queste opzioni sono descritte di seguito.

* **Convalida importazioni di pacchetti OSGi**

   **Elementi controllati**

   Questa convalida esamina il pacchetto per tutti i file JAR (bundle OSGi), ne estrae `manifest.xml` (che contiene le dipendenze con le versioni da cui dipende il bundle OSGi) e verifica che l’istanza AEM esporti tali dipendenze con le versioni corrette.

   **Come viene segnalato**

   Tutte le dipendenze con versione che non possono essere soddisfatte dall&#39;istanza AEM sono elencate nel registro **** attività di Gestione pacchetti.

   **Stati di errore**

   Se le dipendenze non sono soddisfatte, i bundle OSGi nel pacchetto con tali dipendenze non verranno avviati. Ciò comporta l’interruzione della distribuzione dell’applicazione in quanto tutto ciò che si basa sul bundle OSGi non avviato non funzionerà a sua volta correttamente.

   **Risoluzione errori**

   Per risolvere gli errori dovuti ai bundle OSGi non soddisfatti, è necessario modificare la versione della dipendenza nel bundle con importazioni non soddisfatte.

* **Convalida sovrapposizioni**

   **Elementi controllati**

   Questa convalida determina se il pacchetto installato contiene un file già sovrapposto nell’istanza AEM di destinazione.

   Ad esempio, a partire da una sovrapposizione esistente in `/apps/sling/servlet/errorhandler/404.jsp`, un pacchetto che contiene `/libs/sling/servlet/errorhandler/404.jsp`, in modo da modificare il file esistente in `/libs/sling/servlet/errorhandler/404.jsp`.

   **Come viene segnalato**

   Tali sovrapposizioni sono descritte nel registro **delle** attività di Gestione pacchetti.

   **Stati di errore**

   Uno stato di errore indica che il pacchetto sta tentando di distribuire un file già sovrapposto, pertanto le modifiche nel pacchetto verranno sostituite (e quindi &quot;nascoste&quot;) dalla sovrapposizione e non avranno effetto.

   **Risoluzione errori**

   Per risolvere questo problema, il gestore del file della sovrapposizione in `/apps` deve rivedere le modifiche apportate al file della sovrapposizione in `/libs` e incorporare le modifiche necessarie nella sovrapposizione ( `/apps`), quindi ridistribuire il file della sovrapposizione.

   >[!NOTE]
   >
   >Il meccanismo di convalida non può essere conciliato se il contenuto sovrapposto è stato correttamente incorporato nel file della sovrapposizione. Pertanto, tale convalida continuerà a segnalare i conflitti anche dopo che saranno state apportate le modifiche necessarie.

* **Convalida ACL**

   **Elementi controllati**

   Questa convalida verifica quali autorizzazioni vengono aggiunte, come verranno gestite (unione/sostituzione) e se le autorizzazioni correnti verranno interessate.

   **Come viene segnalato**

   Le autorizzazioni sono descritte nel registro **delle** attività di Package Manager.

   **Stati di errore**

   Non è possibile fornire errori espliciti. La convalida indica semplicemente se le nuove autorizzazioni ACL verranno aggiunte o influenzate installando il pacchetto.

   **Risoluzione errori**

   Utilizzando le informazioni fornite dalla convalida, i nodi interessati possono essere revisionati in CRXDE e gli ACL possono essere regolati nel pacchetto in base alle esigenze.

   >[!CAUTION]
   >
   >Come procedura ottimale, si consiglia di evitare che i pacchetti influenzino gli ACL forniti da AEM, in quanto ciò potrebbe causare un comportamento imprevisto del prodotto.

#### Esecuzione della convalida {#performing-validation}

La convalida dei pacchetti può essere eseguita in due modi diversi:

* Tramite l’interfaccia utente di Gestione pacchetti
* Tramite richiesta HTTP POST, ad esempio con cURL

>[!NOTE]
>
>La convalida deve sempre verificarsi dopo il caricamento del pacchetto ma prima di installarlo.

**Convalida del pacchetto tramite Gestione pacchetti**

1. Apri Gestione pacchetti in `https://<server>:<port>/crx/packmgr`
1. Selezionate il pacchetto nell’elenco, quindi selezionate **Altro** dall’intestazione e **Convalida** dal menu a discesa.

   >[!NOTE]
   >
   >Questa operazione deve essere eseguita dopo il caricamento del pacchetto di contenuto, ma prima di installare il pacchetto.

1. Nella finestra di dialogo modale visualizzata, utilizzare le caselle di controllo per selezionare i tipi di convalida e iniziare la convalida facendo clic su **Convalida**. In alternativa, fate clic su **Annulla**.

1. Le convalida scelte vengono quindi eseguite. I risultati vengono visualizzati nel registro attività di Gestione pacchetti.

**Convalida del pacchetto tramite richiesta HTTP POST**

La richiesta POST ha la seguente forma.

```
https://<host>:<port>/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls
```

>[!NOTE]
>
>Il `type` parametro può essere un qualsiasi elenco non ordinato separato da virgole composto da:
>
>* `osgiPackageImports`
>* `overlays`
>* `acls`
>
>
Il valore di `type` default è impostato su `osgiPackageImports` se non viene passato.

Di seguito è riportato un esempio di utilizzo di cURL per eseguire la convalida di un pacchetto.

1. Se utilizzate cURL, eseguite un&#39;istruzione simile a quella riportata di seguito:

   ```shell
   curl -v -X POST --user admin:admin -F file=@/Users/SomeGuy/Desktop/core.wcm.components.all-1.1.0.zip 'http://localhost:4502/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls'
   ```

1. La convalida richiesta viene eseguita e la risposta viene restituita come oggetto JSON.

>[!NOTE]
>
>La risposta a una richiesta HTTP POST di convalida sarà un oggetto JSON con i risultati della convalida.

### Installazione dei pacchetti {#installing-packages}

Dopo aver caricato un pacchetto, dovete installare il contenuto. Per avere installato e funzionante il contenuto del pacchetto, è necessario che sia:

* caricato in AEM ( [caricato dal file system](#uploading-packages-from-your-file-system) o [scaricato dalla condivisione](#downloading-and-installing-packages-from-package-share)del pacchetto)

* installati

>[!CAUTION]
>
>L&#39;installazione di un pacchetto può sovrascrivere o eliminare il contenuto esistente. Caricate un pacchetto solo se siete certi che non eliminerà o sovrascriverà il contenuto necessario.
>
>Per visualizzare il contenuto o l’impatto di un pacchetto, potete:
>
>* Eseguite un&#39;installazione di prova del pacchetto senza modificare il contenuto:
   >  Aprite il pacchetto (fate clic sull&#39;icona o sul nome del pacchetto) e fate clic su **Test Install**(Prova installazione).
   >
   >
* Consultate un elenco dei contenuti del pacchetto:
   >  Aprite il pacchetto e fate clic su **Contenuto**.
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
   >  Per disattivare, utilizzate l’opzione di menu Componenti della console OSGi `com.day.cq.workflow.launcher.impl.WorkflowLauncherImpl`.
   >
   >
* Al termine dell&#39;installazione, riattivate WorkflowLauncher.
>
>
La disattivazione di WorkflowLauncher assicura che il framework di Importazione risorse non modifichi (in modo involontario) le risorse al momento dell’installazione.

1. In Gestione pacchetti, andate al pacchetto da installare.

   Sul lato dei pacchetti che non sono ancora stati installati viene visualizzato il pulsante **Installa** .

   >[!NOTE]
   >
   >In alternativa, potete aprire il pacchetto facendo clic sulla relativa icona per accedere al pulsante **Installa** .

1. Fate clic su **Installa** per avviare l&#39;installazione. Viene visualizzata una finestra di dialogo con richiesta di conferma ed elenco di tutte le modifiche in corso. Al termine, fate clic su **Chiudi** nella finestra di dialogo.

   La parola **Installato** viene visualizzata accanto al pacchetto dopo che è stato installato.

### Caricamento e installazione basati su file system {#file-system-based-upload-and-installation}

Esiste un metodo alternativo per caricare e installare i pacchetti nell’istanza. Nel file system è presente una `crx-quicksart` cartella accanto al file jar e al `license.properties` file. È necessario creare una cartella denominata `install` in `crx-quickstart`. Avrete quindi qualcosa di simile a questo: `<aem_home>/crx-quickstart/install`

In questa cartella di installazione, potete aggiungere direttamente i pacchetti. Saranno automaticamente caricati e installati nell’istanza. Al termine, potete visualizzare i pacchetti in Gestione pacchetti.

Se l’istanza è in esecuzione, l’aggiunta di un pacchetto alla `install` cartella avvia direttamente il caricamento e l’installazione nell’istanza. Se l&#39;istanza non è in esecuzione, i pacchetti inseriti nella `install` cartella verranno installati all&#39;avvio in ordine alfabetico.

>[!NOTE]
>
>È inoltre possibile eseguire questa operazione prima ancora di avviare l&#39;istanza per la prima volta. A tal fine, è necessario creare la `crx-quickstart` cartella manualmente, creare la `install` cartella al suo interno e inserire i pacchetti. Al primo avvio dell&#39;istanza, i pacchetti verranno installati in ordine alfabetico.

### Disinstallazione dei pacchetti {#uninstalling-packages}

AEM consente di disinstallare i pacchetti. Questa azione consente di ripristinare i contenuti del repository interessati dallo snapshot creato immediatamente prima dell&#39;installazione del pacchetto.

>[!NOTE]
>
>Al momento dell&#39;installazione, viene creato un pacchetto di snapshot contenente il contenuto che verrà sovrascritto.
>
>Il pacchetto verrà reinstallato quando disinstallate il pacchetto.

1. In Gestione pacchetti, andate al pacchetto da disinstallare.
1. Fate clic sull&#39;icona del pacchetto da disinstallare.
1. Fate clic su **Disinstalla** per rimuovere il contenuto del pacchetto dall&#39;archivio. Viene visualizzata una finestra di dialogo con richiesta di conferma ed elenco di tutte le modifiche in corso. Al termine, fate clic su **Chiudi** nella finestra di dialogo.

### Eliminazione di pacchetti {#deleting-packages}

Per eliminare un pacchetto dagli elenchi Gestione pacchetti:

>[!NOTE]
>
>I file/nodi installati dal pacchetto **non** vengono eliminati.

1. Nella console **Strumenti** , espandete la cartella **Packages** per mostrare il pacchetto nel riquadro a destra.

1. Fate clic sul pacchetto da eliminare in modo che sia evidenziato e quindi:

   * Fare clic su **Elimina** nel menu della barra degli strumenti.
   * Fare clic con il pulsante destro del mouse e selezionare **Elimina**.
   ![packagesdelete](assets/packagesdelete.png)

1. AEM richiede la conferma dell’eliminazione del pacchetto. Click **OK** to confirm the deletion.

>[!CAUTION]
>
>Se il pacchetto è già stato installato, il contenuto *installato* **non** verrà eliminato.

### Replica dei pacchetti {#replicating-packages}

Replicate il contenuto di un pacchetto per installarlo nell&#39;istanza di pubblicazione:

1. In Gestione **** pacchetti, andate al pacchetto da replicare.

1. Fate clic sull&#39;icona o sul nome del pacchetto da replicare per espanderlo.
1. Nel menu a discesa **Altro** della barra degli strumenti, selezionate **Replica**.

## Condivisione pacchetti {#package-share}

Package Share è un server centralizzato reso disponibile al pubblico per la condivisione di pacchetti di contenuti.

Con Package Share potete scaricare questi pacchetti, che possono includere hotfix ufficiali, set di funzioni, aggiornamenti o contenuti di esempio generati da altri utenti.

Potete anche caricare e condividere i pacchetti all’interno della società.

### Accesso a Package Share {#access-to-package-share}

Non esiste un accesso anonimo a Package Share; in altre parole, solo gli utenti registrati possono visualizzare, scaricare e caricare i pacchetti.

L&#39;accesso a Package Share è disponibile per i nostri partner e clienti. Per poter assegnare i diritti di accesso, è necessario presentare i dettagli di registrazione.

Per accedere a Package Share:

* Utilizzare la pagina [Accedi](#signing-in-to-package-share)
* La prima volta che utilizzate la pagina di accesso dovrete:

   * [Registrati per ottenere un ID](#registering-for-package-share) Adobe e/o per [convalidare l’ID Adobe esistente](#validating-your-adobe-id)
   * in modo che sia possibile creare l&#39;account [di](#package-share-account) Package Share

>[!NOTE]
>
>Gli utenti di Package Share che non sono stati assegnati a un cliente devono unirsi a una community per visualizzare tali risorse facendo clic su **Partecipa** accanto all&#39;accesso alla condivisione del pacchetto.

#### Accesso a Package Share {#signing-in-to-package-share}

1. Nella schermata introduttiva di AEM, fate clic su **Strumenti**.
1. Quindi selezionate **Condivisione** pacchetti. Sarà necessario:

   * accedere con il tuo Adobe ID
   * [Creare un Adobe ID](#registering-for-package-share)
   >[!NOTE]
   >
   >La prima volta che accedete con il vostro Adobe ID, dovete completare la [convalida del vostro indirizzo](#validating-your-adobe-id)e-mail.

   >[!NOTE]
   >
   >Se avete dimenticato la password, utilizzate il collegamento delle pagine [della](https://enterprise-dev.adobe.com/content/edev/en/registration/account.html) Guida (anche nella finestra di dialogo di accesso).

#### Convalida dell’Adobe ID {#validating-your-adobe-id}

La prima volta che accedete a Package Share con il vostro Adobe ID, l&#39;indirizzo e-mail verrà convalidato.

1. Riceverai un messaggio e-mail contenente un collegamento.
1. Fai clic su questo collegamento.
1. Viene aperta una pagina Web.

   L&#39;apertura di questa pagina Web viene eseguita come convalida.

1. L&#39;accesso continuerà.

1. Riceverai un messaggio e-mail contenente un collegamento.
1. Fai clic su questo collegamento.
1. Viene aperta una pagina Web. L&#39;apertura di questa pagina Web viene eseguita come convalida.
1. L&#39;accesso continuerà.

#### Registrazione per Package Share {#registering-for-package-share}

Se avete bisogno di accedere a Package Share, dovrete registrarvi per un Adobe ID:

* La pagina [di accesso di](#signing-in-to-package-share) Package Share offre un collegamento per la registrazione di un ID Adobe.
* È possibile registrarsi per un Adobe ID da determinati software desktop Adobe.
* In alternativa, potete effettuare la registrazione online nella pagina [di accesso di](https://www.adobe.com/cfusion/membership/index.cfm?nf=1&nl=1)Adobe.

Un ID Adobe può essere creato fornendo:

* il tuo indirizzo e-mail
* una password a scelta
* alcune informazioni aggiuntive come il vostro nome e il paese di residenza

#### Account di condivisione del pacchetto {#package-share-account}

La validità della domanda verrà verificata prima di:

* L&#39;account utente viene creato con le autorizzazioni richieste/consentite.
* Il vostro account viene aggiunto al gruppo della società.

>[!NOTE]
>
>Un utente di una delle nostre società partner può anche essere membro del suo gruppo di clienti.

#### Considerazioni sulla rete {#network-considerations}

**IPv6**

Potrebbero verificarsi problemi durante il tentativo di accesso a Package Share da un ambiente IPv6 puro.

Questo perché la condivisione del pacchetto è un servizio ospitato su un server, il che significa che la connessione viene effettuata attraverso diverse reti su Internet. Non si può garantire che tutte le reti di collegamento supportino l&#39;IPv6; in caso contrario, la connessione potrebbe non riuscire.

Per evitare questo problema, potete accedere a Package Share da una rete IPv4, scaricare il pacchetto e quindi caricarlo nell&#39;ambiente IPv6.

**Proxy HTTP**

Package Share non è al momento disponibile se la società esegue un proxy http che richiede l&#39;autenticazione.

Package Share è disponibile solo quando il server AEM ha accesso a Internet senza che sia necessaria l&#39;autenticazione. Per configurare il proxy per tutti i servizi che utilizzano il client http (inclusa la condivisione del pacchetto), utilizzate la configurazione [OSGi del bundle](/help/sites-deploying/osgi-configuration-settings.md)Day Commons HTTP Client 3.1.

### Condivisione pacchetti interni {#inside-package-share}

I pacchetti di Package Share sono disposti in sottostrutture ad albero:

* Pacchetti Adobe forniti da Adobe.
* Pacchetti condivisi forniti da altre aziende e resi pubblici da Adobe.
* I pacchetti aziendali privati.

![chlimage_1-110](assets/chlimage_1-110.png)

### Ricerca e filtro dei pacchetti {#searching-and-filtering-packages}

Condivisione pacchetti offre una barra di ricerca che consente di cercare parole chiave o tag specifici. Sia le parole chiave che i tag supportano più valori.

* Per cercare più parole chiave è necessario separare ciascuna parola chiave da uno spazio.
* Per cercare più tag, dovete selezionarli ciascuno nelle strutture del pacchetto.

Potete anche modificare l&#39;operatore condizionale da OR a AND sul lato destro della barra di riepilogo del filtro.

### Download E Installazione Di Pacchetti Da Package Share {#downloading-and-installing-packages-from-package-share}

Per scaricare pacchetti da Package Share e installarli nell&#39;istanza locale, è più semplice accedere a Package Share dalla propria istanza di AEM. Il pacchetto verrà scaricato e registrato immediatamente in Package Manager, da dove può essere installato.

1. Nella schermata introduttiva di AEM, fate clic su **Strumenti**, quindi selezionate Condivisione **** pacchetti per aprire la pagina Condivisione pacchetti.
1. Utilizzando i dettagli dell&#39;account, accedete a Package Share. Viene visualizzata la pagina di destinazione in cui sono elencati la cartella Adobe, la cartella condivisa e uno specifico per la società.

   >[!NOTE]
   >
   >Prima di iniziare a scaricare i pacchetti da Package Share, accertatevi di disporre dell&#39;accesso [](#access-to-package-share)richiesto.

1. Individuate il pacchetto da scaricare e fate clic su **Scarica**.

1. Torna all’istanza di AEM o passa a Gestione **** pacchetti. Individuate il pacchetto appena scaricato.

   >[!NOTE]
   >
   >Per trovare il pacchetto scaricato, seguite lo stesso percorso di Package Share. Ad esempio, se avete scaricato un pacchetto dal seguente percorso in Package Share:
   >
   >**Pacchetti** > **Pubblico** > **Hotfix**
   Quindi in Gestione pacchetti nell’istanza locale il pacchetto verrà visualizzato anche in:
   **Pacchetti** > **Pubblico** > **Hotfix**

1. Fate clic su **Installa** per installare il pacchetto nell&#39;installazione locale di AEM.

   >[!NOTE]
   Se il pacchetto è già stato installato nell&#39;istanza, l&#39;indicatore **Installato** viene visualizzato accanto al pacchetto invece del pulsante **Installa** .

   >[!CAUTION]
   L&#39;installazione di un pacchetto può sovrascrivere il contenuto esistente nella directory archivio. Pertanto, è consigliabile eseguire prima un&#39;installazione **di** prova. Questo consente di verificare se il contenuto del pacchetto contiene conflitti con il contenuto esistente.

### Download dei pacchetti nel file system da Package Share {#downloading-packages-to-your-file-system-from-package-share}

[Il download e l&#39;installazione](#downloading-and-installing-packages-from-package-share) è molto conveniente, ma se necessario è anche possibile scaricare il pacchetto e salvarlo nel file system locale:

1. In Package Share fate clic sull&#39;icona o sul nome del pacchetto.
1. Click the **Assets** tab.
1. Fate clic su **Scarica su disco**.

### Caricamento di un pacchetto {#uploading-a-package}

Con Package Share (Condivisione pacchetti), potete caricare i pacchetti nell’area interna della società di condivisione dei pacchetti. Questo li rende disponibili per la condivisione all’interno della società.

Questi pacchetti *non* sono disponibili per la community AEM generale, ma sono disponibili per tutti gli utenti registrati nella società.

Per caricare i pacchetti per la condivisione di pacchetti interna della società:

>[!CAUTION]
Per caricare un pacchetto in Package Share, dovete innanzitutto creare una cartella di gruppo con il nome della società in Package Manager locale. Ad esempio, geometrixx. Tutti i pacchetti da caricare per la condivisione devono trovarsi in questa cartella di gruppo.
Non è possibile condividere i pacchetti nell&#39;elenco principale di Gestione pacchetti o in altre cartelle.

1. Aprite Gestione **** pacchetti e passate al pacchetto da caricare.

1. Fate clic sull&#39;icona del pacchetto per aprirlo.
1. Fate clic su **Condividi** per aprire la finestra di dialogo per il caricamento del pacchetto in Package Share (Condivisione pacchetto).
1. Se non avete già eseguito l&#39;accesso a Package Share, dovrete immettere le credenziali di accesso.

   Una volta effettuato l’accesso, in AEM verranno visualizzati i dettagli sul pacchetto da caricare:

   ![chlimage_1-111](assets/chlimage_1-111.png)

1. Fate clic su **Condividi** per caricare il pacchetto nella condivisione pacchetti interna della società.

   AEM visualizza lo stato e indica quando il pacchetto ha completato il caricamento. Dopo di che potete fare clic sulla **x** (angolo in alto a destra) per uscire dalla finestra Pacchetto **** condivisione.

1. Al termine del caricamento, potete spostarvi nella cartella interna della società per visualizzare il pacchetto appena condiviso.

>[!NOTE]
Per modificare un pacchetto disponibile in Package Share, dovete scaricarlo, ricrearlo e caricarlo nuovamente in Package Share.

### Eliminazione Di Un Pacchetto {#deleting-a-package}

Potete eliminare solo i pacchetti che avete caricato procedendo come segue:

1. Nella struttura della società, controllate il gruppo di pacchetti contenente il pacchetto.
1. Fate clic sul pacchetto.
1. Fate clic sul pulsante Elimina.

   ![chlimage_1-18](do-not-localize/chlimage_1-30.png)

1. Fate clic su **Elimina** per confermare l&#39;eliminazione del pacchetto.

### Creazione di pacchetti semi-privati {#making-packages-semi-private}

Potete condividere i pacchetti all&#39;esterno dell&#39;organizzazione, ma non pubblicamente. Questi pacchetti sarebbero considerati semi-privati. Per condividere questi pacchetti semi-privati, sarà necessario ricevere aiuto dal supporto Adobe. A questo scopo, aprite un ticket con il supporto Adobe per richiedere che il pacchetto sia disponibile all’esterno dell’organizzazione. Vi chiederà un elenco degli Adobe ID che desiderate concedere per l&#39;accesso ai pacchetti.

## Distribuzione software (Beta) {#software-distribution-beta}

[Distribuzione](https://downloads.experiencecloud.adobe.com) software è la nuova interfaccia utente progettata per semplificare la ricerca e il download di pacchetti AEM. Al momento si trova in stato beta e può essere accessibile solo ai clienti Adobe Managed Services e AEM come servizi cloud, nonché ai dipendenti Adobe.

>[!NOTE]
* [Package Share](#package-share) resterà attivo finché tutti i clienti non avranno accesso alla distribuzione del software.
* Tutti i pacchetti sono disponibili sia da Package Share che da Software Distribution.


>[!CAUTION]
Il gestore pacchetti AEM non è utilizzabile con la distribuzione software per il momento. I pacchetti vengono scaricati sul disco locale.

