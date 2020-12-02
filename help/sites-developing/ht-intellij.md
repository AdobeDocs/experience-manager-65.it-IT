---
title: Come sviluppare progetti AEM utilizzando IntelliJ IDEA
seo-title: Come sviluppare progetti AEM utilizzando IntelliJ IDEA
description: Utilizzo di IntelliJ IDEA per sviluppare progetti AEM
seo-description: Utilizzo di IntelliJ IDEA per sviluppare progetti AEM
uuid: 382b5008-2aed-4e08-95be-03c48f2b549e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: df6410a2-794e-4fa2-ae8d-37271274d537
translation-type: tm+mt
source-git-commit: b3e1493811176271ead54bae55b1cd0cf759fe71
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 1%

---


# Come sviluppare progetti AEM utilizzando IntelliJ IDEA{#how-to-develop-aem-projects-using-intellij-idea}

## Panoramica {#overview}

Per iniziare AEM sviluppo su IntelliJ, sono necessari i seguenti passaggi.

Ognuno di essi è spiegato più dettagliatamente nel resto di questo How-To.

* Installare IntelliJ
* Imposta il progetto AEM in base al cielo
* Preparare il supporto JSP per IntelliJ nel Maven POM
* Importa progetto Paradiso in IntelliJ

>[!NOTE]
>
>Questa guida si basa su IntelliJ IDEA Ultimate Edition 12.1.4 e AEM 5.6.1.

### Installazione di IntelliJ IDEA {#install-intellij-idea}

Scaricate IntelliJ IDEA dalla pagina dei download di [JetBrains](https://www.jetbrains.com/idea/download/index.html).

Quindi, seguite le istruzioni di installazione presenti nella pagina.

### Imposta il progetto AEM in base a Maven {#set-up-your-aem-project-based-on-maven}

Configurate quindi il progetto utilizzando Maven come descritto in [How-To Build AEM Projects using Apache Maven](/help/sites-developing/ht-projects-maven.md) (Creazione di progetti con Apache Maven).

Per iniziare a lavorare con AEM progetti in IntelliJ IDEA, è sufficiente impostare [Guida introduttiva in 5 minuti](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html).

### Preparazione del supporto JSP per IntelliJ IDEA {#prepare-jsp-support-for-intellij-idea}

IntelliJ IDEA può anche fornire supporto nell&#39;utilizzo di JSP, ad esempio

* completamento automatico delle librerie di tag
* conoscenza degli oggetti definiti da `<cq:defineObjects />` e `<sling:defineObjects />`

Per farlo funzionare, seguire le istruzioni su [Come lavorare con JSP](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps) in [Come creare AEM progetti con Apache Maven](/help/sites-developing/ht-projects-maven.md).

### Importa progetto Paradiso {#import-the-maven-project}

1. Apri la finestra di dialogo **Importa** in IntelliJ IDEA tramite

   * selezione di **Importa progetto** nella schermata di benvenuto se non è ancora aperto alcun progetto
   * selezione di **File -> Importa progetto** dal menu principale

1. Nella finestra di dialogo Importa, selezionate il file POM del progetto.

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. Continuate con le impostazioni predefinite, come mostrato nella finestra di dialogo seguente.

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. Per continuare, fai clic su **Next** e su **Finish** nelle seguenti finestre di dialogo.
1. Ora è impostato per lo sviluppo AEM utilizzando IntelliJ IDEA

   ![chlimage_1-47](assets/chlimage_1-47a.png)

### Debug di JSP con IntelliJ IDEA {#debugging-jsps-with-intellij-idea}

I passaggi seguenti sono necessari per il debug di JSP con IntelliJ IDEA

* Impostazione di un facet Web nel progetto
* Installare il plug-in di supporto JSR45
* Configurare un profilo di debug
* Configurare AEM per la modalità Debug

#### Impostazione di un facet Web nel progetto {#set-up-a-web-facet-in-the-project}

IntelliJ IDEA deve capire dove trovare i JSP per il debug. Poiché IDEA non è in grado di interpretare le impostazioni `content-package-maven-plugin`, è necessario configurarle manualmente.

1. Vai a **File -> Struttura progetto**
1. Selezionare il modulo **Content**
1. Fare clic su **+** sopra l&#39;elenco dei moduli e selezionare **Web**
1. Come directory delle risorse Web, selezionate la `content/src/main/content/jcr_root subdirectory` del progetto come mostrato nella schermata sottostante.

![chlimage_1-48](assets/chlimage_1-48a.png)

#### Installare il plug-in di supporto JSR45 {#install-the-jsr-support-plugin}

1. Passare al riquadro **Plugins** nelle impostazioni IDEA di IntelliJ
1. Passare al plug-in **Integrazione JSR45** e selezionare la casella di controllo accanto ad esso
1. Fare clic su **Applica**
1. Riavvia IntelliJ IDEA quando richiesto

![chlimage_1-49](assets/chlimage_1-49a.png)

#### Configurare un profilo di debug {#configure-a-debug-profile}

1. Vai a **Esegui -> Modifica configurazioni**
1. Premere il tasto **+** e selezionare **JSR45 Remote**
1. Nella finestra di dialogo di configurazione, selezionare **Configura** accanto a **Application Server** e configurare un server generico
1. Impostate la pagina iniziale su un URL appropriato se desiderate aprire un browser quando avviate il debug
1. Rimuovere tutte le attività **Prima del lancio** se si utilizza la sincronizzazione automatica di versione, oppure configurare le attività appropriate del Paradiso se non si
1. Nel riquadro **Avvio/Connessione**, regolare la porta se necessario
1. Copiare gli argomenti della riga di comando proposti da IntelliJ IDEA

![chlimage_1-50](assets/chlimage_1-50a.png) ![chlimage_1-51](assets/chlimage_1-51a.png)

#### Configurare AEM per la modalità di debug {#configure-aem-for-debug-mode}

L&#39;ultimo passo necessario è iniziare AEM con le opzioni JVM proposte da IntelliJ IDEA.

A questo scopo, avviate direttamente il file JAR AEM e aggiungete le seguenti opzioni, ad esempio con la seguente riga di comando:

`java -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y -Xmx1024m -XX:MaxPermSize=256M -jar cq-quickstart-5.6.1.jar`

È inoltre possibile aggiungere queste opzioni allo script iniziale in `crx-quickstart/bin/start` come illustrato di seguito.

```shell
# ...

# default JVM options
if [ -z "$CQ_JVM_OPTS" ]; then
 CQ_JVM_OPTS='-server -Xmx1024m -XX:MaxPermSize=256M -Djava.awt.headless=true'
fi

CQ_JVM_OPTS="$CQ_JVM_OPTS -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y"

# ...
```

#### Avvia debug {#start-debugging}

Ora siete tutti configurati per il debug dei vostri JSP in AEM.

1. Selezionare **Esegui -> Debug -> Profilo di debug**
1. Impostazione di punti di interruzione nel codice del componente
1. Accesso a una pagina nel browser

![chlimage_1-52](assets/chlimage_1-52a.png)

### Debug di pacchetti con IntelliJ IDEA {#debugging-bundles-with-intellij-idea}

È possibile eseguire il debug del codice nei bundle utilizzando una connessione di debug remota standard generica. È possibile seguire la [documentazione Jetbrain sul debug remoto](https://www.jetbrains.com/idea/webhelp/run-debug-configuration-remote.html).
