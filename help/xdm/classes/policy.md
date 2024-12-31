---
title: Police-Klasse
description: Erfahren Sie mehr über die Policy-Klasse im Experience-Datenmodell (XDM).
exl-id: 56cc8c69-84a0-493e-85c5-e0cd994e4bee
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 3%

---

# [!UICONTROL Policy]-Klasse

Im Experience-Datenmodell (XDM) erfasst die [!UICONTROL Policy]-Klasse den Mindestsatz an Eigenschaften, die eine Versicherungspolice definieren.

![](../images/classes/policy.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `assignedBeneficiary` | Array von [[!UICONTROL Person]](../data-types/person.md)-Datentypen | Erfasst den Begünstigten (oder die Begünstigten), der/die der Richtlinie zugewiesen wurde(n). |
| `benefitAmount` | [[!UICONTROL Währung]](../data-types/currency.md) | Der gemäß den Versicherungsbedingungen zu zahlende Betrag. |
| `location` | [[!UICONTROL Anschrift]](../data-types/postal-address.md) | Der Ort, an dem die Versicherungspolice ausgestellt wird. |
| `owner` | [!UICONTROL Objekt] | Erfasst die Profilinformationen des Versicherungsnehmers. |
| `owner.faxPhone` | [[!UICONTROL Telefonnummer]](../data-types/phone-number.md) | Die Faxnummer des Besitzers. |
| `owner.homeAddress` | [[!UICONTROL Anschrift]](../data-types/postal-address.md) | Die Privatadresse des Eigentümers. |
| `owner.homePhone` | [[!UICONTROL Telefonnummer]](../data-types/phone-number.md) | Die private Telefonnummer des Besitzers. |
| `owner.mobilePhone` | [[!UICONTROL Telefonnummer]](../data-types/phone-number.md) | Die Mobiltelefonnummer des Besitzers. |
| `owner.personalEmail` | [[!UICONTROL E-Mail-Adresse]](../data-types/email-address.md) | Die persönliche E-Mail-Adresse des Inhabers. |
| `ID` | [!UICONTROL String] | Eine Kennung für die Versicherungspolice. |
| `_id` | [!UICONTROL String] | Eine eindeutige, systemgenerierte Zeichenfolgenkennung für den Datensatz. Dieses Feld wird verwendet, um die Eindeutigkeit eines einzelnen Datensatzes nachzuverfolgen, Doppelungen von Daten zu verhindern und diesen Datensatz in nachgelagerten Services nachzuschlagen.<br><br>Da dieses Feld systemgeneriert ist, wird bei der Datenaufnahme kein expliziter Wert bereitgestellt. Sie können jedoch auch weiterhin eigene eindeutige ID-Werte angeben, wenn Sie dies wünschen. |
| `endDate` | [!UICONTROL DateTime] | Das Datum, an dem der Versicherungsschutz endet (oder endet). |
| `hasAssignedBeneficiary` | [!UICONTROL Boolesch] | Gibt an, ob der Richtlinie ein Empfänger zugewiesen wurde. |
| `name` | [!UICONTROL String] | Der Name der Versicherungspolice. |
| `startDate` | [!UICONTROL DateTime] | Das Datum, an dem der Versicherungsschutz beginnt (oder beginnt). |
| `type` | [!UICONTROL String] | Die Art der Versicherungspolice, z. B. Haus, Auto, Mieter oder Boot. |

{style="table-layout:auto"}
