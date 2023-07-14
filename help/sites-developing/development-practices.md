---
title: Procedure di sviluppo
description: Best practice per lo sviluppo su Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 65b2029e-03c9-4df4-8579-2b15dbee1035
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 0%

---

# Procedure di sviluppo{#development-practices}

## Lavora secondo una definizione di Fine (DoD) {#work-according-to-a-definition-of-done}

Ogni team ha una definizione diversa di cosa significa &quot;fatto&quot;, ma è importante averne una e assicurarsi che una storia soddisfi i criteri definiti prima di essere accettata.

Alcuni criteri comunemente specificati dai team includono:

* Codice rivisto per la formattazione
* Commenti/Javadoc aggiunti
* Soddisfa i livelli di copertura dei test richiesti
* Supera unit test e integration test
* Convalidato nell’ambiente di controllo qualità
* Localizzazione implementata

Senza un DoD ben definito, è facile trovarsi in una situazione in cui molte cose sono fatte a metà e nulla è veramente completo.

### Definire e rispettare le convenzioni di codifica e formattazione {#define-and-adhere-to-coding-and-formatting-conventions}

Cose come i livelli di rientro e lo spazio vuoto possono non sembrare importanti, ma avere un codice formattato correttamente va molto avanti verso la leggibilità e la manutenibilità. Le convenzioni dovrebbero essere discusse e concordate in team e poi seguite nel codice.

### Obiettivo per un’elevata copertura dei test  {#aim-for-high-test-coverage}

Le dimensioni dell’implementazione di un progetto aumentano, così come il tempo necessario per testarla. Senza una buona copertura dei test, il team di test non può scalare e gli sviluppatori alla fine vengono sepolti nei bug.

Gli sviluppatori devono provare lo sviluppo basato su test (TDD, Test Driven Development), scrivendo test di unità non riusciti prima del codice di produzione che soddisfa i loro requisiti. Il controllo qualità dovrebbe creare una serie automatizzata di test di accettazione per garantire che il sistema funzioni come previsto da un livello elevato.

Sono disponibili framework personalizzati, come Jackalope e Prosper, per semplificare l’ironia sulle API JCR al fine di garantire la produttività degli sviluppatori durante la scrittura di unit test.

### Resta pronto per la demo {#stay-demo-ready}

Il sistema deve essere disponibile per la dimostrazione all’azienda alla fine di ogni iterazione. Mantenendo il sistema in stato demo-ready, il team sarà sempre all&#39;interno di un&#39;iterazione di essere pronto per la produzione e il debito tecnico può essere mantenuto a un livello manutenibile.

### Implementare un ambiente di integrazione continua e utilizzarlo {#implement-a-continuous-integration-environment-and-use-it}

L’implementazione di un ambiente di integrazione continua consente di eseguire in modo semplice e ripetuto unit test e integration test. Separa inoltre le distribuzioni dal team di sviluppo, consentendo alle altre parti del team di essere più efficienti e di effettuare distribuzioni più stabili e prevedibili.

### Mantieni il ciclo di sviluppo veloce mantenendo i tempi di build bassi {#keep-the-development-cycle-fast-by-keeping-build-times-low}

Se l’esecuzione degli unit test richiede molto tempo, gli sviluppatori eviteranno di eseguirli e perderanno il loro valore. Se la generazione e la distribuzione del codice richiedono molto tempo, le persone lo faranno meno spesso. La priorità è data ai tempi di realizzazione brevi, per garantire che il tempo investito nella copertura dei test e nell’infrastruttura CI continui a rendere il team più produttivo.

### Ottimizza Sonar e altri strumenti di analisi del codice statico e agisci in base ai loro rapporti {#fine-tune-sonar-and-other-static-code-analysis-tools-and-act-on-their-reports}

Gli strumenti di analisi del codice possono essere utili, ma solo se i loro rapporti portano ad azioni da parte del team di sviluppo. Senza ottimizzare l’analisi fornita da questi strumenti, i consigli che generano diventano irrilevanti e perdono valore.

### Segui la regola di Scout per ragazzi {#follow-the-boy-scout-rule}

Gli Scout di ragazzi hanno una regola: &quot;Lascialo meglio di come l&#39;hai trovato.&quot; Se tutti i membri del team di sviluppo si attengono a questa regola e fanno pulizia quando si imbattono in un casino, il codice migliorerà costantemente.

### Evita di implementare le funzioni YAGNI {#avoid-implementing-yagni-features}

Le funzionalità YAGNI (You Aren Gonna Need It) sono implementate quando ci aspettiamo che avremo bisogno di qualcosa in futuro, anche se non ne abbiamo bisogno ora. Idealmente, dovremmo implementare la cosa più semplice che funzionerà oggi e utilizzare il refactoring continuo per garantire che l&#39;architettura del sistema evolva con i requisiti nel tempo. Questo ci permette di concentrarci su ciò che conta e prevenire l’eccesso di codice e il creep delle funzioni.
