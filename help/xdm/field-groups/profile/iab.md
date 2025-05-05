---
keywords: Experience Platform;Startseite;beliebte Themen;schema;Schema;XDM;individuelles Profil;Felder;Schemata;Schemata;Schemadesign;Feldergruppe;Feldergruppe;iab;tcf;Einverständnis;
solution: Experience Platform
title: IAB TCF 2.0-Einverständnis-Feldergruppe für Profilschemata
description: Erfahren Sie mehr über die Feldergruppe des IAB TCF 2.0-Einverständnisschemas für die Klasse „XDM Individual Profile“.
exl-id: 52a4fee8-d7f4-4f27-8e26-0c132985eb84
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 1%

---

# [!UICONTROL IAB TCF 2.0 Consent]-Feldergruppe für Profilschemata

>[!NOTE]
>
>Dieses Dokument behandelt die Schemafeldgruppe [!UICONTROL IAB TCF 2.0 Consent] für die Klasse „XDM Individual Profile“. Die Feldergruppe für die XDM ExperienceEvent-Klasse finden Sie im folgenden [Dokument](../event/iab.md).

[!UICONTROL IAB TCF 2.0 Consent] ist eine Standardschemafeldgruppe für die [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md), mit der eine Zeitstempelserie von IAB-Einverständniszeichenfolgen erfasst wird, um Einverständnisänderungsmuster im Zeitverlauf zu verfolgen.

![](../../images/field-groups/iab-profile.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `identityPrivacyInfo` | Zuordnung | Ein Objekt vom Typ Zuordnung , das die individuellen Identitätswerte eines Kunden mit verschiedenen TCF-Einverständniszeichenfolgen verknüpft. Ein Beispiel für die Struktur dieses Objekts finden Sie unten. |

{style="table-layout:auto"}

Die folgende JSON-Datei veranschaulicht die Struktur der `identityPrivacyInfo`.

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

Wie das Beispiel zeigt, entspricht jeder Schlüssel auf Stammebene von `xdm:identityPrivacyInfo` einem Identity-Namespace, der von Identity Service erkannt wird. Jede Namespace-Eigenschaft muss wiederum über mindestens eine Untereigenschaft verfügen, deren Schlüssel mit dem entsprechenden Identitätswert des Kunden für diesen Namespace übereinstimmt. In diesem Beispiel wird der Kunde mit dem Wert für die Experience Cloud-ID (`ECID`) von `13782522493631189` identifiziert.

>[!NOTE]
>
>Während im obigen Beispiel ein einzelnes Namespace/Wert-Paar verwendet wird, um die Identität des Kunden darzustellen, können Sie zusätzliche Schlüssel für andere Namespaces hinzufügen, und jeder Namespace kann mehrere Identitätswerte mit jeweils einem eigenen Satz von TCF-Einverständnisvoreinstellungen aufweisen.

Für jeden Identitätswert muss eine `identityIABConsent`-Eigenschaft angegeben werden, die den TCF-Einverständniswert für die Identität bereitstellt. Der Wert für diese Eigenschaft muss mit dem [[!UICONTROL Einverständniszeichenfolge“ &#x200B;] Datentyp ](../../data-types/consent-string.md).

Weitere Informationen zum Anwendungsfall [ Feldergruppe finden Sie im Handbuch ](../../../landing/governance-privacy-security/consent/iab/overview.md) IAB TCF 2.0-Unterstützung in Experience Platform . Weitere Informationen zur Feldgruppe selbst finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.schema.json)
