---
title: Note sulla versione di AEM Sites
description: Note sulla versione specifiche di Adobe Experience Manager 6.5 Sites.
translation-type: tm+mt
source-git-commit: 23656e023a9a0bfc335655f9cfb0530aa917b3ef
workflow-type: tm+mt
source-wordcount: '872'
ht-degree: 62%

---


# Note sulla versione di AEM Sites {#aem-sites-release-notes}

Per informazioni sui miglioramenti di AEM Sites 6.5, consulta i seguenti riferimenti:

## Sviluppo di componenti e modelli {#component-amp-template-development}

* Archetipo di progetto Maven 18+ per nuovi progetti, consulta le [note sulla versione su Github](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype/releases).
* Archetipo di progetto Maven 1.0.6+ per applicazione a pagina singola per nuovi progetti, consulta le [note sulla versione su Github](https://github.com/adobe/aem-spa-project-archetype/releases).
* HTL versione 1.4, consulta le [note sulla versione su Github](https://github.com/adobe/htl-spec/releases/tag/1.4).

   * Operatore &quot;in&quot; per stringhe, array e oggetti:

      ```html
      ${'a' in 'abc’}
      ${100 in myArray}
      ${'a' in myObject}
      ```

   * Dichiarazioni di variabili con data-sly-set :
      `<sly data-sly-set.title="${currentPage.title}"/>${title}`

   * Elencare e ripetere i parametri di controllo: inizio, passo, fine:
      `<h2 data-sly-repeat="${currentPage.listChildren @ begin = 1, step=2}">${item.title}</h2>`

   * Identificatori per data-sly-unwrapping:

      ```html
      <div data-sly-unwrap.isUnwrapped="${myCondition || myOtherCondition}">
      text <span data-sly-test="${isUnwrapped}>is unwrapped</code>
      </div>
      ```

   * Supporto dei numeri negativi

* Core Components 2.3.2+, consulta le [note sulla versione su Github](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/releases).
* Sistema a griglia per contenitore layout, consulta [Github](https://github.com/Adobe-Marketing-Cloud/aem-responsivegrid).
* Clientlib Manager: Google Closure Compiler è diventato predefinito per minimizzare le clientlibs JavaScript (il vecchio predefinito era Yahoo YUI) e ha aggiornato Google Closure Compiler alla versione v20190121
* Editor modelli e criteri

   * Creare e modificare modelli per le app a pagina singola che utilizzano l&#39;SDK JS (chiamato anche Editor SPA)

* Sito di riferimento We.Retail 4.0, consulta le [note sulla versione su Github](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases).
* Toolkit per aggiornare i siti esistenti per sfruttare le funzionalità più recenti dell’editor, consulta [Archivio Github](https://github.com/adobe/aem-modernize-tools)

>[!CAUTION]
>
>AEM include la versione 1.12.4 della libreria jQuery per fornire la massima compatibilità con il codice personalizzato esistente. Adobe ha apportato modifiche per risolvere problemi di sicurezza noti.

## Amministrazione del sito {#site-administration}

* Nella barra [Riferimento](/help/sites-authoring/author-environment-tools.md#references) è stata integrata una nuova sezione per elencare i collegamenti interni che rimandano alla pagina selezionata. Questa funzione è utile quando si prevede di disattivare o eliminare una pagina, per vedere quali pagine devono essere corrette prima di renderle offline.
* La [vista a elenco](/help/sites-authoring/basic-handling.md#list-view) dispone ora di una nuova colonna per il flusso di lavoro, che mostra lo stato di una pagina che si trova in un flusso di lavoro.
* Nelle [proprietà della pagina](/help/sites-authoring/editing-page-properties.md), è ora possibile sfogliare tra le risorse esistenti quando si assegna una miniatura alla pagina (scheda Miniature).

## Editor pagina {#page-editor}

* Consente la modifica e la composizione contestuale di esperienze di app a pagina singola create con componenti React e Angular lato client che sfruttano l’SDK JS (chiamato anche Editor SPA)
* La modalità Scaffolding viene visualizzata solo se la pagina presenta una pagina di scaffolding configurata.

## Editor e frammenti di contenuto {#content-fragments-amp-editor}

* Nuova barra [Annotazioni](/help/assets/content-fragments/content-fragments-variations.md#viewing-editing-deleting-annotations) nell’Editor frammento di contenuto per lasciare commenti generali e visualizzare i commenti all’interno del testo (anche nella barra Timeline)
* Possibilità di impostare il tipo di contenuto predefinito di un elemento di testo su più righe in un [modello di frammento di contenuto](/help/assets/content-fragments/content-fragments-models.md) su testo semplice, testo RTF o markdown
* Aggiunta di [commenti/annotazioni](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment) selezionando il testo nell’editor di testo avanzato (visualizzazione a schermo intero)
* [Confronto tra le versioni](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions) di un frammento di contenuto affiancate mediante la barra Riferimento
* Il rapporto di download delle risorse ora mostra i relativi frammenti di contenuto
* Aggiunta del [supporto per i frammenti di contenuto all’API HTTP delle risorse](/help/assets/assets-api-content-fragments.md) tramite /api.json. Sono disponibili API per creare, aggiornare, leggere ed eliminare frammenti di contenuto.

## Frammenti di esperienza {#experience-fragments}

* Miglioramento dell’indicizzazione dei [frammenti esperienza](/help/sites-authoring/experience-fragments.md), in modo che il loro contenuto si trovi nella ricerca delle pagine in cui vengono utilizzati
* L’opzione [Export to Target](/help/sites-administering/experience-fragments-target.md) (Esporta per destinazione) permette ora di inviare il frammento di esperienza come JSON (l’impostazione predefinita è HTML) o in entrambi i formati

## Traduzione {#translation}

* Semplificazione della creazione di progetti di traduzione utilizzando la funzione di “progetti principali”
* Semplificazione dell’esecuzione dei progetti di traduzione impostando i lavori di traduzione sullo stato Approvato per impostazione predefinita
* Consente di aggiornare le pagine tradotte con modifiche in una memoria di traduzione di terze parti
* Consente di esportare i lavori di traduzione in formato JSON
* Aggiornare l’integrazione di Microsoft Translation per utilizzare l’API V3

## Gestione multisito (MSM) {#multi-site-management-msm}

* Per le configurazioni di rollout che utilizzano PushOnModify, è stata migliorata la gestione delle operazioni di spostamento delle pagine per evitare uno stato incoerente
* La creazione di una nuova pagina all’interno della struttura di livecopy creerà ora per impostazione predefinita una pagina autonoma
* Utilizzare le funzionalità MSM nelle app a pagina singola che utilizzano l&#39;SDK JS (chiamato anche Editor SPA)

## Lanci {#launches}

* Nuovo flusso di lavoro di revisione e approvazione per i lanci e possibilità di promuovere solo le pagine di lancio approvate
* Aggiunta di un’[opzione nell’interfaccia utente per scegliere di eliminare il lancio subito dopo la fase di promozione](/help/sites-authoring/launches-promoting.md#promoting-launch-pages)

## Simulazione e targeting dei contenuti  {#content-targeting-simulation}

* Il codice JavaScript del livello dati ContextHub e del motore delle regole lato client è stato aggiornato per utilizzare jQuery 3 per impostazione predefinita.

## AEM e Adobe Target {#aem-amp-adobe-target}

>[!CAUTION]
>
>Attualmente:
>
>* È supportato solo `at.js 1.x` se utilizzi Adobe Target come motore di destinazione all’interno AEM console Attività .
   >
   >
* Sono supportati sia `at.js. 1.x` che `at.js 2.x` se utilizzi l’esportazione di frammenti di esperienza in Target ed esegui attività nella console di Target.


* L’integrazione di Adobe Target consente ora di utilizzare l’API standard di Target. Le versioni precedenti di AEM utilizzano l’API HTTP di Target Classic, che ora è obsoleta.
* È inclusa la versione 63 di Adobe Target `mbox.js` . Adobe consiglia vivamente di passare all’implementazione `at.js` v1.x.
* `at.js` È ora inclusa la versione 1.5.0. Adobe consiglia di utilizzare [Adobe Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html) per eseguire il provisioning di `at.js` v1.x nel sito.

## AEM e Adobe Analytics {#aem-amp-adobe-analytics}

* `s_code.js` H.27.5 è incluso. L&#39;Adobe consiglia di passare all&#39;implementazione a `AppMeasurement.js`
* `AppMeasurement.js` È inclusa la versione 1.8.0. Adobe consiglia di utilizzare [Adobe Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html) per eseguire il provisioning di AppMeasurement.js nel sito.

## AEM e commercio {#aem-commerce}

I miglioramenti a Commerce Integration Framework si trovano in un ciclo di rilascio più veloce a partire da AEM 6.4. [Ulteriori informazioni qui](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/docs.html).

## Add-on Communities {#communities-add-on}

Consulta la [pagina delle note sulla versione di Communities](../release-notes/communities-release-notes.md)

## Add-on Screens  {#screens-add-on}

* Utilizzo di Lanci per pianificare future modifiche ai contenuti di segnaletica
* Riproduzione controllata in un canale sequenziale
* Creazione automatica della struttura del progetto utilizzando un file sorgente, ad esempio un foglio Excel

Per ulteriori dettagli sulle modifiche ad AEM Screens, consulta le Note sulla versione nella [Guida utente di AEM Screens](https://docs.adobe.com/content/help/it/experience-manager-screens/user-guide/aem-screens-introduction.html).
