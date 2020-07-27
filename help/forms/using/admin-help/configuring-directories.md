---
title: Configurazione delle directory
seo-title: Configurazione delle directory
description: Scoprite come aggiungere, modificare ed eliminare directory e configurare la gestione degli utenti per utilizzare la visualizzazione a elenco virtuale.
seo-description: Scoprite come aggiungere, modificare ed eliminare directory e configurare la gestione degli utenti per utilizzare la visualizzazione a elenco virtuale.
uuid: 0bf1a8a7-c917-4248-9937-d24e31c5ba17
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 1f15f028-aa81-478e-97eb-f83a4dc0418c
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '3246'
ht-degree: 0%

---


# Configurazione delle directory {#configuring-directories}

Per ciascun dominio Enterprise configurato, specificate le directory richieste dal provider di autenticazione per le informazioni utente. Potete configurare più directory per un dominio.

## Aggiunta di directory o SPI personalizzati {#adding-directories-or-custom-spis}

Per ciascun dominio Enterprise configurato, specificate le directory richieste dal provider di autenticazione per le informazioni utente. È possibile aggiungere una directory a un dominio enterprise esistente o a un nuovo dominio enterprise che si sta aggiungendo. Potete configurare più directory per un dominio. È inoltre possibile configurare un dominio per l&#39;utilizzo di un&#39;interfaccia SPI (Service Provider Interface) personalizzata per la sincronizzazione.

### Aggiungere una directory {#add-a-directory}

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fate clic su Nuovo dominio Enterprise o selezionate un dominio enterprise esistente.
1. Fate clic su Aggiungi directory.
1. Nella casella Nome profilo digitare un nome per distinguere la directory, quindi fare clic su Avanti.
1. Configurare le impostazioni del server di directory. Consultate Impostazioni [](configuring-directories.md#directory-settings)della directory.
1. Per verificare se è possibile stabilire una connessione al server LDAP, fate clic su Prova. Se il test ha esito negativo, controllate l&#39;eccezione nel file di registro di Application Server per determinare la causa principale dell&#39;errore. Fate clic su Chiudi, quindi su Avanti.
1. Selezionate Impostazioni utente e configurate le impostazioni in base alle vostre esigenze. Consultate Impostazioni [](configuring-directories.md#directory-settings)della directory.
1. Per verificare che il DN di base e altri attributi configurati raccolgano il batch corretto di utenti, fate clic su Test. LDAP tenta di recuperare i primi 200 record utilizzando le impostazioni fornite (come il DN di base, il filtro di ricerca e tutti gli attributi).

   Se gli utenti vengono restituiti, i risultati mostrano i valori assegnati a ciascun campo in base all&#39;insieme di attributi. Se il test ha esito negativo a causa di un nome server inesistente, informazioni di autorizzazione errate o attributi errati, viene visualizzato il seguente messaggio di errore: &quot;I criteri di ricerca specificati non hanno restituito alcun risultato&quot;. Per determinare la causa principale dell&#39;errore, esaminare l&#39;eccezione nel file di registro di Application Server. Fate clic su Chiudi, quindi su Avanti.

1. Selezionate Impostazioni gruppo e configurate le impostazioni in base alle vostre esigenze. Consultate Impostazioni [](configuring-directories.md#directory-settings)della directory.
1. Per verificare che il DN di base e altri attributi configurati raccolgano il batch corretto di gruppi, fate clic su Test. Se vengono restituiti i gruppi, i risultati mostrano i valori assegnati a ciascun campo in base all&#39;insieme di attributi. Fai clic su Chiudi.

### Aggiungere un&#39;API personalizzata {#add-a-custom-spi}

Per informazioni sulla creazione di un&#39;API personalizzata, consultate &quot;Developing SPIs for AEM forms&quot; (Sviluppo di SPI per moduli AEM) in [Programmazione con i moduli](https://www.adobe.com/go/learn_aemforms_programming_63)AEM. Per rendere disponibile un nuovo SPI personalizzato distribuito per l&#39;associazione con il dominio, riavviare il server.

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fate clic su Nuovo dominio Enterprise o selezionate un dominio enterprise esistente.
1. Fate clic su Aggiungi directory.
1. Digitate un nome nella casella Nome profilo, selezionate Fornitore SPI personalizzato, quindi fate clic su Avanti.
1. Selezionate un provider utente personalizzato dall’elenco e fate clic su Avanti.
1. Selezionate un provider di gruppi personalizzato dall’elenco e fate clic su Fine.

## Modificare una directory {#edit-a-directory}

Potete modificare i dettagli di una directory precedentemente configurata.

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fare clic sul dominio appropriato nell&#39;elenco e, sulla pagina visualizzata, selezionare la directory appropriata dall&#39;elenco.
1. Configurate le impostazioni di directory, utenti e gruppi come necessario. Consultate Impostazioni [](configuring-directories.md#directory-settings)della directory.
1. Fai clic su OK.

## Eliminare una directory {#delete-a-directory}

Quando sincronizzate i domini dopo l’eliminazione di una directory, tutti gli utenti e i gruppi in tale directory vengono contrassegnati obsoleti nel database. Non verranno restituiti in alcuna ricerca dalla console di amministrazione.

>[!NOTE]
>
>I domini Enterprise richiedono almeno un provider di autenticazione e un provider di directory.

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fare clic sul dominio appropriato nell&#39;elenco.
1. Selezionate la casella di controllo relativa alla directory appropriata e fate clic su Elimina.
1. Fare clic su OK nella pagina di conferma visualizzata e fare di nuovo clic su OK.

## Impostazioni directory {#directory-settings}

Quando aggiungete una directory a un dominio, specificate le seguenti impostazioni di directory.

**Server:** (Obbligatorio) Nome di dominio completo (FQDN, Fully Qualified Domain Name) del server di directory. Ad esempio, per un computer chiamato x sulla rete corp.adobe.com, l&#39;FQDN è x.corp.adobe.com. Un indirizzo IP può essere usato al posto del nome del server FQDN.

**Porta:** (Obbligatorio) La porta utilizzata dal server di directory. In genere 389 o 636 se il protocollo SSL (Secure Sockets Layer) è utilizzato per inviare informazioni di autenticazione attraverso la rete.

**SSL:** (Obbligatorio) Specifica se il server di directory utilizza SSL quando invia dati sulla rete. Il valore predefinito è No. Se si imposta su Sì, il certificato del server LDAP corrispondente deve essere considerato affidabile dall&#39;ambiente runtime Java™ (JRE) del server dell&#39;applicazione.

**Binding** (obbligatorio) Specifica come accedere alla directory.

**Anonimo:** Non è richiesto alcun nome utente o password. Un utente anonimo può recuperare solo una quantità limitata di dati. Questa opzione può essere utile per il test iniziale.

**Utente:** L&#39;autenticazione è obbligatoria. Nella casella Nome, specificare il nome del record utente che può accedere alla directory. È consigliabile immettere il nome distinto completo (DN) dell&#39;account utente, ad esempio cn=Jane Doe, ou=user, dc=can, dc=com. Nella casella Password, specificare la password associata. Queste impostazioni sono necessarie quando si seleziona Utente come opzione di binding.

**Nome:** Nome che può essere usato per connettersi al database LDAP quando l’accesso anonimo non è abilitato. Per Active Directory 2003, specificare `[domain name]\[userid]`. Per Sun™ One, eDirectory o IBM Tivoli Directory Server, specificate il nome completo dell&#39;utente, ad esempio uid=lcuser,ou=it,o=company.com.

**Password:** Password corrispondente al nome specificato per la connessione al database LDAP quando l’accesso anonimo non è abilitato.

**Compila pagina con:** Quando è selezionata questa opzione, compila gli attributi nelle pagine delle impostazioni Utente e Gruppo con i corrispondenti valori LDAP predefiniti.

**Recupera DN di base:** Recupera i DN di base e li visualizza nell&#39;elenco a discesa. Questa impostazione è utile quando hai più DN base e devi selezionare un valore.

**Abilita riferimento:** Questa impostazione è applicabile quando l&#39;organizzazione utilizza più domini Active Directory organizzati in una struttura gerarchica e sono state specificate impostazioni di directory solo per il dominio padre. In questa situazione, quando selezionate questa opzione, Gestione utente può accedere ai dettagli utente e gruppo dai domini secondari.

>[!NOTE]
>
>Fate clic su Prova per verificare se è possibile stabilire una connessione al server LDAP. Per determinare la causa principale di eventuali errori, controllate l&#39;eccezione nel file di registro di Application Server.

### Impostazioni utente {#user-settings}

**Identificatore univoco:** (Obbligatorio) Attributo univoco e costante utilizzato per identificare gli utenti. Utilizzate un attributo non DN come identificatore univoco perché il DN di un utente può cambiare se si sposta in un’altra parte dell’organizzazione. Questa impostazione dipende dal server di directory. Il valore è objectGUID per Active Directory 2003, nsUniqueID per Sun™ One e guid per eDirectory.

>[!NOTE]
>
>Accertatevi di inserire un attributo che sia garantito come univoco nell’organizzazione. L&#39;immissione di un valore non corretto può causare gravi problemi di sistema.

**DN di base:** Impostato come punto di partenza per la sincronizzazione di utenti e gruppi dalla gerarchia LDAP. È consigliabile specificare un DN di base al livello più basso della gerarchia che includa tutti gli utenti e i gruppi che devono essere sincronizzati per i servizi.

Se avete selezionato l&#39;opzione Abilita riferimento nelle impostazioni Directory, impostate l&#39;opzione DN base sulla parte *dc* del DN. Affinché il riferimento funzioni, l&#39;intervallo di ricerca deve includere sia i domini padre che i domini secondari.

>[!NOTE]
>
>Non includete il DN dell&#39;utente in questa impostazione. Per sincronizzare un particolare utente, usate l’impostazione Filtro ricerca.

Sebbene il DN di base sia un&#39;impostazione obbligatoria nella console di amministrazione, alcuni server di directory come IBM Domino Enterprise Server potrebbero richiedere un valore BaseDN vuoto. Per specificare un DN di base vuoto, esportate il file config.xml, modificate l&#39;impostazione nel file config.xml, quindi reimportatelo. Consultate [Importazione ed esportazione del file](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file)di configurazione.

**Filtro di ricerca:** (Obbligatorio) Il filtro di ricerca da utilizzare per trovare il record associato all&#39;utente. Potete eseguire una ricerca di un livello singolo o di un livello secondario. Consultate Sintassi del filtro di ricerca o RFC 2254. Ulteriori informazioni per lo schema di Microsoft AD, vedere Schema di Active Directory.

**Descrizione:** Attributo dello schema per la descrizione dell&#39;utente

**Nome completo:** (Obbligatorio) Attributo schema per il nome completo dell&#39;utente

**ID di login:** (Obbligatorio) Attributo schema per l&#39;ID di accesso dell&#39;utente

**Cognome:** (Obbligatorio) Attributo schema per il cognome dell&#39;utente

**Nome specificato:** (Obbligatorio) Attributo schema per il nome dell&#39;utente

**Iniziali:** Attributo schema per le iniziali dell&#39;utente

**Calendario aziendale:** Consente di mappare un calendario aziendale a un utente, in base al valore di questa impostazione (la chiave del calendario aziendale). I calendari aziendali definiscono i giorni lavorativi e non lavorativi. I moduli AEM possono utilizzare i calendari aziendali per calcolare le date e le ore future per eventi quali promemoria, scadenze e inoltro per moderazione. Il modo in cui assegnate le chiavi del calendario aziendale agli utenti dipende dal dominio Enterprise, locale o ibrido utilizzato. Consultate Configurazione dei calendari aziendali.

Se utilizzate un dominio Enterprise, potete mappare l’impostazione Calendario aziendale su un campo presente nella directory LDAP. Ad esempio, se ogni record utente nella directory contiene un campo del *paese* e si desidera assegnare calendari aziendali in base al paese in cui si trova l&#39;utente, specificare il nome del campo del *paese* come valore per l&#39;impostazione Calendario aziendale. È quindi possibile mappare le chiavi del calendario aziendale (i valori definiti per il campo del *paese* nella directory LDAP) ai calendari aziendali nel flusso di lavoro dei moduli.

Lo spazio utilizzato per visualizzare il nome della chiave del calendario aziendale nelle pagine del flusso di lavoro dei moduli è limitato. Limita il nome della chiave del calendario aziendale a meno di 53 caratteri per evitare che venga troncata su tali pagine.

**Modifica timestamp:** Per abilitare la sincronizzazione della directory delta, imposta questo valore per modificare TimeStamp. Consultate Attivare la sincronizzazione della directory delta.

**Organizzazione:** Attributo schema per il nome dell&#39;organizzazione a cui appartiene l&#39;utente.

**E-mail principale:** Attributo schema per l&#39;indirizzo e-mail principale dell&#39;utente.

**E-mail secondaria:** Attributo schema per l&#39;indirizzo e-mail secondario dell&#39;utente.

**Telefono:** Attributo schema per il numero di telefono dell&#39;utente.

**Indirizzo postale:** Attributo schema per l&#39;indirizzo di posta elettronica dell&#39;utente.

**Impostazioni internazionali:** Attributo dello schema che contiene le informazioni internazionali ISO. Il valore è un codice della lingua a due lettere o un codice della lingua e del paese.

**Fuso orario:** Attributo dello schema che contiene il fuso orario in cui si trova l&#39;utente. Il valore è una stringa come Città/Paese.

**Abilita controllo VLV (Virtual List View):** Un controllo LDAP che consente ai moduli AEM di recuperare i dati in batch dal server di directory. Se utilizzate Sun One come directory LDAP e la directory contiene molti utenti, l’attivazione di VLV crea un indice che Gestione utente può utilizzare per la ricerca degli utenti. Questa funzione è utile quando si utilizza un account utente normale in grado di sincronizzare solo una quantità limitata di dati. Potete inoltre abilitare VLV per i gruppi. Se selezionate Abilita controllo visualizzazione elenco virtuale (VLV), specificate un nome nella casella Campo ordinamento.

>[!NOTE]
>
>Per abilitare VLV, configurare Sun One. Consultate [Configurare la gestione utente per l’utilizzo della visualizzazione a elenco virtuale (VLV)](configuring-directories.md#configure-user-management-to-use-virtual-list-view-vlv).

**Campo di ordinamento:** Se avete selezionato Abilita controllo VLV (Virtual List View Control), specificate il nome attributo utilizzato per ordinare l&#39;indice. Questo nome attributo (ad esempio uid) è quello specificato al momento della creazione di un indice per VLV sul server di directory.

### Impostazioni gruppo {#group-settings}

**Identificatore univoco:** (Obbligatorio) Attributo univoco e costante utilizzato per identificare i gruppi. Utilizzate un attributo non DN come identificatore univoco. Questa impostazione dipende dal server di directory. Il valore è objectGUID per Active Directory 2003, nsUniqueID per Sun One e guid per eDirectory.

>[!NOTE]
>
>Accertatevi di inserire un attributo che sia garantito come univoco nell’organizzazione. L&#39;immissione di un valore non corretto può causare gravi problemi di sistema.

**DN di base:** (Obbligatorio) Nome distinto base della directory.

Sebbene il DN di base sia un&#39;impostazione obbligatoria nella console di amministrazione, alcuni server di directory, come IBM Domino Enterprise Server, richiedono un DN base vuoto. Per specificare un DN di base vuoto, esportate il file config.xml, modificate l&#39;impostazione nel file config.xml, quindi reimportatelo. Consultate [Importazione ed esportazione del file](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file)di configurazione.

**Filtro di ricerca:** (Obbligatorio) Il filtro di ricerca da utilizzare per trovare il record associato al gruppo. Potete eseguire una ricerca di un livello singolo o di un livello secondario.

**Descrizione:** Attributo dello schema per la descrizione del gruppo

**Nome completo:** (Obbligatorio) Attributo schema per il nome completo del gruppo

**DN membro:** (Obbligatorio) Attributo schema per il nome distinto dei membri all&#39;interno di un gruppo

**Identificatore univoco membro:** Identificatore univoco per un utente o un gruppo membro del gruppo selezionato. Questo valore dipende dal server di directory. Il valore è objectSID per AD2003, nsUniqueID per Sun One e guid per eDirectory.

Se il DN membro è specificato con un attributo non DN, User Management utilizza l’identificatore univoco membro per eseguire una query LDAP per raccogliere il DN dell’utente, in quanto corrisponde a un valore di identificatore univoco.

Se DN è specificato come identificatore univoco, non è necessario configurare l’identificatore univoco del membro.

**Organizzazione:** Attributo schema per il nome dell&#39;organizzazione a cui appartiene il gruppo

**E-mail principale:** Attributo dello schema per l&#39;indirizzo e-mail principale del gruppo

**E-mail secondaria:** Attributo schema per l&#39;indirizzo e-mail secondario del gruppo

**Modifica timestamp:** Per abilitare la sincronizzazione della directory delta, imposta questo valore per modificare TimeStamp. Consultate Attivare la sincronizzazione della directory delta.

**Abilita controllo VLV (Virtual List View):** Un controllo LDAP che consente ai moduli AEM di recuperare i dati in batch dal server di directory. Se utilizzate Sun One come directory LDAP e la directory contiene molti gruppi, l’attivazione di VLV crea un indice che User Management può utilizzare per la ricerca dei gruppi. Questa funzione è utile quando si utilizza un account utente normale in grado di sincronizzare solo una quantità limitata di dati. Potete inoltre abilitare VLV per gli utenti. Se selezionate Abilita controllo visualizzazione elenco virtuale, specificate un nome per il campo di ordinamento.

>[!NOTE]
>
>Per abilitare VLV, configurare Sun One. Consultate [Configurare la gestione utente per l’utilizzo della visualizzazione a elenco virtuale (VLV)](configuring-directories.md#configure-user-management-to-use-virtual-list-view-vlv).

**Nome campo ordinamento:** Se avete selezionato Abilita controllo VLV (Virtual List View Control), specificate il nome attributo utilizzato per ordinare l&#39;indice. Questo nome attributo è quello specificato al momento della creazione di un indice per VLV nel server di directory.

>[!NOTE]
>
>Fate clic su Prova per verificare che le impostazioni utente e gruppo vengano raccolte in base al DN di base e ai criteri di ricerca.

Se vengono restituiti utenti e gruppi, i risultati mostrano i valori assegnati a ciascun campo in base all&#39;insieme di attributi.

>[!NOTE]
>
>Gestione utente non supporta ID utente duplicati in un dominio; viene sincronizzato solo un utente con l’ID utente.

## Configurare Gestione utente per l’utilizzo della visualizzazione a elenco virtuale (VLV) {#configure-user-management-to-use-virtual-list-view-vlv}

La sincronizzazione delle directory è un requisito importante per la gestione degli utenti. Gli utenti e i gruppi vengono sincronizzati da una directory aziendale al database dei moduli AEM per assegnare ruoli e autorizzazioni. Il numero di utenti varia da 100 a 100000+ a seconda dei requisiti e rappresenta una sfida tecnica per la sincronizzazione dei dati in modo efficiente.

Il protocollo LDAP fornisce un meccanismo per eseguire query su set di dati di grandi dimensioni in modo impaginato utilizzando i controlli di richiesta. Quando si utilizza Microsoft Active Directory, la sincronizzazione del database da LDAP a AEM moduli utilizza PagedResultsControl per il recupero dei dati in batch di dimensioni particolari. Il server di directory Sun ONE non supporta questo controllo. Per completare una query impaginata sul server di directory Sun ONE, utilizzare il controllo VLV (Virtual List View). Questo controllo include sia la configurazione lato server della directory che l&#39;implementazione lato client.

>[!NOTE]
>
>Questa sezione descrive l&#39;utilizzo del controllo VLV per il server di directory Sun ONE. Tuttavia, potete utilizzare questo controllo per qualsiasi server di directory che supporta il controllo VLV.

1. Quando configurate la directory, selezionate Abilita controllo visualizzazione elenco virtuale (VLV) sia nella pagina Impostazioni utente che nelle pagine Impostazioni gruppo. Quando si seleziona la casella di controllo, è necessario specificare anche un nome di ordinamento nella casella Campo di ordinamento. Il valore predefinito è uid. Consultate [Aggiunta di directory o SPI](configuring-directories.md#adding-directories-or-custom-spis) personalizzati o [Modifica di una directory](configuring-directories.md#edit-a-directory).
1. Utilizzate la console di amministrazione Sun ONE o uno script della riga di comando per creare le voci VLV LDAP per utenti e gruppi. Se si utilizza uno script della riga di comando, è possibile utilizzare i file LDIF degli utenti e dei gruppi di esempio. (vedere [Configurazione del server di directory Sun ONE per VLV](configuring-directories.md#configuring-the-sun-one-directory-server-for-vlv)).
1. Arrestate il server e create l&#39;indice richiesto. (vedere [Creazione dell&#39;indice del server di directory per VLV](configuring-directories.md#create-the-directory-server-index-for-vlv)).

### Configurazione del server di directory Sun ONE per VLV {#configuring-the-sun-one-directory-server-for-vlv}

La creazione di un VLV richiede una coppia di voci che includono le classi `vlvSearch` e `vlvIndex` oggetto. La voce vlvSearch include una base di ricerca e l&#39; `vlvFilter` attributo, che specifica la classe oggetto che contiene gli attributi che si desidera ordinare. La classe `vlvIndex` object include l&#39; `vlvSort` attributo, che specifica uno o più attributi da ordinare e l&#39;ordine in cui ordinarli. (Un segno meno (-) indica l&#39;ordine alfabetico inverso). L&#39;utilizzo di VLV con moduli AEM richiede voci separate per utenti e gruppi.

>[!NOTE]
>
>Le voci dell&#39;oggetto possono essere create utilizzando l&#39;interfaccia utente grafica Sun ONE (GUI) o attraverso uno script della riga di comando. Per istruzioni su come creare le voci dell&#39;oggetto utilizzando l&#39;interfaccia grafica, consultare la documentazione di Sun ONE.

Di seguito è riportato uno script di esempio LDIF per la voce VLV destinata agli utenti:

```text
 dn: cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config
 objectclass: top
 objectclass: vlvSearch
 cn: lcuser
 vlvBase: dc=corp,dc=adobe,dc=com
 vlvScope: 2
 vlvFilter: (&(objectclass=inetOrgPerson))
 aci: (target="ldap:///cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config")(targetattr="*")(version 3.0; acl "Config"
 ;allow(read,search,compare) userdn="ldap:///all"; )
 dn: cn=lcuser,cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config
 cn: lcuser
 vlvSort: cn
 objectclass: top
 objectclass: vlvIndex
```

**Creazione di voci oggetto tramite uno script**

1. Lo script di esempio ha una voce LDAP denominata `lcuser`. Questa voce è relativa alla configurazione VLV per la sincronizzazione degli utenti nei moduli AEM. Modificate di conseguenza le seguenti proprietà:

   **Nome voce:** Il nome della voce in questo esempio è `lcuser`. Se `lcuser` viene modificato, deve essere modificato in tutte le aree dello script di esempio.

   **vlvBase:** Il DN di base specificato nella pagina Impostazioni utente.

   **vlvFilter:** Filtro di ricerca specificato nella pagina Impostazioni utente.

   **vlvSort:** Campo di ordinamento specificato nella sezione delle impostazioni VLV della pagina Impostazioni utente. Un controllo VLV richiede di specificare un controllo di ordinamento. Questo campo viene utilizzato come parametro di ordinamento per l&#39;indice vlv creato.

   **aci:** Il controllo di accesso specificato nello script di esempio concede a qualsiasi utente autenticato il diritto di accedere agli indici VLV per le operazioni di lettura, ricerca e confronto. L&#39;amministratore può limitare l&#39;accesso a un utente di binding, configurato nella pagina Impostazioni server directory specificata nell&#39;interfaccia utente di Gestione utente. Se non vengono assegnate autorizzazioni, la ricerca utente non può usare il VLV e il server LDAP genera un’eccezione di autorizzazione.

   >[!NOTE]
   >
   >Come convenzione, anche il nome della voce vlvIndex è impostato su `lcuser`, ma è possibile assegnargli un nome diverso. Utilizzate lo stesso nome nello strumento vlvindex. (vedere [Creazione dell&#39;indice del server di directory per VLV](configuring-directories.md#create-the-directory-server-index-for-vlv)*).*

1. Utilizzando lo `ldapmodify` strumento fornito con Sun ONE Server, create una voce simile per i gruppi utilizzando rispettivamente il DN di base del gruppo, il filtro di ricerca e il campo di ordinamento:

   `server directory\shared\bin>ldapmodify -v -a -h host -p port -D "admin user" -w "password" -f "LDIF file location"`

   Ad esempio, digitare il testo seguente:

   `D:\tools\ldap\sun\shared\bin> -v -a -h localhost -p 55850 -D "uid=admin,ou=administrators,ou=topologymanagement,o=netscaperoot" -w "admin" -f "D:\tools\ldap\data\vlv feature\users.ldif"`

### Creare l&#39;indice del server di directory per VLV {#create-the-directory-server-index-for-vlv}

Dopo aver configurato le impostazioni di directory e creato le voci VLV LDAP per utenti e gruppi, arrestate il server e create l’indice richiesto.

1. Dopo aver creato le voci dell&#39;oggetto, arrestare Sun ONE Server.
1. Utilizzando lo strumento vlvindex, generate l&#39;indice digitando il testo seguente:

   *istanza del server di directory* `\vlvindex.bat -n userRoot -T lcuser`

   Viene generato il seguente output:

   ```shell
    D:\tools\ldap\sun\shared\bin>..\..\slapd-chetanmeh-xp3\vlvindex.bat -n userRoot -T livecycle
    [21/Nov/2007:16:47:26 +051800] - userRoot: Indexing VLV: livecycle
    [21/Nov/2007:16:47:27 +051800] - userRoot: Indexed 1000 entries (5%).
    [21/Nov/2007:16:47:27 +051800] - userRoot: Indexed 2000 entries (9%).
    ...
    [21/Nov/2007:16:47:29 +051800] - userRoot: Indexed 20000 entries (94%).
    [21/Nov/2007:16:47:29 +051800] - userRoot: Indexed 21000 entries (99%).
    [21/Nov/2007:16:47:29 +051800] - userRoot: Finished indexing.
   ```

   Lo strumento vlvindex è presente nella directory di istanza del server di directory. Se Sun ONE Server ha due istanze che eseguono server1 e server2, lo strumento vlvindex si trova nella directory *del server* Sun ONE\server1. Il valore per il parametro `-T` è il valore dell&#39; `cn` attributo della voce vlvindex creata in precedenza nel LDIF di esempio. In questo caso, lo è `lcuser`.

1. Se VLV è abilitato anche per i gruppi, create l&#39;indice corrispondente per i gruppi. Verificare se gli indici sono creati eseguendo il comando seguente:

   *Sun one server directory* `\shared\bin>ldapsearch -h`*hostname *host`-p`*port no* `-s base -b "" objectclass=*`

   Viene generato un output come i seguenti dati di esempio:

   ```shell
    D:\tools\ldap\sun\shared\bin>ldapsearch.exe -h localhost -p 55850 -s base -b "" objectclass=*
    ldapsearch.exe: started Tue Nov 27 16:34:20 2007
    version: 1
    dn:
    objectClass: top
    namingContexts: dc=corp,dc=adobe,dc=com
    supportedExtension: 2.16.840.1.113730.3.5.7
    ...
    vlvsearch: cn=MCC ou=testdata dc=corp dc=adobe dc=com, cn=userRoot,cn=ldbm dat
        abase,cn=plugins,cn=config
    vlvsearch: cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config
    vlvsearch: cn=Browsing ou=testdata,cn=userRoot,cn=ldbm database,cn=plugins,cn=
        config
    1 matches
   ```

