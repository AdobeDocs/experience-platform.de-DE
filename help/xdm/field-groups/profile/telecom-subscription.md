---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;Schema;XDM;individuelles Profil;Felder;Schemata;Schemata;Schemata;Telekommunikation;Telekommunikation;Schema-Design;Feldergruppe;Feldergruppe;
solution: Experience Platform
title: Feldgruppe des Telekom-Abonnementschemas
description: Erfahren Sie mehr über die Feldgruppe „Telekom-Abonnement-Schema“.
exl-id: 00c20081-09d0-425c-9894-0f957558bd43
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 8%

---

# Schemafeldgruppe [!UICONTROL Telekom]Abonnement

>[!NOTE]
>
>Die Namen mehrerer Schemafeldgruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu den [Namensaktualisierungen für Feldgruppen](../name-updates.md).

[!UICONTROL Telekom-Abonnement] ist eine Standardschemafeldgruppe für die [[!DNL XDM Individual Profile] Klasse](../../classes/individual-profile.md) die den Telekom-Abonnementplan eines Kunden beschreibt, einschließlich Preise, Pakete und individueller Produktabonnements.

Die Feldergruppe bietet ein einzelnes Feld vom Typ „Objekt“, `telecomSubscription`, dessen Eigenschaften unten beschrieben werden.

![Telekom-Abonnementstruktur](../../images/field-groups/telecom-subscription/structure.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `internetSubscription` | Array von Objekten | Beschreibt Details zum Internet-Abonnementplan wie Datenobergrenze, Verbindungstyp und Geschwindigkeitsdetails. Weitere Informationen finden [&#x200B; im &#x200B;](#internetSubscription) Abschnitt unten. |
| `landlineSubscription` | Array von Objekten | Beschreibt Details zum Festnetzabonnementplan, einschließlich ausgewählter Funktionen, Minuten und Wählpläne. Weitere Informationen finden [&#x200B; im &#x200B;](#landlineSubscription) Abschnitt unten. |
| `mediaSubscription` | Array von Objekten | Beschreibt Details zum Medienabonnementplan, einschließlich der Anzahl der Kanäle und der enthaltenen Streaming-Services. Weitere Informationen finden [&#x200B; im &#x200B;](#mediaSubscription) Abschnitt unten. |
| `mobileSubscription` | Array von Objekten | Beschreibt Details zum Mobile-Abonnementplan, einschließlich der Anzahl der Zeilen, Datenraten, Kosten und mehr. Weitere Informationen finden [&#x200B; im &#x200B;](#mobileSubscription) Abschnitt unten. |
| `primarySubscriber` | [[!UICONTROL Person]](../../data-types/person.md) | Beschreibt den Inhaber des Abonnements. |
| `bundleName` | String | Erfasst den Namen eines beliebigen Abonnementpakets, für das der Kunde angemeldet ist, z. B. `Internet + Media`. |
| `primaryPartyID` | String | Eine Kennung für die primäre Person, die für das Abonnement verantwortlich ist, wobei es sich normalerweise um die Telefonnummer des Geräts handelt. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)

## `internetSubscription` {#internetSubscription}

`internetSubscription` wird als Array von -Objekten bereitgestellt. Im Folgenden wird die Struktur der einzelnen Objekte beschrieben.

![internetSubscription](../../images/field-groups/telecom-subscription/internetSubscription.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `subscriptionDetails` | [[!UICONTROL Telekom-Abonnement]](../../data-types/telecom-subscription.md) | Beschreibt allgemeine Details zum Abonnement, einschließlich Abonnementdauer, Gebühren, Status und mehr. Beschreibt allgemeine Details zum Abonnement, einschließlich Abonnementdauer, Gebühren, Status und mehr. |
| `connectionType` | String | Der Verbindungstyp für das Abonnement. |
| `dataCap` | Ganzzahl | Die Datenobergrenze für das Konto in Megabyte (MB). |
| `downloadSpeed` | Ganzzahl | Die maximale Download-Geschwindigkeit, die für das Abonnement verfügbar ist, in Megabyte (MB). |
| `selfSetup` | Boolesch | Gibt an, ob eine Kundin oder ein Kunde für die Internet-Einrichtung ohne Besuch eines Technikers infrage kommt. |
| `uploadSpeed` | Ganzzahl | Die maximale Upload-Geschwindigkeit, die für das Abonnement verfügbar ist, in Megabyte (MB). |

{style="table-layout:auto"}

## `landlineSubscription` {#landlineSubscription}

`landlineSubscription` wird als Array von -Objekten bereitgestellt. Im Folgenden wird die Struktur der einzelnen Objekte beschrieben.

![landlineSubscription](../../images/field-groups/telecom-subscription/landlineSubscription.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `phoneNumber` | [[!UICONTROL Telefonnummer]](../../data-types/telecom-subscription.md) | Die diesem Abonnement zugewiesene Telefonnummer. |
| `subscriptionDetails` | [[!UICONTROL Telekom-Abonnement]](../../data-types/telecom-subscription.md) | Beschreibt allgemeine Details zum Abonnement, einschließlich Abonnementdauer, Gebühren, Status und mehr. |
| `callBlocking` | Boolesch | Gibt an, ob die Funktionen des Festnetzabonnements die Anrufsperre enthalten. |
| `callForwarding` | Boolesch | Gibt an, ob die Funktionen des Festnetzabonnements die Anrufweiterleitung enthalten. |
| `callWaiting` | Boolesch | Gibt an, ob die Funktionen des Festnetzabonnements die Anklopffunktion enthalten. |
| `callerID` | Boolesch | Gibt an, ob die Funktionen des Festnetzabonnements Anrufer-ID enthalten. |
| `internationalCalling` | Boolesch | Gibt an, ob die Funktionen des Festnetzabonnements internationale Anrufe enthalten. |
| `minutes` | Ganzzahl | Die Anzahl der monatlich verfügbaren Minuten im Rahmen des Abonnements. |
| `threeWayCalling` | Boolesch | Gibt an, ob die Funktionen des Festnetzabonnements Drei-Wege-Anrufe enthalten. |
| `unlimitedDomesticLongDistance` | Boolesch | Gibt an, ob die Funktionen des Festnetzabonnements unbegrenzte Inlandsferngespräche beinhalten. |
| `unlimitedLocalCalling` | Boolesch | Gibt an, ob die Funktionen des Festnetzabonnements unbegrenzte Ortsgespräche beinhalten. |
| `voicemail` | Boolesch | Gibt an, ob die Funktionen des Festnetzabonnements Voicemail enthalten. |

{style="table-layout:auto"}

## `mediaSubscription` {#mediaSubscription}

`mediaSubscription` wird als Array von -Objekten bereitgestellt. Im Folgenden wird die Struktur der einzelnen Objekte beschrieben.

![mediaSubscription](../../images/field-groups/telecom-subscription/mediaSubscription.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `streamingServices` | Array von Objekten | Eine Liste aller im Abonnement enthaltenen Streaming-Services. Jedes Array-Element enthält die folgenden Eigenschaften: <ul><li>`promotionLength`: Die Länge der Promotion in Monaten, wenn der Streaming-Service als Teil einer Promotion hinzugefügt wurde.</li><li>`promotionalAddition`: Gibt an, ob der Streaming-Service im Rahmen einer Promotion hinzugefügt wurde.</li><li>`serviceName`: Der Name des Streaming-Services.</li></ul> |
| `subscriptionDetails` | [[!UICONTROL Telekom-Abonnement]](../../data-types/telecom-subscription.md) | Beschreibt allgemeine Details zum Abonnement, einschließlich Abonnementdauer, Gebühren, Status und mehr. |
| `channels` | Ganzzahl | Die Anzahl der mit dem Medienabonnement enthaltenen Kanäle. |

{style="table-layout:auto"}

## `mobileSubscription` {#mobileSubscription}

`mobileSubscription` wird als Array von -Objekten bereitgestellt. Im Folgenden wird die Struktur der einzelnen Objekte beschrieben.

![mobileSubscription](../../images/field-groups/telecom-subscription/mobileSubscription.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `phoneNumber` | [[!UICONTROL Telefonnummer]](../../data-types/telecom-subscription.md) | Die diesem Abonnement zugewiesene Telefonnummer. |
| `subscriptionDetails` | [[!UICONTROL Telekom-Abonnement]](../../data-types/telecom-subscription.md) | Beschreibt allgemeine Details zum Abonnement, einschließlich Abonnementdauer, Gebühren, Status und mehr. |
| `earlyUpgradeEnrollment` | Boolesch | Gibt an, ob sich der Kunde für frühzeitige Upgrades entscheidet. |
| `planLevel` | String | Der Name des diesem Abonnement zugewiesenen Mobilfunkplans. |
| `portedNumber` | Boolesch | Gibt an, ob der Kunde seine Nummer von einem anderen Anbieter portiert. |

{style="table-layout:auto"}
