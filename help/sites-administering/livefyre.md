---
title: Integrazione con Livefyre
seo-title: Integrazione con Livefyre
description: Scoprite come integrare le funzionalità di cura leader di settore di Livefyre con l'istanza di AEM 6.5, consentendo di pubblicare in pochi minuti contenuti generati dagli utenti dai social network al sito.
seo-description: Scoprite come integrare e utilizzare Livefyre con AEM 6.5.
uuid: c355705d-6e0f-4a33-aa1f-d2d1c818aac0
contentOwner: ind14750
content-type: reference
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: bb3fcb53-b8c3-4b1d-9125-4715f34ceb0b
translation-type: tm+mt
source-git-commit: ce64b148ba96cc64670aaf96c1b201bafa282b98
workflow-type: tm+mt
source-wordcount: '1661'
ht-degree: 4%

---


# Integrazione con Livefyre{#integrating-with-livefyre}

Scoprite come integrare le funzionalità di cura leader di settore di Livefyre con l&#39;istanza di AEM 6.5, consentendo di pubblicare in pochi minuti contenuti generati dagli utenti dai social network al sito.

## Guida introduttiva {#getting-started}

### Installare il pacchetto Livefyre per AEM {#install-livefyre-package-for-aem}

AEM 6.5 viene fornito con il pacchetto delle funzioni Livefyre 1.2.6 preinstallato. Questo pacchetto include solo un&#39;integrazione Livefyre limitata con  AEM Sites e deve essere disinstallato prima di installare un pacchetto aggiornato. Con il pacchetto più recente, potete provare l&#39;integrazione completa di Livefyre con AEM, inclusi Siti, Risorse e Commercio.

>[!NOTE]
>
>Alcune caratteristiche del pacchetto AEM-LF dipendono dal framework dei componenti sociali (SCF). Se utilizzate il feature pack di Livefyre come parte di un sito non appartenente a una community, dovete dichiarare *cq.social.scf* come una dipendenza nei clientlibs degli autori del sito Web. Se utilizzate il feature pack LF come parte di un sito Web di una community, questa dipendenza dovrebbe già essere dichiarata.

1. Nella home page AEM fare clic sull&#39;icona **Strumenti** nella barra a sinistra.
1. Andate a **Distribuzione > Pacchetti**.
1. In Gestione pacchetti, scorrete fino a visualizzare il pacchetto delle funzioni Livefyre preinstallato, quindi fate clic sul titolo **cq-social-livefyre-pkg-1.2.6.zip** per espandere le opzioni.
1. Fare clic su **Altro > Disinstalla**.

   ![livefyre-aem-uninstall-64](assets/livefyre-aem-uninstall-64.png)

1. Scaricate il pacchetto Livefyre da [Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).

1. Da Gestione pacchetti, installate il pacchetto scaricato. Per ulteriori informazioni sull&#39;utilizzo di distribuzione software e pacchetti in AEM, vedere [Come utilizzare i pacchetti](/help/sites-administering/package-manager.md)

   ![livefyre-aem4-6-4](assets/livefyre-aem4-6-4.png)

   Il pacchetto Livefyre-AEM è ora installato. Prima di iniziare a utilizzare le funzioni di integrazione, è necessario configurare AEM per l&#39;utilizzo di Livefyre.

   Per ulteriori informazioni e note sulla versione dei pacchetti di funzioni, vedere [Feature Pack](https://helpx.adobe.com/experience-manager/6-3/release-notes/feature-packs-release-notes.html).

### Configurare AEM per l&#39;utilizzo di Livefyre: Creare una cartella di configurazione {#configure-aem-to-use-livefyre-create-a-configuration-folder}

1. Dalla home page AEM fare clic sull&#39;icona **Strumenti** nella barra a sinistra, quindi passare a **Generale > Browser configurazione**.
   * Per ulteriori informazioni, consulta la documentazione del [browser di configurazione](/help/sites-administering/configurations.md).
1. Fare clic su **Crea** per aprire la finestra di dialogo Crea configurazione.
1. Assegnate un nome alla configurazione e selezionate la casella di controllo **Configurazioni cloud**.

   In questo modo verrà creata una cartella in **Strumenti > Distribuzione > Configurazione Livefyre** con il nome fornito.

   ![livefyre-aem-create-config-folder](assets/livefyre-aem-create-config-folder.png)

### Configurare AEM per l&#39;utilizzo di Livefyre: Creare una configurazione Livefyre {#configure-aem-to-use-livefyre-create-a-livefyre-configuration}

Configurate AEM per utilizzare le credenziali di licenza Livefyre della vostra azienda, consentendo la comunicazione tra Livefyre e AEM.

1. Dalla home page AEM, fare clic sull&#39;icona **Strumenti** nella barra a sinistra, quindi passare a **Distribuzione > Configurazione Livefyre**.
1. Selezionate la cartella di configurazione in cui desiderate creare una nuova configurazione Livefyre, quindi fate clic su **Crea**.

   ![create-livefyre-configuration1](assets/create-livefyre-configuration1.png)

   >[!NOTE]
   >
   >Per poter aggiungere le configurazioni di Livefyre, nelle cartelle deve essere abilitata l&#39;opzione Configurazioni cloud nelle relative proprietà. Le cartelle di configurazione vengono create e gestite nel [Browser di configurazione.](/help/sites-administering/configurations.md)
   >
   >Non è possibile creare un nome per una configurazione, a cui fa riferimento il percorso della cartella in cui si trova. Potete avere una sola configurazione per cartella.

1. Selezionate la scheda di configurazione Livefyre appena creata, quindi fate clic su **Properties**.

   ![create-livefyre-configuration2](assets/create-livefyre-configuration2.png)

1. Immettete le credenziali Livefyre della vostra organizzazione, quindi fate clic su **OK**.

   ![configure-aem2](assets/configure-aem2.png)

   Per accedere a queste informazioni, aprire lo studio Livefyre e passare a **Settings > Integration Settings > Credentials**.

   L&#39;istanza AEM è ora configurata per l&#39;utilizzo di Livefyre e potete utilizzare le funzioni di integrazione.

### Personalizza integrazione con Single Sign-On {#customize-single-sign-on-integration}

Il pacchetto Livefyre per AEM include un&#39;integrazione out-of-the-box tra  profili AEM Communities e il servizio SSO di Livefyre.

Quando gli utenti accedono al sito AEM, vengono anche collegati ai componenti social di Livefyre. Quando un utente disconnesso tenta di utilizzare una funzione di componente Livefyre che richiede l’autenticazione (come il caricamento di una foto), il componente Livefyre avvia l’autenticazione dell’utente.

L&#39;integrazione di autenticazione predefinita potrebbe non essere perfetta per ogni sito. Per soddisfare al meglio il flusso di autenticazione nei modelli del sito, potete ignorare il delegato di autenticazione Livefyre predefinito in base alle vostre esigenze. Effettuate le seguenti operazioni:

1. Utilizzando i CRXDE Lite, copiate */libs/social/integrations/livefyre/components/authorizablecomponent/authclientlib* in */apps/social/integrations/livefyre/components/authorizablecomponent/authclientlib*.
1. Modificate e salvate */apps/social/integrations/livefyre/components/authorizablecomponent/authclientlib/auth.js* per implementare un delegato di autenticazione Livefyre che soddisfi le vostre esigenze.

   Per ulteriori informazioni sulla personalizzazione di un delegato di autenticazione, vedere [Integrazione identità](https://answers.livefyre.com/developers/identity-integration/).

   Per ulteriori informazioni su AEM Clientlibs, vedere [Utilizzo di librerie lato client](https://helpx.adobe.com/experience-manager/6-3/sites/developing/using/clientlibs.html).

## Utilizzo di Livefyre con  AEM Sites {#use-livefyre-with-aem-sites}

### Aggiungere componenti Livefyre a una pagina {#add-livefyre-components-to-a-page}

Prima di aggiungere componenti Livefyre a una pagina all’interno di Sites, è necessario abilitare Livefyre per la pagina ereditando una configurazione cloud Livefyre da una pagina padre o aggiungendo la configurazione direttamente alla pagina. Per informazioni su come includere i servizi cloud nel sito, consultate la vostra implementazione.

Una volta che Livefyre è abilitato per la pagina, i contenitori devono essere configurati per consentire ai componenti Livefyre. Per istruzioni su come abilitare diversi componenti, vedere [Configurazione dei componenti in modalità Progettazione](https://helpx.adobe.com/experience-manager/6-3/sites/authoring/using/default-components-designmode.html).

>[!NOTE]
>
>Le app che richiedono l&#39;autenticazione per la pubblicazione non funzionano finché l&#39;autenticazione non viene configurata in Customize Single Sign-On Integration (Personalizza integrazione con Single Sign-On).

1. Dal pannello laterale **Componenti** in modalità di progettazione, selezionate **Livefyre** dal menu per limitare l&#39;elenco ai componenti Livefyre disponibili.

   ![livefyre add](assets/livefyre-add.png)

1. Selezionate un componente Livefyre e trascinatelo nella posizione desiderata sulla pagina.
1. Scegliete se creare una nuova app Livefyre o incorporarne una esistente.

   Se incorporate un&#39;app esistente, AEM vi chiede di selezionare l&#39;app. Se crei una nuova app, l&#39;app dovrà essere compilata prima che venga visualizzato il contenuto. L&#39;app verrà creata nel sito Livefyre e nella rete selezionati quando la configurazione cloud Livefyre sarà abilitata per la pagina.

   Per ulteriori informazioni sull&#39;inserimento di componenti, vedere [Modifica del contenuto della pagina](https://helpx.adobe.com/experience-manager/6-3/sites/authoring/using/editing-content.html).

### Modificare un componente Livefyre per una pagina AEM. {#edit-a-livefyre-component-for-an-aem-page}

In Livefyre Studio è possibile configurare e modificare solo un componente Livefyre. Da AEM:

1. Fate clic sul componente Livefyre da configurare.
1. Fare clic sull&#39;icona **Configura** (chiave inglese) per aprire la finestra di dialogo di configurazione.
1. Fare clic su **Per modificare questo componente, andare a Livefyre Studio**.
1. Modificate l&#39;app in Livefyre Studio.

## Utilizzo di Livefyre con  AEM Assets {#use-livefyre-with-aem-assets}

### Richiesta di diritti e importazione di UGC in  AEM Assets {#request-rights-and-import-ugc-into-aem-assets}

Potete importare contenuti generati dagli utenti di Twitter e Instagram (UGC) da Livefyre Studio a  AEM Assets tramite UGC Importer. Dopo aver selezionato il contenuto da importare, è necessario richiedere i diritti al contenuto prima di completare l&#39;importazione.

>[!NOTE]
>
>Prima di utilizzare le risorse per importare UGC, è necessario configurare gli account Social Account e Rights Request in Livefyre Studio. Vedere [Impostazione: Rights Requests](https://docs.adobe.com/content/help/en/livefyre/using/rights-requests/c-how-requesting-rights-works.html) per ulteriori informazioni.

Per importare UGC in  AEM Assets:

1. Dalla home page AEM, passare a **Risorse > File**.
1. Fare clic su **Crea**, quindi fare clic su **Importa UGC.**

   ![livefyre-aem-import-ugc](assets/livefyre-aem-import-ugc.png)

1. Trova contenuto:

   * Da Livefyre, fate clic sulla scheda Libreria UGC. Utilizzate i filtri e cercate il contenuto presente nella libreria UGC.
   * Da Twitter e Instagram cliccando sulla scheda Twitter o Instagram. Utilizzate la ricerca o i filtri per trovare il contenuto.

1. Selezionate le risorse da importare. Le risorse selezionate vengono conteggiate automaticamente e salvate nella scheda **Selezionato**.
1. **Facoltativo**: Fate clic sulla scheda  **** Selezionato e controllate il contenuto UGC selezionato da importare.
1. Fai clic su **Avanti**.

   ![livefyre-aem-import-ugc2](assets/livefyre-aem-import-ugc2.png)

1. Per le richieste di diritti, scegliete una delle seguenti opzioni per ciascuna risorsa:

   Per Instagram:

   * **Richiedi manualmente** diritti per ricevere un messaggio che possa essere copiato e incollato e inviato manualmente ai proprietari dei contenuti tramite Instagram.
   * **Attribuire manualmente i** diritti del contenuto per ignorare i diritti per le singole risorse.

   >[!NOTE]
   >
   >A causa di aggiornamenti che influiscono sull&#39;aggregazione di contenuto da account utente non business, non è più possibile pubblicare commenti per conto dell&#39;utente o controllare automaticamente la presenza di risposte da parte dell&#39;autore. [Fai clic qui per saperne di più](https://developers.facebook.com/blog/post/2018/04/04/facebook-api-platform-product-changes/).

   ![livefyre-aem-import-ugc3-6-4](assets/livefyre-aem-import-ugc3-6-4.png)

   Per Twitter:

   * **Messaggio** Autorizzatore per inviare un messaggio al proprietario del contenuto in cui si richiede di concedere i diritti alla risorsa.
   * **Attribuire manualmente i** diritti del contenuto per ignorare i diritti per le singole risorse.


1. Fai clic su **Importa**.

   Se avete inviato una richiesta di diritti per Twitter, il proprietario del contenuto visualizzerà il messaggio di richiesta di diritti sul suo account:

   ![livefyre-aem-rights-request-twitter](assets/livefyre-aem-rights-request-twitter.png)

   >[!NOTE]
   >
   >Twitter ha dei limiti sulle richieste identiche provenienti dallo stesso account. Quando importate più risorse, modificate i messaggi singolarmente per evitare di essere contrassegnati.

1. Fate clic su **Fine** nell’angolo in alto a destra per completare il flusso di lavoro Richiesta diritti.

   Potete visualizzare lo stato di una richiesta di diritti in sospeso per una risorsa in Livefyre Studio. Se il contenuto è in attesa di una richiesta di diritti, la risorsa non verrà visualizzata in  AEM Assets finché non verranno concessi i diritti. La risorsa viene visualizzata automaticamente in  AEM Assets quando viene concessa una richiesta di diritti.

   Per Instagram, dovete tenere traccia della risposta del proprietario del contenuto e concedere manualmente i diritti se gli sono stati concessi i diritti per il contenuto.

## Utilizzo di Livefyre con AEM Commerce {#use-livefyre-with-aem-commerce}

### Importazione di cataloghi di prodotti in Livefyre con AEM Commerce {#import-product-catalogs-into-livefyre-with-aem-commerce}

AEM utenti di Commerce possono integrare facilmente il catalogo di prodotti esistente in Livefyre per attirare l&#39;utente nelle app di visualizzazione di Livefyre.

Dopo l&#39;importazione del catalogo prodotti, i prodotti vengono visualizzati in tempo reale nell&#39;istanza Livefyre. Se modificate o eliminate elementi nel catalogo prodotti di AEM Commerce, le modifiche vengono aggiornate automaticamente in LiveCycle.

1. Accertatevi che nell’istanza AEM sia installato il pacchetto Livefyre più recente per AEM.
1. Dalla home page AEM, passare a **AEM Commerce**.
1. Create una nuova raccolta o utilizzate una raccolta esistente.
1. Passate il puntatore del mouse sulla raccolta e fate clic su **Proprietà raccolta** (icona matita).
1. Selezionare **Sincronizza con Livefyre**.
1. Compilate **Livefyre Page Prefix** per collegare questa raccolta a una pagina specifica in AEM.

   Il prefisso della pagina definisce il percorso principale nell’ambiente in cui inizia la ricerca delle pagine di prodotto. Livefyre sceglie la prima pagina a cui è associato un prodotto corrispondente. Per ottenere pagine diverse per prodotti diversi, sono necessarie più raccolte.

## Matrice di supporto AEM per le app Livefyre {#aem-support-matrix-for-livefyre-apps}

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

