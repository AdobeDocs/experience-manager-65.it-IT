---
title: Amministrazione di diritti di accesso, gruppi e utenti
seo-title: Amministrazione di diritti di accesso, gruppi e utenti
description: Scopri ulteriori informazioni sull’amministrazione di diritti di accesso, gruppi e utenti in AEM.
seo-description: Scopri ulteriori informazioni sull’amministrazione di diritti di accesso, gruppi e utenti in AEM.
uuid: 26d7bb25-5a38-43c6-bd6a-9ddba582c60f
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 66674e47-d19f-418f-857f-d91cf8660b6d
docset: aem65
translation-type: tm+mt
source-git-commit: 4b965d8f7814816126601f6366c1ba313e404538

---


# Amministrazione di diritti di accesso, gruppi e utenti{#user-group-and-access-rights-administration}

L&#39;abilitazione dell&#39;accesso a un archivio CRX include diversi argomenti:

* [Diritti](#how-access-rights-are-evaluated) di accesso - Concetti di modo in cui vengono definiti e valutati
* [Amministrazione](#user-administration) utente - gestione dei singoli account utilizzati per l&#39;accesso
* [Amministrazione](#group-administration) dei gruppi: gestione semplificata degli utenti tramite la formazione di gruppi
* [Accesso a Gestione](#access-right-management) diritti - definizione di criteri per il controllo di come tali utenti e gruppi possono accedere alle risorse

Gli elementi di base sono:

**Account** utente CRX autentica l&#39;accesso identificando e verificando un utente (da tale persona o altra applicazione) in base ai dettagli contenuti nell&#39;account utente.

In CRX ogni account utente è un nodo nell’area di lavoro. Un account utente CRX ha le seguenti proprietà:

* Rappresenta un utente di CRX.
* Contiene un nome utente e una password.
* È applicabile a tale area di lavoro.
* Non può avere utenti secondari. Per i diritti di accesso gerarchici è necessario utilizzare i gruppi.

* Potete specificare i diritti di accesso per l&#39;account utente.

   Tuttavia, per semplificare la gestione, consigliamo di assegnare (nella maggior parte dei casi) i diritti di accesso agli account dei gruppi. La gestione dei diritti di accesso per ogni singolo utente diventa molto difficile (le eccezioni sono determinati utenti del sistema quando esistono solo una o due istanze).

**Account** di gruppo Gli account di gruppo sono raccolte di utenti e/o di altri gruppi. Questi vengono utilizzati per semplificare la gestione, in quanto una modifica dei diritti di accesso assegnati a un gruppo viene applicata automaticamente a tutti gli utenti del gruppo. Un utente non deve appartenere ad alcun gruppo, ma spesso appartiene a diversi.

In CRX un gruppo ha le seguenti proprietà:

* Rappresenta un gruppo di utenti con diritti di accesso comuni. Ad esempio, autori o sviluppatori.
* È applicabile a tale area di lavoro.
* Può avere membri; possono essere singoli utenti o altri gruppi.
* Il raggruppamento gerarchico può essere raggiunto con le relazioni tra membri. Non potete inserire un gruppo direttamente sotto un altro gruppo nella directory archivio.
* Potete definire i diritti di accesso per tutti i membri del gruppo.

**I diritti** di accesso CRX utilizzano i diritti di accesso per controllare l&#39;accesso a aree specifiche del repository.

Questo avviene assegnando privilegi per consentire o negare l’accesso a una risorsa (nodo o percorso) nell’archivio. Poiché è possibile assegnare vari privilegi, questi devono essere valutati per determinare quale combinazione è applicabile alla richiesta corrente.

CRX consente di configurare i diritti di accesso per gli account utente e per i gruppi. Gli stessi principi di base di valutazione sono poi applicati a entrambi.

## Valutazione dei diritti di accesso {#how-access-rights-are-evaluated}

>[!NOTE]
>
>CRX implementa il controllo di [accesso come definito da JSR-283](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html).
>
>Un&#39;installazione standard di un repository CRX è configurata per l&#39;utilizzo di elenchi di controllo di accesso basati sulle risorse. Questa è una possibile implementazione del controllo di accesso JSR-283 e una delle implementazioni presenti con Jackrabbit.

### Soggetti e entità {#subjects-and-principals}

CRX utilizza due concetti chiave per valutare i diritti di accesso:

* Un&#39; **entità** è un&#39;entità che possiede diritti di accesso. Le entità includono:

   * Un account utente
   * Un account di gruppo

      Se un account utente appartiene a uno o più di questi gruppi, viene anche associato a ciascuno di tali entità gruppo.

* Un **oggetto** viene utilizzato per rappresentare l’origine di una richiesta.

   Viene utilizzato per consolidare i diritti di accesso applicabili a tale richiesta. Sono tratti da:

   * L&#39;entità utente

      I diritti assegnati direttamente all’account utente.

   * Tutte le entità dei gruppi associate a tale utente

      Tutti i diritti assegnati a uno qualsiasi dei gruppi a cui l&#39;utente appartiene.
   Il risultato viene quindi utilizzato per consentire o negare l&#39;accesso alla risorsa richiesta.

#### Compilazione dell&#39;elenco dei diritti di accesso per un oggetto {#compiling-the-list-of-access-rights-for-a-subject}

In CRX il soggetto dipende da:

* l&#39;entità utente
* tutte le entità gruppo associate a tale utente

L&#39;elenco dei diritti di accesso applicabili all&#39;oggetto è costituito da:

* i diritti assegnati direttamente all&#39;account utente
* più tutti i diritti assegnati a uno qualsiasi dei gruppi a cui l&#39;utente appartiene

![chlimage_1-56](assets/chlimage_1-56.png)

>[!NOTE]
>
>* Quando compila l’elenco, CRX non tiene conto della gerarchia di utenti.
>* CRX utilizza una gerarchia di gruppi solo quando si inserisce un gruppo come membro di un altro gruppo. Nessuna ereditarietà automatica delle autorizzazioni del gruppo.
>* L&#39;ordine in cui specificate i gruppi non influisce sui diritti di accesso.
>



### Risoluzione dei diritti di richiesta e accesso {#resolving-request-and-access-rights}

Quando CRX gestisce la richiesta, confronta la richiesta di accesso dell&#39;oggetto con l&#39;elenco di controllo di accesso nel nodo del repository:

Pertanto, se Linda richiede di aggiornare il `/features` nodo nella seguente struttura del repository:

![chlimage_1-57](assets/chlimage_1-57.png)

### Ordine di precedenza {#order-of-precedence}

I diritti di accesso in CRX sono valutati come segue:

* Le entità utente hanno sempre la precedenza sulle entità gruppo, indipendentemente da quanto segue:

   * ordine nell&#39;elenco di controllo di accesso
   * posizione nella gerarchia dei nodi

* Per un&#39;entità specificata esiste (al massimo) 1 rifiuto e 1 autorizzazione di ingresso in un dato nodo. L&#39;implementazione cancella sempre le voci ridondanti e verifica che lo stesso privilegio non sia elencato sia nelle voci allow che Negative.

>[!NOTE]
>
>Questo processo di valutazione è appropriato per il controllo dell&#39;accesso basato sulle risorse di un&#39;installazione standard CRX.

Seguono due esempi in cui l’utente `aUser` è membro del gruppo `aGroup`:

```xml
   + parentNode
     + acl
       + ace: aUser - deny - write
     + childNode
       + acl
         + ace: aGroup - allow - write
       + grandChildNode
```

Nel caso di cui sopra:

* `aUser` non viene concessa l&#39;autorizzazione di scrittura su `grandChildNode`.

```xml
   + parentNode
     + acl
       + ace: aUser - deny - write
     + childNode
       + acl
         + ace: aGroup - allow - write
         + ace: aUser - deny - write
       + grandChildNode
```

In questo caso:

* `aUser` non viene concessa l&#39;autorizzazione di scrittura su `grandChildNode`.
* Il secondo ACE per `aUser` è ridondante.

I diritti di accesso da entità di più gruppi vengono valutati in base al loro ordine, sia all&#39;interno della gerarchia che all&#39;interno di un unico elenco di controllo di accesso.

### Best practice {#best-practices}

Nella tabella seguente sono elencate alcune raccomandazioni e best practice:

<table>
 <tbody>
  <tr>
   <td>Consiglio...</td>
   <td>Motivo...</td>
  </tr>
  <tr>
   <td><i>Usa gruppi</i></td>
   <td><p>Evitate di assegnare i diritti di accesso in base agli utenti. I motivi sono molteplici:</p>
    <ul>
     <li>Gli utenti sono molti più numerosi dei gruppi, quindi i gruppi semplificano la struttura.</li>
     <li>I gruppi forniscono una panoramica su tutti gli account.</li>
     <li>L'ereditarietà è più semplice con i gruppi.</li>
     <li>Gli utenti vanno e vengono. I gruppi sono a lungo termine.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><i>Sii positivo</i></td>
   <td><p>Utilizzare sempre le istruzioni Allow (Consenti) per specificare i diritti di accesso dell'entità del gruppo (ove possibile). Evitare di utilizzare un'istruzione Rifiuta.</p> <p>Le entità dei gruppi vengono valutate in ordine, sia all'interno della gerarchia che nell'ordine all'interno di un unico elenco di controllo di accesso.</p> </td>
  </tr>
  <tr>
   <td><i>Mantieni semplice</i></td>
   <td><p>Investire un po' di tempo e pensare quando si configura una nuova installazione sarà ben ripagato.</p> <p>L'applicazione di una struttura chiara semplificherà la manutenzione e l'amministrazione in corso, garantendo che sia i colleghi attuali che i futuri successori possano capire facilmente cosa viene implementato.</p> </td>
  </tr>
  <tr>
   <td><i>Prova</i></td>
   <td>Utilizzate un'installazione di test per esercitarvi e assicurarvi di comprendere le relazioni tra i vari utenti e gruppi.</td>
  </tr>
  <tr>
   <td><i>Utenti/gruppi predefiniti</i></td>
   <td>Aggiornate sempre gli utenti e i gruppi predefiniti subito dopo l’installazione per evitare problemi di sicurezza.</td>
  </tr>
 </tbody>
</table>

## Amministrazione utente {#user-administration}

Viene utilizzata una finestra di dialogo standard per l’amministrazione **** utente.

Devi aver effettuato l’accesso nell’area di lavoro appropriata, quindi puoi accedere alla finestra di dialogo da entrambi:

* il collegamento Amministrazione **** utente sulla console principale di CRX
* il menu **Protezione** di CRX Explorer

![chlimage_1-58](assets/chlimage_1-58.png)

**Proprietà**

* **UserID**

   Nome breve per l&#39;account, utilizzato per accedere a CRX.

* **Nome entità**

   Un nome full text per l’account.

* **Password**

   Necessario per accedere a CRX con questo account.

* **ntlmhash**

   Assegnato automaticamente per ogni nuovo account e aggiornato quando la password viene modificata.

* È possibile aggiungere nuove proprietà definendo un nome, un tipo e un valore. Fate clic su Salva (simbolo di spunta verde) per ciascuna nuova proprietà.

**Iscrizione al gruppo**

Vengono visualizzati tutti i gruppi a cui appartiene l&#39;account. La colonna Ereditata indica l&#39;appartenenza ereditata a seguito dell&#39;appartenenza di un altro gruppo.

Facendo clic su un GroupID (se disponibile) si aprirà l&#39;Amministrazione [](#group-administration) gruppo per quel gruppo.

**Impersonatori**

Grazie alla funzionalità Impersona, un utente può lavorare per conto di un altro utente.

Ciò significa che un account utente può specificare altri account (utente o gruppo) che possono funzionare con il proprio account. In altre parole, se l&#39;utente-B è autorizzato a rappresentare l&#39;utente-A, l&#39;utente-B può intraprendere azioni utilizzando i dettagli account completi dell&#39;utente-A (inclusi ID, nome e diritti di accesso).

Questo consente agli account del soggetto di completare le attività come se utilizzassero l&#39;account che stanno impersonando; ad esempio, durante un&#39;assenza o per condividere un carico eccessivo a breve termine.

Se un account ne rappresenta un altro è molto difficile da vedere. I file di registro non contengono informazioni sul fatto che la rappresentazione si è verificata sugli eventi. Quindi se l&#39;utente-B rappresenta l&#39;utente-A, tutti gli eventi avranno l&#39;aspetto di essere eseguiti personalmente dall&#39;utente-A.

### Creazione di un account utente {#creating-a-user-account}

1. Aprite la finestra di dialogo Amministrazione **** utente.
1. Fate clic su **Crea utente**.
1. È quindi possibile inserire le proprietà:

   * **UserID** utilizzato come nome account.
   * **Password** necessaria per l’accesso.
   * **Nome** entità per fornire un nome di testo completo.
   * **Percorso** intermedio che può essere utilizzato per creare una struttura ad albero.

1. Fare clic sul simbolo di spunta Salva (verde).
1. La finestra di dialogo viene espansa per consentire di:

   1. Configure **Properties**.
   1. Consultate Appartenenza **al** gruppo.
   1. Definire **Impersonatori**.

>[!NOTE]
>
>Talvolta, quando si registrano nuovi utenti in installazioni con un numero elevato di:
>
>* utenti
>* gruppi con molti membri
>



### Aggiornamento di un account utente {#updating-a-user-account}

1. Con la finestra di dialogo Amministrazione **** utente, aprite la vista a elenco di tutti gli account.
1. Navigare nella struttura ad albero.
1. Fate clic sull’account richiesto per aprire la modifica.
1. Apportate una modifica e fate clic su Salva (simbolo di spunta verde) per tale voce.
1. **Fate clic su** Chiudi **per terminare oppure su** Elenco... per tornare all&#39;elenco di tutti gli account utente.

### Rimozione di un account utente {#removing-a-user-account}

1. Con la finestra di dialogo Amministrazione **** utente, aprite la vista a elenco di tutti gli account.
1. Navigare nella struttura ad albero.
1. Selezionate l’account richiesto e fate clic su **Rimuovi utente**; l&#39;account verrà eliminato immediatamente.

>[!NOTE]
>
>Questo rimuove il nodo per l&#39;entità dall&#39;archivio.
>
>Le voci dei diritti di accesso non vengono rimosse. Questo assicura l&#39;integrità storica.

### Definizione delle proprietà {#defining-properties}

È possibile definire **Proprietà** per account nuovi o esistenti:

1. Aprite la finestra di dialogo Amministrazione **** utente per l’account appropriato.
1. Definire un nome di **proprietà** .
1. Select the **Type** from the drop-down list.
1. Definire il **valore**.
1. Fate clic su Salva (simbolo di clic verde) per la nuova proprietà.

Le proprietà esistenti possono essere eliminate con il simbolo del cestino.

Ad eccezione di Password, le proprietà non possono essere modificate, devono essere eliminate e ricreati.

#### Modifica della password {#changing-the-password}

La **password** è una proprietà speciale che può essere modificata facendo clic sul collegamento **Cambia password** .

È inoltre possibile cambiare la password al proprio account utente dal menu **Protezione** di CRX Explorer.

### Definizione di un impersonatore {#defining-an-impersonator}

Puoi definire gli autori per account nuovi o esistenti:

1. Aprite la finestra di dialogo Amministrazione **** utente per l’account appropriato.
1. Specificate l&#39;account da consentire di rappresentare tale account.

   Puoi usare Sfoglia... per selezionare un account esistente.

1. Fate clic su Salva (simbolo di spunta verde) per la nuova proprietà.

## Amministrazione gruppo {#group-administration}

Per Amministrazione **** gruppo viene utilizzata una finestra di dialogo standard.

Devi aver effettuato l’accesso nell’area di lavoro appropriata, quindi puoi accedere alla finestra di dialogo da entrambi:

* il collegamento Amministrazione **** gruppo sulla console principale di CRX
* il menu **Protezione** di CRX Explorer

![chlimage_1-8](assets/chlimage_1-8.jpeg)

**Proprietà**

* **GroupID**

   Nome breve per l’account del gruppo.

* **Nome entità**

   Un nome full text per l’account del gruppo.

* È possibile aggiungere nuove proprietà definendo un nome, un tipo e un valore. Fate clic su Salva (simbolo di spunta verde) per ciascuna nuova proprietà.

* **Membri**

   Potete aggiungere utenti o altri gruppi come membri di questo gruppo.

**Iscrizione al gruppo**

Vengono visualizzati tutti i gruppi a cui appartiene l&#39;account del gruppo corrente. La colonna Ereditata indica l&#39;appartenenza ereditata a seguito dell&#39;appartenenza di un altro gruppo.

Facendo clic su un ID gruppo si aprirà la finestra di dialogo per il gruppo.

**Membri**

Elenca tutti gli account (utenti e/o gruppi) che sono membri del gruppo corrente.

La colonna **Ereditata** indica l&#39;appartenenza ereditata a seguito dell&#39;appartenenza a un altro gruppo.

>[!NOTE]
>
>Quando il ruolo Proprietario, Editor o Visualizzatore viene assegnato a un utente in qualsiasi cartella di risorse, viene creato un nuovo gruppo. Il nome del gruppo corrisponde al formato `mac-default-<foldername>` per ciascuna cartella in cui sono definiti i ruoli.

### Creazione di un account di gruppo {#creating-a-group-account}

1. Aprite la finestra di dialogo Amministrazione **** gruppo.
1. Fate clic su **Crea gruppo**.
1. È quindi possibile inserire le proprietà:

   * **Nome** entità per fornire un nome di testo completo.
   * **Percorso** intermedio che può essere utilizzato per creare una struttura ad albero.

1. Fare clic sul simbolo di spunta Salva (verde).
1. La finestra di dialogo viene espansa per consentire di:

   1. Configure **Properties**.
   1. Consultate Appartenenza **al** gruppo.
   1. Gestisci **membri**.

### Aggiornamento di un account di gruppo {#updating-a-group-account}

1. Con la finestra di dialogo Amministrazione **** gruppo, aprite la vista a elenco di tutti gli account.
1. Navigare nella struttura ad albero.
1. Fate clic sull’account richiesto per aprire la modifica.
1. Apportate una modifica e fate clic su Salva (simbolo di spunta verde) per tale voce.
1. **Fate clic su** Chiudi **per terminare oppure su** Elenco... per tornare all&#39;elenco di tutti gli account dei gruppi.

### Rimozione di un account di gruppo {#removing-a-group-account}

1. Con la finestra di dialogo Amministrazione **** gruppo, aprite la vista a elenco di tutti gli account.
1. Navigare nella struttura ad albero.
1. Selezionate l’account richiesto e fate clic su **Rimuovi gruppo**; l&#39;account verrà eliminato immediatamente.

>[!NOTE]
>
>Questo rimuove il nodo per l&#39;entità dall&#39;archivio.
>
>Le voci dei diritti di accesso non vengono rimosse. Questo assicura l&#39;integrità storica.

### Definizione delle proprietà {#defining-properties-1}

È possibile definire le proprietà per gli account nuovi o esistenti:

1. Aprite la finestra di dialogo Amministrazione **** gruppo per l’account appropriato.
1. Definire un nome di **proprietà** .
1. Select the **Type** from the drop-down list.
1. Definire il **valore**.
1. Fate clic su Salva (simbolo di spunta verde) per la nuova proprietà.

Le proprietà esistenti possono essere eliminate con il simbolo del cestino.

### Membri {#members}

È possibile aggiungere membri al gruppo corrente:

1. Aprite la finestra di dialogo Amministrazione **** gruppo per l’account appropriato.
1. Effettua una delle seguenti operazioni:

   * Immettete il nome del membro richiesto (account utente o gruppo).
   * **Oppure utilizza** Sfoglia... per cercare e selezionare l&#39;entità (account utente o gruppo) che si desidera aggiungere.

1. Fate clic su Salva (simbolo di spunta verde) per la nuova proprietà.

Oppure eliminate un membro esistente con il simbolo del cestino.

## Accesso a Right Management {#access-right-management}

Con la scheda Controllo **** accesso di CRXDE Lite è possibile definire i criteri di controllo degli accessi e assegnare i relativi privilegi.

Ad esempio, per Percorso **** corrente, selezionate la risorsa richiesta nel riquadro a sinistra, la scheda Controllo accesso nel riquadro in basso a destra:

![crx_accesscontrol_tab](assets/crx_accesscontrol_tab.png)

Le politiche sono classificate in base a:

* **Criteri di controllo di accesso applicabili**

   Tali criteri possono essere applicati.

   Si tratta di criteri disponibili per la creazione di un criterio locale. Dopo aver selezionato e aggiunto un criterio applicabile, diventa un criterio locale.

* **Criteri di controllo dell&#39;accesso locali**

   Si tratta dei criteri di controllo degli accessi applicati. Potete quindi aggiornarli, ordinarli o rimuoverli.

   Un criterio locale ignora i criteri ereditati dall&#39;elemento padre.

* **Criteri di controllo dell&#39;accesso effettivi**

   Questi sono i criteri di controllo degli accessi che vengono applicati a qualsiasi richiesta di accesso. Esse mostrano i criteri aggregati derivati sia dai criteri locali che da quelli ereditati dall&#39;elemento padre.

### Selezione criteri {#policy-selection}

È possibile selezionare i criteri per:

* **Percorso corrente**

   Come nell’esempio precedente, selezionate una risorsa all’interno della directory archivio. Verranno visualizzati i criteri per questo &quot;percorso corrente&quot;.

* **Archivio**

   Seleziona il controllo di accesso a livello di repository. Ad esempio, quando si imposta il `jcr:namespaceManagement` privilegio, che è pertinente solo per l&#39;archivio, non un nodo.

* **Principale**

   Entità registrata nella directory archivio.

   Potete digitare il nome dell&#39; **entità** oppure fare clic sull&#39;icona a destra del campo per aprire la finestra di dialogo **Seleziona entità** .

   Consente di **cercare** un **utente** o un **gruppo**. Selezionate l&#39;entità desiderata dall&#39;elenco risultante, quindi fate clic su **OK** per riportare il valore nella finestra di dialogo precedente.

![crx_accesscontrol_selectprincipal](assets/crx_accesscontrol_selectprincipal.png)

>[!NOTE]
>
>Per semplificare la gestione, consigliamo di assegnare diritti di accesso agli account di gruppo, non ai singoli account utente.
>
>È più facile gestire alcuni gruppi, piuttosto che molti account utente.

### Privilegi {#privileges}

I seguenti privilegi sono disponibili per la selezione quando si aggiunge una voce di controllo di accesso (consultate API [di](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/security/Privilege.html) protezione per informazioni complete):

<table>
 <tbody>
  <tr>
   <th><strong>Nome privilegio</strong></th>
   <th><strong>Che controlla il privilegio a...</strong></th>
  </tr>
  <tr>
   <td><code>jcr:read</code></td>
   <td>Recuperare un nodo e leggerne le proprietà e i relativi valori.</td>
  </tr>
  <tr>
   <td><code>rep:write</code></td>
   <td>Si tratta di un privilegio aggregato specifico del coniglio di jcr:write e jcr:nodeTypeManagement.<br /> </td>
  </tr>
  <tr>
   <td><code>jcr:all</code></td>
   <td>Si tratta di un privilegio di aggregazione che contiene tutti gli altri privilegi predefiniti.</td>
  </tr>
  <tr>
   <td><strong>Avanzate</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><code>crx:replicate</code></td>
   <td>Eseguire la replica di un nodo.</td>
  </tr>
  <tr>
   <td><code>jcr:addChildNodes</code></td>
   <td>Creare nodi secondari di un nodo.</td>
  </tr>
  <tr>
   <td><code>jcr:lifecycleManagement</code></td>
   <td>Eseguire operazioni del ciclo di vita su un nodo.</td>
  </tr>
  <tr>
   <td><code>jcr:lockManagement</code></td>
   <td>Bloccare e sbloccare un nodo; aggiornare un blocco.</td>
  </tr>
  <tr>
   <td><code>jcr:modifyAccessControl</code></td>
   <td>Modificare i criteri di controllo di accesso di un nodo.</td>
  </tr>
  <tr>
   <td><code>jcr:modifyProperties</code></td>
   <td>Creare, modificare e rimuovere le proprietà di un nodo.</td>
  </tr>
  <tr>
   <td><code>jcr:namespaceManagement</code></td>
   <td>Registrazione, annullamento della registrazione e modifica delle definizioni dello spazio nomi.</td>
  </tr>
  <tr>
   <td><code>jcr:nodeTypeDefinitionManagement</code></td>
   <td>Importa le definizioni dei tipi di nodo nella directory archivio.</td>
  </tr>
  <tr>
   <td><code>jcr:nodeTypeManagement</code></td>
   <td>Aggiungete e rimuovete i tipi di nodo del mixin e modificate il tipo di nodo principale di un nodo. Sono incluse anche tutte le chiamate ai metodi di importazione Node.addNode e XML in cui il mixin o il tipo principale del nuovo nodo è esplicitamente specificato.</td>
  </tr>
  <tr>
   <td><code>jcr:readAccessControl</code></td>
   <td>Leggere i criteri di controllo di accesso di un nodo.</td>
  </tr>
  <tr>
   <td><code>jcr:removeChildNodes</code></td>
   <td>Rimuovere i nodi secondari di un nodo.</td>
  </tr>
  <tr>
   <td><code>jcr:removeNode</code></td>
   <td>Rimuovere un nodo.</td>
  </tr>
  <tr>
   <td><code>jcr:retentionManagement</code></td>
   <td>Eseguire operazioni di gestione della conservazione su un nodo.</td>
  </tr>
  <tr>
   <td><code>jcr:versionManagement</code></td>
   <td>Eseguire operazioni di controllo delle versioni su un nodo.</td>
  </tr>
  <tr>
   <td><code>jcr:workspaceManagement</code></td>
   <td>Creazione ed eliminazione di aree di lavoro tramite l'API JCR.</td>
  </tr>
  <tr>
   <td><code>jcr:write</code></td>
   <td><br /> Si tratta di un privilegio di aggregazione che contiene: - jcr:editProperties<br /> - jcr:addChildNodes<br /> - jcr:removeNode<br /> - jcr:removeChildNodes</td>
  </tr>
  <tr>
   <td><code>rep:privilegeManagement</code></td>
   <td>Registra nuovo privilegio.</td>
  </tr>
 </tbody>
</table>

### Registrazione di nuovi privilegi {#registering-new-privileges}

Potete anche registrare nuovi privilegi:

1. Dalla barra degli strumenti selezionare **Strumenti**, quindi **Privilegi** per visualizzare i privilegi attualmente registrati.

   ![ac_Privilegi](assets/ac_privileges.png)

1. Utilizzate l&#39;icona **Registra privilegio** (**+**) per aprire la finestra di dialogo e definire un nuovo privilegio:

   ![ac_Privilegeregister](assets/ac_privilegeregister.png)

1. Fai clic su **OK** per salvare. Il privilegio sarà ora disponibile per la selezione.

### Aggiunta di una voce di controllo di accesso {#adding-an-access-control-entry}

1. Selezionate la risorsa e aprite la scheda Controllo **** accesso.

1. Per aggiungere un nuovo criterio **di controllo degli accessi** locali, fare clic sull&#39;icona **+** a destra dell&#39;elenco Criteri **di controllo degli accessi** applicabili:

   ![crx_accesscontrol_applicabile](assets/crx_accesscontrol_applicable.png)

1. Una nuova voce viene visualizzata in Criteri di controllo accesso **locale:**

   ![crx_accesscontrol_newlocal](assets/crx_accesscontrol_newlocal.png)

1. Fate clic sull’icona **+** per aggiungere una nuova voce:

   ![crx_accesscontrol_addentry](assets/crx_accesscontrol_addentry.png)

   >[!NOTE]
   >
   >Attualmente è necessaria una soluzione alternativa per specificare una stringa vuota.
   >
   >Per questo è necessario utilizzare &quot;&quot;.

1. Definite i criteri di controllo degli accessi e fate clic su **OK** per salvare. La nuova politica:

   * essere elencati in Criteri di controllo degli accessi **locali**
   * le modifiche si rifletteranno sulle politiche di controllo dell&#39;accesso **efficaci**.

CRX convalida la selezione; per una data entità esiste (al massimo) 1 diniego e 1 permette l&#39;ingresso su un dato nodo. L&#39;implementazione cancella sempre le voci ridondanti e verifica che lo stesso privilegio non sia elencato sia nelle voci allow che Negative.

### Ordering Local Access Control Policies {#ordering-local-access-control-policies}

L&#39;ordine nell&#39;elenco indica l&#39;ordine in cui i criteri vengono applicati.

1. Nella tabella Criteri **di controllo di accesso** locale selezionare la voce desiderata e trascinarla nella nuova posizione nella tabella.

   ![crx_accesscontrol_reorder](assets/crx_accesscontrol_reorder.png)

1. Le modifiche verranno visualizzate nelle tabelle per i criteri di controllo degli accessi **locali** e **effettivi**.

### Rimozione di un criterio di controllo di accesso {#removing-an-access-control-policy}

1. Nella tabella Criteri **controllo accesso** locale fare clic sull&#39;icona rossa (-) a destra della voce.
1. La voce verrà rimossa dalle tabelle per i criteri di controllo degli accessi **locali** e **effettivi**.

### Verifica di un criterio di controllo degli accessi {#testing-an-access-control-policy}

1. **Dalla barra degli strumenti CRXDE Lite selezionare** Strumenti **, quindi** Controllo accesso di prova... .
1. Nel riquadro in alto a destra si apre una nuova finestra di dialogo. Selezionate il **percorso** e/o l’ **entità** da verificare.
1. Fate clic su **Test** per visualizzare i risultati della selezione:

   ![crx_accesscontrol_test](assets/crx_accesscontrol_test.png)