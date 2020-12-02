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


# Configurazione iniziale per abilitazione {#initial-setup-for-enablement}

## Avvio istanze di creazione e pubblicazione {#start-author-and-publish-instances}

A scopo di sviluppo e dimostrazione, sarà necessario eseguire un&#39;istanza di creazione e pubblicazione.

Seguire le istruzioni di base AEM [Guida introduttiva](../../help/sites-deploying/deploy.md#getting-started) che determinano

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
>Se non avete familiarità con AEM, visualizzate la documentazione su [operazioni di base](../../help/sites-authoring/basic-handling.md) e una [guida rapida all&#39;authoring delle pagine](../../help/sites-authoring/qg-page-authoring.md).

## Installazione della versione più recente di Communities {#install-latest-communities-release}

Questa esercitazione crea un [sito community di abilitazione](overview.md#enablement-community). Per verificare che sia installato il pacchetto di funzioni più recente, visita:

* [Ultime versioni](deploy-communities.md#latest-releases)

Per un&#39;esercitazione che crea un sito della community di coinvolgimento [, visitare la [Guida introduttiva  AEM Communities](getting-started.md).](overview.md#engagement-community)

## Configurare le funzioni di abilitazione {#configure-enablement-features}

Per seguire questa esercitazione, è necessario installare correttamente e [configurare l&#39;abilitazione](enablement.md), che richiede prodotti di terze parti, come MySQL e FFmpeg.

## Configura Analytics {#configure-analytics}

Quando [ Adobe Analytics è configurato per il sito della community](analytics.md), sono disponibili ulteriori informazioni nei [report](reports.md) generati sulle risorse di abilitazione e sui percorsi di apprendimento assegnati ai membri della community (utenti in formazione).

## Configura e-mail per notifiche {#configure-email-for-notifications}

La funzione notifiche, disponibile per impostazione predefinita per tutti i siti creati utilizzando la console `Communities Sites`, fornisce un canale e-mail per le notifiche.

Ciò che è necessario è che le e-mail siano configurate correttamente per il sito.

Vedere [Configurazione di Email](email.md).

## Abilitare il servizio Tunnel {#enable-the-tunnel-service}

Quando si crea un sito community nell&#39;ambiente di authoring, il servizio tunnel consente di creare e gestire utenti e gruppi di utenti registrati nell&#39;ambiente di pubblicazione (membri), assegnare ruoli a membri attendibili della community e assegnare contenuti agli utenti in formazione.

Per ulteriori informazioni, vedere [Gestione di utenti e gruppi di utenti](users.md).

Per istruzioni semplici sull&#39;attivazione del servizio tunnel, vedere [Servizio tunnel](deploy-communities.md#tunnel-service-on-author).

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

1. [Impostare le autorizzazioni dei tag](../../help/sites-administering/tags.md#setting-tag-permissions)
1. [Pubblicare i tag](../../help/sites-administering/tags.md#publishing-tags)

Esempio di pacchetto di tag creati per i Tutorials Guida introduttiva  AEM Communities

[Ottieni file](assets/communities_tutorialtags-10.zip)

## Crea membri e gruppi di abilitazione {#create-enablement-members-and-groups}

Per un sito community di abilitazione, i visitatori del sito non devono essere in grado di [registrarsi autonomamente né utilizzare il login mediante social network](sites-console.md#user-management).

Al contrario, con il servizio [tunnel](#enable-the-tunnel-service) abilitato, la [console Membri](members.md) viene utilizzata per registrare nuovi membri nell&#39;ambiente di pubblicazione.

In questa esercitazione, nell’ambiente di pubblicazione vengono creati tre membri. Due membri diventeranno membri di un gruppo di utenti assegnato a un percorso di apprendimento, mentre il terzo membro diventerà un contatto per le risorse di abilitazione.

Un quarto utente viene creato nell’ambiente di authoring e gli viene assegnato il ruolo di Amministratore community e Gestione abilitazione community.

>[!NOTE]
>
>Questi membri vengono creati prima della creazione del sito della community *Enablement Tutorial*.
>
>Se creati successivamente, potrebbero essere aggiunti come membri del gruppo *Membri di Enablement Tutorial* durante la creazione dei membri.
>
>In seguito verranno invece [assegnati al gruppo di membri](enablement-create-site.md#assignuserstocommunityenablemembersgroup).

### Riley Taylor - Iscritti {#riley-taylor-enrollee}

[Create un ](members.md#create-new-member) membro che verrà aggiunto a un gruppo di utenti in formazione, il gruppo Community Ski Class.

* **ID**: riley
* **E-mail**: riley.taylor@mailinator.com
* **Password**: password
* **Conferma password**: password
* **Nome**: Riley
* **Cognome**: Taylor

### Sidney Croft - Iscritti {#sidney-croft-enrollee}

[Create un secondo ](members.md#create-new-member) membro che verrà aggiunto al gruppo Community Ski Class.

* **ID**: sidro
* **E-mail**: sidney.croft@mailinator.com
* **Password**: password
* **Conferma password**: password
* **Nome**: Sidney
* **Cognome**: Croft

### Quinn Harper - Abilitazione contatto risorse e moderatore {#quinn-harper-enablement-resource-contact-and-moderator}

[Create un ](members.md#create-new-member) membro che verrà aggiunto al gruppo di membri del sito community una volta creato il sito. L&#39;iscrizione consentirà al membro di essere assegnato come abilitazione [Contatto risorsa](resources.md#settings) quando viene creata una risorsa di abilitazione per il sito.

* **ID**: quinn
* **E-mail**: quinn.harper@mailinator.com
* **Password**: password
* **Conferma password**: password
* **Nome**: Quinn
* **Cognome**: Harper

### Aggiungere un gruppo di utenti - Community Ski Class {#add-a-user-group-community-ski-class}

[Aggiungete un nuovo ](members.md#create-new-group) gruppo denominato Community Ski Class.

* **ID**: classe sci-comunità
* **Nome**: Classe Ski Community
* **Descrizione**: un gruppo di esempio per assegnare le risorse di abilitazione
* **Aggiungi membri al gruppo**  &#39;add&#39;:

   * riley
   * sidro

* Seleziona **[!UICONTROL Salva]**

### Proprietà delle classi sciistiche della community {#community-ski-class-properties}

![ski-class-properties](assets/ski-class-properties.png)

>[!NOTE]
>
>Durante la creazione del sito, i membri e i gruppi esistenti possono essere aggiunti al gruppo di membri del sito.

## Ruolo amministratore community {#community-administrator-role}

I membri del gruppo Amministratori community possono creare siti community, gestire siti, gestire membri (possono vietare membri della community) e moderare contenuti.

### Crea utente {#create-user}

Create un utente su *author*, al quale viene assegnato il ruolo di Amministratore community:

* Nell’istanza di creazione

   * Ad esempio, [http://localhost:4502/](Http://localhost:4503/)

* Accesso con privilegi di amministratore

   * Ad esempio, nome utente &#39;admin&#39; / password &#39;admin&#39;

* Dalla console principale, passare a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Utenti]**.
* Dal menu **[!UICONTROL Modifica]**, selezionare **[!UICONTROL Aggiungi utente]**.

* Nella finestra di dialogo `Create New User` immettere:

   * **ID&amp;ast;**: sirius
   * **Indirizzo** e-mail: sirius.nilson@mailinator.com
   * **Password&amp;ast;**: password
   * **Conferma password&amp;ast;**: password
   * **Nome**: Sirio
   * **&amp;Ultimo nome;**: Nilson

### Assegna sirius al gruppo di amministratori della community {#assign-sirius-to-community-administrators-group}

Scorri verso il basso fino a `Add User to Groups`:

* Immettere &#39;C&#39; per la ricerca

   * Seleziona `Community Administrators`
   * Seleziona `Community Enablement Managers`

* Seleziona **[!UICONTROL Salva]**

![admin-role](assets/admin-role.png)

