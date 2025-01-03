---
title: Modifica e conversione di domini esistenti
description: Scopri come modificare le impostazioni per i domini esistenti dalla pagina Gestione dominio. Convertire un dominio enterprise esistente in un dominio ibrido o viceversa.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 34ac5f8b-f209-4f99-ad71-4df6f2c88c1e
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# Modifica e conversione di domini esistenti{#editing-and-converting-existing-domains}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Puoi modificare le impostazioni per i domini esistenti dalla pagina Gestione dominio. È inoltre possibile convertire un dominio enterprise esistente in un dominio ibrido.

## Modificare un dominio esistente {#edit-an-existing-domain}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fai clic sul nome del dominio da modificare.
1. Per modificare il nome di dominio, modificare il testo nella casella Nome.
1. Per modificare le informazioni di autenticazione per un dominio enterprise o ibrido, fai clic sul nome di autenticazione appropriato nella parte inferiore della pagina. Nella pagina Modifica autenticazione modificare le impostazioni in base alle esigenze. (Vedi [Impostazioni di autenticazione](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. Per modificare le informazioni sulla directory per un dominio enterprise, fare clic sul nome di directory appropriato nella parte inferiore della pagina. Nella pagina Modifica directory modificare le impostazioni in base alle esigenze. (Vedi [Aggiunta di directory o SPI personalizzati](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis).)
1. Al termine delle modifiche, fare clic su OK.

## Convertire un dominio enterprise in un dominio ibrido {#convert-an-enterprise-domain-to-a-hybrid-domain}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fare clic sul nome del dominio enterprise da convertire.
1. Fai clic su Converti in dominio ibrido.
1. Esaminare le informazioni visualizzate relative ai dati di utenti e gruppi e all&#39;autenticazione degli utenti, quindi fare clic su OK.
1. Modificare le impostazioni per il dominio ibrido e fare clic su OK.

>[!NOTE]
>
>Se il dominio enterprise che si sta convertendo non contiene impostazioni di directory, tutte le impostazioni di autenticazione LDAP andranno perse.

## Convertire un dominio ibrido in un dominio enterprise {#convert-a-hybrid-domain-to-an-enterprise-domain}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fai clic sul nome del dominio ibrido da convertire.
1. Fare clic su Converti in dominio enterprise.
1. Esaminare le informazioni visualizzate relative ai dati di utenti e gruppi e all&#39;autenticazione degli utenti, quindi fare clic su OK.
1. Fai clic su Aggiungi directory e configura le informazioni richieste sulla directory. (Vedi [Aggiunta di directory o SPI personalizzati](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis).)
