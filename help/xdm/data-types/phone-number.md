---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;Schema;XDM;Felder;Schemata;Schemata;Telefonnummer;xdm:phoneNumber;datatype;Datentyp;Datentyp;
solution: Experience Platform
title: Datentyp der Telefonnummer
description: Erfahren Sie mehr über den XDM-Datentyp Telefonnummer .
exl-id: b84e48f9-bbb4-4b8b-9476-4bc1c455ecfd
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 17%

---

# [!UICONTROL Telefonnummer] Datentyp

[!UICONTROL Telefonnummer] ist ein standardmäßiger XDM-Datentyp, der die Details einer Telefonnummer beschreibt.

![](../images/data-types/phone-number.png){width=600}

| Eigenschaft | Beschreibung |
| --- | --- |
| `extension` | Die interne Wählnummer, die für Anrufe von einer privaten Vermittlungsstelle, einem Operator oder einer Telefonzentrale verwendet wird. |
| `number` | Die Telefonnummer. Beachten Sie, dass die Telefonnummer eine Zeichenfolge ist und aussagekräftige Zeichen wie Klammern `()`, Bindestriche `-` oder Zeichen zur Angabe von Unterwahlkennungen wie Erweiterungen `x` z. B. `1-353(0)18391111` oder `+613 9403600x1234` enthalten kann. |
| `primary` | Ein boolescher Wert, der angibt, ob dies die primäre Telefonnummer des Kontakts ist. Im Gegensatz zu Adresse oder E-Mail-Adresse kann es mehrere primäre Telefonnummern geben; eine pro Kommunikationskanal. Der Kommunikationskanal wird durch den Typ definiert (angegeben durch den Namen der übergeordneten Eigenschaft): `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown` und `fax`. |
| `status` | Zeigt an, ob die Telefonnummer derzeit verwendet werden kann. |
| `statusReason` | Eine Beschreibung des aktuellen Status. |
| `validity` | Ein Grad der technischen Korrektheit der Telefonnummer. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp der Telefonnummer finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/phonenumber.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/phonenumber.schema.json)
