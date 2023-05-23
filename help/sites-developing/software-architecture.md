---
title: Architettura software
seo-title: Software Architecture
description: Best practice per l’architettura del software
seo-description: Best practices for architecting your software
uuid: a557f6ca-c3f1-486e-a45e-6e1f986fab41
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 92971747-1c74-4917-b5a0-7b79b3ae1e68
exl-id: cd4f3b4c-5488-4ca7-9c1e-b4c819fda8e8
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 0%

---

# Architettura software{#software-architecture}

## Progettazione per aggiornamenti {#design-for-upgrades}

Quando si estendono i comportamenti OOTB, è importante tenere a mente gli aggiornamenti. Applica sempre le personalizzazioni nella directory /apps e sovrapponi sopra i nodi corrispondenti nella directory /libs oppure utilizza sling:resourceSuperType per estendere il comportamento predefinito. Anche se potrebbero essere necessarie alcune modifiche per supportare una nuova versione dell’AEM, la nuova versione non deve sovrascrivere le personalizzazioni se si segue questa procedura.

### Riutilizzare modelli e componenti quando possibile {#reuse-template-and-components-when-possible}

In questo modo il sito potrà mantenere un aspetto e un comportamento più coerenti e semplificare la manutenzione del codice. Quando è necessario un nuovo modello, assicurati di estendere da un modello di base condiviso in modo che i requisiti globali come l’inclusione della clientlib possano essere codificati in un’unica posizione. Quando è necessario un nuovo componente, cerca opportunità da estendere da un componente esistente.

### Progettare progettazioni di modelli {#design-template-designs}

Definendo quali componenti possono essere inclusi in ciascun parsys sulla pagina, è possibile controllare la coerenza dell’aspetto del sito. Limitando l’accesso alla progettazione nelle pagine, i &quot;super autori&quot; possono essere autorizzati a modificare i componenti consentiti per pagina senza l’intervento degli sviluppatori, garantendo al contempo che gli altri autori seguano gli standard aziendali.

### Sviluppare un’architettura solida {#develop-a-solid-architecture}

SOLID è un acronimo che descrive cinque principi architettonici che devono essere rispettati:

* **S** Principio di responsabilità unico: ogni modulo, classe, metodo ecc. dovrebbe avere una sola responsabilità.
* **O** Penna/Principio chiuso: i moduli devono essere aperti per l’estensione e chiusi per la modifica.
* **L** Principio di sostituzione iskov: i tipi devono essere sostituibili dai relativi sottotipi.
* **I** Principio di segregazione dell’interfaccia: nessun client deve essere costretto a dipendere da metodi che non utilizza.
* **D** Principio di inversione della dipendenza: i moduli di alto livello non devono dipendere da moduli di basso livello. Entrambi dovrebbero dipendere dalle astrazioni. Le astrazioni non devono dipendere dai dettagli. I dettagli devono dipendere dalle astrazioni.

Il rispetto di questi cinque principi dovrebbe tradursi in un sistema rigorosamente distinto.

>[!TIP]
>
>SOLID è un concetto comunemente utilizzato nella programmazione orientata agli oggetti e ogni elemento è ampiamente discusso nella letteratura di settore.
>
>Questo è solo un breve riepilogo presentato per la consapevolezza e si è incoraggiati a familiarizzare con questi concetti in modo più approfondito.

### Seguire il principio di robustezza {#follow-the-robustness-principle}

Il principio di robustezza afferma che dovremmo essere conservatori in ciò che inviamo, ma essere liberali in ciò che accettiamo. In altre parole, quando si inviano messaggi a terzi, è necessario attenersi completamente alle specifiche, ma quando si ricevono messaggi da terze parti, è necessario accettare messaggi non conformi purché il significato del messaggio sia chiaro.

### Implementare i picchi nei propri moduli {#implement-spikes-in-their-own-modules}

Picchi e codice di test sono parte integrante di qualsiasi implementazione del software Agile, ma vogliamo essere sicuri che non vengano inseriti nella nostra base di codice di produzione senza il livello appropriato di supervisione. Di conseguenza, si consiglia di creare picchi nel proprio modulo.

### Implementare gli script di migrazione dei dati nel proprio modulo {#implement-data-migration-scripts-in-their-own-module}

Gli script di migrazione dei dati, mentre il codice di produzione, in genere vengono eseguiti una sola volta all’avvio iniziale di un sito. Pertanto, non appena il sito è attivo, questo diventa un codice morto. Per evitare di generare codice di implementazione che dipende dagli script di migrazione, è necessario implementarli nel loro modulo. Questo ci permette anche di rimuovere e ritirare questo codice immediatamente dopo il lancio, eliminando il codice morto dal sistema.

### Segui le convenzioni Maven pubblicate nei file POM {#follow-published-maven-conventions-in-pom-files}

Apache ha pubblicato convenzioni di stile in [https://maven.apache.org/developers/conventions/code.html](https://maven.apache.org/developers/conventions/code.html). È meglio seguire queste convenzioni, in quanto renderà più facile per le nuove risorse venire rapidamente a conoscenza.
