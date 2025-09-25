---
title: Configurare le directory
description: Scopri come aggiungere, modificare ed eliminare directory e come configurare la gestione degli utenti per l’utilizzo della vista elenco virtuale.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 30edcef2-e8fa-403a-9850-b8dfeeb9ac65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e9afc12af78140ae0ec12cc2ee95fc9e175f8d94
workflow-type: ht
source-wordcount: '3241'
ht-degree: 100%

---


# Configurare le directory {#configuring-directories}

Per ogni dominio enterprise configurato, specifica le directory in cui il provider di autenticazione ricerca le informazioni dell’utente. Puoi configurare più directory per un dominio.

## Aggiungere directory o SPI personalizzati {#adding-directories-or-custom-spis}

Per ogni dominio enterprise configurato, specifica le directory in cui il provider di autenticazione ricerca le informazioni dell’utente. Puoi aggiungere una directory a un dominio enterprise esistente o a un nuovo dominio enterprise che stai aggiungendo. Puoi configurare più directory per un dominio. Inoltre puoi configurare un dominio per l’utilizzo di un’interfaccia del provider di servizi (SPI) personalizzata per la sincronizzazione.

### Aggiungere una directory {#add-a-directory}

>[!NOTE]
>
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utenti > Gestione dominio.
1. Fai clic su Nuovo dominio enterprise o seleziona un dominio enterprise esistente.
1. Fai clic su Aggiungi directory.
1. Nella casella Nome profilo digita un nome per distinguere la directory, quindi fai clic su Avanti.
1. Configura le impostazioni del server delle directory. Consulta [Impostazioni directory](configuring-directories.md#directory-settings).
1. Per verificare che sia possibile effettuare una connessione al server LDAP, fai clic su Test. Se il test ha esito negativo, esamina l’eccezione nel file di registro del server applicazioni per determinare la causa principale dell’errore. Fai clic su Chiudi e quindi su Avanti.
1. Seleziona Impostazioni utente e configura le impostazioni in base alle esigenze. Consulta [Impostazioni directory](configuring-directories.md#directory-settings).
1. Per verificare che il DN di base e gli altri attributi configurati raccolgano il batch di utenti corretto, fai clic su Test. LDAP tenta di recuperare i primi 200 record utilizzando le impostazioni fornite (ad esempio il DN di base, il filtro di ricerca e tutti gli attributi).

   Se vengono restituiti degli utenti, i risultati mostrano i valori assegnati a ciascun campo in base al set di attributi. Se il test non riesce a causa di un nome server inesistente o di informazioni di autorizzazione o attributi non corretti, viene visualizzato il seguente messaggio di errore: “I criteri di ricerca specificati non hanno restituito alcun risultato”. Per determinare la causa principale dell’errore, esamina l’eccezione nel file di registro del server applicazioni. Fai clic su Chiudi e quindi su Avanti.

1. Seleziona Impostazioni gruppo e configura le impostazioni in base alle esigenze. Consulta [Impostazioni directory](configuring-directories.md#directory-settings).
1. Per verificare che il DN di base e gli altri attributi configurati raccolgano il batch di gruppi corretto, fai clic su Test. Se vengono restituiti dei gruppi, i risultati mostrano i valori assegnati a ciascun campo in base al set di attributi. Fai clic su Chiudi.

### Aggiungere un’interfaccia SPI personalizzata {#add-a-custom-spi}

Per informazioni sulla creazione di un’interfaccia del provider di servizi (SPI) personalizzata, consulta “Sviluppare SPI per AEM Forms” in [Programmare con AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_63_it). Per rendere disponibile una SPI personalizzata appena distribuita per l’associazione al dominio, riavvia il server.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utenti > Gestione dominio.
1. Fai clic su Nuovo dominio enterprise o seleziona un dominio enterprise esistente.
1. Fai clic su Aggiungi directory.
1. Digita un nome nella casella Nome profilo, seleziona Provider dell’interfaccia SPI personalizzata, quindi fai clic su Avanti.
1. Seleziona un provider di utenti personalizzato dall’elenco e fai clic su Avanti.
1. Seleziona un provider di gruppi personalizzato dall’elenco e fai clic su Fine.

## Modificare una directory {#edit-a-directory}

Puoi modificare i dettagli di una directory che hai configurato in precedenza.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utenti > Gestione dominio.
1. Fai clic sul dominio appropriato nell’elenco, quindi nella pagina visualizzata seleziona la directory appropriata nell’elenco.
1. Configura le impostazioni di directory, utente e gruppo in base alle esigenze. Consulta [Impostazioni directory](configuring-directories.md#directory-settings).
1. Fai clic su OK.

## Eliminare una directory {#delete-a-directory}

Quando sincronizzi i domini dopo l’eliminazione di una directory, tutti gli utenti e i gruppi in tale directory vengono contrassegnati come obsoleti nel database. Non verranno restituiti in alcuna ricerca dalla console di amministrazione.

>[!NOTE]
>
>I domini Enterprise richiedono almeno un provider di autenticazione e uno di directory.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utenti > Gestione dominio.
1. Fai clic sul dominio appropriato nell’elenco.
1. Seleziona la casella di controllo relativa alla directory appropriata e fai clic su Elimina.
1. Fai clic su OK nella pagina di conferma visualizzata e fai di nuovo clic su OK.

## Impostazioni directory {#directory-settings}

Quando aggiungi una directory a un dominio, specifica le seguenti impostazioni della directory.

**Server:** (obbligatorio) il nome dominio completo (FQDN) del server delle directory. Ad esempio, per un computer denominato x nella rete adobe.com, il nome dominio completo è x.adobe.com. Puoi utilizzare un indirizzo IP al posto del nome del server FQDN.

**Porta:** (obbligatoria) la porta utilizzata dal server delle directory. In genere, 389 o 636 se il protocollo SSL (Secure Sockets Layer) viene utilizzato per l’invio di informazioni di autenticazione sulla rete.

**SSL:** (obbligatorio) specifica se il server della directory utilizza SSL per l’invio di dati in rete. L’impostazione predefinita è no. Se impostato su sì, il certificato del server LDAP corrispondente deve essere considerato attendibile dall’ambiente runtime Java™ (JRE) del server applicazioni.

**Binding** (obbligatorio) specifica come accedere alla directory.

**Anonimo:** non è richiesto alcun nome utente o password. Un utente anonimo può essere in grado di recuperare solo una quantità limitata di dati. Questa opzione può essere utile per il test iniziale.

**Utente:** è richiesta l’autenticazione. Nella casella Nome, specifica il nome del record utente che può accedere alla directory. È consigliabile immettere il nome distinto completo (DN) dell’account utente, ad esempio cn=Jane Doe, ou=user, dc=can, dc=com. Nella casella Password, specifica la password associata. Queste impostazioni sono necessarie quando selezioni Utente come opzione di binding.

**Nome:** il nome che puoi utilizzare per la connessione al database LDAP quando l’accesso anonimo non è abilitato. Per Active Directory 2003, specifica `[domain name]\[userid]`. Per Sun™ One, eDirectory o IBM Tivoli Directory Server, specifica il nome completo dell’utente, ad esempio uid=lcuser,ou=it,o=company.com.

**Password:** la password corrispondente al nome specificato per la connessione al database LDAP quando l’accesso anonimo non è abilitato.

**Popola pagina con:** se selezioni questa opzione, popola gli attributi nelle pagine delle impostazioni Utente e Gruppo con i corrispondenti valori LDAP predefiniti.

**Recupera DN di base:** recupera i DN di base e li visualizza nell’elenco a discesa. Questa impostazione è utile quando disponi di più DN di base e devi selezionare un valore.

**Abilita riferimento:** questa impostazione è applicabile quando l’organizzazione utilizza più domini di Active Directory organizzati in una struttura gerarchica e hai specificato impostazioni di directory solo per il dominio principale. In questa situazione, quando selezioni questa opzione, gestione utenti può accedere ai dettagli di utenti e gruppi dai domini secondari.

>[!NOTE]
>
>Fai clic su Test per verificare che sia possibile effettuare una connessione al server LDAP. Per determinare la causa principale di eventuali errori, esaminare l’eccezione nel file di registro del server applicazioni.

### Impostazioni utente {#user-settings}

**Identificatore univoco:** (obbligatorio) un attributo univoco e costante utilizzato per identificare gli utenti. Utilizza un attributo non DN come identificatore univoco perché il DN di un utente può cambiare se viene spostato in un’altra parte dell’organizzazione. Questa impostazione dipende dal server delle directory. Il valore è objectGUID per Active Directory 2003, nsuniqueID per Sun™ One e guid per eDirectory.

>[!NOTE]
>
>Assicurati di inserire un attributo che sia garantito come univoco all’interno dell’organizzazione. L’immissione di un valore errato può causare gravi problemi di sistema.

**DN di base:** imposta come punto iniziale per la sincronizzazione di utenti e gruppi dalla gerarchia LDAP. È consigliabile specificare un DN di base al livello più basso della gerarchia che includa tutti gli utenti e i gruppi che devono essere sincronizzati per i servizi.

Se nelle impostazioni della directory hai selezionato l’opzione Abilita riferimento, imposta l’opzione DN di base sulla parte *dc* del DN. Affinché il riferimento funzioni, l’intervallo di ricerca deve includere entrambi i domini principale e figlio.

>[!NOTE]
>
>Non includere il DN dell&#39;utente in questa impostazione. Per sincronizzare un utente specifico, utilizza l’impostazione filtro di ricerca.

Sebbene il DN di base sia un’impostazione obbligatoria nella console di amministrazione, alcuni server delle directory, come IBM Domino Enterprise Server, potrebbero richiedere un DN di base vuoto. Per specificare un DN di base vuoto, esporta il file config.xml, modifica l’impostazione nel file config.xml, quindi reimportalo. Consulta [Importazione ed esportazione del file di configurazione](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).

**Filtro di ricerca:** (obbligatorio) il filtro di ricerca da utilizzare per trovare il record associato all’utente. Puoi eseguire una ricerca a un livello o a un livello secondario. Consulta Sintassi del filtro di ricerca o RFC 2254. Per ulteriori informazioni sullo schema di Microsoft AD, consulta Schema di Active Directory.

**Descrizione:** l’attributo dello schema per la descrizione dell’utente

**Nome completo:** (obbligatorio) l’attributo dello schema per il nome completo dell’utente

**ID accesso:** (obbligatorio) l’attributo dello schema per l’ID di accesso dell’utente

**Cognome:** (obbligatorio) l’attributo dello schema per il cognome dell’utente

**Nome assegnato:** (obbligatorio) l’attributo dello schema per il nome dell’utente

**Iniziali:** l’attributo dello schema per le iniziali dell’utente

**Calendario aziendale:** ti consente di mappare un calendario aziendale a un utente in base al valore di questa impostazione (chiave del calendario aziendale). I calendari aziendali definiscono i giorni lavorativi e non lavorativi. AEM Forms può utilizzare i calendari aziendali per il calcolo di date e ore future per eventi quali promemoria, scadenze ed escalation. Il modo in cui assegni le chiavi del calendario aziendale agli utenti dipende dal fatto che utilizzi un dominio Enterprise, locale o ibrido. Consulta Configurazione dei calendari aziendali.

Se utilizzi un dominio Enterprise, puoi mappare l’impostazione del calendario aziendale a un campo nella directory LDAP. Ad esempio, se ogni record utente nella directory contiene un campo *paese* e desideri assegnare calendari aziendali in base al paese in cui si trova l’utente, specifica il nome del campo *paese* come valore per l’impostazione del calendario aziendale. Puoi quindi mappare le chiavi del calendario aziendale (i valori definiti per il campo *paese* nell’elenco LDAP) ai calendari aziendali in Forms Workflow.

Lo spazio utilizzato per visualizzare il nome della chiave del calendario aziendale nelle pagine di Forms Workflow è limitato. Limita il nome della chiave del calendario aziendale a meno di 53 caratteri per evitare che venga troncato su tali pagine.

**Modifica marca temporale:** per abilitare la sincronizzazione della directory delta, imposta questo valore per modificare la marca temporale. Consulta Abilitare la sincronizzazione della directory delta.

**Organizzazione:** l’attributo dello schema per il nome dell’organizzazione a cui appartiene l’utente.

**E-mail principale:** l’attributo dello schema per l’indirizzo e-mail principale dell’utente.

**E-mail secondaria:** l’attributo dello schema per l’indirizzo e-mail secondario dell’utente.

**Telefono:** l’attributo dello schema per il numero di telefono dell’utente.

**Indirizzo postale:** l’attributo dello schema per l’indirizzo postale dell’utente.

**Impostazioni locali:** l’attributo dello schema che contiene le informazioni ISO sulle impostazioni locali. Il valore è un codice lingua a due lettere o un codice lingua e paese.

**Fuso orario:** l’attributo dello schema che contiene il fuso orario in cui si trova l’utente. Il valore è una stringa come Città/Paese.

**Abilita controllo VLV (Virtual List View):** un controllo LDAP che consente ad AEM Forms di recuperare i dati in batch dal server delle directory. Se utilizzi Sun One come directory LDAP e la directory contiene molti utenti, l’abilitazione di VLV crea un indice utilizzabile da gestione utenti durante la ricerca degli utenti. Questa funzione è utile quando utilizzi un account utente normale in grado di sincronizzare solo una quantità limitata di dati. Puoi anche abilitare VLV per i gruppi. Se selezioni Abilita controllo VLV (Virtual List View), specifica un nome nella casella Ordina campo.

>[!NOTE]
>
>Per abilitare VLV, configura Sun One. Consulta [Configurare la gestione utenti per l’utilizzo di VLV (Virtual List View)](configuring-directories.md#configure-user-management-to-use-virtual-list-view-vlv).

**Ordina campo:** se selezioni l’opzione Abilita controllo VLV (Virtual List View), specifica il nome dell’attributo utilizzato per ordinare l’indice. Questo nome attributo (ad esempio UID) è quello specificato quando crei un indice per VLV sul server delle directory.

### Impostazioni gruppo {#group-settings}

**Identificatore univoco:** (obbligatorio) l’attributo univoco e costante utilizzato per identificare i gruppi. Utilizza un attributo non DN come identificatore univoco. Questa impostazione dipende dal server delle directory. Il valore è objectGUID per Active Directory 2003, nsuniqueID per Sun One e guid per eDirectory.

>[!NOTE]
>
>Assicurati di inserire un attributo che sia garantito come univoco all’interno dell’organizzazione. L’immissione di un valore errato può causare gravi problemi di sistema.

**DN di base:** (obbligatorio) il nome distinto di base della directory.

Sebbene il DN di base sia un’impostazione obbligatoria nella console di amministrazione, alcuni server delle directory, come IBM Domino Enterprise Server, richiedono un DN di base vuoto. Per specificare un DN di base vuoto, esporta il file config.xml, modifica l’impostazione nel file config.xml, quindi reimportalo. Consulta [Importazione ed esportazione del file di configurazione](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).

**Filtro di ricerca:** (obbligatorio) il filtro di ricerca da utilizzare per trovare il record associato al gruppo. Puoi eseguire una ricerca a un livello o a un livello secondario.

**Descrizione:** l’attributo dello schema per la descrizione del gruppo

**Nome completo:** (obbligatorio) l’attributo dello schema per il nome completo del gruppo

**DN iscritto:** (obbligatorio) l’attributo dello schema per il nome distinto degli iscritti di un gruppo

**Identificatore univoco iscritto:** l’identificatore univoco per un utente o un gruppo iscritto che appartiene al gruppo selezionato. Questo valore dipende dal server delle directory. Il valore è objectSID per AD2003, nsuniqueID per Sun One e guid per eDirectory.

Se DN iscritto è specificato con un attributo non DN, gestione utenti utilizza l’identificatore univoco iscritto per eseguire una query LDAP per raccogliere il DN dell’utente in quanto corrisponde a un valore identificatore univoco.

Se DN è specificato come identificatore univoco, non devi configurare l’identificatore univoco iscritto.

**Organizzazione:** l’attributo dello schema per il nome dell’organizzazione a cui appartiene il gruppo

**E-mail principale:** l’attributo dello schema per l’indirizzo e-mail principale del gruppo

**E-mail secondaria:** l’attributo dello schema per l’indirizzo e-mail secondario del gruppo

**Modifica marca temporale:** per abilitare la sincronizzazione della directory delta, imposta questo valore per modificare la marca temporale. Consulta Abilitare la sincronizzazione della directory delta.

**Abilita controllo VLV (Virtual List View):** un controllo LDAP che consente ad AEM Forms di recuperare i dati in batch dal server delle directory. Se utilizzi Sun One come directory LDAP e la directory contiene molti gruppi, l’abilitazione di VLV crea un indice utilizzabile da gestione utenti durante la ricerca dei gruppi. Questa funzione è utile quando utilizzi un account utente normale in grado di sincronizzare solo una quantità limitata di dati. Puoi inoltre abilitare VLV per gli utenti. Se selezioni Abilita controllo VLV (Virtual List View), specifica un nome per il campo di ordinamento.

>[!NOTE]
>
>Per abilitare VLV, configura Sun One. Consultare [Configurare la gestione utenti per l’utilizzo di VLV (Virtual List View)](configuring-directories.md#configure-user-management-to-use-virtual-list-view-vlv).

**Nome campo di ordinamento:** se hai selezionato l’opzione Abilita controllo VLV (Virtual List View), specifica il nome dell’attributo utilizzato per ordinare l’indice. Questo nome attributo è quello specificato al momento della creazione di un indice per VLV sul server delle directory.

>[!NOTE]
>
>Fai clic su Test per verificare che le impostazioni utente e gruppo vengano raccolte in base al DN di base e ai criteri di ricerca.

Se vengono restituiti utenti e gruppi, i risultati mostrano i valori assegnati a ciascun campo in base alla serie di attributi.

>[!NOTE]
>
>Gestione utenti non supporta ID utente duplicati all’interno di un dominio; viene sincronizzato un solo utente con l’ID utente.

## Configurare la gestione utenti per l’utilizzo di VLV (Virtual List View) {#configure-user-management-to-use-virtual-list-view-vlv}

La sincronizzazione delle directory è un requisito importante per la gestione utenti. Gli utenti e i gruppi vengono sincronizzati da una directory Enterprise al database di AEM Forms per l’assegnazione di ruoli e autorizzazioni. Il numero di utenti varia da 100 a oltre 100.000 a seconda dei requisiti e rappresenta una sfida tecnica per sincronizzare i dati in modo efficiente.

Il protocollo LDAP fornisce un meccanismo per eseguire query su set di dati di grandi dimensioni su più pagine utilizzando i controlli di richiesta. Quando utilizzi Microsoft Active Directory, la sincronizzazione del database da LDAP ad AEM Forms utilizza PagedResultsControl per recuperare i dati in batch di dimensioni particolari. Sun ONE Directory Server non supporta questo controllo. Per completare una query su più pagine su Sun ONE Directory Server, utilizza il controllo VLV (Virtual List View). Questo controllo coinvolge sia la configurazione lato server delle directory che l’implementazione lato client.

>[!NOTE]
>
>In questa sezione viene descritto l’utilizzo del controllo VLV per Sun ONE Directory Server. Tuttavia, puoi utilizzare questo controllo per qualsiasi server delle directory che supporta il controllo VLV.

1. Durante la configurazione della directory, seleziona Abilita controllo VLV (Virtual List View) sia nella pagina Impostazioni utente che nella pagina Impostazioni gruppo. Quando selezioni la casella di controllo, devi specifica anche un nome di ordinamento nella casella Ordina campo. Il valore predefinito è UID. Consulta [Aggiunta di directory o SPI personalizzati](configuring-directories.md#adding-directories-or-custom-spis) o [Modificare una directory](configuring-directories.md#edit-a-directory).
1. Utilizza la console di amministrazione di Sun ONE o uno script della riga di comando per creare le voci VLV LDAP per utenti e gruppi. Se utilizzi uno script della riga di comando, puoi utilizzare i file LDIF di utenti e gruppi di esempio. Consulta [Configurazione di Sun ONE Directory Server per VLV](configuring-directories.md#configuring-the-sun-one-directory-server-for-vlv).
1. Arresta il server e crea l’indice richiesto. (Consulta [Creare l’indice del server delle directory per VLV](configuring-directories.md#create-the-directory-server-index-for-vlv).)

### Configurazione del server delle directory Sun ONE per VLV {#configuring-the-sun-one-directory-server-for-vlv}

La creazione di un VLV richiede una coppia di voci che includono le classi oggetto `vlvSearch` e `vlvIndex`. La voce vlvSearch include una base di ricerca e l’attributo `vlvFilter`, che specifica la classe oggetto contenente gli attributi che desideri ordinare. La classe oggetto `vlvIndex` include l’attributo `vlvSort`, che specifica uno o più attributi da ordinare e il modo in cui ordinarli. (Il segno meno (-) indica l’ordine alfabetico inverso). L’utilizzo di VLV con AEM Forms richiede voci separate per gli utenti e i gruppi.

>[!NOTE]
>
>Le voci Oggetto possono essere create utilizzando l’interfaccia grafica utente (GUI) di Sun ONE o tramite uno script di una riga di comando. Per istruzioni sulla creazione delle voci Oggetto mediante l’interfaccia grafica utente, consulta la documentazione di Sun ONE.

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

1. Lo script di esempio contiene una voce LDAP denominata `lcuser`. Questa voce è per la configurazione relativa a VLV per la sincronizzazione degli utenti in AEM Forms. Modifica di conseguenza le seguenti proprietà:

   **Nome voce:** il nome della voce in questo esempio è `lcuser`. Se `lcuser` viene modificato, è necessario modificarlo in tutte le aree dello script di esempio.

   **vlvBase:** il DN di base specificato nella pagina Impostazioni utente.

   **vlvFilter:** il filtro di ricerca specificato nella pagina Impostazioni utente.

   **vlvSort:** il campo di ordinamento specificato nella sezione Impostazioni VLV della pagina Impostazioni utente. Un controllo VLV richiede di specificare un controllo di ordinamento. Questo campo viene utilizzato come parametro di ordinamento per l’indice vlv creato.

   **aci:** il controllo degli accessi specificato nello script di esempio concede a qualsiasi utente autenticato il diritto di accedere agli indici VLV per operazioni di lettura, ricerca e confronto. L’amministratore può limitare l’accesso a un utente di binding configurato nella pagina Impostazioni server delle directory, specificato nell’interfaccia utente Gestione utente. Se non vengono concesse le autorizzazioni, la ricerca utente non può utilizzare VLV e il server LDAP genera un’eccezione nell’autorizzazione.

   >[!NOTE]
   >
   >Come convenzione, anche il nome della voce vlvIndex è impostato su `lcuser`, ma puoi assegnarle un nome diverso. Utilizza lo stesso nome nello strumento vlvindex. (Consulta [Creare l’indice del server delle directory per VLV ](configuring-directories.md#create-the-directory-server-index-for-vlv)*.)*

1. Utilizzando lo strumento `ldapmodify` fornito con il server Sun ONE, crea una voce simile per i gruppi utilizzando rispettivamente il DN di base, il filtro di ricerca e il campo di ordinamento del gruppo:

   `server directory\shared\bin>ldapmodify -v -a -h host -p port -D "admin user" -w "password" -f "LDIF file location"`

   Digita, ad esempio, il testo seguente:

   `D:\tools\ldap\sun\shared\bin> -v -a -h localhost -p 55850 -D "uid=admin,ou=administrators,ou=topologymanagement,o=netscaperoot" -w "admin" -f "D:\tools\ldap\data\vlv feature\users.ldif"`

### Creare l’indice del server delle directory per VLV {#create-the-directory-server-index-for-vlv}

Dopo aver configurato le impostazioni della directory e creato le voci VLV LDAP per utenti e gruppi, arresta il server e crea l’indice richiesto.

1. Dopo aver creato le voci oggetto, arresta il server Sun ONE.
1. Utilizzando lo strumento vlvindex, genera l’indice digitando il testo seguente:

   *directory server instance* `\vlvindex.bat -n userRoot -T lcuser`

   Viene generato l’output seguente:

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

   Lo strumento vlvindex è presente nella directory dell’istanza del server delle directory. Se il server Sun ONE dispone di due istanze che eseguono server1 e server2, lo strumento vlvindex si trova nella directory *Sun ONE server directory*\server1. Il valore del parametro `-T` è il valore dell’attributo `cn` della voce vlvindex creata in precedenza nell’LDIF di esempio. In questo caso è `lcuser`.

1. Se VLV è abilitato anche per i gruppi, crea l’indice corrispondente per i gruppi. Verifica se gli indici vengono creati eseguendo il seguente comando:

   *sun one server directory* `\shared\bin>ldapsearch -h`*hostname* `-p`*port no* `-s base -b "" objectclass=*`

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
