---
title: Ristrutturazione repository in AEM 6.5
seo-title: Ristrutturazione repository in AEM 6.5
description: Scopri la ristrutturazione dell’archivio in AEM 6.5
seo-description: Scopri la ristrutturazione dell’archivio in AEM 6.5
uuid: bc577c82-3279-4ddd-898c-607864868db0
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: 274a7f5a-d509-4ca9-9ae5-30e48f34f171
docset: aem65
redirecttarget: /content/help/en/experience-manager/6-5/help/sites-deploying/repository-restructuring.html
translation-type: tm+mt
source-git-commit: bd0dc09ea230416ad3544d14440b7b74b80ec406

---


# Ristrutturazione repository in AEM 6.5 {#repository-restructuring-in-aem}

## Introduzione {#introduction}

Prima di AEM 6.5, il codice cliente era implementato in aree del JCR imprevedibili soggette a modifiche agli aggiornamenti. Per questo motivo, nelle release formali di AEM (Versioni principali, Feature Pack, Service Pack o Hotfix) veniva spesso sovrascritto il codice, la configurazione o il contenuto personalizzato. Inoltre, a volte le modifiche apportate dai clienti hanno sovrascritto il codice o il contenuto del prodotto AEM, rompendo le funzionalità del prodotto.

Questi conflitti non sempre erano risolvibili automaticamente, richiedevano un notevole tempo di elaborazione per contrassegnare e richiedevano un intervento umano per risolverli, la cui risoluzione non era sempre chiara. delineando chiaramente le gerarchie per il codice prodotto AEM e il codice cliente, questi conflitti possono essere evitati.

A tal fine, a partire da AEM 6.5 e per essere continuati nelle release future, il contenuto verrà ristrutturato `/etc` in altre cartelle della directory archivio, insieme a linee guida sui contenuti da inserire, in conformità alle seguenti regole di alto livello:

* Il codice prodotto AEM verrà sempre inserito in `/libs`, che non deve essere sovrascritto dal codice personalizzato
* Il codice personalizzato deve essere inserito in `/apps`, `/content`e `/conf`

Questo articolo è organizzato in tre sezioni, che rappresentano il tipo di contenuto spostato da `/etc`:

1. Configurazione
1. Librerie lato client
1. Varie

Ogni sezione include:

* una tabella con le posizioni ristrutturate e il contesto aggiuntivo. Nel prossimo futuro, si prevede che le tabelle saranno formattate in una struttura piatta per una migliore leggibilità.
* una strategia di estensibilità che consente al codice personalizzato di estendere con successo il codice dell’applicazione AEM in cui risiede `/libs`.

## Compatibilità con versioni precedenti {#backwards-compatibility}

Nella maggior parte dei casi, la compatibilità con le posizioni precedenti viene mantenuta dopo l’aggiornamento ad AEM 6.5. Ciò è possibile grazie alla conservazione e al rispetto delle vecchie posizioni da parte del codice prodotto, oltre alle nuove posizioni aggiunte. Nella maggior parte dei casi, la logica condizionale viene utilizzata per verificare se la cartella precedente esiste e per leggere il contenuto al posto della nuova posizione.

Dopo l&#39;aggiornamento alla versione 6.5, i clienti sono invitati a rimuovere le posizioni precedenti in modo da utilizzare i contenuti nelle nuove posizioni. Le tabelle di seguito contengono istruzioni per aderire alla nuova struttura di contenuto per posizione.

>[!NOTE]
>
>Un&#39;istanza aggiornata sul posto includerà posizioni di contenuto precedenti oltre alle nuove posizioni. Una nuova installazione sviluppatore includerà solo le nuove posizioni.

## Come leggere le tabelle {#how-to-read-the-tables}

La tabella di ciascuna sezione include:

* la soluzione AEM (Siti, Risorse, Moduli, ecc.) per la quale questo contenuto è rilevante
* la vecchia posizione (6.4 e versioni precedenti)
* la nuova posizione 6.5
* Istruzioni per l&#39;allineamento con la nuova struttura del contenuto. Ad esempio, potrebbe essere necessario eseguire uno script o spostare manualmente i file nelle settimane o nei mesi successivi a un aggiornamento 6.5
* L’approccio utilizzato da AEM per mantenere la compatibilità con le versioni precedenti dei vecchi percorsi di contenuti per i clienti che effettuano l’aggiornamento ad AEM 6.5 da una versione precedente

## Configurazione {#configuration}

Le posizioni del contenuto in questa sezione in genere fanno riferimento al contenuto che si trova in una `/settings` cartella in `/libs`, `/apps`o `/conf`.

### Strategia di estensibilità {#extensibility-strategy}

In generale, ma con alcune eccezioni, il contenuto di questa sezione può essere esteso utilizzando la funzione di configurazione [](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html) in base al contesto di Apache Sling.

In poche parole, la configurazione in base al contesto consente di sovrapporre più volte il contenuto di una parte del repository in altre parti del repository. Ad esempio, il contenuto in `/libs` può essere sovrapposto dal contenuto in `/apps`, che può quindi essere sovrapposto dal contenuto in `/conf`. Inoltre, il contenuto di una cartella globale sotto `/conf` può essere sovrapposto da un &quot;tenant&quot; o &quot;sito&quot; specifico (ad esempio `/conf/we-retail/settings`).

In genere, la configurazione in base al contesto viene utilizzata come strategia per l&#39;estensione delle configurazioni delle funzioni, ma in alcuni casi è utilizzata da altri tipi di contenuto.

La tabella seguente include una colonna aggiuntiva denominata &quot;Tipo di configurazione&quot; per spiegare in che misura è possibile sovrapporre una configurazione. Seguono ulteriori dettagli sui seguenti tipi di configurazione:

**non in base al contesto**

* Le risorse si trovano in strutture di cartelle in base al contesto (come `/libs/settings`), ma vi viene sempre fatto riferimento tramite percorso assoluto, in modo che la consapevolezza del contesto non sia effettiva.
* Le risorse potrebbero essere ovunque. Ad esempio, le licenze DRM di Risorse potrebbero essere in `/content/my-customer/licenses/creative-commons.html`
* Esempi:

   * Script del flusso di lavoro -> `/apps/settings/workflow/scripts/noop.ecma`
   * Licenze DRM Assets -> `/apps/settings/dam/drm/my-license`

**Solo globale**

* Funzionalità con configurazione globale
* Come punto di riferimento, precedenza delle impostazioni in questo esempio: `/libs/settings` &lt; `/apps/settings` &lt; `/conf/global`

* AEM supporta solo la configurazione globale e non le configurazioni con tenant
* AEM inizierà sempre a cercare le configurazioni a livello /conf/global

* Esempi:

   * Moduli di avvio per flusso di lavoro -> `/libs/settings/workflow/launcher`
   * Modelli flusso di lavoro -> `/conf/global/settings/workflow/models`

**locatario**

* Per le configurazioni basate sul tenant, consultate questo esempio per la precedenza dei percorsi di configurazione: `/libs/settings` &lt; `/apps/settings` &lt; `/conf/global` &lt; `/conf/we-retail`, dove noi-retail è il nome tenant. Le configurazioni basate sul tenant supportano anche i sub-tenant.

* AEM supporta le configurazioni consolidate. Rispetta la `cq:conf` proprietà nella gerarchia
* Esempi:

   * Modelli modificabili -> `/conf/we-retail/settings/wcm/templates`
   * Configurazioni cloud -> `/conf/we-retail/settings/cloudsettings`

<table>
 <tbody>
  <tr>
   <td><strong>Soluzione</strong></td>
   <td><strong>Posizione precedente</strong><br /> </td>
   <td><strong>Nuova posizione</strong></td>
   <td><strong>Tipo di configurazione in base al contesto</strong><br /> </td>
   <td><strong>Metodo di compatibilità con le versioni precedenti</strong></td>
   <td><strong>Requisiti per l'allineamento all'ultimo modello</strong></td>
  </tr>
  <tr>
   <td>AEM Sites / AEM Forms</td>
   <td><p><code>/etc/cloudservices/typekit</code></p> <p><code>/etc/cloudservices/recaptcha</code></p> <p><code>/etc/cloudservices/echosign</code></p> </td>
   <td><p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/typekit</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/recaptcha</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/echosign</code></p> </td>
   <td>locatario</td>
   <td><p>Servizi cloud legacy.</p> <p>Permanente in un aggiornamento locale. Il codice consente di elencare e leggere i contenuti ancora presenti in AEM come fallback.</p> </td>
   <td>L'utilità di migrazione dei contenuti pigri può essere attivata dall'interfaccia utente di migrazione Forms per effettuare la conversione automatica nel nuovo percorso.<br /> </td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/cloudservices/fdm</code></td>
   <td><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/fdm</code></td>
   <td>locatario</td>
   <td><p>Servizi cloud legacy.</p> <p>Permanente in una configurazione aggiornata locale. Il codice consente di elencare e leggere i contenuti ancora presenti in AEM come fallback.</p> </td>
   <td>L'utilità di migrazione dei contenuti pigri può essere attivata dall'interfaccia utente di migrazione Forms per effettuare la conversione automatica nel nuovo percorso.</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/adhocassetshare</code></td>
   <td><code>/libs/settings/dam/adhocassetshare</code></td>
   <td>locatario</td>
   <td>Le strutture di contenuto precedenti vengono rispettate con una priorità maggiore rispetto a quelle nuove OOOTB.</td>
   <td>Le personalizzazioni a livello di progetto devono essere tagliate e incollate nei percorsi <code>/apps</code> o <code>/conf</code> percorsi equivalenti, a seconda dei casi.</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/workflow/notification/email/downloadasset</code></td>
   <td><code>/libs/settings/dam/workflow</code></td>
   <td>locatario</td>
   <td>Le strutture di contenuto precedenti vengono rispettate con una priorità maggiore rispetto a quelle nuove OOOTB.</td>
   <td>Le personalizzazioni a livello di progetto devono essere tagliate e incollate nei percorsi <code>/apps</code> o <code>/conf</code> percorsi equivalenti, a seconda dei casi.</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/drm/licenses/</code></td>
   <td><code>/libs/settings/dam/drm</code></td>
   <td>non in base al contesto</td>
   <td>Le strutture di contenuto precedenti vengono rispettate con una priorità maggiore rispetto a quelle nuove OOOTB.</td>
   <td>Le personalizzazioni a livello di progetto devono essere tagliate e incollate nei percorsi <code>/apps</code> o <code>/conf</code> percorsi equivalenti, a seconda dei casi.</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/indesign/scripts</code></td>
   <td><code>/libs/settings/dam/indesign</code></td>
   <td>locatario</td>
   <td>Le strutture di contenuto precedenti vengono rispettate con una priorità maggiore rispetto a quelle nuove OOOTB.</td>
   <td><p>Le personalizzazioni a livello di progetto devono essere tagliate e incollate nei percorsi <code>/apps</code> o <code>/conf</code> percorsi equivalenti, a seconda dei casi.</p> <p>Durante il flusso di lavoro di inserimento risorse personalizzato, nella configurazione del processo di estrazione file multimediali potrebbero ancora esistere riferimenti alla vecchia posizione in /etc. Oltre a spostare gli script fuori da /etc ai percorsi /apps e /conf equivalenti, gli argomenti del processo di estrazione file multimediali personalizzati devono essere modificati da percorsi assoluti a percorsi relativi, in modo da adattarli alle modifiche.</p> <p>Per ulteriori informazioni, consultate <a href="https://helpx.adobe.com/experience-manager/6-2/help/assets/indesign.html">questa pagina</a>.</p> <p> </p> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/video</code></td>
   <td><code>/libs/settings/dam/video</code></td>
   <td>locatario</td>
   <td>Le strutture di contenuto precedenti vengono rispettate con una priorità maggiore rispetto a quelle nuove e preconfigurate.</td>
   <td>Le personalizzazioni a livello di progetto devono essere tagliate e incollate nei percorsi <code>/apps</code> o <code>/conf</code> percorsi equivalenti, a seconda dei casi.</td>
  </tr>
  <tr>
   <td>Tutti i bundle </td>
   <td><code>/etc/notification/email/default</code></td>
   <td><code>/libs/settings/dam/notification</code></td>
   <td>locatario</td>
   <td>Le strutture di contenuto precedenti vengono rispettate con una priorità maggiore rispetto a quelle nuove e preconfigurate.</td>
   <td>Le personalizzazioni a livello di progetto devono essere tagliate e incollate nei percorsi <code>/apps</code> o <code>/conf</code> percorsi equivalenti, a seconda dei casi.</td>
  </tr>
  <tr>
   <td>AEM Sites / AEM Assets</td>
   <td><code>/etc/designs</code> </td>
   <td><code>/libs/settings/wcm/designs</code></td>
   <td>non in base al contesto</td>
   <td><p>I servizi di consumo sono a conoscenza della vecchia posizione.</p> <p>Vengono considerate le configurazioni dalla posizione precedente</p> </td>
   <td><br /> Sposta il contenuto personalizzato da <code>/etc/design</code> a <code>/apps/settings/wcm/design</code> per l'allineamento con la nuova struttura del repository. In futuro, prendete in considerazione l'aggiornamento dei siti per utilizzare la funzionalità di modelli modificabili, che sostituisce la necessità della modalità di progettazione e quindi di questo contenuto.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/scaffolding</code></td>
   <td><p><code>/libs/settings/wcm/template-types/scaffolding/scaffolding</code></p> <p><code>/apps/settings/wcm/template-types/scaffolding/scaffolding</code></p> </td>
   <td>non sensibile al contesto</td>
   <td>I componenti nella vecchia posizione in <code>/etc/scaffolding</code> continueranno a funzionare, ma sono stati ritirati.</td>
   <td>Adobe consiglia di usare i nuovi componenti di scaffolding nella nuova posizione.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/blueprints</code></td>
   <td><p>/libs/msm per le configurazioni di blueprint out-of-the-box Screens e Commerce</p> <p> </p> </td>
   <td>non in base al contesto</td>
   <td><p>I Servizi di consumo sono a conoscenza della vecchia posizione.</p> <p>Vengono considerate le configurazioni dalla posizione precedente.</p> </td>
   <td>Le configurazioni devono essere copiate nelle nuove posizioni.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/mobile</code></td>
   <td><code>/libs/settings/mobile</code></td>
   <td>locatario</td>
   <td>La funzione utilizza Configuration Manager e supporta comunque la vecchia posizione come fallback.</td>
   <td>
    <ol>
     <li>Ricolloca le configurazioni da <code>/etc</code> a <code>/conf/&lt;tenant&gt;/settings/mobile</code></li>
     <li>Quindi, aggiornate il riferimento nel contenuto come segue:</li>
    </ol> <p><code>/content/&lt;tenant&gt;/jcr:content/cq:deviceGroups{String[]}=mobile/groups/responsive</code></p> </td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/msm/rolloutConfigs</code></td>
   <td><code>/libs/msm/wcm/rolloutconfigs</code></td>
   <td>N/D</td>
   <td><p>I servizi di consumo sono a conoscenza della vecchia posizione.</p> <p>Se vengono rilevate configurazioni nel percorso legacy, queste verranno utilizzate.</p> </td>
   <td>Per allineare con il nuovo modello, le configurazioni devono essere create nelle nuove posizioni e quelle precedenti in <code>/etc</code> devono essere eliminate.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/segmentation/contexthub</code></td>
   <td><code>/conf/we-retail/settings/wcm/segments</code></td>
   <td>locatario</td>
   <td><p>Segmenti dalla posizione precedente:</p>
    <ul>
     <li>Rimanete in modalità di sola lettura nella console dell'audience.</li>
     <li>È ancora caricato sulla pagina (se il percorso specificato è selezionato in Proprietà <strong>pagina &gt; Personalizzazione &gt; Percorso</strong>segmenti).</li>
     <li>Può essere utilizzato per il targeting del contenuto.</li>
    </ul> </td>
   <td>Puoi usare lo strumento <a href="/help/sites-deploying/upgrading-code-and-customizations.md#migrateconfigurations">di migrazione dei</a> segmenti per effettuare la migrazione alla nuova posizione.</td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/social/config/languageOpts</code></td>
   <td><code>/libs/social/translation/languageOpts</code></td>
   <td>N/D</td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/templates</code></td>
   <td><code>/libs/settings/community/templates</code></td>
   <td> </td>
   <td><p>Il codice è a conoscenza della posizione del modello precedente. I modelli esistenti continueranno a essere citati e a essere letti/scritti da <code>/etc</code>.</p> <p><br /> Per i modelli e-mail, se il cliente aveva già i propri modelli personalizzati in un altro percorso configurando il percorso principale <strong></strong> Modelli in Configurazione <strong>risposta e-mail di</strong> AEM Communities, il percorso rimarrà invariato.</p> </td>
   <td><p>Un'utilità <a href="https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration" target="_blank">di</a> migrazione può allineare i modelli più recenti di AEM Communities.</p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/badging</code></td>
   <td><p><strong>Regole di badge:</strong></p> <p><code>/libs/settings/community/badging</code></p> <p><strong>Immagini badge:</strong></p> <p>Le immagini incluse nella vecchia posizione nella casella <code>/etc/community/badging/images</code> vengono spostate in <code>/libs/community/badging/images </code> </p> <p> </p> <p>Le immagini personalizzate vengono spostate in <code>/content/community/badging/images</code>.</p> <p> </p> </td>
   <td>locatario</td>
   <td><p>Il codice è a conoscenza dei vecchi percorsi di contrassegno.</p> <p><br /> Controllerà prima l'esistenza di percorsi<br /> meno recenti. Se non sono presenti, utilizzeranno i nuovi percorsi.</p> </td>
   <td><p>La migrazione manuale è necessaria per l'allineamento al modello più recente. Per ottenere questo risultato, effettuate le seguenti operazioni:</p>
    <ol>
     <li>Creare un bucket del contesto del sito utilizzando il browser di configurazione in <strong>Strumenti</strong></li>
     <li>Vai alla directory principale del sito</li>
     <li>Impostare la <code>cq:conf</code> proprietà sul percorso del bucket in cui si desidera memorizzare tutte le configurazioni. Lo stesso può essere impostato tramite la procedura guidata di modifica <strong>del sito - Imposta input</strong>configurazione cloud, quindi salvare le modifiche</li>
     <li>Sposta le regole di contrassegno e di punteggio pertinenti dal bucket <code>etc/community/*</code> del contesto del sito creato nel passaggio precedente</li>
     <li>Regolare le proprietà <code>badgingRules</code> e <code>scoringRules</code> le proprietà nella directory principale del sito in modo da disporre di riferimenti relativi alle nuove posizioni delle regole. Ad esempio, se <code>cq:conf</code> è impostato su <code>/conf/we-retail</code>, il valore di <code>badgingRules</code> sarà <code>community/badging/rules</code> se le regole vengono spostate in questo nuovo bucket</li>
     <li>Analogamente, regolare i riferimenti alle regole di punteggio in un nodo di regola di contrassegno per avere un percorso relativo.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><p><code>/etc/cloudservices/facebookconnect</code></p> <p><code>/etc/cloudservices/twitterconnect</code></p> <p><code>/etc/cloudservices/pinterestconnect</code></p> </td>
   <td><p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/facebookconnect</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/twitterconnect</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/pinterestconnect</code></p> </td>
   <td>locatario</td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/scoring</code></td>
   <td><code>/libs/settings/community/scoring</code></td>
   <td> </td>
   <td><p>Il codice è a conoscenza dei vecchi percorsi di contrassegno.</p> <p><br /> Controllerà prima l'esistenza di percorsi<br /> meno recenti. Se non sono presenti, utilizzeranno i nuovi percorsi.</p> </td>
   <td><p>I passaggi di migrazione manuale sono necessari per l'allineamento con il modello più recente.</p> <p>I passaggi sono gli stessi nelle regole di contrassegno riportate sopra.</p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/notifications</code></td>
   <td><code>/libs/settings/community/notifications</code></td>
   <td>non in base al contesto</td>
   <td><p>Queste configurazioni non sono compatibili con le versioni precedenti. Per informazioni su come eseguire la migrazione alle nuove posizioni, vedere la colonna "Requisiti per l'allineamento all'ultimo modello".<br /> </p> <br /> </td>
   <td><p>Per l'allineamento all'ultimo modello è necessaria una migrazione manuale. È possibile utilizzare Granite Configuration Manager per spostare le configurazioni nel nuovo percorso in <code>/apps/settings</code>.</p> <p>Pertanto, è necessario impostare la <code>mergeList</code> proprietà su true sul <code>/libs/settings/community/subscriptions</code> nodo, quindi aggiungere un nodo <code>nt:unstructured</code> secondario.<br /> </p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/subscriptions</code></td>
   <td><code>/libs/settings/community/subscriptions</code></td>
   <td>non in base al contesto</td>
   <td>Queste configurazioni non sono compatibili con le versioni precedenti. Per informazioni su come eseguire la migrazione alle nuove posizioni, vedere la colonna "Requisiti per l'allineamento all'ultimo modello".</td>
   <td><p>Per l'allineamento all'ultimo modello è necessaria una migrazione manuale. È possibile utilizzare Granite Configuration Manager per spostare le configurazioni nel nuovo percorso in <code>/apps/settings</code>.</p> <p>Pertanto, è necessario impostare la <code>mergeList</code> proprietà su true sul <code>/libs/settings/community/subscriptions</code> nodo, quindi aggiungere un nodo <code>nt:unstructured</code> secondario.</p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/socialconfig/srpc/defaultconfiguration</code></td>
   <td><code>/conf/global/settings/community/srpc/defaultconfiguration</code></td>
   <td>globale</td>
   <td>Queste configurazioni sono compatibili con le versioni precedenti. Se i percorsi precedenti vengono rilevati, verranno utilizzati. In caso contrario, i nuovi percorsi avranno la precedenza.</td>
   <td><p>L’attività di migrazione dei contenuti pigri è disponibile sotto forma di <code>CQ64CommunitiesConfigsCleanupTask</code>.</p> <p>Per ulteriori informazioni, consulta la documentazione <a href="/help/sites-deploying/lazy-content-migration.md" target="_blank">sulla migrazione a</a>Lazy.</p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/watchwords</code></td>
   <td><code>/libs/community/watchwords</code></td>
   <td>N/D</td>
   <td>Queste configurazioni sono compatibili con le versioni precedenti. Se i percorsi precedenti vengono rilevati, verranno utilizzati. In caso contrario, i nuovi percorsi avranno la precedenza.</td>
   <td><p>L’attività di migrazione dei contenuti pigri è disponibile sotto forma di <code>CQ64CommunitiesConfigsCleanupTask</code>.</p> <p>Le parole di controllo dovranno essere spostate manualmente da <code>/etc/watchwords</code> a <code>/conf/global/settings/community/watchwords</code>.</p> </td>
  </tr>
  <tr>
   <td>Tutti i bundle </td>
   <td><code>/etc/workflow/models</code></td>
   <td><p><code>/libs/settings/workflow/models</code></p> <p><code>/conf/global/settings/workflow/models</code> </p> <p><code>/var/workflow/models</code></p> </td>
   <td>globale</td>
   <td><p>La posizione legacy viene utilizzata se presente e non esiste alcuna configurazione in <code>/libs</code> o <code>/conf</code>.</p> <p>Quando modificate i modelli di flusso di lavoro OOTB, le sovrapposizioni in base al contesto devono essere create in <code>/conf</code> per poter essere modificate.</p> <p>L'esportazione del pacchetto deve includere il modello in <code>/libs</code> o <code>/conf</code> e il modello di runtime in <code>/var/workflow/models.</code></p> </td>
   <td><p>I modelli appena creati verranno creati nel <code>/conf/global/settings</code> percorso.</p> <p>Eventuali modifiche apportate <code>/etc</code> o che <code>/libs</code> richiedono la creazione esplicita di un override <code>/conf/global/settings</code> prima di procedere alla modifica. Il pulsante Modifica deve essere selezionato e l'override in verrà creato <code>/conf</code> e la modifica sarà consentita.</p> </td>
  </tr>
  <tr>
   <td>Tutti i bundle </td>
   <td><code>/etc/workflow/launcher</code></td>
   <td><p><code>/libs/settings/workflow/launcher</code></p> <p><code>/conf/global/settings/workflow/launcher</code></p> </td>
   <td>globale</td>
   <td>La posizione legacy viene utilizzata se presente e non esiste alcuna configurazione<br /> in <code>/libs</code> o <code>/conf</code> posizioni. In questo modo, vengono mantenuti i avviatori personalizzati.</td>
   <td><p>Le nuove configurazioni del modulo di avvio creato o modificato si trovano nella <code>/conf</code> posizione.</p> <p>Tutti i avviatori devono essere spostati dal percorso legacy <code>/etc</code> a<code> /conf/global/settings/workflow/launcher.</code></p> </td>
  </tr>
  <tr>
   <td>Tutti i bundle </td>
   <td><code>/etc/workflow/models</code></td>
   <td><p><code>/libs/settings/workflow/models</code></p> <p><code>/conf/global/settings/workflow/models</code></p> </td>
   <td>globale</td>
   <td>La posizione legacy viene utilizzata se presente e non esiste alcuna configurazione<br /> in <code>/libs</code> o <code>/conf</code> posizioni. In questo modo, i modelli di flusso di lavoro personalizzati vengono mantenuti.</td>
   <td><p>Tutti i modelli di workflow devono essere spostati dal <code>/etc</code> percorso legacy a <code>/conf/global/settings/workflow/models</code>.</p> <p> </p> </td>
  </tr>
  <tr>
   <td>Tutti i bundle </td>
   <td><code>/etc/workflow/notification</code></td>
   <td><p><code>/libs/settings/workflow/notification</code></p> <p><code>/conf/global/settings/workflow/notification</code></p> </td>
   <td>non in base al contesto</td>
   <td><p>Per la compatibilità con le versioni precedenti, se presente viene utilizzata la posizione precedente.</p> <p>Precedentemente, i modelli forniti dovevano essere sostituiti modificandoli in <code>/etc</code>. Ora, l'override deve essere memorizzato in <code>/conf/global</code>.</p> </td>
   <td>Per ulteriori informazioni, consulta la documentazione Flusso di lavoro.<br /> </td>
  </tr>
  <tr>
   <td>Tutti i bundle </td>
   <td><code>/etc/cloudservices/translation</code></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/translationcfg</code></p> <p> </p> </td>
   <td>locatario</td>
   <td>Servizi cloud legacy. Verrà mantenuta su una configurazione aggiornata locale. Il codice per elencarli e leggerli è ancora presente nel prodotto come fallback.</td>
   <td><p>Per spostare le configurazioni cloud in <code>/conf</code>, potete:</p>
    <ul>
     <li>Crea configurazioni utilizzando la nuova interfaccia<br /> touch o<br /> </li>
     <li>Copiare le configurazioni da <code>/etc/cloudservices/translation</code> alle rispettive nuove posizioni</li>
    </ul> <p>Al termine, le configurazioni devono essere associate a Siti tramite <strong>Siti &gt; Proprietà</strong> nell'interfaccia utente.</p> <p><em>Nota: Affinché questo funzioni, i connettori di conversione devono essere compatibili con AEM 6.5.</em></p> </td>
  </tr>
  <tr>
   <td>Tutti i bundle </td>
   <td><code>/etc/cloudservices/msft-translation</code></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/msft-translation</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/msft-translation</code></p> </td>
   <td>locatario</td>
   <td>Servizi cloud legacy. Verrà mantenuta su una configurazione aggiornata locale. Il codice per elencarli e leggerli è ancora presente nel prodotto come fallback.</td>
   <td><p>Per spostare le configurazioni cloud in <code>/conf</code>, potete:</p>
    <ul>
     <li>Crea configurazioni utilizzando la nuova interfaccia touch o<br /> </li>
     <li>Copiare le configurazioni meno recenti <code>/etc/cloudservices/translation</code> nelle rispettive nuove posizioni</li>
    </ul> <p>Al termine, le configurazioni devono essere associate a Siti tramite <strong>Siti &gt; Proprietà</strong> nell'interfaccia utente.</p> </td>
  </tr>
  <tr>
   <td>Tutti i bundle </td>
   <td><code>/etc/cloudsettings</code></td>
   <td><p><code>/libs/settings/cloudsettings</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudsettings</code></p> </td>
   <td>locatario</td>
   <td><p>Le voci esistenti in <code>/etc</code> questione rimangono invariate al momento dell'aggiornamento dell'istanza.</p> <p>L'accesso all'interfaccia utente delle impostazioni cloud dopo l'aggiornamento copierà le impostazioni cloud esistenti nella nuova struttura del repository, preservando al contempo il contenuto esistente per la compatibilità con le versioni precedenti.</p> </td>
   <td><p>I modelli di contenuto sono identici, solo la posizione è stata modificata per essere allineata alle configurazioni in base al contesto.</p> <p>L’attività <a href="/help/sites-deploying/lazy-content-migration.md">di migrazione</a> Lazy relativa a queste impostazioni cloud esegue le azioni seguenti:</p>
    <ul>
     <li>Copia impostazioni cloud esistenti in <code>/etc/cloudsettings</code> in <code>/conf/global/settings/cloudsettings</code></li>
     <li>Rimuovi tutti gli elementi secondari di <code>/etc/cloudsettings</code></li>
    </ul> <p>Sono tuttavia necessari passaggi manuali dopo l’aggiornamento e prima di eseguire le attività di migrazione pigra:</p>
    <ul>
     <li>Tutti i riferimenti a <code>/etc/cloudsettings/*</code> cui si fa riferimento devono essere aggiornati per indicare <code>/conf/global</code></li>
    </ul> <p>Caveat:</p>
    <ul>
     <li>Il <code>/etc/cloudsettings</code> contenitore deve essere mantenuto</li>
    </ul> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/cloudservices/dmscene7</code></td>
   <td><code>/conf/global/settings/cloudservices/dmscene7</code></td>
   <td>Solo globale</td>
   <td><p>La configurazione cloud per la configurazione Dynamic Media - Scene7 (<code>dynamicmedia_scene7</code> modalità di esecuzione) rimarrà nello stesso percorso. Il processo funziona così. Per regolare il valore di configurazione cloud, sono disponibili due opzioni:</p>
    <ol>
     <li>Aggiornare una configurazione esistente tramite la vecchia interfaccia utente di configurazione cloud.</li>
     <li>Crea una nuova configurazione cloud tramite la nuova interfaccia utente touch. Questo avrà precedenza maggiore rispetto a quello precedente.</li>
    </ol> </td>
   <td><p>Per allineare l'ultimo modello, è necessario eseguire lo script che si trova in:</p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/presets/viewer</code></td>
   <td><p><code>/libs/settings/dam/dm/presets/viewer</code></p> <p><code>/conf/global/settings/dam/dm/presets/viewer</code></p> </td>
   <td>Solo globale</td>
   <td><p>I predefiniti per visualizzatori OOOTB saranno disponibili solo nella nuova posizione, mentre il predefinito per visualizzatori personalizzato resterà disponibile <code>/etc</code> fino a quando non verrà apportata una modifica.</p> <p>Dopo la modifica, verrà salvata nella nuova posizione tramite Lazy Migration. Il server immagini incorporato esaminerà sia il percorso legacy che il nuovo percorso dopo aver ricevuto una richiesta. Pertanto, non è necessario modificarne il codice da incorporare o l'URL.</p> </td>
   <td><p>Il predefinito per visualizzatori preimpostato sarà disponibile solo nella nuova posizione. Per il predefinito per visualizzatori personalizzato, è necessario eseguire lo script di migrazione nel seguente percorso:</p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> <p>Simile al caso di compatibilità con le versioni precedenti, non è necessario regolare il codice copyURL/embed in modo che punti a <code>/conf</code>. La richiesta esistente da <code>/etc</code> indirizzare sotto il cofano al contenuto corretto da <code>/conf</code>.</p> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/imageserver/macros</code></td>
   <td><code>/conf/global/settings/dam/dm/presets/macro</code></td>
   <td>Solo globale</td>
   <td>La macro sotto <code>/etc</code> è ancora valida. Se lo modificate, il nodo modificato verrà spostato nella nuova posizione in <code>/conf</code> tramite un'attività di migrazione Lazy.</td>
   <td><p>È necessario eseguire lo script di migrazione nel seguente percorso:</p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> <p> </p> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/video/dynamicmedia/Adaptive Video Encoding</code></td>
   <td><code>/libs/settings/dam/dm/presets/video/jcr:content/Adaptive Video Encoding</code></td>
   <td>N/D</td>
   <td><p>Il profilo video out-of-the-box verrà rimosso senza aggiornare la proprietà delle cartelle di risorse per il collegamento al profilo.</p> <p>Il processo di codifica prevede una traduzione integrata tra la posizione precedente e quella nuova. Convertirà il vecchio percorso per cercare nel nuovo percorso profilo.</p> </td>
   <td>Nessuna modifica richiesta.</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/video/dynamicmedia</code></td>
   <td><code>/conf/global/settings/dam/dm/presets/video/jcr:content</code></td>
   <td>Solo globale</td>
   <td><p>Il profilo video personalizzato viene mantenuto invariato fino a quando non viene modificato.</p> <p>Quindi verrà spostato nella nuova posizione tramite un'attività di migrazione Lazy. Simile al predefinito video preimpostato per la ricerca sulla codifica. Il processo di codifica include un convertitore di percorsi integrato che consente di esaminare prima la vecchia posizione e quindi la nuova posizione per il profilo video.</p> </td>
   <td><p>Per allineare l'ultimo modello, è possibile eseguire lo script di migrazione in:</p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> <p> </p> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/cloudservices/dynamicmediaservices</code></td>
   <td><code>/conf/global/settings/dam/dm/cloudservices/dynamicmediaservices</code></td>
   <td>Solo globale</td>
   <td><p>Questa configurazione cloud per la configurazione ibrida Dynamic Media (<code>dynamicmedia</code> modalità di esecuzione) rimarrà nello stesso percorso. Il processo funziona così. Se è necessario regolare il valore di configurazione, è possibile farlo in due modi.</p>
    <ol>
     <li>Aggiornare una configurazione esistente tramite la vecchia interfaccia utente di configurazione cloud.</li>
     <li>Crea una nuova configurazione cloud tramite la nuova interfaccia utente touch. Questo avrà precedenza maggiore rispetto a quello precedente.</li>
    </ol> </td>
   <td><p>È necessario eseguire lo script di migrazione per allinearlo al modello più recente. Lo script si trova nel percorso seguente:<br /> </p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/cloudservices/youtube</code></td>
   <td><code>/libs/settings/dam/dm/youtube</code></td>
   <td>Solo globale</td>
   <td><p>La configurazione cloud per la configurazione DM-Youtube rimarrà nello stesso luogo. Il processo funziona così. Se è necessario regolare il valore di configurazione cloud, è possibile farlo in due modi:</p>
    <ol>
     <li>Aggiornare una configurazione esistente tramite la vecchia interfaccia utente di configurazione cloud.</li>
     <li>Crea una nuova configurazione cloud tramite la nuova interfaccia utente touch. Questo avrà precedenza maggiore rispetto a quello precedente.</li>
    </ol> </td>
   <td><p>È possibile eseguire uno script di migrazione per l'allineamento con il modello più recente. Lo script si trova nel seguente percorso:<br /> </p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p> </p> <p> </p> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/presets/analytics</code></td>
   <td><code>/libs/settings/dam/dm/analytics</code></td>
   <td>Solo globale</td>
   <td>Nessuna azione richiesta.</td>
   <td><p>È possibile eseguire uno script di migrazione per l'allineamento alla modalità più recente. Lo script si trova nel seguente percorso:<br /> </p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> </td>
  </tr>
  <tr>
   <td>Tutti i bundle </td>
   <td><p><code>/etc/notification/email/default/com.day.cq.replication</code></p> <p><code>/etc/notification/email/default/com.day.cq.wcm.core.page</code></p> </td>
   <td><code>/libs/settings/notification-templates</code></td>
   <td>Solo globale</td>
   <td>I modelli in <code>/etc/notification/email/default/</code> hanno la precedenza su quelli in <code>/libs/settings/notification-templates</code>.</td>
   <td>Per allineare l'ultimo modello, potete creare nuovi modelli in <code>/apps/settings/notification-templates</code> e apportare nuove modifiche.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><p><code>/etc/msm/rolloutconfigs/launch</code></p> <p><code>/etc/msm/rolloutconfigs/pushonmodifyshallow</code></p> </td>
   <td><p><code>/libs/msm/launches/rolloutconfigs/launch</code></p> <p><code>/libs/msm/launches/rolloutconfigs/pushonmodifyshallow</code></p> </td>
   <td>N/D</td>
   <td><p>I Servizi di consumo sono a conoscenza della vecchia posizione.</p> <p>Se vengono rilevate configurazioni nel percorso legacy, queste verranno utilizzate.</p> </td>
   <td>Per allineare con il nuovo modello, le configurazioni devono essere create nelle nuove posizioni e quelle precedenti in <code>/etc</code> devono essere eliminate.</td>
  </tr>
  <tr>
   <td>Tutti i bundle </td>
   <td><code>/etc/translation/supportedLanguages</code></td>
   <td><p><code>/libs/settings/translation/supportedLanguages</code></p> <p><code>/apps/settings/translation/supportedLanguages</code></p> </td>
   <td>non in base al contesto</td>
   <td>Un avvertimento è che le lingue personalizzate devono essere aggiunte all'elenco.<br /> </td>
   <td>Sovrapponi e aggiorna il nuovo elenco con eventuali altre lingue. In alternativa, anche la copia del vecchio elenco nella <code>/apps</code> posizione potrebbe funzionare.</td>
  </tr>
  <tr>
   <td>Tutti i bundle </td>
   <td><code>/etc/workflow/models/translation/translation_rules.xml</code></td>
   <td><p><code>/libs/settings/translation/rules/translation_rules.xml</code></p> <p><code>/apps/settings/translation/rules/translation_rules.xml</code></p> <p><code>/conf/global/settings/translation/rules/translation_rules.xml</code></p> </td>
   <td>Solo globale</td>
   <td>Verrà mantenuta su una configurazione aggiornata locale. Codice per elencarli e leggerli ancora presenti nel prodotto.</td>
   <td>Per mantenere le modifiche, copiate il file XML da <code>/etc</code> a <code>/libs</code> o <code>/conf</code>. In alternativa,<strong> </strong>rimuovere il file da <code>/etc</code>.</td>
  </tr>
 </tbody>
</table>

## Librerie lato client {#client-side-libraries}

[Le librerie](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/clientlibs.html) lato client sono codice JavaScript e CSS elaborati nel browser.

### Strategia di estensibilità {#extensibility-strategy-1}

AEM fornisce un framework di estensibilità per aggiungere più file JavaScript. Eventuali file con la stessa proprietà &quot;category&quot; verranno aggiunti in coda, consentendo al codice personalizzato di estendere il codice AEM che si trova in `/libs`.

<table>
 <tbody>
  <tr>
   <td><strong>Soluzione</strong></td>
   <td><strong>Posizione precedente</strong><br /> </td>
   <td><strong>Nuova posizione</strong></td>
   <td><strong>Metodo di compatibilità con le versioni precedenti</strong></td>
   <td><strong>Requisiti per l'allineamento all'ultimo modello</strong></td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/clientlibs/fd/fp</code></td>
   <td><code>/libs/fd/fp/components</code></td>
   <td><p>clientlib precedenti che verranno persistenti in un'istanza aggiornata tramite un aggiornamento locale.</p> <p>I nuovi clientlibs hanno gli stessi nomi di categoria insieme alla proprietà "<strong><code>replaces</code></strong>" per evitare l'unione di vecchi e nuovi clientlibs.</p> </td>
   <td>Nessuna azione richiesta.</td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/clientlibs/fd/rte</code></td>
   <td><code>/libs/fd/rte</code></td>
   <td><p>clientlibs legacy che verranno memorizzati in un'istanza aggiornata tramite un aggiornamento locale.</p> <p>I nuovi clientlibs hanno gli stessi nomi di categoria insieme alla proprietà "<strong><code>replaces</code></strong>" per evitare l'unione di vecchi e nuovi clientlibs.</p> </td>
   <td>Nessuna azione richiesta.</td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/clientlibs/fd/af</code></td>
   <td><code>/libs/fd/af/authoring/clientlibs</code></td>
   <td>clientlibs legacy. Sarà persistente in un'istanza aggiornata tramite un aggiornamento locale. I nuovi clientlibs hanno gli stessi nomi di categoria insieme alla proprietà "<strong><code>replaces</code></strong>" per evitare l'unione di vecchi e nuovi clientlibs.</td>
   <td>Nessuna azione richiesta.</td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/clientlibs/fd/themes/themeLibrary</code></td>
   <td>Questa funzione non è più disponibile come parte del pacchetto AEM 6.5.</td>
   <td><p>Temi predefiniti in Moduli adattivi.</p> <p>Verrà mantenuta su una configurazione aggiornata locale.</p> </td>
   <td>Si tratta in parte di contenuto generato dall’utente. Questo verrà distribuito come pacchetto di contenuto di riferimento con il <code>aem-forms-reference-themes</code> nome.</td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/clientlibs/fd/expeditor</code></td>
   <td><code>/libs/fd/expeditor/clientlibs</code></td>
   <td>clientlibs legacy. Sarà persistente in un'istanza aggiornata tramite un aggiornamento locale. I nuovi clientlibs hanno gli stessi nomi di categoria insieme alla proprietà "<strong><code>replaces</code></strong>" per evitare l'unione di vecchi e nuovi clientlibs.</td>
   <td>Nessuna azione richiesta.<p> </p> </td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/clientlibs/fd/fmaddon</code></td>
   <td><code>/libs/fd/fmaddon</code></td>
   <td>Client Analytics e Target legacy che non devono essere utilizzati direttamente. </td>
   <td>È stato ripulito dopo l’aggiornamento utilizzando un filtro di pulizia.</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><p><code>/etc/clientlibs/foundation/asseteditor</code></p> <p><code>/etc/clientlibs/foundation/assetshare</code></p> <p><code>/etc/clientlibs/foundation/assetinsights</code></p> </td>
   <td><code>/libs/dam/clientlibs</code></td>
   <td>I clientlibs legacy hanno nomi di categoria cliente diversi.</td>
   <td>Nessuna azione richiesta.</td>
  </tr>
  <tr>
   <td> </td>
   <td><code>/etc/clientlibs/ckeditor</code></td>
   <td><code>/libs/clientlibs/ckeditor</code></td>
   <td>Questi sono clientlibs legacy. Saranno mantenute in una configurazione aggiornata locale. I nuovi clientlibs hanno gli stessi nomi di categoria insieme alla proprietà "<code>replaces</code>" per evitare l'unione di vecchi e nuovi clientlibs.</td>
   <td>Nessuna azione richiesta.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/foundation/sitecatalyst</code></td>
   <td><code>/libs/cq/analytics/clientlibs/analytics</code></td>
   <td><p>Questi sono clientlibs legacy. Verrà mantenuta su una configurazione aggiornata locale.</p> <p>I nuovi clientlibs hanno gli stessi nomi di categoria.</p> </td>
   <td>Nessuna azione richiesta.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/foundation/personalization</code></td>
   <td><code>/libs/cq/personalization/clientlibs/personalization</code></td>
   <td><p>Questi sono clientlibs legacy. Verrà mantenuta su una configurazione aggiornata locale.</p> <p>I nuovi clientlibs hanno gli stessi nomi di categoria.</p> </td>
   <td>Nessuna azione richiesta.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/foundation/searchpromote</code></td>
   <td><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></td>
   <td><p>Questi sono clientlibs legacy. Verrà mantenuta su una configurazione aggiornata locale.</p> <p>I nuovi clientlibs hanno gli stessi nomi di categoria</p> </td>
   <td>Nessuna azione richiesta.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/foundation/target</code></td>
   <td><code>/libs/cq/target/clientlibs/target</code></td>
   <td><p>Questi sono clientlibs legacy. Verrà mantenuta su una configurazione aggiornata locale.</p> <p>I nuovi clientlibs hanno gli stessi nomi di categoria.</p> </td>
   <td>Nessuna azione richiesta.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/address</code></td>
   <td><code>/libs/cq/address/clientlibs</code></td>
   <td>I nuovi clientlibs hanno gli stessi nomi di categoria.</td>
   <td>Nessuna azione richiesta.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/wcm/foundation</code></td>
   <td><code>/libs/wcm/foundation/clientlibs</code></td>
   <td>clientlibs legacy. Verrà mantenuta su una configurazione aggiornata locale. I nuovi clientlibs hanno gli stessi nomi di categoria insieme alla proprietà "<strong>replace</strong>" per evitare l'unione di vecchi e nuovi clientlibs.</td>
   <td>Nessuna azione richiesta.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/wcm/foundation/grid/grid_base.less</code></td>
   <td><p><code>/libs/wcm/foundation/clientlibs/grid/grid_base.less</code></p> </td>
   <td><p>In un aggiornamento locale il file legacy (/etc/clientlibs/wcm/..._) rimarrà e non verrà rimosso automaticamente, pertanto i riferimenti alla versione precedente /etc/clientlibs/wcm/foundation/grid/grid_base.less continueranno a essere soddisfatti.</p> <p><em>Si noti che il file is è un caso anomalo in cui a questo file LESS viene fatto riferimento dal percorso assoluto tramite istruzioni LESS @import e NOT per categoria clientlib.</em></p> <p>Se il cliente MENO che fa riferimento a "grid_base.less" sta puntando a un file non esistente, la modalità di layout dei modelli modificabili si interrompe e eventuali regolazioni effettuate con esso non saranno presenti (ad es. tutti i componenti avranno la larghezza totale della pagina).</p> </td>
   <td>Aggiorna tutti i riferimenti nel codice personalizzato (ad esempio in qualsiasi file LESS che faccia riferimento al file grid_base.less spostato) in modo che punti alla nuova posizione e rimuova la posizione precedente.</td>
  </tr>
 </tbody>
</table>

Queste sono altre ristrutturazioni che non rientrano nelle sezioni precedenti.

### Strategia di estensibilità {#extensibility-strategy-2}

Vedere ogni riga di tabella per qualsiasi modello di estensibilità supportato. Il contenuto di questa sezione non è in genere esteso.

## Varie {#miscellaneous}

<table>
 <tbody>
  <tr>
   <td><strong>Soluzione</strong></td>
   <td><strong>Posizione precedente</strong><br /> </td>
   <td><strong>Nuova posizione</strong></td>
   <td><strong>Metodo di compatibilità con le versioni precedenti</strong></td>
   <td><strong>Requisiti per l'allineamento all'ultimo modello</strong></td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/designs/fd/fp</code></td>
   <td><code>/libs/fd/fp</code></td>
   <td><p>Modelli OOTB del portale AEM Forms legacy. Questi modelli rimarranno in /etc dopo una configurazione aggiornata sul posto.</p> <p>Nell’elenco dei modelli, al titolo del modello verrà aggiunta la parola<em> "obsoleto</em>" per distinguerli dai modelli più recenti.</p> </td>
   <td>Nessuna azione richiesta.</td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/aep</code></td>
   <td><code>/var/fd/content/annotations</code></td>
   <td>File di annotazione di Gestione corrispondenza legacy. Non deve essere consumato direttamente. Verrà ripulito dopo l'aggiornamento utilizzando un filtro di pulizia.</td>
   <td>Posizione precedente ripulita dopo l’aggiornamento mediante un filtro di pulizia.</td>
  </tr>
  <tr>
   <td>Tutti i bundle </td>
   <td><code>/etc/tags</code></td>
   <td><code>/content/cq:tags</code></td>
   <td>L'API Tag Manager supporta sia la precedente che la nuova posizione. Quando viene avviato il componente OSGi Factory JCR Tag Manager, viene rilevato se è in esecuzione su un'istanza aggiornata o su una versione precedente e utilizza la posizione appropriata.<br /> </td>
   <td><p>Per allineare correttamente il nuovo modello:</p>
    <ol>
     <li>Sostituisce i riferimenti al modello precedente (<code>/etc/tags</code>) con il nuovo (<code>/content/cq:tags</code>) utilizzando la variabile <code>tagID.</code></li>
     <li>Accedere a CRXDE Lite</li>
     <li>Sposta i tag da <code>/etc/tags</code> a <code>/content/cq:tags</code></li>
     <li>Riavviare il componente OSGi <code class="code">com.day.cq.tagging.impl.JcrTagManagerFactoryImpl.
        </code></li>
    </ol> <p> </p> </td>
  </tr>
  <tr>
   <td>Tutti i bundle </td>
   <td><code>/etc/workflow/instances</code></td>
   <td><code>/var/workflow/instances</code></td>
   <td>Posizione legacy utilizzata nell'elaborazione dei<br /> flussi di lavoro in volo. I nuovi flussi di lavoro utilizzano la nuova posizione in <code>/var.</code></td>
   <td>Nessuna azione richiesta.</td>
  </tr>
  <tr>
   <td>Tutti i bundle </td>
   <td><code>/etc/workflow/scripts</code></td>
   <td><p><code>/libs/workflow/scripts</code></p> <p><code>/apps/workflow/scripts</code></p> </td>
   <td><p>I passaggi del modello di flusso di lavoro esistenti che fanno riferimento agli script del flusso di lavoro nella posizione precedente in <code>/etc/workflow/scripts</code> continueranno a puntare a tali script dopo l'aggiornamento ed verranno eseguiti correttamente.</p> <p>Prendete nota dell’interfaccia utente di AEM per la creazione dei passaggi del flusso di lavoro" (Processi, Suddivisioni ecc.) non elenca più gli script <code>/etc/workflow/scripts</code> nel menu a discesa utilizzato select to workflow scripts.</p> </td>
   <td><p>I flussi di lavoro che utilizzano questi script continueranno a funzionare come previsto se il passaggio del processo di workflow associato non venisse modificato in AEM.</p> <p>Tuttavia, per la piena compatibilità con le versioni precedenti, anche quando vengono modificati alcuni passaggi, è necessario un intervento manuale da parte del cliente dopo l'aggiornamento:</p>
    <ul>
     <li>Gli script devono essere spostati da <code>/etc/workflow/scripts</code> a <code>/apps/workflow/scripts.</code></li>
     <li>Eventuali<strong> </strong>riferimenti <code>/etc/workflow/scripts</code> nei passaggi del modello di workflow devono essere aggiornati per fare riferimento alla nuova <code>/apps/workflow/scripts</code> posizione.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Tutti i bundle </td>
   <td><code>/etc/replication/treeactivation</code></td>
   <td><code>/libs/replication/treeactivation</code></td>
   <td>La pagina dell'utilità ClassicUI rimane attiva al momento dell'aggiornamento.</td>
   <td>Nessuna azione richiesta.</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/jobs</code></td>
   <td><code>/var/dam/jobs</code></td>
   <td><p>Posizione temporanea in cui memorizzare i file zip generati per la chiamata di azione di download di Risorse AEM.</p> <p>Non è necessario effettuare l’aggiornamento perché quando il client richiede di scaricare la risorsa, il file verrà generato nella nuova posizione.</p> </td>
   <td>Nessuna azione richiesta.</td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/products</code></td>
   <td><code>/var/commerce/products</code></td>
   <td><p>Il contenuto precedente rimane attivo e utilizzabile dopo l'aggiornamento.</p> <p>È disponibile un’attività di migrazione Lazy per la migrazione alla nuova posizione.</p> </td>
   <td><p>La migrazione viene eseguita tramite un'attività di migrazione Lazy: <code>CQ64CommerceMigrationTask.</code></p> <p>Effettua le seguenti operazioni:</p>
    <ul>
     <li>Regola i riferimenti dalla posizione precedente a quella nuova</li>
     <li>Sposta il contenuto dalla posizione precedente alla nuova posizione</li>
     <li><p>Rimuove la vecchia posizione per attivare l'utilizzo della nuova posizione nell'intero sistema</p> </li>
    </ul> <p>Le posizioni interessate dall'attività sono:</p>
    <ul>
     <li>/etc/commerce/products</li>
     <li>/etc/commerce/collections<br /> </li>
     <li>/etc/commerce/ordered<br /> </li>
     <li>/etc/commerce/payment-methods<br /> </li>
     <li>/etc/commerce/Shipping-methods<br /> </li>
    </ul> <p>Per i cataloghi più grandi, si consiglia di eseguire l’attività di migrazione e-commerce singolarmente trasferendo in AEM la seguente proprietà del sistema Java:</p>
    <ul>
     <li>nome proprietà: <code>com.adobe.upgrade.forcemigration</code></li>
     <li>valore proprietà: <code>com.day.cq.compat.codeupgrade.impl.cq64.CQ64CommerceMigrationTask</code></li>
    </ul> <p>Dopo la migrazione, AEM richiede un riavvio.</p> </td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/orders</code></td>
   <td><code>/var/commerce/orders</code></td>
   <td><p>Il contenuto precedente rimane attivo e utilizzabile dopo l'aggiornamento.</p> <p>È disponibile un’attività di migrazione Lazy per la migrazione alla nuova posizione.</p> </td>
   <td>Consultate la descrizione precedente per <code>/etc/commerce/products</code>.</td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/collections</code></td>
   <td><code>/var/commerce/collections</code></td>
   <td><p>Il contenuto precedente rimane attivo e utilizzabile dopo l'aggiornamento.</p> <p>È disponibile un’attività di migrazione Lazy per la migrazione alla nuova posizione.</p> </td>
   <td>Consultate la descrizione precedente per <code>/etc/commerce/products</code>.</td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/classifications</code></td>
   <td><code>/var/commerce/classifications</code></td>
   <td>Nessuna azione richiesta.</td>
   <td>Nessuna azione richiesta.</td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/shipping-methods</code></td>
   <td><code>/var/commerce/shipping-methods</code></td>
   <td><p>Il contenuto precedente rimane attivo e utilizzabile dopo l'aggiornamento.</p> <p>È disponibile un’attività di migrazione Lazy per la migrazione alla nuova posizione.</p> </td>
   <td>Consultate la descrizione precedente per <code>/etc/commerce/products</code>.</td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/payment-methods</code></td>
   <td><code>/var/commerce/payment-methods</code></td>
   <td><p>Il contenuto precedente rimane attivo e utilizzabile dopo l'aggiornamento.</p> <p>È disponibile un’attività di migrazione Lazy per la migrazione alla nuova posizione.</p> </td>
   <td>Consultate la descrizione precedente per <code>/etc/commerce/products</code>.</td>
  </tr>
  <tr>
   <td>Tutti i bundle </td>
   <td><code>/etc/taskmanagement</code></td>
   <td><code>/var/taskmanagement</code></td>
   <td><p>Nuove attività create in <code>/var/taskmanagement</code></p> <p>Le attività esistenti nella posizione precedente resteranno visibili nella inbox di AEM.</p> </td>
   <td>Nessuna azione richiesta.</td>
  </tr>
  <tr>
   <td>Tutti i bundle </td>
   <td><code>/etc/workflow/packages</code></td>
   <td><code>/var/workflow/packages</code></td>
   <td><p>I pacchetti AEM creati tramite AEM Package Manager sono ancora memorizzati in <code>/etc/workflow/packages.</code></p> <p>Altri pacchetti creati tramite AEM Sites e Workflows continuano a essere memorizzati in<code>/var/workflow/packages.</code></p> <p>I pacchetti trovati in entrambi <code>/etc/workflow/packages</code> e <code>/var/workflow/packages</code> possono essere modificati tramite Gestione pacchetti di AEM. </p> </td>
   <td><p>Nessuna azione richiesta.</p> <p> </p> </td>
  </tr>
  <tr>
   <td>Tutti i bundle </td>
   <td><code>/etc/workflow/instances</code></td>
   <td><code>/var/workflow/instances</code></td>
   <td>Verranno create <code>/var</code> automaticamente nuove istanze del flusso di lavoro.</td>
   <td>Nessuna azione richiesta.</td>
  </tr>
  <tr>
   <td>Tutti i bundle </td>
   <td><code>/etc/commerce/searchpromote</code></td>
   <td><code>/var/cq/searchpromote</code></td>
   <td><p>Nuova posizione per il contenuto di feed Search e Promote.</p> <p>Il vecchio URL continua a funzionare e la richiesta viene inoltrata da ServletFilter alla nuova posizione.</p> </td>
   <td><br /> Nessuna azione richiesta. <br /> </td>
  </tr>
  <tr>
   <td>Tutti i bundle </td>
   <td><code>/etc/dtm-hook</code></td>
   <td><code>/var/cq/dtm/web-hook</code></td>
   <td><p>Nuova posizione per i Web-hooks di DTM.</p> <p>Il vecchio URL continua a funzionare e la richiesta viene inoltrata da ServletFilter alla nuova posizione.</p> </td>
   <td><br /> Nessuna azione richiesta. <br /> </td>
  </tr>
 </tbody>
</table>

