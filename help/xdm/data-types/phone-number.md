---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;Felder;Schemas;Schemas;phoneNumber;xdm:phoneNumber;datatype;Datentyp;Datentyp;
solution: Experience Platform
title: Telefonnummerndatentyp
topic: overview
description: Dieses Dokument bietet eine Übersicht über den XDM-Datentyp für Telefonnummer.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 9%

---


# [!UICONTROL Datentyp ] für Telefonnummern

[!UICONTROL Die ] Telefonnummer ist ein standardmäßiger XDM-Datentyp, der die Details einer Telefonnummer beschreibt.

<img src="../images/data-types/phone-number.png" width="600" /><br />

| Eigenschaft | Beschreibung |
| --- | --- |
| `extension` | Die interne Wählnummer, die für den Anruf von einer privaten Börse, einem Betreiber oder einer Schalttafel verwendet wird. |
| `number` | Die Telefonnummer. Beachten Sie, dass die Telefonnummer eine Zeichenfolge ist, die aussagekräftige Zeichen wie Klammern `()`, Bindestriche `-` oder Zeichen enthalten kann, die auf Unterwählungs-IDs wie Erweiterungen `x` hinweisen, z. B. `1-353(0)18391111` oder `+613 9403600x1234`. |
| `primary` | Ein boolescher Wert, der angibt, ob es sich hierbei um die primäre Telefonnummer des Benutzers handelt. Im Gegensatz zu Adresse oder E-Mail-Adresse kann es mehrere primäre Telefonnummern geben. eine pro Kommunikations-Kanal. Der kommunikation-Kanal wird durch den Typ definiert (durch den Namen der übergeordneten Eigenschaft angegeben): `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown` und `fax`. |
| `status` | Gibt an, ob die Telefonnummer derzeit verwendet werden kann. |
| `statusReason` | Eine Beschreibung des aktuellen Status. |
| `validity` | Ein Grad der technischen Korrektheit der Telefonnummer. |

Weitere Informationen zum Datentyp der Telefonnummer finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/phonenumber.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/phonenumber.schema.json)