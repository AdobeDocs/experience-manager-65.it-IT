---
title: Creazione di un gruppo utenti chiuso
seo-title: Creazione di un gruppo utenti chiuso
description: Scoprite come creare un gruppo di utenti chiuso.
seo-description: Scoprite come creare un gruppo di utenti chiuso.
uuid: dc3c7dbd-2e86-43f9-9377-3b75053203b3
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 6ae57874-a9a1-4208-9001-7f44a1f57cbe
docset: aem65
translation-type: tm+mt
source-git-commit: 29328ff7fde4ed0e7f9728af1be911133259dc6c
workflow-type: tm+mt
source-wordcount: '808'
ht-degree: 0%

---


# Creazione di un gruppo utenti chiuso{#creating-a-closed-user-group}

I gruppi di utenti chiusi (CUG) vengono utilizzati per limitare l’accesso a pagine specifiche che risiedono all’interno di un sito Internet pubblicato. Tali pagine richiedono che i membri assegnati accedano e forniscano le credenziali di protezione.

Per configurare tale area all’interno del sito Web, effettuate le seguenti operazioni:

* [creare il gruppo utenti chiuso effettivo e assegnare i membri](#creating-the-user-group-to-be-used).

* [applica questo gruppo alle ](#applying-your-closed-user-group-to-content-pages) pagine richieste e seleziona (o crea) la pagina di accesso da utilizzare dai membri del gruppo di utenti chiuso; specificato anche quando si applica un CUG a una pagina di contenuto.

* [creare un collegamento, di un modulo, ad almeno una pagina all&#39;interno dell&#39;area](#linking-to-the-realm) protetta, altrimenti non sarà visibile.
* [configura il ](#configure-dispatcher-for-cugs) Dispatcherif in uso.

>[!CAUTION]
>
>I gruppi di utenti chiusi (CUG) devono sempre essere creati tenendo presenti le prestazioni.
>
>Sebbene il numero di utenti e gruppi in un CUG non sia limitato, un numero elevato di CUG in una pagina potrebbe rallentare le prestazioni di rendering.
>
>L&#39;impatto dei CUG dovrebbe sempre essere considerato durante il test delle prestazioni.

## Creazione del gruppo di utenti da utilizzare {#creating-the-user-group-to-be-used}

Per creare un gruppo di utenti chiuso:

1. Andate a **Strumenti - Sicurezza** dalla schermata iniziale AEM.

   >[!NOTE]
   >
   >Per informazioni complete sulla creazione e la configurazione di utenti e gruppi, consultate [Gestione di utenti e gruppi](/help/sites-administering/security.md#managing-users-and-groups).

1. Selezionate la scheda **Groups** dalla schermata successiva.

   ![screenshot_2018-10-30at145502](assets/screenshot_2018-10-30at145502.png)

1. Premere il tasto **Crea** nell&#39;angolo in alto a destra, per creare un nuovo gruppo.
1. Denominate il nuovo gruppo; ad esempio, `cug_access`.

   ![screenshot_2018-10-30at151459](assets/screenshot_2018-10-30at151459.png)

1. Passate alla scheda **Membri** e assegnate gli utenti richiesti a questo gruppo.

   ![screenshot_2018-10-30at151808](assets/screenshot_2018-10-30at151808.png)

1. Attivate gli utenti assegnati al gruppo di utenti chiuso; in questo caso, tutti i membri di `cug_access`.
1. Attivate il gruppo di utenti chiuso in modo che sia disponibile nell’ambiente di pubblicazione; in questo esempio, `cug_access`.

## Applicazione del gruppo di utenti chiuso alle pagine di contenuto {#applying-your-closed-user-group-to-content-pages}

Per applicare il CUG a una pagina:

1. Andate alla pagina principale della sezione limitata che desiderate assegnare al gruppo di utenti chiuso.
1. Selezionate la pagina facendo clic sulla relativa miniatura, quindi facendo clic su **Proprietà** nel pannello superiore.

   ![screenshot_2018-10-30at162632](assets/screenshot_2018-10-30at162632.png)

1. Nella finestra seguente, passare alla scheda **Avanzate**.
1. Scorri verso il basso e abilita la casella di controllo nella sezione **Autenticazione richiesta**.

1. Aggiungi il percorso di configurazione qui sotto, quindi premi Salva.
1. Quindi, passare alla scheda **Autorizzazioni** e premere il pulsante **Edit Closed User Group**.

   ![screenshot_2018-10-30at163003](assets/screenshot_2018-10-30at163003.png)

   >[NOTA!]
   >
   > Non è possibile ripristinare i CUG nella scheda Autorizzazioni dai blueprint alle Live Copy. Pianificate questo aspetto durante la configurazione di Live Copy.
   >
   > Per ulteriori informazioni, vedere [questa pagina](closed-user-groups.md#aem-livecopy).

1. Cercate e aggiungete il vostro CUG nella finestra seguente - in questo caso aggiungete il gruppo denominato **cug_access**. Premere infine **Save**.
1. Fare clic su **Abilitato** per definire che la pagina (e le eventuali pagine figlie) appartengano a un gruppo di utenti chiuso.
1. Specificare la **pagina di login** che i membri del gruppo utilizzeranno; ad esempio:

   `/content/geometrixx/en/toolbar/login.html`

   Se lasciato vuoto, verrà utilizzata la pagina di accesso standard.

1. Aggiungere i **Gruppi consentiti**. Utilizzate + per aggiungere gruppi o - per rimuovere. Solo i membri di questi gruppi potranno accedere alle pagine.
1. Se necessario, assegnate un **realm** (un nome per i gruppi di pagine). Lascia vuoto per usare il titolo della pagina.
1. Fare clic su **OK** per salvare la specifica.

Per informazioni sui profili nell&#39;ambiente di pubblicazione e sui moduli per l&#39;accesso e la disconnessione, vedere [ Identity Management](/help/sites-administering/identity-management.md).

## Collegamento Al Realm {#linking-to-the-realm}

Poiché la destinazione di eventuali collegamenti a CUG Realm non è visibile all’utente anonimo, il controllo dei collegamenti rimuoverà tali collegamenti.

Per evitare questo problema, è consigliabile creare pagine di reindirizzamento non protette che puntino alle pagine all’interno dell’area di autenticazione CUG. Le voci di navigazione vengono quindi sottoposte a rendering senza causare problemi al controllo dei collegamenti. Solo quando l&#39;utente accede effettivamente alla pagina di reindirizzamento, verrà reindirizzato all&#39;interno del realm CUG, dopo aver fornito con successo le proprie credenziali di accesso.

## Configurare il dispatcher per i CUG {#configure-dispatcher-for-cugs}

Se utilizzi Dispatcher, devi definire una farm di Dispatcher con le seguenti proprietà:

* [virtualhost](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#identifying-virtual-hosts-virtualhosts): Corrisponde al percorso delle pagine a cui si applica il CUG.
* \sessionmanagement: vedi sotto.
* [cache](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#configuring-the-dispatcher-cache-cache): Directory cache dedicata ai file a cui si applica il CUG.

### Configurazione della gestione delle sessioni del dispatcher per i gruppi di lavoro di gruppo di utenti (CUG) {#configuring-dispatcher-session-management-for-cugs}

Configurate la gestione delle sessioni [nel dispatcher.any file](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement) per il gruppo di utenti chiuso. Il gestore di autenticazione utilizzato quando l’accesso è richiesto per le pagine CUG determina la modalità di configurazione della gestione delle sessioni.

```xml
/sessionmanagement
    ...
    /header "Cookie:login-token"
    ...
```

>[!NOTE]
>
>Quando una farm del dispatcher ha abilitato la gestione delle sessioni, tutte le pagine gestite dalla farm non vengono memorizzate nella cache. Per memorizzare nella cache le pagine esterne al gruppo di utenti chiuso, crea una seconda farm in dispatcher.any
>che gestisce le pagine non CUG.

1. Configurare [/sessionmanagement](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement) definendo `/directory`; ad esempio:

   ```xml
   /sessionmanagement
     {
     /directory "/usr/local/apache/.sessions"
     ...
     }
   ```

1. Impostare [/allowAuthorized](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#caching-when-authentication-is-used) su `0`.

