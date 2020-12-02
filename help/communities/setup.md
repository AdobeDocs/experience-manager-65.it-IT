---
title: Configurazione iniziale
seo-title: Configurazione iniziale
description: Impostazione di Communities
seo-description: Impostazione di Communities
uuid: c53d280c-c5ae-47cf-8038-f0dea68e15ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 0d462ad1-5619-4bb6-9609-bc8987c40a0c
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 2%

---


# Configurazione iniziale {#initial-setup}

## Avvio istanze di creazione e pubblicazione {#start-author-and-publish-instances}

A scopo di sviluppo e dimostrazione, sarà necessario eseguire un’istanza di creazione e pubblicazione.

A tal fine, seguire le AEM di base [Guida introduttiva](../../help/sites-deploying/deploy.md#getting-started), che si tradurranno in:

* Ambiente di authoring su [localhost:4502](Http://localhost:4502/)
* Ambiente di pubblicazione su [localhost:4503](Http://localhost:4503/)

Per  AEM Communities,

* L’ambiente di authoring è destinato a:

   * Sviluppo di siti, modelli e componenti.
   * Attività amministrative e di configurazione.

* L’ambiente di pubblicazione è destinato a:

   * L&#39;esperienza della community di pubblicazione e moderazione dei contenuti.
   * Creazione di gruppi di community, membri e gruppi di membri.

>[!NOTE]
>
>Se non avete familiarità con AEM, visualizzate la documentazione su [operazioni di base](../../help/sites-authoring/basic-handling.md) e una [guida rapida all&#39;authoring delle pagine](../../help/sites-authoring/qg-page-authoring.md).

## Installazione della versione più recente di Communities {#install-latest-communities-release}

Questa esercitazione crea un [sito della community di coinvolgimento](overview.md#engagement-community) e si basa  feature pack AEM Communities 6.2 versione 1.10.

Per verificare che sia installato il pacchetto di funzioni più recente, visita:

* [Ultime versioni](deploy-communities.md#latest-releases)

Per un&#39;esercitazione che crea un [sito della community di abilitazione](overview.md#enablement-community), visitare la [Guida introduttiva  AEM Communities per Enablement](getting-started-enablement.md).

## Configura Analytics {#configure-analytics}

Quando [ Adobe Analytics è configurato per il sito della community](analytics.md), sono disponibili informazioni sull&#39;attività della community che migliorano l&#39;esperienza del membro della community e forniscono feedback agli amministratori del sito.

L&#39;integrazione con  Adobe Analytics è facoltativa.

## Configura e-mail per notifiche {#configure-email-for-notifications}

La funzione notifiche, disponibile per impostazione predefinita per tutti i siti creati utilizzando la console `Communities Sites`, fornisce un canale e-mail per le notifiche.

Ciò che è necessario è che le e-mail siano configurate correttamente per il sito.

Vedere [Configurazione di Email](email.md).

## Abilitare il servizio Tunnel {#enable-the-tunnel-service}

Quando si crea un sito community nell&#39;ambiente di authoring, il servizio tunnel consente di assegnare ruoli a membri attendibili della community registrati nell&#39;ambiente di pubblicazione. Il servizio tunnel consente inoltre l&#39;accesso ai membri della community dalle [console Membri e Gruppi](members.md) nell&#39;ambiente di authoring.

La convenzione è per i membri e i gruppi di membri creati nell’ambiente di pubblicazione su *non* da ricreare nell’ambiente di authoring. Per ulteriori informazioni, vedere [Gestione di utenti e gruppi di utenti](users.md).

Per istruzioni semplici sull&#39;abilitazione del servizio tunnel su un&#39;istanza **author**, vedere [Tunnel Service](deploy-communities.md#tunnel-service-on-author).

## Ruolo amministratore community {#community-administrator-role}

I membri del gruppo Amministratori community possono creare siti community, gestire siti, gestire membri (possono vietare membri della community) e moderare contenuti.

### Crea utente {#create-user}

Create un utente su *author*, al quale viene assegnato il ruolo di Amministratore community:

* Nell’istanza di creazione

   * Ad esempio, [http://localhost:4502/](Http://localhost:4503/)

* Accesso con privilegi di amministratore

   * Ad esempio, nome utente &#39;admin&#39; / password &#39;admin&#39;

* Dalla console principale, passare a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Utenti]**.
* Dal menu **Modifica**, selezionare **[!UICONTROL Aggiungi utente]**

* Nella finestra di dialogo `Create New User` immettere:

   * **[!UICONTROL ID]**: sirius
   * **[!UICONTROL Indirizzo]** e-mail: sirius.nilson@mailinator.com
   * **[!UICONTROL Password]**: password
   * **[!UICONTROL Conferma password&amp;ast;]**: password
   * **[!UICONTROL Nome]**: Sirio
   * **[!UICONTROL Cognome]**: Nilson

### Assegna sirius al gruppo di amministratori della community {#assign-sirius-to-community-administrators-group}

Scorri verso il basso fino a `Add User to Groups`:

* Immettere &#39;C&#39; per la ricerca

   * Seleziona `Community Administrators`
   * Seleziona `Community Enablement Managers`

* Seleziona **[!UICONTROL Salva]**.

![create-user](assets/create-user.png)

## Abilita accesso tramite social network {#enable-social-login}

Prima che possano essere utilizzate le versioni dimostrative di accesso social con Facebook e Twitter, è necessario

1. Installate un fix pack o [ultimo feature pack](deploy-communities.md#latestfeaturepack) (per le modifiche dell&#39;API Facebook di marzo 2017).
1. [Abilitate il ](social-login.md#adobe-granite-oauth-authentication-handler) provider OAuth nell&#39;ambiente di pubblicazione.

Per i server di produzione, è necessario creare i servizi cloud necessari per fornire il login mediante profilo sociale.

Consultate [Accesso tramite social network con Facebook e Twitter](social-login.md).

## Creare tag di esercitazione {#create-tutorial-tags}

Create i tag da utilizzare per le esercitazioni di coinvolgimento e abilitazione, utilizzando lo spazio dei nomi tag di `Tutorial`.

Utilizzate la [console Tagging](../../help/sites-administering/tags.md#tagging-console) per creare i seguenti tag:

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![tutorial-tags](assets/tutorial-tags.png)

Seguite quindi le istruzioni per:

1. [Impostate le autorizzazioni](../../help/sites-administering/tags.md#setting-tag-permissions) del tag.
1. [Pubblicate i tag](../../help/sites-administering/tags.md#publishing-tags).

Esempio di pacchetto di tag creati per i Tutorials Guida introduttiva  AEM Communities

[Ottieni file](assets/tutorial_tags-v63.zip)

## MongoDB per UGC Common Store {#mongodb-for-ugc-common-store}

Si consiglia, ma facoltativo, di impostare [MSRP](msrp.md) (MongoDB) come [store comune](working-with-srp.md) in modo da provare la flessibilità di moderare tutti gli UGC dagli ambienti di pubblicazione e/o di authoring.

Per istruzioni, visitare [Come impostare MongoDB per Demo](demo-mongo.md).

Per impostazione predefinita, l&#39;installazione delle istanze di creazione e pubblicazione AEM causa la memorizzazione del contenuto generato dall&#39;utente (UGC) in [JCR Tar storage](../../help/sites-deploying/platform.md) a cui si accede utilizzando [JSRP](jsrp.md). JSRP non è uno store comune, il che significa che UGC è visibile solo sull&#39;istanza in cui è stato immesso. In genere, UGC viene immesso in un’istanza di pubblicazione e non sarebbe visibile nell’ambiente di authoring, con la conseguente necessità di utilizzare l’istanza di pubblicazione per tutte le attività di moderazione.