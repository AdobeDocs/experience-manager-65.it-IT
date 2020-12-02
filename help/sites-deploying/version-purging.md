---
title: Rimozione delle versioni
seo-title: Rimozione delle versioni
description: Questo articolo descrive le opzioni disponibili per l'eliminazione delle versioni.
seo-description: Questo articolo descrive le opzioni disponibili per l'eliminazione delle versioni.
uuid: a9fa25c7-e60e-4665-a726-99af9aac8f70
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: fb4d7337-7b94-430b-80d2-f1754f823c2b
docset: aem65
translation-type: tm+mt
source-git-commit: 1f7a45adc73b407c402a51b061632e72d97ca306
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 1%

---


# Scorrimento delle versioni{#version-purging}

In un’installazione standard AEM creare una nuova versione di una pagina o di un nodo quando si attiva una pagina dopo l’aggiornamento del contenuto.

>[!NOTE]
>
>Se non viene apportata alcuna modifica al contenuto, verrà visualizzato il messaggio che indica che la pagina è stata attivata, ma non verrà creata alcuna nuova versione

Potete creare versioni aggiuntive su richiesta utilizzando la scheda **Gestione versioni** della barra laterale. Queste versioni sono memorizzate nella directory archivio e possono essere ripristinate se necessario.

Queste versioni non vengono mai eliminate, pertanto la dimensione del repository aumenterà nel tempo e dovrà essere gestita.

AEM viene fornito con diversi meccanismi per la gestione del repository:

* [Version Manager](#version-manager)
Questa opzione può essere configurata per eliminare le versioni precedenti al momento della creazione di nuove versioni.

* lo strumento [Rimuovi versioni](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool)
Questa funzione è utilizzata per monitorare e mantenere l&#39;archivio.
Consente di intervenire per rimuovere versioni precedenti di un nodo, o una gerarchia di nodi, in base ai seguenti parametri:

   * Il numero massimo di versioni da conservare nella directory archivio.
Quando questo numero viene superato, viene rimossa la versione più vecchia.

   * Età massima di qualsiasi versione conservata nella directory archivio.
Quando l’età di una versione supera tale valore, viene eliminata dalla directory archivio.

* l&#39;attività di manutenzione [Version Purge](/help/sites-administering/operations-dashboard.md#automated-maintenance-tasks). È possibile pianificare l&#39;attività di manutenzione di Rimozione versioni per eliminare automaticamente le versioni precedenti. Questo riduce al minimo la necessità di utilizzare manualmente gli strumenti di rimozione della versione.

>[!CAUTION]
>
>Per ottimizzare le dimensioni del repository è necessario eseguire frequentemente l&#39;attività di eliminazione delle versioni. L&#39;attività deve essere programmata al di fuori degli orari di lavoro quando il traffico è limitato.

## Version Manager {#version-manager}

Oltre a rimuovere esplicitamente utilizzando lo strumento di eliminazione, Version Manager può essere configurato per eliminare le versioni precedenti quando vengono create nuove versioni.

Per configurare Version Manager, [creare una configurazione](/help/sites-deploying/configuring-osgi.md) per:

`PID com.day.cq.wcm.core.impl.VersionManagerImpl`

Sono disponibili le seguenti opzioni:

* `versionmanager.createVersionOnActivation` (Booleano, predefinito: true) Specifica se creare una versione quando le pagine vengono attivate.
Una versione viene creata a meno che l&#39;agente di replica non sia configurato per impedire la creazione di versioni, come viene rispettato da Version Manager.
Una versione viene creata solo se l&#39;attivazione avviene su un percorso contenuto in `versionmanager.ivPaths` (vedi sotto).

* `versionmanager.ivPaths`(String[], predefinito:  `{"/"}`) Specifica i percorsi in cui le versioni vengono implicitamente create al momento dell&#39;attivazione, se  `versionmanager.createVersionOnActivation` è impostata su true.

* `versionmanager.purgingEnabled` (Booleano, predefinito: false) Definisce se abilitare o meno l&#39;eliminazione quando vengono create nuove versioni.

* `versionmanager.purgePaths` (String[], predefinito: {&quot;/content&quot;}) Specifica i percorsi in cui eliminare le versioni al momento della creazione delle nuove versioni.

* `versionmanager.maxAgeDays` (int, predefinito: 30) Durante l&#39;eliminazione delle versioni, tutte le versioni precedenti al valore configurato verranno rimosse. Se il valore è minore di 1, la rimozione non verrà eseguita in base all&#39;età della versione.

* `versionmanager.maxNumberVersions` (int, predefinito 5) Durante la rimozione della versione, verranno rimosse tutte le versioni precedenti alla n-esima versione più recente. Se il valore è minore di 1, l&#39;eliminazione non viene eseguita in base al numero di versioni.

* `versionmanager.minNumberVersions` (int, default 0) Il numero minimo di versioni che verranno conservate indipendentemente dall&#39;età. Se il valore è impostato su un valore inferiore a 1, non viene mantenuto alcun numero minimo di versioni.

>[!NOTE]
>
>Non è consigliabile mantenere un numero elevato di versioni nella directory archivio. Pertanto, durante la configurazione dell&#39;operazione di eliminazione della versione, non escludere troppe versioni dalla rimozione, altrimenti la dimensione del repository non verrà ottimizzata correttamente. Se si conservano numerose versioni a causa di requisiti aziendali, contattare  supporto di Adobe per trovare modi alternativi per ottimizzare le dimensioni del repository.

### Combinazione di opzioni di conservazione {#combining-retention-options}

Le opzioni che definiscono le modalità di mantenimento delle versioni ( `maxAgeDays`, `maxNumberVersions`, `minNumberVersions`), possono essere combinate a seconda delle esigenze.

Ad esempio, quando si definisce il numero massimo di versioni da mantenere E la versione più vecchia da mantenere:

* Impostazione:

   * `maxNumberVersions` = 7

   * `maxAgeDays` = 30

* Con:

   * 10 versioni realizzate negli ultimi 60 giorni
   * 3 di tali versioni create negli ultimi 30 giorni

* Significa che:

   * Le ultime 3 versioni verranno mantenute

Ad esempio, quando si definisce il numero massimo E minimo di versioni da mantenere E la versione più vecchia da mantenere:

* Impostazione:

   * `maxNumberVersions` = 3
   * `maxAgeDays` = 30
   * `minNumberVersions` = 3

* Con:

   * 5 versioni realizzate 60 giorni fa

* Significa che:

   * Verranno mantenute 3 versioni

## Strumento Rimuovi versioni {#purge-versions-tool}

Lo strumento [Purge Versions](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool) consente di eliminare le versioni di un nodo o di una gerarchia di nodi nel repository. Lo scopo principale è quello di ridurre le dimensioni del repository rimuovendo le versioni precedenti dei nodi.
