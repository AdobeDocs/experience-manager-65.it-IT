---
title: Seleziona dinamicamente un utente o un gruppo per i passaggi del flusso di lavoro incentrati su AEM Forms
seo-title: Dynamically select a user or group for AEM Forms-centric workflow steps
description: 'Scopri come selezionare un utente o un gruppo per un flusso di lavoro AEM Forms in fase di esecuzione. '
seo-description: Learn how to select a user or group for an AEM Forms workflow at the runtime.
uuid: 19dcbda4-61af-40b3-b10b-68a341373410
content-type: troubleshooting
topic-tags: publish
discoiquuid: e6c9f3bb-8f20-4889-86f4-d30578fb1c51
exl-id: 3c48660e-5e4f-4615-82d4-9f1f285c2a39
source-git-commit: 8f0e8b15d2ed8b436594fd2be464b4ace29a8902
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 0%

---

# Seleziona dinamicamente un utente o un gruppo per i passaggi del flusso di lavoro incentrati su AEM Forms {#dynamically-select-a-user-or-group-for-aem-forms-centric-workflow-steps}

Scopri come selezionare un utente o un gruppo per un flusso di lavoro AEM Forms in fase di esecuzione.

Nelle grandi organizzazioni, è necessario selezionare in modo dinamico gli utenti per un processo. Ad esempio, selezionando un agente di campo da servire a un cliente in base alla vicinanza dell’agente al cliente. In questo scenario, l&#39;agente viene selezionato dinamicamente.

Assegna le attività e i passaggi Adobe Sign dei [flussi di lavoro incentrati su Forms su OSGi](/help/forms/using/aem-forms-workflow.md) forniscono opzioni per selezionare dinamicamente un utente. È possibile utilizzare i bundle ECMAScript o OSGi per selezionare dinamicamente un assegnatario per il passaggio Assegna attività o per selezionare i firmatari per il passaggio Firma documento.

## Utilizzare ECMAScript per selezionare dinamicamente un utente o un gruppo {#use-ecmascript-to-dynamically-select-a-user-or-group}

ECMAScript è un linguaggio di script. Viene utilizzato per applicazioni di script lato client e server. Esegui i seguenti passaggi per selezionare dinamicamente un utente o un gruppo utilizzando ECMAScript:

1. Apri CRXDE Lite. L&#39;URL è `https://'[server]:[port]'/crx/de/index.jsp`
1. Crea un file con estensione .ecma nel seguente percorso. Se il percorso (struttura del nodo) non esiste, crealo:

   * (Percorso del passaggio Assegna attività) `/apps/fd/dashboard/scripts/participantChooser`
   * (Percorso del passaggio firma) `/apps/fd/workflow/scripts/adobesign`

1. Aggiungi ECMAScript, che ha la logica per selezionare dinamicamente un utente, al file .ecma. Fare clic su **[!UICONTROL Salva tutto]**.

   Per script di esempio, vedere [Esempi ECMAScripts per la selezione dinamica di un utente o di un gruppo](/help/forms/using/dynamically-select-a-user-or-group-for-aem-workflow.md#sample-ecmascripts-to-dynamically-choose-a-user-or-a-group).

1. Aggiungi il nome visualizzato dello script. Questo nome viene visualizzato nei passaggi del flusso di lavoro. Per specificare il nome:

   1. Espandi il nodo dello script, fai clic con il pulsante destro del mouse sul nodo **[!UICONTROL jcr:content]** e fai clic su **[!UICONTROL Mixins]**.
   1. Aggiungi la proprietà `mix:title` nella finestra di dialogo Modifica mixin e fai clic su **OK**.
   1. Aggiungi la seguente proprietà al nodo jcr:content dello script:

      | Nome | Tipo | Valore |
      |--- |--- |--- |
      | jcr:title | Stringa | Specifica il nome dello script. Ad esempio, Scegliere l’agente campo più vicino. Questo nome viene visualizzato nei passaggi Assegna attività e Firma documento . |

   1. Fare clic su **Salva tutto**. Lo script diventa disponibile per la selezione nei componenti di AEM flusso di lavoro.

      ![script](assets/script.png)

### Esempio di script ECMAS per scegliere dinamicamente un utente o un gruppo {#sample-ecmascripts-to-dynamically-choose-a-user-or-a-group}

Nell&#39;esempio seguente ECMAScript viene selezionato dinamicamente un assegnatario per il passaggio Assegna attività. In questo script, viene selezionato un utente in base al percorso del payload. Prima di utilizzare questo script, assicurati che tutti gli utenti menzionati nello script siano presenti in AEM. Se gli utenti menzionati nello script non esistono in AEM, il processo correlato potrebbe non riuscire.

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

Nell&#39;esempio seguente ECMAScript viene selezionato dinamicamente un assegnatario per il passaggio Adobe Sign. Prima di utilizzare lo script seguente, assicurati che le informazioni utente (indirizzi e-mail e numeri di telefono) menzionate nello script siano corrette. Se le informazioni utente menzionate nello script non sono corrette, il processo correlato potrebbe non riuscire.

>[!NOTE]
>
>Quando si utilizza ECMAScript per Adobe Sign, lo script deve trovarsi in crx-repository all&#39;indirizzo /apps/fd/workflow/scripts/adobesign/ e deve avere una funzione chiamata getAdobeSignRecipients per restituire un elenco di utenti.

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

## Usa l&#39;interfaccia Java per scegliere dinamicamente un utente o un gruppo {#use-java-interface-to-dynamically-choose-a-user-or-group}

È possibile utilizzare l&#39;interfaccia Java [RecipientInfoSpecifier](https://www.adobe.io/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) per scegliere in modo dinamico un utente o un gruppo per i passaggi Adobe Sign e Assegna attività. Puoi creare un bundle OSGi che utilizzava l&#39;interfaccia Java [RecipientInfoSpecifier](https://www.adobe.io/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) e distribuirla al server AEM Forms. Rende disponibile l’opzione per la selezione nei componenti Assegna attività e Adobe Sign di AEM flusso di lavoro.

Per compilare il codice di esempio riportato di seguito, è necessario disporre di file jar [SDK client AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) e di file jar [granite](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.workflow.api/1.0.2/) per compilare l&#39;esempio di codice riportato di seguito. Aggiungi questi file jar come dipendenze esterne al progetto di bundle OSGi. Puoi utilizzare qualsiasi Java IDE per creare un bundle OSGi. La procedura seguente fornisce i passaggi per utilizzare Eclipse per creare un bundle OSGi:

1. Apri Eclipse IDE. Passa a **[!UICONTROL File]**> **[!UICONTROL Nuovo progetto]**.
1. Nella schermata Seleziona una procedura guidata, seleziona **[!UICONTROL Progetto Maven]** e fai clic su **[!UICONTROL Avanti]**.
1. Nel nuovo progetto Maven, mantieni i valori predefiniti e fai clic su **[!UICONTROL Avanti]**. Seleziona un archetipo e fai clic su **[!UICONTROL Avanti]**. Ad esempio, maven-archetype-quickstart. Specifica **[!UICONTROL ID gruppo]**, **[!UICONTROL ID artefatto]**, **[!UICONTROL versione]** e **[!UICONTROL pacchetto]** per il progetto, quindi fai clic su **[!UICONTROL Fine]**. Il progetto viene creato.
1. Apri il file pom.xml per la modifica e sostituisci tutti i contenuti del file con quanto segue:

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
               <url>https://repo1.maven.org/maven2/com/adobe/</url>
               <layout>default</layout>
           </repository>
       </repositories>
       <pluginRepositories>
           <pluginRepository>
               <id>adobe</id>
               <name>Adobe Public Repository</name>
               <url>https://repo1.maven.org/maven2/com/adobe/</url>
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

1. Aggiungi il codice sorgente che utilizza l&#39;interfaccia Java [RecipientInfoSpecifier](https://www.adobe.io/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) per scegliere in modo dinamico un utente o un gruppo per il passaggio dell&#39;attività Assegna. Per un codice di esempio, vedi [Esempio per scegliere dinamicamente un utente o un gruppo utilizzando l&#39;interfaccia Java](#-sample-scripts-for).
1. Apri un prompt dei comandi e passa alla directory contenente il progetto di bundle OSGi. Utilizza il seguente comando per creare il bundle OSGi:

   `mvn clean install`

1. Carica il bundle su un server AEM Forms. Puoi utilizzare AEM Gestione pacchetti per importare il bundle nel server AEM Forms.

Dopo l’importazione del bundle, l’opzione per scegliere l’interfaccia Java per la selezione dinamica di un utente o di un gruppo diventa disponibile in per i passaggi Adobe Sign e Assegna attività .

### Esempio di codice Java per scegliere dinamicamente un utente o un gruppo {#sample-java-code-to-dynamically-choose-a-user-or-a-group}

Il codice di esempio seguente sceglie dinamicamente un assegnatario per il passaggio Adobe Sign. Usa il codice in un bundle OSGi. Prima di utilizzare il codice elencato di seguito, assicurati che le informazioni utente (indirizzi e-mail e numeri di telefono) menzionate nel codice siano corrette. Se le informazioni utente menzionate nel codice non sono corrette, il processo correlato può non riuscire.

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
