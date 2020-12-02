---
title: Gestione delle attività in una gerarchia organizzativa utilizzando la vista Manager
seo-title: Gestione delle attività in una gerarchia organizzativa utilizzando la vista Manager
description: In che modo i manager e gli amministratori dell'organizzazione possono accedere e lavorare alle attività dei propri rapporti diretti e indiretti nella scheda Da fare dell'area di lavoro  AEM Forms.
seo-description: In che modo i manager e gli amministratori dell'organizzazione possono accedere e lavorare alle attività dei propri rapporti diretti e indiretti nella scheda Da fare dell'area di lavoro  AEM Forms.
uuid: c44c55e6-6cc1-417d-8e89-c8d5c32914c8
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2e60df86-d8ff-4cf9-b801-9559857b5ff4
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 0%

---


# Gestione delle attività in una gerarchia organizzativa utilizzando la vista Manager{#managing-tasks-in-an-organizational-hierarchy-using-manager-view}

&#39;area di lavoro di AEM Forms, i manager possono ora accedere alle attività assegnate a chiunque all&#39;interno della propria gerarchia, sia direttamente che indirettamente, ed eseguire varie azioni su di esse. Le attività sono disponibili nella scheda Operazioni nell&#39;area di lavoro di  AEM Forms. Le azioni supportate per le attività dei rapporti diretti sono:

**** Inoltra: consente di inoltrare un&#39;attività dal rapporto diretto a qualsiasi utente.

**** ClaimClaim un&#39;attività di un report diretto.

**Reclami e** OpenClaim un&#39;attività di un rapporto diretto e lo apra automaticamente nell&#39;elenco A-do del manager.

**Rifiuta:** rifiuta un&#39;attività inoltrata a un rapporto diretto da un altro utente. Questa opzione è disponibile per le attività inoltrate da altri utenti a un rapporto diretto.

 AEM Forms limita l&#39;accesso di un utente solo alle attività per le quali l&#39;utente dispone del controllo di accesso (ACL). Tale controllo assicura che un utente possa recuperare solo le attività per le quali l&#39;utente dispone delle autorizzazioni di accesso. Utilizzando servizi Web e implementazioni di terze parti per definire la gerarchia, un&#39;organizzazione può personalizzare la definizione di manager e i rapporti diretti in base alle proprie esigenze.

1. Creare un DSC. Per ulteriori informazioni, consultate l&#39;argomento &quot;Sviluppo di componenti per AEM Forms&quot; nella guida [Programmazione con  AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_63).
1. Nel DSC, definite un nuovo SPI per la gestione gerarchica per definire rapporti diretti e la gerarchia all&#39;interno degli utenti AEM Forms . Segue un esempio di snippet di codice Java™.

   ```java
   public class MyHierarchyMgmtService
   {
        /*
       Input : Principal Oid for a livecycle user
       Output : Returns true when the user is either the service invoker OR his direct/indirect report.
       */
       boolean isInHierarchy(String principalOid) {
   
       }
   
       /*
       Input : Principal Oid for a livecycle user
       Output : List of principal Oids for direct reports of the livecycle user
       A user may get direct reports only for himself OR his direct/indirect reports.
       So the API is functionally equivalent to -
       isInHierarchy(principalOid) ? <return direct reports> : <return empty list>
       */
       List<String> getDirectReports(String principalOid) {
   
       }
   
       /*
       Returns whether a livecycle user has direct reports or not.
       It's functionally equivalent to -
       getDirectReports(principalOid).size()>0
       */
       boolean isManager(String principalOid) {
   
       }
   }
   ```

1. Create un file component.xml. Assicurarsi che spec-id sia uguale a quanto mostrato nello snippet di codice riportato di seguito. Segue un frammento di codice di esempio che è possibile riadattare.

   ```xml
   <component xmlns="https://adobe.com/idp/dsc/component/document">
       <component-id>com.adobe.sample.SampleDSC</component-id>
       <version>1.1</version>
       <supports-export>false</supports-export>
         <descriptor-class>com.adobe.idp.dsc.component.impl.DefaultPOJODescriptorImpl</descriptor-class>
         <services>
           <service name="MyHierarchyMgmtService" title="My hierarchy management service" orchestrateable="false">
           <auto-deploy service-id="MyHierarchyMgmtService" category-id="Sample DSC" major-version="1" minor-version="0" />
           <description>Service for resolving hierarchy management.</description>
            <specifications>
            <specification spec-id="com.adobe.idp.taskmanager.dsc.enterprise.HierarchyManagementProvider"/>
            </specifications>
           <specification-version>1.0</specification-version>
           <implementation-class>com.adobe.sample.hierarchymanagement.MyHierarchyMgmtService</implementation-class>
           <request-processing-strategy>single_instance</request-processing-strategy>
           <supported-connectors>default</supported-connectors>
           <operation-config>
               <operation-name>*</operation-name>
               <transaction-type>Container</transaction-type>
               <transaction-propagation>supports</transaction-propagation>
               <!--transaction-timeout>3000</transaction-timeout-->
           </operation-config>
           <operations>
               <operation anonymous-access="true" name="isInHierarchy" method="isInHierarchy">
                   <input-parameter name="principalOid" type="java.lang.String" />
                   <output-parameter name="result" type="java.lang.Boolean"/>
               </operation>
               <operation anonymous-access="true" name="getDirectReports" method="getDirectReports">
                   <input-parameter name="principalOid" type="java.lang.String" />
                   <output-parameter name="result" type="java.util.List"/>
               </operation>
               <operation anonymous-access="true" name="isManager" method="isManager">
                   <input-parameter name="principalOid" type="java.lang.String" />
                   <output-parameter name="result" type="java.lang.Boolean"/>
               </operation>
               </operations>
               </service>
         </services>
   </component>
   ```

1. Implementare DSC tramite Workbench. Riavviate il servizio `ProcessManagementTeamTasksService`.
1. Potrebbe essere necessario aggiornare il browser o disconnettersi/accedere nuovamente con l&#39;utente.

La schermata seguente illustra l’accesso alle attività dei rapporti diretti e alle azioni disponibili.

![cu_manager_view](assets/cu_manager_view.png)

Accesso alle attività dei rapporti diretti e azione sulle attività
