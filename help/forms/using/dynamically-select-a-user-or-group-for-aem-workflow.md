---
title: Selezione dinamica di un utente o di un gruppo per i passaggi di flusso di lavoro AEM Forms-centrico
seo-title: Selezione dinamica di un utente o di un gruppo per i passaggi di flusso di lavoro AEM Forms-centrico
description: 'Scoprite come selezionare un utente o un gruppo per un flusso di lavoro AEM Forms in fase di esecuzione. '
seo-description: 'Scoprite come selezionare un utente o un gruppo per un flusso di lavoro AEM Forms in fase di esecuzione. '
uuid: 19dcbda4-61af-40b3-b10b-68a341373410
content-type: troubleshooting
topic-tags: publish
discoiquuid: e6c9f3bb-8f20-4889-86f4-d30578fb1c51
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 1%

---


# Selezione dinamica di un utente o di un gruppo per i passaggi di flusso di lavoro AEM Forms-centrico {#dynamically-select-a-user-or-group-for-aem-forms-centric-workflow-steps}

Scoprite come selezionare un utente o un gruppo per un flusso di lavoro AEM Forms in fase di esecuzione.

Nelle grandi organizzazioni, è necessario selezionare in modo dinamico gli utenti per un processo. Ad esempio, selezionare un agente di campo per servire un cliente in base alla vicinanza dell&#39;agente al cliente. In questo caso, l&#39;agente viene selezionato in modo dinamico.

I passaggi dell’attività e di Adobe Sign dei flussi di lavoro incentrati su [Forms in OSGi](/help/forms/using/aem-forms-workflow.md) forniscono opzioni per la selezione dinamica di un utente. È possibile utilizzare i bundle ECMAScript o OSGi per selezionare dinamicamente un assegnatario per il passaggio Assegna attività o per selezionare i firmatari per il passaggio Firma documento.

## Utilizzare ECMAScript per selezionare dinamicamente un utente o un gruppo {#use-ecmascript-to-dynamically-select-a-user-or-group}

ECMAScript è un linguaggio di script. Viene utilizzato per applicazioni di script sul lato client e server. Per selezionare in modo dinamico un utente o un gruppo utilizzando ECMAScript, effettuate le seguenti operazioni:

1. Aprite CRXDE Lite. L&#39;URL è `https://'[server]:[port]'/crx/de/index.jsp`
1. Create un file con estensione .ecma nel percorso seguente. Se il percorso (struttura del nodo) non esiste, crearlo:

   * (Percorso del passaggio Assegna attività) `/apps/fd/dashboard/scripts/participantChooser`
   * (Percorso del passaggio Firma) `/apps/fd/workflow/scripts/adobesign`

1. Aggiungete al file .ecma ECMAScript, che ha la logica per selezionare in modo dinamico un utente. Fate clic su **[!UICONTROL Salva tutto]**.

   Per gli script di esempio, vedere [Esempi di script ECMAS per la selezione dinamica di un utente o di un gruppo](/help/forms/using/dynamically-select-a-user-or-group-for-aem-workflow.md#sample-ecmascripts-to-dynamically-choose-a-user-or-a-group).

1. Aggiungete il nome visualizzato dello script. Questo nome viene visualizzato nei passaggi del flusso di lavoro. Per specificare il nome:

   1. Espandete il nodo script, fate clic con il pulsante destro del mouse sul nodo **[!UICONTROL jcr:content]** e fate clic su **[!UICONTROL Mixins]**.
   1. Aggiungete la proprietà `mix:title` nella finestra di dialogo Modifica mix e fate clic su **OK**.
   1. Aggiungete la seguente proprietà al nodo jcr:content di script:

      | Nome | Tipo | Valore |
      |--- |--- |--- |
      | jcr:title | Stringa | Specificate il nome dello script. Ad esempio, Scegliere l&#39;agente campo più vicino. Questo nome viene visualizzato nei passaggi Assegna attività e Firma documento. |

   1. Fate clic su **Salva tutto**. Lo script diventa disponibile per la selezione nei componenti di AEM Workflow.

      ![script](assets/script.png)

### Esempi ECMAScripts per scegliere dinamicamente un utente o un gruppo {#sample-ecmascripts-to-dynamically-choose-a-user-or-a-group}

L&#39;esempio seguente ECMAScript seleziona dinamicamente un assegnatario per il passaggio Assegna attività. In questo script, viene selezionato un utente in base al percorso del payload. Prima di utilizzare questo script, accertatevi che tutti gli utenti menzionati nello script siano presenti in AEM. Se gli utenti menzionati nello script non esistono in AEM, il processo correlato potrebbe non riuscire.

```javascript
function getParticipant() {

var workflowData = graniteWorkItem.getWorkflowData();

if (workflowData.getPayloadType() == "JCR_PATH") { 

var path = workflowData.getPayload().toString(); 
     if (path.indexOf("/content/geometrixx/en") == 0) {
    return "user1";
    } 
   else {
              return "user2";
            }
}
}
```

Il seguente esempio di ECMAScript seleziona dinamicamente un assegnatario per il passaggio Adobe Sign. Prima di utilizzare lo script riportato di seguito, assicurarsi che le informazioni utente (indirizzi e-mail e numeri di telefono) indicate nello script siano corrette. Se le informazioni utente indicate nello script non sono corrette, il processo correlato potrebbe non riuscire.

>[!NOTE]
>
>Quando si utilizza ECMAScript per Adobe Sign, lo script deve trovarsi nell&#39;archivio crx all&#39;indirizzo /apps/fd/workflow/scripts/adobesign/ e deve avere una funzione denominata getAdobeSignRecipients per restituire un elenco di utenti.

```javascript
function getAdobeSignRecipients() {

    var recipientSetInfos = new Packages.java.util.ArrayList();

    var recipientInfoSet = new com.adobe.aem.adobesign.recipient.RecipientSetInfo();
    var recipientInfoList = new Packages.java.util.ArrayList();
    var recipientInfo = new com.adobe.aem.adobesign.recipient.RecipientInfo();

    var email;
    var recipientAuthenticationMethod = com.adobe.aem.adobesign.recipient.RecipientAuthenticationMethod.PHONE;  
    //var recipientAuthenticationMethod = com.adobe.aem.adobesign.recipient.RecipientAuthenticationMethod.NONE;
    var securityOptions = null;

    var phoneNumber = "123456789";
    var countryCode = "+1";
    var recipientPhoneInfo = new Array();
    recipientPhoneInfo.push(new com.adobe.aem.adobesign.recipient.RecipientPhoneInfo(phoneNumber, countryCode));

     securityOptions = new com.adobe.aem.adobesign.recipient.RecipientSecurityOption(recipientAuthenticationMethod, recipientPhoneInfo , null);
    
    email = "example@example.com";
    
    recipientInfo.setEmail(email);
    recipientInfo.setSecurityOptions(securityOptions);
    
    recipientInfoList.add(recipientInfo);
    recipientInfoSet.setMemberInfos(recipientInfoList);
    recipientSetInfos.add(recipientInfoSet);

    return recipientSetInfos;

}
```

## Utilizzare l&#39;interfaccia Java per scegliere dinamicamente un utente o un gruppo {#use-java-interface-to-dynamically-choose-a-user-or-group}

È possibile utilizzare l&#39;interfaccia Java [RecipientInfoSpecifier](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) per scegliere in modo dinamico un utente o un gruppo per i passaggi Adobe Sign e Assign Task. Potete creare un bundle OSGi che utilizzava l’interfaccia Java [RecipientInfoSpecifier](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) e distribuirla al server AEM Forms. Questa opzione è disponibile per la selezione nei componenti Assegna attività e Adobe Sign del flusso di lavoro AEM.

Per compilare l’esempio di codice riportato di seguito, è necessario disporre di file JAR e Jar [SDK](https://helpx.adobe.com/it/aem-forms/kb/aem-forms-releases.html) per client di [AEM Forms](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.workflow.api/1.0.2/) . Aggiungete questi file JAR come dipendenze esterne al progetto bundle OSGi. Potete utilizzare qualsiasi IDE Java per creare un bundle OSGi. La procedura seguente illustra i passaggi per utilizzare Eclipse per creare un bundle OSGi:

1. Aprite Eclipse IDE. Passare a **[!UICONTROL File]**> **[!UICONTROL Nuovo progetto]**.
1. Nella schermata Seleziona una procedura guidata, selezionate Progetto **** Paradiso e fate clic su **[!UICONTROL Avanti]**.
1. Nel progetto New Maven, mantenete le impostazioni predefinite e fate clic su **[!UICONTROL Next (Avanti)]**. Selezionate un archetipo e fate clic su **[!UICONTROL Avanti]**. Ad esempio, maven-archetype-quickstart. Specificate ID **** gruppo, ID **** artefatto, **[!UICONTROL versione]** e **[!UICONTROL pacchetto]** per il progetto, quindi fate clic su **[!UICONTROL Fine]**. Il progetto viene creato.
1. Aprite il file pom.xml per la modifica e sostituite tutto il contenuto del file con quanto segue:

   ```xml
   <project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
       <modelVersion>4.0.0</modelVersion>
   
       <groupId>getAgent</groupId>
       <artifactId>assignToAgent</artifactId>
       <version>1.0</version>
       <packaging>bundle</packaging><!-- packaging type bundle is must -->
   
       <name>assignToAgent</name>
       <url>https://maven.apache.org</url>
       <repositories>
           <repository>
               <id>adobe</id>
               <name>Adobe Public Repository</name>
               <url>https://repo.adobe.com/nexus/content/groups/public/</url>
               <layout>default</layout>
           </repository>
       </repositories>
       <pluginRepositories>
           <pluginRepository>
               <id>adobe</id>
               <name>Adobe Public Repository</name>
               <url>https://repo.adobe.com/nexus/content/groups/public/</url>
               <layout>default</layout>
           </pluginRepository>
       </pluginRepositories>
   
       <dependencies>
           <dependency>
               <groupId>com.adobe.aemfd</groupId>
               <artifactId>aemfd-client-sdk</artifactId>
               <version>6.0.138</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.granite</groupId>
               <artifactId>com.adobe.granite.workflow.api</artifactId>
               <version>1.0.0</version>
           </dependency>
   
           <dependency>
               <groupId>org.osgi</groupId>
               <artifactId>org.osgi.core</artifactId>
               <version>4.2.0</version>
               <scope>provided</scope>
           </dependency>
   
           <dependency>
               <groupId>org.apache.felix</groupId>
               <artifactId>org.apache.felix.scr.annotations</artifactId>
               <version>1.7.0</version>
   
           </dependency>
   
           <dependency>
               <groupId>org.apache.sling</groupId>
               <artifactId>org.apache.sling.api</artifactId>
               <version>2.2.0</version>
   
           </dependency>
   
       </dependencies>
   
       <!-- ====================================================================== -->
       <!-- B U I L D D E F I N I T I O N -->
       <!-- ====================================================================== -->
       <build>
           <plugins>
   
               <plugin>
                   <groupId>org.apache.felix</groupId>
                   <artifactId>maven-bundle-plugin</artifactId>
                   <extensions>true</extensions>
                   <configuration>
                       <instructions>
                           <Bundle-SymbolicName>com.aem.assigntoAgent-bundle</Bundle-SymbolicName>
                       </instructions>
                   </configuration>
               </plugin>
   
               <plugin>
                   <groupId>org.apache.felix</groupId>
                   <artifactId>maven-scr-plugin</artifactId>
                   <version>1.9.0</version>
                   <executions>
                       <execution>
                           <id>generate-scr-descriptor</id>
                           <goals>
                               <goal>scr</goal>
                           </goals>
                       </execution>
                   </executions>
               </plugin>
           </plugins>
       </build>
   
   </project>
   ```

1. Aggiungete il codice sorgente che utilizza l&#39;interfaccia Java [RecipientInfoSpecifier](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) per scegliere in modo dinamico un utente o un gruppo per il passaggio dell&#39;attività Assegna. Per un esempio di codice, consultate [Esempio per la scelta dinamica di un utente o di un gruppo tramite l&#39;interfaccia](#-sample-scripts-for)Java.
1. Aprite un prompt dei comandi e andate alla directory contenente il progetto bundle OSGi. Usate il comando seguente per creare il bundle OSGi:

   `mvn clean install`

1. Caricate il bundle in un server di AEM Forms. Potete utilizzare AEM Package Manager per importare il bundle nel server AEM Forms.

Dopo l&#39;importazione del bundle, per i passaggi di Adobe Sign e Assegna attività diventa disponibile l&#39;opzione Java per selezionare in modo dinamico un utente o un gruppo.

### Esempio di codice Java per scegliere dinamicamente un utente o un gruppo {#sample-java-code-to-dynamically-choose-a-user-or-a-group}

Il seguente codice di esempio sceglie dinamicamente un assegnatario per il passaggio Adobe Sign. Il codice viene utilizzato in un bundle OSGi. Prima di utilizzare il codice riportato di seguito, accertatevi che le informazioni utente (indirizzi e-mail e numeri di telefono) indicate nel codice siano corrette. Se le informazioni utente indicate nel codice non sono corrette, il processo correlato potrebbe non riuscire.

```java
/*************************************************************************

 *
 * ADOBE CONFIDENTIAL
 * __________________
 *
 * Copyright 2016 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
 
package com.aem.impl;

import java.util.ArrayList;
import java.util.List;

import com.adobe.aem.adobesign.recipient.RecipientAuthenticationMethod;
import com.adobe.aem.adobesign.recipient.RecipientInfo;
import com.adobe.aem.adobesign.recipient.RecipientPhoneInfo;
import com.adobe.aem.adobesign.recipient.RecipientSecurityOption;
import com.adobe.aem.adobesign.recipient.RecipientSetInfo;
import com.adobe.fd.workflow.adobesign.api.RecipientInfoSpecifier;
import com.adobe.granite.workflow.WorkflowException;
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.WorkItem;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

/**
 * <code>DummyRecipientInfoSpecifier implementation. A sample code to write implementation of RecipientInfoSpecifier to choose recipients/code>...
 */
@Service

@Component(metatype = false)
public class DummyRecipientChoser implements RecipientInfoSpecifier {
    public List<RecipientSetInfo> getAdobeSignRecipients(WorkItem workItem, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {

        List<RecipientSetInfo> recipientSetInfos = new ArrayList<RecipientSetInfo>();

                //First Recipient

                RecipientSetInfo recipientInfoSet1 = new RecipientSetInfo();
                List<RecipientInfo> recipientInfoList = new ArrayList<RecipientInfo>();
                RecipientInfo recipientInfo1 = new RecipientInfo();//Member to first recipient

                String email;

                RecipientAuthenticationMethod recipientAuthenticationMethod = RecipientAuthenticationMethod.WEB_IDENTITY;
                RecipientSecurityOption securityOptions = null;

                String phoneNumber = "123456789";
                String countryCode = "+1";
                RecipientPhoneInfo[] recipientPhoneInfo = new RecipientPhoneInfo[1];  //if multiple phone numbers, size>1
                recipientPhoneInfo[0] = new RecipientPhoneInfo(phoneNumber, countryCode);
                securityOptions = new RecipientSecurityOption(recipientAuthenticationMethod, recipientPhoneInfo , null);
                 
                email = "example@example.com";

                recipientInfo1.setEmail(email);
                recipientInfo1.setSecurityOptions(securityOptions);

                recipientInfoList.add(recipientInfo1);  //Add member

                recipientInfoSet1.setMemberInfos(recipientInfoList);

                //Second Recipient

                RecipientSetInfo recipientInfoSet2 = new RecipientSetInfo();
                List<RecipientInfo> recipientInfoList2 = new ArrayList<RecipientInfo>();

                recipientAuthenticationMethod = RecipientAuthenticationMethod.PHONE;
                securityOptions = null;
                 
                phoneNumber = "987654321";//"0123456789";

                countryCode = "+1";
                RecipientPhoneInfo[] recipientPhoneInfo_1 = new RecipientPhoneInfo[1];
                recipientPhoneInfo_1[0] = new RecipientPhoneInfo(phoneNumber, countryCode);
                securityOptions = new RecipientSecurityOption(recipientAuthenticationMethod, recipientPhoneInfo_1 , null);
                 
                email = "example2@example.com";//"dummymail2@domain.com";

                RecipientInfo recipientInfo2  = new RecipientInfo();
                recipientInfo2.setEmail(email);
                recipientInfo2.setSecurityOptions(securityOptions);

                recipientInfoList2.add(recipientInfo2);  //Add member

                recipientInfoSet2.setMemberInfos(recipientInfoList2);

                //*********************************

                recipientSetInfos.add(recipientInfoSet1); 
                recipientSetInfos.add(recipientInfoSet2);

        return recipientSetInfos;

    }

}
```

