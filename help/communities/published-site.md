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
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1202'
ht-degree: 1%

---


# Esperienza con il sito pubblicato {#experience-the-published-site}

## Passa a nuovo sito in Pubblica {#browse-to-new-site-on-publish}

Ora che il sito community appena creato è stato pubblicato, individuate l’URL visualizzato al momento della creazione del sito, ma sul server di pubblicazione, ad esempio:

* URL autore = https://localhost:4502/content/sites/engage/en.html
* URL pubblicazione = https://localhost:4503/content/sites/engage/en.html

Per ridurre la confusione relativa al membro che ha effettuato l’accesso in fase di creazione e pubblicazione, si consiglia di utilizzare browser diversi per ogni istanza.

Al primo arrivo sul sito pubblicato, il visitatore del sito in genere non avrebbe già effettuato l’accesso e sarebbe anonimo.

`https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}`

![authorpublished](assets/authorpublished.png)

## Visitatore anonimo del sito {#anonymous-site-visitor}

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

### Impedisci l&#39;accesso anonimo su JCR {#prevent-anonymous-access-on-jcr}

Una limitazione nota espone il contenuto del sito community ai visitatori anonimi attraverso contenuti jcr e json, anche se **consenti l&#39;accesso anonimo** è disabilitato per il contenuto del sito. Tuttavia, questo comportamento può essere controllato utilizzando Limitazioni Sling come soluzione alternativa.

Per proteggere i contenuti del sito della community dall&#39;accesso di utenti anonimi tramite contenuti jcr e json, procedi come segue:

1. Nell&#39;istanza di AEM Author, andate a https:// nomehost:port/editor.html/content/site/sitename.html.

   >[!NOTE]
   >
   >Non andate al sito localizzato.

1. Vai a **Proprietà pagina**.

   ![page-properties](assets/page-properties.png)

1. Vai alla scheda **Avanzate**.

1. Abilita **Autenticazione richiesta**.

   ![autenticazione del sito](assets/site-authentication.png)

1. Aggiungete il percorso della pagina di login. Ad esempio, **/content/......./GetStarted**.
1. Pubblicate la pagina.

## Membro della community trusted {#trusted-community-member}

Questa esperienza presuppone che [Aaron McDonald](/help/communities/tutorials.md#demo-users) sia stato assegnato il ruolo di [community manager e moderatore](/help/communities/create-site.md#roles). In caso contrario, tornate all&#39;ambiente di authoring per [modificare le impostazioni del sito](/help/communities/sites-console.md#modifying-site-properties) e selezionate Aaron McDonald come manager e moderatore della community.

Nell&#39;angolo in alto a destra, selezionare `Log in` e firmare con nome utente (aaron.mcdonald@mailinator.com) e password (password). Notate la possibilità di accedere con le credenziali di Twitter o Facebook.

![login](assets/login.png)

Una volta effettuato l&#39;accesso come membro della community registrato, potete vedere le seguenti voci di menu su cui fare clic ed esplorare il sito della community:

* **** Profileoption consente di visualizzare e modificare il profilo.
* [L&#39;opzione ](/help/communities/configure-messaging.md) Messaggi consente di accedere alla sezione dei messaggi diretti, in cui è possibile:

   1. Visualizzare i messaggi diretti ricevuti (Posta in arrivo), inviati (Elementi inviati) ed eliminati (Cestino).
   1. Comporre nuovi messaggi diretti da inviare a singoli e gruppi.

* [L&#39;](/help/communities/notifications.md) opzione Notifiche consente di accedere alla sezione delle notifiche, in cui è possibile visualizzare gli eventi di interesse e modificare le impostazioni delle notifiche.
* [Se disponete dei privilegi di moderazione, ](/help/communities/published-site.md#moderationlink) Administration vi indirizza  pagina Moderazione AEM Communities.

![adminscreen](assets/adminscreen.png)

Notate che la pagina Calendario è la home page perché il modello di sito di riferimento scelto includeva prima la funzione Calendario, seguita dalla funzione Flusso di attività, dalla funzione Forum e così via. Questa struttura è visibile dalla console [Site Template](/help/communities/sites.md#edit-site-template) o durante la modifica delle proprietà del sito nell&#39;ambiente di authoring:

![sitetemplate](assets/sitetemplate.png)

>[!NOTE]
>
>Per ulteriori informazioni sui componenti e sulle funzioni di Community, visita:
>
>* [Componenti](/help/communities/author-communities.md)  Community (per autori)
>* [Componenti, funzioni e funzionalità Essentials](/help/communities/essentials.md)  (per sviluppatori)


### Collegamento forum {#forum-link}

Per visualizzare la funzione forum di base, fate clic sul collegamento Forum.

I membri possono pubblicare un nuovo argomento o seguire un argomento.

I visitatori del sito possono visualizzare i post e ordinarli in vari modi.

![forumlink](assets/forumlink.png)

### Collegamento gruppi {#groups-link}

Poiché Aaron è un amministratore di gruppo, selezionando il collegamento Gruppi, Aaron potrà creare un nuovo gruppo di community selezionando un modello di gruppo, un’immagine, un gruppo aperto o segreto e i membri invitati.

Questo è un esempio in cui viene creato un gruppo nell’ambiente di pubblicazione.

I gruppi possono essere creati anche nell&#39;ambiente di authoring e gestiti all&#39;interno del sito community nell&#39;ambiente di authoring ([console Gruppi community](/help/communities/groups.md)). L&#39;esperienza di [creazione di gruppi in author](/help/communities/nested-groups.md) è descritta di seguito in questa esercitazione.

![grouplink](assets/grouplink.png)

Crea un gruppo di riferimento:

1. Selezionare **Nuovo gruppo**
1. **scheda Impostazioni**

   * Nome gruppo : `Sports`
   * Descrizione : `A parent group for various sporting groups`.
   * Nome URL del gruppo : `sports`
   * Selezionare `Open Group` (consentire a qualsiasi membro della community di partecipare partecipando)

1. **Scheda Modello**

   * Selezionare `Reference Group` (contiene una funzione di gruppi nella struttura per consentire i gruppi nidificati)

1. Selezionare **Crea gruppo**

   ![creategroup](assets/creategroup.png)

Dopo la creazione del nuovo gruppo, **selezionate il nuovo gruppo Sport** per creare due gruppi (nidificati) al suo interno. Poiché una struttura del sito non può iniziare con la funzione dei gruppi, dopo aver aperto il gruppo Sport, è necessario selezionare il collegamento Gruppi:

![grouplink1](assets/grouplink1.png)

Il secondo gruppo di collegamenti, a partire da `Blog`, appartiene al gruppo attualmente selezionato, il gruppo `Sports`. Selezionando il collegamento Sport `Groups`, è possibile nidificare due gruppi all&#39;interno del gruppo Sport.

Ad esempio, aggiungere due `new groups`.

* Uno denominato `Baseball`

   * Lasciatelo impostato come `Open Group` (iscrizione obbligatoria).
   * Nella scheda Modelli, selezionare `Conversational Group`.

* Uno denominato `Gymnastics`

   * Modificatene l&#39;impostazione su `Member Only Group` (iscrizione limitata).
   * Nella scheda Modelli, selezionare `Conversational Group`.

**Avviso**:

* Prima di visualizzare entrambi i gruppi potrebbe essere necessario aggiornare la pagina.
* Questo modello *not* include la funzione dei gruppi, pertanto non sarà possibile effettuare ulteriori nidificazioni dei gruppi.
* All&#39;autore, la [console Gruppi](/help/communities/groups.md) offre una terza scelta, ovvero un `Public Group` (iscrizione facoltativa).

Una volta creati entrambi i gruppi, selezionate il gruppo Baseball, un gruppo aperto e notate i relativi collegamenti:

`Discussions` `What's New` `Members`

I collegamenti del gruppo sono visualizzati sotto i collegamenti del sito principale e i risultati sono la seguente visualizzazione:

![grouplink2](assets/grouplink2.png)

Per l&#39;autore, con privilegi amministrativi, andate alla console [Gruppi community](/help/communities/members.md) e aggiungete Weston McCall al gruppo `Community Engage Gymnastics <uid> Members`.

Continuando a pubblicare, disconnettetevi come Aaron McDonald e visualizzate i gruppi nel Gruppo sportivo come visitatore anonimo del sito:

* Dalla home page
* Seleziona il collegamento `Groups`
* Seleziona il collegamento `Sports`
* Selezionare il collegamento Sport&#39; `Groups`

Solo il gruppo di baseball sarà visibile.

Effettuate l&#39;accesso come Weston McCall (weston.mccall@dodgit.com / password) e andate alla stessa posizione. Notate che Weston è in grado di `Join` aprire il gruppo `Baseball` e `enter or Leave` il gruppo privato `Gymnastics`.

![grouplink3](assets/grouplink3.png)

### Collegamento pagina Web {#web-page-link}

Visualizzare la pagina Web di base inclusa nel sito selezionando il collegamento Pagina Web. Per aggiungere contenuti a questa pagina nell’ambiente di authoring è possibile utilizzare gli strumenti AEM di authoring standard.

Ad esempio, andate all&#39;istanza **author**, aprite la cartella `engage` nella console [Siti community](/help/communities/sites-console.md), selezionate l&#39;icona **Apri sito** per passare alla modalità di modifica dell&#39;autore. Selezionate quindi la modalità di anteprima per selezionare il collegamento `Web Page`, quindi selezionate la modalità di modifica per aggiungere i componenti Titolo e Testo. Infine, ripubblicate solo la pagina o l’intero sito.

![webpagelink](assets/webpagelink.png)

### Collegamento moderazione {#moderationlink}

Quando il membro della community dispone di privilegi di moderazione, il collegamento Moderazione sarà visibile e la selezione visualizzerà il contenuto della community pubblicato e consentirà di essere [moderato](/help/communities/moderate-ugc.md) in modo simile alla [console di moderazione](/help/communities/moderation.md) nell&#39;ambiente di authoring.

Utilizzate il pulsante Indietro del browser per tornare al sito pubblicato. La maggior parte delle console non è accessibile dalla navigazione globale nell’ambiente di pubblicazione. [](/help/communities/moderate-ugc.md)

![moderationlink](assets/moderationlink.png)

## Registrazione automatica {#self-registration}

Dopo la disconnessione, è possibile creare una nuova registrazione utente.

* Seleziona `Log In`
* Seleziona `Sign up for a new account`

![registration](assets/registration.png)

![registrazione](assets/signup.png)

Per impostazione predefinita, l’indirizzo e-mail è l’ID di login. Se questa opzione è deselezionata, il visitatore può immettere il proprio ID di accesso (nome utente). Il nome utente deve essere univoco nell’ambiente di pubblicazione.

Dopo aver specificato il nome utente, l&#39;e-mail e la password, selezionando `Sign Up` l&#39;utente sarà in grado di crearlo e di consentirne la firma.

Una volta effettuato l&#39;accesso, la prima pagina presentata è la pagina `Profile`, che possono personalizzare.

![profilo](assets/profile.png)

Se il membro dimentica il suo ID di accesso, è possibile recuperare utilizzando il suo indirizzo e-mail.

![forgotusername](assets/forgotusername.png)

