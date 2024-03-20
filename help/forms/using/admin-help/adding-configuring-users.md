---
title: Aggiunta e configurazione di utenti
description: Le impostazioni Gestione utente nella console di amministrazione consentono di creare o eliminare utenti e configurare altre impostazioni utente.
contentOwner: admin
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
exl-id: 50eea35d-d844-4f4b-9cbe-7d84bd6b1e3b
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1727'
ht-degree: 0%

---

# Aggiunta e configurazione di utenti {#adding-and-configuring-users}

Le informazioni di utenti e gruppi vengono conservate in un sistema di storage di terze parti, ad esempio una directory LDAP. Gestione utenti non scrive sul sistema di storage di terze parti. Gestione utenti sincronizza invece le informazioni su utenti e gruppi con il proprio database

## Creare un utente {#create-a-user}

Quando crei degli utenti, puoi aggiungerli ai gruppi e assegnare loro ruoli.

1. Nella console di amministrazione, fai clic su **[!UICONTROL Impostazioni > Gestione utente > Utenti e gruppi]** e fai clic su **[!UICONTROL Nuovo utente]**. .
1. Sotto **[!UICONTROL Impostazioni generali]**, fornire le informazioni richieste e quindi fare clic su **[!UICONTROL Successivo]**. Per informazioni dettagliate sulle impostazioni, consulta [Impostazioni utente](adding-configuring-users.md#user-settings).
1. (Facoltativo) Per aggiungere l’utente a un gruppo, fai clic su **[!UICONTROL Trova Gruppi]** ed eseguire le seguenti operazioni:

   * In **[!UICONTROL Trova]** digitare tutto o parte del nome del gruppo.
   * Seleziona il dominio da cercare, seleziona il numero di elementi da visualizzare e fai clic su **[!UICONTROL Trova]**.
   * (Facoltativo) Per visualizzare i dettagli del gruppo, selezionare il nome del gruppo e quindi fare clic su **[!UICONTROL OK]** per tornare alla pagina dei risultati della ricerca.
   * Selezionare la casella di controllo relativa al gruppo e fare clic su **[!UICONTROL OK]**.
   * Fai clic su **[!UICONTROL Avanti]**.

1. (Facoltativo) Per assegnare ruoli all’utente, fai clic su **[!UICONTROL Trova Ruoli]**, selezionare la casella di controllo relativa ai ruoli da assegnare e quindi fare clic su **[!UICONTROL OK]**.
1. Clic **[!UICONTROL Fine]**.

   >[!NOTE]
   >
   >Se riscontri problemi di accesso con l’utente, consulta [L’utente di AEM Forms su JEE non riesce ad accedere ad AEM Forms sul lato OSGi](https://helpx.adobe.com/aem-forms/kb/AEM-users-fails-to-login.html).

## Impostazioni utente {#user-settings}

Specificare le impostazioni seguenti quando si crea o si modifica un utente.

**Nome canonico:** (Obbligatorio) Identificatore univoco dell’utente. Ogni utente e gruppo di un dominio deve avere un nome canonico univoco. Selezionare la casella di controllo Generato dal sistema per consentire a Gestione utenti di assegnare un valore univoco oppure deselezionare la casella di controllo e specificare un valore personalizzato per il Nome canonico.

Evita di usare i caratteri di sottolineatura (_) nei nomi canonici, ad esempio, `sample_user`. Quando si cercano gli utenti in base al loro nome canonico, quelli contenenti caratteri di sottolineatura non vengono restituiti.

**Nome:** (Obbligatorio) Nome dell’utente

**Cognome** (Obbligatorio) Cognome dell’utente

**Nome comune:** Nome completo o nome visualizzato dell&#39;utente. Ad esempio, se Nome = Gloria e Cognome = Rios, allora Nome comune = Gloria Rios.

**E-mail:** Indirizzo e-mail dell’utente

**Telefono:** Numero di telefono dell&#39;utente

**Descrizione:** Descrizione facoltativa. Utilizza questo campo in base alle esigenze della tua organizzazione.

**Indirizzo:** Indirizzo e-mail dell&#39;utente

**Organizzazione:** Organizzazione a cui appartiene l&#39;utente

**Alias e-mail:** Alias e-mail dell’utente. Separa gli alias e-mail con virgole.

**Dominio:** Dominio a cui appartiene l&#39;utente

**Lingua:** Impostazioni internazionali ISO dell&#39;utente

**Chiave calendario aziendale:** Consente di mappare un calendario aziendale a un utente, in base al valore di questa impostazione. I calendari aziendali definiscono i giorni lavorativi e non lavorativi. I moduli AEM possono utilizzare i calendari aziendali per calcolare le date e le ore future per eventi quali promemoria, scadenze e inoltri per moderazione. Il modo in cui si assegnano le chiavi del calendario aziendale agli utenti dipende dal fatto che si utilizzi un dominio enterprise, locale o ibrido. (vedere [Aggiunta di domini](/help/forms/using/admin-help/adding-domains.md#adding-domains).)

Se si utilizza un dominio locale o ibrido, le informazioni relative agli utenti vengono memorizzate solo nel database Gestione utenti. Per questi utenti, impostare la chiave del calendario aziendale su una stringa. Quindi mappa la chiave del calendario aziendale (la stringa) su un calendario aziendale nel flusso di lavoro di Forms.

Se si utilizza un dominio enterprise, le informazioni sugli utenti risiedono in un sistema di storage di terze parti, ad esempio una directory LDAP. Gestione utenti sincronizza le informazioni utente dalla directory con il database Gestione utenti. Questa funzione consente di mappare una chiave del calendario aziendale a un campo nella directory LDAP. Si consideri ad esempio uno scenario in cui ogni record utente nella directory contiene un campo paese e si desidera assegnare calendari aziendali in base al paese in cui si trova l&#39;utente. In questo caso, specificare il nome del campo del paese come valore per l&#39;impostazione della chiave del calendario aziendale. È quindi possibile mappare le chiavi del calendario aziendale, ovvero i valori definiti per il campo Paese nell&#39;elenco LDAP, ai calendari aziendali nel flusso di lavoro dei moduli.

Per ulteriori informazioni sui calendari aziendali, tra cui le modalità di mapping delle chiavi del calendario aziendale ai calendari aziendali, vedere [Configurazione dei calendari aziendali](/help/forms/using/admin-help/configuring-business-calendars.md#configuring-business-calendars).

Limita il nome a meno di 53 caratteri. Un nome più breve consente di evitare problemi durante la visualizzazione della chiave del calendario aziendale nelle pagine Gestione processi della console di amministrazione.

**ID utente:** (Obbligatorio) ID utente utilizzato dall’utente per accedere. L’ID utente non distingue tra maiuscole e minuscole e deve essere univoco in tutto il dominio.

Nei domini enterprise, utilizza un attributo non DN come ID utente, in quanto il DN di un utente può cambiare se si sposta in un&#39;altra parte dell&#39;organizzazione. Questa impostazione dipende dal server delle directory. Il valore è `objectGUID` per Active Directory 2003, `nsuniqueID` per Sun™ One e `guid` per eDirectory.

Assicurati che l’ID utente sia univoco. Non utilizzarne uno che è stato assegnato a un utente eliminato.

I moduli AEM non sono in grado di distinguere tra account utente con ID utente e password identici ma appartenenti a domini diversi. Per evitare questo problema, non creare account con lo stesso ID utente su più domini.

Quando si utilizza SQL Server come database, non è possibile creare un ID utente che superi i 255 caratteri.

Quando si utilizza MySQL, l&#39;ID utente può contenere caratteri estesi. Tuttavia, quando si effettua un confronto tra due stringhe, come abcde e âbcdè, queste vengono considerate uguali. Ad esempio, durante la sincronizzazione, se al database è stato aggiunto un nuovo utente, viene eseguito un confronto per verificare se nel database esiste un utente con lo stesso ID utente. Se utente *abcde* esiste nel database quando il nuovo utente *âbcdè* è stato aggiunto, il confronto non è in grado di distinguere tra i due nomi. Si presume che l&#39;utente esista nel database e che il nuovo utente venga ignorato e non aggiunto.

Evita di creare nomi utente che iniziano con un cancelletto (#). L&#39;esecuzione di ricerche di attività non restituisce alcun risultato per tali nomi utente. (vedere [Utilizzo delle attività](/help/forms/using/admin-help/tasks.md#working-with-tasks).)

**Password e conferma password:** Password utilizzata dall&#39;utente per accedere. Deve contenere almeno otto caratteri. Non è richiesta una password per un utente che fa parte di un dominio ibrido.

## Visualizzare i dettagli relativi a un utente {#view-details-about-a-user}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Utenti e gruppi.
1. Specificare le informazioni per restringere la ricerca e, nell&#39;elenco In, selezionare Utenti e quindi fare clic su Trova. I risultati della ricerca sono elencati nella parte inferiore della pagina. È possibile ordinare l&#39;elenco facendo clic su una delle intestazioni di colonna.
1. Fai clic sul nome dell’utente per visualizzare i dettagli relativi a. Nella pagina Modifica utente sono visualizzati i dettagli dell’utente riportati di seguito:

   * Informazioni generali sull’identificazione, ad esempio nome, e-mail, indirizzo, dominio e organizzazione
   * Ruoli assegnati all&#39;utente
   * Gruppi di cui l&#39;utente è membro

## Modificare la password per un utente locale {#change-the-password-for-a-local-user}

1. Nella console di amministrazione, fai clic su **[!UICONTROL Impostazioni > Gestione utente > Utenti e gruppi]**.
1. Specifica le informazioni per restringere la ricerca di un utente specifico e fai clic su **[!UICONTROL Trova]**. I risultati della ricerca sono elencati nella parte inferiore della pagina. È possibile ordinare l&#39;elenco facendo clic su una delle intestazioni di colonna.
1. Fai clic sul nome dell’utente e quindi su **[!UICONTROL Cambia password]**.
1. Digitare e confermare la nuova password, quindi fare clic su **[!UICONTROL OK]**. La password deve contenere almeno otto caratteri.

## Modificare le proprietà di un utente {#edit-a-user-s-properties}

1. Nella console di amministrazione, fai clic su **[!UICONTROL Impostazioni > Gestione utente > Utenti e gruppi]**.
1. Per trovare l&#39;utente da modificare, eseguire le operazioni seguenti:

   * In **[!UICONTROL Trova]** digitare i criteri di ricerca.
   * In **[!UICONTROL Utilizzo di]** elenco, seleziona **[!UICONTROL Nome]**, **[!UICONTROL E-mail]**, o **[!UICONTROL ID utente]**.
   * In **[!UICONTROL Nell’elenco]**, seleziona **[!UICONTROL Utenti]**.
   * Selezionare il dominio, selezionare il numero di elementi da visualizzare e quindi fare clic su **[!UICONTROL Trova]**.

1. Fai clic sull’utente da modificare.
1. Per un utente che fa parte di un dominio locale o ibrido, sulla **[!UICONTROL Dettaglio]** , modificare il **[!UICONTROL Impostazioni generali]** e **[!UICONTROL Impostazioni di accesso]** e fai clic su **[!UICONTROL Salva]**. Per informazioni dettagliate sulle impostazioni, consulta [Impostazioni utente](adding-configuring-users.md#user-settings). Non è possibile modificare le impostazioni generali e di accesso per un utente che appartiene a un dominio enterprise.
1. Per modificare le impostazioni di gruppo per l&#39;utente, fare clic su **[!UICONTROL Appartenenza al gruppo]** ed effettuare le seguenti operazioni:

   * Clic **[!UICONTROL Trova gruppo]** e completare le informazioni di ricerca.
   * Per aggiungere l&#39;utente a un nuovo gruppo, selezionare la casella di controllo relativa al gruppo e fare clic su **[!UICONTROL OK]** e quindi fare clic su **[!UICONTROL Salva]**.

   >[!NOTE]
   >
   >Gli utenti locali non possono essere aggiunti ai gruppi di directory. Tuttavia, gli utenti della directory possono essere aggiunti ai gruppi locali.

   * Per rimuovere l&#39;utente da un gruppo, selezionare la casella di controllo relativa al gruppo e fare clic su **[!UICONTROL Elimina]** e quindi fare clic su **[!UICONTROL Salva]**.

1. Per modificare i ruoli dell&#39;utente, fare clic su **[!UICONTROL Assegnazioni Ruolo]** ed effettuare le seguenti operazioni:

   * Per visualizzare un elenco di ruoli, fare clic su **[!UICONTROL Trova Ruoli]**.
   * Per aggiungere un ruolo, selezionare la casella di controllo relativa al ruolo, quindi fare clic su **[!UICONTROL OK]** e quindi fare clic su **[!UICONTROL Salva]**.
   * Per rimuovere un ruolo, selezionare la casella di controllo relativa al ruolo, quindi fare clic su **[!UICONTROL Annulla assegnazione]** e quindi fare clic su **[!UICONTROL Salva]**.

## Eliminare un utente {#delete-a-user}

1. Nella console di amministrazione, fai clic su **[!UICONTROL Impostazioni > Gestione utente > Utenti e gruppi]**.
1. Per trovare l&#39;utente da eliminare, eseguire le operazioni seguenti:

   * In **[!UICONTROL Trova]** digitare i criteri di ricerca.
   * In **[!UICONTROL Utilizzo di]** elenco, seleziona **[!UICONTROL Nome]**, **[!UICONTROL E-mail]**, o **[!UICONTROL ID utente]**.
   * In **[!UICONTROL Nell’elenco]**, seleziona **[!UICONTROL Utenti]**.
   * Selezionare il dominio, selezionare il numero di elementi da visualizzare e quindi fare clic su **[!UICONTROL Trova]**.

1. Selezionare la casella di controllo per l&#39;utente e fare clic su **[!UICONTROL Elimina]** e quindi fare clic su **[!UICONTROL OK]**.

>[!NOTE]
>
>AEM Forms su JEE consente inoltre agli utenti del componente aggiuntivo AEM Forms in esecuzione su un OSGi di essere riconosciuti come utenti AEM. Ciò è necessario per gli scenari in cui è necessario il single sign-on tra AEM Forms su JEE e il componente aggiuntivo AEM forms in esecuzione su un OSGi (ad esempio, area di lavoro di HTML). L’operazione di eliminazione sopra indicata rimuove un utente solo da AEM Forms su JEE. L’utente non viene eliminato dal componente aggiuntivo AEM Forms in esecuzione nell’ambiente OSGi. Tuttavia, qualsiasi tentativo di accesso effettuato dopo l’eliminazione dell’utente (un tentativo di accesso al server JEE per il componente aggiuntivo AEM Forms o al componente aggiuntivo AEM Forms nell’ambiente OSGi) viene negato.

## Crea gestore errori di accesso personalizzato {#create-custom-login-error-handler}

Se un utente senza i moduli AEM e le autorizzazioni CQ richiesti tenta di accedere alle seguenti applicazioni incorporate in CQ, viene reindirizzato alla pagina CQ 404 predefinita contenente la traccia degli errori:

* Soluzione per la gestione della corrispondenza
* Area di lavoro moduli AEM

  ***nota **: Flex Workspace è obsoleto per il rilascio di moduli AEM.*

* gestione moduli
* Reporting processi

CQ fornisce un meccanismo per sostituire il gestore jsp 404 predefinito.

Per informazioni dettagliate su come personalizzare la pagina di gestione degli errori, consulta [Personalizzazione delle pagine visualizzate dal gestore degli errori](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/customizing-errorhandler-pages.html?lang=en) nella documentazione di Adobe Experience Manager.
