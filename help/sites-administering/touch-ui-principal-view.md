---
title: Visualizzazione principale per la gestione delle autorizzazioni
seo-title: Visualizzazione principale per la gestione delle autorizzazioni
description: Scopri la nuova interfaccia utente touch che semplifica la gestione delle autorizzazioni.
seo-description: Scopri la nuova interfaccia utente touch che semplifica la gestione delle autorizzazioni.
uuid: 16c5889a-60dd-4b66-bbc4-74fbdb5fc32f
contentOwner: sarchiz
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
discoiquuid: db8665fa-353f-45c2-8e37-169d5c1df873
docset: aem65
translation-type: tm+mt
source-git-commit: a156e09e77951041dce017f2f78069bc050b6bdb
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 1%

---


# Vista principale per Gestione autorizzazioni{#principal-view-for-permissions-management}

## Panoramica {#overview}

AEM 6.5 introduce la gestione delle autorizzazioni per utenti e gruppi. La funzionalità principale rimane la stessa dell’interfaccia classica, ma è più semplice da usare ed efficiente.

## Guida all’uso {#how-to-use}

### Accesso all&#39;interfaccia {#accessing-the-ui}

La nuova gestione delle autorizzazioni basata sull&#39;interfaccia utente è accessibile dalla scheda Autorizzazioni in Protezione, come illustrato di seguito:

![](assets/screen_shot_2019-03-17at63333pm.png)

La nuova visualizzazione facilita l’analisi dell’intero set di privilegi e restrizioni per una determinata entità in tutti i percorsi in cui le Autorizzazioni sono state concesse esplicitamente. Ciò elimina la necessità di andare a

CRXDE per gestire privilegi e restrizioni avanzati. È stato consolidato nella stessa prospettiva. Per impostazione predefinita, il gruppo è &quot;tutti&quot;.

![](assets/unu-1.png)

È presente un filtro che consente all&#39;utente di selezionare il tipo di entità da esaminare in **Utenti**, **Gruppi** o **Tutti** e cercare qualsiasi entità&#x200B;**.**

![](assets/image2019-3-20_23-52-51.png)

### Visualizzazione delle autorizzazioni per un&#39;entità {#viewing-permissions-for-a-principal}

Il frame a sinistra consente agli utenti di scorrere verso il basso per trovare l&#39;entità o cercare un gruppo o un utente in base al filtro selezionato, come illustrato di seguito:

![](assets/doi-1.png)

Facendo clic sul nome vengono visualizzate le autorizzazioni assegnate a destra. Il riquadro delle autorizzazioni mostra l&#39;elenco delle voci di controllo degli accessi su percorsi specifici, insieme alle restrizioni configurate.

![](assets/trei-1.png)

### Aggiunta di una nuova voce di controllo di accesso per un&#39;entità {#adding-new-access-control-entry-for-a-principal}

È possibile aggiungere nuove autorizzazioni aggiungendo una nuova voce di controllo dell&#39;accesso facendo clic sul pulsante Aggiungi ACE.

![](assets/patru.png)

Viene visualizzata la finestra mostrata di seguito, il passaggio successivo consiste nel scegliere un percorso in cui l&#39;autorizzazione deve essere configurata.

![](assets/cinci-1.png)

Qui si seleziona un percorso in cui si desidera configurare un&#39;autorizzazione per **dam-users**:

![](assets/sase-1.png)

Dopo aver selezionato il percorso, il flusso di lavoro torna a questa schermata, in cui l&#39;utente può selezionare uno o più privilegi dagli spazi dei nomi disponibili (come `jcr`, `rep` o `crx`) come mostrato di seguito.

I privilegi possono essere aggiunti ricercando il campo di testo e quindi selezionando dall&#39;elenco.

>[!NOTE]
>
>Per un elenco completo dei privilegi e delle descrizioni, vedere [questa pagina](/help/sites-administering/user-group-ac-admin.md#access-right-management).

![](assets/image2019-3-21_0-5-47.png) ![](assets/image2019-3-21_0-6-53.png)

Dopo aver selezionato l&#39;elenco dei privilegi, l&#39;utente può scegliere il Tipo di autorizzazione: Rifiuta o Consenti, come illustrato di seguito.

![](assets/screen_shot_2019-03-17at63938pm.png) ![](assets/screen_shot_2019-03-17at63947pm.png)

### Utilizzo di limitazioni {#using-restrictions}

Oltre all&#39;elenco dei privilegi e al tipo di autorizzazione per un determinato percorso, questa schermata consente anche di aggiungere restrizioni per il controllo di accesso con granularità fine, come illustrato di seguito:

![](assets/image2019-3-21_1-4-14.png)

>[!NOTE]
>
>Per ulteriori informazioni sul significato di ogni limitazione, consultare [questa pagina](/help/sites-administering/user-group-ac-admin.md#restrictions).

È possibile aggiungere restrizioni come mostrato di seguito scegliendo il tipo di restrizione, immettendo il valore e premendo l&#39;icona **+**. ![](assets/sapte-1.png) ![](assets/opt-1.png)

Il nuovo controllo ACE si riflette nell&#39;elenco di controllo degli accessi come mostrato di seguito. Tenere presente che `jcr:write` è un privilegio di aggregazione che include `jcr:removeNode` aggiunto sopra, ma che non è mostrato sotto come coperto in `jcr:write`.

### Modifica di ACE {#editing-aces}

Per modificare le voci di controllo di accesso, selezionate un’entità e scegliete l’ACE da modificare.

Ad esempio, qui è possibile modificare la voce seguente per **dam-users** facendo clic sull&#39;icona matita a destra:

![](assets/image2019-3-21_0-35-39.png)

La schermata di modifica viene visualizzata con le voci ACE configurate preselezionate, che possono essere eliminate facendo clic sull’icona a croce accanto a esse oppure con nuovi privilegi per il percorso specificato, come mostrato di seguito.

![](assets/noua-1.png)

Qui si aggiunge il privilegio `addChildNodes` per **dam-users** nel percorso specificato.

![](assets/image2019-3-21_0-45-35.png)

Le modifiche possono essere salvate facendo clic sul pulsante **Salva** in alto a destra, e le modifiche si rifletteranno nelle nuove autorizzazioni per **dam-users **come mostrato di seguito:

![](assets/zece-1.png)

### Eliminazione di ACE {#deleting-aces}

Le voci di controllo di accesso possono essere eliminate per rimuovere tutte le autorizzazioni assegnate a un&#39;entità su un percorso specifico. L’icona X accanto a ACE può essere utilizzata per eliminarla come illustrato di seguito:

![](assets/image2019-3-21_0-53-19.png) ![](assets/unspe.png)

### Combinazioni di privilegi per l&#39;interfaccia classica {#classic-ui-privilege-combinations}

La nuova interfaccia utente delle autorizzazioni utilizza in modo esplicito il set di privilegi di base invece di combinazioni predefinite che non rispecchiano realmente i privilegi sottostanti esatti assegnati.

Ciò causava confusione riguardo alla configurazione esatta. La tabella seguente elenca la mappatura tra le combinazioni di privilegi dall’interfaccia classica e i privilegi effettivi che le costituiscono:

<table>
 <tbody>
  <tr>
   <th>Combinazioni di privilegi per l’interfaccia classica</th>
   <th>Privilegi dell’interfaccia utente Autorizzazioni</th>
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

