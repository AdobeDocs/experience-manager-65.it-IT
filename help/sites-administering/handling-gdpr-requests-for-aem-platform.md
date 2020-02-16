---
title: Gestione delle richieste GDPR per AEM Foundation
seo-title: Gestione delle richieste GDPR per AEM Foundation
description: 'null'
seo-description: 'null'
uuid: d470061c-bbcf-4d86-9ce3-6f24a764ca39
contentOwner: sarchiz
discoiquuid: 8ee843b6-8cea-45fc-be6c-99c043f075d4
translation-type: tm+mt
source-git-commit: 85a3dac5db940b81da9e74902a6aa475ec8f1780

---


# Gestione delle richieste GDPR per AEM Foundation{#handling-gdpr-requests-for-the-aem-foundation}

>[!IMPORTANT]
>
>Il GDPR è utilizzato come esempio nelle sezioni seguenti, ma i dettagli trattati sono applicabili a tutte le normative sulla protezione dei dati e sulla privacy; come GDPR, CCPA ecc.

## Supporto GDPR di AEM Foundation {#aem-foundation-gdpr-support}

A livello di AEM Foundation, i Dati personali memorizzati sono il Profilo utente. Di conseguenza, le informazioni contenute in questo articolo riguardano principalmente come accedere e eliminare i profili utente, rispettivamente per soddisfare le richieste di accesso e eliminazione del GDPR.

## Accesso a un profilo utente {#accessing-a-user-profile}

### Passaggi manuali {#manual-steps}

1. Aprite la console Amministrazione utente, accedendo a **[!UICONTROL Impostazioni - Protezione - Utenti]** o sfogliando direttamente `https://<serveraddress>:<serverport>/libs/granite/security/content/useradmin.html`

   ![useradmin2](assets/useradmin2.png)

1. Quindi, cercate l’utente in questione digitando il nome nella barra di ricerca nella parte superiore della pagina:

   ![usersearch](assets/usersearch.png)

1. Infine, aprite il profilo utente facendo clic su di esso, quindi selezionate nella scheda **[!UICONTROL Dettagli]** .

   ![userprofile_small](assets/userprofile_small.png)

### API HTTP {#http-api}

Come già detto, Adobe fornisce API per l&#39;accesso ai dati utente, al fine di facilitare l&#39;automazione. Esistono diversi tipi di API che potete utilizzare:

**API UserProperties**

```shell
curl -u user:password http://localhost:4502/libs/granite/security/search/profile.userproperties.json\?authId\=cavery
```

**API Sling**

*Individuazione della home page dell&#39;utente:*

```xml
curl -g -u user:password 'http://localhost:4502/libs/granite/security/search/authorizables.json?query={"condition":[{"named":"cavery"}]}'
     {"authorizables":[{"type":"user","authorizableId_xss":"cavery","authorizableId":"cavery","name_xss":"Carlene Avery","name":"Carlene Avery","home":"/home/users/we-retail/DSCP-athB1NYLBXvdTuN"}],"total":1}
```

*Recupero dei dati utente*

Utilizzando il percorso del nodo dalla proprietà home del payload JSON restituito dal comando precedente:

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile.-1.json'
```

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profiles.-1.json'
```

## Disattivazione di un utente ed eliminazione dei profili associati {#disabling-a-user-and-deleting-the-associated-profiles}

### Disattiva utente {#disable-user}

1. Aprite la console Amministrazione utente ed effettuate la ricerca dell’utente in questione, come descritto sopra.
1. Passate il puntatore del mouse sull’utente e fate clic sull’icona di selezione. Il profilo diventa grigio e indica che è selezionato.

1. Premere il pulsante Disattiva nel menu superiore per disattivare l&#39;utente:

   ![userdisable](assets/userdisable.png)

1. Infine, confermate l’azione:

   ![image2018-2-6_1-40-58](assets/image2018-2-6_1-40-58.png)

   L&#39;interfaccia utente indica quindi che l&#39;utente è stato disattivato in grigio e aggiunge un blocco alla scheda del profilo:

   ![disableuser](assets/disableduser.png)

### Elimina informazioni profilo utente {#delete-user-profile-information}

1. Accedete a CRXDE Lite, quindi cercate `[!UICONTROL userId]`:

   ![image2018-2-6_1-57-11](assets/image2018-2-6_1-57-11.png)

1. Apri il nodo utente in cui si trova per impostazione `[!UICONTROL /home/users]` predefinita:

   ![image2018-2-6_1-58-25](assets/image2018-2-6_1-58-25.png)

1. Eliminare i nodi del profilo e tutti i relativi elementi figlio. Esistono due formati per i nodi del profilo, a seconda della versione di AEM:

   1. Il profilo privato predefinito in `[!UICONTROL /profile]`
   1. `[!UICONTROL /profiles]`, per i nuovi profili creati con AEM 6.5.
   ![image2018-2-6_2-0-4](assets/image2018-2-6_2-0-4.png)

### API HTTP {#http-api-1}

Le procedure seguenti utilizzano lo strumento della riga di `curl` comando per illustrare come disabilitare l&#39;utente con la **[!UICONTROL caverna]** `userId` ed eliminare i profili disponibili nel percorso predefinito.

* *Individuazione della home page dell&#39;utente*

```shell
curl -g -u user:password 'http://localhost:4502/libs/granite/security/search/authorizables.json?query={"condition":[{"named":"cavery"}]}'
     {"authorizables":[{"type":"user","authorizableId_xss":"cavery","authorizableId":"cavery","name_xss":"Carlene Avery","name":"Carlene Avery","home":"/home/users/we-retail/DSCP-athB1NYLBXvdTuN"}],"total":1}
```

* *Disattivazione dell&#39;utente*

Utilizzando il percorso del nodo dalla proprietà home del payload JSON restituito dal comando precedente:

```shell
curl -X POST -u user:password -FdisableUser="describe the reasons for disabling this user (GDPR in this case)" 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN.rw.userprops.html'
```

* *Eliminazione dei profili utente*

Utilizzando il percorso del nodo dalla proprietà home del payload JSON restituito dal comando di individuazione dell&#39;account e dalle posizioni note del nodo del profilo casella:

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```

