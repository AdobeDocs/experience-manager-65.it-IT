---
title: Aggiunta e configurazione di utenti
seo-title: Adding and configuring users
description: Le impostazioni User Management nella console di amministrazione consentono di creare o eliminare utenti e configurare altre impostazioni utente.
seo-description: The User Management settings in the administration console allow you to create or delete users  and configure other user settings.
uuid: fe650cdb-7d0d-4f38-9899-e5349559ed32
contentOwner: admin
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
discoiquuid: 20ca99e3-4843-4254-b3e9-0255cc752363
exl-id: 50eea35d-d844-4f4b-9cbe-7d84bd6b1e3b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1739'
ht-degree: 0%

---

# Aggiunta e configurazione di utenti {#adding-and-configuring-users}

Le informazioni utente e gruppo vengono mantenute in un sistema di storage di terze parti, ad esempio una directory LDAP. Gestione utente non scrive nel sistema di storage di terze parti. Gestione utente sincronizza invece le informazioni utente e gruppo con il proprio database

## Creare un utente {#create-a-user}

Quando crei degli utenti, puoi aggiungerli ai gruppi e assegnare loro ruoli.

1. Nella console di amministrazione, fai clic su **[!UICONTROL Impostazioni > Gestione utente > Utenti e gruppi]** e fai clic su **[!UICONTROL Nuovo utente]**. .
1. Sotto **[!UICONTROL Impostazioni generali]**, fornire le informazioni richieste, quindi fare clic su **[!UICONTROL Successivo]**. Per informazioni dettagliate sulle impostazioni, vedi [Impostazioni utente](adding-configuring-users.md#user-settings).
1. (Facoltativo) Per aggiungere l&#39;utente a un gruppo, fai clic su **[!UICONTROL Trova gruppi]** ed eseguire le seguenti operazioni:

   * In **[!UICONTROL Trova]** digitare tutto o parte del nome del gruppo.
   * Selezionare il dominio da cercare, selezionare il numero di elementi da visualizzare e fare clic su **[!UICONTROL Trova]**.
   * (Facoltativo) Per visualizzare i dettagli del gruppo, selezionare il nome del gruppo, quindi fare clic su **[!UICONTROL OK]** per tornare alla pagina dei risultati della ricerca.
   * Seleziona la casella di controllo del gruppo e fai clic su **[!UICONTROL OK]**.
   * Fai clic su **[!UICONTROL Avanti]**.

1. (Facoltativo) Per assegnare ruoli all’utente, fai clic su **[!UICONTROL Trova ruoli]**, seleziona la casella di controllo relativa ai ruoli da assegnare, quindi fai clic su **[!UICONTROL OK]**.
1. Fai clic su **[!UICONTROL Fine]**.

   >[!NOTE]
   >
   >Se riscontri problemi di accesso con l&#39;utente, consulta [L&#39;utente AEM Forms su JEE non riesce ad accedere su AEM Forms sul lato OSGi](https://helpx.adobe.com/aem-forms/kb/AEM-users-fails-to-login.html).

## Impostazioni utente {#user-settings}

Quando crei o modifichi un utente, specifica le seguenti impostazioni.

**Nome canonico:** (Obbligatorio) Identificatore univoco per l&#39;utente. Ogni utente e gruppo in un dominio deve avere un nome canonico univoco. Selezionare la casella di controllo System Generated (Generazione sistema) per consentire a User Management di assegnare un valore univoco oppure deselezionare la casella di controllo e specificare un valore personalizzato per il Canonical Name (Nome canonico).

Evita di utilizzare caratteri di sottolineatura (_) nei nomi canonici, ad esempio `sample_user`. Quando cerchi utenti in base al loro nome canonico, quelli contenenti caratteri di sottolineatura non vengono restituiti.

**Nome:** (Obbligatorio) Nome dell&#39;utente

**Cognome:** (Obbligatorio) Cognome dell&#39;utente

**Nome comune:** Nome completo o nome visualizzato dell&#39;utente. Ad esempio, se Nome = Gloria e Cognome = Rios, Nome comune = Gloria Rios.

**E-mail:** Indirizzo e-mail dell’utente

**Telefono:** Numero di telefono dell’utente

**Descrizione:** Descrizione facoltativa. Utilizza questo campo in base alle esigenze della tua organizzazione.

**Indirizzo:** Indirizzo postale dell’utente

**Organizzazione:** Organizzazione a cui appartiene l&#39;utente

**Alias e-mail:** Alias e-mail dell’utente. Separa gli alias e-mail con virgole.

**Dominio:** Dominio a cui appartiene l&#39;utente

**Impostazioni internazionali:** Impostazioni internazionali ISO dell’utente

**Chiave del calendario aziendale:** Consente di mappare un calendario aziendale a un utente in base al valore di questa impostazione. I calendari aziendali definiscono i giorni lavorativi e non lavorativi. I moduli AEM possono utilizzare calendari aziendali per calcolare date e ore future relative a eventi quali promemoria, scadenze ed escalation. Il modo in cui si assegnano le chiavi del calendario aziendale agli utenti dipende dal fatto che si utilizzi un dominio enterprise, locale o ibrido. (Vedi [Aggiunta di domini](/help/forms/using/admin-help/adding-domains.md#adding-domains).)

Se si utilizza un dominio locale o ibrido, le informazioni sugli utenti vengono memorizzate solo nel database User Management. Per questi utenti, impostare la Chiave del calendario aziendale su una stringa. Quindi mappare la chiave del calendario aziendale (la stringa) su un calendario aziendale nel flusso di lavoro dei moduli.

Se utilizzi un dominio enterprise, le informazioni sugli utenti risiedono in un sistema di storage di terze parti, ad esempio una directory LDAP. User Management sincronizza le informazioni utente dalla directory con il database User Management. Questa funzione consente di mappare una chiave del calendario aziendale su un campo nella directory LDAP. Ad esempio, considerare uno scenario in cui ogni record utente nella directory contiene un campo paese e si desidera assegnare calendari aziendali in base al paese in cui si trova l&#39;utente. In questo caso, specificare il nome del campo del paese come valore per l&#39;impostazione Chiave calendario aziendale. È quindi possibile mappare le chiavi del calendario aziendale (i valori definiti per il campo paese nella directory LDAP) ai calendari aziendali nel flusso di lavoro dei moduli.

Per ulteriori informazioni sui calendari aziendali, inclusa la modalità di mappatura delle chiavi del calendario aziendale sui calendari aziendali, vedere [Configurazione dei calendari aziendali](/help/forms/using/admin-help/configuring-business-calendars.md#configuring-business-calendars).

Limita il nome a meno di 53 caratteri. Un nome più breve aiuta a evitare problemi nella visualizzazione della chiave del calendario aziendale nelle pagine Gestione processi nella console di amministrazione.

**ID utente:** (Obbligatorio) ID utente utilizzato dall&#39;utente per effettuare l&#39;accesso. L’ID utente non distingue tra maiuscole e minuscole e deve essere univoco nel dominio .

Nei domini aziendali, utilizza un attributo non DN come ID utente perché il DN di un utente può cambiare se si sposta in un&#39;altra parte dell&#39;organizzazione. Questa impostazione dipende dal server di directory. Il valore è `objectGUID` per Active Directory 2003, `nsuniqueID` per Sun™ One, e `guid` per eDirectory.

Assicurati che l&#39;ID utente sia univoco. Non utilizzare uno assegnato a un utente eliminato.

I moduli AEM non possono distinguere tra account utente che hanno ID utente e password identici ma appartengono a domini diversi. Per evitare questo problema, non creare account con lo stesso ID utente su più domini.

Quando si utilizza SQL Server come database, non è possibile creare un ID utente che superi i 255 caratteri.

Quando si utilizza MySQL, l&#39;ID utente può contenere caratteri estesi. Tuttavia, quando si effettua un confronto tra due stringhe, quali abcde e âbcdè, esse sono considerate uguali. Ad esempio, durante la sincronizzazione, se un nuovo utente è stato aggiunto al database, viene effettuato un confronto per verificare se nel database esiste un utente con lo stesso ID utente. Se l&#39;utente *basso* esiste già nel database quando il nuovo utente *âbcdè* viene aggiunto, il confronto non è in grado di distinguere tra i due nomi. Si presume che l&#39;utente esista già nel database e che il nuovo utente venga ignorato e non aggiunto.

Evitare di creare nomi utente che iniziano con un simbolo cancelletto (#). L&#39;esecuzione delle ricerche delle attività non restituisce alcun risultato per questi nomi utente. (Vedi [Utilizzo delle attività](/help/forms/using/admin-help/tasks.md#working-with-tasks).)

**Password e conferma password:** Password utilizzata dall&#39;utente per l&#39;accesso. Deve contenere almeno otto caratteri. Una password non è necessaria per un utente che fa parte di un dominio ibrido.

## Visualizzare i dettagli di un utente {#view-details-about-a-user}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Utenti e gruppi.
1. Specificare le informazioni per limitare la ricerca e, nell&#39;elenco In, selezionare Utenti, quindi fare clic su Trova. I risultati della ricerca sono elencati nella parte inferiore della pagina. Per ordinare l’elenco, fai clic su una delle intestazioni di colonna.
1. Fai clic sul nome dell’utente di cui visualizzare i dettagli. Nella pagina Modifica utente sono visualizzati i dettagli seguenti relativi all’utente:

   * Informazioni generali di identificazione come nome, e-mail, indirizzo, dominio e organizzazione
   * Ruoli assegnati all’utente
   * Gruppi di cui fa parte l&#39;utente

## Modificare la password per un utente locale {#change-the-password-for-a-local-user}

1. Nella console di amministrazione, fai clic su **[!UICONTROL Impostazioni > Gestione utente > Utenti e gruppi]**.
1. Specificare le informazioni per limitare la ricerca di un utente specifico e fare clic su **[!UICONTROL Trova]**. I risultati della ricerca sono elencati nella parte inferiore della pagina. Per ordinare l’elenco, fai clic su una delle intestazioni di colonna.
1. Fai clic sul nome dell’utente e quindi fai clic su **[!UICONTROL Modifica password]**.
1. Digitare e confermare la nuova password, quindi fare clic su **[!UICONTROL OK]**. La password deve contenere almeno otto caratteri.

## Modificare le proprietà di un utente {#edit-a-user-s-properties}

1. Nella console di amministrazione, fai clic su **[!UICONTROL Impostazioni > Gestione utente > Utenti e gruppi]**.
1. Per trovare l&#39;utente da modificare, eseguire le operazioni seguenti:

   * In **[!UICONTROL Trova]** digitare i criteri di ricerca.
   * In **[!UICONTROL Utilizzo]** elenco, selezionare **[!UICONTROL Nome]**, **[!UICONTROL E-mail]** oppure **[!UICONTROL ID utente]**.
   * In **[!UICONTROL Nell&#39;elenco]**, seleziona **[!UICONTROL Utenti]**.
   * Selezionare il dominio, selezionare il numero di elementi da visualizzare, quindi fare clic su **[!UICONTROL Trova]**.

1. Fai clic sull’utente da modificare.
1. Per un utente che fa parte di un dominio locale o ibrido, nel **[!UICONTROL Dettaglio]** scheda , modifica **[!UICONTROL Impostazioni generali]** e **[!UICONTROL Impostazioni di accesso]** e fai clic su **[!UICONTROL Salva]**. Per informazioni dettagliate sulle impostazioni, vedi [Impostazioni utente](adding-configuring-users.md#user-settings). Non è possibile modificare le impostazioni generali e di accesso per un utente che appartiene a un dominio enterprise.
1. Per modificare le impostazioni del gruppo per l&#39;utente, fai clic sul pulsante **[!UICONTROL Iscrizione al gruppo]** eseguire le operazioni seguenti:

   * Fai clic su **[!UICONTROL Trova gruppo]** e completare le informazioni di ricerca.
   * Per aggiungere l&#39;utente a un nuovo gruppo, selezionare la casella di controllo relativa al gruppo, fare clic su **[!UICONTROL OK]**, quindi fai clic su **[!UICONTROL Salva]**.

   >[!NOTE]
   >
   >Impossibile aggiungere utenti locali ai gruppi di directory. Tuttavia, gli utenti della directory possono essere aggiunti ai gruppi locali.

   * Per rimuovere l&#39;utente da un gruppo, selezionare la casella di controllo relativa al gruppo, fare clic su **[!UICONTROL Elimina]**, quindi fai clic su **[!UICONTROL Salva]**.


1. Per modificare i ruoli dell’utente, fai clic sul pulsante **[!UICONTROL Assegnazioni ruoli]** eseguire le operazioni seguenti:

   * Per visualizzare un elenco di ruoli, fai clic su **[!UICONTROL Trova ruoli]**.
   * Per aggiungere un ruolo, seleziona la casella di controllo relativa al ruolo e fai clic su **[!UICONTROL OK]**, quindi fai clic su **[!UICONTROL Salva]**.
   * Per rimuovere un ruolo, selezionare la casella di controllo relativa al ruolo, fare clic su **[!UICONTROL Annulla assegnazione]**, quindi fai clic su **[!UICONTROL Salva]**.

## Eliminare un utente {#delete-a-user}

1. Nella console di amministrazione, fai clic su **[!UICONTROL Impostazioni > Gestione utente > Utenti e gruppi]**.
1. Per trovare l&#39;utente da eliminare, eseguire le operazioni seguenti:

   * In **[!UICONTROL Trova]** digitare i criteri di ricerca.
   * In **[!UICONTROL Utilizzo]** elenco, selezionare **[!UICONTROL Nome]**, **[!UICONTROL E-mail]** oppure **[!UICONTROL ID utente]**.
   * In **[!UICONTROL Nell&#39;elenco]**, seleziona **[!UICONTROL Utenti]**.
   * Selezionare il dominio, selezionare il numero di elementi da visualizzare, quindi fare clic su **[!UICONTROL Trova]**.

1. Seleziona la casella di controllo per l’utente e fai clic su **[!UICONTROL Elimina]**, quindi fai clic su **[!UICONTROL OK]**.

>[!NOTE]
>
>AEM Forms su JEE consente inoltre agli utenti del componente aggiuntivo AEM forms in esecuzione su un OSGi di essere riconosciuti come utenti AEM. Questo è necessario per gli scenari in cui è richiesto il single sign-on tra AEM Forms su JEE e il componente aggiuntivo AEM forms in esecuzione su un OSGi (ad esempio, l’area di lavoro di HTML). L’operazione di eliminazione di cui sopra rimuove un utente solo da AEM Forms su JEE. L’utente non viene eliminato dal componente aggiuntivo AEM Forms in esecuzione nell’ambiente OSGi. Ma qualsiasi tentativo di accesso effettuato dopo l&#39;eliminazione dell&#39;utente (un tentativo di accesso al server JEE aggiuntivo di AEM Forms o al componente aggiuntivo AEM Forms nell&#39;ambiente OSGi) è negato.

## Crea handler di errori di accesso personalizzato {#create-custom-login-error-handler}

Se un utente senza i moduli AEM e le autorizzazioni CQ richiesti tenta di accedere alle seguenti applicazioni incorporate in CQ, l&#39;utente viene reindirizzato alla pagina CQ 404 predefinita contenente la traccia di errore:

* Soluzione per la gestione della corrispondenza
* Area di lavoro moduli AEM

   ***nota **: Flex Workspace è obsoleto per AEM versione dei moduli.*

* Forms Manager
* Reporting processi

CQ fornisce un meccanismo per sostituire il jsp 404 handler predefinito.

Per informazioni dettagliate su come personalizzare la pagina di gestione degli errori, consulta [Personalizzazione delle pagine mostrate dal gestore errori](https://docs.adobe.com/docs/en/cq/current/developing/customizing_error_handler_pages.html) nella documentazione di Adobe Experience Manager.
