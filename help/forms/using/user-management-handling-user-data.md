---
title: Gestione degli utenti Forms | Gestione dei dati utente
description: Il componente Gestione utenti di AEM Forms JEE consente la creazione, l’autorizzazione e la gestione degli utenti per l’accesso ad AEM Forms.
uuid: 2b76b69f-6f3a-4f1a-a2a4-d39f5e529f75
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a88fc933-f1af-4798-b72f-10e7b0d2fd11
role: Admin
exl-id: eeeab5d1-073a-4e13-a781-391dfe70bb37
source-git-commit: 20b0d0db54dc30285c056a10032f02ba45f8baca
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 0%

---

# Gestione degli utenti Forms | Gestione dei dati utente {#forms-user-management-handling-user-data}

La gestione degli utenti è un componente di AEM Forms JEE che consente di creare, gestire e autorizzare gli utenti di AEM Forms ad accedere ad AEM Forms. La gestione utente utilizza i domini come directory per ottenere le informazioni utente. Sono supportati i seguenti tipi di dominio:

**Domini locali**: questo tipo di dominio non è connesso a un sistema di storage di terze parti. Al contrario, gli utenti e i gruppi vengono creati localmente e risiedono nel database User Management. Le password vengono memorizzate localmente e l&#39;autenticazione viene eseguita utilizzando un database locale.

**Domini ibridi**: questo tipo di dominio non è connesso a un sistema di storage di terze parti. Al contrario, gli utenti e i gruppi vengono creati localmente e risiedono nel database User Management. A differenza dei domini locali, i domini ibridi utilizzano un provider di autenticazione esterno, che può essere LDAP, Kerberos, SAML o un provider di autenticazione personalizzato.

**Domini aziendali**: è costituito da utenti e gruppi che risiedono in un sistema di storage di terze parti, ad esempio una directory LDAP. Gestione utenti non scrive sul sistema di storage di terze parti. Gestione utenti sincronizza invece le informazioni su utenti e gruppi con il database Gestione utenti. I domini Enterprise utilizzano anche un provider di autenticazione esterno, che può essere LDAP, Kerberos, SAML o un provider di autenticazione personalizzato.

<!-- Fix broken links For more information about how user management works and configured, see AEM Forms JEE administration help. -->

## Dati utente e archivi dati {#user-data-and-data-stores}

La gestione utente memorizza i dati utente in un database, ad esempio My Sql, Oracle, MS SQL Server e IBM DB2. Inoltre, per tutti gli utenti che hanno effettuato l’accesso almeno una volta nelle applicazioni Forms su AEM Author at `https://'[server]:[port]'lc`, l’utente viene creato nell’archivio AEM. Pertanto, la gestione degli utenti viene memorizzata nei seguenti archivi di dati:

* Database
* Archivio AEM
* Archiviazione di terze parti come la directory LDAP

>[!NOTE]
>
>I dati archiviati in archivi di terze parti non rientrano nell&#39;ambito di questo documento. Contatta direttamente il fornitore di terze parti per gestire i dati utente in tali archivi.

### Database {#database}

Gestione utenti memorizza i dati utente nelle tabelle di database seguenti:

<table>
 <tbody>
  <tr>
   <td>Tabella di database</td>
   <td>Descrizione</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalEntity</code></td>
   <td><p>Memorizza informazioni sulle entità principali. Un’entità principale può essere un utente, un gruppo o un ruolo.</p> <p> </p> </td>
  </tr>
  <tr>
   <td><code>EdcPrincipalUserEntity</code></td>
   <td>Memorizza le informazioni personali (PII, personally identifiable information) degli utenti. Contiene una voce per ogni utente dai domini locali, aziendali e ibridi.</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalLocalAccountEntity</code></p> <p><code class="code">EdcPrincipalLocalAccount
       </code>(database Oracle e MS SQL)</p> </td>
   <td>Memorizza i dati solo per gli utenti locali.</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalEmailAliasEntity</code></p> <p><code class="code">EdcPrincipalEmailAliasEn
       </code>(database Oracle e MS SQL)</p> </td>
   <td>Contiene le voci di tutti gli utenti dai domini locali, aziendali e ibridi. Contiene gli ID e-mail degli utenti.</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalGrpCtmntEntity</code></p> <p><code>EdcPrincipalGrpCtmntEnti</code><br /> (database Oracle e MS SQL)</p> </td>
   <td>Memorizza la mappatura tra utenti e gruppi.</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalRoleEntity</code></td>
   <td>Memorizza la mappatura tra ruoli e entità principale sia per gli utenti che per i gruppi.</td>
  </tr>
  <tr>
   <td><code>EdcPriResPrmEntity</code></td>
   <td>Memorizza la mappatura tra entità e autorizzazioni per utenti e gruppi.</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalMappingEntity</code></p> <p><code>EdcPrincipalMappingEntit</code><br /> (database Oracle e MS SQL)</p> </td>
   <td>Memorizza i valori di attributo vecchi e nuovi corrispondenti a un'entità principale.<br /> </td>
  </tr>
 </tbody>
</table>

### Archivio AEM {#aem-repository}

Dati di gestione utenti per gli utenti che hanno effettuato almeno un accesso alle applicazioni Forms in `https://'[server]:[port]'lc` è conservato anche nell’archivio dell’AEM.

## Accedere ed eliminare i dati utente {#access-and-delete-user-data}

È possibile accedere ed esportare i dati di gestione utente per gli utenti nei database di gestione utente e nell&#39;archivio AEM e, se necessario, eliminarli definitivamente.

### Database {#database-1}

Per esportare o eliminare i dati utente dal database di gestione utenti, è necessario connettersi al database utilizzando un client di database e individuare l&#39;ID entità in base ad alcuni dati PII dell&#39;utente. Ad esempio, per recuperare l’ID principale di un utente che utilizza un ID di accesso, esegui quanto segue `select` sul database.

In `select` , sostituisci il `<user_login_id>` con l’ID di accesso dell’utente di cui desideri recuperare l’ID principale.

```sql
select refprincipalid from EdcPrincipalUserEntity where uidstring = <user_login_id>
```

Una volta individuato l’ID principale, puoi esportare o eliminare i dati utente.

#### Esporta dati utente {#export-user-data}

Eseguire i seguenti comandi di database per esportare i dati di gestione utente per un ID entità dalle tabelle di database. In `select` comando, sostituisci `<principal_id>` con l’ID principale dell’utente di cui desideri esportare i dati.

>[!NOTE]
>
>I comandi seguenti utilizzano i nomi delle tabelle di database nei database My SQL e IBM DB2. Quando si eseguono questi comandi su database Oracle e MS SQL, sostituire i seguenti nomi di tabella nei comandi:
>
>* Sostituisci `EdcPrincipalLocalAccountEntity` con `EdcPrincipalLocalAccount`
>
>* Sostituisci `EdcPrincipalEmailAliasEntity` con `EdcPrincipalEmailAliasEn`
>
>* Sostituisci `EdcPrincipalMappingEntity` con `EdcPrincipalMappingEntit`
>
>* Sostituisci `EdcPrincipalGrpCtmntEntity` con `EdcPrincipalGrpCtmntEnti`
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

Per eliminare i dati di gestione utenti per un ID entità dalle tabelle del database, procedere come segue.

1. Eliminare i dati utente dal repository AEM, se applicabile, come descritto in [Elimina dati utente](/help/forms/using/user-management-handling-user-data.md#delete-aem).
1. Arresta il server AEM Forms.
1. Eseguire i seguenti comandi di database per eliminare i dati di gestione utente per un ID entità dalle tabelle di database. In `Delete` comando, sostituisci `<principal_id>` con l’ID principale dell’utente di cui desideri eliminare i dati.

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

### Archivio AEM {#aem-repository-1}

Gli utenti di Forms JEE hanno i propri dati nell’archivio AEM se hanno effettuato l’accesso all’istanza di authoring di AEM Forms almeno una. Puoi accedere ai dati dei loro utenti ed eliminarli dall’archivio AEM.

#### Accedere ai dati utente {#access-user-data}

Per visualizzare l’utente creato nell’archivio AEM, accedi a `https://'[server]:[port]'/lc/useradmin` con le credenziali di amministratore AEM. Tieni presente che `server` e `port` nell’URL sono quelli dell’istanza di authoring AEM. Qui puoi cercare gli utenti con il loro nome utente. Fare doppio clic su un utente per visualizzare informazioni quali proprietà, autorizzazioni e gruppi per l&#39;utente. Il `Path` per un utente specifica il percorso del nodo utente creato nell&#39;archivio AEM.

#### Elimina dati utente {#delete-aem}

Per eliminare un utente:

1. Vai a `https://'[server]:[port]'/lc/useradmin` con le credenziali di amministratore AEM.
1. Cercare un utente e fare doppio clic sul nome utente per aprire le proprietà utente. Copia il `Path` proprietà.
1. Vai a AEM CRX DELite all’indirizzo `https://'[server]:[port]'/lc/crx/de/index.jsp` e naviga o cerca nel percorso utente.
1. Elimina il percorso e fai clic su **[!UICONTROL Salva tutto]** per eliminare definitivamente l’utente dall’archivio AEM.
