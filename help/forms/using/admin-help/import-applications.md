---
title: Importare e gestire le applicazioni
description: Scopri come importare e gestire le applicazioni. Un’applicazione è un contenitore per l’archiviazione delle risorse necessarie per implementare una soluzione AEM forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/importing_and_managing_applications_and_archives
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: f17726c0-3591-4d25-a8b5-3a7024249a56
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 0%

---

# Importare e gestire le applicazioni{#import-and-manage-applications}

Nei moduli AEM, un&#39;applicazione *application* è un contenitore per l&#39;archiviazione delle risorse necessarie per l&#39;implementazione di una soluzione di moduli AEM. Esempi di risorse sono le progettazioni di moduli, i frammenti di moduli, le immagini, i processi, i file DDX, le guide dei moduli, le pagine di HTML e i file di SWF. Durante la fase di sviluppo di un progetto, gli utenti di Workbench possono distribuire le applicazioni direttamente dalla vista Applicazioni di Workbench. Una volta distribuite, queste applicazioni vengono visualizzate nella console di amministrazione, nella scheda Applicazioni della pagina Gestione applicazioni.

Quando un&#39;applicazione è completa e pronta per essere distribuita su un server di produzione, l&#39;utente Workbench inserisce l&#39;applicazione in un *file dell&#39;applicazione moduli AEM* (.lca). L&#39;amministratore utilizza quindi la console di amministrazione per importare e distribuire il file dell&#39;applicazione utilizzando la scheda Applicazioni della pagina Gestione applicazioni.

È inoltre possibile utilizzare la scheda Archivi nella pagina Gestione applicazioni per importare LCA creati con Workbench 8.x.

>[!NOTE]
>
>Esiste un problema noto che i file LCA di una versione futura non sono necessariamente compatibili con le versioni precedenti. Anche se potrebbe essere possibile visualizzare e importare file LCA da una versione futura di moduli AEM (ad esempio, una versione di anteprima), ciò non è supportato e potrebbe causare un comportamento aberrante.

Utilizzare la scheda Applicazioni per importare e gestire le applicazioni create in Workbench. Gli amministratori dell’applicazione possono anche esportare la configurazione di runtime di un’applicazione. L’esportazione della configurazione di runtime elimina la necessità di riconfigurare manualmente le impostazioni nell’ambiente di produzione prima di avviare le applicazioni distribuite. Il file di configurazione runtime contiene:

* impostazioni di configurazione del servizio
* impostazioni di configurazione del pool
* impostazioni di configurazione endpoint
* profili di sicurezza

## Importare un&#39;applicazione o un archivio {#import-an-application-or-archive}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione applicazioni.
1. Fai clic su Importa.
1. Fare clic su Sfoglia, selezionare il file .lca da importare e fare clic su Anteprima. Nella pagina Anteprima applicazione vengono visualizzate informazioni sull&#39;applicazione.
1. (Facoltativo) Per visualizzare un elenco delle risorse contenute nell’applicazione, fai clic su Visualizza Assets.
1. (Facoltativo) Per distribuire le risorse in fase di esecuzione, seleziona Distribuisci Assets in fase di esecuzione al termine dell’importazione. Se non selezioni questa opzione, puoi distribuire le risorse in un secondo momento.
1. Fai clic su Importa. L&#39;applicazione viene visualizzata nella scheda Applicazioni.
1. Accedi al repository di CRX con le credenziali di amministratore.
1. Passa a content/dam/lcapplications

   >[!NOTE]
   >
   >Le applicazioni importate vengono visualizzate nel nodo lcapplications.

1. Fare clic su una delle applicazioni importate.

   Nella scheda Proprietà a destra vengono visualizzate le proprietà del nodo CRX selezionato.

   La proprietà **syncState** indica lo stato di sincronizzazione dei dati tra il server AEM Forms e l&#39;archivio CRX. Non appena il processo di importazione inizia, questo stato viene impostato su 0 (zero). Questo stato indica che i dati non sono attualmente sincronizzati. Quando i dati vengono sincronizzati, lo stato è impostato su 1.

## Distribuire un&#39;applicazione {#deploy-an-application}

È possibile distribuire le applicazioni importate o che gli utenti Workbench hanno importato da Workbench.

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione applicazioni.
1. Selezionare la casella di controllo accanto all&#39;applicazione che si desidera distribuire e fare clic su Distribuisci.
1. Fare clic su OK nella finestra di dialogo di conferma visualizzata.

## Annullare la distribuzione di un’applicazione {#undeploy-an-application}

È possibile annullare la distribuzione delle applicazioni dal runtime.

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione applicazioni.
1. Selezionare la casella di controllo accanto all&#39;applicazione di cui si desidera annullare la distribuzione e fare clic su Annulla distribuzione.
1. Fare clic su OK nella finestra di dialogo di conferma visualizzata.

## Rimuovere un&#39;applicazione dal server {#remove-an-application-from-the-server}

Disdistribuire l&#39;applicazione prima di rimuoverla dal server.

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione applicazioni.
1. Selezionare la casella di controllo accanto all&#39;applicazione che si desidera rimuovere e fare clic su Rimuovi.
1. Fare clic su OK nella finestra di dialogo di conferma visualizzata.

## Importare la configurazione runtime di un&#39;applicazione {#import-an-application-s-runtime-configuration}

Se l&#39;amministratore dell&#39;applicazione ha esportato la configurazione di runtime di un&#39;applicazione, è possibile importarla nell&#39;applicazione distribuita. Puoi importarlo utilizzando la console di amministrazione o tramite la distribuzione LCA basata su script.

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione applicazioni.
1. Fare clic sul nome dell&#39;applicazione.
1. Fai clic su Importa configurazione runtime.
1. Fare clic su Sfoglia e selezionare il file XML contenente la configurazione di runtime.
1. Fai clic su Importa.

## Esportare la configurazione runtime di un&#39;applicazione {#export-an-application-s-runtime-configuration}

È possibile esportare le informazioni di configurazione runtime per le applicazioni distribuite.

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione applicazioni.
1. Fare clic sul nome dell&#39;applicazione.
1. Fare clic su Esporta configurazione runtime e salvare il file di configurazione (XML) prodotto.

## Distribuzione con script delle applicazioni AEM forms {#scripted-deployment-of-aem-forms-applications}

È inoltre possibile utilizzare uno strumento di distribuzione basato su script per distribuire i file dell&#39;applicazione, incluso un file settings.xml che specifica le impostazioni seguenti:

* impostazioni di configurazione del servizio
* impostazioni di configurazione del pool
* impostazioni di configurazione endpoint
* profili di sicurezza

La distribuzione con script elimina la necessità di riconfigurare manualmente le impostazioni nell’ambiente di produzione prima di avviare le applicazioni distribuite.

1. Dal prompt dei comandi passare a *[radice aem-forms]*/sdk/misc/Foundation/ArchiveManagement.
1. Per istruzioni più dettagliate, consultate il file Leggimi.txt.
1. Modificare manualmente i file scriptedDeploy.bat e sample-files/sample.xml come descritto nel file readme.txt.
1. Eseguire il file scriptedDeploy.bat. Questa azione distribuisce il file di archivio dei moduli AEM con le impostazioni di esclusione.
