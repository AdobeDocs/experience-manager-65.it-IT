---
title: ' Amministrazione degli utenti e sicurezza'
seo-title: ' Amministrazione degli utenti e sicurezza'
description: Ulteriori informazioni su Amministrazione utente e sicurezza in AEM.
seo-description: Ulteriori informazioni su Amministrazione utente e sicurezza in AEM.
uuid: 4512c0bf-71bf-4f64-99f6-f4fa5a61d572
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: e72da81b-4085-49b0-86c3-11ad48978a8a
docset: aem65
translation-type: tm+mt
source-git-commit: 0d5a48be283484005013ef3ed7ad015b43f6398b
workflow-type: tm+mt
source-wordcount: '5487'
ht-degree: 2%

---


#  Amministrazione degli utenti e sicurezza{#user-administration-and-security}

Questo capitolo descrive come configurare e gestire l&#39;autorizzazione utente e descrive anche la teoria che sta alla base del funzionamento dell&#39;autenticazione e dell&#39;autorizzazione in AEM.

## Utenti e gruppi in AEM {#users-and-groups-in-aem}

In questa sezione vengono descritte in dettaglio le varie entità e i concetti correlati, per facilitare la configurazione di un concetto di gestione utente semplice da gestire.

### Utenti {#users}

Gli utenti accederanno a AEM con il proprio account. Ciascun account utente è univoco e contiene i dettagli di base dell&#39;account, insieme ai privilegi assegnati.

Gli utenti sono spesso membri di Gruppi, il che semplifica l&#39;allocazione di tali autorizzazioni e/o privilegi.

### Gruppi {#groups}

I gruppi sono raccolte di utenti e/o altri gruppi; tutti chiamati membri di un gruppo.

Il loro scopo principale è semplificare il processo di manutenzione riducendo il numero di entità da aggiornare, in quanto una modifica apportata a un gruppo viene applicata a tutti i membri del gruppo. I gruppi riflettono spesso:

* un ruolo all&#39;interno della domanda; ad esempio un utente autorizzato a navigare sul contenuto o un utente autorizzato a contribuire al contenuto.
* la propria organizzazione; potete estendere i ruoli per distinguere tra collaboratori di diversi reparti quando sono limitati a rami diversi nella struttura del contenuto.

Di conseguenza, i gruppi tendono a rimanere stabili, mentre gli utenti arrivano e vanno più spesso.

Con la pianificazione e una struttura pulita, l&#39;uso dei gruppi può riflettere la vostra struttura, fornendo una chiara panoramica e un meccanismo efficiente per gli aggiornamenti.

### Built-in Users and Groups {#built-in-users-and-groups}

AEM WCM installa un numero di utenti e gruppi. Questi possono essere visualizzati quando accedete per la prima volta alla console di sicurezza dopo l&#39;installazione.

Le tabelle seguenti elencano ciascuna voce con:

* una breve descrizione
* eventuali raccomandazioni sulle modifiche necessarie

*Cambiare tutte le password* predefinite (se non si elimina l&#39;account stesso in determinate circostanze).

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
   <td><p>Account di amministrazione del sistema con diritti di accesso completi.</p> <p>Questo account viene utilizzato per la connessione tra AEM WCM e CRX.</p> <p>Se si elimina accidentalmente questo account, verrà ricreato al riavvio del repository (nella configurazione predefinita).</p> <p>L'account amministratore è un requisito della piattaforma AEM. Di conseguenza, questo account non può essere eliminato.</p> </td>
   <td><p> Adobe consiglia vivamente di modificare la password per questo account utente rispetto a quella predefinita.</p> <p>Preferibilmente all'installazione, anche se può essere fatto dopo.</p> <p>Nota: Questo account non deve essere confuso con l’account amministratore del motore servlet CQ.</p> </td>
  </tr>
  <tr>
   <td><p>anonimo</p> <p> </p> </td>
   <td>User</td>
   <td><p>Contiene i diritti predefiniti per l'accesso non autenticato a un'istanza. Per impostazione predefinita, questo contiene i diritti di accesso minimi.</p> <p>Se eliminate accidentalmente questo account, verrà ricreato all’avvio. Non può essere eliminato in modo permanente, ma può essere disabilitato.</p> </td>
   <td>Evitate di eliminare o disattivare questo account, in quanto influirà negativamente sul funzionamento delle istanze dell'autore. Se vi sono dei requisiti di sicurezza che vi impongono di eliminarli, accertatevi di verificare correttamente gli effetti che ha sui vostri sistemi prima.</td>
  </tr>
  <tr>
   <td><p>author</p> <p>Password predefinita: author</p> </td>
   <td>User</td>
   <td><p>Un account autore autorizzato a scrivere in /content. Include i privilegi di collaboratore e di surfer.</p> <p>Può essere utilizzato come webmaster in quanto ha accesso all'intera struttura /content.</p> <p>Questo non è un utente incorporato, ma un altro utente dimostrativo geometrixx</p> </td>
   <td><p> Adobe consiglia di eliminare completamente l’account o di cambiare la password rispetto al valore predefinito.</p> <p>Preferibilmente all'installazione, anche se può essere fatto dopo.</p> </td>
  </tr>
  <tr>
   <td>amministratori</td>
   <td>Gruppo</td>
   <td><p>Gruppo che conferisce diritti di amministratore a tutti i membri. Solo l'amministratore può modificare questo gruppo.</p> <p>Ha diritti di accesso completi.</p> </td>
   <td>Se imposti un’opzione di rifiuto per tutti su un nodo, gli amministratori avranno accesso solo se sarà nuovamente attivato per quel gruppo.</td>
  </tr>
  <tr>
   <td>content-authors</td>
   <td>Gruppo</td>
   <td><p>Gruppo responsabile per la modifica dei contenuti. Richiede autorizzazioni di lettura, modifica, creazione ed eliminazione.</p> </td>
   <td>Potete creare gruppi personalizzati di autori di contenuti con diritti di accesso specifici per il progetto, a condizione di aggiungere autorizzazioni di lettura, modifica, creazione ed eliminazione.</td>
  </tr>
  <tr>
   <td>collaboratore</td>
   <td>Gruppo</td>
   <td><p>Privilegi di base che consentono all’utente di scrivere contenuti (solo in funzionalità).</p> <p>Non assegna privilegi alla struttura /content; questi devono essere allocati specificamente per i singoli gruppi o utenti.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>dam-users</td>
   <td>Gruppo</td>
   <td>Gruppo di riferimento predefinito per un utente AEM Assets  tipico. I membri di questo gruppo dispongono dei privilegi appropriati per abilitare il caricamento/condivisione di risorse e raccolte.</td>
   <td> </td>
  </tr>
  <tr>
   <td>everyone</td>
   <td>Gruppo</td>
   <td><p>Ogni utente in AEM è membro del gruppo di tutti, anche se potreste non visualizzare il gruppo o la relazione di appartenenza in tutti gli strumenti.</p> <p>Questo gruppo può essere considerato come il diritto predefinito, in quanto può essere utilizzato per applicare le autorizzazioni a tutti, anche agli utenti che verranno creati in futuro.</p> </td>
   <td><p>Non modificate o eliminate questo gruppo.</p> <p>La modifica di questo account ha ulteriori implicazioni in termini di sicurezza.</p> </td>
  </tr>
  <tr>
   <td>tag-administrators</td>
   <td>Gruppo</td>
   <td>Gruppo consentito per la modifica dei tag.</td>
   <td> </td>
  </tr>
  <tr>
   <td>amministratori utente</td>
   <td>Gruppo</td>
   <td>Autorizza l’amministrazione degli utenti, ovvero il diritto di creare utenti e gruppi.</td>
   <td> </td>
  </tr>
  <tr>
   <td>editor di workflow</td>
   <td>Gruppo</td>
   <td>Gruppo autorizzato a creare e modificare modelli di workflow.</td>
   <td> </td>
  </tr>
  <tr>
   <td>workflow-users</td>
   <td>Gruppo</td>
   <td><p>Un utente che partecipa a un flusso di lavoro deve essere membro del gruppo utenti del flusso di lavoro. Questo gli dà pieno accesso a: /etc/workflow/istanze in modo che possa aggiornare l’istanza del flusso di lavoro.</p> <p>Il gruppo è incluso nell’installazione standard, ma dovete aggiungere manualmente gli utenti al gruppo.</p> </td>
  </tr>
 </tbody>
</table>

## Autorizzazioni in AEM {#permissions-in-aem}

AEM utilizza gli ACL per determinare le azioni che un utente o un gruppo può eseguire e dove può eseguire tali azioni.

### Autorizzazioni e ACL {#permissions-and-acls}

Le autorizzazioni definiscono chi può eseguire quali azioni su una risorsa. Le autorizzazioni sono il risultato delle valutazioni del controllo [di](#access-control-lists-and-how-they-are-evaluated) accesso.

Potete modificare le autorizzazioni concesse o negate a un determinato utente selezionando o deselezionando le caselle di controllo per le singole [azioni](security.md#actions)AEM. Un segno di spunta indica che un’azione è consentita. Nessun segno di spunta indica che un’azione è stata rifiutata.

La posizione del segno di spunta nella griglia indica anche le autorizzazioni di cui dispongono gli utenti in quali posizioni all’interno di AEM (ossia, quali percorsi).

### Azioni {#actions}

Le azioni possono essere eseguite su una pagina (risorsa). Per ogni pagina nella gerarchia, potete specificare quale azione l&#39;utente può intraprendere sulla pagina. [Le autorizzazioni](#permissions-and-acls) consentono di consentire o negare un’azione.

<table>
 <tbody>
  <tr>
   <td><strong>Azione </strong></td>
   <td><strong>Descrizione </strong></td>
  </tr>
  <tr>
   <td>Leggi</td>
   <td>All’utente è consentito leggere la pagina e tutte le pagine figlie.</td>
  </tr>
  <tr>
   <td>Modifica</td>
   <td><p>L'utente può:</p>
    <ul>
     <li>modificate il contenuto esistente sulla pagina e su qualsiasi pagina figlia.</li>
     <li>creare nuovi paragrafi sulla pagina o su qualsiasi pagina figlia.</li>
    </ul> <p>A livello JCR, gli utenti possono modificare una risorsa modificandone le proprietà, il blocco, il controllo delle versioni, le non-modifiche e dispongono dell’autorizzazione di scrittura completa sui nodi che definiscono un nodo figlio jcr:content, ad esempio cq:Page, nt:file, cq:Asset.</p> </td>
  </tr>
  <tr>
   <td>Crea</td>
   <td><p>L'utente può:</p>
    <ul>
     <li>create una nuova pagina o pagina figlia.</li>
    </ul> <p>Se si <strong>nega la modifica</strong> , le sottostrutture sotto jcr:content vengono espressamente escluse perché la creazione di jcr:content e dei relativi nodi figlio viene considerata una modifica di pagina. Ciò vale solo per i nodi che definiscono un nodo figlio jcr:content.</p> </td>
  </tr>
  <tr>
   <td>Elimina</td>
   <td><p>L'utente può:</p>
    <ul>
     <li>eliminare paragrafi esistenti dalla pagina o da una pagina figlia.</li>
     <li>eliminare una pagina o una pagina figlia.</li>
    </ul> <p>Se <strong>la modifica</strong> viene rifiutata, le sottostrutture sotto jcr:content vengono esplicitamente escluse in quanto la rimozione di jcr:content e i relativi nodi figlio viene considerata una modifica di pagina. Ciò vale solo per i nodi che definiscono un nodo figlio jcr:content.</p> </td>
  </tr>
  <tr>
   <td>Leggi ACL</td>
   <td>L'utente può leggere l'elenco dei controlli di accesso della pagina o delle pagine figlie.</td>
  </tr>
  <tr>
   <td>Modifica ACL</td>
   <td>L'utente può modificare l'elenco dei controlli di accesso della pagina o di qualsiasi pagina figlia.</td>
  </tr>
  <tr>
   <td>Replica</td>
   <td>L'utente può replicare il contenuto in un altro ambiente (ad esempio, nell'ambiente di pubblicazione). Il privilegio viene applicato anche a tutte le pagine figlie.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>AEM genera automaticamente i gruppi di utenti per l&#39;assegnazione del ruolo (Proprietario, Editor, Visualizzatore) nelle [raccolte](/help/assets/manage-collections.md). Tuttavia, l&#39;aggiunta manuale di ACL per tali gruppi può introdurre vulnerabilità di protezione all&#39;interno di AEM.  Adobe consiglia di evitare di aggiungere ACL manualmente.

### Elenchi di controllo degli accessi e modalità di valutazione {#access-control-lists-and-how-they-are-evaluated}

AEM WCM utilizza gli elenchi di controllo degli accessi per organizzare le autorizzazioni applicate alle varie pagine.

Gli elenchi di controllo degli accessi sono composti di singole autorizzazioni e vengono utilizzati per determinare l’ordine in cui tali autorizzazioni vengono effettivamente applicate. L&#39;elenco è formato in base alla gerarchia delle pagine in esame. L’elenco viene quindi analizzato dal basso fino a ottenere la prima autorizzazione appropriata per l’applicazione a una pagina.

>[!NOTE]
>
>Esistono ACL inclusi con i campioni. Si consiglia di esaminare e determinare gli elementi appropriati per le applicazioni. Per esaminare gli ACL inclusi, passare a **CRXDE **e selezionare la scheda Controllo **** accesso per i nodi seguenti:
>
>`/etc/cloudservices/facebookconnect/geometrixx-outdoorsfacebookapp`: Consente a tutti l&#39;accesso in lettura.
>`/etc/cloudservices/twitterconnect/geometrixx-outdoors-twitter-app`: Consente a tutti l&#39;accesso in lettura.
>`/home/users/geometrixx-outdoors`: Consente a tutti di accedere in lettura a `*/profile*` e
>`*/social/relationships/following/*`.
>
>L&#39;applicazione personalizzata può impostare l&#39;accesso per altre relazioni, ad esempio `*/social/relationships/friend/*` o `*/social/relationships/pending-following/*`.
>
>Quando create ACL specifici per le comunità, ai membri che aderiscono a tali community possono essere concesse autorizzazioni aggiuntive. Ad esempio, questo potrebbe verificarsi quando gli utenti si uniscono alle comunità a `/content/geometrixx-outdoors/en/community/hiking` o `/content/geometrixx-outdoors/en/community/winter-sports`.

### Stati di autorizzazione {#permission-states}

>[!NOTE]
>
>Per gli utenti CQ 5.3:
>
>Contrariamente alle versioni precedenti di CQ, non è più necessario **creare** ed **eliminare** le pagine se l’utente deve solo modificarle. Concedere invece l’azione di **modifica** solo se si desidera che gli utenti siano in grado di creare, modificare o eliminare componenti sulle pagine esistenti.
>
>Per motivi di compatibilità con le versioni precedenti, i test delle azioni non tengono conto del trattamento speciale dei nodi che definiscono **jcr:content** .

| **Azione** | **Descrizione** |
|---|---|
| Consenti (segno di spunta) | AEM WCM consente all&#39;utente di eseguire l&#39;azione su questa pagina o su qualsiasi pagina figlia. |
| Nega (nessun segno di spunta) | AEM WCM non consente all&#39;utente di eseguire l&#39;azione su questa pagina né su alcuna pagina figlia. |

Le autorizzazioni vengono applicate anche a tutte le pagine figlie.

Se un&#39;autorizzazione non viene ereditata dal nodo padre ma dispone di almeno una voce locale, i seguenti simboli vengono aggiunti alla casella di controllo. Una voce locale è una voce creata nell&#39;interfaccia CRX 2.2 (gli ACL jolly al momento possono essere creati solo in CRX.)

Per un&#39;azione in un determinato percorso:

<table>
 <tbody>
  <tr>
   <td>* (asterisco)</td>
   <td>Vi è almeno una voce locale (efficace o inefficace). Questi ACL con caratteri jolly sono definiti in CRX.</td>
  </tr>
  <tr>
   <td>! (punto esclamativo)</td>
   <td>Almeno una voce non ha attualmente alcun effetto.</td>
  </tr>
 </tbody>
</table>

Quando si passa il puntatore del mouse sopra l&#39;asterisco o il punto esclamativo, una descrizione comandi fornisce ulteriori dettagli sulle voci dichiarate. La descrizione comandi è divisa in due parti:

<table>
 <tbody>
  <tr>
   <td>Parte superiore</td>
   <td><p>Elenca le voci effettive.</p> </td>
  </tr>
  <tr>
   <td>Parte inferiore</td>
   <td>Elenca le voci non efficaci che possono avere un effetto altrove nella struttura (come indicato da un attributo speciale presente con il corrispondente ACE che limita l'ambito della voce). In alternativa, si tratta di una voce il cui effetto è stato revocato da un'altra voce definita nel percorso specificato o in un nodo antenato.</td>
  </tr>
 </tbody>
</table>

![chlimage_1-112](assets/chlimage_1-112.png)

>[!NOTE]
>
>Se non sono definite autorizzazioni per una pagina, tutte le azioni vengono negate.

Di seguito sono riportate alcune raccomandazioni sulla gestione degli elenchi di controllo degli accessi:

* Non assegnate autorizzazioni direttamente agli utenti. Assegnateli solo ai gruppi.

   Questo semplificherà la manutenzione, poiché il numero di gruppi è molto inferiore al numero di utenti, e anche meno volatile.

* Se desiderate che un gruppo/utente possa solo modificare le pagine, non consentite loro di creare o negare i diritti. Concedi loro solo diritti di modifica e lettura.
* Utilizzate Nega con cautela. Per quanto possibile utilizzare solo Consenti.

   L’utilizzo di Rifiuta può causare effetti imprevisti se le autorizzazioni vengono applicate in un ordine diverso da quello previsto. Se un utente è membro di più di un gruppo, le istruzioni Deny di un gruppo possono annullare l&#39;istruzione Allow di un altro gruppo o viceversa. È difficile mantenere una panoramica quando questo accade e può facilmente portare a risultati imprevisti, mentre Consenti assegnazioni non causano tali conflitti.

    Adobe consiglia di utilizzare le procedure [consigliate](#best-practices)Consenti anziché Rifiuta.

Prima di modificare entrambe le autorizzazioni, accertatevi di comprenderne il funzionamento e interrelazionarvi. Consultate la documentazione CRX per illustrare in che modo AEM WCM [valuta i diritti](/help/sites-administering/user-group-ac-admin.md#how-access-rights-are-evaluated) di accesso e per esempi sull&#39;impostazione di elenchi di controllo di accesso.

### Autorizzazioni  {#permissions}

Le autorizzazioni consentono a utenti e gruppi di accedere AEM funzionalità sulle pagine AEM.

Le autorizzazioni vengono cercate per percorso espandendo/comprimendo i nodi e l&#39;ereditarietà delle autorizzazioni può essere tracciata fino al nodo principale.

Potete concedere o negare le autorizzazioni selezionando o deselezionando le caselle di controllo appropriate.

![cqcartolarypermissionstab](assets/cqsecuritypermissionstab.png)

### Visualizzazione di informazioni dettagliate sulle autorizzazioni {#viewing-detailed-permission-information}

Insieme alla vista griglia, AEM fornisce una visualizzazione dettagliata delle autorizzazioni per un utente/gruppo selezionato in un determinato percorso. La visualizzazione Dettagli fornisce ulteriori informazioni.

Oltre a visualizzare le informazioni, potete anche includere o escludere l’utente o il gruppo corrente da un gruppo. Consultate [Aggiunta di utenti o gruppi durante l’aggiunta di autorizzazioni](#adding-users-or-groups-while-adding-permissions). Le modifiche apportate qui si riflettono immediatamente nella parte superiore della visualizzazione dettagliata.

Per accedere alla visualizzazione Dettagli, nella scheda **Autorizzazioni** , fate clic su **Dettagli** per qualsiasi gruppo/utente e percorso selezionato.

![permissionari](assets/permissiondetails.png)

I dettagli sono suddivisi in due parti:

<table>
 <tbody>
  <tr>
   <td>Parte superiore</td>
   <td><p>Ripete le informazioni visualizzate nella griglia ad albero. Per ogni azione, un'icona indica se l'azione è consentita o rifiutata:</p>
    <ul>
     <li>nessuna icona = nessuna voce dichiarata</li>
     <li>(tick) = azione dichiarata (allow)</li>
     <li>(-) = azione dichiarata (rifiuto)</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Parte inferiore</td>
   <td><p>Mostra la griglia di utenti e gruppi che esegue le seguenti operazioni:</p>
    <ul>
     <li>Dichiara una voce per il percorso specificato E</li>
     <li>È l'operatore OR autorizzato specificato è un gruppo</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Impersonazione di un altro utente {#impersonating-another-user}

With the [Impersonate functionality](/help/sites-authoring/user-properties.md#user-settings) a user can work on behalf of another user.

Ciò significa che un account utente può specificare altri account che possono funzionare con il proprio account. In altre parole, se l&#39;utente-B è autorizzato a rappresentare l&#39;utente-A, l&#39;utente-B può intraprendere azioni utilizzando i dettagli account completi dell&#39;utente-A.

Questo consente agli account del soggetto di completare le attività come se utilizzassero l&#39;account che stanno impersonando; ad esempio, durante un&#39;assenza o per condividere un carico eccessivo a breve termine.

>[!NOTE]
>
>Affinché la rappresentazione funzioni correttamente per gli utenti non amministratori, è necessario che nel `/home/users` percorso sia presente l&#39;utente/impersona (nel caso precedente user-B) con autorizzazioni di lettura.
>
>Per ulteriori informazioni su come ottenere questo risultato, consulta [Autorizzazioni in AEM](/help/sites-administering/security.md#permissions-in-aem).

>[!CAUTION]
>
>Se un account ne rappresenta un altro è molto difficile da vedere. Una voce viene inserita nel registro di controllo quando la rappresentazione inizia e termina, ma gli altri file di registro (come il registro di accesso) non contengono informazioni sul fatto che la rappresentazione si è verificata sugli eventi. Pertanto, se l&#39;utente-B rappresenta l&#39;utente-A, tutti gli eventi avranno l&#39;aspetto di essere eseguiti personalmente dall&#39;utente-A.

>[!CAUTION]
>
>Il blocco di pagina può essere eseguito quando si impersona un utente. Tuttavia, una pagina bloccata in tale modalità può essere sbloccata solo dall&#39;utente impersonato o da un utente con qualità di amministratore.
>
>Non è consentito sbloccare le pagine bloccate impersonando l’utente che le ha boccate.

### Best practice   {#best-practices}

Di seguito vengono descritte le procedure ottimali per l&#39;utilizzo di autorizzazioni e privilegi:

| Regola | Motivo |
|--- |--- |
| *Usa gruppi* | Evitate di assegnare i diritti di accesso in base agli utenti. I motivi sono molteplici:<ul><li>Gli utenti sono molti più numerosi dei gruppi, quindi i gruppi semplificano la struttura.</li><li>I gruppi forniscono una panoramica su tutti gli account.</li> <li>L&#39;ereditarietà è più semplice con i gruppi.</li><li>Gli utenti vanno e vengono. I gruppi sono a lungo termine.</li></ul> |
| *Sii positivo* | Utilizzate sempre le istruzioni Allow (Consenti) per specificare i diritti del gruppo (ove possibile). Evitare di utilizzare un&#39;istruzione Rifiuta. I gruppi vengono valutati in ordine e l&#39;ordine può essere definito in modo diverso per utente. In altre parole: È possibile che l&#39;ordine in cui le istruzioni vengono implementate e valutate sia limitato. Se si utilizzano solo le istruzioni Allow (Consenti), l&#39;ordine non ha importanza. |
| *Mantieni semplice* | Investire un po&#39; di tempo e pensare quando si configura una nuova installazione sarà ben ripagato. L&#39;applicazione di una struttura chiara semplificherà la manutenzione e l&#39;amministrazione in corso, garantendo che sia i colleghi attuali che i futuri successori possano comprendere facilmente ciò che viene implementato. |
| *Prova* | Utilizzate un&#39;installazione di test per esercitarvi e assicurarvi di comprendere le relazioni tra i vari utenti e gruppi. |
| *Utenti/gruppi predefiniti* | Aggiornate sempre gli utenti e i gruppi predefiniti subito dopo l’installazione per evitare problemi di sicurezza. |

## Managing Users and Groups {#managing-users-and-groups}

Gli utenti includono le persone che utilizzano il sistema e i sistemi esterni che effettuano richieste al sistema.

Un gruppo è un set di utenti.

Entrambi possono essere configurati utilizzando la funzionalità Amministrazione utente nella console di sicurezza.

### Accesso all&#39;amministrazione degli utenti con la console di sicurezza {#accessing-user-administration-with-the-security-console}

Potete accedere a tutti gli utenti, i gruppi e le autorizzazioni associate utilizzando la console Protezione. Tutte le procedure descritte in questa sezione vengono eseguite in questa finestra.

Per accedere AEM protezione WCM, effettuare una delle seguenti operazioni:

* Nella schermata introduttiva o in diverse aree di AEM, fate clic sull’icona relativa alla protezione:

![](do-not-localize/wcmtoolbar.png)

* Passa direttamente a `https://<server>:<port>/useradmin`. Assicuratevi di accedere AEM come amministratore.

Viene visualizzata la finestra seguente:

![cqcartolarypage](assets/cqsecuritypage.png)

Nella struttura ad albero a sinistra sono elencati tutti gli utenti e i gruppi attualmente presenti nel sistema. È possibile selezionare le colonne desiderate, ordinare il contenuto delle colonne e persino modificare l&#39;ordine di visualizzazione delle colonne trascinando l&#39;intestazione della colonna in una nuova posizione.

![cqcartolarycolumncontext](assets/cqsecuritycolumncontext.png)

Le schede forniscono l&#39;accesso a varie configurazioni:

<!-- ??? in table below. -->

| Scheda | Descrizione |
|--- |--- |
| Filtro, casella | Un meccanismo per filtrare gli utenti e/o i gruppi elencati. Consultate [Filtrare utenti e gruppi](#filtering-users-and-groups). |
| Nascondi utenti | Un interruttore di attivazione/disattivazione che nasconderà tutti gli utenti elencati, lasciando solo i gruppi. Consultate [Nascondere utenti e gruppi](#hiding-users-and-groups). |
| Nascondi gruppi | Un interruttore di attivazione/disattivazione che nasconderà tutti i gruppi elencati, lasciando solo gli utenti. Consultate [Nascondere utenti e gruppi](#hiding-users-and-groups). |
| Modifica | Un menu che consente di creare ed eliminare nonché attivare e disattivare utenti o gruppi. Consultate [Creazione di utenti e gruppi](#creating-users-and-groups) ed [Eliminazione di utenti e gruppi](#deleting-users-and-groups). |
| Proprietà | Elenca le informazioni sull’utente o sul gruppo che possono includere informazioni e-mail, una descrizione e un nome. Consente inoltre di modificare la password di un utente. Consultate [Creazione di utenti e gruppi](#creating-users-and-groups), [Modifica delle proprietà](#modifying-user-and-group-properties) utente e gruppo e [Modifica della password](#changing-a-user-password)utente. |
| Gruppi | Elenca tutti i gruppi a cui appartiene l&#39;utente o il gruppo selezionato. Potete assegnare l’utente o i gruppi selezionati ad altri gruppi o rimuoverli dai gruppi. Consultate [Gruppi](#adding-users-or-groups-to-a-group). |
| Membri | Disponibile solo per i gruppi. Elenca i membri di un particolare gruppo. Vedere [Membri](#members-adding-users-or-groups-to-a-group). |
| Autorizzazioni  | Potete assegnare le autorizzazioni a un utente o a un gruppo. Consente di controllare quanto segue:<ul><li>Autorizzazioni relative a pagine/nodi specifici. Consultate [Impostazione delle autorizzazioni](#setting-permissions). </li><li>Autorizzazioni relative alla creazione ed eliminazione di pagine e modifiche gerarchiche. ??? consente di [allocare privilegi](#settingprivileges), ad esempio la modifica della gerarchia, che consente di creare ed eliminare pagine,</li><li>Autorizzazioni correlate ai privilegi [di](#setting-replication-privileges) replica (in genere dall’autore alla pubblicazione) in base a un percorso.</li></ul> |
| Impersonatori | Consente a un altro utente di rappresentare l’account. Utile quando un utente deve agire per conto di un altro utente. Consultate [Impersonazione di utenti](#impersonating-another-user). |
| Preferenze | Imposta [le preferenze per il gruppo o l’utente](#setting-user-and-group-preferences). Ad esempio, preferenze per la lingua. |

### Filtering Users and Groups {#filtering-users-and-groups}

Potete filtrare l’elenco immettendo un’espressione di filtro che nasconda tutti gli utenti e i gruppi che non corrispondono all’espressione. Potete anche nascondere utenti e gruppi utilizzando i pulsanti [Nascondi utente e Nascondi gruppo](#hiding-users-and-groups) .

Per filtrare utenti o gruppi:

1. Nell&#39;elenco ad albero a sinistra, digitare l&#39;espressione del filtro nello spazio disponibile. Ad esempio, l&#39;immissione di **admin** visualizza tutti gli utenti e i gruppi che contengono questa stringa.
1. Fare clic sulla lente di ingrandimento per filtrare l&#39;elenco.

   ![cqcartolaryfilter](assets/cqsecurityfilter.png)

1. Fate clic su **x** per rimuovere tutti i filtri.

### Hiding Users and Groups {#hiding-users-and-groups}

Nascondere utenti o gruppi è un altro modo per filtrare l’elenco di tutti gli utenti e i gruppi in un sistema. Ci sono due meccanismi di attivazione/disattivazione. Facendo clic su Nascondi utente, tutti gli utenti vengono nascosti e facendo clic su Nascondi gruppi tutti i gruppi vengono nascosti (non potete nascondere sia gli utenti che i gruppi allo stesso tempo). Per filtrare l’elenco utilizzando un’espressione di filtro, consultate [Applicazione di filtri a utenti e gruppi](#filtering-users-and-groups).

Per nascondere utenti e gruppi:

1. Nella console **Protezione** , fate clic su **Nascondi utenti** o su **Nascondi gruppi**. Il pulsante selezionato viene evidenziato.

   ![cqcartolaryhideusers](assets/cqsecurityhideusers.png)

1. Per visualizzare nuovamente gli utenti o i gruppi, fate di nuovo clic sul pulsante corrispondente.

### Creating Users and Groups {#creating-users-and-groups}

Per creare un nuovo utente o gruppo:

1. Nell&#39;elenco ad albero della console **Protezione** , fare clic su **Modifica** , quindi su **Crea utente** o su **Crea gruppo**.

   ![cqseruityeditcontextmenu](assets/cqseruityeditcontextmenu.png)

1. Inserite i dettagli richiesti, a seconda che stiate creando un utente o un gruppo.

   * Se selezionate **Crea utente,** immettete l’ID di accesso, il nome e il cognome, l’indirizzo e-mail e una password. Per impostazione predefinita, AEM crea un percorso basato sulla prima lettera del cognome, ma potete selezionare un altro percorso.

   ![create ateuserdialog](assets/createuserdialog.png)

   * Se selezionate **Crea gruppo**, immettete un ID gruppo e una descrizione facoltativa.

   ![creategroupdialog](assets/creategroupdialog.png)

1. Fai clic su **Crea**. L’utente o il gruppo creato viene visualizzato nell’elenco ad albero.

### Deleting Users and Groups {#deleting-users-and-groups}

Per eliminare un utente o un gruppo:

1. Nella console **Protezione** , selezionate l’utente o il gruppo da eliminare. Per eliminare più elementi, tenete premuto il tasto Maiusc e fate clic oppure Ctrl e fate clic per selezionarli.
1. Fate clic su **Modifica,** quindi selezionate Elimina. AEM WCM chiede se si desidera eliminare l’utente o il gruppo.
1. Fate clic su **OK** per confermare o su Annulla per annullare l’azione.

### Modifica delle proprietà di utenti e gruppi {#modifying-user-and-group-properties}

Per modificare le proprietà utente e gruppo:

1. Nella console **Protezione** , fate doppio clic sul nome utente o del gruppo da modificare.

1. Fate clic sulla scheda **Proprietà** , apportate le modifiche necessarie e fate clic su **Salva**.

   ![cqcartolaryuserprops](assets/cqsecurityuserprops.png)

>[!NOTE]
>
>Il percorso dell&#39;utente viene visualizzato nella parte inferiore delle proprietà dell&#39;utente. Non può essere modificato.

### Modifica di una password utente {#changing-a-user-password}

Per modificare la password di un utente, effettuate le seguenti operazioni.

>[!NOTE]
>
>Non potete usare la console Protezione per cambiare la password dell&#39;amministratore. Per modificare la password dell&#39;account amministratore, utilizzate la console [](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user) Utenti fornita da Granite Operations.
>
>Se utilizzate  AEM Forms su JEE, non utilizzate le istruzioni riportate di seguito per cambiare la password, ma utilizzate  AEM Forms sulla console di amministrazione JEE (/adminui) per modificare la password.

1. Nella console **Protezione** , fate doppio clic sul nome utente per il quale desiderate cambiare la password.
1. Fare clic sulla scheda **Proprietà** (se non è già attiva).
1. Fate clic su **Imposta password**. Viene visualizzata la finestra Imposta password, in cui potete modificare la password.

   ![cqcartolaryuserpassword](assets/cqsecurityuserpassword.png)

1. Immettete due volte la nuova password; poiché non sono visualizzati in testo chiaro, questo è un messaggio di conferma - se non corrispondono, il sistema visualizza un errore.
1. Fate clic su **Set** per attivare la nuova password dell&#39;account.

### Aggiunta di utenti o gruppi a un gruppo {#adding-users-or-groups-to-a-group}

AEM offre tre modi diversi per aggiungere utenti o gruppi a un gruppo esistente:

* Quando vi trovate nel gruppo, potete aggiungere membri (utenti o gruppi).
* Quando vi trovate nel membro, potete aggiungere membri ai gruppi.
* Quando lavorate su Autorizzazioni, potete aggiungere membri ai gruppi.

### Gruppi - Aggiunta di utenti o gruppi a un gruppo {#groups-adding-users-or-groups-to-a-group}

La scheda **Gruppi** mostra i gruppi a cui appartiene l&#39;account corrente. Potete utilizzarlo per aggiungere l’account selezionato a un gruppo:

1. Fate doppio clic sul nome dell’account (utente o gruppo) che desiderate assegnare a un gruppo.
1. Click the **Groups** tab. Viene visualizzato un elenco di gruppi a cui l’account appartiene già.
1. Nell’elenco ad albero, fate clic sul nome del gruppo a cui desiderate aggiungere l’account e trascinatelo nel riquadro **Gruppi** . Per aggiungere più utenti, tenete premuto Maiusc e fate clic o Ctrl e trascinate i nomi desiderati.

   ![cqcartolaryaddusertogroup](assets/cqsecurityaddusertogroup.png)

1. Click **Save** to save your changes.

### Membri - Aggiunta di utenti o gruppi a un gruppo {#members-adding-users-or-groups-to-a-group}

La scheda **Membri** funziona solo per i gruppi e mostra quali utenti e gruppi appartengono al gruppo corrente. Potete utilizzarlo per aggiungere account a un gruppo:

1. Fate doppio clic sul nome del gruppo al quale desiderate aggiungere i membri.
1. Click the **Members** tab. Viene visualizzato un elenco di membri che appartengono già a questo gruppo.
1. Nell’elenco ad albero, fate clic sul nome del membro che desiderate aggiungere al gruppo e trascinatelo nel riquadro **Membri** . Per aggiungere più utenti, tenete premuto Maiusc e fate clic o Ctrl e trascinate i nomi desiderati.

   ![cqcartolaryadduserasmembro](assets/cqsecurityadduserasmember.png)

1. Click **Save** to save your changes.

### Aggiunta di utenti o gruppi durante l&#39;aggiunta di autorizzazioni {#adding-users-or-groups-while-adding-permissions}

Per aggiungere membri a un gruppo in un determinato percorso:

1. Fate doppio clic sul nome del gruppo o dell’utente a cui desiderate aggiungere gli utenti.

1. Click the **Permissions** tab.

1. Andate al percorso a cui desiderate aggiungere le autorizzazioni e fate clic su **Dettagli**. La parte inferiore della finestra dei dettagli fornisce informazioni su chi dispone delle autorizzazioni per quella pagina.

   ![chlimage_1-113](assets/chlimage_1-113.png)

1. Selezionate la casella di controllo nella colonna **Membro** per i membri per i quali desiderate disporre delle autorizzazioni per tale percorso. Deselezionare la casella di controllo relativa al membro per il quale si desidera rimuovere le autorizzazioni. Nella cella a cui sono state apportate modifiche viene visualizzato un triangolo rosso.
1. Fate clic su **OK** per salvare le modifiche.

### Rimozione di utenti o gruppi da gruppi {#removing-users-or-groups-from-groups}

AEM offre tre modi diversi per rimuovere utenti o gruppi da un gruppo:

* Quando vi trovate nel profilo del gruppo, potete rimuovere i membri (utenti o gruppi).
* Quando vi trovate nel profilo membro, potete rimuovere i membri dai gruppi.
* Quando lavorate su Autorizzazioni, potete rimuovere i membri dai gruppi.

### Gruppi - Rimozione di utenti o gruppi da gruppi {#groups-removing-users-or-groups-from-groups}

Per rimuovere un account utente o gruppo da un gruppo:

1. Fate doppio clic sul nome del gruppo o dell’account utente che desiderate rimuovere da un gruppo.
1. Click the **Groups** tab. Potete vedere a quali gruppi appartiene l&#39;account selezionato.
1. Nel riquadro **Gruppi** , fate clic sul nome dell’utente o del gruppo da rimuovere dal gruppo e fate clic su **Rimuovi**. Per rimuovere più account, tenete premuto Maiusc e fate clic o Ctrl e fate clic su di essi, quindi fate clic su **Rimuovi**.

   ![cqcartolaryremoveuserfromgrp](assets/cqsecurityremoveuserfromgrp.png)

1. Click **Save** to save your changes.

### Membri - Rimozione di utenti o gruppi da gruppi {#members-removing-users-or-groups-from-groups}

Per rimuovere account da un gruppo:

1. Fate doppio clic sul nome del gruppo da cui desiderate rimuovere i membri.
1. Click the **Members** tab. Viene visualizzato un elenco di membri che appartengono già a questo gruppo.
1. Nel riquadro **Membri** , fate clic sul nome del membro che desiderate rimuovere dal gruppo e fate clic su **Rimuovi**. Per rimuovere più utenti, tenete premuto Maiusc e fate clic o Ctrl e fate clic su di essi, quindi fate clic su **Rimuovi**.

   ![cqcartolaryremove_ember](assets/cqsecurityremovemember.png)

1. Click **Save** to save your changes.

### Rimozione di utenti o gruppi durante l&#39;aggiunta di autorizzazioni {#removing-users-or-groups-while-adding-permissions}

Per rimuovere membri da un gruppo a un determinato percorso:

1. Fate doppio clic sul nome del gruppo o dell’utente da cui desiderate rimuovere gli utenti.

1. Click the **Permissions** tab.

1. Individuate il percorso in cui desiderate rimuovere le autorizzazioni e fate clic su **Dettagli**. La parte inferiore della finestra dei dettagli fornisce informazioni su chi dispone delle autorizzazioni per quella pagina.

   ![chlimage_1-114](assets/chlimage_1-114.png)

1. Selezionate la casella di controllo nella colonna **Membro** per i membri per i quali desiderate disporre delle autorizzazioni per tale percorso. Deselezionare la casella di controllo relativa al membro per il quale si desidera rimuovere le autorizzazioni. Nella cella a cui sono state apportate modifiche viene visualizzato un triangolo rosso.
1. Fate clic su **OK** per salvare le modifiche.

### Sincronizzazione utente {#user-synchronization}

Quando la distribuzione è una farm [di](/help/sites-deploying/recommended-deploys.md#tarmk-farm)pubblicazione, gli utenti e i gruppi devono essere sincronizzati tra tutti i nodi di pubblicazione.

Per informazioni sulla sincronizzazione degli utenti e su come attivarla, consultate Sincronizzazione [](/help/sites-administering/sync.md)utente.

## Gestione delle autorizzazioni {#managing-permissions}

>[!NOTE]
>
> Adobe ha introdotto una nuova visualizzazione principale basata sull&#39;interfaccia touch per la gestione delle autorizzazioni. Per ulteriori dettagli su come usarlo, consultate [questa pagina](/help/sites-administering/touch-ui-principal-view.md).

Questa sezione descrive come impostare le autorizzazioni, compresi i privilegi di replica.

### Impostazione delle autorizzazioni {#setting-permissions}

Le autorizzazioni consentono agli utenti di eseguire determinate azioni sulle risorse in determinati percorsi. Include inoltre la possibilità di creare o eliminare pagine.

Per aggiungere, modificare o eliminare autorizzazioni:

1. Nella console **Protezione** , fate doppio clic sul nome dell’utente o del gruppo per il quale desiderate impostare le autorizzazioni o [cercare i nodi](#searching-for-nodes).

1. Click the **Permissions** tab.

   ![cquserpermissions](assets/cquserpermissions.png)

1. Nella griglia ad albero, selezionare una casella di controllo per consentire all&#39;utente o al gruppo selezionato di eseguire un&#39;azione o deselezionare una casella di controllo per negare all&#39;utente o al gruppo selezionato di eseguire un&#39;azione. Per ulteriori informazioni, fate clic su **Dettagli**.

1. When finished, click **Save**.

### Impostazione dei privilegi di replica {#setting-replication-privileges}

Il privilegio di replica è il diritto di pubblicare contenuto e può essere impostato per gruppi e utenti.

>[!NOTE]
>
>* Tutti i diritti di replica applicati a un gruppo si applicano a tutti gli utenti del gruppo.
>* I privilegi di replica di un utente sostituiscono i privilegi di replica di un gruppo.
>* I diritti di replica Consenti hanno una precedenza superiore rispetto ai diritti di replica Rifiuta. Consulta [Autorizzazioni in AEM](#permissions-in-aem) per ulteriori informazioni.

>



Per impostare i privilegi di replica:

1. Selezionate l’utente o il gruppo dall’elenco, fate doppio clic per aprire, quindi fate clic su **Autorizzazioni**.
1. Nella griglia, individuate il percorso in cui desiderate che l&#39;utente disponga dei privilegi di replica o [ricerchi i nodi.](#searching-for-nodes)

1. Nella colonna **Replica** del percorso selezionato, selezionate una casella di controllo per aggiungere il privilegio di replica per l&#39;utente o il gruppo oppure deselezionate la casella di controllo per rimuovere il privilegio di replica. AEM visualizza un triangolo rosso ovunque siano state apportate modifiche non ancora salvate.

   ![cquserreplicatepermissions](assets/cquserreplicatepermissions.png)

1. Click **Save** to save your changes.

### Ricerca di nodi {#searching-for-nodes}

Quando aggiungete o rimuovete autorizzazioni, potete cercare il nodo oppure sfogliare.

Esistono due tipi diversi di ricerca dei percorsi:

* Ricerca percorso - Se la stringa di ricerca inizia con &quot;/&quot;, la ricerca cerca i nodi secondari diretti del percorso specificato:

![cqcartolarypathsearch](assets/cqsecuritypathsearch.png)

Nella casella di ricerca, potete effettuare le seguenti operazioni:

| Azione | Azioni |
|--- |--- |
| Tasto freccia destra | Seleziona un nodo secondario nel risultato della ricerca |
| Freccia giù | Avvia di nuovo la ricerca. |
| Tasto Invio | Seleziona un nodo secondario e lo carica nell&#39;albero |

* Ricerca fullText - Se la stringa di ricerca non inizia con &quot;/&quot;, viene eseguita una ricerca full-text su tutti i nodi sotto il percorso &quot;/content&quot;.

![cqcartolaryfulltextsearch](assets/cqsecurityfulltextsearch.png)

Per eseguire una ricerca su percorsi o testo completo:

1. Nella console Protezione, selezionate un utente o un gruppo e fate clic sulla scheda **Autorizzazioni** .

1. Nella casella Ricerca, immettere un termine da cercare.

### Impersonazione degli utenti {#impersonating-users}

Potete specificare uno o più utenti autorizzati a rappresentare l&#39;utente corrente. Ciò significa che possono cambiare le impostazioni dell&#39;account a quelle dell&#39;utente corrente e agire per conto di tale utente.

Utilizzare questa funzione con cautela, in quanto può consentire agli utenti di eseguire azioni che non possono essere eseguite dal proprio utente. Durante la rappresentazione di un utente, agli utenti viene notificato che non hanno eseguito l&#39;accesso come se stessi.

Esistono diversi scenari in cui potrebbe essere utile utilizzare questa funzionalità, tra cui:

* Se sei fuori ufficio, puoi permettere ad un&#39;altra persona di impersonarti mentre sei via. Utilizzando questa funzione, potete assicurarvi che qualcuno disponga dei diritti di accesso e non sia necessario modificare un profilo utente o fornire la password.
* Può essere utilizzato a scopo di debug. Ad esempio, per vedere come il sito Web cerca un utente con diritti di accesso limitati. Inoltre, se un utente si lamenta di problemi tecnici, puoi impersonare tale utente per diagnosticare e risolvere il problema.

Per rappresentare un utente esistente:

1. Nell’elenco ad albero, selezionate il nome della persona che desiderate assegnare ad altri utenti da rappresentare. Fate doppio clic per aprire.
1. Click the **Impersonators** tab.
1. Fate clic sull&#39;utente che desiderate poter rappresentare l&#39;utente selezionato. Trascinate l’utente (che rappresenterà) dall’elenco al riquadro Impersona. Il nome viene visualizzato nell’elenco.

   ![chlimage_1-115](assets/chlimage_1-115.png)

1. Fai clic su **Salva**.

### Impostazione delle preferenze utente e gruppo {#setting-user-and-group-preferences}

Per impostare le preferenze di utenti e gruppi, comprese la lingua, la gestione delle finestre e le preferenze delle barre degli strumenti:

1. Selezionate l’utente o il gruppo di cui desiderate modificare le preferenze nella struttura ad albero a sinistra. Per selezionare più utenti o gruppi, tenete premuto Ctrl o Maiusc e fate clic sulle selezioni.
1. Click the **Preferences** tab.

   ![cqsecurity preferences](assets/cqsecuritypreferences.png)

1. Apportate le modifiche necessarie alle preferenze di gruppo o utente e fate clic su **Salva** al termine.

### Impostazione di utenti o amministratori per concedere il privilegio di gestire altri utenti {#setting-users-or-administrators-to-have-the-privilege-to-manage-other-users}

Per impostare utenti o amministratori in modo che dispongano dei privilegi per eliminare/attivare/disattivare altri utenti:

1. Aggiungete l’utente a cui desiderate assegnare i privilegi per gestire altri utenti al gruppo di amministratori e salvate le modifiche.

   ![cqcartolaryaddmembertoadmin](assets/cqsecurityaddmembertoadmin.png)

1. Nella scheda **Autorizzazioni** dell&#39;utente, andate a &quot;/&quot; e nella colonna Replica, selezionate la casella di controllo per consentire la replica in &quot;/&quot; e fate clic su **Salva**.

   ![cqcartolaryreplicatepermissions](assets/cqsecurityreplicatepermissions.png)

   L&#39;utente selezionato ora può disattivare, attivare, eliminare e creare utenti.

### Estensione dei privilegi a livello di progetto {#extending-privileges-on-a-project-level}

Se intendete implementare i privilegi specifici dell’applicazione, le seguenti informazioni descrivono cosa dovete sapere per implementare un privilegio personalizzato e come applicarlo in CQ:

Il privilegio di modifica gerarchica è coperto da una combinazione di privilegi jcr. Il privilegio di replica è denominato **crx:repliche** memorizzato/valutato insieme ad altri privilegi nell&#39;archivio jcr. Essa non è tuttavia applicata a livello di CCR.

La definizione e la registrazione di privilegi personalizzati fa ufficialmente parte dell&#39;API [](https://jackrabbit.apache.org/api/2.8/org/apache/jackrabbit/api/security/authorization/PrivilegeManager.html) Jackrabbit dalla versione 2.4 (vedere anche [JCR-2887](https://issues.apache.org/jira/browse/JCR-2887)). Ulteriori informazioni sull&#39;utilizzo sono contenute in JCR Access Control Management, come definito da [JSR 283](https://jcp.org/en/jsr/detail?id=283) (sezione 16). Inoltre, l&#39;API Jackrabbit definisce un paio di estensioni.

Il meccanismo di registrazione dei privilegi si riflette nell&#39;interfaccia utente in Configurazione **** archivio.

La registrazione di nuovi privilegi (personalizzati) è di per sé protetta da un privilegio incorporato che deve essere concesso a livello di repository (in JCR: passando &#39;null&#39; come parametro &#39;absPath&#39; nell&#39;API mgt ac, vedete jsr 333 per ulteriori dettagli). Per impostazione predefinita, **l&#39;amministratore** e tutti i membri degli amministratori dispongono di tale privilegio.

>[!NOTE]
>
>Mentre l&#39;implementazione si occupa della convalida e della valutazione dei privilegi personalizzati, non può applicarli a meno che non siano aggregati di privilegi predefiniti.
