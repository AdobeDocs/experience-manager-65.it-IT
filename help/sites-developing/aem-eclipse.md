---
title: Strumenti AEM Developer per Eclipse
seo-title: AEM Developer Tools for Eclipse
description: Strumenti AEM Developer per Eclipse
seo-description: null
uuid: 566e49f2-6f28-4aa7-bfe0-b5f9675310bf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: a2ae76a8-50b0-4e43-b791-ad3be25b8582
exl-id: 00473769-c447-4966-a71e-117c669e0151
source-git-commit: 71842228dd3cb1ce3b79728912e8333d25fccefc
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 4%

---

# Strumenti AEM Developer per Eclipse{#aem-developer-tools-for-eclipse}

![](do-not-localize/chlimage_1-9.png)

## Panoramica {#overview}

&quot;AEM Developer Tools&quot; è un plug-in Eclipse basato su [Plug-in Eclipse per Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html) rilasciato sotto la Licenza Apache 2.

Offre diverse funzioni che semplificano AEM sviluppo:

* Integrazione perfetta con le istanze AEM tramite Eclipse Server Connector.
* Sincronizzazione per i bundle OSGI e di contenuto.
* Supporto per il debug con funzionalità di hot swap del codice.
* Bootstrap semplice di progetti AEM mediante una Creazione guidata progetto specifica.
* Facile editing delle proprietà JCR.

## Requisiti {#requirements}

Prima di utilizzare gli strumenti per sviluppatori AEM, procedi come segue:

* Scarica e installa [IDE Eclipse per sviluppatori Java™ EE](https://www.eclipse.org/downloads/packages/release/luna/r/eclipse-ide-java-ee-developers). AEM Developer Tools supporta attualmente Eclipse Kepler o versioni successive

* Può essere utilizzato con AEM versione 5.6.1 o successiva
* Configura l&#39;installazione dell&#39;eclipse per assicurarti di disporre di almeno 1 GB di memoria heap modificando il tuo `eclipse.ini` file di configurazione come descritto in [Domande frequenti su Eclipse](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse%3F).

>[!NOTE]
>
>Su macOS, fai clic con il pulsante destro del mouse **Eclipse.app**, quindi seleziona **Mostra contenuto del pacchetto** per trovare il `eclipse.ini`.

## Come installare AEM Developer Tools per Eclipse {#how-to-install-the-aem-developer-tools-for-eclipse}

Una volta realizzato il [requisiti](#requirements) sopra, è possibile installare il plug-in come segue:

1. Sfoglia il **Strumenti per sviluppatori AEM** sito web `https://eclipse.adobe.com/aem/dev-tools/`.

1. Copia il **Collegamento di installazione**.

   In alternativa, puoi scaricare un archivio invece di utilizzare il collegamento di installazione. In questo modo l&#39;installazione offline viene abilitata, ma le notifiche di aggiornamento automatico vengono perse.

1. In Eclipse, apri la **Aiuto** menu.
1. Fai clic su **Installazione di un nuovo software**.
1. Fai clic su **Aggiungi..**.
1. In **Nome** digitare AEM strumenti per sviluppatori.
1. In **Posizione** copia l’URL di installazione.
1. Fai clic su **Ok**.
1. Controlla entrambi **AEM** e **Sling** plugin.
1. Fai clic su **Avanti**.
1. Fai clic su **Avanti**.
1. Accetta gli accordi di collegamento e fai clic su **Fine**.
1. Fai clic su **Sì** per riavviare Eclipse.

## Importazione di progetti esistenti {#how-to-import-existing-projects}

>[!NOTE]
>
>Vedi [Come lavorare con un bundle in Eclipse quando è stato scaricato da AEM](https://stackoverflow.com/questions/29699726/how-to-work-with-a-bundle-in-eclipse-when-it-was-downloaded-from-aem/29705407#29705407).

## La prospettiva AEM {#the-aem-perspective}

Gli strumenti di sviluppo AEM per Eclipse vengono forniti con una prospettiva che offre il pieno controllo sui progetti e le istanze AEM.

![chlimage_1-2](assets/chlimage_1-2a.jpeg)

## Esempio di progetto con più moduli {#sample-multi-module-project}

Gli &quot;AEM Developer Tools&quot; includono un progetto campione con più moduli che consente di imparare rapidamente a usare una configurazione di progetto in Eclipse. Funge anche da guida alle best practice per diverse funzioni AEM. [Ulteriori informazioni su Project Archetype](https://github.com/adobe/aem-project-archetype).

Per creare il progetto di esempio, completa i passaggi seguenti:

1. In **File** > **Nuovo** > **Progetto** menu, passare alla **AEM** e seleziona **Progetto AEM modulo multiplo di esempio**.

   ![chlimage_1-69](assets/chlimage_1-69a.png)

1. Fai clic su **Avanti**.

   >[!NOTE]
   >
   >Questo passaggio potrebbe richiedere un po&#39; perché m2eclipse deve eseguire la scansione dei cataloghi archetype.

   ![chlimage_1-70](assets/chlimage_1-70a.png)

1. Scegli **com.adobe.granite.archetipi : sample-project-archetype : (numero più alto)** dal menu , quindi fai clic su **Successivo**.

   ![chlimage_1-71](assets/chlimage_1-71a.png)

1. Compila un **Nome**, **ID gruppo** e un **ID dell&#39;artefatto** per il progetto di esempio. Puoi anche scegliere di impostare alcune proprietà avanzate.

   ![chlimage_1-72](assets/chlimage_1-72a.png)

1. Ora configura un server AEM a cui Eclipse può connettersi.

   Per utilizzare la funzione di debug, assicurati di aver avviato AEM in modalità di debug, ottenibile aggiungendo quanto segue alla riga di comando:

   ```
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![chlimage_1-73](assets/chlimage_1-73a.png)

1. Fai clic su **Fine**. Viene creata la struttura del progetto.

   >[!NOTE]
   >
   >Su un nuovo impianto (più precisamente: quando le dipendenze maven non sono mai state scaricate) puoi ottenere la creazione del progetto con errori. In questo caso, segui la procedura descritta in [Risoluzione della definizione del progetto non valida](#resolving-invalid-project-definition).

## Risoluzione dei problemi {#troubleshooting}

### Risoluzione della definizione del progetto non valida {#resolving-invalid-project-definition}

Per risolvere le dipendenze non valide e la definizione del progetto procedere come segue:

1. Seleziona tutti i progetti creati.
1. Fai clic con il pulsante destro del mouse. Nel menu **Maven**, seleziona **Aggiorna progetti**.
1. Controlla **Forza aggiornamenti di snapshot/release**.
1. Fai clic su **OK**. Eclipse cerca di scaricare le dipendenze richieste.

### Abilitazione del completamento automatico della libreria tag nei file JSP {#enabling-tag-library-autocompletion-in-jsp-files}

Il completamento automatico della libreria di tag funziona automaticamente, dato che le dipendenze corrette vengono aggiunte al progetto. C&#39;è un problema noto quando si utilizza il Jar Uber AEM, che non include i file tld e TagExtraInfo necessari.

Per aggirare questo problema, accertati che l’artefatto org.apache.sling.scripting.jsp.taglib sia nel percorso classico prima del Jar Uber AEM. Per i progetti Maven, inserisci la seguente dipendenza nel file pom.xml prima del file JAR Uber.

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

* La [**Strumenti Apache Sling IDE per Eclipse** Guida utente](https://sling.apache.org/documentation/development/ide-tooling.html), questa documentazione illustra i concetti generali, l’integrazione dei server e le funzionalità di distribuzione supportate dagli strumenti di sviluppo di AEM.
* La [Sezione Risoluzione dei problemi](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting).
* La [Elenco dei problemi noti](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues).

funzionario [Eclipse](https://www.eclipse.org/) può essere utile per configurare l’ambiente:

* [Guida introduttiva di Eclipse](https://www.eclipse.org/getting-started/)
* [Sistema di Aiuto di Eclipse Luna](https://help.eclipse.org/latest/index.jsp)
* [Integrazione Maven (m2eclipse)](https://www.eclipse.org/m2e/)
