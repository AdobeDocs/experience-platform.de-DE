---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;emailAddress;xdm:emailAddress;email;email address;datatype;data-type;data type;
solution: Experience Platform
title: Datentyp E-Mail-Adresse
topic: overview
description: Dieses Dokument bietet eine Übersicht über den XDM-Datentyp der E-Mail-Adresse.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 4%

---


# [!UICONTROL Datentyp für E-Mail-Adresse]

[!UICONTROL Die E-Mail-Adresse] ist ein standardmäßiger XDM-Datentyp, der die Details einer E-Mail-Adresse beschreibt.

<img src="../images/data-types/email-address.png" width="450" /><br />

| Eigenschaft | Beschreibung |
| --- | --- |
| `address` | Die technische Adresse der E-Mail, wie sie in RFC2822 und nachfolgenden Standards (z. B. `name@domain.com`) allgemein definiert ist. |
| `label` | Zusätzliche Anzeigeinformationen, die verfügbar sein können. Wenn eine E-Mail beispielsweise eine Rich-Adresse-Anzeige von Microsoft Outlook enthält `John Smith smithjr@company.uk`, wird `John Smith` diese in dieses Feld eingefügt. |
| `primary` | Gibt an, ob dies die primäre E-Mail-Adresse der Person ist. Ein Profil kann zu einem bestimmten Zeitpunkt nur eine `primary` E-Mail-Adresse haben. |
| `status` | Gibt an, ob die E-Mail-Adresse derzeit verwendet werden kann |
| `statusReason` | Eine Beschreibung des aktuellen `status`. |
| `type` | Die Art, wie das Konto mit der Person verbunden ist (z. B. `work` oder `personal`). |


Weitere Informationen zum Datentyp der E-Mail-Adresse finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/emailaddress.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/emailaddress.schema.json)