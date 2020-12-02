---
title: Modifica e conversione di domini esistenti
seo-title: Modifica e conversione di domini esistenti
description: Scopri come modificare le impostazioni per i domini esistenti dalla pagina Gestione dominio. Conversione di un dominio enterprise esistente in un dominio ibrido o viceversa.
seo-description: Scopri come modificare le impostazioni per i domini esistenti dalla pagina Gestione dominio. Conversione di un dominio enterprise esistente in un dominio ibrido o viceversa.
uuid: 4cc9547e-b4ec-4588-b1cf-18720f06149a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 44dec184-3ef7-4ba6-a87f-ad171d3cb188
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---


# Modifica e conversione di domini esistenti{#editing-and-converting-existing-domains}

Puoi modificare le impostazioni per i domini esistenti dalla pagina Gestione dominio. È inoltre possibile convertire un dominio enterprise esistente in un dominio ibrido.

## Modificare un dominio esistente {#edit-an-existing-domain}

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fate clic sul nome del dominio da modificare.
1. Per modificare il nome del dominio, modificare il testo nella casella Nome.
1. Per modificare le informazioni di autenticazione per un dominio Enterprise o ibrido, fate clic sul nome di autenticazione appropriato nella parte inferiore della pagina. Nella pagina Modifica autenticazione, modificate le impostazioni in base alle esigenze. (Vedere [Impostazioni di autenticazione](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. Per modificare le informazioni di directory per un dominio Enterprise, fate clic sul nome di directory appropriato nella parte inferiore della pagina. Nella pagina Edit Directory (Modifica directory), modificate le impostazioni come necessario. (Vedere [Aggiunta di directory o SPI](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis) personalizzati.)
1. Una volta completate le modifiche, fate clic su OK.

## Conversione di un dominio Enterprise in un dominio ibrido {#convert-an-enterprise-domain-to-a-hybrid-domain}

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fate clic sul nome del dominio enterprise da convertire.
1. Fare clic su Converti in dominio ibrido.
1. Esaminate le informazioni visualizzate in merito ai dati utente e di gruppo e all’autenticazione degli utenti, quindi fate clic su OK.
1. Modificate le impostazioni per il dominio ibrido e fate clic su OK.

>[!NOTE]
>
>Se il dominio enterprise che si sta convertendo non contiene impostazioni di directory, tutte le impostazioni di autenticazione LDAP vanno perse.

## Conversione di un dominio ibrido in un dominio Enterprise {#convert-a-hybrid-domain-to-an-enterprise-domain}

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fare clic sul nome del dominio ibrido da convertire.
1. Fate clic su Converti in dominio Enterprise.
1. Esaminate le informazioni visualizzate in merito ai dati utente e di gruppo e all’autenticazione degli utenti, quindi fate clic su OK.
1. Fate clic su Aggiungi directory e configurate le informazioni di directory richieste. (Vedere [Aggiunta di directory o SPI](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis) personalizzati.)

