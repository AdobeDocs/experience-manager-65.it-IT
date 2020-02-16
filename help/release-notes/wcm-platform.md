---
title: Base e archivio di AEM
description: Note sulla versione specifiche di piattaforma e archivio AEM in Adobe Experience Manager 6.3.
uuid: 70626eda-c514-44bd-9f28-ff7abdc22f53
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: 66ecf4c5-6d0f-4586-880d-7d1c8a5a5614
docset: aem65
translation-type: tm+mt
source-git-commit: 4dc4a518c212555b7833ac27de02087a403d3517

---


# Base e archivio di AEM{#aem-foundation-repository}

## Elenco delle modifiche {#list-of-changes}

### Archivio {#repository}

* Adobe Experience Manager 6.5 si basa sulle versioni aggiornate del framework basato su OSGi (Apache Sling e Apache Felix) e del Java Content Repository: Apache Jackrabbit Oak 1.10.2.
* Please see [Apache Jackrabbit Oak Jira v. 1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt), [Apache Jackrabbit Oak Jira v. 1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt) and [Apache Jackrabbit Oak Jira v. 1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt) for a full overview of fixed issues.

>[!CAUTION]
>
>* La nuova versione di Oak Segment Tar presente a partire da AEM 6.3 richiede una migrazione dell’archivio. Questo passaggio è obbligatorio se stai effettuando l’aggiornamento da una versione precedente di TarMK o vuoi cambiare la nuova scheda Segment Tar da un altro tipo di persistenza. For more information on what the benefits of the new Segment Tar are, see the [Migrating to Oak Segment Tar FAQ](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar).
>



### Supporto per Java {#java-support}

* Nuovo supporto per Java 11, che si aggiunge alla versione già supportata di Java 8
* Per prestazioni ottimali, sovrascrivi i valori GC predefiniti con altri valori. Per ulteriori informazioni, consulta la sezione [Installazione e aggiornamento](/help/sites-deploying/custom-standalone-install.md).
* Gli aggiornamenti di manutenzione per Java 11 e Java 8 saranno distribuiti da Adobe in modo che i clienti possano usarli in progetti relativi ad AEM, qualora non siano disponibili pubblicamente da Oracle

### OSGI {#osgi}

* Sono state aggiunte le librerie di utilità Promesse OSGi e Converter

### Progetti e flussi di lavoro {#projects-and-workflows}

* Il nuovo editor per modelli di flusso di lavoro introdotto nella versione 6.4 è stato migliorato per includere più operazioni come copia e pubblicazione, supporto delle variabili nei passaggi del flusso di lavoro e miglioramento delle suddivisioni OR e AND.

### Ricerca {#searching}

* La ricerca in Oak supporta ora i facet dinamici. Ad esempio, la barra laterale del filtro nella ricerca delle risorse mostra la quantità stimata di risultati.
* QueryBuilder è stato esteso per fornire risultati con facet dinamici

### Protezione {#security}

* Aggiunta la scadenza della password per l’utente amministratore.

### Interfaccia utente {#user-interface}

Sono stati apportati vari miglioramenti all’interfaccia utente per renderla più produttiva e facile da usare.

* AEM 6.5 introduce una nuova interfaccia utente di gestione delle autorizzazioni per utenti e gruppi con cui è più facile visualizzare e configurare l’intero insieme di diritti e restrizioni senza ricorrere a CRXDE.
* La vista a colonne ora carica solo le voci che sono visibili sullo schermo e ne carica altre solo quando l’utente inizia a scorrere. Questa funzione era già disponibile nelle viste a elenco e a schede dalla versione 6.0 (migliorata in 6.4)
* La vista a colonna ora include lo stato del flusso di lavoro per le pagine/risorse, se applicabile
* L’azione “Seleziona tutto” permette di eseguire rapidamente un’azione su tutte le pagine/risorse nella stessa cartella
* L’azione “Seleziona tutto” tenta di eseguire l’azione su tutte le pagine/risorse, non solo sugli elementi caricati. Viene visualizzata una finestra di avvertenza qualora l’azione non sia stata aggiornata per gestire le azioni collettive

>[!CAUTION]
>
>* Adobe non prevede di apportare ulteriori miglioramenti all’interfaccia utente classica. In AEM 6.5 è già inclusa l’interfaccia utente classica e i clienti che eseguono l’aggiornamento da versioni precedenti possono continuare a usarla normalmente. Note that Classic UI remains fully supported while being deprecated [Read more](/help/sites-deploying/ui-recommendations.md).
>



### Aggiornamento {#upgrade}

* La procedura di aggiornamento rimane sostanzialmente la stessa nella versione 6.5.
* Continueremo a supportare la compatibilità con le versioni precedenti, la valutazione della complessità dell’aggiornamento e le funzionalità di aggiornamento progressivo introdotte nella versione 6.4. Sono stati apportati aggiornamenti specifici a queste aree, ove necessario.
* Il pacchetto Pattern Detector è stato semplificato e ci sarà un pacchetto per la valutazione degli aggiornamenti a 6.5 per le versioni sorgente disponibili.
* Please see the [Upgrade documentation](/help/sites-deploying/upgrade.md) for more details on upgrade procedure.

### Server web {#web-server}

* La distribuzione di Quickstart utilizza Eclipse Jetty 9.4.15 come motore servlet (AEM 6.4 fornito con 9.3.22)

