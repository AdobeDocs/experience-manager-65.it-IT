---
title: Configurazione iniziale
description: Scopri come configurare inizialmente le community Adobe Experience Manager.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
exl-id: 6bda0f09-7ae5-4540-b035-9dd249ac3186
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 1%

---

# Configurazione iniziale {#initial-setup}

## Avvia istanze di Author e Publish {#start-author-and-publish-instances}

A scopo di sviluppo e dimostrazione, è necessario eseguire un’istanza Author e una Publish.

Per farlo, segui le istruzioni di base di Adobe Experience Manager (AEM) [Guida introduttiva](../../help/sites-deploying/deploy.md#getting-started), che si traducono nel seguente:

* Ambiente di authoring in [localhost:4502](http://localhost:4502/)
* Ambiente Publish su [localhost:4503](http://localhost:4503/)

Per AEM Communities,

* L’ambiente di authoring è destinato a:

   * Sviluppo di siti, modelli e componenti.
   * Attività amministrative e di configurazione.

* L’ambiente Publish è destinato a:

   * Esperienza comunitaria di pubblicazione e moderazione di contenuti.
   * Creazione di gruppi community, membri e gruppi di membri.

>[!NOTE]
>
>Se non conosci l&#39;AEM, consulta la documentazione sulle [operazioni di base](../../help/sites-authoring/basic-handling.md) e una [guida rapida all&#39;authoring delle pagine](../../help/sites-authoring/qg-page-authoring.md).

## Installa versione più recente di Communities {#install-latest-communities-release}

Questa esercitazione crea un [sito community di engagement](overview.md#engagement-community) basato su AEM Communities 6.2 feature pack versione 1.10.

Per verificare che sia installato il feature pack più recente, visitare il sito:

* [Ultime versioni](deploy-communities.md#latest-releases)

## Configura Analytics {#configure-analytics}

Quando [Adobe Analytics è configurato per il sito della community](analytics.md), sono disponibili informazioni sull&#39;attività della community che migliorano l&#39;esperienza dei membri della community e forniscono feedback agli amministratori del sito.

L’integrazione con Adobe Analytics è facoltativa.

## Configura e-mail per notifiche {#configure-email-for-notifications}

La funzionalità delle notifiche, disponibile per impostazione predefinita per tutti i siti creati utilizzando la console `Communities Sites`, fornisce un canale e-mail per le notifiche.

È necessario che l’e-mail sia configurata correttamente per il sito.

Vedi [Configurazione dell&#39;e-mail](email.md).

## Abilita il servizio tunnel {#enable-the-tunnel-service}

Durante la creazione di un sito community nell&#39;ambiente di authoring, il servizio tunnel consente di assegnare ruoli a membri della community attendibili registrati nell&#39;ambiente Publish. Il servizio tunnel consente inoltre l&#39;accesso ai membri della community dalle console [Membri e gruppi](members.md) nell&#39;ambiente di authoring.

La convenzione prevede che i membri e i gruppi di membri creati nell&#39;ambiente Publish possano *non* essere ricreati nell&#39;ambiente di authoring. Per ulteriori informazioni, vedere [Gestione di utenti e gruppi di utenti](users.md).

Per istruzioni semplici per abilitare il servizio tunnel in un&#39;istanza **Author**, vedere [Servizio tunnel](deploy-communities.md#tunnel-service-on-author).

## Ruolo di amministratore community {#community-administrator-role}

I membri del gruppo Amministratori community possono creare siti community, gestire siti, gestire membri (possono escludere membri dalla community) e moderare i contenuti.

### Crea utente {#create-user}

Crea un utente su *author*, al quale viene assegnato il ruolo di amministratore community:

* Sull’istanza di authoring

   * Ad esempio, [http://localhost:4502/](http://localhost:4503/)

* Accedi con privilegi di amministratore

   * Ad esempio, nome utente &quot;admin&quot; / password &quot;admin&quot;

* Dalla console principale, passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Utenti]**.
* Dal menu **Modifica**, seleziona **[!UICONTROL Aggiungi utente]**

* Nella finestra di dialogo `Create New User` immetti:

   * **[!UICONTROL ID]**: sirius
   * **[!UICONTROL Indirizzo e-mail]**: sirius.nilson@mailinator.com
   * **[!UICONTROL Password]**: password
   * **[!UICONTROL Conferma password&ast;]**: password
   * **[!UICONTROL Nome]**: Sirius
   * **[!UICONTROL Cognome]**: Nilson

### Assegna Sirius al gruppo amministratori community {#assign-sirius-to-community-administrators-group}

Scorri verso il basso fino a `Add User to Groups`:

* Inserisci &#39;C&#39; per cercare

   * Seleziona `Community Administrators`
   * Seleziona `Community Enablement Managers`

* Seleziona **[!UICONTROL Salva]**.

![create-user](assets/create-user.png)

## Abilita accesso social network {#enable-social-login}

Prima di poter utilizzare le versioni dimostrative di accesso social network con Facebook e Twitter, è necessario

1. Installa un fix pack o [l&#39;ultimo feature pack](deploy-communities.md#latestfeaturepack) (per le modifiche API di Facebook di marzo 2017).
1. [Abilitare il provider OAuth](social-login.md#adobe-granite-oauth-authentication-handler) nell&#39;ambiente di pubblicazione.

Per i server di produzione, è necessario creare i servizi cloud necessari per fornire l’accesso social.

Consulta [Accesso social network con Facebook e Twitter](social-login.md).

## Creare tag tutorial {#create-tutorial-tags}

Creare i tag in modo da poterli utilizzare per le esercitazioni di coinvolgimento, utilizzando lo spazio dei nomi dei tag di `Tutorial`.

Utilizza la [console di assegnazione tag](../../help/sites-administering/tags.md#tagging-console) per creare i seguenti tag:

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![tutorial-tags](assets/tutorial-tags.png)

Quindi seguire le istruzioni per:

1. [Impostare le autorizzazioni tag](../../help/sites-administering/tags.md#setting-tag-permissions).
1. [Publish dei tag](../../help/sites-administering/tags.md#publishing-tags).

Pacchetto di esempio di tag creati per i Tutorials della Guida introduttiva di AEM Communities

[Ottieni file](assets/tutorial_tags-v63.zip)

## MongoDB per archivio comune UGC {#mongodb-for-ugc-common-store}

È consigliabile, ma facoltativo, impostare [MSRP](msrp.md) (MongoDB) come [archivio comune](working-with-srp.md) per sperimentare la flessibilità di moderazione di tutti i contenuti generati dagli ambienti di pubblicazione e/o di authoring.

Per istruzioni, visita [Come configurare MongoDB per Demo](demo-mongo.md).

Per impostazione predefinita, l&#39;installazione delle istanze AEM di authoring e pubblicazione fa sì che il contenuto generato dall&#39;utente (UGC) venga archiviato nell&#39;archivio Tar [JCR](../../help/sites-deploying/platform.md), a cui si accede utilizzando [JSRP](jsrp.md). JSRP non è un archivio comune, il che significa che UGC è visibile solo sull’istanza in cui è stato immesso. In genere, l&#39;UGC viene immesso in un&#39;istanza di pubblicazione e non è visibile nell&#39;ambiente di authoring, pertanto tutte le attività di moderazione devono utilizzare l&#39;istanza di pubblicazione.
