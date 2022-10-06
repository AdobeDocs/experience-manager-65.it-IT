---
title: Configurazione iniziale per l'abilitazione
seo-title: Initial Setup
description: Configurazione iniziale per l'abilitazione
seo-description: Initial Setup for Enablement
uuid: 873ec41d-c088-41d9-a535-de5300661de6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: f2ac3d66-cc79-498f-83fb-dd96feb88de2
exl-id: ed494922-3e15-4778-84c1-35c8846ce980
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 2%

---

# Configurazione iniziale per l&#39;abilitazione  {#initial-setup-for-enablement}

## Avvia istanze di authoring e pubblicazione {#start-author-and-publish-instances}

A scopo di sviluppo e dimostrazione, sarà necessario eseguire un autore e un’istanza di pubblicazione.

Seguire le AEM di base [Introduzione](../../help/sites-deploying/deploy.md#getting-started) istruzioni che

* Ambiente di authoring in [localhost:4502](Http://localhost:4502/)
* Ambiente di pubblicazione su [localhost:4503](Http://localhost:4503/)

Per AEM Communities,

* L’ambiente di authoring è destinato a:

   * Sviluppo di siti, modelli, componenti, risorse di abilitazione e percorsi di apprendimento.
   * Assegnazione di membri e gruppi di membri per abilitare risorse e percorsi di apprendimento.
   * Generazione di rapporti su assegnazioni, viste e post.
   * Attività amministrative e di configurazione.

* L’ambiente di pubblicazione è destinato a:

   * Formazione/formazione basata su argomenti gestiti da Enablement Manager.
   * Creazione di commenti e valutazioni di risorse di abilitazione e percorsi di apprendimento.
   * Contatta i contatti delle risorse.

>[!NOTE]
>
>Se non hai familiarità con AEM, consulta la documentazione su [trattamento di base](../../help/sites-authoring/basic-handling.md) e [guida rapida all’authoring delle pagine](../../help/sites-authoring/qg-page-authoring.md).

## Installa la versione più recente di Communities {#install-latest-communities-release}

Questa esercitazione crea un [sito della community di abilitazione](overview.md#enablement-community). Per verificare che sia installato il pacchetto di funzionalità più recente, visita:

* [Versioni più recenti](deploy-communities.md#latest-releases)

Per un&#39;esercitazione che crea un [sito community di coinvolgimento](overview.md#engagement-community)visita [Guida introduttiva ad AEM Communities](getting-started.md).

## Configurare le funzionalità di abilitazione {#configure-enablement-features}

Per seguire questa esercitazione, è necessario installare correttamente e [configurare l&#39;abilitazione](enablement.md), che richiede prodotti di terze parti, come MySQL e FFmpeg.

## Configura Analytics {#configure-analytics}

Quando [Adobe Analytics è configurato per il sito della community](analytics.md), ulteriori informazioni sono disponibili nella sezione [rapporti](reports.md) generati su risorse di abilitazione e percorsi di apprendimento assegnati ai membri della community (studenti).

## Configura e-mail per le notifiche {#configure-email-for-notifications}

La funzione di notifica, disponibile per impostazione predefinita per tutti i siti creati utilizzando `Communities Sites` fornisce un canale e-mail per le notifiche.

Ciò che è necessario è che l’e-mail sia configurata correttamente per il sito.

Vedi [Configurazione e-mail](email.md).

## Attivare il servizio tunnel {#enable-the-tunnel-service}

Durante la creazione di un sito community nell’ambiente di authoring, il servizio tunnel consente di creare e gestire utenti e gruppi di utenti registrati nell’ambiente di pubblicazione (membri), assegnare ruoli ai membri affidabili della community e assegnare contenuti agli studenti.

Per ulteriori informazioni consulta [Gestione di utenti e gruppi di utenti](users.md).

Per istruzioni semplici sull&#39;attivazione del servizio tunnel, vedi [Servizio tunnel](deploy-communities.md#tunnel-service-on-author).

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

1. [Impostare le autorizzazioni del tag](../../help/sites-administering/tags.md#setting-tag-permissions)
1. [Pubblicare i tag](../../help/sites-administering/tags.md#publishing-tags)

Pacchetto di esempio di tag creati per i Tutorials Guida introduttiva di AEM Communities

[Ottieni file](assets/communities_tutorialtags-10.zip)

## Creare membri e gruppi di abilitazione {#create-enablement-members-and-groups}

Per un sito della community di abilitazione, i visitatori del sito non devono essere in grado di [registrazione automatica e accesso social](sites-console.md#user-management).

Invece, con la [servizio tunnel](#enable-the-tunnel-service) abilitato [Console dei membri](members.md) viene utilizzato per registrare nuovi membri nell’ambiente di pubblicazione.

In questa esercitazione vengono creati tre membri nell’ambiente di pubblicazione. Due membri diventeranno membri di un gruppo di utenti assegnato a un percorso di apprendimento, mentre il terzo membro diventerà un contatto di risorse di abilitazione.

Un quarto utente viene creato nell’ambiente di authoring e assegnato i ruoli di Amministratore community e Gestore abilitazione community.

>[!NOTE]
>
>Questi membri vengono creati prima della creazione del *Tutorial sull’abilitazione* sito della community.
>
>Se sono stati creati successivamente, possono essere aggiunti come membri del *Gruppo di membri tutorial di abilitazione* durante la creazione del membro.
>
>Invece, più tardi, saranno [assegnato al gruppo di membri](enablement-create-site.md#assignuserstocommunityenablemembersgroup).

### Riley Taylor - Iscriviti {#riley-taylor-enrollee}

[Crea un membro](members.md#create-new-member) che verrà aggiunto a un gruppo di studenti - il gruppo Community Ski Class.

* **ID**: riley
* **E-mail**: riley.taylor@mailinator.com
* **Password**: password
* **Conferma password**: password
* **Nome**: Riley
* **Cognome**: Taylor

### Sidney Croft - Iscrizione {#sidney-croft-enrollee}

[Crea un secondo membro](members.md#create-new-member) che saranno aggiunti al gruppo Community Ski Class.

* **ID**: sidro
* **E-mail**: sidney.croft@mailinator.com
* **Password**: password
* **Conferma password**: password
* **Nome**: Sidney
* **Cognome**: Croft

### Quinn Harper - Contatto risorse di abilitazione e moderatore {#quinn-harper-enablement-resource-contact-and-moderator}

[Crea un membro](members.md#create-new-member) che verranno aggiunti al gruppo membro del sito della community una volta creato il sito. Questa appartenenza consentirà al membro di essere assegnato come abilitazione [Contatto risorsa](resources.md#settings) quando viene creata una risorsa di abilitazione per il sito.

* **ID**: ciuffo
* **E-mail**: quinn.harper@mailinator.com
* **Password**: password
* **Conferma password**: password
* **Nome**: Quinn
* **Cognome**: Harper

### Aggiungi un gruppo di utenti - Community Ski Class {#add-a-user-group-community-ski-class}

[Aggiungi un nuovo gruppo](members.md#create-new-group) Classe sciistica comunitaria.

* **ID**: classe sciistica
* **Nome**: Classe sciistica comunitaria
* **Descrizione**: un gruppo di esempio per l’assegnazione di risorse di abilitazione
* **Aggiungi membri al gruppo** &#39;add&#39;:

   * riley
   * sidro

* Seleziona **[!UICONTROL Salva]**

### Proprietà delle classi di sci della community {#community-ski-class-properties}

![ski-class-properties](assets/ski-class-properties.png)

>[!NOTE]
>
>Durante la creazione del sito, i membri e i gruppi esistenti possono essere aggiunti al gruppo di membri del sito community.

## Ruolo Amministratore community {#community-administrator-role}

I membri del gruppo Amministratori community possono creare siti di community, gestire siti, gestire membri (possono vietare membri della community) e moderare contenuti.

### Crea utente {#create-user}

Crea un utente su *autore*, cui è stato assegnato il ruolo di amministratore comunitario:

* Sull’istanza di authoring

   * Ad esempio: [http://localhost:4502/](Http://localhost:4503/)

* Accesso con privilegi di amministratore

   * Ad esempio, nome utente &#39;admin&#39; / password &#39;admin&#39;

* Dalla console principale, passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Utenti]**.
* Da **[!UICONTROL Modifica]** menu, seleziona **[!UICONTROL Aggiungi utente]**.

* In `Create New User` finestra di dialogo immetti:

   * **ID&amp;ast;**: siriano
   * **Indirizzo e-mail**: sirius.nilson@mailinator.com
   * **Password&amp;ast;**: password
   * **&amp;Conferma password;**: password
   * **Nome**: Sirio
   * **Cognome&amp;sto;**: Nilson

### Assegna Sirius al gruppo di amministratori della community {#assign-sirius-to-community-administrators-group}

Scorri verso il basso fino a `Add User to Groups`:

* Inserisci &quot;C&quot; per cercare

   * Seleziona `Community Administrators`
   * Seleziona `Community Enablement Managers`

* Seleziona **[!UICONTROL Salva]**

![admin-role](assets/admin-role.png)
