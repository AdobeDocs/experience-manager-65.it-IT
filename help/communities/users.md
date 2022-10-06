---
title: Gestione di utenti e gruppi di utenti
seo-title: Managing Users and User Groups
description: Gli utenti di AEM Communities possono registrarsi autonomamente e modificare i propri profili
seo-description: Users of AEM Communities can self-register and edit their profiles
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
source-wordcount: '2168'
ht-degree: 0%

---

# Gestione di utenti e gruppi di utenti {#managing-users-and-user-groups}

## Panoramica {#overview}

In AEM Communities, nell’ambiente di pubblicazione, gli utenti possono registrarsi autonomamente e modificare i propri profili. Dati i permessi appropriati, possono inoltre:

* Crea sub-community all’interno del sito della community (consulta [gruppi comunitari](creating-groups.md)).

* [Moderato](moderation.md) contenuto generato dall’utente (UGC).

* Essere [risorsa di abilitazione](resources.md) contatti.

* Essere [privilegiato](#privileged-members-group) per creare voci per blog, calendari, QnA e forum.

Gli utenti registrati nell’ambiente di pubblicazione sono generalmente denominati *membri della comunità (membri)* distinguerli *utenti* nell’ambiente di authoring.

Le autorizzazioni vengono concesse assegnando i membri a uno dei [gruppi membri (utente)](#publish-group-roles) creato dinamicamente quando il sito della community è [creato](sites-console.md) o [Modificata](sites-console.md#modifying-site-properties) dall’ambiente di authoring. Quando lavori dall’ambiente di authoring, i membri sono visibili dall’ambiente di pubblicazione tramite la funzione [servizio tunnel](#tunnel-service).

Per progettazione, i membri e i gruppi di membri creati nell’ambiente di pubblicazione non devono essere visualizzati nell’ambiente di authoring. Analogamente, gli utenti e i gruppi di utenti creati nell’ambiente di authoring hanno lo scopo di rimanere nell’ambiente di authoring.

Quando gli utenti dell&#39;autore e i membri al momento della pubblicazione provengono dallo stesso elenco di utenti, ad esempio sincronizzati dalla stessa directory LDAP, non vengono considerati lo stesso utente con le stesse autorizzazioni e appartenenza al gruppo sia negli ambienti di authoring che di pubblicazione. I ruoli dei membri e degli utenti devono essere stabiliti separatamente al momento della pubblicazione e dell&#39;autore, a seconda dei casi.

Per [pubblica azienda](topologies.md), la registrazione e le modifiche apportate a un’istanza di pubblicazione devono essere sincronizzate con altre istanze di pubblicazione per consentire loro di accedere agli stessi dati utente. Per maggiori dettagli vedi [Sincronizzazione utente](sync.md), che include una sezione che descrive [Cosa Succede Quando..](sync.md#what-happens-when).

### Limiti per contributi {#contribution-limits}

Al fine di proteggere dallo spam, è possibile limitare la frequenza di pubblicazione dei contenuti da parte dei membri. Inoltre, è possibile limitare automaticamente i contributi dei nuovi iscritti.

Per maggiori dettagli, vedi [Limiti dei contributi degli Stati membri](limits.md).

### Gruppi di utenti creati dinamicamente {#dynamically-created-user-groups}

Quando si crea un nuovo sito community, i nuovi gruppi di utenti vengono creati in modo dinamico con ID univoci (uid) e autorizzazioni appropriate per varie funzioni amministrative necessarie per gestire il sito community nell’ambiente di authoring (consulta [Ruoli gruppo autore](#author-group-roles)) o l’ambiente di pubblicazione (consulta [Ruoli gruppo di pubblicazione](#publish-group-roles)).

I nomi dei gruppi vengono generati dal nome assegnato al sito durante [creazione di siti community](sites-console.md#step13asitetemplate). Gli ID univoci evitano conflitti di denominazione per siti community e gruppi community con nomi simili sullo stesso server.

Ad esempio, se il nome del sito era &quot;*coinvolgere*&quot; per un sito intitolato &quot;We.Retail Engage&quot;, uno dei gruppi di utenti creati è:

* Community *Coinvolgi* Membri

## Ambiente di authoring {#author-environment}

### Servizio tunnel {#tunnel-service}

Quando si utilizza l’ambiente di authoring in [creare siti](sites-console.md), [modificare le proprietà del sito](sites-console.md#modifying-site-properties) e [gestire membri della community e gruppi di membri](members.md), è necessario accedere a utenti e gruppi di utenti registrati nell’ambiente di pubblicazione.

Il servizio tunnel fornisce questo accesso utilizzando l&#39;agente di replica sull&#39;autore.

* Per maggiori dettagli, vedi [istruzioni di configurazione](deploy-communities.md#tunnel-service-on-author) nella pagina di distribuzione.

La [Console Membri e gruppi di Communities](members.md) sono destinati esclusivamente alla gestione di utenti (membri) e gruppi di utenti (gruppi di membri) registrati solo nell’ambiente di pubblicazione.

Per gestire gli utenti e i gruppi di utenti registrati nell’ambiente di authoring, utilizza la funzione [Console di sicurezza](../../help/sites-administering/security.md)

### Ruoli gruppo autore {#author-group-roles}

| Se membro del gruppo.. | Ruolo principale |
|---|---|
| amministratori | Il gruppo di amministratori è costituito da amministratori di sistema che dispongono di tutte le capacità di un amministratore della community e dalla possibilità di gestire il gruppo di amministratori della community. |
| Amministratori community | Il gruppo Amministratori community diventa automaticamente membro di tutti i siti della community e di tutti i gruppi della community creati sul sito. Un membro iniziale del gruppo Amministratori community è il gruppo Amministratori. Nell’ambiente di authoring, gli amministratori della community possono creare siti di community, gestirli, gestirli e moderare i contenuti. |
| Community &lt;*nome del sito*> Sitecontentmanager | Community Site Content Manager è in grado di eseguire operazioni di authoring AEM tradizionali, creazione di contenuti e modifica di pagine per un sito community. |
| Responsabili dell&#39;abilitazione della community | Il gruppo Community Enablement Manager è costituito da utenti disponibili per l&#39;assegnazione per gestire il gruppo Enablement Manager di un sito community. |
| Community &lt;*nome del sito* > Siteenablementmanager | Il gruppo Community Site Enablement Manager è costituito da utenti che sono stati assegnati per gestire l&#39;abilitazione di un sito community [risorse](resources.md). |
| Nessuno | Un visitatore anonimo del sito non può accedere all’ambiente di authoring. |

### Amministratori di sistema {#system-administrators}

I membri del gruppo di amministratori sono amministratori di sistema in grado di eseguire la configurazione iniziale di un’installazione di AEM per gli ambienti di authoring e di pubblicazione.

A scopo dimostrativo e di sviluppo, il gruppo di amministratori ha un membro il cui id utente è *admin* e la password è *admin*.

Per gli ambienti di produzione, è necessario modificare il gruppo di amministratori predefiniti.

Assicurati di seguire il [Lista di controllo sicurezza](../../help/sites-administering/security-checklist.md).

## Ambiente di pubblicazione {#publish-environment}

### Diventare membro {#becoming-a-member}

Nell’ambiente di pubblicazione, a seconda del [impostazioni](sites-console.md#user-management) del sito community, un visitatore del sito può diventare membro della community:

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
| Community &lt;*nome del sito*> &lt;*nome gruppo*> Membri | Un membro del gruppo comunitario è un membro della comunità che ha aderito a un gruppo comunitario aperto o è stato invitato a un gruppo comunitario chiuso. Hanno le capacità di un membro per quel gruppo di comunità all&#39;interno del sito. |
| Community &lt;*nome del sito*> Amministratori di gruppo | Un amministratore di gruppo di siti community è un membro della community fidato che viene assegnato per creare e gestire sottocommunity (gruppi) all’interno di un sito community. Included è la capacità di fornire moderazione nel contesto. |
| *Gruppo di sicurezza dei membri con privilegi* | Un gruppo di utenti creato e gestito manualmente allo scopo di limitare la creazione di contenuti. Vedi [Gruppo di membri con privilegi](#privileged-members-group). |
| Nessuno | Un visitatore anonimo del sito, che scopre il sito, può visualizzare e cercare siti della community che consentono l’accesso anonimo. Per partecipare e pubblicare contenuti, l’utente deve registrarsi autonomamente (se consentito) e diventare membro della community. |

### Assegnazione dei membri ai ruoli del gruppo di pubblicazione {#assigning-members-to-publish-group-roles}

Quando [creazione di un sito community](sites-console.md) nell’ambiente di authoring o quando [modifica delle proprietà del sito,](sites-console.md#modifying-site-properties) ai membri possono essere assegnati vari ruoli eseguiti nell’ambiente di pubblicazione, ad esempio moderatori, amministratori di gruppo, contatti di risorse o membri con privilegi.

[Abilitazione del servizio tunnel](sync.md#accessingpublishusersfromauthor) determina la presentazione delle scelte di assegnazione da parte dei membri al momento della pubblicazione anziché da parte degli utenti all&#39;autore.

I membri selezionati verranno automaticamente assegnati al [gruppo appropriato](#publish-group-roles) e le loro appartenenze saranno incluse quando il sito della comunità sarà (ri)pubblicato.

### Gruppo membri privilegiati {#privileged-members-group}

Lo scopo di un gruppo di sicurezza per i membri privilegiati è quello di limitare la creazione di contenuti per alcune funzioni della community a un sottoinsieme privilegiato di membri di un sito community.

Il gruppo di membri privilegiati è un gruppo di membri creato e gestito utilizzando il [Console Gruppi community](members.md).

Dopo la creazione di un gruppo di membri privilegiati e con [servizio tunnel abilitato](sync.md#accessingpublishusersfromauthor), la struttura di un sito community esistente può essere [Modificata](sites-console.md#modify-structure) per modificare la configurazione delle sue funzioni di community in &quot;Consenti membri con privilegi&quot; e aggiungere il gruppo creato.

Le funzioni comunitarie che consentono la specificazione di uno o più gruppi di membri privilegiati sono:

* [Funzione blog](functions.md#blog-function) - Limitare la creazione di nuovi articoli.
* [Funzione calendario](functions.md#calendar-function) - Limitare la creazione di nuovi eventi.
* [Funzione forum](functions.md#forum-function) - Limitare la creazione di nuovi argomenti.
* [Funzione QnA](functions.md#qna-function) - Limitare la creazione di nuove domande.

Quando una funzione community non è protetta (nessun gruppo di membri privilegiati assegnato), a tutti i membri del sito community è consentito creare contenuti di funzionalità (articoli, eventi, argomenti, domande).

>[!NOTE]
>
>L&#39;aggiunta di un utente a un gruppo di membri privilegiati per un sito community consente loro di creare privilegi solo se sono anche membri dello stesso sito community.

## Creazione di membri della community {#creating-community-members}

### Posizione archivio {#repository-location}

Affinché alcune funzioni funzionino correttamente, è necessario creare utenti e gruppi di utenti con i privilegi appropriati.

Quando i membri vengono creati in `/home/users/community`, ereditano le ACL appropriate che danno privilegi di lettura ai profili dei membri.

Allo stesso modo, i gruppi di utenti personalizzati della community (come i gruppi di membri privilegiati) devono essere creati in `/home/groups/community`.

Utilizzo della [Console Membri e gruppi di Communities](members.md) creerà utenti e gruppi in questi percorsi.

Per specificare un percorso personalizzato è necessario utilizzare l’interfaccia classica di sicurezza, accessibile in [https://&lt;server>:&lt;port>/useradmin](http://localhost:4503/useradmin).

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

In genere, la possibilità per un visitatore del sito di registrarsi autonomamente non è consentita per un [comunità di abilitazione](overview.md#enablement-community) in quanto i costi sono associati a ciascun membro. Gli studenti di abilitazione e le risorse vengono gestiti da un utente a cui è stato assegnato il [ruolo](#author-group-roles) di `enablement manager` [durante la creazione del sito](sites-console.md#enablement) sull&#39;autore (aggiunto come membro del gruppo) `Community <site-name> Siteenablementmanagers`). La `enablement manager` è anche responsabile [assegnazione di risorse di apprendimento](resources.md) ai membri della comunità su autore.

Solo utenti membri del gruppo globale `Community Enablement Managers` può essere selezionato come `enablement manager` per un sito specifico della community.

Per creare un utente a cui può essere assegnato il ruolo di `Community Site Enablement Manager`, utilizza la console di sicurezza dell’interfaccia classica per specificare il percorso:

Su un&#39;istanza dell&#39;autore:

1. Accesso con privilegi di amministratore, passa alla console di sicurezza dell’interfaccia classica.

   Ad esempio: [http://localhost:4502/useradmin](http://localhost:4502/useradmin)

2. Dal menu Modifica, seleziona **[!UICONTROL Crea utente]**.
3. Compila il `Create User` finestra di dialogo.
   * Il percorso deve essere `/home/users/community`.
4. Seleziona **[!UICONTROL Crea]**.

   ![create-community-user](assets/create-community-user.png)

* Nel riquadro a sinistra, cerca l’utente appena creato e seleziona per visualizzarlo nel riquadro a destra.

   ![utente della community](assets/view-community-user.png)

Nel riquadro a sinistra:

1. Deseleziona la casella di ricerca e seleziona **[!UICONTROL Nascondi utenti]**.
2. Individua e trascina `community-enablementmanagers` al **[!UICONTROL Gruppi]** scheda del nuovo utente visualizzato nel riquadro a destra.

   ![gruppo di assegnazione](assets/assign-group.png)

### Ruolo degli amministratori della community {#community-administrators-role}

Come indicato nella [Ruoli gruppo autore](#author-group-roles) I membri del gruppo Amministratori community possono creare siti di community, gestire siti, gestire membri (possono vietare membri della community) e moderare contenuti.

Segui gli stessi passaggi della creazione e dell’assegnazione di un utente al ruolo di [responsabile dell&#39;abilitazione](#communitysiteenablementmanagerrole), ma aggiungi c `ommunity-administrators` nella scheda Gruppi dell’utente.

### Integrazione LDAP {#ldap-integration}

AEM supporta l&#39;utilizzo di LDAP per l&#39;autenticazione degli utenti e la creazione di account utente. Questo è descritto in [Configurazione di LDAP con AEM 6](../../help/sites-administering/ldap-config.md).

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

In questo modo gli utenti vengono automaticamente assegnati al gruppo di membri del sito della community e la posizione dell&#39;archivio viene assegnata `/home/users/community` e `/home/groups/community`, in modo che ereditino le autorizzazioni appropriate per visualizzare il profilo degli altri.

* La `User auto membership` deve essere `rep:authorizableId` proprietà, non `givenName` (nome visualizzato) dal profilo.

## Sincronizzazione Degli Utenti Tra Le Istanze AEM {#synchronizing-users-among-aem-instances}

Quando si utilizza un [pubblica azienda](topologies.md), assicurati che gli utenti abbiano lo stesso percorso in ogni istanza di pubblicazione importando gli utenti prima in un’istanza e [abilitazione della sincronizzazione utente](sync.md) per distribuire gli utenti alle altre istanze di pubblicazione.

Se si importano gruppi di utenti, per assicurarsi che i gruppi di utenti abbiano lo stesso percorso in ogni istanza di pubblicazione, importare in un&#39;istanza, quindi [creare un pacchetto](../../help/sites-administering/package-manager.md#creating-a-new-package) per esportare e installare il pacchetto su tutte le altre istanze di pubblicazione.

Mentre la sincronizzazione dei gruppi di utenti tramite la sincronizzazione utente verrà inclusa in una versione futura, attualmente solo la *iscrizione* di un gruppo di utenti verrà sincronizzato quando la sincronizzazione utente viene eseguita.

## Informazioni sui gruppi della community {#about-community-groups}

Quando si discute dei gruppi, ci sono due argomenti distinti:

* **[Gruppi comunitari](overview.md#communitygroups)**

   I gruppi comunitari sono le sub-comunità che possono essere create nell&#39;ambiente di pubblicazione per un sito comunitario che supporta la creazione di gruppi di comunità. La creazione di un gruppo di community determina l’aggiunta di più pagine al sito web e viene gestita in modo simile al sito della comunità padre. Per ulteriori informazioni, visita [Nozioni di base sui gruppi community](essentials-groups.md) per sviluppatori e [Gruppo community](creating-groups.md) per gli autori.

* **[Gruppi di membri](../../help/sites-administering/security.md)**

   I gruppi di membri sono i gruppi a cui i membri possono appartenere e sono gestiti tramite la console Gruppi. Gran parte della discussione su questa pagina è stata dedicata ai gruppi membri. I gruppi di membri vengono creati automaticamente per un sito della community, con il prefisso *`Community`*, può essere denominato gruppo comunitario, pertanto il contesto del dibattito deve essere considerato.
