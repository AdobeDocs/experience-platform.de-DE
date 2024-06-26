---
keywords: Experience Platform; home; beliebte Themen; Schema; XDM; individuelles Profil; Felder; Schemas; Schemas; Schemadesign; Feldergruppe; Feldergruppe; iab; tcf; Einverständnis
solution: Experience Platform
title: IAB TCF 2.0 Consent Field Group für Profilschemas
description: Erfahren Sie mehr über die IAB TCF 2.0-Feldergruppe für das Einwilligungsschema für die Klasse "XDM Individual Profile".
exl-id: 52a4fee8-d7f4-4f27-8e26-0c132985eb84
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 1%

---

# [!UICONTROL IAB TCF 2.0-Zustimmung] Feldergruppe für Profilschemata

>[!NOTE]
>
>Dieses Dokument behandelt die [!UICONTROL IAB TCF 2.0-Zustimmung] Schemafeldgruppe für die Klasse &quot;XDM Individual Profile&quot;. Die Feldergruppe, die für die XDM ExperienceEvent-Klasse vorgesehen ist, finden Sie im Folgenden. [Dokument](../event/iab.md) anstatt.

[!UICONTROL IAB TCF 2.0-Zustimmung] ist eine Standardschemafeldgruppe für die [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md) wird verwendet, um IAB-Zustimmungszeichenfolgen mit Zeitstempel zu erfassen, um Zustimmungsänderungen im Laufe der Zeit zu verfolgen.

![](../../images/field-groups/iab-profile.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `identityPrivacyInfo` | Zuordnung | Ein map -Objekt, das die individuellen Identitätswerte eines Kunden mit verschiedenen TCF-Zustimmungszeichenfolgen verknüpft. Nachfolgend finden Sie ein Beispiel für die Struktur dieses Objekts. |

{style="table-layout:auto"}

Die folgende JSON-Datei zeigt die Struktur der `identityPrivacyInfo` map.

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

Wie das Beispiel zeigt, ist jeder Schlüssel auf der Stammebene von `xdm:identityPrivacyInfo` entspricht einem vom Identity Service erkannten Identitäts-Namespace. Jede Namespace-Eigenschaft muss wiederum mindestens eine Untereigenschaft aufweisen, deren Schlüssel mit dem entsprechenden Identitätswert des Kunden für diesen Namespace übereinstimmt. In diesem Beispiel wird der Kunde mit einer Experience Cloud-ID (`ECID`) Wert `13782522493631189`.

>[!NOTE]
>
>Im obigen Beispiel wird zwar ein einzelnes Namespace-Wert-Paar verwendet, um die Identität des Kunden darzustellen, Sie können aber auch zusätzliche Schlüssel für andere Namespaces hinzufügen. Jeder Namespace kann mehrere Identitätswerte mit jeweils eigenen TCF-Zustimmungsvoreinstellungen aufweisen.

Für jeden Identitätswert wird ein `identityIABConsent` -Eigenschaft muss angegeben werden, die den TCF-Zustimmungswert für die Identität bereitstellt. Der Wert für diese Eigenschaft muss mit dem [[!UICONTROL Zustimmungszeichenfolge] Datentyp](../../data-types/consent-string.md).

Siehe Handbuch unter [IAB TCF 2.0-Unterstützung in Platform](../../../landing/governance-privacy-security/consent/iab/overview.md) für weitere Informationen zum Anwendungsfall dieser Feldergruppe. Weitere Informationen zur Feldergruppe selbst finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.schema.json)
