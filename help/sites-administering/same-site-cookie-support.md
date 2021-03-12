---
title: Supporto per cookie per lo stesso sito per AEM 6.5
description: Supporto per cookie per lo stesso sito per AEM 6.5
topic-tags: security
translation-type: tm+mt
source-git-commit: ac2f3d69fd20d7779120a194c698d6f0dd6e6a84
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 1%

---


# Supporto per cookie per lo stesso sito per AEM 6.5 {#same-site-cookie-support-for-aem-65}

A partire dalla versione 80, Chrome e versioni successive Safari, ha introdotto un nuovo modello per la sicurezza dei cookie. Questa modalità è progettata per introdurre controlli di sicurezza sulla disponibilità di cookie per siti di terze parti, tramite un’impostazione denominata `SameSite`. Per informazioni più dettagliate, consulta questo [articolo](https://web.dev/samesite-cookies-explained/).

Il valore predefinito di questa impostazione (`SameSite=Lax`) potrebbe causare il mancato funzionamento dell&#39;autenticazione tra istanze o servizi AEM. Questo perché i domini o le strutture URL di questi servizi potrebbero non rientrare nei vincoli di questo criterio dei cookie.

Per ovviare a questo problema, è necessario impostare l’attributo per cookie SameSite su `None` per il token di accesso.

Per farlo, segui i passaggi seguenti:

1. Vai alla console Web all&#39;indirizzo `http://serveraddress:serverport/system/console/configMgr`
1. Cerca e fai clic su **Adobe Granite Token Authentication Handler**
1. Imposta l&#39;attributo **SameSite per il cookie login-token** su `None`, come illustrato nell&#39;immagine seguente
   ![samesite](assets/samesite1.png)
1. Fai clic su Salva
1. Una volta aggiornata questa impostazione e gli utenti vengono disconnessi e connessi di nuovo, i cookie `login-token` avranno impostato l&#39;attributo `None` e saranno inclusi nelle richieste intersito.
