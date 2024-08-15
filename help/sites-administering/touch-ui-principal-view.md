---
title: Visualizzazione entità per la gestione delle autorizzazioni
description: Scopri la nuova interfaccia utente touch che facilita la gestione delle autorizzazioni.
contentOwner: sarchiz
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
docset: aem65
exl-id: 4ce19c95-32cb-4bb8-9d6f-a5bc08a3688d
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 6f3c4f4aa4183552492c6ce5039816896bd67495
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 1%

---


# Visualizzazione entità per la gestione delle autorizzazioni{#principal-view-for-permissions-management}

## Panoramica {#overview}

AEM 6.5 introduce la gestione delle autorizzazioni per utenti e gruppi. La funzionalità principale rimane la stessa dell’interfaccia classica, ma è più semplice ed efficiente.

## Guida all’uso {#how-to-use}

### Accesso all’interfaccia utente {#accessing-the-ui}

La nuova gestione delle autorizzazioni basata sull’interfaccia utente è accessibile tramite la scheda Autorizzazioni in Sicurezza, come illustrato di seguito:

![Interfaccia utente per la gestione delle autorizzazioni](assets/screen_shot_2019-03-17at63333pm.png)

La nuova visualizzazione consente di esaminare più facilmente l’intero insieme di privilegi e restrizioni per una determinata entità principale in tutti i percorsi in cui sono state concesse esplicitamente le autorizzazioni. Questo elimina la necessità di passare a

CRXDE per gestire privilegi e restrizioni avanzati. È stato consolidato nella stessa visualizzazione. Il valore predefinito della visualizzazione è Gruppo &quot;tutti&quot;.

![Visualizzazione del gruppo &quot;tutti&quot;](assets/unu-1.png)

È disponibile un filtro che consente all&#39;utente di selezionare il tipo di entità da esaminare **Utenti**, **Gruppi** o **Tutti** e cercare un&#39;entità&#x200B;**.**

![Cerca tipi di entità](assets/image2019-3-20_23-52-51.png)

### Visualizzazione delle autorizzazioni per un’entità {#viewing-permissions-for-a-principal}

Il frame a sinistra consente agli utenti di scorrere verso il basso per trovare un’entità principale o cercare un gruppo o un utente in base al filtro selezionato, come illustrato di seguito:

![Visualizza autorizzazioni per entità](assets/doi-1.png)

Facendo clic sul nome, a destra vengono visualizzate le autorizzazioni assegnate. Nel riquadro delle autorizzazioni viene visualizzato l&#39;elenco delle voci di controllo di accesso in percorsi specifici con le limitazioni configurate.

![Visualizza elenco ACL](assets/trei-1.png)

### Aggiunta di una nuova voce di controllo di accesso per un&#39;entità {#adding-new-access-control-entry-for-a-principal}

È possibile aggiungere nuove autorizzazioni aggiungendo una voce di controllo di accesso. È sufficiente fare clic sul pulsante Aggiungi ACE.

![Aggiungi nuovo ACL per entità](assets/patru.png)

Viene visualizzata la finestra mostrata di seguito. Il passaggio successivo consiste nel scegliere un percorso in cui configurare l’autorizzazione.

![Configura percorso autorizzazioni](assets/cinci-1.png)

In questo caso, viene selezionato un percorso in cui è possibile configurare un&#39;autorizzazione per **dam-users**:

![Configurazione di esempio per dam-users](assets/sase-1.png)

Dopo aver selezionato il percorso, il flusso di lavoro torna a questa schermata, in cui l&#39;utente può selezionare uno o più privilegi dagli spazi dei nomi disponibili (ad esempio `jcr`, `rep` o `crx`) come mostrato di seguito.

I privilegi possono essere aggiunti effettuando una ricerca utilizzando il campo di testo e selezionando dall’elenco.

>[!NOTE]
>
>Per un elenco completo dei privilegi e delle descrizioni, vedere [User, Group, and Access Rights Administration](/help/sites-administering/user-group-ac-admin.md#access-right-management).

![Autorizzazione di ricerca per un determinato percorso.](assets/image2019-3-21_0-5-47.png) ![Aggiungi nuova voce per &#39;dam-users&#39; come mostrato da un percorso selezionato in colonne verticali.](assets/image2019-3-21_0-6-53.png)

Dopo aver selezionato l&#39;elenco dei privilegi, l&#39;utente può scegliere il Tipo di autorizzazione: Nega o Consenti, come illustrato di seguito.

![Seleziona autorizzazione](assets/screen_shot_2019-03-17at63938pm.png) ![Seleziona autorizzazione](assets/screen_shot_2019-03-17at63947pm.png)

### Utilizzo delle restrizioni {#using-restrictions}

Oltre all’elenco dei privilegi e al tipo di autorizzazione su un determinato percorso, questa schermata consente di aggiungere restrizioni per il controllo degli accessi a grana fine, come illustrato di seguito:

![Aggiungi restrizioni](assets/image2019-3-21_1-4-14.png)

>[!NOTE]
>
>Per ulteriori informazioni sul significato di ciascuna restrizione, vedere [la documentazione di Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html).

Le restrizioni possono essere aggiunte come mostrato di seguito scegliendo il tipo di restrizione, immettendo il valore e premendo l&#39;icona **+**.

![Aggiungere il tipo di restrizione](assets/sapte-1.png) ![Aggiungere il tipo di restrizione](assets/opt-1.png)

La nuova voce ACE viene visualizzata nell&#39;elenco di controllo di accesso come illustrato di seguito. Si noti che `jcr:write` è un privilegio aggregato che include `jcr:removeNode` aggiunto in precedenza, ma non mostrato di seguito come relativo coperto in `jcr:write`.

### Modifica delle ACE {#editing-aces}

Le voci di controllo di accesso possono essere modificate selezionando un&#39;entità principale e scegliendo l&#39;ACE che si desidera modificare.

Ad esempio, qui puoi modificare la voce seguente per **dam-users** facendo clic sull&#39;icona della matita a destra:

![Aggiungi restrizione](assets/image2019-3-21_0-35-39.png)

Viene visualizzata la schermata di modifica con ACE configurati preselezionati. Per eliminarli, fai clic sull’icona a forma di croce accanto a essi oppure puoi aggiungere nuovi privilegi per il percorso specificato, come illustrato di seguito.

![Modifica voce](assets/noua-1.png)

Qui viene aggiunto il privilegio `addChildNodes` per **dam-users** sul percorso specificato.

![Aggiungi privilegio](assets/image2019-3-21_0-45-35.png)

Le modifiche possono essere salvate facendo clic sul pulsante **Salva** in alto a destra e le modifiche si riflettono nelle nuove autorizzazioni per **dam-users**, come illustrato di seguito:

![Salva modifiche](assets/zece-1.png)

### Eliminazione di ACE {#deleting-aces}

È possibile eliminare le voci di controllo di accesso per rimuovere tutte le autorizzazioni concesse a un utente/gruppo/ruolo in un percorso specifico. L&#39;icona X accanto a ACE può essere utilizzata per eliminarla come illustrato di seguito:

![Elimina ACE](assets/image2019-3-21_0-53-19.png) ![Elimina ACE](assets/unspe.png)

### Combinazioni di privilegi dell’interfaccia classica {#classic-ui-privilege-combinations}

La nuova interfaccia utente delle autorizzazioni utilizza esplicitamente il set di privilegi di base invece di combinazioni predefinite che non riflettono realmente i privilegi sottostanti esatti concessi.

Ciò ha causato confusione su ciò che è esattamente configurato. Nella tabella seguente viene elencato il mapping tra le combinazioni di privilegi dell’interfaccia classica e i privilegi effettivi che le costituiscono:

<table>
 <tbody>
  <tr>
   <th>Combinazioni di privilegi dell’interfaccia classica</th>
   <th>Autorizzazioni UI Privilegio</th>
  </tr>
  <tr>
   <td>Lettura</td>
   <td><code>jcr:read</code></td>
  </tr>
  <tr>
   <td>Modifica</td>
   <td><p><code>jcr:modifyProperties</code></p> <p><code>jcr:lockManagement</code></p> <p><code>jcr:versionManagement</code></p> </td>
  </tr>
  <tr>
   <td>Creare</td>
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
