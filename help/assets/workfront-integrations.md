---
title: Integrazione di [!DNL Experience Manager Assets] con  [!DNL Adobe Workfront]
description: Introduzione all'integrazione tra [!DNL Assets] e [!DNL Workfront]
role: Admin,Leader,Developer
feature: Workfront Integrations and Apps
exl-id: 57e2bffe-8094-4557-99c8-7b482681687e
hide: true
solution: Experience Manager, Workfront
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '1113'
ht-degree: 7%

---

# Integrazione di [!DNL Adobe Experience Manager Assets] con [!DNL Adobe Workfront] {#assets-integration-overview}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-integrations.html?lang=en) |
| AEM 6.5 | Questo articolo |

[!DNL Adobe Workfront] è un&#39;applicazione per la gestione dell&#39;intero ciclo di vita del lavoro in un&#39;unica posizione. L’integrazione tra [!DNL Workfront] e [!DNL Adobe Experience Manager Assets] consente alle organizzazioni di migliorare la velocità dei contenuti e il time-to-market, grazie a un collegamento intrinseco tra il lavoro e la gestione delle risorse digitali. Nel contesto di gestione del proprio lavoro in Workfront, gli utenti possono accedere ai documenti e alle immagini necessari.

[!DNL Workfront for Experience Manager enhanced connector] abilita processi aziendali avanzati con flussi di lavoro end-to-end e fornisce esperienze client end-to-end personalizzate e archiviazione centrale. Adobe offre un connettore standard e un connettore avanzato per integrare le due soluzioni. Vedi le funzionalità supportate di seguito per un confronto e scopri [le novità di [!DNL enhanced connector]](https://one.workfront.com/s/csh?context=2467&pubname=the-new-workfront-experience).

[!DNL Workfront for Experience Manage enhanced connector] consente all&#39;organizzazione di:

* Crea automaticamente le cartelle Experience Manager collegate in Workfront e organizzale in base a portfolio, programmi e progetti Workfront.
* Sincronizza i metadati del progetto Workfront con le cartelle Experience Manager collegate.
* I metadati di Experience Manager vengono aggiornati con le nuove versioni.
* Imposta gli stati degli oggetti Workfront in base a condizioni configurabili utilizzando i flussi di lavoro Experience Manager.
* Pubblicare risorse in Experience Manager Publish Environment o Brand Portal.

Consulta Supporto piattaforma e [prerequisiti per il connettore avanzato](https://one.workfront.com/s/csh?context=2467&pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* Adobe richiede la distribuzione e la configurazione di [!DNL Adobe Workfront for Experience Manager enhanced connector] solo tramite partner certificati o [!DNL Adobe Professional Services]. Se distribuita e configurata senza un partner certificato o [!DNL Adobe Professional Services], non è supportata da Adobe.
>
>* Adobe potrebbe rilasciare aggiornamenti a [!DNL Adobe Workfront] e [!DNL Adobe Experience Manager] che rendono ridondante questo connettore; in tal caso, i clienti potrebbero dover passare dall&#39;utilizzo di questo connettore.
>
>* Adobe supporta le versioni migliorate del connettore 1.7.4 e successive. Le versioni precedenti prerelease e personalizzate non sono supportate. Per verificare la versione avanzata del connettore, passa al gruppo `digital.hoodoo` disponibile nel riquadro a sinistra in [Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en).
>
>* Consulta [Esame di certificazione partner per il connettore avanzato Workfront for Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Per informazioni sull&#39;esame, vedere [Guida all&#39;esame](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).

## Confronta diverse integrazioni tra [!DNL Assets] e [!DNL Workfront] {#feature-parity-matrix}

Di seguito sono riportati i dettagli delle funzionalità disponibili tramite vari tipi di integrazioni tra [!DNL Assets] e [!DNL Workfront].

| Funzione | Descrizione | [!DNL Workfront] e [!DNL Assets Essentials] *Nessun connettore (preconfigurato)* | [!DNL Workfront for Experience Manager enhanced connector] *Richiede Connettore* | Workfront e [!DNL Experience Manager as a Cloud Service] *Nessun connettore (preconfigurato)* |
|----|----|----|-----|-----|
| Metodi di implementazione | Appropriato per l&#39;offerta [!DNL Assets]. | Assets Essentials | Adobe Managed Services, on-premise | Cloud Service |
| **Generale** |  |  |  |  |
| Invia file digitali da [!DNL Workfront] a [!DNL Assets] | È possibile caricare in AEM Assets l’ultima versione di un documento WF collegata come nuova versione del documento. | ✓ | ✓ | ✓ |
| Collegare manualmente le cartelle di AEM agli oggetti di Workfront | Le cartelle AEM esistenti possono essere collegate come una cartella Workfront e le relative risorse secondarie vengono collegate come nuovi documenti Workfront. | ✓ | ✓ | ✓ |
| Collega [!DNL Assets] a oggetti Workfront | Le risorse esistenti in AEM possono essere collegate a un nuovo documento Workfront o come nuova versione di un documento esistente. | ✓ | ✓ | ✓ |
| Gli Assets aggiunti alle cartelle collegate vengono inviati automaticamente ad AEM | Se un documento viene aggiunto a una cartella collegata, la risorsa associata viene caricata automaticamente in AEM Assets come nuova risorsa. | ✓ | ✓ | ✓ |
| Scaricare Linked AEM Assets da Workfront | Quando una risorsa è collegata in Workfront, l’utente può scaricarne i byte. | ✓ | ✓ | ✓ |
| Cerca AEM Assets da Workfront | Il selettore AEM Assets in Workfront consente ricerche full-text nelle risorse. | ✓ | ✓ | ✓ |
| Cercare cartelle di AEM da Workfront | Il selettore AEM Assets in Workfront consente ricerche full-text nelle cartelle. | ✓ | ✓ | ✓ |
| Visualizzare e navigare nella gerarchia di cartelle di AEM da Workfront | Il selettore AEM Assets in Workfront consente di navigare nella gerarchia AEM Assets limitata dalla   i controlli di accesso e le autorizzazioni associati all’utente impostati in AEM. | ✓ | ✓ | ✓ |
| Tracciare le versioni delle risorse nelle timeline di AEM | Gestisce la cronologia delle versioni dei documenti tra Workfront e AEM. | ✓ | ✓ | ✓ |
| Scollegare Assets da AEM Assets in Workfront | È possibile scollegare dal documento Workfront associato una risorsa collegata esistente da AEM. Questa operazione non elimina la risorsa originale all’interno di AEM. | ✓ | ✓ | ✓ |
| Aggiungi risorsa con nuove versioni ad AEM Assets da Workfront | Quando in Workfront viene aggiunta una nuova versione a un documento, l’utente può inviare la nuova versione ad AEM per sostituire la versione esistente. | ✓ | ✓ | ✓ |
| Assets collegato in Workfront quando si fa clic su Utente diretto in AEM | Gli utenti vengono indirizzati ad AEM per visualizzare in anteprima una risorsa collegata da Workfront. | ✓ | ✓ | Prossimo |
| Creazione automatica di cartelle AEM collegate in Workfront | Crea automaticamente cartelle AEM collegate in Workfront utilizzando gli stati del progetto. Configura automaticamente le cartelle di AEM in base a portfolio, programmi e progetti Workfront. | No | ✓ | No |
| Passa direttamente agli archivi di AEM da Workfront | Consenti agli utenti di passare agli archivi AEM disponibili configurati in Workfront. | ✓ | No | ✓ |
| Creare cartelle AEM collegate in Workfront | Crea manualmente le cartelle AEM collegate in Workfront utilizzando l’opzione disponibile nella scheda Documenti. | ✓ | No | ✓ |
| Sincronizzazione commenti | Sincronizza automaticamente i commenti per le risorse da [!DNL Workfront] a [!DNL Assets] | No | ✓ | No |
| Supporto di più ambienti Workfront collegati a un unico ambiente AEM | Gli utenti di più ambienti Workfront possono connettersi a un singolo ambiente AEM. | ✓ | No | ✓ |
| Supporto di più ambienti AEM collegati a un unico ambiente Workfront | Gli utenti all’interno di un singolo ambiente Workfront possono inviare o collegare risorse tra più ambienti AEM. | ✓ | ✓ | ✓ |
| **Metadati** |  |  |  |  |
| Mappare i metadati delle risorse Workfront su AEM Assets | Le proprietà dell’oggetto Workfront e del modulo personalizzato possono essere mappate alle proprietà dei metadati delle risorse AEM. I valori vengono inviati al caricamento/collegamento iniziale. | ✓ | ✓ | ✓ |
| Creazione automatica di un documento Forms personalizzato in Workfront | Allegare moduli personalizzati a documenti, attività e problemi di Workfront utilizzando i flussi di lavoro di AEM. | No | ✓ | No |
| Aggiornamento automatico bidirezionale dei metadati tra AEM Assets e Workfront | Aggiorna automaticamente i metadati tra AEM Assets e Workfront. Inizialmente, la risorsa deve essere inviata da Workfront ad AEM e i metadati della risorsa Workfront devono essere mappati sulle risorse AEM affinché gli aggiornamenti bidirezionali dei metadati funzionino correttamente. | No | ✓ | No |
| Visualizzazione in tempo reale in Workfront per metadati mappati su AEM | Visualizza i metadati mappati aggiornati su AEM nei pannelli Dettagli documento e Riepilogo documento di Workfront. | ✓ | No | ✓ |
| Invio in tempo reale di metadati Workfront aggiornati ad AEM | Aggiorna automaticamente in AEM i metadati Workfront mappati senza dover eseguire il repushing di una risorsa o di una sua nuova versione. | ✓ | No | ✓ |
| Mappare i metadati di Workfront alle cartelle di AEM Assets | Sincronizza i metadati del progetto Workfront con le cartelle AEM collegate. | No | ✓ | ✓ |
| Aggiornamenti dei metadati di AEM con nuove versioni | È possibile effettuare una configurazione in AEM per determinare se anche una risorsa con nuove versioni in Workfront deve essere inviata con le modifiche apportate ai relativi metadati. | No | ✓ | No |
| Aggiornamento automatico dei metadati di AEM in seguito alle modifiche apportate al Forms personalizzato in Workfront | AEM consente di abbonarsi agli aggiornamenti ai moduli del documento in Workfront. Di conseguenza, eventuali aggiornamenti ai metadati del modulo personalizzato del documento di Workfront modificano i valori dei campi di metadati di AEM mappati. | No | ✓ | No |
| **Flussi di lavoro (preconfigurati)** |  |  |  |  |
| Creare una nuova versione di bozza in Linked Assets | Quando si collega una risorsa in Workfront, è possibile generare automaticamente una bozza. | No | Personalizzato | No |
| Imposta stato su oggetti Workfront | Impostare gli stati degli oggetti di Workfront in base a condizioni configurabili tramite flussi di lavoro AEM | No | ✓ | Prossimo |
| Pubblicare Assets in AEM Publish Environment o Brand Portal | Offri agli utenti di Workfront la possibilità di pubblicare automaticamente le risorse collegate in un ambiente di pubblicazione AEM o in un Brand Portal. | No | ✓ | Prossimo |
