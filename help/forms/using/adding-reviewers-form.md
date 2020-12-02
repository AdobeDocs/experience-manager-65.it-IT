---
title: Associazione di revisori per l'invio a un modulo
seo-title: Associazione di revisori per l'invio a un modulo
description: Scoprite come associare i revisori per l'invio a un modulo in  AEM Forms. I revisori associati rivedono un modulo inviato tramite il portale dei moduli.
seo-description: Scoprite come associare i revisori per l'invio a un modulo in  AEM Forms. I revisori associati rivedono un modulo inviato tramite il portale dei moduli.
uuid: 58c8c8fb-9262-4c37-b9b2-e46fe21b77d9
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 71d1aa10-d191-49bc-a50f-1098324f1cfe
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---


# Associazione di revisori per l&#39;invio a un modulo {#associating-submission-reviewers-with-a-form}

Quando si crea un modulo, è possibile specificare gli utenti che rivedono gli invii del modulo tramite il portale dei moduli e fornire feedback. L&#39;organizzazione può raccogliere i commenti e rielaborare i moduli inviati.

 AEM Forms consente di associare un gruppo di revisori a un modulo. Gli utenti aggiunti a un gruppo di revisione di un modulo possono vedere gli invii del modulo e fornire feedback.

I gruppi di revisori assegnati a un modulo possono esaminare solo gli invii del modulo specificato.

## Prerequisito {#prerequisite}

### Abilitazione della proprietà dei gruppi di revisori per l&#39;invio di moduli adattivi tramite l&#39;editor dello schema di metadati {#enabling-submission-reviewer-groups-property-for-adaptive-forms-using-metadata-schema-editor}

Per associare un gruppo di revisori a un modulo, modificare lo schema di metadati dei moduli adattivi. Per impostazione predefinita, non è possibile aggiungere un gruppo di revisori a un modulo inviato.

Per modificare lo schema di metadati:

1. In modalità di authoring, in  Experience Manager, fate clic su **Strumenti** > **Risorse** > **Schemi metadati**.
1. Nella pagina Forms schema, passare a **Forms** > **Forms Authored in AEM.**

   L’URL della pagina è:

   ```html
   https://<hostname>:<port>/mnt/overlay/dam/gui/content/metadataschemaeditor/
    schemalist.html/forms/aem-authored
   ```

1. Selezionare **Modulo adattivo** e fare clic su **Modifica**.
1. Nella pagina Modifica modulo, fare clic su **Avanzate**.
1. Nella scheda Avanzate, trascinare il componente **Testo su riga singola** disponibile in Modulo di creazione.
1. Selezionate il componente di testo aggiunto per visualizzarne le impostazioni.

   In Impostazioni, immettete `./jcr:content/metadata/form-submission-reviewer-group` nel campo Mappa su proprietà.

   Il campo del gruppo di revisori per l&#39;invio nelle proprietà Avanzate del modulo adattivo è attivato con il nome specificato in Etichetta campo.

## Associazione di revisori per l&#39;invio a un modulo {#associating-submission-reviewers-with-a-form-1}

Per associare i revisori all’invio a un modulo adattivo, create un gruppo di revisori e aggiungeteli. Aggiungere il gruppo di revisori creato nel campo del revisore per l&#39;invio del modulo nelle proprietà avanzate del modulo.
I gruppi di utenti consentono di associare diversi set di revisori per l’invio a diversi moduli adattivi. Questa funzione impedisce la revisione dell&#39;invio da parte di un utente non autorizzato.

Prima di eseguire le operazioni seguenti, vedere [Prerequisite](../../forms/using/adding-reviewers-form.md#prerequisite).

Per creare un gruppo e aggiungervi dei membri, andate a **Strumenti** > **Operazioni** > **Protezione** > **Gruppi**.
Per ulteriori informazioni, vedere [Amministrazione utente e servizi](/help/sites-administering/security.md).
Assicuratevi di aggiungere il gruppo creato come membro del gruppo di utenti out-of-the-box: **forms-submit-reviewers**. Questo gruppo di utenti viene fornito con  AEM Forms e assicura che gli utenti vengano aggiunti come revisori per l’invio.

Per associare gruppi di utenti a un modulo adattivo:

1. In modalità authoring, passare a **Forms** > **Forms &amp; Documents**.
1. Utilizzare l&#39;opzione **Select **per selezionare un modulo adattivo, quindi fare clic su **Visualizza proprietà**.
1. Nella finestra Proprietà del modulo, fare clic su **Modifica**, quindi su **AVANZATO**.
1. Immettete il gruppo nel campo del gruppo di revisori per l&#39;invio e fate clic su **Done**.

   Il campo del gruppo di revisori per l&#39;invio viene visualizzato con il nome specificato nello schema di metadati modificato dei moduli adattivi.

>[!NOTE]
>
>Replicare utenti e moduli per garantire la disponibilità di utenti e moduli nell&#39;implementazione remota di  AEM Forms.
>
>Assicurati che tutti gli utenti vengano replicati come membri di revisione dei gruppi di utenti nell&#39;implementazione remota.

