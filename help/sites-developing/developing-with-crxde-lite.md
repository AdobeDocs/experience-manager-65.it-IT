---
title: Sviluppo con CRXDE Liti
seo-title: Developing with CRXDE Lite
description: CRXDE Liti è incorporato nell’AEM e consente di eseguire attività di sviluppo standard nel browser
seo-description: CRXDE Lite is embedded into AEM and enables you to perform standard development tasks in the browser
uuid: f4890354-d8b8-4fb9-af2f-3359f931f883
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 4537c1fb-f99c-42e2-a222-b037794bdb52
docset: aem65
exl-id: 9e88ca55-ac3d-4857-b6b2-aeb732562664
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '2137'
ht-degree: 2%

---

# Sviluppo con CRXDE Liti{#developing-with-crxde-lite}

Questa sezione descrive come sviluppare l’applicazione AEM utilizzando CRXDE Liti.

Per ulteriori informazioni sui diversi ambienti di sviluppo disponibili, consulta la panoramica.

CRXDE Liti è incorporato nell’AEM e consente di eseguire attività di sviluppo standard nel browser. Con CRXDE Liti puoi creare un progetto, creare e modificare file (come .jsp e .java), cartelle, modelli, componenti, finestre di dialogo, nodi, proprietà e bundle durante la registrazione.
CRXDE Liti è consigliato quando non hai accesso diretto al server AEM, quando sviluppi un’applicazione estendendo o modificando i componenti predefiniti e i bundle Java o quando non hai bisogno di un debugger dedicato, del completamento del codice e dell’evidenziazione della sintassi.

>[!NOTE]
>
>A partire dalla versione 6.5.5.0 dell&#39;AEM, l&#39;accesso anonimo alla CRXDE Liti non è più possibile.
>Gli utenti vengono reindirizzati alla schermata di accesso.


>[!NOTE]
>
>Si consiglia di utilizzare il [Strumenti per sviluppatori AEM per Eclipse](/help/sites-developing/aem-eclipse.md) e [Estensione per parentesi HTL AEM](/help/sites-developing/aem-brackets.md) durante lo sviluppo del progetto.

## Guida introduttiva di CRXDE Liti {#getting-started-with-crxde-lite}

Per iniziare a utilizzare CRXDE Liti, procedere come segue:

1. Installare AEM.
1. Nel browser, immetti `https://<host>:<port>/crx/de`. Per impostazione predefinita, è `https://localhost:4502/crx/de`.
1. Immetti il **nome utente** e **password**. Per impostazione predefinita è `admin` e `admin`.

1. Fai clic su **OK**.

L’interfaccia utente di CRXDE Liti si presenta come segue nel browser:

![chlimage_1-18](assets/crx-interface.jpg)

Ora puoi utilizzare CRXDE Liti per sviluppare l’applicazione.

## Panoramica dell’interfaccia utente {#overview-of-the-user-interface}

CRXDE Liti offre le seguenti funzionalità:

<table>
 <tbody>
  <tr>
   <td>Barra del commutatore superiore</td>
   <td>Consente di passare rapidamente da CRXDE Liti a Gestione pacchetti e Condivisione pacchetti.</td>
  </tr>
  <tr>
   <td>Widget percorso nodo</td>
   <td><p>Visualizza il percorso del nodo attualmente selezionato.</p> <p>Puoi anche utilizzarlo per passare a un nodo, immettendo manualmente il percorso o incollandolo da un’altra posizione e premendo Invio.</p> <p>Fornisce inoltre supporto per la ricerca di nodi con un nome di nodo specifico. Inserisci il nome del nodo che desideri trovare e attendi (o premi il simbolo di ricerca sul lato destro). È possibile provare a immettere, ad esempio, la stringa <em>quercia</em> per vedere come funziona. Se uno o più nodi vengono caricati nel riquadro dell'elenco delle cartelle, verrà visualizzato l'elenco e sarà possibile selezionare il percorso e premere Invio per individuarlo. Si noti che funziona solo per i nodi attualmente caricati nell’applicazione client CRXDE nel browser. Se si desidera eseguire una ricerca nell'intero repository, utilizzare Strumenti, quindi Query.</p> </td>
  </tr>
  <tr>
   <td>Riquadro di Explorer</td>
   <td><p>Visualizza una struttura di tutti i nodi del repository.</p> <p>Fai clic su un nodo per visualizzarne le proprietà nel <strong>Proprietà</strong> scheda. Dopo aver fatto clic su un nodo, puoi selezionare un’azione nella barra degli strumenti. Fai di nuovo clic sul nodo per rinominarlo.</p> <p>Filtro navigazione albero (icona binoculare): consente di filtrare i nodi nell’archivio per i quali il nome contiene il testo di input. Si applica solo ai nodi che sono stati caricati localmente.<br /> </p> </td>
  </tr>
  <tr>
   <td>Riquadro di modifica</td>
   <td><p><strong>Home</strong> scheda: consente di cercare contenuti e/o documentazione e di accedere alle risorse per gli sviluppatori (documentazione, blog per sviluppatori, knowledge base) e al supporto (home page e centro di supporto di Adobe).<br /> </p> <p>Fare doppio clic su un file in <strong>Esplora</strong> per visualizzarne il contenuto, ad esempio un file .jsp o .java. Puoi quindi modificarlo e salvare le modifiche.</p> <p>Dopo aver modificato un file in <strong>Modifica</strong> sulla barra degli strumenti sono disponibili i seguenti strumenti:<br /> </p> - <strong>Mostra nella struttura: </strong>mostra il file nella struttura del repository.<br /> - <strong>Cerca/Sostituisci...</strong>: esegui la ricerca o sostituisci.<br /> <br /> Fare doppio clic sulla riga di stato del <strong>Modifica</strong> apre il riquadro <strong>Vai alla riga</strong> in modo da poter immettere un numero di riga specifico.<br /> </td>
  </tr>
  <tr>
   <td>Scheda Proprietà<br /> </td>
   <td>Visualizza le proprietà del nodo selezionato. Puoi aggiungere nuove proprietà o eliminare quelle esistenti.<br /> </td>
  </tr>
  <tr>
   <td>Scheda Controllo di accesso</td>
   <td><p>Visualizza le autorizzazioni in base al percorso corrente, a livello di repository o entità principale.</p> <p>Le autorizzazioni sono suddivise in</p> <p>- <strong>Criterio di controllo dell’accesso applicabile</strong>: i criteri che possono essere applicati alla selezione corrente.</p> <p>- <strong>Criteri di controllo dell'accesso locale</strong>: i criteri correnti applicati localmente alla selezione corrente.</p> <p>- <strong>Criteri di controllo dell'accesso effettivi</strong>: i criteri correnti applicati per la selezione corrente, possono essere impostati localmente o ereditati dai nodi padre.</p> <p>Nota. Per poter visualizzare le informazioni sul controllo di accesso, l'utente connesso a CRXDE Liti deve disporre dei diritti per la lettura delle voci ACL. L’utente anonimo non può visualizzare queste informazioni per impostazione predefinita. Accedi come, ad esempio, amministratore per visualizzare le informazioni.</p> </td>
  </tr>
  <tr>
   <td>Scheda Replica</td>
   <td><p>Visualizza lo stato di replica del nodo corrente. Puoi replicare e replicare per eliminare il nodo corrente.</p> </td>
  </tr>
  <tr>
   <td>Scheda Console<br /> </td>
   <td><p><strong>Registri del server</strong>:</p> <p>Visualizza i messaggi dei registri. Puoi configurare il livello di registro, cancellare la console, fissare la posizione di scorrimento selezionata e abilitare/disabilitare la visualizzazione dei messaggi.<br /> </p> <p><strong>Controllo della versione</strong>:</p> <p>Visualizza i messaggi di controllo della versione.<br /> </p> </td>
  </tr>
  <tr>
   <td>Scheda Informazioni sulla build<br /> </td>
   <td>Visualizza informazioni durante la generazione di un bundle.<br /> </td>
  </tr>
  <tr>
   <td>Aggiorna<br /> </td>
   <td>Aggiorna la selezione corrente. Le modifiche apportate da altri utenti vengono aggiornate nella vista dell’archivio. Le modifiche apportate non vengono modificate.<br /> </td>
  </tr>
  <tr>
   <td>Salva tutto</td>
   <td><p><strong>Salva tutto</strong>:<br /> </p> <p>Salva tutte le modifiche apportate. Fino a quando non fai clic su Salva, le modifiche sono temporanee e andranno perse quando esci dalla console.</p> <p><strong>Versione precedente</strong>:</p> <p>Elimina tutte le modifiche apportate al nodo selezionato dall'ultima azione di salvataggio, quindi ricarica lo stato corrente dell'archivio per il nodo selezionato.</p> <p><strong>Ripristina tutto</strong>:</p> <p>Elimina tutte le modifiche apportate in tutto l'archivio dall'ultima azione di salvataggio, quindi ricarica lo stato corrente dell'archivio.</p> </td>
  </tr>
  <tr>
   <td>Creare ...<br /> </td>
   <td><p>Menu a discesa per creare quanto segue sotto il nodo selezionato:<br /> </p> <p>- <strong>Nodo</strong>: nodo con tipo di nodo arbitrario<br /> </p> <p>- <strong>File</strong>: nodo nt:file e relativo sottonodo nt:resource</p> <p>- <strong>Cartella</strong>: nt:folder node</p> <p>- <strong>Modello</strong>: modello AEM</p> <p>- <strong>Componente</strong>: componente AEM</p> <p>- <strong>Finestra di dialogo</strong>: finestra di dialogo AEM</p> </td>
  </tr>
  <tr>
   <td>Eliminare<br /> </td>
   <td>Elimina il nodo selezionato.<br /> </td>
  </tr>
  <tr>
   <td>Copiare</td>
   <td>Copia il nodo selezionato.<br /> </td>
  </tr>
  <tr>
   <td>Incolla<br /> </td>
   <td>Incolla il nodo copiato sotto il nodo selezionato.<br /> </td>
  </tr>
  <tr>
   <td>Sposta ...<br /> </td>
   <td>Sposta il nodo selezionato sul nodo impostato tramite la finestra di dialogo.</td>
  </tr>
  <tr>
   <td>Rinomina ...<br /> </td>
   <td>Rinomina il nodo selezionato.<br /> </td>
  </tr>
  <tr>
   <td>Mixin...<br /> </td>
   <td>Consente di aggiungere tipi mixin al tipo di nodo. I tipi mixin vengono utilizzati principalmente per aggiungere funzioni avanzate come il controllo delle versioni, il controllo degli accessi, i riferimenti e il blocco al nodo.</td>
  </tr>
  <tr>
   <td>Strumenti<br /> </td>
   <td><p>Menu a discesa con i seguenti strumenti:</p> <p>- <strong>Configurazione server...</strong>: per accedere alla console Felix.</p> <p>- <strong>Query...</strong>: per eseguire una query sull’archivio.</p> <p>- <strong>Privilegi...</strong>: per aprire gestione dei privilegi, in cui è possibile visualizzare e aggiungere privilegi.</p> <p>- <strong>Test controllo accesso...</strong>: luogo in cui è possibile verificare l’autorizzazione per un determinato percorso e/o entità principale.</p> <p>- <strong>Esporta tipo di nodo</strong>: per esportare i tipi di nodo nel sistema come notazione del nodo.</p> <p>- <strong>Importa tipo di nodo...</strong>: per importare tipi di nodo utilizzando la notazione cnd.</p> <p>- <strong>Installa SiteCatalyst Debugger...</strong>: istruzioni su come installare Analytics Debugger.</p> </td>
  </tr>
  <tr>
   <td>Widget di accesso<br /> </td>
   <td><p>Visualizza gli utenti attualmente connessi e l'area di lavoro a cui sono connessi, ad esempio admin@crx.default.</p> <p>Fai clic su di esso per accedere o accedere nuovamente come utente specifico. Se non specifichi un'area di lavoro a cui accedere, verrà effettuato l'accesso all'area di lavoro predefinita, crx.default.</p> <p>Se desideri sfogliare il repository come utente anonimo, utilizza <strong>anonimo</strong> come nome di accesso ed eventuali password (ad esempio, uno spazio o un punto).<br /> </p> <p>Se l’autorizzazione non è più valida (ad esempio, è scaduta), il widget di accesso visualizza "<strong>Non autorizzato - Accesso...</strong>". Fai clic su di esso per accedere di nuovo.</p> </td>
  </tr>
 </tbody>
</table>

## Creazione di una cartella {#creating-a-folder}

Per creare una cartella con CRXDE Liti:

1. Apri CRXDE Liti nel browser.
1. Nel riquadro di spostamento fare clic con il pulsante destro del mouse sulla cartella in cui si desidera creare la nuova cartella e selezionare **Crea...**, quindi **Crea cartella...**.

1. Inserisci la cartella **Nome** e fai clic su **OK**.

1. Clic **Salva tutto** per salvare le modifiche sul server.

## Creazione di un modello {#creating-a-template}

Per creare un modello con CRXDE Liti:

1. Apri CRXDE Liti nel browser.
1. Nel riquadro di spostamento fare clic con il pulsante destro del mouse sulla cartella in cui si desidera creare il modello e selezionare **Crea...**, quindi **Crea modello...**.

1. Inserisci il **Etichetta**, **Titolo**, **Descrizione**, **Tipo di risorsa** e **Classificazione** del modello. Fai clic su **Avanti**.

1. Questo passaggio è facoltativo: imposta **Percorsi consentiti**. Fai clic su **Avanti**

1. Questo passaggio è facoltativo: imposta **Elementi padre consentiti**. Fai clic su **Avanti**.

1. Questo passaggio è facoltativo: imposta **Elementi figlio consentiti**. Fai clic su **OK**.

1. Clic **Salva tutto** per salvare le modifiche sul server.

Crea:

* Un nodo di tipo `cq:Template` con proprietà modello

* Un nodo figlio di tipo `cq:PageContent` con proprietà Contenuto pagina

Puoi aggiungere proprietà al modello: fai riferimento a [Creazione di una proprietà](#creating-a-property) sezione.

## Creazione di un componente {#creating-a-component}

La funzione descritta qui è disponibile solo se è installato CQ5, ovvero se il tipo di nodo `cq:Component` è disponibile nell’archivio.

Per creare un componente con CRXDE Liti:

1. Apri CRXDE Liti nel browser.
1. Nel riquadro di spostamento fare clic con il pulsante destro del mouse sulla cartella in cui si desidera creare il componente e selezionare **Crea...**, quindi **Crea componente...**.

1. Inserisci il **Etichetta**, **Titolo**, **Descrizione**, **Tipo di risorsa super** e **Gruppo** del componente. Fai clic su **Avanti**.

1. Questo passaggio è facoltativo: imposta le proprietà del componente **È contenitore,** **Nessuna decorazione**, **Nome cella** e **Percorso finestra di dialogo**. Fai clic su **Avanti**.

1. Questo passaggio è facoltativo: imposta la proprietà del componente **Elementi padre consentiti**. Fai clic su **Avanti**.

1. Questo passaggio è facoltativo: imposta la proprietà del componente **Elementi figlio consentiti**. Fai clic su **OK**.

1. Clic **Salva tutto** per salvare le modifiche sul server.

Crea:

* Un nodo di tipo `cq:Component`
* Proprietà componente
* Script .jsp di un componente

## Creazione di una finestra di dialogo {#creating-a-dialog}

Per creare una finestra di dialogo con CRXDE Liti:

1. Apri CRXDE Liti nel browser.
1. Nel riquadro di spostamento fare clic con il pulsante destro del mouse sul componente in cui si desidera creare la finestra di dialogo e selezionare **Crea...**, quindi **Crea finestra di dialogo...**.

1. Inserisci il **Etichetta** e **Titolo**. Fai clic su **OK**.

1. Clic **Salva tutto** l per salvare le modifiche sul server.

Crea una finestra di dialogo con la seguente struttura:

`dialog[cq:Dialog]/items[cq:Widget]/items[cq:WidgetCollection]/tab1[cq:Panel]`

Ora puoi adattare la finestra di dialogo alle tue esigenze modificando le proprietà o creando nuovi nodi.

Per modificare una finestra di dialogo, puoi anche utilizzare l’Editor finestre di dialogo. Facendo doppio clic sul nodo della finestra di dialogo in CRXDE Liti verrà visualizzato l’editor. Ulteriori informazioni sull’Editor finestre di dialogo sono disponibili [qui](/help/sites-developing/dialog-editor.md).

## Creazione di un nodo {#creating-a-node}

Per creare un nodo con CRXDE Liti:

1. Apri CRXDE Liti nel browser.
1. Nel riquadro di spostamento fare clic con il pulsante destro del mouse sul nodo in cui si desidera creare il nuovo nodo e selezionare **Crea...**, quindi **Crea nodo...**.
1. Inserisci il **Nome** e **Tipo**. Fai clic su **OK**.
1. Clic **Salva tutto** per salvare le modifiche sul server.

Ora puoi adattare il nodo alle tue esigenze modificando le proprietà o creando nuovi nodi.

>[!NOTE]
>
>La maggior parte delle operazioni di modifica, incluso Crea nodo, mantiene tutte le modifiche in memoria e le memorizza nell’archivio solo al momento del salvataggio (tramite il pulsante &quot;Salva tutto&quot;). Tuttavia, alcune operazioni, come lo spostamento, vengono mantenute automaticamente.
>
>La convalida che verifica se il nodo appena creato è consentito dal tipo di nodo del nodo principale viene eseguita prima dall’archivio JCR al momento del salvataggio delle modifiche. Se ricevi un messaggio di errore durante il salvataggio di un nodo, controlla se la struttura del contenuto è valida (ad esempio, non puoi creare un nodo `nt:unstructured` nodo come elemento secondario di `nt:folder` nodo ).

## Creazione di una proprietà {#creating-a-property}

Per creare una proprietà con CRXDE Liti:

1. Apri CRXDE Liti nel browser.
1. Nel riquadro di spostamento selezionare il nodo in cui si desidera aggiungere la nuova proprietà.
1. In **Proprietà** nel riquadro inferiore, immettere il **Nome**, il **Tipo** e **Valore**. Clic **Aggiungi**.

1. Clic **Salva tutto** per salvare le modifiche sul server.

## Creazione di uno script {#creating-a-script}

Per creare un nuovo script:

1. Apri CRXDE Liti nel browser.
1. Nel riquadro di spostamento fare clic con il pulsante destro del mouse sul componente in cui si desidera creare lo script e selezionare **Crea...**, quindi **Crea file...**.

1. Inserisci il file **Nome** inclusa la sua estensione. Fai clic su **OK**.

1. Il nuovo file viene aperto come scheda nel riquadro Modifica.
1. Modifica il file.
1. Clic **Salva tutto** per salvare le modifiche.

## Esportazione e importazione di tipi di nodo {#exporting-and-importing-node-types}

Con CRXDE Liti è possibile importare e/o esportare le definizioni dei tipi di nodo in [Notazione CND (Compact Namespace and Node Type Definition, spazio dei nomi compatto e definizione del tipo di nodo)](https://jackrabbit.apache.org/jcr/node-type-notation.html).

Per esportare la definizione di un tipo di nodo:

1. Apri CRXDE Liti nel browser.
1. Seleziona il nodo richiesto.
1. Seleziona **Strumenti** allora **Esporta tipo di nodo**.

1. La definizione, in notazione cnd, verrà visualizzata nel browser. Se necessario, salva le informazioni.

Per importare una definizione di tipo di nodo:

1. Apri CRXDE Liti nel browser.
1. Seleziona **Strumenti** allora **Importa tipo di nodo...**.

1. Immettere la notazione CND per la definizione nella casella di testo.
1. Verifica **Consenti aggiornamento** se stai aggiornando una definizione esistente.
1. Clic **Importa**.

## Registrazione {#logging}

Con CRXDE Liti è possibile visualizzare il file `error.log` che si trova nel file system in `<crx-install-dir>/crx-quickstart/server/logs` e filtrarlo con il livello di registro appropriato. Procedere come segue:

1. Apri CRXDE Liti nel browser.
1. In **Console** nella parte inferiore della finestra, nel menu a discesa a destra, seleziona **Registri server**.

1. Fai clic su **Interrompi** per visualizzare i messaggi.

Operazioni disponibili:

* Regolare i parametri di registro nella console Felix facendo clic sul pulsante **Configurazioni di registrazione** icona.
* Cancellare i messaggi facendo clic sul pulsante **Pennello** icona.
* Fissa il messaggio alla selezione corrente facendo clic sul pulsante **Fissa** icona.
* Attiva o disattiva la visualizzazione dei messaggi facendo clic sul pulsante **Interrompi** icona.

## Controllo accesso {#access-control}

>[!NOTE]
>
>Consulta [Amministrazione di utenti, gruppi e diritti di accesso](/help/sites-administering/user-group-ac-admin.md) per ulteriori informazioni.
