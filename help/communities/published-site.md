---
title: Esperienza del sito pubblicato
description: Scopri come passare all’URL visualizzato durante la creazione di un sito, ma sul server di pubblicazione.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: ebc4e1e7-34f0-4f4e-9f00-178dfda23ce4
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1195'
ht-degree: 0%

---

# Esperienza del sito pubblicato {#experience-the-published-site}

## Passa a nuovo sito in Publish {#browse-to-new-site-on-publish}

Dopo la pubblicazione del sito delle community appena creato, individuare l&#39;URL visualizzato durante la creazione del sito, ma nel server di pubblicazione, ad esempio:

* URL autore = https://localhost:4502/content/sites/engage/en.html
* URL PUBLISH = https://localhost:4503/content/sites/engage/en.html

Per ridurre al minimo la confusione in merito al membro che ha effettuato l’accesso durante l’authoring e la pubblicazione, si consiglia di utilizzare browser diversi per ogni istanza.

Quando si accede al sito pubblicato per la prima volta, in genere il visitatore del sito non ha già effettuato l’accesso e rimane anonimo.

`https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}`

![pubblicato/i](assets/authorpublished.png)

## Visitatore sito anonimo {#anonymous-site-visitor}

Un visitatore anonimo del sito visualizza quanto segue nell’interfaccia utente:

* Titolo del sito (esercitazione introduttiva)
* Nessun collegamento profilo
* Collegamento Nessun messaggio
* Collegamento Nessuna notifica
* Campo di ricerca
* Collegamento di accesso
* Banner del brand
* Collegamenti del menu per i componenti inclusi nel modello del sito di riferimento.

Se si selezionano vari collegamenti, si noterà che sono in modalità di sola lettura.

### Impedisci accesso anonimo su JCR {#prevent-anonymous-access-on-jcr}

Una limitazione nota espone il contenuto del sito community ai visitatori anonimi tramite il contenuto JCR e JSON, anche se **consenti accesso anonimo** è disabilitato per il contenuto del sito. Tuttavia, questo comportamento può essere controllato utilizzando Sling Restrictions come soluzione alternativa.

Per proteggere il contenuto del sito community dall’accesso da parte di utenti anonimi tramite il contenuto JCR e JSON , effettua le seguenti operazioni:

1. Nell’istanza Autore AEM, vai a https:// nomehost:port/editor.html/content/site/sitename.html.

   >[!NOTE]
   >
   >Non passare al sito localizzato.

1. Vai a **Proprietà pagina**.

   ![proprietà-pagina](assets/page-properties.png)

1. Passa alla scheda **Avanzate**.

1. Abilita **Autenticazione richiesta**.

   ![autenticazione sito](assets/site-authentication.png)

1. Aggiungi il percorso della pagina di accesso. Ad esempio, **/content/......./GetStarted**.
1. Publish la pagina.

## Membro community attendibile {#trusted-community-member}

Questa esperienza presuppone che a [Aaron McDonald](/help/communities/tutorials.md#demo-users) siano stati assegnati i ruoli di [manager e moderatore della community](/help/communities/create-site.md#roles). In caso contrario, tornare all&#39;ambiente di authoring per [modificare le impostazioni del sito](/help/communities/sites-console.md#modifying-site-properties) e selezionare Aaron McDonald come manager e moderatore della community.

Nell&#39;angolo superiore destro selezionare `Log in` e firmare con nome utente (aaron.mcdonald@mailinator.com) e password (password). Nota la possibilità di accedere con le credenziali di Twitter o Facebook.

![accesso](assets/login.png)

Dopo aver effettuato l&#39;accesso come membro della community registrato, notare le seguenti voci di menu per fare clic ed esplorare il sito della community:

* L&#39;opzione **Profilo** consente di visualizzare e modificare il profilo.
* L&#39;opzione [Messaggi](/help/communities/configure-messaging.md) ti indirizza alla sezione Messaggistica diretta, in cui puoi eseguire le seguenti operazioni:

   1. Visualizza i messaggi diretti ricevuti (Posta in arrivo), inviati (Elementi inviati) ed eliminati (Cestino).
   1. Comporre nuovi messaggi diretti in modo da poter inviare a singoli utenti e gruppi.

* L&#39;opzione [Notifiche](/help/communities/notifications.md) ti indirizza alla sezione delle notifiche, dove puoi visualizzare gli eventi di tuo interesse e modificare le impostazioni delle notifiche.
* [Amministrazione](/help/communities/published-site.md#moderationlink) reindirizza alla pagina di moderazione di AEM Communities, se si dispone di privilegi di moderazione.

![adminscreen](assets/adminscreen.png)

Si noti che la pagina Calendario è la home page perché il modello del sito di riferimento selezionato include prima la funzione Calendario, quindi la funzione Flusso attività, la funzione Forum e così via. Questa struttura è visibile dalla console [Modello sito](/help/communities/sites.md#edit-site-template) o durante la modifica delle proprietà del sito nell&#39;ambiente di authoring:

![sitetemplate](assets/sitetemplate.png)

>[!NOTE]
>
>Per ulteriori informazioni sui componenti e sulle funzioni di Communities, visita:
>
>* [Componenti community](/help/communities/author-communities.md) (per autori)
>* [Componente, funzione e funzionalità di base](/help/communities/essentials.md) (per sviluppatori)

### Collegamento forum {#forum-link}

Per visualizzare la funzione di forum di base, selezionare il collegamento Forum.

I membri possono pubblicare un nuovo argomento o seguire un argomento.

I visitatori del sito possono visualizzare i post e ordinarli in vari modi.

![forumlink](assets/forumlink.png)

### Collegamento Gruppi {#groups-link}

Poiché Aaron è un amministratore di gruppo, selezionando il collegamento Gruppi è possibile creare un gruppo di community selezionando un modello di gruppo, un&#39;immagine, se il gruppo è aperto o segreto e invitando i membri.

Questo è un esempio in cui un gruppo viene creato nell’ambiente di pubblicazione.

È inoltre possibile creare gruppi nell&#39;ambiente di authoring e gestirli all&#39;interno del sito community nell&#39;ambiente di authoring ([console Gruppi community](/help/communities/groups.md)). L&#39;esperienza di [creazione di gruppi sull&#39;autore](/help/communities/nested-groups.md) è successiva in questa esercitazione.

![collegamentogruppo](assets/grouplink.png)

Creare un gruppo di riferimento:

1. Seleziona **Nuovo gruppo**
1. **Scheda Impostazioni**

   * Nome gruppo: `Sports`
   * Descrizione: `A parent group for various sporting groups`.
   * Nome URL gruppo: `sports`
   * Seleziona `Open Group` (consenti a qualsiasi membro della community di partecipare tramite l&#39;iscrizione)

1. **Scheda Modello**

   * Seleziona `Reference Group` (contiene una funzione di gruppi nella sua struttura per consentire i gruppi nidificati)

1. Seleziona **Crea gruppo**

   ![gruppo creativo](assets/creategroup.png)

Dopo la creazione del nuovo gruppo, **selezionare il nuovo gruppo Sport** per creare due gruppi (nidificati) al suo interno. Poiché una struttura del sito non può iniziare con la funzione gruppi, dopo l’apertura del gruppo Sport è necessario selezionare il collegamento Gruppi:

![collegamentogruppo1](assets/grouplink1.png)

Il secondo gruppo di collegamenti, che inizia con `Blog`, appartiene al gruppo attualmente selezionato, il gruppo `Sports`. Selezionando il collegamento Sport `Groups`, è possibile nidificare due gruppi all&#39;interno del gruppo Sport.

Ad esempio, aggiungere due `new groups`.

* Uno denominato `Baseball`

   * Lascialo impostato come `Open Group` (iscrizione obbligatoria).
   * Nella scheda Modelli, selezionare `Conversational Group`.

* Uno denominato `Gymnastics`

   * Cambia l&#39;impostazione in `Member Only Group` (appartenenza limitata).
   * Nella scheda Modelli, selezionare `Conversational Group`.

**Avviso**:

* Potrebbe essere necessario aggiornare la pagina prima di visualizzare entrambi i gruppi.
* Questo modello *non* include la funzione dei gruppi, pertanto non è possibile nidificare ulteriormente i gruppi.
* Per l&#39;autore, la console [Gruppi](/help/communities/groups.md) fornisce una terza scelta: `Public Group` (iscrizione facoltativa).

Una volta creati entrambi i gruppi, seleziona il gruppo di baseball, un gruppo aperto, e osserva i collegamenti:

`Discussions` `What's New` `Members`

I collegamenti del gruppo vengono visualizzati sotto i collegamenti del sito principale e i risultati vengono visualizzati nella seguente schermata:

![collegamentogruppo2](assets/grouplink2.png)

All&#39;autore - con privilegi amministrativi, passare alla console [Gruppi community](/help/communities/members.md) e aggiungere Weston McCall al gruppo `Community Engage Gymnastics <uid> Members`.

Continuando con la pubblicazione, esci come Aaron McDonald e visualizza i gruppi nel gruppo Sport come un visitatore anonimo del sito:

* Dalla home page
* Seleziona collegamento `Groups`
* Seleziona collegamento `Sports`
* Seleziona il collegamento `Groups` per Sport

Solo il gruppo di baseball è visibile.

Accedi come Weston McCall (weston.mccall@dodgit.com / password) e passa alla stessa posizione. Si noti che Weston è in grado di `Join` il gruppo `Baseball` aperto e `enter or Leave` il gruppo `Gymnastics` privato.

![collegamentogruppo3](assets/grouplink3.png)

### Collegamento pagina web {#web-page-link}

Visualizzare la pagina Web di base inclusa nel sito selezionando il collegamento Pagina Web. Per aggiungere contenuti a questa pagina nell’ambiente di authoring, è possibile utilizzare gli strumenti AEM standard.

Ad esempio, vai all&#39;istanza **author**, apri la cartella `engage` nella console [Communities Sites](/help/communities/sites-console.md), seleziona l&#39;icona **Apri sito** per accedere alla modalità di modifica dell&#39;autore. Quindi seleziona la modalità anteprima in modo da poter selezionare il collegamento `Web Page`, quindi seleziona la modalità di modifica per aggiungere i componenti Titolo e Testo. Infine, ripubblica solo la pagina o l’intero sito.

![webpagelink](assets/webpagelink.png)

### Collegamento per moderazione {#moderationlink}

Quando il membro della community dispone di privilegi di moderazione, è visibile il collegamento Moderazione. Selezionando il collegamento, viene visualizzato il contenuto della community pubblicato e ne viene consentita la [moderazione](/help/communities/moderate-ugc.md) in modo simile alla [console di moderazione](/help/communities/moderation.md) nell&#39;ambiente di authoring.

Utilizza il pulsante Indietro del browser per tornare al sito pubblicato. La maggior parte delle console non è accessibile dalla navigazione globale nell’ambiente di pubblicazione.

![collegamento moderazione](assets/moderationlink.png)

## Registrazione autonoma {#self-registration}

Dopo la disconnessione, è possibile creare una registrazione utente.

* Seleziona `Log In`
* Seleziona `Sign up for a new account`

![registrazione](assets/registration.png)

![abbonamento](assets/signup.png)

Per impostazione predefinita, l’indirizzo e-mail è l’ID di accesso. Se questa opzione è deselezionata, il visitatore può immettere il proprio ID di accesso (nome utente). Il nome utente deve essere univoco nell’ambiente di pubblicazione.

Dopo aver specificato il nome, l&#39;indirizzo e-mail e la password dell&#39;utente, selezionando `Sign Up` l&#39;utente verrà creato e sarà possibile firmarlo.

Dopo l&#39;accesso, la prima pagina visualizzata è la pagina `Profile`, che possono personalizzare.

![profilo](assets/profile.png)

Se il membro dimentica il proprio ID di accesso, è possibile recuperare utilizzando il proprio indirizzo e-mail.

![nomeutente dimenticato](assets/forgotusername.png)
