---
title: AEM Foundation e repository
description: Note sulla versione per la piattaforma e l’archivio Adobe Experience Manager.
translation-type: tm+mt
source-git-commit: 8d60e064ab50f24016c049c8d5d0fceb784c99a3
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 56%

---


# AEM Foundation e repository {#aem-foundation-repository}

## Elenco delle modifiche {#list-of-changes}

### Archivio {#repository}

* Adobe Experience Manager 6.5 si basa sulle versioni aggiornate del framework basato su OSGi (Apache Sling e Apache Felix) e del Java Content Repository: Apache Jackrabbit Oak 1.10.2.
* Per una panoramica dei problemi risolti, vedere [Apache Jackrabbit Oak Jira v. 1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt), [Apache Jackrabbit Oak Jira v. 1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt) e [Apache Jackrabbit Oak Jira v. 1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt).

>[!CAUTION]
>
>La nuova versione di Oak Segment Tar presente a partire da AEM 6.3 richiede una migrazione dell’archivio. Questo passaggio è obbligatorio se stai effettuando l’aggiornamento da una versione precedente di TarMK o vuoi cambiare la nuova scheda Segment Tar da un altro tipo di persistenza. Per ulteriori informazioni sui vantaggi della nuova ar segmento, vedere le [Domande frequenti sulla migrazione alla ar segmento Oak](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar).

### Supporto per Java {#java-support}

* Nuovo supporto per Java 11, che si aggiunge alla versione già supportata di Java 8.
* Per prestazioni ottimali, sovrascrivi i valori GC predefiniti con altri valori. Per ulteriori informazioni, consulta la sezione [Installazione e aggiornamento](/help/sites-deploying/custom-standalone-install.md).
* Gli aggiornamenti di manutenzione di Java 11 e Java 8 vengono distribuiti dal Adobe  per l&#39;utilizzo da parte dei clienti nei progetti AEM, quando non sono disponibili al pubblico da  Oracle.

### OSGI {#osgi}

* Sono state aggiunte le librerie di utilità Promesse OSGi e Converter.

### Progetti e flussi di lavoro {#projects-and-workflows}

* Il nuovo editor per modelli di workflow introdotto in 6.4 è stato migliorato per includere più operazioni come Copia e Pubblica, Supporto delle variabili nei passaggi del flusso di lavoro e suddivisioni `OR` e `AND` migliorate.

### Ricerca {#searching}

* La ricerca in Oak supporta ora i facet dinamici. Ad esempio, la barra laterale del filtro nella ricerca delle risorse mostra la quantità stimata di risultati.
* QueryBuilder è stato esteso per fornire risultati con facet dinamici.

### Sicurezza {#security}

* Aggiunta la scadenza della password per l’utente amministratore.

### Interfaccia utente {#user-interface}

Sono stati apportati vari miglioramenti all’interfaccia utente per renderla più produttiva e facile da usare.

* AEM 6.5 introduce una nuova interfaccia utente di gestione delle autorizzazioni per utenti e gruppi con cui è più facile visualizzare e configurare l’intero insieme di diritti e restrizioni senza ricorrere a CRXDE.
* La vista a colonne ora carica solo le voci che sono visibili sullo schermo e ne carica altre solo quando l’utente inizia a scorrere. Questa funzione era già disponibile nelle viste a elenco e a schede dalla versione 6.0 (migliorata in 6.4).
* La vista a colonna ora include lo stato del flusso di lavoro per le pagine/risorse, se applicabile.
* L’azione Seleziona tutto permette di eseguire rapidamente un’azione su tutte le pagine/risorse nella stessa cartella.
* L’azione Seleziona tutto tenta di eseguire l’azione su tutte le pagine/risorse, non solo sugli elementi caricati. Se l&#39;azione non viene aggiornata per gestire le azioni di massa, viene visualizzato un avviso.

>[!CAUTION]
>
> Adobe non apporterà ulteriori miglioramenti all’interfaccia classica.  Experience Manager 6.5 include l&#39;interfaccia classica per la compatibilità con le versioni precedenti. L&#39;interfaccia classica rimane completamente supportata anche se è obsoleta [Leggi tutto](/help/sites-deploying/ui-recommendations.md).

### Aggiornamento {#upgrade}

* La procedura di aggiornamento rimane sostanzialmente la stessa nella versione 6.5.
* Continueremo a supportare la compatibilità con le versioni precedenti, la valutazione della complessità dell’aggiornamento e le funzionalità di aggiornamento progressivo introdotte nella versione 6.4. Sono stati apportati aggiornamenti specifici a queste aree, ove necessario.
* Il pacchetto Pattern Detector è stato semplificato e ci sarà un pacchetto per la valutazione degli aggiornamenti a 6.5 per le versioni sorgente disponibili.
* Per informazioni dettagliate sulla procedura di aggiornamento, consultare la [documentazione di aggiornamento](/help/sites-deploying/upgrade.md).

### Server web {#web-server}

* La distribuzione di Quickstart utilizza Eclipse Jetty 9.4.15 come motore servlet (AEM 6.4 fornito con 9.3.22).
