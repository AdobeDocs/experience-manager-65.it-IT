---
title: Architettura del software
seo-title: Architettura del software
description: Best practice per l’architettura del software
seo-description: Best practice per l’architettura del software
uuid: a557f6ca-c3f1-486e-a45e-6e1f986fab41
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 92971747-1c74-4917-b5a0-7b79b3ae1e68
exl-id: cd4f3b4c-5488-4ca7-9c1e-b4c819fda8e8
translation-type: tm+mt
source-git-commit: 423e17dadf2e506eb68b37851dde5e68ed950866
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 0%

---

# Architettura del software{#software-architecture}

## Progettazione di aggiornamenti {#design-for-upgrades}

Quando estendi i comportamenti OOTB, è importante tenere a mente gli aggiornamenti. Applica sempre le personalizzazioni nella directory /apps e sovrapponi sui nodi corrispondenti nella directory /libs oppure utilizza sling:resourceSuperType per estendere il comportamento predefinito. Sebbene possano essere necessarie alcune modifiche per supportare una nuova versione di AEM, la nuova versione non deve sovrascrivere le personalizzazioni, se seguita questa procedura.

### Riutilizzare modelli e componenti quando possibile {#reuse-template-and-components-when-possible}

In questo modo il sito potrà mantenere un aspetto più coerente e semplificare la manutenzione del codice. Quando è necessario un nuovo modello, assicurati di estenderlo da un modello di base condiviso in modo che i requisiti globali come l’inclusione clientlib possano essere codificati in un’unica posizione. Quando è necessario un nuovo componente, cerca le opportunità per estenderlo da un componente esistente.

### Progettazioni dei modelli di progettazione {#design-template-designs}

Definendo quali componenti possono essere inclusi in ogni parsys della pagina, è possibile controllare la coerenza dell’aspetto del sito. Limitando l’accesso alla progettazione sulle pagine, è possibile consentire agli &quot;autori avanzati&quot; di modificare i componenti consentiti per pagina senza l’intervento degli sviluppatori, garantendo al contempo che gli altri autori seguano gli standard aziendali.

### Sviluppare un&#39;architettura SOLID {#develop-a-solid-architecture}

SOLID è un acronimo che descrive cinque principi architettonici cui attenersi:

* **** Principio di responsabilità singola: ogni modulo, classe, metodo, ecc. deve avere una sola responsabilità.
* **** Principio aperto/chiuso: i moduli devono essere aperti per l’estensione e chiusi per la modifica.
* **** Principio di sostituzione di Liskov - i tipi dovrebbero essere sostituibili dai loro sottotipi.
* **** Principio di segmentazione dell’interfaccia - nessun client deve essere obbligato a dipendere da metodi che non utilizza.
* **** Principio di inversione della dipendenza: i moduli di alto livello non devono dipendere da moduli di basso livello. Entrambi devono dipendere dalle astrazioni. Le astrazioni non devono dipendere dai dettagli. I dettagli devono dipendere dalle astrazioni.

Il rispetto di questi cinque principi dovrebbe tradursi in un sistema che garantisca una rigorosa separazione delle preoccupazioni.

>[!TIP]
>
>SOLID è un concetto comunemente utilizzato nella programmazione orientata agli oggetti e ogni elemento è ampiamente discusso nella letteratura industriale.
>
>Questo è solo un breve riassunto presentato per la consapevolezza e siete incoraggiati a familiarizzare con questi concetti in modo più approfondito.

### Segui il principio di robustezza {#follow-the-robustness-principle}

Il principio della robustezza afferma che dovremmo essere conservatori in ciò che inviamo, ma essere liberali in ciò che accettiamo. In altre parole, quando inviamo messaggi a terzi, dovremmo conformarci completamente alle specifiche, ma quando riceviamo messaggi da terzi, dovremmo accettare messaggi non conformi purché il significato del messaggio sia chiaro.

### Implementare picchi nei propri moduli {#implement-spikes-in-their-own-modules}

Picchi e codice di test sono parte integrante di qualsiasi implementazione del software Agile, ma vogliamo assicurarci che non entrino nella nostra base di codice di produzione senza il livello di supervisione appropriato. Di conseguenza, si consiglia di creare picchi nel proprio modulo.

### Implementare gli script di migrazione dei dati nel proprio modulo {#implement-data-migration-scripts-in-their-own-module}

Gli script di migrazione dei dati, mentre il codice di produzione, vengono in genere eseguiti una sola volta all’avvio iniziale di un sito. Pertanto, non appena il sito è attivo, questo diventa codice morto. Per evitare di generare codice di implementazione che dipende dagli script di migrazione, è necessario implementarli nel proprio modulo. Questo ci permette anche di rimuovere e ritirare questo codice subito dopo il lancio, eliminando il codice morto dal sistema.

### Segui le convenzioni Maven pubblicate nei file POM {#follow-published-maven-conventions-in-pom-files}

Apache ha pubblicato le convenzioni di stile in [https://maven.apache.org/developers/conventions/code.html](https://maven.apache.org/developers/conventions/code.html). È meglio seguire queste convenzioni, in quanto renderà più semplice l&#39;introduzione rapida di nuove risorse.
