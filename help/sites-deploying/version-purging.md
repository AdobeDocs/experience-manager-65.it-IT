---
title: Rimozione delle versioni
seo-title: Version Purging
description: Questo articolo descrive le opzioni disponibili per l'eliminazione delle versioni.
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

# Rimozione delle versioni{#version-purging}

In un’installazione standard AEM crea una nuova versione di una pagina o di un nodo quando attivi una pagina dopo l’aggiornamento del contenuto.

>[!NOTE]
>
>Se non viene apportata alcuna modifica al contenuto, verrà visualizzato il messaggio che indica che la pagina è stata attivata, ma non verrà creata alcuna nuova versione

Puoi creare versioni aggiuntive su richiesta utilizzando la **Controllo delle versioni** scheda della barra laterale. Queste versioni sono memorizzate nell’archivio e possono essere ripristinate se necessario.

Queste versioni non vengono mai eliminate, pertanto la dimensione dell’archivio aumenterà nel tempo e deve quindi essere gestita.

AEM viene fornito con vari meccanismi per aiutarti a gestire il tuo archivio:

* la [Gestione versioni](#version-manager)
Questa può essere configurata per eliminare le versioni precedenti quando vengono create nuove versioni.

* la [Eliminare le versioni](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool) strumento Viene utilizzato come parte del monitoraggio e della manutenzione dell’archivio.
Ti consente di intervenire per rimuovere le vecchie versioni di un nodo, o una gerarchia di nodi, in base a questi parametri:

   * Il numero massimo di versioni da conservare nell’archivio.
Quando questo numero viene superato, la versione più vecchia viene rimossa.

   * L’età massima di qualsiasi versione conservata nell’archivio.
Quando l’età di una versione supera questo valore, viene eliminata dall’archivio.

* la [Attività di manutenzione dell&#39;eliminazione della versione](/help/sites-administering/operations-dashboard.md#automated-maintenance-tasks). È possibile pianificare l&#39;attività di manutenzione Pulizia versione per eliminare automaticamente le versioni precedenti. Di conseguenza, questo riduce al minimo la necessità di utilizzare manualmente gli strumenti di eliminazione delle versioni.

>[!CAUTION]
>
>Per ottimizzare le dimensioni del repository, è necessario eseguire frequentemente l&#39;attività di eliminazione della versione. L&#39;attività deve essere pianificata al di fuori dell&#39;orario di lavoro quando vi è una quantità limitata di traffico.

## Gestione versioni {#version-manager}

Oltre all&#39;eliminazione esplicita tramite lo strumento di eliminazione, Version Manager può essere configurato per eliminare le versioni precedenti quando vengono create nuove versioni.

Per configurare Version Manager, [creare una configurazione](/help/sites-deploying/configuring-osgi.md) per:

`PID com.day.cq.wcm.core.impl.VersionManagerImpl`

Sono disponibili le seguenti opzioni:

* `versionmanager.createVersionOnActivation` (Booleano, predefinito: true) Specifica se creare una versione quando le pagine vengono attivate.
Viene creata una versione a meno che l’agente di replica non sia configurato in modo da eliminare la creazione di versioni, che viene rispettata da Version Manager.
Una versione viene creata solo se l&#39;attivazione avviene su un percorso contenuto in `versionmanager.ivPaths` (vedi sotto).

* `versionmanager.ivPaths`(Stringa[], predefinito: `{"/"}`) Specifica i percorsi in cui le versioni vengono create implicitamente all&#39;attivazione se `versionmanager.createVersionOnActivation` è impostato su true.

* `versionmanager.purgingEnabled` (Booleano, predefinito: false) Definisce se abilitare o meno l&#39;eliminazione quando vengono create nuove versioni.

* `versionmanager.purgePaths` (Stringa[], predefinito: {&quot;/content&quot;}) Specifica i percorsi in cui eliminare le versioni quando vengono create nuove versioni.

* `versionmanager.maxAgeDays` (int, predefinito: 30) Durante l&#39;eliminazione della versione, verrà rimossa qualsiasi versione precedente al valore configurato. Se il valore è minore di 1, la rimozione non verrà eseguita in base all&#39;età della versione.

* `versionmanager.maxNumberVersions` (int, default 5) Durante l’eliminazione della versione, verranno rimosse tutte le versioni precedenti all’ultima versione. Se il valore è minore di 1, la rimozione non viene eseguita in base al numero di versioni.

* `versionmanager.minNumberVersions` (int, default 0) Il numero minimo di versioni che verranno mantenute indipendentemente dall&#39;età. Se il valore è impostato su un valore inferiore a 1, non viene mantenuto un numero minimo di versioni.

>[!NOTE]
>
>Si sconsiglia di mantenere un numero elevato di versioni nell’archivio. Quindi, quando configuri l&#39;operazione di eliminazione della versione, fai attenzione a non escludere troppe versioni dalla rimozione, altrimenti la dimensione dell&#39;archivio non verrà ottimizzata correttamente. Se mantieni un numero elevato di versioni a causa di requisiti aziendali, contatta il supporto Adobe per trovare modi alternativi per ottimizzare le dimensioni dell’archivio.

### Combinazione delle opzioni di conservazione {#combining-retention-options}

Le opzioni che definiscono come mantenere le versioni ( `maxAgeDays`, `maxNumberVersions`, `minNumberVersions`), può essere combinato a seconda delle tue esigenze.

Ad esempio, quando definisci il numero massimo di versioni da mantenere E la versione più vecchia da mantenere:

* Impostazione:

   * `maxNumberVersions` = 7

   * `maxAgeDays` = 30

* Con:

   * 10 versioni effettuate negli ultimi 60 giorni
   * 3 di queste versioni create negli ultimi 30 giorni

* Ciò significa che:

   * Verranno mantenute le ultime 3 versioni

Ad esempio, quando definisci il numero massimo E minimo di versioni da mantenere e la versione più vecchia da mantenere:

* Impostazione:

   * `maxNumberVersions` = 3
   * `maxAgeDays` = 30
   * `minNumberVersions` = 3

* Con:

   * 5 versioni realizzate 60 giorni fa

* Ciò significa che:

   * Verranno mantenute 3 versioni

## Strumento Elimina versioni {#purge-versions-tool}

La [Eliminare le versioni](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool) strumento è destinato a eliminare le versioni di un nodo o una gerarchia di nodi nel tuo archivio. Il suo scopo principale è quello di aiutarti a ridurre le dimensioni dell’archivio rimuovendo le vecchie versioni dei nodi.
