---
title: Sviluppo con CRXDE Lite
seo-title: Developing with CRXDE Lite
description: CRXDE Lite è incorporato in AEM e consente di eseguire attività di sviluppo standard nel browser
seo-description: CRXDE Lite is embedded into AEM and enables you to perform standard development tasks in the browser
uuid: f4890354-d8b8-4fb9-af2f-3359f931f883
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 4537c1fb-f99c-42e2-a222-b037794bdb52
docset: aem65
exl-id: 9e88ca55-ac3d-4857-b6b2-aeb732562664
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2134'
ht-degree: 2%

---

# Sviluppo con CRXDE Lite{#developing-with-crxde-lite}

Questa sezione descrive come sviluppare l’applicazione AEM utilizzando CRXDE Lite.

Per ulteriori informazioni sui diversi ambienti di sviluppo disponibili, consulta la documentazione della panoramica .

CRXDE Lite è incorporato in AEM e consente di eseguire attività di sviluppo standard nel browser. Con CRXDE Lite è possibile creare un progetto, creare e modificare file (come .jsp e .java), cartelle, modelli, componenti, finestre di dialogo, nodi, proprietà e bundle durante la registrazione.
CRXDE Lite è consigliato quando non si dispone dell’accesso diretto al server AEM, quando si sviluppa un’applicazione estendendo o modificando i componenti predefiniti e i bundle Java o quando non è necessario un debugger dedicato, il completamento del codice e l’evidenziazione della sintassi.

>[!NOTE]
>
>A partire dal AEM 6.5.5.0, l&#39;accesso anonimo di CRXDE Lite non è più possibile.
>Gli utenti vengono reindirizzati alla schermata di accesso.


>[!NOTE]
>
>Si consiglia di utilizzare il [AEM Developer Tools per Eclipse](/help/sites-developing/aem-eclipse.md) e [Estensione AEM parentesi graffe HTL](/help/sites-developing/aem-brackets.md) durante lo sviluppo del progetto.

## Guida introduttiva di CRXDE Lite {#getting-started-with-crxde-lite}

Per iniziare a utilizzare CRXDE Lite, procedere come segue:

1. Installa AEM.
1. Nel browser, immetti `https://<host>:<port>/crx/de`. Per impostazione predefinita, è `https://localhost:4502/crx/de`.
1. Inserisci il tuo **username** e **password**. Per impostazione predefinita `admin` e `admin`.

1. Fai clic su **OK**.

L’interfaccia utente di CRXDE Lite si presenta così nel browser:

![chlimage_1-18](assets/crx-interface.jpg)

È ora possibile utilizzare CRXDE Lite per sviluppare l’applicazione.

## Panoramica dell’interfaccia utente {#overview-of-the-user-interface}

CRXDE Lite offre le seguenti funzionalità:

<table>
 <tbody>
  <tr>
   <td>Barra di commutazione superiore</td>
   <td>Consente di passare rapidamente da CRXDE Lite, Gestione pacchetti e Condivisione pacchetti.</td>
  </tr>
  <tr>
   <td>Widget percorso nodo</td>
   <td><p>Visualizza il percorso del nodo attualmente selezionato.</p> <p>Puoi anche usarlo per saltare a un nodo, immettendo il percorso a mano, o incollandolo da un altro punto, e premendo Invio.</p> <p>Fornisce inoltre il supporto per la ricerca di nodi con un nome di nodo specifico. Inserisci il nome del nodo da trovare e attendi (o premi il simbolo di ricerca sul lato destro). Puoi provare a immettere, ad esempio, la stringa <em>quercia</em> nel widget per vedere come funziona. Se nel riquadro Esplora risorse viene caricato uno o più nodi, verrà visualizzato l'elenco, sarà possibile selezionare il percorso e premere Invio per passare a tale percorso. Si noti che funziona solo per i nodi attualmente caricati nell'applicazione client CRXDE nel browser. Se si desidera cercare l'intero archivio, utilizzare Strumenti, quindi Query.</p> </td>
  </tr>
  <tr>
   <td>Riquadro di Esplora risorse</td>
   <td><p>Visualizza una struttura ad albero di tutti i nodi della directory archivio.</p> <p>Fai clic su un nodo per visualizzarne le proprietà nel <strong>Proprietà</strong> scheda . Dopo aver fatto clic su un nodo, puoi selezionare un’azione nella barra degli strumenti. Fare nuovamente clic sul nodo per rinominarlo.</p> <p>Filtro di navigazione ad albero (icona binoculare): consente di filtrare i nodi nell’archivio per i quali il nome contiene il testo di input. Si applica solo ai nodi caricati localmente.<br /> </p> </td>
  </tr>
  <tr>
   <td>Riquadro di modifica</td>
   <td><p><strong>Pagina principale</strong> scheda: consente di cercare contenuti e/o documentazione e di accedere alle risorse per gli sviluppatori (documentazione, blog per sviluppatori, knowledge base) e al supporto (ad Adobe homepage e centro di supporto).<br /> </p> <p>Fai doppio clic su un file nel <strong>Esplora risorse</strong> per visualizzare il contenuto; come ad esempio un file .jsp o .java. Puoi quindi modificarlo e salvare le modifiche.</p> <p>Una volta modificato un file nella <strong>Modifica</strong> nella barra degli strumenti sono disponibili i seguenti strumenti:<br /> </p> - <strong>Mostra nella struttura: </strong>mostra il file nella struttura del repository.<br /> - <strong>Cerca/Sostituisci ...</strong>: eseguire ricerche o sostituire.<br /> <br /> Fare doppio clic sulla linea di stato del <strong>Modifica</strong> apre il riquadro <strong>Vai alla riga</strong> consente di immettere un numero di riga specifico a cui passare.<br /> </td>
  </tr>
  <tr>
   <td>Scheda Proprietà<br /> </td>
   <td>Visualizza le proprietà del nodo selezionato. È possibile aggiungere nuove proprietà o eliminare quelle esistenti.<br /> </td>
  </tr>
  <tr>
   <td>Scheda Controllo accesso</td>
   <td><p>Visualizza le autorizzazioni in base al percorso, al livello dell'archivio o all'entità corrente.</p> <p>Le autorizzazioni sono suddivise in</p> <p>- <strong>Criteri applicabili per il controllo degli accessi</strong>: Criteri che possono essere applicati alla selezione corrente.</p> <p>- <strong>Criteri di controllo accessi locali</strong>: I criteri correnti applicati localmente alla selezione corrente.</p> <p>- <strong>Politiche di controllo dell'accesso efficaci</strong>: I criteri correnti applicati per la selezione corrente possono essere impostati localmente o ereditati dai nodi principali.</p> <p>Nota. Per poter visualizzare le informazioni sul controllo di accesso, l'utente che ha effettuato l'accesso a CRXDE Lite deve disporre dei diritti per leggere le voci ACL. L'utente anonimo non può visualizzare queste informazioni per impostazione predefinita. Per visualizzare le informazioni, effettua l'accesso come, ad esempio, amministratore.</p> </td>
  </tr>
  <tr>
   <td>Scheda Replica</td>
   <td><p>Visualizza lo stato di replica del nodo corrente. Puoi replicare e replicare l’eliminazione del nodo corrente.</p> </td>
  </tr>
  <tr>
   <td>Scheda Console<br /> </td>
   <td><p><strong>Registri del server</strong>:</p> <p>Visualizza i messaggi dei registri. Puoi configurare il livello di registro, cancellare la console, fissare la posizione di scorrimento selezionata e abilitare/disabilitare la visualizzazione dei messaggi.<br /> </p> <p><strong>Controllo della versione</strong>:</p> <p>Visualizza i messaggi di controllo della versione.<br /> </p> </td>
  </tr>
  <tr>
   <td>Scheda Informazioni build<br /> </td>
   <td>Visualizza le informazioni quando viene generato un bundle.<br /> </td>
  </tr>
  <tr>
   <td>Aggiorna<br /> </td>
   <td>Aggiorna la selezione corrente. Le modifiche apportate da altri utenti vengono aggiornate nella visualizzazione dell’archivio. Le modifiche apportate non vengono modificate.<br /> </td>
  </tr>
  <tr>
   <td>Salva tutto</td>
   <td><p><strong>Salva tutto</strong>:<br /> </p> <p>Salva tutte le modifiche apportate. Fino a quando non fai clic su salva, le modifiche sono temporanee e andranno perse quando chiudi la console.</p> <p><strong>Versione precedente</strong>:</p> <p>Ignora tutte le modifiche apportate al nodo selezionato dall'ultima azione di salvataggio, quindi ricarica lo stato corrente dell'archivio per il nodo selezionato.</p> <p><strong>Ripristina tutto</strong>:</p> <p>Elimina tutte le modifiche apportate all’intero archivio dall’ultima azione di salvataggio, quindi ricarica lo stato corrente dell’archivio.</p> </td>
  </tr>
  <tr>
   <td>Creare ...<br /> </td>
   <td><p>Menu a discesa per creare quanto segue sotto il nodo selezionato:<br /> </p> <p>- <strong>Nodo</strong>: un nodo con un tipo di nodo arbitrario<br /> </p> <p>- <strong>File</strong>: nodo nt:file e il relativo sottonodo nt:resource</p> <p>- <strong>Cartella</strong>: nt:folder node</p> <p>- <strong>Modello</strong>: modello AEM</p> <p>- <strong>Componente</strong>: Componente AEM</p> <p>- <strong>Finestra</strong>: Finestra di dialogo AEM</p> </td>
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
   <td>Consente di aggiungere tipi mixin al tipo di nodo. I tipi di mixin vengono utilizzati principalmente per aggiungere funzioni avanzate quali controllo delle versioni, controllo degli accessi, riferimento e blocco al nodo.</td>
  </tr>
  <tr>
   <td>Strumenti<br /> </td>
   <td><p>Menu a discesa con i seguenti strumenti:</p> <p>- <strong>Configurazione server ...</strong>: per accedere alla console Felix.</p> <p>- <strong>Query in corso..</strong>: per eseguire query sul repository.</p> <p>- <strong>Privilegi ...</strong>: per aprire la gestione dei privilegi, dove puoi visualizzare e aggiungere privilegi.</p> <p>- <strong>Controllo accesso test ...</strong>: un luogo in cui è possibile verificare l'autorizzazione per un determinato percorso e/o entità principale.</p> <p>- <strong>Esporta tipo di nodo</strong>: per esportare i tipi di nodo nel sistema come notazione cnd.</p> <p>- <strong>Importa tipo di nodo ...</strong>: per importare i tipi di nodo utilizzando la notazione cnd.</p> <p>- <strong>Installa Debugger SiteCatalyst ...</strong>: istruzioni su come installare Analytics Debugger.</p> </td>
  </tr>
  <tr>
   <td>Widget di accesso<br /> </td>
   <td><p>Visualizza gli utenti attualmente connessi e l’area di lavoro a cui sono connessi, ad esempio admin@crx.default.</p> <p>Fai clic su di esso per accedere o riaccedere come utente specifico. Se non si specifica un'area di lavoro a cui accedere, si sarà connessi all'area di lavoro predefinita, crx.default.</p> <p>Se desideri sfogliare il repository come utente anonimo, utilizza <strong>anonimo</strong> come nome di accesso e qualsiasi password (ad esempio, uno spazio o un punto).<br /> </p> <p>Se l'autorizzazione non è più valida (ad esempio, è scaduta), nel widget di accesso viene visualizzato "<strong>Non autorizzato - Accesso..</strong>". Fai clic su di esso per effettuare di nuovo l’accesso.</p> </td>
  </tr>
 </tbody>
</table>

## Creazione di una cartella {#creating-a-folder}

Per creare una cartella con CRXDE Lite:

1. Apri CRXDE Lite nel browser.
1. Nel riquadro di spostamento fare clic con il pulsante destro del mouse sulla cartella in cui si desidera creare la nuova cartella, selezionare **Crea ...**, quindi **Crea cartella ...**.

1. Immettere la cartella **Nome** e fai clic su **OK**.

1. Fai clic su **Salva tutto** per salvare le modifiche sul server.

## Creazione di un modello {#creating-a-template}

Per creare un modello con CRXDE Lite:

1. Apri CRXDE Lite nel browser.
1. Nel riquadro di navigazione fare clic con il pulsante destro del mouse sulla cartella in cui si desidera creare il modello, selezionare **Crea ...**, quindi **Crea modello ...**.

1. Inserisci il **Etichetta**, **Titolo**, **Descrizione**, **Tipo di risorsa** e **Classifica** del modello. Fai clic su **Avanti**.

1. Questo passaggio è facoltativo: imposta **Percorsi consentiti**. Fai clic su **Avanti**

1. Questo passaggio è facoltativo: imposta **Genitori consentiti**. Fai clic su **Avanti**.

1. Questo passaggio è facoltativo: imposta **Bambini consentiti**. Fai clic su **OK**.

1. Fai clic su **Salva tutto** per salvare le modifiche sul server.

Crea:

* Un nodo di tipo `cq:Template` con proprietà del modello

* Un nodo figlio di tipo `cq:PageContent` con proprietà Contenuto pagina

Puoi aggiungere proprietà al modello: fare riferimento alla [Creazione di una proprietà](#creating-a-property) sezione .

## Creazione di un componente {#creating-a-component}

La funzione qui descritta è disponibile solo se CQ5 è installato, ovvero se il tipo di nodo `cq:Component` è disponibile nell’archivio.

Per creare un componente con CRXDE Lite:

1. Apri CRXDE Lite nel browser.
1. Nel riquadro di navigazione fare clic con il pulsante destro del mouse sulla cartella in cui si desidera creare il componente, selezionare **Crea ...**, quindi **Crea componente ...**.

1. Inserisci il **Etichetta**, **Titolo**, **Descrizione**, **Super tipo di risorsa** e **Gruppo** del componente. Fai clic su **Avanti**.

1. Questo passaggio è facoltativo: impostare le proprietà del componente **Contenitore** **Nessuna decorazione**, **Nome cella** e **Percorso finestra di dialogo**. Fai clic su **Avanti**.

1. Questo passaggio è facoltativo: imposta la proprietà component **Genitori consentiti**. Fai clic su **Avanti**.

1. Questo passaggio è facoltativo: imposta la proprietà component **Bambini consentiti**. Fai clic su **OK**.

1. Fai clic su **Salva tutto** per salvare le modifiche sul server.

Crea:

* Un nodo di tipo `cq:Component`
* Proprietà dei componenti
* Script .jsp di un componente

## Creazione di una finestra di dialogo {#creating-a-dialog}

Per creare una finestra di dialogo con CRXDE Lite:

1. Apri CRXDE Lite nel browser.
1. Nel riquadro di navigazione fare clic con il pulsante destro del mouse sul componente in cui si desidera creare la finestra di dialogo, selezionare **Crea ...**, quindi **Crea finestra di dialogo..**.

1. Inserisci il **Etichetta** e **Titolo**. Fai clic su **OK**.

1. Fai clic su **Salva tutto** l per salvare le modifiche sul server.

Viene creata una finestra di dialogo con la seguente struttura:

`dialog[cq:Dialog]/items[cq:Widget]/items[cq:WidgetCollection]/tab1[cq:Panel]`

È ora possibile adattare la finestra di dialogo alle proprie esigenze modificando le proprietà o creando nuovi nodi.

È inoltre possibile utilizzare l’Editor finestra di dialogo per modificare una finestra di dialogo. Fai doppio clic sul nodo della finestra di dialogo in CRXDE Lite per visualizzare l’editor. Ulteriori informazioni sull’Editor finestra di dialogo sono disponibili [qui](/help/sites-developing/dialog-editor.md).

## Creazione di un nodo {#creating-a-node}

Per creare un nodo con CRXDE Lite:

1. Apri CRXDE Lite nel browser.
1. Nel riquadro di navigazione fare clic con il pulsante destro del mouse sul nodo in cui si desidera creare il nuovo nodo, selezionare **Crea ...**, quindi **Crea nodo ...**.
1. Inserisci il **Nome** e **Tipo**. Fai clic su **OK**.
1. Fai clic su **Salva tutto** per salvare le modifiche sul server.

Ora puoi adattare il nodo alle tue esigenze modificando le proprietà o creando nuovi nodi.

>[!NOTE]
>
>La maggior parte delle operazioni di modifica, tra cui Crea nodo, conserva tutte le modifiche nella memoria e le memorizza solo al momento del salvataggio (tramite il pulsante &quot;Salva tutto&quot;). Tuttavia, alcune operazioni come lo spostamento vengono mantenute automaticamente.
>
>La convalida relativa al fatto che il nodo appena creato sia consentito dal tipo di nodo del nodo principale viene eseguita anche dall&#39;archivio JCR prima di salvare le modifiche. Se ricevi un messaggio di errore durante il salvataggio di un nodo, controlla se la struttura del contenuto è valida (ad esempio, non puoi creare un `nt:unstructured` come nodo figlio di `nt:folder` node).

## Creazione di una proprietà {#creating-a-property}

Per creare una proprietà con CRXDE Lite:

1. Apri CRXDE Lite nel browser.
1. Nel riquadro di navigazione selezionare il nodo in cui si desidera aggiungere la nuova proprietà.
1. In **Proprietà** nel riquadro inferiore, immetti la **Nome**, **Tipo** e **Valore**. Fate clic su **Aggiungi**.

1. Fai clic su **Salva tutto** per salvare le modifiche sul server.

## Creazione di uno script {#creating-a-script}

Per creare un nuovo script:

1. Apri CRXDE Lite nel browser.
1. Nel riquadro di navigazione fare clic con il pulsante destro del mouse sul componente in cui si desidera creare lo script, selezionare **Crea ...**, quindi **Crea file ...**.

1. Inserisci il file **Nome** compresa la sua estensione. Fai clic su **OK**.

1. Il nuovo file viene aperto come scheda nel riquadro Modifica.
1. Modifica il file.
1. Fai clic su **Salva tutto** per salvare le modifiche.

## Esportazione e importazione di tipi di nodo {#exporting-and-importing-node-types}

Con CRXDE Lite è possibile importare e/o esportare le definizioni dei tipi di nodo in [Notazione CND (Compact Namespace and Node Type Definition)](https://jackrabbit.apache.org/jcr/node-type-notation.html).

Per esportare una definizione del tipo di nodo:

1. Apri CRXDE Lite nel browser.
1. Seleziona il nodo richiesto.
1. Seleziona **Strumenti** then **Esporta tipo di nodo**.

1. La definizione, nella notazione del cnd, verrà visualizzata nel browser. Se necessario, salva le informazioni.

Per importare una definizione del tipo di nodo:

1. Apri CRXDE Lite nel browser.
1. Seleziona **Strumenti** then **Importa tipo di nodo...**.

1. Immettere la notazione CND per la definizione nella casella di testo.
1. Controlla **Consenti aggiornamento** se stai aggiornando una definizione esistente.
1. Fai clic su **Importa**.

## Registrazione {#logging}

Con CRXDE Lite è possibile visualizzare il file `error.log` che si trova nel file system in `<crx-install-dir>/crx-quickstart/server/logs` e filtrarlo con il livello di log appropriato. Procedere come segue:

1. Apri CRXDE Lite nel browser.
1. In **Console** scheda nella parte inferiore della finestra, nel menu a discesa a destra, selezionare **Registri server**.

1. Fai clic sul pulsante **Interrompi** per visualizzare i messaggi.

Operazioni disponibili:

* Per regolare i parametri di registro nella console Felix, fai clic sul pulsante **Configurazioni di registrazione** icona.
* Cancella i messaggi facendo clic sul pulsante **Pennello** icona.
* Aggiungi il messaggio alla selezione corrente facendo clic sul pulsante **Pin** icona.
* Attiva o disattiva la visualizzazione dei messaggi facendo clic sul pulsante **Interrompi** icona.

## Controllo accesso {#access-control}

>[!NOTE]
>
>Vedi [Amministrazione di utenti, gruppi e diritti di accesso](/help/sites-administering/user-group-ac-admin.md) per ulteriori informazioni.
