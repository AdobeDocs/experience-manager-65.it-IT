---
title: Strumenti per sviluppatori AEM per Eclipse
seo-title: Strumenti per sviluppatori AEM per Eclipse
description: 'null'
seo-description: 'null'
uuid: 566e49f2-6f28-4aa7-bfe0-b5f9675310bf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: a2ae76a8-50b0-4e43-b791-ad3be25b8582
translation-type: tm+mt
source-git-commit: 6d216e7521432468a01a29ad2879f8708110d970

---


# Strumenti per sviluppatori AEM per Eclipse{#aem-developer-tools-for-eclipse}

![](do-not-localize/chlimage_1-9.png)

## Panoramica {#overview}

AEM Developer Tools for Eclipse è un plug-in Eclipse basato sul plug-in [Eclipse per Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html) rilasciato sotto la licenza Apache 2.

Offre diverse funzioni che semplificano lo sviluppo di AEM:

* Integrazione perfetta con le istanze AEM tramite il connettore Eclipse Server.
* Sincronizzazione sia per il contenuto che per i bundle OSGI.
* Supporto per il debug con la funzionalità di sostituzione del codice.
* Avvio semplice di progetti AEM tramite una procedura guidata specifica per la creazione di progetti.
* Facile modifica delle proprietà JCR.

## Requisiti {#requirements}

Prima di utilizzare AEM Developer Tools, è necessario:

* Scaricate e installate [Eclipse IDE per sviluppatori](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar)Java EE. AEM Developer Tools supporta attualmente Eclipse Kepler o versioni successive

* Può essere utilizzato con AEM versione 5.6.1 o successiva
* Configurate l&#39;installazione dell&#39;eclisse per garantire che possiate disporre di almeno 1 gigabyte di memoria heap modificando il file di `eclipse.ini` configurazione come descritto nelle domande frequenti [Eclipse](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse%3F).

>[!NOTE]
>
>In macOS, per trovare il contenuto **del pacchetto è necessario fare clic con il pulsante destro del mouse su** Eclipse.app **, quindi selezionare** Mostra contenuto `eclipse.ini`**pacchetto.**

## Come installare AEM Developer Tools per Eclipse {#how-to-install-the-aem-developer-tools-for-eclipse}

Una volta soddisfatti i [requisiti](#requirements) di cui sopra, potete installare il plug-in come segue:

1. Sfogliate il sito Web [**AEM **Developer Tools](https://eclipse.adobe.com/aem/dev-tools/).

1. Copiate il collegamento **all’** installazione.

   In alternativa potete scaricare un archivio invece di utilizzare il collegamento di installazione. Questo consente l&#39;installazione offline, ma in questo modo non riceverete notifiche di aggiornamento automatico.

1. In Eclipse, aprite il menu **Aiuto** .
1. Fate clic su **Installa nuovo software**.
1. Fate clic su **Aggiungi...**.
1. In **Nome** , digitate Strumenti per sviluppatori AEM.
1. In **Location** copiate l’URL di installazione.
1. Click **Ok**.
1. Controllate entrambi i plug-in **AEM** e **Sling** .
1. Fai clic su **Avanti**.
1. Fai clic su **Avanti**.
1. Accettate gli accordi di collegamento e fate clic su **Fine**.
1. Fate clic su **Sì** per riavviare Eclipse.

## Come importare progetti esistenti {#how-to-import-existing-projects}

>[!NOTE]
>
>Consultate [Come utilizzare un bundle in Eclipse scaricato da AEM](https://stackoverflow.com/questions/29699726/how-to-work-with-a-bundle-in-eclipse-when-it-was-downloaded-from-aem/29705407#29705407).

## La prospettiva AEM {#the-aem-perspective}

Gli strumenti di sviluppo AEM per Eclipse vengono forniti con una prospettiva che offre il pieno controllo sui progetti e le istanze AEM.

![chlimage_1-2](assets/chlimage_1-2a.jpeg)

## Esempio di progetto con più moduli {#sample-multi-module-project}

Gli strumenti per sviluppatori AEM per Eclipse sono dotati di un progetto di esempio con più moduli che consente di velocizzare rapidamente la procedura di configurazione di un progetto in Eclipse e di fungere da guida best practice per diverse funzioni di AEM. [Ulteriori informazioni su Project Archetype](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype).

Per creare il progetto di esempio, effettuate le seguenti operazioni:

1. Nel menu **File** > **Nuovo** > **Progetto** , andate alla sezione **AEM** e selezionate **AEM Sample Multi-Module Project**.

   ![chlimage_1-69](assets/chlimage_1-69a.png)

1. Fai clic su **Avanti**.

   >[!NOTE]
   >
   >Questo passaggio potrebbe richiedere un po&#39; perché m2eclipse deve eseguire la scansione dei cataloghi archetype.

   ![chlimage_1-70](assets/chlimage_1-70a.png)

1. Scegliete **com.adobe.granite.archetypes : sample-project-archetype : (numero più alto)** dal menu, quindi fate clic su **Avanti**.

   ![chlimage_1-71](assets/chlimage_1-71a.png)

1. Compilate un **Nome**, un ID **** gruppo e un ID **** articolo per il progetto di esempio. Potete anche scegliere di impostare alcune proprietà avanzate.

   ![chlimage_1-72](assets/chlimage_1-72a.png)

1. È quindi necessario configurare un server AEM a cui Eclipse si connetterà.

   Per utilizzare la funzione Debugger, è necessario avviare AEM in modalità debug, che può essere ottenuta ad esempio aggiungendo quanto segue alla riga di comando:

   ```
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![chlimage_1-73](assets/chlimage_1-73a.png)

1. Click **Finish**. La struttura del progetto viene creata.

   >[!NOTE]
   >
   >Per una nuova installazione (più precisamente: quando non sono mai state scaricate le dipendenze morali) è possibile che il progetto venga creato con errori. In questo caso, seguire la procedura descritta in [Risoluzione della definizione](#resolving-invalid-project-definition)di progetto non valida.

## Risoluzione dei problemi {#troubleshooting}

### Risoluzione della definizione di progetto non valida {#resolving-invalid-project-definition}

Per risolvere dipendenze non valide e definire il progetto, procedere come segue:

1. Seleziona tutti i progetti creati.
1. Fare clic con il pulsante destro del mouse. Nel menu **Paradiso** selezionare **Aggiorna progetti**.
1. Controllare **gli aggiornamenti di snapshot/release**.
1. Fai clic su **OK**. Eclipse tenta di scaricare le dipendenze richieste.

### Abilitazione del completamento automatico della libreria di tag nei file JSP {#enabling-tag-library-autocompletion-in-jsp-files}

Il completamento automatico della libreria di tag non è disponibile, in quanto al progetto vengono aggiunte le dipendenze corrette. Esiste un problema noto quando si utilizza AEM Uber Jar, che non include i file tld e TagExtraInfo richiesti.

Per ovviare a questo problema, accertatevi che l&#39;artifact org.apache.sling.scripting.jsp.taglib sia posizionato nel percorso di classe prima di AEM Uber Jar. Per i progetti Maven, posizionate la seguente dipendenza nel file pom.xml prima del file Uber Jar.

```xml
<dependency>
  <groupId>org.apache.sling</groupId>
  <artifactId>org.apache.sling.scripting.jsp.taglib</artifactId>
  <scope>provided</scope>
</dependency>
```

Accertatevi di aggiungere la versione corretta per la distribuzione di AEM.

## More information {#more-information}

Il sito ufficiale Apache Sling IDE tooltool per Eclipse fornisce informazioni utili:

* La guida [**utente Apache Sling IDE tooling for Eclipse **](https://sling.apache.org/documentation/development/ide-tooling.html), che illustra i concetti generali, l’integrazione dei server e le funzionalità di implementazione supportate dagli strumenti di sviluppo AEM.
* La sezione [Risoluzione dei problemi](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting).
* Elenco dei problemi [noti](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues).

La seguente documentazione ufficiale [Eclipse](https://eclipse.org/) può aiutare a configurare l’ambiente:

* [Guida introduttiva ad Eclipse](https://eclipse.org/users/)
* [Eclipse Luna Help System](https://help.eclipse.org/luna/index.jsp)
* [Integrazione di Maven (m2eclipse)](https://www.eclipse.org/m2e/)

