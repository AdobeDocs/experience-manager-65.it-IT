---
title: Configurazione delle directory
description: Scopri come aggiungere, modificare ed eliminare directory e configurare la gestione degli utenti per l’utilizzo della visualizzazione a elenco virtuale.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 30edcef2-e8fa-403a-9850-b8dfeeb9ac65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '3229'
ht-degree: 0%

---

# Configurazione delle directory {#configuring-directories}

Per ogni dominio enterprise configurato, specificare le directory in cui il provider di autenticazione esegue la query delle informazioni utente. Puoi configurare più directory per un dominio.

## Aggiunta di directory o SPI personalizzati {#adding-directories-or-custom-spis}

Per ogni dominio enterprise configurato, specificare le directory in cui il provider di autenticazione esegue la query delle informazioni utente. È possibile aggiungere una directory a un dominio enterprise esistente o a un nuovo dominio enterprise che si sta aggiungendo. Puoi configurare più directory per un dominio. È inoltre possibile configurare un dominio per l&#39;utilizzo di una SPI (Service Provider Interface) personalizzata per la sincronizzazione.

### Aggiungi una directory {#add-a-directory}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fare clic su Nuovo dominio enterprise o selezionare un dominio enterprise esistente.
1. Fare clic su Aggiungi directory.
1. Nella casella Nome profilo digitare un nome per distinguere la directory e quindi fare clic su Avanti.
1. Configurare le impostazioni del server delle directory. (Vedi [Impostazioni directory](configuring-directories.md#directory-settings).)
1. Per verificare che sia possibile effettuare una connessione al server LDAP, fare clic su Test. Se il test ha esito negativo, esaminare l&#39;eccezione nel file di registro di Application Server per determinare la causa principale dell&#39;errore. Fare clic su Chiudi e quindi su Avanti.
1. Seleziona Impostazioni utente e configura le impostazioni come richiesto. (Vedi [Impostazioni directory](configuring-directories.md#directory-settings).)
1. Per verificare che il DN di base e altri attributi configurati raccolgano il batch di utenti corretto, fare clic su Test. LDAP tenta di recuperare i primi 200 record utilizzando le impostazioni fornite (ad esempio il DN di base, il filtro di ricerca e tutti gli attributi).

   Se gli utenti vengono restituiti, i risultati mostrano i valori assegnati a ciascun campo in base alla serie di attributi. Se il test non riesce a causa di un nome server inesistente, informazioni di autorizzazione non corrette o attributi non corretti, viene visualizzato il seguente messaggio di errore: &quot;I criteri di ricerca specificati non hanno restituito alcun risultato&quot;. Per determinare la causa principale dell&#39;errore, esaminare l&#39;eccezione nel file di registro di Application Server. Fare clic su Chiudi e quindi su Avanti.

1. Seleziona Impostazioni gruppo e configura le impostazioni in base alle esigenze. (Vedi [Impostazioni directory](configuring-directories.md#directory-settings).)
1. Per verificare che il DN di base e altri attributi configurati raccolgano il batch di gruppi corretto, fare clic su Test. Se vengono restituiti gruppi, i risultati mostrano i valori assegnati a ciascun campo in base alla serie di attributi. Fai clic su Chiudi.

### Aggiungere una SPI personalizzata {#add-a-custom-spi}

Per informazioni sulla creazione di un SPI personalizzato, vedere &quot;Sviluppo di SPI per i moduli AEM&quot; in [Programmazione con moduli AEM](https://www.adobe.com/go/learn_aemforms_programming_63). Per rendere disponibile un SPI personalizzato appena distribuito per l&#39;associazione al dominio, riavviare il server.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fare clic su Nuovo dominio enterprise o selezionare un dominio enterprise esistente.
1. Fare clic su Aggiungi directory.
1. Digitare un nome nella casella Nome profilo, selezionare Provider SPI personalizzato e quindi fare clic su Avanti.
1. Selezionare un provider utente personalizzato dall&#39;elenco e fare clic su Avanti.
1. Selezionare un provider di gruppi personalizzato dall&#39;elenco e fare clic su Fine.

## Modificare una directory {#edit-a-directory}

Puoi modificare i dettagli di una directory configurata in precedenza.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fare clic sul dominio appropriato nell&#39;elenco e nella pagina visualizzata selezionare la directory appropriata dall&#39;elenco.
1. Configurare le impostazioni di directory, utente e gruppo in base alle esigenze. (Vedi [Impostazioni directory](configuring-directories.md#directory-settings).)
1. Fare clic su OK.

## Eliminare una directory {#delete-a-directory}

Quando si sincronizzano i domini dopo l&#39;eliminazione di una directory, tutti gli utenti e i gruppi in tale directory vengono contrassegnati come obsoleti nel database. Non verranno restituiti in alcuna ricerca dalla console di amministrazione.

>[!NOTE]
>
>I domini Enterprise richiedono almeno un provider di autenticazione e un provider di directory.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fare clic sul dominio appropriato nell&#39;elenco.
1. Selezionare la casella di controllo relativa alla directory appropriata e fare clic su Elimina.
1. Fare clic su OK nella pagina di conferma visualizzata e fare di nuovo clic su OK.

## Impostazioni directory {#directory-settings}

Quando aggiungi una directory a un dominio, specifica le seguenti impostazioni di directory.

**Server:** (obbligatorio) Nome di dominio completo (FQDN) del server delle directory. Ad esempio, per un computer denominato x nella rete adobe.com, il nome di dominio completo è x.adobe.com. È possibile utilizzare un indirizzo IP al posto del nome del server FQDN.

**Porta:** (obbligatoria) Porta utilizzata dal server delle directory. In genere, 389 o 636 se il protocollo SSL (Secure Sockets Layer) viene utilizzato per l&#39;invio di informazioni di autenticazione sulla rete.

**SSL:** (obbligatorio) Specifica se il server delle directory utilizza SSL per l&#39;invio di dati in rete. Il valore predefinito è No. Se impostato su Sì, il certificato del server LDAP corrispondente deve essere considerato attendibile dall&#39;ambiente runtime Java™ (JRE) del server applicazioni.

**Binding** (obbligatorio) Specifica come accedere alla directory.

**Anonimo:** Non è richiesto alcun nome utente o password. Un utente anonimo può essere in grado di recuperare solo una quantità limitata di dati. Questa opzione può essere utile per il test iniziale.

**Utente:** autenticazione richiesta. Nella casella Nome specificare il nome del record utente che può accedere alla directory. È consigliabile immettere il nome distinto completo (DN) dell&#39;account utente, ad esempio cn=Jane Doe, ou=user, dc=can, dc=com. Nella casella Password specificare la password associata. Queste impostazioni sono necessarie quando si seleziona Utente come opzione di binding.

**Nome:** Nome che può essere utilizzato per connettersi al database LDAP quando l&#39;accesso anonimo non è abilitato. Per Active Directory 2003, specificare `[domain name]\[userid]`. Per Sun™ One, eDirectory o IBM Tivoli Directory Server, specificare il nome completo dell&#39;utente, ad esempio uid=lcuser,ou=it,o=company.com.

**Password:** Password corrispondente al nome specificato per la connessione al database LDAP quando l&#39;accesso anonimo non è abilitato.

**Popola pagina con:** Se questa opzione è selezionata, compila gli attributi nelle pagine delle impostazioni Utente e Gruppo con i corrispondenti valori LDAP predefiniti.

**Recupera DN di base:** Recupera i DN di base e li visualizza nell&#39;elenco a discesa. Questa impostazione è utile quando si dispone di più DN di base e si deve selezionare un valore.

**Abilita riferimento:** Questa impostazione è applicabile quando l&#39;organizzazione utilizza più domini di Active Directory organizzati in una struttura gerarchica e sono state specificate impostazioni di directory solo per il dominio padre. In questa situazione, quando selezioni questa opzione, Gestione utenti può accedere ai dettagli di utenti e gruppi dai domini secondari.

>[!NOTE]
>
>Fare clic su Prova per verificare che sia possibile effettuare una connessione al server LDAP. Per determinare la causa principale di eventuali errori, esaminare l&#39;eccezione nel file di registro di Application Server.

### Impostazioni utente {#user-settings}

**Identificatore univoco:** (obbligatorio) attributo univoco e costante utilizzato per identificare gli utenti. Utilizzare un attributo non DN come identificatore univoco perché il DN di un utente può cambiare se si sposta in un&#39;altra parte dell&#39;organizzazione. Questa impostazione dipende dal server delle directory. Il valore è objectGUID per Active Directory 2003, nsuniqueID per Sun™ One e guid per eDirectory.

>[!NOTE]
>
>Assicurati di inserire un attributo che sia garantito come univoco all’interno dell’organizzazione. L&#39;immissione di un valore errato può causare gravi problemi di sistema.

**DN di base:** Imposta come punto iniziale per la sincronizzazione di utenti e gruppi dalla gerarchia LDAP. È consigliabile specificare un DN di base al livello più basso della gerarchia che includa tutti gli utenti e i gruppi che devono essere sincronizzati per i servizi.

Se nelle impostazioni della directory è stata selezionata l&#39;opzione Abilita riferimento, impostare l&#39;opzione DN di base sulla parte *dc* del DN. Affinché il riferimento funzioni, l’intervallo di ricerca deve includere sia i domini padre che quelli figlio.

>[!NOTE]
>
>Non includere il DN dell&#39;utente in questa impostazione. Per sincronizzare un utente specifico, utilizzare l&#39;impostazione Filtro di ricerca.

Sebbene il DN di base sia un&#39;impostazione obbligatoria nella console di amministrazione, alcuni server delle directory, come IBM Domino Enterprise Server, potrebbero richiedere un DN di base vuoto. Per specificare un DN di base vuoto, esportare il file config.xml, modificare l&#39;impostazione nel file config.xml, quindi reimportarlo. (Vedere [Importazione ed esportazione del file di configurazione](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).)

**Filtro di ricerca:** (obbligatorio) Filtro di ricerca da utilizzare per trovare il record associato all&#39;utente. È possibile eseguire una ricerca a un livello o a un livello secondario. Consultate Sintassi del filtro di ricerca o RFC 2254. Per ulteriori informazioni sullo schema di Microsoft AD, vedere Schema di Active Directory.

**Descrizione:** attributo dello schema per la descrizione dell&#39;utente

**Nome completo:** (obbligatorio) Attributo schema per il nome completo dell&#39;utente

**ID accesso:** (obbligatorio) Attributo schema per l&#39;ID di accesso dell&#39;utente

**Cognome:** (obbligatorio) Attributo schema per il cognome dell&#39;utente

**Nome assegnato:** (obbligatorio) Attributo schema per il nome dell&#39;utente

**Iniziali:** Attributo schema per le iniziali dell&#39;utente

**Calendario aziendale:** consente di mappare un calendario aziendale a un utente in base al valore di questa impostazione (chiave del calendario aziendale). I calendari aziendali definiscono i giorni lavorativi e non lavorativi. I moduli AEM possono utilizzare i calendari aziendali per calcolare le date e le ore future per eventi quali promemoria, scadenze e inoltri per moderazione. Il modo in cui si assegnano le chiavi del calendario aziendale agli utenti dipende dal fatto che si utilizzi un dominio enterprise, locale o ibrido. Consultate Configurazione dei calendari aziendali.

Se si utilizza un dominio enterprise, è possibile mappare l&#39;impostazione del Calendario aziendale a un campo nella directory LDAP. Ad esempio, se ogni record utente nella directory contiene un campo *paese* e si desidera assegnare calendari aziendali in base al paese in cui si trova l&#39;utente, specificare il nome del campo *paese* come valore per l&#39;impostazione Calendario aziendale. È quindi possibile mappare le chiavi del calendario aziendale (i valori definiti per il campo *paese* nell&#39;elenco LDAP) ai calendari aziendali nel flusso di lavoro di Forms.

Lo spazio utilizzato per visualizzare il nome della chiave del calendario aziendale nelle pagine del flusso di lavoro dei moduli è limitato. Limita il nome della chiave del calendario aziendale a meno di 53 caratteri per evitare che venga troncato su tali pagine.

**Modifica timestamp:** Per abilitare la sincronizzazione della directory delta, impostare questo valore per modificare il timestamp. Consultate Abilitare la sincronizzazione della directory delta.

**Organizzazione:** attributo dello schema per il nome dell&#39;organizzazione a cui appartiene l&#39;utente.

**E-mail primaria:** attributo dello schema per l&#39;indirizzo e-mail principale dell&#39;utente.

**Attributo schema e-mail secondaria:** per l&#39;indirizzo e-mail secondario dell&#39;utente.

**Telefono:** Attributo dello schema per il numero di telefono dell&#39;utente.

**Indirizzo postale:** Attributo schema per l&#39;indirizzo postale dell&#39;utente.

**Impostazioni internazionali:** Attributo dello schema che contiene le informazioni sulle impostazioni internazionali ISO. Il valore è un codice della lingua a due lettere o un codice della lingua e del paese.

**Fuso orario:** attributo dello schema che contiene il fuso orario in cui si trova l&#39;utente. Il valore è una stringa come Città/Paese.

**Attiva controllo VLV (Virtual List View):** controllo LDAP che consente ai moduli AEM di recuperare i dati in batch dal server delle directory. Se si utilizza Sun One come directory LDAP e la directory contiene molti utenti, l&#39;abilitazione di VLV crea un indice utilizzabile da Gestione utenti durante la ricerca degli utenti. Questa funzione è utile quando si utilizza un account utente normale in grado di sincronizzare solo una quantità limitata di dati. È inoltre possibile abilitare VLV per i gruppi. Se si seleziona Attiva controllo VLV (Virtual List View), specificare un nome nella casella Ordina campo.

>[!NOTE]
>
>Per abilitare VLV, configurare Sun One. Vedere [Configurare la gestione utenti per l&#39;utilizzo della visualizzazione elenco virtuale](configuring-directories.md#configure-user-management-to-use-virtual-list-view-vlv).

**Campo di ordinamento:** Se è stata selezionata l&#39;opzione Abilita controllo VLV (Virtual List View), specificare il nome dell&#39;attributo utilizzato per ordinare l&#39;indice. Questo nome di attributo (ad esempio uid) è quello specificato quando si crea un indice per VLV sul server delle directory.

### Impostazioni gruppo {#group-settings}

**Identificatore univoco:** (obbligatorio) attributo univoco e costante utilizzato per identificare i gruppi. Utilizza un attributo non DN come identificatore univoco. Questa impostazione dipende dal server delle directory. Il valore è objectGUID per Active Directory 2003, nsuniqueID per Sun One e guid per eDirectory.

>[!NOTE]
>
>Assicurati di inserire un attributo che sia garantito come univoco all’interno dell’organizzazione. L&#39;immissione di un valore errato può causare gravi problemi di sistema.

**Nome distinto di base:** (obbligatorio) Nome distinto di base della directory.

Sebbene il DN di base sia un&#39;impostazione obbligatoria nella console di amministrazione, alcuni server delle directory, come IBM Domino Enterprise Server, richiedono un DN di base vuoto. Per specificare un DN di base vuoto, esportare il file config.xml, modificare l&#39;impostazione nel file config.xml, quindi reimportarlo. (Vedere [Importazione ed esportazione del file di configurazione](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).)

**Filtro di ricerca:** (obbligatorio) Filtro di ricerca da utilizzare per trovare il record associato al gruppo. È possibile eseguire una ricerca a un livello o a un livello secondario.

**Descrizione:** attributo dello schema per la descrizione del gruppo

**Nome completo:** (obbligatorio) Attributo schema per il nome completo del gruppo

**DN membro:** (obbligatorio) Attributo schema per il nome distinto dei membri di un gruppo

**Identificatore univoco membro:** Identificatore univoco per un utente o un gruppo membro del gruppo selezionato. Questo valore dipende dal server delle directory. Il valore è objectSID per AD2003, nsuniqueID per Sun One e guid per eDirectory.

Se DN membro è specificato con un attributo non DN, Gestione utenti utilizza Identificatore univoco membro per eseguire una query LDAP per raccogliere il DN dell&#39;utente in quanto corrisponde a un valore di identificatore univoco.

Se DN è specificato come identificatore univoco, non è necessario configurare Identificatore univoco membro.

**Organizzazione:** Attributo dello schema per il nome dell&#39;organizzazione a cui appartiene il gruppo

**E-mail primaria:** Attributo dello schema per l&#39;indirizzo e-mail principale del gruppo

**E-mail secondaria:** Attributo dello schema per l&#39;indirizzo e-mail secondario del gruppo

**Modifica timestamp:** Per abilitare la sincronizzazione della directory delta, impostare questo valore per modificare il timestamp. Consultate Abilitare la sincronizzazione della directory delta.

**Attiva controllo VLV (Virtual List View):** controllo LDAP che consente ai moduli AEM di recuperare i dati in batch dal server delle directory. Se si utilizza Sun One come directory LDAP e la directory contiene molti gruppi, l&#39;abilitazione di VLV crea un indice utilizzabile da Gestione utente durante la ricerca dei gruppi. Questa funzione è utile quando si utilizza un account utente normale in grado di sincronizzare solo una quantità limitata di dati. È inoltre possibile abilitare VLV per gli utenti. Se si seleziona Abilita controllo VLV (Virtual List View), specificare un nome per il campo di ordinamento.

>[!NOTE]
>
>Per abilitare VLV, configurare Sun One. Vedere [Configurare la gestione utenti per l&#39;utilizzo della visualizzazione elenco virtuale](configuring-directories.md#configure-user-management-to-use-virtual-list-view-vlv).

**Nome campo di ordinamento:** Se è stata selezionata l&#39;opzione Abilita controllo VLV (Virtual List View), specificare il nome dell&#39;attributo utilizzato per ordinare l&#39;indice. Questo nome di attributo è quello specificato al momento della creazione di un indice per VLV sul server delle directory.

>[!NOTE]
>
>Fare clic su Prova per verificare che le impostazioni utente e gruppo vengano raccolte in base al DN di base e ai criteri di ricerca.

Se vengono restituiti utenti e gruppi, i risultati mostrano i valori assegnati a ciascun campo in base alla serie di attributi.

>[!NOTE]
>
>Gestione utenti non supporta ID utente duplicati all’interno di un dominio; viene sincronizzato un solo utente con l’ID utente.

## Configurare User Management per l&#39;utilizzo di Virtual List View (VLV) {#configure-user-management-to-use-virtual-list-view-vlv}

La sincronizzazione delle directory è un requisito importante per la gestione degli utenti. Gli utenti e i gruppi vengono sincronizzati da una directory enterprise al database dei moduli AEM per l&#39;assegnazione di ruoli e autorizzazioni. Il numero di utenti varia da 100 a 100000+ a seconda dei requisiti e rappresenta una sfida tecnica per sincronizzare i dati in modo efficiente.

Il protocollo LDAP fornisce un meccanismo per eseguire query su set di dati di grandi dimensioni in modo impaginato utilizzando i controlli di richiesta. Quando si utilizza Microsoft Active Directory, la sincronizzazione del database da LDAP a AEM Forms utilizza PagedResultsControl per recuperare i dati in batch di dimensioni particolari. Il server delle directory Sun ONE non supporta questo controllo. Per completare una query impaginata sul server delle directory Sun ONE, utilizzare il controllo Virtual List View (VLV). Questo controllo coinvolge sia la configurazione lato server delle directory che l&#39;implementazione lato client.

>[!NOTE]
>
>In questa sezione viene descritto l&#39;utilizzo del controllo VLV per Sun ONE Directory Server. Tuttavia, è possibile utilizzare questo controllo per qualsiasi server delle directory che supporta il controllo VLV.

1. Durante la configurazione della directory, selezionare Abilita controllo VLV (Virtual List View) sia nella pagina Impostazioni utente che nella pagina Impostazioni gruppo. Quando si seleziona la casella di controllo, è necessario specificare anche un nome di ordinamento nella casella Campo di ordinamento. Il valore predefinito è uid. (Vedi [Aggiunta di directory o SPI personalizzati](configuring-directories.md#adding-directories-or-custom-spis) o [Modifica di una directory](configuring-directories.md#edit-a-directory).)
1. Utilizzare la console di amministrazione di Sun ONE o uno script della riga di comando per creare le voci VLV LDAP per utenti e gruppi. Se si utilizza uno script della riga di comando, è possibile utilizzare i file LDIF di utenti e gruppi di esempio. (Vedere [Configurazione di Sun ONE Directory Server per VLV](configuring-directories.md#configuring-the-sun-one-directory-server-for-vlv).)
1. Arresta il server e crea l&#39;indice richiesto. (Vedere [Creare l&#39;indice del server delle directory per VLV](configuring-directories.md#create-the-directory-server-index-for-vlv).)

### Configurazione di Sun ONE Directory Server per VLV {#configuring-the-sun-one-directory-server-for-vlv}

La creazione di un VLV richiede una coppia di voci che includono le classi di oggetti `vlvSearch` e `vlvIndex`. La voce vlvSearch include una base di ricerca e l&#39;attributo `vlvFilter`, che specifica la classe oggetto contenente gli attributi che si desidera ordinare. La classe dell&#39;oggetto `vlvIndex` include l&#39;attributo `vlvSort`, che specifica uno o più attributi da ordinare e l&#39;ordine in cui ordinarli. (Il segno meno (-) indica l&#39;ordine alfabetico inverso). L’utilizzo del VLV con i moduli AEM richiede voci separate per gli utenti e i gruppi.

>[!NOTE]
>
>Le voci Object possono essere create utilizzando l&#39;interfaccia grafica utente (GUI) di Sun ONE o tramite uno script della riga di comando. Per istruzioni sulla creazione delle voci Object mediante l&#39;interfaccia grafica, consultare la documentazione di Sun ONE.

Di seguito è riportato un esempio di script LDIF per la voce VLV per gli utenti:

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

**Creare le voci oggetto utilizzando uno script**

1. Lo script di esempio contiene una voce LDAP denominata `lcuser`. Questa voce è per la configurazione relativa a VLV per la sincronizzazione degli utenti nei moduli AEM. Modifica di conseguenza le seguenti proprietà:

   **Nome voce:** Il nome voce in questo esempio è `lcuser`. Se `lcuser` viene modificato, è necessario modificarlo in tutte le aree dello script di esempio.

   **vlvBase:** il DN di base specificato nella pagina Impostazioni utente.

   **vlvFilter:** Il filtro di ricerca specificato nella pagina Impostazioni utente.

   **vlvSort:** Il campo di ordinamento specificato nella sezione Impostazioni VLV della pagina Impostazioni utente. Un controllo VLV richiede di specificare un controllo di ordinamento. Questo campo viene utilizzato come parametro di ordinamento per l&#39;indice vlv creato.

   **aci:** Il controllo di accesso specificato nello script di esempio concede a qualsiasi utente autenticato il diritto di accedere agli indici VLV per operazioni di lettura, ricerca e confronto. L&#39;amministratore può limitare l&#39;accesso a un utente di associazione configurato nella pagina Impostazioni server delle directory specificata nell&#39;interfaccia utente Gestione utente. Se non vengono assegnate autorizzazioni, la ricerca utente non può utilizzare VLV e il server LDAP genera un&#39;eccezione di autorizzazione.

   >[!NOTE]
   >
   >Come convenzione, anche il nome della voce vlvIndex è impostato su `lcuser`, ma è possibile assegnargli un nome diverso. Utilizzare lo stesso nome nello strumento vlvindex. (Vedere [Creare l&#39;indice del server delle directory per VLV ](configuring-directories.md#create-the-directory-server-index-for-vlv)*.)*

1. Utilizzando lo strumento `ldapmodify` fornito con Sun ONE Server, creare una voce simile per i gruppi utilizzando rispettivamente il DN di base, il filtro di ricerca e il campo di ordinamento del gruppo:

   `server directory\shared\bin>ldapmodify -v -a -h host -p port -D "admin user" -w "password" -f "LDIF file location"`

   Digitare ad esempio il testo seguente:

   `D:\tools\ldap\sun\shared\bin> -v -a -h localhost -p 55850 -D "uid=admin,ou=administrators,ou=topologymanagement,o=netscaperoot" -w "admin" -f "D:\tools\ldap\data\vlv feature\users.ldif"`

### Creare l&#39;indice del server delle directory per VLV {#create-the-directory-server-index-for-vlv}

Dopo aver configurato le impostazioni della directory e creato le voci VLV LDAP per utenti e gruppi, arrestare il server e creare l&#39;indice richiesto.

1. Dopo aver creato le voci oggetto, arrestare Sun ONE Server.
1. Utilizzando lo strumento vlvindex, generate l&#39;indice digitando il testo seguente:

   *istanza del server delle directory* `\vlvindex.bat -n userRoot -T lcuser`

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

   Lo strumento vlvindex è presente nella directory dell&#39;istanza del server delle directory. Se il server Sun ONE dispone di due istanze che eseguono server1 e server2, lo strumento vlvindex si trova nella directory del server *Sun ONE*\server1. Il valore del parametro `-T` è il valore dell&#39;attributo `cn` della voce vlvindex creata in precedenza nell&#39;LDIF di esempio. In questo caso, è `lcuser`.

1. Se VLV è abilitato anche per i gruppi, creare l&#39;indice corrispondente per i gruppi. Verifica se gli indici vengono creati eseguendo il seguente comando:

   *sun una directory server* `\shared\bin>ldapsearch -h`*nomehost* `-p`*porta no* `-s base -b "" objectclass=*`

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
