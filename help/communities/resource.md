---
title: Creare e assegnare risorse di abilitazione
seo-title: Create and Assign Enablement Resources
description: Aggiungi risorse di abilitazione
seo-description: Add enablement resources
uuid: da940242-0c9b-4ad8-8880-61fd41461c3b
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 8fe97181-600e-42ac-af25-d5d4db248740
exl-id: 78908a9c-a260-44ff-ad1e-baa6d78ae399
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 7%

---

# Creare e assegnare risorse di abilitazione {#create-and-assign-enablement-resources}

## Aggiungi una risorsa di abilitazione {#add-an-enablement-resource}

Per aggiungere una risorsa di abilitazione al nuovo sito della community:

* Effettua l’accesso come amministratore di sistema nell’istanza di authoring:
   * Ad esempio: [http://localhost:4502/](Http://localhost:4503/)
* Dalla navigazione globale, seleziona **[!UICONTROL Community]** > **[!UICONTROL Risorse]**

   ![riferimenti](assets/resources.png)

   ![enablement-resource](assets/enablement-resource.png)
* Seleziona il sito community a cui vengono aggiunte le risorse di abilitazione:
   * Seleziona **[!UICONTROL Tutorial sull’abilitazione]**.
* Dal menu , seleziona **[!UICONTROL Crea]**.
* Seleziona **[!UICONTROL Risorsa]**.

![create-resource](assets/create-enablement-resource.png)

### Informazioni di base {#basic-info}

Compila le informazioni di base per la risorsa:

* **[!UICONTROL Nome sito]**

   Imposta il nome del sito community selezionato: Tutorial sull’abilitazione

* **[!UICONTROL Nome &amp;risorsa;]**

   Lezioni di sci 1

* **[!UICONTROL Tag]**

   Esercitazione: Sport / Sci

* **[!UICONTROL Mostra nel catalogo]**

   Impostalo su **On**.

* **[!UICONTROL Descrizione]**

   Scivolare sulla neve per principianti.

* **[!UICONTROL Aggiungi]**

   Aggiungi un&#39;immagine per rappresentare la risorsa al membro nella relativa vista Assegnazioni.

   ![basic-info](assets/basic-info.png)

* Seleziona **[!UICONTROL Avanti]**

### Aggiungi contenuto {#add-content}

Viene visualizzato come se fosse possibile selezionare più risorse, ma solo una è consentita.

Seleziona la `'+' icon`, nell&#39;angolo in alto a destra, per iniziare il processo di scelta della risorsa identificando l&#39;origine.

![contenuto aggiuntivo](assets/add-content.png)

![risorsa di caricamento](assets/upload-resource.png)

Carica una risorsa. Se una risorsa video, carica un’immagine personalizzata da visualizzare prima dell’avvio della riproduzione del video o consente di generare una miniatura dal video (potrebbero essere necessari alcuni minuti, non è necessario attendere).

![caricare-video](assets/upload-video.png)

* Seleziona **[!UICONTROL Avanti]**.

### Impostazioni {#settings}

* **[!UICONTROL Impostazioni social]**

   Lascia le impostazioni predefinite per esaminare i commenti e la valutazione delle risorse di abilitazione da parte degli studenti.

* **[!UICONTROL Data di scadenza]**

   *(Facoltativo)* È possibile selezionare una data entro la quale l&#39;assegnazione deve essere completata.

* **[!UICONTROL Autore risorse]**

   *(Facoltativo)* Lascia vuoto.

* **[!UICONTROL Contatto &amp;risorsa;]**

   *(Obbligatorio)* Utilizzare il menu a discesa per selezionare un membro `Quinn Harper`.

* **[!UICONTROL Esperto risorse]**

   *(Facoltativo)* Lascia vuoto.

   **Nota**: Se gli utenti o i gruppi non sono visibili, verifica che siano stati aggiunti al `Community Enable Members` gruppo e *Salvato* nell’istanza di pubblicazione.

   ![enablement-settings](assets/enablement-settings.png)

* Seleziona **[!UICONTROL Avanti]**

### Assegnazioni {#assignments}

* **[!UICONTROL Aggiungi assegnatari]**

   Lascia non impostato perché questa risorsa di abilitazione verrà aggiunta a un percorso di apprendimento. Se uno studente viene assegnato alla singola risorsa di abilitazione e a un percorso di apprendimento contenente la risorsa di abilitazione, lo studente verrà assegnato due volte alla risorsa di abilitazione.

   ![assegnazioni aggiuntive](assets/add-assignments.png)

* Seleziona **[!UICONTROL Crea]**

   ![create-resource](assets/create-resource.png)

La creazione della risorsa viene ripristinata nella console Risorse selezionando la risorsa appena creata. Da questa console è possibile pubblicare, aggiungere studenti e modificare altre impostazioni.

Per caricare una nuova versione della risorsa di abilitazione, è consigliabile creare una nuova risorsa, quindi annullare l’iscrizione dei membri dalla versione precedente e iscriverli nella nuova versione.

### Pubblicare la risorsa {#publish-the-resource}

Prima che gli iscritti possano vedere il Rescourse assegnato, è necessario pubblicarlo:

* Seleziona il mondo `Publish` icona

L’attivazione viene confermata con un messaggio di successo:

![publish-resource](assets/publish-resource.png)

## Aggiungi una seconda risorsa di abilitazione {#add-a-second-enablement-resource}

Ripeti i passaggi precedenti per creare e pubblicare una seconda risorsa di abilitazione correlata dalla quale verrà creato un percorso di apprendimento.

![add-resource](assets/add-resource.png)

**Pubblica** la seconda risorsa.

Torna all’elenco delle risorse di Enablement Tutorial.

*Suggerimento: Se entrambe le risorse non sono visibili, aggiorna la pagina.*

![refresh-resource](assets/refresh-resource.png)

## Aggiungere un percorso di apprendimento {#add-a-learning-path}

Un percorso di apprendimento è un raggruppamento logico di risorse di abilitazione che formano un corso.

* Dalla console Risorse, seleziona `+ Create`
* Seleziona **[!UICONTROL Percorso di apprendimento]**

![percorso di apprendimento-aggiuntivo](assets/add-learning-path.png)

Aggiungi il **[!UICONTROL Informazioni di base]**:

* **[!UICONTROL Nome percorso di apprendimento]**

   Lezioni di sci

* **[!UICONTROL Tag]**

   Esercitazione: Sciare

* **[!UICONTROL Mostra nel catalogo]**

   Lascia deselezionato

* **[!UICONTROL Caricare un’immagine]**

   Per rappresentare il percorso di apprendimento nella console Risorse .

   ![apprendere percorso-base](assets/learningpath-basic.png)

* Seleziona **[!UICONTROL Avanti]**.

Ignora il pannello successivo in quanto non sono presenti percorsi di apprendimento preliminari da aggiungere.

* Seleziona **[!UICONTROL Avanti]**

Nel pannello Aggiungi risorse :

* Seleziona `+ Add Resources` per selezionare le 2 risorse sciistiche da aggiungere al percorso di apprendimento.

   Nota: Solo **pubblicato** Le risorse saranno selezionabili.

>[!NOTE]
>
>È possibile selezionare solo le risorse disponibili allo stesso livello del percorso di apprendimento. Ad esempio, per un percorso di apprendimento creato in un gruppo sono disponibili solo le risorse a livello di gruppo; per un percorso di apprendimento creato in un sito community, le risorse in tale sito sono disponibili per l’aggiunta al percorso di apprendimento.

* Seleziona **[!UICONTROL Invia]**.

   ![percorso di apprendimento](assets/learningpath-add.png)

   ![create-learning path](assets/create-learningpath.png)

* Seleziona **[!UICONTROL Avanti]**

   ![apprendimento delle impostazioni del percorso](assets/learningpath-settings.png)

* **[!UICONTROL Aggiungi assegnatari]**

   Utilizza il menu a discesa per selezionare il `Community Ski Class` gruppo, che deve includere i membri `Riley Taylor` e `Sidney Croft.`

* **[!UICONTROL Percorso di apprendimento Contatti&amp;ast;]**

   *(Obbligatorio)* Utilizzare il menu a discesa per selezionare un membro `Quinn Harper`.

* Seleziona **[!UICONTROL Crea]**.

   ![informazioni su percorso](assets/learningpath-info.png)

La creazione corretta del percorso di apprendimento torna alla console Risorse con il percorso di apprendimento appena creato selezionato. Da questa console è possibile pubblicare, aggiungere studenti e modificare altre impostazioni.

**Pubblica** il percorso di apprendimento.
