---
title: Gestione delle richieste RGPD per Adobe Experience Manager Foundation
description: Gestione delle richieste RGPD per Adobe Experience Manager Foundation
contentOwner: sarchiz
exl-id: 411d40ab-6be8-4658-87f6-74d2ac1a4913
source-git-commit: 96e2e945012046e6eac878389b7332985221204e
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 43%

---

# Gestione delle richieste RGPD per Adobe Experience Manager (AEM) Foundation{#handling-gdpr-requests-for-the-aem-foundation}

>[!IMPORTANT]
>
>Il RGPD è utilizzato come esempio nelle sezioni seguenti, ma i dettagli coperti sono applicabili a tutte le normative su privacy e protezione dei dati, come RGPD, CCPA, ecc.

## Supporto per il RGPD di AEM Foundation {#aem-foundation-gdpr-support}

A livello di AEM Foundation, i dati personali memorizzati sono il profilo utente. Pertanto, le informazioni contenute in questo articolo riguardano principalmente come accedere ed eliminare i profili utente, rispettivamente per soddisfare le richieste di accesso al RGPD e di cancellazione.

## Accesso a un profilo utente {#accessing-a-user-profile}

### Passaggi manuali {#manual-steps}

1. Apri la console User Administration (Amministrazione utenti) navigando su **[!UICONTROL Impostazioni - Protezione - Utenti]** o navigando direttamente in `https://<serveraddress>:<serverport>/libs/granite/security/content/useradmin.html`

   ![useradmin2](assets/useradmin2.png)

1. Quindi, cerca l’utente in questione digitando il nome nella barra di ricerca nella parte superiore della pagina:

   ![usersearch](assets/usersearch.png)

1. Infine, apri il profilo utente facendo clic su di esso, quindi seleziona la scheda **[!UICONTROL Dettagli]**.

   ![userprofile_small](assets/userprofile_small.png)

### API HTTP {#http-api}

Come accennato, Adobe fornisce API per accedere ai dati utente, per facilitare l’automazione. Esistono diversi tipi di API che puoi utilizzare:

**API UserProperties**

```shell
curl -u user:password http://localhost:4502/libs/granite/security/search/profile.userproperties.json\?authId\=cavery
```

**API Sling**

*Individuazione della home utente:*

```xml
curl -g -u user:password 'http://localhost:4502/libs/granite/security/search/authorizables.json?query={"condition":[{"named":"cavery"}]}'
     {"authorizables":[{"type":"user","authorizableId_xss":"cavery","authorizableId":"cavery","name_xss":"Carlene Avery","name":"Carlene Avery","home":"/home/users/we-retail/DSCP-athB1NYLBXvdTuN"}],"total":1}
```

*Recupero dati utente*

Utilizzo del percorso del nodo dalla proprietà home del payload JSON restituito dal comando precedente:

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile.-1.json'
```

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profiles.-1.json'
```

## Disabilitazione di un utente ed eliminazione dei profili associati {#disabling-a-user-and-deleting-the-associated-profiles}

### Disattiva utente {#disable-user}

1. Apri la console User Administration e cerca l’utente in questione, come descritto sopra.
1. Passa il puntatore del mouse sull’utente e fai clic sull’icona di selezione. Il profilo diventa grigio e indica che è selezionato.

1. Premi il pulsante Disattiva nel menu superiore per disabilitare l’utente:

   ![userdisable](assets/userdisable.png)

1. Infine, conferma l’azione:

   ![image2018-2-6_1-40-58](assets/image2018-2-6_1-40-58.png)

   L’interfaccia utente indica che l’utente è disattivato togliendo il grigio e aggiungendo un blocco alla scheda del profilo:

   ![disableduser](assets/disableduser.png)

### Eliminare informazioni sul profilo utente {#delete-user-profile-information}

1. Accedi a CRXDE Lite, quindi cerca il `[!UICONTROL userId]`:

   ![image2018-2-6_1-57-11](assets/image2018-2-6_1-57-11.png)

1. Apri il nodo utente che si trova in `[!UICONTROL /home/users]` per impostazione predefinita:

   ![image2018-2-6_1-58-25](assets/image2018-2-6_1-58-25.png)

1. Elimina i nodi del profilo e tutti i relativi nodi secondari. Esistono due formati per i nodi del profilo, a seconda della versione dell’AEM:

   1. Il profilo privato predefinito in `[!UICONTROL /profile]`
   1. `[!UICONTROL /profiles]`, per i nuovi profili creati con AEM 6.5.

   ![image2018-2-6_2-0-4](assets/image2018-2-6_2-0-4.png)

### API HTTP {#http-api-1}

Le procedure seguenti utilizzano `curl` strumento da riga di comando per illustrare come disabilitare l&#39;utente con **[!UICONTROL caverna]** `userId` ed eliminare i profili di `cavery` disponibili nel percorso predefinito.

* *Individuazione della home utente*

```shell
curl -g -u user:password 'http://localhost:4502/libs/granite/security/search/authorizables.json?query={"condition":[{"named":"cavery"}]}'
     {"authorizables":[{"type":"user","authorizableId_xss":"cavery","authorizableId":"cavery","name_xss":"Carlene Avery","name":"Carlene Avery","home":"/home/users/we-retail/DSCP-athB1NYLBXvdTuN"}],"total":1}
```

* *Disabilitazione dell’utente*

Utilizzo del percorso del nodo dalla proprietà home del payload JSON restituito dal comando precedente:

```shell
curl -X POST -u user:password -FdisableUser="describe the reasons for disabling this user (GDPR in this case)" 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN.rw.userprops.html'
```

* *Eliminazione dei profili utente*

Utilizzo del percorso del nodo dalla proprietà home del payload JSON restituito dal comando di individuazione account e dalle posizioni note dei nodi del profilo predefinite:

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```
