---
title: Creazione di un gruppo utenti chiuso
seo-title: Creating a Closed User Group
description: Scopri come creare un gruppo utenti chiuso.
seo-description: Learn how to work with Closed User Groups in Adobe Experience Manager.
uuid: dc3c7dbd-2e86-43f9-9377-3b75053203b3
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 6ae57874-a9a1-4208-9001-7f44a1f57cbe
docset: aem65
exl-id: 9efba91d-45e8-42e1-9db6-490d21bf7412
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 2%

---

# Creazione di un gruppo utenti chiuso{#creating-a-closed-user-group}

I gruppi chiusi di utenti (CUG) vengono utilizzati per limitare l’accesso a pagine specifiche che risiedono in un sito Internet pubblicato. Tali pagine richiedono ai membri assegnati di accedere e fornire le credenziali di sicurezza.

Per configurare tale area all’interno del sito web:

* [creare il gruppo utenti chiuso effettivo e assegnare membri](#creating-the-user-group-to-be-used).

* [applica questo gruppo alle pagine richieste](#applying-your-closed-user-group-to-content-pages) e seleziona (o crea) la pagina di accesso per l’utilizzo da parte dei membri del CUG; specificato anche quando si applica un CUG a una pagina di contenuto.

* [creare un collegamento, sotto forma di testo, ad almeno una pagina nell&#39;area protetta](#linking-to-the-cug-pages), altrimenti non sarà visibile.

* [configurare Dispatcher](#configure-dispatcher-for-cugs) se in uso.

>[!CAUTION]
>
>I gruppi chiusi di utenti (CUG) devono sempre essere creati tenendo presenti le prestazioni.
>
>Anche se il numero di utenti e gruppi in un CUG non è limitato, un numero elevato di CUG in una pagina può rallentare le prestazioni di rendering.
>
>L’impatto dei gruppi di utenti chiusi (CUG) deve sempre essere considerato durante l’esecuzione del test delle prestazioni.

## Creazione Del Gruppo Di Utenti Da Utilizzare {#creating-the-user-group-to-be-used}

Per creare un gruppo utenti chiuso:

1. Vai a **Strumenti - Sicurezza** dal homescreen dell&#39;AEM.

   >[!NOTE]
   >
   >Consulta [Gestione di utenti e gruppi](/help/sites-administering/security.md#managing-users-and-groups) per informazioni complete sulla creazione e la configurazione di utenti e gruppi.

1. Seleziona la **Gruppi** dalla schermata successiva.

   ![screenshot_2018-10-30at145502](assets/screenshot_2018-10-30at145502.png)

1. Premere il tasto **Crea** nell&#39;angolo in alto a destra per creare un nuovo gruppo.
1. Assegna un nome al nuovo gruppo; ad esempio, `cug_access`.

   ![screenshot_2018-10-30at151459](assets/screenshot_2018-10-30at151459.png)

1. Vai a **Membri** e assegna gli utenti richiesti a questo gruppo.

   ![screenshot_2018-10-30at151808](assets/screenshot_2018-10-30at151808.png)

1. Attiva tutti gli utenti che hai assegnato al tuo CUG; in questo caso, tutti i membri di `cug_access`.
1. Attiva il gruppo utenti chiuso in modo che sia disponibile nell’ambiente di pubblicazione; in questo esempio, `cug_access`.

## Applicazione Del Gruppo Di Utenti Chiuso Alle Pagine Di Contenuto {#applying-your-closed-user-group-to-content-pages}

Per applicare il gruppo utenti chiusi a una o più pagine:

1. Passare alla pagina principale della sezione limitata che si desidera assegnare al gruppo utenti chiusi.
1. Seleziona la pagina facendo clic sulla relativa miniatura e selezionando **Proprietà** nella barra degli strumenti superiore.

   ![screenshot_2018-10-30at162632](assets/screenshot_2018-10-30at162632.png)

1. Nella finestra seguente aprire **Avanzate** scheda.

1. Scorri verso il basso fino a **Autenticazione richiesta** sezione.

   1. Attiva il **Abilita** casella di spunta.

   1. Aggiungi il percorso al tuo **Pagina di accesso**.
Questo è facoltativo; se lasciato vuoto, verrà utilizzata la pagina di accesso standard.

   ![CUG aggiunto](assets/cug-authentication-requirement.png)

1. Quindi, vai al **Autorizzazioni** e seleziona **Modifica gruppo utenti chiuso**.

   ![screenshot_2018-10-30at163003](assets/screenshot_2018-10-30at163003.png)

   >[!NOTE]
   >
   >Non è possibile eseguire il rollout dei CUG nella scheda Autorizzazioni in Live Copy da Blueprint. Pianifica tutto questo durante la configurazione delle Live Copy.
   >
   >Per ulteriori informazioni, consulta [questa pagina](closed-user-groups.md#aem-livecopy).

1. Il **Modifica gruppo utenti chiuso** viene aperta una finestra di dialogo. Qui puoi cercare e selezionare il tuo CUG, quindi confermare la selezione del gruppo con **Salva**.

   Il gruppo verrà aggiunto all’elenco; ad esempio, il gruppo **cug_access**.

   ![CUG aggiunto](assets/cug-added.png)

1. Conferma le modifiche con **Salva e chiudi**.

>[!NOTE]
>
>Consulta [Identity Management](/help/sites-administering/identity-management.md) per informazioni sui profili nell’ambiente di pubblicazione e per fornire moduli per l’accesso e la disconnessione.

## Collegamento alle pagine dei gruppi utenti chiusi (CUG) {#linking-to-the-cug-pages}

Poiché la destinazione di qualsiasi collegamento alle pagine CUG non è visibile all’utente anonimo, il LinkChecker rimuoverà tali collegamenti.

Per evitare questo problema, è consigliabile creare pagine di reindirizzamento non protette che puntano a pagine all’interno dell’area CUG. Le voci di navigazione vengono quindi sottoposte a rendering senza causare problemi al LinkChecker. Solo quando accede effettivamente alla pagina di reindirizzamento, l’utente viene reindirizzato all’interno dell’area del gruppo utenti chiusi (CUG), dopo aver fornito correttamente le credenziali di accesso.

## Configurare Dispatcher per i gruppi utenti chiusi (CUG) {#configure-dispatcher-for-cugs}

Se utilizzi Dispatcher, devi definire una farm di Dispatcher con le seguenti proprietà:

* [virtualhosts](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#identifying-virtual-hosts-virtualhosts): corrisponde al percorso delle pagine a cui si applica il CUG.
* \sessionmanagement: vedi di seguito.
* [cache](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#configuring-the-dispatcher-cache-cache): directory della cache dedicata ai file a cui si applica il gruppo utenti chiusi (CUG).

### Configurazione della gestione delle sessioni del Dispatcher per i gruppi utenti chiusi (CUG) {#configuring-dispatcher-session-management-for-cugs}

Configura [gestione delle sessioni nel file dispatcher.any](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#enabling-secure-sessions-sessionmanagement) per il CUG. Il gestore di autenticazione utilizzato quando viene richiesto l&#39;accesso per le pagine CUG determina la modalità di configurazione della gestione delle sessioni.

```xml
/sessionmanagement
    ...
    /header "Cookie:login-token"
    ...
```

>[!NOTE]
>
>Quando la gestione delle sessioni è abilitata in una farm di Dispatcher, tutte le pagine gestite dalla farm non vengono memorizzate in cache. Per memorizzare in cache le pagine che si trovano al di fuori del gruppo utenti chiusi (CUG), crea una seconda farm in dispatcher.any
>che gestisce le pagine non appartenenti a gruppi utenti chiusi (CUG).

1. Configura [/sessionmanagement](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#enabling-secure-sessions-sessionmanagement) definendo `/directory`; ad esempio:

   ```xml
   /sessionmanagement
     {
     /directory "/usr/local/apache/.sessions"
     ...
     }
   ```

1. Imposta [/allowAuthorized](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#caching-when-authentication-is-used) a `0`.
