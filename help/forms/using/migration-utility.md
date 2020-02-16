---
title: Migrazione di risorse e documenti AEM Forms
seo-title: Migrazione di risorse e documenti AEM Forms
description: L’utility di migrazione consente di migrare risorse e documenti AEM Forms da AEM 6.3 Forms o versioni precedenti a AEM 6.4 Forms.
seo-description: L’utility di migrazione consente di migrare risorse e documenti AEM Forms da AEM 6.3 Forms o versioni precedenti a AEM 6.4 Forms.
uuid: a3fdf940-7fc2-441c-91c8-ad66ba47e5f2
content-type: reference
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-strategy: max-2018
discoiquuid: 39dfef85-d047-4b6d-a0f5-92bd77df103b
docset: aem65
translation-type: tm+mt
source-git-commit: 3226edb575de3d9f8bff53f5ca81e2957f37c544

---


# Migrazione di risorse e documenti AEM Forms{#migrate-aem-forms-assets-and-documents}

L’utility Migrazione converte le risorse [Moduli](../../forms/using/introduction-forms-authoring.md)adattivi, le configurazioni [](/help/sites-developing/extending-cloud-config.md)cloud e le risorse [Gestione](/help/forms/using/cm-overview.md) corrispondenza dal formato utilizzato nelle versioni precedenti al formato utilizzato in AEM 6.5 Forms. Quando si esegue l&#39;utility di migrazione, vengono migrati i seguenti elementi:

* Componenti personalizzati per i moduli adattivi
* Moduli adattivi e modelli di gestione della corrispondenza
* Configurazioni cloud
* Gestione della corrispondenza e risorse per moduli adattivi

>[!NOTE]
>
>In caso di aggiornamento non aggiornato, per le risorse di Gestione della corrispondenza potete eseguire la migrazione ogni volta che importate le risorse. Per la migrazione alla gestione della corrispondenza è necessario che sia installato il pacchetto di compatibilità dei moduli.

## Approccio alla migrazione {#approach-to-migration}

È possibile [effettuare l’aggiornamento](../../forms/using/upgrade.md) alla versione più recente di AEM Forms 6.5 da AEM Forms 6.4, 6.3 o 6.2 oppure eseguire una nuova installazione. A seconda se avete aggiornato l’installazione precedente o eseguito una nuova installazione, dovete effettuare una delle seguenti operazioni:

**In caso di aggiornamento locale**

Se avete eseguito un aggiornamento locale, l’istanza aggiornata dispone già delle risorse e dei documenti. Tuttavia, prima di poter utilizzare le risorse e i documenti, dovrete installare il pacchetto [di compatibilità](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) AEMFD (compreso il pacchetto di compatibilità per la gestione della corrispondenza)

Quindi devi aggiornare le risorse e i documenti [eseguendo l&#39;utility](#runningmigrationutility)di migrazione.

**In caso di installazione fuori luogo**

Se si tratta di un&#39;installazione obsoleta (fresca), prima di poter utilizzare le risorse e i documenti, dovrete installare il pacchetto [Compatibilità](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) AEMFD (compreso il pacchetto Compatibilità di gestione della corrispondenza).

Quindi devi importare il pacchetto di risorse (zip o cmp) nella nuova configurazione e quindi aggiornare le risorse e i documenti [eseguendo l’utility](#runningmigrationutility)Migrazione. Adobe consiglia di creare nuove risorse nella nuova configurazione solo dopo aver eseguito l’utility di migrazione.

A causa di [precedenti modifiche relative](/help/sites-deploying/backward-compatibility.md) alla compatibilità, vengono modificati i percorsi di alcune cartelle nell’archivio crx. Esportate e importate manualmente le dipendenze (librerie e risorse personalizzate) dalla configurazione precedente all’ambiente nuovo.

## Leggi prima di procedere con la migrazione {#prerequisites}

Per le risorse Gestione corrispondenza:

* Per le risorse importate dalla piattaforma precedente, viene aggiunta una proprietà: **fd:version=1.0**.
* A partire da AEM 6.1 Forms, i commenti non sono disponibili. I commenti aggiunti in precedenza sono disponibili nelle risorse ma non sono automaticamente visibili nell’interfaccia. Per rendere visibili i commenti, è necessario personalizzare la proprietà ExtendedProperties nell&#39;interfaccia utente di AEM Forms.
* In alcune versioni precedenti, come LiveCycle ES4, il testo veniva modificato utilizzando Flex RichTextEditor, ma da AEM 6.1 Forms viene utilizzato l’editor HTML. A causa di questo rendering e dell&#39;aspetto dei font, le dimensioni e i margini dei font possono essere diversi dalle versioni precedenti dell&#39;interfaccia utente di Author. Tuttavia, durante il rendering le lettere hanno lo stesso aspetto.
* Gli elenchi nei moduli di testo vengono migliorati e ora il rendering è diverso. Potrebbero esserci delle differenze visive. È consigliabile eseguire il rendering e visualizzare le lettere in cui si utilizzano gli elenchi nei moduli di testo.
* Poiché i moduli di contenuto immagine sono convertiti in risorse DAM, layout e frammenti vengono aggiunti ai moduli durante la migrazione, la proprietà Aggiornato da di per questi moduli diventa admin.
* La cronologia delle versioni delle risorse non viene migrata e non è disponibile dopo la migrazione. La cronologia successiva della versione viene mantenuta dopo la migrazione.
* Lo stato Pronto per la pubblicazione è obsoleto a partire da AEM 6.1 Forms, pertanto tutte le risorse nello stato Pronto per la pubblicazione vengono modificate in Stato Modificato.
* Poiché l&#39;interfaccia utente è aggiornata in AEM Forms 6.3, anche i passaggi per eseguire le personalizzazioni sono diversi. Se state eseguendo la migrazione da una versione precedente alla 6.3, dovete ripristinare la personalizzazione.
* I frammenti di layout si spostano da /content/apps/cm/layouts/fragmentlayouts/1001 a /content/apps/cm/module/fragmentlayouts. Il riferimento al dizionario dati nelle risorse visualizza il percorso del dizionario dati invece del nome.
* Eventuali spazi tabulazione utilizzati per l&#39;allineamento nei moduli di testo devono essere regolati. Per ulteriori informazioni, consultate Gestione della [corrispondenza - Utilizzo della spaziatura tra le schede per disporre il testo](https://helpx.adobe.com/aem-forms/kb/cm-tab-spacing-limitations.html).
* Le configurazioni di Asset Composer (Compositore risorse) vengono modificate nelle configurazioni di Correspondence Management.
* Le risorse vengono spostate in cartelle con nomi quali Testo esistente ed Elenco esistente.

## Utilizzo dell&#39;utilità di migrazione {#using-the-migration-utility}

### Esecuzione dell&#39;utility di migrazione {#runningmigrationutility}

Eseguite l’utility di migrazione prima di apportare modifiche alle risorse o di crearle. È consigliabile non eseguire l&#39;utility dopo aver apportato modifiche o creato risorse. Accertatevi che l’interfaccia utente Gestione corrispondenza o Risorse moduli adattivi non sia aperta durante il processo di migrazione.

Quando si esegue l&#39;utility di migrazione per la prima volta, viene creato un registro con il percorso e il nome seguenti: \[directory-installazione-aem]\cq-quickstart\logs\aem-forms-migration.log. Questo registro continua ad essere aggiornato con le informazioni sulla gestione della corrispondenza e sulla migrazione dei moduli adattivi, come lo spostamento delle risorse.

>[!NOTE]
>
>Prima di eseguire l&#39;utility di migrazione, assicurarsi di aver eseguito un backup del repository crx.

1. In una sessione del browser, accedi all’istanza di creazione di AEM come amministratore.

1. Aprite il seguente URL nel browser:

   https://[*hostname*]:[*port*]/[*context_path*]/libs/fd/foundation/gui/content/migration.html

   Il browser presenta quattro opzioni:

   * Migrazione risorse AEM Forms
   * Migrazione di componenti personalizzati per moduli adattivi
   * Migrazione dei modelli di moduli adattivi
   * Migrazione configurazioni AEM Forms Cloud

1. Per eseguire la migrazione, effettuate le seguenti operazioni:

   * Per migrare **le risorse**, tocca Migrazione risorse AEM Forms e, nella schermata successiva, tocca **Avvia migrazione**. Viene eseguita la migrazione dei seguenti elementi:

      * Moduli adattivi
      * Frammenti di documenti
      * Temi
      * Lettere
      * Dizionari dati
   >[!NOTE]
   >
   >Durante la migrazione delle risorse, è possibile che vengano visualizzati messaggi di avviso come &quot;Conflitto trovato per...&quot;. Tali messaggi indicano che non è stato possibile migrare le regole per alcuni componenti nei moduli adattivi. Ad esempio, se il componente ha un evento con regole e script, se le regole si verificano dopo uno script nessuna delle regole per il componente viene migrata. Tuttavia, tali regole possono essere migrate aprendo l’editor delle regole nella creazione di moduli adattivi.
   >
   >
   >Per migrare questi componenti è necessario aprirli nell&#39;Editor regole nell&#39;editor moduli adattivi.
   >
   >
   >
   >    * Per migrare regole e script (non richiesti se si esegue l&#39;aggiornamento dalla versione 6.3) in componenti personalizzati, toccare Migrazione componenti personalizzati per moduli adattivi e, nella schermata successiva, toccare Avvia migrazione. Viene eseguita la migrazione dei seguenti elementi: >
      >
      >
      >        

      * Regole e script creati con l&#39;editor di regole (6.1 FP1 e versioni successive)
      >        * Script creati utilizzando la scheda Script dell&#39;interfaccia utente 6.1 e versioni precedenti
   >
   >
   >    * Per migrare i modelli (non richiesti se si esegue l&#39;aggiornamento da 6.3 e 6.4), toccare Migrazione modelli di moduli adattivi e, nella schermata successiva, toccare Avvia migrazione. Viene eseguita la migrazione dei seguenti elementi:
      >
      >
      >
      >        


      * Vecchi modelli: i modelli di moduli adattivi creati in /apps con AEM 6.1 Forms o versioni precedenti. Sono inclusi gli script definiti nei componenti modello.
      >        * Nuovi modelli: modelli di moduli adattivi creati utilizzando l&#39;editor modelli in /conf. Ciò include la migrazione di regole e script creati utilizzando l&#39;editor di regole.


   * Per migrare i componenti personalizzati per moduli adattivi, toccate Migrazione **componenti personalizzati per moduli** adattivi e, nella pagina Migrazione componenti personalizzati, toccate **Avvia migrazione**. Viene eseguita la migrazione dei seguenti elementi:

      * Componenti personalizzati creati per i moduli adattivi
      * Eventuali sovrapposizioni di componenti.
   * Per migrare i modelli di modulo adattivo, toccare Migrazione **dei modelli di moduli** adattivi e nella pagina Migrazione dei componenti personalizzati toccare **Avvia migrazione**. Viene eseguita la migrazione dei seguenti elementi:

      * Modelli di moduli adattivi creati con /apps o /conf utilizzando AEM Template Editor.
   * Migra i servizi di configurazione di AEM Forms Cloud per sfruttare il nuovo paradigma del servizio cloud basato sul contesto, che include l&#39;interfaccia touch (in /conf). Quando si esegue la migrazione dei servizi di configurazione cloud AEM Forms, i servizi cloud in /etc vengono spostati in /conf. Se non disponete di personalizzazioni dei servizi cloud che dipendono dai percorsi legacy (/etc), è consigliabile eseguire l&#39;utility di migrazione subito dopo l&#39;aggiornamento alla versione 6.5 e utilizzare l&#39;interfaccia utente touch della configurazione cloud per qualsiasi ulteriore lavoro. Se disponete di personalizzazioni dei servizi cloud esistenti, continuate a utilizzare l&#39;interfaccia classica durante l&#39;aggiornamento fino a quando le personalizzazioni non vengono aggiornate in modo da allinearsi ai percorsi migrati (/conf) ed eseguire l&#39;utility di migrazione.
   Per migrare i servizi **cloud di** AEM Forms, che includono quanto segue, tocca Migrazione configurazione cloud AEM Forms (la migrazione della configurazione cloud è indipendente dal pacchetto di compatibilità AEM FD), tocca Migrazione delle configurazioni cloud AEM Forms e, nella pagina Migrazione configurazione, tocca **Avvia migrazione**:

   * Servizi cloud per il modello dati modulo

      * Percorso di origine: /etc/cloudservices/fdm
      * Percorso di destinazione: /conf/global/settings/cloudconfigs/fdm
   * Recaptcha

      * Percorso di origine: /etc/cloudservices/acquistcha
      * Percorso di destinazione: /conf/global/settings/cloudconfigs/ricontcha
   * Adobe Sign

      * Percorso di origine: /etc/cloudservices/echosign
      * Percorso di destinazione: /conf/global/settings/cloudconfigs/echosign
   * Servizi cloud di Typekit

      * Percorso di origine: /etc/cloudservices/typekit
      * Percorso di destinazione: /conf/global/settings/cloudconfigs/typekit
   La finestra del browser visualizza quanto segue durante il processo di migrazione:

   * Quando le risorse vengono aggiornate: Risorse aggiornate.
   * Una volta completata la migrazione: Migrazione delle risorse completata.
   Una volta eseguita, l&#39;utilità di migrazione effettua le seguenti operazioni:

   * **Aggiunge i tag alle risorse**: Aggiunge il tag &quot;Correspondence Management: Risorse migrate&quot; / &quot;Moduli adattivi: Risorse migrate&quot;. alle risorse migrate, in modo che gli utenti possano identificare le risorse migrate. Quando eseguite l&#39;utility Migrazione, tutte le risorse esistenti nel sistema vengono contrassegnate come Migrate.
   * **Genera tag**: Le categorie e le sottocategorie presenti nel sistema precedente vengono create come tag, quindi questi tag sono associati alle risorse di gestione della corrispondenza pertinenti in AEM. Ad esempio, come tag vengono generati una categoria (attestazioni) e una sottocategoria (attestazioni) di un modello di lettera.

















1. Al termine dell&#39;esecuzione dell&#39;utility di migrazione, procedere alle attività di [gestione](#housekeepingtasks).

### Attività di pulizia dopo l&#39;esecuzione dell&#39;utility di migrazione {#housekeepingtasks}

Dopo aver eseguito l&#39;utility Migrazione, effettua le seguenti operazioni di pulizia: [](../../forms/using/import-export-forms-templates.md)

1. Verificate che la versione XFA di layout e layout di frammenti sia 3.3 o successiva. Se si utilizzano layout e layout di frammenti di una versione precedente, potrebbero verificarsi problemi durante il rendering della lettera. Per aggiornare la versione di un XFA precedente all&#39;ultima versione, effettua i seguenti passaggi:

   1. [Scaricare l&#39;XFA come file](../../forms/using/import-export-forms-templates.md#p-import-and-export-assets-in-correspondence-management-p) ZIP dall&#39;interfaccia utente di Forms.
   1. Estrarre il file.
   1. Aprire il file XFA nella versione più recente di Designer e salvarlo. La versione di XFA viene aggiornata alla versione più recente.
   1. Caricare l&#39;XFA nell&#39;interfaccia utente di Forms.

1. Pubblicate tutte le risorse pubblicate nel sistema precedente prima della migrazione. L’utility di migrazione aggiorna le risorse solo nell’istanza di creazione e per aggiornare le risorse nell’istanza o nelle istanze di pubblicazione, è necessario pubblicare le risorse.
1. In AEM Forms 6.4 e 6.5, alcuni dei diritti dei gruppi di utenti dei moduli vengono modificati. Se si desidera che gli utenti siano in grado di caricare i file XDP e i moduli adattivi contenenti script o di utilizzare l&#39;editor di codice, è necessario aggiungerli al gruppo di utenti che forniscono moduli. Analogamente, gli autori dei modelli non possono più utilizzare l&#39;editor di codice nell&#39;Editor regole. Per consentire agli utenti di utilizzare l&#39;editor di codice, aggiungeteli al gruppo af-template-script-writers. Per istruzioni sull’aggiunta di utenti ai gruppi, consultate [Gestione di utenti e gruppi](/help/communities/users.md)di utenti.

