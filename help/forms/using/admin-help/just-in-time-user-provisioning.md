---
title: Provisioning puntuale degli utenti
seo-title: Just-in-time user provisioning
description: Utilizza il provisioning just-in-time per aggiungere utenti a Gestione utenti dopo l’autenticazione corretta e assegnare in modo dinamico ruoli e gruppi rilevanti al nuovo utente.
seo-description: Use just-in-time provisioning to add users to User Management after successfull authentication and dynamically assign relevant roles and groups to the new user.
uuid: a5ad4698-70bb-487b-a069-7133e2f420c2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e80c3f98-baa1-45bc-b713-51a2eb5ec165
exl-id: 7bde0a09-192a-44a8-83d0-c18e335e9afa
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# Provisioning puntuale degli utenti {#just-in-time-user-provisioning}

I moduli AEM supportano il provisioning in tempo reale di utenti che non esistono ancora in Gestione utente. Con il provisioning in tempo reale, gli utenti vengono aggiunti automaticamente a Gestione utente dopo che le loro credenziali sono state autenticate correttamente. Inoltre, i ruoli e i gruppi rilevanti vengono assegnati in modo dinamico al nuovo utente.

## Necessità di provisioning degli utenti in tempo reale {#need-for-just-in-time-user-provisioning}

L’autenticazione tradizionale funziona in questo modo:

1. Quando un utente tenta di accedere AEM moduli, Gestione utente trasmette le credenziali dell’utente in sequenza a tutti i provider di autenticazione disponibili. (Le credenziali di accesso includono una combinazione nome utente/password, ticket Kerberos, firma PKCS7 e così via.)
1. Il provider di autenticazione convalida le credenziali.
1. Il provider di autenticazione controlla quindi se l&#39;utente esiste nel database User Management. Sono possibili i seguenti risultati:

   **Esiste:** Se l&#39;utente è corrente e sbloccato, Gestione utente restituisce l&#39;autenticazione riuscita. Tuttavia, se l&#39;utente non è corrente o è bloccato, Gestione utente restituisce un errore di autenticazione.

   **Non esiste:** Gestione utente restituisce un errore di autenticazione.

   **Non valido:** Gestione utente restituisce un errore di autenticazione.

1. Viene valutato il risultato restituito dal provider di autenticazione. Se il provider di autenticazione ha restituito l&#39;autenticazione, l&#39;utente può effettuare l&#39;accesso. In caso contrario, User Management controlla con il provider di autenticazione successivo (passaggi 2-3).
1. Se le credenziali utente non vengono convalidate da alcun provider di autenticazione disponibile, viene restituito un errore di autenticazione.

Quando si implementa il provisioning in tempo reale, un nuovo utente viene creato dinamicamente in Gestione utente se uno dei provider di autenticazione convalida le credenziali dell’utente. (Dopo il passaggio 3 nella procedura di autenticazione tradizionale, sopra.)

## Implementare il provisioning degli utenti in tempo reale {#implement-just-in-time-user-provisioning}

### API per il provisioning just-in-time {#apis-for-just-in-time-provisioning}

AEM forms fornisce le seguenti API per il provisioning in tempo reale:

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

### Considerazioni durante la creazione di un dominio abilitato solo nel tempo {#considerations-while-creating-a-just-in-time-enabled-domain}

* Durante la creazione di un `IdentityCreator` per un dominio ibrido, assicurati che per l’utente locale sia specificata una password fittizia. Non lasciare vuoto questo campo password.
* Raccomandazione: Utilizzo `DomainSpecificAuthentication` per convalidare le credenziali utente rispetto a un dominio specifico.

### Creare un dominio abilitato nel tempo {#create-a-just-in-time-enabled-domain}

1. Scrivi un DSC che implementa le API nella sezione &quot;API per il provisioning just-in-time&quot;.
1. Distribuire il DSC nel server dei moduli.
1. Crea un dominio abilitato per il momento:

   * In Admin Console, fai clic su Impostazioni > Gestione utente > Gestione dominio > Nuovo dominio Enterprise.
   * Configura il dominio e seleziona Abilita provisioning in tempo. <!--Fix broken link (See Setting up and managing domains).-->
   * Aggiungi provider di autenticazione. Durante l’aggiunta di provider di autenticazione, nella schermata Nuova autenticazione , seleziona un creatore di identità registrato e un fornitore di assegnazione.

1. Salva il nuovo dominio.

## Dietro le quinte {#behind-the-scenes}

Supponiamo che un utente stia tentando di accedere a AEM moduli e che un provider di autenticazione accetti le credenziali utente. Se l&#39;utente non esiste ancora nel database di Gestione utente, il controllo di identità dell&#39;utente non riesce. AEM Forms esegue ora le azioni seguenti:

1. Crea un `UserProvisioningBO` con i dati di autenticazione e inserirli in una mappa delle credenziali.
1. In base alle informazioni di dominio restituite da `UserProvisioningBO`, recupera e richiama il `IdentityCreator` e `AssignmentProvider` per il dominio .
1. Richiama `IdentityCreator`. Se restituisce un risultato positivo `AuthResponse`estratto `UserInfo` dalla mappa delle credenziali. Passa a `AssignmentProvider` per l’assegnazione di gruppi/ruoli e qualsiasi altro post-elaborazione dopo la creazione dell’utente.
1. Se l&#39;utente viene creato correttamente, il tentativo di accesso dell&#39;utente viene restituito come riuscito.
1. Per i domini ibridi, estrai le informazioni utente dai dati di autenticazione forniti al provider di autenticazione. Se queste informazioni vengono recuperate correttamente, crea l’utente on-the-fly.

>[!NOTE]
>
>La funzionalità di provisioning just-in-time viene fornita con un&#39;implementazione predefinita di `IdentityCreator` che puoi utilizzare per creare utenti in modo dinamico. Gli utenti vengono creati con le informazioni associate alle directory nel dominio .
