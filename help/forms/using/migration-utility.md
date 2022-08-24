---
title: Migrare risorse e documenti AEM Forms
seo-title: Migrate AEM Forms assets and documents
description: L’utility Migration ti consente di migrare risorse e documenti AEM Forms da Forms 6.3 o versioni precedenti a AEM Forms 6.4.
seo-description: The Migration utility allows you to Migrate AEM Forms assets and documents from AEM 6.3 Forms or prior versions to AEM 6.4 Forms.
uuid: a3fdf940-7fc2-441c-91c8-ad66ba47e5f2
content-type: reference
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-strategy: max-2018
discoiquuid: 39dfef85-d047-4b6d-a0f5-92bd77df103b
docset: aem65
role: Admin
exl-id: 0f9aab7d-8e41-449a-804b-7e1bfa90befd
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1743'
ht-degree: 2%

---

# Migrare risorse e documenti AEM Forms{#migrate-aem-forms-assets-and-documents}

L&#39;utility di migrazione converte il [Risorse Forms adattive](../../forms/using/introduction-forms-authoring.md), [configurazioni cloud](/help/sites-developing/extending-cloud-config.md)e [Attività di gestione della corrispondenza](/help/forms/using/cm-overview.md) dal formato utilizzato nelle versioni precedenti al formato utilizzato in Forms 6.5. Quando esegui l&#39;utilità di migrazione, vengono migrati i seguenti elementi:

* Componenti personalizzati per i moduli adattivi
* Moduli adattivi e modelli di gestione della corrispondenza
* Configurazioni cloud
* Gestione della corrispondenza e risorse dei moduli adattivi

>[!NOTE]
>
>In caso di aggiornamento fuori luogo, per le risorse di Gestione Corrispondenza, puoi eseguire la migrazione ogni volta che importi le risorse. Per la migrazione alla gestione della corrispondenza è necessario che sia installato il pacchetto di compatibilità Forms.

## Approccio alla migrazione {#approach-to-migration}

È possibile [aggiornamento](../../forms/using/upgrade.md) all’ultima versione di AEM Forms 6.5 da AEM Forms 6.4, 6.3 o 6.2 oppure eseguire una nuova installazione. A seconda che sia stata aggiornata l&#39;installazione precedente o eseguita una nuova installazione, è necessario effettuare una delle seguenti operazioni:

**In caso di aggiornamento sul posto**

Se hai eseguito un aggiornamento sul posto, l’istanza aggiornata dispone già delle risorse e dei documenti. Tuttavia, prima di poter utilizzare le risorse e i documenti, dovrai installare [Pacchetto di compatibilità AEMFD](https://helpx.adobe.com/it/aem-forms/kb/aem-forms-releases.html) (include il pacchetto di compatibilità per la gestione della corrispondenza)

Quindi devi aggiornare le risorse e i documenti per [esecuzione dell&#39;utility Migration](#runningmigrationutility).

**In caso di installazione fuori luogo**

Se si tratta di un&#39;installazione obsoleta (nuova), prima di poter utilizzare le risorse e i documenti, sarà necessario installare [Pacchetto di compatibilità AEMFD](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) (include il pacchetto di compatibilità per la gestione della corrispondenza).

Quindi devi importare il pacchetto risorse (zip o cmp) nella nuova configurazione e quindi aggiornare le risorse e i documenti per [esecuzione dell&#39;utility Migration](#runningmigrationutility). Adobe consiglia di creare nuove risorse nella nuova configurazione solo dopo aver eseguito l&#39;utilità di migrazione.

A causa di [relativo alla compatibilità con le versioni precedenti](/help/sites-deploying/backward-compatibility.md) le modifiche, le posizioni di alcune cartelle in crx-repository vengono modificate. Esporta e importa manualmente le dipendenze (librerie e risorse personalizzate) dalla configurazione precedente all’ambiente nuovo.

## Leggi prima di procedere con la migrazione {#prerequisites}

Per le attività di gestione della corrispondenza:

* Per le risorse importate dalla piattaforma precedente, viene aggiunta una proprietà : **fd:version=1.0**.
* A partire AEM 6.1 Forms, i commenti non sono disponibili. I commenti aggiunti in precedenza sono disponibili nelle risorse ma non sono visibili automaticamente nell’interfaccia. Per rendere visibili i commenti, è necessario personalizzare la proprietà ExtendedProperties nell’interfaccia utente di AEM Forms.
* In alcune delle versioni precedenti, come LiveCycle ES4, il testo veniva modificato utilizzando Flex RichTextEditor, ma a partire da AEM 6.1 Forms viene utilizzato l’editor di HTML. A causa di questo rendering e dell’aspetto dei font, delle dimensioni dei font e dei margini dei font, le versioni precedenti dell’interfaccia utente di Author potrebbero essere diverse. Tuttavia, durante il rendering le lettere hanno lo stesso aspetto.
* Gli elenchi nei moduli di testo vengono migliorati e ora vengono sottoposti a rendering in modo diverso. Ci possono essere differenze visive. È consigliabile eseguire il rendering e visualizzare le lettere in cui si utilizzano gli elenchi nei moduli di testo.
* Poiché i moduli di contenuto immagine sono convertiti in risorse DAM e i layout e i frammenti vengono aggiunti ai moduli durante la migrazione, la proprietà Updated By per per questi moduli diventa admin.
* La cronologia delle versioni delle risorse non viene migrata e non è disponibile dopo la migrazione. Viene mantenuta la cronologia delle versioni successive dopo la migrazione.
* Lo stato Ready to Publish (Pronto per la pubblicazione) è obsoleto a partire da Forms 6.1, pertanto tutte le risorse nello stato Ready to Publish (Pronto per la pubblicazione) vengono modificate in Modified state (Stato modificato).
* Poiché l’interfaccia utente è aggiornata in AEM Forms 6.3, anche i passaggi per eseguire le personalizzazioni sono diversi. Se effettui la migrazione da una versione precedente alla 6.3, devi ripristinare la personalizzazione.
* I frammenti di layout si spostano da /content/apps/cm/layouts/fragmentlayouts/1001 a /content/apps/cm/modules/fragmentlayouts. Il riferimento al dizionario dati nelle risorse visualizza il percorso del dizionario dati anziché il nome.
* Eventuali spazi tabulazione utilizzati per l’allineamento nei moduli di testo devono essere regolati. Per ulteriori informazioni, consulta [Gestione Corrispondenza - Utilizzo della spaziatura tra le tabulazioni per disporre il testo](https://helpx.adobe.com/aem-forms/kb/cm-tab-spacing-limitations.html).
* Le configurazioni del compositore risorse cambiano nelle configurazioni di Gestione Corrispondenza.
* Le risorse vengono spostate in cartelle con nomi quali Testo esistente ed Elenco esistente.

## Utilizzo dell’utility Migration {#using-the-migration-utility}

### Esecuzione dell&#39;utility di migrazione {#runningmigrationutility}

Esegui l’utility Migrazione prima di apportare modifiche alle risorse o di crearle. Si consiglia di non eseguire l&#39;utilità dopo aver apportato modifiche o creato risorse. Assicurati che l’interfaccia utente Gestione Corrispondenza o Risorse Forms adattive non sia aperta durante l’esecuzione del processo di migrazione.

Quando si esegue l&#39;utilità di migrazione per la prima volta, viene creato un registro con il percorso e il nome seguenti: `\[aem-installation-directory]\cq-quickstart\logs\aem-forms-migration.log`. Questo registro continua ad essere aggiornato con le informazioni relative alla gestione della corrispondenza e alla migrazione adattiva di Forms, ad esempio lo spostamento delle risorse.

>[!NOTE]
>
>Prima di eseguire l&#39;utility di migrazione, assicurati di aver effettuato un backup del tuo archivio crx.

1. In una sessione del browser, accedi AEM’istanza di authoring come Amministratore.

1. Apri il seguente URL nel browser:

   https://[*hostname*]:[*porta*]/[*context_path*]/libs/fd/foundation/gui/content/migration.html

   Il browser visualizza quattro opzioni:

   * Migrazione risorse AEM Forms
   * Migrazione adattata dei componenti personalizzati Forms
   * Migrazione dei modelli Forms adattivi
   * Migrazione configurazioni AEM Forms Cloud

1. Per eseguire la migrazione, procedi come segue:

   * Per eseguire la migrazione **assets**, tocca Migrazione risorse AEM Forms e, nella schermata successiva, tocca **Avvia migrazione**. Viene eseguita la migrazione dei seguenti elementi:

      * Moduli adattivi
      * Frammenti di documento
      * Temi
      * Lettere
      * Dizionari dati

   >[!NOTE]
   >
   >Durante la migrazione delle risorse, potresti trovare messaggi di avviso come &quot;Conflict found for...&quot; (Conflitto trovato per...). Tali messaggi indicano che non è stato possibile eseguire la migrazione delle regole per alcuni dei componenti nei moduli adattivi. Ad esempio, se il componente ha un evento con entrambe le regole e gli script, se le regole si verificano dopo uno script, nessuna delle regole per il componente viene migrata. È possibile [eseguire la migrazione di tali regole aprendo l’editor di regole](#migrate-rules) nella creazione di moduli adattivi.

   * Per migrare i componenti personalizzati dei moduli adattivi, tocca **Migrazione adattata dei componenti personalizzati Forms** e nella pagina Migrazione componenti personalizzati , tocca **Avvia migrazione**. Viene eseguita la migrazione dei seguenti elementi:

      * Componenti personalizzati scritti per Forms adattivo
      * Eventuali sovrapposizioni dei componenti.
   * Per migrare i modelli di modulo adattivo, tocca **Migrazione adattata dei modelli Forms** e nella pagina Migrazione componenti personalizzati , tocca **Avvia migrazione**. Viene eseguita la migrazione dei seguenti elementi:

      * Modelli di modulo adattivo creati in `/apps` o `/conf` utilizzando AEM Editor modelli.
   * Esegui la migrazione dei servizi di configurazione di AEM Forms Cloud per sfruttare il nuovo paradigma di servizio cloud consapevole del contesto, che include l’interfaccia utente touch (in `/conf`). Quando esegui la migrazione dei servizi di configurazione di AEM Forms Cloud, i servizi cloud in `/etc` vengono spostati in `/conf`. Se non disponi di personalizzazioni dei servizi cloud che dipendono dai percorsi precedenti (`/etc`), si consiglia di eseguire l&#39;utility di migrazione subito dopo l&#39;aggiornamento alla versione 6.5 e di utilizzare la configurazione cloud Touch UI per qualsiasi ulteriore lavoro. Se disponi di personalizzazioni esistenti per i servizi cloud, continua a utilizzare l’interfaccia classica per l’aggiornamento della configurazione fino a quando le personalizzazioni non vengono aggiornate per allinearle ai percorsi migrati (`/conf`), quindi esegui l&#39;utility di migrazione.

   Per eseguire la migrazione **Servizi cloud AEM Forms**, che includono quanto segue, tocca Migrazione configurazione cloud AEM Forms (la migrazione della configurazione cloud è indipendente dal pacchetto di compatibilità AEM FD), tocca Migrazione configurazioni cloud AEM Forms e quindi nella pagina Migrazione configurazione , tocca **Avvia migrazione**:

   * Servizi cloud del modello dati modulo

      * Percorso di origine: `/etc/cloudservices/fdm`
      * Percorso di destinazione: `/conf/global/settings/cloudconfigs/fdm`
   * Recaptcha

      * Percorso di origine: `/etc/cloudservices/recaptcha`
      * Percorso di destinazione: `/conf/global/settings/cloudconfigs/recaptcha`
   * Adobe Sign

      * Percorso di origine: `/etc/cloudservices/echosign`
      * Percorso di destinazione: `/conf/global/settings/cloudconfigs/echosign`
   * Servizi cloud di Typekit

      * Percorso di origine: `/etc/cloudservices/typekit`
      * Percorso di destinazione: `/conf/global/settings/cloudconfigs/typekit`

   La finestra del browser mostra quanto segue durante il processo di migrazione:

   * Quando le risorse vengono aggiornate: Aggiornamento delle risorse completato.
   * Una volta completata la migrazione: Migrazione delle risorse completata.

   Quando viene eseguita, l’utility di migrazione effettua le seguenti operazioni:

   * **Aggiunge i tag alle risorse**: Aggiunge il tag &quot;Gestione della corrispondenza : Risorse migrate&quot; / &quot;Forms adattivo: Risorse migrate&quot;. alle risorse migrate, in modo che gli utenti possano identificare le risorse migrate. Quando esegui l&#39;utility Migrazione, tutte le risorse esistenti nel sistema vengono contrassegnate come Migrazione.
   * **Genera tag**: Le categorie e le sottocategorie presenti nel sistema precedente vengono create come tag e quindi tali tag sono associati alle relative risorse di Gestione Corrispondenza in AEM. Ad esempio, come tag vengono generati una categoria (attestazioni) e una sottocategoria (attestazioni) di un modello di lettera.










1. Al termine dell&#39;esecuzione dell&#39;utility di migrazione, procedi al [compiti di gestione](#housekeepingtasks).

#### Eseguire la migrazione delle regole utilizzando l’editor di regole {#migrate-rules}

È possibile migrare questi componenti aprendoli nell’editor di regole nell’editor di Forms adattivo.

* Per eseguire la migrazione di regole e script (non necessari se si esegue l’aggiornamento dalla versione 6.3) nei componenti personalizzati, tocca Migrazione componenti personalizzati Forms adattivi e, nella schermata successiva, tocca Avvia migrazione. Viene eseguita la migrazione dei seguenti elementi:

   * Regole e script creati con l’editor di regole (6.1 FP1 e versioni successive)

   * Script creati utilizzando la scheda Script nell’interfaccia utente di 6.1 e versioni precedenti

* Per migrare i modelli (non necessari se si esegue l’aggiornamento dalla versione 6.3 e 6.4), tocca Migrazione modelli di Forms adattivi e, nella schermata successiva, tocca Avvia migrazione. Viene eseguita la migrazione dei seguenti elementi:

   * Modelli precedenti - i modelli di moduli adattivi creati in /apps utilizzando AEM 6.1 Forms o versioni precedenti. Ciò include gli script definiti nei componenti del modello.

   * Nuovi modelli: modelli di moduli adattivi creati utilizzando l’editor di modelli in /conf. Ciò include la migrazione di regole e script creati utilizzando l&#39;editor di regole.

### Attività di gestione delle famiglie dopo l&#39;esecuzione dell&#39;utility di migrazione {#housekeepingtasks}

Dopo aver eseguito l&#39;utility Migrazione, si occupa delle seguenti attività di gestione:

1. Assicurati che la versione XFA dei layout di layout e frammenti sia 3.3 o successiva. Se utilizzi layout e layout di frammenti di una versione precedente, potrebbero esserci problemi nel rendering della lettera. Per aggiornare la versione di un XFA precedente alla versione più recente, completa i passaggi seguenti:

   1. [Scarica XFA come file zip](../../forms/using/import-export-forms-templates.md#p-import-and-export-assets-in-correspondence-management-p) dall’interfaccia utente di Forms.
   1. Estrai il file.
   1. Apri il file XFA nella versione più recente di Designer e salvalo. La versione di XFA viene aggiornata a quella più recente.
   1. Carica l&#39;XFA nell&#39;interfaccia utente di Forms.

1. Pubblica tutte le risorse pubblicate nel sistema precedente prima della migrazione. L’utility di migrazione aggiorna le risorse solo sull’istanza di authoring e per aggiornare le risorse nell’istanza o nelle istanze di pubblicazione è necessario pubblicare le risorse.

1. In AEM Forms 6.4 e 6.5, alcuni dei diritti dei gruppi di utenti dei moduli vengono modificati. Se desideri che uno qualsiasi dei tuoi utenti sia in grado di caricare XDP e Adaptive Forms contenenti script o utilizzare l&#39;editor di codice, devi aggiungerli al gruppo utenti di forms-power-users. Allo stesso modo, gli autori di modelli non possono più utilizzare l&#39;editor di codice nell&#39;editor di regole. Per consentire agli utenti di utilizzare l’editor di codice, aggiungili al gruppo af-template-script-writers. Per istruzioni su come aggiungere utenti ai gruppi, consulta [Gestione di utenti e gruppi di utenti](/help/communities/users.md).
