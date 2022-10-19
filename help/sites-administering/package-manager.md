---
title: Gestione pacchetti
description: Scopri le basi della gestione dei pacchetti AEM con Gestione pacchetti.
feature: Administering
role: Admin
uuid: cba76a5f-5d75-4d63-a0f4-44c13fa1baf2
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 6694a135-d1e1-4afb-9f5b-23991ee70eee
docset: aem65
exl-id: e8929d7c-9920-4c02-95a9-6f7f7a365203
source-git-commit: d303a374fd4ab8e398fd909dec4ce6155a2163f5
workflow-type: tm+mt
source-wordcount: '3573'
ht-degree: 1%

---


# Gestione pacchetti {#working-with-packages}

I pacchetti consentono l&#39;importazione e l&#39;esportazione del contenuto del repository. Puoi utilizzare i pacchetti per installare nuovi contenuti, installare nuove funzionalità, trasferire contenuti tra le istanze e eseguire il backup del contenuto dell’archivio.

Utilizzando Gestione pacchetti, puoi trasferire i pacchetti tra l’istanza AEM e il file system locale a scopo di sviluppo.

## Cosa sono i pacchetti? {#what-are-packages}

Un pacchetto è un file zip che contiene il contenuto dell’archivio sotto forma di serializzazione del file system, chiamato serializzazione vault, che fornisce una rappresentazione semplice da usare e facile da modificare di file e cartelle. Il contenuto incluso nel pacchetto è definito utilizzando i filtri.

Un pacchetto contiene anche metadati vault, incluse le definizioni del filtro e le informazioni di configurazione dell&#39;importazione. Nel pacchetto possono essere incluse ulteriori proprietà di contenuto, che non vengono utilizzate per l’estrazione del pacchetto, ad esempio una descrizione, un’immagine visiva o un’icona. Queste proprietà aggiuntive di contenuto sono per il consumatore del pacchetto di contenuti e solo a scopo informativo.

>[!NOTE]
>
>I pacchetti rappresentano la versione corrente del contenuto al momento della creazione del pacchetto. Non includono versioni precedenti del contenuto AEM conservato nell’archivio.

## Gestione pacchetti {#package-manager}

Gestione pacchetti gestisce i pacchetti nell’installazione AEM. Dopo aver [assegnate le autorizzazioni necessarie](#permissions-needed-for-using-the-package-manager) puoi utilizzare Gestione pacchetti per diverse azioni, tra cui configurazione, creazione, download e installazione dei pacchetti.

### Autorizzazioni necessarie {#required-permissions}

Per creare, modificare, caricare e installare pacchetti, gli utenti devono disporre delle autorizzazioni appropriate per i seguenti nodi:

* Diritti completi, esclusa la cancellazione `/etc/packages`
* Il nodo che contiene il contenuto del pacchetto

>[!CAUTION]
>
>La concessione di autorizzazioni per i pacchetti può portare alla divulgazione di informazioni sensibili e alla perdita di dati.
>
>Per limitare questi rischi, si consiglia vivamente di concedere autorizzazioni specifiche di gruppo solo sui sottoalberi dedicati.

### Accesso a Gestione pacchetti {#accessing}

Puoi accedere a Gestione pacchetti in tre modi:

1. Dal menu principale AEM -> **Strumenti** -> **Distribuzione** -> **Pacchetti**
1. Da [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) utilizzo della barra del commutatore superiore
1. Direttamente tramite l&#39;accesso `http://<host>:<port>/crx/packmgr/`

### Interfaccia utente di Gestione pacchetti {#ui}

Package Manager è suddiviso in quattro aree funzionali principali:

* **Pannello di navigazione a sinistra** - Questo pannello ti consente di filtrare e ordinare l’elenco dei pacchetti.
* **Elenco pacchetti** - Elenco dei pacchetti nell&#39;istanza filtrati e ordinati in base alle selezioni nel pannello di navigazione a sinistra.
* **Registro attività** - Questo pannello viene inizialmente ridotto a icona ed espande per descrivere in dettaglio l’attività di Gestione pacchetti, ad esempio quando viene generato o installato un pacchetto. Nella scheda Registro attività sono disponibili pulsanti aggiuntivi per:
   * **Cancella log**
   * **Mostra/Nascondi**
* **Barra degli strumenti** - La barra degli strumenti contiene i pulsanti di aggiornamento per il pannello di navigazione a sinistra e l’elenco dei pacchetti, nonché i pulsanti per la ricerca, la creazione e il caricamento dei pacchetti.

![Interfaccia utente di Gestione pacchetti](assets/package-manager-ui.png)

Facendo clic su un’opzione nel pannello di navigazione a sinistra, l’elenco dei pacchetti viene filtrato immediatamente.

Facendo clic sul nome di un pacchetto, si espande la voce nell’elenco dei pacchetti per visualizzare ulteriori dettagli sul pacchetto.

![Dettagli del pacchetto espanso](assets/package-expand.png)

È possibile eseguire numerose azioni su un pacchetto tramite i pulsanti della barra degli strumenti disponibili quando i dettagli del pacchetto vengono espansi.

* [Modifica](#edit-package)
* [Genera](#building-a-package)
* [Reinstalla](#reinstalling-packages)
* [Scarica](#downloading-packages-to-your-file-system)
* [Condividi](#share)

Ulteriori azioni sono disponibili sotto **Altro** pulsante .

* [Elimina](#deleting-packages)
* [Copertura](#package-coverage)
* [Contenuti](#viewing-package-contents-and-testing-installation)
* [Ripeti adattamento](#rewrapping-a-package)
* [Altre versioni](#other-versions)
* [Disinstalla](#uninstalling-packages)
* [Installazione di test](#viewing-package-contents-and-testing-installation)
* [Convalida](#validating-packages)
* [Replica](#replicating-packages)

### Stato del pacchetto {#package-status}

Ogni voce nell&#39;elenco dei pacchetti dispone di un indicatore di stato che ti consente di conoscere immediatamente lo stato del pacchetto. Passando il mouse sullo stato viene visualizzata una descrizione comandi con i dettagli dello stato.

![Stato del pacchetto](assets/package-status.png)

Se il pacchetto è stato modificato o non è mai stato generato, lo stato viene presentato come collegamento per intraprendere un&#39;azione rapida per ricostruire o installare il pacchetto.

## Impostazioni pacchetto {#package-settings}

Un pacchetto è essenzialmente un set di filtri e di dati dell’archivio basati su tali filtri. Utilizzando l’interfaccia utente di Gestione pacchetti, puoi fare clic su un pacchetto e quindi sul pulsante **Modifica** per visualizzare i dettagli di un pacchetto, incluse le seguenti impostazioni.

* [Impostazioni generali](#general-settings)
* [Filtri del pacchetto](#package-filters)
* [Dipendenze dei pacchetti](#package-dependencies)
* [Impostazioni avanzate](#advanced-settings)
* [Schermate del pacchetto](#package-screenshots)

### Impostazioni generali {#general-settings}

Puoi modificare diverse impostazioni del pacchetto per definire informazioni quali la descrizione del pacchetto, le dipendenze e i dettagli del provider.

La **Impostazioni pacchetto** la finestra di dialogo è disponibile tramite **Modifica** quando [creazione](#creating-a-new-package) o [modifica](#viewing-and-editing-package-information) un pacchetto. Dopo aver apportato le modifiche, fai clic su **Salva**.

![Finestra di dialogo Modifica pacchetto, impostazioni generali](assets/general-settings.png)

| Campo | Descrizione |
|---|---|
| Nome | Nome del pacchetto |
| Gruppo | Per organizzare i pacchetti, è possibile digitare il nome di un nuovo gruppo o selezionare un gruppo esistente |
| Versione | Testo da utilizzare per la versione |
| Descrizione | Breve descrizione del pacchetto che consente il markup HTML per la formattazione |
| Miniatura  | Icona visualizzata con l’elenco dei pacchetti |

#### Miniature pacchetto {#thumbnails}

Una miniatura fornisce una rappresentazione visiva di riferimento rapido di ciò che contiene il pacchetto. Questo viene quindi mostrato nell&#39;elenco dei pacchetti e può aiutare a identificare facilmente il pacchetto, o la classe del pacchetto.

Di seguito sono riportati alcuni esempi di convenzioni utilizzate per i colli ufficiali:

Hotfix ufficiale

![Miniatura dell&#39;hotfix ufficiale](assets/official-hotfix.png)

AEM ufficiale Installazione dell&#39;estensione

![Installazione AEM ufficiale o miniatura dell&#39;estensione](assets/official-installation.png)

Service Pack ufficiale

![Icona ufficiale del service pack AEM](assets/official-service-pack.png)

Utilizza un&#39;icona univoca per il pacchetto. Non riutilizzare un&#39;icona utilizzata dall&#39;Adobe.

### Filtri del pacchetto {#package-filters}

I filtri identificano i nodi del repository da includere nel pacchetto. A **Definizione del filtro** specifica le seguenti informazioni:

* La **Percorso radice** del contenuto da includere
* **Regole** che includono o escludono nodi specifici sotto il percorso principale

Aggiungi regole utilizzando **+** pulsante . Rimuovi le regole utilizzando **-** pulsante .

Le regole vengono applicate in base al loro ordine in modo da posizionarle come richiesto utilizzando **Su** e **Giù** pulsanti freccia.

I filtri possono includere zero o più regole. Quando non sono definite regole, il pacchetto contiene tutto il contenuto presente nel percorso principale.

Puoi definire una o più definizioni di filtro per un pacchetto. Utilizza più di un filtro per includere il contenuto di più percorsi principali.

![Scheda Filtri](assets/edit-filter.png)

Durante la creazione dei filtri, puoi definire un percorso o utilizzare un’espressione regolare per specificare tutti i nodi da includere o escludere.

| Tipo di regola | Descrizione |
|---|---|
| include | L’inclusione di una directory includerà tale directory e tutti i file e le cartelle presenti in tale directory (ovvero l’intero sottoalbero), ma **non** includere altri file o cartelle dal percorso principale specificato. |
| escludi | L’esclusione di una directory esclude tale directory e tutti i file e le cartelle presenti in tale directory (ovvero l’intera sottostruttura). |

I filtri dei pacchetti sono definiti più spesso al primo momento [crea il pacchetto.](#creating-a-new-package) Tuttavia possono anche essere modificati in un secondo momento, dopodiché il pacchetto deve essere ricostruito per aggiornare il contenuto in base alle nuove definizioni di filtro.

>[!TIP]
>
>Un pacchetto può contenere più definizioni di filtro in modo che i nodi da posizioni diverse possano essere facilmente combinati in un unico pacchetto.

### Dipendenze {#dependencies}

![Scheda Dipendenze](assets/dependencies.png)

| Campo | Descrizione | Esempio/Dettagli |
|---|---|---|
| Testato con | Il nome e la versione del prodotto a cui è destinato il pacchetto o con cui è compatibile. | `6.5` |
| Problemi risolti | Un campo di testo che consente di elencare i dettagli dei bug corretti con questo pacchetto, un bug per riga | - |
| Dipende da | Elenca gli altri pacchetti necessari in modo che il pacchetto corrente venga eseguito come previsto quando installato | `groupId:name:version` |
| Sostituisce | Elenco dei pacchetti obsoleti che questo pacchetto sostituisce | `groupId:name:version` |

### Impostazioni avanzate {#advanced-settings}

![Scheda Impostazioni avanzate](assets/advanced-settings.png)

| Campo | Descrizione | Esempio/Dettagli |
|---|---|---|
| Nome | Nome del provider del pacchetto | `WKND Media Group` |
| URL | URL del provider | `https://wknd.site` |
| Collegamento | Collegamento specifico del pacchetto a una pagina del provider | `https://wknd.site/package/` |
| Richiede | Definisce se ci sono restrizioni durante l&#39;installazione del pacchetto | **Amministratore** - Il pacchetto deve essere installato solo con privilegi di amministratore <br>**Riavvia** - AEM riavviato dopo l&#39;installazione del pacchetto |
| Gestione AC | Specifica come vengono gestite le informazioni sul controllo di accesso definite nel pacchetto quando il pacchetto viene importato | **Ignora** - Conservare le ACL nell&#39;archivio <br>**Sovrascrittura** - Sovrascrivi ACL nel repository <br>**Unisci** - Unire entrambi i set di ACL <br>**MergePreserve** - Unisci il controllo di accesso nel contenuto con quello fornito con il pacchetto aggiungendo le voci di controllo di accesso delle entità principali non presenti nel contenuto <br>**Cancella** - Cancella ACL |

### Schermate del pacchetto {#package-screenshots}

Puoi allegare più schermate al pacchetto per fornire una rappresentazione visiva di come appare il contenuto.

![Scheda Schermate](assets/screenshots.png)

## Azioni del pacchetto {#package-actions}

Ci sono molte azioni che possono essere intraprese su un pacchetto.

### Creazione di un pacchetto {#creating-a-new-package}

1. [Accedi a Gestione pacchetti.](#accessing)

1. Fai clic su **Crea pacchetto**.

   >[!TIP]
   >
   >Se l’istanza contiene molti pacchetti, potrebbe essere presente una struttura di cartelle. In questi casi, è più facile passare alla cartella di destinazione richiesta prima di creare il nuovo pacchetto.

1. In **Nuovo pacchetto** , immetti i campi seguenti:

   ![Finestra di dialogo Nuovo pacchetto](assets/new-package-dialog.png)

   * **Nome pacchetto** - Seleziona un nome descrittivo per identificare facilmente il contenuto del pacchetto.

   * **Versione** - Questo è un campo di testo per indicare una versione. Questo viene aggiunto al nome del pacchetto per formare il nome del file zip.

   * **Gruppo** - Nome del gruppo di destinazione (o della cartella). I gruppi consentono di organizzare i pacchetti. Se non esiste già, viene creata una cartella per il gruppo. Se lasci vuoto il nome del gruppo, verrà creato il pacchetto nell&#39;elenco dei pacchetti principali.

1. Fai clic su **OK** per creare il pacchetto.

1. AEM elenca il nuovo pacchetto nella parte superiore dell’elenco dei pacchetti.

   ![Nuovo pacchetto](assets/new-package.png)

1. Fai clic su **Modifica** per definire [contenuto del pacchetto.](#package-contents) Fai clic su **Salva** al termine della modifica delle impostazioni.

1. Ora puoi [Crea](#building-a-package) il tuo pacchetto.

Non è obbligatorio costruire immediatamente il pacchetto dopo averlo creato. Un pacchetto non generato non contiene contenuto ed è costituito solo dai dati del filtro e da altri metadati del pacchetto.

### Creazione di un pacchetto {#building-a-package}

Un pacchetto viene spesso generato contemporaneamente a te [crea il pacchetto](#creating-a-new-package), ma puoi tornare in un momento successivo per generare o ricostruire il pacchetto. Questo può essere utile se il contenuto all’interno dell’archivio è stato modificato o se i filtri del pacchetto sono cambiati.

1. [Accedi a Gestione pacchetti.](#accessing)

1. Apri i dettagli del pacchetto dall’elenco dei pacchetti facendo clic sul nome del pacchetto.

1. Fai clic su **Crea**. Una finestra di dialogo richiede la conferma della creazione del pacchetto, in quanto eventuali contenuti del pacchetto esistenti verranno sovrascritti.

1. Fai clic su **OK**. AEM crea il pacchetto, elencando tutti i contenuti aggiunti al pacchetto così come lo fa nell’elenco delle attività. Quando completato AEM visualizza una conferma della generazione del pacchetto e (quando chiudi la finestra di dialogo) aggiorna le informazioni sull’elenco dei pacchetti.

### Modifica di un pacchetto {#edit-package}

Una volta caricato un pacchetto in AEM, puoi modificarne le impostazioni.

1. [Accedi a Gestione pacchetti.](#accessing)

1. Apri i dettagli del pacchetto dall’elenco dei pacchetti facendo clic sul nome del pacchetto.

1. Fai clic su **Modifica** e aggiorna **[Impostazioni pacchetto](#package-settings)** se necessario.

1. Fai clic su **Salva** da salvare.

Potrebbe essere necessario [ricostruire il pacchetto](#building-a-package) per aggiornarne il contenuto in base alle modifiche apportate.

### Ritorno a capo di un pacchetto {#rewrapping-a-package}

Una volta costruito un pacchetto, può essere rispedito. Il rewrapping modifica le informazioni del pacchetto senza bisogno di miniature, descrizioni e così via, senza modificare il contenuto del pacchetto.

1. [Accedi a Gestione pacchetti.](#accessing)

1. Apri i dettagli del pacchetto dall’elenco dei pacchetti facendo clic sul nome del pacchetto.

1. Fai clic su **Modifica** e aggiorna **[Impostazioni pacchetto](#package-settings)** se necessario.

1. Fai clic su **Salva** da salvare.

1. Fai clic su **Altro** -> **Riavvolgere** e una finestra di dialogo chiederà una conferma.

### Visualizzazione di altre versioni del pacchetto {#other-versions}

Poiché ogni versione di un pacchetto viene visualizzata nell’elenco come qualsiasi altro pacchetto, Gestione pacchetti può trovare altre versioni di un pacchetto selezionato.

1. [Accedi a Gestione pacchetti.](#accessing)

1. Apri i dettagli del pacchetto dall’elenco dei pacchetti facendo clic sul nome del pacchetto.

1. Fai clic su **Altro** -> **Altre versioni** viene visualizzata una finestra di dialogo con un elenco di altre versioni dello stesso pacchetto con informazioni sullo stato.

### Visualizzazione del contenuto del pacchetto e verifica dell’installazione {#viewing-package-contents-and-testing-installation}

Una volta generato un pacchetto, puoi visualizzarne il contenuto.

1. [Accedi a Gestione pacchetti.](#accessing)

1. Apri i dettagli del pacchetto dall’elenco dei pacchetti facendo clic sul nome del pacchetto.

1. Per visualizzare il contenuto, fai clic su **Altro** -> **Contenuto**, e Gestione pacchetti elenca l’intero contenuto del pacchetto nel registro attività.

   ![Contenuto del pacchetto](assets/package-contents.png)

1. Per eseguire una prova dell&#39;installazione, fare clic su **Altro** -> **Test installazione** e Package Manager nel registro attività riporta i risultati come se l&#39;installazione fosse stata eseguita.

   ![Installazione di prova](assets/test-install.png)

### Download dei pacchetti nel file system {#downloading-packages-to-your-file-system}

1. [Accedi a Gestione pacchetti.](#accessing)

1. Apri i dettagli del pacchetto dall’elenco dei pacchetti facendo clic sul nome del pacchetto.

1. Fai clic sul pulsante **Scarica** o il nome file collegato del pacchetto nell&#39;area dei dettagli del pacchetto.

1. AEM scaricare il pacchetto sul computer.

### Condivisione di un pacchetto {#share}

Package Share era un servizio pubblico centralizzato per la distribuzione dei pacchetti di contenuti. Condivisione pacchetti sostituita da [Distribuzione di software](#software-distribution) e questo pulsante non funziona più.

### Caricamento dei pacchetti dal file system {#uploading-packages-from-your-file-system}

1. [Accedi a Gestione pacchetti.](#accessing)

1. Seleziona la cartella del gruppo in cui desideri caricare il pacchetto.

1. Fai clic sul pulsante **Carica pacchetto** pulsante .

1. Fornisci le informazioni necessarie sul pacchetto caricato.

   ![Finestra di dialogo di caricamento del pacchetto](assets/package-upload-dialog.png)

   * **Pacchetto** - Utilizzare **Sfoglia..** per selezionare il pacchetto richiesto dal file system locale.
   * **Forza caricamento** - Se esiste già un pacchetto con questo nome, questa opzione forza il caricamento e sovrascrive il pacchetto esistente.

1. Fai clic su **OK** e il pacchetto selezionato viene caricato e l&#39;elenco dei pacchetti viene aggiornato di conseguenza.

Il contenuto del pacchetto esiste ora in AEM, ma per renderlo disponibile per l’uso, assicurati di [installa il pacchetto](#installing-packages).

### Convalida dei pacchetti {#validating-packages}

Poiché i pacchetti possono modificare il contenuto esistente, spesso è utile convalidare queste modifiche prima dell&#39;installazione.

#### Opzioni di convalida {#validation-options}

Package Manager può eseguire le seguenti convalide:

* [Importazioni dei pacchetti OSGi](#osgi-package-imports)
* [Sovrapposizioni](#overlays)
* [ACL](#acls)

##### Convalida importazioni di pacchetti OSGi {#osgi-package-imports}

**Elementi controllati**

Questa convalida esamina il pacchetto per tutti i file JAR (bundle OSGi), ne estrae `manifest.xml` (che contiene le dipendenze con versione su cui si basa il bundle OSGi) e verifica le esportazioni dell&#39;istanza AEM con le versioni corrette.

**Come viene segnalato**

Tutte le dipendenze con versione che non possono essere soddisfatte dall&#39;istanza AEM sono elencate nel Registro attività di Gestione pacchetti.

**Stati di errore**

Se le dipendenze non sono soddisfatte, i bundle OSGi nel pacchetto con quelle dipendenze non si avvieranno. Questo si traduce in un&#39;implementazione non funzionante, in quanto tutto ciò che si basa sul bundle OSGi non avviato non funzionerà a sua volta correttamente.

**Risoluzione degli errori**

Per risolvere gli errori dovuti ai bundle OSGi non soddisfatti, è necessario modificare la versione della dipendenza nel bundle con importazioni non soddisfatte.

##### Convalida sovrapposizioni {#overlays}

**Elementi controllati**

Questa convalida determina se il pacchetto installato contiene un file già sovrapposto nell&#39;istanza AEM di destinazione.

Ad esempio, se hai impostato una sovrapposizione esistente in `/apps/sling/servlet/errorhandler/404.jsp`, un pacchetto che contiene `/libs/sling/servlet/errorhandler/404.jsp`, in modo da modificare il file esistente in `/libs/sling/servlet/errorhandler/404.jsp`.

**Come viene segnalato**

Tali sovrapposizioni sono descritte nel registro attività di Gestione pacchetti.

**Stati di errore**

Uno stato di errore indica che il pacchetto sta tentando di distribuire un file già sovrapposto, pertanto le modifiche nel pacchetto verranno sostituite (e quindi &quot;nascoste&quot;) dalla sovrapposizione e non avranno effetto.

**Risoluzione degli errori**

Per risolvere questo problema, il gestore del file di sovrapposizione in `/apps` deve esaminare le modifiche apportate al file sovrapposto in `/libs` e incorpora le modifiche necessarie nella sovrapposizione ( `/apps`) e ridistribuisci il file sovrapposto.

>[!NOTE]
>
>Il meccanismo di convalida non può essere riconciliato se il contenuto sovrapposto è stato correttamente incorporato nel file di sovrapposizione. Pertanto questa convalida continuerà a segnalare i conflitti anche dopo aver apportato le modifiche necessarie.

##### Convalida ACL {#acls}

**Elementi controllati**

Questa convalida verifica quali autorizzazioni vengono aggiunte, come verranno gestite (unione/sostituzione) e se le autorizzazioni correnti saranno interessate.

**Come viene segnalato**

Le autorizzazioni sono descritte nel registro attività di Gestione pacchetti.

**Stati di errore**

Non è possibile fornire errori espliciti. La convalida indica semplicemente se eventuali nuove autorizzazioni ACL verranno aggiunte o influenzate dall&#39;installazione del pacchetto.

**Risoluzione degli errori**

Utilizzando le informazioni fornite dalla convalida, i nodi interessati possono essere rivisti in CRXDE e le ACL possono essere regolate nel pacchetto come necessario.

>[!CAUTION]
>
>Come best practice, si consiglia di non influenzare gli ACL forniti da AEM, in quanto ciò potrebbe causare un comportamento imprevisto.

#### Esecuzione della convalida {#performing-validation}

La convalida dei pacchetti può essere eseguita in due modi diversi:

* [Tramite l’interfaccia utente di Gestione pacchetti](#via-package-manager)
* [Tramite richiesta HTTP POST, ad esempio con cURL](#via-post-request)

La convalida deve sempre verificarsi dopo il caricamento del pacchetto ma prima di installarlo.

##### Convalida Del Pacchetto Tramite Gestione Pacchetti {#via-package-manager}

1. [Accedi a Gestione pacchetti.](#accessing)

1. Apri i dettagli del pacchetto dall’elenco dei pacchetti facendo clic sul nome del pacchetto.

1. Per convalidare il pacchetto, fai clic su **Altro** -> **Convalida**,

1. Nella finestra di dialogo modale visualizzata, utilizzare le caselle di controllo per selezionare i tipi di convalida e iniziare la convalida facendo clic su **Convalida**.

1. Le convalide scelte vengono quindi eseguite e i risultati vengono visualizzati nel Registro attività di Gestione pacchetti.

##### Convalida Del Pacchetto Tramite Richiesta HTTP POST {#via-post-request}

La richiesta di POST si presenta come segue.

```
https://<host>:<port>/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls
```

La `type` può essere un qualsiasi elenco non ordinato e separato da virgole composto da:

* `osgiPackageImports`
* `overlays`
* `acls`

Il valore di `type` impostazioni predefinite `osgiPackageImports` se non è passato in modo esplicito.

Quando utilizzi cURL, esegui un’istruzione simile alla seguente:

```shell
curl -v -X POST --user admin:admin -F file=@/Users/SomeGuy/Desktop/core.wcm.components.all-1.1.0.zip 'http://localhost:4502/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls'
```

Quando si convalida tramite richiesta POST, la risposta viene inviata nuovamente come oggetto JSON.

### Visualizzazione della copertura del pacchetto {#package-coverage}

I pacchetti sono definiti dai relativi filtri. Puoi chiedere a Gestione pacchetti di applicare i filtri di un pacchetto al contenuto dell’archivio esistente per mostrare quale contenuto dell’archivio è coperto dalla definizione di filtro del pacchetto.

1. [Accedi a Gestione pacchetti.](#accessing)

1. Apri i dettagli del pacchetto dall’elenco dei pacchetti facendo clic sul nome del pacchetto.

1. Fai clic su **Altro** -> **Copertura**.

1. I dettagli di copertura sono elencati nel Registro attività.

### Installazione dei pacchetti {#installing-packages}

Il caricamento di un pacchetto aggiunge solo il contenuto del pacchetto all’archivio, ma non è accessibile. Per utilizzare il contenuto del pacchetto, devi installare il pacchetto caricato.

>[!CAUTION]
>
>L’installazione di un pacchetto può sovrascrivere o eliminare il contenuto esistente. Carica un pacchetto solo se sei sicuro che non elimini o sovrascrivi il contenuto necessario.

Prima dell’installazione del pacchetto, Gestione pacchetti crea automaticamente un pacchetto di snapshot contenente il contenuto che verrà sovrascritto. Se disinstalli il pacchetto, lo snapshot verrà reinstallato.

1. [Accedi a Gestione pacchetti.](#accessing)

1. Apri i dettagli del pacchetto che desideri installare dall&#39;elenco dei pacchetti facendo clic sul nome del pacchetto.

1. Fai clic su **Installa** nei dettagli dell&#39;elemento o **Installa** nello stato del pacchetto.

1. Viene visualizzata una finestra di dialogo che richiede la conferma e consente di specificare ulteriori opzioni.

   * **Solo estrazione** - Estrai il pacchetto solo in modo che non venga creata alcuna istantanea e quindi non sarà possibile disinstallarlo
   * **Salva soglia** - Numero di nodi transitori fino all&#39;attivazione del salvataggio automatico (aumenta se si verificano eccezioni di modifica simultanea)
   * **Estrai pacchetti secondari** - Attiva l&#39;estrazione automatica dei pacchetti secondari
   * **Gestione del controllo degli accessi** - Specifica come vengono gestite le informazioni sul controllo di accesso definite nel pacchetto quando il pacchetto viene installato (le opzioni sono le stesse del [impostazioni avanzate del pacchetto](#advanced-settings))
   * **Gestione delle dipendenze** - Specificare la modalità di gestione delle dipendenze durante l&#39;installazione

1. Fai clic su **Installa**.

1. Il registro attività descrive l’avanzamento dell’installazione.

>[!CAUTION]
>
>* Se stai installando risorse digitali, devi:
   >  Per prima cosa, disattiva WorkflowLauncher.
   >  Per disattivare, utilizza l’opzione di menu Componenti della console OSGi
   >  `com.day.cq.workflow.launcher.impl.WorkflowLauncherImpl.`
>* Al termine dell’installazione, riattiva WorkflowLauncher.
>
>La disattivazione di WorkflowLauncher assicura che il framework di Importazione risorse non manipoli (involontariamente) le risorse al momento dell’installazione.

Una volta completata e completata l&#39;installazione, l&#39;elenco dei pacchetti viene aggiornato e la parola **Installato** viene visualizzato nello stato del pacchetto.

### Reinstallazione dei pacchetti {#reinstalling-packages}

La reinstallazione dei pacchetti esegue gli stessi passaggi su un pacchetto già installato che vengono elaborati quando [installazione iniziale del pacchetto.](#installing-packages)

### Caricamento e installazione basati su file system {#file-system-based-upload-and-installation}

È possibile rinunciare completamente a Gestione pacchetti durante l&#39;installazione dei pacchetti. AEM rilevare i pacchetti inseriti in una posizione specifica nel file system locale della macchina host e caricarli e installarli automaticamente.

1. Nella cartella di installazione di AEM è presente un `crx-quicksart` accanto al jar e `license.properties` file. Crea una cartella denominata `install` sotto `crx-quickstart` che determina il percorso `<aem-home>/crx-quickstart/install`.

1. In questa cartella, aggiungi i pacchetti. Vengono caricati e installati automaticamente nell’istanza.

1. Al termine del caricamento e dell’installazione, puoi vedere i pacchetti in Gestione pacchetti come se avessi utilizzato l’interfaccia utente Gestione pacchetti per installarli.

Se l&#39;istanza è in esecuzione, il caricamento e l&#39;installazione iniziano immediatamente quando lo aggiungi al pacchetto al `install` cartella

Se l&#39;istanza non è in esecuzione, i pacchetti posizionati nel `install` all&#39;avvio vengono installate le cartelle in ordine alfabetico.

### Disinstallazione dei pacchetti {#uninstalling-packages}

La disinstallazione del pacchetto ripristina il contenuto dell&#39;archivio sullo snapshot creato automaticamente da Gestione pacchetti prima dell&#39;installazione.

1. [Accedi a Gestione pacchetti.](#accessing)

1. Apri i dettagli del pacchetto da disinstallare dall&#39;elenco dei pacchetti facendo clic sul nome del pacchetto.

1. Fai clic su **Altro** -> **Disinstalla**, per rimuovere il contenuto di questo pacchetto dall’archivio.

1. Viene visualizzata una finestra di dialogo per richiedere conferma ed elencare tutte le modifiche in corso.

1. Il pacchetto viene rimosso e lo snapshot viene applicato. L’avanzamento del processo viene visualizzato nel Registro attività.

### Eliminazione dei pacchetti {#deleting-packages}

L&#39;eliminazione di un pacchetto comporta solo l&#39;eliminazione dei relativi dettagli da Gestione pacchetti. Se il pacchetto è già installato, il contenuto installato non verrà eliminato.

1. [Accedi a Gestione pacchetti.](#accessing)

1. Apri i dettagli del pacchetto che desideri eliminare dall’elenco dei pacchetti facendo clic sul nome del pacchetto.

1. Gestione pacchetti richiede la conferma dell’eliminazione del pacchetto. Fai clic su **OK** per confermare l’eliminazione.

1. Le informazioni sul pacchetto vengono eliminate e i dettagli vengono segnalati nel Registro attività.

### Replica dei pacchetti {#replicating-packages}

Replicare il contenuto di un pacchetto per installarlo nell&#39;istanza di pubblicazione.

1. [Accedi a Gestione pacchetti.](#accessing)

1. Apri i dettagli del pacchetto da replicare dall&#39;elenco dei pacchetti facendo clic sul nome del pacchetto.

1. Fai clic su **Altro** -> **Replicare**.

1. Il pacchetto viene replicato e i dettagli sono riportati nel registro attività.

## Distribuzione di software {#software-distribution}

I pacchetti AEM possono essere utilizzati per creare e condividere contenuti tra ambienti AEM.

[Distribuzione di software](https://downloads.experiencecloud.adobe.com) è un servizio centralizzato progettato per semplificare la ricerca e il download di pacchetti AEM.

Per ulteriori informazioni, consulta la [Documentazione sulla distribuzione software.](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html)

>[!NOTE]
>
>Gestione pacchetti non è attualmente integrato con Distribuzione software come con il precedente servizio Condivisione pacchetti. Pertanto i pulsanti di condivisione e altri collegamenti a Condivisione pacchetti in Gestione pacchetti non funzionano più. La soluzione consiste nel scaricare i pacchetti sul disco locale.
