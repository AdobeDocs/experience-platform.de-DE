---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;phoneNumber;xdm:phoneNumber;datatype;data-type;data type;
solution: Experience Platform
title: Datentyp Telefonnummer
topic: overview
description: Dieses Dokument bietet eine Übersicht über den XDM-Datentyp für Telefonnummer.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 10%

---


# [!UICONTROL Datentyp Telefonnummer]

[!UICONTROL Telefonnummer] ist ein standardmäßiger XDM-Datentyp, der die Details einer Telefonnummer beschreibt.

<img src="../images/data-types/phone-number.png" width="600" /><br />

| Eigenschaft | Beschreibung |
| --- | --- |
| `extension` | Die interne Wählnummer, die für den Anruf von einer privaten Börse, einem Betreiber oder einer Schalttafel verwendet wird. |
| `number` | Die Telefonnummer. Note the phone number is a string and may include meaningful characters such as brackets `()`, hyphens `-`, or characters to indicate sub-dialing identifiers like extensions `x` for example, `1-353(0)18391111` or `+613 9403600x1234`. |
| `primary` | Ein boolescher Wert, der angibt, ob es sich hierbei um die primäre Telefonnummer des Benutzers handelt. Im Gegensatz zu Adresse oder E-Mail-Adresse kann es mehrere primäre Telefonnummern geben. eine pro Kommunikations-Kanal. Der kommunikation-Kanal wird durch den Typ definiert (durch den Namen der übergeordneten Eigenschaft angegeben): `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown`und `fax`. |
| `status` | Gibt an, ob die Telefonnummer derzeit verwendet werden kann. |
| `statusReason` | Eine Beschreibung des aktuellen Status. |
| `validity` | Ein Grad der technischen Korrektheit der Telefonnummer. |

Weitere Informationen zum Datentyp der Telefonnummer finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/phonenumber.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/phonenumber.schema.json)