---
title: Configurazione dell’Annulla per la modifica delle pagine
seo-title: Configuring Undo for Page Editing
description: Scopri come configurare il supporto Annulla per la modifica delle pagine in AEM.
seo-description: Learn how to configure Undo support for page editing in AEM.
uuid: e5a49587-a2a6-41d5-b449-f7a8f7e4cee6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 3cc7efc5-bcb2-41c9-b78b-308f6b7a298e
exl-id: 2cf3ac3f-ee17-480d-a32a-c57631502693
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 2%

---

# Configurazione dell’Annulla per la modifica delle pagine{#configuring-undo-for-page-editing}

La [Servizio OSGi](/help/sites-deploying/configuring-osgi.md)  **Configurazione Annulla Day CQ WCM** ( `com.day.cq.wcm.undo.UndoConfigService`) espone diverse proprietà che controllano il comportamento dei comandi Annulla e Ripristina per la modifica delle pagine.

## Configurazione predefinita {#default-configuration}

In un’installazione standard le impostazioni predefinite sono definite come proprietà `sling:OsgiConfig`nodo:

`/libs/wcm/core/config.author/com.day.cq.wcm.undo.UndoConfig`

Questo nodo contiene `cq.wcm.undo.whitelist` e `cq.wcm.undo.blacklist` per le altre proprietà vengono utilizzate le impostazioni predefinite.

>[!CAUTION]
>
>You ***deve*** non modificare nulla nel `/libs` percorso.
>
>Questo perché il contenuto di `/libs` viene sovrascritto la prossima volta che aggiorni l’istanza (e potrebbe essere sovrascritto quando applichi un hotfix o un feature pack).

## Configurazione di Annulla e Ripristina {#configuring-undo-and-redo}

Puoi configurare queste proprietà del servizio OSGi per la tua istanza.

>[!NOTE]
>
>Quando si lavora con AEM esistono diversi metodi per gestire le impostazioni di configurazione di tali servizi; vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) per ulteriori dettagli e procedure consigliate.

Di seguito sono elencate le proprietà visualizzate nella console Web, seguite dal nome del parametro OSGi corrispondente, insieme a una descrizione e al valore predefinito (se appropriato):

* **Attiva**
( 
`cq.wcm.undo.enabled`)

   * **Descrizione**: Determina se gli autori delle pagine possono annullare e ripristinare le modifiche.
   * **Predefinito**: `Selected`
   * **Tipo**: `Boolean`

* **Percorso**
( 
`cq.wcm.undo.path`)

   * **Descrizione**: Percorso dell&#39;archivio per i dati di annullamento binari persistenti. Quando gli autori modificano i dati binari, come le immagini, la versione originale dei dati viene mantenuta qui. Quando le modifiche ai dati binari vengono annullate, i dati di annullamento binari vengono ripristinati nella pagina.
   * **Predefinito**: `/var/undo`
   * **Tipo**: `String`

   >[!NOTE]
   >
   >Per impostazione predefinita, solo gli amministratori possono accedere al `/var/undo` nodo. Gli autori possono eseguire operazioni di annullamento e ripristino sul contenuto binario solo dopo aver ottenuto le autorizzazioni necessarie per accedere ai dati di annullamento binari.

* **Min. validità**
( 
`cq.wcm.undo.validity`)

   * **Descrizione**: La quantità minima di tempo in ore in cui vengono archiviati i dati di annullamento binari. Dopo questo periodo di tempo, i dati binari sono disponibili per l&#39;eliminazione, per risparmiare spazio su disco.
   * **Predefinito**: `10`
   * **Tipo**: `Integer`

* **Passaggi**
( 
`cq.wcm.undo.steps`)

   * **Descrizione**: Numero massimo di azioni di pagina memorizzate nella cronologia di annullamento.
   * **Predefinito**: `20`
   * **Tipo**: `Integer`

* **Persistenza**
( 
`cq.wcm.undo.persistence`)

   * **Descrizione**: Classe che persiste nella cronologia di annullamento. Sono fornite due classi di persistenza:

      * `CQ.undo.persistence.WindowNamePersistence`: Persiste la cronologia utilizzando la proprietà window.name .
      * `CQ.undo.persistence.CookiePersistance`: Persiste la cronologia tramite i cookie.
   * **Predefinito**: `CQ.undo.persistence.WindowNamePersistence`
   * **Tipo**: `String`


* **Modalità di persistenza**
( 
`cq.wcm.undo.persistence.mode`)

   * **Descrizione**: Determina quando la cronologia di annullamento viene mantenuta. Selezionare questa opzione per mantenere la cronologia degli annullamenti dopo ogni modifica della pagina. Deseleziona questa opzione per persistere solo quando si verifica un ricaricamento della pagina (ad esempio, l’utente passa a una pagina diversa).

      La cronologia degli annullamenti persistenti utilizza le risorse del browser Web. Se il browser degli utenti reagisce lentamente alle modifiche della pagina, prova a mantenere la cronologia degli annullamenti nei ricaricamenti della pagina.

   * **Predefinito**: `Selected`
   * **Tipo**: `Boolean`

* **Modalità Marker**
( 
`cq.wcm.undo.markermode`)

   * **Descrizione**: Specifica il cue visivo da utilizzare per indicare quali paragrafi sono interessati dall’azione di annullamento o ripristino. I seguenti valori sono validi:

      * flash: L’indicatore di selezione dei paragrafi lampeggia temporaneamente.
      * seleziona: Il paragrafo viene selezionato.
   * **Predefinito**: `flash`
   * **Tipo**: `String`


* **Componenti buoni**
( 
`cq.wcm.undo.whitelist`)

   * **Descrizione**: Elenco dei componenti interessati dai comandi Annulla e Ripristina. Aggiungi i percorsi dei componenti a questo elenco quando funzionano correttamente con Annulla/Ripristina. Aggiungi un asterisco (&amp;ast;) per specificare un gruppo di componenti:

      * Il valore seguente specifica il componente testo di base:

         `foundation/components/text`

      * Il valore seguente specifica tutti i componenti di base:

         `foundation/components/*`
   * Quando si eseguono operazioni Annulla o Ripristina su un componente che non è presente nell’elenco, viene visualizzato un messaggio che indica che il comando può non essere affidabile.

   * **Predefinito**: La proprietà viene compilata con molti componenti AEM.
   * **Tipo**: `String[]`


* **Componenti non validi**
( 
`cq.wcm.undo.blacklist`)

   * **Descrizione**: Elenco dei componenti e/o delle operazioni dei componenti che non devono essere interessati dal comando Annulla. Aggiungere componenti e operazioni dei componenti che non si comportano correttamente con il comando Annulla:

      * Aggiungi un percorso componente quando non desideri eseguire nessuna delle operazioni del componente nella cronologia di annullamento, ad esempio `collab/forum/components/post`
      * Aggiungere due punti (:) e un&#39;operazione al percorso quando si desidera che l&#39;operazione specifica venga omessa dalla cronologia degli annullamenti (altre operazioni funzionano correttamente), ad esempio `collab/forum/components/post:insertParagraph.`

   >[!NOTE]
   >
   >Quando un&#39;operazione è presente in questo elenco, viene comunque aggiunta alla cronologia di annullamento. Gli utenti non possono annullare le operazioni esistenti prima di un **Componente non valido** nella cronologia di annullamento.

   * Di seguito sono riportati i nomi di operazione tipici:

      * `insertParagraph`: Il componente viene aggiunto alla pagina.
      * `removeParagraph`: Il componente viene eliminato.
      * `moveParagraph`: Il paragrafo viene spostato in una posizione diversa.
      * `updateParagraph`: Le proprietà del paragrafo vengono modificate.
   * **Predefinito**: La proprietà viene compilata con diverse operazioni dei componenti.
   * **Tipo**: `String[]`
