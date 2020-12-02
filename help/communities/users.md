---
title: Gestione di utenti e gruppi di utenti
seo-title: Gestione di utenti e gruppi di utenti
description: Gli utenti di  AEM Communities possono registrarsi e modificare i propri profili
seo-description: Gli utenti di  AEM Communities possono registrarsi e modificare i propri profili
uuid: aeba424e-ea7e-4da5-b94f-ea8af4caa7d2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 774c2553-b629-456b-afa7-5713490f4a0a
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '2183'
ht-degree: 0%

---


# Gestione di utenti e gruppi di utenti {#managing-users-and-user-groups}

## Panoramica {#overview}

In  AEM Communities, nell’ambiente di pubblicazione, gli utenti possono registrarsi autonomamente e modificare i propri profili. Considerate le autorizzazioni appropriate, possono anche:

* Crea sub-community all&#39;interno del sito della community (vedi [gruppi della community](creating-groups.md)).

* [Contenuto generato ](moderation.md) dall&#39;utente moderatore (UGC).

* Essere [enablement resource](resources.md) contatti.

* Sii [privilegiato](#privileged-members-group) per creare post per blog, calendari, QnA e forum.

Gli utenti registrati nell&#39;ambiente di pubblicazione sono generalmente denominati *membri della community (membri)* per distinguerli dagli *utenti* nell&#39;ambiente di authoring.

Le autorizzazioni vengono concesse assegnando i membri a uno dei [gruppi di membri (utenti)](#publish-group-roles) creati dinamicamente quando il sito della community è [creato](sites-console.md) o [modificato](sites-console.md#modifying-site-properties) dall&#39;ambiente di authoring. Quando si lavora dall&#39;ambiente di authoring, i membri sono visibili dall&#39;ambiente di pubblicazione mediante il [servizio tunnel](#tunnel-service).

Per impostazione predefinita, i membri e i gruppi di membri creati nell’ambiente di pubblicazione non devono essere visualizzati nell’ambiente di authoring. Gli utenti e i gruppi di utenti creati nell’ambiente di authoring hanno lo stesso scopo di rimanere nell’ambiente di authoring.

Quando gli utenti autori e i membri al momento della pubblicazione provengono dallo stesso elenco di utenti, ad esempio sincronizzati dalla stessa directory LDAP, non vengono considerati lo stesso utente con le stesse autorizzazioni e appartenenza al gruppo sia nell’ambiente di creazione che nell’ambiente di pubblicazione. I ruoli dei membri e degli utenti devono essere stabiliti separatamente al momento della pubblicazione e dell’autore, a seconda dei casi.

Per una [farm di pubblicazione](topologies.md), la registrazione e le modifiche apportate a un&#39;istanza di pubblicazione devono essere sincronizzate con altre istanze di pubblicazione per consentire loro di accedere agli stessi dati utente. Per informazioni dettagliate, vedere [Sincronizzazione utente](sync.md), che include una sezione che descrive [Cosa accade quando...](sync.md#what-happens-when).

### Limiti per contributi {#contribution-limits}

Al fine di proteggere contro lo spam, è possibile limitare la frequenza di pubblicazione dei contenuti da parte dei membri. Inoltre, è possibile limitare automaticamente i contributi dei nuovi iscritti.

Per informazioni dettagliate, vedere [Limiti contributi membri](limits.md).

### Gruppi di utenti creati dinamicamente {#dynamically-created-user-groups}

Quando viene creato un nuovo sito community, i nuovi gruppi utenti vengono creati dinamicamente con ID univoci (uid) e autorizzazioni appropriate per le varie funzioni amministrative necessarie per gestire il sito community nell&#39;ambiente di creazione (vedere [Ruoli gruppo autore](#author-group-roles)) o nell&#39;ambiente di pubblicazione (vedere [Ruoli gruppo pubblicazione](#publish-group-roles)).

I nomi dei gruppi vengono generati dal nome assegnato al sito durante la creazione del sito [community](sites-console.md#step13asitetemplate). Gli ID univoci evitano conflitti di denominazione per siti community e gruppi community con lo stesso nome sullo stesso server.

Ad esempio, se il nome del sito era &quot;*interazione*&quot; per un sito denominato &quot;We.Retail Engage&quot;, uno dei gruppi di utenti creati sarebbe:

* Membri della community *Engage*

## Ambiente di authoring {#author-environment}

### Servizio Tunnel {#tunnel-service}

Quando si utilizza l&#39;ambiente di authoring per [creare siti](sites-console.md), [modificare le proprietà del sito](sites-console.md#modifying-site-properties) e [gestire membri e gruppi di membri della community](members.md), è necessario accedere a utenti e gruppi di utenti registrati nell&#39;ambiente di pubblicazione.

Il servizio tunnel fornisce questo accesso tramite l&#39;agente di replica in fase di creazione.

* Per informazioni dettagliate, consultate [istruzioni di configurazione](deploy-communities.md#tunnel-service-on-author) nella pagina di distribuzione.

Le [console Membri e Gruppi community](members.md) sono riservate esclusivamente alla gestione di utenti (membri) e gruppi di utenti (gruppi membri) registrati solo nell&#39;ambiente di pubblicazione.

Per gestire utenti e gruppi di utenti registrati nell&#39;ambiente di authoring, utilizzare la [console di sicurezza](../../help/sites-administering/security.md)

### Ruoli gruppo di autori {#author-group-roles}

| Se membro del gruppo... | Ruolo principale |
|---|---|
| amministratori | Il gruppo Administrators è composto da amministratori di sistema che dispongono di tutte le capacità di un amministratore community e di gestire il gruppo Community Administrators. |
| Amministratori community | Il gruppo Amministratori community diventa automaticamente membro di tutti i siti community e di tutti i gruppi di community creati sul sito. Un membro iniziale del gruppo Amministratori community è il gruppo Amministratori. Nell’ambiente di authoring, gli amministratori della community possono creare siti per la community, gestire i siti, gestire i membri (possono vietare i membri della community) e moderare i contenuti. |
| Community &lt;*nome del sito*> Sitecontentmanager | Community Site Content Manager è in grado di eseguire operazioni AEM di authoring, creazione di contenuti e modifica delle pagine per un sito community. |
| Manager abilitazione community | Il gruppo Manager abilitazione comunità è costituito da utenti disponibili per l&#39;assegnazione per gestire il gruppo Manager abilitazione di un sito community. |
| Community &lt;*nome del sito* > Siteenablementmanager | Il gruppo Manager abilitazione sito community è composto da utenti assegnati per la gestione dell&#39;abilitazione di un sito community [resources](resources.md). |
| Nessuno | Un visitatore anonimo del sito non può accedere all’ambiente di authoring. |

### Amministratori di sistema {#system-administrators}

I membri del gruppo di amministratori sono amministratori di sistema in grado di eseguire la configurazione iniziale di un’installazione AEM per gli ambienti di creazione e pubblicazione.

A scopo dimostrativo e di sviluppo, il gruppo di amministratori ha un membro il cui ID utente è *admin* e la password è *admin*.

Per gli ambienti di produzione, il gruppo di amministratori predefiniti deve essere modificato.

Assicurarsi di seguire la [lista di controllo di sicurezza](../../help/sites-administering/security-checklist.md).

## Ambiente di pubblicazione {#publish-environment}

### Diventare membro {#becoming-a-member}

Nell&#39;ambiente di pubblicazione, a seconda delle [impostazioni](sites-console.md#user-management) del sito community, un visitatore del sito può diventare membro della community:

* Quando il sito della comunità è privato (chiuso):
   * Per invito
   * Per azioni di un amministratore

* Quando il sito della comunità è pubblico (aperto):
   * Per autoregistrazione
   * Per accesso tramite social network con Facebook e Twitter

>[!NOTE]
>
>Se un visitatore del sito si registra come membro di un sito community aperto, diventa automaticamente membro di altri siti community aperti nello stesso ambiente di pubblicazione.

### Ruoli gruppo pubblicazione {#publish-group-roles}

| Se membro del gruppo... | Ruolo principale |
|---|---|
| Membri della community &lt;** | Un membro della community è un utente registrato. Possono accedere, modificare il loro profilo, partecipare a un gruppo di community aperto, pubblicare contenuti per la community, inviare messaggi ad altri membri e seguire le attività del sito. |
| Community &lt;*nome del sito*> Moderatori | Un moderatore del sito community è un membro fidato della comunità che è in grado di moderare l&#39;UGC sia in massa, utilizzando la console di moderazione, sia contestualmente, sulla pagina in cui viene pubblicato il contenuto. |
| Community &lt;*nome del sito*> &lt;*nome del gruppo* | Un membro del gruppo è un membro della comunità che ha aderito a un gruppo comunitario aperto o che è stato invitato in un gruppo comunitario chiuso. Hanno le capacità di un membro per quel gruppo di community all&#39;interno del sito. |
| Amministratori di gruppi &lt;** | L&#39;amministratore di un gruppo di siti community è un membro affidabile della community, assegnato per creare e gestire sottocomunità (gruppi) all&#39;interno di un sito community. Inclusa è la capacità di fornire moderazione contestuale. |
| *Gruppo di sicurezza dei membri privilegiati* | Un gruppo di utenti creato e mantenuto manualmente allo scopo di limitare la creazione di contenuti. Vedere [Gruppo di membri privilegiati](#privileged-members-group). |
| Nessuno | Un visitatore anonimo del sito, che scopre il sito, può visualizzare ed effettuare ricerche nei siti della community che consentono l&#39;accesso anonimo. Per partecipare e pubblicare contenuti, l&#39;utente deve registrarsi autonomamente (se consentito) e diventare membro della community. |

### Assegnazione di membri ai ruoli del gruppo di pubblicazione {#assigning-members-to-publish-group-roles}

Durante la [creazione di un sito community](sites-console.md) nell&#39;ambiente di authoring, o durante la [modifica delle proprietà del sito, ai membri](sites-console.md#modifying-site-properties) possono essere assegnati vari ruoli eseguiti nell&#39;ambiente di pubblicazione, ad esempio moderatori, amministratori di gruppo, contatti di risorse o membri privilegiati.

[Abilitando i ](sync.md#accessingpublishusersfromauthor) servizi del tunnel si ottengono risultati nelle scelte di assegnazione presentate dai membri al momento della pubblicazione invece che dagli utenti all&#39;autore.

I membri selezionati verranno automaticamente assegnati al [gruppo appropriato](#publish-group-roles) e le loro appartenenze saranno incluse quando il sito community viene (ri)pubblicato.

### Gruppo membri privilegiati {#privileged-members-group}

Lo scopo di un gruppo di sicurezza di membri privilegiati è limitare la creazione di contenuto per determinate funzioni della community a un sottoinsieme privilegiato di membri di un sito community.

Il gruppo di membri privilegiati è un gruppo di membri creato e gestito utilizzando la [console Gruppi community](members.md).

Dopo la creazione di un gruppo di membri privilegiati, e con il servizio [tunnel abilitato](sync.md#accessingpublishusersfromauthor), la struttura di un sito community esistente può essere [modificata](sites-console.md#modify-structure) per modificare la configurazione delle funzioni della community in &quot;Consenti membri privilegiati&quot; e aggiungere il gruppo creato.

Le funzioni comunitarie che consentono di specificare uno o più gruppi di membri privilegiati sono:

* [Funzione](functions.md#blog-function)  blog - Per limitare la creazione di nuovi articoli.
* [Funzione](functions.md#calendar-function)  Calendario - Per limitare la creazione di nuovi eventi.
* [Funzione](functions.md#forum-function)  forum - Per limitare la creazione di nuovi argomenti.
* [Funzione](functions.md#qna-function)  QnA: per limitare la creazione di nuove domande.

Quando una funzione community non è protetta (non è assegnato alcun gruppo di membri privilegiati), tutti i membri del sito community possono creare contenuti di funzioni (articoli, eventi, argomenti, domande).

>[!NOTE]
>
>L&#39;aggiunta di un utente a un gruppo di membri privilegiati per un sito community concederà loro privilegi di creazione solo se sono anche membri dello stesso sito community.

## Creazione di membri della community {#creating-community-members}

### Percorso archivio {#repository-location}

Affinché alcune funzioni funzionino correttamente, è necessario creare utenti e gruppi di utenti con i privilegi appropriati.

Quando i membri vengono creati in `/home/users/community`, ereditano gli ACL appropriati che assegnano privilegi di lettura ai profili dei membri.

Allo stesso modo, i gruppi di utenti della community personalizzata (come i gruppi di membri privilegiati) devono essere creati in `/home/groups/community`.

Utilizzando le console [Membri e gruppi della community](members.md) sarà possibile creare utenti e gruppi in questi percorsi.

Per specificare un percorso personalizzato è necessario utilizzare l&#39;interfaccia classica di protezione, accessibile in [https://&lt;server>:&lt;porta>/useradmin](http://localhost:4503/useradmin).

Per assegnare privilegi di lettura per i percorsi membri personalizzati, in tutte le istanze pubblicate impostare ACL simili a `/home/users/community`:

```xml
<allow
  jcr:primaryType="rep:GrantACE"
  rep:principalName="everyone"
  rep:privileges="{Name}[jcr:read]" >
  <rep:restrictions
    jcr:primaryType="rep:Restrictions"
    rep:glob="*/profile*" />
</allow>
```

Per assegnare i privilegi appropriati per i percorsi dei gruppi di membri personalizzati, ad esempio /home/groups/mycompany, su tutte le istanze pubblicate impostare ACL simili a `/home/groups/community`:

```xml
<allow
  jcr:primaryType="rep:GrantACE"
  rep:principalName="community-administrators"
  rep:privileges="{Name}[jcr:read]"  />
```

### Console {#consoles}

Solo nell’ambiente di authoring sono disponibili quattro console separate:

| console | Strumenti, protezione, utenti | Strumenti, Sicurezza, Gruppi | Community, Membri | Community, Gruppi |
|----------|-----------------------|------------------------|------------------------------------------------------------|------------------------------------------------------------|
| gestisce | utenti dell’autore | gruppi di utenti sull’autore | membri pubblicati | gruppi membri in fase di pubblicazione |
| richiede | autorizzazione amministratore | autorizzazione amministratore | autorizzazione amministratore, servizio tunnel, sincronizzazione utente per la pubblicazione farm | autorizzazione amministratore, servizio tunnel, sincronizzazione utente per la pubblicazione farm |

### Ruolo di Gestione abilitazione community {#community-enablement-manager-role}

La possibilità per un visitatore del sito di registrarsi autonomamente non è in genere consentita per una [community di abilitazione](overview.md#enablement-community) in quanto i costi sono associati a ciascun membro. Gli utenti in formazione e le risorse di abilitazione vengono gestiti da un utente a cui è stato assegnato il [ruolo](#author-group-roles) di `enablement manager` [durante la creazione del sito](sites-console.md#enablement) sull&#39;autore (aggiunto come membro del gruppo `Community <site-name> Siteenablementmanagers`). La `enablement manager` è inoltre responsabile dell&#39; [assegnazione di risorse di apprendimento](resources.md) ai membri della community in fase di creazione.

Solo gli utenti membri del gruppo globale `Community Enablement Managers` possono essere selezionati come `enablement manager` per un sito community specifico.

Per creare un utente al quale può essere assegnato il ruolo di `Community Site Enablement Manager`, utilizzate la console di protezione dell&#39;interfaccia classica per specificare il percorso:

In un’istanza di creazione:

1. Effettuato l’accesso con privilegi di amministratore, passa alla classica console di sicurezza dell’interfaccia utente.

   Ad esempio, [http://localhost:4502/useradmin](http://localhost:4502/useradmin)

2. Dal menu Modifica, selezionare **[!UICONTROL Crea utente]**.
3. Compilate la finestra di dialogo `Create User`.
   * Il percorso deve essere `/home/users/community`.
4. Seleziona **[!UICONTROL Crea]**.

   ![create-community-user](assets/create-community-user.png)

* Nel riquadro a sinistra, cercare l’utente appena creato e selezionare per visualizzarlo nel riquadro a destra.

   ![utente della community](assets/view-community-user.png)

Nel riquadro a sinistra:

1. Deselezionare la casella di ricerca e selezionare **[!UICONTROL Nascondi utenti]**.
2. Individuare e trascinare `community-enablementmanagers` nella scheda **[!UICONTROL Groups]** del nuovo utente visualizzata nel riquadro a destra.

   ![assign-group](assets/assign-group.png)

### Ruolo Amministratori community {#community-administrators-role}

Come indicato nel grafico [Ruoli gruppo autori](#author-group-roles), i membri del gruppo Amministratori community possono creare siti community, gestire siti, gestire membri (possono vietare membri della community) e moderare contenuti.

Seguire gli stessi passaggi per creare e assegnare un utente al ruolo di [enablement manager](#communitysiteenablementmanagerrole), ma aggiungere un gruppo c `ommunity-administrators` nella scheda Gruppi dell&#39;utente.

### Integrazione LDAP {#ldap-integration}

AEM supporta l’utilizzo di LDAP per l’autenticazione degli utenti e per la creazione di account utente. Questo è descritto in [Configurazione di LDAP con AEM 6](../../help/sites-administering/ldap-config.md).

Di seguito sono riportati alcuni dettagli di configurazione specifici per i membri della community e i gruppi di membri.

1. Configurare LDAP per ogni istanza di pubblicazione AEM.
2. [Provider di identità LDAP](../../help/sites-administering/ldap-config.md#configuring-the-ldap-identity-provider)

   * Nessuna istruzione speciale

3. [Gestore di sincronizzazione](../../help/sites-administering/ldap-config.md#configuring-the-synchronization-handler)

   * Impostate le seguenti proprietà:

      * **[!UICONTROL Iscrizione]** automatica utente:  `community-<site name>-<uid>-members`
      * **[!UICONTROL Prefisso percorso utente]**:  `/community`
      * **[!UICONTROL Prefisso]** percorso gruppo:  `/community`

4. [Modulo di login esterno](../../help/sites-administering/ldap-config.md#the-external-login-module)

   * nessuna istruzione speciale

Ciò comporta l&#39;assegnazione automatica degli utenti al gruppo di membri del sito della community e la posizione del repository `/home/users/community` e `/home/groups/community`, in modo che questi possano ereditare le autorizzazioni appropriate per visualizzare il profilo dell&#39;altro.

* Il valore `User auto membership` deve essere la proprietà `rep:authorizableId`, non la proprietà `givenName` (nome visualizzato) del profilo.

## Sincronizzazione degli utenti tra AEM istanze {#synchronizing-users-among-aem-instances}

Quando si utilizza una [farm di pubblicazione](topologies.md), assicurarsi che gli utenti abbiano lo stesso percorso in ogni istanza di pubblicazione importando gli utenti prima in un&#39;istanza e [abilitando la sincronizzazione utente](sync.md) su Sling, distribuire gli utenti alle altre istanze di pubblicazione.

Se importate dei gruppi di utenti, per essere certi che i gruppi di utenti abbiano lo stesso percorso in ciascuna istanza di pubblicazione, importate in un&#39;istanza, quindi [create un pacchetto](../../help/sites-administering/package-manager.md#creating-a-new-package) per l&#39;esportazione e installate il pacchetto su tutte le altre istanze di pubblicazione.

Anche se la sincronizzazione di gruppi di utenti tramite la sincronizzazione degli utenti verrà inclusa in una versione futura, al momento solo la *appartenenza* di un gruppo di utenti verrà sincronizzata quando viene eseguita la sincronizzazione degli utenti.

## Informazioni sui gruppi community {#about-community-groups}

Quando si discute di gruppi, ci sono due argomenti distinti:

* **[Gruppi community](overview.md#communitygroups)**

   I gruppi comunitari sono le sub-comunità che possono essere create nell&#39;ambiente di pubblicazione per un sito della comunità che supporta la creazione di gruppi della comunità. La creazione di un gruppo community genera un numero maggiore di pagine aggiunte al sito Web e gestite in modo simile al sito della community principale. Per ulteriori informazioni, vedere [Community Group Essentials](essentials-groups.md) per gli sviluppatori e [Community Group](creating-groups.md) per gli autori.

* **[Gruppi di membri](../../help/sites-administering/security.md)**

   I gruppi di membri sono i gruppi a cui i membri possono appartenere e che sono gestiti tramite la console Gruppi. Gran parte della discussione su questa pagina è stata dedicata ai gruppi membri. I gruppi di membri creati automaticamente per un sito comunitario, con il prefisso *`Community`*, possono essere definiti come gruppo comunitario, pertanto il contesto della discussione deve essere considerato.
