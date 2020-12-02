---
title: Gestione utenti Forms | Gestione dei dati utente
seo-title: Gestione utenti Forms | Gestione dei dati utente
description: Gestione utenti Forms | Gestione dei dati utente
uuid: 2b76b69f-6f3a-4f1a-a2a4-d39f5e529f75
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a88fc933-f1af-4798-b72f-10e7b0d2fd11
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 0%

---


# Gestione utenti Forms | Gestione dei dati utente {#forms-user-management-handling-user-data}

Gestione utente è un componente AEM Forms JEE  che consente di creare, gestire e autorizzare  utenti AEM Forms ad accedere  AEM Forms. La gestione utente utilizza i domini come directory per ottenere informazioni sugli utenti. Sono supportati i seguenti tipi di dominio:

**Domini** locali: Questo tipo di dominio non è connesso a un sistema di storage di terze parti. Al contrario, gli utenti e i gruppi vengono creati localmente e risiedono nel database Gestione utente. Le password vengono memorizzate localmente e l&#39;autenticazione viene eseguita utilizzando un database locale.

**Domini** ibridi: Questo tipo di dominio non è connesso a un sistema di storage di terze parti. Al contrario, gli utenti e i gruppi vengono creati localmente e risiedono nel database Gestione utente. A differenza dei domini locali, i domini ibridi utilizzano un provider di autenticazione esterno, che può essere LDAP, Kerberos, SAML o un provider di autenticazione personalizzato.

**Domini** Enterprise: Sono costituiti da utenti e gruppi che risiedono in un sistema di storage di terze parti, ad esempio una directory LDAP. Gestione utente non scrive nel sistema di storage di terze parti. Gestione utente sincronizza invece le informazioni utente e gruppo con il database Gestione utente. I domini Enterprise utilizzano anche un provider di autenticazione esterno, che può essere LDAP, Kerberos, SAML o un provider di autenticazione personalizzato.

<!-- Fix broken links For more information about how user management works and configured, see AEM Forms JEE administration help. -->

## Archivio dati utente {#user-data-and-data-stores}

La gestione utente memorizza i dati utente in un database, ad esempio My Sql,  Oracle, MS SQL Server e IBM DB2. Inoltre, ogni utente che ha eseguito l&#39;accesso almeno una volta nelle applicazioni Forms all&#39;AEM autore in `https://'[server]:[port]'lc`, viene creato AEM repository. Pertanto, la gestione degli utenti viene memorizzata nei seguenti archivi di dati:

* Database
* AEM repository
* Memorizzazione di terze parti come directory LDAP

>[!NOTE]
>
>I dati archiviati in archivi di terze parti non rientrano nell&#39;ambito di applicazione di questo documento. Contatta direttamente il fornitore di terze parti per gestire i dati utente in tali archivi.

### Database {#database}

La gestione utente memorizza i dati utente nelle seguenti tabelle di database:

<table>
 <tbody>
  <tr>
   <td>Tabella database</td>
   <td>Descrizione</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalEntity</code></td>
   <td><p>Memorizza informazioni sulle entità principali. Un'entità può essere un utente, un gruppo o un ruolo.</p> <p> </p> </td>
  </tr>
  <tr>
   <td><code>EdcPrincipalUserEntity</code></td>
   <td>Memorizza informazioni personali identificabili (PII) degli utenti. Contiene una voce per ogni utente dai domini locali, enterprise e ibridi.</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalLocalAccountEntity</code></p> <p><code class="code">EdcPrincipalLocalAccount
       </code>( database Oracle e MS SQL)</p> </td>
   <td>Memorizza i dati solo per gli utenti locali.</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalEmailAliasEntity</code></p> <p><code class="code">EdcPrincipalEmailAliasEn
       </code>( database Oracle e MS SQL)</p> </td>
   <td>Contiene voci di tutti gli utenti provenienti da domini locali, enterprise e ibridi. Contiene gli ID e-mail dell’utente.</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalGrpCtmntEntity</code></p> <p><code>EdcPrincipalGrpCtmntEnti</code> ( database Oracle e MS SQL)</p> </td>
   <td>Memorizza la mappatura tra utenti e gruppi.</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalRoleEntity</code></td>
   <td>Memorizza la mappatura tra ruoli e entità per utenti e gruppi.</td>
  </tr>
  <tr>
   <td><code>EdcPriResPrmEntity</code></td>
   <td>Memorizza la mappatura tra entità e autorizzazioni per utenti e gruppi.</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalMappingEntity</code></p> <p><code>EdcPrincipalMappingEntit</code> ( database Oracle e MS SQL)</p> </td>
   <td>Memorizza i valori degli attributi vecchi e nuovi corrispondenti a un'entità.<br /> </td>
  </tr>
 </tbody>
</table>

### AEM repository {#aem-repository}

I dati di gestione utenti per gli utenti che hanno eseguito almeno una volta l&#39;accesso alle applicazioni Forms in `https://'[server]:[port]'lc` vengono memorizzati anche AEM repository.

## Accesso ed eliminazione dei dati utente {#access-and-delete-user-data}

È possibile accedere ed esportare i dati di gestione utenti per gli utenti nei database di gestione utenti e AEM repository e, se necessario, eliminarli definitivamente.

### Database {#database-1}

Per esportare o eliminare i dati utente dal database di gestione utenti, è necessario connettersi al database utilizzando un client di database e individuare l&#39;ID principale in base ad alcuni PII dell&#39;utente. Ad esempio, per recuperare l&#39;ID principale di un utente utilizzando un ID di login, eseguite il seguente comando `select` nel database.

Nel comando `select`, sostituire il `<user_login_id>` con l&#39;ID di login dell&#39;utente di cui si desidera recuperare l&#39;ID principale.

```sql
select refprincipalid from EdcPrincipalUserEntity where uidstring = <user_login_id>
```

Una volta noto l’ID principale, potete esportare o eliminare i dati utente.

#### Esportare i dati utente {#export-user-data}

Eseguite i seguenti comandi del database per esportare i dati di gestione utente per un ID principale dalle tabelle del database. Nel comando `select`, sostituire `<principal_id>` con l&#39;ID principale dell&#39;utente di cui si desidera esportare i dati.

>[!NOTE]
>
>I seguenti comandi utilizzano i nomi delle tabelle del database nei database My SQL e IBM DB2. Quando eseguite questi comandi  database Oracle e MS SQL, sostituite i seguenti nomi di tabella nei comandi:
>
>* Sostituire `EdcPrincipalLocalAccountEntity` con `EdcPrincipalLocalAccount`
   >
   >
* Sostituire `EdcPrincipalEmailAliasEntity` con `EdcPrincipalEmailAliasEn`
   >
   >
* Sostituire `EdcPrincipalMappingEntity` con `EdcPrincipalMappingEntit`
   >
   >
* Sostituire `EdcPrincipalGrpCtmntEntity` con `EdcPrincipalGrpCtmntEnti`

>



```sql
Select * from EdcPrincipalLocalAccountEntity where refuserprincipalid in (Select id from EdcPrincipalUserEntity where refprincipalid in (Select id from EDCPRINCIPALENTITY where id='<principal_id>'));

Select * from EdcPrincipalEmailAliasEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalRoleEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPriResPrmEntity where refprinid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalUserEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalMappingEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalGrpCtmntEntity where refchildprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalEntity where id='<principal_id>';
```

#### Elimina dati utente {#delete-user-data}

Effettuate le seguenti operazioni per eliminare i dati di gestione utente per un ID entità dalle tabelle del database.

1. Eliminate i dati utente AEM repository, se applicabile, come descritto in [Elimina dati utente](/help/forms/using/user-management-handling-user-data.md#delete-aem).
1. Arrestate il  server AEM Forms.
1. Eseguite i seguenti comandi del database per eliminare i dati di gestione utente per un ID principale dalle tabelle del database. Nel comando `Delete`, sostituire `<principal_id>` con l&#39;ID principale dell&#39;utente di cui si desidera eliminare i dati.

   ```sql
   Delete from EdcPrincipalLocalAccountEntity where refuserprincipalid in (Select id from EdcPrincipalUserEntity where refprincipalid in (select id from EdcPrincipalEntity where id='<principal_id>'));
   
   Delete from EdcPrincipalEmailAliasEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalRoleEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPriResPrmEntity where refprinid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalUserEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalMappingEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalGrpCtmntEntity where refchildprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalEntity where id='<principal_id>';
   ```

1. Avviate il server AEM Forms .

### AEM repository {#aem-repository-1}

Gli utenti Forms JEE hanno i propri dati AEM repository se hanno eseguito l&#39;accesso all&#39;istanza  autore di AEM Forms almeno uno. È possibile accedere e eliminare i relativi dati utente AEM repository.

#### Accesso ai dati utente {#access-user-data}

Per visualizzare l&#39;utente creato AEM repository, accedere a `https://'[server]:[port]'/lc/useradmin` con AEM credenziali di amministratore. Tenere presente che `server` e `port` nell&#39;URL sono quelli dell&#39;istanza di autore AEM. Qui potete cercare gli utenti con il loro nome utente. Fate doppio clic su un utente per visualizzare informazioni quali proprietà, autorizzazioni e gruppi per l’utente. La proprietà `Path` di un utente specifica il percorso del nodo utente creato AEM repository.

#### Elimina dati utente {#delete-aem}

Per eliminare un utente:

1. Andate a `https://'[server]:[port]'/lc/useradmin` con AEM credenziali di amministratore.
1. Cercate un utente e fate doppio clic sul nome utente per aprire le proprietà utente. Copiare la proprietà `Path`.
1. Andate AEM CRX DELite in `https://'[server]:[port]'/lc/crx/de/index.jsp` e individuate o cercate il percorso utente.
1. Eliminate il percorso e fate clic su **[!UICONTROL Salva tutto]** per eliminare definitivamente l&#39;utente AEM repository.

