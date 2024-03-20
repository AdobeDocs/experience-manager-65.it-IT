---
title: Conflitti di rollout MSM
description: Scopri come gestire i conflitti di rollout di Multi Site Manager.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
feature: Multi Site Manager
exl-id: e145e79a-c363-4a33-b9f9-99502ed20563
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 18%

---

# Conflitti di rollout MSM{#msm-rollout-conflicts}

Possono verificarsi conflitti se nuove pagine con lo stesso nome vengono create sia nel ramo blueprint che in un ramo Live Copy dipendente.

Tali conflitti devono essere gestiti e risolti al momento del rollout.

## Gestione dei conflitti {#conflict-handling}

Quando esistono delle pagine in conflitto (nei rami blueprint e Live Copy), MSM ti consente di definire come (o anche se) devono essere gestite.

Per garantire che il rollout non sia bloccato, le definizioni possibili possono includere:

* quale pagina (blueprint o live copy) ha la priorità durante il rollout,
* quali pagine vengono rinominate (e come),
* come questo influisce su qualsiasi contenuto pubblicato.

  Il comportamento predefinito di Adobe Experience Manager (AEM) è che il contenuto pubblicato non è interessato. Pertanto, se una pagina creata manualmente nel ramo Live Copy è stata pubblicata, il contenuto viene comunque pubblicato dopo la gestione e il rollout dei conflitti.

Oltre alla funzionalità standard, è possibile aggiungere gestori di conflitti personalizzati per implementare regole diverse. Questi possono anche consentire la pubblicazione di azioni come un singolo processo.

### Esempio di scenario {#example-scenario}

Nelle sezioni seguenti è necessario utilizzare l&#39;esempio di una nuova pagina `b`, creato sia nel ramo blueprint che Live Copy (creato manualmente), per illustrare i vari metodi di risoluzione dei conflitti:

* blueprint: `/b`

  Una pagina master; con una pagina figlio, bp-level-1.

* live copy: `/b`

  Una pagina creata manualmente nel ramo Live Copy; con una pagina figlio, `lc-level-1`.

   * Attivato al momento della pubblicazione come `/b`, insieme alla pagina figlio.

**Prima del rollout**

<table>
 <tbody>
  <tr>
   <td><strong>blueprint prima del rollout</strong></td>
   <td><strong>live copy prima del rollout</strong></td>
   <td><strong>pubblica prima del rollout</strong></td>
  </tr>
  <tr>
   <td><code>b</code><br /> <br /> (creato nel ramo blueprint, pronto per il rollout)<br /> </td>
   <td><code>b</code><br /> <br /> (creato manualmente nel ramo live copy)<br /> </td>
   <td><code>b</code><br /> <br /> (contiene il contenuto della pagina b creato manualmente nel ramo live copy)</td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code> /lc-level-1</code><br /> <br /> (creato manualmente nel ramo live copy)<br /> </td>
   <td><code> /lc-level-1</code><br /> <br /> (contiene il contenuto della pagina)<br /> child-level-1 creato manualmente nel ramo live copy)</td>
  </tr>
 </tbody>
</table>

## Gestione rollout e gestione dei conflitti {#rollout-manager-and-conflict-handling}

La gestione del rollout consente di attivare o disattivare la gestione dei conflitti.

Questa operazione viene eseguita utilizzando [Configurazione OSGi](/help/sites-deploying/configuring-osgi.md) di **Day CQ WCM Rollout Manager**:

* **Gestire i conflitti con le pagine create manualmente**:

  ( `rolloutmgr.conflicthandling.enabled`)

  Impostato su true se il gestore di rollout deve gestire i conflitti da una pagina creata nella Live Copy con un nome esistente nella blueprint.

L’AEM ha [comportamento predefinito quando la gestione dei conflitti è stata disattivata](#behavior-when-conflict-handling-deactivated).

## Gestori dei conflitti {#conflict-handlers}

L’AEM utilizza gestori di conflitti per risolvere eventuali conflitti di pagina esistenti durante il rollout del contenuto da blueprint a Live Copy. La ridenominazione delle pagine è uno dei metodi più comuni per risolvere tali conflitti. Per consentire la selezione di diversi comportamenti, è possibile utilizzare più gestori di conflitti.

AEM fornisce:

* Il [gestore di conflitti predefinito](#default-conflict-handler):

   * `ResourceNameRolloutConflictHandler`

* La possibilità di attuare una [gestore personalizzato](#customized-handlers).
* Meccanismo di classificazione del servizio che consente di impostare la priorità di ogni singolo gestore. Viene utilizzato il servizio con la classificazione più alta.

### Gestore dei conflitti predefinito {#default-conflict-handler}

Il gestore di conflitti predefinito:

* Si chiama `ResourceNameRolloutConflictHandler`

* Con questo gestore, la pagina blueprint ha la precedenza.
* La classificazione del servizio per questo gestore è impostata su bassa (ovvero al di sotto del valore predefinito per il `service.ranking` proprietà ) poiché si presume che i gestori personalizzati necessitino di una classificazione più elevata. Tuttavia, la classificazione non è il valore minimo assoluto per garantire flessibilità quando necessario.

Questo gestore di conflitti ha la precedenza sulla blueprint. Pagina Live Copy `/b` viene spostato (all’interno del ramo live copy) in `/b_msm_moved`.

* live copy: `/b`

  Viene spostato (all’interno della Live Copy) in `/b_msm_moved`. Questo funge da backup e assicura che non venga perso alcun contenuto.

   * `lc-level-1` non viene spostato.

* blueprint: `/b`

  Viene distribuito alla pagina Live Copy `/b`.

   * `bp-level-1` viene distribuito nella Live Copy.

**Dopo il rollout**

<table>
 <tbody>
  <tr>
   <td><strong>blueprint dopo il rollout</strong></td>
   <td><strong>live copy dopo il rollout</strong><br /> </td>
   <td></td>
   <td><strong>live copy dopo il rollout</strong><br /> <br /> <br /> </td>
   <td><strong>pubblica dopo il rollout</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code><br /> <br /> (contiene il contenuto della pagina blueprint b su cui è stato eseguito il rollout)<br /> </td>
   <td></td>
   <td><code>b_msm_moved</code><br /> <br /> (contiene il contenuto della pagina b creato manualmente nel ramo live copy)</td>
   <td><code>b</code><br /> <br /> (nessuna modifica; contiene il contenuto della pagina originale b creato manualmente nel ramo live copy e ora denominato b_msm_move)<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code class="code"> /bp-level-1</code></td>
   <td><code> /lc-level-1</code><br /> <br /> (nessuna modifica)</td>
   <td><code> </code></td>
   <td><code> /lc-level-1</code><br /> <br /> (nessuna modifica)</td>
  </tr>
 </tbody>
</table>

### Gestori personalizzati {#customized-handlers}

I gestori di conflitti personalizzati ti consentono di implementare regole personalizzate. Utilizzando il meccanismo di classificazione del servizio è inoltre possibile definire il modo in cui interagiscono con altri gestori.

I gestori di conflitti personalizzati possono disporre dei seguenti elementi:

* Nome in base alle tue esigenze.
* Sviluppato/configurato in base alle tue esigenze; ad esempio, puoi sviluppare un gestore in modo che la pagina Live Copy abbia la precedenza.
* Progettato per essere configurato utilizzando [Configurazione OSGi](/help/sites-deploying/configuring-osgi.md), in particolare:

   * **Classifica dei servizi**:

     Definisce l&#39;ordine relativo ad altri gestori di conflitti ( `service.ranking`).

     Il valore predefinito è 0.

### Comportamento quando la gestione dei conflitti è disattivata {#behavior-when-conflict-handling-deactivated}

Se si esegue manualmente [disattivare la gestione dei conflitti](#rollout-manager-and-conflict-handling), l’AEM non interviene su alcuna pagina in conflitto (le pagine non in conflitto vengono distribuite come previsto).

>[!CAUTION]
>
>L’AEM non fornisce alcuna indicazione che i conflitti vengano ignorati, in quanto questo comportamento deve essere configurato in modo esplicito, pertanto si presume che sia il comportamento richiesto.

In questo caso, la Live Copy ha effettivamente la precedenza. La pagina blueprint `/b` non viene copiato e la pagina live copy `/b` viene lasciato intatto.

* blueprint: `/b`

  Non viene copiato, ma viene ignorato.

* live copy: `/b`

  Lo stesso.

<table>
 <caption>
   Dopo il rollout
 </caption>
 <tbody>
  <tr>
   <td><strong>blueprint dopo il rollout</strong></td>
   <td><strong>live copy dopo il rollout</strong><br /> <br /> <br /> </td>
   <td><strong>pubblica dopo il rollout</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code><br /> <br /> (nessuna modifica; presenta il contenuto della pagina b creato manualmente nel ramo live copy)</td>
   <td><code>b</code><br /> <br /> (nessuna modifica; contiene il contenuto della pagina b creato manualmente nel ramo live copy)<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code><br /> </td>
   <td><code> /lc-level-1</code><br /> <br /> (nessuna modifica)</td>
   <td><code> /lc-level-1</code><br /> <br /> (nessuna modifica)</td>
  </tr>
 </tbody>
</table>

### Classificazioni di servizio {#service-rankings}

La classificazione del servizio [OSGi](https://www.osgi.org/) può essere utilizzata per definire la priorità dei singoli gestori di conflitti.
