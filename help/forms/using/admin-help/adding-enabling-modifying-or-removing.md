---
title: Aggiunta, abilitazione, modifica o rimozione di endpoint
seo-title: Adding, enabling, modifying, or removing endpoints
description: Scopri come aggiungere, abilitare, modificare e rimuovere endpoint.
seo-description: Learn how to add, enable, modify and remove endpoints.
uuid: c53f225b-3d55-42f6-8982-0cd7dde0c4f5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7d0d4f96-fc72-4e2b-a2cc-5741b0a30f74
exl-id: b7461d5c-95d1-4da2-9d2a-f54c410a87f9
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# Aggiunta, abilitazione, modifica o rimozione di endpoint {#adding-enabling-modifying-or-removing-endpoints}

## Aggiungere un endpoint a un servizio {#add-an-endpoint-to-a-service}

Gli endpoint possono essere aggiunti solo ai servizi. Un endpoint non può esistere da solo, ma deve essere associato a un servizio.

>[!NOTE]
>
>È consigliabile utilizzare nomi univoci quando si aggiungono endpoint.

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione servizi.
1. Nella pagina Gestione servizio fare clic sul servizio da configurare.
1. Nell&#39;elenco della scheda Endpoints, selezionare il tipo di endpoint da aggiungere e fare clic su Aggiungi.
1. A seconda del tipo di endpoint, configura impostazioni endpoint aggiuntive.

[Impostazioni endpoint cartella controllata](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings)

[Impostazioni endpoint e-mail](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings)

[Configurazione degli endpoint di Task Manager](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints)

[Impostazioni endpoint remoto](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings)

1. Fai clic su Aggiungi.

## Attivare o disattivare un endpoint {#enable-or-disable-an-endpoint}

Per impostazione predefinita, i nuovi endpoint vengono attivati automaticamente. Tuttavia, se hai disattivato un endpoint, devi attivarlo affinché sia operativo.

Se riscontri problemi con i servizi, disattiva gli endpoint associati per una migliore risoluzione del problema. È inoltre possibile disattivare gli endpoint durante la normale manutenzione del sistema o durante l&#39;aggiornamento di un servizio.

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione endpoint.
1. Nella pagina Gestione endpoint selezionare la casella di controllo relativa all&#39;endpoint da attivare o disattivare e fare clic su Attiva o Disattiva.

## Modificare un endpoint {#modify-an-endpoint}

>[!NOTE]
>
>Le modifiche apportate alla configurazione di un endpoint tramite la console di amministrazione non vengono riportate nelle copie delle applicazioni in fase di progettazione. Se si ridistribuisce un&#39;applicazione, tutte le modifiche apportate agli endpoint mediante la console di amministrazione andranno perse.

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione endpoint.
1. Nella pagina Gestione endpoint fare clic sull&#39;endpoint da modificare.
1. Nella pagina Aggiorna endpoint modificare il nome, la descrizione e le impostazioni dell&#39;endpoint.

   >[!NOTE]
   >
   >Non includere un carattere &lt; nel nome o nella descrizione, poiché il nome o la descrizione visualizzati in Workspace verranno troncati.

1. Per salvare le modifiche, fare clic su Aggiorna.

È inoltre possibile eseguire questa operazione dalla pagina Gestione servizi selezionando un servizio e facendo clic sulla scheda Endpoint.

## Rimuovere un endpoint {#remove-an-endpoint}

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione endpoint.
1. Nella pagina Gestione endpoint selezionare la casella di controllo relativa all&#39;endpoint da rimuovere e fare clic su Rimuovi. L’endpoint non viene più visualizzato.
