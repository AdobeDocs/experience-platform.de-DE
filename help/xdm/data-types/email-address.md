---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; emailAddress; xdm:emailAddress; E-Mail; E-Mail-Adresse; E-Mail-Adresse; Datentyp; Datentyp;
solution: Experience Platform
title: Datentyp E-Mail-Adresse
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über den XDM-Datentyp "E-Mail-Adresse".
exl-id: 1364df42-f89f-4f48-bcda-5332f3828326
source-git-commit: fe6abe468025ab3373f802954aedceeb1af625fe
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 4%

---

# [!UICONTROL Email-Adresse] Datentyp

[!UICONTROL Email-Adresse] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der die Details einer E-Mail-Adresse beschreibt.

<img src="../images/data-types/email-address.png" width="450" /><br />

| Eigenschaft | Beschreibung |
| --- | --- |
| `address` | Die technische Adresse der E-Mail, wie sie üblicherweise in RFC2822 und nachfolgenden Standards definiert ist (z. B. `name@domain.com`).<br><br>In XDM müssen E-Mail-Adressen eine gültige Domäne der obersten Ebene enthalten, um die Validierung zu bestehen. Siehe Folgendes [Dokument](https://data.iana.org/TLD/tlds-alpha-by-domain.txt) für eine vollständige Liste der gültigen Top-Level-Domains, wie von der Internet Assigned Numbers Authority (IANA) definiert. |
| `label` | Zusätzliche verfügbare Anzeigeinformationen. Wenn beispielsweise eine E-Mail eine Rich-Adresse in Microsoft Outlook aufweist, wird Folgendes angezeigt: `John Smith smithjr@company.uk`, `John Smith` in dieses Feld eingefügt werden. |
| `primary` | Gibt an, ob dies die primäre E-Mail-Adresse des Kontakts ist. Ein Profil kann nur eine `primary` E-Mail-Adresse zu einem bestimmten Zeitpunkt. |
| `status` | Gibt an, ob die E-Mail-Adresse derzeit verwendet werden kann |
| `statusReason` | Eine Beschreibung des aktuellen `status`. |
| `type` | Die Art und Weise, wie das Konto die Person betrifft (z. B. `work` oder `personal`). |

{style=&quot;table-layout:auto&quot;}


Weitere Informationen zum Datentyp der E-Mail-Adresse finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.schema.json)
