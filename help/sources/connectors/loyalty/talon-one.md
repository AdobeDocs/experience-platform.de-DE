---
title: Übersicht zu talon.one Source
description: Erfahren Sie mehr über die Quellen von Talon.One auf Adobe Experience Platform
badge: Beta
last-substantial-update: 2026-04-06T00:00:00Z
exl-id: 92ed180a-6175-45e2-a831-0f40fd8606b0
source-git-commit: f3026e0a717c07d95f12e3aeaf380ddc1b87c712
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 2%

---

# [!DNL Talon.One]

>[!AVAILABILITY]
>
>Die [!DNL Talon.One] befinden sich in der Betaphase. Weitere Informationen zur Verwendung von Beta[gekennzeichneten Quellen finden Sie &#x200B;](../../home.md#terms-and-conditions) den „Nutzungsbedingungen“ in der Quellenübersicht .

Mit [!DNL Talon.One] können Sie ganz einfach personalisierte Marketing-Kampagnen für Ihre Kunden erstellen, verwalten und optimieren. Nutzen Sie diese leistungsstarke Plattform, um Rabatte auszuführen, Coupons zu verteilen, Empfehlungsprogramme zu starten, Treueprogramme einzurichten und Gamified Incentives anzubieten - alles von einem skalierbaren System aus, das Ihnen hilft, Ihre Zielgruppe anzusprechen und zu belohnen.

Sie können die [!DNL Talon.One] im Adobe Experience Platform-Quellkatalog verwenden, um sowohl Batch- als auch Streaming-Treuedaten aus Ihrem [!DNL Talon.One] aufzunehmen.

* [Talon.one Streaming-Ereignisse](../../tutorials/ui/create/loyalty/talon-one-streaming.md)
* [Talon.One Batch Source Connector](../../tutorials/ui/create/loyalty/talon-one-batch.md)

>[!TIP]
>
>Treuedaten beziehen sich auf Informationen zum Treueprogramm Ihrer Endbenutzer wie Treuepunkte, ausgegebene Treuepunkte, aktuelle Stufe, gewährte Coupons, Empfehlungen und Leistungen.

## Voraussetzungen {#prerequisites}

Geben Sie Werte für die folgenden Anmeldeinformationen an, um sich zu authentifizieren und die [!DNL Talon.One Batch Source Connector] zu verbinden.

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| Domain | Die eindeutige URL, die mit Ihrer [!DNL Talon.One] Anwendungsumgebung verknüpft ist. Stellen Sie sicher, dass Sie bei der Eingabe Ihrer Domain weder das Protokoll noch den Pfad angeben. | `acmetalonone.us-east4` |
| API-Schlüssel für die [!DNL Talon.One] | Der Management-API-Schlüssel ist eine Berechtigung zur Authentifizierung und Autorisierung des Zugriffs auf die Management-API von [!DNL Talon.One]. Dies verarbeitet Vorgänge wie: <ul><li>Gutscheine importieren</li><li>Abrufen von Kampagnendaten</li><li>Verwalten von Anwendungen und Endpunkten</li></ul> | `ManagementKey-v1 {YOUR_MANAGEMENT_KEY}` |

## Zuordnung {#mapping}

Um Ihnen zu helfen, jedes Effektobjekt auf der Grundlage seines eindeutigen `effectType` zuzuordnen, können Sie die Datenvorbereitungs-`array_to_map` verwenden. Auf diese Weise können Sie einfach ein ungeordnetes Array von Effekten in Schlüssel-Wert-Paare konvertieren, die Ihren Anforderungen entsprechen. Eine Anleitung finden Sie im folgenden Beispiel .

Sie können auch die standardisierten Treuefeldergruppen verwenden, die Adobe bereitstellt, um Ihre Treueprogrammkonzepte konsistent zu modellieren.

>[!BEGINTABS]

>[!TAB Treuedetails]

Dies ist eine standardmäßige XDM-Feldergruppe für XDM Individual Profile, mit der der Treueprogramm-Mitgliedschaftsstatus einer Person beschrieben wird, indem deren Datensatzattribute und nicht Ereignisdaten erfasst werden. Verwenden Sie diese Feldergruppe in Ihren Profilschemata, um Folgendes zu erfassen:

* **Wer** der Teilnehmer ist im Programm (`loyaltyID`, `program`, `status`, `tier`)
* Ihre **aktuellen und Lebensdauersalden** (`points`, `lifetimePoints`, `expiredPoints` usw.)
* Wichtige **Mitgliedschaftsdaten** (`joinDate`, `upgradeDate`, `tierExpiryDate`)

>[!TAB Details zu Treueereignissen]

Die Feldergruppe Treueprogramm-Ereignisdetails wurde entwickelt, um Treueprogramm-Aktivitäten auf Ereignisebene zu erfassen, z. B. Punkte, die in einer bestimmten Transaktion verdient oder eingelöst wurden. Diese Feldergruppe enthält Felder wie `xdm:points`, `xdm:pointsRedeemed`, `xdm:pointsAsOfDate` und `xdm:program`. Verwenden Sie diese Feldergruppe auf Ereignisebene in Ihren Erlebnisereignis-Schemata, um Folgendes zu erfassen:

* **Pro-Ereignis-Bewegungen** in Punkten (gewonnen, eingelöst, abgelaufen)
* **Rabatte** die durch Treuescheine oder Empfehlungen gewährt wurden
* **Programm-IDs** und Transaktions-IDs zur Abstimmung mit dem Treueanbieter.

>[!ENDTABS]

| Quelle | Ziel |
| ---- | --- |
| `array_to_map(data.effects, "effectType").addLoyaltyPoints.campaignId` | `_{TENANT_ID}.loyalty.pointsGained[0].promotionId` |
| `array_to_map(data.effects, "effectType").addLoyaltyPoints.props.value` | `_{TENANT_ID}.loyalty.pointsGained[0].value` |
| `array_to_map(data.effects, "effectType").deductLoyaltyPoints.campaignId` | `_{TENANT_ID}.loyalty.pointsRedemption[0].promotionId` |
| `array_to_map(data.effects, "effectType").acceptCoupon.campaignId` | `_{TENANT_ID}.loyalty.couponRedemption[0].campaignId` |
| `array_to_map(data.effects, "effectType").deductLoyaltyPoints.props.value` | `_{TENANT_ID}.loyalty.pointsRedemption[0].value` |
| `array_to_map(data.effects, "effectType").acceptCoupon.props.value` | `_{TENANT_ID}.loyalty.couponRedemption[0].id` |
| `array_to_map(data.effects, "effectType").setDiscount.campaignId` | `_{TENANT_ID}.loyalty.discounts[0].promotionId` |
| `array_to_map(data.effects, "effectType").setDiscount.props.value` | `_{TENANT_ID}.loyalty.discounts[0].value` |
| `data.created` | `timestamp` |
| `data.attributes.params.profileId` | `personID` |
| `data.attributes.integrationId` | `_id` |
| `data.attributes.params.cartItems[*].name` | `productListItems[*].name` |
| `data.attributes.params.cartItems[*].category` | `productListItems[*].productCategories[0].categoryID` |
| `data.attributes.params.cartItems[*].sku` | `productListItems[*].SKU` |

{style="table-layout:auto"}

## Nächste Schritte

Lesen Sie die folgende Dokumentation, um zu erfahren, wie Sie Ihr [!DNL Talon.One]-Konto mit Experience Platform verbinden und sowohl Batch- als auch Streaming-Treuedaten aufnehmen können.

* [Talon.one Streaming-Ereignisse](../../tutorials/ui/create/loyalty/talon-one-streaming.md)
* [Talon.One Batch Source Connector](../../tutorials/ui/create/loyalty/talon-one-batch.md)
