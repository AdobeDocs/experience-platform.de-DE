---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;Schema;XDM;Felder;Schemata;Schemata;emailAddress;xdm:emailAddress;E-Mail;E-Mail-Adresse;Datentyp;Datentyp;
solution: Experience Platform
title: Datentyp der E-Mail-Adresse
description: Erfahren Sie mehr über den XDM-Datentyp der E-Mail-Adresse.
exl-id: 1364df42-f89f-4f48-bcda-5332f3828326
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# [!UICONTROL E-Mail]Adresse) Datentyp

[!UICONTROL E-Mail]Adresse) ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der die Details einer E-Mail-Adresse beschreibt.

<img src="../images/data-types/email-address.png" width="450" /><br />

| Eigenschaft | Beschreibung |
| --- | --- |
| `address` | Die technische E-Mail-Adresse, wie sie üblicherweise in RFC2822 und nachfolgenden Standards definiert ist (z. B. `name@domain.com`).<br><br>In XDM müssen E-Mail-Adressen eine gültige Domain auf oberster Ebene enthalten, damit die Validierung erfolgreich ist. Eine vollständige Liste der gültigen Top-Level[Domains, wie von der Internet Assigned Numbers Authority (IANA) definiert, finden Sie im folgenden Dokument](https://data.iana.org/TLD/tlds-alpha-by-domain.txt). |
| `label` | Zusätzliche Anzeigeinformationen, die möglicherweise verfügbar sind. Wenn beispielsweise eine E-Mail eine Microsoft Outlook-Rich-Address-Anzeige von `John Smith smithjr@company.uk` aufweist, wird `John Smith` in dieses Feld eingefügt. |
| `primary` | Gibt an, ob dies die primäre E-Mail-Adresse des Kontakts ist. Ein Profil kann zu einem bestimmten Zeitpunkt jeweils nur eine `primary` E-Mail-Adresse haben. |
| `status` | Gibt an, ob die E-Mail-Adresse derzeit verwendet werden kann |
| `statusReason` | Eine Beschreibung des aktuellen `status`. |
| `type` | Die Art und Weise, wie sich das Konto auf die Person bezieht (wie `work` oder `personal`). |

{style="table-layout:auto"}


Weitere Informationen zum Datentyp der E-Mail-Adresse finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.schema.json)
