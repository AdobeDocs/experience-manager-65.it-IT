---
title: Come sviluppare AEM progetti con Eclipse
seo-title: Come sviluppare AEM progetti con Eclipse
description: Questa guida descrive come utilizzare Eclipse per sviluppare progetti basati su AEM
seo-description: Questa guida descrive come utilizzare Eclipse per sviluppare progetti basati su AEM
uuid: 79fee76f-6bcc-498f-af46-530816b41bbe
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: aa58cfb8-ec15-4698-a8f0-97683b0de51c
translation-type: tm+mt
source-git-commit: 06f1f753b9bb7f7336454f166e03f753e3735a16
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---


# Come sviluppare AEM progetti con Eclipse{#how-to-develop-aem-projects-using-eclipse}

Questa guida descrive come utilizzare Eclipse per sviluppare progetti basati su AEM.

>[!NOTE]
>
> Adobe ora fornisce gli [AEM strumenti di sviluppo per Eclipse](/help/sites-developing/aem-eclipse.md) che aiutano a sviluppare soluzioni AEM con Eclipse.

## Panoramica {#overview}

Per iniziare AEM sviluppo su Eclipse, sono necessari i seguenti passaggi.

Ognuno di essi viene spiegato più dettagliatamente nel resto del presente Procedura.

* Installazione di Eclipse 4.3 (Kepler)
* Imposta il progetto AEM in base al cielo
* Preparare il supporto JSP per Eclipse nel Maven POM
* Importa progetto Paradiso in Eclipse

>[!NOTE]
>
>Questa guida si basa su Eclipse 4.3 (Kepler) e AEM 5.6.1.

## Installazione di Eclipse {#install-eclipse}

Scaricate &quot;Eclipse IDE for Java EE Developers&quot; dalla pagina [Download Eclipse](https://www.eclipse.org/downloads/).

Installate Eclipse seguendo le [istruzioni di installazione](https://wiki.eclipse.org/Eclipse/Installation).

## Imposta il progetto AEM in base a Maven {#set-up-your-aem-project-based-on-maven}

Configurate quindi il progetto utilizzando Maven come descritto in [How-To Build AEM Projects using Apache Maven](/help/sites-developing/ht-projects-maven.md) (Creazione di progetti con Apache Maven).

## Preparazione del supporto JSP per Eclipse {#prepare-jsp-support-for-eclipse}

Eclipse può anche fornire supporto nell&#39;utilizzo di JSP, ad esempio

* completamento automatico delle librerie di tag
* Consapevolezza Eclipse degli oggetti definiti da &lt;cq:defineObjects /> e &lt;sling:defineObjects />

Per farlo funzionare:

1. Seguite le istruzioni riportate in [How-To Work with JSP](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps) in [How-To Build AEM Projects using Apache Maven](/help/sites-developing/ht-projects-maven.md) (Come lavorare con JSP&lt;a1/> in &lt;a2/>How-To Build Projects using Apache Maven).
1. Aggiungi quanto segue alla sezione &lt;build /> nel POM del modulo di contenuto.

   Il plugin di supporto Maven di Eclipse, m2e, non fornisce supporto per il maven-jspc-plugin, e questa configurazione dice a m2e di ignorare il plugin e il relativo compito di pulire i risultati di compilazione temporanea.

   Questo non è un problema: come indicato in [How-To Work with JSP](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps), il maven-jspc-plugin in in questa configurazione è utilizzato solo per convalidare che i JSP siano compilati come parte del processo di compilazione. Eclipse segnala già eventuali problemi in JSP e non si affida a questo plugin Maven per essere in grado di farlo.

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

### Importa progetto Paradiso in Eclipse {#import-the-maven-project-into-eclipse}

1. In Eclipse, scegliete File > Importa...
1. Nella finestra di dialogo Importa, scegliete Paradiso > Progetti Paradiso esistenti, quindi fate clic su &quot;Avanti&quot;.

   ![chlimage_1-41](assets/chlimage_1-41a.png)

1. Inserite il percorso della cartella di livello principale del progetto, quindi fate clic su &quot;Seleziona tutto&quot; e &quot;Fine&quot;.

   ![chlimage_1-42](assets/chlimage_1-42a.png)

1. Ora tutti siete pronti per utilizzare Eclipse per sviluppare il progetto AEM, incluso il completamento automatico JSP.

   ![chlimage_1-43](assets/chlimage_1-43a.png)

   >[!NOTE]
   >
   >Se includi `/libs/foundation/global.jsp` o altri JSP in `/libs`, dovrai copiarli nel progetto in modo che Eclipse possa risolvere l&#39;inclusione. Allo stesso tempo, è necessario assicurarsi che non sia incluso nel pacchetto di contenuti da Maven. Come raggiungere questo obiettivo è descritto in [Come creare progetti AEM con Apache Maven](/help/sites-developing/ht-projects-maven.md).

