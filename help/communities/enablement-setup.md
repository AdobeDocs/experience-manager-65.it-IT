---
title: Configurazione iniziale per l'abilitazione
seo-title: Configurazione iniziale
description: Configurazione iniziale per l'abilitazione
seo-description: Configurazione iniziale per l'abilitazione
uuid: 873ec41d-c088-41d9-a535-de5300661de6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: f2ac3d66-cc79-498f-83fb-dd96feb88de2
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 1%

---


# Configurazione iniziale per l&#39;abilitazione  {#initial-setup-for-enablement}

## Avvio istanze di creazione e pubblicazione {#start-author-and-publish-instances}

A scopo di sviluppo e dimostrazione, sarà necessario eseguire un&#39;istanza di creazione e pubblicazione.

Seguite le istruzioni di base AEM [Guida introduttiva](../../help/sites-deploying/deploy.md#getting-started) per ottenere

* Ambiente di authoring su [localhost:4502](Http://localhost:4502/)
* Ambiente di pubblicazione su [localhost:4503](Http://localhost:4503/)

Per  AEM Communities,

* L’ambiente di authoring è destinato a:

   * Sviluppo di siti, modelli, componenti, risorse di abilitazione e percorsi di apprendimento.
   * Assegnazione di membri e gruppi di membri per abilitare risorse e percorsi di apprendimento.
   * Generazione di rapporti su assegnazioni, viste e post.
   * Attività amministrative e di configurazione.

* L’ambiente di pubblicazione è destinato a:

   * Formazione/formazione basata su argomenti gestiti da Enablement Manager.
   * Creazione di commenti e valutazioni per risorse di abilitazione e percorsi di apprendimento.
   * Contatta i contatti delle risorse.

>[!NOTE]
>
>Se non avete familiarità con AEM, consultate la documentazione sulla gestione [](../../help/sites-authoring/basic-handling.md) di base e una guida [rapida alle pagine](../../help/sites-authoring/qg-page-authoring.md)di authoring.

## Installa ultima versione di Communities {#install-latest-communities-release}

Questa esercitazione crea un sito community di [abilitazione](overview.md#enablement-community). Per verificare che sia installato il pacchetto di funzioni più recente, visita:

* [Ultime versioni](deploy-communities.md#latest-releases)

Per un&#39;esercitazione che crea un sito [per la community di](overview.md#engagement-community)coinvolgimento, visita la [Guida introduttiva ad  AEM Communities](getting-started.md).

## Configurare le funzioni di abilitazione {#configure-enablement-features}

Per seguire questa esercitazione, è necessario installare e [configurare correttamente l&#39;abilitazione](enablement.md), che richiede prodotti di terze parti, come MySQL e FFmpeg.

## Configura Analytics {#configure-analytics}

Quando [Adobe Analytics è configurato per il sito](analytics.md)community, sono disponibili ulteriori informazioni nei [rapporti](reports.md) generati sulle risorse di abilitazione e sui percorsi di apprendimento assegnati ai membri della community (utenti in formazione).

## Configura e-mail per notifiche {#configure-email-for-notifications}

La funzione notifiche, disponibile per impostazione predefinita per tutti i siti creati utilizzando la `Communities Sites` console, fornisce un canale e-mail per le notifiche.

Ciò che è necessario è che le e-mail siano configurate correttamente per il sito.

See [Configuring Email](email.md).

## Abilitare il servizio Tunnel {#enable-the-tunnel-service}

Quando si crea un sito community nell&#39;ambiente di authoring, il servizio tunnel consente di creare e gestire utenti e gruppi di utenti registrati nell&#39;ambiente di pubblicazione (membri), assegnare ruoli a membri attendibili della community e assegnare contenuti agli utenti in formazione.

Per ulteriori informazioni, consulta [Gestione di utenti e gruppi](users.md)di utenti.

Per istruzioni semplici sull&#39;attivazione del servizio tunnel, vedere Servizio [](deploy-communities.md#tunnel-service-on-author)tunnel.

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

1. [Impostare le autorizzazioni dei tag](../../help/sites-administering/tags.md#setting-tag-permissions)
1. [Pubblicare i tag](../../help/sites-administering/tags.md#publishing-tags)

Esempio di pacchetto di tag creati per i Tutorials Guida introduttiva  AEM Communities

[Ottieni file](assets/communities_tutorialtags-10.zip)

## Creazione di membri e gruppi di abilitazione {#create-enablement-members-and-groups}

Per un sito di abilitazione per community, i visitatori del sito non devono poter registrarsi [autonomamente né utilizzare il login](sites-console.md#user-management)per social network.

Con il servizio [](#enable-the-tunnel-service) tunnel attivato, la console [](members.md) Membri viene utilizzata per registrare nuovi membri nell’ambiente di pubblicazione.

In questa esercitazione, nell’ambiente di pubblicazione vengono creati tre membri. Due membri diventeranno membri di un gruppo di utenti assegnato a un percorso di apprendimento, mentre il terzo membro diventerà un contatto per le risorse di abilitazione.

Un quarto utente viene creato nell’ambiente di authoring e gli viene assegnato il ruolo di Amministratore community e Gestione abilitazione community.

>[!NOTE]
>
>Questi membri vengono creati prima della creazione del sito della community *Enablement Tutorial* .
>
>Se creati successivamente, possono essere aggiunti come membri del gruppo *di membri* Enablement Tutorial durante la creazione di un membro.
>
>In seguito verranno invece [assegnati al gruppo](enablement-create-site.md#assignuserstocommunityenablemembersgroup)di membri.

### Riley Taylor - Iscritto {#riley-taylor-enrollee}

[Create un membro](members.md#create-new-member) che verrà aggiunto a un gruppo di utenti in formazione, il gruppo Community Ski Class.

* **ID**: riley
* **E-mail**: riley.taylor@mailinator.com
* **Password**: password
* **Conferma password**: password
* **Nome**: Riley
* **Cognome**: Taylor

### Sidney Croft - Iscritti {#sidney-croft-enrollee}

[Crea un secondo membro](members.md#create-new-member) che verrà aggiunto al gruppo Community Ski Class.

* **ID**: sidro
* **E-mail**: sidney.croft@mailinator.com
* **Password**: password
* **Conferma password**: password
* **Nome**: Sidney
* **Cognome**: Croft

### Quinn Harper - Abilitazione contatto risorse e moderatore {#quinn-harper-enablement-resource-contact-and-moderator}

[Create un membro](members.md#create-new-member) che verrà aggiunto al gruppo di membri del sito community una volta creato il sito. L&#39;iscrizione consentirà al membro di essere assegnato come contatto [delle](resources.md#settings) risorse per l&#39;abilitazione quando viene creata una risorsa per l&#39;abilitazione per il sito.

* **ID**: quinn
* **E-mail**: quinn.harper@mailinator.com
* **Password**: password
* **Conferma password**: password
* **Nome**: Quinn
* **Cognome**: Harper

### Aggiungere un gruppo di utenti - Community Ski Class {#add-a-user-group-community-ski-class}

[Aggiungete un nuovo gruppo](members.md#create-new-group) denominato Community Ski Class.

* **ID**: classe sci-comunità
* **Nome**: Classe Ski Community
* **Descrizione**: un gruppo di esempio per assegnare le risorse di abilitazione
* **Aggiungi membri al gruppo** &#39;aggiungi&#39;:

   * riley
   * sidro

* Seleziona **[!UICONTROL Salva]**

### Proprietà della classe Ski Community {#community-ski-class-properties}

![ski-class-properties](assets/ski-class-properties.png)

>[!NOTE]
>
>Durante la creazione del sito, i membri e i gruppi esistenti possono essere aggiunti al gruppo di membri del sito.

## Ruolo amministratore community {#community-administrator-role}

I membri del gruppo Amministratori community possono creare siti community, gestire siti, gestire membri (possono vietare membri della community) e moderare contenuti.

### Crea utente {#create-user}

Create un utente all’ *autore*, al quale verrà assegnato il ruolo di Amministratore community:

* Nell’istanza di creazione

   * Ad esempio, [http://localhost:4502/](Http://localhost:4503/)

* Accesso con privilegi di amministratore

   * Ad esempio, nome utente &#39;admin&#39; / password &#39;admin&#39;

* Dalla console principale, accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Protezione]** > **[!UICONTROL Utenti]**.
* Dal menu **[!UICONTROL Modifica]** , selezionate **[!UICONTROL Aggiungi utente]**.

* Nella `Create New User` finestra di dialogo immetti:

   * **ID&amp;ast;**: sirius
   * **Indirizzo** e-mail: sirius.nilson@mailinator.com
   * **Password&amp;ast;**: password
   * **Conferma password&amp;ast;**: password
   * **Nome**: Sirio
   * **Cognome&amp;ast;**: Nilson

### Assegna Sirius al gruppo Amministratori community {#assign-sirius-to-community-administrators-group}

Scorri verso il basso fino a `Add User to Groups`:

* Immettere &#39;C&#39; per la ricerca

   * Seleziona `Community Administrators`
   * Seleziona `Community Enablement Managers`

* Seleziona **[!UICONTROL Salva]**

![admin-role](assets/admin-role.png)

