---
title: Importare e gestire le applicazioni
description: Scopri come importare e gestire le applicazioni. Un’applicazione è un contenitore per l’archiviazione delle risorse necessarie per l’implementazione di una soluzione AEM Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/importing_and_managing_applications_and_archives
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: f17726c0-3591-4d25-a8b5-3a7024249a56
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '852'
ht-degree: 100%

---

# Importare e gestire le applicazioni{#import-and-manage-applications}

In AEM Forms, un’*applicazione* è un contenitore per l’archiviazione delle risorse necessarie per l’implementazione di una soluzione AEM Forms. Esempi di risorse sono le progettazioni di moduli, i frammenti di moduli, le immagini, i processi, i file DDX, le guide dei moduli, le pagine HTML e i file SWF. Durante la fase di sviluppo di un progetto, gli utenti di Workbench possono distribuire le applicazioni direttamente dalla vista applicazioni di Workbench. Una volta distribuite, queste applicazioni vengono visualizzate nella console di amministrazione, nella scheda Applicazioni della pagina Gestione applicazioni.

Quando un’applicazione è completa e pronta per essere distribuita su un server di produzione, l’utente Workbench inserisce l’applicazione in un *file applicazione AEM Forms* (.lca). L’amministratore utilizza quindi la console di amministrazione per importare e distribuire il file applicazione utilizzando la scheda Applicazioni della pagina Gestione applicazioni.

Puoi inoltre utilizzare la scheda Archivi nella pagina Gestione applicazioni per importare LCA creati con Workbench 8.x.

>[!NOTE]
>
>Esiste un problema noto per cui i file LCA di una versione futura non sono necessariamente compatibili con le versioni precedenti. Anche se potrebbe essere possibile visualizzare e importare file LCA da una versione futura di AEM Forms (ad esempio, una versione in anteprima), questa operazione non è supportata e potrebbe causare un comportamento anomalo.

Utilizza la scheda Applicazioni per importare e gestire le applicazioni create in Workbench. Gli amministratori dell’applicazione possono anche esportare la configurazione runtime di un’applicazione. L’esportazione della configurazione runtime elimina la necessità di riconfigurare manualmente le impostazioni nell’ambiente di produzione prima di avviare le applicazioni distribuite. Il file di configurazione runtime contiene:

* impostazioni di configurazione del servizio
* impostazioni di configurazione del pool
* impostazioni di configurazione dell’endpoint
* profili di sicurezza

## Importare un’applicazione o un archivio {#import-an-application-or-archive}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

1. Nella console di amministrazione, fai clic su Servizi > Applicazioni e servizi > Gestione applicazioni.
1. Fai clic su Importa.
1. Fai clic su Sfoglia, seleziona il file .lca da importare e fai clic su Anteprima. Nella pagina Anteprima applicazione vengono visualizzate informazioni sull’applicazione.
1. (Facoltativo) Per visualizzare un elenco delle risorse contenute nell’applicazione, fai clic su Visualizza risorse.
1. (Facoltativo) Per distribuire le risorse al runtime, seleziona Distribuisci risorse in runtime al termine dell’importazione. Se non selezioni questa opzione, puoi distribuire le risorse in un secondo momento.
1. Fai clic su Importa. L’applicazione viene visualizzata nella scheda Applicazioni.
1. Accedi all’archivio CRX con le credenziali amministratore.
1. Passa a content/dam/lcapplications

   >[!NOTE]
   >
   >Le applicazioni importate vengono visualizzate nel nodo lcapplications.

1. Fai clic su una delle applicazioni importate.

   Nella scheda Proprietà a destra vengono visualizzate le proprietà del nodo CRX selezionato.

   La proprietà **syncState** indica lo stato di sincronizzazione dei dati tra il server AEM Forms e l’archivio CRX. Non appena il processo di importazione inizia, questo stato viene impostato su 0 (zero). Questo stato indica che i dati non sono attualmente sincronizzati. Quando i dati vengono sincronizzati, lo stato è impostato su 1.

## Distribuire un’applicazione {#deploy-an-application}

Puoi distribuire le applicazioni importate o che gli utenti Workbench hanno importato da Workbench.

1. Nella console di amministrazione, fai clic su Servizi > Applicazioni e servizi > Gestione applicazioni.
1. Seleziona la casella di controllo accanto all’applicazione da distribuire e fai clic su Distribuisci.
1. Fai clic su OK nella finestra di dialogo di conferma visualizzata.

## Annullare la distribuzione di un’applicazione {#undeploy-an-application}

Puoi annullare la distribuzione delle applicazioni dal runtime.

1. Nella console di amministrazione, fai clic su Servizi > Applicazioni e servizi > Gestione applicazioni.
1. Seleziona la casella di controllo accanto all’applicazione di cui annullare la distribuzione e fai clic su Annulla distribuzione.
1. Fai clic su OK nella finestra di dialogo di conferma visualizzata.

## Rimuovere un’applicazione dal server {#remove-an-application-from-the-server}

Annulla la distribuzione dell’applicazione prima di rimuoverla dal server.

1. Nella console di amministrazione, fai clic su Servizi > Applicazioni e servizi > Gestione applicazioni.
1. Seleziona la casella di controllo accanto all’applicazione che desideri rimuovere e fai clic su Rimuovi.
1. Fai clic su OK nella finestra di dialogo di conferma visualizzata.

## Importare la configurazione di runtime di un’applicazione {#import-an-application-s-runtime-configuration}

Se l’amministratore dell’applicazione ha esportato la configurazione di runtime di un’applicazione, è possibile importarla nell’applicazione distribuita. Puoi importarla utilizzando la console di amministrazione o tramite la distribuzione LCA basata su script.

1. Nella console di amministrazione, fai clic su Servizi > Applicazioni e servizi > Gestione applicazioni.
1. Fai clic sul nome dell’applicazione.
1. Fai clic su Importa configurazione runtime.
1. Fai clic su Sfoglia e seleziona il file XML contenente la configurazione di runtime.
1. Fai clic su Importa.

## Esportare la configurazione runtime di un’applicazione {#export-an-application-s-runtime-configuration}

È possibile esportare le informazioni di configurazione runtime per le applicazioni distribuite.

1. Nella console di amministrazione, fai clic su Servizi > Applicazioni e servizi > Gestione applicazioni.
1. Fai clic sul nome dell’applicazione.
1. Fai clic su Esporta configurazione runtime e salva il file di configurazione (XML) che è stato prodotto.

## Distribuzione con script delle applicazioni AEM Forms {#scripted-deployment-of-aem-forms-applications}

È inoltre possibile utilizzare uno strumento di distribuzione basato su script per distribuire i file dell’applicazione, incluso un file settings.xml che specifica le impostazioni seguenti:

* impostazioni di configurazione del servizio
* impostazioni di configurazione del pool
* impostazioni di configurazione dell’endpoint
* profili di sicurezza

La distribuzione con script elimina la necessità di riconfigurare manualmente le impostazioni nell’ambiente di produzione prima di avviare le applicazioni distribuite.

1. Dal prompt dei comandi, passa a *[aem-forms root]*/sdk/misc/Foundation/ArchiveManagement.
1. Per istruzioni più dettagliate, rivedi il file ReadMe.txt.
1. Modifica manualmente i file scriptedDeploy.bat e sample-files/sample.xml come descritto nel file readme.txt.
1. Esegui il file scriptedDeploy.bat. Questa azione distribuisce il file di archivio di AEM Forms con le impostazioni di sostituzione.
