---
title: Richtlinienklasse
description: Erfahren Sie mehr über die Policy-Klasse im Experience-Datenmodell (XDM).
exl-id: 56cc8c69-84a0-493e-85c5-e0cd994e4bee
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 3%

---

# [!UICONTROL Policy] class

Im Experience-Datenmodell (XDM) erfasst die Klasse [!UICONTROL Richtlinie] den Mindestsatz von Eigenschaften, die eine Versicherungspolice definieren.

![](../images/classes/policy.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `assignedBeneficiary` | Array von Datentypen für [[!UICONTROL Person]](../data-types/person.md) | Erfasst den Begünstigten (bzw. die Begünstigten), der/die der Politik zugewiesen ist. |
| `benefitAmount` | [[!UICONTROL Währung]](../data-types/currency.md) | Der gemäß den Vertragsbedingungen zu zahlende Betrag. |
| `location` | [[!UICONTROL Postanschrift]](../data-types/postal-address.md) | Der Ort, an dem die Versicherungspolice ausgestellt wird. |
| `owner` | [!UICONTROL Objekt] | Erfasst die Profilinformationen des Versicherungsnehmers. |
| `owner.faxPhone` | [[!UICONTROL Telefonnummer]](../data-types/phone-number.md) | Die Faxnummer des Eigentümers. |
| `owner.homeAddress` | [[!UICONTROL Postanschrift]](../data-types/postal-address.md) | Die Wohnadresse des Eigentümers. |
| `owner.homePhone` | [[!UICONTROL Telefonnummer]](../data-types/phone-number.md) | Die Privattelefonnummer des Eigentümers. |
| `owner.mobilePhone` | [[!UICONTROL Telefonnummer]](../data-types/phone-number.md) | Die Mobiltelefonnummer des Eigentümers. |
| `owner.personalEmail` | [[!UICONTROL E-Mail-Adresse]](../data-types/email-address.md) | Die persönliche E-Mail-Adresse des Eigentümers. |
| `ID` | [!UICONTROL String] | Eine Kennung für die Versicherungspolice. |
| `_id` | [!UICONTROL String] | Eine eindeutige, systemgenerierte Zeichenfolgenkennung für den Datensatz. Dieses Feld wird verwendet, um die Eindeutigkeit eines einzelnen Datensatzes zu verfolgen, Datenduplizierung zu verhindern und diesen Datensatz in nachgelagerten Diensten nachzuschlagen.<br><br>Da dieses Feld systemseitig generiert wird, wird bei der Datenerfassung kein expliziter Wert angegeben. Sie können jedoch weiterhin Ihre eigenen eindeutigen ID-Werte angeben, wenn Sie möchten. |
| `endDate` | [!UICONTROL DateTime] | Das Datum, an dem der Versicherungsschutz endet (oder endete). |
| `hasAssignedBeneficiary` | [!UICONTROL Boolean] | Gibt an, ob der Richtlinie ein Empfänger zugewiesen ist. |
| `name` | [!UICONTROL String] | Der Name der Versicherungspolice. |
| `startDate` | [!UICONTROL DateTime] | Das Datum, an dem der Versicherungsschutz beginnt (oder begonnen hat). |
| `type` | [!UICONTROL String] | Die Art der Versicherungspolice, z. B. zu Hause, Auto, Mieter oder Boot. |

{style="table-layout:auto"}
