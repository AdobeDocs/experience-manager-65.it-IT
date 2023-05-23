---
title: Configurazione iniziale
seo-title: Initial Setup
description: Impostazione delle community
seo-description: Setting up Communities
uuid: c53d280c-c5ae-47cf-8038-f0dea68e15ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 0d462ad1-5619-4bb6-9609-bc8987c40a0c
exl-id: 6bda0f09-7ae5-4540-b035-9dd249ac3186
source-git-commit: 942db8fe3dad16be53dc6abe0e519d97a659e480
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 2%

---

# Configurazione iniziale {#initial-setup}

## Avvia istanze di authoring e pubblicazione {#start-author-and-publish-instances}

A scopo di sviluppo e dimostrazione, sarà necessario eseguire un’istanza Author e una Publish.

Per farlo, seguire le istruzioni di base dell’AEM [Guida introduttiva](../../help/sites-deploying/deploy.md#getting-started) istruzioni, che si tradurranno in:

* Ambiente di authoring su [localhost:4502](Http://localhost:4502/)
* Ambiente di pubblicazione su [localhost:4503](Http://localhost:4503/)

Per AEM Communities,

* L’ambiente di authoring è destinato a:

   * Sviluppo di siti, modelli e componenti.
   * Attività amministrative e di configurazione.

* L’ambiente di pubblicazione è destinato a:

   * Esperienza comunitaria di pubblicazione e moderazione di contenuti.
   * Creazione di gruppi community, membri e gruppi di membri.

>[!NOTE]
>
>Se non conosci l’AEM, consulta la documentazione su [operazioni di base](../../help/sites-authoring/basic-handling.md) e un [guida rapida all’authoring delle pagine](../../help/sites-authoring/qg-page-authoring.md).

## Installa versione più recente di Communities {#install-latest-communities-release}

Questa esercitazione crea un [sito community di engagement](overview.md#engagement-community) ed è basato su AEM Communities 6.2 feature pack versione 1.10.

Per verificare che sia installato il feature pack più recente, visitare il sito:

* [Ultime versioni](deploy-communities.md#latest-releases)

## Configura Analytics {#configure-analytics}

Quando [Adobe Analytics è configurato per il sito community](analytics.md), sono disponibili informazioni sull&#39;attività della community che migliorano l&#39;esperienza dei membri della community e forniscono feedback agli amministratori del sito.

L’integrazione con Adobe Analytics è facoltativa.

## Configura e-mail per notifiche {#configure-email-for-notifications}

La funzione di notifica, disponibile per impostazione predefinita per tutti i siti creati utilizzando `Communities Sites` , fornisce un canale e-mail per le notifiche.

È necessario che l’e-mail sia configurata correttamente per il sito.

Consulta [Configurazione dell’e-mail](email.md).

## Abilita il servizio tunnel {#enable-the-tunnel-service}

Durante la creazione di un sito community nell&#39;ambiente di authoring, il servizio tunnel consente di assegnare ruoli a membri della community trusted registrati nell&#39;ambiente di pubblicazione. Il servizio di tunnel consente anche l&#39;accesso ai membri della comunità dal [Console membri e gruppi](members.md) nell’ambiente di authoring.

La convenzione è destinata ai membri e ai gruppi di membri creati nell’ambiente di pubblicazione per *non* nell’ambiente di authoring. Per ulteriori informazioni, consulta [Gestione di utenti e gruppi di utenti](users.md).

Per istruzioni semplici per abilitare il servizio tunnel su un **autore** istanza, vedi [Servizio tunnel](deploy-communities.md#tunnel-service-on-author).

## Ruolo di amministratore community {#community-administrator-role}

I membri del gruppo Amministratori community possono creare siti community, gestire siti, gestire membri (possono escludere membri dalla community) e moderare i contenuti.

### Crea utente {#create-user}

Crea un utente il *autore*, al quale è assegnato il ruolo di amministratore community:

* Sull’istanza di authoring

   * Ad esempio: [http://localhost:4502/](Http://localhost:4503/)

* Accedi con privilegi di amministratore

   * Ad esempio, nome utente &quot;admin&quot; / password &quot;admin&quot;

* Dalla console principale, accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Utenti]**.
* Dalla sezione **Modifica** menu, seleziona **[!UICONTROL Aggiungi utente]**

* In `Create New User` finestra di dialogo immetti:

   * **[!UICONTROL ID]**: sirius
   * **[!UICONTROL Indirizzo e-mail]**: sirius.nilson@mailinator.com
   * **[!UICONTROL Password]**: password
   * **[!UICONTROL Conferma password&amp;ast;]**: password
   * **[!UICONTROL Nome]**: Sirio
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

1. Installare un fix pack o [feature pack più recente](deploy-communities.md#latestfeaturepack) (per le modifiche all’API Facebook di marzo 2017).
1. [Abilitare il provider OAuth](social-login.md#adobe-granite-oauth-authentication-handler) nell’ambiente di pubblicazione.

Per i server di produzione, è necessario creare i servizi cloud necessari per fornire l’accesso social.

Consulta [Accesso social network con Facebook e Twitter](social-login.md).

## Creare tag tutorial {#create-tutorial-tags}

Crea i tag da utilizzare per le esercitazioni coinvolgenti, utilizzando lo spazio dei nomi tag di `Tutorial`.

Utilizza il [Console assegnazione tag](../../help/sites-administering/tags.md#tagging-console) per creare i seguenti tag:

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![tutorial-tags](assets/tutorial-tags.png)

Quindi seguire le istruzioni per:

1. [Impostare le autorizzazioni tag](../../help/sites-administering/tags.md#setting-tag-permissions).
1. [Pubblicare i tag](../../help/sites-administering/tags.md#publishing-tags).

Pacchetto di esempio di tag creati per i Tutorials della Guida introduttiva di AEM Communities

[Ottieni file](assets/tutorial_tags-v63.zip)

## MongoDB per archivio comune UGC {#mongodb-for-ugc-common-store}

Si consiglia, ma facoltativo, di impostare [MSRP](msrp.md) (MongoDB) come [archivio comune](working-with-srp.md) per sperimentare la flessibilità di moderare tutti i contenuti UGC dagli ambienti di pubblicazione e/o di authoring.

Per istruzioni visita [Come impostare MongoDB per la demo](demo-mongo.md).

Per impostazione predefinita, l’installazione delle istanze AEM di authoring e pubblicazione fa sì che i contenuti generati dagli utenti (UGC) vengano memorizzati in [Archiviazione Tar JCR](../../help/sites-deploying/platform.md) a cui si accede tramite [JSRP](jsrp.md). JSRP non è un archivio comune, il che significa che UGC è visibile solo sull’istanza in cui è stato immesso. In genere, l&#39;UGC viene immesso in un&#39;istanza di pubblicazione e non è visibile nell&#39;ambiente di authoring, pertanto tutte le attività di moderazione devono utilizzare l&#39;istanza di pubblicazione.
