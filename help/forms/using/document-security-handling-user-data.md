---
title: Document Security | Gestione dei dati utente
seo-title: Document Security | Gestione dei dati utente
description: Document Security | Gestione dei dati utente
uuid: 1624a465-8b0c-4347-a53f-1118bfa6e18f
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 898268cb-4426-421f-8f63-d75bd85cb57f
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 0%

---


# Document Security | Gestione dei dati utente {#document-security-handling-user-data}

 protezione dei documenti AEM Forms consente di creare, archiviare e applicare ai documenti impostazioni di protezione predefinite. Essa garantisce che solo gli utenti autorizzati possano utilizzare i documenti. È possibile proteggere i documenti utilizzando i criteri. Un criterio è una raccolta di informazioni che include le impostazioni di protezione e un elenco di utenti autorizzati. Potete applicare un criterio a uno o più documenti e autorizzare gli utenti aggiunti  gestione utenti AEM Forms JEE.

<!-- Fix broken link For more information about how document security works, see AEM Forms JEE administration help. -->

## Archivio dati utente {#user-data-and-data-stores}

Document Security memorizza criteri e dati relativi ai documenti protetti, inclusi i dati utente in un database, come SQL,  Oracle, MS SQL Server e IBM DB2. Inoltre, i dati per gli utenti autorizzati in un criterio archiviato nella gestione degli utenti. Per informazioni sui dati memorizzati nella gestione degli utenti, vedere [Gestione utente Forms: Gestione dei dati utente](/help/forms/using/user-management-handling-user-data.md).

Nella tabella seguente è illustrato come Document Security organizza i dati nelle tabelle del database.

<table>
 <tbody>
  <tr>
   <td>Tabella database</td>
   <td>Descrizione</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalKeyEntity</code></td>
   <td>Memorizza informazioni sulle chiavi principali per gli utenti. Le chiavi vengono utilizzate nei flussi di lavoro offline per la protezione dei documenti.</td>
  </tr>
  <tr>
   <td><code>EdcAuditEntity</code></td>
   <td>Memorizza informazioni sul controllo degli eventi come eventi utente, eventi di documenti ed eventi dei criteri.</td>
  </tr>
  <tr>
   <td><p><code>EdcLicenseEntity</code></p> </td>
   <td>Memorizza il record di un documento protetto. Memorizza i dettagli della licenza per ogni documento protetto.</td>
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
   <td>Memorizza informazioni sugli utenti che possono creare criteri personali che vengono visualizzate nella scheda Criteri personali della pagina Criteri. </td>
  </tr>
  <tr>
   <td><code>EdcPolicyEntity</code></td>
   <td>Memorizza informazioni sui criteri. Ogni criterio corrisponde a una riga nella tabella.</td>
  </tr>
  <tr>
   <td><code>EdcPolicyXmlEntity</code></td>
   <td>Memorizza i file XML per i criteri attivi. Un codice XML di criteri<sup> </sup>contiene riferimenti agli ID principali degli utenti associati al criterio. L'XML dei criteri è memorizzato come oggetto Blob.</td>
  </tr>
  <tr>
   <td><code>EdcPolicyArchiveEntity</code></td>
   <td>Memorizza informazioni sui criteri archiviati. Un criterio archiviato contiene l'XML del criterio memorizzato come oggetto Blob.</td>
  </tr>
  <tr>
   <td><p><code>EdcPolicySetPrincipalEntity</code></p> <p><code>EdcPolicySetPrincipalEnt</code> ( database Oracle e MS SQL)</p> </td>
   <td>Memorizza la mappatura tra set di criteri e utenti.</td>
  </tr>
  <tr>
   <td><code>EdcInvitedUserEntity</code></td>
   <td>Memorizza le informazioni sull'utente invitato.</td>
  </tr>
 </tbody>
</table>

## Accesso ed eliminazione dei dati utente {#access-and-delete-user-data}

È possibile accedere ed esportare i dati di protezione dei documenti per gli utenti nei database, nonché, se necessario, eliminarli definitivamente.

Per esportare o eliminare i dati utente da un database, è necessario connettersi al database utilizzando un client di database e individuare l&#39;ID principale in base ad alcune informazioni personali dell&#39;utente. Ad esempio, per recuperare l&#39;ID principale di un utente utilizzando un ID di login, eseguite il seguente comando `select` nel database.

Nel comando `select`, sostituire il `<user_login_id>` con l&#39;ID di login dell&#39;utente di cui si desidera recuperare l&#39;ID principale dalla tabella del database `EdcPrincipalUserEntity`.

```sql
select refprincipalid from EdcPrincipalUserEntity where uidstring = <user_login_id>
```

Una volta noto l’ID principale, potete esportare o eliminare i dati utente.

### Esportare i dati utente {#export-user-data}

Eseguite i seguenti comandi del database per esportare i dati utente per un ID entità dalle tabelle del database. Nel comando `select`, sostituire `<principal_id>` con l&#39;ID principale dell&#39;utente di cui si desidera esportare i dati.

>[!NOTE]
>
>I seguenti comandi utilizzano i nomi delle tabelle del database nei database My SQL e IBM DB2. Quando eseguite questi comandi su  database Oracle e MS SQL, sostituite `EdcPolicySetPrincipalEntity` con `EdcPolicySetPrincipalEnt` nei comandi.

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
>Per esportare i dati dalla tabella `EdcAuditEntity`, utilizzare l&#39;API [EventManager.exportEvents](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/index.html?com/adobe/livecycle/rightsmanagement/client/EventManager.html) che utilizza [EventSearchFilter](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/com/adobe/livecycle/rightsmanagement/client/infomodel/EventSearchFilter.html) come parametro per esportare i dati di controllo in base a `principalId`, `policyId` o `licenseId`.

Per ottenere dati completi su un utente del sistema, è necessario accedere ed esportare i dati dal database di gestione utenti. Per ulteriori informazioni, vedere [Gestione degli utenti Forms: Gestione dei dati utente](/help/forms/using/user-management-handling-user-data.md).

### Elimina dati utente {#delete-user-data}

Per eliminare i dati di protezione del documento per un ID entità dalle tabelle del database, eseguire le operazioni seguenti.

1. Arrestate il  server AEM Forms.
1. Eseguite i seguenti comandi del database per eliminare i dati per l&#39;ID principale dalle tabelle del database per la protezione del documento. Nel comando `Delete`, sostituire `<principal_id>` con l&#39;ID principale dell&#39;utente di cui si desidera eliminare i dati.

   ```sql
   Delete from EdcPrincipalKeyEntity where principalid = '<principal_id>';
   
   Delete from EdcMyPolicyListEntity where principalId = '<principal_id>';
   
   Delete from edcpolicyarchiveentity where policyownerId = '<principal_id>';
   
   Delete from edcpolicysetprincipalentity where principalId = '<principal_id>';
   
   Delete from edcinviteduserentity where principalId = '<principal_id>';
   ```

   >[!NOTE]
   >
   >Per eliminare i dati dalla tabella `EdcAuditEntity`, utilizzare l&#39;API [EventManager.deleteEvents](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/index.html?com/adobe/livecycle/rightsmanagement/client/EventManager.html) che utilizza [EventSearchFilter](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/com/adobe/livecycle/rightsmanagement/client/infomodel/EventSearchFilter.html) come parametro per eliminare i dati di controllo basati su `principalId`, `policyId` o `licenseId`.

1. I file XML dei criteri attivi e archiviati sono memorizzati rispettivamente nelle tabelle di database `EdcPolicyXmlEntity` e `EdcPolicyArchiveEntity`. Per eliminare dati per un utente da queste tabelle, effettuare le seguenti operazioni:

   1. Aprire il BLOB XML di ciascuna riga nella tabella `EdcPolicyXMLEntity` o `EdcPolicyArchiveEntity` ed estrarre il file XML. Il file XML è simile a quello illustrato di seguito.
   1. Modificate il file XML per rimuovere il BLOB per l’ID principale.
   1. Ripetere i passaggi 1 e 2 per l&#39;altro file.

   >[!NOTE]
   >
   >È necessario rimuovere il BLOB completo all&#39;interno del tag `Principal` per un ID entità, altrimenti l&#39;XML dei criteri potrebbe risultare danneggiato o inutilizzabile.

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

   Oltre a eliminare i dati direttamente dalla tabella `EdcPolicyXmlEntity`, sono disponibili due modi per ottenere questo risultato:

   **Utilizzo della console di amministrazione**

   1. In qualità di amministratore, accedi alla console di amministrazione Forms JEE all&#39;indirizzo https://[*server*]:[*port*]/adminui.
   1. Passa a **[!UICONTROL Servizi > Document Security > Policy Sets]**.
   1. Aprite un set di criteri ed eliminate l&#39;utente dal criterio.

   **Utilizzo della pagina Web di protezione dei documenti**

   Gli utenti di Document Security che dispongono delle autorizzazioni per creare criteri personali possono eliminare i dati utente dai propri criteri. A questo scopo:

   1. Gli utenti che dispongono di criteri personali accedono alla pagina Web relativa alla protezione dei documenti all&#39;indirizzo https://[*server*]:[*port*]/edc.
   1. Passa a **[!UICONTROL Servizi > Document Security > My Policies]**.
   1. Aprite un criterio ed eliminate l&#39;utente dal criterio.

   >[!NOTE]
   >
   >Gli amministratori possono cercare, accedere ed eliminare dati utente dai criteri personali di altri utenti in **[!UICONTROL Services > Document Security > My Policies]** tramite la console di amministrazione.

1. Eliminate i dati per l&#39;ID entità dal database di gestione utenti. Per i passaggi dettagliati, vedere [Gestione utente Forms | Gestione dei dati utente](/help/forms/using/user-management-handling-user-data.md).
1. Avviate il server AEM Forms .

