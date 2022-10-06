---
title: Ristrutturazione dell’archivio per AEM Communities nella versione 6.4
seo-title: Repository Restructuring for AEM Communities in 6.4
description: Scopri come apportare le modifiche necessarie per migrare alla nuova struttura dell’archivio in AEM 6.4 per Communities.
seo-description: Learn how to make the necessary changes in order to migrate to the new repository structure in AEM 6.4 for Communities.
uuid: d161655f-4074-44a7-8d69-38e80934c58b
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 7383265b-0ed4-4ea7-b741-0a417d187bdd
feature: Upgrading
exl-id: 4d2bdd45-a29a-4936-b8da-f7e011d81e83
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 3%

---

# Ristrutturazione dell’archivio per AEM Communities nella versione 6.5 {#repository-restructuring-for-aem-communities-in}

Come descritto nell&#39;elemento padre [Ristrutturazione dell’archivio in AEM 6.4](/help/sites-deploying/repository-restructuring.md) I clienti che eseguono l’aggiornamento a AEM 6.5 devono utilizzare questa pagina per valutare lo sforzo di lavoro associato alle modifiche dell’archivio che influiscono sulla soluzione AEM Communities. Alcune modifiche richiedono un lavoro durante il processo di aggiornamento di AEM 6.5, mentre altre possono essere differite fino a un aggiornamento futuro.

**Con aggiornamento alla versione 6.5**

* [Modelli di notifica e-mail](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#e-mail-notification-templates)
* [Configurazioni sottoscrizione](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#subscription-configurations)

**Prima dell’aggiornamento futuro**

* [Configurazioni di badging](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#badging-configurations)
* [Progettazione console di Classic Communities](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#classic-communities-console-designs)
* [Configurazioni di accesso facebook Social](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#facebook-social-login-configurations)
* [Configurazioni opzioni lingua](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#language-options-configurations)

* [Configurazioni di accesso pinterest Social](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#pinterest-social-login-configurations)
* [Configurazioni punteggio](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#scoring-configurations)
* [Configurazioni di accesso twitter Social](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#twitter-social-login-configurations)
* [Varie](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#misc)

## Con aggiornamento alla versione 6.5 {#with-upgrade}

### Modelli di notifica e-mail {#e-mail-notification-templates}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/community/notifications</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><code>/libs/settings/community/notifications</code></td>
  </tr>
  <tr>
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Migrazione manuale tramite necessaria se si desidera passare al nuovo percorso in "<code>/apps/settings</code>". Puoi utilizzare Granite Configuration Manager per eseguire la migrazione.</p> <p>Puoi eseguire la migrazione impostando la proprietà <code>mergeList</code> a <code>true</code> su "<code>/libs/settings/community/subscriptions</code>" nodo e aggiungi un <code>nt:unstructured</code> nodo figlio.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Configurazioni sottoscrizione {#subscription-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/community/subscriptions</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><code>/libs/settings/community/subscriptions</code></td>
  </tr>
  <tr>
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Migrazione manuale tramite necessaria se si desidera passare al nuovo percorso in "<code>/apps/settings</code>". Puoi utilizzare Granite Configuration Manager per eseguire la migrazione.</p> <p>Puoi eseguire la migrazione impostando la proprietà <code>mergeList</code> a <code>true</code> su "<code>/libs/settings/community/subscriptions</code>" nodo e aggiungi un <code>nt:unstructured</code> nodo figlio.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Configurazioni delle parole d’ordine {#watchwords-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td>/etc/watchwords</td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td>/libs/community/watchwords</td>
  </tr>
  <tr>
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td>È disponibile un’attività di migrazione Lazy per ripulire le configurazioni di Communities.<br /> <p>L'attività sposta le parole d'ordine da <code>/etc/watchwords</code> a <code>/conf/global/settings/community/watchwords</code>.</p> <p>Se le parole d'ordine personalizzate sono memorizzate in SCM, devono essere distribuite in <code>/apps/settings/...</code> e devi assicurarti che non ci sia una sovrapposizione <code>/conf/global/settings/...</code> configurazione che avrebbe la precedenza.</p> <p>L’attività di migrazione viene rimossa <code>/etc</code> posizioni.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

## Prima dell’aggiornamento futuro {#prior-to-upgrade}

### Configurazioni di badging {#badging-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/community/badging</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><strong>Regole di badge:</strong></p> <p><code>/libs/settings/community/badging</code></p> <p><strong>Immagini badge:</strong></p> <p>Per le immagini predefinite: <code>/etc/community/badging/images are moved to /libs/community/badging/images</code></p> <p>Per immagini personalizzate: <code>/content/community/badging/images</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>È richiesta la migrazione manuale.</p> <p>Se la tua istanza ha personalizzato le regole di badging/punteggio, non esiste un modo automatico per inserire tutte le regole in un bucket. È necessario specificare i dati dei clienti in base al bucket conf (globale o specifico del sito) che si desidera utilizzare per il sito.</p> <p>Non è disponibile alcuna interfaccia utente per configurare il badging e il punteggio per un sito.</p> <p>Per allineare la nuova struttura del repository:</p>
    <ol>
     <li>Crea un bucket del contesto del sito utilizzando <strong>Browser di configurazione</strong> sotto <strong>Strumenti</strong></li>
     <li>Vai alla directory principale del sito</li>
     <li>Imposta <code>cq:confproperty</code> al percorso del bucket in cui memorizzare tutte le impostazioni. Lo stesso può essere impostato tramite il sito <strong>Modifica guidata - Imposta input configurazione cloud</strong>.</li>
     <li>Sposta regole di badging e regole di punteggio pertinenti da <code>/etc/community/*</code> al bucket del contesto del sito creato nel passaggio precedente.</li>
     <li>Regola le proprietà delle regole di badging e delle regole di punteggio nella directory principale del sito per disporre di riferimenti relativi alle nuove posizioni delle regole.
      <ol>
       <li>Ad esempio, se la proprietà per <code>cq:conf = /conf/we-retail</code>, quindi <code>badgingRules [] = community/badging/rules</code> se le regole vengono ora spostate in questo nuovo bucket.</li>
      </ol> </li>
     <li>Analogamente, regola i riferimenti alle regole di punteggio in un nodo di regola di badging in modo che abbiano un percorso relativo.</li>
    </ol> <p> </p> <p>Infine, ripulisci rimuovendo la risorsa <code>/etc/community/badging</code></p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Progettazione console di Classic Communities {#classic-communities-console-designs}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/designs/social/console</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><code>/libs/settings/wcm/designs/social/console</code></p> <p><code>/apps/settings/wcm/designs/social/console</code></p> </td>
  </tr>
  <tr>
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td>N/D</td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Configurazioni di accesso facebook Social {#facebook-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/cloudservices/facebookconnect</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><code class="code">/conf/global/settings/cloudconfigs/facebookconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/facebookconnect</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Tutte le nuove configurazioni di Facebook Cloud devono essere migrate alla nuova posizione.</p>
    <ol>
     <li>Esegui la migrazione delle configurazioni esistenti nella posizione precedente alla nuova posizione.
      <ol>
       <li>Ricrea manualmente nuove configurazioni di accesso Facebook Social tramite l’interfaccia utente di authoring AEM in <strong>Strumenti &gt; Cloud Services &gt; Configurazione accesso social Facebook</strong>.<br /> oppure <br /> </li>
       <li>Copia le nuove configurazioni di Facebook Cloud dalla posizione precedente alla nuova posizione appropriata, in <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>Aggiorna la directory principale del sito AEM Communities per fare riferimento alla nuova configurazione di accesso social Facebook impostando la variabile <code>[cq:Page]/jcr:content@cq:conf</code> sul percorso assoluto nella nuova posizione.</li>
     <li>Disassociare il Cloud Service Facebook Connect legacy da qualsiasi directory principale del sito AEM Communities aggiornata per fare riferimento alla nuova posizione.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Configurazioni opzioni lingua {#language-options-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/social/config/languageOpts</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><code>/libs/social/translation/languageOpts</code></td>
  </tr>
  <tr>
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td>N/D<br /> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Configurazioni di accesso pinterest Social {#pinterest-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/cloudservices/pinterestconnect</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><code class="code">/conf/global/settings/cloudconfigs/pinterestconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/pinterestconnect</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Tutte le nuove configurazioni di Pinterest Cloud devono essere migrate alla nuova posizione.</p>
    <ol>
     <li>Esegui la migrazione delle configurazioni esistenti nella posizione precedente alla nuova posizione.
      <ol>
       <li>Ricrea manualmente nuove configurazioni di accesso Pinterest Social tramite l’interfaccia utente di authoring AEM in <strong>Strumenti &gt; Cloud Services &gt; Configurazione accesso social Pinterest</strong>.<br /> oppure</li>
       <li>Copia le nuove configurazioni di Pinterest Cloud dalla posizione precedente alla nuova posizione appropriata in <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>Aggiorna la directory principale del sito AEM Communities per fare riferimento alla nuova configurazione di accesso social Pinterest impostando la variabile <code>[cq:Page]/jcr:content@cq:conf</code> sul percorso assoluto nella nuova posizione.</li>
     <li>Disassociare il Cloud Service Pinterest Connect legacy da qualsiasi directory principale del sito AEM Communities aggiornata per fare riferimento alla nuova posizione.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Configurazioni punteggio {#scoring-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/community/scoring</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><code>/libs/settings/community/scoring</code></td>
  </tr>
  <tr>
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Per allinearsi alla nuova struttura del repository, è possibile memorizzare le regole di punteggio in <code>/apps/settings/</code> o /<code>conf/.../settings</code></p>
    <ol>
     <li>Per <code>/apps/settings</code>, fungerebbe da regole globali o predefinite gestite in SCM.</li>
    </ol> <p>Crea configurazioni in base al contesto in <code>/conf/</code> utilizzando CRXDELite:</p>
    <ol>
     <li>Crea le configurazioni desiderate <code>/conf/.../settings</code> posizione<br /> </li>
     <li>Il sito community deve avere <code>cq:conf </code>proprietà impostata.
      <ol>
       <li>Se no <code>cq:conf</code> è impostato, le regole di punteggio saranno lette direttamente dal percorso specificato per la proprietà '<code>scoringRules</code>' nel nodo principale del sito, ad esempio: <code>/content/we-retail/us/en/community/jcr:content</code></li>
      </ol> </li>
    </ol> <p>Pulizia: Rimuovi la risorsa <code>/etc/community/scoring</code></p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Configurazioni di accesso twitter Social {#twitter-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/cloudservices/twitterconnect</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><code class="code">/conf/global/settings/cloudconfigs/twitterconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/twitterconnect</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Tutte le nuove configurazioni di Twitter Cloud devono essere migrate alla nuova posizione.</p>
    <ol>
     <li>Esegui la migrazione delle configurazioni esistenti nella posizione precedente alla nuova posizione.
      <ol>
       <li>Ricrea manualmente nuove configurazioni di accesso Twitter Social tramite l’interfaccia utente di authoring AEM in <strong>Strumenti &gt; Cloud Services &gt; Configurazione accesso social Twitter</strong>.<br /> oppure <br /> </li>
       <li>Copia le nuove configurazioni di Twitter Cloud dalla posizione precedente alla nuova posizione appropriata, in <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>Aggiorna la directory principale del sito AEM Communities per fare riferimento alla nuova configurazione di accesso social Twitter impostando la variabile <code>[cq:Page]/jcr:content@cq:conf</code> sul percorso assoluto nella nuova posizione.</li>
     <li>Disassociare il Cloud Service Twitter Connect legacy da qualsiasi directory principale del sito AEM Communities aggiornata per fare riferimento alla nuova posizione.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Varie {#misc}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/community/templates</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><code>/libs/settings/community/templates</code></td>
  </tr>
  <tr>
   <td><strong>Orientamento alla ristrutturazione</strong></td>
   <td><p>Adobe ha fornito un'utilità di migrazione in:</p> <p><a href="https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration">https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration</a></p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>I modelli personalizzati esistenti passerebbero a <code>/conf/global/settings/community/template/&lt;groups/sites/functions&gt;</code></td>
  </tr>
 </tbody>
</table>
