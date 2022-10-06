---
title: Configurazione iniziale
seo-title: Initial Setup
description: Impostazione di Communities
seo-description: Setting up Communities
uuid: c53d280c-c5ae-47cf-8038-f0dea68e15ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 0d462ad1-5619-4bb6-9609-bc8987c40a0c
exl-id: 6bda0f09-7ae5-4540-b035-9dd249ac3186
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 2%

---

# Configurazione iniziale {#initial-setup}

## Avvia istanze di authoring e pubblicazione {#start-author-and-publish-instances}

A scopo di sviluppo e dimostrazione, sarà necessario eseguire un autore e un’istanza di pubblicazione.

Per farlo, segui la AEM di base [Introduzione](../../help/sites-deploying/deploy.md#getting-started) le istruzioni che si tradurranno in:

* Ambiente di authoring in [localhost:4502](Http://localhost:4502/)
* Ambiente di pubblicazione su [localhost:4503](Http://localhost:4503/)

Per AEM Communities,

* L’ambiente di authoring è destinato a:

   * Sviluppo di siti, modelli e componenti.
   * Attività amministrative e di configurazione.

* L’ambiente di pubblicazione è destinato a:

   * L&#39;esperienza comunitaria di pubblicazione e moderazione dei contenuti.
   * Creazione di gruppi di community, membri e gruppi di membri.

>[!NOTE]
>
>Se non hai familiarità con AEM, consulta la documentazione su [trattamento di base](../../help/sites-authoring/basic-handling.md) e [guida rapida all’authoring delle pagine](../../help/sites-authoring/qg-page-authoring.md).

## Installa la versione più recente di Communities {#install-latest-communities-release}

Questa esercitazione crea un [sito community di coinvolgimento](overview.md#engagement-community) e si basa sul feature pack AEM Communities 6.2 versione 1.10.

Per verificare che sia installato il pacchetto di funzionalità più recente, visita:

* [Versioni più recenti](deploy-communities.md#latest-releases)

Per un&#39;esercitazione che crea un [sito della community di abilitazione](overview.md#enablement-community)visita [Guida introduttiva ad AEM Communities per l&#39;abilitazione](getting-started-enablement.md).

## Configura Analytics {#configure-analytics}

Quando [Adobe Analytics è configurato per il sito della community](analytics.md), sono disponibili informazioni sull’attività della community che migliorano l’esperienza del membro della community e forniscono feedback agli amministratori del sito.

L’integrazione con Adobe Analytics è facoltativa.

## Configura e-mail per le notifiche {#configure-email-for-notifications}

La funzione di notifica, disponibile per impostazione predefinita per tutti i siti creati utilizzando `Communities Sites` fornisce un canale e-mail per le notifiche.

Ciò che è necessario è che l’e-mail sia configurata correttamente per il sito.

Vedi [Configurazione e-mail](email.md).

## Attivare il servizio tunnel {#enable-the-tunnel-service}

Quando crei un sito community nell’ambiente di authoring, il servizio tunnel consente di assegnare ruoli a membri della community fidati registrati nell’ambiente di pubblicazione. Il servizio tunnel consente inoltre l&#39;accesso ai membri della comunità [Console Membri e gruppi](members.md) nell’ambiente di authoring.

La convenzione si applica ai membri e ai gruppi di membri creati nell&#39;ambiente di pubblicazione in *not* nell’ambiente di authoring. Per ulteriori informazioni consulta [Gestione di utenti e gruppi di utenti](users.md).

Per istruzioni semplici per attivare il servizio tunnel su un **autore** istanza, vedi [Servizio tunnel](deploy-communities.md#tunnel-service-on-author).

## Ruolo Amministratore community {#community-administrator-role}

I membri del gruppo Amministratori community possono creare siti di community, gestire siti, gestire membri (possono vietare membri della community) e moderare contenuti.

### Crea utente {#create-user}

Crea un utente su *autore*, cui è stato assegnato il ruolo di amministratore comunitario:

* Sull’istanza di authoring

   * Ad esempio: [http://localhost:4502/](Http://localhost:4503/)

* Accesso con privilegi di amministratore

   * Ad esempio, nome utente &#39;admin&#39; / password &#39;admin&#39;

* Dalla console principale, passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Utenti]**.
* Da **Modifica** menu, seleziona **[!UICONTROL Aggiungi utente]**

* In `Create New User` finestra di dialogo immetti:

   * **[!UICONTROL ID]**: siriano
   * **[!UICONTROL Indirizzo e-mail]**: sirius.nilson@mailinator.com
   * **[!UICONTROL Password]**: password
   * **[!UICONTROL &amp;Conferma password;]**: password
   * **[!UICONTROL Nome]**: Sirio
   * **[!UICONTROL Cognome]**: Nilson

### Assegna Sirius al gruppo di amministratori della community {#assign-sirius-to-community-administrators-group}

Scorri verso il basso fino a `Add User to Groups`:

* Inserisci &quot;C&quot; per cercare

   * Seleziona `Community Administrators`
   * Seleziona `Community Enablement Managers`

* Seleziona **[!UICONTROL Salva]**.

![create-user](assets/create-user.png)

## Abilita accesso social {#enable-social-login}

Prima di poter utilizzare le versioni dimostrative di accesso social con Facebook e Twitter, è necessario

1. Installa un fix pack o [pacchetto di funzionalità più recente](deploy-communities.md#latestfeaturepack) (per le modifiche dell’API Facebook di marzo 2017).
1. [Abilitare il provider OAuth](social-login.md#adobe-granite-oauth-authentication-handler) nell’ambiente di pubblicazione.

Per i server di produzione, è necessario creare i servizi cloud necessari per fornire l’accesso social.

Vedi [Accesso social con Facebook e Twitter](social-login.md).

## Creare tag tutorial {#create-tutorial-tags}

Crea tag da utilizzare per le esercitazioni di coinvolgimento e abilitazione, utilizzando lo spazio dei nomi tag di `Tutorial`.

Utilizza la [Console di assegnazione tag](../../help/sites-administering/tags.md#tagging-console) per creare i seguenti tag:

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![tutorial-tags](assets/tutorial-tags.png)

Quindi segui le istruzioni per:

1. [Impostare le autorizzazioni del tag](../../help/sites-administering/tags.md#setting-tag-permissions).
1. [Pubblicare i tag](../../help/sites-administering/tags.md#publishing-tags).

Pacchetto di esempio di tag creati per i Tutorials Guida introduttiva di AEM Communities

[Ottieni file](assets/tutorial_tags-v63.zip)

## MongoDB per archivio comune UGC {#mongodb-for-ugc-common-store}

Si consiglia, ma facoltativo, di impostare [MSRP](msrp.md) (MongoDB) come [negozio comune](working-with-srp.md) per provare la flessibilità di moderare tutti gli UGC dagli ambienti di pubblicazione e/o di authoring.

Per istruzioni, visita [Come impostare MongoDB per la demo](demo-mongo.md).

Per impostazione predefinita, l’installazione delle istanze di authoring e pubblicazione AEM fa sì che il contenuto generato dall’utente (UGC) sia memorizzato in [Archiviazione JCR Tar](../../help/sites-deploying/platform.md) accessibile tramite [JSRP](jsrp.md). JSRP non è un archivio comune, il che significa che UGC è visibile solo sull&#39;istanza in cui è stato inserito. In genere, UGC viene inserito in un&#39;istanza di pubblicazione e non sarebbe visibile nell&#39;ambiente di authoring, dando luogo a tutte le attività di moderazione che devono utilizzare l&#39;istanza di pubblicazione.
