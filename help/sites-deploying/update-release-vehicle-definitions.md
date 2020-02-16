---
title: Aggiorna definizioni veicolo di rilascio
seo-title: Aggiorna definizioni veicolo di rilascio
description: Questo articolo descrive i vari tipi di rilasci di AEM, inclusi rilasci completi, pacchetti di funzioni e Service Pack.
seo-description: Questo articolo descrive i vari tipi di rilasci di AEM, inclusi rilasci completi, pacchetti di funzioni e Service Pack.
uuid: 388fb6f5-0249-41e2-a460-1bb4cd0f8494
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 32695db5-d62d-4959-8a24-3d56b4a19904
translation-type: tm+mt
source-git-commit: b827c8acb1db158060d209c819fc72ffbfeca65f

---


# AEM - Definizioni dei veicoli di rilascio degli aggiornamenti{#update-release-vehicle-definitions}

Questo documento contiene informazioni sui diversi tipi di rilasci di Adobe Experience Manager (AEM), inclusi rilasci completi, pacchetti di funzioni e Service Pack che Adobe distribuisce ai propri clienti.

>[!Note]
>
>Per la pianificazione delle versioni di aggiornamento di AEM, fai riferimento alla roadmap degli aggiornamenti di [AEM](https://helpx.adobe.com/experience-manager/update-releases-roadmap.html)

## Versione completa {#full-release}

<table>
 <tbody>
  <tr>
   <td><strong>Definizione</strong></td>
   <td>
    <ul>
     <li>Rilascio pianificato</li>
     <li>Supporta i percorsi di aggiornamento per versioni specifiche, definiti nelle note sulla versione</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Denominazione</strong></td>
   <td>
    <ul>
     <li>I numeri di versione per le release principali aumentano in base alla formula X+1.Y.Z. </li>
     <li>I numeri di versione per rilasci minori aumentano in base alla formula X.Y+1.Z</li>
    </ul> <p>Dove X è il numero di versione principale, Y è il numero di versione secondario e Z il numero di patch.</p> </td>
  </tr>
  <tr>
   <td><strong>Inclusioni</strong></td>
   <td>
    <ul>
     <li>Nuove funzioni</li>
     <li>Miglioramenti</li>
     <li>Correzioni di bug</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Documentazione</strong></td>
   <td>
    <ul>
     <li>Le note sulla versione sono disponibili nel portale della documentazione</li>
     <li>La documentazione su funzioni, miglioramenti e correzioni di bug è disponibile nel portale della documentazione</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Cadenza</strong></td>
   <td>Annuale</td>
  </tr>
  <tr>
   <td><strong>Disponibilità e installazione</strong></td>
   <td>
    <ul>
     <li>Fornito come programma di installazione autonomo</li>
     <li>Disponibile dal sito Web delle licenze e dal sito Web delle licenze dei servizi gestiti</li>
     <li>Può richiedere la migrazione dell'archivio dei contenuti</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Livello di test</strong></td>
   <td>Completamente convalidato da QA</td>
  </tr>
 </tbody>
</table>

## Service Pack {#service-pack}

<table>
 <tbody>
  <tr>
   <td><strong>Definizione</strong></td>
   <td>
    <ul>
     <li>Rilascio pianificato</li>
     <li>Attualmente non è possibile eseguire il rollback</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Denominazione</strong></td>
   <td>
    <ul>
     <li>Numero di rilascio della patch: numero a una cifra</li>
     <li>Dopo l'installazione, aumenterà la cifra della patch del numero di rilascio installata, in base alla formula X.Y.Z.SPx</li>
     <li>Dove X è il numero di versione principale, Y è il numero di versione secondario e Z il numero di patch. x è il numero del service pack.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Inclusioni</strong></td>
   <td>
    <ul>
     <li>Nuove funzioni</li>
     <li>Miglioramenti</li>
     <li>Correzioni di bug</li>
     <li>Pacchetti di funzioni di interesse comune (se presenti)</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Documentazione</strong></td>
   <td>
    <ul>
     <li>Note sulla versione disponibili nel portale della documentazione</li>
     <li>Documentazione su funzioni, miglioramenti, correzioni di bug nel portale della documentazione</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Cadenza</strong></td>
   <td>Trimestrale</td>
  </tr>
  <tr>
   <td><strong>Disponibilità e installazione</strong></td>
   <td>
    <ul>
     <li>Consegnato come pacchetto</li>
     <li>Disponibile su Package Share</li>
     <li>Richiede l'installazione funzionale esistente</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Livello di test</strong></td>
   <td>
    <ul>
     <li>Tutte le correzioni QA convalidate</li>
     <li>Integrità complessiva del pacchetto con esecuzioni di automazione</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Cumulative Fix Pack  {#cumulative-fix-pack-aem}

<table>
 <tbody>
  <tr>
   <td><strong>Definizione</strong></td>
   <td>
    <ul>
     <li>Modello di consegna singola delle correzioni di rilascio</li>
     <li>Pacchetto di contenuti di aggregazione contenente il pacchetto di contenuti di singoli componenti</li>
     <li>I CFP sono il rollover delle correzioni rapide e non ne fanno parte alcun miglioramento.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Denominazione</strong></td>
   <td><p>X.Y.Z.CFPx</p> <p>Dove X è il numero di versione principale, Y è il numero di versione secondario e Z il numero di patch. x è il numero cumulativo del Service Pack.</p> </td>
  </tr>
  <tr>
   <td><strong>Inclusioni</strong></td>
   <td><p>CFP è un fix pack cumulativo contenente correzioni di tutti i componenti per un periodo di tempo specificato. Ad esempio, se un cliente applica CFP3, CFP3 = CFP1 + CFP2.</p> </td>
  </tr>
  <tr>
   <td><strong>Documentazione</strong></td>
   <td>Note sulla versione disponibili nel portale della documentazione</td>
  </tr>
  <tr>
   <td><strong>Cadenza</strong></td>
   <td>Quateralmente</td>
  </tr>
  <tr>
   <td><strong>Disponibilità e installazione</strong></td>
   <td>
    <ul>
     <li>Consegnato come pacchetto</li>
     <li>Disponibile su Package Share</li>
     <li>A seconda dell'ultimo service pack rilasciato</li>
     <li>Il CFP dipende da se stesso. I clienti non devono preoccuparsi di trovare/risolvere dipendenze. Il CFP deve essere installato nell'ultimo Service Pack rilasciato.</li>
     <li>CFP può essere installato come pacchetto singolo, migliorando l'esperienza dei clienti.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Livello di test</strong></td>
   <td>QA convalidato a livello di integrazione e test di regressione</td>
  </tr>
 </tbody>
</table>

## Oak Cumulative Fix Pack {#oak-cumulative-fix-pack}

<table>
 <tbody>
  <tr>
   <td><strong>Definizione</strong></td>
   <td>
    <ul>
     <li>Simile a un CFP standard, ma contiene solo correzioni relative al Oak</li>
     <li>Il COFP è autonomo (senza dipendenze). I clienti non devono preoccuparsi di trovare/risolvere dipendenze. [1]</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Denominazione</strong></td>
   <td>quercia &lt;versione&gt;</td>
  </tr>
  <tr>
   <td><strong>Inclusioni</strong></td>
   <td>COFP è un fix pack cumulativo contenente correzioni di tutti i componenti Oak per una versione 1.x specifica. Ad esempio, se il cliente applica COHF 1.x.3, COHF 1.x.3. = COHF 1.x.1 + COHF 1.x.2.</td>
  </tr>
  <tr>
   <td><strong>Documentazione</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Cadenza</strong></td>
   <td><p>Se necessario</p> </td>
  </tr>
  <tr>
   <td><strong>Disponibilità e installazione</strong></td>
   <td>
    <ul>
     <li>Il processo di installazione COFP è stato semplificato per migliorare l'esperienza del cliente. (I clienti possono semplicemente installare un singolo pacchetto per tutti i componenti).</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Livello di test</strong></td>
   <td><p>QA convalidato</p> </td>
  </tr>
 </tbody>
</table>

## Correzione {#hot-fix}

<table>
 <tbody>
  <tr>
   <td><strong>Definizione</strong></td>
   <td><p>Pacchetto che include uno o più file creati per risolvere un difetto del prodotto che riduce in modo significativo i servizi essenziali o influisce in modo significativo sulle operazioni aziendali. </p> </td>
  </tr>
  <tr>
   <td><strong>Denominazione</strong></td>
   <td>cq-&lt;Versione Rilascio&gt;-hotfix-&lt;ID hotfix&gt;-&lt;versione hotfix&gt;</td>
  </tr>
  <tr>
   <td><strong>Inclusioni</strong></td>
   <td>Include correzioni per un problema specifico</td>
  </tr>
  <tr>
   <td><strong>Documentazione</strong></td>
   <td>Le note sulla versione degli hotfix pubblici sono disponibili solo su richiesta del cliente tramite il portale di assistenza AEM.</td>
  </tr>
  <tr>
   <td><strong>Cadenza</strong></td>
   <td>Se necessario</td>
  </tr>
  <tr>
   <td><strong>Disponibilità e installazione</strong></td>
   <td>
    <ul>
     <li>Consegnato come pacchetto</li>
     <li>Disponibile su Package Share</li>
     <li>A seconda dell'ultimo service pack rilasciato</li>
     <li>La maggior parte delle correzioni rapide è autonoma, a meno che non sia specificato. Può essere installato in qualsiasi ordine. Può essere verificato tramite la scheda Dettagli condivisione pacchetto dell'elemento Dependencies (Dipendenze).</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Livello di test</strong></td>
   <td>
    <ul>
     <li>Convalidato dall'Assistenza clienti</li>
     <li>Le correzioni rapide di AEM non beneficiano dello stesso livello di garanzia qualità dei service pack o delle release del prodotto. Pertanto, devono essere convalidati in un ambiente di pre-produzione come parte dei processi di distribuzione di qualità.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Sovrapposizione {#overlay}

<table>
 <tbody>
  <tr>
   <td><strong>Definizione</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Denominazione</strong></td>
   <td>overlay-&lt;ID ticket&gt;</td>
  </tr>
  <tr>
   <td><strong>Inclusioni</strong></td>
   <td>Correzione di bug per un file JS o JSP</td>
  </tr>
  <tr>
   <td><strong>Documentazione</strong></td>
   <td>Nessuno</td>
  </tr>
  <tr>
   <td><strong>Cadenza</strong></td>
   <td>Se necessario</td>
  </tr>
  <tr>
   <td><strong>Disponibilità e installazione</strong></td>
   <td>
    <ul>
     <li>Fornito come pacchetto dall'assistenza clienti AEM</li>
     <li>Non necessariamente incluso nei service pack o nelle versioni complete</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Livello di test</strong></td>
   <td>Convalidato dall'Assistenza clienti</td>
  </tr>
 </tbody>
</table>

## Feature Pack {#feature-pack}

<table>
 <tbody>
  <tr>
   <td><strong>Definizione</strong></td>
   <td>
    <ul>
     <li>I Feature Pack sono funzionalità aggiuntive e vengono forniti tramite Service Pack. Se una versione di AEM ha rilasciato l’ultimo service pack, Adobe non invierà alcun feature pack per tale versione in futuro.</li>
     <li>I PQ contengono miglioramenti del prodotto, pianificati per una versione successiva del prodotto, ma consegnati in anticipo in base alla decisione di Adobe Product Management.</li>
     <li>Le funzioni vengono sempre unite con la versione principale successiva e quindi riportate alla versione AEM richiesta dal cliente</li>
     <li>I pacchetti di funzioni di interesse comune e GA vengono uniti nel service pack successivo</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Denominazione</strong></td>
   <td>cq-&lt;Versione Rilascio&gt;-featurepack-&lt;ID Feature Pack&gt;-&lt;versione Feature Pack&gt;</td>
  </tr>
  <tr>
   <td><strong>Inclusioni</strong></td>
   <td>
    <ul>
     <li>Nuove funzioni</li>
     <li>Miglioramenti</li>
     <li>Correzioni di bug (aggiornamenti di prodotto incrementali)</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Documentazione</strong></td>
   <td>La documentazione è disponibile su helpx.adobe.com.</td>
  </tr>
  <tr>
   <td><strong>Cadenza</strong></td>
   <td>Varia con area prodotto</td>
  </tr>
  <tr>
   <td><strong>Disponibilità e installazione</strong></td>
   <td>
    <ul>
     <li>Consegnato tramite Service Pack</li>
     <li>Disponibile in Package Share. I clienti accettano i termini e le condizioni di Adobe tramite Package Share.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Livello di test</strong></td>
   <td>I pacchetti di funzioni di disponibilità generale sono convalidati dal QA</td>
  </tr>
 </tbody>
</table>

* [1]: Le correzioni OAK non vengono distribuite come singole correzioni rapide. Tuttavia, sono inclusi nella successiva correzione cumulativa per la quercia. Se necessario, è possibile mettere a disposizione una build diagnostica oltre al COFP più recente. La condizione preliminare è che il cliente abbia eseguito il COFP più recente. Le build diagnostiche forniscono solo lo stesso livello di garanzia qualità di una correzione rapida. Pertanto, non forniscono lo stesso livello di garanzia qualità di un fix pack cumulativo, service pack o release del prodotto. La correzione finale viene fornita con il successivo CFP.

