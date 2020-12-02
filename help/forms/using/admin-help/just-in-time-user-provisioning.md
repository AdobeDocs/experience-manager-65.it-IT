---
title: Provisioning degli utenti in tempo reale
seo-title: Provisioning degli utenti in tempo reale
description: Utilizzate il provisioning just-in-time per aggiungere utenti a Gestione utenti dopo l'autenticazione riuscita e assegnare in modo dinamico ruoli e gruppi rilevanti al nuovo utente.
seo-description: Utilizzate il provisioning just-in-time per aggiungere utenti a Gestione utenti dopo l'autenticazione riuscita e assegnare in modo dinamico ruoli e gruppi rilevanti al nuovo utente.
uuid: a5ad4698-70bb-487b-a069-7133e2f420c2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e80c3f98-baa1-45bc-b713-51a2eb5ec165
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 0%

---


# Provisioning dell&#39;utente in tempo reale {#just-in-time-user-provisioning}

AEM moduli supporta il provisioning temporaneo di utenti che non esistono ancora in Gestione utente. Con il provisioning &quot;in-time&quot;, gli utenti vengono automaticamente aggiunti a Gestione utente dopo che le loro credenziali sono state autenticate correttamente. Inoltre, i ruoli e i gruppi rilevanti vengono assegnati in modo dinamico al nuovo utente.

## Necessità di un provisioning semplice da parte dell&#39;utente {#need-for-just-in-time-user-provisioning}

Questo è il funzionamento dell&#39;autenticazione tradizionale:

1. Quando un utente tenta di accedere ai AEM moduli, Gestione utente passa le credenziali dell&#39;utente in sequenza a tutti i provider di autenticazione disponibili. (Le credenziali di accesso includono una combinazione nome utente/password, ticket Kerberos, firma PKCS7 e così via).
1. Il provider di autenticazione convalida le credenziali.
1. Il provider di autenticazione verifica quindi se l&#39;utente esiste nel database Gestione utente. Sono possibili i seguenti risultati:

   **Esiste:** se l&#39;utente è corrente e sbloccato, Gestione utente restituisce il successo dell&#39;autenticazione. Tuttavia, se l&#39;utente non è corrente o è bloccato, Gestione utente restituisce un errore di autenticazione.

   **Non esiste:** User Management restituisce un errore di autenticazione.

   **Non valido:** User Management restituisce un errore di autenticazione.

1. Il risultato restituito dal provider di autenticazione viene valutato. Se il provider di autenticazione ha restituito un esito positivo, l&#39;utente può effettuare l&#39;accesso. In caso contrario, Gestione utente verifica con il provider di autenticazione successivo (passaggi da 2 a 3).
1. L&#39;errore di autenticazione viene restituito se nessun provider di autenticazione disponibile convalida le credenziali utente.

Quando viene implementato il provisioning &quot;in-time&quot;, un nuovo utente viene creato in modo dinamico in Gestione utente se uno dei provider di autenticazione convalida le credenziali dell&#39;utente. (Dopo il passaggio 3 della procedura di autenticazione tradizionale, sopra).

## Implementare il provisioning dell&#39;utente &quot;just-in-time&quot; {#implement-just-in-time-user-provisioning}

### API per il provisioning in tempo reale {#apis-for-just-in-time-provisioning}

AEM moduli forniscono le seguenti API per il provisioning just-in-time:

```java
package com.adobe.idp.um.spi.authentication  ;
publ ic interface IdentityCreator {
/**
* Tries  to create a user with the  in formation  provided in the <code>UserProvisioningBO</code> object.
* If the user is successfully created, a valid AuthResponse is returned along with the information using which the user was created.
* It is the responsibility of the IdentityCreator to set the User obje ct  in the cre dential map with th e  ke y  <code>UMA u thenticationUtil.authenticatedUserKey</code>
* The credentials are available in the <code>UserProvisioningBO</code> object in the 'credentials' property.
* If the IdentityCreator is unable to create a user due to any reason, it returns <code>null</code>
* @param userBO An object of <code>com.adobe. i dp.um . spi.authenti c ationUserProvisioningBO</code>
* @return */public AuthResponse create(UserProvisioningBO userBO);
/**
* Returns the name of the IdentityCreator which will be registered in preferences.
* This name is used to associate the IdentityProvider with the Auth Provider Configuration in the domain.
* @return The name of the Identity Creator which is recognized in Configuration.
*/
public String getName();
}
package com.adobe.idp.um.spi.authentication;
import com.adobe.idp.um.api.infomodel.User;
public interface AssignmentProvider {
/**
* Tries to assign roles or permissions or group memberships to users created via Just-in-time provisioning.
* @param user The User created via the Just-in-time provisioning process.
* @return a Boolean flag indicating whether the assignment was successful or not.
*/
public Boolean assign(User user);
/**
* Returns the name of the AssignmentProvider through which it is registered under preferences.
* This name is used to associate the AssignmentProvider with the Auth Provider Configuration in the domain.
* @return The name of the AssignmentProvider which is recognized in Configuration.
*/public String getName();
}
```

### Considerazioni durante la creazione di un dominio abilitato nel tempo {#considerations-while-creating-a-just-in-time-enabled-domain}

* Durante la creazione di un `IdentityCreator` personalizzato per un dominio ibrido, accertatevi che per l&#39;utente locale sia specificata una password fittizia. Non lasciate vuoto questo campo password.
* Raccomandazione: Utilizzate `DomainSpecificAuthentication` per convalidare le credenziali utente rispetto a un dominio specifico.

### Crea un dominio abilitato solo nel tempo {#create-a-just-in-time-enabled-domain}

1. Scrivete un DSC che implementa le API nella sezione &quot;API per il provisioning just-in-time&quot;.
1. Implementare il DSC nel server dei moduli.
1. Crea un dominio abilitato solo nel tempo:

   * In Admin Console, fai clic su Settings (Impostazioni) > User Management (Gestione utente) > Domain Management (Gestione dominio) > New Enterprise Domain (Nuovo dominio Enterprise).
   * Configurate il dominio e selezionate Abilita solo provisioning in tempo. <!--Fix broken link (See Setting up and managing domains).-->
   * Aggiunta di provider di autenticazione. Durante l&#39;aggiunta di provider di autenticazione, nella schermata Nuova autenticazione, selezionate un creatore di identità registrato e un provider di assegnazione.

1. Salva il nuovo dominio.

## Dietro le quinte {#behind-the-scenes}

Si supponga che un utente stia tentando di accedere AEM moduli e che un provider di autenticazione accetti le credenziali utente. Se l&#39;utente non esiste ancora nel database Gestione utente, il controllo dell&#39;identità dell&#39;utente non riesce. AEM moduli ora esegue le azioni seguenti:

1. Creare un oggetto `UserProvisioningBO` con i dati di autenticazione e inserirlo in una mappa delle credenziali.
1. In base alle informazioni sul dominio restituite da `UserProvisioningBO`, recupera e richiama le `IdentityCreator` e `AssignmentProvider` registrate per il dominio.
1. Richiama `IdentityCreator`. Se restituisce un `AuthResponse` riuscito, estrarre `UserInfo` dalla mappa delle credenziali. Trasferitelo a `AssignmentProvider` per l&#39;assegnazione di gruppo/ruolo e qualsiasi altro post-elaborazione dopo la creazione dell&#39;utente.
1. Se l’utente è stato creato correttamente, restituite il tentativo di accesso da parte dell’utente come riuscito.
1. Per i domini ibridi, estraete le informazioni utente dai dati di autenticazione forniti al provider di autenticazione. Se queste informazioni vengono recuperate correttamente, create l’utente al volo.

>[!NOTE]
>
>La funzione di provisioning just-in-time viene fornita con un&#39;implementazione predefinita di `IdentityCreator` che potete utilizzare per creare gli utenti in modo dinamico. Gli utenti vengono creati con le informazioni associate alle directory del dominio.

