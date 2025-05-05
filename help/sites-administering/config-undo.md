---
title: Configurazione dell’annullamento per la modifica delle pagine
description: Scopri come configurare il supporto Undo per la modifica delle pagine in AEM.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: 2cf3ac3f-ee17-480d-a32a-c57631502693
solution: Experience Manager, Experience Manager Sites
feature: Configuring
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 0%

---

# Configurazione dell’annullamento per la modifica delle pagine{#configuring-undo-for-page-editing}

Il servizio [OSGi](/help/sites-deploying/configuring-osgi.md) **Day CQ WCM Undo Configuration** ( `com.day.cq.wcm.undo.UndoConfigService`) espone diverse proprietà che controllano il comportamento dei comandi Annulla e Ripristina per la modifica delle pagine.

## Configurazione predefinita {#default-configuration}

In un&#39;installazione standard le impostazioni predefinite sono definite come proprietà nel nodo `sling:OsgiConfig`:

`/libs/wcm/core/config.author/com.day.cq.wcm.undo.UndoConfig`

Questo nodo contiene `cq.wcm.undo.whitelist` e `cq.wcm.undo.blacklist` proprietà. Per le altre proprietà vengono utilizzate le impostazioni predefinite.

>[!CAUTION]
>
>***must*** non modificare nulla nel percorso `/libs`.
>
>Il contenuto di `/libs` viene sovrascritto al successivo aggiornamento dell&#39;istanza (e potrebbe essere sovrascritto quando si applica un hotfix o un feature pack).

## Configurazione di Annulla e Ripristina {#configuring-undo-and-redo}

Puoi configurare queste proprietà del servizio OSGi per la tua istanza.

>[!NOTE]
>
>Quando si lavora con AEM, esistono diversi metodi per gestire le impostazioni di configurazione per tali servizi; vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) per ulteriori dettagli e le procedure consigliate.

Di seguito è riportato un elenco delle proprietà visualizzate nella console Web, seguite dal nome del parametro OSGi corrispondente, insieme a una descrizione e al valore predefinito (se appropriato):

* **Abilita**
( `cq.wcm.undo.enabled`)

   * **Descrizione**: determina se gli autori delle pagine possono annullare e ripristinare le modifiche.
   * **Predefinito**: `Selected`
   * **Tipo**: `Boolean`

* **Percorso**
( `cq.wcm.undo.path`)

   * **Descrizione**: il percorso dell&#39;archivio per i dati di annullamento binari persistenti. Quando gli autori modificano dati binari come immagini, la versione originale dei dati viene mantenuta qui. Quando le modifiche ai dati binari vengono annullate, questi dati di annullamento binari vengono ripristinati nella pagina.
   * **Predefinito**: `/var/undo`
   * **Tipo**: `String`

  >[!NOTE]
  >
  >Per impostazione predefinita, solo gli amministratori possono accedere al nodo `/var/undo`. Gli autori possono eseguire operazioni Annulla e Ripristina sul contenuto binario solo dopo aver ottenuto le autorizzazioni necessarie per accedere ai dati di annullamento binari.

* **min. validità**
( `cq.wcm.undo.validity`)

   * **Descrizione**: quantità minima di tempo per la memorizzazione dei dati di annullamento binari, in ore. Dopo questo periodo di tempo, i dati binari sono disponibili per l&#39;eliminazione, per risparmiare spazio su disco.
   * **Predefinito**: `10`
   * **Tipo**: `Integer`

* **Passaggi**
( `cq.wcm.undo.steps`)

   * **Descrizione**: numero massimo di azioni di pagina archiviate nella cronologia di annullamento.
   * **Predefinito**: `20`
   * **Tipo**: `Integer`

* **Persistenza**
( `cq.wcm.undo.persistence`)

   * **Descrizione**: classe che persiste nella cronologia delle operazioni Annulla. Sono fornite due classi di persistenza:

      * `CQ.undo.persistence.WindowNamePersistence`: mantiene la cronologia utilizzando la proprietà window.name.
      * `CQ.undo.persistence.CookiePersistance`: persiste la cronologia utilizzando i cookie.

   * **Predefinito**: `CQ.undo.persistence.WindowNamePersistence`
   * **Tipo**: `String`

* **Modalità persistenza**
( `cq.wcm.undo.persistence.mode`)

   * **Descrizione**: determina quando la cronologia delle operazioni di annullamento viene mantenuta. Selezionare questa opzione per rendere persistente la cronologia delle operazioni Annulla dopo ogni modifica della pagina. Deseleziona questa opzione per renderla persistente solo quando si verifica un ricaricamento della pagina (ad esempio, l’utente passa a una pagina diversa).

     La cronologia degli undo persistenti utilizza le risorse del browser Web. Se il browser degli utenti reagisce lentamente alle modifiche apportate alla pagina, prova a mantenere la cronologia delle operazioni Annulla durante i ricaricamenti della pagina.

   * **Predefinito**: `Selected`
   * **Tipo**: `Boolean`

* **Modalità marcatore**
( `cq.wcm.undo.markermode`)

   * **Descrizione**: specifica il segnale visivo da utilizzare per indicare i paragrafi interessati quando si verifica un annullamento o un ripristino. I seguenti valori sono validi:

      * flash: l&#39;indicatore di selezione dei paragrafi lampeggia temporaneamente.
      * select: Il paragrafo viene selezionato.

   * **Predefinito**: `flash`
   * **Tipo**: `String`

* **Componenti validi**
( `cq.wcm.undo.whitelist`)

   * **Descrizione**: elenco di componenti che devono essere interessati dai comandi Annulla e Ripristina. Aggiungete i percorsi dei componenti a questo elenco quando funzionano correttamente con Annulla/Ripristina. Aggiungete un asterisco (&ast;) per specificare un gruppo di componenti:

      * Il valore seguente specifica il componente testo di base:

        `foundation/components/text`

      * Il valore seguente specifica tutti i componenti di base:

        `foundation/components/*`

   * Quando si esegue un&#39;operazione Annulla o Ripristina su un componente non incluso nell&#39;elenco, viene visualizzato un messaggio che indica che il comando può essere inaffidabile.

   * **Predefinito**: la proprietà è compilata con molti componenti forniti da AEM.
   * **Tipo**: `String[]`

* **Componenti non validi**
( `cq.wcm.undo.blacklist`)

   * **Descrizione**: elenco di componenti e/o operazioni di componenti che non si desidera siano interessati dal comando Annulla. Aggiungi componenti e operazioni sui componenti che non si comportano correttamente con il comando Annulla:

      * Aggiungere un percorso di componente quando non si desidera eseguire nessuna delle operazioni del componente nella cronologia di annullamento, ad esempio `collab/forum/components/post`
      * Aggiungere i due punti (:) e un&#39;operazione al percorso quando si desidera che tale operazione specifica venga omessa dalla cronologia di annullamento (altre operazioni funzionano correttamente), ad esempio `collab/forum/components/post:insertParagraph.`

  >[!NOTE]
  >
  >Quando un&#39;operazione si trova in questo elenco, viene comunque aggiunta alla cronologia di annullamento. Gli utenti non possono annullare operazioni precedenti a un&#39;operazione di tipo **Componente non valido** nella cronologia delle operazioni di annullamento.

   * Di seguito sono riportati i nomi tipici delle operazioni:

      * `insertParagraph`: componente aggiunto alla pagina.
      * `removeParagraph`: componente eliminato.
      * `moveParagraph`: il paragrafo è stato spostato in una posizione diversa.
      * `updateParagraph`: le proprietà del paragrafo vengono modificate.

   * **Predefinito**: la proprietà è compilata con diverse operazioni del componente.
   * **Tipo**: `String[]`
