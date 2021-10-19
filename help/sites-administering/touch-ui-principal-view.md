---
title: Visualizzazione principale per la gestione delle autorizzazioni
seo-title: Principal View for Permissions Management
description: Scopri la nuova interfaccia utente touch che facilita la gestione delle autorizzazioni.
seo-description: Learn about the new Touch UI interface that facilitates permissions management.
uuid: 16c5889a-60dd-4b66-bbc4-74fbdb5fc32f
contentOwner: sarchiz
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
discoiquuid: db8665fa-353f-45c2-8e37-169d5c1df873
docset: aem65
exl-id: 4ce19c95-32cb-4bb8-9d6f-a5bc08a3688d
source-git-commit: 4ea49fe6745b23f01f46edfe07ff3dd8c8299729
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 1%

---

# Visualizzazione principale per la gestione delle autorizzazioni{#principal-view-for-permissions-management}

## Panoramica {#overview}

AEM 6.5 introduce la gestione delle autorizzazioni per utenti e gruppi. La funzionalità principale rimane la stessa dell’interfaccia classica, ma è più semplice da usare ed efficiente.

## Guida all’uso {#how-to-use}

### Accesso all’interfaccia utente {#accessing-the-ui}

La nuova gestione delle autorizzazioni basata sull&#39;interfaccia utente è accessibile tramite la scheda Autorizzazioni in Sicurezza come mostrato di seguito:

![](assets/screen_shot_2019-03-17at63333pm.png)

La nuova visualizzazione facilita l&#39;analisi dell&#39;intero insieme di privilegi e restrizioni per una determinata entità principale in tutti i percorsi in cui le autorizzazioni sono state concesse esplicitamente. Questo elimina la necessità di passare a

CRXDE per gestire privilegi e restrizioni avanzati. È stato consolidato nella stessa prospettiva. Per impostazione predefinita, la visualizzazione è impostata sul gruppo &quot;tutti&quot;.

![](assets/unu-1.png)

Esiste un filtro che consente all&#39;utente di selezionare il tipo di entità da esaminare **Utenti**, **Gruppi** oppure **Tutto** e cerca qualsiasi entità&#x200B;**.**

![](assets/image2019-3-20_23-52-51.png)

### Visualizzazione delle autorizzazioni per un entità {#viewing-permissions-for-a-principal}

La cornice a sinistra consente agli utenti di scorrere verso il basso per trovare un&#39;entità principale o cercare un gruppo o un utente in base al filtro selezionato, come illustrato di seguito:

![](assets/doi-1.png)

Facendo clic sul nome vengono visualizzate le autorizzazioni assegnate a destra. Il riquadro delle autorizzazioni mostra l&#39;elenco delle voci di controllo accessi su percorsi specifici insieme alle restrizioni configurate.

![](assets/trei-1.png)

### Aggiunta di una nuova voce di controllo di accesso per un Principale {#adding-new-access-control-entry-for-a-principal}

È possibile aggiungere nuove autorizzazioni aggiungendo una nuova voce Controllo accessi facendo clic sul pulsante Aggiungi ACE .

![](assets/patru.png)

Viene visualizzata la finestra mostrata di seguito, il passaggio successivo consiste nel scegliere un percorso in cui l’autorizzazione deve essere configurata.

![](assets/cinci-1.png)

Qui selezioniamo un percorso in cui desideri configurare un’autorizzazione per **utenti dam**:

![](assets/sase-1.png)

Dopo aver selezionato il percorso, il flusso di lavoro torna a questa schermata, in cui l’utente può quindi selezionare uno o più privilegi dai namespace disponibili (come `jcr`, `rep` o `crx`) come mostrato di seguito.

I privilegi possono essere aggiunti ricercando utilizzando il campo di testo e quindi selezionando dall’elenco.

>[!NOTE]
>
>Per un elenco completo dei privilegi e delle descrizioni, consulta [questa pagina](/help/sites-administering/user-group-ac-admin.md#access-right-management).

![](assets/image2019-3-21_0-5-47.png) ![](assets/image2019-3-21_0-6-53.png)

Dopo aver selezionato l’elenco dei privilegi, l’utente può scegliere il Tipo di autorizzazione : Rifiuta o consenti, come illustrato di seguito.

![](assets/screen_shot_2019-03-17at63938pm.png) ![](assets/screen_shot_2019-03-17at63947pm.png)

### Utilizzo di restrizioni {#using-restrictions}

Oltre all&#39;elenco dei privilegi e al Tipo di autorizzazione su un determinato percorso, questa schermata consente anche di aggiungere restrizioni per il controllo accessi a grana fine come mostrato di seguito:

![](assets/image2019-3-21_1-4-14.png)

>[!NOTE]
>
>Per maggiori informazioni sul significato di ciascuna restrizione, consulta [Documentazione di Jackrabbit Oak](http://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html).

È possibile aggiungere restrizioni come mostrato di seguito scegliendo il tipo di restrizione, inserendo il valore e premendo il pulsante **+** icona.

![](assets/sapte-1.png) ![](assets/opt-1.png)

Il nuovo ACE si riflette nell&#39;elenco di controllo accessi come mostrato di seguito. Tieni presente che `jcr:write` è un privilegio aggregato che include `jcr:removeNode` che è stato aggiunto sopra, ma non è mostrato sotto come il suo coperto `jcr:write`.

### Modifica degli ACE {#editing-aces}

È possibile modificare le voci di controllo degli accessi selezionando un&#39;entità e scegliendo l&#39;ACE che si desidera modificare.

Ad esempio, qui puoi modificare la voce seguente per **utenti dam** facendo clic sull’icona a forma di matita a destra:

![Aggiungi restrizione](assets/image2019-3-21_0-35-39.png)

La schermata di modifica viene visualizzata con gli ACE configurati preselezionati, che possono essere eliminati facendo clic sull&#39;icona incrociata accanto a essi o nuovi privilegi possono essere aggiunti per il percorso specificato, come mostrato di seguito.

![Modifica voce](assets/noua-1.png)

In questa sezione viene aggiunta la variabile `addChildNodes` privilegio **utenti dam** sul percorso indicato.

![](assets/image2019-3-21_0-45-35.png)

Le modifiche possono essere salvate facendo clic sul pulsante **Salva** in alto a destra, e le modifiche si rifletteranno sulle nuove autorizzazioni per **dam-users **come mostrato di seguito:

![](assets/zece-1.png)

### Eliminazione degli ACE {#deleting-aces}

Le voci di controllo di accesso possono essere eliminate per rimuovere tutte le autorizzazioni concesse a un&#39;entità in un percorso specifico. L’icona X accanto a ACE può essere utilizzata per eliminarla come mostrato di seguito:

![](assets/image2019-3-21_0-53-19.png) ![](assets/unspe.png)

### Combinazioni di privilegi per l’interfaccia classica {#classic-ui-privilege-combinations}

La nuova interfaccia utente delle autorizzazioni utilizza in modo esplicito il set di privilegi di base invece delle combinazioni predefinite che non riflettono esattamente i privilegi sottostanti concessi.

Ciò causava confusione in merito alla configurazione esatta. La tabella seguente elenca la mappatura tra le combinazioni di privilegi dall’interfaccia classica ai privilegi effettivi che le costituiscono:

<table>
 <tbody>
  <tr>
   <th>Combinazioni di privilegi per l’interfaccia classica</th>
   <th>Privilegio interfaccia utente autorizzazioni</th>
  </tr>
  <tr>
   <td>Leggi</td>
   <td><code>jcr:read</code></td>
  </tr>
  <tr>
   <td>Modifica</td>
   <td><p><code>jcr:modifyProperties</code></p> <p><code>jcr:lockManagement</code></p> <p><code>jcr:versionManagement</code></p> </td>
  </tr>
  <tr>
   <td>Crea</td>
   <td><p><code>jcr:addChildNodes</code></p> <p><code>jcr:nodeTypeManagement</code></p> </td>
  </tr>
  <tr>
   <td>Elimina</td>
   <td><p><code>jcr:removeNode</code></p> <p><code>jcr:removeChildNodes</code></p> </td>
  </tr>
  <tr>
   <td>Leggi ACL</td>
   <td><code>jcr:readAccessControl</code></td>
  </tr>
  <tr>
   <td>Modifica ACL</td>
   <td><code>jcr:modifyAccessControl</code></td>
  </tr>
  <tr>
   <td>Replica</td>
   <td><code>crx:replicate</code></td>
  </tr>
 </tbody>
</table>
