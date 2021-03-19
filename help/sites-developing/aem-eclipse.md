---
title: AEM Developer Tools per Eclipse
seo-title: AEM Developer Tools per Eclipse
description: AEM Developer Tools per Eclipse
seo-description: 'null'
uuid: 566e49f2-6f28-4aa7-bfe0-b5f9675310bf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: a2ae76a8-50b0-4e43-b791-ad3be25b8582
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 2%

---


# AEM Developer Tools per Eclipse{#aem-developer-tools-for-eclipse}

![](do-not-localize/chlimage_1-9.png)

## Panoramica {#overview}

AEM Developer Tools per Eclipse è un plug-in Eclipse basato sul [plug-in Eclipse per Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html) rilasciato sotto la Licenza Apache 2.

Offre diverse funzioni che semplificano AEM sviluppo:

* Integrazione perfetta con le istanze AEM tramite Eclipse Server Connector.
* Sincronizzazione per i bundle OSGI e di contenuto.
* Supporto per il debug con funzionalità di hot swap del codice.
* Bootstrap semplice dei progetti AEM tramite una Creazione guidata progetto specifica.
* Facile editing delle proprietà JCR.

## Requisiti {#requirements}

Prima di utilizzare gli strumenti per sviluppatori AEM, è necessario:

* Scarica e installa [Eclipse IDE for Java EE Developers](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar). AEM Developer Tools supporta attualmente Eclipse Kepler o versioni successive

* Può essere utilizzato con AEM versione 5.6.1 o successiva
* Configura l&#39;installazione dell&#39;eclissi per assicurarti di disporre di almeno 1 gigabyte di memoria heap modificando il file di configurazione `eclipse.ini` come descritto in [Eclipse FAQ](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse%3F).

>[!NOTE]
>
>Su macOS, è necessario fare clic con il pulsante destro del mouse su **Eclipse.app** e quindi selezionare **Mostra contenuto pacchetto** per trovare il `eclipse.ini`**.**

## Come installare AEM Developer Tools per Eclipse {#how-to-install-the-aem-developer-tools-for-eclipse}

Una volta soddisfatti i [requisiti](#requirements) di cui sopra, è possibile installare il plug-in come segue:

1. Sfoglia il [**AEM** sito Web Developer Tools](https://eclipse.adobe.com/aem/dev-tools/).

1. Copia il **collegamento di installazione**.

   In alternativa, puoi scaricare un archivio invece di utilizzare il collegamento di installazione. Questo consente l’installazione offline ma in questo modo le notifiche di aggiornamento automatico verranno perse.

1. In Eclipse, apri il menu **Help** .
1. Fare clic su **Installa nuovo software**.
1. Fate clic su **Aggiungi...**.
1. In **Name** digitare AEM strumenti per sviluppatori.
1. In **Posizione** copia l&#39;URL di installazione.
1. Fare clic su **Ok**.
1. Controlla i plug-in **AEM** e **Sling**.
1. Fai clic su **Avanti**.
1. Fai clic su **Avanti**.
1. Accettate i contratti di collegamento e fate clic su **Fine**.
1. Fare clic su **Sì** per riavviare Eclipse.

## Come importare progetti esistenti {#how-to-import-existing-projects}

>[!NOTE]
>
>Vedi [Come lavorare con un bundle in Eclipse quando è stato scaricato da AEM](https://stackoverflow.com/questions/29699726/how-to-work-with-a-bundle-in-eclipse-when-it-was-downloaded-from-aem/29705407#29705407).

## La prospettiva AEM {#the-aem-perspective}

Gli strumenti di sviluppo AEM per Eclipse vengono forniti con una prospettiva che offre il pieno controllo sui progetti e le istanze AEM.

![chlimage_1-2](assets/chlimage_1-2a.jpeg)

## Progetto Multi-Modulo di esempio {#sample-multi-module-project}

AEM Developer Tools per Eclipse viene fornito con un progetto campione con più moduli che consente di imparare rapidamente a usare una configurazione di progetto in Eclipse, oltre a fungere da guida pratica per diverse funzioni AEM. [Ulteriori informazioni su Project Archetype](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype).

Per creare il progetto di esempio, effettua le seguenti operazioni:

1. Nel menu **File** > **Nuovo** > **Progetto**, passa alla sezione **AEM** e seleziona **AEM Progetto modulo multiplo di esempio**.

   ![chlimage_1-69](assets/chlimage_1-69a.png)

1. Fai clic su **Avanti**.

   >[!NOTE]
   >
   >Questo passaggio potrebbe richiedere un po’ di tempo, dato che m2eclipse deve eseguire la scansione dei cataloghi archetype.

   ![chlimage_1-70](assets/chlimage_1-70a.png)

1. Scegli **com.adobe.granite.archetipi : sample-project-archetype : (numero più alto)** dal menu, quindi fare clic su **Avanti**.

   ![chlimage_1-71](assets/chlimage_1-71a.png)

1. Compila un **Nome**, **ID gruppo** e un **ID elemento** per il progetto di esempio. Puoi anche scegliere di impostare alcune proprietà avanzate.

   ![chlimage_1-72](assets/chlimage_1-72a.png)

1. È quindi necessario configurare un server AEM a cui Eclipse si connetterà.

   Per utilizzare la funzione di debug, è necessario aver avviato AEM in modalità di debug, che può essere ottenuta, ad esempio, aggiungendo quanto segue alla riga di comando:

   ```
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![chlimage_1-73](assets/chlimage_1-73a.png)

1. Fare clic su **Fine**. Viene creata la struttura del progetto.

   >[!NOTE]
   >
   >Su un nuovo impianto (più precisamente: quando le dipendenze maven non sono mai state scaricate) puoi ottenere la creazione del progetto con errori. In questo caso, segui la procedura descritta in [Risoluzione della definizione di progetto non valida](#resolving-invalid-project-definition).

## Risoluzione dei problemi {#troubleshooting}

### Risoluzione della definizione del progetto non valida {#resolving-invalid-project-definition}

Per risolvere le dipendenze non valide e la definizione del progetto procedere come segue:

1. Seleziona tutti i progetti creati.
1. Fai clic con il pulsante destro del mouse. Nel menu **Maven** seleziona **Aggiorna progetti**.
1. Controllare **Force Updates of Snapshot/Release**.
1. Fai clic su **OK**. Eclipse cerca di scaricare le dipendenze richieste.

### Abilitazione del completamento automatico della libreria tag nei file JSP {#enabling-tag-library-autocompletion-in-jsp-files}

Il completamento automatico della libreria di tag funziona automaticamente, dato che le dipendenze corrette vengono aggiunte al progetto. C&#39;è un problema noto quando si utilizza il Jar Uber AEM, che non include i file tld e TagExtraInfo necessari.

Per aggirare questo problema, accertati che l’artefatto org.apache.sling.scripting.jsp.taglib sia situato nel percorso classico prima del Jar Uber AEM. Per i progetti Maven, inserisci la seguente dipendenza nel file pom.xml prima del file JAR Uber.

```xml
<dependency>
  <groupId>org.apache.sling</groupId>
  <artifactId>org.apache.sling.scripting.jsp.taglib</artifactId>
  <scope>provided</scope>
</dependency>
```

Assicurati di aggiungere la versione corretta per la distribuzione di AEM.

## Ulteriori informazioni {#more-information}

Il sito web ufficiale Apache Sling IDE tooling for Eclipse fornisce informazioni utili:

* La [**guida utente Apache Sling IDE tooling for Eclipse**](https://sling.apache.org/documentation/development/ide-tooling.html), questa documentazione ti guiderà attraverso i concetti generali, le funzionalità di integrazione e distribuzione dei server supportate dagli strumenti di sviluppo AEM.
* La sezione [Risoluzione dei problemi](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting).
* Elenco [Problemi noti](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues).

La seguente documentazione ufficiale [Eclipse](https://eclipse.org/) può aiutare a configurare l&#39;ambiente:

* [Guida introduttiva di Eclipse](https://eclipse.org/users/)
* [Sistema di Aiuto di Eclipse Luna](https://help.eclipse.org/luna/index.jsp)
* [Integrazione Maven (m2eclipse)](https://www.eclipse.org/m2e/)

