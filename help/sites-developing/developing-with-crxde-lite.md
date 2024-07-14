---
title: Sviluppo con CRXDE Lite
description: CRXDE Lite è incorporato in Adobe Experience Manager (AEM) e consente di eseguire attività di sviluppo standard nel browser
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
docset: aem65
exl-id: 9e88ca55-ac3d-4857-b6b2-aeb732562664
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '2118'
ht-degree: 1%

---

# Sviluppo con CRXDE Lite{#developing-with-crxde-lite}

Questa sezione descrive come sviluppare l’applicazione Adobe Experience Manager (AEM) utilizzando CRXDE Lite.

Per ulteriori informazioni sui diversi ambienti di sviluppo disponibili, consulta la documentazione della panoramica.

CRXDE Lite è incorporato nell’AEM e consente di eseguire attività di sviluppo standard nel browser. Con CRXDE Lite puoi creare un progetto, creare e modificare file (come .jsp e .java), cartelle, modelli, componenti, finestre di dialogo, nodi, proprietà e bundle durante la registrazione.
CRXDE Lite è consigliato quando non si dispone di accesso diretto al server AEM. Oppure, quando sviluppi un’applicazione estendendo o modificando i componenti predefiniti e i bundle Java™, oppure quando non hai bisogno di un debugger dedicato, del completamento del codice e dell’evidenziazione della sintassi.

>[!NOTE]
>
>A partire dalla versione 6.5.5.0 dell&#39;AEM, l&#39;accesso anonimo alla CRXDE Liti non è più possibile.
>Gli utenti vengono reindirizzati alla schermata di accesso.


>[!NOTE]
>
>L&#39;Adobe consiglia di utilizzare [Strumenti per sviluppatori AEM per Eclipse](/help/sites-developing/aem-eclipse.md) e l&#39;estensione per parentesi HTL [AEM](/help/sites-developing/aem-brackets.md) durante lo sviluppo del progetto.

## Guida introduttiva di CRXDE Lite {#getting-started-with-crxde-lite}

Per iniziare a utilizzare CRXDE Lite, procedere come segue:

1. Installare AEM.
1. Nel browser immettere `https://<host>:<port>/crx/de`. Per impostazione predefinita è `https://localhost:4502/crx/de`.
1. Immetti **username** e **password**. Per impostazione predefinita sono `admin` e `admin`.

1. Fai clic su **OK**.

L’interfaccia utente di CRXDE Lite si presenta come segue nel browser:

![chlimage_1-18](assets/crx-interface.jpg)

Ora puoi utilizzare CRXDE Lite per sviluppare l’applicazione.

## Panoramica dell’interfaccia utente {#overview-of-the-user-interface}

CRXDE Lite offre le seguenti funzionalità:

<table>
 <tbody>
  <tr>
   <td>Barra del commutatore superiore</td>
   <td>Passaggio rapido tra CRXDE Lite, Gestione pacchetti e Condivisione pacchetti.</td>
  </tr>
  <tr>
   <td>Widget percorso nodo</td>
   <td><p>Visualizza il percorso del nodo selezionato.</p> <p>Puoi anche utilizzarlo per passare a un nodo, immettendo manualmente il percorso o incollandolo da un’altra posizione e premendo Invio.</p> <p>Fornisce inoltre supporto per la ricerca di nodi con un nome di nodo specifico. Inserisci il nome del nodo che desideri trovare e attendi (o premi il simbolo di ricerca sul lato destro). Prova a immettere, ad esempio, la stringa <em>oak</em> nel widget per vedere come funziona. Se uno o più nodi vengono caricati nel riquadro dell'elenco delle cartelle, viene visualizzato l'elenco e puoi selezionare il percorso e premere Invio per individuarlo. Funziona solo per i nodi caricati nell’applicazione client CRXDE nel browser. Se si desidera eseguire una ricerca nell'intero repository, utilizzare Strumenti, quindi Query.</p> </td>
  </tr>
  <tr>
   <td>Riquadro di Explorer</td>
   <td><p>Visualizza una struttura di tutti i nodi del repository.</p> <p>Fai clic su un nodo per visualizzarne le proprietà nella scheda <strong>Proprietà</strong>. Dopo aver fatto clic su un nodo, puoi selezionare un’azione nella barra degli strumenti. Fai di nuovo clic sul nodo per rinominarlo.</p> <p>Filtro navigazione albero (icona binoculare): consente di filtrare i nodi nell’archivio per i quali il nome contiene il testo di input. Si applica solo ai nodi che sono stati caricati localmente.<br /> </p> </td>
  </tr>
  <tr>
   <td>Riquadro di modifica</td>
   <td><p>Scheda <strong>Home</strong>: consente di cercare contenuti e/o documentazione e di accedere alle risorse per sviluppatori (documentazione, blog per sviluppatori, knowledge base) e al supporto (home page e centro di supporto di Adobe).<br /> </p> <p>Fare doppio clic su un file nel riquadro <strong>Explorer</strong> per visualizzarne il contenuto. Ad esempio, un file .jsp o .java. Puoi quindi modificarlo e salvare le modifiche.</p> <p>Dopo aver modificato un file nel riquadro <strong>Modifica</strong>, nella barra degli strumenti sono disponibili i seguenti strumenti:<br /> </p> - <strong>Mostra nella struttura: </strong>mostra il file nella struttura dell'archivio.<br /> - <strong>Ricerca/Sostituisci ...</strong>: eseguire la ricerca o la sostituzione.<br /> <br /> Fare doppio clic sulla riga di stato del riquadro <strong>Modifica</strong> per aprire la finestra di dialogo <strong>Vai alla riga</strong>, in modo da poter immettere un numero di riga specifico da utilizzare.<br /> </td>
  </tr>
  <tr>
   <td>Scheda Proprietà<br /> </td>
   <td>Visualizza le proprietà del nodo selezionato. È possibile aggiungere nuove proprietà o eliminare quelle esistenti.<br /> </td>
  </tr>
  <tr>
   <td>Scheda Controllo di accesso</td>
   <td><p>Visualizza le autorizzazioni in base al percorso, al livello di archivio o all’entità principale.</p> <p>Le autorizzazioni sono suddivise in</p> <p>- <strong>Criteri di controllo di accesso applicabili</strong>: i criteri che possono essere applicati alla selezione.</p> <p>- <strong>Criteri di controllo di accesso locali</strong>: criteri applicati localmente alla selezione.</p> <p>- <strong>Criteri di controllo di accesso effettivi</strong>: i criteri applicati per la selezione potrebbero essere impostati localmente o ereditati dai nodi padre.</p> <p>Nota. Per poter visualizzare le informazioni sul controllo di accesso, l'utente connesso a CRXDE Lite deve disporre dei diritti di lettura per le voci ACL. Per impostazione predefinita, l’utente anonimo non può visualizzare queste informazioni; ad esempio, effettua l’accesso come amministratore.</p> </td>
  </tr>
  <tr>
   <td>Scheda Replica</td>
   <td><p>Visualizza lo stato di replica del nodo. Puoi replicare e replicare l’eliminazione del nodo.</p> </td>
  </tr>
  <tr>
   <td>Scheda Console<br /> </td>
   <td><p><strong>Registri server</strong>:</p> <p>Visualizza i messaggi dei registri. È possibile configurare il livello di log, cancellare la console, fissare la posizione di scorrimento selezionata e abilitare o disabilitare la visualizzazione dei messaggi.<br /> </p> <p><strong>Controllo versione</strong>:</p> <p>Visualizza i messaggi di controllo della versione.<br /> </p> </td>
  </tr>
  <tr>
   <td>Scheda Informazioni compilazione<br /> </td>
   <td>Visualizza informazioni durante la generazione di un bundle.<br /> </td>
  </tr>
  <tr>
   <td>Aggiorna<br /> </td>
   <td>Aggiorna la selezione. Le modifiche apportate da altri utenti vengono aggiornate nella vista dell’archivio. Le modifiche apportate non hanno effetto.<br /> </td>
  </tr>
  <tr>
   <td>Salva tutto</td>
   <td><p><strong>Salva tutto</strong>:<br /> </p> <p>Salva tutte le modifiche apportate. Fino a quando non fai clic su Salva, le modifiche sono temporanee e vengono perse quando esci dalla console.</p> <p><strong>Ripristina</strong>:</p> <p>Elimina tutte le modifiche apportate al nodo selezionato dall'ultima azione di salvataggio, quindi ricarica lo stato dell'archivio per il nodo selezionato.</p> <p><strong>Ripristina tutto</strong>:</p> <p>Elimina tutte le modifiche apportate in tutto l'archivio dall'ultima azione di salvataggio, quindi ricarica lo stato dell'archivio.</p> </td>
  </tr>
  <tr>
   <td>Crea ...<br /> </td>
   <td><p>Menu a discesa per creare i seguenti elementi nel nodo selezionato:<br /> </p> <p>- <strong>Nodo</strong>: nodo con tipo di nodo arbitrario<br /> </p> <p>- <strong>File</strong>: nodo nt:file e relativo sottonodo nt:resource</p> <p>- <strong>Cartella</strong>: nt:folder node</p> <p>- <strong>Modello</strong>: modello AEM</p> <p>- <strong>Componente</strong>: componente AEM</p> <p>- <strong>Finestra di dialogo</strong>: finestra di dialogo AEM</p> </td>
  </tr>
  <tr>
   <td>Elimina<br /> </td>
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
   <td>Sposta...<br /> </td>
   <td>Sposta il nodo selezionato sul nodo impostato tramite la finestra di dialogo.</td>
  </tr>
  <tr>
   <td>Rinomina ...<br /> </td>
   <td>Rinomina il nodo selezionato.<br /> </td>
  </tr>
  <tr>
   <td>Mixin ...<br /> </td>
   <td>Consente di aggiungere tipi mixin al tipo di nodo. I tipi mixin vengono utilizzati principalmente per aggiungere funzioni avanzate come il controllo delle versioni, il controllo degli accessi, i riferimenti e il blocco al nodo.</td>
  </tr>
  <tr>
   <td>Strumenti<br /> </td>
   <td><p>Menu a discesa con i seguenti strumenti:</p> <p>- <strong>Configurazione server ...</strong>: per accedere alla console Felix.</p> <p>- <strong>Query ...</strong>: per eseguire una query nell'archivio.</p> <p>- <strong>Privilegi ...</strong>: per aprire Gestione privilegi, in cui è possibile visualizzare e aggiungere privilegi.</p> <p>- <strong>Verifica controllo dell'accesso ...</strong>: posizione in cui è possibile verificare l'autorizzazione per un determinato percorso e/o entità.</p> <p>- <strong>Esporta tipo di nodo</strong>: per esportare i tipi di nodo nel sistema come notazione cnd.</p> <p>- <strong>Importa tipo di nodo ...</strong>: per importare tipi di nodo utilizzando la notazione cnd.</p> <p>- <strong>Installare Debugger di SiteCatalyst ...</strong>: istruzioni sull'installazione di Analytics Debugger.</p> </td>
  </tr>
  <tr>
   <td>Widget di accesso<br /> </td>
   <td><p>Visualizza gli utenti connessi e l'area di lavoro a cui hanno effettuato l'accesso, ad esempio admin@crx.default.</p> <p>Fai clic su di esso per accedere o accedere nuovamente come utente specifico. Se non si specifica un'area di lavoro a cui accedere, viene eseguito l'accesso all'area di lavoro predefinita crx.default.</p> <p>Se desideri sfogliare il repository come utente anonimo, utilizza <strong>anonimo</strong> come nome di accesso e qualsiasi password (ad esempio, uno spazio o un punto).<br /> </p> <p>Se l'autorizzazione non è più valida (ad esempio è scaduta), nel widget di accesso verrà visualizzato "<strong>Non autorizzato - Accesso...</strong>". Fai clic su di esso per accedere di nuovo.</p> </td>
  </tr>
 </tbody>
</table>

## Creazione di una cartella {#creating-a-folder}

Per creare una cartella con CRXDE Lite:

1. Apri CRXDE Lite nel browser.
1. Nel riquadro di spostamento fare clic con il pulsante destro del mouse sulla cartella in cui si desidera creare la cartella, selezionare **Crea ...**, quindi **Crea cartella ...**.

1. Immettere la cartella **Name** e fare clic su **OK**.

1. Fai clic su **Salva tutto** per salvare le modifiche sul server.

## Creazione di un modello {#creating-a-template}

Per creare un modello con CRXDE Lite:

1. Apri CRXDE Lite nel browser.
1. Nel riquadro di spostamento fare clic con il pulsante destro del mouse sulla cartella in cui si desidera creare il modello, selezionare **Crea ...**, quindi **Crea modello ...**.

1. Immetti l&#39;**etichetta**, il **titolo**, la **descrizione**, il **tipo di risorsa** e la **classificazione** del modello. Fai clic su **Avanti**.

1. Questo passaggio è facoltativo: impostare **Percorsi consentiti**. Fai clic su **Avanti**

1. Questo passaggio è facoltativo: imposta **Elementi padre consentiti**. Fai clic su **Avanti**.

1. Questo passaggio è facoltativo: impostare **Elementi figlio consentiti**. Fai clic su **OK**.

1. Fai clic su **Salva tutto** per salvare le modifiche sul server.

Crea:

* Un nodo di tipo `cq:Template` con proprietà di modello

* Un nodo figlio di tipo `cq:PageContent` con proprietà Contenuto pagina

Puoi aggiungere proprietà al modello: consulta la sezione [Creazione di una proprietà](#creating-a-property).

## Creazione di un componente {#creating-a-component}

La funzionalità qui descritta è disponibile solo se è installato CQ5, ovvero se il tipo di nodo `cq:Component` è disponibile nell&#39;archivio.

Per creare un componente con CRXDE Lite:

1. Apri CRXDE Lite nel browser.
1. Nel riquadro di spostamento fare clic con il pulsante destro del mouse sulla cartella in cui si desidera creare il componente, selezionare **Crea ...**, quindi **Crea componente ...**.

1. Immetti **Etichetta**, **Titolo**, **Descrizione**, **Tipo di risorsa privilegiato** e **Gruppo** del componente. Fai clic su **Avanti**.

1. Questo passaggio è facoltativo: impostare le proprietà del componente **Contenitore Is,** **Nessuna decorazione**, **Nome cella** e **Percorso finestra di dialogo**. Fai clic su **Avanti**.

1. Questo passaggio è facoltativo: impostare la proprietà del componente **Elementi padre consentiti**. Fai clic su **Avanti**.

1. Questo passaggio è facoltativo: impostare la proprietà del componente **Elementi figlio consentiti**. Fai clic su **OK**.

1. Fai clic su **Salva tutto** per salvare le modifiche sul server.

Crea:

* Un nodo di tipo `cq:Component`
* Proprietà componente
* Script .jsp di un componente

## Creazione di una finestra di dialogo {#creating-a-dialog}

Per creare una finestra di dialogo con CRXDE Lite:

1. Apri CRXDE Lite nel browser.
1. Nel riquadro di spostamento fare clic con il pulsante destro del mouse sul componente in cui si desidera creare la finestra di dialogo, selezionare **Crea ...**, quindi **Crea finestra di dialogo ...**.

1. Immetti **Label** e **Title**. Fai clic su **OK**.

1. Fai clic su **Salva Al** l per salvare le modifiche sul server.

Crea una finestra di dialogo con la seguente struttura:

`dialog[cq:Dialog]/items[cq:Widget]/items[cq:WidgetCollection]/tab1[cq:Panel]`

È ora possibile adattare la finestra di dialogo alle proprie esigenze modificando le proprietà o creando nodi.

Per modificare una finestra di dialogo, puoi anche utilizzare l’Editor finestre di dialogo. Facendo doppio clic sul nodo della finestra di dialogo in CRXDE Lite viene visualizzato l’editor. Ulteriori informazioni sull&#39;Editor finestre di dialogo sono disponibili [qui](/help/sites-developing/dialog-editor.md).

## Creazione di un nodo {#creating-a-node}

Per creare un nodo con CRXDE Lite:

1. Apri CRXDE Lite nel browser.
1. Nel riquadro di spostamento fare clic con il pulsante destro del mouse sul nodo in cui si desidera creare il nodo, selezionare **Crea ...**, quindi **Crea nodo ...**.
1. Immetti **Nome** e **Tipo**. Fai clic su **OK**.
1. Fai clic su **Salva tutto** per salvare le modifiche sul server.

Ora puoi adattare il nodo alle tue esigenze modificando le proprietà o creando nodi.

>[!NOTE]
>
>La maggior parte delle operazioni di modifica, incluso Crea nodo, mantiene tutte le modifiche in memoria e le archivia nell’archivio solo al momento del salvataggio (tramite il pulsante &quot;Salva tutto&quot;). Tuttavia, alcune operazioni, come lo spostamento, vengono mantenute automaticamente.
>
>La convalida che verifica se il nodo appena creato è consentito dal tipo di nodo del nodo principale viene eseguita prima dall’archivio JCR al momento del salvataggio delle modifiche. Se durante il salvataggio di un nodo viene visualizzato un messaggio di errore, verificare se la struttura del contenuto è valida, ad esempio non è possibile creare un nodo `nt:unstructured` come nodo figlio di `nt:folder`.

## Creazione di una proprietà {#creating-a-property}

Per creare una proprietà con CRXDE Lite:

1. Apri CRXDE Lite nel browser.
1. Nel riquadro di spostamento selezionare il nodo in cui si desidera aggiungere la nuova proprietà.
1. Nella scheda **Proprietà** nel riquadro inferiore, immettere **Nome**, **Tipo** e **Valore**. Fare clic su **Aggiungi**.

1. Fai clic su **Salva tutto** per salvare le modifiche sul server.

## Creazione di uno script {#creating-a-script}

Per creare uno script:

1. Apri CRXDE Lite nel browser.
1. Nel riquadro di spostamento fare clic con il pulsante destro del mouse sul componente in cui si desidera creare lo script, selezionare **Crea ...**, quindi **Crea file ...**.

1. Immetti il file **Name** inclusa la relativa estensione. Fai clic su **OK**.

1. Il nuovo file viene aperto come scheda nel riquadro Modifica.
1. Modifica il file.
1. Fai clic su **Salva tutto** per salvare le modifiche.

## Esportazione e importazione di tipi di nodo {#exporting-and-importing-node-types}

Con CRXDE Lite è possibile importare e/o esportare le definizioni dei tipi di nodo nella notazione [CND (Compact Namespace and Node Type Definition)](https://jackrabbit.apache.org/jcr/node-type-notation.html).

Per esportare la definizione di un tipo di nodo:

1. Apri CRXDE Lite nel browser.
1. Seleziona il nodo richiesto.
1. Selezionare **Strumenti** e quindi **Esporta tipo di nodo**.

1. La definizione, in notazione cnd, viene visualizzata nel browser. Se necessario, salva le informazioni.

Per importare una definizione di tipo di nodo:

1. Apri CRXDE Lite nel browser.
1. Seleziona **Strumenti** e poi **Importa tipo di nodo...**.

1. Immettere la notazione CND per la definizione nella casella di testo.
1. Selezionare **Consenti aggiornamento** se si sta aggiornando una definizione esistente.
1. Fai clic su **Importa**.

## Registrazione {#logging}

Con CRXDE Lite è possibile visualizzare il file `error.log` presente nel file system in `<crx-install-dir>/crx-quickstart/server/logs` e filtrarlo con il livello di registro appropriato. Procedere come segue:

1. Apri CRXDE Lite nel browser.
1. Nella scheda **Console** nella parte inferiore della finestra, seleziona **Registri server** nel menu a discesa a destra.

1. Fai clic sull&#39;icona **Interrompi** per visualizzare i messaggi.

Operazioni disponibili:

* Regola i parametri di registro nella console Felix facendo clic sull&#39;icona **Configurazioni di registrazione**.
* Cancellare i messaggi facendo clic sull&#39;icona **Pennello**.
* Fissare il messaggio alla selezione facendo clic sull&#39;icona **Fissa**.
* Attiva o disattiva la visualizzazione dei messaggi facendo clic sull&#39;icona **Interrompi**.

## Controllo accesso {#access-control}

>[!NOTE]
>
>Per ulteriori informazioni, vedere [Utenti, gruppi e amministrazione dei diritti di accesso](/help/sites-administering/user-group-ac-admin.md).
