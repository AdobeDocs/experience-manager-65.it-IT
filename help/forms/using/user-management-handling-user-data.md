---
title: Gestione utente Forms | Gestione dei dati utente
seo-title: Gestione utente Forms | Gestione dei dati utente
description: Gestione utente Forms | Gestione dei dati utente
uuid: 2b76b69f-6f3a-4f1a-a2a4-d39f5e529f75
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a88fc933-f1af-4798-b72f-10e7b0d2fd11
role: Admin
exl-id: eeeab5d1-073a-4e13-a781-391dfe70bb37
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 0%

---

# Gestione utente Forms | Gestione dei dati utente {#forms-user-management-handling-user-data}

La gestione degli utenti è un componente JEE di AEM Forms che consente di creare, gestire e autorizzare gli utenti AEM Forms ad accedere ad AEM Forms. La gestione utente utilizza i domini come directory per ottenere le informazioni utente. Sono supportati i seguenti tipi di dominio:

**Domini** locali: Questo tipo di dominio non è connesso a un sistema di storage di terze parti. Al contrario, gli utenti e i gruppi vengono creati localmente e risiedono nel database User Management. Le password vengono memorizzate localmente e l&#39;autenticazione viene eseguita utilizzando un database locale.

**Domini** ibridi: Questo tipo di dominio non è connesso a un sistema di storage di terze parti. Al contrario, gli utenti e i gruppi vengono creati localmente e risiedono nel database User Management. A differenza dei domini locali, i domini ibridi utilizzano un provider di autenticazione esterno, che può essere LDAP, Kerberos, SAML o un provider di autenticazione personalizzato.

**Domini** aziendali: Sono costituiti da utenti e gruppi che risiedono in un sistema di storage di terze parti, ad esempio una directory LDAP. Gestione utente non scrive nel sistema di storage di terze parti. Al contrario, User Management sincronizza le informazioni utente e gruppo con il database User Management. I domini Enterprise utilizzano anche un provider di autenticazione esterno, che può essere LDAP, Kerberos, SAML o un provider di autenticazione personalizzato.

<!-- Fix broken links For more information about how user management works and configured, see AEM Forms JEE administration help. -->

## Archiviazione dati e dati utente {#user-data-and-data-stores}

La gestione utenti memorizza i dati utente in un database, ad esempio My Sql, Oracle, MS SQL Server e IBM DB2. Inoltre, qualsiasi utente che abbia effettuato l&#39;accesso almeno una volta nelle applicazioni Forms su AEM autore in `https://'[server]:[port]'lc`, l&#39;utente viene creato in AEM archivio. Pertanto, la gestione degli utenti viene memorizzata nei seguenti archivi di dati:

* Database
* archivio AEM
* Archiviazione di terze parti come la directory LDAP

>[!NOTE]
>
>I dati archiviati in archivi di terze parti non rientrano nell&#39;ambito di applicazione di questo documento. Contatta direttamente il fornitore di terze parti per gestire i dati utente in tali archivi.

### Database {#database}

La gestione utenti memorizza i dati utente nelle seguenti tabelle di database:

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
   <td>Memorizza informazioni personali identificabili (PII) degli utenti. Contiene una voce per ogni utente proveniente da domini locali, Enterprise e ibridi.</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalLocalAccountEntity</code></p> <p><code class="code">EdcPrincipalLocalAccount
       </code>(database SQL Oracle e MS)</p> </td>
   <td>Memorizza i dati solo per gli utenti locali.</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalEmailAliasEntity</code></p> <p><code class="code">EdcPrincipalEmailAliasEn
       </code>(database SQL Oracle e MS)</p> </td>
   <td>Contiene voci di tutti gli utenti di domini locali, Enterprise e ibridi. Contiene gli ID e-mail dell’utente.</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalGrpCtmntEntity</code></p> <p><code>EdcPrincipalGrpCtmntEnti</code> (database SQL Oracle e MS)</p> </td>
   <td>Memorizza la mappatura tra utenti e gruppi.</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalRoleEntity</code></td>
   <td>Memorizza la mappatura tra ruoli e entità per utenti e gruppi.</td>
  </tr>
  <tr>
   <td><code>EdcPriResPrmEntity</code></td>
   <td>Memorizza la mappatura tra entità principale e autorizzazioni per utenti e gruppi.</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalMappingEntity</code></p> <p><code>EdcPrincipalMappingEntit</code> (database SQL Oracle e MS)</p> </td>
   <td>Memorizza i valori degli attributi vecchi e nuovi corrispondenti a un'entità principale.<br /> </td>
  </tr>
 </tbody>
</table>

### archivio AEM {#aem-repository}

I dati di gestione degli utenti per gli utenti che hanno effettuato almeno un accesso alle applicazioni Forms in `https://'[server]:[port]'lc` vengono memorizzati anche AEM repository.

## Accedere ed eliminare i dati utente {#access-and-delete-user-data}

È possibile accedere ed esportare i dati di gestione utenti per gli utenti nei database di gestione utenti e AEM archivio e, se necessario, eliminarli definitivamente.

### Database {#database-1}

Per esportare o eliminare i dati utente dal database di gestione utenti, è necessario connettersi al database utilizzando un client di database e individuare l&#39;ID principale in base ad alcuni dati PII dell&#39;utente. Ad esempio, per recuperare l&#39;ID principale di un utente utilizzando un ID di accesso, esegui il seguente comando `select` sul database.

Nel comando `select` sostituisci `<user_login_id>` con l&#39;ID di accesso dell&#39;utente di cui desideri recuperare l&#39;ID principale.

```sql
select refprincipalid from EdcPrincipalUserEntity where uidstring = <user_login_id>
```

Una volta conosciuto l’ID principale, puoi esportare o eliminare i dati utente.

#### Esportare i dati utente {#export-user-data}

Esegui i seguenti comandi del database per esportare i dati di gestione utente per un ID principale dalle tabelle del database. Nel comando `select` sostituisci `<principal_id>` con l’ID principale dell’utente di cui desideri esportare i dati.

>[!NOTE]
>
>I seguenti comandi utilizzano i nomi delle tabelle del database nei database My SQL e IBM DB2. Quando esegui questi comandi sui database Oracle e MS SQL, sostituisci i seguenti nomi di tabella nei comandi:
>
>* Sostituisci `EdcPrincipalLocalAccountEntity` con `EdcPrincipalLocalAccount`
   >
   >
* Sostituisci `EdcPrincipalEmailAliasEntity` con `EdcPrincipalEmailAliasEn`
   >
   >
* Sostituisci `EdcPrincipalMappingEntity` con `EdcPrincipalMappingEntit`
   >
   >
* Sostituisci `EdcPrincipalGrpCtmntEntity` con `EdcPrincipalGrpCtmntEnti`

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

#### Eliminare i dati utente {#delete-user-data}

Per eliminare i dati di gestione utente per un ID principale dalle tabelle del database, procedi come segue.

1. Elimina i dati utente AEM repository, se applicabile, come descritto in [Elimina i dati utente](/help/forms/using/user-management-handling-user-data.md#delete-aem).
1. Spegni il server AEM Forms.
1. Esegui i seguenti comandi del database per eliminare i dati di gestione utente per un ID principale dalle tabelle del database. Nel comando `Delete` sostituisci `<principal_id>` con l’ID principale dell’utente di cui desideri eliminare i dati.

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

1. Avvia il server AEM Forms.

### archivio AEM {#aem-repository-1}

Gli utenti JEE di Forms hanno i loro dati nell’archivio AEM se hanno effettuato l’accesso all’istanza di authoring di AEM Forms almeno uno. È possibile accedere e eliminare i dati utente da AEM repository.

#### Accedere ai dati utente {#access-user-data}

Per visualizzare l&#39;utente creato AEM repository, accedi a `https://'[server]:[port]'/lc/useradmin` con AEM credenziali di amministratore. Nell’URL `server` e `port` sono quelli dell’istanza di authoring AEM. Qui puoi cercare gli utenti con il loro nome utente. Fare doppio clic su un utente per visualizzare informazioni quali proprietà, autorizzazioni e gruppi per l&#39;utente. La proprietà `Path` di un utente specifica il percorso del nodo utente creato AEM repository.

#### Eliminare i dati utente {#delete-aem}

Per eliminare un utente:

1. Vai a `https://'[server]:[port]'/lc/useradmin` con AEM credenziali di amministratore.
1. Cerca un utente e fai doppio clic sul nome utente per aprire le proprietà dell’utente. Copia la proprietà `Path` .
1. Vai a AEM CRX DELite in `https://'[server]:[port]'/lc/crx/de/index.jsp` e naviga o cerca il percorso utente.
1. Elimina il percorso e fai clic su **[!UICONTROL Salva tutto]** per eliminare definitivamente l&#39;utente dall&#39;archivio AEM.
