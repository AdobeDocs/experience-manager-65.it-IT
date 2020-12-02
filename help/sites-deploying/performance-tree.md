---
title: Struttura delle prestazioni
seo-title: Struttura delle prestazioni
description: Scopri i passaggi da seguire per risolvere i problemi di prestazioni in AEM.
seo-description: Scopri i passaggi da seguire per risolvere i problemi di prestazioni in AEM.
uuid: ab0624f7-6b39-4255-89e0-54c74b54cd98
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 5febbb1e-795c-49cd-a8f4-c6b4b540673d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 5%

---


# Albero prestazioni{#performance-tree}

## Ambito {#scope}

Il diagramma seguente è inteso a fornire indicazioni sui passi da intraprendere per risolvere i problemi di prestazioni. È suddiviso in 5 sezioni per una lettura più semplice.

Ogni passaggio del diagramma è collegato a una risorsa della documentazione o a una raccomandazione.

## Prerequisiti e supposizioni {#prerequisites-and-assumptions}

Il presupposto è che un problema di prestazioni venga osservato in una determinata pagina (una console AEM o una pagina Web) e possa essere riprodotto in modo coerente. Prima di avviare l&#39;indagine, è necessario disporre di un metodo per verificare o controllare le prestazioni.

L&#39;analisi inizia dal passaggio 0. L&#39;obiettivo è quello di determinare quale entità (dispatcher, host esterno o AEM) è responsabile del problema di prestazioni, quindi determinare quale area (server o rete) deve essere esaminata.

### Sezione 1 {#section}

![chlimage_1-103](assets/chlimage_1-103.png)

### Sezione 2 {#section-1}

![chlimage_1-104](assets/chlimage_1-104.png)

### Sezione 3 {#section-2}

![chlimage_1-105](assets/chlimage_1-105.png)

### Sezione 4 {#section-3}

![chlimage_1-106](assets/chlimage_1-106.png)

### Sezione 5 {#section-4}

![chlimage_1-107](assets/chlimage_1-107.png)

## Collegamenti di riferimento {#reference-links}

<table>
 <tbody>
  <tr>
   <td><strong>Incremento</strong></td>
   <td><strong>Titolo</strong></td>
   <td><strong>Riferimenti</strong></td>
  </tr>
  <tr>
   <td><strong>Passaggio 0</strong></td>
   <td>Analizza flusso richiesta</td>
   <td><p>Potete utilizzare l’analisi standard delle richieste HTTP nel browser per analizzare il flusso di richieste. Per ulteriori informazioni su come eseguire questa operazione su Chrome, vedere:<br /> </p> <p><a href="https://developers.google.com/web/tools/chrome-devtools/profile/network-performance/resource-loading">https://developers.google.com/web/tools/chrome-devtools/profile/network-performance/resource-</a><a href="https://developers.google.com/web/tools/chrome-devtools/profile/network-performance/understanding-resource-timing"><br /> loadinghttps://developers.google.com/web/tools/chrome-devtools/profile/network-performance/understanding-resource-timing</a><br /> </p> </td>
  </tr>
  <tr>
   <td><strong>Passaggio 2</strong></td>
   <td>Le richieste vengono da host esterni?</td>
   <td>Potete utilizzare l’analisi standard delle richieste HTTP nel browser per analizzare il flusso di richieste. Consultate i collegamenti riportati sopra su come eseguire questa operazione in Chrome.<br /> </td>
  </tr>
  <tr>
   <td><strong>Passaggio 3</strong></td>
   <td>È possibile memorizzare le richieste nella cache?</td>
   <td>Per ulteriori informazioni sulle richieste memorizzabili nella cache e sui consigli generali per l'ottimizzazione delle prestazioni del dispatcher, vedere <a href="/help/sites-deploying/configuring-performance.md#optimizing-performance-when-using-the-dispatcher">Dispatcher Performance Optimization</a>.</td>
  </tr>
  <tr>
   <td><strong>Passaggio 4</strong></td>
   <td>Le richieste vengono dal Dispatcher?</td>
   <td><p>Per verificare se le richieste sono memorizzate nella cache correttamente, consultare la <a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#debugging">documentazione relativa al debug del dispatcher</a>.<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>Passaggio 5</strong></td>
   <td>Il dispatcher sta tentando di autenticare ogni richiesta tramite AEM?</td>
   <td>Verificare se il dispatcher invia <code>HEAD</code> richieste di autenticazione a AEM prima di distribuire la risorsa nella cache. È possibile eseguire questa operazione cercando <code>HEAD</code> richieste nella AEM <code>access.log</code>. Per ulteriori informazioni, vedere <a href="/help/sites-deploying/configure-logging.md">Registrazione</a>.<br /> </td>
  </tr>
  <tr>
   <td><strong>Passaggio 6</strong></td>
   <td>La posizione geografica del Dispatcher è lontana dagli utenti?</td>
   <td>Sposta il dispatcher più vicino agli utenti.</td>
  </tr>
  <tr>
   <td><strong>Passaggio 7</strong></td>
   <td>Il livello di rete del Dispatcher è OK?</td>
   <td><br /> Esaminate il livello di rete per i problemi di saturazione e latenza.<p> </p> </td>
  </tr>
  <tr>
   <td><strong>Passaggio 8</strong></td>
   <td>La lentezza è riproducibile con un'istanza locale?</td>
   <td><br /> <p>Utilizzate <a href="/help/sites-developing/tough-day.md">Tough Day</a> per replicare le condizioni "real world" dalle istanze di produzione. Se questo non è realistico per lo spazio di sviluppo, verificare l'istanza di produzione (o una sosta identica) in un contesto di rete diverso.<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>Passaggio 9</strong></td>
   <td>La posizione geografica del server è lontana dagli utenti?</td>
   <td>Avvicinare il server agli utenti.</td>
  </tr>
  <tr>
   <td><strong>Passaggi 10 e 29</strong></td>
   <td>Indagine del livello di rete</td>
   <td><p>Esaminate il livello di rete per i problemi di saturazione e latenza.</p> <p>Per il livello di authoring, si consiglia di non superare i 100 millisecondi.</p> <p>Per ulteriori informazioni sui suggerimenti per l'ottimizzazione delle prestazioni, vedere <a href="https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html">questa pagina</a>.</p> </td>
  </tr>
  <tr>
   <td><strong>Passaggio 11</strong></td>
   <td>Avvicinare il server o aggiungerne uno per regione</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Passaggio 12</strong></td>
   <td>Risoluzione dei problemi AEM server</td>
   <td>Per ulteriori informazioni, consulta i seguenti passaggi secondari del diagramma.</td>
  </tr>
  <tr>
   <td><strong>Passaggio 13</strong></td>
   <td>Controllare i requisiti hardware</td>
   <td>Consultate la documentazione sulle <a href="/help/managing/hardware-sizing-guidelines.md">Linee guida sul ridimensionamento hardware</a>.<br /> </td>
  </tr>
  <tr>
   <td><strong>Passaggio 14</strong></td>
   <td>Verifica delle cause frequenti dei problemi di prestazioni</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Passaggio 15</strong></td>
   <td>Trova richieste lente</td>
   <td><p>È possibile verificare la presenza di richieste lente analizzando il <code>request.log</code> o utilizzando <code>rlog.jar</code>.</p> <p>Per ulteriori informazioni sull'utilizzo di rlog.jar, consultate questa pagina.</p> <p>Vedere <a href="/help/sites-deploying/monitoring-and-maintaining.md#using-rlog-jar-to-find-requests-with-long-duration-times">Utilizzo di rlog.jar per trovare richieste con tempi di durata prolungata</a>.<br /> </p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Passaggio 16</strong></td>
   <td>Server profilo</td>
   <td><p>Per informazioni sugli strumenti di profilatura utilizzabili con AEM, vedere <a href="/help/sites-deploying/monitoring-and-maintaining.md#tools-for-monitoring-and-analyzing-performance">Strumenti per il monitoraggio e l'analisi delle prestazioni</a>.<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>Passaggio 17</strong></td>
   <td>Trovare metodi lenti nel profiling</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Passaggio 18</strong></td>
   <td>Scenari comuni di profilazione</td>
   <td>Vedere <a href="/help/sites-deploying/monitoring-and-maintaining.md#analyzing-specific-scenarios">Analisi di scenari specifici</a> nella sezione Ottimizzazione delle prestazioni.<br /> </td>
  </tr>
  <tr>
   <td><strong>Passaggio 19</strong></td>
   <td>100% CPU</td>
   <td><a href="/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance">https://helpx.adobe.com/experience-manager/6-3/sites-deploying/monitoring-and-maintaining.html#MonitoringPerformance</a></td>
  </tr>
  <tr>
   <td><strong>Passaggio 20</strong></td>
   <td>Memoria insufficiente</td>
   <td><br />
    <ol>
     <li><a href="/help/sites-deploying/monitoring-and-maintaining.md#out-of-memory">Memoria insufficiente</a></li>
     <li><a href="/help/sites-deploying/troubleshooting.md">La mia applicazione genera errori di memoria insufficiente</a></li>
     <li><a href="https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html">Analizzare i problemi di memoria sull'Helpx.</a><br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Passaggio 21</strong></td>
   <td>I/O disco</td>
   <td><p>Vedere la sezione <a href="/help/sites-deploying/monitoring-and-maintaining.md#disk-i-o">I/O del disco</a> nella documentazione relativa al monitoraggio e alla manutenzione.</p> </td>
  </tr>
  <tr>
   <td><strong>Passaggi 22 e 22.1</strong></td>
   <td>Rapporto cache</td>
   <td>Vedere <a href="/help/sites-deploying/configuring-performance.md#calculating-the-dispatcher-cache-ratio">Calcolo del rapporto della cache del dispatcher</a>.<br /> <br /> </td>
  </tr>
  <tr>
   <td><strong>Passaggio 23</strong></td>
   <td>Query lente</td>
   <td><a href="/help/sites-deploying/best-practices-for-queries-and-indexing.md">Best practice per query e indicizzazione</a></td>
  </tr>
  <tr>
   <td><strong>Passaggio 24</strong></td>
   <td>Ottimizzazione del repository</td>
   <td>
    <ul>
     <li><a href="https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html">Suggerimenti per il tuning delle prestazioni</a></li>
     <li><a href="/help/sites-deploying/configuring-performance.md#configuring-for-performance">Configurazione per prestazioni</a></li>
     <li><a href="https://www.slideshare.net/jukka/repository-performance-tuning">Ottimizzazione delle prestazioni del repository</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Passaggio 25</strong></td>
   <td>Flussi di lavoro in esecuzione</td>
   <td>
    <ul>
     <li><a href="/help/sites-deploying/configuring-performance.md#concurrent-workflow-processing">Elaborazione flusso di lavoro simultanea</a></li>
     <li><a href="/help/sites-deploying/configuring-performance.md#configure-the-queue-for-a-specific-workflow">Configurare la coda per un flusso di lavoro specifico</a></li>
     <li><a href="/help/sites-administering/workflows-administering.md#regular-purging-of-workflow-instances">Rimozione regolare delle istanze del flusso di lavoro</a></li>
     <li><a href="/help/sites-developing/workflows.md#transient-workflows">Flussi di lavoro transitori</a><br /> </li>
    </ul> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Passaggio 26</strong></td>
   <td>Infrastruttura MSM</td>
   <td><p><a href="/help/sites-administering/msm-best-practices.md">Best practice per i manager multisito</a><br /> </p> </td>
  </tr>
  <tr>
   <td><strong>Passaggio 27</strong></td>
   <td>Ottimizzazione delle risorse</td>
   <td>
    <ol>
     <li><a href="/help/sites-deploying/configuring-performance.md#cq-dam-asset-synchronization-service">Servizio di sincronizzazione risorse</a></li>
     <li><a href="/help/sites-deploying/configuring-performance.md#multiple-dam-instances">Istanze DAM multiple</a></li>
     <li>Articoli per suggerimenti sull'ottimizzazione delle prestazioni <a href="https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html">qui</a> e <a href="https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html">qui</a>.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Passaggio 28</strong></td>
   <td>Sessioni non chiuse</td>
   <td><p> </p> <p><a href="/help/sites-administering/troubleshoot.md#checking-for-unclosed-jcr-sessions">Verifica delle sessioni JCR non chiuse</a></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Passaggio 30</strong></td>
   <td>Spostare il dispatcher più vicino (aggiungere uno per "regione"?)</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Passaggio 31</strong></td>
   <td>Usare CDN davanti al dispatcher</td>
   <td><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html#using-dispatcher-with-a-cdn">Utilizzo di Dispatcher con una rete CDN</a><br /> </td>
  </tr>
  <tr>
   <td><strong>Passaggio 32</strong></td>
   <td>Utilizzare la gestione delle sessioni a livello di dispatcher per scaricare AEM server</td>
   <td><p><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement">Abilitazione di sessioni sicure</a></p> </td>
  </tr>
  <tr>
   <td><strong>Passaggio 33</strong></td>
   <td>Richieste incluse nella cache</td>
   <td>
    <ol>
     <li><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html">Configurazione del dispatcher generale</a></li>
     <li><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#configuring-the-dispatcher-cache-cache">Configurazione della cache del dispatcher</a></li>
    </ol> <p>Come migliorare il rapporto cache; rendi le richieste inseribili nella cache (procedure ottimali per il dispatcher)</p> <p>Inoltre, prendere in considerazione le seguenti impostazioni per ottimizzare le configurazioni di memorizzazione nella cache<br /> </p>
    <ol>
     <li>Impostare una regola di assenza della cache per le richieste HTTP non GET</li>
     <li>Configurare le stringhe di query affinché non possano essere memorizzate nella cache</li>
     <li>Non memorizzare nella cache gli URL con estensioni mancanti</li>
     <li>Intestazioni di autenticazione cache (possibile dalla versione 4.1.10 del dispatcher)</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Passaggio 34</strong></td>
   <td>Versione dispatcher aggiornamento</td>
   <td><p>Puoi scaricare la versione più recente del dispatcher nel seguente percorso:</p> <p><a href="https://helpx.adobe.com/experience-manager/dispatcher/release-notes.html">Segui il collegamento</a></p> </td>
  </tr>
  <tr>
   <td><strong>Passaggio 35</strong></td>
   <td>Configurare il dispatcher</td>
   <td><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html">Configurazione del dispatcher</a><br /> </td>
  </tr>
  <tr>
   <td><strong>Passaggio 36</strong></td>
   <td>Verifica annullamento validità cache</td>
   <td><br />
    <ul>
     <li><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html#invalidating-dispatcher-cache-from-the-authoring-environment">Annullamento validità cache per il livello Author;</a></li>
     <li><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance">Annullamento della validità della cache per il livello di pubblicazione.</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Passaggi 37 e 38</strong></td>
   <td>Caricamento pigro</td>
   <td><a href="https://docs.adobe.com/ddc/en/gems/aem-web-performance.html">Consulta la sessione Gem su AEM Web Performance.</a><br /> </td>
  </tr>
  <tr>
   <td><strong>Passaggio 39</strong></td>
   <td>Usare la preconnessione per ridurre il sovraccarico di connessione</td>
   <td>Vedi la Sessione Gem sopra indicata. È inoltre possibile effettuare la preconnessione della documentazione aggiuntiva su W3c:<a href="https://www.w3.org/TR/resource-hints/#dfn-preconnect"> https://www.w3.org/TR/resource-hints/#dfn-preconnect</a></td>
  </tr>
  <tr>
   <td><strong>Passaggi 40 e 41</strong><br /> </td>
   <td>Ospitanti esterni latenza e tempo di risposta</td>
   <td>Analizzare la latenza e il tempo di risposta per gli host esterni.</td>
  </tr>
  <tr>
   <td><strong>Passaggi 45 <br /> e 47</strong><br /> </td>
   <td>Utilizzo di HTTP/2</td>
   <td>Vedi la Sessione Gem per i passaggi 37,38 e 39. Inoltre, controllate <a href="https://help-forums.adobe.com/content/adobeforums/en/experience-manager-forum/adobe-experience-manager.topic.html/forum__kdzc-does_anyoneknowwhe.html">questo </a> post del forum sul supporto HTTP/2.<br /> </td>
  </tr>
  <tr>
   <td><strong>Passaggio 49</strong></td>
   <td>Riduci dimensioni payload</td>
   <td><a href="/help/sites-deploying/osgi-configuration-settings.md">Attivate </a> Gzipand per  <a href="https://docs.adobe.com/ddc/en/gems/aem-web-performance.html">ridurre le dimensioni</a> dell’immagine.<br /> </td>
  </tr>
  <tr>
   <td><strong>Passaggi 42 e 43</strong></td>
   <td>Keep-Alive</td>
   <td><p>L'intestazione <code>Keep-Alive</code> è presente nelle diverse richieste di riutilizzo delle connessioni? In caso contrario, ciò significherebbe che ogni richiesta porta a un altro stabilimento di collegamento, che introduce costi aggiuntivi non necessari. (Analisi delle richieste HTTP standard nel browser)</p> <p>È possibile controllare lo <a href="/help/sites-administering/proxy-jar.md">strumento Server proxy</a> per verificare la presenza di connessioni Keep-Alive.<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>Passaggio 44</strong></td>
   <td>Quante richieste vengono fatte?</td>
   <td>Eseguite l’analisi standard delle richieste HTTP nel browser.</td>
  </tr>
  <tr>
   <td><strong>Passaggio 46</strong></td>
   <td>Riduzione del numero di richieste</td>
   <td>
    <ol>
     <li>Concatenate le risorse (immagini, sprite CSS, JSON, ecc.)<br /> </li>
     <li>Incorporazione di Clientlibs:
      <ol>
       <li><a href="/help/sites-developing/clientlibs.md#creating-client-library-folders">Creazione di cartelle</a>  libreria client - vedere l'intestazione Utilizzo dell'incorporamento per ridurre al minimo le richieste</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Passaggio 48</strong></td>
   <td>Qual è la dimensione del payload?</td>
   <td>Analisi delle richieste HTTP standard nel browser</td>
  </tr>
  <tr>
   <td><strong>Passaggi 50 e 51</strong></td>
   <td>Blocco del codice JS</td>
   <td><a href="https://docs.adobe.com/ddc/en/gems/aem-web-performance.html">https://docs.adobe.com/ddc/en/gems/aem-web-performance.html</a></td>
  </tr>
 </tbody>
</table>

