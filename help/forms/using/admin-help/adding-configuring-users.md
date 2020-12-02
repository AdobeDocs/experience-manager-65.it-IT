---
title: 'Aggiunta e configurazione di utenti '
seo-title: 'Aggiunta e configurazione di utenti '
description: Le impostazioni di gestione utenti nella console di amministrazione consentono di creare o eliminare utenti e di configurare altre impostazioni utente.
seo-description: Le impostazioni di gestione utenti nella console di amministrazione consentono di creare o eliminare utenti e di configurare altre impostazioni utente.
uuid: fe650cdb-7d0d-4f38-9899-e5349559ed32
contentOwner: admin
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
discoiquuid: 20ca99e3-4843-4254-b3e9-0255cc752363
translation-type: tm+mt
source-git-commit: a929252a13f66da8ac3e52aea0655b12bdd1425f
workflow-type: tm+mt
source-wordcount: '1763'
ht-degree: 0%

---


# Aggiunta e configurazione di utenti {#adding-and-configuring-users}

Le informazioni su utenti e gruppi vengono conservate in un sistema di storage di terze parti, ad esempio una directory LDAP. Gestione utente non scrive nel sistema di storage di terze parti. Gestione utente sincronizza invece le informazioni utente e gruppo con il proprio database

## Creare un utente {#create-a-user}

Quando create degli utenti, potete aggiungerli ai gruppi e assegnare loro i ruoli.

1. Nella console di amministrazione, fate clic su **[!UICONTROL Impostazioni > Gestione utente > Utenti e gruppi]**, quindi fate clic su **[!UICONTROL Nuovo utente]**.
.
1. In **[!UICONTROL Impostazioni generali]**, fornire le informazioni necessarie, quindi fare clic su **[!UICONTROL Next]**. Per informazioni dettagliate sulle impostazioni, vedere [Impostazioni utente](adding-configuring-users.md#user-settings).
1. (Facoltativo) Per aggiungere l&#39;utente a un gruppo, fare clic su **[!UICONTROL Trova gruppi]** ed effettuare le seguenti operazioni:

   * Nella casella **[!UICONTROL Trova]**, digitare tutto o parte del nome del gruppo.
   * Selezionare il dominio da cercare, selezionare il numero di elementi da visualizzare e fare clic su **[!UICONTROL Trova]**.
   * (Facoltativo) Per visualizzare i dettagli del gruppo, selezionate il nome del gruppo, quindi fate clic su **[!UICONTROL OK]** per tornare alla pagina dei risultati della ricerca.
   * Selezionare la casella di controllo del gruppo e fare clic su **[!UICONTROL OK]**.
   * Fai clic su **[!UICONTROL Avanti]**.

1. (Facoltativo) Per assegnare i ruoli all&#39;utente, fare clic su **[!UICONTROL Trova ruoli]**, selezionare la casella di controllo dei ruoli da assegnare, quindi fare clic su **[!UICONTROL OK]**.
1. Fare clic su **[!UICONTROL Fine]**.

   >[!NOTE]
   >
   >Se si verifica un problema di accesso con l&#39;utente, vedere [ AEM Forms su un utente JEE non riesce ad accedere  AEM Forms su OSGi side](https://helpx.adobe.com/aem-forms/kb/AEM-users-fails-to-login.html).

## Impostazioni utente {#user-settings}

Specificate le seguenti impostazioni quando create o modificate un utente.

**Nome canonico:** (obbligatorio) Identificatore univoco per l’utente. Ogni utente e gruppo in un dominio deve avere un nome canonico univoco. Selezionate la casella di controllo Sistema generato per consentire a Gestione utente di assegnare un valore univoco, oppure deselezionate la casella di controllo e specificate un valore personalizzato per il Nome canonico.

Evitare di utilizzare caratteri di sottolineatura (_) nei nomi canonici, ad esempio `sample_user`. Quando cercate degli utenti in base al loro nome canonico, quelli che contengono caratteri di sottolineatura non vengono restituiti.

**Nome:** (obbligatorio) nome specificato dall&#39;utente

**Cognome:** (obbligatorio)

**Nome comune: nome** completo o nome visualizzato per l’utente. Ad esempio, se Nome = Gloria e Cognome = Rios, Nome comune = Gloria Rios.

**E-mail:indirizzo e-mail** dell&#39;utente

**Telefono:numero di telefono dell&#39;** utente

**Descrizione:descrizione** facoltativa. Utilizzate questo campo in base alle esigenze della vostra organizzazione.

**Indirizzo:indirizzo** postale dell&#39;utente

**Organizzazione:** organizzazione a cui appartiene l&#39;utente

**Alias e-mail:alias e-mail** dell&#39;utente. Separate gli alias e-mail con virgole.

**Dominio:** Dominio a cui appartiene l&#39;utente

**Impostazioni internazionali:impostazione internazionale ISO dell&#39;** utente

**Chiave calendario aziendale:** consente di mappare un calendario aziendale a un utente, in base al valore di questa impostazione. I calendari aziendali definiscono i giorni lavorativi e non lavorativi. AEM moduli possono utilizzare calendari aziendali per calcolare date e ore future per eventi quali promemoria, scadenze ed escalation. Il modo in cui assegnate le chiavi del calendario aziendale agli utenti dipende dal dominio Enterprise, locale o ibrido utilizzato. (Vedere [Aggiunta di domini](/help/forms/using/admin-help/adding-domains.md#adding-domains).)

Se utilizzate un dominio locale o ibrido, le informazioni sugli utenti vengono memorizzate solo nel database Gestione utente. Per questi utenti, impostate la chiave del calendario aziendale su una stringa. Quindi mappare la chiave del calendario aziendale (la stringa) su un calendario aziendale nel flusso di lavoro dei moduli.

Se utilizzate un dominio Enterprise, le informazioni sugli utenti risiedono in un sistema di storage di terze parti, ad esempio una directory LDAP. Gestione utente sincronizza le informazioni utente dalla directory con il database Gestione utente. Questa funzione consente di mappare una chiave del calendario aziendale su un campo presente nella directory LDAP. Ad esempio, si consideri uno scenario in cui ogni record utente nella directory contiene un campo paese e si desidera assegnare calendari aziendali in base al paese in cui si trova l&#39;utente. In questo caso, si specifica il nome del campo del paese come valore per l&#39;impostazione Chiave del calendario aziendale. È quindi possibile mappare le chiavi del calendario aziendale (i valori definiti per il campo del paese nella directory LDAP) ai calendari aziendali nel flusso di lavoro dei moduli.

Per ulteriori informazioni sui calendari aziendali, comprese le modalità di mappatura delle chiavi del calendario aziendale ai calendari aziendali, vedere [Configurazione dei calendari aziendali](/help/forms/using/admin-help/configuring-business-calendars.md#configuring-business-calendars).

Limita il nome a meno di 53 caratteri. Un nome più breve consente di evitare problemi durante la visualizzazione della chiave del calendario aziendale nelle pagine Gestione processi nella console di amministrazione.

**ID utente:** (obbligatorio) ID utente utilizzato dall’utente per effettuare l’accesso. L&#39;ID utente non fa distinzione tra maiuscole e minuscole e deve essere univoco nel dominio.

Nei domini enterprise, utilizzate un attributo non DN come ID utente perché il DN di un utente può cambiare se si sposta in un&#39;altra parte dell&#39;organizzazione. Questa impostazione dipende dal server di directory. Il valore è `objectGUID` per Active Directory 2003, `nsuniqueID` per Sun™ One e `guid` per eDirectory.

Accertatevi che l&#39;ID utente sia univoco. Non usate uno assegnato a un utente eliminato.

AEM moduli non possono distinguere tra account utente con ID utente e password identici ma appartenenti a domini diversi. Per evitare questo problema, non create account con lo stesso ID utente su più domini.

Quando utilizzate SQL Server come database, non potete creare un ID utente che superi i 255 caratteri.

Quando si utilizza MySQL, l&#39;ID utente può contenere caratteri estesi. Tuttavia, quando si effettua un confronto tra due stringhe, come abcde e âbcdè, esse sono considerate uguali. Ad esempio, durante la sincronizzazione, se un nuovo utente è stato aggiunto al database, viene effettuato un confronto per verificare se nel database esiste un utente con lo stesso ID utente. Se l&#39;utente *abcde* esiste già nel database quando viene aggiunto il nuovo utente *âbcdè*, il confronto non può distinguere tra i due nomi. Si presume che l&#39;utente esista già nel database e che il nuovo utente sia ignorato e non aggiunto.

Evitare di creare nomi utente che iniziano con un simbolo cancelletto (#). L&#39;esecuzione delle ricerche di attività non restituisce alcun risultato per tali nomi utente. (Vedere [Uso delle attività](/help/forms/using/admin-help/tasks.md#working-with-tasks).)

**Password e Conferma password:** password utilizzata dall&#39;utente per effettuare l&#39;accesso. Deve contenere almeno otto caratteri. Una password non è necessaria per un utente che fa parte di un dominio ibrido.

## Visualizza dettagli su un utente {#view-details-about-a-user}

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Utenti e gruppi.
1. Specificate le informazioni per limitare la ricerca e, nell’elenco In, selezionate Utenti e fate clic su Trova. I risultati della ricerca sono elencati nella parte inferiore della pagina. Potete ordinare l’elenco facendo clic su una delle intestazioni di colonna.
1. Fate clic sul nome dell&#39;utente per visualizzare i dettagli. Nella pagina Modifica utente sono visualizzati i dettagli seguenti sull’utente:

   * Informazioni generali di identificazione, quali nome, indirizzo e-mail, dominio e organizzazione
   * Ruoli assegnati all’utente
   * Gruppi di cui l’utente è membro

## Modificare la password di un utente locale {#change-the-password-for-a-local-user}

1. Nella console di amministrazione, fate clic su **[!UICONTROL Impostazioni > Gestione utente > Utenti e gruppi]**.
1. Specificate le informazioni per limitare la ricerca di un particolare utente e fate clic su **[!UICONTROL Trova]**. I risultati della ricerca sono elencati nella parte inferiore della pagina. Potete ordinare l’elenco facendo clic su una delle intestazioni di colonna.
1. Fate clic sul nome dell&#39;utente e quindi su **[!UICONTROL Cambia password]**.
1. Digitare e confermare la nuova password, quindi fare clic su **[!UICONTROL OK]**. La password deve contenere almeno otto caratteri.

## Modificare le proprietà di un utente {#edit-a-user-s-properties}

1. Nella console di amministrazione, fate clic su **[!UICONTROL Impostazioni > Gestione utente > Utenti e gruppi]**.
1. Per trovare l’utente da modificare, effettuate le seguenti operazioni:

   * Nella casella **[!UICONTROL Trova]** digitare i criteri di ricerca.
   * Nell&#39;elenco **[!UICONTROL Utilizzo di]**, selezionare **[!UICONTROL Nome]**, **[!UICONTROL E-mail]** o **[!UICONTROL ID utente]**.
   * In **[!UICONTROL Nell&#39;elenco]**, selezionare **[!UICONTROL Utenti]**.
   * Selezionare il dominio, selezionare il numero di elementi da visualizzare, quindi fare clic su **[!UICONTROL Trova]**.

1. Fate clic sull’utente da modificare.
1. Per un utente che fa parte di un dominio locale o ibrido, nella scheda **[!UICONTROL Dettagli]** modificare le **[!UICONTROL Impostazioni generali]** e **[!UICONTROL Impostazioni di accesso]**, quindi fare clic su **[!UICONTROL Salva]**. Per informazioni dettagliate sulle impostazioni, vedere [Impostazioni utente](adding-configuring-users.md#user-settings). Non potete modificare le impostazioni generali e di accesso per un utente appartenente a un dominio Enterprise.
1. Per modificare le impostazioni del gruppo per l&#39;utente, fare clic sulla scheda **[!UICONTROL Appartenenza al gruppo]** ed effettuare le seguenti operazioni:

   * Fare clic su **[!UICONTROL Trova gruppo]** e completare la ricerca.
   * Per aggiungere l&#39;utente a un nuovo gruppo, selezionare la casella di controllo del gruppo, fare clic su **[!UICONTROL OK]**, quindi fare clic su **[!UICONTROL Salva]**.

   >[!NOTE]
   >
   >Gli utenti locali non possono essere aggiunti ai gruppi di directory. Tuttavia, gli utenti della directory possono essere aggiunti ai gruppi locali.

   * Per rimuovere l&#39;utente da un gruppo, selezionate la casella di controllo del gruppo, fate clic su **[!UICONTROL Elimina]**, quindi su **[!UICONTROL Salva]**.


1. Per modificare i ruoli dell&#39;utente, fare clic sulla scheda **[!UICONTROL Assegnazioni ruoli]** ed effettuare le seguenti operazioni:

   * Per visualizzare un elenco dei ruoli, fare clic su **[!UICONTROL Trova ruoli]**.
   * Per aggiungere un ruolo, selezionare la casella di controllo relativa al ruolo, fare clic su **[!UICONTROL OK]**, quindi fare clic su **[!UICONTROL Salva]**.
   * Per rimuovere un ruolo, selezionare la casella di controllo relativa al ruolo, fare clic su **[!UICONTROL Annulla assegnazione]**, quindi fare clic su **[!UICONTROL Salva]**.

## Eliminare un utente {#delete-a-user}

1. Nella console di amministrazione, fate clic su **[!UICONTROL Impostazioni > Gestione utente > Utenti e gruppi]**.
1. Per trovare l&#39;utente da eliminare, eseguire le operazioni seguenti:

   * Nella casella **[!UICONTROL Trova]** digitare i criteri di ricerca.
   * Nell&#39;elenco **[!UICONTROL Utilizzo di]**, selezionare **[!UICONTROL Nome]**, **[!UICONTROL E-mail]** o **[!UICONTROL ID utente]**.
   * In **[!UICONTROL Nell&#39;elenco]**, selezionare **[!UICONTROL Utenti]**.
   * Selezionare il dominio, selezionare il numero di elementi da visualizzare, quindi fare clic su **[!UICONTROL Trova]**.

1. Selezionare la casella di controllo per l&#39;utente, fare clic su **[!UICONTROL Elimina]**, quindi fare clic su **[!UICONTROL OK]**.

>[!NOTE]
>
> AEM Forms su JEE consente inoltre agli utenti del componente aggiuntivo AEM dei moduli in esecuzione su un OSGi di essere riconosciuti come utenti AEM. Questo è richiesto per gli scenari in cui è richiesto il single sign-on tra  AEM Forms su JEE e il componente aggiuntivo AEM in esecuzione su un OSGi (ad esempio, area di lavoro HTML). L&#39;operazione di eliminazione di cui sopra rimuove un utente solo da  AEM Forms su JEE. L&#39;utente non viene eliminato  componente aggiuntivo AEM Forms in esecuzione nell&#39;ambiente OSGi. Tuttavia, ogni tentativo di accesso effettuato dopo l’eliminazione dell’utente (un tentativo di accesso a  server JEE del componente aggiuntivo AEM Forms o  componente aggiuntivo AEM Forms nell’ambiente OSGi) viene negato.

## Crea gestore di errori di login personalizzato {#create-custom-login-error-handler}

Se un utente senza i moduli AEM e le autorizzazioni CQ richiesti tenta di accedere alle seguenti applicazioni incorporate in CQ, viene reindirizzato alla pagina CQ 404 predefinita contenente la traccia di errore:

* Soluzione per la gestione della corrispondenza
* Area di lavoro moduli AEM

   ***nota **: Flex Workspace è obsoleto per AEM rilascio di moduli.*

* Forms Manager
* Reporting processi

CQ fornisce un meccanismo per ignorare l&#39;jsp del gestore 404 predefinito.

Per informazioni dettagliate su come personalizzare la pagina di gestione degli errori, vedere [Personalizzazione delle pagine mostrate dal gestore errori](https://docs.adobe.com/docs/en/cq/current/developing/customizing_error_handler_pages.html) nella documentazione Adobe Experience Manager.
