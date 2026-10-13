---
title: Modifica e conversione di domini esistenti
description: Scopri come modificare le impostazioni di domini esistenti nella pagina Gestione dominio. Converti un dominio Enterprise esistente in un dominio ibrido o viceversa.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 34ac5f8b-f209-4f99-ad71-4df6f2c88c1e
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 100%
---
# Modifica e conversione di domini esistenti{#editing-and-converting-existing-domains}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Puoi modificare le impostazioni di domini esistenti nella pagina Gestione dominio. Puoi, inoltre, convertire un dominio enterprise esistente in un dominio ibrido.

## Modificare un dominio esistente {#edit-an-existing-domain}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utenti > Gestione dominio.
1. Fai clic sul nome del dominio per modificarlo.
1. Per modificare il nome del dominio, cambia il testo nella casella Nome.
1. Per modificare le informazioni di autenticazione per un dominio enterprise o ibrido, fai clic sul nome di autenticazione appropriato nella parte inferiore della pagina. Nella pagina Modifica autenticazione, cambia le impostazioni in base alle esigenze. (Consulta [Impostazioni di autenticazione](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. Per modificare le informazioni sulla directory di un dominio enterprise, fai clic sul nome di directory appropriato nella parte inferiore della pagina. Nella pagina Modifica directory, cambia le impostazioni in base alle esigenze. (Consulta [Aggiunta di directory o SPI personalizzati](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis).)
1. Al termine delle modifiche, fai clic su OK.

## Convertire un dominio enterprise in un dominio ibrido {#convert-an-enterprise-domain-to-a-hybrid-domain}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utenti > Gestione dominio.
1. Fai clic sul nome del dominio enterprise da convertire.
1. Fai clic su Converti in dominio ibrido.
1. Esamina le informazioni visualizzate relative ai dati di utenti e gruppi e all’autenticazione degli utenti, quindi fai clic su OK.
1. Modifica le impostazioni del dominio ibrido e fai clic su OK.

>[!NOTE]
>
>Se il dominio enterprise che stai convertendo non contiene impostazioni di directory, tutte le impostazioni di autenticazione LDAP andranno perse.

## Convertire un dominio ibrido in un dominio enterprise {#convert-a-hybrid-domain-to-an-enterprise-domain}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utenti > Gestione dominio.
1. Fai clic sul nome del dominio ibrido da convertire.
1. Fai clic su Converti in dominio enterprise.
1. Esamina le informazioni visualizzate relative ai dati di utenti e gruppi e all’autenticazione degli utenti, quindi fai clic su OK.
1. Fai clic su Aggiungi directory e configura le informazioni richieste sulla directory. (Consulta [Aggiunta di directory o SPI personalizzati](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis).)
