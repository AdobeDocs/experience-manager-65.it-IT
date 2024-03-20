---
title: Visualizzazione dell'avatar utente
description: Come personalizzare l’area di lavoro di AEM Forms per visualizzare l’immagine di un utente connesso.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: ee0708b0-b630-4a2b-84b6-3c0b92dd7777
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# Visualizzazione dell&#39;avatar utente {#displaying-the-user-avatar}

L’avatar dell’utente connesso viene visualizzato nell’angolo superiore destro dell’area di lavoro di AEM Forms. Nella vista Manager vengono inoltre visualizzati gli avatar dei report diretti nella gerarchia organizzativa. Puoi configurare AEM Forms Workspace in modo da scegliere le immagini utente dal database, ad esempio il server LDAP.

>[!NOTE]
>
>Le proporzioni supportate per le immagini utente sono 1:1.

1. Creare un DSC utilizzando i dettagli indicati nel passaggio successivo. Per ulteriori informazioni, consulta l’argomento &quot;Sviluppo di componenti per AEM Forms&quot; in [Programmazione con AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_63) guida.
1. In DSC, definisci un nuovo SPI che espone i metodi getCurrentUserImageUrl e getUserImageUrl per ottenere un URL di immagine per un utente di AEM Forms. Di seguito è riportato un frammento di codice Java™ di esempio:

   ```java
   public class DemoUserImageURLProviderService {
     public String getCurrentUserImageUrl()
     {
        // return the URL for profile Image of logged in user
     }
     public String getUserImageUrl(String principalOid)
     {
         // return the URL for profile Image for user represented by this principal Oid
      }
   }
   ```

1. Creare un file component.xml. Assicurarsi che spec-id sia come mostrato nello snippet di codice riportato di seguito.

   Il seguente frammento di codice è un esempio. Personalizzalo per soddisfare le tue esigenze specifiche.

   ```java
   <component xmlns="https://adobe.com/idp/dsc/component/document">
       <component-id>com.adobe.sample.DemoUsersComponent</component-id>
       <version>1.1</version>
       <supports-export>false</supports-export>
       <descriptor-class>com.adobe.idp.dsc.component.impl.DefaultPOJODescriptorImpl</descriptor-class>
       <services>
           <service name="DemoUserImageURLProviderService" title="Demo User ImageURL provider service" orchestrateable="false">
           <auto-deploy service-id="DemoUserImageURLProviderService" category-id="Demo Users Component DSC" major-version="1" minor-version="0" />
           <description>Service for resolving user image url.</description>
            <specifications>
            <specification spec-id="com.adobe.idp.taskmanager.dsc.enterprise.UserImageUrlProvider"/>
            </specifications>
           <specification-version>1.0</specification-version>
           <implementation-class>com.adobe.sample.demousers.DemoUserImageURLProviderService</implementation-class>
           <request-processing-strategy>single_instance</request-processing-strategy>
           <supported-connectors>default</supported-connectors>
           <operation-config>
               <operation-name>*</operation-name>
               <transaction-type>Container</transaction-type>
               <transaction-propagation>supports</transaction-propagation>
               <!--transaction-timeout>3000</transaction-timeout-->
           </operation-config>
           <operations>
               <operation anonymous-access="false" name="getCurrentUserImageUrl" method="getCurrentUserImageUrl">
                   <output-parameter name="result" type="java.lang.String"/>
               </operation>
               <operation anonymous-access="false" name="getUserImageUrl"
   method="getUserImageUrl">
               <input-parameter name="principalOid" type="java.lang.String"/>
               <output-parameter name="result" type="java.lang.String"/>
               </operation>
           </operations>
           </service>
       </services>
   </component>
   ```

1. Distribuire DSC tramite Workbench. Riavvia `ProcessManagementClientSessionService` servizio.
1. Potrebbe essere necessario aggiornare il browser o disconnettersi/accedere di nuovo con l&#39;utente.
