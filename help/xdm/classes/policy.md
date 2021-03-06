---
title: Richtlinienklasse
description: Dieses Dokument bietet einen Überblick über die Policy-Klasse im Experience-Datenmodell (XDM).
source-git-commit: c0437b8f9d93c46dbec991a33a893a5b9e0cdf2c
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 11%

---

# [!UICONTROL Politik] class

Im Experience-Datenmodell (XDM) wird die [!UICONTROL Politik] -Klasse erfasst den Mindestsatz von Eigenschaften, die eine Versicherungspolice definieren.

![](../images/classes/policy.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `assignedBeneficiary` | Array von [[!UICONTROL Person]](../data-types/person.md) Datentypen | Erfasst den Begünstigten (bzw. die Begünstigten), der/die der Politik zugewiesen ist. |
| `benefitAmount` | [[!UICONTROL Währung]](../data-types/currency.md) | Der gemäß den Vertragsbedingungen zu zahlende Betrag. |
| `location` | [[!UICONTROL Postadresse]](../data-types/postal-address.md) | Der Ort, an dem die Versicherungspolice ausgestellt wird. |
| `owner` | [!UICONTROL Objekt] | Erfasst die Profilinformationen des Versicherungsnehmers. |
| `owner.faxPhone` | [[!UICONTROL Telefonnummer]](../data-types/phone-number.md) | Die Faxnummer des Eigentümers. |
| `owner.homeAddress` | [[!UICONTROL Postadresse]](../data-types/postal-address.md) | Die Wohnadresse des Eigentümers. |
| `owner.homePhone` | [[!UICONTROL Telefonnummer]](../data-types/phone-number.md) | Die Telefonnummer des Eigentümers. |
| `owner.mobilePhone` | [[!UICONTROL Telefonnummer]](../data-types/phone-number.md) | Die Mobiltelefonnummer des Eigentümers. |
| `owner.personalEmail` | [[!UICONTROL E-Mail-Adresse]](../data-types/email-address.md) | Die persönliche E-Mail-Adresse des Eigentümers. |
| `ID` | [!UICONTROL Zeichenfolge] | Eine Kennung für die Versicherungspolice. |
| `_id` | [!UICONTROL Zeichenfolge] | Eine eindeutige, systemgenerierte Zeichenfolgenkennung für den Datensatz. Dieses Feld wird verwendet, um die Eindeutigkeit eines einzelnen Datensatzes zu verfolgen, Datenduplizierung zu verhindern und diesen Datensatz in nachgelagerten Diensten nachzuschlagen.<br><br>Da dieses Feld systemgeneriert wird, wird bei der Datenerfassung kein expliziter Wert angegeben. Sie können jedoch weiterhin Ihre eigenen eindeutigen ID-Werte angeben, wenn Sie möchten. |
| `endDate` | [!UICONTROL DateTime] | Das Datum, an dem der Versicherungsschutz endet (oder endete). |
| `hasAssignedBeneficiary` | [!UICONTROL Boolesch] | Gibt an, ob der Richtlinie ein Empfänger zugewiesen ist. |
| `name` | [!UICONTROL Zeichenfolge] | Der Name der Versicherungspolice. |
| `startDate` | [!UICONTROL DateTime] | Das Datum, an dem der Versicherungsschutz beginnt (oder begonnen hat). |
| `type` | [!UICONTROL Zeichenfolge] | Die Art der Versicherungspolice, z. B. zu Hause, Auto, Mieter oder Boot. |

{style=&quot;table-layout:auto&quot;}
