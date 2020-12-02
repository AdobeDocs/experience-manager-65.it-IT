---
title: Definizione dei casi di test
seo-title: Definizione dei casi di test
description: I casi di test devono essere basati sui casi di utilizzo e sulle specifiche dettagliate dei requisiti
seo-description: I casi di test devono essere basati sui casi di utilizzo e sulle specifiche dettagliate dei requisiti
uuid: daaa5370-bcd3-45a6-9974-f9b5af6a1529
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: f01eb2aa-6891-4f5d-8a4a-43fc1534c222
docset: aem65
translation-type: tm+mt
source-git-commit: da08613be784f43ad3e3c3652b7e015640a48a9d
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---


# Definizione dei casi di test{#defining-your-test-cases}

I casi di test devono essere basati su:

**Casi di utilizzo**

* Questi definiscono la funzionalità necessaria in termini di interazione tra gli attori (ruoli che avviano determinate azioni) e il sistema.
* I Casi di utilizzo devono essere definiti dal cliente.

**Specifiche dettagliate**

* Tutti i requisiti funzionali e di prestazioni devono essere sottoposti a test.

Le prove devono definire chiaramente:

* Prerequisiti; questi possono riguardare sistemi, configurazioni o esperienza tester specifici.
* Le misure da seguire; ad un livello di dettaglio adeguato.
* Risultati previsti.
* Cancella criteri per superato o non superato.

La prospettiva di automatizzare i test case è ovviamente attraente in quanto può eliminare le attività ripetitive.

## Test manuali e automatizzati {#manual-versus-automated-tests}

Tuttavia, l&#39;automazione dei test case è un investimento significativo, pertanto occorre considerare alcuni aspetti:

* Richiedi tempo, fatica ed esperienza per la configurazione.
* Se basato su browser, esiste un rischio maggiore di problemi quando vengono installati gli aggiornamenti del browser; che richiedono ulteriore tempo per la correzione.
* Solo realizzabili per grandi progetti.
* Ideale quando vengono generate più versioni per il test o nel piano di rilascio a lungo termine.

## Verifica degli aspetti specifici {#testing-specific-aspects}

Durante il test AEM alcuni dettagli specifici sono di particolare interesse:

**Ambienti di authoring e pubblicazione**

Anche se, coperto in [Ambienti](/help/sites-developing/the-basics.md#environments) è utile evidenziare un fattore determinante di AEM per quanto riguarda il test.

È necessario considerare AEM come due applicazioni:

* ambiente *Author*
Questa istanza consente agli autori di inserire e pubblicare contenuti.
Questo dispone di un set di utenti piccolo (e) e prevedibile, per i quali funzionalità e prestazioni specifiche sono fondamentali.

* ambiente *Publish*
Questa istanza presenta il sito Web nel modulo pubblicato per l’accesso dei visitatori.
In genere questo tipo di utenti è composto da un numero maggiore, dove il volume di traffico non è sempre prevedibile al 100%. Le prestazioni sono ancora cruciali, quando si risponde alle richieste. Occorre inoltre considerare la memorizzazione nella cache e il bilanciamento del carico.

Anche se lo stesso software in quanto tale, essi:

* servire scopi diversi
* avere requisiti diversi in termini di funzionalità e prestazioni
* sono configurate in modo diverso
* sono sintonizzati separatamente
* avranno ciascuno una propria serie di prove di accettazione

In altre parole devono essere testati separatamente e con diversi casi di prova.

**Personalizzazione**

Quando si esegue il test della personalizzazione, ogni singolo caso di utilizzo deve essere ripetuto utilizzando più account utente per dimostrare il comportamento.

È inoltre necessario verificare che la memorizzazione nella cache sia corretta.

**Il dispatcher**

La maggior parte dei progetti installerà il dispatcher per il caching e il bilanciamento del carico.

Il test è difficile (il caching si verifica a vari livelli e in diverse posizioni) e deve essere eseguito a livello di scatola nera. Gli aspetti chiave per i quali eseguire la prova sono:

* **Accertatevi**
con precisione che gli aggiornamenti di contenuto siano visibili al visitatore del sito Web.

* ****
Continuità, assicurarsi che il sito Web sia ancora disponibile quando un server viene spento.

* **I**
cluster sono utilizzati per fornire:

   * ****
Failover: se un server non riesce, gli altri server del cluster subiranno l&#39;elaborazione.

   * **Il bilanciamento**
PerformanceLoad con failover completo aumenta le prestazioni di un cluster.
Se utilizzato per un progetto cliente, il cluster deve essere testato per confermare il corretto funzionamento della configurazione.

## Verifica del software di terze parti {#testing-third-party-software}

Qualsiasi software di terze parti interfacciato a AEM verrà fatto riferimento nelle Specifiche dettagliate dei requisiti.

Eventuali prove richieste (in funzione dell&#39;ambito di applicazione definito) devono essere analizzate e si deve ottenere una prova pulita.
