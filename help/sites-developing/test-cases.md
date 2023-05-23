---
title: Definizione dei test case
seo-title: Defining your Test Cases
description: I test case devono essere basati sui casi d’uso e sulle specifiche dettagliate dei requisiti
seo-description: Your test cases should be based upon the use cases and the detailed requirements specification
uuid: daaa5370-bcd3-45a6-9974-f9b5af6a1529
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: f01eb2aa-6891-4f5d-8a4a-43fc1534c222
docset: aem65
exl-id: c09cde0d-401c-437f-9ec8-a0530c1312d5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# Definizione dei test case{#defining-your-test-cases}

I test case devono essere basati su:

**Casi d’uso**

* Definiscono le funzionalità richieste in termini di interazione tra gli attori (ruoli che avviano determinate azioni) e il sistema.
* I casi d’uso devono essere definiti dal cliente.

**Specifiche dettagliate dei requisiti**

* Tutti i requisiti funzionali e prestazionali devono essere testati.

I test dovrebbero definire chiaramente:

* Prerequisiti, che possono riguardare sistemi, configurazioni o esperienze di test specifici.
* Passaggi da seguire; a un livello di dettaglio adeguato.
* Risultati previsti.
* Cancella i criteri per il superamento o il fallimento.

La prospettiva di automatizzare i test case è ovviamente allettante in quanto può eliminare le attività ripetitive.

## Test manuali e automatizzati {#manual-versus-automated-tests}

Tuttavia, automatizzare i test case è un investimento significativo, pertanto alcuni aspetti dovrebbero essere presi in considerazione:

* Richiede tempo, fatica ed esperienza per l&#39;installazione e la configurazione.
* Se basati su browser, aumenta il rischio di problemi durante l’installazione degli aggiornamenti del browser, che richiedono ulteriore tempo per la correzione.
* Realmente realizzabile solo per grandi progetti.
* Questa opzione è utile quando vengono generate più versioni a scopo di test o nel piano di rilascio a lungo termine.

## Verifica di aspetti specifici {#testing-specific-aspects}

Durante il test dell’AEM, sono di particolare interesse alcuni dettagli specifici:

**Ambienti Author e Publish**

Anche se, coperto in [Ambienti](/help/sites-developing/the-basics.md#environments) è opportuno sottolineare un fattore decisivo dell’AEM per quanto riguarda i test.

Deve considerare l’AEM come due applicazioni:

* il *Autore* ambiente Questa istanza consente agli autori di inserire e pubblicare contenuti.
Questo ha un piccolo(i) set prevedibile di utenti, per i quali sono fondamentali funzionalità e prestazioni specifiche.

* il *Pubblica* ambiente Questa istanza presenta il sito web come forma pubblicata, accessibile ai visitatori.
Questo di solito ha un set più ampio di utenti, dove il volume di traffico non è sempre prevedibile al 100%. Le prestazioni sono ancora cruciali, quando si risponde alle richieste. Devono essere presi in considerazione anche il caching e il bilanciamento del carico.

Anche se lo stesso software come tale, essi:

* per scopi diversi
* hanno requisiti diversi in termini di funzionalità e prestazioni
* sono configurati in modo diverso
* sono sintonizzati separatamente
* avranno ciascuno una propria serie di test di accettazione

In altre parole, devono essere testati separatamente e con test case diversi.

**Personalizzazione**

Durante il test di personalizzazione, ogni singolo caso d’uso deve essere ripetuto utilizzando più account utente per dimostrare il comportamento.

È inoltre necessario verificare il comportamento corretto della memorizzazione in cache.

**Dispatcher**

La maggior parte dei progetti installa Dispatcher per il caching e il bilanciamento del carico.

Il test è difficile (la memorizzazione in cache si verifica a vari livelli e in varie posizioni) e deve essere eseguito in modalità black box. Gli aspetti chiave da testare per sono:

* **Precisione**
assicurati che gli aggiornamenti dei contenuti vengano visualizzati dal visitatore del sito web.

* **Continuità**
assicurarsi che il sito Web sia ancora disponibile quando un server viene arrestato.

* **Cluster**
I cluster vengono utilizzati per fornire:

   * **Failover**
Se un server ha esito negativo, l&#39;elaborazione verrà ripresa dagli altri server del cluster.

   * **Prestazioni**
Il bilanciamento del carico con failover completo aumenta le prestazioni di un cluster.
Se utilizzato per un progetto del cliente, il cluster deve essere testato per confermare il corretto funzionamento della configurazione.

## Verifica del software di terze parti {#testing-third-party-software}

Qualsiasi software di terze parti interfacciato con l&#39;AEM sarà menzionato nelle Specifiche dettagliate dei requisiti.

Tutte le prove necessarie (a seconda dell’ambito definito) devono essere analizzate e si deve ottenere una prova pulita.
