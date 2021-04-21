---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;Felder;Schemas;Schemas;emailAddress;xdm:emailAddress;email;email address;datatype;data-type;data-type;
solution: Experience Platform
title: Datentyp E-Mail-Adresse
topic-legacy: overview
description: Dieses Dokument bietet eine Übersicht über den XDM-Datentyp der E-Mail-Adresse.
exl-id: 1364df42-f89f-4f48-bcda-5332f3828326
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 3%

---

# [!UICONTROL Datentyp ] für E-Mail-Adressen

[!UICONTROL E-Mail-] Adresse ist ein Standard-XDM-Datentyp, der die Details einer E-Mail-Adresse beschreibt.

<img src="../images/data-types/email-address.png" width="450" /><br />

| Eigenschaft | Beschreibung |
| --- | --- |
| `address` | Die technische Adresse der E-Mail, wie in RFC2822 und den nachfolgenden Standards (z. B. `name@domain.com`) allgemein definiert. |
| `label` | Zusätzliche Anzeigeinformationen, die verfügbar sein können. Beispiel: Wenn eine E-Mail eine Rich-Address-Anzeige von `John Smith smithjr@company.uk` in Microsoft Outlook enthält, wird `John Smith` in dieses Feld eingefügt. |
| `primary` | Gibt an, ob dies die primäre E-Mail-Adresse der Person ist. Ein Profil kann zu einem bestimmten Zeitpunkt nur eine `primary`-E-Mail-Adresse haben. |
| `status` | Gibt an, ob die E-Mail-Adresse derzeit verwendet werden kann |
| `statusReason` | Eine Beschreibung des aktuellen `status`. |
| `type` | Die Art, wie das Konto mit der Person verknüpft ist (z. B. `work` oder `personal`). |


Weitere Informationen zum Datentyp der E-Mail-Adresse finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/emailaddress.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/emailaddress.schema.json)
