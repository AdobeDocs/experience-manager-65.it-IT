---
title: Pratiche di sviluppo
seo-title: Pratiche di sviluppo
description: Best practice per lo sviluppo di AEM
seo-description: Best practice per lo sviluppo di AEM
uuid: 27a75f7f-6e2c-4113-9e9f-c5013a4594c2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8b0297a1-d922-410f-9aaf-3a6b87e11dc0
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 0%

---


# Pratiche di sviluppo{#development-practices}

## Lavorare secondo la definizione di Fine {#work-according-to-a-definition-of-done}

Ogni squadra ha una definizione diversa di ciò che &quot;fatto&quot; significa, ma è importante avere una storia e assicurarsi che soddisfi i criteri definiti prima di essere accettato.

Alcuni criteri comunemente specificati dai team includono:

* Codice rivisto per la formattazione
* Commenti/Javadoc aggiunto
* Soddisfa i livelli di copertura dei test richiesti
* Supera i test di unità e integrazione
* Convalida nell&#39;ambiente QA
* Localizzazione implementata

Senza un DoD ben definito, è facile finire in una situazione in cui molte cose sono a metà strada e niente è veramente completo.

### Definire e aderire alle convenzioni di codifica e formattazione {#define-and-adhere-to-coding-and-formatting-conventions}

Cose come i livelli di rientro e lo spazio vuoto possono non sembrare importanti, ma avere un codice formattato correttamente va molto lontano verso la leggibilità e la manutenzione. Le convenzioni dovrebbero essere discusse e concordate come squadra e seguite nel codice.

### Obiettivo per una copertura di prova elevata {#aim-for-high-test-coverage}

Con l&#39;aumento delle dimensioni dell&#39;implementazione di un progetto, il tempo necessario per eseguire il test sarà pari a quello necessario. Senza una buona copertura di test, il team di test non sarà in grado di scalare e gli sviluppatori finiranno per essere sepolti in bug.

Gli sviluppatori devono praticare il TDD, scrivendo test di unità non riusciti prima del codice di produzione che soddisferà i loro requisiti. Il QA dovrebbe creare un insieme automatizzato di test di accettazione per garantire che il sistema funzioni come previsto da un livello elevato.

Sono disponibili dei framework personalizzati, come Jackalope e Prosper, per semplificare il gioco delle API JCR in modo da garantire la produttività degli sviluppatori durante la scrittura di unit test.

### Pronto per la demo {#stay-demo-ready}

Il sistema dovrebbe essere disponibile per la dimostrazione al business alla fine di ogni iterazione. Mantenendo il sistema in uno stato demo-ready, il team sarà sempre all&#39;interno di un&#39;iterazione di essere pronto alla produzione e il debito tecnico può essere mantenuto a un livello sostenibile.

### Implementare un ambiente di integrazione continua e utilizzarlo {#implement-a-continuous-integration-environment-and-use-it}

L&#39;implementazione di un ambiente di integrazione continua consente di eseguire facilmente e ripetutamente test di unità e test di integrazione. Inoltre, disaccoppierà le installazioni del team di sviluppo, consentendo alle altre parti del team di essere più efficienti e garantendo installazioni più stabili e prevedibili.

### Mantenere il ciclo di sviluppo veloce mantenendo bassi i tempi di creazione {#keep-the-development-cycle-fast-by-keeping-build-times-low}

Se l&#39;esecuzione dei test di unità richiede molto tempo, gli sviluppatori non li eseguiranno e perderanno il loro valore. Se ci vuole molto tempo per creare il codice e distribuirlo, le persone lo faranno meno spesso. Rendere prioritari i tempi di realizzazione brevi assicura che il tempo dedicato alla copertura dei test e all&#39;infrastruttura CI continui a rendere il team più produttivo.

### Ottimizzate Sonar e altri strumenti di analisi del codice statici e agite sui loro report {#fine-tune-sonar-and-other-static-code-analysis-tools-and-act-on-their-reports}

Gli strumenti di analisi del codice possono essere utili, ma solo se i loro rapporti portano all’azione del team di sviluppo. Senza l&#39;ottimizzazione dell&#39;analisi fornita da questi strumenti, le raccomandazioni generate non saranno rilevanti e perderanno il loro valore.

### Seguire la regola di Scout  ragazzo {#follow-the-boy-scout-rule}

I Scout  Ragazzo hanno una regola: &quot;Lascialo meglio di quanto lo trovi.&quot; Finché tutti i membri del team di sviluppo aderiranno a questa regola e ripuliranno qualcosa quando incontreranno un casino, il codice migliorerà costantemente.

### Evitare di implementare le funzionalità YAGNI {#avoid-implementing-yagni-features}

Le funzioni YAGNI (o non ne avrete bisogno) sono implementate quando ci aspettiamo che avremo bisogno di qualcosa in futuro, anche se ora non ne abbiamo bisogno. Idealmente, dovremmo implementare la cosa più semplice che funzionerà oggi e utilizzare il refactoring continuo per assicurare che l&#39;architettura del sistema evolva con i requisiti nel tempo. Questo ci permetterà di concentrarci su ciò che conta ed evitare il codice gonfiabile e la confusione delle caratteristiche.
