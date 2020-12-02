---
title: Architettura del software
seo-title: Architettura del software
description: Best practice per l'architettura del software
seo-description: Best practice per l'architettura del software
uuid: a557f6ca-c3f1-486e-a45e-6e1f986fab41
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 92971747-1c74-4917-b5a0-7b79b3ae1e68
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 0%

---


# Architettura software{#software-architecture}

## Progettazione per gli aggiornamenti {#design-for-upgrades}

Quando si estendono i comportamenti OOTB, è importante tenere a mente gli aggiornamenti. Applicate sempre le personalizzazioni nella directory /apps e sovrapponete ai nodi corrispondenti nella directory /libs oppure utilizzate sling:resourceSuperType per estendere il comportamento out-of-the-box. Anche se possono essere necessarie alcune modifiche per supportare una nuova versione AEM, la nuova versione non deve sovrascrivere le personalizzazioni se questa procedura viene seguita.

### Riutilizza modelli e componenti quando possibile {#reuse-template-and-components-when-possible}

In questo modo il sito potrà mantenere un aspetto e un aspetto più coerenti e semplificare la manutenzione del codice. Quando è necessario un nuovo modello, accertatevi di estenderlo da un modello di base condiviso in modo che i requisiti globali, come l&#39;inclusione clientlib, possano essere codificati in un&#39;unica posizione. Quando è necessario un nuovo componente, cercate le opportunità di estendere da un componente esistente.

### Progettazione di modelli {#design-template-designs}

Definendo quali componenti possono essere inclusi in ogni parsys della pagina, è possibile controllare l&#39;aspetto del sito. Limitando l&#39;accesso alla progettazione sulle pagine, è possibile consentire agli &quot;autori super&quot; di modificare i componenti consentiti per pagina senza l&#39;intervento dello sviluppatore, garantendo nel contempo che gli altri autori seguano gli standard aziendali.

### Sviluppare un&#39;architettura SOLID {#develop-a-solid-architecture}

SOLID è un acronimo che descrive cinque principi architettonici che devono essere rispettati:

* **Principio di responsabilità** unica: ogni modulo, classe, metodo, ecc. dovrebbe fare solo una cosa.
* **Principio** aperto/chiuso: i moduli devono essere aperti per l&#39;estensione e chiusi per la modifica.
* **Principio di** sostituzione di Liskov - i tipi dovrebbero essere sostituiti dai loro sottotipi.
* **Principio di segmentazione** dell&#39;interfaccia: nessun cliente deve essere costretto a dipendere da metodi che non utilizza.
* **Principio di** dipendenza: i moduli di alto livello non devono dipendere dai moduli di basso livello. Entrambi devono dipendere dalle astrazioni. Le astrazioni non devono dipendere dai dettagli. I dettagli devono dipendere dalle astrazioni.

Il rispetto di questi cinque principi dovrebbe tradursi in un sistema che preveda una netta separazione delle preoccupazioni.

### Segui il principio di robustezza {#follow-the-robustness-principle}

Il principio della solidità afferma che dovremmo essere conservatori in ciò che inviamo, ma essere liberali in ciò che accettiamo. In altre parole, quando inviamo messaggi a terzi, dovremmo essere completamente conformi alle specifiche, ma quando riceviamo messaggi da terzi, dovremmo accettare messaggi non conformi fintanto che il significato del messaggio è chiaro.

### Implementare i picchi nei propri moduli {#implement-spikes-in-their-own-modules}

Picchi e codice di test sono parte integrante di qualsiasi implementazione software Agile, ma vogliamo assicurarci che non entrino nella nostra base di codice di produzione senza il livello appropriato di sorveglianza. Di conseguenza, si consiglia di creare picchi nel proprio modulo.

### Implementare gli script di migrazione dei dati nel proprio modulo {#implement-data-migration-scripts-in-their-own-module}

Gli script di migrazione dei dati, mentre il codice di produzione, vengono in genere eseguiti una sola volta all&#39;avvio iniziale di un sito. Pertanto, non appena il sito è attivo, questo diventa codice morto. Per evitare che venga creato codice di implementazione che dipende dagli script di migrazione, questi devono essere implementati nel proprio modulo. Questo ci permette anche di rimuovere e ritirare questo codice subito dopo il lancio, eliminando il codice morto dal sistema.

### Seguite le convenzioni pubblicate in formato Maven nei file POM {#follow-published-maven-conventions-in-pom-files}

Apache ha pubblicato le convenzioni di stile in [https://maven.apache.org/developers/conventions/code.html](https://maven.apache.org/developers/conventions/code.html). E&#39; meglio seguire queste convenzioni, in quanto renderà più facile reperire rapidamente nuove risorse.
