---
title: Conflitti di rollout MSM
seo-title: MSM Rollout Conflicts
description: Scopri come gestire i conflitti di rollout di Multi Site Manager.
seo-description: Learn how to deal with Multi Site Manager rollout conflicts.
uuid: 7a640905-aae2-498e-b95c-2c73008fa1cd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 16db5334-604f-44e2-9993-10d683dee5bb
feature: Multi Site Manager
exl-id: e145e79a-c363-4a33-b9f9-99502ed20563
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 31%

---

# Conflitti di rollout MSM{#msm-rollout-conflicts}

Possono verificarsi conflitti se vengono create nuove pagine con lo stesso nome di pagina sia nel ramo blueprint che in un ramo Live Copy dipendente.

Tali conflitti devono essere gestiti e risolti al momento del rollout.

## Gestione dei conflitti {#conflict-handling}

In presenza di pagine in conflitto (nei rami blueprint e Live Copy), MSM ti consente di definire come (o anche se) devono essere gestite.

Per garantire che il rollout non sia bloccato, le definizioni possibili possono includere:

* quale pagina (blueprint o Live Copy) avrà priorità durante il rollout,
* quali pagine verranno rinominate (e come),
* questo influisce su eventuali contenuti pubblicati.

   Il comportamento predefinito di AEM (preconfigurato) consiste nel fatto che il contenuto pubblicato non sarà interessato. Quindi, se è stata pubblicata una pagina creata manualmente nel ramo Live Copy, il contenuto verrà comunque pubblicato dopo la gestione e il rollout dei conflitti.

Oltre alla funzionalità standard, è possibile aggiungere gestori di conflitti personalizzati per implementare regole diverse. Questi possono anche consentire la pubblicazione di azioni come un singolo processo.

### Esempio di scenario {#example-scenario}

Nelle sezioni seguenti viene utilizzato l’esempio di una nuova pagina `b`, creato sia nella blueprint che nel ramo Live Copy (creato manualmente), per illustrare i vari metodi di risoluzione dei conflitti:

* blueprint: `/b`

   Una pagina master; con 1 pagina figlio, bp-level-1.

* Live Copy: `/b`

   Una pagina creata manualmente nel ramo Live Copy; con 1 pagina figlio, `lc-level-1`.

   * Attivato al momento della pubblicazione come `/b`, insieme alla pagina figlio.

**Prima del rollout**

<table>
 <tbody>
  <tr>
   <td><strong>blueprint prima del rollout</strong></td>
   <td><strong>Live Copy prima del rollout</strong></td>
   <td><strong>pubblicare prima del rollout</strong></td>
  </tr>
  <tr>
   <td><code>b</code> <br /> (creato nel ramo blueprint, pronto per il rollout)<br /> </td>
   <td><code>b</code> <br /> (creato manualmente nel ramo Live Copy)<br /> </td>
   <td><code>b</code> <br /> (contiene il contenuto della pagina b che è stata creata manualmente nel ramo Live Copy)</td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code> /lc-level-1</code> <br /> (creato manualmente nel ramo Live Copy)<br /> </td>
   <td><code> /lc-level-1</code> <br /> (contiene il contenuto della pagina<br /> livello-1 figlio creato manualmente nel ramo Live Copy)</td>
  </tr>
 </tbody>
</table>

## Gestione rollout e gestione dei conflitti {#rollout-manager-and-conflict-handling}

La gestione del rollout consente di attivare o disattivare la gestione dei conflitti.

Questa operazione viene eseguita utilizzando [Configurazione OSGi](/help/sites-deploying/configuring-osgi.md) di **Day CQ WCM Rollout Manager**:

* **Gestisci i conflitti con le pagine create manualmente**:

   ( `rolloutmgr.conflicthandling.enabled`)

   Imposta su true se il gestore di rollout deve gestire i conflitti di una pagina creata nella Live Copy con un nome esistente nella blueprint.

AEM segue un [comportamento predefinito quando la gestione dei conflitti è stata disattivata](#behavior-when-conflict-handling-deactivated).

## Gestori dei conflitti {#conflict-handlers}

AEM utilizza gestori di conflitti per risolvere eventuali conflitti di pagina esistenti durante il rollout del contenuto da una blueprint a una Live Copy. La ridenominazione delle pagine è uno dei metodi più comuni per risolvere tali conflitti. Per consentire la selezione di diversi comportamenti, è possibile utilizzare più gestori di conflitti.

AEM fornisce:

* Il [gestore di conflitti predefinito](#default-conflict-handler):

   * `ResourceNameRolloutConflictHandler`

* Possibilità di implementare un [gestore personalizzato](#customized-handlers).
* Meccanismo di classificazione del servizio che consente di impostare la priorità di ogni singolo gestore. Viene utilizzato il servizio con la classificazione più alta.

### Gestore dei conflitti predefinito {#default-conflict-handler}

Il gestore di conflitti predefinito:

* È chiamato `ResourceNameRolloutConflictHandler`

* Con questo gestore la pagina blueprint ha la precedenza.
* La classificazione del servizio per questo gestore è impostata su bassa ( &quot;cioè sotto il valore predefinito per `service.ranking` proprietà) poiché si presume che i gestori personalizzati avranno bisogno di una classificazione più alta. Tuttavia, la classificazione non è il valore minimo assoluto per garantire flessibilità quando necessario.

Questo gestore di conflitti ha la precedenza sulla blueprint. La pagina Live Copy `/b` viene spostato (all’interno del ramo Live Copy) in `/b_msm_moved`.

* Live Copy: `/b`

   Viene spostato (all’interno della Live Copy) in `/b_msm_moved`. Questo funge da backup e assicura che non venga perso alcun contenuto.

   * `lc-level-1` non viene spostato.

* blueprint: `/b`

   Viene eseguito il rollout nella pagina Live Copy `/b`.

   * `bp-level-1` viene implementato nella Live Copy.

**Dopo il rollout**

<table>
 <tbody>
  <tr>
   <td><strong>blueprint dopo il rollout</strong></td>
   <td><strong>live copy dopo il rollout</strong><br /> </td>
   <td></td>
   <td><strong>live copy dopo il rollout</strong><br /> <br /> <br /> </td>
   <td><strong>pubblicare dopo il rollout</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code> <br /> (presenta il contenuto della pagina blueprint b che è stata implementata)<br /> </td>
   <td></td>
   <td><code>b_msm_moved</code> <br /> (presenta il contenuto della pagina b che è stata creata manualmente nel ramo Live Copy)</td>
   <td><code>b</code> <br /> (nessuna modifica; contiene il contenuto della pagina originale b creato manualmente nel ramo Live Copy e ora denominato b_msm_move)<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code class="code"> /bp-level-1</code></td>
   <td><code> /lc-level-1</code> <br /> (nessuna modifica)</td>
   <td><code> </code></td>
   <td><code> /lc-level-1</code> <br /> (nessuna modifica)</td>
  </tr>
 </tbody>
</table>

### Gestori personalizzati {#customized-handlers}

I gestori di conflitti personalizzati ti consentono di implementare regole personalizzate. Utilizzando il meccanismo di classificazione del servizio è inoltre possibile definire il modo in cui interagiscono con altri gestori.

I gestori di conflitti personalizzati possono:

* Essere nominati in base alle tue esigenze.
* essere sviluppati/configurati in base alle proprie esigenze; ad esempio, puoi sviluppare un gestore in modo che la pagina Live Copy abbia la precedenza.
* Può essere progettato per essere configurato utilizzando [Configurazione OSGi](/help/sites-deploying/configuring-osgi.md); in particolare:

   * **Classifica dei servizi**:

      Definisce l&#39;ordine relativo ad altri gestori di conflitti ( `service.ranking`).

      Il valore predefinito è 0.

### Comportamento quando la gestione dei conflitti è disattivata {#behavior-when-conflict-handling-deactivated}

Se manualmente [disattivare la gestione dei conflitti](#rollout-manager-and-conflict-handling) quindi AEM non esegue alcuna azione su alcuna pagina in conflitto (le pagine non in conflitto vengono distribuite come previsto).

>[!CAUTION]
>
>AEM non fornisce alcuna indicazione che i conflitti vengono ignorati in quanto questo comportamento deve essere configurato in modo esplicito, quindi si presume che sia il comportamento richiesto.

In questo caso la Live Copy ha effettivamente la precedenza. La pagina blueprint `/b` non viene copiata e la pagina Live Copy `/b` è lasciato intatto.

* blueprint: `/b`

   Non viene copiata, ma viene ignorata.

* Live Copy: `/b`

   Rimane la stessa.

<table>
 <caption>
   Dopo il rollout
 </caption>
 <tbody>
  <tr>
   <td><strong>blueprint dopo il rollout</strong></td>
   <td><strong>live copy dopo il rollout</strong><br /> <br /> <br /> </td>
   <td><strong>pubblicare dopo il rollout</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code> <br /> (nessuna modifica; ha il contenuto della pagina b che è stata creata manualmente nel ramo Live Copy)</td>
   <td><code>b</code> <br /> (nessuna modifica; contiene il contenuto della pagina b che è stata creata manualmente nel ramo Live Copy)<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code> </td>
   <td><code> /lc-level-1</code> <br /> (nessuna modifica)</td>
   <td><code> /lc-level-1</code> <br /> (nessuna modifica)</td>
  </tr>
 </tbody>
</table>

### Classificazioni di servizio {#service-rankings}

La classificazione del servizio [OSGi](https://www.osgi.org/) può essere utilizzata per definire la priorità dei singoli gestori di conflitti.
