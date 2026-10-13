---
title: Gestione degli elenchi di revoche di certificati
description: Scopri come gestire gli elenchi di revoche dei certificati. Puoi importare, modificare ed eliminare gli elenchi di revoche dei certificati (CRL) utilizzando Gestione archivio fonti attendibili.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 01e966f6-a650-4565-80d1-e2297f25da5c
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
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
source-wordcount: '180'
ht-degree: 100%
---
# Gestione degli elenchi di revoche di certificati{#managing-certificate-revocationlists}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Tramite la Gestione dell’archivio fonti attendibili, puoi importare, modificare ed eliminare gli elenchi di revoche di certificati (CRL). Sono supportati gli elenchi di revoche di certificati con codifica Base64 e DER.

## Importare un CRL {#import-a-crl}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione archivio fonti attendibili > Elenchi di revoche di certificati e quindi su Importa.
1. Nella casella Alias digita un identificatore per il CRL.
1. Fai clic su Sfoglia per individuare il CRL e quindi su OK.

## Esportare un CRL {#export-a-crl}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione archivio fonti attendibili > Elenchi di revoche di certificati.
1. Fai clic sul nome dell’alias del CRL in modo da poterlo esportare e quindi su Esporta.
1. Segui le istruzioni per esportare il CRL. I CRL vengono esportati con codifica Base64.
1. Fai clic su OK.

## Eliminare un CRL {#delete-a-crl}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione archivio fonti attendibili > Elenchi di revoche di certificati.
1. Seleziona le caselle di controllo relative ai CRL da eliminare, fai clic su Elimina e quindi su OK.
