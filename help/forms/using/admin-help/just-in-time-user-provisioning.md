---
title: Provisioning utente just-in-time
description: Utilizza il provisioning just-in-time per aggiungere utenti alla Gestione utenti dopo la corretta autenticazione e assegnare dinamicamente ruoli e gruppi rilevanti al nuovo utente.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7bde0a09-192a-44a8-83d0-c18e335e9afa
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '575'
ht-degree: 100%

---

# Provisioning utente just-in-time {#just-in-time-user-provisioning}

AEM Forms supporta il provisioning just-in-time degli utenti che non esistono ancora in Gestione utenti. Con il provisioning just-in-time, gli utenti vengono aggiunti automaticamente alla Gestione utenti dopo la corretta autenticazione delle credenziali. Inoltre, i ruoli e i gruppi rilevanti vengono assegnati in modo dinamico al nuovo utente.

## Necessità di provisioning utente just-in-time {#need-for-just-in-time-user-provisioning}

L’autenticazione tradizionale funziona in questo modo:

1. Quando un utente tenta di accedere ad AEM Forms, gestione utenti passa le credenziali dell’utente in sequenza a tutti i provider di autenticazione disponibili. Le credenziali di accesso includono una combinazione nome utente/password, un ticket Kerberos, una firma PKCS7 e così via.
1. Il provider di autenticazione convalida le credenziali.
1. Il provider di autenticazione verifica quindi se l’utente esiste nel database della Gestione utenti. Sono possibili i seguenti risultati:

   **Esiste:** se l’utente è corrente e sbloccato, gestione utenti restituirà l’autenticazione completata. Tuttavia, se l’utente non è attuale o è bloccato, Gestione utenti restituisce un errore di autenticazione.

   **Non esiste:** gestione utenti restituisce un errore di autenticazione.

   **Non valido:** gestione utenti restituisce un errore di autenticazione.

1. Viene valutato il risultato restituito dal provider di autenticazione. Se il provider di autenticazione ha restituito l’autenticazione, l’utente può accedere. In caso contrario, Gestione utente controlla con il provider di autenticazione successivo (passaggi 2-3).
1. Se nessun provider di autenticazione disponibile convalida le credenziali utente, viene restituito un errore di autenticazione.

Quando implementi il provisioning just-in-time, viene creato dinamicamente un nuovo utente in gestione utenti se uno dei provider di autenticazione convalida le credenziali dell’utente. Dopo il passaggio 3 nella procedura di autenticazione tradizionale precedente.

## Implementare il provisioning utente just-in-time {#implement-just-in-time-user-provisioning}

### API per il provisioning just-in-time {#apis-for-just-in-time-provisioning}

AEM Forms fornisce le seguenti API per il provisioning just-in-time:

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

### Considerazioni durante la creazione di un dominio con abilitazione just-in-time {#considerations-while-creating-a-just-in-time-enabled-domain}

* Durante la creazione di un `IdentityCreator` personalizzato per un dominio ibrido, verifica che sia specificata una password fittizia per l’utente locale. Non lasciare vuoto il campo password.
* Consiglio: utilizza `DomainSpecificAuthentication` per convalidare le credenziali utente rispetto a un dominio specifico.

### Creare un dominio con abilitazione just-in-time {#create-a-just-in-time-enabled-domain}

1. Scrivi un DSC che implementa le API nella sezione “API per il provisioning just-in-time”.
1. Distribuisci DSC nel server Forms.
1. Creare un dominio con abilitazione just-in-time:

   * Nella console di amministrazione, fai clic su Impostazioni > Gestione utenti > Gestione domini > Nuovo dominio Enterprise.
   * Configura il dominio e seleziona Abilita provisioning just-in-time. <!--Fix broken link (See Setting up and managing domains).-->
   * Aggiungi provider di autenticazione. Durante l’aggiunta dei provider di autenticazione, nella schermata Nuova autenticazione, seleziona un creatore di identità e un provider di assegnazione registrati.

1. Salva il nuovo dominio.

## Dietro le quinte {#behind-the-scenes}

Supponiamo che un utente stia tentando di accedere ad AEM Forms e che un provider di autenticazione accetti le credenziali utente. Se l’utente non esiste ancora nel database di gestione utenti, il controllo dell’identità dell’utente non riesce. AEM Forms ora esegue queste azioni:

1. Crea un oggetto `UserProvisioningBO` con i dati di autenticazione e lo inserisce in una mappa delle credenziali.
1. In base alle informazioni sul dominio restituite da `UserProvisioningBO`, recupera e richiama `IdentityCreator` e `AssignmentProvider` registrati per il dominio.
1. Richiama `IdentityCreator`. Se restituisce un `AuthResponse` corretto, estrae `UserInfo` dalla mappa delle credenziali. Lo trascerisce a `AssignmentProvider` per l’assegnazione gruppo/ruolo e qualsiasi altra post-elaborazione dopo la creazione dell’utente.
1. Se l&#39;utente è stato creato correttamente, restituisce come operazione riuscita il tentativo di accesso dell’utente.
1. Per i domini ibridi, richiama le informazioni utente dai dati di autenticazione forniti al provider di autenticazione. Se queste informazioni vengono recuperate correttamente, crea l’utente immediatamente..

>[!NOTE]
>
>La funzionalità di provisioning just-in-time viene fornita con un’implementazione predefinita di `IdentityCreator` che è possibile utilizzare per creare gli utenti in modo dinamico. Gli utenti vengono creati con le informazioni associate alle directory nel dominio.
