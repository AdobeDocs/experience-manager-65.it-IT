---
title: Aggiungere e configurare gli utenti
description: Le impostazioni Gestione utente nella console di amministrazione consentono di creare o eliminare utenti e configurare altre impostazioni utente.
contentOwner: admin
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
exl-id: 50eea35d-d844-4f4b-9cbe-7d84bd6b1e3b
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '1739'
ht-degree: 100%

---

# Aggiungere e configurare gli utenti {#adding-and-configuring-users}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Le informazioni di utenti e gruppi vengono gestite in un sistema di archiviazione di terze parti, ad esempio una directory LDAP. La Gestione utenti non scrive sul sistema di archiviazione di terze parti. Gestione utenti sincronizza invece le informazioni di utenti e gruppi con il proprio database

## Creare un utente {#create-a-user}

Quando crei degli utenti, puoi aggiungerli ai gruppi e assegnare loro ruoli.

1. Nella console di amministrazione, fai clic su **[!UICONTROL Impostazioni > Gestione utente > Utenti e gruppi]**, quindi su **[!UICONTROL Nuovo utente]**.
.
1. In **[!UICONTROL Impostazioni generali]**, fornisci le informazioni richieste, quindi fai clic su **[!UICONTROL Avanti]**. Per informazioni dettagliate sulle impostazioni, consulta [Impostazioni utente](adding-configuring-users.md#user-settings).
1. (Facoltativo) Per aggiungere l’utente a un gruppo, fai clic su **[!UICONTROL Trova gruppi]** ed esegui queste attività:

   * Nella casella **[!UICONTROL Trova]**, digita tutto o parte del nome del gruppo.
   * Seleziona il dominio in cui eseguire la ricerca, seleziona il numero di elementi da mostrare e fai clic su **[!UICONTROL Trova]**.
   * (Facoltativo) Per visualizzare i dettagli del gruppo, seleziona il nome del gruppo, quindi fai clic su **[!UICONTROL OK]** per tornare alla pagina dei risultati della ricerca.
   * Seleziona la casella di controllo per il gruppo e fai clic su **[!UICONTROL OK]**.
   * Fai clic su **[!UICONTROL Avanti]**.

1. (Facoltativo) Per assegnare ruoli all’utente, fai clic su **[!UICONTROL Trova ruoli]**, seleziona la casella di controllo relativa ai ruoli da assegnare e quindi fai clic su **[!UICONTROL OK]**.
1. Fai clic su **[!UICONTROL Fine]**.

   >[!NOTE]
   >
   >Se riscontri problemi di accesso con l’utente, consulta [L’utente AEM Forms su JEE non riesce ad accedere ad AEM Forms lato OSGi](ttps://helpx.adobe.com/it/aem-forms/kb/AEM-users-fails-to-login.html).

## Impostazioni utente {#user-settings}

Specifica le impostazioni seguenti quando crei o modifichi un utente.

**Nome canonico:** (obbligatorio) Identificatore univoco dell’utente. Ogni utente e gruppo di un dominio deve avere un nome canonico univoco. Seleziona la casella di controllo Generato dal sistema per consentire a Gestione utenti di assegnare un valore univoco oppure deseleziona la casella di controllo e specifica un valore personalizzato per il Nome canonico.

Evita di utilizzare caratteri di sottolineatura (_) nei nomi canonici, ad esempio `sample_user`. Durante la ricerca di utenti in base al loro nome canonico, quelli contenenti caratteri di sottolineatura non vengono restituiti.

**Nome:** (obbligatorio) nome dell’utente

**Cognome:** (obbligatorio) cognome dell’utente

**Nome comune:** nome completo o nome visualizzato dell’utente. Ad esempio, se Nome = Gloria e Cognome = Rios, allora Nome comune = Gloria Rios.

**E-mail:** indirizzo e-mail dell’utente

**Telefono:** numero di telefono dell’utente

**Descrizione:** descrizione facoltativa. Utilizza questo campo in base alle esigenze della tua organizzazione.

**Indirizzo:** indirizzo postale dell’utente

**Organizzazione:** organizzazione a cui appartiene l’utente

**Alias e-mail:** alias e-mail dell’utente. Separa gli alias e-mail con virgole.

**Dominio:** dominio a cui appartiene l’utente

**Impostazioni locali:** impostazioni locali ISO dell’utente

**Chiave calendario aziendale:** consente di mappare un calendario aziendale a un utente, in base al valore di questa impostazione. I calendari aziendali definiscono i giorni lavorativi e non lavorativi. AEM Forms può utilizzare i calendari aziendali per il calcolo di date e ore future per eventi quali promemoria, scadenze ed escalation. Il modo in cui assegni le chiavi del calendario aziendale agli utenti dipende dal fatto che utilizzi un dominio enterprise, locale o ibrido. (Consulta [Aggiungere domini](/help/forms/using/admin-help/adding-domains.md#adding-domains)).

Se utilizzi un dominio locale o ibrido, le informazioni relative agli utenti vengono memorizzate solo nel database di Gestione utenti. Per questi utenti, imposta la chiave del calendario aziendale su una stringa. Quindi, mappa la chiave del calendario aziendale (la stringa) su un calendario aziendale nel flusso di lavoro di Forms.

Se utilizzi un dominio Enterprise, le informazioni sugli utenti si trovano in un sistema di archiviazione di terze parti, ad esempio una directory LDAP. La Gestione utenti sincronizza le informazioni utente dalla directory con il database Gestione utenti. Questa funzione consente di mappare una chiave del calendario aziendale a un campo nella directory LDAP. Ad esempio, prendi in considerazione uno scenario in cui ogni record utente nella directory contiene un campo paese e desideri assegnare calendari aziendali in base al paese in cui si trova l’utente. In questo caso, specificare il nome del campo del paese come valore per l’impostazione della chiave del calendario aziendale. È quindi possibile mappare le chiavi del calendario aziendale, ovvero i valori definiti per il campo Paese nell’elenco LDAP, ai calendari aziendali in Forms Workflow.

Per ulteriori informazioni sui calendari aziendali, tra cui le modalità di mapping delle chiavi del calendario aziendale ai calendari aziendali, vedere [Configurazione dei calendari aziendali](/help/forms/using/admin-help/configuring-business-calendars.md#configuring-business-calendars).

Limitare il nome a meno di 53 caratteri. Un nome più breve consente di evitare problemi durante la visualizzazione della chiave del calendario aziendale nelle pagine Gestione processi della console di amministrazione.

**ID utente:** (obbligatorio) ID utente utilizzato dall’utente per accedere. L’ID utente non distingue tra maiuscole e minuscole e deve essere univoco in tutto il dominio.

Nei domini enterprise, utilizzare un attributo non DN come ID utente, in quanto il DN di un utente può cambiare se si sposta in un’altra parte dell’organizzazione. Questa impostazione dipende dal server delle directory. Il valore è `objectGUID` per Active Directory 2003, `nsuniqueID` per Sun™ One e `guid` per eDirectory.

Assicurarsi che il nome utente sia univoco. Non utilizzarne uno che è stato assegnato a un utente eliminato.

AEM Forms non è in grado di distinguere tra account utente con ID utente e password identici ma appartenenti a domini diversi. Per evitare questo problema, non creare account con lo stesso ID utente su più domini.

Quando si utilizza SQL Server come database, non è possibile creare un ID utente che superi i 255 caratteri.

Quando si utilizza MySQL, l’ID utente può contenere caratteri estesi. Tuttavia, quando si effettua un confronto tra due stringhe, come abcde e âbcdè, queste vengono considerate uguali. Ad esempio, durante la sincronizzazione, se al database è stato aggiunto un nuovo utente, viene eseguito un confronto per verificare se nel database esiste un utente con lo stesso ID utente. Se l’utente *abcde* esiste nel database quando viene aggiunto il nuovo utente *âbcdè*, il confronto non è in grado di distinguere i due nomi. Si presume che l’utente esista nel database e che il nuovo utente venga ignorato e non aggiunto.

Evitare di creare nomi utente che iniziano con un numero (#). L’esecuzione di ricerche di attività non restituisce alcun risultato per tali nomi utente. Vedere [Utilizzo delle attività](/help/forms/using/admin-help/tasks.md#working-with-tasks).

**Password e conferma password:** Password utilizzata dall’utente per accedere. Deve contenere almeno otto caratteri. Non è richiesta una password per un utente che fa parte di un dominio ibrido.

## Visualizzare i dettagli relativi a un utente {#view-details-about-a-user}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Utenti e gruppi.
1. Specificare le informazioni per restringere la ricerca e, nell’elenco In, selezionare Utenti e quindi fare clic su Trova. I risultati della ricerca sono elencati nella parte inferiore della pagina. Puoi ordinare l’elenco facendo clic su una delle intestazioni di colonna.
1. Fare clic sul nome dell’utente per visualizzare i dettagli. Nella pagina Modifica utente sono visualizzati i dettagli dell’utente riportati di seguito:

   * Informazioni generali sull’identificazione, ad esempio nome, e-mail, indirizzo, dominio e organizzazione
   * Ruoli assegnati all’utente
   * Gruppi a cui appartiene l’utente

## Modificare la password per un utente locale {#change-the-password-for-a-local-user}

1. Nella console di amministrazione, fare clic su **[!UICONTROL Impostazioni > Gestione utente > Utenti e gruppi]**.
1. Specificare le informazioni per restringere la ricerca di un utente specifico e fare clic su **[!UICONTROL Trova]**. I risultati della ricerca sono elencati nella parte inferiore della pagina. Puoi ordinare l’elenco facendo clic su una delle intestazioni di colonna.
1. Fare clic sul nome dell’utente e quindi su **[!UICONTROL Modifica password]**.
1. Digitare e confermare la nuova password, quindi fare clic su **[!UICONTROL OK]**. La password deve contenere almeno otto caratteri.

## Modificare le proprietà degli utenti {#edit-a-user-s-properties}

1. Nella console di amministrazione, fai clic su **[!UICONTROL Impostazioni > Gestione utente > Utenti e gruppi]**.
1. Per trovare l’utente da modificare, esegui le operazioni seguenti:

   * Nella casella **[!UICONTROL Trova]** digita i criteri di ricerca.
   * Nell’elenco **[!UICONTROL Utilizzo]** seleziona **[!UICONTROL Nome]**, **[!UICONTROL E-mail]** o **[!UICONTROL ID utente]**.
   * Nell’elenco **[!UICONTROL In]**, seleziona **[!UICONTROL Utenti]**.
   * Seleziona il dominio, il numero di elementi da visualizzare e quindi fai clic su **[!UICONTROL Trova]**.

1. Fai clic sull’utente da modificare.
1. Per un utente che fa parte di un dominio locale o ibrido, nella scheda **[!UICONTROL Dettagli]** modifica le **[!UICONTROL Impostazioni generali]** e le **[!UICONTROL Impostazioni di accesso]**, quindi fai clic su **[!UICONTROL Salva]**. Per informazioni dettagliate sulle impostazioni, consulta [Impostazioni utente](adding-configuring-users.md#user-settings). Non puoi modificare le impostazioni generali e di accesso per un utente che appartiene a un dominio Enterprise.
1. Per modificare le impostazioni del gruppo per l’utente, fai clic sulla scheda **[!UICONTROL Iscrizione al gruppo]** ed esegui le attività seguenti:

   * Fai clic su **[!UICONTROL Trova gruppo]** e completa le informazioni di ricerca.
   * Per aggiungere l’utente a un nuovo gruppo, seleziona la casella di controllo relativa al gruppo, fai clic su **[!UICONTROL OK]** e quindi su **[!UICONTROL Salva]**.

   >[!NOTE]
   >
   >Gli utenti locali non possono essere aggiunti ai gruppi di directory. Tuttavia, gli utenti della directory possono essere aggiunti ai gruppi locali.

   * Per rimuovere l’utente da un gruppo, seleziona la casella di controllo relativa al gruppo, fai clic su **[!UICONTROL Elimina]** e quindi su **[!UICONTROL Salva]**.

1. Per modificare i ruoli dell’utente, fai clic sulla scheda **[!UICONTROL Assegnazioni ruolo]** ed esegui le attività seguenti:

   * Per visualizzare un elenco di ruoli, fai clic su **[!UICONTROL Trova ruoli]**.
   * Per aggiungere un ruolo, seleziona la casella di controllo relativa al ruolo, fai clic su **[!UICONTROL OK]** e quindi su **[!UICONTROL Salva]**.
   * Per rimuovere un ruolo, seleziona la casella di controllo per il ruolo, fai clic su **[!UICONTROL Annulla assegnazione]** e quindi su **[!UICONTROL Salva]**.

## Eliminare un utente {#delete-a-user}

1. Nella console di amministrazione, fai clic su **[!UICONTROL Impostazioni > Gestione utenti > Utenti e gruppi]**.
1. Per trovare l’utente da eliminare, esegui le operazioni seguenti:

   * Nella casella **[!UICONTROL Trova]** digita i criteri di ricerca.
   * Nell’elenco **[!UICONTROL Utilizzo]** seleziona **[!UICONTROL Nome]**, **[!UICONTROL E-mail]** o **[!UICONTROL ID utente]**.
   * Nell’elenco **[!UICONTROL In]**, seleziona **[!UICONTROL Utenti]**.
   * Seleziona il dominio, il numero di elementi da visualizzare e quindi fai clic su **[!UICONTROL Trova]**.

1. Seleziona la casella di controllo per l’utente, fai clic su **[!UICONTROL Elimina]** e quindi su **[!UICONTROL OK]**.

>[!NOTE]
>
>AEM Forms su JEE consente inoltre agli utenti del componente aggiuntivo AEM Forms in esecuzione su un OSGi di essere riconosciuti come utenti AEM. È necessario per gli scenari in cui è richiesto il single sign-on tra AEM Forms su JEE e il componente aggiuntivo AEM Forms in esecuzione su un OSGi (ad esempio, l’area di lavoro di HTML). L’operazione di eliminazione sopra indicata rimuove un utente solo da AEM Forms su JEE. L’utente non viene eliminato dal componente aggiuntivo AEM Forms in esecuzione nell’ambiente OSGi. Tuttavia, qualsiasi tentativo di accesso effettuato dopo l’eliminazione dell’utente (un tentativo di accesso al componente aggiuntivo AEM Forms sul server JEE o al componente aggiuntivo AEM Forms nell’ambiente OSGi) viene negato.

## Crea gestore errori di accesso personalizzato {#create-custom-login-error-handler}

Se un utente senza le autorizzazioni AEM Forms e CQ richieste tenta di accedere alle seguenti applicazioni incorporate in CQ, viene reindirizzato alla pagina CQ 404 predefinita contenente la traccia degli errori:

* Soluzione di gestione della corrispondenza
* Area di lavoro di AEM Forms

  ***nota **: Flex Workspace è obsoleto per la versione di AEM Forms.*

* Gestione moduli
* Rapporti sui processi

CQ fornisce un meccanismo per sostituire il gestore jsp 404 predefinito.

Per informazioni dettagliate su come personalizzare la pagina di gestione degli errori, consulta [Personalizzazione delle pagine visualizzate dal Gestore degli errori](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/implementing/developing/platform/customizing-errorhandler-pages#) nella documentazione di Adobe Experience Manager.
