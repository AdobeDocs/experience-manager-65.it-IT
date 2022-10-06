---
title: Definizione dei casi di test
seo-title: Defining your Test Cases
description: I casi di test devono essere basati sui casi di utilizzo e sulle specifiche dei requisiti dettagliati
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

# Definizione dei casi di test{#defining-your-test-cases}

I casi di test devono essere basati su:

**Casi d&#39;uso**

* Questi definiscono la funzionalità necessaria in termini di interazione tra gli attori (ruoli che avviano determinate azioni) e il sistema.
* I casi d’uso devono essere definiti dal cliente.

**Specifiche tecniche**

* Tutti i requisiti funzionali e di prestazioni devono essere verificati.

Le prove devono definire chiaramente:

* Prerequisiti; questi possono riguardare sistemi, configurazioni o esperienza di tester specifici.
* Le misure da seguire; ad un livello di dettaglio adeguato.
* Risultati previsti.
* Cancella i criteri per il superamento o il mancato funzionamento.

La prospettiva di automatizzare i test case è ovviamente attraente in quanto può eliminare i compiti ripetitivi.

## Test manuali e automatici {#manual-versus-automated-tests}

Tuttavia, automatizzare i test case è un investimento significativo, pertanto alcuni aspetti dovrebbero essere presi in considerazione:

* Richiedi tempo, fatica ed esperienza per la configurazione e la configurazione.
* Se basato sul browser, aumenta il rischio di problemi quando vengono installati gli aggiornamenti del browser; che richiedono ulteriore tempo per correggere.
* Solo progetti veramente realizzabili.
* È utile quando vengono generate più versioni per eseguire test o nel piano di rilascio a lungo termine.

## Verifica di aspetti specifici {#testing-specific-aspects}

Nel testare AEM alcuni dettagli specifici sono di particolare interesse:

**Ambienti di authoring e pubblicazione**

Tuttavia, sono coperti [Ambienti](/help/sites-developing/the-basics.md#environments) vale la pena evidenziare un fattore decisivo di AEM per quanto riguarda i test.

È necessario considerare AEM come due applicazioni:

* la *Autore* ambiente Questa istanza consente agli autori di inserire e pubblicare contenuti.
Questo dispone di un set di utenti piccolo (er) e prevedibile, per i quali funzionalità e prestazioni specifiche sono cruciali.

* la *Pubblica* ambiente Questa istanza presenta il sito web nel relativo modulo pubblicato per l’accesso dei visitatori.
Questo di solito ha un set più ampio di utenti, in cui il volume di traffico non è sempre prevedibile al 100%. Le prestazioni restano cruciali quando si risponde alle richieste. Occorre inoltre considerare la memorizzazione in cache e il bilanciamento del carico.

Anche se lo stesso software in quanto tale, essi:

* a scopi diversi
* hanno requisiti diversi in termini di funzionalità e prestazioni
* sono configurati in modo diverso
* sono sintonizzati separatamente
* avranno ciascuno una propria serie di prove di accettazione

In altre parole devono essere testati separatamente e con diversi casi di prova.

**Personalizzazione**

Quando verifichi la personalizzazione ogni singolo caso d’uso deve essere ripetuto utilizzando più account utente per dimostrare il comportamento.

È inoltre necessario controllare il comportamento corretto nella memorizzazione in cache.

**Dispatcher**

La maggior parte dei progetti installerà Dispatcher per la memorizzazione in cache e il bilanciamento del carico.

Il test è difficile (la memorizzazione in cache si verifica a vari livelli e in varie posizioni) e deve essere eseguita a livello di black-box. Gli aspetti chiave per i quali eseguire la prova sono:

* **Precisione**
assicurati che gli aggiornamenti dei contenuti siano visualizzati dal visitatore del sito web.

* **Continuità**
assicurati che il sito web sia ancora disponibile quando un server viene arrestato.

* **Cluster**
I cluster vengono utilizzati per fornire:

   * **Failover**
Se un server non riesce, gli altri server del cluster subiranno un&#39;elaborazione.

   * **Prestazioni**
Il bilanciamento del carico con failover completo aumenta le prestazioni di un cluster.
Se utilizzato per un progetto cliente, il cluster deve essere testato per confermare il corretto funzionamento della configurazione.

## Verifica di software di terze parti {#testing-third-party-software}

Qualsiasi software di terze parti interfacciato a AEM sarà menzionato nelle Specifiche dettagliate dei requisiti.

Eventuali prove richieste (in funzione della portata definita) devono essere analizzate e sottoposte a prova pulita.
