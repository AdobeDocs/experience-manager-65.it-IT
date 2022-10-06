---
title: Scopri lo sviluppo di CMS Headless
description: In questa parte del Percorso AEM Headless Developer, scopri la tecnologia headless e perché utilizzarla.
exl-id: f0989cea-3102-43cd-976e-9a6b265d9c15
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1595'
ht-degree: 1%

---

# Scopri lo sviluppo di CMS Headless {#learn-about}

In questa parte del [AEM Percorso di sviluppo headless,](overview.md) scopri la tecnologia headless e perché usarla.

## Obiettivo {#objective}

Questo documento è utile per comprendere la distribuzione dei contenuti headless e perché deve essere utilizzato. Dopo la lettura dovresti:

* Comprendere i concetti e la terminologia di base per la distribuzione di contenuti headless
* Capire perché e quando è richiesto un headless
* Conoscere ad alto livello come vengono utilizzati i concetti senza testa e come si relazionano

## Distribuzione completa dei contenuti {#full-stack}

Sin dall&#39;introduzione dei sistemi di gestione dei contenuti (CMS), facili da usare e su larga scala, le aziende li hanno sfruttati come posizione centrale per gestire messaggi, branding e comunicazioni. Utilizzando il CMS come punto centrale per l&#39;amministrazione delle esperienze, è possibile migliorare l&#39;efficienza eliminando la necessità di duplicare attività in sistemi diversi.

![Il classico CMS full-stack](assets/full-stack.png)

In un CMS completo, tutte le funzionalità per la manipolazione del contenuto si trovano nel CMS. Le caratteristiche del sistema compongono diversi componenti dello stack CMS. La soluzione completa offre molti vantaggi.

* Hai un sistema da mantenere.
* I contenuti vengono gestiti a livello centrale.
* Tutti i servizi del sistema sono integrati.
* L’authoring dei contenuti è semplice.

Quindi, se desideri aggiungere un nuovo canale o supportare nuovi tipi di esperienze, puoi inserire uno (o più) nuovi componenti nella pila e disporre di una sola posizione per apportare le modifiche.

![Aggiunta di un nuovo canale alla pila](assets/adding-channel.png)

La complessità delle dipendenze all’interno dello stack diventa rapidamente evidente, in quanto è possibile che altri elementi dello stack debbano essere regolati per adattarsi alle modifiche.

## Limiti di consegna full-stack {#limits}

L’approccio completo dello stack crea intrinsecamente un silo in cui tutte le esperienze arrivano in un unico sistema. Le modifiche o le aggiunte a un componente del silo richiedono modifiche ad altri componenti che possono rendere le modifiche ad alta intensità di tempo e costose.

Ciò vale in particolare per il sistema di presentazione, che nelle configurazioni tradizionali è spesso strettamente legato al CMS. Per ogni nuovo canale si intende generalmente un aggiornamento del sistema di presentazione, che può interessare tutti gli altri canali.

![La complessità cresce man mano che i canali vengono aggiunti a uno stack](assets/presentation-complexity.png)

I limiti di questo silo naturale possono diventare evidenti, in quanto si spinge più per coordinare le modifiche tra tutti i componenti dello stack.

Gli utenti si aspettano un coinvolgimento indipendentemente dalla piattaforma o dal punto di contatto, il che richiede flessibilità nella distribuzione delle esperienze.  Questo approccio multicanale è lo standard delle esperienze digitali e in determinate circostanze un approccio completo può rivelarsi inflessibile.

## Testa senza testa {#the-head}

La testa di qualsiasi sistema è generalmente il renderer di output di quel sistema, tipicamente sotto forma di un&#39;interfaccia grafica o di un&#39;altra uscita grafica.

Un server headless, ad esempio, è probabilmente seduto in un rack in una stanza server da qualche parte e non ha monitor collegato. Per accedervi è necessario connettersi in remoto. In questo caso, il monitor è la testina perché si occupa del rendering dell&#39;output del server. In qualità di consumatore del servizio, fornisci la tua testa (il monitor) quando ci si connette da remoto.

Quando parliamo di un CMS headless, il CMS gestisce i contenuti e continua a consegnarli ai consumatori. Tuttavia, consegnando solo il **content** in modo standardizzato, un CMS headless omette il rendering finale dell&#39;output, lasciando **presentazione** del contenuto al servizio che consuma.

![CMS headless](assets/headless-cms.png)

I servizi che consumano, siano essi esperienze AR, un webshop, esperienze mobili, app web progressive (PWA), ecc, prendono i contenuti dal CMS headless e forniscono il loro rendering. Si prendono cura di fornire le proprie teste per i contenuti.

Omettendo la testa si semplifica il CMS rimuovendo la complessità. In questo modo si sposta anche la responsabilità di rendere i contenuti ai servizi che ne hanno effettivamente bisogno e che sono spesso più adatti a tale rendering.

## Disaccoppiamento {#decoupling}

La distribuzione headless è possibile esponendo un set di API affidabili e flessibili in cui è possibile sfruttare tutte le esperienze. L’API funge da linguaggio comune tra i servizi e li associa a livello di contenuto tramite la distribuzione standardizzata dei contenuti, ma offre la flessibilità necessaria per implementare le proprie soluzioni.

Headless è un esempio di scollamento del contenuto dalla presentazione. O in senso più generico, disaccoppiando il front end dal back end della pila di servizi. In una configurazione senza testa, il sistema di presentazione (la testa) viene scollegato dalla gestione dei contenuti (la coda). I due interagiscono solo tramite chiamate API.

Questo disaccoppiamento consente a ogni servizio che consuma (front-end) di creare la propria esperienza in base allo stesso contenuto distribuito tramite le API, garantendo il riutilizzo e la coerenza dei contenuti. I servizi di consumo possono quindi implementare i propri sistemi di presentazione, consentendo la scalabilità orizzontale dello stack di gestione dei contenuti (back-end).

## Sostanze tecnologiche {#technology}

Un approccio headless consente di creare uno stack tecnologico in grado di adattarsi rapidamente e facilmente alle esigenze future di esperienza digitale.

In passato, le API per CMS erano solitamente basate su REST. Il trasferimento di stato di rappresentanza (REST) fornisce risorse come testo in modo senza stato. Questo consente di leggere e modificare le risorse con un set di operazioni predefinito. REST ha consentito una grande interoperabilità tra i servizi sul web garantendo una rappresentazione senza stato del contenuto.

È ancora necessario disporre di API REST affidabili. Tuttavia le richieste REST possono essere grandi e complesse. Se hai più consumatori che fanno chiamate REST per tutti i tuoi canali, questo composti di verbosità e le prestazioni possono essere influenzate.

La distribuzione di contenuti headless utilizza spesso le API GraphQL. GraphQL consente un trasferimento senza stato simile, ma consente query più mirate, riducendo il numero totale di query necessarie e migliorando le prestazioni. È comune vedere le soluzioni utilizzare un mix di REST e GraphQL, essenzialmente scegliendo lo strumento migliore per il lavoro in corso.

Qualunque sia la tua API scelta, definendo un sistema headless basato su API comuni, puoi sfruttare il browser più recente e altre tecnologie web come le app web progressive (PWA). Le API creano un&#39;interfaccia standard facilmente estensibile e adattabile.

In genere, il rendering del contenuto viene eseguito sul lato client. In genere, significa che qualcuno effettua una chiamata al contenuto su un dispositivo mobile, che il CMS consegna il contenuto e che quindi il dispositivo mobile (il client) è responsabile del rendering del contenuto servito. Se il dispositivo è vecchio o altrimenti lento, anche l&#39;esperienza digitale è lenta.

La possibilità di scollegare i contenuti dalla presentazione consente di avere un maggiore controllo su tali problemi di prestazioni lato client. Il rendering lato server (SSR) trasferisce la responsabilità del rendering del contenuto dal browser del client al server. In questo modo, in qualità di fornitore del contenuto, puoi offrire al pubblico un livello di prestazioni garantito, se necessario.

## Sfide organizzative {#organization}

Headless apre un mondo di flessibilità per la distribuzione delle esperienze digitali. Ma questa flessibilità può anche presentare la propria sfida.

Avere molti canali diversi può significare che ciascuno di essi dispone di propri sistemi di presentazione. Anche se tutti utilizzano lo stesso contenuto tramite le stesse API, l’esperienza può essere diversa a causa delle diverse presentazioni. Occorre prestare attenzione e preoccupazione per garantire la coerenza dell&#39;esperienza del cliente.

Implementando sistemi di progettazione attenti, condividendo librerie di pattern e sfruttando componenti di progettazione riutilizzabili e framework lato client aperti consolidati, è possibile garantire esperienze coerenti, ma questo deve essere pianificato.

## Il futuro è senza testa e il futuro è adesso {#future}

Le esperienze digitali continueranno a definire il modo in cui i brand interagiscono con i clienti. La novità del design headless è la flessibilità che ci offre per rispondere alle aspettative dei clienti in continua evoluzione.

È impossibile prevedere il futuro, ma senza testa vi dà l&#39;agilità di reagire a qualsiasi cosa il futuro porti.

## AEM e senza testa {#aem-and-headless}

Continuando a utilizzare questo percorso di sviluppatori, scoprirai come AEM supporta la consegna headless lungo le sue funzionalità di consegna full-stack.

In qualità di leader di settore nella gestione dell&#39;esperienza digitale, Adobe si rende conto che la soluzione ideale per le sfide del mondo reale che i creatori di esperienze affrontano raramente è una scelta binaria. Questo è il motivo per cui AEM non solo supporta entrambi i modelli, ma consente anche unicamente la combinazione ibrida senza soluzione di continuità dei due, combinando i vantaggi di uno stack headless e completo, per aiutarti a servire al meglio i consumatori dei contenuti, ovunque si trovino.

Questo percorso si concentra sul modello di distribuzione dei contenuti headless. Tuttavia, una volta che si dispone di questa conoscenza fondamentale, è possibile esplorare ulteriormente come sfruttare il potere di entrambi i modelli.

## Novità {#what-is-next}

Grazie per aver iniziato sul tuo percorso AEM senza testa! Dopo aver letto questo documento, devi:

* Comprendi i concetti e la terminologia di base per la distribuzione di contenuti headless.
* Capire perché e quando è richiesto il headless.
* Scopri ad alto livello come vengono utilizzati i concetti senza testa e come si relazionano.

Sviluppa questa conoscenza e continua il tuo percorso AEM headless rivedendo il documento successivo [Guida introduttiva di AEM Headless](getting-started.md) dove verrà illustrato come impostare gli strumenti necessari e come iniziare a pensare a come AEM la distribuzione di contenuti headless e ai relativi prerequisiti.

## Risorse aggiuntive {#additional-resources}

Mentre è consigliabile passare alla parte successiva del percorso di sviluppo headless rivedendo il documento [Guida introduttiva di AEM Headless](getting-started.md)Di seguito sono riportate alcune risorse aggiuntive facoltative che consentono di approfondire alcuni concetti menzionati in questo documento, ma non è necessario che continuino nel percorso headless.

* [AEM Tutorials headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=it) - Segui questi tutorial pratici per scoprire come utilizzare le varie opzioni per distribuire contenuti agli endpoint headless con AEM e scegliere quello che fa per te.
