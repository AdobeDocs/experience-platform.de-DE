---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; emailAddress; xdm:emailAddress; E-Mail; E-Mail-Adresse; E-Mail-Adresse; Datentyp; Datentyp;
solution: Experience Platform
title: Datentyp E-Mail-Adresse
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über den XDM-Datentyp "E-Mail-Adresse".
exl-id: 1364df42-f89f-4f48-bcda-5332f3828326
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 5%

---

# [!UICONTROL Datentyp ] der E-Mail-Adresse

[!UICONTROL E-Mail-] Adresse ist ein standardmäßiger XDM-Datentyp, der die Details einer E-Mail-Adresse beschreibt.

<img src="../images/data-types/email-address.png" width="450" /><br />

| Eigenschaft | Beschreibung |
| --- | --- |
| `address` | Die technische Adresse der E-Mail, wie sie üblicherweise in RFC2822 und nachfolgenden Standards definiert ist (z. B. `name@domain.com`). |
| `label` | Zusätzliche verfügbare Anzeigeinformationen. Wenn eine E-Mail beispielsweise eine Rich-Adresse von Microsoft Outlook mit `John Smith smithjr@company.uk` aufweist, wird `John Smith` in dieses Feld eingefügt. |
| `primary` | Gibt an, ob dies die primäre E-Mail-Adresse des Kontakts ist. Ein Profil kann zu einem bestimmten Zeitpunkt nur eine `primary` E-Mail-Adresse haben. |
| `status` | Gibt an, ob die E-Mail-Adresse derzeit verwendet werden kann |
| `statusReason` | Eine Beschreibung des aktuellen `status`. |
| `type` | Die Art, wie das Konto mit der Person in Beziehung steht (z. B. `work` oder `personal`). |

{style=&quot;table-layout:auto&quot;}


Weitere Informationen zum Datentyp der E-Mail-Adresse finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/emailaddress.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/emailaddress.schema.json)
