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
1. In Impostazioni **** generali, fornite le informazioni necessarie, quindi fate clic su **[!UICONTROL Avanti]**. Per informazioni dettagliate sulle impostazioni, consultate Impostazioni [](adding-configuring-users.md#user-settings)utente.
1. (Facoltativo) Per aggiungere l’utente a un gruppo, fate clic su **[!UICONTROL Trova gruppi]** ed effettuate le seguenti operazioni:

   * Nella casella **[!UICONTROL Trova]** , digitate tutto o parte del nome del gruppo.
   * Selezionate il dominio da cercare, selezionate il numero di elementi da visualizzare e fate clic su **[!UICONTROL Trova]**.
   * (Facoltativo) Per visualizzare i dettagli del gruppo, selezionate il nome del gruppo, quindi fate clic su **[!UICONTROL OK]** per tornare alla pagina dei risultati della ricerca.
   * Selezionate la casella di controllo relativa al gruppo e fate clic su **[!UICONTROL OK]**.
   * Fai clic su **[!UICONTROL Avanti]**.

1. (Facoltativo) Per assegnare i ruoli all&#39;utente, fare clic su **[!UICONTROL Trova ruoli]**, selezionare la casella di controllo dei ruoli da assegnare, quindi fare clic su **[!UICONTROL OK]**.
1. Click **[!UICONTROL Finish]**.

   >[!NOTE]
   >
   >Se si verifica un problema di accesso con l’utente, consultate [AEM Forms su JEE user (utente JEE) non riesce a effettuare l’accesso  AEM Forms su OSGi lato](https://helpx.adobe.com/aem-forms/kb/AEM-users-fails-to-login.html).

## Impostazioni utente {#user-settings}

Specificate le seguenti impostazioni quando create o modificate un utente.

**Nome canonico:** (Obbligatorio) Identificatore univoco per l’utente. Ogni utente e gruppo in un dominio deve avere un nome canonico univoco. Selezionate la casella di controllo Sistema generato per consentire a Gestione utente di assegnare un valore univoco, oppure deselezionate la casella di controllo e specificate un valore personalizzato per il Nome canonico.

Evitare di utilizzare caratteri di sottolineatura (_) nei nomi canonici, ad esempio `sample_user`. Quando cercate degli utenti in base al loro nome canonico, quelli che contengono caratteri di sottolineatura non vengono restituiti.

**Nome:** (Obbligatorio) Nome specificato dall&#39;utente

**Cognome:** (Obbligatorio) Cognome utente

**Nome comune:** Nome completo o nome visualizzato per l’utente. Ad esempio, se Nome = Gloria e Cognome = Rios, Nome comune = Gloria Rios.

**E-mail:** Indirizzo e-mail dell’utente

**Telefono:** Numero di telefono dell’utente

**Descrizione:** Descrizione facoltativa. Utilizzate questo campo in base alle esigenze della vostra organizzazione.

**Indirizzo:** Indirizzo postale dell&#39;utente

**Organizzazione:** Organizzazione a cui appartiene l&#39;utente

**Alias e-mail:** Alias e-mail dell’utente. Separate gli alias e-mail con virgole.

**Dominio:** Dominio a cui appartiene l&#39;utente

**Impostazioni internazionali:** Impostazioni internazionali ISO dell&#39;utente

**Chiave calendario aziendale:** Consente di mappare un calendario aziendale a un utente, in base al valore di questa impostazione. I calendari aziendali definiscono i giorni lavorativi e non lavorativi. AEM moduli possono utilizzare calendari aziendali per calcolare date e ore future per eventi quali promemoria, scadenze ed escalation. Il modo in cui assegnate le chiavi del calendario aziendale agli utenti dipende dal dominio Enterprise, locale o ibrido utilizzato. (Vedere [Aggiunta di domini](/help/forms/using/admin-help/adding-domains.md#adding-domains).)

Se utilizzate un dominio locale o ibrido, le informazioni sugli utenti vengono memorizzate solo nel database Gestione utente. Per questi utenti, impostate la chiave del calendario aziendale su una stringa. Quindi mappare la chiave del calendario aziendale (la stringa) su un calendario aziendale nel flusso di lavoro dei moduli.

Se utilizzate un dominio Enterprise, le informazioni sugli utenti risiedono in un sistema di storage di terze parti, ad esempio una directory LDAP. Gestione utente sincronizza le informazioni utente dalla directory con il database Gestione utente. Questa funzione consente di mappare una chiave del calendario aziendale su un campo presente nella directory LDAP. Ad esempio, si consideri uno scenario in cui ogni record utente nella directory contiene un campo paese e si desidera assegnare calendari aziendali in base al paese in cui si trova l&#39;utente. In questo caso, si specifica il nome del campo del paese come valore per l&#39;impostazione Chiave del calendario aziendale. È quindi possibile mappare le chiavi del calendario aziendale (i valori definiti per il campo del paese nella directory LDAP) ai calendari aziendali nel flusso di lavoro dei moduli.

Per ulteriori informazioni sui calendari aziendali, inclusa la modalità di mappatura delle chiavi del calendario aziendale ai calendari aziendali, vedere [Configurazione dei calendari](/help/forms/using/admin-help/configuring-business-calendars.md#configuring-business-calendars)aziendali.

Limita il nome a meno di 53 caratteri. Un nome più breve consente di evitare problemi durante la visualizzazione della chiave del calendario aziendale nelle pagine Gestione processi nella console di amministrazione.

**ID utente:** (Obbligatorio) ID utente utilizzato dall&#39;utente per effettuare l&#39;accesso. L&#39;ID utente non fa distinzione tra maiuscole e minuscole e deve essere univoco nel dominio.

Nei domini enterprise, utilizzate un attributo non DN come ID utente perché il DN di un utente può cambiare se si sposta in un&#39;altra parte dell&#39;organizzazione. Questa impostazione dipende dal server di directory. Il valore è `objectGUID` per Active Directory 2003, `nsuniqueID` per Sun™ One e `guid` per eDirectory.

Accertatevi che l&#39;ID utente sia univoco. Non usate uno assegnato a un utente eliminato.

AEM moduli non possono distinguere tra account utente con ID utente e password identici ma appartenenti a domini diversi. Per evitare questo problema, non create account con lo stesso ID utente su più domini.

Quando utilizzate SQL Server come database, non potete creare un ID utente che superi i 255 caratteri.

Quando si utilizza MySQL, l&#39;ID utente può contenere caratteri estesi. Tuttavia, quando si effettua un confronto tra due stringhe, come abcde e âbcdè, esse sono considerate uguali. Ad esempio, durante la sincronizzazione, se un nuovo utente è stato aggiunto al database, viene effettuato un confronto per verificare se nel database esiste un utente con lo stesso ID utente. Se nel database esiste già un *codice utente* con l&#39;aggiunta del nuovo utente *âbcdè* , il confronto non può distinguere tra i due nomi. Si presume che l&#39;utente esista già nel database e che il nuovo utente sia ignorato e non aggiunto.

Evitare di creare nomi utente che iniziano con un simbolo cancelletto (#). L&#39;esecuzione delle ricerche di attività non restituisce alcun risultato per tali nomi utente. (See [Working with tasks](/help/forms/using/admin-help/tasks.md#working-with-tasks).)

**Password e conferma password:** Password utilizzata dall&#39;utente per effettuare l&#39;accesso. Deve contenere almeno otto caratteri. Una password non è necessaria per un utente che fa parte di un dominio ibrido.

## Visualizzazione dei dettagli su un utente {#view-details-about-a-user}

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Utenti e gruppi.
1. Specificate le informazioni per limitare la ricerca e, nell’elenco In, selezionate Utenti e fate clic su Trova. I risultati della ricerca sono elencati nella parte inferiore della pagina. Potete ordinare l’elenco facendo clic su una delle intestazioni di colonna.
1. Fate clic sul nome dell&#39;utente per visualizzare i dettagli. Nella pagina Modifica utente sono visualizzati i dettagli seguenti sull’utente:

   * Informazioni generali di identificazione, quali nome, indirizzo e-mail, dominio e organizzazione
   * Ruoli assegnati all’utente
   * Gruppi di cui l’utente è membro

## Modificare la password di un utente locale {#change-the-password-for-a-local-user}

1. Nella console di amministrazione, fate clic su **[!UICONTROL Impostazioni > Gestione utente > Utenti e gruppi]**.
1. Specificate le informazioni per limitare la ricerca di un particolare utente e fate clic su **[!UICONTROL Trova]**. I risultati della ricerca sono elencati nella parte inferiore della pagina. Potete ordinare l’elenco facendo clic su una delle intestazioni di colonna.
1. Fate clic sul nome dell’utente e quindi su **[!UICONTROL Cambia password]**.
1. Digitare e confermare la nuova password, quindi fare clic su **[!UICONTROL OK]**. La password deve contenere almeno otto caratteri.

## Modificare le proprietà di un utente {#edit-a-user-s-properties}

1. Nella console di amministrazione, fate clic su **[!UICONTROL Impostazioni > Gestione utente > Utenti e gruppi]**.
1. Per trovare l’utente da modificare, effettuate le seguenti operazioni:

   * Nella casella **[!UICONTROL Trova]** , digitate i criteri di ricerca.
   * Nell&#39;elenco **[!UICONTROL Uso]** , selezionare **[!UICONTROL Nome]**, **[!UICONTROL E-mail]** o ID **** utente.
   * Nell&#39;elenco **[!UICONTROL In, selezionare]** Utenti ****.
   * Selezionate il dominio, selezionate il numero di elementi da visualizzare, quindi fate clic su **[!UICONTROL Trova]**.

1. Fate clic sull’utente da modificare.
1. Per un utente che fa parte di un dominio locale o ibrido, nella scheda **[!UICONTROL Dettagli]** , modificate le impostazioni **** Generali e le impostazioni **[!UICONTROL di]** accesso e fate clic su **[!UICONTROL Salva]**. Per informazioni dettagliate sulle impostazioni, consultate Impostazioni [](adding-configuring-users.md#user-settings)utente. Non potete modificare le impostazioni generali e di accesso per un utente appartenente a un dominio Enterprise.
1. Per modificare le impostazioni del gruppo per l’utente, fate clic sulla scheda Appartenenza **[!UICONTROL al]** gruppo ed effettuate le seguenti operazioni:

   * Fate clic su **[!UICONTROL Trova gruppo]** e completate le informazioni di ricerca.
   * Per aggiungere l’utente a un nuovo gruppo, selezionate la casella di controllo del gruppo, fate clic su **[!UICONTROL OK]**, quindi su **[!UICONTROL Salva]**.

   >[!NOTE]
   >
   >Gli utenti locali non possono essere aggiunti ai gruppi di directory. Tuttavia, gli utenti della directory possono essere aggiunti ai gruppi locali.

   * Per rimuovere l’utente da un gruppo, selezionate la casella di controllo del gruppo, fate clic su **[!UICONTROL Elimina]**, quindi su **[!UICONTROL Salva]**.


1. Per modificare i ruoli dell&#39;utente, fate clic sulla scheda Assegnazioni **** ruoli ed effettuate le seguenti operazioni:

   * Per visualizzare un elenco dei ruoli, fare clic su **[!UICONTROL Trova ruoli]**.
   * Per aggiungere un ruolo, selezionate la casella di controllo relativa al ruolo, fate clic su **[!UICONTROL OK]** e quindi su **[!UICONTROL Salva]**.
   * Per rimuovere un ruolo, selezionate la casella di controllo relativa al ruolo, fate clic su **[!UICONTROL Annulla assegnazione]**, quindi fate clic su **[!UICONTROL Salva]**.

## Eliminare un utente {#delete-a-user}

1. Nella console di amministrazione, fate clic su **[!UICONTROL Impostazioni > Gestione utente > Utenti e gruppi]**.
1. Per trovare l&#39;utente da eliminare, eseguire le operazioni seguenti:

   * Nella casella **[!UICONTROL Trova]** , digitate i criteri di ricerca.
   * Nell&#39;elenco **[!UICONTROL Uso]** , selezionare **[!UICONTROL Nome]**, **[!UICONTROL E-mail]** o ID **** utente.
   * Nell&#39;elenco **[!UICONTROL In, selezionare]** Utenti ****.
   * Selezionate il dominio, selezionate il numero di elementi da visualizzare, quindi fate clic su **[!UICONTROL Trova]**.

1. Selezionate la casella di controllo dell’utente, fate clic su **[!UICONTROL Elimina]**, quindi su **[!UICONTROL OK]**.

>[!NOTE]
>
> AEM Forms su JEE consente inoltre agli utenti del componente aggiuntivo AEM dei moduli in esecuzione su un OSGi di essere riconosciuti come utenti AEM. Questo è richiesto per gli scenari in cui è richiesto il single sign-on tra  AEM Forms su JEE e il componente aggiuntivo AEM in esecuzione su un OSGi (ad esempio, area di lavoro HTML). L&#39;operazione di eliminazione di cui sopra rimuove un utente solo da  AEM Forms su JEE. L&#39;utente non viene eliminato  componente aggiuntivo AEM Forms in esecuzione nell&#39;ambiente OSGi. Tuttavia, ogni tentativo di accesso effettuato dopo l’eliminazione dell’utente (un tentativo di accesso a  server JEE del componente aggiuntivo AEM Forms o  componente aggiuntivo AEM Forms nell’ambiente OSGi) viene negato.

## Crea gestore errori di login personalizzato {#create-custom-login-error-handler}

Se un utente senza i moduli AEM e le autorizzazioni CQ richiesti tenta di accedere alle seguenti applicazioni incorporate in CQ, viene reindirizzato alla pagina CQ 404 predefinita contenente la traccia di errore:

* Soluzione per la gestione della corrispondenza
* Area di lavoro moduli AEM

   ***nota **: Flex Workspace è obsoleto per AEM rilascio di moduli.*

* Forms Manager
* Reporting processi

CQ fornisce un meccanismo per ignorare l&#39;jsp del gestore 404 predefinito.

Per informazioni dettagliate su come personalizzare la pagina di gestione degli errori, vedere [Personalizzazione delle pagine mostrate dal gestore](https://docs.adobe.com/docs/en/cq/current/developing/customizing_error_handler_pages.html) errori nella documentazione di Adobe Experience Manager.
