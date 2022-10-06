---
title: Modifica e conversione di domini esistenti
seo-title: Editing and converting existing domains
description: Scopri come modificare le impostazioni per i domini esistenti dalla pagina Gestione dominio. Converti un dominio enterprise esistente in un dominio ibrido o viceversa.
seo-description: Learn how to change the settings for existing domains from the Domain Management page. Convert an existing enterprise domain to a hybrid domain or vice versa.
uuid: 4cc9547e-b4ec-4588-b1cf-18720f06149a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 44dec184-3ef7-4ba6-a87f-ad171d3cb188
exl-id: 34ac5f8b-f209-4f99-ad71-4df6f2c88c1e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---

# Modifica e conversione di domini esistenti{#editing-and-converting-existing-domains}

Puoi modificare le impostazioni per i domini esistenti dalla pagina Gestione dominio. È inoltre possibile convertire un dominio enterprise esistente in un dominio ibrido.

## Modificare un dominio esistente {#edit-an-existing-domain}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fai clic sul nome del dominio da modificare.
1. Per modificare il nome di dominio, modificare il testo nella casella Nome.
1. Per modificare le informazioni di autenticazione per un dominio enterprise o ibrido, fai clic sul nome di autenticazione appropriato nella parte inferiore della pagina. Nella pagina Modifica autenticazione modificare le impostazioni in base alle esigenze. (Vedi [Impostazioni di autenticazione](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. Per modificare le informazioni sulla directory di un dominio enterprise, fare clic sul nome della directory appropriata nella parte inferiore della pagina. Nella pagina Modifica directory modificare le impostazioni in base alle esigenze. (Vedi [Aggiunta di directory o SPI personalizzati](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis).)
1. Una volta completate le modifiche, fare clic su OK.

## Convertire un dominio enterprise in un dominio ibrido {#convert-an-enterprise-domain-to-a-hybrid-domain}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fare clic sul nome del dominio dell&#39;organizzazione da convertire.
1. Fare clic su Converti in dominio ibrido.
1. Controllare le informazioni visualizzate relative ai dati utente e gruppo e l&#39;autenticazione degli utenti, quindi fare clic su OK.
1. Modificare le impostazioni del dominio ibrido e fare clic su OK.

>[!NOTE]
>
>Se il dominio enterprise che si sta convertendo non contiene impostazioni di directory, tutte le impostazioni di autenticazione LDAP andranno perse.

## Convertire un dominio ibrido in un dominio enterprise {#convert-a-hybrid-domain-to-an-enterprise-domain}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fai clic sul nome del dominio ibrido da convertire.
1. Fare clic su Converti in dominio Enterprise.
1. Controllare le informazioni visualizzate relative ai dati utente e gruppo e l&#39;autenticazione degli utenti, quindi fare clic su OK.
1. Fare clic su Aggiungi directory e configurare le informazioni di directory richieste. (Vedi [Aggiunta di directory o SPI personalizzati](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis).)
