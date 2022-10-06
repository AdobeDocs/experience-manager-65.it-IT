---
title: Aggiunta di domini
seo-title: Adding domains
description: Scopri come aggiungere un dominio Enterprise, locale o ibrido utilizzando le impostazioni di Gestione dei domini e le considerazioni generali sui nomi di dominio e sugli ID.
seo-description: Learn how to add an enterprise, local, or hybrid domain using Domain Management settings and general considerations for domain names and IDs.
uuid: 3ae1e5d4-ea5b-4e0b-be97-3957c3702d5f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d4004ffe-c981-487d-b803-dc4492ae5998
exl-id: c708936d-7aa7-4b92-be2d-d97008f187d2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 0%

---

# Aggiunta di domini {#adding-domains}

## Aggiungi un dominio enterprise {#add-an-enterprise-domain}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fare clic su Nuovo dominio organizzazione.
1. Nella casella ID digitare un identificatore univoco per il dominio e nella casella Nome digitare un nome descrittivo per il dominio. (Vedi [Considerazioni importanti sui nomi di dominio e sugli ID](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. Specifica se abilitare il blocco dell&#39;account. (Vedi [Configurare le impostazioni di blocco dell’account](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings).) Per impostazione predefinita, l’opzione Abilita blocco account è selezionata.
1. Fare clic su Aggiungi autenticazione e, nell&#39;elenco Provider di autenticazione, selezionare un provider, a seconda del meccanismo di autenticazione utilizzato dall&#39;organizzazione. I valori possibili sono LDAP, Kerberos, SAML o un provider di autenticazione personalizzato.

   Se si seleziona LDAP, è possibile utilizzare il server LDAP specificato nella configurazione della directory, oppure è possibile scegliere un server LDAP diverso da utilizzare per l&#39;autenticazione. Se scegli un server diverso, gli utenti devono esistere su entrambi i server LDAP.

1. Fornisci eventuali informazioni aggiuntive richieste sulla pagina. (Vedi [Impostazioni di autenticazione](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. Aggiungi una directory o un&#39;interfaccia SPI (Service Provider Interface) personalizzata. (Vedi [Aggiunta di directory o SPI personalizzati](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis).)
1. Fare clic su Fine, quindi su OK.

Dopo aver creato un dominio enterprise, sincronizza manualmente la directory o crea un trigger per eseguire una sincronizzazione prima che Gestione utente possa utilizzarla. È quindi possibile impostare una pianificazione della sincronizzazione della directory ed eseguire la sincronizzazione manuale come necessario. (Vedi [Sincronizzazione delle directory](/help/forms/using/admin-help/synchronizing-directories.md#synchronizing-directories).)

## Aggiungi un dominio locale {#add-a-local-domain}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fare clic su Nuovo dominio locale.
1. Nella casella ID digitare un identificatore univoco per il dominio e digitare un nome descrittivo per il dominio nella casella Nome. (Vedi [Considerazioni importanti sui nomi di dominio e sugli ID](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. Specificare se abilitare il blocco dell&#39;account e quindi fare clic su OK. (Vedi [Configurare le impostazioni di blocco dell’account](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings).) Per impostazione predefinita, l’opzione Abilita blocco account è selezionata.

## Aggiungi un dominio ibrido {#add-a-hybrid-domain}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fare clic su Nuovo dominio ibrido.
1. Nella casella ID digitare un identificatore univoco per il dominio e digitare un nome descrittivo per il dominio nella casella Nome. (Vedi [Considerazioni importanti sui nomi di dominio e sugli ID](adding-domains.md#important-considerations-for-domain-names-and-ids).)
1. Fare clic su Aggiungi autenticazione e, nell&#39;elenco Provider di autenticazione, selezionare un provider, a seconda del meccanismo di autenticazione utilizzato dall&#39;organizzazione. I valori possibili sono LDAP, Kerberos, SAML o un provider di autenticazione personalizzato.
1. Fornisci eventuali informazioni aggiuntive richieste sulla pagina. (Vedi [Impostazioni di autenticazione](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. Fare clic su OK, quindi di nuovo su OK.

## Considerazioni importanti sui nomi di dominio e sugli ID {#important-considerations-for-domain-names-and-ids}

Quando scegli un nome di dominio e un ID, considera quanto segue:

### Considerazioni generali {#general-considerations}

* Quando utilizzi un provider di database diverso da DB2, l&#39;ID dominio può contenere fino a 50 byte. Se si utilizzano caratteri ASCII a byte singolo, il limite è di 50 caratteri. Se l’identificatore del dominio contiene caratteri multibyte, questo limite viene ridotto. Ad esempio, se crei un dominio il cui identificatore contiene caratteri a 3 byte, il limite è di 16 caratteri. Inoltre, non puoi creare domini che contengono caratteri a 4 byte. Se crei un ID di dominio che supera questo limite, AEM moduli si troveranno in uno stato instabile. Per recuperare da questo stato instabile, vedi &quot; [Rimuovere un dominio contenente caratteri estesi o multibyte](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters)&quot; in questa pagina.
* Il numero di domini Enterprise e di domini locali che possono essere creati all’interno AEM moduli dipende dalla lunghezza di ciascuno degli ID di dominio. Quando si aggiunge un dominio Enterprise o ibrido, Gestione utente aggiorna la stringa configInstance nel nodo AuthProviders del file di configurazione dei moduli AEM (config.xml). La stringa configInstance contiene un elenco separato da due punti dei percorsi assoluti di tutti i domini associati al provider di autorizzazione. Questa stringa ha un limite di dimensione di 8192 caratteri. Una volta raggiunto tale limite, non puoi creare altri domini.

### Considerazioni sull&#39;utilizzo di DB2 {#considerations-when-using-db2}

Quando si utilizza DB2 per il database dei moduli AEM, la lunghezza massima consentita dell’ID dominio dipende dal tipo di caratteri utilizzati:

* 100 byte singolo (ASCII) (ad esempio, caratteri utilizzati nelle lingue inglese, francese o tedesca)
* 50 byte doppio (ad esempio, caratteri utilizzati nelle lingue cinese, giapponese o coreana)
* 25 a quattro byte (ad esempio, caratteri utilizzati nella lingua cinese tradizionale)

### Considerazioni sull&#39;utilizzo di MySQL {#considerations-when-using-mysql}

Quando si utilizza MySQL come database di moduli AEM, si applicano le seguenti limitazioni:

* Utilizza solo caratteri a byte singolo (ASCII) per l’ID di dominio e il nome di dominio. Se si utilizzano caratteri ASCII estesi, AEM moduli si troveranno in uno stato instabile e potrebbe generare un&#39;eccezione se si tenta di eliminare il dominio. Per recuperare da questo stato instabile, vedi &quot; [Rimuovere un dominio contenente caratteri estesi o multibyte](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters)&quot; argomento in questa pagina.
* Non puoi creare due domini con lo stesso nome ma con maiuscole e minuscole diverse. Ad esempio, durante il tentativo di creazione di un dominio denominato *Adobe* quando un dominio denominato *adobe* causa un errore già esistente.
* Gestione utente non è in grado di distinguere tra due nomi di dominio che differiscono solo nell&#39;uso di caratteri estesi. Ad esempio, se crei un dominio denominato *basso* e un dominio denominato *âbcdè*, sono considerate uguali.

### Rimuovere un dominio contenente caratteri estesi o multibyte {#remove-a-domain-that-contains-extended-or-multi-byte-characters}

1. Esporta il file di configurazione come descritto in [Importazione ed esportazione del file di configurazione](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).
1. Apri il file di configurazione e sotto il nodo Domini individua il nodo il cui attributo di nome corrisponde al nome del dominio creato con caratteri estesi o multibyte. Elimina l&#39;intero nodo correlato a quel dominio.
1. Nel database, cerca il dominio nella tabella edcprincipaldomainentity :

   * Seleziona `*` da edcprincipaldomainentity.
   * Trovare il nome di dominio che contiene caratteri estesi o multibyte e impostarne lo stato su OBSOLETE.

1. Importa il file di configurazione aggiornato, come descritto in [Importazione ed esportazione del file di configurazione](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).
