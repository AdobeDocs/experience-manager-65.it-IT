---
title: Amministrazione degli utenti e sicurezza
description: Scopri l’amministrazione degli utenti e la sicurezza in AEM.
uuid: 4512c0bf-71bf-4f64-99f6-f4fa5a61d572
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: e72da81b-4085-49b0-86c3-11ad48978a8a
docset: aem65
exl-id: 53d8c654-8017-4528-a44e-e362d8b59f82
feature: Security
source-git-commit: 3430897fc98aecbcf6cc7bf6bdc9b3df24e92366
workflow-type: tm+mt
source-wordcount: '5398'
ht-degree: 1%

---

# Amministrazione degli utenti e sicurezza{#user-administration-and-security}

Questo capitolo descrive come configurare e mantenere l&#39;autorizzazione utente e descrive anche la teoria dietro il funzionamento dell&#39;autenticazione e dell&#39;autorizzazione in AEM.

## Utenti e gruppi in AEM {#users-and-groups-in-aem}

Questa sezione descrive in dettaglio le varie entità e i concetti correlati per consentirti di configurare un concetto di gestione degli utenti facile da gestire.

### Utenti {#users}

Gli utenti accedono a AEM con il proprio account. Ogni account utente è univoco e contiene i dettagli dell&#39;account di base, insieme ai privilegi assegnati.

Gli utenti sono spesso membri di Gruppi, il che semplifica l&#39;allocazione di tali autorizzazioni e/o privilegi.

### Gruppi {#groups}

I gruppi sono raccolte di utenti o di altri gruppi o di entrambi. Queste collezioni sono tutte chiamate membri di un gruppo.

Il loro scopo principale è semplificare il processo di manutenzione riducendo il numero di entità da aggiornare, in quanto una modifica apportata a un gruppo viene applicata a tutti i membri del gruppo. I gruppi riflettono spesso:

* un ruolo all&#39;interno della domanda; ad esempio chi può navigare sul contenuto o chi può contribuire al contenuto.
* la propria organizzazione; è possibile estendere i ruoli per distinguere tra collaboratori di diversi reparti quando sono limitati a rami diversi nella struttura del contenuto.

Pertanto i gruppi tendono a rimanere stabili, mentre gli utenti arrivano e vanno più frequentemente.

Con la pianificazione e una struttura pulita, l&#39;uso dei gruppi può riflettere la vostra struttura, fornendo una panoramica chiara e un meccanismo efficiente per gli aggiornamenti.

### Utenti e gruppi incorporati {#built-in-users-and-groups}

AEM WCM installa diversi utenti e gruppi. Queste raccolte vengono visualizzate quando si accede per la prima volta alla console di sicurezza dopo l’installazione.

Nelle tabelle seguenti sono elencate tutte le voci insieme a:

* breve descrizione
* eventuali raccomandazioni sulle modifiche necessarie

*Modificare tutte le password predefinite* (se non si elimina l&#39;account stesso in determinate circostanze).

<table>
 <tbody>
  <tr>
   <td>ID utente</td>
   <td>Tipo</td>
   <td>Descrizione</td>
   <td>Consiglio</td>
  </tr>
  <tr>
   <td><p>admin</p> <p>Password predefinita: admin</p> </td>
   <td>User</td>
   <td><p>Account di amministrazione del sistema con diritti di accesso completi.</p> <p>Questo account viene utilizzato per la connessione tra AEM WCM e CRX.</p> <p>Se elimini accidentalmente questo account, viene ricreato al riavvio dell'archivio (nella configurazione predefinita).</p> <p>L’account amministratore è un requisito della piattaforma AEM. Di conseguenza, questo account non può essere eliminato.</p> </td>
   <td><p>Adobe consiglia di modificare la password predefinita per questo account utente.</p> <p>Preferibilmente all'installazione, anche se può essere fatto dopo.</p> <p>Nota: Non confondere questo account con l'account amministratore del CQ Servlet Engine.</p> </td>
  </tr>
  <tr>
   <td><p>anonimo</p> <p> </p> </td>
   <td>User</td>
   <td><p>Contiene i diritti predefiniti per l’accesso non autenticato a un’istanza. Per impostazione predefinita, questo account dispone dei diritti di accesso minimi.</p> <p>Se elimini accidentalmente questo account, viene ricreato all'avvio. Non può essere eliminato in modo permanente, ma può essere disattivato.</p> </td>
   <td>Evita di eliminare o disabilitare questo account, in quanto influisce negativamente sul funzionamento delle istanze di authoring. Se sono presenti requisiti di sicurezza che ti impongono di eliminarli, assicurati di testare correttamente gli effetti che ha sul tuo sistema prima.</td>
  </tr>
  <tr>
   <td><p>creazione</p> <p>Password predefinita: autore</p> </td>
   <td>User</td>
   <td><p>Un account autore autorizzato a scrivere su /content. Comprende i privilegi di collaboratore e surfista.</p> <p>Può essere utilizzato come webmaster in quanto ha accesso all’intera struttura /content.</p> <p>Questo account non è un utente incorporato, ma un altro utente dimostrativo di Geometrixx</p> </td>
   <td><p>L'Adobe consiglia di eliminare completamente l'account o di modificare la password predefinita.</p> <p>Preferibilmente all'installazione, anche se può essere fatto dopo.</p> </td>
  </tr>
  <tr>
   <td>amministratori</td>
   <td>Gruppo</td>
   <td><p>Gruppo che concede diritti di amministratore a tutti i membri. Solo l'amministratore è autorizzato a modificare questo gruppo.</p> <p>Dispone di diritti di accesso completi.</p> </td>
   <td>Anche se imposti un 'deny-all' su un nodo, gli amministratori possono ancora accedere al nodo</td>
  </tr>
  <tr>
   <td>content-authors</td>
   <td>Gruppo</td>
   <td><p>Gruppo responsabile della modifica dei contenuti. Richiede autorizzazioni di lettura, modifica, creazione ed eliminazione.</p> </td>
   <td>È possibile creare gruppi di autori di contenuti personalizzati con diritti di accesso specifici per il progetto, a condizione di aggiungere autorizzazioni di lettura, modifica, creazione ed eliminazione.</td>
  </tr>
  <tr>
   <td>collaboratore</td>
   <td>Gruppo</td>
   <td><p>Privilegi di base che consentono all’utente di scrivere contenuti (solo in, funzionalità).</p> <p>Non alloca privilegi alla struttura /content. Deve essere allocato per i singoli gruppi o utenti.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>utenti dam</td>
   <td>Gruppo</td>
   <td>Gruppo di riferimento preconfigurato per un utente AEM Assets tipico. I membri di questo gruppo dispongono dei privilegi appropriati per consentire il caricamento/condivisione di risorse e raccolte.</td>
   <td> </td>
  </tr>
  <tr>
   <td>tutti</td>
   <td>Gruppo</td>
   <td><p>Ogni utente in AEM è membro del gruppo tutti, anche se potresti non vedere il gruppo o la relazione di iscrizione in tutti gli strumenti.</p> <p>Questo gruppo può essere considerato come i diritti predefiniti in quanto può essere utilizzato per applicare le autorizzazioni per tutti, anche gli utenti che verranno creati in futuro.</p> </td>
   <td><p>Non modificare o eliminare il gruppo.</p> <p>La modifica di questo account ha ulteriori implicazioni in termini di sicurezza.</p> </td>
  </tr>
  <tr>
   <td>amministratori di tag</td>
   <td>Gruppo</td>
   <td>Gruppo che può modificare i tag.</td>
   <td> </td>
  </tr>
  <tr>
   <td>utenti-amministratori</td>
   <td>Gruppo</td>
   <td>Autorizza l’amministrazione degli utenti, ovvero il diritto di creare utenti e gruppi.</td>
   <td> </td>
  </tr>
  <tr>
   <td>editor di workflow</td>
   <td>Gruppo</td>
   <td>Gruppo autorizzato a creare e modificare modelli di flusso di lavoro.</td>
   <td> </td>
  </tr>
  <tr>
   <td>utenti del flusso di lavoro</td>
   <td>Gruppo</td>
   <td><p>Un utente che partecipa a un flusso di lavoro deve essere membro del gruppo utenti del flusso di lavoro. Consente all’utente di accedere a tutte le funzioni di: /etc/workflow/instances in modo che possano aggiornare l'istanza del flusso di lavoro.</p> <p>Il gruppo è incluso nell’installazione standard, ma devi aggiungere manualmente i tuoi utenti al gruppo.</p> </td>
  </tr>
 </tbody>
</table>

## Autorizzazioni in AEM {#permissions-in-aem}

AEM utilizza le ACL per determinare quali azioni può intraprendere un utente o un gruppo e dove può eseguire tali azioni.

### Autorizzazioni e ACL {#permissions-and-acls}

Le autorizzazioni definiscono chi può eseguire le azioni su una risorsa. Le autorizzazioni sono il risultato di [controllo di accesso](#access-control-lists-and-how-they-are-evaluated) valutazioni.

È possibile modificare le autorizzazioni concesse/negate a un determinato utente selezionando o deselezionando le caselle di controllo relative al singolo AEM [azioni](security.md#actions). Un segno di spunta indica che un’azione è consentita. Nessun segno di spunta indica che un’azione è negata.

La posizione del segno di spunta nella griglia indica anche le autorizzazioni disponibili per gli utenti in quali posizioni all’interno di AEM (ovvero, quali percorsi).

### Azioni {#actions}

Le azioni possono essere eseguite su una pagina (risorsa). Per ogni pagina nella gerarchia, puoi specificare quale azione l’utente può eseguire in quella pagina. [Autorizzazioni](#permissions-and-acls) consente di consentire o negare un’azione.

<table>
 <tbody>
  <tr>
   <td><strong>Azione </strong></td>
   <td><strong>Descrizione </strong></td>
  </tr>
  <tr>
   <td>Leggi</td>
   <td>L’utente può leggere la pagina e le relative pagine figlie.</td>
  </tr>
  <tr>
   <td>Modifica</td>
   <td><p>L’utente può:</p>
    <ul>
     <li>modifica il contenuto esistente sulla pagina e su qualsiasi pagina figlia.</li>
     <li>creare paragrafi sulla pagina o su qualsiasi pagina figlia.</li>
    </ul> <p>A livello di JCR, gli utenti possono modificare una risorsa modificandone le proprietà, il blocco, il controllo delle versioni, le modifiche non desiderate e dispongono di un'autorizzazione di scrittura completa sui nodi che definiscono un nodo figlio jcr:content. Ad esempio cq:Page, nt:file, cq:Asset.</p> </td>
  </tr>
  <tr>
   <td>Creare</td>
   <td><p>L’utente può:</p>
    <ul>
     <li>creare una pagina o una pagina figlia.</li>
    </ul> <p>Se <strong>modificare</strong> è negato, le sottostrutture sotto jcr:content sono escluse perché la creazione di jcr:content e dei relativi nodi figlio sono considerate una modifica della pagina. Questa regola si applica solo ai nodi che definiscono un nodo figlio jcr:content.</p> </td>
  </tr>
  <tr>
   <td>Eliminare</td>
   <td><p>L’utente può:</p>
    <ul>
     <li>eliminare i paragrafi esistenti dalla pagina o da una pagina figlia.</li>
     <li>eliminare una pagina o una pagina figlia.</li>
    </ul> <p>Se <strong>modificare</strong> viene negato l’esclusione di eventuali sottoalberi sotto jcr:content, in quanto la rimozione di jcr:content e i relativi nodi figlio sono considerati una modifica della pagina. Questa regola si applica solo ai nodi che definiscono un nodo figlio jcr:content.</p> </td>
  </tr>
  <tr>
   <td>Leggi ACL</td>
   <td>L’utente può leggere l’elenco dei controlli di accesso della pagina o delle pagine figlie.</td>
  </tr>
  <tr>
   <td>Modifica ACL</td>
   <td>L’utente può modificare l’elenco dei controlli di accesso della pagina o di qualsiasi pagina figlia.</td>
  </tr>
  <tr>
   <td>Replica</td>
   <td>L’utente può replicare il contenuto in un altro ambiente (ad esempio, nell’ambiente di pubblicazione). Il privilegio viene applicato anche a qualsiasi pagina figlia.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>AEM genera automaticamente i gruppi di utenti per l’assegnazione dei ruoli (Proprietario, Editor, Visualizzatore) in [Raccolte](/help/assets/manage-collections.md). Tuttavia, l&#39;aggiunta manuale di ACL per tali gruppi può introdurre vulnerabilità di sicurezza in AEM. Adobe consiglia di evitare di aggiungere manualmente ACL.

### Elenchi di controllo accessi e modalità di valutazione {#access-control-lists-and-how-they-are-evaluated}

AEM WCM utilizza gli elenchi di controllo accessi (ACL, Access Control List) per organizzare le autorizzazioni applicate alle varie pagine.

Gli elenchi di controllo degli accessi sono costituiti dalle singole autorizzazioni e vengono utilizzati per determinare l&#39;ordine in cui tali autorizzazioni vengono applicate. L’elenco viene formato in base alla gerarchia delle pagine in esame. Tale elenco viene quindi analizzato dal basso verso l’alto fino a quando non viene trovata la prima autorizzazione appropriata per l’applicazione a una pagina.

>[!NOTE]
>
>Ci sono ACL inclusi con i campioni. È consigliabile esaminare e determinare ciò che è appropriato per le applicazioni. Per esaminare le ACL incluse, vai a **CRXDE** e seleziona la **Controllo degli accessi** scheda per i seguenti nodi:
>
>* `/etc/cloudservices`
>* `/home/users/we-retail`
>
>L&#39;applicazione personalizzata può impostare l&#39;accesso per altre relazioni, ad esempio:
>
>* `*/social/relationships/friend/*`
>* oppure `*/social/relationships/pending-following/*`.
>
>Quando crei ACL specifici per le community, ai membri che si uniscono a tali community possono essere concesse autorizzazioni aggiuntive. Ad esempio, quando gli utenti si uniscono alle community all’indirizzo: `/content/we-retail/us/en/community`

### Stati delle autorizzazioni {#permission-states}

>[!NOTE]
>
>Per gli utenti CQ 5.3:
>
>A differenza delle versioni precedenti di CQ, **creare** e **delete** non devono più essere concessi se un utente deve solo modificare le pagine. Invece, concedi **modificare** Solo se desideri che gli utenti siano in grado di creare, modificare o eliminare componenti su pagine esistenti.
>
>Per motivi di compatibilità con le versioni precedenti, i test delle azioni non richiedono un trattamento speciale dei nodi che definiscono **jcr:content** di cui tener conto.

| **Azione** | **Descrizione** |
|---|---|
| Consenti (segno di spunta) | AEM WCM consente all’utente di eseguire l’azione su questa pagina o su qualsiasi pagina figlia. |
| Nega (nessun segno di spunta) | AEM WCM non consente all’utente di eseguire l’azione su questa pagina o su alcuna pagina figlia. |

Le autorizzazioni vengono applicate anche a qualsiasi pagina figlia.

Se un&#39;autorizzazione non viene ereditata dal nodo padre ma presenta almeno una voce locale per tale nodo, alla casella di controllo vengono aggiunti i simboli seguenti. Una voce locale è una voce creata nell&#39;interfaccia CRX 2.2 (le ACL con caratteri jolly al momento possono essere create solo in CRX.)

Per un&#39;azione in un determinato percorso:

<table>
 <tbody>
  <tr>
   <td>* (asterisco)</td>
   <td>Vi è almeno un ingresso locale (efficace o inefficace). Questi ACL con caratteri jolly sono definiti in CRX.</td>
  </tr>
  <tr>
   <td>! (punto esclamativo)</td>
   <td>Almeno una voce non ha attualmente alcun effetto.</td>
  </tr>
 </tbody>
</table>

Quando passi il cursore sopra l’asterisco o il punto esclamativo, una descrizione comandi fornisce ulteriori dettagli sulle voci dichiarate. La descrizione comando è divisa in due parti:

<table>
 <tbody>
  <tr>
   <td>Parte superiore</td>
   <td><p>Elenca le voci effettive.</p> </td>
  </tr>
  <tr>
   <td>Parte inferiore</td>
   <td>Elenca le voci non efficaci che possono avere effetti altrove nell'albero (come indicato da un attributo speciale presente con il corrispondente ACE che limita l'ambito della voce). In alternativa, si tratta di una voce il cui effetto viene revocato da un'altra voce definita nel percorso specificato o in un nodo antenato.</td>
  </tr>
 </tbody>
</table>

![chlimage_1-112](assets/chlimage_1-112.png)

>[!NOTE]
>
>Se non sono definite autorizzazioni per una pagina, tutte le azioni vengono negate.

Di seguito sono riportate le raccomandazioni sulla gestione degli elenchi di controllo accessi:

* Non assegnare le autorizzazioni direttamente agli utenti. Assegnali solo ai gruppi.

   In questo modo la manutenzione risulta più semplice, in quanto il numero di gruppi è molto inferiore al numero di utenti e anche meno volatile.

* Se desideri che un gruppo/utente sia in grado solo di modificare le pagine, non concedere loro diritti di creazione o negazione. Concedi loro solo diritti di modifica e lettura.
* Usa con cautela Deny. Per quanto possibile, utilizzare solo Consenti.

   L’utilizzo di deny può causare effetti imprevisti se le autorizzazioni vengono applicate in un ordine diverso da quello previsto. Se un utente è membro di più gruppi, le istruzioni di rifiuto di un gruppo possono annullare l&#39;istruzione Allow di un altro gruppo o viceversa. È difficile mantenere una panoramica quando si verifica una cosa del genere e può facilmente portare a risultati imprevisti, mentre Consenti assegnazioni non causano tali conflitti.

   L&#39;Adobe consiglia di utilizzare Consenti anziché Rifiuta per vedere [Best practice](#best-practices).

Prima di modificare entrambe le autorizzazioni, assicurati di capire come funzionano e come si relazionano. Vedi la documentazione CRX che illustra come AEM WCM [valuta i diritti di accesso](/help/sites-administering/user-group-ac-admin.md#how-access-rights-are-evaluated), ed esempi sulla configurazione degli elenchi di controllo accessi.

### Autorizzazioni {#permissions}

Le autorizzazioni consentono agli utenti e ai gruppi di accedere alla funzionalità AEM sulle pagine AEM.

È possibile sfogliare le autorizzazioni in base al percorso espandendo/comprimendo i nodi e tenere traccia dell&#39;ereditarietà delle autorizzazioni fino al nodo principale.

È possibile concedere o negare le autorizzazioni selezionando o deselezionando le caselle di controllo appropriate.

![cqcartolarypermissionstab](assets/cqsecuritypermissionstab.png)

### Visualizzazione di informazioni dettagliate sulle autorizzazioni {#viewing-detailed-permission-information}

Insieme alla vista a griglia, AEM fornisce una visualizzazione dettagliata delle autorizzazioni per un utente/gruppo selezionato in un determinato percorso. La visualizzazione dei dettagli fornisce ulteriori informazioni.

Oltre a visualizzare le informazioni, puoi includere o escludere l’utente o il gruppo corrente da un gruppo. Vedi [Aggiunta di utenti o gruppi durante l&#39;aggiunta di autorizzazioni](#adding-users-or-groups-while-adding-permissions). Le modifiche apportate vengono immediatamente riportate nella parte superiore della visualizzazione dettagliata.

Per accedere alla vista Dettaglio, nella **Autorizzazioni** scheda , fai clic su **Dettagli** per qualsiasi gruppo/utente e percorso selezionati.

![dettagli delle autorizzazioni](assets/permissiondetails.png)

I dettagli sono suddivisi in due parti:

<table>
 <tbody>
  <tr>
   <td>Parte superiore</td>
   <td><p>Ripete le informazioni visualizzate nella griglia ad albero. Per ogni azione, un’icona indica se l’azione è consentita o negata:</p>
    <ul>
     <li>nessuna icona = nessuna voce dichiarata</li>
     <li>(segno di spunta) = azione dichiarata (permesso)</li>
     <li>(-) = azione dichiarata (rifiuto)</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Parte inferiore</td>
   <td><p>Mostra la griglia di utenti e gruppi che esegue le seguenti operazioni:</p>
    <ul>
     <li>Dichiara una voce per il percorso specificato AND</li>
     <li>È l'operatore OR autorizzato dato un gruppo</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Impersona di un altro utente {#impersonating-another-user}

Con la [Funzionalità Impersona](/help/sites-authoring/user-properties.md#user-settings), un utente può lavorare per conto di un altro utente.

In altre parole, un account utente può specificare altri account che possono funzionare con il proprio account. Ad esempio, se l’utente-B può rappresentare l’utente-A, l’utente-B può agire utilizzando i dettagli completi dell’account utente-A.

Questa funzionalità consente agli account impersonatore di completare le attività come se stessero utilizzando l’account che stanno impersonando. Ad esempio, durante un&#39;assenza o per condividere un carico eccessivo a breve termine.

>[!NOTE]
>
>Affinché la rappresentazione funzioni per gli utenti non amministratori, è necessario che l&#39;impersonatore (nel caso precedente user-B) disponga delle autorizzazioni READ nel `/home/users` percorso.
>
>Vedi [Autorizzazioni in AEM](/help/sites-administering/security.md#permissions-in-aem).

>[!CAUTION]
>
>Se un account ne impersona un altro, è difficile vederlo. Una voce viene eseguita nel registro di controllo quando la rappresentazione inizia e termina, ma gli altri file di registro (come il registro di accesso) non contengono informazioni relative all’avvenuta rappresentazione degli eventi. Quindi, se l’utente-B rappresenta l’utente-A, tutti gli eventi hanno l’aspetto di un’esecuzione eseguita dall’utente-A.

>[!CAUTION]
>
>Il blocco di pagina può essere eseguito quando si impersona un utente. Tuttavia, una pagina bloccata in questo modo può essere sbloccata solo come utente impersonato o come utente con privilegi di amministratore.
>
>Non è consentito sbloccare le pagine bloccate impersonando l’utente che le ha boccate.

### Best practice {#best-practices}

Di seguito sono descritte le best practice per l’utilizzo di autorizzazioni e privilegi:

| Regola | Motivo |
|--- |--- |
| *Usa gruppi* | Evita di assegnare diritti di accesso in base all’utente. Questo consiglio è motivato per diversi motivi:<ul><li>Hai molti più utenti dei gruppi, quindi i gruppi semplificano la struttura.</li><li>I gruppi forniscono una panoramica su tutti gli account.</li> <li>L&#39;ereditarietà è più semplice con i gruppi.</li><li>Gli utenti vanno e vengono. I gruppi sono a lungo termine.</li></ul> |
| *Sii Positivo* | Utilizzare sempre le istruzioni Allow per specificare i diritti del gruppo (laddove possibile). Evitare di utilizzare un&#39;istruzione Rifiuta. I gruppi vengono valutati in ordine e l&#39;ordine può essere definito in modo diverso per utente. In altre parole: È possibile che il controllo sull&#39;ordine in cui le istruzioni vengono implementate e valutate sia limitato. Se si utilizzano solo le istruzioni Allow, l&#39;ordine non ha importanza. |
| *Mantieni semplice* | Investire un po&#39; di tempo e pensare quando si configura una nuova installazione ne vale la pena. L&#39;applicazione di una struttura chiara semplifica la manutenzione e l&#39;amministrazione correnti, garantendo che sia i colleghi attuali che i futuri successori possano comprendere facilmente ciò che viene implementato. |
| *Prova* | Utilizza un’installazione di test per esercitarti e accertarti di comprendere le relazioni tra i vari utenti e gruppi. |
| *Utenti/gruppi predefiniti* | Aggiorna sempre gli utenti e i gruppi predefiniti immediatamente dopo l&#39;installazione per evitare problemi di sicurezza. |

## Gestione di utenti e gruppi {#managing-users-and-groups}

Gli utenti includono le persone che utilizzano il sistema e i sistemi esterni che effettuano richieste al sistema.

Un gruppo è un insieme di utenti.

Entrambi possono essere configurati utilizzando la funzionalità Amministrazione utente della console di sicurezza.

### Accesso all’amministrazione degli utenti tramite la console di sicurezza {#accessing-user-administration-with-the-security-console}

Puoi accedere a tutti gli utenti, i gruppi e le autorizzazioni associate utilizzando la console Sicurezza. Tutte le procedure descritte in questa sezione vengono eseguite in questa finestra.

Per accedere AEM protezione WCM, effettuare una delle seguenti operazioni:

* Nella schermata introduttiva o in diverse aree di AEM, fai clic sull’icona di protezione :

![](do-not-localize/wcmtoolbar.png)

* Passa direttamente a `https://<server>:<port>/useradmin`. Assicurati di accedere a AEM come amministratore.

Viene visualizzata la finestra seguente:

![cqcartolarypage](assets/cqsecuritypage.png)

Nella struttura ad albero a sinistra sono elencati tutti gli utenti e i gruppi attualmente presenti nel sistema. È possibile selezionare le colonne desiderate, ordinare il contenuto delle colonne e persino modificare l’ordine di visualizzazione delle colonne trascinando l’intestazione della colonna in una nuova posizione.

![cqcartolarycolumncontext](assets/cqsecuritycolumncontext.png)

Le schede consentono di accedere a varie configurazioni:

<!-- ??? in table below. -->

| Tabulazione | Descrizione |
|--- |--- |
| Casella filtro | Un meccanismo per filtrare gli utenti, i gruppi o entrambi elencati. Vedi [Filtrare utenti e gruppi](#filtering-users-and-groups). |
| Nascondi utenti | Un interruttore che nasconde tutti gli utenti elencati, lasciando solo i gruppi. Vedi [Nascondere utenti e gruppi](#hiding-users-and-groups). |
| Nascondi gruppi | Un interruttore che nasconde tutti i gruppi elencati, lasciando solo gli utenti. Vedi [Nascondere utenti e gruppi](#hiding-users-and-groups). |
| Modifica | Un menu che consente di creare ed eliminare, nonché attivare e disattivare utenti o gruppi. Vedi [Creazione di utenti e gruppi](#creating-users-and-groups) e [Eliminazione di utenti e gruppi](#deleting-users-and-groups). |
| Proprietà | Elenca informazioni sull’utente o il gruppo che possono includere informazioni e-mail, una descrizione e un nome. Consente inoltre di modificare la password di un utente. Vedi [Creazione di utenti e gruppi](#creating-users-and-groups), [Modifica delle proprietà di utenti e gruppi](#modifying-user-and-group-properties) e [Modifica di una password utente](#changing-a-user-password). |
| Gruppi | Elenca tutti i gruppi a cui appartiene l&#39;utente o il gruppo selezionato. È possibile assegnare l&#39;utente o i gruppi selezionati a gruppi aggiuntivi o rimuoverli dai gruppi. Vedi [Gruppi](#adding-users-or-groups-to-a-group). |
| Membri | Disponibile solo per i gruppi. Elenca i membri di un gruppo specifico. Vedi [Membri](#members-adding-users-or-groups-to-a-group). |
| Autorizzazioni | È possibile assegnare autorizzazioni a un utente o a un gruppo. Consente di controllare quanto segue:<ul><li>Autorizzazioni relative a pagine/nodi particolari. Vedi [Impostazione delle autorizzazioni](#setting-permissions). </li><li>Autorizzazioni relative alla creazione ed eliminazione di pagine e alla modifica della gerarchia. ?? consente di: [assegnare privilegi](#settingprivileges), come la modifica gerarchica, che consente di creare ed eliminare pagine,</li><li>Autorizzazioni relative a [privilegi di replica](#setting-replication-privileges) (di solito dall’autore alla pubblicazione) in base a un percorso.</li></ul> |
| Impersonatori | Consente a un altro utente di rappresentare l’account. Utile quando un utente deve agire per conto di un altro utente. Vedi [Impersona utenti](#impersonating-another-user). |
| Preferenze | Set [preferenze per il gruppo o l&#39;utente](#setting-user-and-group-preferences). Ad esempio, le preferenze relative alla lingua. |

### Filtrare utenti e gruppi {#filtering-users-and-groups}

È possibile filtrare l’elenco immettendo un’espressione di filtro che nasconde tutti gli utenti e i gruppi che non corrispondono all’espressione. Puoi anche nascondere utenti e gruppi utilizzando la [Nascondi gruppo](#hiding-users-and-groups) pulsanti.

Per filtrare utenti o gruppi:

1. Nell’elenco ad albero a sinistra, digita l’espressione del filtro nello spazio disponibile. Ad esempio, immettendo **admin** visualizza tutti gli utenti e i gruppi contenenti questa stringa.
1. Fare clic sulla lente di ingrandimento per filtrare l’elenco.

   ![cqcartolaryfilter](assets/cqsecurityfilter.png)

1. Fai clic sul pulsante **x** per rimuovere tutti i filtri.

### Nascondere utenti e gruppi {#hiding-users-and-groups}

Nascondere utenti o gruppi è un altro modo per filtrare l’elenco di tutti gli utenti e i gruppi in un sistema. Ci sono due meccanismi di attivazione/disattivazione. Facendo clic su Nascondi utente, tutti gli utenti vengono nascosti e facendo clic su Nascondi gruppi vengono nascosti tutti i gruppi (non è possibile nascondere contemporaneamente utenti e gruppi). Per filtrare l’elenco utilizzando un’espressione di filtro, vedi [Filtrare utenti e gruppi](#filtering-users-and-groups).

Per nascondere utenti e gruppi:

1. In **Sicurezza** console, fai clic su **Nascondi utenti** o **Nascondi gruppi**. Il pulsante selezionato viene evidenziato.

   ![cqcartolaryhideusers](assets/cqsecurityhideusers.png)

1. Per far riapparire utenti o gruppi, fai di nuovo clic sul pulsante corrispondente.

### Creazione di utenti e gruppi {#creating-users-and-groups}

Per creare un utente o un gruppo:

1. In **Sicurezza** elenco ad albero della console fare clic su **Modifica** e quindi **Crea utente** o **Crea gruppo**.

   ![cqseruityeditcontextmenu](assets/cqseruityeditcontextmenu.png)

1. Immetti i dettagli richiesti, a seconda che tu stia creando un utente o un gruppo.

   * Se si seleziona **Crea utente,** immetti l’ID di accesso, il nome e il cognome, l’indirizzo e-mail e una password. Per impostazione predefinita, AEM crea un percorso basato sulla prima lettera del cognome, ma puoi selezionare un altro percorso.

   ![createuserdialog](assets/createuserdialog.png)

   * Se si seleziona **Crea gruppo**, inserisci un ID gruppo e una descrizione facoltativa.

   ![creategroupdialog](assets/creategroupdialog.png)

1. Fai clic su **Crea**. L&#39;utente o il gruppo creato viene visualizzato nell&#39;elenco ad albero.

### Eliminazione di utenti e gruppi {#deleting-users-and-groups}

Per eliminare un utente o un gruppo:

1. In **Sicurezza** seleziona l’utente o il gruppo da eliminare. Se si desidera eliminare più elementi, fare clic tenendo premuto il tasto Maiusc o il tasto Ctrl per selezionarli.
1. Fai clic su **Modifica,** quindi selezionare Elimina. AEM WCM chiede se si desidera eliminare l’utente o il gruppo.
1. Fai clic su **OK** per confermare o annullare.

### Modifica delle proprietà di utenti e gruppi {#modifying-user-and-group-properties}

Per modificare le proprietà utente e gruppo:

1. In **Sicurezza** fare doppio clic sul nome utente o gruppo che si desidera modificare.

1. Fai clic sul pulsante **Proprietà** apporta le modifiche necessarie e fai clic su **Salva**.

   ![cqcartolaryuserprops](assets/cqsecurityuserprops.png)

>[!NOTE]
>
>Il percorso dell&#39;utente viene visualizzato nella parte inferiore delle proprietà dell&#39;utente. Non può essere modificato.

### Modifica di una password utente {#changing-a-user-password}

Per modificare la password di un utente, attenersi alla procedura descritta di seguito.

>[!NOTE]
>
>Non puoi usare la console Sicurezza per modificare la password dell’amministratore. Per modificare la password dell&#39;account amministratore, utilizza il [Console Utenti](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user) che Granite Operations fornisce.
>
>Se utilizzi AEM Forms su JEE, non utilizzare le istruzioni riportate di seguito per modificare la password, piuttosto utilizzare AEM Forms su JEE Admin Console (/adminui) per modificare la password.

1. In **Sicurezza** fare doppio clic sul nome utente per il quale si desidera modificare la password.
1. Fai clic sul pulsante **Proprietà** (se non è già attivo).
1. Fai clic su **Imposta password**. Viene visualizzata la finestra Imposta password, che consente di modificare la password.

   ![cqcartolaryuserpassword](assets/cqsecurityuserpassword.png)

1. Immettere due volte la nuova password; poiché non vengono visualizzate in testo non crittografato, questa azione è di conferma; se non corrispondono, il sistema visualizza un errore.
1. Fai clic su **Imposta** per attivare la nuova password dell&#39;account.

### Aggiunta di utenti o gruppi a un gruppo {#adding-users-or-groups-to-a-group}

AEM offre tre modi diversi per aggiungere utenti o gruppi a un gruppo esistente:

* Quando ti trovi nel gruppo, puoi aggiungere membri (utenti o gruppi).
* Quando sei nel membro, puoi aggiungere membri ai gruppi.
* Quando si lavora su Autorizzazioni, è possibile aggiungere membri ai gruppi.

### Gruppi - Aggiunta di utenti o gruppi a un gruppo {#groups-adding-users-or-groups-to-a-group}

La **Gruppi** La scheda ti mostra a quali gruppi appartiene l’account corrente. Puoi utilizzarlo per aggiungere l’account selezionato a un gruppo:

1. Fare doppio clic sul nome dell&#39;account (utente o gruppo) che si desidera assegnare a un gruppo.
1. Fai clic sul pulsante **Gruppi** scheda . Viene visualizzato un elenco di gruppi a cui l’account appartiene già.
1. Nell’elenco ad albero, fai clic sul nome del gruppo a cui desideri aggiungere l’account e trascinalo nell’elenco **Gruppi** riquadro. Se desideri aggiungere più utenti, fai clic su o su Ctrl+clic su tali nomi e trascinali.

   ![cqcartolaryaddusertogroup](assets/cqsecurityaddusertogroup.png)

1. Fai clic su **Salva** per salvare le modifiche.

### Membri: aggiunta di utenti o gruppi a un gruppo {#members-adding-users-or-groups-to-a-group}

La **Membri** La scheda funziona solo per i gruppi e mostra gli utenti e i gruppi che appartengono al gruppo corrente. Puoi utilizzarlo per aggiungere account a un gruppo:

1. Fare doppio clic sul nome del gruppo a cui si desidera aggiungere i membri.
1. Fai clic sul pulsante **Membri** scheda . Viene visualizzato un elenco di membri che appartengono già a questo gruppo.
1. Nell&#39;elenco ad albero, fare clic sul nome del membro che si desidera aggiungere al gruppo e trascinarlo nella **Membri** riquadro. Se desideri aggiungere più utenti, fai clic su o su Ctrl+clic su tali nomi e trascinali.

   ![cqcartolaryadduserasmembro](assets/cqsecurityadduserasmember.png)

1. Fai clic su **Salva** per salvare le modifiche.

### Aggiunta di utenti o gruppi durante l&#39;aggiunta di autorizzazioni {#adding-users-or-groups-while-adding-permissions}

Per aggiungere membri a un gruppo in un determinato percorso:

1. Fare doppio clic sul nome del gruppo o dell&#39;utente a cui si desidera aggiungere gli utenti.

1. Fai clic sul pulsante **Autorizzazioni** scheda .

1. Passa al percorso a cui desideri aggiungere le autorizzazioni e fai clic su **Dettagli**. La parte inferiore della finestra dei dettagli fornisce informazioni su chi dispone delle autorizzazioni per quella pagina.

   ![chlimage_1-113](assets/chlimage_1-113.png)

1. Seleziona la casella di controllo in **Membro** per i membri che si desidera avere le autorizzazioni per quel percorso. Deselezionare la casella di controllo relativa al membro per il quale si desidera rimuovere le autorizzazioni. Nella cella modificata viene visualizzato un triangolo rosso.
1. Fai clic su **OK** per salvare le modifiche.

### Rimozione di utenti o gruppi dai gruppi {#removing-users-or-groups-from-groups}

AEM offre tre modi diversi per rimuovere utenti o gruppi da un gruppo:

* Quando ti trovi nel profilo di gruppo, puoi rimuovere i membri (utenti o gruppi).
* Quando ti trovi nel profilo membro, puoi rimuovere i membri dai gruppi.
* Quando lavori su Autorizzazioni, puoi rimuovere i membri dai gruppi.

### Gruppi - Rimozione di utenti o gruppi dai gruppi {#groups-removing-users-or-groups-from-groups}

Per rimuovere un account utente o di gruppo da un gruppo:

1. Fare doppio clic sul nome del gruppo o dell&#39;account utente che si desidera rimuovere da un gruppo.
1. Fai clic sul pulsante **Gruppi** scheda . Puoi vedere a quali gruppi appartiene l’account selezionato.
1. In **Gruppi** fare clic sul nome dell&#39;utente o del gruppo che si desidera rimuovere dal gruppo e fare clic su **Rimuovi**. (Per rimuovere più account, fare clic su di essi tenendo premuto Maiusc o Ctrl, quindi fare clic su di essi **Rimuovi**.)

   ![cqcartolaryremoveuserfromgrp](assets/cqsecurityremoveuserfromgrp.png)

1. Fai clic su **Salva** per salvare le modifiche.

### Membri: rimozione di utenti o gruppi da gruppi {#members-removing-users-or-groups-from-groups}

Per rimuovere account da un gruppo:

1. Fare doppio clic sul nome del gruppo da cui si desidera rimuovere i membri.
1. Fai clic sul pulsante **Membri** scheda . Viene visualizzato un elenco di membri che appartengono già a questo gruppo.
1. In **Membri** fare clic sul nome del membro che si desidera rimuovere dal gruppo e fare clic su **Rimuovi**. (Per rimuovere più utenti, fare clic su di essi tenendo premuto Maiusc o Ctrl, quindi fare clic su di essi **Rimuovi**.)

   ![cqcartolaryrimuovemember](assets/cqsecurityremovemember.png)

1. Fai clic su **Salva** per salvare le modifiche.

### Rimozione di utenti o gruppi durante l&#39;aggiunta di autorizzazioni {#removing-users-or-groups-while-adding-permissions}

Per rimuovere i membri da un gruppo in un determinato percorso:

1. Fare doppio clic sul nome del gruppo o dell&#39;utente da cui si desidera rimuovere gli utenti.

1. Fai clic sul pulsante **Autorizzazioni** scheda .

1. Passa al percorso a cui desideri rimuovere le autorizzazioni e fai clic su **Dettagli**. La parte inferiore della finestra dei dettagli fornisce informazioni su chi dispone delle autorizzazioni per quella pagina.

   ![chlimage_1-114](assets/chlimage_1-114.png)

1. Seleziona la casella di controllo in **Membro** per i membri che si desidera avere le autorizzazioni per quel percorso. Deselezionare la casella di controllo relativa al membro per il quale si desidera rimuovere le autorizzazioni. Nella cella modificata viene visualizzato un triangolo rosso.
1. Fai clic su **OK** per salvare le modifiche.

### Sincronizzazione utente {#user-synchronization}

Quando la distribuzione è [pubblica azienda](/help/sites-deploying/recommended-deploys.md#tarmk-farm), gli utenti e i gruppi devono essere sincronizzati tra tutti i nodi di pubblicazione.

Per informazioni sulla sincronizzazione utente e su come abilitarla, consulta [Sincronizzazione utente](/help/sites-administering/sync.md).

## Gestione delle autorizzazioni {#managing-permissions}

>[!NOTE]
>
>Adobe ha introdotto una nuova visualizzazione principale basata sull&#39;interfaccia utente touch per la gestione delle autorizzazioni. Per ulteriori dettagli su come usarlo, consulta [questa pagina](/help/sites-administering/touch-ui-principal-view.md).

Questa sezione descrive come impostare le autorizzazioni, inclusi i privilegi di replica.

### Impostazione delle autorizzazioni {#setting-permissions}

Le autorizzazioni consentono agli utenti di eseguire determinate azioni sulle risorse in determinati percorsi. Include anche la possibilità di creare o eliminare pagine.

Per aggiungere, modificare o eliminare autorizzazioni:

1. In **Sicurezza** fare doppio clic sul nome dell&#39;utente o del gruppo per il quale si desidera impostare le autorizzazioni o [cercare i nodi](#searching-for-nodes).

1. Fai clic sul pulsante **Autorizzazioni** scheda .

   ![cquserpermissions](assets/cquserpermissions.png)

1. Nella griglia ad albero, selezionare una casella di controllo per consentire all&#39;utente o al gruppo selezionato di eseguire un&#39;azione oppure deselezionare una casella di controllo per negare all&#39;utente o al gruppo selezionato di eseguire un&#39;azione. Per ulteriori informazioni, fai clic su **Dettagli**.

1. Al termine, fai clic su **Salva**.

### Impostazione dei privilegi di replica {#setting-replication-privileges}

Il privilegio di replica è il diritto di pubblicare contenuto e può essere impostato per gruppi e utenti.

>[!NOTE]
>
>* Tutti i diritti di replica applicati a un gruppo si applicano a tutti gli utenti di quel gruppo.
>* I privilegi di replica di un utente sostituiscono i privilegi di replica di un gruppo.
>* I diritti di replica consentiti hanno una precedenza superiore rispetto ai diritti di replica negati. Vedi [Autorizzazioni in AEM](#permissions-in-aem) per ulteriori informazioni.
>


Per impostare i privilegi di replica:

1. Seleziona l’utente o il gruppo dall’elenco, fai doppio clic per aprirlo e fai clic su **Autorizzazioni**.
1. Nella griglia, passare al percorso in cui si desidera che l&#39;utente disponga dei privilegi di replica o [cerca i nodi.](#searching-for-nodes)

1. In **Replicare** nel percorso selezionato, selezionare una casella di controllo per aggiungere il privilegio di replica per l&#39;utente o il gruppo selezionato oppure deselezionare la casella di controllo per rimuovere il privilegio di replica. AEM viene visualizzato un triangolo rosso in qualsiasi punto in cui sono state apportate modifiche che non sono ancora state salvate.

   ![cquserreplicatepermissions](assets/cquserreplicatepermissions.png)

1. Fai clic su **Salva** per salvare le modifiche.

### Ricerca dei nodi {#searching-for-nodes}

Quando aggiungi o rimuovi autorizzazioni, puoi sfogliare o cercare il nodo.

Esistono due tipi diversi di ricerca dei percorsi:

* Ricerca percorso - Se la stringa di ricerca inizia con un &quot;/&quot;, cerca i sottonodi diretti del percorso specificato:

![cqcartolarypathsearch](assets/cqsecuritypathsearch.png)

Nella casella di ricerca è possibile effettuare le seguenti operazioni:

| Azione | Effetto |
|--- |--- |
| Freccia destra | Seleziona un sottonodo nel risultato della ricerca |
| Freccia giù | Inizia nuovamente la ricerca. |
| Tasto Enter (Return) | Seleziona un sottonodo e lo carica nella griglia ad albero |

* Ricerca FullText - Se la stringa di ricerca non inizia con un &quot;/&quot;, viene eseguita una ricerca full-text su tutti i nodi sotto il percorso &quot;/content&quot;.

![cqcartolaryfulltextsearch](assets/cqsecurityfulltextsearch.png)

Per eseguire una ricerca su percorsi o testo completo:

1. Nella console Protezione, seleziona un utente o un gruppo e fai clic sul pulsante **Autorizzazioni** scheda .

1. Nella casella Cerca immettere un termine da cercare.

### Impersona utenti {#impersonating-users}

Puoi specificare uno o più utenti autorizzati a rappresentare l’utente corrente. Grazie a questa funzionalità, gli utenti possono passare alle impostazioni dell&#39;account dell&#39;utente corrente e agire a nome di questo utente.

Utilizzare questa funzione con cautela, in quanto può consentire agli utenti di eseguire azioni che non possono essere eseguite dal proprio utente. Durante la rappresentazione di un utente, gli utenti ricevono una notifica del fatto che non hanno effettuato l’accesso come se stessi.

Esistono vari scenari in cui potresti voler utilizzare questa funzionalità, tra cui:

* Se sei fuori ufficio, puoi lasciare che un&#39;altra persona ti impersoni mentre sei via. Utilizzando questa funzione, puoi assicurarti che qualcuno disponga dei tuoi diritti di accesso e non devi modificare un profilo utente o fornire la tua password.
* È possibile utilizzarlo a scopo di debug. Ad esempio, per vedere come il sito Web cerca un utente con diritti di accesso limitati. Inoltre, se un utente si lamenta di problemi tecnici, puoi impersonare tale utente per diagnosticare e risolvere il problema.

Per rappresentare un utente esistente:

1. Nell’elenco ad albero, selezionare il nome della persona che si desidera assegnare ad altri utenti da rappresentare. Fare doppio clic per aprire.
1. Fai clic sul pulsante **Impersonatori** scheda .
1. Fai clic sull’utente che desideri poter rappresentare l’utente selezionato. Trascina l’utente (l’impersonatore) dall’elenco al riquadro Impersona . Il nome viene visualizzato nell’elenco.

   ![chlimage_1-115](assets/chlimage_1-115.png)

1. Fai clic su **Salva**.

### Impostazione delle preferenze utente e gruppo {#setting-user-and-group-preferences}

Per impostare le preferenze utente e gruppo, incluse la lingua, la gestione delle finestre e le preferenze della barra degli strumenti:

1. Selezionare l&#39;utente o il gruppo di cui si desidera modificare le preferenze nella struttura a sinistra. Per selezionare più utenti o gruppi, fare clic sulle selezioni tenendo premuto Ctrl o Maiusc.
1. Fai clic sul pulsante **Preferenze** scheda .

   ![cqsecurity preferences](assets/cqsecuritypreferences.png)

1. Apporta le modifiche necessarie al gruppo o alle preferenze utente e fai clic su **Salva** una volta finito.

### Impostazione di utenti o amministratori per avere il privilegio di gestire altri utenti {#setting-users-or-administrators-to-have-the-privilege-to-manage-other-users}

Per impostare gli utenti o gli amministratori in modo che dispongano dei privilegi per eliminare/attivare/disattivare altri utenti:

1. Aggiungi l&#39;utente che desideri assegnare privilegi per gestire altri utenti al gruppo di amministratori e salva le modifiche.

   ![cqcartolaryaddmembertoadmin](assets/cqsecurityaddmembertoadmin.png)

1. Nel **Autorizzazioni** scheda , passa a &quot;/&quot; e nella colonna Replica seleziona la casella di controllo per consentire la replica in &quot;/&quot; e fai clic su **Salva**.

   ![cqcartolaryreplicatepermissions](assets/cqsecurityreplicatepermissions.png)

   L’utente selezionato può ora disattivare, attivare, eliminare e creare gli utenti.

### Estensione dei privilegi a livello di progetto {#extending-privileges-on-a-project-level}

Se prevedi di implementare privilegi specifici per le applicazioni, le informazioni seguenti descrivono ciò che devi sapere per implementare un privilegio personalizzato e come applicarlo in CQ:

Il privilegio di modifica della gerarchia è coperto da una combinazione di privilegi jcr. Il privilegio di replica è denominato **crx:replica** che viene memorizzato/valutato insieme ad altri privilegi nell’archivio jcr. Tuttavia, essa non viene applicata a livello di jcr.

La definizione e la registrazione dei privilegi personalizzati fa ufficialmente parte del [API Jackrabbit](https://jackrabbit.apache.org/oak/docs/security/privilege.html) alla versione 2.4 (vedi anche [JCR-2887](https://issues.apache.org/jira/browse/JCR-2887)). L&#39;ulteriore utilizzo è coperto da JCR Access Control Management, come definito da [JSR 283](https://jcp.org/en/jsr/detail?id=283) (sezione 16). Inoltre, l’API Jackrabbit definisce un paio di estensioni.

Il meccanismo di registrazione dei privilegi si riflette nell&#39;interfaccia utente in **Configurazione archivio**.

La registrazione di nuovi privilegi (personalizzati) è a sua volta protetta da un privilegio integrato che deve essere concesso a livello di archivio. In JCR: passando &#39;null&#39; come parametro &#39;absPath&#39; nell&#39;api mgt di ac, vedi jsr 333 per ulteriori dettagli. Per impostazione predefinita, **admin** e tutti i membri degli amministratori hanno quel privilegio concesso.

>[!NOTE]
>
>L’implementazione si occupa della convalida e della valutazione dei privilegi personalizzati, ma non può applicarli a meno che non siano aggregati di privilegi incorporati.
