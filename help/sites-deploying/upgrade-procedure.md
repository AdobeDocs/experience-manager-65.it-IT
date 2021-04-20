---
title: Procedura di aggiornamento
seo-title: Procedura di aggiornamento
description: Scopri la procedura da seguire per aggiornare AEM.
seo-description: Scopri la procedura da seguire per aggiornare AEM.
uuid: 81126a70-c082-4f01-a1ad-7152182da88b
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: 5c035d4c-6e03-48b6-8404-800b52d659b8
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 0%

---


# Procedura di aggiornamento {#upgrade-procedure}

>[!NOTE]
>
>L’aggiornamento richiederà tempi di inattività per il livello di authoring, in quanto la maggior parte degli aggiornamenti AEM vengono eseguiti sul posto. Seguendo queste best practice, è possibile ridurre o eliminare i tempi di inattività del livello di pubblicazione.

Quando aggiorni gli ambienti di AEM, è necessario considerare le differenze di approccio tra l’aggiornamento degli ambienti di authoring o di pubblicazione per ridurre al minimo i tempi di inattività sia per gli autori che per gli utenti finali. Questa pagina illustra la procedura di alto livello per l’aggiornamento di una topologia AEM attualmente in esecuzione su una versione di AEM 6.x. Poiché il processo è diverso tra i livelli di authoring e pubblicazione e le implementazioni basate su Mongo e TarMK, ogni livello e microkernel è stato elencato in una sezione separata. Durante l’esecuzione della distribuzione, consigliamo innanzitutto di aggiornare l’ambiente di authoring, determinare il successo e quindi procedere con gli ambienti di pubblicazione.

<!--
>[!IMPORTANT]
>
>The downtime during the upgrade can be significally reduced by indexing the repository before performing the upgrade. For more information, see [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)
-->

## Livello di authoring TarMK {#tarmk-author-tier}

### Topologia iniziale {#starting-topology}

La topologia presunta per questa sezione è costituita da un server Author in esecuzione su TarMK con uno standby a freddo. La replica si verifica dal server Author alla farm di pubblicazione TarMK. Anche se non è illustrato qui, questo approccio può essere utilizzato anche per le distribuzioni che utilizzano lo scaricamento. Assicurati di aggiornare o ricreare l&#39;istanza di offload sulla nuova versione dopo aver disabilitato gli agenti di replica sull&#39;istanza Author e prima di riabilitarli.

![tarmk_start_topology](assets/tarmk_starting_topology.jpg)

### Preparazione all&#39;aggiornamento {#upgrade-preparation}

![upgrade-preparation-author](assets/upgrade-preparation-author.png)

1. Interrompere la creazione dei contenuti

1. Arresta l&#39;istanza di standby

1. Disattiva gli agenti di replica sull&#39;autore

1. Esegui le [attività di manutenzione pre-aggiornamento](/help/sites-deploying/pre-upgrade-maintenance-tasks.md).

### Esecuzione aggiornamento {#upgrade-execution}

![execute_upgrade](assets/execute_upgrade.jpg)

1. Esegui l&#39; [aggiornamento sul posto](/help/sites-deploying/in-place-upgrade.md)
1. Aggiorna il modulo dispatcher *se necessario*

1. Controllo qualità convalida l&#39;aggiornamento

1. Arresta l&#39;istanza dell&#39;autore.

### In caso di esito positivo {#if-successful}

![if_success](assets/if_successful.jpg)

1. Copia l&#39;istanza aggiornata per creare un nuovo standby a freddo

1. Avvia l&#39;istanza Author

1. Avvia l&#39;istanza Standby.

### In caso di esito negativo (rollback) {#if-unsuccessful-rollback}

![rollback](assets/rollback.jpg)

1. Avvia l&#39;istanza di standby a freddo come nuovo primario

1. Ricrea l’ambiente Authoring dallo standby a freddo.

## Cluster di authoring MongoMK {#mongomk-author-cluster}

### Topologia iniziale {#starting-topology-1}

La topologia presunta per questa sezione è costituita da un cluster Autore MongoMK con almeno due istanze Autore AEM, supportate da almeno due database MongoMK. Tutte le istanze Autore condividono un datastore. Questi passaggi devono essere applicati sia ai datastore S3 che ai file . La replica si verifica dai server Author alla farm TarMK Publish.

![mongo-topologia](assets/mongo-topology.jpg)

### Preparazione all&#39;aggiornamento {#upgrade-preparation-1}

![mongo-upgrade_prep](assets/mongo-upgrade_prep.jpg)

1. Interrompere la creazione dei contenuti
1. Clonare l&#39;archivio dati per il backup
1. Interrompi tutte le istanze AEM Author tranne una, il tuo autore principale
1. Rimuovi tutti i nodi MongoDB tranne uno dal set di repliche, l&#39;istanza Mongo primaria
1. Aggiornare il file `DocumentNodeStoreService.cfg` dell&#39;autore principale in modo che rifletta il set di repliche per membro singolo
1. Riavvia l&#39;autore principale per assicurarne il corretto riavvio
1. Disattiva gli agenti di replica sull&#39;autore principale
1. Esegui [attività di manutenzione pre-aggiornamento](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) sull&#39;istanza di authoring principale
1. Se necessario, aggiorna MongoDB sull&#39;istanza Mongo primaria alla versione 3.2 con WiredTiger

### Esecuzione aggiornamento {#Upgrade-execution-1}

![esecuzione di un mongo](assets/mongo-execution.jpg)

1. Esegui un [aggiornamento sul posto](/help/sites-deploying/in-place-upgrade.md) sull&#39;autore principale
1. Aggiorna il Dispatcher o il modulo Web *se necessario*
1. Controllo qualità convalida l&#39;aggiornamento

### In caso di esito positivo {#if-successful-1}

![mongo-secondari](assets/mongo-secondaries.jpg)

1. Crea nuove istanze di authoring 6.5, connesse all&#39;istanza Mongo aggiornata

1. Rigenera i nodi MongoDB rimossi dal cluster

1. Aggiornare i file `DocumentNodeStoreService.cfg` per riflettere l&#39;intero set di repliche

1. Riavvia le istanze di authoring, una alla volta

1. Rimuovi l&#39;archivio dati clonati.

### In caso di esito negativo (rollback) {#if-unsuccessful-rollback-2}

![mongo-rollback](assets/mongo-rollback.jpg)

1. Riconfigura le istanze di authoring secondarie per connettersi all’archivio dati clonati

1. Arrestare l&#39;istanza primaria Author aggiornata

1. Spegni l&#39;istanza primaria Mongo aggiornata.

1. Avvia le istanze Mongo secondarie con una di esse come nuova istanza primaria

1. Configurare i file `DocumentNodeStoreService.cfg` nelle istanze di authoring secondarie in modo che puntino al set di repliche delle istanze Mongo non ancora aggiornate

1. Avvia le istanze di authoring secondarie

1. Pulisci le istanze dell’autore aggiornate, il nodo Mongo e l’archivio dati.

## TarMK Publish Farm {#tarmk-publish-farm}

### TarMK Publish Farm {#tarmk-publish-farm-1}

La topologia presunta per questa sezione è costituita da due istanze di pubblicazione TarMK, precedute da Dispatcher che a loro volta sono precedute da un load balancer. La replica si verifica dal server Author alla farm di pubblicazione TarMK.

![tarmk-pub-farm v5](assets/tarmk-pub-farmv5.png)

### Esecuzione aggiornamento {#upgrade-execution-2}

![upgrade-publish2](assets/upgrade-publish2.png)

1. Arresta il traffico verso l’istanza Publish 2 al load balancer
1. Esegui [manutenzione pre-aggiornamento](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) su Publish 2
1. Esegui un [aggiornamento in-place](/help/sites-deploying/in-place-upgrade.md) su Publish 2
1. Aggiorna il Dispatcher o il modulo Web *se necessario*
1. Svuotare la cache del Dispatcher
1. Il controllo qualità convalida la pubblicazione 2 tramite Dispatcher, dietro il firewall
1. Arresta pubblicazione 2
1. Copia l&#39;istanza Publish 2
1. Avvia pubblicazione 2

### In caso di esito positivo {#if-successful-2}

![upgrade-publish1](assets/upgrade-publish1.png)

1. Abilita il traffico a Pubblica 2
1. Arresta il traffico per pubblicare 1
1. Arresta l’istanza Publish 1
1. Sostituisci l’istanza Publish 1 con una copia di Publish 2
1. Aggiorna il Dispatcher o il modulo Web *se necessario*
1. Svuotare la cache del Dispatcher per Pubblica 1
1. Avvia pubblicazione 1
1. Il controllo qualità convalida la pubblicazione 1 tramite Dispatcher, dietro il firewall

### In caso di esito negativo (rollback) {#if-unsuccessful-rollback-1}

![pub_rollback](assets/pub_rollback.jpg)

1. Crea una copia di Publish 1
1. Sostituisci l’istanza Publish 2 con una copia di Publish 1
1. Svuotare la cache del Dispatcher per Pubblica 2
1. Avvia pubblicazione 2
1. Il controllo qualità convalida la pubblicazione 2 tramite Dispatcher, dietro il firewall
1. Abilita il traffico a Pubblica 2

## Passaggi per l&#39;aggiornamento finale {#final-upgrade-steps}

1. Abilita il traffico alla pubblicazione 1
1. Il controllo qualità esegue la convalida finale da un URL pubblico
1. Abilitare gli agenti di replica dall’ambiente Author
1. Riprendere l’authoring dei contenuti
1. Esegui [controlli post-aggiornamento](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md).

![finale](assets/final.jpg)

