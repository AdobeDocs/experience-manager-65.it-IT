---
title: Importazione e gestione di applicazioni
seo-title: Importazione e gestione di applicazioni
description: Scoprite come importare e gestire le applicazioni.
seo-description: Scoprite come importare e gestire le applicazioni.
uuid: 7fba6c4e-1a3e-4a4b-9201-acf2ff66a9df
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/importing_and_managing_applications_and_archives
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dc53a6d0-317a-4abd-990c-455e13f8b824
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 0%

---


# Importa e gestisci applicazioni{#import-and-manage-applications}

Nei AEM moduli, un&#39;applicazione *è un contenitore per la memorizzazione delle risorse necessarie per l&#39;implementazione di una soluzione di moduli AEM.* Esempi di risorse sono strutture del modulo, frammenti di modulo, immagini, processi, file DDX, guide dei moduli, pagine HTML e file SWF. Durante la fase di sviluppo di un progetto, gli utenti di Workbench possono distribuire le applicazioni direttamente dalla vista Applicazioni in Workbench. Una volta distribuite, queste applicazioni vengono visualizzate nella console di amministrazione, nella scheda Applicazioni della pagina Gestione applicazione.

Quando un&#39;applicazione è completa e pronta per la distribuzione in un server di produzione, l&#39;utente Workbench inserisce l&#39;applicazione in un file dell&#39;applicazione dei moduli *AEM* (.lca). Quindi, un amministratore utilizza la console di amministrazione per importare e distribuire il file dell&#39;applicazione, utilizzando la scheda Applicazioni nella pagina Gestione applicazione.

È inoltre possibile utilizzare la scheda degli archivi nella pagina Gestione applicazione per importare gli LCA creati utilizzando Workbench 8.x.

>[!NOTE]
>
>Esiste un problema noto che i file LCA di una versione futura non sono necessariamente compatibili con le versioni precedenti. Anche se può essere possibile visualizzare e importare file LCA da una versione futura dei moduli AEM (ad esempio, una versione di anteprima), tale operazione non è supportata e può generare un comportamento anomalo.

Utilizzare la scheda Applicazioni per importare e gestire le applicazioni create in Workbench. Gli amministratori delle applicazioni possono anche esportare la configurazione di runtime per un&#39;applicazione. L&#39;esportazione della configurazione di runtime elimina la necessità di riconfigurare manualmente le impostazioni nell&#39;ambiente di produzione prima di avviare le applicazioni distribuite. Il file di configurazione del runtime contiene:

* impostazioni di configurazione del servizio
* impostazioni di configurazione del pool
* impostazioni di configurazione endpoint
* profili di protezione

## Importare un&#39;applicazione o un archivio {#import-an-application-or-archive}

1. Nella console di amministrazione, fate clic su Servizi > Applicazioni e servizi > Gestione applicazione.
1. Fai clic su Importa.
1. Fate clic su Sfoglia, selezionate il file .lca da importare e fate clic su Anteprima. Nella pagina Anteprima applicazione sono visualizzate informazioni sull’applicazione.
1. (Facoltativo) Per visualizzare un elenco delle risorse contenute nell’applicazione, fate clic su Visualizza risorse.
1. (Facoltativo) Per distribuire le risorse in fase di esecuzione, selezionare Distribuisci risorse in fase di esecuzione al termine dell&#39;importazione. Se non selezionate questa opzione, potete distribuire le risorse in un secondo momento.
1. Fai clic su Importa. L&#39;applicazione viene visualizzata nella scheda Applicazioni.
1. Accedete all&#39;archivio CRX con le credenziali di amministratore.
1. Spostarsi tra i contenuti/dam/lcapplications

   >[!NOTE]
   >
   >Le applicazioni importate vengono visualizzate nel nodo delle applicazioni.

1. Fare clic su una delle applicazioni importate.

   Nella scheda Proprietà a destra sono visualizzate le proprietà del nodo CRX selezionato.

   La proprietà **syncState** indica lo stato di sincronizzazione dei dati tra il server AEM moduli e l&#39;archivio CRX. Non appena il processo di importazione inizia, questo stato viene impostato su 0 (zero). Questo stato indica che i dati non sono attualmente sincronizzati. Quando i dati sono sincronizzati, lo stato è impostato su 1.

## Distribuzione di un&#39;applicazione {#deploy-an-application}

È possibile distribuire le applicazioni che sono state importate o che gli utenti di Workbench hanno importato da Workbench.

1. Nella console di amministrazione, fate clic su Servizi > Applicazioni e servizi > Gestione applicazione.
1. Selezionate la casella di controllo accanto all’applicazione da distribuire e fate clic su Distribuisci.
1. Fare clic su OK nella finestra di dialogo di conferma visualizzata.

## Annullare la distribuzione di un&#39;applicazione {#undeploy-an-application}

Potete annullare la distribuzione delle applicazioni dal runtime.

1. Nella console di amministrazione, fate clic su Servizi > Applicazioni e servizi > Gestione applicazione.
1. Selezionate la casella di controllo accanto all’applicazione da annullare la distribuzione e fate clic su Annulla distribuzione.
1. Fare clic su OK nella finestra di dialogo di conferma visualizzata.

## Rimozione di un&#39;applicazione dal server {#remove-an-application-from-the-server}

Disdistribuire l&#39;applicazione prima di rimuoverla dal server.

1. Nella console di amministrazione, fate clic su Servizi > Applicazioni e servizi > Gestione applicazione.
1. Selezionate la casella di controllo accanto all’applicazione da rimuovere e fate clic su Rimuovi.
1. Fare clic su OK nella finestra di dialogo di conferma visualizzata.

## Importare la configurazione di runtime di un&#39;applicazione {#import-an-application-s-runtime-configuration}

Se un amministratore dell&#39;applicazione ha esportato la configurazione di runtime per un&#39;applicazione, potete importarla nell&#39;applicazione distribuita. Potete importarlo utilizzando la console di amministrazione o tramite la distribuzione LCA con script.

1. Nella console di amministrazione, fate clic su Servizi > Applicazioni e servizi > Gestione applicazione.
1. Fate clic sul nome dell’applicazione.
1. Fate clic su Importa configurazione runtime.
1. Fate clic su Sfoglia e selezionate il file XML che contiene la configurazione di runtime.
1. Fai clic su Importa.

## Esportare la configurazione di runtime di un&#39;applicazione {#export-an-application-s-runtime-configuration}

Potete esportare le informazioni di configurazione del runtime per le applicazioni distribuite.

1. Nella console di amministrazione, fate clic su Servizi > Applicazioni e servizi > Gestione applicazione.
1. Fate clic sul nome dell’applicazione.
1. Fate clic su Esporta configurazione runtime e salvate il file di configurazione (XML) prodotto.

## Implementazione con script di applicazioni di moduli AEM {#scripted-deployment-of-aem-forms-applications}

Potete anche utilizzare uno strumento di distribuzione con script per distribuire i file dell&#39;applicazione, incluso un file settings.xml che specifica le seguenti impostazioni:

* impostazioni di configurazione del servizio
* impostazioni di configurazione del pool
* impostazioni di configurazione endpoint
* profili di protezione

La distribuzione con script elimina la necessità di riconfigurare manualmente le impostazioni nell&#39;ambiente di produzione prima di avviare le applicazioni distribuite.

1. Dal prompt dei comandi, passare a *[aem-forms root]*/sdk/misc/Foundation/ArchiveManagement.
1. Leggere il file ReadMe.txt per istruzioni più dettagliate.
1. Modificate manualmente i file scriptedDeploy.bat e sample-files/sample.xml come descritto nel file readme.txt.
1. Eseguire il file scriptedDeploy.bat. Questa azione consente di distribuire il file di archivio dei moduli AEM con le impostazioni di esclusione.

