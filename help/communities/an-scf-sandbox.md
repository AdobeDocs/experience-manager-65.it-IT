---
title: Creare una sandbox SCF
description: Questo tutorial è principalmente destinato agli sviluppatori, nuovi all’AEM, che sono interessati a utilizzare i componenti SCF. Questo video illustra come creare un sito Sandbox SCF
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 89858814-6625-4a56-8359-cc1eca402816
source-git-commit: fd937341e26edd0c3edfced8e862066ebc30f9a3
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# Creare una sandbox SCF  {#create-an-scf-sandbox}

A partire dalle community AEM 6.1, il modo più semplice per creare rapidamente una sandbox è quello di creare un sito community. Consulta [Guida introduttiva ad AEM Communities](getting-started.md).

Un altro strumento utile per gli sviluppatori è il [Guida ai componenti della community](components-guide.md), che consente di esplorare e creare rapidamente un prototipo dei componenti e delle funzioni di Communities.

L&#39;esercizio di creazione di un sito web può essere utile per comprendere la struttura di un sito web AEM che può includere caratteristiche di Communities, fornendo allo stesso tempo semplici pagine su cui esplorare la possibilità di lavorare con [framework della componente social network (SCF)](scf.md).

Questo tutorial è principalmente destinato agli sviluppatori, nuovi all’AEM, che sono interessati a utilizzare i componenti SCF. Questo video illustra la creazione del sito Sandbox SCF, in modo simile al tutorial per [Come creare un sito web Internet completo](../../help/sites-developing/website.md) che si concentra su strutture all’interno del sito, come la navigazione, il logo, la ricerca, la barra degli strumenti e l’elenco delle pagine figlie.

Lo sviluppo avviene su un’istanza di authoring, mentre la sperimentazione con il sito è consigliata su un’istanza di pubblicazione.

I passaggi descritti in questa esercitazione sono i seguenti:

* [Imposta struttura sito Web](setup-website.md)
* [Applicazione sandbox iniziale](initial-app.md)
* [Contenuto sandbox iniziale](initial-content.md)
* [Sviluppa applicazione sandbox](develop-app.md)
* [Aggiungi Clientlibs](add-clientlibs.md)
* [Sviluppare contenuti sandbox](develop-content.md)

>[!CAUTION]
>
>Questo tutorial non crea un sito community con la funzionalità creata utilizzando [Console Siti community](sites-console.md). Ad esempio, questo tutorial non descrive come impostare l’accesso, la registrazione automatica, [accesso social network](social-login.md), messaggi, profili e così via.
>
>Se si preferisce un sito di community semplice, seguire le istruzioni [Crea una pagina di esempio](create-sample-page.md) esercitazione.

## Prerequisiti {#prerequisites}

Questa esercitazione presuppone che siano installati un autore AEM e un&#39;istanza di pubblicazione AEM con [versione più recente](deploy-communities.md#latest-releases) delle comunità.

Di seguito sono riportati alcuni collegamenti utili per sviluppatori che non hanno mai utilizzato la piattaforma AEM:

* [Guida introduttiva](../../help/sites-deploying/deploy.md#getting-started): per la distribuzione di istanze AEM.

   * [Nozioni di base](../../help/sites-developing/the-basics.md): per sviluppatori di siti web e funzionalità.
   * [Primi passaggi per gli autori](../../help/sites-authoring/first-steps.md): per l’authoring dei contenuti della pagina.

## Utilizzo dell’ambiente di sviluppo di CRXDE Lite {#using-crxde-lite-development-environment}

Gli sviluppatori di AEM passano molto tempo nel [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) ambiente di sviluppo in un’istanza di authoring. CRXDE Lite offre un accesso meno limitato all’archivio CRX. Gli strumenti dell’interfaccia classica e le console dell’interfaccia touch forniscono un accesso più strutturato a parti specifiche dell’archivio CRX.

Dopo aver effettuato l’accesso con privilegi di amministratore, è possibile accedere a CRXDE Lite in diversi modi:

1. Dalla navigazione globale, seleziona navigazione **[!UICONTROL Strumenti > CRXDE Lite]**.

   ![crxde-lite](assets/tools-crxde.png)

2. Dalla sezione [pagina iniziale dell’interfaccia classica](http://localhost:4502/welcome.html), scorri verso il basso e fai clic su **[!UICONTROL CRXDE Lite]** nel pannello a destra.

   ![classic-ui-crxde](assets/classic-ui-crxde.png)

3. Cerca direttamente in `CRXDE Lite`: `<server>:<port>/crx/de`

   Ad esempio, in un’istanza di authoring locale: [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

Per lavorare con CRXDE Lite, devi accedere con privilegi di sviluppatore o amministratore. Per l’istanza localhost predefinita, puoi accedere con

* `username: admin`
* `password: admin`


Questo login va in timeout ed è necessario effettuare nuovamente l’accesso periodicamente utilizzando il menu a discesa nell’estremità destra della barra degli strumenti di CRXDE Lite.

Se non hai effettuato l’accesso, non potrai navigare nell’archivio JCR o eseguire operazioni di modifica/salvataggio.

***In caso di dubbi, effettua di nuovo l’accesso.***

![riaccedi](assets/relogin.png)
