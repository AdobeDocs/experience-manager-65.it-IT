---
title: Eliminazione di moduli e risorse correlate
description: Come eliminare un modulo o una risorsa in AEM Forms e l’impatto sulle risorse di riferimento e di riferimento e sui moduli XFA.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
role: Admin,User
exl-id: b31f9f56-dd33-4478-ad34-01ac7d5a1b40
solution: Experience Manager, Experience Manager Forms
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# Eliminazione di moduli e risorse correlate {#deleting-forms-and-related-resources}

Puoi eliminare i moduli e le risorse per rimuovere tali risorse dall’archivio. L’operazione di eliminazione funziona su tutti i tipi di risorse e le cartelle.

Se elimini una risorsa dall’istanza Autore, viene eliminata anche dall’istanza Pubblica. Il server AEM Forms è costituito dalle istanze Author e Publish. L’istanza di authoring è per la creazione e la gestione delle risorse e delle risorse dei moduli. L’istanza Publish contiene le risorse dei moduli pubblicati e le risorse correlate disponibili per gli utenti finali.

## Come eliminare un modulo {#how-to-delete-a-form}

1. Accedi all’interfaccia utente di AEM Forms, accedendo a `https://[hostname]:'port'/aem/forms.html.`
1. Passare al modulo che si desidera eliminare e selezionarlo. Fai clic su Elimina ![aem6forms_delete2](assets/aem6forms_delete2.png) dalla barra degli strumenti e conferma l’operazione di eliminazione.

   >[!NOTE]
   >
   >È possibile eliminare un solo modulo alla volta. Eliminare più moduli singolarmente o eliminare la cartella principale.

1. Prima di eliminare una risorsa, AEM Forms verifica la presenza di riferimenti e richiede una conferma esplicita. Fai clic su Forza eliminazione se desideri eliminare la risorsa indipendentemente dallo stato della relazione.

   >[!NOTE]
   >
   >L’eliminazione di una risorsa a cui fanno riferimento altre risorse può causare problemi funzionali.

   >[!NOTE]
   >
   >Se la risorsa selezionata è una cartella e contiene tale risorsa nella gerarchia, elimina le altre risorse singolarmente o l’intera cartella.

## Impatto dell’eliminazione di un modulo XFA di riferimento {#impact-of-deleting-a-referenced-xfa-form}

In AEM Forms, è possibile fare riferimento a un modello di modulo XFA da un modulo adattivo o da un altro modello di modulo XFA. Inoltre, un modello può fare riferimento a una risorsa o a un altro modello XFA.

Non è consigliabile eliminare un modulo XFA a cui fa riferimento un modulo adattivo, in quanto potrebbe danneggiare il modulo adattivo. Quando un modulo adattivo fa riferimento a un modulo XFA, i relativi campi sono associati. Dopo l’eliminazione di XFA, il modulo adattivo non è in grado di sincronizzare i propri campi con i campi XFA e visualizza un messaggio di errore per tali campi. Per ulteriori informazioni sull’impatto dell’eliminazione XFA di riferimento e sulle AF sporche, consulta [Aggiornamento dei moduli XFA di riferimento](/help/forms/using/get-xdp-pdf-documents-aem.md#p-updating-referenced-xfa-forms-p).

Per eliminare un modulo XFA di questo tipo, aggiorna il modulo adattivo e rimuovi le associazioni con i campi XFA.
