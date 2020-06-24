---
title: Integrazione con Livefyre
seo-title: Integrazione con Livefyre
description: Scoprite come integrare le funzionalità di cura leader di settore di Livefyre con l'istanza AEM 6.5, consentendo di pubblicare in pochi minuti contenuti generati dagli utenti (UGC) dai social network al sito.
seo-description: Scoprite come integrare e utilizzare Livefyre con AEM 6.5.
uuid: c355705d-6e0f-4a33-aa1f-d2d1c818aac0
contentOwner: ind14750
content-type: reference
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: bb3fcb53-b8c3-4b1d-9125-4715f34ceb0b
translation-type: tm+mt
source-git-commit: 70b18dbe351901abb333d491dd06a6c1c1c569d6
workflow-type: tm+mt
source-wordcount: '1706'
ht-degree: 4%

---


# Integrazione con Livefyre{#integrating-with-livefyre}

Scoprite come integrare le funzionalità di cura leader di settore di Livefyre con l&#39;istanza AEM 6.5, consentendo di pubblicare in pochi minuti contenuti generati dagli utenti (UGC) dai social network al sito.

## Guida introduttiva {#getting-started}

### Installare il pacchetto Livefyre per AEM {#install-livefyre-package-for-aem}

AEM 6.5 viene fornito con il pacchetto delle funzioni Livefyre 1.2.6 preinstallato. Questo pacchetto include solo un&#39;integrazione Livefyre limitata con i AEM Sites e deve essere disinstallato prima di installare un pacchetto aggiornato. Con il pacchetto più recente, puoi provare l’integrazione completa di Livefyre con AEM, compresi Siti, Risorse e Commercio.

>[!NOTE]
>
>Alcune funzioni del pacchetto AEM-LF dipendono dal framework dei componenti social (SCF). Se utilizzate il feature pack di Livefyre come parte di un sito non appartenente a una comunità, dovete dichiarare *cq.social.scf* come una dipendenza nei clientlibs degli autori del sito Web. Se utilizzate il feature pack LF come parte di un sito Web di una community, questa dipendenza dovrebbe già essere dichiarata.

1. Dalla home page di AEM, fai clic sull’icona **Strumenti** nella parte sinistra.
1. Andate a **Distribuzione > Pacchetti**.
1. In Gestione pacchetti, scorrete fino a visualizzare il pacchetto delle funzioni Livefyre preinstallato, quindi fate clic sul titolo del pacchetto **cq-social-livefyre-pkg-1.2.6.zip** per espandere le opzioni.
1. Fate clic su **Altro > Disinstalla**.

   ![livefyre-aem-uninstall-64](assets/livefyre-aem-uninstall-64.png)

1. Tornate alla home page di AEM, fate clic su Strumenti, quindi selezionate **Distribuzione > Condivisione** pacchetti.

   Viene visualizzato un elenco di pacchetti di funzioni e hotfix disponibili per il download.

1. Nella ricerca per parole chiave, cercate &quot;Livefyre&quot;, quindi selezionate il pacchetto di funzioni Livefyre corrispondente alla versione di AEM.

   ![livefyre-aem3-6-4](assets/livefyre-aem3-6-4.png)

1. Nella pagina delle informazioni sul pacchetto di funzioni, fate clic su **Scarica**, quindi leggete il contratto di licenza per il pacchetto e fate clic su **Accetto**.
1. Tornate a Gestione pacchetti, individuate il pacchetto appena scaricato e fate clic su **Installa**.

   ![livefyre-aem4-6-4](assets/livefyre-aem4-6-4.png)

   Il pacchetto Livefyre-AEM è ora installato. Prima di iniziare a utilizzare le funzioni di integrazione, è necessario configurare AEM per l&#39;utilizzo di Livefyre.

   Per ulteriori informazioni sui pacchetti, vedere [Come utilizzare i pacchetti](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/package-manager.html).

   Per ulteriori informazioni e note sulla versione dei pacchetti di funzioni, consulta [Feature Pack](https://helpx.adobe.com/experience-manager/6-3/release-notes/feature-packs-release-notes.html).

### Configurare AEM per l&#39;utilizzo di Livefyre: Creare una cartella di configurazione {#configure-aem-to-use-livefyre-create-a-configuration-folder}

1. Dalla home page di AEM, fai clic sull’icona **Strumenti** nella barra a sinistra, quindi passa a **Generale > Browser** di configurazione.
1. Fate clic su **Crea** per aprire la finestra di dialogo Crea configurazione.
1. Assegnate un nome alla configurazione e selezionate la casella di controllo **Cloud Configurations (Configurazioni** cloud).

   In questo modo verrà creata una cartella in **Strumenti > Distribuzione > Configurazione** Livefyre con il nome fornito.

   ![livefyre-aem-create-config-folder](assets/livefyre-aem-create-config-folder.png)

### Configurare AEM per l&#39;utilizzo di Livefyre: Creare una configurazione Livefyre {#configure-aem-to-use-livefyre-create-a-livefyre-configuration}

Configurate AEM per l&#39;utilizzo delle credenziali di licenza Livefyre dell&#39;organizzazione, consentendo la comunicazione tra Livefyre e AEM.

1. Dalla home page di AEM, fate clic sull&#39;icona **Strumenti** nella barra a sinistra, quindi selezionate **Distribuzione > Configurazione** Livefyre.
1. Selezionate la cartella di configurazione in cui desiderate creare una nuova configurazione Livefyre, quindi fate clic su **Crea**.

   ![create-livefyre-configuration1](assets/create-livefyre-configuration1.png)

   >[!NOTE]
   >
   >Per poter aggiungere le configurazioni di Livefyre, nelle cartelle deve essere abilitata l&#39;opzione Configurazioni cloud nelle relative proprietà. Le cartelle di configurazione vengono create e gestite nel browser di configurazione.
   >
   >Non è possibile creare un nome per una configurazione, a cui fa riferimento il percorso della cartella in cui si trova. Potete avere una sola configurazione per cartella.

1. Selezionate la scheda di configurazione Livefyre appena creata, quindi fate clic su **Proprietà**.

   ![create-livefyre-configuration2](assets/create-livefyre-configuration2.png)

1. Immettete le credenziali Livefyre della vostra organizzazione, quindi fate clic su **OK**.

   ![configure-aem2](assets/configure-aem2.png)

   Per accedere a queste informazioni, aprire lo studio Livefyre e passare a **Impostazioni > Impostazioni integrazione > Credenziali**.

   L&#39;istanza di AEM è ora configurata per l&#39;utilizzo di Livefyre e potete utilizzare le funzioni di integrazione.

### Personalizza integrazione con Single Sign-On {#customize-single-sign-on-integration}

Il pacchetto Livefyre per AEM include un&#39;integrazione out-of-the-box tra i profili AEM Communities e il servizio SSO di Livefyre.

Quando gli utenti accedono al sito AEM, vengono anche collegati ai componenti social di Livefyre. Quando un utente disconnesso tenta di utilizzare una funzione di componente Livefyre che richiede l’autenticazione (come il caricamento di una foto), il componente Livefyre avvia l’autenticazione dell’utente.

L&#39;integrazione di autenticazione predefinita potrebbe non essere perfetta per ogni sito. Per soddisfare al meglio il flusso di autenticazione nei modelli del sito, potete ignorare il delegato di autenticazione Livefyre predefinito in base alle vostre esigenze. Effettuate le seguenti operazioni:

1. Utilizzando CRXDE Lite, copiare */libs/social/integrations/livefyre/components/authorizablecomponent/authclientlib* in */apps/social/integrations/livefyre/components/authorizablecomponent/authclientlib*.
1. Modificate e salvate */apps/social/integrations/livefyre/components/authorizablecomponent/authclientlib/auth.js* per implementare un delegato Livefyre Auth che soddisfi le vostre esigenze.

   Per ulteriori informazioni sulla personalizzazione di un delegato di autenticazione, vedi Integrazione [](https://answers.livefyre.com/developers/identity-integration/)identità.

   Per ulteriori informazioni sulle librerie AEM, consultate [Utilizzo delle librerie](https://helpx.adobe.com/experience-manager/6-3/sites/developing/using/clientlibs.html)lato client.

## Utilizzo di Livefyre con AEM Sites {#use-livefyre-with-aem-sites}

### Aggiunta di componenti Livefyre a una pagina {#add-livefyre-components-to-a-page}

Prima di aggiungere componenti Livefyre a una pagina all’interno di Sites, è necessario abilitare Livefyre per la pagina ereditando una configurazione cloud Livefyre da una pagina padre o aggiungendo la configurazione direttamente alla pagina. Per informazioni su come includere i servizi cloud nel sito, consultate la vostra implementazione.

Una volta che Livefyre è abilitato per la pagina, i contenitori devono essere configurati per consentire ai componenti Livefyre. Consultate [Configurazione dei componenti in modalità](https://helpx.adobe.com/experience-manager/6-3/sites/authoring/using/default-components-designmode.html) Progettazione per istruzioni su come abilitare diversi componenti.

>[!NOTE]
>
>Le app che richiedono l&#39;autenticazione per la pubblicazione non funzionano finché l&#39;autenticazione non viene configurata in Customize Single Sign-On Integration (Personalizza integrazione con Single Sign-On).

1. Dal pannello laterale **Componenti** in modalità di progettazione, selezionate **Livefyre** dal menu per limitare l’elenco ai componenti Livefyre disponibili.

   ![livefyre add](assets/livefyre-add.png)

1. Selezionate un componente Livefyre e trascinatelo nella posizione desiderata sulla pagina.
1. Scegliete se creare una nuova app Livefyre o incorporarne una esistente.

   Se incorporate un&#39;app esistente, AEM vi chiede di selezionare l&#39;app. Se crei una nuova app, l&#39;app dovrà essere compilata prima che venga visualizzato il contenuto. L&#39;app verrà creata nel sito Livefyre e nella rete selezionati quando la configurazione cloud Livefyre sarà abilitata per la pagina.

   Per ulteriori informazioni sull’inserimento di componenti, consultate [Modifica del contenuto](https://helpx.adobe.com/experience-manager/6-3/sites/authoring/using/editing-content.html)della pagina.

### Modificare un componente Livefyre per una pagina AEM. {#edit-a-livefyre-component-for-an-aem-page}

In Livefyre Studio è possibile configurare e modificare solo un componente Livefyre. Da AEM:

1. Fate clic sul componente Livefyre da configurare.
1. Fate clic sull&#39;icona **Configura** (chiave inglese) per aprire la finestra di dialogo di configurazione.
1. Click **To edit this component, go to Livefyre Studio**.
1. Modificate l&#39;app in Livefyre Studio.

## Utilizzo di Livefyre con AEM Assets {#use-livefyre-with-aem-assets}

### Richiesta di diritti e importazione di UGC negli AEM Assets {#request-rights-and-import-ugc-into-aem-assets}

Potete importare contenuti generati dagli utenti di Twitter e Instagram (UGC) da Livefyre Studio ai AEM Assets mediante l’Importazione UGC. Dopo aver selezionato il contenuto da importare, è necessario richiedere i diritti al contenuto prima di completare l&#39;importazione.

>[!NOTE]
>
>Prima di utilizzare le risorse per importare UGC, è necessario configurare gli account Social Account e Rights Request in Livefyre Studio. Consultate [Impostazione: Rights Request](https://docs.adobe.com/content/help/en/livefyre/using/rights-requests/c-how-requesting-rights-works.html) for more information.

Per importare UGC in AEM Assets:

1. Dalla home page di AEM, passa a **Risorse > File**.
1. Fate clic su **Crea**, quindi su **Importa UGC.**

   ![livefyre-aem-import-ugc](assets/livefyre-aem-import-ugc.png)

1. Trova contenuto:

   * Da Livefyre, fate clic sulla scheda Libreria UGC. Utilizzate i filtri e cercate il contenuto presente nella libreria UGC.
   * Da Twitter e Instagram cliccando sulla scheda Twitter o Instagram. Utilizzate la ricerca o i filtri per trovare il contenuto.

1. Selezionate le risorse da importare. Le risorse selezionate vengono contate automaticamente e salvate nella scheda **Selezionato** .
1. **Facoltativo**: Fai clic sulla scheda **Selezionato** e controlla il contenuto UGC selezionato da importare.
1. Fai clic su **Avanti**.

   ![livefyre-aem-import-ugc2](assets/livefyre-aem-import-ugc2.png)

1. Per le richieste di diritti, scegliete una delle seguenti opzioni per ciascuna risorsa:

   Per Instagram:

   * **Richiedete manualmente i diritti** per ricevere un messaggio che possa essere copiato e incollato e inviato manualmente ai proprietari dei contenuti tramite Instagram.
   * **Attribuire manualmente i diritti** di contenuto per ignorare i diritti per singole risorse.

   >[!NOTE]
   >
   >A causa di aggiornamenti che influiscono sull&#39;aggregazione di contenuto da account utente non business, non è più possibile pubblicare commenti per conto dell&#39;utente o controllare automaticamente la presenza di risposte da parte dell&#39;autore. [Fai clic qui per saperne di più](https://developers.facebook.com/blog/post/2018/04/04/facebook-api-platform-product-changes/).

   ![livefyre-aem-import-ugc3-6-4](assets/livefyre-aem-import-ugc3-6-4.png)

   Per Twitter:

   * **Message Author** per inviare un messaggio al proprietario del contenuto in cui chiede i diritti per la risorsa.
   * **Attribuire manualmente i diritti** di contenuto per ignorare i diritti per singole risorse.


1. Fai clic su **Importa**.

   Se avete inviato una richiesta di diritti per Twitter, il proprietario del contenuto visualizzerà il messaggio di richiesta di diritti sul suo account:

   ![livefyre-aem-rights-request-twitter](assets/livefyre-aem-rights-request-twitter.png)

   >[!NOTE]
   >
   >Twitter ha dei limiti sulle richieste identiche provenienti dallo stesso account. Quando importate più risorse, modificate i messaggi singolarmente per evitare di essere contrassegnati.

1. Fate clic su **Fine** nell’angolo in alto a destra per completare il flusso di lavoro Richiesta diritti.

   Potete visualizzare lo stato di una richiesta di diritti in sospeso per una risorsa in Livefyre Studio. Se il contenuto è in attesa di una richiesta di diritti, la risorsa non verrà visualizzata in AEM Assets finché non verranno concessi i diritti. La risorsa viene visualizzata automaticamente nei AEM Assets quando viene concessa una richiesta di diritti.

   Per Instagram, dovete tenere traccia della risposta del proprietario del contenuto e concedere manualmente i diritti se gli sono stati concessi i diritti per il contenuto.

## Utilizzo di Livefyre con AEM Commerce {#use-livefyre-with-aem-commerce}

### Importazione di cataloghi di prodotti in Livefyre con AEM Commerce {#import-product-catalogs-into-livefyre-with-aem-commerce}

Gli utenti di AEM Commerce possono integrare facilmente il catalogo di prodotti esistente in Livefyre per attirare l&#39;utente nelle app di visualizzazione di Livefyre.

Dopo l&#39;importazione del catalogo prodotti, i prodotti vengono visualizzati in tempo reale nell&#39;istanza Livefyre. Se modificate o eliminate elementi nel catalogo prodotti di AEM Commerce, le modifiche vengono aggiornate automaticamente in LiveCycle.

1. Accertati che nell’istanza di AEM sia installato il pacchetto Livefyre più recente.
1. Dalla home page di AEM, andate ad **AEM Commerce**.
1. Create una nuova raccolta o utilizzate una raccolta esistente.
1. Passate il puntatore del mouse sulla raccolta e fate clic su Proprietà **** raccolta (icona matita).
1. Selezionate **Sincronizza con Livefyre**.
1. Compila il prefisso **pagina** Livefyre per collegare questa raccolta a una pagina specifica in AEM.

   Il prefisso della pagina definisce il percorso principale nell’ambiente in cui inizia la ricerca delle pagine di prodotto. Livefyre sceglie la prima pagina a cui è associato un prodotto corrispondente. Per ottenere pagine diverse per prodotti diversi, sono necessarie più raccolte.

## Matrice di supporto di AEM per le app Livefyre {#aem-support-matrix-for-livefyre-apps}

| App Livefyre | AEM 6.1 | AEM 6.2 | AEM 6.3 | AEM 6.4   |
|---|---|---|---|---|
| Carosello | X | X | X | X |
| Chat | X | X | X | X |
| Commenti | X | X | X | X |
| Filmstrip |  | X | X | X |
| LiveBlog | X | X | X | X |
| Mappa | X | X | X | X |
| Muro di supporto | X | X | X | X |
| Mosaico | X | X | X | X |
| Sondaggio |  | X | X | X |
| Recensioni |  | X | X | X |
| Scheda singola | X | X | X | X |
| Storify 2 |  | X | X | X |
| Tendenze |  | X | X | X |
| Pulsante Carica |  | X | X | X |

