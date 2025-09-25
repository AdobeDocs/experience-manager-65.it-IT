---
title: Aggiungere domini
description: Scopri come aggiungere un dominio Enterprise, locale o ibrido utilizzando le impostazioni di Gestione dominio e le considerazioni generali per i nomi di dominio e gli ID.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: c708936d-7aa7-4b92-be2d-d97008f187d2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '941'
ht-degree: 100%

---

# Aggiungere domini {#adding-domains}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

## Aggiungere un dominio enterprise {#add-an-enterprise-domain}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utenti > Gestione dominio.
1. Fai clic su Nuovo dominio enterprise.
1. Nella casella ID, digita un identificatore univoco per il dominio e nella casella Nome digita un nome descrittivo per il dominio. (Consulta [Considerazioni importanti per i nomi di dominio e gli ID](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. Specifica se abilitare il blocco account. (Consulta [Configurare le impostazioni di blocco account](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings).) Per impostazione predefinita, Abilita blocco account è selezionato.
1. Fai clic su Aggiungi autenticazione e, nell’elenco Provider di autenticazione, seleziona un provider, a seconda del meccanismo di autenticazione utilizzato dall’organizzazione. I valori possibili sono LDAP, Kerberos, SAML o un provider di autenticazione personalizzato.

   Se selezioni LDAP, puoi utilizzare il server LDAP specificato nella configurazione della directory oppure scegliere un server LDAP diverso da utilizzare per l’autenticazione. Se scegli un server diverso, gli utenti devono esistere in entrambi i server LDAP.

1. Fornisci eventuali informazioni aggiuntive richieste sulla pagina. (Consulta [Impostazioni di autenticazione](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. Aggiungi una directory o un’interfaccia del provider di servizi (SPI) personalizzata. (Consulta [Aggiunta di directory o SPI personalizzati](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis).)
1. Fai clic su Fine e quindi su OK.

Dopo aver creato un dominio enterprise, sincronizza manualmente la directory o crea un trigger per eseguire una sincronizzazione prima che la Gestione utente possa utilizzarla. Puoi, quindi, configurare una pianificazione di sincronizzazione della directory ed eseguire la sincronizzazione manuale in base alle esigenze. (Consulta [Sincronizzazione delle directory](/help/forms/using/admin-help/synchronizing-directories.md#synchronizing-directories).)

## Aggiungere un dominio locale {#add-a-local-domain}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utenti > Gestione dominio.
1. Fai clic su Nuovo dominio locale.
1. Nella casella ID, digita un identificatore univoco per il dominio e, nella casella Nome, digita un nome descrittivo per il dominio. (Consulta [Considerazioni importanti per i nomi di dominio e gli ID](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. Specifica se attivare il blocco dell’account e quindi fai clic su OK. (Consulta [Configurare le impostazioni di blocco account](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings).) Per impostazione predefinita, Abilita blocco account è selezionato.

## Aggiungere un dominio ibrido {#add-a-hybrid-domain}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utenti > Gestione dominio.
1. Fai clic su Nuovo dominio ibrido.
1. Nella casella ID, digita un identificatore univoco per il dominio e, nella casella Nome, digita un nome descrittivo per il dominio. (Consulta [Considerazioni importanti per i nomi di dominio e gli ID](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. Fai clic su Aggiungi autenticazione e, nell’elenco Provider di autenticazione, seleziona un provider, a seconda del meccanismo di autenticazione utilizzato dall’organizzazione. I valori possibili sono LDAP, Kerberos, SAML o un provider di autenticazione personalizzato.
1. Fornisci eventuali informazioni aggiuntive richieste sulla pagina. (Consulta [Impostazioni di autenticazione](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. Fai clic su OK e quindi di nuovo su OK.

## Considerazioni importanti per i nomi di dominio e gli ID {#important-considerations-for-domain-names-and-ids}

Quando scegli un nome di dominio e un ID, tieni presenti le seguenti considerazioni:

### Considerazioni generali {#general-considerations}

* Quando utilizzi un provider di database diverso da DB2, l’ID dominio può contenere fino a 50 byte. Se utilizzi caratteri ASCII a byte singolo, il limite è di 50 caratteri. Se l’identificatore del dominio contiene caratteri multibyte, questo limite viene ridotto. Ad esempio, se crei un dominio il cui identificatore contiene caratteri a 3 byte, il limite è di 16 caratteri. Inoltre, non è possibile creare domini che contengono caratteri a 4 byte. Se crei un ID dominio che supera questo limite, AEM Forms si trovarà in uno stato instabile. Per riparare questo stato instabile, consulta “[Rimuovere un dominio contenente caratteri estesi o multibyte](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters)” in questa pagina.
* Il numero di domini Enterprise e locali che possono essere creati all’interno di AEM Forms dipende dalla lunghezza di ciascuno degli ID di dominio. Quando aggiungi un dominio Enterprise o ibrido, Gestione utenti aggiorna la stringa configInstance nel nodo AuthProviders del file di configurazione di AEM Forms (config.xml). La stringa configInstance contiene un elenco separato da due punti dei percorsi assoluti di tutti i domini associati al provider di autorizzazione. Questa stringa ha una dimensione massima di 8192 caratteri. Una volta raggiunto tale limite, non puoi creare domini aggiuntivi.

### Considerazioni riguardanti l’utilizzo di DB2 {#considerations-when-using-db2}

Quando utilizzi DB2 come database di AEM Forms, la lunghezza massima consentita dell’ID dominio dipende dal tipo di caratteri utilizzati:

* 100 caratteri a byte singolo (ASCII), ad esempio caratteri utilizzati in inglese, francese o tedesco
* 50 caratteri a byte doppio, ad esempio caratteri utilizzati in cinese, giapponese o coreano
* 25 caratteri a quattro byte (ad esempio, caratteri utilizzati nella lingua cinese tradizionale)

### Considerazioni riguardanti l’utilizzo di MySQL {#considerations-when-using-mysql}

Quando utilizzi MySQL come database di AEM Forms, si applicano le seguenti limitazioni:

* Come ID di dominio e nome di dominio vengono utilizzati solo caratteri ASCII (byte singolo). Se utilizzi caratteri ASCII estesi, i moduli AEM si troveranno in uno stato instabile e potrebbero generare un’eccezione se tenti di eliminare il dominio. Per riparare questo stato instabile, consulta l’argomento “[Rimuovi un dominio contenente caratteri estesi o multi-byte](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters)” in questa pagina.
* Non puoi creare due domini con lo stesso nome e con la sola differenza di lettere maiuscole e minuscole. Se ad esempio tenti di creare un dominio denominato *Adobe* quando esiste già un dominio denominato *adobe*, verrà generato un errore.
* Gestione Utente non è in grado di distinguere tra due nomi di dominio che differiscono solo per l’utilizzo di caratteri estesi. Ad esempio, se crei un dominio denominato *abcde* e un dominio denominato *âbcdè*, verranno considerati uguali.

### Rimuovere un dominio contenente caratteri estesi o multi-byte {#remove-a-domain-that-contains-extended-or-multi-byte-characters}

1. Esporta il file di configurazione come descritto in [Importazione ed esportazione del file di configurazione](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).
1. Apri il file di configurazione e, sotto il nodo Domini, individua il nodo il cui attributo name corrisponde al nome del dominio creato con caratteri estesi o multi-byte. Elimina l’intero nodo correlato a tale dominio.
1. Nel database, cerca il dominio nella tabella edcprincipaldomainentity:

   * Seleziona `*` da edcprincipaldomainentity.
   * Trova il nome di dominio che contiene caratteri estesi o multi-byte e impostane lo stato su OBSOLETO.

1. Importa il file di configurazione aggiornato come descritto in [Importazione ed esportazione del file di configurazione](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).
