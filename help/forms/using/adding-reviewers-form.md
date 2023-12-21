---
title: Associazione dei revisori di invio a un modulo
description: Scopri come associare i revisori per l’invio a un modulo in AEM Forms. I revisori associati esaminano un modulo inviato tramite il portale dei moduli.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms, Foundation Components
exl-id: 46e7b858-44d1-41c8-9f44-4e959e593dc1
source-git-commit: d85fc98d9a31bc4014aef4311ba0f838c7ef619a
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 0%

---

# Associazione dei revisori di invio a un modulo {#associating-submission-reviewers-with-a-form}

<span class="preview"> L’Adobe consiglia di utilizzare l’acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [creazione di un nuovo Forms adattivo](/help/forms/using/create-an-adaptive-form-core-components.md) o [aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

Quando si crea un modulo, è possibile specificare gli utenti che esaminano gli invii del modulo tramite il portale moduli e forniscono feedback. La tua organizzazione può raccogliere feedback e rielaborare i moduli inviati.

AEM Forms consente di associare un gruppo di revisori a un modulo. Gli utenti aggiunti a un gruppo di revisione di un modulo vedranno gli invii di questo modulo e forniranno un feedback.

I gruppi di revisori assegnati a un modulo possono esaminare solo gli invii del modulo specificato.

## Prerequisito {#prerequisite}

### Abilitazione della proprietà dei gruppi di revisori per l’invio di moduli adattivi tramite l’editor schema metadati {#enabling-submission-reviewer-groups-property-for-adaptive-forms-using-metadata-schema-editor}

Per associare un gruppo di revisori a un modulo, modifica lo schema di metadati dei moduli adattivi. Per impostazione predefinita, non è possibile aggiungere un gruppo di revisori a un modulo inviato.

Per modificare lo schema metadati:

1. Nella modalità di authoring, in Experience Manager, fai clic su **Strumenti** > **Risorse** > **Schemi metadati**.
1. Nella pagina Forms schema, passa a **Forms** > **Forms creato nell&#39;AEM.**

   L’URL della pagina è:

   ```html
   https://<hostname>:<port>/mnt/overlay/dam/gui/content/metadataschemaeditor/
    schemalist.html/forms/aem-authored
   ```

1. Seleziona **Modulo adattivo** e fai clic su **Modifica**.
1. Nella pagina Modifica modulo fare clic su **Avanzate**.
1. Nella scheda Avanzate, trascina e rilascia la **Testo su riga singola** componente disponibile in Genera modulo.
1. Seleziona il componente testo aggiunto per visualizzarne le impostazioni.

   In Impostazioni, immetti `./jcr:content/metadata/form-submission-reviewer-group` nel campo Mappa su proprietà.

   Il campo gruppo revisore invio nelle proprietà avanzate del modulo adattivo è abilitato con il nome specificato in Etichetta campo.

## Associazione dei revisori di invio a un modulo {#associating-submission-reviewers-with-a-form-1}

Per associare i revisori per l’invio a un modulo adattivo, crea un gruppo di revisori e aggiungi gli utenti. Aggiungi il gruppo di revisori creato nel campo revisore invio modulo nelle proprietà avanzate del modulo.
I gruppi di utenti consentono di associare diversi gruppi di revisori per l’invio a diversi moduli adattivi. Questa funzione impedisce a un utente non autorizzato di inviare un messaggio di revisione.

Prima di eseguire i passaggi seguenti, consulta [Prerequisito](../../forms/using/adding-reviewers-form.md#prerequisite).

Per creare un gruppo e aggiungervi membri, passare a **Strumenti** > **Operazioni** > **Sicurezza** > **Gruppi**.
Per ulteriori informazioni, consulta [Amministrazione utenti e servizi](/help/sites-administering/security.md).
Assicurati di aggiungere il gruppo creato come membro del gruppo di utenti predefinito: **forms-submit-reviewers**. Questo gruppo di utenti viene fornito con AEM Forms e garantisce che gli utenti vengano aggiunti come revisori per l’invio.

Per associare gruppi di utenti a un modulo adattivo:

1. In modalità authoring, passa a **Forms** > **Forms e documenti**.
1. Utilizza l’opzione **Seleziona **per selezionare un modulo adattivo e fai clic su **Visualizza proprietà**.
1. Nella finestra Proprietà del modulo fare clic su **Modifica** e quindi fare clic su **AVANZATE**.
1. Immettere il gruppo nel campo gruppo revisore invio e fare clic su **Fine**.

   Il campo gruppo revisore invio viene visualizzato con il nome specificato nello schema metadati modificato dei moduli adattivi.

>[!NOTE]
>
>Replica di utenti e moduli per garantire la disponibilità di utenti e moduli nell’implementazione remota di AEM Forms.
>
>Assicurati che tutti gli utenti vengano replicati durante la revisione dei membri dei gruppi di utenti nell’implementazione remota.
