---
title: Architettura software
description: Scopri alcune best practice per l’architettura del software per Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: cd4f3b4c-5488-4ca7-9c1e-b4c819fda8e8
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: a28883778c5e8fb90cbbd0291ded17059ab2ba7e
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 0%

---

# Architettura software{#software-architecture}

## Progettazione per aggiornamenti {#design-for-upgrades}

Quando si estendono comportamenti preconfigurati, è importante tenere presente gli aggiornamenti. Applica sempre le personalizzazioni nella directory /apps e sovrapponi sopra i nodi corrispondenti nella directory /libs oppure utilizza sling:resourceSuperType per estendere il comportamento predefinito. Anche se potrebbero essere necessarie alcune modifiche per supportare una nuova versione dell’AEM, la nuova versione non deve sovrascrivere le personalizzazioni se si segue questa pratica.

### Riutilizzare modelli e componenti quando possibile {#reuse-template-and-components-when-possible}

In questo modo il sito potrà mantenere un aspetto e un’atmosfera più coerenti e semplificare la manutenzione del codice. Quando è necessario un nuovo modello, assicurati di estendere da un modello di base condiviso in modo che i requisiti globali come l’inclusione della clientlib possano essere codificati in un’unica posizione. Quando è necessario un nuovo componente, cerca opportunità da estendere da un componente esistente.

### Progettare progettazioni di modelli {#design-template-designs}

Definendo quali componenti possono essere inclusi in ciascun parsys sulla pagina, è possibile controllare la coerenza dell’aspetto del sito. Limitando l’accesso alla progettazione nelle pagine, i &quot;super autori&quot; possono essere autorizzati a modificare i componenti consentiti per pagina senza l’intervento degli sviluppatori, garantendo al contempo che gli altri autori seguano gli standard aziendali.

### Sviluppare un’architettura solida {#develop-a-solid-architecture}

SOLID è un acronimo che descrive cinque principi architettonici che devono essere rispettati:

* **S** Principio di responsabilità unico: ogni modulo, classe, metodo e così via dovrebbe avere una sola responsabilità.
* **O** Penna/Principio chiuso: i moduli devono essere aperti per l’estensione e chiusi per la modifica.
* **L** Principio di sostituzione iskov: i tipi devono essere sostituibili dai relativi sottotipi.
* **I** Principio di segregazione dell’interfaccia: nessun client deve essere costretto a dipendere da metodi che non utilizza.
* **D** Principio di inversione della dipendenza: i moduli di alto livello non devono dipendere da moduli di basso livello. Entrambi dovrebbero dipendere dalle astrazioni. Le astrazioni non devono dipendere dai dettagli. I dettagli devono dipendere dalle astrazioni.

Il rispetto di questi cinque principi dovrebbe tradursi in un sistema rigorosamente distinto.

>[!TIP]
>
>SOLID è un concetto comunemente utilizzato nella programmazione orientata agli oggetti e ogni elemento è ampiamente discusso nella letteratura di settore.
>
>Queste informazioni sono solo un breve riepilogo presentato per la consapevolezza e si è incoraggiati a familiarizzare con questi concetti in modo più approfondito.

### Seguire il principio di robustezza {#follow-the-robustness-principle}

Il principio di robustezza afferma che si dovrebbe essere conservatori in ciò che si invia, ma essere liberali in ciò che si accetta. In altre parole, quando invii messaggi a terzi, devi conformarsi completamente alle specifiche. Tuttavia, quando ricevi messaggi da una terza parte, devi accettare messaggi non conformi purché il significato del messaggio sia chiaro.

### Implementare i picchi nei propri moduli {#implement-spikes-in-their-own-modules}

Picchi e codice di test fanno parte di qualsiasi implementazione del software Agile. Tuttavia, è importante assicurarsi che non vengano incluse nella base di codice di produzione senza il livello di supervisione appropriato. Di conseguenza, si consiglia di creare i picchi nel proprio modulo.

### Implementare gli script di migrazione dei dati nel proprio modulo {#implement-data-migration-scripts-in-their-own-module}

Gli script di migrazione dei dati, mentre il codice di produzione, vengono eseguiti una sola volta all’avvio iniziale di un sito. Pertanto, quando il sito è attivo, gli script diventano codice morto. Per evitare di generare codice di implementazione che dipende dagli script di migrazione, questi devono essere implementati nel loro modulo. In questo modo possiamo rimuovere e ritirare questo codice immediatamente dopo il lancio, eliminando il codice morto dal sistema.

### Segui le convenzioni Maven pubblicate nei file POM {#follow-published-maven-conventions-in-pom-files}

Apache ha pubblicato convenzioni di stile in [https://maven.apache.org/developers/conventions/code.html](https://maven.apache.org/developers/conventions/code.html). È meglio seguire queste convenzioni perché consente di velocizzare l&#39;emergere di nuove risorse.
