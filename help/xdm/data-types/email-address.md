---
keywords: Experience Platform;home;popular topics;schema;XDM;fields;schemas;Schemas;Schemas;emailAddress;xdm:emailAddress;email;email address;datatype;data-type;data type; data type
solution: Experience Platform
title: Datentyp E-Mail-Adresse
description: Erfahren Sie mehr über den Datentyp "E-Mail-Adresse - XDM".
exl-id: 1364df42-f89f-4f48-bcda-5332f3828326
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# Datentyp [!UICONTROL E-Mail-Adresse]

[!UICONTROL E-Mail-Adresse] ist ein standardmäßiger XDM-Datentyp (Experience-Datenmodell), der die Details einer E-Mail-Adresse beschreibt.

<img src="../images/data-types/email-address.png" width="450" /><br />

| Eigenschaft | Beschreibung |
| --- | --- |
| `address` | Die technische Adresse der E-Mail, wie sie üblicherweise in RFC2822 und nachfolgenden Standards definiert ist (z. B. `name@domain.com`).<br><br>In XDM müssen E-Mail-Adressen eine gültige Domäne der obersten Ebene enthalten, damit die Validierung besteht. Eine vollständige Liste der gültigen Top-Level-Domänen, wie von der Internet Assigned Numbers Authority (IANA) definiert, finden Sie im folgenden [Dokument](https://data.iana.org/TLD/tlds-alpha-by-domain.txt) . |
| `label` | Zusätzliche verfügbare Anzeigeinformationen. Wenn eine E-Mail beispielsweise über eine Rich-Adresse in Microsoft Outlook mit dem Wert `John Smith smithjr@company.uk` verfügt, wird in dieses Feld der Wert `John Smith` eingefügt. |
| `primary` | Gibt an, ob dies die primäre E-Mail-Adresse des Kontakts ist. Ein Profil kann zu einem bestimmten Zeitpunkt nur eine `primary` E-Mail-Adresse haben. |
| `status` | Gibt an, ob die E-Mail-Adresse derzeit verwendet werden kann |
| `statusReason` | Eine Beschreibung des aktuellen `status`. |
| `type` | Die Art, wie das Konto mit der Person in Beziehung steht (z. B. `work` oder `personal`). |

{style="table-layout:auto"}


Weitere Informationen zum Datentyp der E-Mail-Adresse finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.schema.json)
