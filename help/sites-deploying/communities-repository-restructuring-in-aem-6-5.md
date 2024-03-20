---
title: Ristrutturazione dell’archivio per AEM Communities nella versione 6.4
description: Scopri come apportare le modifiche necessarie per migrare alla nuova struttura dell’archivio in AEM 6.4 per Communities.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 4d2bdd45-a29a-4936-b8da-f7e011d81e83
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 1%

---

# Ristrutturazione dell’archivio per AEM Communities nella versione 6.5 {#repository-restructuring-for-aem-communities-in}

Come descritto sull’elemento padre [Ristrutturazione dell’archivio in AEM 6.4](/help/sites-deploying/repository-restructuring.md) pagina, i clienti che eseguono l’aggiornamento a AEM 6.5 devono utilizzare questa pagina per valutare l’impegno di lavoro associato alle modifiche dell’archivio che influiscono sulla soluzione AEM Communities. Alcune modifiche richiedono un impegno di lavoro durante il processo di aggiornamento AEM 6.5, mentre altre possono essere differite fino a un aggiornamento futuro.

**Con aggiornamento 6.5**

* [Modelli di notifica tramite posta elettronica](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#e-mail-notification-templates)
* [Configurazioni di abbonamento](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#subscription-configurations)

**Prima di un aggiornamento futuro**

* [Configurazioni badge](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#badging-configurations)
* [Progettazioni console community classiche](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#classic-communities-console-designs)
* [Configurazioni di accesso social network tramite facebook](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#facebook-social-login-configurations)
* [Configurazioni opzioni lingua](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#language-options-configurations)

* [Configurazioni di accesso social network tramite pinterest](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#pinterest-social-login-configurations)
* [Configurazioni punteggio](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#scoring-configurations)
* [Configurazioni accesso social network tramite Twitter](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#twitter-social-login-configurations)
* [Varie](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#misc)

## Con aggiornamento 6.5 {#with-upgrade}

### Modelli di notifica tramite posta elettronica {#e-mail-notification-templates}

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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>È necessaria la migrazione manuale se desideri passare al nuovo percorso in "<code>/apps/settings</code>". Puoi utilizzare Granite Configuration Manager per eseguire la migrazione.</p> <p>Puoi eseguire la migrazione impostando la proprietà <code>mergeList</code> a <code>true</code> sulla "<code>/libs/settings/community/subscriptions</code>" e aggiungi un <code>nt:unstructured</code> nodo figlio.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Configurazioni di abbonamento {#subscription-configurations}

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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>È necessaria la migrazione manuale se desideri passare al nuovo percorso in "<code>/apps/settings</code>". Puoi utilizzare Granite Configuration Manager per eseguire la migrazione.</p> <p>Puoi eseguire la migrazione impostando la proprietà <code>mergeList</code> a <code>true</code> sulla "<code>/libs/settings/community/subscriptions</code>" e aggiungi un <code>nt:unstructured</code> nodo figlio.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Configurazioni parole d’ordine {#watchwords-configurations}

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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td>È disponibile un’attività Migrazione lenta per ripulire le configurazioni Communities.<br /> <p>L'attività sposta le parole d'ordine da <code>/etc/watchwords</code> a <code>/conf/global/settings/community/watchwords</code>.</p> <p>Se le parole d'ordine personalizzate vengono memorizzate in SCM, devono essere distribuite in <code>/apps/settings/...</code> e devi assicurarti che non ci siano sovrapposizioni <code>/conf/global/settings/...</code> che avrebbe la precedenza.</p> <p>L’attività di migrazione rimuove <code>/etc</code> posizioni.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

## Prima di un aggiornamento futuro {#prior-to-upgrade}

### Configurazioni badge {#badging-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/community/badging</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><strong>Regole badge:</strong></p> <p><code>/libs/settings/community/badging</code></p> <p><strong>Immagini badge:</strong></p> <p>Per le immagini predefinite: <code>/etc/community/badging/images are moved to /libs/community/badging/images</code></p> <p>Per le immagini personalizzate: <code>/content/community/badging/images</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>È necessaria la migrazione manuale.</p> <p>Se l’istanza ha personalizzato le regole di badge/punteggio, non esiste un modo automatico per inserire tutte le regole in un bucket. Sono necessari input del cliente su quale bucket di configurazione (globale o specifico del sito) desideri utilizzare per il sito.</p> <p>Nessuna interfaccia utente disponibile per configurare i badge e il punteggio per un sito.</p> <p>Per allinearsi alla nuova struttura dell’archivio:</p>
    <ol>
     <li>Creare un bucket di contesto del sito utilizzando <strong>Browser configurazioni</strong> in <strong>Strumenti</strong></li>
     <li>Vai alla directory principale del sito</li>
     <li>Imposta <code>cq:confproperty</code> al percorso del bucket in cui desideri memorizzare tutte le impostazioni. Lo stesso può essere impostato tramite il sito <strong>Modifica guidata - Imposta input configurazione cloud</strong>.</li>
     <li>Sposta le regole di badge e punteggio pertinenti da <code>/etc/community/*</code> al bucket di contesto del sito creato nel passaggio precedente.</li>
     <li>Regola le proprietà delle regole di assegnazione dei badge e delle regole di assegnazione del punteggio nella directory principale del sito in modo che abbiano riferimenti relativi a nuove posizioni delle regole.
      <ol>
       <li>Ad esempio, se la proprietà per <code>cq:conf = /conf/we-retail</code>, quindi <code>badgingRules [] = community/badging/rules</code> se le regole vengono ora spostate in questo nuovo bucket.</li>
      </ol> </li>
     <li>Allo stesso modo, regola i riferimenti alle regole di punteggio in un nodo di regola di badge in modo che abbiano un percorso relativo.</li>
    </ol> <p> </p> <p>Infine, effettua la pulizia rimuovendo la risorsa <code>/etc/community/badging</code></p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Progettazioni console community classiche {#classic-communities-console-designs}

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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td>N/D</td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Configurazioni di accesso social network tramite facebook {#facebook-social-login-configurations}

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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>È necessario eseguire la migrazione di tutte le nuove configurazioni cloud di Facebook nella nuova posizione.</p>
    <ol>
     <li>Migra le configurazioni esistenti nella posizione precedente alla nuova posizione.
      <ol>
       <li>Facebook Ricreare manualmente le nuove configurazioni di accesso social network tramite l’interfaccia utente di creazione AEM all’indirizzo <strong>Strumenti &gt; Cloud Service &gt; Configurazione accesso social network tramite Facebook</strong>.<br /> oppure <br /> </li>
       <li>Copia le nuove configurazioni cloud di Facebook dalla posizione precedente alla nuova posizione appropriata, in <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>Aggiorna qualsiasi directory principale del sito AEM Communities per fare riferimento alla nuova configurazione di accesso social network di Facebook impostando <code>[cq:Page]/jcr:content@cq:conf</code> al percorso assoluto nella nuova posizione.</li>
     <li>Separa il Cloud Service Facebook Connect legacy da qualsiasi directory principale del sito AEM Communities aggiornata per fare riferimento alla nuova posizione.</li>
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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td>N/D<br /> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Configurazioni di accesso social network tramite pinterest {#pinterest-social-login-configurations}

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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>È necessario eseguire la migrazione di tutte le nuove configurazioni cloud di Pinterest nella nuova posizione.</p>
    <ol>
     <li>Migra le configurazioni esistenti nella posizione precedente alla nuova posizione.
      <ol>
       <li>Pinterest Ricreare manualmente le nuove configurazioni di accesso social network tramite l’interfaccia utente di creazione AEM all’indirizzo <strong>Strumenti &gt; Cloud Service &gt; Configurazione accesso social network tramite Pinterest</strong>.<br /> o</li>
       <li>Copia le nuove configurazioni cloud di Pinterest dalla posizione precedente alla nuova posizione appropriata in <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>Aggiorna qualsiasi directory principale del sito AEM Communities per fare riferimento alla nuova configurazione di accesso social network di Pinterest impostando il <code>[cq:Page]/jcr:content@cq:conf</code> al percorso assoluto nella nuova posizione.</li>
     <li>Separa il Cloud Service Pinterest Connect legacy da qualsiasi directory principale del sito AEM Communities aggiornata per fare riferimento alla nuova posizione.</li>
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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Per allinearsi alla nuova struttura dell’archivio, le regole di punteggio possono essere memorizzate in <code>/apps/settings/</code> o /<code>conf/.../settings</code></p>
    <ol>
     <li>Per <code>/apps/settings</code>, fungerebbe da regola globale o predefinita gestita in SCM.</li>
    </ol> <p>Creare configurazioni in base al contesto in <code>/conf/</code> utilizzando CRXDELite:</p>
    <ol>
     <li>Crea le configurazioni nel <code>/conf/.../settings</code> posizione<br /> </li>
     <li>Il sito Communities deve avere <code>cq:conf </code>proprietà impostata.
      <ol>
       <li>In caso negativo <code>cq:conf</code> è impostato, le regole di punteggio vengono lette direttamente dal percorso specificato per la proprietà '<code>scoringRules</code>' nel nodo principale del sito, ad esempio: <code>/content/we-retail/us/en/community/jcr:content</code></li>
      </ol> </li>
    </ol> <p>Pulizia: rimuovere la risorsa <code>/etc/community/scoring</code></p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Configurazioni accesso social network tramite Twitter {#twitter-social-login-configurations}

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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>È necessario eseguire la migrazione di tutte le nuove configurazioni cloud di Twitter alla nuova posizione.</p>
    <ol>
     <li>Migra le configurazioni esistenti nella posizione precedente alla nuova posizione.
      <ol>
       <li>Twitter Ricreare manualmente le nuove configurazioni di accesso social network tramite l’interfaccia utente di creazione dell’AEM all’indirizzo <strong>Strumenti &gt; Cloud Service &gt; Configurazione accesso social network tramite Twitter</strong>.<br /> oppure <br /> </li>
       <li>Copia le nuove configurazioni cloud di Twitter dalla posizione precedente alla nuova posizione appropriata, in <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>Aggiorna qualsiasi directory principale del sito AEM Communities per fare riferimento alla nuova configurazione di accesso social network del Twitter impostando <code>[cq:Page]/jcr:content@cq:conf</code> al percorso assoluto nella nuova posizione.</li>
     <li>Disassociare il Cloud Service di connessione del Twitter legacy da qualsiasi directory principale del sito AEM Communities aggiornata per fare riferimento alla nuova posizione.</li>
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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>Adobe ha fornito un’utility di migrazione in:</p> <p><a href="https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration">https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration</a></p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>I modelli personalizzati esistenti verranno spostati in <code>/conf/global/settings/community/template/&lt;groups/sites/functions&gt;</code></td>
  </tr>
 </tbody>
</table>
