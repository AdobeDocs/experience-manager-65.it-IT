---
title: Gestione degli elenchi di revoche dei certificati
seo-title: Managing certificate revocationlists
description: Scopri come gestire gli elenchi di revoche dei certificati.
seo-description: Learn how to manage certificate revocation lists.
uuid: d8c4b64c-a273-4f5d-8b71-f6ea455c0f0a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9744cc2d-5e6b-4341-9270-43d479bdca04
exl-id: 01e966f6-a650-4565-80d1-e2297f25da5c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 1%

---

# Gestione degli elenchi di revoche dei certificati{#managing-certificate-revocationlists}

Utilizzando la funzione di gestione dell&#39;archivio certificati è possibile importare, modificare ed eliminare elenchi di revoche di certificati (CRL, Certificate Revocation List). Sono supportati gli elenchi di revoche dei certificati con codifica DER e Base64.

## Importare un CRL {#import-a-crl}

1. Nella console di amministrazione, fare clic su Impostazioni > Gestione archivio attendibilità > Elenchi di revoca certificati, quindi fare clic su Importa.
1. Nella casella Alias digitare un identificatore per il CRL.
1. Fare clic su Sfoglia per individuare il CRL e quindi su OK.

## Esportare un CRL {#export-a-crl}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione archivio attendibilità > Elenchi di revoca certificati.
1. Fare clic sul nome dell&#39;alias del CRL da esportare, quindi fare clic su Esporta.
1. Seguire le istruzioni per esportare il CRL. I CRL vengono esportati nella codifica Base64.
1. Fai clic su OK.

## Eliminare un CRL {#delete-a-crl}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione archivio attendibilità > Elenchi di revoca certificati.
1. Selezionare le caselle di controllo per i CRL da eliminare, fare clic su Elimina e quindi su OK.
