---
title: Ristrutturazione del repository per  AEM Communities in 6.4
seo-title: Ristrutturazione del repository per  AEM Communities in 6.4
description: Scoprite come apportare le modifiche necessarie per eseguire la migrazione alla nuova struttura del repository in AEM 6.4 per Communities.
seo-description: Scoprite come apportare le modifiche necessarie per eseguire la migrazione alla nuova struttura del repository in AEM 6.4 per Communities.
uuid: d161655f-4074-44a7-8d69-38e80934c58b
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 7383265b-0ed4-4ea7-b741-0a417d187bdd
translation-type: tm+mt
source-git-commit: d20ddba254c965e1b0c0fc84a482b7e89d4df5cb
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 3%

---


# Ristrutturazione del repository per  AEM Communities in 6.5 {#repository-restructuring-for-aem-communities-in}

Come descritto nella pagina [Ristrutturazione del repository principale di AEM 6.4](/help/sites-deploying/repository-restructuring.md), i clienti che effettuano l&#39;aggiornamento a AEM 6.5 devono utilizzare questa pagina per valutare lo sforzo di lavoro associato alle modifiche del repository che hanno un impatto sulla soluzione  AEM Communities. Alcune modifiche richiedono sforzi di lavoro durante il processo di aggiornamento di AEM 6.5, mentre altre possono essere posticipate fino a un aggiornamento futuro.

**Con aggiornamento 6.5**

* [Modelli di notifica e-mail](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#e-mail-notification-templates)
* [Configurazioni iscrizione](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#subscription-configurations)

**Prima dell&#39;aggiornamento futuro**

* [Configurazioni di Badging](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#badging-configurations)
* [Progettazione console di Classic Communities](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#classic-communities-console-designs)
* [Configurazioni di accesso tramite social network Facebook](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#facebook-social-login-configurations)
* [Configurazioni opzioni lingua](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#language-options-configurations)

* [Configurazioni di accesso tramite social network Pinterest](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#pinterest-social-login-configurations)
* [Configurazioni punteggio](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#scoring-configurations)
* [Configurazioni di accesso Twitter Social](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#twitter-social-login-configurations)
* [Misc](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#misc)

## Con aggiornamento 6.5 {#with-upgrade}

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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>La migrazione manuale è necessaria se si desidera passare al nuovo percorso in "<code>/apps/settings</code>". È possibile utilizzare Granite Configuration Manager per eseguire la migrazione.</p> <p>È possibile eseguire la migrazione impostando la proprietà <code>mergeList</code> su <code>true</code> sul nodo "<code>/libs/settings/community/subscriptions</code>" e aggiungendo un nodo secondario <code>nt:unstructured</code>.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Configurazioni iscrizione {#subscription-configurations}

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
   <td><p>La migrazione manuale è necessaria se si desidera passare al nuovo percorso in "<code>/apps/settings</code>". È possibile utilizzare Granite Configuration Manager per eseguire la migrazione.</p> <p>È possibile eseguire la migrazione impostando la proprietà <code>mergeList</code> su <code>true</code> sul nodo "<code>/libs/settings/community/subscriptions</code>" e aggiungendo un nodo secondario <code>nt:unstructured</code>.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Configurazioni Watchwords {#watchwords-configurations}

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
   <td>È disponibile un'attività di migrazione Lazy per ripulire le configurazioni community.<br /> <p>L'attività sposta le parole d'ordine da <code>/etc/watchwords</code> a <code>/conf/global/settings/community/watchwords</code>.</p> <p>Se le parole d'ordine personalizzate sono memorizzate in SCM, devono essere distribuite su <code>/apps/settings/...</code> e occorre assicurarsi che non vi sia una configurazione sovrapposta <code>/conf/global/settings/...</code> che abbia la precedenza.</p> <p>L'attività di migrazione rimuove le posizioni <code>/etc</code>.</p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

## Prima dell&#39;aggiornamento futuro {#prior-to-upgrade}

### Configurazioni di Badging {#badging-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Posizione precedente</strong></td>
   <td><code>/etc/community/badging</code></td>
  </tr>
  <tr>
   <td><strong>Nuove posizioni</strong></td>
   <td><p><strong>Regole di badge:</strong></p> <p><code>/libs/settings/community/badging</code></p> <p><strong>Immagini badge:</strong></p> <p>Per le immagini predefinite: <code>/etc/community/badging/images are moved to /libs/community/badging/images</code></p> <p>Per le immagini personalizzate: <code>/content/community/badging/images</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td><p>È richiesta la migrazione manuale.</p> <p>Se la tua istanza ha personalizzato le regole di assegnazione dei badging/punteggio, non esiste un modo automatico per posizionare tutte le regole sotto un bucket. Hai bisogno di input da parte del cliente sul quale desideri usare il bucket conf (globale o specifico) per il tuo sito.</p> <p>Nessuna interfaccia utente disponibile per configurare il contrassegno e il punteggio per un sito.</p> <p>Per allineare con la nuova struttura del repository:</p>
    <ol>
     <li>Creare un bucket di contesto del sito utilizzando il <strong>browser di configurazione</strong> in <strong>Strumenti</strong></li>
     <li>Vai alla directory principale del sito</li>
     <li>Impostare <code>cq:confproperty</code> sul percorso del bucket in cui si desidera memorizzare tutte le impostazioni. Lo stesso può essere impostato tramite il sito <strong>Modifica guidata - Imposta input configurazione cloud</strong>.</li>
     <li>Sposta le regole di contrassegno e di punteggio pertinenti da <code>/etc/community/*</code> al bucket del contesto del sito creato nel passaggio precedente.</li>
     <li>Regola le proprietà Regole di contrassegno e Regole di punteggio nella directory principale del sito per disporre di riferimenti relativi alle nuove posizioni delle regole.
      <ol>
       <li>Ad esempio, se la proprietà per <code>cq:conf = /conf/we-retail</code>, <code>badgingRules [] = community/badging/rules</code> se le regole ora vengono spostate in questo nuovo bucket.</li>
      </ol> </li>
     <li>Analogamente, regolare i riferimenti alle regole di punteggio in un nodo di regola contrassegno per ottenere un percorso relativo.</li>
    </ol> <p> </p> <p>Infine, pulite la risorsa rimuovendo <code>/etc/community/badging</code></p> </td>
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
   <td><strong>Orientamenti per la ristrutturazione</strong></td>
   <td>N/D</td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Configurazioni di accesso tramite social network di Facebook {#facebook-social-login-configurations}

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
   <td><p>Qualsiasi nuova configurazione di Facebook Cloud deve essere migrata nella nuova posizione.</p>
    <ol>
     <li>Migra le configurazioni esistenti nella posizione precedente alla nuova posizione.
      <ol>
       <li>Ricreate manualmente le nuove configurazioni di accesso tramite social network di Facebook tramite l'interfaccia utente di authoring AEM in <strong>Strumenti &gt; Cloud Services &gt; Configurazione accesso tramite social network di Facebook</strong>.<br /> o <br /> </li>
       <li>Copia le nuove configurazioni di Facebook Cloud da Posizione precedente alla nuova posizione appropriata, in <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>Aggiornate  radice del sito AEM Communities per fare riferimento alla nuova configurazione di accesso tramite social network di Facebook impostando la proprietà <code>[cq:Page]/jcr:content@cq:conf</code> sul percorso assoluto nella nuova posizione.</li>
     <li>Separate il Cloud Service di Facebook Connect legacy da qualsiasi  directory principale del sito AEM Communities aggiornata per fare riferimento alla nuova posizione.</li>
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

### Configurazioni di accesso tramite social network Pinterest {#pinterest-social-login-configurations}

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
   <td><p>Qualsiasi nuova configurazione di Pinterest Cloud deve essere migrata nella nuova posizione.</p>
    <ol>
     <li>Migra le configurazioni esistenti nella posizione precedente alla nuova posizione.
      <ol>
       <li>Create manualmente nuove configurazioni di accesso tramite social network Pinterest tramite l'interfaccia utente di authoring AEM in <strong>Strumenti &gt; Cloud Services &gt; Configurazione accesso tramite social network Pinterest</strong>.<br /> o</li>
       <li>Copiate le nuove configurazioni di Pinterest Cloud dalla posizione precedente alla nuova posizione appropriata in <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>Aggiornate  radice del sito AEM Communities per fare riferimento alla nuova configurazione di accesso tramite social network Pinterest impostando la proprietà <code>[cq:Page]/jcr:content@cq:conf</code> sul percorso assoluto nella nuova posizione.</li>
     <li>Separate il Cloud Service Pinterest Connect legacy da qualsiasi  directory principale del sito AEM Communities aggiornata in base alla nuova posizione.</li>
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
   <td><p>Per allineare con la nuova struttura del repository, le regole di punteggio possono essere memorizzate in <code>/apps/settings/</code> o /<code>conf/.../settings</code></p>
    <ol>
     <li>Per <code>/apps/settings</code>, si tratterebbe di regole globali o predefinite gestite in SCM.</li>
    </ol> <p>Crea configurazioni basate sul contesto in <code>/conf/</code> utilizzando CRXDELite:</p>
    <ol>
     <li>Creare le configurazioni nella posizione <code>/conf/.../settings</code> desiderata<br /> </li>
     <li>La proprietà <code>cq:conf </code>del sito community deve essere impostata.
      <ol>
       <li>Se non è impostata alcuna <code>cq:conf</code>, le regole di punteggio verranno lette direttamente dal percorso specificato per la proprietà '<code>scoringRules</code>' nel nodo principale del sito, ad esempio: <code>/content/we-retail/us/en/community/jcr:content</code></li>
      </ol> </li>
    </ol> <p>Pulizia: Rimuovere la risorsa <code>/etc/community/scoring</code></p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Configurazioni di accesso social network per Twitter {#twitter-social-login-configurations}

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
   <td><p>Qualsiasi nuova configurazione di Twitter Cloud deve essere migrata nella nuova posizione.</p>
    <ol>
     <li>Migra le configurazioni esistenti nella posizione precedente alla nuova posizione.
      <ol>
       <li>Ricreate manualmente le nuove configurazioni di accesso a Twitter mediante l'interfaccia utente di authoring AEM in <strong>Strumenti &gt; Cloud Services &gt; Configurazione accesso a Twitter tramite social network</strong>.<br /> o <br /> </li>
       <li>Copia le nuove configurazioni di Twitter Cloud da Posizione precedente alla nuova posizione appropriata, in <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>Aggiornate  radice del sito AEM Communities per fare riferimento alla nuova configurazione di accesso social network di Twitter impostando la proprietà <code>[cq:Page]/jcr:content@cq:conf</code> sul percorso assoluto nella nuova posizione.</li>
     <li>Separate il Cloud Service precedente di Twitter Connect da qualsiasi  radice del sito AEM Communities aggiornata in riferimento alla nuova posizione.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Misc {#misc}

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
   <td><p> Adobe ha fornito un'utility di migrazione all'indirizzo:</p> <p><a href="https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration">https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration</a></p> </td>
  </tr>
  <tr>
   <td><strong>Note</strong></td>
   <td>I modelli personalizzati esistenti si sposteranno in <code>/conf/global/settings/community/template/&lt;groups/sites/functions&gt;</code></td>
  </tr>
 </tbody>
</table>

