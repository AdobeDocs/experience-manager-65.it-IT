---
title: Aggiunta di domini
seo-title: Aggiunta di domini
description: Scopri come aggiungere un dominio Enterprise, locale o ibrido utilizzando le impostazioni di Gestione dominio e considerazioni generali per i nomi di dominio e gli ID.
seo-description: Scopri come aggiungere un dominio Enterprise, locale o ibrido utilizzando le impostazioni di Gestione dominio e considerazioni generali per i nomi di dominio e gli ID.
uuid: 3ae1e5d4-ea5b-4e0b-be97-3957c3702d5f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d4004ffe-c981-487d-b803-dc4492ae5998
translation-type: tm+mt
source-git-commit: d3719a9ce2fbb066f99445475af8e1f1e7476f4e
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 0%

---


# Aggiunta di domini {#adding-domains}

## Aggiungere un dominio Enterprise {#add-an-enterprise-domain}

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fate clic su Nuovo dominio Enterprise.
1. Nella casella ID, digitate un identificatore univoco per il dominio e digitate nella casella Nome un nome descrittivo per il dominio. (Vedere [Considerazioni importanti per i nomi di dominio e gli ID](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. Specificate se abilitare il blocco dell&#39;account. (Vedere [Configurare le impostazioni di blocco dell&#39;account](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings).) Per impostazione predefinita, Abilita blocco account è selezionato.
1. Fate clic su Aggiungi autenticazione e, nell&#39;elenco Provider autenticazione, selezionate un provider, a seconda del meccanismo di autenticazione utilizzato dall&#39;organizzazione. I valori possibili sono LDAP, Kerberos, SAML o un provider di autenticazione personalizzato.

   Se selezionate LDAP, potete usare il server LDAP specificato nella configurazione di directory oppure scegliere un altro server LDAP da usare per l’autenticazione. Se scegliete un server diverso, gli utenti devono esistere su entrambi i server LDAP.

1. Fornite eventuali informazioni aggiuntive richieste sulla pagina. (Vedere [Impostazioni di autenticazione](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. Aggiungere una directory o un&#39;interfaccia SPI (Service Provider Interface) personalizzata. (Vedere [Aggiunta di directory o SPI](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis) personalizzati.)
1. Fare clic su Fine, quindi su OK.

Dopo aver creato un dominio Enterprise, sincronizzate manualmente la directory o create un trigger per eseguire una sincronizzazione prima che Gestione utente possa utilizzarla. Potete quindi impostare una pianificazione della sincronizzazione delle directory ed eseguire la sincronizzazione manuale come necessario. (Vedere [Sincronizzazione delle directory](/help/forms/using/admin-help/synchronizing-directories.md#synchronizing-directories).)

## Aggiungere un dominio locale {#add-a-local-domain}

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fare clic su Nuovo dominio locale.
1. Nella casella ID, digitate un identificatore univoco per il dominio e, nella casella Nome, digitate un nome descrittivo per il dominio. (Vedere [Considerazioni importanti per i nomi di dominio e gli ID](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. Specificate se abilitare il blocco dell&#39;account e fate clic su OK. (Vedere [Configurare le impostazioni di blocco dell&#39;account](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings).) Per impostazione predefinita, Abilita blocco account è selezionato.

## Aggiungi un dominio ibrido {#add-a-hybrid-domain}

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fate clic su Nuovo dominio ibrido.
1. Nella casella ID, digitate un identificatore univoco per il dominio e, nella casella Nome, digitate un nome descrittivo per il dominio. (Vedere [Considerazioni importanti per i nomi di dominio e gli ID](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. Fate clic su Aggiungi autenticazione e, nell&#39;elenco Provider autenticazione, selezionate un provider, a seconda del meccanismo di autenticazione utilizzato dall&#39;organizzazione. I valori possibili sono LDAP, Kerberos, SAML o un provider di autenticazione personalizzato.
1. Fornite eventuali informazioni aggiuntive richieste sulla pagina. (Vedere [Impostazioni di autenticazione](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. Fate clic su OK, quindi di nuovo su OK.

## Considerazioni importanti per i nomi di dominio e gli ID {#important-considerations-for-domain-names-and-ids}

Quando scegli un nome di dominio e un ID, tieni presente le considerazioni seguenti:

### Considerazioni generali {#general-considerations}

* Se si utilizza un provider di database diverso da DB2, l&#39;ID di dominio può contenere fino a 50 byte. Se si utilizzano caratteri ASCII a byte singolo, il limite è di 50 caratteri. Se l’identificatore di dominio contiene caratteri multibyte, questo limite viene ridotto. Ad esempio, se create un dominio il cui identificatore contiene 3 caratteri byte, il limite è di 16 caratteri. Inoltre, non è possibile creare domini che contengono caratteri a 4 byte. Se si crea un ID di dominio che supera questo limite, AEM moduli si troveranno in uno stato instabile. Per recuperare da questo stato instabile, vedere &quot; [Rimuovere un dominio che contiene caratteri estesi o multibyte](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters)&quot; in questa pagina.
* Il numero di domini enterprise e di domini locali che è possibile creare all&#39;interno AEM moduli dipende dalla lunghezza di ciascun ID di dominio. Quando si aggiunge un dominio Enterprise o ibrido, Gestione utente aggiorna la stringa configInstance nel nodo AuthProviders del file di configurazione dei moduli AEM (config.xml). La stringa configInstance contiene un elenco separato da due punti dei percorsi assoluti di tutti i domini associati al provider di autorizzazione. Questa stringa ha un limite di dimensione di 8192 caratteri. Una volta raggiunto tale limite, non è possibile creare altri domini.

### Considerazioni per l&#39;utilizzo di DB2 {#considerations-when-using-db2}

Quando si utilizza DB2 per il database dei moduli AEM, la lunghezza massima consentita per l&#39;ID di dominio dipende dal tipo di caratteri utilizzati:

* 100 byte singolo (ASCII) (ad esempio, caratteri utilizzati nelle lingue inglese, francese o tedesco)
* 50 a doppio byte (ad esempio, caratteri utilizzati nelle lingue cinese, giapponese o coreana)
* 25 a quattro byte (ad esempio, caratteri utilizzati nella lingua cinese tradizionale)

### Considerazioni sull&#39;utilizzo di MySQL {#considerations-when-using-mysql}

Quando si utilizza MySQL come database di moduli AEM, si applicano le seguenti limitazioni:

* Utilizzate solo caratteri a byte singolo (ASCII) per l&#39;ID di dominio e il nome di dominio. Se si utilizzano caratteri ASCII estesi, AEM moduli si troveranno in uno stato instabile e potrebbe generare un&#39;eccezione se si tenta di eliminare il dominio. Per recuperare da questo stato instabile, vedere l&#39;argomento &quot; [Rimuovere un dominio che contiene caratteri estesi o multibyte](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters)&quot; in questa pagina.
* Non è possibile creare due domini con lo stesso nome ma con maiuscole e minuscole diverse. Ad esempio, se si tenta di creare un dominio denominato *Adobe* quando esiste già un dominio denominato *adobe*, si verifica un errore.
* Gestione utente non può distinguere tra due nomi di dominio che differiscono solo per l&#39;uso di caratteri estesi. Ad esempio, se si crea un dominio denominato *abcde* e un dominio denominato *âbcdè*, questi vengono considerati uguali.

### Rimuovere un dominio che contiene caratteri estesi o multibyte {#remove-a-domain-that-contains-extended-or-multi-byte-characters}

1. Esportate il file di configurazione come descritto in [Importazione ed esportazione del file di configurazione](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).
1. Apri il file di configurazione e sotto il nodo Domains, individua il nodo il cui attributo nome corrisponde al nome del dominio creato con caratteri estesi o multibyte. Elimina l’intero nodo correlato a tale dominio.
1. Nel database, cercate il dominio nella tabella edcprincipaldomainentity:

   * Selezionare `*` da edcprincipaldomainentity.
   * Trovate il nome di dominio che contiene caratteri estesi o multibyte e impostatene lo stato su OBSOLETE.

1. Importare il file di configurazione aggiornato, come descritto in [Importazione ed esportazione del file di configurazione](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).

