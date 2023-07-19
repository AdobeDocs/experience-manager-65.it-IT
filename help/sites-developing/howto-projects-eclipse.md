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
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---

# Come sviluppare progetti AEM utilizzando Eclipse{#how-to-develop-aem-projects-using-eclipse}

Questa guida descrive come utilizzare Eclipse per sviluppare progetti basati su AEM.

>[!NOTE]
>
>L&#39;Adobe ora fornisce [Strumenti di sviluppo AEM per Eclipse](/help/sites-developing/aem-eclipse.md) che consente di sviluppare soluzioni per l’AEM con Eclipse.

## Panoramica {#overview}

Per iniziare a sviluppare l’AEM su Eclipse, sono necessari i seguenti passaggi.

Ognuno di essi viene spiegato più dettagliatamente nel resto di questa procedura.

* Installare Eclipse 4.3 (Kepler)
* Configurare il progetto AEM in base a Maven
* Preparare il supporto JSP per Eclipse nel POM Maven
* Importare il progetto Maven in Eclipse

>[!NOTE]
>
>Questa guida si basa su Eclipse 4.3 (Kepler) e AEM 5.6.1.

## Installare Eclipse {#install-eclipse}

Scarica l’&quot;IDE Eclipse per sviluppatori Java EE&quot; da [Pagina Download di Eclipse](https://www.eclipse.org/downloads/).

Installa Eclipse seguendo la [Istruzioni di installazione](https://wiki.eclipse.org/Eclipse/Installation).

## Configurare il progetto AEM in base a Maven {#set-up-your-aem-project-based-on-maven}

Quindi, imposta il progetto utilizzando Maven come descritto in [Come creare progetti AEM con Apache Maven](/help/sites-developing/ht-projects-maven.md).

## Preparare il supporto JSP per Eclipse {#prepare-jsp-support-for-eclipse}

Eclipse può anche fornire supporto nell’utilizzo di JSP, ad esempio,

* completamento automatico delle librerie di tag
* Eclipse-awareness degli oggetti definiti da &lt;cq:defineobjects /> e &lt;sling:defineobjects />

Perché ciò funzioni:

1. Segui le istruzioni su [Come utilizzare le JSP](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps) in [Come creare progetti AEM con Apache Maven](/help/sites-developing/ht-projects-maven.md).
1. Aggiungi quanto segue a &lt;build /> nel POM del modulo dei contenuti.

   Il plug-in di supporto Maven di Eclipse, m2e, non fornisce il supporto per maven-jspc-plugin, e questa configurazione dice a m2e di ignorare il plug-in e l’attività correlata di pulizia dei risultati della compilazione temporanea.

   Questo non è un problema: come indicato in [Come utilizzare le JSP](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps), il maven-jspc-plugin in questa configurazione viene utilizzato solo per convalidare la compilazione dei JSP come parte del processo di build. Eclipse segnala già qualsiasi problema nei JSP e non si basa su questo plug-in Maven per poterlo fare.

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

1. In Eclipse, scegliete File > Importa...
1. Nella finestra di dialogo Importa, scegli Maven > Progetti Maven esistenti, quindi fai clic su &quot;Successivo&quot;.

   ![chlimage_1-41](assets/chlimage_1-41a.png)

1. Inserisci il percorso della cartella principale del progetto, quindi fai clic su &quot;Seleziona tutto&quot; e &quot;Fine&quot;.

   ![chlimage_1-42](assets/chlimage_1-42a.png)

1. Ora è tutto pronto per utilizzare Eclipse per sviluppare il progetto AEM, incluso il completamento automatico JSP.

   ![chlimage_1-43](assets/chlimage_1-43a.png)

   >[!NOTE]
   >
   >Se includi `/libs/foundation/global.jsp` o altre JSP in `/libs`, dovrai copiarlo nel progetto in modo che Eclipse possa risolvere l’inclusione. Allo stesso tempo, devi accertarti che non sia incluso nel pacchetto di contenuti da Maven. Come ottenere questo risultato è descritto in [Come creare progetti AEM con Apache Maven](/help/sites-developing/ht-projects-maven.md).
