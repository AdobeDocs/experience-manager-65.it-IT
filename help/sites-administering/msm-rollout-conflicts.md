---
title: Conflitti tra rollout MSM
seo-title: Conflitti tra rollout MSM
description: Scoprite come gestire i conflitti di rollout di Multi Site Manager.
seo-description: Scoprite come gestire i conflitti di rollout di Multi Site Manager.
uuid: 7a640905-aae2-498e-b95c-2c73008fa1cd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 16db5334-604f-44e2-9993-10d683dee5bb
translation-type: tm+mt
source-git-commit: 47b69098a45f774501ebb62ee1a14a8d209ad101
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 0%

---


# Conflitti di rollout MSM{#msm-rollout-conflicts}

Possono verificarsi conflitti se vengono create nuove pagine con lo stesso nome di pagina sia nel ramo blueprint che in un ramo Live Copy dipendente.

Tali conflitti devono essere gestiti e risolti al momento dell&#39;implementazione.

## Gestione dei conflitti {#conflict-handling}

In presenza di pagine in conflitto (nelle diramazioni blueprint e Live Copy), MSM consente di definire come (o anche se) devono essere gestite.

Per garantire che il rollout non sia bloccato, le possibili definizioni possono includere:

* quale pagina (blueprint o live copy) avrà priorità durante l’implementazione,
* quali pagine verranno rinominate (e come),
* come questo influirà su qualsiasi contenuto pubblicato.

   Il comportamento predefinito di AEM (out-of-the-box) è che il contenuto pubblicato non verrà influenzato. Pertanto, se una pagina creata manualmente nel ramo Live Copy è stata pubblicata, il contenuto sarà ancora pubblicato dopo la gestione dei conflitti e l&#39;implementazione.

Oltre alla funzionalità standard, è possibile aggiungere gestori di conflitti personalizzati per implementare regole diverse. Possono inoltre consentire la pubblicazione di azioni come un singolo processo.

### Esempio di scenario {#example-scenario}

Nelle sezioni seguenti viene illustrato l&#39;esempio di una nuova pagina `b`, creata sia nel blueprint che nel ramo Live Copy (creata manualmente), per illustrare i vari metodi di risoluzione dei conflitti:

* blueprint: `/b`

   Una pagina master; con 1 pagina figlia, bp-level-1.

* live copy: `/b`

   Una pagina creata manualmente nel ramo Live Copy; con 1 pagina figlia, `lc-level-1`.

   * Attivato alla pubblicazione come `/b`, insieme alla pagina figlia.

**Prima del rollout**

<table>
 <tbody>
  <tr>
   <td><strong>blueprint prima del rollout</strong></td>
   <td><strong>live copy prima del rollout</strong></td>
   <td><strong>pubblica prima del rollout</strong></td>
  </tr>
  <tr>
   <td><code>b</code> <br /> (creato in ramo blueprint, pronto per il rollout)<br /> </td>
   <td><code>b</code> <br /> (creato manualmente nel ramo Live Copy)<br /> </td>
   <td><code>b</code> <br /> (contiene il contenuto della pagina b che è stata creata manualmente nel ramo Live Copy)</td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code> /lc-level-1</code> <br /> (creato manualmente nel ramo Live Copy)<br /> </td>
   <td><code> /lc-level-1</code> <br /> (contiene il contenuto della pagina<br /> livello figlio-1 creata manualmente nel ramo Live Copy)</td>
  </tr>
 </tbody>
</table>

## Gestione rollout e gestione dei conflitti {#rollout-manager-and-conflict-handling}

Il manager rollout consente di attivare o disattivare la gestione dei conflitti.

Questa operazione viene eseguita utilizzando la [configurazione OSGi](/help/sites-deploying/configuring-osgi.md) di **Day CQ WCM Rollout Manager**:

* **Gestione dei conflitti con le pagine** create manualmente:

   ( `rolloutmgr.conflicthandling.enabled`)

   Impostato su true se il manager del rollout deve gestire i conflitti da una pagina creata nella Live Copy con un nome esistente nel blueprint.

AEM ha un comportamento [predefinito quando la gestione dei conflitti è stata disattivata](#behavior-when-conflict-handling-deactivated).

## Gestori conflitti {#conflict-handlers}

AEM utilizza gestori di conflitti per risolvere eventuali conflitti di pagina esistenti durante il rollout del contenuto da una blueprint a una Live Copy. La ridenominazione delle pagine è uno dei metodi più comuni per risolvere tali conflitti. Possono essere operativi più gestori di conflitti per consentire una selezione di comportamenti diversi.

AEM fornisce:

* Il gestore di conflitti [predefinito](#default-conflict-handler):

   * `ResourceNameRolloutConflictHandler`

* Possibilità di implementare un [handler personalizzato](#customized-handlers).
* Meccanismo di classificazione del servizio che consente di impostare la priorità di ogni singolo gestore. Viene utilizzato il servizio con la classificazione più alta.

### Gestore conflitti predefinito {#default-conflict-handler}

Il gestore di conflitti predefinito:

* È denominato `ResourceNameRolloutConflictHandler`

* Con questo gestore, la pagina di blueprint ha la precedenza.
* La classificazione del servizio per questo gestore è impostata su bassa ( &quot;es. sotto il valore predefinito per la proprietà `service.ranking`), in quanto si presuppone che i gestori personalizzati necessitino di una classificazione più elevata. Tuttavia, la classifica non è il minimo assoluto per garantire la flessibilità quando necessario.

Questo gestore di conflitti ha la precedenza sul modello. La pagina della Live Copy `/b` viene spostata (all&#39;interno del ramo Live Copy) in `/b_msm_moved`.

* live copy: `/b`

   Viene spostato (all&#39;interno della Live Copy) in `/b_msm_moved`. Questo funge da backup e assicura che non venga perso alcun contenuto.

   * `lc-level-1` non viene spostato.

* blueprint: `/b`

   Viene eseguito il rollout nella pagina Live Copy `/b`.

   * `bp-level-1` viene implementato nella Live Copy.

**Dopo l&#39;implementazione**

<table>
 <tbody>
  <tr>
   <td><strong>blueprint dopo il rollout</strong></td>
   <td><strong>live copy after rollout</strong><br /> </td>
   <td></td>
   <td><strong>live copy after rollout</strong><br /> <br /> <br /> </td>
   <td><strong>pubblicazione dopo l'implementazione</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code> <br /> (contiene il contenuto della pagina blueprint b che è stata implementata)<br /> </td>
   <td></td>
   <td><code>b_msm_moved</code> <br /> (contiene il contenuto della pagina b che è stata creata manualmente nel ramo Live Copy)</td>
   <td><code>b</code> <br /> (nessuna modifica; contiene il contenuto della pagina originale b che è stata creata manualmente nel ramo Live Copy ed è ora denominata b_msm_move)<br /> </td>
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

I gestori di conflitti personalizzati consentono di implementare le proprie regole. Utilizzando il meccanismo di classificazione del servizio è inoltre possibile definire il modo in cui interagiscono con altri gestori.

I gestori di conflitti personalizzati possono:

* Assegnate un nome in base alle vostre esigenze.
* essere sviluppati/configurati in base alle vostre esigenze; ad esempio, è possibile sviluppare un gestore in modo che la pagina Live Copy abbia la precedenza.
* Può essere configurato utilizzando la [configurazione OSGi](/help/sites-deploying/configuring-osgi.md); in particolare:

   * **Classificazione** servizio:

      Definisce l&#39;ordine relativo ad altri gestori di conflitti ( `service.ranking`).

      Il valore predefinito è 0.

### Comportamento quando la gestione dei conflitti è disattivata {#behavior-when-conflict-handling-deactivated}

Se si disattiva manualmente [la gestione dei conflitti](#rollout-manager-and-conflict-handling), AEM non intervenire su alcuna pagina in conflitto (le pagine non in conflitto vengono distribuite come previsto).

>[!CAUTION]
>
>AEM non indica che i conflitti vengono ignorati in quanto questo comportamento deve essere configurato in modo esplicito, pertanto si presume che sia il comportamento richiesto.

In questo caso la Live Copy ha la precedenza. La pagina di blueprint `/b` non viene copiata e la pagina di live copy `/b` non viene toccata.

* blueprint: `/b`

   Non viene copiato, ma viene ignorato.

* live copy: `/b`

   Resta lo stesso.

<table>
 <caption>
   Dopo l'implementazione
 </caption>
 <tbody>
  <tr>
   <td><strong>blueprint dopo il rollout</strong></td>
   <td><strong>live copy after rollout</strong><br /> <br /> <br /> </td>
   <td><strong>pubblicazione dopo l'implementazione</strong><br /> <br /> </td>
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

### Classificazioni servizio {#service-rankings}

La classificazione [OSGi](https://www.osgi.org/) può essere utilizzata per definire la priorità dei singoli gestori di conflitti.
