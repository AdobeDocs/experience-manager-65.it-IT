---
title: Eliminazione di moduli e risorse correlate
seo-title: Eliminazione di moduli e risorse correlate
description: Come eliminare un modulo o una risorsa in  AEM Forms e l'impatto sulle risorse di riferimento e di provenienza e sui moduli XFA.
seo-description: Come eliminare un modulo o una risorsa in  AEM Forms e l'impatto sulle risorse di riferimento e di provenienza e sui moduli XFA.
uuid: df522b87-59d8-4678-922d-c9aab82b1381
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: c8519eec-f841-4867-baa9-a9e03042755e
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---


# Eliminazione di moduli e risorse correlate {#deleting-forms-and-related-resources}

È possibile eliminare moduli e risorse per rimuovere tali risorse dalla directory archivio. L’operazione di eliminazione funziona su tutti i tipi di risorse e cartelle.

Se eliminate una risorsa dall’istanza Autore, anche la risorsa viene eliminata dall’istanza Pubblica.  server AEM Forms è costituito da istanze Author e Publish. L’istanza Author consente di creare e gestire le risorse e le risorse dei moduli. L&#39;istanza Pubblica contiene le risorse dei moduli pubblicati e le risorse correlate disponibili per gli utenti finali.

## Come eliminare un modulo {#how-to-delete-a-form}

1. Accedete all&#39;interfaccia utente  AEM Forms, accedendo a `https://[hostname]:'port'/aem/forms.html.`
1. Individuare e selezionare il modulo da eliminare. Fare clic su Elimina ![aem6forms_delete2](assets/aem6forms_delete2.png) dalla barra degli strumenti e confermare l&#39;operazione di eliminazione.

   >[!NOTE]
   >
   >È possibile eliminare un solo modulo alla volta. Eliminare più moduli singolarmente o eliminare la cartella principale.

1. Prima di eliminare una risorsa,  AEM Forms verifica la presenza di riferimenti e richiede una conferma esplicita. Fate clic su Forza eliminazione per eliminare la risorsa indipendentemente dallo stato della relazione.

   >[!NOTE]
   >
   >L’eliminazione di una risorsa cui fanno riferimento altre risorse può causare problemi funzionali.

   >[!NOTE]
   >
   >Se la risorsa selezionata è una cartella e contiene tale risorsa nella sua gerarchia, eliminate le altre risorse singolarmente o eliminate l’intera cartella.

## Impatto dell&#39;eliminazione di un modulo XFA di riferimento {#impact-of-deleting-a-referenced-xfa-form}

In  AEM Forms, è possibile fare riferimento a un modello di modulo XFA in un modulo adattivo o in un altro modello di modulo XFA. Inoltre, un modello può fare riferimento a una risorsa o a un altro modello XFA.

Non è consigliabile eliminare un modulo XFA cui viene fatto riferimento da un modulo adattivo, in quanto potrebbe danneggiare il modulo adattivo. Quando un modulo adattivo fa riferimento a un modulo XFA, i relativi campi sono associati. Dopo l&#39;eliminazione XFA, il modulo adattivo non è in grado di sincronizzare i campi con i campi XFA e visualizza un messaggio di errore per tali campi. Per ulteriori informazioni sull&#39;impatto dell&#39;eliminazione XFA di riferimento e sui AF sporchi, vedere [Aggiornamento dei moduli XFA di riferimento](/help/forms/using/get-xdp-pdf-documents-aem.md#p-updating-referenced-xfa-forms-p).

Per eliminare un modulo XFA di questo tipo, aggiornare il modulo adattivo e rimuovere i binding con i campi XFA.
