---
title: Rimozione versione
seo-title: Version Purging
description: Questo articolo descrive le opzioni disponibili per l’eliminazione della versione.
seo-description: This article describes the available options for version purging.
uuid: a9fa25c7-e60e-4665-a726-99af9aac8f70
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: fb4d7337-7b94-430b-80d2-f1754f823c2b
docset: aem65
feature: Configuring
exl-id: 6f0b1951-bdda-475f-b6c0-bc18de082b7c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 1%

---

# Rimozione versione{#version-purging}

In un’installazione standard, AEM crea una nuova versione di una pagina o di un nodo quando attivi una pagina dopo l’aggiornamento del contenuto.

>[!NOTE]
>
>Se non viene apportata alcuna modifica al contenuto, verrà visualizzato il messaggio che indica che la pagina è stata attivata, ma non verrà creata alcuna nuova versione

Puoi creare versioni aggiuntive su richiesta utilizzando **Controllo delle versioni** della barra laterale. Queste versioni vengono memorizzate nell’archivio e possono essere ripristinate se necessario.

Queste versioni non vengono mai eliminate, pertanto le dimensioni dell’archivio aumenteranno nel tempo e devono quindi essere gestite.

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
>Per ottimizzare le dimensioni dell’archivio, è necessario eseguire frequentemente l’attività di rimozione della versione. L’attività deve essere pianificata al di fuori dell’orario di lavoro in presenza di una quantità limitata di traffico.

## Gestione versioni {#version-manager}

Oltre alla rimozione esplicita mediante lo strumento di rimozione, Gestione versioni può essere configurato per eliminare le versioni precedenti quando vengono create nuove versioni.

Per configurare Gestione versioni: [creare una configurazione](/help/sites-deploying/configuring-osgi.md) per:

`PID com.day.cq.wcm.core.impl.VersionManagerImpl`

Sono disponibili le seguenti opzioni:

* `versionmanager.createVersionOnActivation` (Booleano, impostazione predefinita: true) Specifica se creare una versione quando le pagine sono attivate.
Viene creata una versione a meno che l’agente di replica non sia configurato per sopprimere la creazione delle versioni, che viene rispettata da Gestione versioni.
Una versione viene creata solo se l&#39;attivazione avviene su un percorso contenuto in `versionmanager.ivPaths` (vedi sotto).

* `versionmanager.ivPaths`(Stringa[], impostazione predefinita: `{"/"}`) Specifica i percorsi in cui le versioni vengono create in modo implicito al momento dell&#39;attivazione se `versionmanager.createVersionOnActivation` è impostato su true.

* `versionmanager.purgingEnabled` (Booleano, predefinito: false) Definisce se abilitare o meno la rimozione quando vengono create nuove versioni.

* `versionmanager.purgePaths` (Stringa[], impostazione predefinita: {&quot;/content&quot;}) Specifica in quali percorsi eliminare le versioni quando vengono create nuove versioni.

* `versionmanager.maxAgeDays` (int, impostazione predefinita: 30) Al momento dell’eliminazione della versione, tutte le versioni precedenti al valore configurato verranno rimosse. Se il valore è minore di 1, la rimozione non verrà eseguita in base alla data della versione.

* `versionmanager.maxNumberVersions` (int, impostazione predefinita 5) Al momento dell’eliminazione della versione, verranno rimosse tutte le versioni precedenti all’n-esima versione più recente. Se il valore è minore di 1, la rimozione non viene eseguita in base al numero di versioni.

* `versionmanager.minNumberVersions` (int, impostazione predefinita: 0) Il numero minimo di versioni che verranno mantenute indipendentemente dall’età. Se il valore è impostato su un valore minore di 1, non viene mantenuto alcun numero minimo di versioni.

>[!NOTE]
>
>Si sconsiglia di mantenere un numero elevato di versioni nell’archivio. Pertanto, durante la configurazione dell’operazione di eliminazione della versione, presta attenzione a non escludere troppe versioni dalla rimozione, altrimenti la dimensione dell’archivio non verrà ottimizzata correttamente. Se conservi un numero elevato di versioni a causa di requisiti aziendali, contatta il supporto Adobe per trovare modi alternativi per ottimizzare la dimensione dell’archivio.

### Combinazione delle opzioni di conservazione {#combining-retention-options}

Le opzioni che definiscono il modo in cui le versioni devono essere conservate ( `maxAgeDays`, `maxNumberVersions`, `minNumberVersions`), possono essere combinati in base alle tue esigenze.

Ad esempio, quando definisci il numero massimo di versioni da mantenere E la versione più vecchia da mantenere:

* Impostazione:

   * `maxNumberVersions` = 7

   * `maxAgeDays` = 30

* Con:

   * 10 versioni effettuate negli ultimi 60 giorni
   * 3 di queste versioni create negli ultimi 30 giorni

* Significa che:

   * Le ultime 3 versioni verranno mantenute

Ad esempio, quando definisci il numero massimo E minimo di versioni da mantenere E la versione più vecchia da mantenere:

* Impostazione:

   * `maxNumberVersions` = 3
   * `maxAgeDays` = 30
   * `minNumberVersions` = 3

* Con:

   * 5 versioni effettuate 60 giorni fa

* Significa che:

   * Verranno mantenute 3 versioni

## Strumento Rimuovi versioni {#purge-versions-tool}

Il [Rimuovi versioni](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool) Questo strumento serve per eliminare le versioni di un nodo o di una gerarchia di nodi nell’archivio. Il suo scopo principale è quello di aiutare a ridurre le dimensioni dell’archivio rimuovendo le versioni precedenti dei nodi.
