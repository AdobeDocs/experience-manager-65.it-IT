---
title: Document Security | Gestione dei dati utente
description: Scopri in che modo AEM Forms Document Security consente di gestire i dati utente e gli archivi di dati, nonché di accedere, eliminare ed esportare i dati utente.
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Admin,User
exl-id: 00c01a12-1180-4f35-9179-461bf177c787
solution: Experience Manager, Experience Manager Forms
feature: Document Security,Adaptive Forms
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 0%

---

# Document Security | Gestione dei dati utente {#document-security-handling-user-data}

AEM Forms document security consente di creare, archiviare e applicare impostazioni di protezione predefinite ai documenti. In questo modo solo gli utenti autorizzati possono utilizzare i documenti. È possibile proteggere i documenti utilizzando le policy. Una policy è una raccolta di informazioni che includono impostazioni di sicurezza e un elenco di utenti autorizzati. Puoi applicare una policy a uno o più documenti e autorizzare gli utenti aggiunti nella gestione utenti di AEM Forms JEE.

<!-- Fix broken link For more information about how document security works, see AEM Forms JEE administration help. -->

## Dati utente e archivi dati {#user-data-and-data-stores}

Document Security memorizza in un database criteri e dati relativi a documenti protetti, inclusi i dati utente, ad esempio My Sql, Oracle, MS® SQL Server e IBM® DB2®. Inoltre, i dati per gli utenti autorizzati in una policy vengono archiviati nella gestione degli utenti. Per informazioni sui dati archiviati nella gestione utenti, vedere [Gestione utenti Forms: gestione dati utente](/help/forms/using/user-management-handling-user-data.md).

Nella tabella seguente viene illustrato il modo in cui Document Security organizza i dati nelle tabelle di database.

<table>
 <tbody>
  <tr>
   <td>Tabella di database</td>
   <td>Descrizione</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalKeyEntity</code></td>
   <td>Memorizza informazioni sulle chiavi principali per gli utenti. Le chiavi vengono utilizzate nei flussi di lavoro di Document Security offline.</td>
  </tr>
  <tr>
   <td><code>EdcAuditEntity</code></td>
   <td>Memorizza informazioni sul controllo di eventi quali eventi utente, eventi documento ed eventi criteri.</td>
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
   <td>Memorizza informazioni sugli utenti che possono creare criteri personali visualizzati nella scheda Criteri personali della pagina Criteri. </td>
  </tr>
  <tr>
   <td><code>EdcPolicyEntity</code></td>
   <td>Memorizza informazioni sui criteri. Ogni criterio corrisponde a una riga nella tabella.</td>
  </tr>
  <tr>
   <td><code>EdcPolicyXmlEntity</code></td>
   <td>Memorizza i file XML per i criteri attivi. Un criterio XML<sup> </sup>contiene riferimenti agli ID entità degli utenti associati al criterio. Il codice XML dei criteri viene memorizzato come oggetto BLOB.</td>
  </tr>
  <tr>
   <td><code>EdcPolicyArchiveEntity</code></td>
   <td>Memorizza informazioni sui criteri archiviati. Un criterio archiviato contiene il relativo XML dei criteri archiviato come oggetto Blob.</td>
  </tr>
  <tr>
   <td><p><code>EdcPolicySetPrincipalEntity</code></p> <p><code>EdcPolicySetPrincipalEnt</code><br /> (database Oracle e MS® SQL)</p> </td>
   <td>Memorizza la mappatura tra set di criteri e utenti.</td>
  </tr>
  <tr>
   <td><code>EdcInvitedUserEntity</code></td>
   <td>Memorizza informazioni sull'utente invitato.</td>
  </tr>
 </tbody>
</table>

## Accedere ed eliminare i dati utente {#access-and-delete-user-data}

È possibile accedere ed esportare i dati di Document Security per gli utenti dei database e, se necessario, eliminarli definitivamente.

Per esportare o eliminare dati utente da un database, è necessario connettersi al database utilizzando un client di database e individuare l&#39;ID entità in base ad alcune informazioni personali dell&#39;utente. Ad esempio, per recuperare l&#39;ID entità di un utente che utilizza un ID di accesso, eseguire il comando `select` seguente nel database.

Nel comando `select`, sostituire `<user_login_id>` con l&#39;ID di accesso dell&#39;utente di cui si desidera recuperare l&#39;ID principale dalla tabella del database `EdcPrincipalUserEntity`.

```sql
select refprincipalid from EdcPrincipalUserEntity where uidstring = <user_login_id>
```

Una volta individuato l’ID principale, puoi esportare o eliminare i dati utente.

### Esporta dati utente {#export-user-data}

Eseguire i seguenti comandi di database per esportare i dati utente per un ID entità dalle tabelle di database. Nel comando `select`, sostituire `<principal_id>` con l&#39;ID principale dell&#39;utente di cui si desidera esportare i dati.

>[!NOTE]
>
>I comandi seguenti utilizzano i nomi delle tabelle di database nei database My SQL e IBM® DB2®. Quando si eseguono questi comandi su database Oracle e MS® SQL, sostituire `EdcPolicySetPrincipalEntity` con `EdcPolicySetPrincipalEnt` nei comandi.

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
>Per esportare i dati dalla tabella `EdcAuditEntity`, utilizzare l&#39;API [EventManager.exportEvents](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/programlc/javadoc/index.html?com/adobe/livecycle/rightsmanagement/client/EventManager.html) che accetta [EventSearchFilter](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/programlc/javadoc/com/adobe/livecycle/rightsmanagement/client/infomodel/EventSearchFilter.html) come parametro per esportare i dati di controllo in base a `principalId`, `policyId` o `licenseId`.

Per ottenere dati completi su un utente nel sistema, è necessario accedere ed esportare i dati dal database di gestione utenti. Per ulteriori informazioni, vedere [Gestione utenti di Forms: gestione dei dati utente](/help/forms/using/user-management-handling-user-data.md).

### Elimina dati utente {#delete-user-data}

Per eliminare i dati di Document Security relativi a un ID entità dalle tabelle di database, procedere come segue.

1. Arresta il server AEM Forms.
1. Eseguire i seguenti comandi di database per eliminare i dati per l&#39;ID entità dalle tabelle di database per la protezione dei documenti. Nel comando `Delete`, sostituire `<principal_id>` con l&#39;ID principale dell&#39;utente di cui si desidera eliminare i dati.

   ```sql
   Delete from EdcPrincipalKeyEntity where principalid = '<principal_id>';
   
   Delete from EdcMyPolicyListEntity where principalId = '<principal_id>';
   
   Delete from edcpolicyarchiveentity where policyownerId = '<principal_id>';
   
   Delete from edcpolicysetprincipalentity where principalId = '<principal_id>';
   
   Delete from edcinviteduserentity where principalId = '<principal_id>';
   ```

   >[!NOTE]
   >
   >Per eliminare i dati dalla tabella `EdcAuditEntity`, utilizzare l&#39;API [EventManager.deleteEvents](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/programlc/javadoc/index.html?com/adobe/livecycle/rightsmanagement/client/EventManager.html) che accetta [EventSearchFilter](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/programlc/javadoc/com/adobe/livecycle/rightsmanagement/client/infomodel/EventSearchFilter.html) come parametro per eliminare i dati di controllo basati su `principalId`, `policyId` o `licenseId`.

1. I file XML dei criteri attivi e archiviati sono archiviati rispettivamente nelle tabelle di database `EdcPolicyXmlEntity` e `EdcPolicyArchiveEntity`. Per eliminare i dati di un utente da queste tabelle, eseguire le operazioni seguenti:

   1. Aprire il BLOB XML di ogni riga nella tabella `EdcPolicyXMLEntity` o `EdcPolicyArchiveEntity` ed estrarre il file XML. Il file XML è simile a quello mostrato di seguito.
   1. Modifica il file XML in modo da poter rimuovere il BLOB per l’ID entità.
   1. Ripetere i passaggi 1 e 2 per l&#39;altro file.

   >[!NOTE]
   >
   >Rimuovere il BLOB completo all&#39;interno del tag `Principal` per un ID entità o il codice XML dei criteri potrebbe essere danneggiato o inutilizzabile.

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

   Oltre a eliminare i dati direttamente dalla tabella `EdcPolicyXmlEntity`, è possibile eseguire questa operazione in altri due modi:

   **Utilizzo della console di amministrazione**

   1. In qualità di amministratore, accedi alla console di amministrazione di Forms JEE all&#39;indirizzo https://[*server*]:[*porta*]/adminui.
   1. Passa a **[!UICONTROL Servizi > Document Security > Set di criteri]**.
   1. Aprire un set di criteri ed eliminare l&#39;utente dal criterio.

   **Utilizzo della pagina Web di Document Security**

   Gli utenti di Document Security che dispongono delle autorizzazioni per creare policy personali possono eliminare i dati degli utenti dai propri criteri. Per eseguire questa operazione:

   1. Gli utenti con criteri personali accedono alla pagina Web di Document Security all’indirizzo https://[*server*]:[*porta*]/sec.
   1. Passa a **[!UICONTROL Servizi > Document Security > I miei criteri]**.
   1. Apri una policy ed elimina l’utente dalla policy.

   >[!NOTE]
   >
   >Gli amministratori possono cercare, accedere ed eliminare i dati utente dai criteri personali di altri utenti in **[!UICONTROL Servizi > Document Security > I miei criteri]** utilizzando la console di amministrazione.

1. Elimina i dati per l&#39;ID entità dal database di gestione utenti. Per i passaggi dettagliati, consulta [Gestione utente di Forms | Gestione dei dati utente](/help/forms/using/user-management-handling-user-data.md).
1. Avvia il server AEM Forms.
