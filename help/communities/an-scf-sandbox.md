---
title: Creare una sandbox SCF
seo-title: Creare una sandbox SCF
description: Questa esercitazione è destinata principalmente agli sviluppatori, nuovi o AEM, interessati all’utilizzo dei componenti SCF.  Viene descritto come creare un sito sandbox SCF
seo-description: Questa esercitazione è destinata principalmente agli sviluppatori, nuovi o AEM, interessati all’utilizzo dei componenti SCF.  Viene descritto come creare un sito sandbox SCF
uuid: ee52e670-e1e6-4bcd-9548-c963142e6704
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e1b5c25d-cbdd-421c-b81a-feb6039610a3
translation-type: tm+mt
source-git-commit: 548e19b0fc76ede8685ea938ed871fbdc8c3858f
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 1%

---



# Creare una sandbox SCF  {#create-an-scf-sandbox}


A partire AEM community 6.1, il modo più semplice per creare rapidamente una sandbox è creare un sito community. See [Getting Started with AEM Communities](getting-started.md).

Un altro strumento utile per gli sviluppatori è la guida [](components-guide.md)Community Components, che consente di esplorare e creare rapidamente prototipi di componenti e caratteristiche di Communities.

L’esercizio di creazione di un sito Web può essere utile per comprendere la struttura di un sito Web AEM che può includere funzioni di Community, fornendo al contempo pagine semplici su cui esplorare l’utilizzo del framework di componenti [sociali (SCF)](scf.md).

Questa esercitazione è destinata principalmente agli sviluppatori, nuovi o AEM, interessati all’utilizzo dei componenti SCF. Viene descritta la creazione di un sito sandbox SCF, simile all’esercitazione [How to Create a Fully Featured Internet Website](../../help/sites-developing/website.md) (Come creare un sito Internet completo) che si concentra sulle strutture del sito, come la navigazione, il logo, la ricerca, la barra degli strumenti e l’elenco delle pagine figlie.

Lo sviluppo avviene in un’istanza di authoring, mentre la sperimentazione con il sito risulta ottimale in un’istanza di pubblicazione.

I passaggi di questa esercitazione sono:

* [Imposta struttura sito Web](setup-website.md)
* [Applicazione sandbox iniziale](initial-app.md)
* [Contenuto sandbox iniziale](initial-content.md)
* [Sviluppo di applicazioni sandbox](develop-app.md)
* [Aggiungi Clientlibs](add-clientlibs.md)
* [Sviluppo di contenuto sandbox](develop-content.md)

>[!CAUTION]
>
>Questa esercitazione non crea un sito community con le funzionalità create mediante la console [Siti](sites-console.md)community. Ad esempio, questa esercitazione non descrive come impostare login, registrazione automatica, login [per](social-login.md)social network, messaggi, profili e così via.
>
>Se preferite un semplice sito community, seguite l’esercitazione [Create a Sample Page (Crea una pagina](create-sample-page.md) di esempio).

## Prerequisiti {#prerequisites}

Questa esercitazione presuppone che siano installati un’istanza di creazione AEM e una AEM pubblicazione con l’ [ultima versione](deploy-communities.md#latest-releases) di Communities.

Di seguito sono riportati alcuni utili collegamenti per gli sviluppatori che non hanno mai utilizzato la piattaforma AEM:

* [Guida introduttiva](../../help/sites-deploying/deploy.md#getting-started): per distribuire AEM istanze.

   * [Nozioni di base](../../help/sites-developing/the-basics.md): per sviluppatori di siti Web e funzionalità.
   * [Primi passi per gli autori](../../help/sites-authoring/first-steps.md): per la creazione del contenuto della pagina.

## Utilizzo dell&#39;ambiente di sviluppo CRXDE Lite {#using-crxde-lite-development-environment}

AEM gli sviluppatori trascorrono gran parte del loro tempo nell’ambiente di sviluppo [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) per un’istanza di authoring. CRXDE Lite fornisce un accesso meno limitato all&#39;archivio CRX. Gli strumenti dell’interfaccia classica e le console dell’interfaccia touch consentono di accedere in modo più strutturato a porzioni specifiche dell’archivio CRX.

Dopo aver effettuato l&#39;accesso con privilegi di amministratore, è possibile accedere ai CRXDE Lite in vari modi:

1. Dalla navigazione globale, selezionate **[!UICONTROL Strumenti di navigazione > CRXDE Lite]**.

   ![crxde-lite](assets/tools-crxde.png)

2. Dalla pagina [di benvenuto dell’interfaccia](http://localhost:4502/welcome.html)classica, scorri verso il basso e fai clic su **[!UICONTROL CRXDE Lite]** nel pannello a destra.

   ![classic-ui-crxde](assets/classic-ui-crxde.png)

3. Passa direttamente a `CRXDE Lite`: `<server>:<port>/crx/de`

   Ad esempio, in un’istanza di creazione locale: [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

Per lavorare con i CRXDE Lite, dovete accedere con i privilegi di sviluppatore o amministratore. Per l&#39;istanza localhost predefinita, è possibile accedere con

* `username: admin`
* `password: admin`


**Tieni presente** che questo accesso si interromperà e che sarà necessario eseguire nuovamente l&#39;accesso utilizzando il pull down all&#39;estremità destra della barra degli strumenti CRXDe Lite.

Se non è stato effettuato l&#39;accesso, non sarà possibile navigare nell&#39;archivio JCR né eseguire operazioni di modifica/salvataggio.

***In caso di dubbi, effettuate nuovamente l&#39;accesso!***

![login](assets/relogin.png)
