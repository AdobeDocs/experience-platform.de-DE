---
title: Einverständnis festlegen
description: Legt das gewünschte Einverständnis für den Besucher fest.
source-git-commit: 8dd658c46fc92ae6d450213ab79f2766f4211c53
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# Einverständnis festlegen

Die **[!UICONTROL Set consent]** Aktion bestimmt, ob die Tag-Erweiterung Daten senden (Opt-in), Daten verwerfen (Opt-out) oder [ (Standardeinverständnis](../configure/consent.md) verwenden soll (Einverständnis unbekannt). Wenn ein Benutzer das Einverständnis für Ihre Site zulässt oder verweigert, können Sie diese Aktion verwenden, um seine Voreinstellungen mit der Tag-Erweiterung zu synchronisieren. Die JavaScript-Bibliotheksäquivalenz dieser Aktion ist der [`setConsent`](/help/collection/js/commands/setconsent.md).

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei ](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Rules]** und wählen Sie dann die gewünschte Regel aus.
1. Wählen Sie unter [!UICONTROL Actions] eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Legen Sie das Dropdown-Feld [!UICONTROL Extension] auf **[!UICONTROL Adobe Experience Platform Web SDK]** und dann den [!UICONTROL Action type] auf **[!UICONTROL Set consent]** fest.

Die Tag-Erweiterung unterstützt die folgenden Standards:

* **[Adobe Standard](/help/landing/governance-privacy-security/consent/adobe/overview.md)**: Es werden sowohl 1.0- als auch 2.0-Standards unterstützt.
* **[IAB Transparency &amp; Consent Framework](/help/landing/governance-privacy-security/consent/iab/overview.md)**: Wenn Sie diesen Standard verwenden, wird das Echtzeit-Kundenprofil des Besuchers mit den Einverständnisinformationen aktualisiert, sofern Ihre Implementierung korrekt konfiguriert ist:
   1. Das Schema Individuelles XDM-Profil enthält die Feldergruppe [IAB TCF 2.0-Einverständnis](/help/xdm/field-groups/profile/iab.md).
   1. Das Erlebnisereignis-Schema enthält die [IAB TCF 2.0-Einverständnis-Feldergruppe](/help/xdm/field-groups/event/iab.md).

Adobe empfiehlt, alle Voreinstellungen für das Einverständnisdialogfeld separat zu speichern, z. B. in einem Datenelement. Die Tag-Erweiterung bietet keine Möglichkeit, das Einverständnis abzurufen. Um sicherzustellen, dass die Benutzereinstellungen mit der Tag-Erweiterung synchron bleiben, können Sie diese Aktion bei jedem Laden der Seite ausführen.

## Verfügbare Felder

Dieser Aktionstyp unterstützt die folgenden Konfigurationsoptionen:

* **[!UICONTROL Instance]**: Die SDK-Instanz, für die die Aktion gilt. Dieses Dropdown-Menü ist deaktiviert, wenn Ihre Implementierung eine einzige SDK-Instanz verwendet.
* **[!UICONTROL Identity map]**: Ein Datenelement, das steuert, wie eine ECID generiert wird und mit welchen IDs Einverständnisinformationen verknüpft sind.
* **[!UICONTROL Consent information]**: Legt fest, ob ein Formular ausgefüllt oder ein Datenelement mit Einverständnisinformationen bereitgestellt werden soll.
* **[!UICONTROL Standard]**: Der Einverständnisstandard, den Sie verwenden möchten. Zu den verfügbaren Optionen gehören &quot;[!UICONTROL Adobe]&quot; und &quot;[!UICONTROL IAB TCF]&quot;.
* **[!UICONTROL Version]**: Die Version des Einverständnisstandards, den Sie verwenden möchten.
* **[!UICONTROL Datastream configuration overrides]**: Dieser Befehl unterstützt Überschreibungen der Datenstromkonfiguration, sodass Sie steuern können, welche Apps und Services diese Daten erhalten. Wenn Sie eine Überschreibung der Datenstromkonfiguration sowohl in einem einzelnen Befehl als auch in den Konfigurationseinstellungen der Tag-Erweiterung festlegen, hat der einzelne Befehl Vorrang. Weitere [ finden Sie unter ](../configure/configuration-overrides.md) der Datenstromkonfiguration .

## Erstellen einer Regel, die die Einverständnisinformationen aktualisiert

Ein idealer Zeitpunkt für die Verwendung dieser Aktion ist, wenn sich die Einverständnisvoreinstellungen eines Kunden geändert haben. Sie können eine Tag-Regel erstellen, die auf diese Änderung wartet.

1. Navigieren Sie in einer Tag-Eigenschaft zu **[!UICONTROL Rules]** und wählen Sie **[!UICONTROL Add rule]** aus.
1. Geben Sie der Regel einen gewünschten Namen und wählen Sie dann das Symbol &quot;`+`&quot; neben **[!UICONTROL Events]**.
1. Legen Sie die folgenden Eigenschaften auf der linken Seite fest:
   * **[!UICONTROL Extension]**: [!UICONTROL Core]
   * **[!UICONTROL EVent type]**: [!UICONTROL Custom code]
1. Öffnen Sie den Editor auf der rechten Seite und verwenden Sie den folgenden Code als Vorlage:

```javascript
// Wait for window.__tcfapi to be defined, then trigger when the customer has completed their consent and preferences.
function addEventListener() {
  if (window.__tcfapi) {
    window.__tcfapi("addEventListener", 2, function (tcData, success) {
      if (success && tcData.eventStatus === "useractioncomplete") {
        // save the tcData.tcString in a data element
        _satellite.setVar("IAB TCF Consent String", tcData.tcString);
        _satellite.setVar("IAB TCF Consent GDPR", tcData.gdprApplies);
        trigger();
      }
    });
  } else {
    // window.__tcfapi wasn't defined. Check again in 100 milliseconds
    setTimeout(addEventListener, 100);
  }
}
addEventListener();
```

1. Wählen Sie **[!UICONTROL Keep changes]** aus.

Der obige Block mit benutzerdefiniertem Code hat zwei Möglichkeiten:

* Trigger bei der Regel, wenn sich die Einverständnisvoreinstellungen geändert haben.
* Legt zwei Datenelemente fest: **IAB TCF Consent String** und **IAB TCF Consent DSGVO**.

Diese Datenelemente sind beim Festlegen der Aktion &quot;[!UICONTROL Set Consent]&quot; nützlich:

1. Klicken Sie auf das Symbol &quot;`+`&quot; neben **[!UICONTROL Actions]**.
1. Legen Sie die folgenden Eigenschaften auf der linken Seite fest:
   * **[!UICONTROL Extension]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Action type]**: [!UICONTROL Set consent]
1. Legen Sie die folgenden Eigenschaften auf der rechten Seite fest:
   * **[!UICONTROL Standard]**: [!UICONTROL IAB TCF]
   * **[!UICONTROL Version]**: [!UICONTROL 2.0]
   * **[!UICONTROL Value]**: `%IAB TCF Consent String%`
   * **[!UICONTROL Does GDPR apply to this consent value]**: [!UICONTROL Provide a data element], mit dem Wert `%IAB TCF Consent GDPR%`

![IAB-Einverständnisaktion festlegen](../assets/iab-action.png)

>[!NOTE]
>
>Sie können diese Datenelemente nicht mit der Datenelementauswahl auswählen, da sie mit benutzerdefiniertem Code erstellt wurden. Sie müssen den Datenelementnamen mit den Prozentzeichen eingeben.
