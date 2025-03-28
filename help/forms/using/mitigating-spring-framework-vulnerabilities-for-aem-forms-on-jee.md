---
title: Mitigazione delle vulnerabilità del framework di primavera per AEM Forms su JEE
description: Mitigazione delle vulnerabilità del framework di primavera per AEM Forms su JEE
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 61cce7cd8290156bec6dcc351a59093f545a4ec7
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 1%

---


# Mitigazione delle vulnerabilità del framework di primavera per AEM Forms su JEE

Questo documento fornisce indicazioni su come risolvere due vulnerabilità critiche del framework di primavera che interessano AEM Forms su JEE:

- **[CVE-2024-38819](https://spring.io/security/cve-2024-38819)**: vulnerabilità di attraversamento del percorso nei framework web funzionali
- **[CVE-2024-38820](https://spring.io/security/cve-2024-38820)**: Eccezione di corrispondenza sensibile a maiuscole e minuscole del DataBinder del framework di primavera

## Versioni interessate

- Adobe Experience Manager 6.5 Forms su JEE
- Versioni da AEM 6.5 Forms GA a 6.5.22.0

## Risoluzione

### Soluzioni specifiche per le versioni

| Versione AEM Forms | Azione richiesta |
|-------------------|-----------------|
| 6.5.22.0 | 1. [Scarica l&#39;hotfix per il tuo ambiente](/help/release-notes/aem-forms-hotfix.md). </br> 2. Per installare questa correzione, seguire le istruzioni per [installare Service Pack in un AEM Form su JEE](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). |
| 6.5.17.0 - 6.5.21.0 | [Applica i passaggi di mitigazione manuali](#manual-mitigation-steps). |
| 6.5 - 6.5.16.0 | 1. [Installare il service pack più recente](/help/release-notes/release-notes.md)<br>2. [Implementa la soluzione appropriata](#version-specific-solutions) in base alla versione aggiornata. |

> **Nota**: AEM Forms supporta ufficialmente solo i sei Service Pack più recenti. Gli utenti delle versioni precedenti devono prima effettuare l’aggiornamento al service pack più recente e quindi installare l’hotfix richiesto.

## Considerazioni sull’implementazione

### Per ambienti cluster

Quando si lavora con una distribuzione in cluster:

- Applica sostituzioni file JAR (passaggio #4) in **tutti i nodi** nel cluster
- Mantenere la coerenza utilizzando versioni JAR identiche in tutti i server
- Completare gli aggiornamenti su tutti i nodi prima di avviare qualsiasi riavvio del servizio
- Implementare una strategia di riavvio coordinata per ridurre al minimo i tempi di inattività del sistema

### Per ambienti a nodo singolo

Quando si lavora con una distribuzione autonoma:

- Segui un processo semplificato in quanto non sono presenti server di localizzazione da gestire
- Ometti eventuali passaggi relativi alla configurazione o all&#39;avvio del server di localizzazione
- Completa tutti gli altri passaggi come indicato, in particolare le sostituzioni JAR e gli aggiornamenti manifesti
- Riavvia il server applicazioni dopo aver implementato tutte le modifiche

## Passaggi di Mitigazione manuali

1. Arrestare i server applicazioni.
1. Server di arresto e localizzazione.
1. Rimuovi i file JAR di primavera dall’ORECCHIO principale:
   1. Accedi a `[Adobe_Experience_Manager_Forms installation directory]/deploy`.
   1. Aprire il file `adobe-core-<appserver>.ear` utilizzando uno strumento di gestione dell&#39;archivio. Dove `<appserver>` può essere JBoss, WebLogic o WebSphere, a seconda dell&#39;ambiente:
   - **Per JBoss:** Passare alla cartella `ear/lib` ed eliminare i seguenti file JAR:
- `spring-core-<version>.jar`
- `spring-web-<version>.jar`

   - **Per WebLogic o WebSphere:** eliminare i seguenti file JAR dalla radice dell&#39;EAR:
- `spring-core-<version>.jar`
- `spring-web-<version>.jar`

   - **Per tutti i server applicazioni:** Al livello principale di `adobe-core-<appserver>.ear`, aprire il file `adobe-dscf.jar` e modificare il file `META-INF/MANIFEST.MF` per rimuovere eventuali riferimenti ai seguenti file JAR:
- `spring-core-<version>.jar`
- `spring-web-<version>.jar`

1. Sostituisci file JAR dalla distribuzione Geode:
   1. Passa a `<Adobe_Experience_Manager_Forms>/lib/caching/lib`
   1. Sostituisci i file JAR esistenti con le versioni aggiornate:
   - `spring-context-<version>.jar` → `spring-context-6.1.14.jar`
   - `spring-beans-<version>.jar` → `spring-beans-6.1.14.jar`
   - `spring-core-<version>.jar` → `spring-core-6.1.14.jar`
   - `spring-jcl-<version>.jar` → `spring-jcl-6.1.14.jar`
   - `spring-web-<version>.jar` → `spring-web-6.1.14.jar`

   Per ottenere i file JAR più recenti, scarica il file spring-6.1.14-jars.zip da [Distribuzione di software Adobe](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/spring-6.1.14-jars.zip) ed estrai il file ZIP per accedere ai file JAR del framework Spring aggiornati.

   1. Aggiorna i file MANIFEST.MF nei seguenti file JAR:
   - `geode-server-all-<version>.jar`
   - `gfsh-dependencies.jar`

   Per ogni JAR:
   - Aprire il file JAR con uno strumento di gestione dell’archivio
   - Individua ed estrai il file `META-INF/MANIFEST.MF`
   - Modificare il file MANIFEST.MF in un editor di testo
   - Trova la sezione &quot;Percorso-Classe&quot; e aggiorna tutti i riferimenti al framework Spring:
      - Da `spring-core-<version>.jar` a `spring-core-6.1.14.jar`
      - Da `spring-web-<version>.jar` a `spring-web-6.1.14.jar`
      - Da `spring-context-<version>.jar` a `spring-context-6.1.14.jar`
      - Da `spring-beans-<version>.jar` a `spring-beans-6.1.14.jar`
      - Da `spring-jcl-<version>.jar` a `spring-jcl-6.1.14.jar`
   - Salvare il file MANIFEST.MF modificato
   - Sostituisci il file MANIFEST.MF originale nel file JAR con la versione aggiornata
   - Salvare il file JAR

   1. Problemi comuni da considerare:
      - Verifica che non siano presenti voci duplicate nel manifesto
      - Gestisci terminazioni riga corrette
      - Verifica che tutti i JAR di riferimento siano presenti nei percorsi specificati

   1. Passaggi della verifica:
      - Verifica se il manifesto è aggiornato correttamente
      - Verifica che tutte le dipendenze di primavera siano correttamente referenziate
      - Assicurati che non rimangano riferimenti alla versione precedente
      - Eseguire il test dell&#39;applicazione per verificare che non vi siano problemi di caricamento della classe

1. Esegui Configuration Manager.

1. Riavvia server:
   - Avviare i server di localizzazione utilizzando JDK 17
   - Avviare gli Application Server utilizzando la stessa versione JDK (JDK 8 o JDK 11) utilizzata in precedenza.
