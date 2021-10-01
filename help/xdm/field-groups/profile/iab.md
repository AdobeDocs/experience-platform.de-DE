---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; individuelles Profil; Felder; Schemas; Schemas; Schemadesign; Feldergruppe; Feldergruppe; iab; tcf; Einverständnis
solution: Experience Platform
title: IAB TCF 2.0-Gruppe für Einverständnisschema-Feld
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über die IAB TCF 2.0-Feldergruppe für das Einwilligungsschema für die Klasse "XDM Individual Profile".
exl-id: 52a4fee8-d7f4-4f27-8e26-0c132985eb84
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 2%

---

# [!UICONTROL IAB TCF 2.0-] Feldergruppe &quot;Einwilligungsschema&quot;

>[!NOTE]
>
>Dieses Dokument behandelt die Schemafeldgruppe [!UICONTROL IAB TCF 2.0 Consent] für die Klasse &quot;XDM Individual Profile&quot;. Die Feldergruppe, die für die XDM ExperienceEvent-Klasse bestimmt ist, finden Sie stattdessen im folgenden [Dokument](../event/iab.md) .

[!UICONTROL IAB TCF 2.0 ] Konfiguriert eine Schemafeldgruppe für die  [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) Klasse, die zum Erfassen einer IAB-Zustimmungszeichenfolge mit Zeitstempel verwendet wird, um Zustimmungsänderungen im Laufe der Zeit zu verfolgen.

![](../../images/field-groups/iab-profile.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `identityPrivacyInfo` | Zuordnung | Ein map -Objekt, das die individuellen Identitätswerte eines Kunden mit verschiedenen TCF-Zustimmungszeichenfolgen verknüpft. Nachfolgend finden Sie ein Beispiel für die Struktur dieses Objekts. |

{style=&quot;table-layout:auto&quot;}

Die folgende JSON-Datei zeigt die Struktur der `identityPrivacyInfo`-Karte.

```json
{
  "identityPrivacyInfo": {
    "ECID": {
      "13782522493631189": {
        "identityIABConsent": {
          "consentTimestamp": "2020-04-11T05:05:05Z",
          "consentString": {
            "consentStandard": "IAB TCF",
            "consentStandardVersion": "2.0",
            "consentStringValue": "BObdrPUOevsguAfDqFENCNAAAAAmeAAA.PVAfDObdrA.DqFENCAmeAENCDA",
            "gdprApplies": true,
            "containsPersonalData": false
          }
        }
      }
    }
  }
}
```

Wie das Beispiel zeigt, entspricht jeder Schlüssel der Stammebene von `xdm:identityPrivacyInfo` einem vom Identity Service erkannten Identitäts-Namespace. Jede Namespace-Eigenschaft muss wiederum mindestens eine Untereigenschaft aufweisen, deren Schlüssel mit dem entsprechenden Identitätswert des Kunden für diesen Namespace übereinstimmt. In diesem Beispiel wird der Kunde mit dem Experience Cloud-ID-Wert (`ECID`) von `13782522493631189` identifiziert.

>[!NOTE]
>
>Im obigen Beispiel wird zwar ein einzelnes Namespace-Wert-Paar verwendet, um die Identität des Kunden darzustellen, Sie können aber auch zusätzliche Schlüssel für andere Namespaces hinzufügen. Jeder Namespace kann mehrere Identitätswerte mit jeweils eigenen TCF-Zustimmungsvoreinstellungen aufweisen.

Für jeden Identitätswert muss eine `identityIABConsent` -Eigenschaft angegeben werden, die den TCF-Zustimmungswert für die Identität bereitstellt. Der Wert für diese Eigenschaft muss dem Datentyp [[!UICONTROL Consent String] ](../../data-types/consent-string.md) entsprechen.

Weitere Informationen zum Anwendungsfall dieser Feldergruppe finden Sie im Handbuch zur [IAB TCF 2.0-Unterstützung in Platform](../../../landing/governance-privacy-security/consent/iab/overview.md) . Weitere Informationen zur Feldergruppe selbst finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.schema.json)
