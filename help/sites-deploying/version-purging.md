---
title: Rimozione versione
description: Questo articolo descrive le opzioni disponibili per l’eliminazione della versione.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
docset: aem65
feature: Configuring
exl-id: 6f0b1951-bdda-475f-b6c0-bc18de082b7c
source-git-commit: 4e2ee7da5424ac6677eaa2392de7803e7543d13c
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 1%

---

# Rimozione versione{#version-purging}

In un’installazione standard, Adobe Experience Manager (AEM) crea una versione di una pagina o di un nodo quando attivi una pagina dopo l’aggiornamento del contenuto.

>[!NOTE]
>
>Se non viene apportata alcuna modifica al contenuto, viene visualizzato il messaggio che indica che la pagina è stata attivata, ma non viene creata alcuna nuova versione.

Puoi creare versioni aggiuntive su richiesta utilizzando **Controllo delle versioni** della barra laterale. Queste versioni vengono memorizzate nell’archivio e possono essere ripristinate, se necessario.

Queste versioni non vengono mai eliminate, pertanto le dimensioni dell’archivio aumentano nel tempo e devono quindi essere gestite.

L’AEM viene fornito con vari meccanismi per aiutarti a gestire l’archivio:

* il [Gestione versioni](#version-manager)
Questa può essere configurata per eliminare le versioni precedenti quando vengono create nuove versioni.

* il [Rimuovi versioni](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool) strumento Utilizzato come parte del monitoraggio e della manutenzione dell’archivio.
Consente di intervenire per rimuovere le versioni precedenti di un nodo o di una gerarchia di nodi, in base ai seguenti parametri:

   * Il numero massimo di versioni da mantenere nell’archivio.
Se questo numero viene superato, viene rimossa la versione meno recente.

   * L’età massima di qualsiasi versione mantenuta nell’archivio.
Quando la validità di una versione supera questo valore, viene eliminata dall’archivio.

* il [Attività di manutenzione Pulizia delle versioni](/help/sites-administering/operations-dashboard.md#automated-maintenance-tasks). È possibile pianificare l&#39;attività di manutenzione Pulizia delle versioni per eliminare automaticamente le versioni precedenti. In questo modo si riduce la necessità di utilizzare manualmente gli strumenti di Pulizia delle versioni.

>[!CAUTION]
>
>Per ottimizzare le dimensioni dell&#39;archivio, eseguire frequentemente l&#39;operazione di eliminazione della versione. L’attività deve essere pianificata al di fuori dell’orario di lavoro in presenza di una quantità limitata di traffico.

## Gestione versioni {#version-manager}

Oltre alla rimozione esplicita mediante lo strumento di rimozione, Gestione versioni può essere configurato per eliminare le versioni precedenti quando vengono create nuove versioni.

Per configurare Gestione versioni: [creare una configurazione](/help/sites-deploying/configuring-osgi.md) per:

`PID com.day.cq.wcm.core.impl.VersionManagerImpl`

Sono disponibili le seguenti opzioni:

* `versionmanager.createVersionOnActivation` (Booleano, impostazione predefinita: true) Specifica se creare una versione quando le pagine sono attivate.
Viene creata una versione a meno che l’agente di replica non sia configurato per sopprimere la creazione delle versioni, che viene rispettata da Gestione versioni.
Una versione viene creata solo se l&#39;attivazione avviene su un percorso contenuto in `versionmanager.ivPaths` (vedi sotto).

* `versionmanager.ivPaths`(Stringa[], impostazione predefinita: `{"/"}`) Specifica i percorsi in cui le versioni vengono create in modo implicito al momento dell&#39;attivazione se `versionmanager.createVersionOnActivation` è impostato su true.

* `versionmanager.purgingEnabled` (Booleano, impostazione predefinita: false) Definisce se abilitare la rimozione quando vengono create nuove versioni.

* `versionmanager.purgePaths` (Stringa[], impostazione predefinita: {&quot;/content&quot;}) Specifica in quali percorsi eliminare le versioni quando vengono create nuove versioni.

* `versionmanager.maxAgeDays` (int, impostazione predefinita: 30) Al momento dell’eliminazione della versione, vengono rimosse tutte le versioni precedenti al valore configurato. Se il valore è minore di 1, la rimozione non viene eseguita in base alla data della versione.

* `versionmanager.maxNumberVersions` (int, impostazione predefinita 5) Al momento dell’eliminazione della versione, vengono rimosse tutte le versioni precedenti all’n-esima versione più recente. Se il valore è minore di 1, la rimozione non viene eseguita in base al numero di versioni.

* `versionmanager.minNumberVersions` (int, valore predefinito 0) Il numero minimo di versioni conservate indipendentemente dall’età. Se il valore è impostato su un valore minore di 1, non viene mantenuto alcun numero minimo di versioni.

>[!NOTE]
>
>Si sconsiglia di mantenere molte versioni nell’archivio. Pertanto, durante la configurazione dell’operazione di eliminazione della versione, fai attenzione a non escludere troppe versioni dalla rimozione, altrimenti la dimensione dell’archivio non viene ottimizzata correttamente. Se conservi un numero elevato di versioni a causa di requisiti aziendali, contatta il supporto di Adobe per trovare modi alternativi per ottimizzare la dimensione dell’archivio.

### Combinazione delle opzioni di conservazione {#combining-retention-options}

Le opzioni che definiscono il modo in cui le versioni devono essere conservate ( `maxAgeDays`, `maxNumberVersions`, `minNumberVersions`), possono essere combinati in base alle tue esigenze.

Ad esempio, quando definisci il numero massimo di versioni da mantenere E la versione più vecchia da mantenere:

* Impostazione:

   * `maxNumberVersions` = 7

   * `maxAgeDays` = 30

* Con:

   * Sono state realizzate dieci versioni negli ultimi 60 giorni
   * Tre di queste versioni sono state create negli ultimi 30 giorni

* Ciò significa che:

   * Le ultime tre versioni vengono mantenute

Ad esempio, quando definisci il numero massimo E minimo di versioni da mantenere E la versione più vecchia da mantenere:

* Impostazione:

   * `maxNumberVersions` = 3
   * `maxAgeDays` = 30
   * `minNumberVersions` = 3

* Con:

   * Cinque versioni sono state realizzate 60 giorni fa

* Ciò significa che:

   * Vengono conservate tre versioni

## Strumento Rimuovi versioni {#purge-versions-tool}

Il [Rimuovi versioni](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool) Questo strumento serve per eliminare le versioni di un nodo o di una gerarchia di nodi nell’archivio. Il suo scopo principale è quello di aiutare a ridurre le dimensioni dell’archivio rimuovendo le versioni precedenti dei nodi.
