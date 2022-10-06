---
title: Configurazione delle directory
seo-title: Configuring directories
description: Scopri come aggiungere, modificare ed eliminare le directory e configurare la gestione degli utenti per utilizzare la visualizzazione a elenco virtuale.
seo-description: Learn how to add, edit and delete directories and configure user management to use virtual list view.
uuid: 0bf1a8a7-c917-4248-9937-d24e31c5ba17
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 1f15f028-aa81-478e-97eb-f83a4dc0418c
exl-id: 30edcef2-e8fa-403a-9850-b8dfeeb9ac65
source-git-commit: 1cdd15800548362ccdd9e70847d9df8ce93ee06e
workflow-type: tm+mt
source-wordcount: '3227'
ht-degree: 0%

---

# Configurazione delle directory {#configuring-directories}

Per ogni dominio enterprise configurato, specificare le directory richieste dal provider di autenticazione per le informazioni utente. Puoi configurare più directory per un dominio.

## Aggiunta di directory o SPI personalizzati {#adding-directories-or-custom-spis}

Per ogni dominio enterprise configurato, specificare le directory richieste dal provider di autenticazione per le informazioni utente. È possibile aggiungere una directory a un dominio enterprise esistente o a un nuovo dominio enterprise che si sta aggiungendo. Puoi configurare più directory per un dominio. Puoi anche configurare un dominio per l’utilizzo di un’interfaccia SPI (Service Provider Interface) personalizzata per la sincronizzazione.

### Aggiungi una directory {#add-a-directory}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fare clic su Nuovo dominio Enterprise o selezionare un dominio enterprise esistente.
1. Fare clic su Aggiungi directory.
1. Nella casella Nome profilo digitare un nome per distinguere questa directory e quindi fare clic su Avanti.
1. Configura le impostazioni del server delle directory. (Vedi [Impostazioni directory](configuring-directories.md#directory-settings).)
1. Per verificare che sia possibile effettuare una connessione al server LDAP, fare clic su Prova. Se il test non riesce, esaminare l&#39;eccezione nel file di log di Application Server per determinare la causa principale dell&#39;errore. Fare clic su Chiudi, quindi su Avanti.
1. Seleziona Impostazioni utente e configura le impostazioni in base alle esigenze. (Vedi [Impostazioni directory](configuring-directories.md#directory-settings).)
1. Per verificare che il DN di base e gli altri attributi configurati raccolgano il batch di utenti corretto, fare clic su Prova. LDAP tenta di recuperare i primi 200 record utilizzando le impostazioni fornite (come il DN di base, il filtro di ricerca e tutti gli attributi).

   Se gli utenti vengono restituiti, i risultati mostrano i valori assegnati a ciascun campo in base al set di attributi. Se il test non riesce a causa di un nome di server inesistente, informazioni di autorizzazione errate o attributi errati, viene visualizzato il seguente messaggio di errore: &quot;I criteri di ricerca specificati non restituivano alcun risultato&quot;. Per determinare la causa principale dell&#39;errore, esaminare l&#39;eccezione nel file di registro di Application Server. Fare clic su Chiudi, quindi su Avanti.

1. Seleziona Impostazioni gruppo e configura le impostazioni in base alle esigenze. (Vedi [Impostazioni directory](configuring-directories.md#directory-settings).)
1. Per verificare che il DN di base e gli altri attributi configurati raccolgano il batch di gruppi corretto, fare clic su Prova. Se vengono restituiti gruppi, i risultati mostrano i valori assegnati a ciascun campo in base al set di attributi. Fai clic su Chiudi.

### Aggiungi un SPI personalizzato {#add-a-custom-spi}

Per informazioni sulla creazione di un SPI personalizzato, vedere &quot;Sviluppo di SPI per moduli AEM&quot; in [Programmazione con moduli AEM](https://www.adobe.com/go/learn_aemforms_programming_63). Per rendere disponibile un nuovo SPI personalizzato implementato per l&#39;associazione con il dominio, riavvia il server.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fare clic su Nuovo dominio Enterprise o selezionare un dominio enterprise esistente.
1. Fare clic su Aggiungi directory.
1. Digitare un nome nella casella Nome profilo, selezionare Provider SPI personalizzato, quindi fare clic su Avanti.
1. Selezionare un provider utente personalizzato dall&#39;elenco e fare clic su Avanti.
1. Selezionare un provider di gruppi personalizzato dall&#39;elenco e fare clic su Fine.

## Modificare una directory {#edit-a-directory}

Puoi modificare i dettagli di una directory configurata in precedenza.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fai clic sul dominio appropriato nell’elenco e, nella pagina visualizzata, seleziona la directory appropriata dall’elenco.
1. Configura le impostazioni della directory, dell’utente e del gruppo in base alle esigenze. (Vedi [Impostazioni directory](configuring-directories.md#directory-settings).)
1. Fai clic su OK.

## Eliminare una directory {#delete-a-directory}

Quando si sincronizzano i domini dopo l&#39;eliminazione di una directory, tutti gli utenti e i gruppi in tale directory vengono contrassegnati come obsoleti nel database. Non verranno restituiti in alcuna ricerca dalla console di amministrazione.

>[!NOTE]
>
>I domini Enterprise richiedono almeno un provider di autenticazione e un provider di directory.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fai clic sul dominio appropriato nell’elenco.
1. Selezionare la casella di controllo relativa alla directory appropriata e fare clic su Elimina.
1. Fare clic su OK nella pagina di conferma visualizzata e fare di nuovo clic su OK.

## Impostazioni directory {#directory-settings}

Quando aggiungi una directory a un dominio, specifica le seguenti impostazioni di directory.

**Server:** (Obbligatorio) Nome di dominio completo (FQDN) del server delle directory. Ad esempio, per un computer chiamato x sulla rete adobe.com, l&#39;FQDN è x.adobe.com. Un indirizzo IP può essere utilizzato al posto del nome del server FQDN.

**Porta:** (Obbligatorio) La porta utilizzata dal server delle directory. In genere 389 o 636 se il protocollo SSL (Secure Sockets Layer) viene utilizzato per l&#39;invio di informazioni di autenticazione sulla rete.

**SSL:** (Obbligatorio) Specifica se il server di directory utilizza SSL quando invia dati sulla rete. Il valore predefinito è No. Se è impostato su Sì, il certificato del server LDAP corrispondente deve essere considerato attendibile dall&#39;ambiente di runtime Java™ (JRE) del server dell&#39;applicazione.

**Binding** (Obbligatorio) Specifica come accedere alla directory.

**Anonimo:** Non è richiesto alcun nome utente o password. Un utente anonimo può essere in grado di recuperare solo una quantità limitata di dati. Questa opzione può essere utile per il test iniziale.

**Utente:** L&#39;autenticazione è obbligatoria. Nella casella Nome specificare il nome del record utente che può accedere alla directory. È consigliabile inserire il nome distinto completo (DN) dell’account utente, ad esempio cn=Jane Doe, ou=user, dc=can, dc=com. Nella casella Password specificare la password associata. Queste impostazioni sono necessarie quando si seleziona Utente come opzione Binding.

**Nome:** Nome che può essere utilizzato per connettersi al database LDAP quando l&#39;accesso anonimo non è abilitato. Per Active Directory 2003, specificare `[domain name]\[userid]`. Per Sun™ One, eDirectory o IBM Tivoli Directory Server, specificare il nome completo dell&#39;utente, ad esempio uid=lcuser,ou=it,o=company.com.

**Password:** Password corrispondente al nome specificato per la connessione al database LDAP quando l&#39;accesso anonimo non è abilitato.

**Popolare la pagina con:** Quando è selezionata, compila gli attributi nelle pagine delle impostazioni Utente e Gruppo con i corrispondenti valori LDAP predefiniti.

**Recupera DN di base:** Recupera i DN di base e li visualizza nell&#39;elenco a discesa. Questa impostazione è utile quando disponi di più DN di base e devi selezionare un valore.

**Abilita riferimento:** Questa impostazione è applicabile quando l&#39;organizzazione utilizza più domini di Active Directory organizzati in una struttura gerarchica e si dispone di impostazioni di directory specificate solo per il dominio padre. In questa situazione, quando selezioni questa opzione, Gestione utente può accedere ai dettagli di utenti e gruppi dai domini figlio.

>[!NOTE]
>
>Fai clic su Prova per verificare che sia possibile effettuare una connessione al server LDAP. Per determinare la causa principale di eventuali errori, esaminare l&#39;eccezione nel file di registro di Application Server.

### Impostazioni utente {#user-settings}

**Identificatore univoco:** (Obbligatorio) Attributo univoco e costante utilizzato per identificare gli utenti. Utilizza un attributo non DN come identificatore univoco perché il DN di un utente può cambiare se si sposta in un&#39;altra parte dell&#39;organizzazione. Questa impostazione dipende dal server di directory. Il valore è objectGUID per Active Directory 2003, nsuniqueID per Sun™ One e guid per eDirectory.

>[!NOTE]
>
>Assicurati di inserire un attributo che sia garantito come univoco nell&#39;organizzazione. L&#39;immissione di un valore non corretto può causare gravi problemi di sistema.

**DN di base:** Imposta come punto di partenza per la sincronizzazione di utenti e gruppi dalla gerarchia LDAP. È consigliabile specificare un DN di base al livello più basso della gerarchia che includa tutti gli utenti e i gruppi che devono essere sincronizzati per i servizi.

Se è stata selezionata l&#39;opzione Abilita riferimento nelle impostazioni Directory, impostare l&#39;opzione DN di base su *dc* parte del DN. Affinché il riferimento funzioni, l’intervallo di ricerca deve includere sia i domini padre che quelli secondari.

>[!NOTE]
>
>Non includere il DN dell’utente in questa impostazione. Per sincronizzare un particolare utente, utilizza l’impostazione Filtro di ricerca .

Sebbene Base DN sia un&#39;impostazione obbligatoria nella console di amministrazione, alcuni server di directory come IBM Domino Enterprise Server potrebbero richiedere un BaseDN vuoto. Per specificare un DN Base vuoto, esportare il file config.xml, modificare l&#39;impostazione nel file config.xml e quindi reimportarlo. (Vedi [Importazione ed esportazione del file di configurazione](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).)

**Filtro di ricerca:** (Obbligatorio) Il filtro di ricerca da utilizzare per trovare il record associato all&#39;utente. È possibile eseguire una ricerca a un livello o a un livello secondario. (Consulta Sintassi del filtro di ricerca o RFC 2254). Per ulteriori informazioni sullo schema di Microsoft AD, vedere Schema di Active Directory.

**Descrizione:** Attributo schema per la descrizione dell’utente

**Nome completo:** (Obbligatorio) Attributo schema per il nome completo dell&#39;utente

**ID di accesso:** (Obbligatorio) Attributo schema per l&#39;ID di accesso dell&#39;utente

**Cognome:** (Obbligatorio) Attributo schema per il cognome dell’utente

**Nome:** (Obbligatorio) Attributo schema per il nome dell’utente

**Iniziali:** Attributo schema per le iniziali dell’utente

**Calendario aziendale:** Consente di mappare un calendario aziendale a un utente in base al valore di questa impostazione (la chiave del calendario aziendale). I calendari aziendali definiscono i giorni lavorativi e non lavorativi. I moduli AEM possono utilizzare calendari aziendali per calcolare date e ore future relative a eventi quali promemoria, scadenze ed escalation. Il modo in cui si assegnano le chiavi del calendario aziendale agli utenti dipende dal fatto che si utilizzi un dominio enterprise, locale o ibrido. (Vedere Configurazione dei calendari aziendali.)

Se utilizzi un dominio Enterprise, puoi mappare l&#39;impostazione Calendario aziendale su un campo nella directory LDAP. Ad esempio, se ogni record utente nella directory contiene un *paese* e si desidera assegnare calendari aziendali in base al paese in cui si trova l&#39;utente, specificare il *paese* Nome del campo come valore per l&#39;impostazione del calendario aziendale. È quindi possibile mappare le chiavi del calendario aziendale (i valori definiti per *paese* nella directory LDAP) ai calendari aziendali nel flusso di lavoro dei moduli.

Lo spazio utilizzato per visualizzare il nome della chiave del calendario aziendale nelle pagine del flusso di lavoro dei moduli è limitato. Limita il nome della chiave del calendario aziendale a meno di 53 caratteri per evitare che venga troncata su tali pagine.

**Modifica timestamp:** Per abilitare la sincronizzazione della directory delta, imposta questo valore per modificare TimeStamp. (Consultare Attivare la sincronizzazione della directory delta .)

**Organizzazione:** Attributo schema per il nome dell&#39;organizzazione a cui appartiene l&#39;utente.

**E-mail principale:** Attributo schema per l’indirizzo e-mail principale dell’utente.

**E-mail secondaria:** Attributo schema per l’indirizzo e-mail secondario dell’utente.

**Telefono:** Attributo schema per il numero di telefono dell’utente.

**Indirizzo postale:** Attributo schema per l’indirizzo di posta dell’utente.

**Impostazioni internazionali:** Attributo dello schema contenente le informazioni internazionali ISO. Il valore è un codice di lingua a due lettere o un codice di lingua e paese.

**Fuso orario:** Attributo dello schema contenente il fuso orario in cui si trova l’utente. Il valore è una stringa come Città/Paese.

**Attiva controllo VLV (Virtual List View):** Controllo LDAP che consente ai moduli AEM di recuperare i dati in batch dal server delle directory. Se utilizzi Sun One come directory LDAP e la directory contiene molti utenti, l&#39;abilitazione di VLV crea un indice che User Management può utilizzare durante la ricerca degli utenti. Questa funzione è utile quando si utilizza un account utente normale che può sincronizzare solo una quantità limitata di dati. Puoi anche abilitare VLV per i gruppi. Se si seleziona Abilita controllo visualizzazione elenco virtuale (VLV), specificare un nome nella casella Campo di ordinamento.

>[!NOTE]
>
>Per abilitare VLV, configurare Sun One. Vedi [Configurare User Management per l’utilizzo della visualizzazione elenco virtuale (VLV)](configuring-directories.md#configure-user-management-to-use-virtual-list-view-vlv).

**Campo di ordinamento:** Se hai selezionato Abilita controllo visualizzazione elenco virtuale (VLV), specifica il nome dell’attributo utilizzato per ordinare l’indice. Questo nome attributo (ad esempio uid) è quello specificato quando è stato creato un indice per VLV sul server delle directory.

### Impostazioni del gruppo {#group-settings}

**Identificatore univoco:** (Obbligatorio) Attributo univoco e costante utilizzato per identificare i gruppi. Utilizza un attributo non-DN come identificatore univoco. Questa impostazione dipende dal server di directory. Il valore è objectGUID per Active Directory 2003, nsuniqueID per Sun One e guid per eDirectory.

>[!NOTE]
>
>Assicurati di inserire un attributo che sia garantito come univoco nell&#39;organizzazione. L&#39;immissione di un valore non corretto può causare gravi problemi di sistema.

**DN di base:** (Obbligatorio) Nome distinto di base della directory.

Sebbene Base DN sia un&#39;impostazione obbligatoria nella console di amministrazione, alcuni server di directory come IBM Domino Enterprise Server richiedono un BaseDN vuoto. Per specificare un DN Base vuoto, esportare il file config.xml, modificare l&#39;impostazione nel file config.xml e quindi reimportarlo. (Vedi [Importazione ed esportazione del file di configurazione](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).)

**Filtro di ricerca:** (Obbligatorio) Il filtro di ricerca da utilizzare per trovare il record associato al gruppo. È possibile eseguire una ricerca a un livello o a un livello secondario.

**Descrizione:** Attributo schema per la descrizione del gruppo

**Nome completo:** (Obbligatorio) Attributo schema per il nome completo del gruppo

**DN membro:** (Obbligatorio) Attributo schema per il nome distinto dei membri all&#39;interno di un gruppo

**Identificatore univoco membro:** Identificatore univoco per un utente o gruppo che è membro del gruppo selezionato. Questo valore dipende dal server di directory. Il valore è objectSID per AD2003, nsuniqueID per Sun One e guid per eDirectory.

Se il DN del membro è specificato con un attributo non DN, User Management utilizza l’identificatore univoco del membro per eseguire una query su LDAP per raccogliere il DN dell’utente, in quanto corrisponde a un valore di identificatore univoco.

Se DN è specificato come identificatore univoco, non è necessario configurare l&#39;identificativo univoco del membro.

**Organizzazione:** Attributo schema per il nome dell&#39;organizzazione a cui appartiene il gruppo

**E-mail principale:** Attributo schema per l’indirizzo e-mail principale del gruppo

**E-mail secondaria:** Attributo schema per l’indirizzo e-mail secondario del gruppo

**Modifica timestamp:** Per abilitare la sincronizzazione della directory delta, imposta questo valore per modificare TimeStamp. (Consultare Attivare la sincronizzazione della directory delta .)

**Attiva controllo VLV (Virtual List View):** Controllo LDAP che consente ai moduli AEM di recuperare i dati in batch dal server delle directory. Se utilizzi Sun One come directory LDAP e la directory contiene molti gruppi, l&#39;abilitazione di VLV crea un indice che User Management può utilizzare durante la ricerca dei gruppi. Questa funzione è utile quando si utilizza un account utente normale che può sincronizzare solo una quantità limitata di dati. Puoi anche abilitare il VLV per gli utenti. Se si seleziona Abilita controllo visualizzazione elenco virtuale (VLV), specificare un nome del campo di ordinamento.

>[!NOTE]
>
>Per abilitare VLV, configurare Sun One. Vedi [Configurare User Management per l’utilizzo della visualizzazione elenco virtuale (VLV)](configuring-directories.md#configure-user-management-to-use-virtual-list-view-vlv).

**Nome campo di ordinamento:** Se hai selezionato Abilita controllo visualizzazione elenco virtuale (VLV), specifica il nome dell’attributo utilizzato per ordinare l’indice. Questo nome attributo è quello specificato quando è stato creato un indice per VLV sul server delle directory.

>[!NOTE]
>
>Fai clic su Prova per verificare che le impostazioni utente e gruppo siano raccolte in base al DN di base e ai criteri di ricerca.

Se vengono restituiti utenti e gruppi, i risultati mostrano i valori assegnati a ciascun campo in base al set di attributi.

>[!NOTE]
>
>Gestione utente non supporta ID utente duplicati all’interno di un dominio; viene sincronizzato un solo utente con l’ID utente.

## Configurare User Management per l’utilizzo della visualizzazione elenco virtuale (VLV) {#configure-user-management-to-use-virtual-list-view-vlv}

La sincronizzazione della directory è un requisito importante per la gestione degli utenti. Gli utenti e i gruppi vengono sincronizzati da una directory enterprise al database dei moduli AEM per assegnare ruoli e autorizzazioni. Il numero di utenti varia da 100 a 100000+ a seconda dei requisiti, e rappresenta una sfida tecnica per sincronizzare i dati in modo efficiente.

Il protocollo LDAP fornisce un meccanismo per eseguire query su set di dati di grandi dimensioni in modo impaginato utilizzando i controlli di richiesta. Quando si utilizza Microsoft Active Directory, LDAP per AEM la sincronizzazione del database dei moduli utilizza PagedResultsControl per recuperare i dati in batch di dimensioni particolari. Il server di directory Sun ONE non supporta questo controllo. Per completare una query impaginata sul server di directory Sun ONE, utilizzare il controllo VLV (Virtual List View). Questo controllo include sia la configurazione lato server della directory che l&#39;implementazione lato client.

>[!NOTE]
>
>Questa sezione descrive l&#39;utilizzo del controllo VLV per Sun ONE Directory Server. Tuttavia, è possibile utilizzare questo controllo per qualsiasi server di directory che supporta il controllo VLV.

1. Durante la configurazione della directory, selezionare Abilita controllo visualizzazione elenco virtuale (VLV) sia nella pagina Impostazioni utente che nella pagina Impostazioni gruppo. Quando si seleziona la casella di controllo, è inoltre necessario specificare un nome di ordinamento nella casella Campo di ordinamento. Il valore predefinito è uid. (Vedi [Aggiunta di directory o SPI personalizzati](configuring-directories.md#adding-directories-or-custom-spis) o [Modificare una directory](configuring-directories.md#edit-a-directory).)
1. Utilizza la console di amministrazione Sun ONE o uno script a riga di comando per creare le voci VLV LDAP per utenti e gruppi. Se si utilizza uno script della riga di comando, è possibile utilizzare i file LDIF di esempio per gli utenti e i gruppi. (Vedi [Configurazione del server di directory Sun ONE per VLV](configuring-directories.md#configuring-the-sun-one-directory-server-for-vlv).)
1. Arresta il server e crea l&#39;indice richiesto. (Vedi [Creare l&#39;indice del server di directory per VLV](configuring-directories.md#create-the-directory-server-index-for-vlv).)

### Configurazione del server di directory Sun ONE per VLV {#configuring-the-sun-one-directory-server-for-vlv}

La creazione di un VLV richiede una coppia di voci che includono `vlvSearch` e `vlvIndex` classi oggetto. La voce vlvSearch include una base di ricerca e il `vlvFilter` attributo , che specifica la classe oggetto contenente gli attributi che si desidera ordinare. La `vlvIndex` la classe object include `vlvSort` attributo , che specifica uno o più attributi da ordinare e l&#39;ordine in cui ordinarli. (Il segno meno (-) indica l&#39;ordine alfabetico inverso). L’utilizzo di VLV con moduli AEM richiede voci separate per utenti e gruppi.

>[!NOTE]
>
>Le voci dell&#39;oggetto possono essere create utilizzando l&#39;interfaccia utente grafica Sun ONE (GUI) o attraverso uno script a riga di comando. Per istruzioni su come creare le voci dell&#39;oggetto utilizzando l&#39;interfaccia grafica, vedere la documentazione Sun ONE.

Ecco uno script di esempio LDIF per la voce VLV per gli utenti:

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

**Creare le voci dell’oggetto utilizzando uno script**

1. Lo script di esempio ha una voce LDAP denominata `lcuser`. Questa voce è relativa alla configurazione VLV per la sincronizzazione utente nei moduli AEM. Modifica di conseguenza le seguenti proprietà:

   **Nome voce:** Il nome della voce in questo esempio è `lcuser`. Se `lcuser` viene modificato e deve essere modificato in tutte le aree dello script di esempio.

   **vlvBase:** Il DN di base specificato nella pagina Impostazioni utente.

   **vlvFilter:** Filtro di ricerca specificato nella pagina Impostazioni utente.

   **vlvSort:** Campo di ordinamento specificato nella sezione delle impostazioni VLV della pagina Impostazioni utente. Un controllo VLV richiede di specificare un controllo di ordinamento. Questo campo viene utilizzato come parametro di ordinamento per l&#39;indice vlv creato.

   **aci:** Il controllo di accesso specificato nello script di esempio concede a qualsiasi utente autenticato il diritto di accedere agli indici VLV per le operazioni di lettura, ricerca e confronto. L&#39;amministratore può limitare l&#39;accesso a un utente di binding, configurato nella pagina Impostazioni server delle directory specificata nell&#39;interfaccia utente Gestione utente. Se non si forniscono le autorizzazioni, la ricerca utente non può utilizzare il VLV e il server LDAP genera un&#39;eccezione di autorizzazione.

   >[!NOTE]
   >
   >Come convenzione, anche il nome della voce vlvIndex è impostato su `lcuser`ma puoi dargli un nome diverso. Usa lo stesso nome nello strumento vlvindex. (Vedi [Creare l&#39;indice del server di directory per VLV ](configuring-directories.md#create-the-directory-server-index-for-vlv)*.)*

1. Utilizzo della `ldapmodify` strumento fornito con Sun ONE Server, creare una voce simile per i gruppi utilizzando rispettivamente Base DN del gruppo, Filtro di ricerca e Campo di ordinamento:

   `server directory\shared\bin>ldapmodify -v -a -h host -p port -D "admin user" -w "password" -f "LDIF file location"`

   Ad esempio, digitare il testo seguente:

   `D:\tools\ldap\sun\shared\bin> -v -a -h localhost -p 55850 -D "uid=admin,ou=administrators,ou=topologymanagement,o=netscaperoot" -w "admin" -f "D:\tools\ldap\data\vlv feature\users.ldif"`

### Creare l&#39;indice del server di directory per VLV {#create-the-directory-server-index-for-vlv}

Dopo aver configurato le impostazioni della directory e creato le voci VLV LDAP per utenti e gruppi, interrompi il server e crea l&#39;indice richiesto.

1. Dopo aver creato le voci dell&#39;oggetto, arrestare Sun ONE Server.
1. Utilizzando lo strumento vlvindex, genera l&#39;indice digitando il seguente testo:

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

   Lo strumento vlvindex è presente nella directory dell&#39;istanza del server delle directory. Se Sun ONE Server ha due istanze che eseguono server1 e server2, lo strumento vlvindex si trova in *Directory server Sun ONE*\server1 directory. Il valore del parametro `-T` è il valore del `cn` attributo della voce vlvindex creata in precedenza nel LDIF campione. In questo caso è `lcuser`.

1. Se VLV è abilitato anche per i gruppi, creare l&#39;indice corrispondente per i gruppi. Verifica se gli indici sono creati eseguendo il comando seguente:

   *directory server Sun one* `\shared\bin>ldapsearch -h`*hostname* `-p`*porta n.* `-s base -b "" objectclass=*`

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
