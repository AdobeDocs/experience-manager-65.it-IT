---
title: Come sviluppare progetti AEM utilizzando IntelliJ IDEA
description: Utilizzo di IntelliJ IDEA per sviluppare progetti AEM
uuid: 382b5008-2aed-4e08-95be-03c48f2b549e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: df6410a2-794e-4fa2-ae8d-37271274d537
exl-id: 5a79c79b-df65-4cb2-b9d4-eda994c992ec
source-git-commit: af60428255fb883265ade7b2d9f363aacb84b9ad
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 1%

---

# Come sviluppare progetti AEM utilizzando IntelliJ IDEA{#how-to-develop-aem-projects-using-intellij-idea}

## Panoramica {#overview}

Per iniziare a utilizzare AEM sviluppo su IntelliJ, sono necessari i seguenti passaggi.

Ogni passaggio è spiegato più dettagliatamente nel resto di questo argomento.

* Installa IntelliJ
* Imposta il progetto AEM in base a Maven
* Preparare il supporto JSP per IntelliJ nel Maven POM
* Importare il progetto Maven in IntelliJ

>[!NOTE]
>
>Questa guida si basa su IntelliJ IDEA Ultimate Edition 12.1.4 e AEM 5.6.1.

### Installa IntelliJ IDEA {#install-intellij-idea}

Scarica IntelliJ IDEA da [la pagina Download su JetBrains](https://www.jetbrains.com/idea/download/).

Quindi, segui le istruzioni di installazione su quella pagina.

### Imposta il progetto AEM in base a Maven {#set-up-your-aem-project-based-on-maven}

Quindi, imposta il progetto utilizzando Maven come descritto in [Come generare progetti AEM con Apache Maven](/help/sites-developing/ht-projects-maven.md).

Per iniziare a lavorare con progetti AEM in IntelliJ IDEA, la configurazione di base in [Introduzione in 5 minuti](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) è sufficiente.

### Preparare il supporto JSP per IntelliJ IDEA {#prepare-jsp-support-for-intellij-idea}

IntelliJ IDEA può anche fornire supporto nell&#39;utilizzo di JSP, ad esempio:

* completamento automatico delle librerie di tag
* conoscenza degli oggetti definiti `<cq:defineObjects />` e `<sling:defineObjects />`

Per farlo funzionare, segui le istruzioni su [Come lavorare con i JSP](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps) in [Come generare progetti AEM con Apache Maven](/help/sites-developing/ht-projects-maven.md).

### Importa progetto Maven {#import-the-maven-project}

1. Apri **Importa** dialogo in IntelliJ IDEA di

   * selezione **Importa progetto** nella schermata di benvenuto se non hai ancora aperto un progetto
   * selezione **File -> Importa progetto** dal menu principale

1. Nella finestra di dialogo Importa selezionare il file POM del progetto.

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. Procedi con le impostazioni predefinite come mostrato nella finestra di dialogo seguente.

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. Continua attraverso le seguenti finestre di dialogo facendo clic su **Successivo** e **Fine**.
1. Ora è configurato per lo sviluppo AEM utilizzando IntelliJ IDEA

   ![chlimage_1-47](assets/chlimage_1-47a.png)

### Debug di JSP con IntelliJ IDEA {#debugging-jsps-with-intellij-idea}

I seguenti passaggi sono necessari per il debug di JSP con IntelliJ IDEA

* Configurare un facet Web nel progetto
* Installare il plugin di supporto JSR45
* Configurare un profilo di debug
* Configurare AEM per la modalità di debug

#### Configurare un facet Web nel progetto {#set-up-a-web-facet-in-the-project}

IntelliJ IDEA deve capire dove trovare i JSP per il debug. Poiché IDEA non è in grado di interpretare il `content-package-maven-plugin` deve essere configurato manualmente.

1. Vai a **File -> Struttura del progetto**
1. Seleziona la **Contenuto** modulo
1. Fai clic su **+** sopra l’elenco dei moduli e seleziona **Web**
1. Come directory delle risorse Web, selezionare il `content/src/main/content/jcr_root subdirectory` del progetto, come illustrato nella schermata seguente.

![chlimage_1-48](assets/chlimage_1-48a.png)

#### Installare il plugin di supporto JSR45 {#install-the-jsr-support-plugin}

1. Vai a **Plug-in** nelle impostazioni IntelliJ IDEA
1. Passa a **Integrazione JSR45** Plug-in e seleziona la casella di controllo accanto ad esso
1. Fai clic su **Applica**
1. Riavvia IntelliJ IDEA quando richiesto

![chlimage_1-49](assets/chlimage_1-49a.png)

#### Configurare un profilo di debug {#configure-a-debug-profile}

1. Vai a **Esegui -> Modifica configurazioni**
1. Hit **+** e seleziona **Remoto JSR45**
1. Nella finestra di dialogo di configurazione, seleziona **Configura** accanto a **Server applicazioni** e configurare un server generico
1. Impostare la pagina iniziale su un URL appropriato se si desidera aprire un browser quando si avvia il debug
1. Rimuovi tutto **Prima del lancio** attività se si utilizza la sincronizzazione automatica vlt o si configurano le attività Maven appropriate se non si
1. Sulla **Avvio/connessione** se necessario, regolare la porta
1. Copia gli argomenti della riga di comando proposti da IntelliJ IDEA

![chlimage_1-50](assets/chlimage_1-50a.png) ![chlimage_1-51](assets/chlimage_1-51a.png)

#### Configurare AEM per la modalità di debug {#configure-aem-for-debug-mode}

L&#39;ultimo passo necessario è quello di iniziare AEM con le opzioni JVM proposte da IntelliJ IDEA.

Avvia direttamente il file jar AEM e aggiungi queste opzioni, ad esempio con la seguente riga di comando:

`java -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y -Xmx1024m -jar cq-quickstart-6.5.0.jar`

È inoltre possibile aggiungere queste opzioni allo script iniziale in `crx-quickstart/bin/start` come mostrato di seguito.

```shell
# ...

# default JVM options
if [ -z "$CQ_JVM_OPTS" ]; then
 CQ_JVM_OPTS='-server -Xmx1024m -Djava.awt.headless=true'
fi

CQ_JVM_OPTS="$CQ_JVM_OPTS -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y"

# ...
```

#### Avvia debug {#start-debugging}

Ora tutti gli utenti sono configurati per eseguire il debug dei JSP in AEM.

1. Seleziona **Esegui -> Debug -> Il Tuo Profilo Di Debug**
1. Impostare i punti di interruzione nel codice del componente
1. Accedere a una pagina nel browser

![chlimage_1-52](assets/chlimage_1-52a.png)

### Debug dei bundle con IntelliJ IDEA {#debugging-bundles-with-intellij-idea}

È possibile eseguire il debug del codice nei bundle utilizzando una connessione di debug remota standard generica. Puoi seguire la [Documentazione JetBrain sul debug remoto](https://www.jetbrains.com/help/idea/remote-debugging-with-product.html#remote-interpreter).
