---
title: Come sviluppare progetti AEM utilizzando Eclipse
seo-title: How to Develop AEM Projects Using Eclipse
description: Questa guida descrive come utilizzare Eclipse per sviluppare progetti basati su AEM
seo-description: This guide describes how to use Eclipse for developing AEM based projects
uuid: 79fee76f-6bcc-498f-af46-530816b41bbe
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: aa58cfb8-ec15-4698-a8f0-97683b0de51c
exl-id: 9d421599-0417-4329-a528-9cda4e3716f5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# Come sviluppare progetti AEM utilizzando Eclipse{#how-to-develop-aem-projects-using-eclipse}

Questa guida descrive come utilizzare Eclipse per lo sviluppo di progetti basati su AEM.

>[!NOTE]
>
>L&#39;Adobe ora fornisce [Strumenti di sviluppo AEM per Eclipse](/help/sites-developing/aem-eclipse.md) che consente di sviluppare soluzioni AEM con Eclipse.

## Panoramica {#overview}

Per iniziare a utilizzare AEM sviluppo su Eclipse, sono necessari i seguenti passaggi.

Ognuno di essi viene spiegato più dettagliatamente nel resto del presente How-To.

* Installa Eclipse 4.3 (Kepler)
* Imposta il progetto AEM in base a Maven
* Preparare il supporto JSP per Eclipse nel Maven POM
* Importare il progetto Maven in Eclipse

>[!NOTE]
>
>Questa guida si basa su Eclipse 4.3 (Kepler) e AEM 5.6.1.

## Installa Eclipse {#install-eclipse}

Scarica &quot;Eclipse IDE for Java EE Developers&quot; dal [Pagina Download di Eclipse](https://www.eclipse.org/downloads/).

Installa Eclipse seguendo la [Istruzioni di installazione](https://wiki.eclipse.org/Eclipse/Installation).

## Imposta il progetto AEM in base a Maven {#set-up-your-aem-project-based-on-maven}

Quindi, imposta il progetto utilizzando Maven come descritto in [Come generare progetti AEM con Apache Maven](/help/sites-developing/ht-projects-maven.md).

## Preparare il supporto JSP per Eclipse {#prepare-jsp-support-for-eclipse}

Eclipse può anche fornire supporto nell’utilizzo di JSP, ad esempio

* completamento automatico delle librerie di tag
* Consapevolezza di oggetti definiti da &lt;cq:defineobjects /> e &lt;sling:defineobjects />

Per questo lavoro:

1. Segui le istruzioni su [Come lavorare con i JSP](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps) in [Come generare progetti AEM con Apache Maven](/help/sites-developing/ht-projects-maven.md).
1. Aggiungi quanto segue al &lt;build /> nella sezione POM del modulo di contenuto.

   Il plugin di supporto Maven di Eclipse, m2e, non fornisce supporto per il maven-jspc-plugin, e questa configurazione dice a m2e di ignorare il plugin e il relativo compito di pulire i risultati di compilazione temporanea.

   Questo non è un problema: come indicato in [Come lavorare con i JSP](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps), il maven-jspc-plugin in questa configurazione viene utilizzato solo per convalidare che i JSP vengano compilati come parte del processo di creazione. Eclipse segnala già eventuali problemi in JSP e non si affida a questo plug-in Maven per poterlo fare.

   **myproject/content/pom.xml**

   ```xml
   <build>
     <!-- ... -->
     <pluginManagement>
       <plugins>
         <!--This plugin's configuration is used to store Eclipse m2e settings only. It has no influence on the Maven build itself.-->
         <plugin>
           <groupId>org.eclipse.m2e</groupId>
           <artifactId>lifecycle-mapping</artifactId>
           <version>1.0.0</version>
           <configuration>
             <lifecycleMappingMetadata>
               <pluginExecutions>
                 <pluginExecution>
                   <pluginExecutionFilter>
                     <groupId>org.apache.sling</groupId>
                     <artifactId>maven-jspc-plugin</artifactId>
                     <versionRange>[2.0.6,)</versionRange>
                     <goals>
                       <goal>jspc</goal>
                     </goals>
                   </pluginExecutionFilter>
                   <action>
                     <ignore/>
                   </action>
                 </pluginExecution>
                 <pluginExecution>
                   <pluginExecutionFilter>
                     <groupId>org.apache.maven.plugins</groupId>
                     <artifactId>maven-clean-plugin</artifactId>
                     <versionRange>[2.4.1,)</versionRange>
                     <goals>
                       <goal>clean</goal>
                     </goals>
                   </pluginExecutionFilter>
                   <action>
                     <ignore/>
                   </action>
                 </pluginExecution>
               </pluginExecutions>
             </lifecycleMappingMetadata>
           </configuration>
         </plugin>
       </plugins>
     </pluginManagement>
   </build>
   ```

### Importare il progetto Maven in Eclipse {#import-the-maven-project-into-eclipse}

1. In Eclipse, scegli File > Importa...
1. Nella finestra di dialogo Importa, scegli Maven > Progetti Maven esistenti, quindi fai clic su &quot;Successivo&quot;.

   ![chlimage_1-41](assets/chlimage_1-41a.png)

1. Inserisci il percorso della cartella di livello principale del progetto, quindi fai clic su &quot;Seleziona tutto&quot; e &quot;Fine&quot;.

   ![chlimage_1-42](assets/chlimage_1-42a.png)

1. Ora sei impostato per l’utilizzo di Eclipse per sviluppare il progetto AEM, incluso il completamento automatico JSP.

   ![chlimage_1-43](assets/chlimage_1-43a.png)

   >[!NOTE]
   >
   >Se include `/libs/foundation/global.jsp` o altri JSP in `/libs`, sarà necessario copiarlo nel progetto in modo che Eclipse possa risolvere l’inclusione. Allo stesso tempo, assicurati che Maven non includa nel pacchetto di contenuti. Come ottenere questo risultato è descritto in [Come creare progetti AEM utilizzando Apache Maven](/help/sites-developing/ht-projects-maven.md).
