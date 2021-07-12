---
title: Sicurezza dei documenti | Gestione dei dati utente
seo-title: Sicurezza dei documenti | Gestione dei dati utente
description: Sicurezza dei documenti | Gestione dei dati utente
uuid: 1624a465-8b0c-4347-a53f-1118bfa6e18f
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 898268cb-4426-421f-8f63-d75bd85cb57f
role: Admin
exl-id: 00c01a12-1180-4f35-9179-461bf177c787
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 0%

---

# Sicurezza dei documenti | Gestione dei dati utente {#document-security-handling-user-data}

La protezione dei documenti AEM Forms consente di creare, memorizzare e applicare impostazioni di protezione predefinite ai documenti. In questo modo, solo gli utenti autorizzati possono utilizzare i documenti. È possibile proteggere i documenti utilizzando i criteri. Un criterio è una raccolta di informazioni che include le impostazioni di protezione e un elenco di utenti autorizzati. Puoi applicare un criterio a uno o più documenti e autorizzare gli utenti aggiunti nella gestione utenti JEE di AEM Forms.

<!-- Fix broken link For more information about how document security works, see AEM Forms JEE administration help. -->

## Archiviazione dati e dati utente {#user-data-and-data-stores}

La sicurezza dei documenti memorizza i criteri e i dati relativi a documenti protetti, inclusi i dati utente in un database, ad esempio My Sql, Oracle, MS SQL Server e IBM DB2. Inoltre, i dati per gli utenti autorizzati in un criterio memorizzato nella gestione utenti. Per informazioni sui dati archiviati nella gestione degli utenti, consulta [Gestione utenti Forms: Gestione dei dati utente](/help/forms/using/user-management-handling-user-data.md).

Nella tabella seguente viene illustrato come la protezione dei documenti organizza i dati nelle tabelle del database.

<table>
 <tbody>
  <tr>
   <td>Tabella database</td>
   <td>Descrizione</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalKeyEntity</code></td>
   <td>Memorizza informazioni sulle chiavi principali per gli utenti. Le chiavi vengono utilizzate nei flussi di lavoro di sicurezza dei documenti offline.</td>
  </tr>
  <tr>
   <td><code>EdcAuditEntity</code></td>
   <td>Memorizza informazioni sull'evento di controllo, ad esempio eventi utente, eventi documento ed eventi policy.</td>
  </tr>
  <tr>
   <td><p><code>EdcLicenseEntity</code></p> </td>
   <td>Memorizza la registrazione di un documento protetto. Memorizza i dettagli della licenza per ogni documento protetto.</td>
  </tr>
  <tr>
   <td><p><code>EdcDocumentEntity</code></p> </td>
   <td>Memorizza il nome del documento per ogni licenza creata nel sistema.</td>
  </tr>
  <tr>
   <td><p><code>EdcRevokationEntity</code></p> </td>
   <td>Memorizza informazioni sulla revoca e il ripristino di documenti protetti.</td>
  </tr>
  <tr>
   <td><code>EdcMyPolicyListEntity</code></td>
   <td>Memorizza informazioni sugli utenti che possono creare criteri personali visualizzati nella scheda Criteri personali della pagina Criteri. </td>
  </tr>
  <tr>
   <td><code>EdcPolicyEntity</code></td>
   <td>Memorizza informazioni sui criteri. Ogni criterio corrisponde a una riga nella tabella.</td>
  </tr>
  <tr>
   <td><code>EdcPolicyXmlEntity</code></td>
   <td>Memorizza i file XML per i criteri attivi. Un criterio XML<sup> </sup>contiene riferimenti agli ID principali degli utenti associati al criterio. XML dei criteri viene memorizzato come oggetto Blob.</td>
  </tr>
  <tr>
   <td><code>EdcPolicyArchiveEntity</code></td>
   <td>Memorizza informazioni sui criteri archiviati. Un criterio archiviato contiene il relativo XML dei criteri memorizzato come oggetto Blob.</td>
  </tr>
  <tr>
   <td><p><code>EdcPolicySetPrincipalEntity</code></p> <p><code>EdcPolicySetPrincipalEnt</code> (database SQL Oracle e MS)</p> </td>
   <td>Memorizza la mappatura tra il set di criteri e gli utenti.</td>
  </tr>
  <tr>
   <td><code>EdcInvitedUserEntity</code></td>
   <td>Memorizza informazioni sull'utente invitato.</td>
  </tr>
 </tbody>
</table>

## Accedere ed eliminare i dati utente {#access-and-delete-user-data}

È possibile accedere ed esportare i dati di sicurezza dei documenti per gli utenti dei database e, se necessario, eliminarli definitivamente.

Per esportare o eliminare i dati utente da un database, è necessario connettersi al database utilizzando un client di database e individuare l&#39;ID principale in base ad alcune informazioni personali dell&#39;utente. Ad esempio, per recuperare l&#39;ID principale di un utente utilizzando un ID di accesso, esegui il seguente comando `select` sul database.

Nel comando `select` sostituisci `<user_login_id>` con l&#39;ID di accesso dell&#39;utente di cui desideri recuperare l&#39;ID principale dalla tabella di database `EdcPrincipalUserEntity`.

```sql
select refprincipalid from EdcPrincipalUserEntity where uidstring = <user_login_id>
```

Una volta conosciuto l’ID principale, puoi esportare o eliminare i dati utente.

### Esportare i dati utente {#export-user-data}

Esegui i seguenti comandi del database per esportare i dati utente per un ID principale dalle tabelle del database. Nel comando `select` sostituisci `<principal_id>` con l’ID principale dell’utente di cui desideri esportare i dati.

>[!NOTE]
>
>I seguenti comandi utilizzano i nomi delle tabelle del database nei database My SQL e IBM DB2. Quando esegui questi comandi sui database Oracle e MS SQL, sostituisci `EdcPolicySetPrincipalEntity` con `EdcPolicySetPrincipalEnt` nei comandi.

```sql
Select * from EdcPrincipalKeyEntity where principalid = '<principal_id>';

Select * from EdcLicenseEntity where publisherId = '<principal_id>';

Select * from EdcDocumentEntity where id in (Select documentid from EdcLicenseEntity where publisherId = '<principal_id>');

Select * from EdcRevokationEntity where licenseid in (Select id from EdcLicenseEntity where publisherId = '<principal_id>');

Select * from EdcMyPolicyListEntity where principalId = '<principal_id>';

Select * from edcpolicyentity where policyownerId = '<principal_id>';

Select * from edcpolicyxmlentity where policyidref in (Select id from edcpolicyentity where policyownerId = '<principal_id>');

Select * from edcpolicyarchiveentity where policyownerId = '<principal_id>';

Select * from edcpolicysetprincipalentity where principalId = '<principal_id>';

Select * from edcinviteduserentity where principalId = '<principal_id>';
```

>[!NOTE]
>
>Per esportare i dati dalla tabella `EdcAuditEntity`, utilizza l&#39;API [EventManager.exportEvents](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/index.html?com/adobe/livecycle/rightsmanagement/client/EventManager.html) che utilizza [EventSearchFilter](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/com/adobe/livecycle/rightsmanagement/client/infomodel/EventSearchFilter.html) come parametro per esportare i dati di audit in base a `principalId`, `policyId` o `licenseId`.

Per ottenere dati completi su un utente del sistema, è necessario accedere ed esportare dati dal database di gestione utenti. Per ulteriori informazioni, consulta [Gestione utenti Forms: Gestione dei dati utente](/help/forms/using/user-management-handling-user-data.md).

### Eliminare i dati utente {#delete-user-data}

Per eliminare i dati di sicurezza dei documenti per un ID principale dalle tabelle del database, procedere come segue.

1. Spegni il server AEM Forms.
1. Esegui i seguenti comandi del database per eliminare i dati per l&#39;ID principale dalle tabelle del database per la sicurezza dei documenti. Nel comando `Delete` sostituisci `<principal_id>` con l’ID principale dell’utente di cui desideri eliminare i dati.

   ```sql
   Delete from EdcPrincipalKeyEntity where principalid = '<principal_id>';
   
   Delete from EdcMyPolicyListEntity where principalId = '<principal_id>';
   
   Delete from edcpolicyarchiveentity where policyownerId = '<principal_id>';
   
   Delete from edcpolicysetprincipalentity where principalId = '<principal_id>';
   
   Delete from edcinviteduserentity where principalId = '<principal_id>';
   ```

   >[!NOTE]
   >
   >Per eliminare i dati dalla tabella `EdcAuditEntity`, utilizza l&#39;API [EventManager.deleteEvents](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/index.html?com/adobe/livecycle/rightsmanagement/client/EventManager.html) che utilizza [EventSearchFilter](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/com/adobe/livecycle/rightsmanagement/client/infomodel/EventSearchFilter.html) come parametro per eliminare i dati di audit in base a `principalId`, `policyId` o `licenseId`.

1. I file XML dei criteri attivi e archiviati vengono archiviati nelle tabelle di database `EdcPolicyXmlEntity` e `EdcPolicyArchiveEntity`, rispettivamente. Per eliminare i dati di un utente da queste tabelle, procedi come segue:

   1. Apri il BLOB XML di ogni riga nella tabella `EdcPolicyXMLEntity` o `EdcPolicyArchiveEntity` ed estrae il file XML. Il file XML è simile a quello mostrato di seguito.
   1. Modifica il file XML per rimuovere il BLOB per l’ID principale.
   1. Ripetere i passaggi 1 e 2 per l’altro file.

   >[!NOTE]
   >
   >È necessario rimuovere il BLOB completo all&#39;interno del tag `Principal` per un ID principale oppure il file XML dei criteri potrebbe essere danneggiato o inutilizzabile.

   ```xml
   <ns2:Principal PrincipalNameType="USER">
       <ns2:PrincipalDomain>OID</ns2:PrincipalDomain>
       <ns2:PrincipalName>56F33FEB-098A-1036-A651-00000A2A2656</ns2:PrincipalName>
   </ns2:Principal>
   </ns2:PolicyEntry>
       <ns2:Property PropertyName="isCertified">
           <ns2:PropertyValue xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xmlns:xs="https://www.w3.org/2001/XMLSchema" xsi:type="xs:string">false</ns2:PropertyValue>
       </ns2:Property>
       <ns2:Property PropertyName="encryptionAlgorithm">
           <ns2:PropertyValue xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xmlns:xs="https://www.w3.org/2001/XMLSchema" xsi:type="xs:string">AES128</ns2:PropertyValue>
       </ns2:Property>
       <ns2:Property PropertyName="AccessDeniedErrorMessage">
           <ns2:PropertyValue xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xmlns:xs="https://www.w3.org/2001/XMLSchema" xsi:type="xs:string"></ns2:PropertyValue>
       </ns2:Property>
   <ns2:PolicyEntry>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.onlineOpen" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.copy" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.offlineOpen" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.accessible" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.editNotes" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.edit" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.fillAndSign" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.printHigh" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.printLow" Access="ALLOW"/>
   ```

   Oltre a eliminare i dati direttamente dalla tabella `EdcPolicyXmlEntity`, sono disponibili altri due modi per ottenere questo risultato:

   **Utilizzo della console di amministrazione**

   1. In qualità di amministratore, accedi alla console di amministrazione JEE per Forms all&#39;indirizzo https://[*server*]:[*port*]/adminui.
   1. Passa a **[!UICONTROL Servizi > Sicurezza dei documenti > Set di criteri]**.
   1. Apri un set di criteri ed elimina l’utente dal criterio.

   **Utilizzo della pagina Web di protezione dei documenti**

   Gli utenti che dispongono delle autorizzazioni per la creazione di criteri personali possono eliminare i dati degli utenti dai propri criteri. Per eseguire questa operazione:

   1. Gli utenti che dispongono di criteri personali accedono alla pagina web sulla sicurezza dei documenti all&#39;indirizzo https://[*server*]:[*port*]/edc.
   1. Passa a **[!UICONTROL Servizi > Sicurezza dei documenti > Criteri personali]**.
   1. Aprire un criterio ed eliminare l&#39;utente dal criterio.

   >[!NOTE]
   >
   >Gli amministratori possono cercare, accedere ed eliminare i dati utente dai criteri personali di altri utenti in **[!UICONTROL Servizi > Sicurezza dei documenti > Criteri personali]** utilizzando la console di amministrazione.

1. Elimina i dati per l&#39;ID principale dal database di gestione utenti. Per i passaggi dettagliati, vedi [Gestione utente Forms | Gestione dei dati utente](/help/forms/using/user-management-handling-user-data.md).
1. Avvia il server AEM Forms.
