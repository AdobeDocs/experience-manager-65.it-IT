---
title: Visualizzazione dell’avatar utente
seo-title: Visualizzazione dell’avatar utente
description: Come personalizzare l’area di lavoro AEM Forms per visualizzare l’immagine di un utente connesso.
seo-description: Come personalizzare l’area di lavoro AEM Forms per visualizzare l’immagine di un utente connesso.
uuid: 2961dc93-f0d0-4842-80f1-3c239a20e348
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: aec03ea5-17a6-4775-92cb-2ad361895fdf
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---


# Visualizzazione dell’avatar utente {#displaying-the-user-avatar}

L’avatar dell’utente connesso viene visualizzato nell’angolo superiore destro dell’area di lavoro AEM Forms. Inoltre, gli avatar dei rapporti diretti nella gerarchia organizzativa vengono visualizzati nella vista Manager. Potete configurare l’area di lavoro AEM Forms per scegliere le immagini utente dal database, ad esempio il server LDAP.

>[!NOTE]
>
>Le proporzioni supportate per le immagini utente sono 1:1.

1. Create un DSC utilizzando i dettagli indicati nel passaggio successivo. Per ulteriori informazioni, vedere &#39;Sviluppo di componenti per AEM Forms&#39; nella guida alla [programmazione con AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_63) .
1. In DSC, definite un nuovo SPI che espone i metodi getCurrentUserImageUrl e getUserImageUrl per ottenere un URL immagine per un utente di AEM Forms. Segue un esempio di snippet di codice Java™:

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

1. Create un file component.xml. Verifica che spec-id sia come mostrato nello snippet di codice seguente.

   Esempio di snippet di codice riportato di seguito. Personalizzatelo in base alle vostre esigenze specifiche.

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

1. Implementare DSC tramite Workbench. Riavviate `ProcessManagementClientSessionService` il servizio.
1. Potrebbe essere necessario aggiornare il browser o disconnettersi/accedere nuovamente con l&#39;utente.
