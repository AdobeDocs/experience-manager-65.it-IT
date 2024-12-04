---
title: Aggiunta di domini
description: Scopri come aggiungere un dominio enterprise, locale o ibrido utilizzando le impostazioni di Gestione dominio e le considerazioni generali per i nomi di dominio e gli ID.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: c708936d-7aa7-4b92-be2d-d97008f187d2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: eac8a82c78d7f209512d32e7fcd7083bbebf1cb5
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---

# Aggiunta di domini {#adding-domains}

Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

## Aggiungere un dominio enterprise {#add-an-enterprise-domain}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fare clic su Nuovo dominio enterprise.
1. Nella casella ID digitare un identificatore univoco per il dominio e nella casella Nome digitare un nome descrittivo per il dominio. (Vedi [Considerazioni importanti per i nomi di dominio e gli ID](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. Specifica se abilitare il blocco account. (Vedere [Configurare le impostazioni di blocco account](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings).) Per impostazione predefinita, l&#39;opzione Abilita blocco account è selezionata.
1. Fare clic su Aggiungi autenticazione e, nell&#39;elenco Provider di autenticazione, selezionare un provider, a seconda del meccanismo di autenticazione utilizzato dall&#39;organizzazione. I valori possibili sono LDAP, Kerberos, SAML o un provider di autenticazione personalizzato.

   Se si seleziona LDAP, è possibile utilizzare il server LDAP specificato nella configurazione della directory oppure scegliere un server LDAP diverso da utilizzare per l&#39;autenticazione. Se si sceglie un server diverso, gli utenti devono esistere in entrambi i server LDAP.

1. Fornisci eventuali informazioni aggiuntive richieste sulla pagina. (Vedi [Impostazioni di autenticazione](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. Aggiungere una directory o una SPI (Service Provider Interface) personalizzata. (Vedi [Aggiunta di directory o SPI personalizzati](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis).)
1. Fare clic su Fine e quindi su OK.

Dopo aver creato un dominio enterprise, sincronizza manualmente la directory o crea un trigger per eseguire una sincronizzazione prima che la gestione utente possa utilizzarla. È quindi possibile impostare una pianificazione di sincronizzazione della directory ed eseguire la sincronizzazione manuale in base alle esigenze. (Vedi [Sincronizzazione delle directory](/help/forms/using/admin-help/synchronizing-directories.md#synchronizing-directories).)

## Aggiungi un dominio locale {#add-a-local-domain}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fare clic su Nuovo dominio locale.
1. Nella casella ID digitare un identificatore univoco per il dominio e nella casella Nome digitare un nome descrittivo per il dominio. (Vedi [Considerazioni importanti per i nomi di dominio e gli ID](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. Specificare se attivare il blocco dell&#39;account e quindi fare clic su OK. (Vedere [Configurare le impostazioni di blocco account](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings).) Per impostazione predefinita, l&#39;opzione Abilita blocco account è selezionata.

## Aggiungere un dominio ibrido {#add-a-hybrid-domain}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fai clic su Nuovo dominio ibrido.
1. Nella casella ID digitare un identificatore univoco per il dominio e nella casella Nome digitare un nome descrittivo per il dominio. (Vedi [Considerazioni importanti per i nomi di dominio e gli ID](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. Fare clic su Aggiungi autenticazione e, nell&#39;elenco Provider di autenticazione, selezionare un provider, a seconda del meccanismo di autenticazione utilizzato dall&#39;organizzazione. I valori possibili sono LDAP, Kerberos, SAML o un provider di autenticazione personalizzato.
1. Fornisci eventuali informazioni aggiuntive richieste sulla pagina. (Vedi [Impostazioni di autenticazione](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. Fare clic su OK e quindi di nuovo su OK.

## Considerazioni importanti per i nomi di dominio e gli ID {#important-considerations-for-domain-names-and-ids}

Quando scegli un nome di dominio e un ID, tieni presenti le seguenti considerazioni:

### Considerazioni generali {#general-considerations}

* Quando si utilizza un provider di database diverso da DB2, l&#39;ID dominio può contenere fino a 50 byte. Se si utilizzano caratteri ASCII a byte singolo, il limite è di 50 caratteri. Se l’identificatore del dominio contiene caratteri multibyte, questo limite viene ridotto. Ad esempio, se crei un dominio il cui identificatore contiene caratteri a 3 byte, il limite è di 16 caratteri. Inoltre, non è possibile creare domini che contengono caratteri a 4 byte. Se crei un ID dominio che supera questo limite, i moduli AEM saranno in uno stato instabile. Per ripristinare da questo stato instabile, vedere &quot; [Rimuovere un dominio contenente caratteri estesi o multibyte](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters)&quot; in questa pagina.
* Il numero di domini enterprise e domini locali che possono essere creati all’interno dei moduli AEM dipende dalla lunghezza di ciascuno degli ID di dominio. Quando si aggiunge un dominio enterprise o ibrido, Gestione utente aggiorna la stringa configInstance nel nodo AuthProviders del file di configurazione dei moduli AEM (config.xml). La stringa configInstance contiene un elenco separato da due punti dei percorsi assoluti di tutti i domini associati al provider di autorizzazione. Questa stringa ha una dimensione massima di 8192 caratteri. Una volta raggiunto tale limite, non puoi creare domini aggiuntivi.

### Considerazioni durante l&#39;utilizzo di DB2 {#considerations-when-using-db2}

Quando si utilizza DB2 per il database dei moduli AEM, la lunghezza massima consentita dell’ID dominio dipende dal tipo di caratteri utilizzati:

* 100 caratteri a byte singolo (ASCII), ad esempio caratteri utilizzati in inglese, francese o tedesco
* 50 caratteri a byte doppio, ad esempio caratteri utilizzati in cinese, giapponese o coreano
* 25 caratteri a quattro byte (ad esempio, caratteri utilizzati nella lingua cinese tradizionale)

### Considerazioni durante l&#39;utilizzo di MySQL {#considerations-when-using-mysql}

Quando si utilizza MySQL come database AEM forms, si applicano le seguenti limitazioni:

* Per l&#39;ID di dominio e il nome di dominio vengono utilizzati solo caratteri ASCII (Single-Byte). Se si utilizzano caratteri ASCII estesi, i moduli AEM saranno in uno stato instabile e potrebbero generare un&#39;eccezione se si tenta di eliminare il dominio. Per ripristinare da questo stato instabile, vedere l&#39;argomento &quot; [Rimuovi un dominio contenente caratteri estesi o multibyte](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters)&quot; in questa pagina.
* Non puoi creare due domini con lo stesso nome ma con lettere maiuscole e minuscole diverse. Se, ad esempio, si tenta di creare un dominio denominato *Adobe* quando esiste già un dominio denominato *adobe*, verrà generato un errore.
* User Management non è in grado di distinguere tra due nomi di dominio che differiscono solo per l’utilizzo di caratteri estesi. Ad esempio, se crei un dominio denominato *abcde* e un dominio denominato *âbcdè*, verranno considerati uguali.

### Rimuovere un dominio contenente caratteri estesi o multibyte {#remove-a-domain-that-contains-extended-or-multi-byte-characters}

1. Esportare il file di configurazione come descritto in [Importazione ed esportazione del file di configurazione](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).
1. Apri il file di configurazione e, sotto il nodo Domini, individua il nodo il cui attributo name corrisponde al nome del dominio creato con caratteri estesi o multibyte. Elimina l’intero nodo correlato a tale dominio.
1. Nel database, cercare il dominio nella tabella edcprincipaldomainentity:

   * Selezionare `*` da edcprincipaldomainentity.
   * Trovare il nome di dominio che contiene caratteri estesi o multibyte e impostarne lo stato su OBSOLETO.

1. Importare il file di configurazione aggiornato come descritto in [Importazione ed esportazione del file di configurazione](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).
