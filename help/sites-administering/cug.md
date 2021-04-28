---
title: Creazione di un gruppo utenti chiuso
seo-title: Creazione di un gruppo utenti chiuso
description: Scopri come creare un gruppo utenti chiuso.
seo-description: Scopri come creare un gruppo utenti chiuso.
uuid: dc3c7dbd-2e86-43f9-9377-3b75053203b3
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 6ae57874-a9a1-4208-9001-7f44a1f57cbe
docset: aem65
exl-id: 9efba91d-45e8-42e1-9db6-490d21bf7412
translation-type: tm+mt
source-git-commit: cb4b0cb60b8709beea3da70495a15edc8c4831b8
workflow-type: tm+mt
source-wordcount: '808'
ht-degree: 0%

---

# Creazione di un gruppo utenti chiuso{#creating-a-closed-user-group}

I gruppi di utenti chiusi vengono utilizzati per limitare l’accesso a pagine specifiche che risiedono all’interno di un sito Internet pubblicato. Tali pagine richiedono l’accesso ai membri assegnati e l’immissione di credenziali di sicurezza.

Per configurare tale area all’interno del sito web:

* [creare il gruppo utenti chiuso effettivo e assegnare i membri](#creating-the-user-group-to-be-used).

* [applica questo gruppo alle ](#applying-your-closed-user-group-to-content-pages) pagine richieste e seleziona (o crea) la pagina di accesso da utilizzare dai membri del CUG; specificato anche quando si applica un gruppo utenti chiuso a una pagina di contenuto.

* [crea un collegamento, di un modulo, ad almeno una pagina all’interno dell’area](#linking-to-the-realm) protetta, altrimenti non sarà visibile.
* [configura il ](#configure-dispatcher-for-cugs) Dispatcherif in uso.

>[!CAUTION]
>
>I gruppi di utenti chiusi devono sempre essere creati tenendo presenti le prestazioni.
>
>Anche se il numero di utenti e gruppi in un CUG non è limitato, un numero elevato di CUG in una pagina può rallentare le prestazioni di rendering.
>
>L’impatto dei CUG deve sempre essere considerato durante il test delle prestazioni.

## Creazione del gruppo di utenti da utilizzare {#creating-the-user-group-to-be-used}

Per creare un gruppo utenti chiuso:

1. Vai a **Strumenti - Sicurezza** dalla schermata iniziale AEM.

   >[!NOTE]
   >
   >Per informazioni complete sulla creazione e la configurazione di utenti e gruppi, consulta [Gestione di utenti e gruppi](/help/sites-administering/security.md#managing-users-and-groups) .

1. Seleziona la scheda **Gruppi** dalla schermata successiva.

   ![screenshot_2018-10-30at145502](assets/screenshot_2018-10-30at145502.png)

1. Premi il pulsante **Crea** nell&#39;angolo in alto a destra per creare un nuovo gruppo.
1. Assegnare un nome al nuovo gruppo; ad esempio, `cug_access`.

   ![screenshot_2018-10-30at151459](assets/screenshot_2018-10-30at151459.png)

1. Vai alla scheda **Membri** e assegna gli utenti richiesti a questo gruppo.

   ![screenshot_2018-10-30at151808](assets/screenshot_2018-10-30at151808.png)

1. Attivare gli utenti assegnati al gruppo utenti chiuso; in questo caso, tutti i membri di `cug_access`.
1. Attiva il gruppo di utenti chiusi in modo che sia disponibile nell&#39;ambiente di pubblicazione; in questo esempio, `cug_access`.

## Applicazione del gruppo utenti chiuso alle pagine dei contenuti {#applying-your-closed-user-group-to-content-pages}

Per applicare il CUG a una pagina:

1. Passa alla pagina principale della sezione con restrizioni che desideri assegnare al CUG.
1. Seleziona la pagina facendo clic sulla relativa miniatura, quindi fai clic su **Proprietà** nel pannello superiore.

   ![screenshot_2018-10-30at162632](assets/screenshot_2018-10-30at162632.png)

1. Nella finestra seguente, vai alla scheda **Avanzate** .
1. Scorri verso il basso e abilita la casella di controllo nella sezione **Autenticazione richiesta** .

1. Aggiungi il percorso di configurazione qui sotto, quindi premi Salva.
1. Quindi, vai alla scheda **Autorizzazioni** e premi il pulsante **Modifica gruppo utenti chiuso** .

   ![screenshot_2018-10-30at163003](assets/screenshot_2018-10-30at163003.png)

   >[NOTA!]
   >
   > Non è possibile eseguire il rollout dei CUG nella scheda Autorizzazioni in Live Copy da Blueprint. Pianifica tutto questo durante la configurazione di Live Copy.
   >
   > Per ulteriori informazioni, consulta [questa pagina](closed-user-groups.md#aem-livecopy).

1. Cerca e aggiungi il tuo CUG nella finestra seguente - in questo caso aggiungi il gruppo denominato **cug_access**. Infine, premere **Save**.
1. Fai clic su **Abilitato** per definire che questa pagina (e tutte le pagine figlie) appartiene a un CUG.
1. Specificare la **pagina di accesso** che i membri del gruppo utilizzeranno; ad esempio:

   `/content/geometrixx/en/toolbar/login.html`

   Questa opzione è facoltativa, se viene lasciata vuota, verrà utilizzata la pagina di accesso standard.

1. Aggiungi i **Gruppi consentiti**. Utilizza + per aggiungere gruppi o - per rimuovere. Solo i membri di questi gruppi potranno accedere alle pagine e accedervi.
1. Assegna un **realm** (un nome per i gruppi di pagine) se necessario. Lascia vuoto per usare il titolo della pagina.
1. Fare clic su **OK** per salvare la specifica.

Per informazioni sui profili nell’ambiente di pubblicazione e sui moduli per l’accesso e la disconnessione, consulta [Identity Management](/help/sites-administering/identity-management.md) .

## Collegamento Al Realm {#linking-to-the-realm}

Poiché il target di qualsiasi link al Realm CUG non è visibile all&#39;utente anonimo, il linkchecker rimuoverà tali link.

Per evitare questo problema, è consigliabile creare pagine di reindirizzamento non protette che puntano a pagine all’interno del realm CUG. Le voci di navigazione vengono quindi rese senza causare problemi al linkchecker. Solo quando si accede effettivamente alla pagina di reindirizzamento, l&#39;utente verrà reindirizzato all&#39;interno del Realm CUG - dopo aver fornito con successo le proprie credenziali di accesso.

## Configurare Dispatcher per i gruppi di utenti chiusi {#configure-dispatcher-for-cugs}

Se utilizzi Dispatcher, devi definire una farm del Dispatcher con le seguenti proprietà:

* [virtualhost](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#identifying-virtual-hosts-virtualhosts): Corrisponde al percorso delle pagine a cui si applica il CUG.
* \sessionmanagement: vedi sotto.
* [cache](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#configuring-the-dispatcher-cache-cache): Directory cache dedicata ai file a cui si applica il CUG.

### Configurazione della gestione della sessione di Dispatcher per i gruppi di utenti chiusi {#configuring-dispatcher-session-management-for-cugs}

Configura la gestione delle sessioni [nel file dispatcher.any](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement) per il CUG. Il gestore di autenticazione utilizzato quando viene richiesto l’accesso per le pagine CUG determina la modalità di configurazione della gestione delle sessioni.

```xml
/sessionmanagement
    ...
    /header "Cookie:login-token"
    ...
```

>[!NOTE]
>
>Quando una farm del Dispatcher ha abilitato la gestione delle sessioni, tutte le pagine gestite dalla farm non vengono memorizzate nella cache. Per memorizzare nella cache le pagine esterne al gruppo di lavoro chiuso, crea una seconda farm in dispatcher.any
>che gestisce le pagine non CUG.

1. Configura [/sessionmanagement](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement) definendo `/directory`; ad esempio:

   ```xml
   /sessionmanagement
     {
     /directory "/usr/local/apache/.sessions"
     ...
     }
   ```

1. Impostare [/allowAuthorized](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#caching-when-authentication-is-used) su `0`.
