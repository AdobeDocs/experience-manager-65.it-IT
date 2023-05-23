---
title: Gestione identità
seo-title: Identity Management
description: Scopri come gestire le identità in AEM.
seo-description: Learn about identity management in AEM.
uuid: d9b83cd7-c47a-41a5-baa4-bbf385d13bfd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 994a5751-7267-4a61-9bc7-01440a256c65
docset: aem65
exl-id: acb5b235-523e-4c01-9bd2-0cc2049f88e2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1222'
ht-degree: 2%

---

# Gestione identità{#identity-management}

I singoli visitatori del sito web possono essere identificati solo se è possibile consentire loro di accedere. Esistono diversi motivi per cui potrebbe essere utile fornire una funzionalità di accesso:

* [AEM Communities](/help/communities/overview.md)I visitatori del sito devono effettuare l&#39;accesso per pubblicare contenuti nella community.
* [Gruppi utenti chiusi](/help/sites-administering/cug.md)

   Potrebbe essere necessario limitare l’accesso al sito web (o a sue sezioni) a visitatori specifici.

* [Personalizzazione](/help/sites-administering/personalization.md) Consentire ai visitatori di configurare alcuni aspetti delle modalità di accesso al sito web.

La funzionalità di accesso (e disconnessione) è fornita da un [account con un **Profilo**](#profiles-and-user-accounts), che contiene informazioni aggiuntive sul visitatore (utente) registrato. Le procedure effettive di registrazione e di autorizzazione possono differire:

* Autoregistrazione dal sito web

   A [Sito community](/help/communities/sites-console.md) può essere configurato per consentire ai visitatori di registrarsi autonomamente o di accedere con i propri account Facebook o Twitter.

* Richiesta di registrazione dal sito web

   Per un gruppo di utenti chiuso puoi consentire ai visitatori di richiedere la registrazione, ma applicare l’autorizzazione tramite un flusso di lavoro.

* Registra ogni account dall’ambiente di authoring

   Se disponi di un numero limitato di profili che necessitano comunque dell’autorizzazione, puoi decidere di registrarli direttamente.

Per consentire ai visitatori di registrarsi, è possibile utilizzare una serie di componenti e moduli per raccogliere le informazioni di identificazione richieste, quindi le informazioni di profilo aggiuntive (spesso facoltative). Dopo la registrazione, essi dovrebbero anche essere in grado di verificare e aggiornare i dati che hanno presentato.

È possibile configurare o sviluppare ulteriori funzionalità:

* Configurare la replica inversa necessaria.
* Consenti a un utente di rimuovere il proprio profilo sviluppando un modulo insieme a un flusso di lavoro.

>[!NOTE]
>
>Le informazioni specificate nel profilo possono essere utilizzate anche per fornire all&#39;utente contenuti mirati tramite [Segmenti](/help/sites-administering/campaign-segmentation.md) e [Campagne](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md).

## Forms di registrazione {#registration-forms}

A [modulo](/help/sites-authoring/default-components.md#form-component) può essere utilizzato per raccogliere le informazioni di registrazione, quindi generare il nuovo account e profilo.

Gli utenti possono, ad esempio, richiedere un nuovo profilo utilizzando la pagina Geometrixx
`http://localhost:4502/content/geometrixx-outdoors/en/user/register.html`

![modulo di registrazione](assets/registerform.png)

Quando si invia la richiesta, viene visualizzata la pagina del profilo in cui l’utente può fornire i dati personali.

![profilepage](assets/profilepage.png)

Il nuovo account è visibile anche nel [Console Utenti](/help/sites-administering/security.md).

## Accesso {#login}

Il componente di accesso può essere utilizzato per raccogliere le informazioni di accesso, quindi attivare il processo di accesso.

Questo fornisce al visitatore i campi standard di **Nome utente** e **Password**, con un **Login** per attivare la procedura di accesso quando vengono immesse le credenziali.

Ad esempio, gli utenti possono effettuare l’accesso o creare un nuovo account utilizzando **Accedi** sulla barra degli strumenti del Geometrixx, che utilizza la pagina:

`http://localhost:4502/content/geometrixx-outdoors/en/user/sign-in.html`

![accesso](assets/login.png)

## Disconnessione {#logging-out}

Poiché è presente un meccanismo di accesso, è necessario anche un meccanismo di disconnessione. Questo è disponibile come **Esci** opzione in Geometrixx.

## Visualizzazione e aggiornamento di un profilo {#viewing-and-updating-a-profile}

A seconda del modulo di registrazione, il visitatore potrebbe avere delle informazioni registrate nel suo profilo. Dovrebbero essere in grado di visualizzarlo e/o aggiornarlo in una fase successiva. Questa operazione può essere eseguita con un modulo simile, ad esempio in Geometrixx:

```
http://localhost:4502/content/geometrixx-outdoors/en/user/profile.html
```

Per visualizzare i dettagli del profilo, fai clic su **Il mio profilo** nell’angolo in alto a destra di qualsiasi pagina, ad esempio con `admin` account:
`http://localhost:4502/home/users/a/admin/profile.form.html/content/geometrixx-outdoors/en/user/profile.html.`

È possibile visualizzare un altro profilo utilizzando [contesto client](/help/sites-administering/client-context.md) (nell’ambiente di authoring e con privilegi sufficienti):

1. Apri una pagina; ad esempio la pagina Geometrixx:

   `http://localhost:4502/cf#/content/geometrixx/en.html`

1. Clic **Il mio profilo** nell’angolo in alto a destra. Visualizzerai il profilo del tuo account corrente, ad esempio l’amministratore.
1. Premi **control-alt-C** per aprire il contesto client.
1. Nell’angolo in alto a sinistra del contesto client, fai clic su **Caricare un profilo** pulsante.

   ![](do-not-localize/loadprofile.png)

1. Seleziona un altro profilo dall’elenco a discesa nella finestra di dialogo; ad esempio, **Alison Parker**.
1. Fai clic su **OK**.
1. Fai di nuovo clic su **Il mio profilo**. Il modulo verrà aggiornato con i dettagli di Alison.

   ![profilealison](assets/profilealison.png)

1. Ora puoi utilizzare **Modifica profilo** o **Cambia password** per aggiornare i dettagli.

## Aggiunta di campi alla definizione del profilo {#adding-fields-to-the-profile-definition}

Puoi aggiungere campi alla definizione del profilo. Ad esempio, per aggiungere un campo &quot;Colore preferito&quot; al profilo di Geometrixx:

1. Dalla console Siti web, passa a Geometrixx Outdoors Sito > Inglese > Utente > Il mio profilo.
1. Fai doppio clic sul pulsante **Il mio profilo** per aprirla per la modifica.
1. In **Componenti** scheda della barra laterale espandi **Modulo** sezione.
1. Trascina un **Elenco a discesa** dalla barra laterale al modulo, appena sotto il **Informazioni su di me** campo.
1. Fai doppio clic su **Elenco a discesa** per aprire la finestra di dialogo per la configurazione e immettere:

   * **Nome elemento** - `favoriteColor`
   * **Titolo** - `Favorite Color`
   * **Elementi** - Aggiungere più colori come elementi

   Clic **OK** per salvare.

1. Chiudi la pagina e torna a **Siti Web** e attiva la pagina Il mio profilo.

   La prossima volta che visualizzi un profilo puoi selezionare un colore preferito:

   ![aparkerfavcolor](assets/aparkerfavcolour.png)

   Il campo verrà salvato in **profilo** sezione dell’account utente pertinente:

   ![aparkercrxdelite](assets/aparkercrxdelite.png)

## Stati del profilo {#profile-states}

Esistono diversi casi d’uso che richiedono di sapere se un utente (o piuttosto il suo profilo) si trova in un *stato specifico* o no.

Ciò comporta la definizione di una proprietà appropriata nel profilo utente in modo che:

* è visibile e accessibile all’utente
* definisce due stati per ogni proprietà
* consente di alternare tra i due stati definiti

Questa operazione viene eseguita con:

* [Provider di stato](#state-providers)

   Gestire i due stati di una proprietà specifica e le transizioni tra i due stati.

* [Flussi di lavoro](#workflows)

   Gestire le azioni relative agli stati.

È possibile definire più stati, ad esempio in Geometrixx:

* iscrizione (o annullamento) a notifiche su newsletter o thread di commenti
* aggiunta e rimozione di una connessione a un amico

### Provider di stato {#state-providers}

Un provider di stato gestisce lo stato corrente della proprietà in questione, insieme alle transizioni tra i due stati possibili.

I provider di stati sono implementati come componenti, quindi possono essere personalizzati per il progetto. In Geometrixx questi includono:

* Effettua/cancella sottoscrizione topic forum
* Aggiungi/Rimuovi amico

### Flussi di lavoro {#workflows}

I provider di stati gestiscono una proprietà di profilo e i relativi stati.

È necessario un flusso di lavoro per implementare le azioni relative agli stati. Ad esempio, per l’abbonamento alle notifiche, il flusso di lavoro gestirà l’azione di abbonamento effettiva; per l’annullamento dell’abbonamento alle notifiche, il flusso di lavoro gestirà la rimozione dell’utente dall’elenco di abbonamento.

## Profili e account utente {#profiles-and-user-accounts}

I profili vengono memorizzati nel repository dei contenuti come parte del[account utente](/help/sites-administering/user-group-ac-admin.md).

Il profilo si trova in `/home/users/geometrixx`:

![chlimage_1-138](assets/chlimage_1-138.png)

In un’installazione standard (authoring o pubblicazione) tutti hanno accesso in lettura all’intera serie di informazioni di profilo di tutti gli utenti. tutti sono un &quot;*Gruppo incorporato contenente automaticamente tutti gli utenti e i gruppi esistenti. Impossibile modificare l&#39;elenco dei membri*&quot;.

Questi diritti di accesso sono definiti dal seguente ACL con caratteri jolly:

/home tutti consentono jcr:read rep:glob = &#42;/profile&#42;

Ciò consente di:

* forum, commenti o post di blog per visualizzare informazioni (come icona o nome completo) dal profilo appropriato
* collegamenti alle pagine di profilo geometrixx

Se tale accesso non è appropriato per l&#39;installazione in uso, è possibile modificare le impostazioni predefinite.

Questa operazione può essere eseguita utilizzando **[Controllo dell’accesso](/help/sites-administering/user-group-ac-admin.md#access-right-management)** scheda:

![aclmanager](assets/aclmanager.png)

## Componenti del profilo {#profile-components}

Per definire i requisiti del profilo per il sito è inoltre disponibile una serie di componenti del profilo.

### Campo per password verificata {#checked-password-field}

Questo componente offre due campi per:

* inserimento di una password
* un segno di spunta per verificare che la password sia stata inserita correttamente.

Con le impostazioni predefinite, il componente viene visualizzato come segue:

![dc_profiles_checkedpassword](assets/dc_profiles_checkedpassword.png)

### Foto avatar profilo {#profile-avatar-photo}

Questo componente offre all’utente un meccanismo per selezionare e caricare un file di foto avatar.

![dc_profiles_avatarphoto](assets/dc_profiles_avatarphoto.png)

### Nome completo profilo {#profile-detailed-name}

Questo componente consente all’utente di immettere un nome dettagliato.

![dc_profiles_detailedname](assets/dc_profiles_detailedname.png)

### Genere profilo {#profile-gender}

Questo componente consente all’utente di inserire il proprio genere.

![dc_profiles_gender](assets/dc_profiles_gender.png)
