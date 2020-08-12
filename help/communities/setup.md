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
source-git-commit: 6ab91667ad668abf80ccf1710966169b3a187928
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 2%

---


# Configurazione iniziale {#initial-setup}

## Avvio istanze di creazione e pubblicazione {#start-author-and-publish-instances}

A scopo di sviluppo e dimostrazione, sarà necessario eseguire un’istanza di creazione e pubblicazione.

A tal fine, segui le istruzioni di base AEM [Guida introduttiva](../../help/sites-deploying/deploy.md#getting-started) , che si tradurranno in:

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
>Se non avete familiarità con AEM, consultate la documentazione sulla gestione [](../../help/sites-authoring/basic-handling.md) di base e una guida [rapida alle pagine](../../help/sites-authoring/qg-page-authoring.md)di authoring.


## Installa ultima versione di Communities {#install-latest-communities-release}

Questa esercitazione crea un sito [community di](overview.md#engagement-community) coinvolgimento e si basa  feature pack AEM Communities 6.2 versione 1.10.

Per verificare che sia installato il pacchetto di funzioni più recente, visita:

* [Ultime versioni](deploy-communities.md#latest-releases)

Per un&#39;esercitazione che crea un sito [per](overview.md#enablement-community)la community di abilitazione, visitate la [Guida introduttiva ad  AEM Communities per l&#39;abilitazione](getting-started-enablement.md).

## Configura Analytics {#configure-analytics}

Quando [Adobe Analytics è configurato per il sito](analytics.md)community, sono disponibili informazioni sull&#39;attività della community che migliorano l&#39;esperienza del membro della community e forniscono feedback agli amministratori del sito.

L&#39;integrazione con  Adobe Analytics è facoltativa.

## Configura e-mail per notifiche {#configure-email-for-notifications}

La funzione notifiche, disponibile per impostazione predefinita per tutti i siti creati utilizzando la `Communities Sites` console, fornisce un canale e-mail per le notifiche.

Ciò che è necessario è che le e-mail siano configurate correttamente per il sito.

See [Configuring Email](email.md).

## Abilitare il servizio Tunnel {#enable-the-tunnel-service}

Quando si crea un sito community nell&#39;ambiente di authoring, il servizio tunnel consente di assegnare ruoli a membri attendibili della community registrati nell&#39;ambiente di pubblicazione. Il servizio tunnel consente inoltre l&#39;accesso ai membri della community dalle console [Membri e Gruppi](members.md) nell&#39;ambiente di authoring.

La convenzione prevede che i membri e i gruppi di membri creati nell’ambiente di pubblicazione *non* vengano ricreati nell’ambiente di authoring. Per ulteriori informazioni, consulta [Gestione di utenti e gruppi](users.md)di utenti.

Per istruzioni semplici sull’attivazione del servizio tunnel in un’istanza di **authoring** , consultate Servizio [](deploy-communities.md#tunnel-service-on-author)tunnel.

## Ruolo amministratore community {#community-administrator-role}

I membri del gruppo Amministratori community possono creare siti community, gestire siti, gestire membri (possono vietare membri della community) e moderare contenuti.

### Crea utente {#create-user}

Create un utente all’ *autore*, al quale verrà assegnato il ruolo di Amministratore community:

* Nell’istanza di creazione

   * Ad esempio, [http://localhost:4502/](Http://localhost:4503/)

* Accesso con privilegi di amministratore

   * Ad esempio, nome utente &#39;admin&#39; / password &#39;admin&#39;

* Dalla console principale, accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Protezione]** > **[!UICONTROL Utenti]**.
* Dal menu **Modifica **, selezionate**[!UICONTROL Aggiungi utente ]**

* Nella `Create New User` finestra di dialogo immetti:

   * **[!UICONTROL ID]**: sirius
   * **[!UICONTROL Indirizzo]** e-mail: sirius.nilson@mailinator.com
   * **[!UICONTROL Password]**: password
   * **[!UICONTROL Conferma password&amp;ast;]**: password
   * **[!UICONTROL Nome]**: Sirio
   * **[!UICONTROL Cognome]**: Nilson

### Assegna Sirius al gruppo Amministratori community {#assign-sirius-to-community-administrators-group}

Scorri verso il basso fino a `Add User to Groups`:

* Immettere &#39;C&#39; per la ricerca

   * Seleziona `Community Administrators`
   * Seleziona `Community Enablement Managers`

* Seleziona **[!UICONTROL Salva]**.

![create-user](assets/create-user.png)

## Abilita login per social network {#enable-social-login}

Prima che possano essere utilizzate le versioni dimostrative di accesso social con Facebook e Twitter, è necessario

1. Installate un fix pack o l&#39; [ultimo feature pack](deploy-communities.md#latestfeaturepack) (per le modifiche dell&#39;API Facebook di marzo 2017).
1. [Abilitate il provider](social-login.md#adobe-granite-oauth-authentication-handler) OAuth nell&#39;ambiente di pubblicazione.

Per i server di produzione, è necessario creare i servizi cloud necessari per fornire il login mediante profilo sociale.

Consultate Accesso [social network con Facebook e Twitter](social-login.md).

## Creare tag di esercitazione {#create-tutorial-tags}

Create i tag da utilizzare per le esercitazioni di coinvolgimento e abilitazione, utilizzando lo spazio dei nomi tag di `Tutorial`.

Utilizzate la console [](../../help/sites-administering/tags.md#tagging-console) Assegnazione tag per creare i seguenti tag:

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![tutorial-tags](assets/tutorial-tags.png)

Seguite quindi le istruzioni per:

1. [Impostate le autorizzazioni](../../help/sites-administering/tags.md#setting-tag-permissions)del tag.
1. [Pubblicate i tag](../../help/sites-administering/tags.md#publishing-tags).

Esempio di pacchetto di tag creati per i Tutorials Guida introduttiva  AEM Communities

[Ottieni file](assets/tutorial_tags-v63.zip)

## MongoDB per archivio comune UGC {#mongodb-for-ugc-common-store}

Si consiglia, ma facoltativo, di impostare [MSRP](msrp.md) (MongoDB) come archivio [](working-with-srp.md) comune per provare la flessibilità di moderare tutti gli UGC dagli ambienti di pubblicazione e/o di authoring.

Per istruzioni, visitare [How to Setup MongoDB for Demo](demo-mongo.md).

Per impostazione predefinita, l’installazione delle istanze di creazione e pubblicazione AEM causa la memorizzazione del contenuto generato dall’utente (UGC) nell’archivio [](../../help/sites-deploying/platform.md) JCR Tar a cui si accede tramite [JSRP](jsrp.md). JSRP non è uno store comune, il che significa che UGC è visibile solo sull&#39;istanza in cui è stato immesso. In genere, UGC viene immesso in un’istanza di pubblicazione e non sarebbe visibile nell’ambiente di authoring, con la conseguente necessità di utilizzare l’istanza di pubblicazione per tutte le attività di moderazione.