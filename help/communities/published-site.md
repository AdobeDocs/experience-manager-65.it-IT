---
title: Scopri il sito pubblicato
seo-title: Scopri il sito pubblicato
description: Passare a un sito pubblicato
seo-description: Passare a un sito pubblicato
uuid: 44594e9e-27ad-475d-953d-3611b04f0df8
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: dd0cbc05-a361-46bc-b9f1-d045f8f23890
docset: aem65
translation-type: tm+mt
source-git-commit: bd9abe033216a00b93b2098e12b100ad478a8d08
workflow-type: tm+mt
source-wordcount: '1202'
ht-degree: 1%

---


# Scopri il sito pubblicato {#experience-the-published-site}

## Passa a nuovo sito in Pubblica {#browse-to-new-site-on-publish}

Ora che il sito community appena creato è stato pubblicato, individuate l’URL visualizzato al momento della creazione del sito, ma sul server di pubblicazione, ad esempio:

* URL autore = https://localhost:4502/content/sites/engage/en.html
* URL pubblicazione = https://localhost:4503/content/sites/engage/en.html

Per ridurre la confusione relativa al membro che ha effettuato l’accesso in fase di creazione e pubblicazione, si consiglia di utilizzare browser diversi per ogni istanza.

Al primo arrivo sul sito pubblicato, il visitatore del sito in genere non avrebbe già effettuato l’accesso e sarebbe anonimo.

`https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}`

![chlimage_1-31](assets/chlimage_1-31.png)

## Visitatore del sito anonimo {#anonymous-site-visitor}

Un visitatore anonimo del sito vede quanto segue nell’interfaccia utente:

* Titolo del sito (Esercitazione introduttiva)
* Nessun collegamento profilo
* Nessun collegamento messaggi
* Nessun collegamento di notifica
* Campo di ricerca
* Collegamento di accesso
* Il banner del marchio
* Collegamenti ai menu per i componenti inclusi nel Modello del sito di riferimento.

Se selezionate vari collegamenti, questi saranno in modalità di sola lettura.

### Impedire l&#39;accesso anonimo su JCR {#prevent-anonymous-access-on-jcr}

Un limite noto espone il contenuto del sito della community ai visitatori anonimi attraverso contenuti jcr e json, anche se **consente l&#39;accesso** anonimo è disabilitato per il contenuto del sito. Tuttavia, questo comportamento può essere controllato utilizzando Limitazioni Sling come soluzione alternativa.

Per proteggere i contenuti del sito della community dall&#39;accesso di utenti anonimi tramite contenuti jcr e json, procedi come segue:

1. Nell’istanza AEM Author, andate a https:// hostname:port/editor.html/content/site/sitename.html.

   >[!NOTE]
   >
   >Non andate al sito localizzato.

1. Vai a Proprietà **** pagina.

   ![page-properties](assets/page-properties.png)

1. Vai alla scheda **Avanzate** .

1. Enable **Authentication Requirement**.

   ![autenticazione del sito](assets/site-authentication.png)

1. Aggiungete il percorso della pagina di login. Ad esempio, **/content/......./GetStarted**.
1. Pubblicate la pagina.

## Membro della comunità di fiducia {#trusted-community-member}

Questa esperienza presuppone che [ad Aaron McDonald](/help/communities/tutorials.md#demo-users) siano stati assegnati i ruoli di manager e moderatore [della](/help/communities/create-site.md#roles)comunità. In caso contrario, tornate nell&#39;ambiente di authoring per [modificare le impostazioni](/help/communities/sites-console.md#modifying-site-properties) del sito e selezionate Aaron McDonald come responsabile della community e moderatore.

Nell&#39;angolo superiore destro, selezionate `Log in`e firmate con nome utente (aaron.mcdonald@mailinator.com) e password (password). Notate la possibilità di accedere con le credenziali di Twitter o Facebook.

![chlimage_1-32](assets/chlimage_1-32.png)

Una volta effettuato l&#39;accesso come membro della community registrato, potete vedere le seguenti voci di menu su cui fare clic ed esplorare il sito della community:

* **L’opzione Profilo** consente di visualizzare e modificare il profilo.
* [L’opzione Messaggi](/help/communities/configure-messaging.md) consente di accedere alla sezione dei messaggi diretti, in cui è possibile:

   1. Visualizzare i messaggi diretti ricevuti (Posta in arrivo), inviati (Elementi inviati) ed eliminati (Cestino).
   1. Comporre nuovi messaggi diretti da inviare a singoli e gruppi.

* [L&#39;opzione Notifiche](/help/communities/notifications.md) consente di accedere alla sezione delle notifiche, in cui è possibile visualizzare gli eventi di interesse e modificare le impostazioni delle notifiche.
* [Se disponete di privilegi di moderazione, Amministrazione](/help/communities/published-site.md#moderationlink) vi indirizza alla pagina Moderazione AEM Communities.

![chlimage_1-33](assets/chlimage_1-33.png)

Notate che la pagina Calendario è la home page perché il modello di sito di riferimento scelto includeva prima la funzione Calendario, seguita dalla funzione Flusso di attività, dalla funzione Forum e così via. Questa struttura è visibile dalla console Modello [](/help/communities/sites.md#edit-site-template) sito o quando si modificano le proprietà del sito nell’ambiente di authoring:

![chlimage_1-34](assets/chlimage_1-34.png)

>[!NOTE]
>
>Per ulteriori informazioni sui componenti e sulle funzioni di Community, visita:
>
>* [Componenti](/help/communities/author-communities.md) Community (per autori)
>* [Componenti, funzioni e funzionalità Essentials](/help/communities/essentials.md) (per sviluppatori)

>



### Collegamento forum {#forum-link}

Per visualizzare la funzione forum di base, fate clic sul collegamento Forum.

I membri possono pubblicare un nuovo argomento o seguire un argomento.

I visitatori del sito possono visualizzare i post e ordinarli in vari modi.

![chlimage_1-35](assets/chlimage_1-35.png)

### Collegamento gruppi {#groups-link}

Poiché Aaron è un amministratore di gruppo, selezionando il collegamento Gruppi, Aaron potrà creare un nuovo gruppo di community selezionando un modello di gruppo, un’immagine, un gruppo aperto o segreto e i membri invitati.

Questo è un esempio in cui viene creato un gruppo nell’ambiente di pubblicazione.

I gruppi possono essere creati anche nell’ambiente di authoring e gestiti all’interno del sito della community nell’ambiente di authoring (console[Gruppi](/help/communities/groups.md)community). Questa esercitazione illustra come [creare gruppi in fase di creazione](/help/communities/nested-groups.md) .

![classic-ui](assets/classic-ui.png)

Crea un gruppo di riferimento:

1. Seleziona **nuovo gruppo**
1. **scheda Impostazioni**

   * Nome gruppo : `Sports`
   * Descrizione : `A parent group for various sporting groups`.
   * Nome URL del gruppo : `sports`
   * Selezione `Open Group` (consentire a qualsiasi membro della community di partecipare partecipando)

1. **Scheda Modello**

   * Seleziona `Reference Group` (contiene una funzione di gruppi nella sua struttura per consentire i gruppi nidificati)

1. Seleziona **Crea gruppo**

![classic-ui-website](assets/classic-ui-website.png)

Dopo aver creato un nuovo gruppo, **selezionate il nuovo gruppo** Sport per creare due gruppi (nidificati) al suo interno. Poiché una struttura del sito non può iniziare con la funzione dei gruppi, dopo aver aperto il gruppo Sport, è necessario selezionare il collegamento Gruppi:

![classic-ui-create-page](assets/classic-ui-create-page.png)

Il secondo gruppo di collegamenti, a partire da `Blog`, appartiene al gruppo attualmente selezionato, il `Sports` gruppo. Selezionando il collegamento Sport&#39; `Groups` , è possibile nidificare due gruppi all&#39;interno del gruppo Sport.

Ad esempio, aggiungetene due `new groups`.

* Uno con nome `Baseball`

   * Lasciatelo impostato come `Open Group` (iscrizione obbligatoria).
   * Nella scheda Modelli, selezionare `Conversational Group`.

* Uno con nome `Gymnastics`

   * Modificatene l&#39;impostazione in `Member Only Group` (iscrizione limitata).
   * Nella scheda Modelli, selezionare `Conversational Group`.

**Avviso**:

* Prima di visualizzare entrambi i gruppi potrebbe essere necessario aggiornare la pagina.
* Questo modello *non* include la funzione dei gruppi, pertanto non sarà possibile effettuare ulteriori nidificazioni dei gruppi.
* Per l’autore, la console [](/help/communities/groups.md) Gruppi offre una terza scelta, un’iscrizione `Public Group` (facoltativa).

Una volta creati entrambi i gruppi, selezionate il gruppo Baseball, un gruppo aperto e notate i relativi collegamenti:

`Discussions` `What's New` `Members`

I collegamenti del gruppo sono visualizzati sotto i collegamenti del sito principale e i risultati sono la seguente visualizzazione:

![classic-ui-website-page](assets/classic-ui-website-page.png)

Per l’autore, con privilegi amministrativi, andate alla console [Gruppi di](/help/communities/members.md) Communities e aggiungete Weston McCall al `Community Engage Gymnastics <uid> Members` gruppo.

Continuando a pubblicare, disconnettetevi come Aaron McDonald e visualizzate i gruppi nel Gruppo sportivo come visitatore anonimo del sito:

* Dalla home page
* Select `Groups` link
* Select `Sports` link
* Selezionate il collegamento Sport&#39; `Groups`

Solo il gruppo di baseball sarà visibile.

Effettuate l&#39;accesso come Weston McCall (weston.mccall@dodgit.com / password) e andate alla stessa posizione. Notate che Weston è in grado di aprire `Join` il `Baseball` gruppo e `enter or Leave` il `Gymnastics` gruppo privato.

![classic-ui-repository-view](assets/classic-ui-repository-view.png)

### Collegamento pagina Web {#web-page-link}

Visualizzare la pagina Web di base inclusa nel sito selezionando il collegamento Pagina Web. Per aggiungere contenuti a questa pagina nell’ambiente di authoring è possibile utilizzare gli strumenti AEM di authoring standard.

Ad esempio, passate all’istanza di **creazione** , aprite la `engage` cartella nella console [Siti](/help/communities/sites-console.md)community, selezionate l’icona **Apri sito** per passare alla modalità di modifica dell’autore. Selezionate quindi la modalità di anteprima per selezionare il `Web Page` collegamento, quindi selezionate la modalità di modifica per aggiungere i componenti Titolo e Testo. Infine, ripubblicate solo la pagina o l’intero sito.

![classic-ui-repository-path](assets/classic-ui-repository-path.png)

### Collegamento moderazione {#moderationlink}

Quando il membro della community dispone di privilegi di moderazione, il collegamento Moderazione sarà visibile e la selezione di tale collegamento consente di visualizzare il contenuto della community pubblicato e di [moderarlo](/help/communities/moderate-ugc.md) in modo simile alla console [di](/help/communities/moderation.md) moderazione nell&#39;ambiente di authoring.

Utilizzate il pulsante Indietro del browser per tornare al sito pubblicato. La maggior parte delle console non è accessibile dalla navigazione globale nell’ambiente di pubblicazione. [](/help/communities/moderate-ugc.md)

![chlimage_1-42](assets/chlimage_1-42.png)

## Autoregistrazione {#self-registration}

Dopo la disconnessione, è possibile creare una nuova registrazione utente.

* Seleziona `Log In`
* Seleziona `Sign up for a new account`

![chlimage_1-43](assets/chlimage_1-43.png) ![chlimage_1-44](assets/chlimage_1-44.png)

Per impostazione predefinita, l’indirizzo e-mail è l’ID di login. Se questa opzione è deselezionata, il visitatore può immettere il proprio ID di accesso (nome utente). Il nome utente deve essere univoco nell’ambiente di pubblicazione.

Dopo aver specificato il nome utente, l&#39;e-mail e la password, selezionando `Sign Up` l&#39;utente verrà creato e sarà possibile apporvi la firma.

Una volta effettuato l’accesso, la prima pagina presentata è la `Profile` pagina corrispondente, che possono personalizzare.

![chlimage_1-45](assets/chlimage_1-45.png)

Se il membro dimentica il suo ID di accesso, è possibile recuperare utilizzando il suo indirizzo e-mail.

![chlimage_1-46](assets/chlimage_1-46.png)

