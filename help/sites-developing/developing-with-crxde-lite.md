---
title: Sviluppo con CRXDE Lite
seo-title: Sviluppo con CRXDE Lite
description: CRXDE Lite è integrato in AEM e consente di eseguire attività di sviluppo standard nel browser
seo-description: CRXDE Lite è integrato in AEM e consente di eseguire attività di sviluppo standard nel browser
uuid: f4890354-d8b8-4fb9-af2f-3359f931f883
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 4537c1fb-f99c-42e2-a222-b037794bdb52
docset: aem65
translation-type: tm+mt
source-git-commit: cb141914428f42a9755b5479ab1652c8ca51f640
workflow-type: tm+mt
source-wordcount: '2155'
ht-degree: 2%

---


# Sviluppo con CRXDE Lite{#developing-with-crxde-lite}

Questa sezione descrive come sviluppare l&#39;applicazione AEM utilizzando CRXDE Lite.

Per ulteriori informazioni sui diversi ambienti di sviluppo disponibili, consulta la documentazione di panoramica.

CRXDE Lite è integrato in AEM e consente di eseguire attività di sviluppo standard nel browser. Con i CRXDE Lite, potete creare un progetto, creare e modificare file (come .jsp e .java), cartelle, modelli, componenti, finestre di dialogo, nodi, proprietà e bundle durante la registrazione.
CRXDE Lite è consigliato quando non si dispone dell&#39;accesso diretto al server AEM, quando si sviluppa un&#39;applicazione estendendo o modificando i componenti out-of-the-box e i bundle Java o quando non è necessario un debugger dedicato, completamento del codice e evidenziazione della sintassi.

>[!NOTE]
>
>A partire dal AEM 6.5.5.0, l&#39;accesso anonimo di CRXDE Lite non è più possibile.
>Gli utenti vengono reindirizzati alla schermata di accesso.


>[!NOTE]
>
>È consigliabile utilizzare [AEM Developer Tools for Eclipse](/help/sites-developing/aem-eclipse.md) e [AEM HTL Brackets Extension](/help/sites-developing/aem-brackets.md) durante lo sviluppo del progetto.

## Guida introduttiva all&#39;CRXDE Lite {#getting-started-with-crxde-lite}

Per iniziare con CRXDE Lite, procedere come segue:

1. Installare AEM.
1. Nel browser, immettere `https://<host>:<port>/crx/de`. Per impostazione predefinita è `https://localhost:4502/crx/de`.
1. Immettere **username** e **password**. Per impostazione predefinita è `admin` e `admin`.

1. Fai clic su **OK**.

L’interfaccia utente CRXDE Lite si presenta come segue nel browser:

![chlimage_1-18](assets/crx-interface.jpg)

È ora possibile utilizzare CRXDE Lite per sviluppare l&#39;applicazione.

## Panoramica dell&#39;interfaccia utente {#overview-of-the-user-interface}

CRXDE Lite offre le seguenti funzionalità:

<table>
 <tbody>
  <tr>
   <td>Barra di commutazione superiore</td>
   <td>Consente di passare rapidamente da CRXDE Lite, Package Manager e Package Share.</td>
  </tr>
  <tr>
   <td>Widget percorso nodo</td>
   <td><p>Visualizza il percorso del nodo attualmente selezionato.</p> <p>Potete anche utilizzarlo per passare a un nodo, immettendo il percorso a mano, o incollandolo da un'altra posizione, e premendo Invio.</p> <p>Fornisce inoltre supporto per la ricerca di nodi con un nome di nodo specifico. Inserite il nome del nodo da trovare e attendete (o toccate il simbolo di ricerca sul lato destro). Potete provare a inserire, ad esempio, la stringa <em>quercia</em> nel widget per vedere come funziona. Se un determinato nodo o nodi viene caricato nel riquadro di esplorazione, verrà visualizzato l'elenco, quindi sarà possibile selezionare il percorso e premere Invio per passare a tale percorso. Si noti che funziona solo per i nodi attualmente caricati nell'applicazione client CRXDE nel browser. Se si desidera eseguire una ricerca nell'intero repository, utilizzare Strumenti, quindi Query.</p> </td>
  </tr>
  <tr>
   <td>Riquadro di Esplora risorse</td>
   <td><p>Visualizza una struttura ad albero di tutti i nodi della directory archivio.</p> <p>Fare clic su un nodo per visualizzarne le proprietà nella scheda <strong>Proprietà</strong>. Dopo aver fatto clic su un nodo, è possibile selezionare un'azione nella barra degli strumenti. Fare di nuovo clic sul nodo per rinominarlo.</p> <p>Filtro di navigazione albero (icona binoculare): consente di filtrare i nodi della directory archivio per i quali il nome contiene il testo di input. Si applica solo ai nodi caricati localmente.<br /> </p> </td>
  </tr>
  <tr>
   <td>Riquadro di modifica</td>
   <td><p><strong></strong> Hometab: consente di effettuare ricerche nei contenuti e/o nella documentazione e di accedere alle risorse per gli sviluppatori (documentazione, blog per sviluppatori, knowledge base) e al supporto ( pagina iniziale e centro di assistenza).<br /> </p> <p>Fare doppio clic su un file nel riquadro <strong>Esplora risorse</strong> per visualizzarne il contenuto; come ad esempio un file .jsp o .java. Potete quindi modificarlo e salvare le modifiche.</p> <p>Dopo aver modificato un file nel riquadro <strong>Modifica</strong>, nella barra degli strumenti sono disponibili i seguenti strumenti:<br /> </p> - <strong>Mostra nella struttura: </strong>mostra il file nella struttura del repository.<br /> -  <strong>Cerca/Sostituisci ...</strong>: eseguire ricerche o sostituire.<br /> <br /> Fate doppio clic sulla riga di stato del riquadro  <strong></strong> Editpane per aprire la finestra di dialogo  <strong>Vai a </strong> linea, in modo da immettere un numero di riga specifico a cui passare.<br /> </td>
  </tr>
  <tr>
   <td>scheda Proprietà<br /> </td>
   <td>Visualizza le proprietà del nodo selezionato. È possibile aggiungere nuove proprietà o eliminare quelle esistenti.<br /> </td>
  </tr>
  <tr>
   <td>Scheda Controllo accesso</td>
   <td><p>Visualizza le autorizzazioni in base al percorso, al livello del repository o all'entità corrente.</p> <p>Le autorizzazioni sono suddivise in</p> <p>- <strong>Criterio di controllo degli accessi applicabile</strong>: Criteri che possono essere applicati alla selezione corrente.</p> <p>- <strong>Criteri per il controllo degli accessi locali</strong>: Criteri correnti applicati localmente alla selezione corrente.</p> <p>- <strong>Criteri di controllo di accesso effettivi</strong>: I criteri correnti applicati alla selezione corrente possono essere impostati localmente o ereditati dai nodi padre.</p> <p>Nota. Per poter visualizzare le informazioni sul controllo di accesso, l'utente che ha eseguito l'accesso al CRXDE Lite deve disporre dei diritti per la lettura delle voci ACL. L'utente anonimo non può visualizzare queste informazioni per impostazione predefinita. Per visualizzare le informazioni, effettuate l'accesso, ad esempio, come amministratore.</p> </td>
  </tr>
  <tr>
   <td>Scheda Replica</td>
   <td><p>Visualizza lo stato di replica del nodo corrente. È possibile replicare e replicare l'eliminazione del nodo corrente.</p> </td>
  </tr>
  <tr>
   <td>Scheda Console<br /> </td>
   <td><p><strong>Registri del server</strong>:</p> <p>Visualizza i messaggi dei registri. È possibile configurare il livello di registro, cancellare la console, fissare la posizione di scorrimento selezionata e attivare/disattivare la visualizzazione dei messaggi.<br /> </p> <p><strong>Controllo della versione</strong>:</p> <p>Visualizza i messaggi relativi al controllo delle versioni.<br /> </p> </td>
  </tr>
  <tr>
   <td>Scheda Informazioni build<br /> </td>
   <td>Visualizza informazioni durante la creazione di un bundle.<br /> </td>
  </tr>
  <tr>
   <td>Aggiorna<br /> </td>
   <td>Aggiorna la selezione corrente. Le modifiche apportate da altri utenti vengono aggiornate nella visualizzazione della directory archivio. Le modifiche apportate non vengono applicate.<br /> </td>
  </tr>
  <tr>
   <td>Salva tutto</td>
   <td><p><strong>Salva tutto</strong>:<br /> </p> <p>Salva tutte le modifiche apportate. Fino a quando non si fa clic su Salva, le modifiche sono temporanee e andranno perse quando si esce dalla console.</p> <p><strong>Versione precedente</strong>:</p> <p>Ignora tutte le modifiche apportate al nodo selezionato dall'ultima azione di salvataggio, quindi ricarica lo stato corrente del repository per il nodo selezionato.</p> <p><strong>Ripristina tutto</strong>:</p> <p>Elimina tutte le modifiche apportate all’intero repository dall’ultima azione di salvataggio, quindi ricarica lo stato corrente dell’archivio.</p> </td>
  </tr>
  <tr>
   <td>Crea ...<br /> </td>
   <td><p>Menu a discesa per creare quanto segue sotto il nodo selezionato:<br /> </p> <p>- <strong>Node</strong>: un nodo con un tipo di nodo arbitrario<br /> </p> <p>- <strong>File</strong>: nt:nodo file e relativo nodo secondario nt:resource</p> <p>- <strong>Cartella</strong>: nt:folder, nodo</p> <p>- <strong>Modello</strong>: modello AEM</p> <p>- <strong>Componente</strong>: Componente AEM</p> <p>- <strong>Finestra di dialogo</strong>: AEM, finestra di dialogo</p> </td>
  </tr>
  <tr>
   <td>Elimina<br /> </td>
   <td>Elimina il nodo selezionato.<br /> </td>
  </tr>
  <tr>
   <td>Copia</td>
   <td>Copia il nodo selezionato.<br /> </td>
  </tr>
  <tr>
   <td>Incolla<br /> </td>
   <td>Incolla il nodo copiato sotto il nodo selezionato.<br /> </td>
  </tr>
  <tr>
   <td>Sposta ...<br /> </td>
   <td>Sposta il nodo selezionato nel nodo impostato attraverso la finestra di dialogo.</td>
  </tr>
  <tr>
   <td>Rinomina ...<br /> </td>
   <td>Rinomina il nodo selezionato.<br /> </td>
  </tr>
  <tr>
   <td>Mixin...<br /> </td>
   <td>Consente di aggiungere tipi di mixin al tipo di nodo. I tipi di mixin vengono utilizzati principalmente per aggiungere al nodo funzioni avanzate quali controllo delle versioni, controllo degli accessi, riferimenti e blocco.</td>
  </tr>
  <tr>
   <td>Strumenti<br /> </td>
   <td><p>Menu a discesa con i seguenti strumenti:</p> <p>- <strong>Configurazione server ...</strong>: per accedere alla console Felix.</p> <p>- <strong>Query ...</strong>: per eseguire una query nell'archivio.</p> <p>- <strong>Privilegi ...</strong>: per aprire la gestione dei privilegi, dove puoi visualizzare e aggiungere privilegi.</p> <p>- <strong>Controllo di accesso alla prova ...</strong>: un luogo in cui è possibile verificare l'autorizzazione per determinati percorsi e/o entità.</p> <p>- <strong>Tipo di nodo di esportazione</strong>: per esportare i tipi di nodi nel sistema come notazione cnd.</p> <p>- <strong>Importa tipo di nodo ...</strong>: per importare i tipi di nodo utilizzando la notazione cnd.</p> <p>- <strong>Installare il debugger di SiteCatalyst ...</strong>: istruzioni su come installare Analytics Debugger.</p> </td>
  </tr>
  <tr>
   <td>Widget di accesso<br /> </td>
   <td><p>Visualizza gli utenti attualmente connessi e l’area di lavoro in cui sono connessi, ad esempio admin@crx.default.</p> <p>Fate clic su di esso per accedere o effettuare nuovamente l'accesso come utente specifico. Se non specificate un'area di lavoro a cui accedere, vi verrà eseguito l'accesso all'area di lavoro predefinita, crx.default.</p> <p>Se si desidera sfogliare l'archivio come utente anonimo, utilizzare <strong>anonimo</strong> come nome di login e qualsiasi password (ad esempio, uno spazio o un punto).<br /> </p> <p>Se l'autorizzazione non è più valida (ad esempio, è scaduta), nel widget di accesso viene visualizzato "<strong>Non autorizzato - Accesso...</strong>". Fate clic su di esso per effettuare nuovamente l'accesso.</p> </td>
  </tr>
 </tbody>
</table>

## Creazione di una cartella {#creating-a-folder}

Per creare una cartella con un CRXDE Lite:

1. Aprite il CRXDE Lite nel browser.
1. Nel riquadro di navigazione, fare clic con il pulsante destro del mouse sulla cartella in cui si desidera creare la nuova cartella, selezionare **Crea ...**, quindi **Crea cartella ...**.

1. Immettere la cartella **Name** e fare clic su **OK**.

1. Fare clic su **Salva tutto** per salvare le modifiche sul server.

## Creazione di un modello {#creating-a-template}

Per creare un modello con un CRXDE Lite:

1. Aprite il CRXDE Lite nel browser.
1. Nel riquadro di navigazione, fare clic con il pulsante destro del mouse sulla cartella in cui si desidera creare il modello, selezionare **Crea ...**, quindi **Crea modello ...**.

1. Immettere **Label**, **Title**, **Description**, **Resource Type** e **Ranking** del modello. Fai clic su **Avanti**.

1. Questo passaggio è facoltativo: impostare i **Percorsi consentiti**. Fai clic su **Avanti**

1. Questo passaggio è facoltativo: impostare **Genitori consentiti**. Fai clic su **Avanti**.

1. Questo passaggio è facoltativo: impostare **Elementi secondari consentiti**. Fai clic su **OK**.

1. Fare clic su **Salva tutto** per salvare le modifiche sul server.

Crea:

* Un nodo di tipo `cq:Template` con proprietà Modello

* Un nodo figlio di tipo `cq:PageContent` con proprietà Contenuto pagina

Potete aggiungere proprietà al modello: fare riferimento alla sezione [Creazione di una proprietà](#creating-a-property).

## Creazione di un componente {#creating-a-component}

La funzione qui descritta è disponibile solo se CQ5 è installato, ovvero se il tipo di nodo `cq:Component` è disponibile nella directory archivio.

Per creare un componente con CRXDE Lite:

1. Aprite il CRXDE Lite nel browser.
1. Nel riquadro di navigazione, fare clic con il pulsante destro del mouse sulla cartella in cui si desidera creare il componente, selezionare **Crea ...**, quindi **Crea componente ...**.

1. Immettere **Label**, **Title**, **Description**, **Super Resource Type** e **Group** del componente. Fai clic su **Avanti**.

1. Questo passaggio è facoltativo: impostare le proprietà del componente **Contenitore Is,** **No Decoration**, **Cell Name** e **Dialog Path**. Fai clic su **Avanti**.

1. Questo passaggio è facoltativo: impostare la proprietà del componente **Parametri consentiti**. Fai clic su **Avanti**.

1. Questo passaggio è facoltativo: impostare la proprietà del componente **Elementi secondari consentiti**. Fai clic su **OK**.

1. Fare clic su **Salva tutto** per salvare le modifiche sul server.

Crea:

* Un nodo di tipo `cq:Component`
* Proprietà dei componenti
* Script .jsp di un componente

## Creazione di una finestra di dialogo {#creating-a-dialog}

Per creare una finestra di dialogo con un CRXDE Lite:

1. Aprite il CRXDE Lite nel browser.
1. Nel riquadro di navigazione, fare clic con il pulsante destro del mouse sul componente in cui si desidera creare la finestra di dialogo, selezionare **Crea ...**, quindi **Crea finestra di dialogo ...**.

1. Immettere **Label** e **Title**. Fai clic su **OK**.

1. Fare clic su **Salva Al** l per salvare le modifiche sul server.

Viene creata una finestra di dialogo con la struttura seguente:

`dialog[cq:Dialog]/items[cq:Widget]/items[cq:WidgetCollection]/tab1[cq:Panel]`

È ora possibile adattare la finestra di dialogo alle proprie esigenze modificando le proprietà o creando nuovi nodi.

È inoltre possibile utilizzare l&#39;Editor finestre di dialogo per modificare una finestra di dialogo. Facendo doppio clic sul nodo della finestra di dialogo nel CRXDE Lite, verrà visualizzato l&#39;editor. Ulteriori informazioni sull&#39;Editor finestra di dialogo sono disponibili [qui](/help/sites-developing/dialog-editor.md).

## Creazione di un nodo {#creating-a-node}

Per creare un nodo con CRXDE Lite:

1. Aprite il CRXDE Lite nel browser.
1. Nel riquadro di navigazione, fare clic con il pulsante destro del mouse sul nodo in cui si desidera creare il nuovo nodo, selezionare **Crea ...**, quindi **Crea nodo ...**.
1. Immettere **Name** e **Type**. Fai clic su **OK**.
1. Fare clic su **Salva tutto** per salvare le modifiche sul server.

È ora possibile adattare il nodo alle proprie esigenze modificando le proprietà o creando nuovi nodi.

>[!NOTE]
>
>La maggior parte delle operazioni di modifica, incluso Create Node, conserva tutte le modifiche in memoria e le memorizza nella directory archivio solo al momento del salvataggio (tramite il pulsante &quot;Save All&quot;). Tuttavia, alcune operazioni come quella di spostamento vengono automaticamente mantenute.
>
>La convalida relativa all&#39;eventuale autorizzazione del nodo appena creato da parte del tipo di nodo padre viene eseguita anche dall&#39;archivio JCR prima del salvataggio delle modifiche. Se durante il salvataggio di un nodo viene visualizzato un messaggio di errore, verificare se la struttura del contenuto è valida (ad esempio, non è possibile creare un nodo `nt:unstructured` come elemento secondario di `nt:folder` nodo).

## Creazione di una proprietà {#creating-a-property}

Per creare una proprietà con un CRXDE Lite:

1. Aprite il CRXDE Lite nel browser.
1. Nel riquadro di navigazione, selezionare il nodo in cui si desidera aggiungere la nuova proprietà.
1. Nella scheda **Proprietà** del riquadro inferiore, immettere **Nome**, **Tipo** e **Valore**. Fate clic su **Aggiungi**.

1. Fare clic su **Salva tutto** per salvare le modifiche sul server.

## Creazione di uno script {#creating-a-script}

Per creare un nuovo script:

1. Aprite il CRXDE Lite nel browser.
1. Nel riquadro di navigazione, fare clic con il pulsante destro del mouse sul componente in cui si desidera creare lo script, selezionare **Crea ...**, quindi **Crea file ...**.

1. Immettere il file **Name**, inclusa l&#39;estensione. Fai clic su **OK**.

1. Il nuovo file si apre come scheda nel riquadro Modifica.
1. Modificate il file.
1. Fare clic su **Salva tutto** per salvare le modifiche.

## Esportazione e importazione di tipi di nodo {#exporting-and-importing-node-types}

Con il CRXDE Lite è possibile importare e/o esportare le definizioni dei tipi di nodo nella notazione [CND (Compact Namespace and Node Type Definition)](https://jackrabbit.apache.org/jcr/node-type-notation.html).

Per esportare una definizione di tipo di nodo:

1. Aprite il CRXDE Lite nel browser.
1. Selezionare il nodo desiderato.
1. Selezionare **Strumenti**, quindi **Esporta tipo di nodo**.

1. La definizione, nella notazione cnd, verrà visualizzata nel browser. Se necessario, salvate le informazioni.

Per importare una definizione di tipo di nodo:

1. Aprite il CRXDE Lite nel browser.
1. Selezionare **Strumenti**, quindi **Importa tipo di nodo...**.

1. Immettete la notazione CND per la definizione nella casella di testo.
1. Selezionare **Consenti aggiornamento** se si sta aggiornando una definizione esistente.
1. Fai clic su **Importa**.

## Registrazione {#logging}

Con CRXDE Lite è possibile visualizzare il file `error.log` che si trova nel file system in `<crx-install-dir>/crx-quickstart/server/logs` e filtrarlo con il livello di registro appropriato. Procedere come segue:

1. Aprite il CRXDE Lite nel browser.
1. Nella scheda **Console** in fondo alla finestra, nel menu a discesa a destra, selezionare **Registri server**.

1. Fare clic sull&#39;icona **Stop** per visualizzare i messaggi.

Operazioni disponibili:

* Per regolare i parametri di registro nella console Felix, fai clic sull&#39;icona **Configurazioni di registrazione**.
* Cancella i messaggi facendo clic sull&#39;icona **Pennello**.
* Inserire il messaggio nella selezione corrente facendo clic sull&#39;icona **Pin**.
* Abilita o disabilita la visualizzazione dei messaggi facendo clic sull&#39;icona **Stop**.

## Controllo accesso {#access-control}

>[!NOTE]
>
>Per ulteriori informazioni, consultate [Utenti, gruppi e amministrazione dei diritti di accesso](/help/sites-administering/user-group-ac-admin.md).
