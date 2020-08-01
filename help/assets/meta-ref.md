---
title: Riferimento schemi metadati
description: 'Scoprite le convenzioni standard per la descrizione dei metadati delle risorse, inclusi Dublin Core, IPTC e altri schemi di metadati. '
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 2%

---


# Riferimento schemi metadati {#metadata-schemata-reference}

Il riferimento seguente contiene informazioni su uno specifico schema di metadati (in ordine alfabetico), un elenco delle proprietà e delle relative definizioni.

## Dublin Core {#dublin-core}

I metadati Dublin Core forniscono un set standardizzato di convenzioni per la descrizione delle risorse, al fine di facilitarne la ricerca. In [!DNL Assets]Dublin Core descrive le risorse digitali come video, audio, immagini e documenti.

Il semplice set di metadati Dublin Core Metadata Element Set (DCMES) contiene 15 elementi di metadati, come elencato nella tabella seguente. Ciascun elemento Dublin Core è facoltativo e può essere ripetuto. Potete aggiungere o eliminare i metadati Dublin Core come fareste per i metadati specifici per i tipi di supporti.

Oltre al DCMES, esistono altri elementi di metadati creati dall&#39;iniziativa Dublin Core. Per ulteriori informazioni, consulta [Dublin Core Initiative](https://dublincore.org/) .

| Proprietà | Descrizione |
| ----------- | ------------------------------------------------------------------------------------------------------------------------ |
| collaboratore | La persona o la società responsabile del contributo al contenuto. |
| cover | La posizione geografica o il periodo di tempo coperto dall&#39;attività. |
| creatore | La persona o la società responsabile della creazione del contenuto. |
| data | Data o periodo di tempo associato alla risorsa. |
| descrizione | Ulteriori informazioni sulla risorsa. |
| format | Il formato file, il supporto fisico o le dimensioni della risorsa. [!DNL Experience Manager] utilizza `dc:format` per indicare il tipo MIME della risorsa. |
| identifier | Un riferimento univoco alla risorsa. |
| language | La lingua della risorsa (ad esempio, en per l’inglese). |
| publisher | La persona o la società responsabile della messa a disposizione della risorsa. |
| relation | Una risorsa correlata. |
| rights | Informazioni su chi dispone dei diritti per questa risorsa. |
| source | Un&#39;attività correlata da cui è derivata l&#39;attività. |
| subject | Argomento della risorsa. |
| titolo | Un nome per la risorsa. |
| tipo | La natura o il genere del bene. |

## IPTC {#iptc}

L&#39;International Press Telecommunications Council (IPTC) è un consorzio di agenzie di informazione di tutto il mondo, uno dei suoi obiettivi è quello di sviluppare e mantenere gli standard tecnici. L&#39;IPTC ha definito una serie di standard di metadati fotografici per le immagini che sono quasi universalmente accettati dai fotografi. Questi standard di metadati facevano parte dello standard più ampio noto come IPTC Information Interchange Model (IIM) creato negli anni &#39;90.

Sebbene le informazioni dell&#39;intestazione IPTC siano state in gran parte sostituite da XMP, per XMP sono disponibili uno schema di base IPTC e uno schema di estensione. Nei programmi di immagini, le proprietà XMP e IPTC sono sincronizzate.
