---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; Telefonnummer; xdm:phoneNumber; Datentyp; Datentyp; Datentyp;
solution: Experience Platform
title: Datentyp Telefonnummer
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über den XDM-Datentyp für Telefonnummern.
exl-id: b84e48f9-bbb4-4b8b-9476-4bc1c455ecfd
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 10%

---

# [!UICONTROL Datentyp ] der Telefonnummer

[!UICONTROL Telefonnummern ] sind ein standardmäßiger XDM-Datentyp, der die Details einer Telefonnummer beschreibt.

<img src="../images/data-types/phone-number.png" width="600" /><br />

| Eigenschaft | Beschreibung |
| --- | --- |
| `extension` | Die interne Wählnummer, die zum Anrufen von einer privaten Börse, einem Betreiber oder einer Telefonzentrale verwendet wird. |
| `number` | Die Telefonnummer. Beachten Sie, dass die Telefonnummer eine Zeichenfolge ist und aussagekräftige Zeichen wie Klammern `()`, Bindestriche `-` oder Zeichen enthalten kann, um untergeordnete Kennungen wie Erweiterungen `x` anzugeben, z. B. `1-353(0)18391111` oder `+613 9403600x1234`. |
| `primary` | Ein boolescher Wert, der anzeigt, ob dies die primäre Telefonnummer des Kontakts ist. Im Gegensatz zu Adresse oder E-Mail-Adresse kann es mehrere primäre Telefonnummern geben. einen pro Kommunikationskanal. Der Kommunikationskanal wird durch den Typ definiert (durch den Namen der übergeordneten Eigenschaft angegeben): `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown` und `fax`. |
| `status` | Gibt an, ob die Telefonnummer derzeit verwendet werden kann. |
| `statusReason` | Eine Beschreibung des aktuellen Status. |
| `validity` | Ein Grad der technischen Korrektheit der Telefonnummer. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zum Datentyp der Telefonnummer finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/phonenumber.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/phonenumber.schema.json)
