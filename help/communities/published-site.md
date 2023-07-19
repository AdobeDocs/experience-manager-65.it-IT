---
title: Esperienza del sito pubblicato
seo-title: Experience the Published Site
description: Accedere a un sito pubblicato
seo-description: Browse to a published site
uuid: 44594e9e-27ad-475d-953d-3611b04f0df8
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: dd0cbc05-a361-46bc-b9f1-d045f8f23890
docset: aem65
exl-id: ebc4e1e7-34f0-4f4e-9f00-178dfda23ce4
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 1%

---

# Esperienza del sito pubblicato {#experience-the-published-site}

## Passa al nuovo sito al momento della pubblicazione {#browse-to-new-site-on-publish}

Dopo la pubblicazione del sito delle community appena creato, individuare l&#39;URL visualizzato durante la creazione del sito, ma nel server di pubblicazione, ad esempio:

* URL autore = https://localhost:4502/content/sites/engage/en.html
* URL pubblicazione = https://localhost:4503/content/sites/engage/en.html

Per ridurre al minimo la confusione in merito al membro che ha effettuato l’accesso durante l’authoring e la pubblicazione, si consiglia di utilizzare browser diversi per ogni istanza.

Quando si accede al sito pubblicato per la prima volta, in genere il visitatore del sito non ha già effettuato l’accesso e rimane anonimo.

`https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}`

![pubblicato da authoring](assets/authorpublished.png)

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

Se si selezionano vari collegamenti, questi saranno in modalità di sola lettura.

### Impedisci accesso anonimo su JCR {#prevent-anonymous-access-on-jcr}

Tuttavia, una limitazione nota espone il contenuto del sito community a visitatori anonimi tramite il contenuto JCR e JSON. **consenti accesso anonimo** è disabilitato per il contenuto del sito. Tuttavia, questo comportamento può essere controllato utilizzando Sling Restrictions come soluzione alternativa.

Per proteggere il contenuto del sito community dall’accesso da parte di utenti anonimi tramite il contenuto JCR e JSON , effettua le seguenti operazioni:

1. Nell’istanza di AEM Author, vai a https:// nomehost:port/editor.html/content/site/sitename.html.

   >[!NOTE]
   >
   >Non passare al sito localizzato.

1. Vai a **Proprietà pagina**.

   ![page-properties](assets/page-properties.png)

1. Vai a **Avanzate** scheda.

1. Abilita **Autenticazione richiesta**.

   ![autenticazione del sito](assets/site-authentication.png)

1. Aggiungi il percorso della pagina di accesso. Ad esempio: **/content/......./GetStarted**.
1. Pubblica la pagina.

## Membro community attendibile {#trusted-community-member}

Questa esperienza presuppone [Aaron McDonald](/help/communities/tutorials.md#demo-users) Gli è stato assegnato il ruolo di [manager e moderatore della community](/help/communities/create-site.md#roles). In caso contrario, torna all’ambiente di authoring per [modificare le impostazioni del sito](/help/communities/sites-console.md#modifying-site-properties) e seleziona Aaron McDonald come manager e moderatore della community.

Nell’angolo superiore destro, seleziona `Log in`, e firmare con nome utente (aaron.mcdonald@mailinator.com) e password (password). Nota la possibilità di accedere con le credenziali di Twitter o Facebook.

![accesso](assets/login.png)

Dopo aver effettuato l&#39;accesso come membro della community registrato, notare le seguenti voci di menu per fare clic ed esplorare il sito della community:

* **Profilo** consente di visualizzare e modificare il profilo.
* [Messaggi](/help/communities/configure-messaging.md) L’opzione ti indirizza alla sezione direct messaging, dove puoi:

   1. Visualizza i messaggi diretti ricevuti (Posta in arrivo), inviati (Elementi inviati) ed eliminati (Cestino).
   1. Creare nuovi messaggi diretti da inviare a singoli utenti e gruppi.

* [Notifiche](/help/communities/notifications.md) L’opzione ti reindirizza alla sezione notifiche, dove puoi visualizzare gli eventi di tuo interesse e modificare le impostazioni delle notifiche.
* [Amministrazione](/help/communities/published-site.md#moderationlink) reindirizza alla pagina Moderazione di AEM Communities, se si dispone di privilegi di moderazione.

![adminscreen](assets/adminscreen.png)

Osserva che la pagina Calendario è la home page perché il modello del sito di riferimento selezionato includeva prima la funzione Calendario, seguita dalla funzione Flusso di attività, dalla funzione Forum e così via. Questa struttura è visibile dalla sezione [Modello del sito](/help/communities/sites.md#edit-site-template) o durante la modifica delle proprietà del sito nell’ambiente di authoring:

![sitetemplate](assets/sitetemplate.png)

>[!NOTE]
>
>Per ulteriori informazioni sui componenti e sulle funzioni di Communities, visita:
>
>* [Componenti community](/help/communities/author-communities.md) (per autori)
>* [Nozioni di base su componenti, funzioni e funzioni](/help/communities/essentials.md) (per sviluppatori)

### Collegamento forum {#forum-link}

Per visualizzare la funzione di forum di base, selezionare il collegamento Forum.

I membri possono pubblicare un nuovo argomento o seguire un argomento.

I visitatori del sito possono visualizzare i post e ordinarli in vari modi.

![forumlink](assets/forumlink.png)

### Collegamento Gruppi {#groups-link}

Poiché Aaron è un amministratore di gruppo, selezionando il collegamento Gruppi sarà possibile creare un nuovo gruppo di community selezionando un modello di gruppo, un&#39;immagine, se il gruppo è aperto o segreto e invitando i membri.

Questo è un esempio in cui un gruppo viene creato nell’ambiente di pubblicazione.

I gruppi possono essere creati anche nell’ambiente di authoring e gestiti all’interno del sito community nell’ambiente di authoring ([Console Gruppi community](/help/communities/groups.md)). L’esperienza di [creazione di gruppi sull&#39;autore](/help/communities/nested-groups.md) è il prossimo in questo tutorial.

![grouplink](assets/grouplink.png)

Creare un gruppo di riferimento:

1. Seleziona **Nuovo gruppo**
1. **Scheda Impostazioni**

   * Nome gruppo : `Sports`
   * Descrizione : `A parent group for various sporting groups`.
   * Nome URL del gruppo : `sports`
   * Seleziona `Open Group` (consenti a qualsiasi membro della community di partecipare)

1. **Scheda Modello**

   * Seleziona `Reference Group` (contiene una funzione di gruppi nella sua struttura per consentire i gruppi nidificati)

1. Seleziona **Crea gruppo**

   ![creategroup](assets/creategroup.png)

Dopo la creazione di un nuovo gruppo, **seleziona il nuovo gruppo Sport** per creare due gruppi (nidificati) al suo interno. Poiché una struttura del sito non può iniziare con la funzione gruppi, dopo l’apertura del gruppo Sport è necessario selezionare il collegamento Gruppi:

![grouplink1](assets/grouplink1.png)

Il secondo set di collegamenti, che inizia con `Blog`, appartengono al gruppo attualmente selezionato, il `Sports` gruppo. Selezionando la casella Sport&#39; `Groups` collegamento, è possibile nidificare due gruppi all’interno del gruppo Sport.

Ad esempio, aggiungi due `new groups`.

* Uno denominato `Baseball`

   * Lascia impostato come `Open Group` (iscrizione obbligatoria).
   * Nella scheda Modelli, seleziona `Conversational Group`.

* Uno denominato `Gymnastics`

   * Cambia l’impostazione in `Member Only Group` (iscrizione limitata).
   * Nella scheda Modelli, seleziona `Conversational Group`.

**Avviso**:

* Potrebbe essere necessario aggiornare la pagina prima di visualizzare entrambi i gruppi.
* Questo modello funziona *non* includi la funzione dei gruppi, in modo che non sia possibile nidificare ulteriormente i gruppi.
* Nell’autore, il [Console Gruppi](/help/communities/groups.md) offre una terza scelta: `Public Group` (iscrizione facoltativa).

Una volta creati entrambi i gruppi, seleziona il gruppo di baseball, un gruppo aperto, e osserva i collegamenti:

`Discussions` `What's New` `Members`

I collegamenti del gruppo vengono visualizzati sotto i collegamenti del sito principale e il risultato è il seguente:

![grouplink2](assets/grouplink2.png)

In fase di authoring, con privilegi di amministratore, accedi al [Console Gruppi community](/help/communities/members.md) e aggiungi Weston McCall al `Community Engage Gymnastics <uid> Members` gruppo.

Continuando con la pubblicazione, esci come Aaron McDonald e visualizza i gruppi nel gruppo Sport come un visitatore anonimo del sito:

* Dalla home page
* Seleziona `Groups` link
* Seleziona `Sports` link
* Seleziona la sezione Sport&#39; `Groups` link

Solo il gruppo di baseball sarà visibile.

Accedi come Weston McCall (weston.mccall@dodgit.com / password) e passa alla stessa posizione. Weston è in grado di: `Join` l&#39;apertura `Baseball` gruppo e `enter or Leave` il privato `Gymnastics` gruppo.

![grouplink3](assets/grouplink3.png)

### Collegamento pagina web {#web-page-link}

Visualizzare la pagina Web di base inclusa nel sito selezionando il collegamento Pagina Web. Per aggiungere contenuti a questa pagina nell’ambiente di authoring, è possibile utilizzare gli strumenti AEM standard.

Ad esempio, vai a **autore** istanza, apri la `engage` cartella in [Console Siti community](/help/communities/sites-console.md), seleziona la **Apri sito** per accedere alla modalità di modifica dell’autore. Quindi seleziona la modalità anteprima per selezionare `Web Page` , quindi seleziona la modalità di modifica per aggiungere i componenti Titolo e Testo. Infine, ripubblica solo la pagina o l’intero sito.

![webpagelink](assets/webpagelink.png)

### Collegamento per moderazione {#moderationlink}

Quando il membro della community dispone dei privilegi di moderazione, il collegamento Moderazione sarà visibile e, selezionandolo, verrà visualizzato il contenuto della community pubblicato e verrà consentito [moderato](/help/communities/moderate-ugc.md) in modo simile al [console di moderazione](/help/communities/moderation.md) nell’ambiente di authoring.

Utilizza il pulsante Indietro del browser per tornare al sito pubblicato. La maggior parte delle console non è accessibile dalla navigazione globale nell’ambiente di pubblicazione.

![moderationlink](assets/moderationlink.png)

## Registrazione autonoma {#self-registration}

Dopo la disconnessione, è possibile creare una nuova registrazione utente.

* Seleziona `Log In`
* Seleziona `Sign up for a new account`

![registrazione](assets/registration.png)

![iscrizione](assets/signup.png)

Per impostazione predefinita, l’indirizzo e-mail è l’ID di accesso. Se questa opzione è deselezionata, il visitatore può immettere il proprio ID di accesso (nome utente). Il nome utente deve essere univoco nell’ambiente di pubblicazione.

Dopo aver specificato il nome, l’e-mail e la password dell’utente, seleziona `Sign Up` creerà l’utente e gli consentirà di firmare.

Una volta effettuato l’accesso, viene visualizzata la prima pagina `Profile` , che possono personalizzare.

![profilo](assets/profile.png)

Se il membro dimentica il proprio ID di accesso, è possibile recuperare utilizzando il proprio indirizzo e-mail.

![forgotusername](assets/forgotusername.png)
