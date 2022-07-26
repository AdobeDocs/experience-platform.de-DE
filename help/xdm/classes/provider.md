---
title: Anbieterklasse
description: Dieses Dokument bietet einen Überblick über die Provider-Klasse im Experience-Datenmodell (XDM).
source-git-commit: cf39f943e27cd11b0eabbc344774fa12482a8f92
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 7%

---

# [!UICONTROL Anbieter] class

Im Experience-Datenmodell (XDM) wird die [!UICONTROL Anbieter] -Klasse erfasst den Mindestsatz von Eigenschaften, die eine Anbietergeschäftseinheit definieren (z. B. einen Gesundheitsdienstleister oder einen Versicherer).

![Klassenstruktur](../images/classes/provider.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `providerName` | [[!UICONTROL Personenname]](../data-types/person-name.md) | Der Name des Anbieters. |
| `_id` | [!UICONTROL Zeichenfolge] | Eine eindeutige, systemgenerierte Zeichenfolgenkennung für den Datensatz. Dieses Feld wird verwendet, um die Eindeutigkeit eines einzelnen Datensatzes zu verfolgen, Datenduplizierung zu verhindern und diesen Datensatz in nachgelagerten Diensten nachzuschlagen.<br><br>Da dieses Feld systemgeneriert wird, wird bei der Datenerfassung kein expliziter Wert angegeben. Sie können jedoch weiterhin Ihre eigenen eindeutigen ID-Werte angeben, wenn Sie möchten. |
| `providerId` | [!UICONTROL Zeichenfolge] | Eine eindeutige Kennung für den Provider. |

{style=&quot;table-layout:auto&quot;}

Die Klasse kann mit der [[!UICONTROL Gesundheitsdienstleister] Feldergruppe](../field-groups/provider/healthcare-provider.md) weitere Informationen über einen Gesundheitsdienstleister.
