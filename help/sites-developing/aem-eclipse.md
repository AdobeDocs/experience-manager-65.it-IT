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

&quot;AEM Developer Tools&quot; è un plug-in di Eclipse basato su [Plug-in Eclipse per Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html) rilasciata con la Licenza Apache 2.

Offre diverse funzioni che facilitano lo sviluppo dell’AEM:

* Integrazione perfetta con le istanze AEM tramite il connettore del server Eclipse.
* Sincronizzazione sia per i bundle di contenuti che per quelli OSGI.
* Supporto del debug con funzionalità di hot-swapping del codice.
* Semplice Bootstrap di progetti AEM tramite una procedura guidata specifica per la creazione di progetti.
* Facile modifica delle proprietà JCR.

## Requisiti {#requirements}

Prima di utilizzare gli strumenti per sviluppatori dell’AEM, effettua le seguenti operazioni:

* Scarica e installa [IDE Eclipse per sviluppatori Java™ EE](https://www.eclipse.org/downloads/packages/release/luna/r/eclipse-ide-java-ee-developers). Gli strumenti per sviluppatori di AEM supportano attualmente Eclipse Kepler o versioni successive

* Può essere utilizzato con AEM versione 5.6.1 o successiva
* Configurare l&#39;installazione dell&#39;eclissi per assicurarsi di disporre di almeno 1 GB di memoria heap modificando `eclipse.ini` file di configurazione come descritto in [Domande frequenti su Eclipse](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse%3F).

>[!NOTE]
>
>In macOS, fai clic con il pulsante destro del mouse **Eclipse.app**, quindi selezionare **Mostra contenuto pacchetto** per trovare `eclipse.ini`.

## Come installare gli strumenti per sviluppatori AEM per Eclipse {#how-to-install-the-aem-developer-tools-for-eclipse}

Dopo aver soddisfatto le [requisiti](#requirements) sopra, è possibile installare il plug-in come segue:

1. Sfoglia **Strumenti per sviluppatori AEM** sito Web all&#39;indirizzo `https://eclipse.adobe.com/aem/dev-tools/`.

1. Copia il **Collegamento di installazione**.

   In alternativa, è possibile scaricare un archivio invece di utilizzare il collegamento di installazione. Questa operazione consente l’installazione offline, ma non le notifiche di aggiornamento automatico.

1. In Eclipse, apri il file **Aiuto** menu.
1. Clic **Installare un nuovo software**.
1. Clic **Aggiungi...**.
1. In entrata **Nome** digitare AEM Developer Tools.
1. In entrata **Posizione** copia l’URL di installazione.
1. Clic **Ok**.
1. Controlla entrambi **AEM** e **Sling** plug-in.
1. Fai clic su **Avanti**.
1. Fai clic su **Avanti**.
1. Accettare i contratti di linea e fare clic su **Fine**.
1. Clic **Sì** per riavviare Eclipse.

## Importare Progetti Esistenti {#how-to-import-existing-projects}

>[!NOTE]
>
>Consulta [Come lavorare con un bundle in Eclipse quando è stato scaricato da AEM](https://stackoverflow.com/questions/29699726/how-to-work-with-a-bundle-in-eclipse-when-it-was-downloaded-from-aem/29705407#29705407).

## La prospettiva dell&#39;AEM {#the-aem-perspective}

Gli strumenti di sviluppo AEM per Eclipse vengono forniti con una prospettiva che offre il pieno controllo sui tuoi progetti e istanze AEM.

![chlimage_1-2](assets/chlimage_1-2a.jpeg)

## Esempio di progetto con più moduli {#sample-multi-module-project}

Gli &quot;Strumenti per sviluppatori AEM&quot; includono un esempio di progetto con più moduli che ti consente di imparare rapidamente a utilizzare la configurazione di un progetto in Eclipse. Funge anche da guida alle best practice per diverse funzioni dell’AEM. [Ulteriori informazioni su Archetipo progetto](https://github.com/adobe/aem-project-archetype).

La procedura seguente illustra come creare il progetto di esempio:

1. In **File** > **Nuovo** > **Progetto** , passare al menu **AEM** sezione e seleziona **Esempio di progetto con più moduli AEM**.

   ![chlimage_1-69](assets/chlimage_1-69a.png)

1. Fai clic su **Avanti**.

   >[!NOTE]
   >
   >Questo passaggio potrebbe richiedere del tempo perché m2eclipse deve analizzare i cataloghi dell’archetipo.

   ![chlimage_1-70](assets/chlimage_1-70a.png)

1. Scegli **com.adobe.granite.archetypes : sample-project-archetype : (numero più alto)** dal menu, quindi fai clic su **Successivo**.

   ![chlimage_1-71](assets/chlimage_1-71a.png)

1. Compila un **Nome**, **ID gruppo**, e un **ID artefatto** per il progetto di esempio. Puoi anche scegliere di impostare alcune proprietà avanzate.

   ![chlimage_1-72](assets/chlimage_1-72a.png)

1. Ora configura un server AEM a cui Eclipse può connettersi.

   Per utilizzare la funzione di debugger, accertati di aver avviato AEM in modalità di debug aggiungendo quanto segue alla riga di comando:

   ```
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![chlimage_1-73](assets/chlimage_1-73a.png)

1. Clic **Fine**. Viene creata la struttura del progetto.

   >[!NOTE]
   >
   >In una nuova installazione (nello specifico, quando le dipendenze Maven non sono mai state scaricate) puoi creare il progetto con errori. In questo caso, seguire la procedura descritta in [Risoluzione di una definizione di progetto non valida](#resolving-invalid-project-definition).

## Risoluzione dei problemi {#troubleshooting}

### Risoluzione di una definizione di progetto non valida {#resolving-invalid-project-definition}

Per risolvere le dipendenze non valide e la definizione del progetto procedere come segue:

1. Seleziona tutti i progetti creati.
1. Fare clic con il pulsante destro del mouse. Nel menu **Maven**, seleziona **Aggiorna Progetti**.
1. Verifica **Forza aggiornamenti di snapshot/release**.
1. Fai clic su **OK**. Eclipse tenta di scaricare le dipendenze richieste.

### Abilitazione del completamento automatico della libreria di tag nei file JSP {#enabling-tag-library-autocompletion-in-jsp-files}

Il completamento automatico della libreria di tag funziona in modo predefinito, dato che al progetto vengono aggiunte le dipendenze appropriate. Esiste un problema noto quando si utilizza il file JAR Uber dell’AEM, che non include i file tld e TagExtraInfo necessari.

Per ovviare a questo problema, accertati che l’artefatto org.apache.sling.scripting.jsp.taglib si trovi nel percorso di classe prima del file JAR Uber dell’AEM. Per i progetti Maven, inserisci la seguente dipendenza nel file pom.xml prima del file JAR Uber.

```xml
<dependency>
  <groupId>org.apache.sling</groupId>
  <artifactId>org.apache.sling.scripting.jsp.taglib</artifactId>
  <scope>provided</scope>
</dependency>
```

Assicurati di aggiungere la versione corretta per la distribuzione dell’AEM.

## Ulteriori informazioni {#more-information}

Il sito web ufficiale Apache Sling IDE tooling per Eclipse fornisce informazioni utili:

* Il [**Strumenti IDE Apache Sling per Eclipse** Guida utente](https://sling.apache.org/documentation/development/ide-tooling.html), questa documentazione descrive i concetti generali, l’integrazione dei server e le funzionalità di implementazione supportate dagli strumenti di sviluppo AEM.
* Il [Sezione Risoluzione dei problemi](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting).
* Il [Elenco dei problemi noti](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues).

Il seguente funzionario [Eclipse](https://www.eclipse.org/) La documentazione di può essere utile per configurare l’ambiente:

* [Guida introduttiva a Eclipse](https://www.eclipse.org/getting-started/)
* [Guida di Eclipse Luna](https://help.eclipse.org/latest/index.jsp)
* [Integrazione Maven (m2eclipse)](https://www.eclipse.org/m2e/)
