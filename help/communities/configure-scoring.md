---
title: Punteggio e Badge Essentials
seo-title: Punteggio e Badge Essentials
description: Panoramica delle funzioni Punteggio e Badge
seo-description: Panoramica delle funzioni Punteggio e Badge
uuid: 6e3af071-04e8-4dc1-977a-0da711b72961
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 628b6dcd-8b1c-4166-8fc2-843baa86ac1c
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 0%

---


# Punteggio e Badge Essentials {#scoring-and-badges-essentials}

La funzione  punteggio e distintivi AEM Communities consente di identificare e premiare i membri della community.

I dettagli relativi alla configurazione della funzione sono descritti in

* [Punteggio e distintivi delle community](/help/communities/implementing-scoring.md)

Questa pagina contiene ulteriori dettagli tecnici :

* Come [visualizzare un contrassegno](#displaying-badges) come immagine o testo
* Come attivare la registrazione di [debug estesa](#debug-log-for-scoring-and-badging)
* Come [accedere a UGC](#ugc-for-scoring-and-badging) relativi al punteggio e al contrassegno

>[!CAUTION]
>
>La struttura di implementazione visibile in CRXDE Lite è soggetta a modifiche.

## Visualizzazione dei badge {#displaying-badges}

Se un contrassegno viene visualizzato come testo o immagine viene controllato sul lato client nel modello HBS.

Ad esempio, cercare `this.isAssigned` in `/libs/social/forum/components/hbs/topic/list-item.hbs`:

```
{{#each author.badges}}

  {{#if this.isAssigned}}

    <div class="scf-badge-text">

      {{this.title}}

    </div>

  {{/if}}

{{/each}}

{{#each author.badges}}

  {{#unless this.isAssigned}}

    <img class="scf-badge-image" alt="{{this.title}}" title="{{this.title}}" src="{{this.imageUrl}}" />

  {{/unless}}

{{/each}}
```

Se true, isAssigned indica che il contrassegno è stato assegnato a un ruolo e che il contrassegno deve essere visualizzato come testo.

Se false, viene assegnato indica che il contrassegno è stato assegnato per un punteggio ottenuto e che il contrassegno deve essere visualizzato come immagine.

Eventuali modifiche a questo comportamento devono essere apportate in uno script personalizzato (override o sovrapposizione). Consultate Personalizzazione lato [client](/help/communities/client-customize.md).

## Registro di debug per il punteggio e il contrassegno {#debug-log-for-scoring-and-badging}

Per facilitare il debug del punteggio e del contrassegno, è possibile configurare un file di registro personalizzato. Il contenuto di questo file di registro può quindi essere fornito all&#39;assistenza clienti in caso di problemi con la funzionalità.

Per istruzioni dettagliate, vedere [Creazione di un file](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file)di registro personalizzato.

Per impostare rapidamente un file slinglog:

1. Accedere al supporto **dei registri della console Web di** Adobe Experience Manager, ad esempio

   * https://localhost:4502/system/console/slinglog

1. Seleziona **Aggiungi nuovo logger**

   1. Seleziona `DEBUG` per il livello di **registro**

   1. Immettere un nome per il file **di** registro, ad esempio

      * logs/scoring-debug.log
   1. Inserite due voci **Logger** (classe) (utilizzando l&#39; `+` icona)

      * `com.adobe.cq.social.scoring`
      * `com.adobe.cq.social.badging`
   1. Seleziona **Salva**



![debug-scoring-log](assets/debug-scoring-log.png)

Per visualizzare le voci di registro:

* Dalla console Web

   * Nel menu **Stato**
   * Seleziona file **di registro**
   * Cercare il nome del file di registro, ad esempio `scoring-debug`

* Sul disco locale del server

   * Il file di registro si trova in &lt;*server-install-dir*>/crx-quickstart/logs/&lt;*log-file-name*>.log

   * Esempio, `.../crx-quickstart/logs/scoring-debug.log`

![punteggio-log](assets/scoring-log.png)

## UGC per il punteggio e il contrassegno {#ugc-for-scoring-and-badging}

È possibile visualizzare l&#39;UGC relativo al punteggio e al contrassegno quando l&#39;SRP scelto è JSRP o MSRP, ma non ASRP. (Se non avete familiarità con questi termini, consultate [Community Content Storage](/help/communities/working-with-srp.md) and [Storage Resource Provider Overview](/help/communities/srp.md)(Panoramica sui fornitori di risorse di archiviazione e archiviazione).

Le descrizioni per accedere ai dati di punteggio e contrassegno utilizzano JSRP, in quanto l&#39;UGC è facilmente accessibile tramite [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

**JSRP sull’autore**: la sperimentazione nell’ambiente di authoring produce UGC visibile solo dall’ambiente di authoring.

**JSRP al momento della pubblicazione**: analogamente, se si eseguono test nell’ambiente di pubblicazione, sarà necessario accedere ai CRXDE Lite con privilegi amministrativi in un’istanza di pubblicazione. Se l’istanza di pubblicazione è in esecuzione in modalità [di](/help/sites-administering/production-ready.md) produzione (nosamplecontent runmode), sarà necessario [abilitare CRXDE Lite](/help/sites-administering/enabling-crxde-lite.md).

La posizione di base di UGC su JSRP è `/content/usergenerated/asi/jcr/`.

### API Punteggio e Badging {#scoring-and-badging-apis}

Le seguenti API sono disponibili per l&#39;uso:

* [com.adobe.cq.social.scoring.api](https://docs.adobe.com/content/docs/en/aem/6-3/develop/ref/javadoc/com/adobe/cq/social/scoring/api/package-summary.html)
* [com.adobe.cq.social.badging.api](https://docs.adobe.com/content/docs/en/aem/6-3/develop/ref/javadoc/com/adobe/cq/social/badging/api/package-summary.html)

I più recenti Javadocs per il pacchetto di funzionalità installato sono disponibili per gli sviluppatori dall&#39;archivio del Adobe . Vedere [Utilizzo di Paradiso per le community: Javadocs](/help/communities/maven.md#javadocs).

**La posizione e il formato dell’UGC nel repository sono soggetti a modifiche senza preavviso**.

### Esempio di configurazione {#example-setup}

Le schermate dei dati del repository derivano dalla configurazione del punteggio e del contrassegno per un forum su due siti AEM diversi:

1. Un sito AEM *con* un ID univoco (sito community creato tramite la procedura guidata):

   * Utilizzo del sito Esercitazione introduttiva (interazione) creato durante l’esercitazione [introduttiva](/help/communities/getting-started.md)
   * Individuare il nodo della pagina del forum

      `/content/sites/engage/en/forum/jcr:content`

   * Aggiunta di proprietà di punteggio e contrassegno

   ```
   scoringRules = [/libs/settings/community/scoring/rules/comments-scoring,
   /libs/settings/community/scoring/rules/forums-scoring]
   ```

   ```
   badgingRules =[/libs/settings/community/badging/rules/comments-scoring,
   /libs/settings/community/badging/rules/forums-scoring]
   ```

   * Individuare il nodo del componente forum

      `/content/sites/engage/en/forum/jcr:content/content/primary/forum`
( `sling:resourceType = social/forum/components/hbs/forum`)

   * Aggiungi proprietà a simboli di visualizzazione

      `allowBadges = true`

   * Un utente accede, crea un argomento del forum e riceve un contrassegno di bronzo


1. Un sito AEM *senza* un ID univoco:

   * Utilizzo della guida [Community Components](/help/communities/components-guide.md)
   * Individuare il nodo della pagina del forum

      `/content/community-components/en/forum/jcr:content`

   * Aggiunta di proprietà di punteggio e contrassegno

   ```
   scoringRules = [/libs/settings/community/scoring/rules/comments-scoring,
   /libs/settings/community/scoring/rules/forums-scoring]
   ```

   ```
   badgingRules =[/libs/settings/community/badging/rules/comments-badging,
   /libs/settings/community/badging/rules/forums-badging]
   ```

   * Individuare il nodo del componente forum

      `/content/community-components/en/forum/jcr:content/content/forum`
( `sling:resourceType = social/forum/components/hbs/forum`)

   * Aggiungi proprietà a simboli di visualizzazione

      `allowBadges = true`

   * Un utente accede, crea un argomento del forum e riceve un contrassegno di bronzo


1. A un utente viene assegnato un contrassegno moderatore utilizzando cURL:

   ```shell
   curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:assignBadge" -F "badgeContentPath=/libs/settings/community/badging/images/moderator/jcr:content/moderator.png" https://localhost:4503/home/users/community/w271OOup2Z4DjnOQrviv/profile.social.json
   ```

   Poiché un utente ha guadagnato due simboli di bronzo ed è stato assegnato un badge moderatore, questo è il modo in cui l&#39;utente appare con la sua voce forum.

   ![moderatore](assets/moderator.png)

>[!NOTE]
>
>Questo esempio non segue le best practice seguenti:
>
>* I nomi delle regole di punteggio devono essere univoci a livello globale; non devono terminare con lo stesso nome.
>
>  
Un esempio di cosa *non* fare:
>
>  /libs/settings/community/scoring/rules/site1/forums-scoring
>  /libs/settings/community/scoring/rules/site2/forums-scoring
>
>* Creazione di immagini di contrassegno univoche per diversi siti AEM


### UGC per punteggio di accesso {#access-scoring-ugc}

È preferibile utilizzare le [API](#scoring-and-badging-apis) .

A scopo investigativo, utilizzando JSRP per esempio, la cartella base contenente i punteggi è

* `/content/usergenerated/asi/jcr/scoring`

Il nodo figlio di `scoring` è il nome della regola di punteggio. Di conseguenza, si consiglia di assegnare a un server nomi univoci per le regole di punteggio.

Per il sito di Geometrixx Engage, l&#39;utente e il relativo punteggio si trovano in un percorso conteggiato con il nome della regola di punteggio, l&#39;ID del sito della community ( `engage-ba81p`), un ID univoco e l&#39;ID dell&#39;utente:

* `.../scoring/forums-scoring/engage-ba81p/6d179715c0e93cb2b20886aa0434ca9b5a540401/riley`

Per il sito della guida per i componenti della community, l’utente e il relativo punteggio si trovano in un percorso costruito con il nome della regola di punteggio, un ID predefinito ( `default-site`), un ID univoco e l’ID dell’utente:

* `.../scoring/forums-scoring/default-site/b27a17cb4910a9b69fe81fb1b492ba672d2c086e/riley`

Il punteggio è memorizzato nella proprietà `scoreValue_tl` che può contenere solo un valore o fare riferimento indirettamente a un atomicCounter.

![access-scoring-ugc](assets/access-scoring-ugc.png)

### Accesso UGC {#access-badging-ugc}

È preferibile utilizzare le [API](#scoring-and-badging-apis) .

A scopo investigativo, utilizzando JSRP per esempio, la cartella di base contenente informazioni sui simboli assegnati o assegnati è

* `/content/usergenerated/asi/jcr`

Seguito dal percorso del profilo dell&#39;utente, che termina in una cartella dei simboli, ad esempio:

* `/home/users/community/w271OOup2Z4DjnOQrviv/profile/badges`

#### Badge aggiudicato {#awarded-badge}

![badging-ugc](assets/access-badging-ugc.png)

#### Badge assegnato {#assigned-badge}

![badge assegnato](assets/assigned-badge.png)

## Informazioni aggiuntive {#additional-information}

Per visualizzare un elenco ordinato di membri in base ai punti:

* [Funzione](/help/communities/functions.md#leaderboard-function) della classifica per l&#39;inclusione in un sito o modello di gruppo community.
* [Componente](/help/communities/enabling-leaderboard.md)Leaderboard, componente della funzione Leaderboard per l’authoring delle pagine.

