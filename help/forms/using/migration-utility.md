---
title: Migrare risorse e documenti AEM Forms
description: L’utility di migrazione consente di migrare risorse e documenti Forms di Adobe Experience Manager (AEM) da AEM 6.3 Forms o versioni precedenti a AEM 6.4 Forms.
content-type: reference
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-strategy: max-2018
docset: aem65
role: Admin,User
exl-id: 0f9aab7d-8e41-449a-804b-7e1bfa90befd
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1736'
ht-degree: 1%

---

# Migrare risorse e documenti AEM Forms{#migrate-aem-forms-assets-and-documents}

L&#39;utilità di migrazione converte le [risorse di Forms adattivi](../../forms/using/introduction-forms-authoring.md), le [configurazioni cloud](/help/sites-developing/extending-cloud-config.md) e le [risorse di gestione della corrispondenza](/help/forms/using/cm-overview.md) dal formato utilizzato nelle versioni precedenti al formato utilizzato in Adobe Experience Manager (AEM) 6.5 Forms. Quando si esegue l&#39;utilità di migrazione, viene eseguita la migrazione dei seguenti elementi:

* Componenti personalizzati per moduli adattivi
* Moduli adattivi e modelli per la gestione della corrispondenza
* Configurazioni cloud
* Risorse per la gestione della corrispondenza e i moduli adattivi

>[!NOTE]
>
>In caso di aggiornamento fuori sede, per le risorse di Gestione della corrispondenza puoi eseguire la migrazione ogni volta che importi le risorse. Per la migrazione di Gestione corrispondenza, è necessario che sia installato il pacchetto di compatibilità di Forms.

## Approccio alla migrazione {#approach-to-migration}

È possibile [aggiornare](../../forms/using/upgrade.md) alla versione più recente di AEM Forms 6.5 da AEM Forms 6.4, 6.3 o 6.2 o da una nuova installazione. A seconda che sia stata aggiornata l&#39;installazione precedente o sia stata eseguita una nuova installazione, è necessario eseguire una delle operazioni seguenti:

**Se è presente un aggiornamento sul posto**

Se hai eseguito un aggiornamento sul posto, l’istanza aggiornata dispone già delle risorse e dei documenti. Tuttavia, prima di poter utilizzare le risorse e i documenti, è necessario installare il [pacchetto di compatibilità AEMFD](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en) (incluso il pacchetto di compatibilità per Gestione corrispondenza)

È quindi necessario aggiornare le risorse e i documenti [eseguendo l&#39;utilità di migrazione](#runningmigrationutility).

**In caso di installazione fuori sede**

Se si tratta di un&#39;installazione fuori sede (nuova), prima di poter utilizzare le risorse e i documenti, è necessario installare il [pacchetto di compatibilità AEMFD](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en) (incluso il pacchetto di compatibilità per Gestione corrispondenza).

Quindi devi importare il pacchetto di risorse (zip o cmp) nella nuova configurazione e quindi aggiornare le risorse e i documenti eseguendo [l&#39;utilità di migrazione](#runningmigrationutility). L’Adobe consiglia di creare le risorse nella nuova configurazione solo dopo aver eseguito l’utility di migrazione.

A causa di [modifiche relative alla compatibilità con le versioni precedenti](/help/sites-deploying/backward-compatibility.md), vengono modificate le posizioni di alcune cartelle nell&#39;archivio crx. Esportare e importare manualmente le dipendenze (librerie e risorse personalizzate) dalla configurazione precedente a un nuovo ambiente.

## Prima di procedere con la migrazione {#prerequisites}

Per le risorse di Gestione della corrispondenza:

* Per le risorse importate dalla piattaforma precedente, viene aggiunta una proprietà: **fd:version=1.0**.
* A partire dalla versione Forms dell’AEM 6.1, non è possibile esprimere commenti in modo predefinito. I commenti aggiunti in precedenza sono disponibili nelle risorse, ma non sono visibili automaticamente nell’interfaccia. Personalizza la proprietà extendedProperties nell’interfaccia utente di AEM Forms per rendere visibili i commenti.
* In alcune delle versioni precedenti, come il LiveCycle ES4, il testo è stato modificato utilizzando Flex RichTextEditor, ma a partire da AEM 6.1 Forms, viene utilizzato l&#39;editor HTML. A causa di questo rendering e dell’aspetto dei caratteri, le dimensioni e i margini dei caratteri possono essere diversi dalle versioni precedenti nell’interfaccia utente di Author. Tuttavia, le lettere hanno lo stesso aspetto quando vengono sottoposte a rendering.
* Gli elenchi nei moduli di testo vengono migliorati e ora vengono riprodotti in modo diverso. Potrebbero esserci delle differenze visive. L’Adobe consiglia di eseguire il rendering e visualizzare le lettere in cui si utilizzano gli elenchi nei moduli di testo.
* Poiché i moduli di contenuto immagine vengono convertiti in risorse DAM e i layout e i frammenti vengono aggiunti ai moduli durante la migrazione, la proprietà Updated By di questi moduli cambia in admin.
* La cronologia delle versioni delle risorse non viene migrata e non è disponibile dopo la migrazione. La cronologia delle versioni successive alla migrazione viene mantenuta.
* Lo stato Pronto per Publish è diventato obsoleto a partire da AEM 6.1 Forms, quindi tutte le risorse nello stato Pronto per Publish sono passate allo stato Modificato.
* Poiché l’interfaccia utente di è stata aggiornata in AEM Forms 6.3, anche i passaggi per eseguire le personalizzazioni sono diversi. Ripristina la personalizzazione se esegui la migrazione da una versione precedente alla 6.3.
* I frammenti di layout vengono spostati da `/content/apps/cm/layouts/fragmentlayouts/1001` a `/content/apps/cm/modules/fragmentlayouts`. Il riferimento del dizionario dati nelle risorse visualizza il percorso del dizionario dati anziché il nome.
* Eventuali spazi di tabulazione utilizzati per l&#39;allineamento nei moduli di testo devono essere riregolati. Per ulteriori informazioni, vedere [Gestione della corrispondenza - Utilizzo della spaziatura tra le schede per la disposizione del testo](https://helpx.adobe.com/aem-forms/kb/cm-tab-spacing-limitations.html).
* Le configurazioni del compositore risorse vengono modificate nelle configurazioni di Gestione della corrispondenza.
* Assets viene spostato in cartelle con nomi quali Testo esistente ed Elenco esistente.

## Utilizzo dell&#39;utilità Migration {#using-the-migration-utility}

### Esecuzione dell&#39;utilità di migrazione {#runningmigrationutility}

Esegui l’utility di migrazione prima di modificare le risorse o crearle. L’Adobe consiglia di non eseguire l’utility dopo aver apportato modifiche o creato risorse. Assicurati che l’interfaccia utente di Assets per la gestione della corrispondenza o per Forms adattivo non sia aperta mentre il processo di migrazione è in esecuzione.

Quando si esegue l&#39;utilità di migrazione per la prima volta, viene creato un registro con il percorso e il nome seguenti: `\[aem-installation-directory]\cq-quickstart\logs\aem-forms-migration.log`. Questo registro viene costantemente aggiornato con le informazioni sulla migrazione di Gestione della corrispondenza e Forms adattivo, ad esempio lo spostamento delle risorse.

>[!NOTE]
>
>Prima di eseguire l’utility di migrazione, accertati di aver eseguito un backup dell’archivio crx.

1. In una sessione del browser, accedi all’istanza Autore AEM come Amministratore.

1. Apri il seguente URL nel browser:

   https://[*nomehost*]:[*porta*]/[*percorso_contesto*]/libs/fd/foundation/gui/content/migration.html

   Il browser visualizza quattro opzioni:

   * Migrazione risorse AEM Forms
   * Migrazione dei componenti personalizzati di Forms adattivi
   * Migrazione di modelli Forms adattivi
   * Migrazione configurazioni AEM Forms Cloud

1. Per eseguire la migrazione, effettuare le seguenti operazioni:

   * Per eseguire la migrazione di **risorse**, seleziona AEM Forms Assets Migration e nella schermata successiva seleziona **Start Migration**. Viene eseguita la migrazione dei seguenti elementi:

      * Moduli adattivi
      * Frammenti di documenti
      * Temi
      * Lettere
      * Dizionari dati

   >[!NOTE]
   >
   >Durante la migrazione delle risorse, potresti trovare messaggi di avviso come &quot;Conflitto trovato per...&quot;. Questi messaggi indicano che non è stato possibile migrare le regole per alcuni dei componenti nei moduli adattivi. Ad esempio, se il componente aveva un evento con sia regole che script, se le regole si verificano dopo uno script, nessuna delle regole per il componente viene migrata. Puoi [migrare tali regole aprendo l&#39;editor di regole](#migrate-rules) nell&#39;authoring di moduli adattivi.

   * Per migrare i componenti personalizzati del modulo adattivo, seleziona **Migrazione componenti personalizzati Forms adattivi** e nella pagina Migrazione componenti personalizzati seleziona **Avvia migrazione**. Viene eseguita la migrazione dei seguenti elementi:

      * Componenti personalizzati scritti per Adaptive Forms
      * Eventuali sovrapposizioni dei componenti.

   * Per migrare i modelli di modulo adattivo, seleziona **Migrazione modello Forms adattivo** e nella pagina Migrazione componenti personalizzati seleziona **Avvia migrazione**. Viene eseguita la migrazione dei seguenti elementi:

      * Modelli di modulo adattivo creati in `/apps` o `/conf` utilizzando l&#39;Editor modelli AEM.

   * Eseguire la migrazione dei servizi di configurazione cloud di AEM Forms per utilizzare il nuovo paradigma del servizio cloud in base al contesto, che include l&#39;interfaccia utente touch (in `/conf`). Durante la migrazione dei servizi di configurazione cloud di AEM Forms, i servizi cloud in `/etc` vengono spostati in `/conf`. Se non si dispone di personalizzazioni dei servizi cloud che dipendono dai percorsi legacy (`/etc`), l&#39;Adobe consiglia di eseguire l&#39;utilità di migrazione dopo l&#39;aggiornamento alla versione 6.5; utilizzare l&#39;interfaccia utente touch della configurazione cloud per ulteriori operazioni. Se sono presenti personalizzazioni di servizi cloud esistenti, continuare a utilizzare l&#39;interfaccia utente classica nella configurazione aggiornata fino a quando le personalizzazioni non vengono aggiornate in modo da allinearle ai percorsi migrati (`/conf`), quindi eseguire l&#39;utilità di migrazione.

   Per eseguire la migrazione di **AEM Forms Cloud Services**, che include quanto segue, selezionare Migrazione configurazione cloud AEM Forms (la migrazione della configurazione cloud è indipendente dal pacchetto di compatibilità AEMFD). Seleziona AEM Forms Cloud Configurations Migration (Migrazione configurazioni cloud), quindi nella pagina Configuration Migration (Migrazione configurazione) seleziona **Start Migration** (Avvia migrazione):

   * Servizi cloud del modello dati modulo

      * Percorso Source: `/etc/cloudservices/fdm`
      * Percorso di destinazione: `/conf/global/settings/cloudconfigs/fdm`

   * Recaptcha

      * Percorso Source: `/etc/cloudservices/recaptcha`
      * Percorso di destinazione: `/conf/global/settings/cloudconfigs/recaptcha`

   * Adobe Sign

      * Percorso Source: `/etc/cloudservices/echosign`
      * Percorso di destinazione: `/conf/global/settings/cloudconfigs/echosign`

   * Servizi cloud Typekit

      * Percorso Source: `/etc/cloudservices/typekit`
      * Percorso di destinazione: `/conf/global/settings/cloudconfigs/typekit`

   La finestra del browser mostra quanto segue durante il processo di migrazione:

   * Quando le risorse vengono aggiornate: Assets viene aggiornato correttamente.
   * Al termine della migrazione: migrazione delle risorse completata.

   Quando viene eseguita, l&#39;utilità Migration esegue le operazioni seguenti:

   * **Aggiunge i tag alle risorse**: aggiunge il tag &quot;Gestione della corrispondenza: Assets migrato&quot; / &quot;Forms adattivo: Assets migrato&quot;. alle risorse migrate, in modo che gli utenti possano identificare le risorse migrate. Quando si esegue l&#39;utilità Migration, tutte le risorse esistenti nel sistema vengono contrassegnate come Migrate.
   * **Genera tag**: le categorie e le sottocategorie presenti nel sistema precedente vengono create come tag e quindi questi tag vengono associati alle risorse di Gestione della corrispondenza pertinenti in AEM. Ad esempio, una categoria (Attestazioni) e una sottocategoria (Attestazioni) di un modello di lettera vengono generate come tag.

1. Al termine dell&#39;esecuzione dell&#39;utilità di migrazione, passare alle [attività di manutenzione](#housekeepingtasks).

#### Eseguire la migrazione delle regole tramite l’editor di regole {#migrate-rules}

Questi componenti possono essere migrati aprendoli nell’editor di regole nell’editor di Forms adattivo.

* Per migrare regole e script (non necessari se si esegue l’aggiornamento da 6.3) nei componenti personalizzati, seleziona Migrazione componenti personalizzati di Forms adattivi e nella schermata successiva seleziona Avvia migrazione. Viene eseguita la migrazione dei seguenti elementi:

   * Regole e script creati utilizzando l’editor di regole (6.1 FP1 e versioni successive)

   * Script creati utilizzando la scheda Script nell’interfaccia utente di 6.1 e versioni precedenti

* Per eseguire la migrazione dei modelli (non richiesto per l’aggiornamento da 6.3 e 6.4), seleziona Migrazione modello Forms adattivo e nella schermata successiva seleziona Avvia migrazione. Viene eseguita la migrazione dei seguenti elementi:

   * Modelli precedenti: i modelli di moduli adattivi creati in /apps utilizzando AEM 6.1 Forms o versioni precedenti. Sono inclusi gli script definiti nei componenti del modello.

   * Nuovi modelli: modelli di moduli adattivi creati utilizzando l&#39;editor modelli in `/conf`. Ciò include la migrazione di regole e script creati utilizzando l’editor di regole.

### Attività di manutenzione dopo l’esecuzione dell’utility di migrazione {#housekeepingtasks}

Dopo aver eseguito l&#39;utilità Migration, eseguire le seguenti operazioni di manutenzione:

1. Assicurati che la versione XFA dei layout e dei layout dei frammenti sia la 3.3 o successiva. Se utilizzi layout e layout di frammenti di una versione precedente, potrebbero esserci problemi nel rendering della lettera. La procedura seguente illustra come aggiornare una versione di un XFA precedente alla versione più recente:

   1. [Scarica XFA come file zip](../../forms/using/import-export-forms-templates.md#p-import-and-export-assets-in-correspondence-management-p) dall&#39;interfaccia utente di Forms.
   1. Estrai il file.
   1. Apri il file XFA nell’ultimo Designer e salvalo. La versione di XFA viene aggiornata a quella più recente.
   1. Carica XFA nell’interfaccia utente di Forms.

1. Publish tutte le risorse pubblicate nel sistema precedente prima della migrazione. L’utility di migrazione aggiorna le risorse solo nell’istanza di authoring e, per aggiornare le risorse nelle istanze di Publish, devi pubblicare le risorse.

1. In AEM Forms 6.4 e 6.5, alcuni dei diritti dei gruppi di utenti di Forms vengono modificati. Se desideri consentire a uno degli utenti di caricare XDP e Forms adattivi contenenti script o utilizzare un editor di codice, devi aggiungerli al gruppo forms-power-users. Analogamente, gli autori di modelli non possono più utilizzare l’editor di codice nell’editor di regole. Per consentire agli utenti di utilizzare un editor di codice, aggiungerli al gruppo af-template-script-writer. Per istruzioni sull&#39;aggiunta di utenti ai gruppi, vedere [Gestione di utenti e gruppi di utenti](/help/communities/users.md).
