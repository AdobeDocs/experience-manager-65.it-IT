---
title: Nozioni di base su punteggio e distintivi
description: Scopri in che modo la funzione di punteggio e badge di Adobe Experience Manager Communities identifica e premia i membri della community.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 470a382a-2aa7-449e-bf48-b5a804c5b114
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 0%

---

# Nozioni di base su punteggio e distintivi {#scoring-and-badges-essentials}

La funzione di punteggio e badge di AEM Communities identifica e premia i membri della community.

I dettagli della configurazione della funzione sono descritti in

* [Punteggio community e badge](/help/communities/implementing-scoring.md)

Questa pagina contiene ulteriori dettagli tecnici:

* Procedura [visualizzare un badge](#displaying-badges) come immagine o testo
* Come attivare la modalità estesa [debug logging](#debug-log-for-scoring-and-badging)
* Procedura [accedere a UGC](#ugc-for-scoring-and-badging) relativi a punteggio e badge

>[!CAUTION]
>
>La struttura di implementazione visibile in CRXDE Liti è soggetta a modifiche.

## Visualizzazione dei badge {#displaying-badges}

Se un badge viene visualizzato come testo o immagine è controllato sul lato client nel modello HBS.

Ad esempio, cerca `this.isAssigned` in `/libs/social/forum/components/hbs/topic/list-item.hbs`:

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

Se true, `isAssigned` indica che il badge è stato assegnato per un ruolo e deve essere visualizzato come testo.

Se false, `isAssigned` indica che il badge è stato assegnato per un punteggio ottenuto e deve essere visualizzato come immagine.

Qualsiasi modifica a questo comportamento deve essere apportata in uno script personalizzato (override o overlay). Consulta [Personalizzazione lato client](/help/communities/client-customize.md).

## Registro di debug per punteggio e badge {#debug-log-for-scoring-and-badging}

Per facilitare il debug di punteggi e contrassegni, è possibile impostare un file di registro personalizzato. Il contenuto di questo file di registro può quindi essere fornito all’assistenza clienti in caso di problemi con la funzione.

Per istruzioni dettagliate, visita [Creare un file di registro personalizzato](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file).

Per configurare rapidamente un file di log di Slinglog:

1. Accedere a **Supporto del registro della console Web Adobe Experience Manager**, ad esempio

   * https://localhost:4502/system/console/slinglog

1. Seleziona **Aggiungi nuovo logger**

   1. Seleziona `DEBUG` per **Livello registro**

   1. Inserisci un nome per **File di registro**, ad esempio

      * logs/scoring-debug.log

   1. Inserisci due **Logger** voci (classe) (utilizzando `+` )

      * `com.adobe.cq.social.scoring`
      * `com.adobe.cq.social.badging`

   1. Seleziona **Salva**

![debug-scoring-log](assets/debug-scoring-log.png)

Per visualizzare le voci di registro:

* Dalla console web

   * Sotto **Stato** menu
   * Seleziona **File di registro**
   * Cerca il nome del file di registro, ad esempio `scoring-debug`

* Sul disco locale del server

   * Il file di registro si trova in &lt;*server-install-dir*>/crx-quickstart/logs/&lt;*log-file-name*>.log

   * Ad esempio `.../crx-quickstart/logs/scoring-debug.log`

![registro punteggio](assets/scoring-log.png)

## UGC per punteggio e badge {#ugc-for-scoring-and-badging}

È possibile visualizzare il UGC relativo al punteggio e al contrassegno quando l’SRP scelto è JSRP o MSRP, ma non ASRP. (Se non conosci questi termini, consulta [Archiviazione contenuti community](/help/communities/working-with-srp.md) e [Panoramica del provider di risorse di archiviazione](/help/communities/srp.md).)

Le descrizioni per l’accesso ai dati di punteggio e badge utilizzano JSRP, in quanto l’UGC è facilmente accessibile tramite [CRXDE Liti](/help/sites-developing/developing-with-crxde-lite.md).

**JSRP sull’autore**: la sperimentazione nell’ambiente di authoring genera contenuti generati dall’utente che sono visibili solo dall’ambiente di authoring.

**JSRP in fase di pubblicazione**: analogamente, se si esegue il test nell’ambiente di pubblicazione, è necessario accedere a CRXDE Liti con privilegi amministrativi su un’istanza di pubblicazione. Se l’istanza Publish è in esecuzione in [modalità di produzione](/help/sites-administering/production-ready.md) (modalità di esecuzione nosamplecontent), è necessario [abilita CRXDE Liti](/help/sites-administering/enabling-crxde-lite.md).

La posizione di base di UGC su JSRP è `/content/usergenerated/asi/jcr/`.

### API per assegnazione punteggi e assegnazione badge {#scoring-and-badging-apis}

Sono disponibili le seguenti API:

* [com.adobe.cq.social.scoring.api in 6.3](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=it)
* [com.adobe.cq.social.badging.api in 6.3](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=it)

Gli ultimi JavaScript per il feature pack installato sono disponibili per gli sviluppatori dall’archivio Adobe. Consulta [Utilizzo di Maven per le community : Javadocs](/help/communities/maven.md#javadocs).

**La posizione e il formato dell’UGC nell’archivio sono soggetti a modifiche senza preavviso**.

### Esempio di configurazione {#example-setup}

Le schermate dei dati dell&#39;archivio provengono dall&#39;impostazione del punteggio e del badge per un forum su due diversi siti AEM:

1. Un sito AEM *con* id univoco (sito community creato tramite procedura guidata):

   * Utilizzo del sito Guida introduttiva (coinvolgi) creato durante il [tutorial introduttivo](/help/communities/getting-started.md)
   * Individua il nodo della pagina del forum

     `/content/sites/engage/en/forum/jcr:content`

   * Aggiungere proprietà di punteggio e badge

   ```
   scoringRules = [/libs/settings/community/scoring/rules/comments-scoring,
   /libs/settings/community/scoring/rules/forums-scoring]
   ```

   ```
   badgingRules =[/libs/settings/community/badging/rules/comments-scoring,
   /libs/settings/community/badging/rules/forums-scoring]
   ```

   * Individua il nodo del componente forum

     `/content/sites/engage/en/forum/jcr:content/content/primary/forum`
( `sling:resourceType = social/forum/components/hbs/forum`)

   * Per visualizzare i badge, aggiungi la proprietà

     `allowBadges = true`

   * Un utente effettua l’accesso, crea un argomento del forum e riceve un distintivo bronzo

1. Un sito AEM *senza* un id univoco :

   * Utilizzo di [Guida ai componenti della community](/help/communities/components-guide.md)
   * Individua il nodo della pagina del forum

     `/content/community-components/en/forum/jcr:content`

   * Aggiungere proprietà di punteggio e badge

   ```
   scoringRules = [/libs/settings/community/scoring/rules/comments-scoring,
   /libs/settings/community/scoring/rules/forums-scoring]
   ```

   ```
   badgingRules =[/libs/settings/community/badging/rules/comments-badging,
   /libs/settings/community/badging/rules/forums-badging]
   ```

   * Individua il nodo del componente forum

     `/content/community-components/en/forum/jcr:content/content/forum`
( `sling:resourceType = social/forum/components/hbs/forum`)

   * Per visualizzare i badge, aggiungi la proprietà

     `allowBadges = true`

   * Un utente effettua l’accesso, crea un argomento del forum e riceve un distintivo bronzo

1. A un utente viene assegnato un badge moderatore utilizzando cURL:

   ```shell
   curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:assignBadge" -F "badgeContentPath=/libs/settings/community/badging/images/moderator/jcr:content/moderator.png" https://localhost:4503/home/users/community/w271OOup2Z4DjnOQrviv/profile.social.json
   ```

   Poiché un utente ha ottenuto due distintivi bronzo ed è stato insignito di un distintivo moderatore, appare con la sua voce forum come segue:

   ![moderatore](assets/moderator.png)

>[!NOTE]
>
>Questo esempio non segue le seguenti best practice:
>
>* I nomi delle regole di punteggio devono essere univoci a livello globale; non devono terminare con lo stesso nome.
>
>  Un esempio di cosa *non* da fare:
>
>  /libs/settings/community/scoring/rules/site1/forums-scoring
>  /libs/settings/community/scoring/rules/site2/forums-scoring
>
>* Creazione di immagini distintive univoche per diversi siti AEM

### UGC per punteggio di accesso {#access-scoring-ugc}

Uso del [API](#scoring-and-badging-apis) è da preferirsi.

A scopo investigativo, utilizzando JSRP per l’esempio, la cartella di base contenente i punteggi è

* `/content/usergenerated/asi/jcr/scoring`

Nodo figlio di `scoring` è il nome della regola di punteggio. Pertanto, una best practice prevede che i nomi delle regole di punteggio su un server siano univoci a livello globale.

Per il sito Geometrixx Engage, l’utente e il relativo punteggio si trovano in un percorso costruito con il nome della regola di punteggio, ID sito community ( `engage-ba81p`), un ID univoco e l&#39;ID dell&#39;utente:

* `.../scoring/forums-scoring/engage-ba81p/6d179715c0e93cb2b20886aa0434ca9b5a540401/riley`

Per il sito guida dei componenti community, l’utente e il relativo punteggio si trovano in un percorso costruito con il nome della regola di punteggio, un ID predefinito ( `default-site`), un ID univoco e l&#39;ID dell&#39;utente:

* `.../scoring/forums-scoring/default-site/b27a17cb4910a9b69fe81fb1b492ba672d2c086e/riley`

Il punteggio viene memorizzato nella proprietà `scoreValue_tl` che possono contenere solo un valore o fare riferimento indirettamente a un atomicCounter.

![access-scoring-ugc](assets/access-scoring-ugc.png)

### UGC per assegnazione badge di accesso {#access-badging-ugc}

Uso del [API](#scoring-and-badging-apis) è da preferirsi.

A scopo investigativo, utilizzando JSRP per l’esempio, la cartella di base contenente le informazioni sui badge assegnati o assegnati è

* `/content/usergenerated/asi/jcr`

Seguito dal percorso del profilo dell’utente, che termina con una cartella di badge, ad esempio:

* `/home/users/community/w271OOup2Z4DjnOQrviv/profile/badges`

#### Badge aggiudicato {#awarded-badge}

![award-badging-ugc](assets/access-badging-ugc.png)

#### Badge assegnato {#assigned-badge}

![assigned-badge](assets/assigned-badge.png)

## Informazioni aggiuntive {#additional-information}

Per visualizzare un elenco ordinato di membri in base ai punti:

* [Funzione classifica](/help/communities/functions.md#leaderboard-function) da includere in un sito community o in un modello di gruppo.
* [Componente classifica](/help/communities/enabling-leaderboard.md), componente in primo piano della funzione Classifica, per l’authoring delle pagine.
