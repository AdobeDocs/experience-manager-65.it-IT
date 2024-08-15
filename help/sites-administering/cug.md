---
title: Creazione di un gruppo utenti chiuso
description: Scopri come creare un gruppo utenti chiuso.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
docset: aem65
exl-id: 9efba91d-45e8-42e1-9db6-490d21bf7412
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 6f3c4f4aa4183552492c6ce5039816896bd67495
workflow-type: tm+mt
source-wordcount: '710'
ht-degree: 1%

---

# Creazione di un gruppo utenti chiuso{#creating-a-closed-user-group}

I gruppi chiusi di utenti (CUG) vengono utilizzati per limitare l’accesso a pagine specifiche che risiedono in un sito Internet pubblicato. Tali pagine richiedono ai membri assegnati di accedere e fornire le credenziali di sicurezza.

Per configurare tale area all’interno del sito web:

* [creare il gruppo utenti chiuso effettivo e assegnare i membri](#creating-the-user-group-to-be-used).

* [applica il gruppo alle pagine richieste](#applying-your-closed-user-group-to-content-pages) e seleziona (o crea) la pagina di accesso per l&#39;utilizzo da parte dei membri del gruppo utenti chiusi (CUG); specificato anche quando si applica un gruppo utenti chiusi (CUG) a una pagina di contenuto.

* [creare un collegamento, in qualche modo, ad almeno una pagina all&#39;interno dell&#39;area protetta](#linking-to-the-cug-pages), altrimenti non sarà visibile.

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

1. Passa a **Strumenti - Sicurezza** dalla home page AEM.

   >[!NOTE]
   >
   >Per informazioni complete sulla creazione e la configurazione di utenti e gruppi, vedere [Gestione di utenti e gruppi](/help/sites-administering/security.md#managing-users-and-groups).

1. Seleziona la scheda **Gruppi** dalla schermata successiva.

   ![screenshot_2018-10-30at145502](assets/screenshot_2018-10-30at145502.png)

1. Per creare un gruppo, premi il pulsante **Crea** nell&#39;angolo in alto a destra.
1. Assegna un nome al nuovo gruppo, ad esempio `cug_access`.

   ![screenshot_2018-10-30at151459](assets/screenshot_2018-10-30at151459.png)

1. Vai alla scheda **Membri** e assegna gli utenti richiesti a questo gruppo.

   ![screenshot_2018-10-30at151808](assets/screenshot_2018-10-30at151808.png)

1. Attiva tutti gli utenti assegnati al tuo gruppo utenti chiusi (CUG); in questo caso, tutti i membri di `cug_access`.
1. Attiva il gruppo utenti chiuso in modo che sia disponibile nell&#39;ambiente di pubblicazione; in questo esempio, `cug_access`.

## Applicazione Del Gruppo Di Utenti Chiuso Alle Pagine Di Contenuto {#applying-your-closed-user-group-to-content-pages}

Per applicare il gruppo utenti chiusi a una o più pagine:

1. Passare alla pagina principale della sezione limitata che si desidera assegnare al gruppo utenti chiusi.
1. Selezionare la pagina facendo clic sulla relativa miniatura e selezionando **Proprietà** nella barra degli strumenti superiore.

   ![screenshot_2018-10-30at162632](assets/screenshot_2018-10-30at162632.png)

1. Nella finestra seguente aprire la scheda **Avanzate**.

1. Scorri verso il basso fino alla sezione **Requisiti di autenticazione**.

   1. Attiva la casella di spunta **Abilita**.

   1. Aggiungi il percorso alla **pagina di accesso**.
Questa opzione è facoltativa, se lasciata vuota, viene utilizzata la pagina di accesso standard.

   ![CUG aggiunto](assets/cug-authentication-requirement.png)

1. Quindi, vai alla scheda **Autorizzazioni** e seleziona **Modifica gruppo utenti chiuso**.

   ![screenshot_2018-10-30at163003](assets/screenshot_2018-10-30at163003.png)

   >[!NOTE]
   >
   >Non è possibile eseguire il rollout dei CUG nella scheda Autorizzazioni in Live Copy da Blueprint. Pianifica tutto questo durante la configurazione della Live Copy.
   >
   >Per ulteriori informazioni, consulta [Gruppi utenti chiusi in AEM - Livecopy](closed-user-groups.md#aem-livecopy).

1. Viene visualizzata la finestra di dialogo **Modifica gruppo utenti chiuso**. Qui puoi cercare e selezionare il tuo CUG, quindi confermare la selezione del gruppo con **Salva**.

   Il gruppo verrà aggiunto all&#39;elenco, ad esempio il gruppo **cug_access**.

   ![CUG aggiunto](assets/cug-added.png)

1. Conferma le modifiche con **Salva e chiudi**.

>[!NOTE]
>
>Consulta [Identity Management](/help/sites-administering/identity-management.md) per informazioni sui profili nell&#39;ambiente di pubblicazione e per fornire moduli per l&#39;accesso e la disconnessione.

## Collegamento alle pagine dei gruppi utenti chiusi (CUG) {#linking-to-the-cug-pages}

Poiché la destinazione di qualsiasi collegamento alle pagine CUG non è visibile all’utente anonimo, il LinkChecker rimuoverà tali collegamenti.

Per evitare questo problema, è consigliabile creare pagine di reindirizzamento non protette che puntano a pagine all’interno dell’area CUG. Le voci di navigazione vengono quindi sottoposte a rendering senza causare problemi al LinkChecker. Solo quando accede effettivamente alla pagina di reindirizzamento, l’utente viene reindirizzato all’interno dell’area del gruppo utenti chiusi (CUG), dopo aver fornito correttamente le credenziali di accesso.

## Configurare Dispatcher per i gruppi utenti chiusi (CUG) {#configure-dispatcher-for-cugs}

Se utilizzi Dispatcher, devi definire una farm di Dispatcher con le seguenti proprietà:

* [virtualhosts](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#identifying-virtual-hosts-virtualhosts): corrisponde al percorso delle pagine a cui si applica il gruppo utenti chiusi.
* \sessionmanagement: vedi di seguito.
* [cache](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring-the-dispatcher-cache-cache): directory della cache dedicata ai file a cui si applica il gruppo utenti chiusi.

### Configurazione della gestione delle sessioni di Dispatcher per i gruppi utenti chiusi (CUG) {#configuring-dispatcher-session-management-for-cugs}

Configura la gestione di [sessione nel file dispatcher.any](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement) per il gruppo utenti chiusi. Il gestore di autenticazione utilizzato quando viene richiesto l&#39;accesso per le pagine CUG determina la modalità di configurazione della gestione delle sessioni.

```xml
/sessionmanagement
    ...
    /header "Cookie:login-token"
    ...
```

>[!NOTE]
>
>Quando la gestione delle sessioni è abilitata in una farm di Dispatcher, tutte le pagine gestite dalla farm non vengono memorizzate nella cache. Per memorizzare in cache le pagine che si trovano al di fuori del gruppo utenti chiusi (CUG), crea una seconda farm in dispatcher.any
>che gestisce le pagine non appartenenti a gruppi utenti chiusi (CUG).

1. Configurare [/sessionmanagement](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement) definendo `/directory`, ad esempio:

   ```xml
   /sessionmanagement
     {
     /directory "/usr/local/apache/.sessions"
     ...
     }
   ```

1. Imposta [/allowAuthorized](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#caching-when-authentication-is-used) su `0`.
