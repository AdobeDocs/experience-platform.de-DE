---
keywords: Experience Platform;home;popular topics;schema;XDM;fields;schemas;Schemas;phoneNumber;xdm:phoneNumber;datatype;data-type;data-type;data-type
solution: Experience Platform
title: Datentyp Telefonnummer
description: Erfahren Sie mehr über den XDM-Datentyp für Telefonnummern.
exl-id: b84e48f9-bbb4-4b8b-9476-4bc1c455ecfd
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 18%

---

# Datentyp [!UICONTROL Telefonnummer]

[!UICONTROL Telefonnummer] ist ein standardmäßiger XDM-Datentyp, der die Details einer Telefonnummer beschreibt.

<img src="../images/data-types/phone-number.png" width="600" /><br />

| Eigenschaft | Beschreibung |
| --- | --- |
| `extension` | Die interne Wählnummer, die für Anrufe von einer privaten Vermittlungsstelle, einem Operator oder einer Telefonzentrale verwendet wird. |
| `number` | Die Telefonnummer. Beachten Sie, dass die Telefonnummer eine Zeichenfolge ist und aussagekräftige Zeichen wie Klammern `()`, Bindestriche `-` oder Zeichen enthalten kann, die auf IDs für Unterwählungen wie Erweiterungen `x` (z. B. `1-353(0)18391111` oder `+613 9403600x1234` verweisen. |
| `primary` | Ein boolescher Wert, der anzeigt, ob dies die primäre Telefonnummer des Kontakts ist. Im Gegensatz zu Adresse oder E-Mail-Adresse kann es mehrere primäre Telefonnummern geben, eine pro Kommunikationskanal. Der Kommunikationskanal wird durch den Typ definiert (der durch den Namen der übergeordneten Eigenschaft angegeben wird): `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown` und `fax`. |
| `status` | Gibt an, ob die Telefonnummer derzeit verwendet werden kann. |
| `statusReason` | Eine Beschreibung des aktuellen Status. |
| `validity` | Ein Grad der technischen Korrektheit der Telefonnummer. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp der Telefonnummer finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/phonenumber.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/phonenumber.schema.json)
