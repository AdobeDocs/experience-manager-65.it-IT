---
title: Importare e gestire le applicazioni
seo-title: Import and manage applications
description: Scopri come importare e gestire le applicazioni.
seo-description: Learn how to import and manage applications.
uuid: 7fba6c4e-1a3e-4a4b-9201-acf2ff66a9df
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/importing_and_managing_applications_and_archives
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dc53a6d0-317a-4abd-990c-455e13f8b824
exl-id: f17726c0-3591-4d25-a8b5-3a7024249a56
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 0%

---

# Importare e gestire le applicazioni{#import-and-manage-applications}

Nei moduli AEM *applicazione* è un contenitore per l’archiviazione delle risorse necessarie per l’implementazione di una soluzione AEM forms. Esempi di risorse sono strutture del modulo, frammenti di modulo, immagini, processi, file DDX, guide dei moduli, pagine HTML e file SWF. Durante la fase di sviluppo di un progetto, gli utenti di Workbench possono distribuire le applicazioni direttamente dalla vista Applicazioni di Workbench. Una volta distribuite, queste applicazioni vengono visualizzate nella console di amministrazione, nella scheda Applicazioni della pagina Gestione applicazioni .

Quando un&#39;applicazione è completa e pronta per la distribuzione in un server di produzione, l&#39;utente Workbench crea un pacchetto dell&#39;applicazione in un *file dell’applicazione AEM forms* (.lca). Quindi, un amministratore utilizza la console di amministrazione per importare e distribuire il file dell&#39;applicazione, utilizzando la scheda Applicazioni nella pagina Gestione applicazioni.

È inoltre possibile utilizzare la scheda archivi nella pagina Gestione applicazioni per importare gli LCA creati utilizzando workbench 8.x.

>[!NOTE]
>
>Esiste un problema noto che i file LCA di una versione futura non sono necessariamente compatibili con le versioni precedenti. Anche se può essere possibile visualizzare e importare file LCA da una versione futura dei moduli AEM (ad esempio, una versione di anteprima), questo non è supportato e può causare un comportamento anomalo.

Utilizzare la scheda Applicazioni per importare e gestire le applicazioni create in Workbench. Gli amministratori dell&#39;applicazione possono anche esportare la configurazione di runtime per un&#39;applicazione. L&#39;esportazione della configurazione di runtime elimina la necessità di riconfigurare manualmente le impostazioni nell&#39;ambiente di produzione prima di avviare le applicazioni distribuite. Il file di configurazione del runtime contiene:

* impostazioni di configurazione del servizio
* impostazioni di configurazione del pool
* impostazioni di configurazione dell’endpoint
* profili di sicurezza

## Importare un&#39;applicazione o un archivio {#import-an-application-or-archive}

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione applicazioni.
1. Fai clic su Importa.
1. Fai clic su Sfoglia e seleziona il file .lca da importare, quindi fai clic su Anteprima. Nella pagina Preview Application (Anteprima applicazione) vengono visualizzate informazioni sull&#39;applicazione.
1. (Facoltativo) Per visualizzare un elenco delle risorse contenute nell’applicazione, fai clic su Visualizza risorse.
1. (Facoltativo) Per distribuire le risorse in fase di runtime, seleziona Distribuisci risorse in fase di esecuzione al termine dell’importazione. Se non selezioni questa opzione, puoi distribuire le risorse in un secondo momento.
1. Fai clic su Importa. L&#39;applicazione viene visualizzata nella scheda Applicazioni.
1. Accedi all&#39;archivio CRX con le credenziali di amministratore.
1. Passa a content/dam/lcapplications

   >[!NOTE]
   >
   >Le applicazioni importate vengono visualizzate nel nodo delle applicazioni.

1. Fare clic su una delle applicazioni importate.

   La scheda Proprietà a destra mostra le proprietà del nodo CRX selezionato.

   La **syncState** La proprietà indica lo stato di sincronizzazione dei dati tra il server di AEM forms e l&#39;archivio CRX. Non appena il processo di importazione inizia, questo stato viene impostato su 0 (zero). Questo stato indica che i dati non sono attualmente sincronizzati. Quando i dati sono sincronizzati, lo stato è impostato su 1.

## Distribuzione di un&#39;applicazione {#deploy-an-application}

È possibile distribuire applicazioni importate o importate da Workbench.

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione applicazioni.
1. Seleziona la casella di controllo accanto all’applicazione da distribuire e fai clic su Distribuisci .
1. Fate clic su OK nella finestra di dialogo di conferma visualizzata.

## Disdistribuire un&#39;applicazione {#undeploy-an-application}

Puoi annullare la distribuzione delle applicazioni dal runtime.

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione applicazioni.
1. Seleziona la casella di controllo accanto all’applicazione di cui desideri annullare la distribuzione e fai clic su Annulla distribuzione .
1. Fate clic su OK nella finestra di dialogo di conferma visualizzata.

## Rimuovere un&#39;applicazione dal server {#remove-an-application-from-the-server}

Disdistribuire l&#39;applicazione prima di rimuoverla dal server.

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione applicazioni.
1. Selezionare la casella di controllo accanto all&#39;applicazione che si desidera rimuovere e fare clic su Rimuovi.
1. Fate clic su OK nella finestra di dialogo di conferma visualizzata.

## Importare la configurazione di runtime di un’applicazione {#import-an-application-s-runtime-configuration}

Se un amministratore dell&#39;applicazione ha esportato la configurazione di runtime per un&#39;applicazione, è possibile importarla nell&#39;applicazione distribuita. È possibile importarlo utilizzando la console di amministrazione o tramite la distribuzione LCA con script.

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione applicazioni.
1. Fare clic sul nome dell&#39;applicazione.
1. Fare clic su Importa configurazione runtime.
1. Fai clic su Sfoglia e seleziona il file XML contenente la configurazione di runtime.
1. Fai clic su Importa.

## Esportare la configurazione di runtime di un’applicazione {#export-an-application-s-runtime-configuration}

Puoi esportare le informazioni di configurazione del runtime per le applicazioni distribuite.

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione applicazioni.
1. Fare clic sul nome dell&#39;applicazione.
1. Fai clic su Esporta configurazione runtime e salva il file di configurazione (XML) prodotto.

## Distribuzione con script di applicazioni AEM forms {#scripted-deployment-of-aem-forms-applications}

È inoltre possibile utilizzare uno strumento di distribuzione con script per distribuire i file dell&#39;applicazione, incluso un file settings.xml che specifica le seguenti impostazioni:

* impostazioni di configurazione del servizio
* impostazioni di configurazione del pool
* impostazioni di configurazione dell’endpoint
* profili di sicurezza

La distribuzione con script elimina la necessità di riconfigurare manualmente le impostazioni nell’ambiente di produzione prima di avviare le applicazioni distribuite.

1. Da un prompt dei comandi, passa a *[root di aem forms]*/sdk/misc/Foundation/ArchiveManagement.
1. Per istruzioni più dettagliate, consulta il file ReadMe.txt .
1. Modifica manualmente i file scriptedDeploy.bat e sample-files/sample.xml come descritto nel file readme.txt.
1. Esegui il file scriptedDeploy.bat. Questa azione distribuisce il file di archivio dei moduli di AEM con le impostazioni di sostituzione.
