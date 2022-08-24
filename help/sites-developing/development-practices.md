---
title: Pratiche di sviluppo
seo-title: Development Practices
description: Best practice per lo sviluppo di AEM
seo-description: Best practices for developing on AEM
uuid: 27a75f7f-6e2c-4113-9e9f-c5013a4594c2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8b0297a1-d922-410f-9aaf-3a6b87e11dc0
exl-id: 65b2029e-03c9-4df4-8579-2b15dbee1035
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 0%

---

# Pratiche di sviluppo{#development-practices}

## Lavorare secondo una definizione di fine {#work-according-to-a-definition-of-done}

Ogni team ha una definizione diversa di ciò che &quot;fatto&quot; significa, ma è importante averne uno e assicurarsi che una storia soddisfi i criteri definiti prima di essere accettata.

Alcuni criteri comunemente specificati dai team includono:

* Codice rivisto per la formattazione
* Commenti/Javadoc aggiunto
* Soddisfa i livelli di copertura dei test richiesti
* Supera i test di unità e integrazione
* Convalida nell’ambiente QA
* Localizzazione implementata

Senza un DoD ben definito, è facile finire in una situazione in cui molte cose sono a metà strada e niente è veramente completo.

### Definire e rispettare le convenzioni di codifica e formattazione {#define-and-adhere-to-coding-and-formatting-conventions}

Cose come i livelli di rientro e lo spazio vuoto possono non sembrare importanti, ma avere un codice formattato correttamente fa un lungo cammino verso la leggibilità e la manutenzione. Le convenzioni dovrebbero essere discusse e concordate come squadra e seguite nel codice.

### Obiettivo della copertura di prova elevata  {#aim-for-high-test-coverage}

Man mano che le dimensioni dell’implementazione di un progetto aumentano, aumenta anche il tempo necessario per testarla. Senza una buona copertura dei test, il team di test non sarà in grado di scalare e gli sviluppatori alla fine saranno sepolti in bug.

Gli sviluppatori devono eseguire il TDD scrivendo test di unità non riusciti prima del codice di produzione che soddisfi i loro requisiti. Il controllo qualità dovrebbe creare un insieme automatizzato di test di accettazione per garantire che il sistema funzioni come previsto da un livello elevato.

Sono disponibili framework personalizzati, come Jackalope e Prosper, per semplificare la gestione delle API JCR in modo da garantire la produttività degli sviluppatori durante la scrittura di unit test.

### Pronti per la demo {#stay-demo-ready}

Il sistema dovrebbe essere disponibile per la demo all&#39;azienda al termine di ogni iterazione. Mantenendo il sistema in uno stato demo-ready, il team sarà sempre all&#39;interno di un&#39;iterazione di essere pronto per la produzione e il debito tecnico può essere mantenuto a un livello di manutenzione.

### Implementare un ambiente di integrazione continua e utilizzarlo {#implement-a-continuous-integration-environment-and-use-it}

L’implementazione di un ambiente di integrazione continua consente di eseguire facilmente e ripetutamente i test di unità e i test di integrazione. Disaccoppierà inoltre le distribuzioni dal team di sviluppo, consentendo alle altre parti del team di essere più efficienti e garantendo implementazioni più stabili e prevedibili.

### Mantenere il ciclo di sviluppo rapidamente mantenendo bassi i tempi di creazione {#keep-the-development-cycle-fast-by-keeping-build-times-low}

Se l’esecuzione dei test di unità richiede molto tempo, gli sviluppatori eviteranno di eseguirli e perderanno il loro valore. Se ci vuole molto tempo per costruire il codice e distribuirlo, le persone lo faranno meno spesso. Rendere i tempi di compilazione brevi una priorità garantisce che il tempo dedicato alla copertura dei test e all&#39;infrastruttura CI continui a rendere il team più produttivo.

### Ottimizza Sonar e altri strumenti di analisi del codice statico e agisce sui loro report {#fine-tune-sonar-and-other-static-code-analysis-tools-and-act-on-their-reports}

Gli strumenti di analisi del codice possono essere utili, ma solo se i loro rapporti portano all’azione del team di sviluppo. Senza perfezionare l’analisi fornita da questi strumenti, le raccomandazioni che generano non saranno rilevanti e perderanno il loro valore.

### Segui la regola dello Scout dei ragazzi {#follow-the-boy-scout-rule}

Gli Scout dei ragazzi hanno una regola: &quot;Lascialo stare meglio di quanto lo hai trovato.&quot; Finché tutti i membri del team di sviluppo aderiranno a questa regola e ripuliranno qualcosa quando incontreranno un disastro, il codice migliorerà costantemente.

### Evita di implementare le funzioni YAGNI {#avoid-implementing-yagni-features}

Le funzionalità YAGNI (o non ne avrai bisogno) sono cose che vengono implementate quando ci aspettiamo che avremo bisogno di qualcosa in futuro, anche se non ne avremo bisogno ora. Idealmente, dovremmo implementare la cosa più semplice che funzionerà oggi e utilizzare il refactoring continuo per garantire che l&#39;architettura del sistema evolva con i requisiti nel tempo. Questo ci permetterà di concentrarci su ciò che conta e di evitare il gonfiore del codice e il creep di funzionalità.
