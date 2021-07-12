---
title: Gestione di utenti e gruppi di utenti
seo-title: Gestione di utenti e gruppi di utenti
description: Gli utenti di AEM Communities possono registrarsi autonomamente e modificare i propri profili
seo-description: Gli utenti di AEM Communities possono registrarsi autonomamente e modificare i propri profili
uuid: aeba424e-ea7e-4da5-b94f-ea8af4caa7d2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 774c2553-b629-456b-afa7-5713490f4a0a
role: Admin
exl-id: 4237085a-d70d-41de-975d-153f58336daa
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '2183'
ht-degree: 0%

---

# Gestione di utenti e gruppi di utenti {#managing-users-and-user-groups}

## Panoramica {#overview}

In AEM Communities, nell’ambiente di pubblicazione, gli utenti possono registrarsi autonomamente e modificare i propri profili. Dati i permessi appropriati, possono inoltre:

* Crea sub-community all&#39;interno del sito della community (consulta [gruppi di community](creating-groups.md)).

* [](moderation.md) Contenuto generato dall’utente moderatore (UGC).

* Essere [enablement resource](resources.md) contatti.

* Sii [con privilegi](#privileged-members-group) per creare voci per blog, calendari, QnA e forum.

Gli utenti registrati nell’ambiente di pubblicazione sono generalmente denominati *membri della community (membri)* per distinguerli dagli utenti *utenti* nell’ambiente di authoring.

Le autorizzazioni vengono concesse assegnando i membri a uno dei [gruppi di membri (utenti)](#publish-group-roles) creati dinamicamente quando il sito della community è [creato](sites-console.md) o [modificato](sites-console.md#modifying-site-properties) dall&#39;ambiente di authoring. Quando lavori dall&#39;ambiente di authoring, i membri sono visibili dall&#39;ambiente di pubblicazione tramite il [servizio tunnel](#tunnel-service).

Per progettazione, i membri e i gruppi di membri creati nell’ambiente di pubblicazione non devono essere visualizzati nell’ambiente di authoring. Analogamente, gli utenti e i gruppi di utenti creati nell’ambiente di authoring hanno lo scopo di rimanere nell’ambiente di authoring.

Quando gli utenti dell&#39;autore e i membri al momento della pubblicazione provengono dallo stesso elenco di utenti, ad esempio sincronizzati dalla stessa directory LDAP, non vengono considerati lo stesso utente con le stesse autorizzazioni e appartenenza al gruppo sia negli ambienti di authoring che di pubblicazione. I ruoli dei membri e degli utenti devono essere stabiliti separatamente al momento della pubblicazione e dell&#39;autore, a seconda dei casi.

Per una [farm di pubblicazione](topologies.md), la registrazione e le modifiche apportate a un&#39;istanza di pubblicazione devono essere sincronizzate con altre istanze di pubblicazione per consentire loro di accedere agli stessi dati utente. Per informazioni dettagliate, vedere [Sincronizzazione utente](sync.md), che include una sezione che descrive [cosa accade quando...](sync.md#what-happens-when).

### Limiti per contributi {#contribution-limits}

Al fine di proteggere dallo spam, è possibile limitare la frequenza di pubblicazione dei contenuti da parte dei membri. Inoltre, è possibile limitare automaticamente i contributi dei nuovi iscritti.

Per informazioni dettagliate, consulta [Limiti dei contributi dei membri](limits.md).

### Gruppi di utenti creati dinamicamente {#dynamically-created-user-groups}

Quando viene creato un nuovo sito community, i nuovi gruppi di utenti vengono creati in modo dinamico con ID univoci (uid) e autorizzazioni appropriate per varie funzioni amministrative necessarie per gestire il sito community nell&#39;ambiente di authoring (consulta [Ruoli gruppo autori](#author-group-roles)) o nell&#39;ambiente di pubblicazione (consulta [Ruoli gruppo di pubblicazione](#publish-group-roles)).

I nomi dei gruppi vengono generati dal nome assegnato al sito durante la [creazione del sito community](sites-console.md#step13asitetemplate). Gli ID univoci evitano conflitti di denominazione per siti community e gruppi community con nomi simili sullo stesso server.

Ad esempio, se il nome del sito era &quot;*coinvolgi*&quot; per un sito intitolato &quot;We.Retail Engage&quot;, uno dei gruppi di utenti creati sarebbe:

* Membri della community *Coinvolgi*

## Ambiente di authoring {#author-environment}

### Servizio tunnel {#tunnel-service}

Quando si utilizza l&#39;ambiente di authoring per [creare siti](sites-console.md), [modificare le proprietà del sito](sites-console.md#modifying-site-properties) e [gestire membri e gruppi di membri della community](members.md), è necessario accedere agli utenti e ai gruppi di utenti registrati nell&#39;ambiente di pubblicazione.

Il servizio tunnel fornisce questo accesso utilizzando l&#39;agente di replica sull&#39;autore.

* Per informazioni dettagliate, consulta [istruzioni di configurazione](deploy-communities.md#tunnel-service-on-author) nella pagina di distribuzione.

Le [console Membri e gruppi della community](members.md) sono destinate esclusivamente alla gestione di utenti (membri) e gruppi di utenti (gruppi membri) registrati solo nell’ambiente di pubblicazione.

Per gestire utenti e gruppi di utenti registrati nell&#39;ambiente di authoring, utilizza la [console di sicurezza](../../help/sites-administering/security.md)

### Ruoli gruppo autore {#author-group-roles}

| Se membro del gruppo.. | Ruolo principale |
|---|---|
| amministratori | Il gruppo di amministratori è costituito da amministratori di sistema che dispongono di tutte le capacità di un amministratore della community e dalla possibilità di gestire il gruppo di amministratori della community. |
| Amministratori community | Il gruppo Amministratori community diventa automaticamente membro di tutti i siti della community e di tutti i gruppi della community creati sul sito. Un membro iniziale del gruppo Amministratori community è il gruppo Amministratori. Nell’ambiente di authoring, gli amministratori della community possono creare siti di community, gestirli, gestirli e moderare i contenuti. |
| Community &lt;*nome del sito*> Sitecontentmanager | Community Site Content Manager è in grado di eseguire operazioni di authoring AEM tradizionali, creazione di contenuti e modifica di pagine per un sito community. |
| Responsabili dell&#39;abilitazione della community | Il gruppo Community Enablement Manager è costituito da utenti disponibili per l&#39;assegnazione per gestire il gruppo Enablement Manager di un sito community. |
| Community &lt;*nome del sito* > Siteenablementmanager | Il gruppo Community Site Enablement Manager è costituito da utenti assegnati per gestire l&#39;abilitazione di un sito community [risorse](resources.md). |
| Nessuna | Un visitatore anonimo del sito non può accedere all’ambiente di authoring. |

### Amministratori di sistema {#system-administrators}

I membri del gruppo di amministratori sono amministratori di sistema in grado di eseguire la configurazione iniziale di un’installazione di AEM per gli ambienti di authoring e di pubblicazione.

A scopo dimostrativo e di sviluppo, il gruppo di amministratori ha un membro il cui id utente è *admin* e la password è *admin*.

Per gli ambienti di produzione, è necessario modificare il gruppo di amministratori predefiniti.

Segui la [Lista di controllo sicurezza](../../help/sites-administering/security-checklist.md).

## Ambiente di pubblicazione {#publish-environment}

### Diventare membro {#becoming-a-member}

Nell&#39;ambiente di pubblicazione, a seconda delle [impostazioni](sites-console.md#user-management) del sito community, un visitatore del sito può diventare membro della community:

* Quando il sito della community è privato (chiuso):
   * Su invito
   * Da parte di un amministratore

* Quando il sito della community è pubblico (aperto):
   * Per autoregistrazione
   * Per accesso social con Facebook e Twitter

>[!NOTE]
>
>Se un visitatore del sito si registra come membro di un sito community aperto, diventa automaticamente membro di altri siti community aperti nello stesso ambiente di pubblicazione.

### Ruoli gruppo di pubblicazione {#publish-group-roles}

| Se membro del gruppo.. | Ruolo principale |
|---|---|
| Community &lt;*nome del sito*> Membri | Un membro del sito community è un utente registrato. Possono accedere, modificare il loro profilo, partecipare a un gruppo community aperto, pubblicare contenuti nella community, inviare messaggi ad altri membri e seguire le attività del sito. |
| Community &lt;*nome del sito*> Moderatori | Un moderatore di sito community è un membro fidato della community che è in grado di moderare UGC in massa, utilizzando la console di moderazione o nel contesto, nella pagina in cui viene pubblicato il contenuto. |
| Community &lt;*nome sito*> &lt;*nome gruppo*> Membri | Un membro del gruppo comunitario è un membro della comunità che ha aderito a un gruppo comunitario aperto o è stato invitato a un gruppo comunitario chiuso. Hanno le capacità di un membro per quel gruppo di comunità all&#39;interno del sito. |
| Community &lt;*nome sito*> Amministratori di gruppi | Un amministratore di gruppo di siti community è un membro della community fidato che viene assegnato per creare e gestire sottocommunity (gruppi) all’interno di un sito community. Included è la capacità di fornire moderazione nel contesto. |
| *Gruppo di sicurezza dei membri con privilegi* | Un gruppo di utenti creato e gestito manualmente allo scopo di limitare la creazione di contenuti. Vedere [Gruppo di membri con privilegi](#privileged-members-group). |
| Nessuna | Un visitatore anonimo del sito, che scopre il sito, può visualizzare e cercare siti della community che consentono l’accesso anonimo. Per partecipare e pubblicare contenuti, l’utente deve registrarsi autonomamente (se consentito) e diventare membro della community. |

### Assegnazione dei membri ai ruoli del gruppo di pubblicazione {#assigning-members-to-publish-group-roles}

Quando [si crea un sito community](sites-console.md) nell&#39;ambiente di authoring o quando [si modificano le proprietà del sito, ai membri](sites-console.md#modifying-site-properties) possono essere assegnati vari ruoli eseguiti nell&#39;ambiente di pubblicazione, ad esempio moderatori, amministratori di gruppo, contatti di risorse o membri con privilegi.

[Abilitando i ](sync.md#accessingpublishusersfromauthor) servizi del tunnel, si ottengono risultati nelle scelte di assegnazione presentate dai membri in fase di pubblicazione invece che dagli utenti in fase di creazione.

I membri selezionati verranno assegnati automaticamente al [gruppo appropriato](#publish-group-roles) e le loro appartenenze saranno incluse quando il sito della community viene (ri)pubblicato.

### Gruppo membri privilegiati {#privileged-members-group}

Lo scopo di un gruppo di sicurezza per i membri privilegiati è quello di limitare la creazione di contenuti per alcune funzioni della community a un sottoinsieme privilegiato di membri di un sito community.

Il gruppo di membri privilegiati è un gruppo di membri creato e gestito utilizzando la [console Gruppi community](members.md).

Dopo la creazione di un gruppo di membri privilegiati e con il servizio [tunnel abilitato](sync.md#accessingpublishusersfromauthor), la struttura di un sito community esistente può essere [modificata](sites-console.md#modify-structure) per modificare la configurazione delle funzioni della community in &quot;Consenti membri con privilegi&quot; e aggiungere il gruppo creato.

Le funzioni comunitarie che consentono la specificazione di uno o più gruppi di membri privilegiati sono:

* [Funzione](functions.md#blog-function)  blog - Per limitare la creazione di nuovi articoli.
* [Funzione](functions.md#calendar-function)  calendario: per limitare la creazione di nuovi eventi.
* [Funzione forum](functions.md#forum-function)  - Per limitare la creazione di nuovi argomenti.
* [Funzione](functions.md#qna-function)  QnA: per limitare la creazione di nuove domande.

Quando una funzione community non è protetta (nessun gruppo di membri privilegiati assegnato), a tutti i membri del sito community è consentito creare contenuti di funzionalità (articoli, eventi, argomenti, domande).

>[!NOTE]
>
>L&#39;aggiunta di un utente a un gruppo di membri privilegiati per un sito community consente loro di creare privilegi solo se sono anche membri dello stesso sito community.

## Creazione di membri della community {#creating-community-members}

### Posizione archivio {#repository-location}

Affinché alcune funzioni funzionino correttamente, è necessario creare utenti e gruppi di utenti con i privilegi appropriati.

Quando i membri vengono creati in `/home/users/community`, ereditano le ACL corrette che danno privilegi di lettura ai profili dei membri.

Allo stesso modo, i gruppi di utenti personalizzati della community (come i gruppi di membri privilegiati) devono essere creati in `/home/groups/community`.

Utilizzando le [console Membri e gruppi della community](members.md) verranno creati utenti e gruppi in questi percorsi.

Per specificare un percorso personalizzato è necessario utilizzare l’interfaccia classica di sicurezza, accessibile da [https://&lt;server>:&lt;port>/useradmin](http://localhost:4503/useradmin).

Per assegnare privilegi di lettura per i percorsi membri personalizzati, su tutte le istanze di pubblicazione impostare ACL simili a `/home/users/community`:

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

Per assegnare i privilegi appropriati per i percorsi dei gruppi di membri personalizzati, come /home/groups/mycompany, su tutte le istanze di pubblicazione impostare ACL simili a `/home/groups/community`:

```xml
<allow
  jcr:primaryType="rep:GrantACE"
  rep:principalName="community-administrators"
  rep:privileges="{Name}[jcr:read]"  />
```

### Console {#consoles}

Sono disponibili quattro console separate solo nell’ambiente di authoring:

| console | Strumenti, Sicurezza, Utenti | Strumenti, Sicurezza, Gruppi | Comunità, membri | Community, gruppi |
|----------|-----------------------|------------------------|------------------------------------------------------------|------------------------------------------------------------|
| gestisce | utenti su autore | gruppi di utenti sull’autore | membri in pubblicazione | gruppi di membri in pubblicazione |
| richiede | autorizzazione amministratore | autorizzazione amministratore | autorizzazione amministratore, servizio tunnel, sincronizzazione utente per farm di pubblicazione | autorizzazione amministratore, servizio tunnel, sincronizzazione utente per farm di pubblicazione |

### Ruolo di Community Enablement Manager {#community-enablement-manager-role}

La possibilità per un visitatore del sito di registrarsi autonomamente non è in genere consentita per una [community di abilitazione](overview.md#enablement-community) in quanto esistono costi associati a ciascun membro. Gli studenti e le risorse di abilitazione sono gestiti da un utente a cui è stato assegnato il [ruolo](#author-group-roles) di `enablement manager` [durante la creazione del sito](sites-console.md#enablement) sull&#39;autore (aggiunto come membro del gruppo `Community <site-name> Siteenablementmanagers`). `enablement manager` è anche responsabile dell&#39; [assegnazione di risorse di apprendimento](resources.md) ai membri della community sull&#39;autore.

Solo gli utenti membri del gruppo globale `Community Enablement Managers` possono essere selezionati come `enablement manager` per un sito community specifico.

Per creare un utente a cui può essere assegnato il ruolo di `Community Site Enablement Manager`, utilizza la console di sicurezza dell’interfaccia classica per specificare il percorso:

Su un&#39;istanza dell&#39;autore:

1. Accesso con privilegi di amministratore, passa alla console di sicurezza dell’interfaccia classica.

   Ad esempio, [http://localhost:4502/useradmin](http://localhost:4502/useradmin)

2. Dal menu Modifica, selezionare **[!UICONTROL Crea utente]**.
3. Compila la finestra di dialogo `Create User` .
   * Il percorso deve essere `/home/users/community`.
4. Seleziona **[!UICONTROL Crea]**.

   ![create-community-user](assets/create-community-user.png)

* Nel riquadro a sinistra, cerca l’utente appena creato e seleziona per visualizzarlo nel riquadro a destra.

   ![utente della community](assets/view-community-user.png)

Nel riquadro a sinistra:

1. Deseleziona la casella di ricerca e seleziona **[!UICONTROL Nascondi utenti]**.
2. Individua e trascina `community-enablementmanagers` nella scheda **[!UICONTROL Gruppi]** del nuovo utente visualizzato nel riquadro di destra.

   ![gruppo di assegnazione](assets/assign-group.png)

### Ruolo degli amministratori della community {#community-administrators-role}

Come indicato nel grafico [Ruoli gruppo autori](#author-group-roles), i membri del gruppo Amministratori community possono creare siti community, gestire siti, gestire membri (possono vietare membri della community) e moderare contenuti.

Segui gli stessi passaggi descritti per creare e assegnare un utente al ruolo di [enablement manager](#communitysiteenablementmanagerrole), ma aggiungi il gruppo c `ommunity-administrators` nella scheda Gruppi dell&#39;utente.

### Integrazione LDAP {#ldap-integration}

AEM supporta l&#39;utilizzo di LDAP per l&#39;autenticazione degli utenti e la creazione di account utente. Questo è descritto in [Configurazione di LDAP con AEM 6](../../help/sites-administering/ldap-config.md).

Di seguito sono riportati alcuni dettagli di configurazione specifici per i membri della community e i gruppi di membri.

1. Configura LDAP per ogni istanza di pubblicazione AEM.
2. [Provider di identità LDAP](../../help/sites-administering/ldap-config.md#configuring-the-ldap-identity-provider)

   * Nessuna istruzione speciale

3. [Gestore di sincronizzazione](../../help/sites-administering/ldap-config.md#configuring-the-synchronization-handler)

   * Imposta le seguenti proprietà:

      * **[!UICONTROL Iscrizione]** automatica utente:  `community-<site name>-<uid>-members`
      * **[!UICONTROL Prefisso]** percorso utente:  `/community`
      * **[!UICONTROL Prefisso]** percorso gruppo:  `/community`

4. [Modulo di accesso esterno](../../help/sites-administering/ldap-config.md#the-external-login-module)

   * nessuna istruzione speciale

In questo modo gli utenti vengono automaticamente assegnati al gruppo di membri del sito community e la posizione del repository è `/home/users/community` e `/home/groups/community`, in modo che ereditino le autorizzazioni appropriate per visualizzare il profilo degli altri utenti.

* Il valore `User auto membership` deve essere la proprietà `rep:authorizableId` e non il `givenName` (nome visualizzato) dal profilo.

## Sincronizzazione Degli Utenti Tra Le Istanze AEM {#synchronizing-users-among-aem-instances}

Quando utilizzi una [farm di pubblicazione](topologies.md), assicurati che gli utenti abbiano lo stesso percorso in ogni istanza di pubblicazione importando gli utenti prima in un&#39;istanza e [abilitando la sincronizzazione utente](sync.md) a Sling distribuendo gli utenti alle altre istanze di pubblicazione.

Se si importano gruppi di utenti, per assicurarsi che i gruppi di utenti abbiano lo stesso percorso in ogni istanza di pubblicazione, importa in un&#39;istanza, quindi [crea un pacchetto](../../help/sites-administering/package-manager.md#creating-a-new-package) per l&#39;esportazione e installa quel pacchetto su tutte le altre istanze di pubblicazione.

Mentre la sincronizzazione dei gruppi di utenti tramite la sincronizzazione utente verrà inclusa in una versione futura, attualmente solo la *appartenenza* di un gruppo di utenti verrà sincronizzata quando la sincronizzazione utente viene eseguita.

## Informazioni sui gruppi community {#about-community-groups}

Quando si discute dei gruppi, ci sono due argomenti distinti:

* **[Gruppi comunitari](overview.md#communitygroups)**

   I gruppi comunitari sono le sub-comunità che possono essere create nell&#39;ambiente di pubblicazione per un sito comunitario che supporta la creazione di gruppi di comunità. La creazione di un gruppo di community determina l’aggiunta di più pagine al sito web e viene gestita in modo simile al sito della comunità padre. Per ulteriori informazioni, visita [Community Group Essentials](essentials-groups.md) per gli sviluppatori e [Community Group](creating-groups.md) per gli autori.

* **[Gruppi di membri](../../help/sites-administering/security.md)**

   I gruppi di membri sono i gruppi a cui i membri possono appartenere e sono gestiti tramite la console Gruppi. Gran parte della discussione su questa pagina è stata dedicata ai gruppi membri. I gruppi di membri creati automaticamente per un sito comunitario, con prefisso *`Community`*, possono essere definiti gruppo comunitario, pertanto il contesto della discussione deve essere considerato.
