---
title: Gestione di utenti e gruppi di utenti
description: Gli utenti di AEM Communities possono auto-registrarsi e modificare i propri profili
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 4237085a-d70d-41de-975d-153f58336daa
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1910'
ht-degree: 0%

---

# Gestione di utenti e gruppi di utenti {#managing-users-and-user-groups}

## Panoramica {#overview}

In AEM Communities, nell’ambiente di pubblicazione, gli utenti possono registrarsi autonomamente e modificare i propri profili. Viste le autorizzazioni appropriate, essi possono anche:

* Creare comunità secondarie all&#39;interno del sito community (vedere [gruppi community](creating-groups.md)).

* [Modera](moderation.md) contenuti generati dagli utenti (UGC, User Generated Content).

* Essere [privilegiato](#privileged-members-group) per creare voci per blog, calendari, domande e forum.

Gli utenti registrati nell’ambiente di pubblicazione vengono generalmente denominati *membri della community (membri)* per distinguerli *utenti* nell’ambiente di authoring.

Le autorizzazioni vengono concesse assegnando membri a uno dei [gruppi di membri (utenti)](#publish-group-roles) creato in modo dinamico quando il sito community è [creato](sites-console.md) o [modificato](sites-console.md#modifying-site-properties) dall’ambiente di authoring. Quando si lavora dall’ambiente di authoring, i membri sono visibili dall’ambiente di pubblicazione tramite [servizio tunnel](#tunnel-service).

In base alla progettazione, i membri e i gruppi di membri creati nell’ambiente di pubblicazione non devono essere visualizzati nell’ambiente di authoring. Analogamente, gli utenti e i gruppi di utenti creati nell’ambiente di authoring devono rimanere in tale ambiente.

Quando gli utenti per l’authoring e i membri per la pubblicazione provengono dallo stesso elenco di utenti, ad esempio sincronizzati dalla stessa directory LDAP, non vengono considerati lo stesso utente con le stesse autorizzazioni e con l’iscrizione al gruppo sia nell’ambiente di authoring che in quello di pubblicazione. I ruoli dei membri e degli utenti devono essere stabiliti separatamente in pubblicazione e autore, a seconda dei casi.

Per un [farm di pubblicazione](topologies.md), la registrazione e le modifiche effettuate su un’istanza Publish devono essere sincronizzate con altre istanze Publish per poter accedere agli stessi dati utente. Per maggiori dettagli, consulta [Sincronizzazione utente](sync.md), che include una sezione che descrive [Cosa Succede Quando...](sync.md#what-happens-when).

### Limiti per contributi {#contribution-limits}

Per proteggersi dallo spam, è possibile limitare la frequenza di pubblicazione dei contenuti da parte dei membri. Inoltre, è possibile limitare automaticamente i contributi dei membri appena registrati.

Per ulteriori informazioni, consulta [Limiti contributi membri](limits.md).

### Gruppi di utenti creati in modo dinamico {#dynamically-created-user-groups}

Quando si crea un nuovo sito community, vengono creati dinamicamente nuovi gruppi di utenti con ID univoci (UID) e autorizzazioni appropriati per varie funzioni amministrative necessarie per gestire il sito community nell’ambiente di authoring (vedi [Ruoli del gruppo di authoring](#author-group-roles)) o l&#39;ambiente di pubblicazione (vedere [Pubblica ruoli gruppo](#publish-group-roles)).

I nomi dei gruppi vengono generati dal nome assegnato al sito durante [creazione di siti community](sites-console.md#step13asitetemplate). Gli ID univoci evitano conflitti di denominazione per siti e gruppi community con nomi simili sullo stesso server.

Ad esempio, se il nome del sito è &quot;*coinvolgere*&quot; per un sito denominato &quot;Coinvolgi&quot;, uno dei gruppi di utenti creati sarà:

* Community *Coinvolgi* Membri

## Ambiente di authoring {#author-environment}

### Servizio tunnel {#tunnel-service}

Quando si utilizza l’ambiente di authoring per [creare siti](sites-console.md), [modifica proprietà sito](sites-console.md#modifying-site-properties) e [gestire membri e gruppi di membri della community](members.md), è necessario accedere agli utenti e ai gruppi di utenti registrati nell’ambiente di pubblicazione.

Il servizio tunnel fornisce questo accesso utilizzando l’agente di replica sull’istanza di authoring.

* Per ulteriori informazioni, consulta [istruzioni di configurazione](deploy-communities.md#tunnel-service-on-author) nella pagina distribuzione.

Il [Console per membri e gruppi community](members.md) hanno lo scopo esclusivo di gestire gli utenti (membri) e i gruppi di utenti (gruppi di membri) registrati solo nell’ambiente di pubblicazione.

Per gestire utenti e gruppi di utenti registrati nell’ambiente di authoring, utilizza [Console di sicurezza](../../help/sites-administering/security.md)

### Ruoli del gruppo di authoring {#author-group-roles}

| Se membro del gruppo... | Ruolo principale |
|---|---|
| amministratori | Il gruppo degli amministratori è composto da amministratori di sistema che dispongono di tutte le competenze di un amministratore della comunità e della capacità di gestire il gruppo degli amministratori della comunità. |
| Amministratori community | Il gruppo Amministratori community diventa automaticamente membro di tutti i siti e i gruppi della community creati sul sito. Un membro iniziale del gruppo Community Administrators è il gruppo Administrators. Nell’ambiente di authoring, gli amministratori della community possono creare siti community, gestire siti, gestire membri (possono bandire membri dalla community) e moderare i contenuti. |
| Community &lt;*nome del sito*> Sitecontentmanager | Community Site Content Manager consente di eseguire l&#39;authoring AEM tradizionale, la creazione di contenuti e la modifica di pagine per un sito community. |
| Nessuno | Un visitatore anonimo del sito non può accedere all’ambiente di authoring. |

### Amministratori di sistema {#system-administrators}

I membri del gruppo amministratori sono amministratori di sistema in grado di eseguire la configurazione iniziale di un’installazione AEM sia per l’ambiente di authoring che per quello di pubblicazione.

A scopo dimostrativo e di sviluppo, il gruppo amministratori ha un membro il cui ID utente è *admin* e la password è *admin*.

Per gli ambienti di produzione, è necessario modificare il gruppo di amministratori predefinito.

Assicurati di seguire la [Elenco di controllo della sicurezza](../../help/sites-administering/security-checklist.md).

## Ambiente di pubblicazione {#publish-environment}

### Diventare membro {#becoming-a-member}

Nell’ambiente di pubblicazione, a seconda di [impostazioni](sites-console.md#user-management) del sito community, un visitatore del sito può diventare membro della community:

* Quando il sito community è privato (chiuso):
   * Su invito
   * Mediante azioni di un amministratore

* Quando il sito community è pubblico (aperto):
   * Per autoregistrazione
   * Per accesso social network con Facebook e Twitter

>[!NOTE]
>
>Quando un visitatore si registra come membro di un sito community aperto, diventa automaticamente membro di altri siti community aperti nello stesso ambiente di pubblicazione.

### Pubblica ruoli gruppo {#publish-group-roles}

| Se membro del gruppo... | Ruolo principale |
|---|---|
| Community &lt;*nome del sito*> Membri | Un membro del sito community è un utente registrato. Possono effettuare l&#39;accesso, modificare il proprio profilo, partecipare a un gruppo di community aperto, pubblicare contenuti nella community, inviare messaggi ad altri membri e seguire le attività del sito. |
| Community &lt;*nome del sito*> Moderatori | Un moderatore del sito della community è un membro fidato della community che è in grado di moderare UGC in blocco, utilizzando la console di moderazione o nel contesto, nella pagina in cui viene pubblicato il contenuto. |
| Community &lt;*nome del sito*> &lt;*nome gruppo*> Membri | Un membro del gruppo community è un membro della community che ha aderito a un gruppo aperto o è stato invitato a un gruppo chiuso. Possiedono le capacità di un membro per quel gruppo della community all’interno del sito. |
| Community &lt;*nome del sito*> Amministratori di gruppi | L&#39;amministratore di un gruppo del sito della community è un membro della community attendibile assegnato alla creazione e alla gestione di comunità secondarie (gruppi) all&#39;interno di un sito della community. È inclusa la possibilità di fornire moderazione nel contesto. |
| *Gruppo di sicurezza membri privilegiati* | Gruppo di utenti creato e gestito manualmente allo scopo di limitare la creazione di contenuti. Consulta [Gruppo membri privilegiati](#privileged-members-group). |
| Nessuno | Un visitatore anonimo del sito, che scopre il sito, può visualizzare e cercare i siti della community che consentono l’accesso anonimo. Per partecipare e pubblicare contenuti, l’utente deve auto-registrarsi (se consentito) e diventare membro della community. |

### Assegnazione di membri ai ruoli del gruppo di pubblicazione {#assigning-members-to-publish-group-roles}

Quando [creazione di un sito community](sites-console.md) nell’ambiente di authoring o quando [modifica delle proprietà del sito,](sites-console.md#modifying-site-properties) ai membri possono essere assegnati vari ruoli eseguiti nell’ambiente di pubblicazione, ad esempio moderatori, amministratori di gruppi, contatti per le risorse o membri con privilegi.

[Abilitazione del servizio tunnel](sync.md#accessingpublishusersfromauthor) consente di presentare le scelte di assegnazione dai membri al momento della pubblicazione anziché dagli utenti all’autore.

I membri selezionati verranno assegnati automaticamente al [gruppo appropriato](#publish-group-roles) e le loro appartenenze saranno incluse quando il sito community verrà (ri)pubblicato.

### Gruppo membri privilegiati {#privileged-members-group}

Lo scopo di un gruppo di sicurezza membri privilegiati è quello di limitare la creazione di contenuto per determinate funzioni di community a un sottoinsieme privilegiato di membri di un sito community.

Il gruppo di membri con privilegi è un gruppo di membri creato e gestito utilizzando [Console Gruppi community](members.md).

Dopo la creazione di un gruppo di membri con privilegi e con [servizio tunnel abilitato](sync.md#accessingpublishusersfromauthor), la struttura di un sito community esistente può essere [modificato](sites-console.md#modify-structure) per modificare la configurazione delle funzioni community in &quot;Consenti membri privilegiati&quot; e aggiungere il gruppo creato.

Le funzioni community che consentono di specificare uno o più gruppi di membri con privilegi sono:

* [Funzione blog](functions.md#blog-function) - limitare la creazione di nuovi articoli;
* [Funzione calendario](functions.md#calendar-function) - Limitare la creazione di nuovi eventi.
* [Funzione forum](functions.md#forum-function) - Limitare la creazione di nuovi argomenti.
* [Funzione QnA](functions.md#qna-function) - limitare la creazione di nuove domande;

Quando una funzione di community non è protetta (non è stato assegnato alcun gruppo di membri con privilegi), tutti i membri del sito della community possono creare contenuti di funzionalità (articoli, eventi, argomenti, domande).

>[!NOTE]
>
>L&#39;aggiunta di un utente a un gruppo di membri privilegiati per un sito community consente di creare privilegi solo se l&#39;utente è anche membro dello stesso sito community.

## Creazione di membri della community {#creating-community-members}

### Posizione archivio {#repository-location}

Per il corretto funzionamento di alcune funzioni, è necessario creare utenti e gruppi di utenti con i privilegi appropriati.

Quando i membri vengono creati in `/home/users/community`, ereditano gli ACL appropriati che assegnano privilegi di lettura ai profili dei membri.

Analogamente, è necessario creare gruppi di utenti community personalizzati (ad esempio gruppi di membri con privilegi) in `/home/groups/community`.

Utilizzo di [Console per membri e gruppi community](members.md) creerà utenti e gruppi in questi percorsi.

Per specificare un percorso personalizzato è necessario utilizzare l&#39;interfaccia utente di protezione classica, accessibile da [https://&lt;server>:&lt;port>/useradmin](http://localhost:4503/useradmin).

Per assegnare i privilegi di lettura per i percorsi membri personalizzati, in tutte le istanze di pubblicazione impostare ACL simili a `/home/users/community`:

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

Per assegnare i privilegi appropriati per i percorsi dei gruppi di membri personalizzati, ad esempio /home/groups/mycompany, in tutte le istanze di pubblicazione impostare ACL simili a `/home/groups/community`:

```xml
<allow
  jcr:primaryType="rep:GrantACE"
  rep:principalName="community-administrators"
  rep:privileges="{Name}[jcr:read]"  />
```

### Console {#consoles}

Sono disponibili quattro console separate solo nell’ambiente di authoring:

| console | Strumenti, protezione, utenti | Strumenti, sicurezza, gruppi | Community, Membri | Community, Gruppi |
|----------|-----------------------|------------------------|------------------------------------------------------------|------------------------------------------------------------|
| gestisce | utenti all’authoring | gruppi di utenti per authoring | membri al momento della pubblicazione | gruppi di membri alla pubblicazione |
| richiede | autorizzazione amministratore | autorizzazione amministratore | autorizzazione amministratore, servizio tunnel, sincronizzazione utenti per farm di pubblicazione | autorizzazione amministratore, servizio tunnel, sincronizzazione utenti per farm di pubblicazione |

### Ruolo Amministratori community {#community-administrators-role}

Come indicato nella [Ruoli del gruppo di authoring](#author-group-roles) , i membri del gruppo Amministratori community possono creare siti community, gestire siti, gestire membri (possono escludere membri dalla community) e moderare i contenuti.

Segui gli stessi passaggi della creazione e assegnazione di un utente al ruolo di gestione attivazione, ma aggiungi c `ommunity-administrators` nella scheda Gruppi dell&#39;utente.

### Integrazione LDAP {#ldap-integration}

L&#39;AEM supporta l&#39;utilizzo del protocollo LDAP per l&#39;autenticazione degli utenti e la creazione di account utente. Questo è descritto in [Configurazione di LDAP con AEM 6](../../help/sites-administering/ldap-config.md).

Di seguito sono riportati alcuni dettagli di configurazione specifici per i membri della community e i gruppi di membri.

1. Configura LDAP per ogni istanza di pubblicazione AEM.
2. [Provider di identità LDAP](../../help/sites-administering/ldap-config.md#configuring-the-ldap-identity-provider)

   * Nessuna istruzione speciale

3. [Gestore di sincronizzazione](../../help/sites-administering/ldap-config.md#configuring-the-synchronization-handler)

   * Imposta le seguenti proprietà:

      * **[!UICONTROL Iscrizione automatica utente]**: `community-<site name>-<uid>-members`
      * **[!UICONTROL Prefisso percorso utente]**: `/community`
      * **[!UICONTROL Prefisso percorso gruppo]**: `/community`

4. [Modulo di accesso esterno](../../help/sites-administering/ldap-config.md#the-external-login-module)

   * nessuna istruzione speciale

In questo modo gli utenti vengono automaticamente assegnati al gruppo membri del sito community e il percorso dell&#39;archivio viene `/home/users/community` e `/home/groups/community`, in modo che ereditino le autorizzazioni appropriate per visualizzare il profilo dell&#39;altro utente.

* Il `User auto membership` il valore deve essere `rep:authorizableId` proprietà, non `givenName` (nome visualizzato) dal profilo.

## Sincronizzazione degli utenti tra le istanze AEM {#synchronizing-users-among-aem-instances}

Quando si utilizza una [farm di pubblicazione](topologies.md), assicurati che gli utenti abbiano lo stesso percorso in ogni istanza di pubblicazione importando prima gli utenti in una sola istanza e [abilitazione della sincronizzazione utente](sync.md) Sling distribuisce gli utenti alle altre istanze di pubblicazione.

Se importi gruppi di utenti, per garantire che i gruppi di utenti abbiano lo stesso percorso in ogni istanza di pubblicazione, importa in un&#39;istanza, quindi [creare un pacchetto](../../help/sites-administering/package-manager.md#creating-a-new-package) per l’esportazione e installa quel pacchetto su tutte le altre istanze di pubblicazione.

Anche se la sincronizzazione dei gruppi di utenti tramite la sincronizzazione degli utenti sarà inclusa in una versione futura, al momento solo il *iscrizione* di un gruppo di utenti verrà sincronizzato durante l&#39;esecuzione della sincronizzazione degli utenti.

## Informazioni sui gruppi community {#about-community-groups}

Quando si parla di gruppi, ci sono due argomenti distinti:

* **[Gruppi community](overview.md#communitygroups)**

  I gruppi community sono le sottocomunità che possono essere create nell’ambiente di pubblicazione di un sito community che supporta la creazione di gruppi community. La creazione di un gruppo community comporta l&#39;aggiunta di più pagine al sito Web e viene gestita in modo simile al sito della community principale. Per ulteriori informazioni, visita [Nozioni di base sul gruppo community](essentials-groups.md) per sviluppatori e [Gruppo community](creating-groups.md) per autori.

* **[Gruppi di membri](../../help/sites-administering/security.md)**

  I gruppi di membri sono i gruppi a cui possono appartenere i membri e vengono gestiti tramite la console Gruppi. Gran parte della discussione su questa pagina è stata dedicata ai gruppi membri. I gruppi di membri creati automaticamente per un sito community, ai quali viene aggiunto il prefisso *`Community`*, può essere definito gruppo comunitario, pertanto occorre considerare il contesto della discussione.
