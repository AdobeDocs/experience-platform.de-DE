---
title: Integrieren der IAB TCF 2.0-Unterstützung mithilfe von Tags und der Platform Web SDK-Erweiterung
description: Erfahren Sie, wie Sie die IAB TCF 2.0-Zustimmung mit Tags und der Adobe Experience Platform Web SDK-Erweiterung einrichten.
exl-id: dc0e6b68-8257-4862-9fc4-50b370ef204f
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 0%

---

# Integrieren der IAB TCF 2.0-Unterstützung mithilfe von Tags und der Platform Web SDK-Erweiterung

Adobe Experience Platform Web SDK unterstützt das Interactive Advertising Bureau Transparency &amp; Consent Framework, Version 2.0 (IAB TCF 2.0). In diesem Handbuch erfahren Sie, wie Sie eine Tag-Eigenschaft zum Senden von IAB TCF 2.0-Zustimmungsinformationen an Adobe mithilfe der Adobe Experience Platform Web SDK-Tag-Erweiterung einrichten.

Wenn Sie keine Tags verwenden möchten, lesen Sie bitte das Handbuch unter [Verwendung von IAB TCF 2.0 ohne Tags](./without-launch.md).

## Erste Schritte

Um das IAB TCF 2.0 mit Tags und der Platform Web SDK-Erweiterung verwenden zu können, müssen Sie über ein XDM-Schema und einen Datensatz verfügen.

Darüber hinaus setzt dieses Handbuch ein Verständnis des Adobe Experience Platform Web SDK voraus. Für einen schnellen Auffrischungskurs lesen Sie bitte die [Übersicht über das Adobe Experience Platform Web SDK](../../home.md) und [Häufig gestellte Fragen](../../web-sdk-faq.md) Dokumentation.

## Festlegen der Standardzustimmung

In der Erweiterungskonfiguration gibt es eine Einstellung für die Standardzustimmung. Dadurch wird das Verhalten von Kunden gesteuert, die kein Zustimmungs-Cookie haben. Wenn Sie Erlebnisereignisse für Kunden in die Warteschlange stellen möchten, die kein Zustimmungscookie haben, setzen Sie dies auf `pending`. Wenn Sie Erlebnisereignisse für Kunden verwerfen möchten, die kein Zustimmungs-Cookie haben, setzen Sie dies auf `out`. Sie können auch ein Datenelement verwenden, um den standardmäßigen Zustimmungswert dynamisch festzulegen.

Weitere Informationen zum Konfigurieren der Standardzustimmung finden Sie im Abschnitt [Standardzustimmungsabschnitt](../../fundamentals/configuring-the-sdk.md#default-consent) im SDK-Konfigurationshandbuch.

## Profil mit Zustimmungsinformationen aktualisieren {#consent-code-1}

So rufen Sie die `setConsent` Wenn sich die Zustimmungsvoreinstellungen Ihrer Kunden geändert haben, müssen Sie eine neue Tag-Regel erstellen. Fügen Sie zunächst ein neues Ereignis hinzu und wählen Sie den Ereignistyp &quot;Benutzerspezifischer Code&quot;der Haupterweiterung aus.

Verwenden Sie das folgende Code-Beispiel für Ihr neues Ereignis:

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

Dieser benutzerspezifische Code umfasst zwei Dinge:

* Legt zwei Datenelemente fest, eines mit der Zustimmungszeichenfolge und eines mit der `gdprApplies` Markierung. Dies ist später beim Ausfüllen der Aktion &quot;Einverständnis festlegen&quot;nützlich.

* Trigger der Regel, wenn sich die Zustimmungseinstellungen geändert haben. Die Aktion &quot;Einverständnis festlegen&quot;sollte immer verwendet werden, wenn sich die Zustimmungseinstellungen geändert haben. Fügen Sie die Aktion &quot;Einverständnis festlegen&quot;in die Erweiterung ein und füllen Sie das Formular wie folgt aus:

* Standard: &quot;IAB TCF&quot;
* Version: &quot;2.0&quot;
* Wert: &quot;%IAB TCF Consent String%&quot;
* Die DSGVO gilt: &quot;%IAB TCF Einverständniserklärung DSGVO%&quot;

![IAB-Einverständnisaktion festlegen](../../images/consent/iab-tcf/with-launch/iab-action.png)

>[!IMPORTANT]
>
>Sie können diese Datenelemente nicht mit der Datenelementauswahl auswählen, da sie über benutzerdefinierten Code erstellt wurden. Sie müssen den Datenelementnamen mit Prozentzeichen eingeben. Dieser Code aktualisiert das Profil Ihres Kunden mit seinen neuen Zustimmungsvoreinstellungen, sobald diese sich ändern. Darüber hinaus gibt der Server einen Cookie-Wert zurück, der verhindern könnte, dass das Adobe Experience Platform Web SDK Erlebnisereignisse aufzeichnet.

## Erstellen eines XDM-Datenelements für Erlebnisereignisse

Die Zustimmungszeichenfolge sollte im XDM-Erlebnisereignis enthalten sein. Verwenden Sie dazu das Datenelement &quot;XDM-Objekt&quot;. Erstellen Sie zunächst ein neues XDM-Objekt-Datenelement oder verwenden Sie alternativ eines, das Sie bereits zum Senden von Ereignissen erstellt haben. Wenn Sie Ihrem Schema die Feldergruppe &quot;Erlebnisereignis-Datenschutz&quot;hinzugefügt haben, sollte Ihnen eine `consentStrings` -Schlüssel im XDM-Objekt.

1. Auswählen **[!UICONTROL consentStrings]**.

1. Auswählen **[!UICONTROL Bereitstellen einzelner Elemente]** und wählen Sie **[!UICONTROL Element hinzufügen]**.

1. Erweitern Sie die **[!UICONTROL consentString]** -Überschrift, erweitern Sie das erste Element und geben Sie dann die folgenden Werte ein:

* `consentStandard`: IAB TCF
* `consentStandardVersion`: 2,0
* `consentStringValue`: %IAB TCF-Zustimmungszeichenfolge%
* `gdprApplies`: %IAB TCF Einverständniserklärung DSGVO%

>[!IMPORTANT]
>
>Sie können diese Datenelemente nicht mit der Datenelementauswahl auswählen, da sie über benutzerdefinierten Code erstellt wurden. Sie müssen den Datenelementnamen mit Prozentzeichen eingeben.

## Senden eines ersten Erlebnisereignisses mit IAB TCF 2.0-Einverständnisinformationen

Wenn das anfängliche Erlebnisereignis auf der Seite mit einem Seitenladeereignis ausgelöst wird, wurde die Zustimmungszeichenfolge möglicherweise noch nicht geladen. Diese Regel soll das aktuelle Seitenladeereignis ersetzen. Um sicherzustellen, dass die Zustimmungsinformationen zuerst geladen werden, erstellen Sie eine neue Regel und fügen Sie den folgenden Code als benutzerspezifisches Code-Ereignis hinzu:

```javascript
// Wait for window.__tcfapi to be defined, then trigger when there is a consent string
function addEventListener() {
  if (window.__tcfapi) {
    window.__tcfapi("addEventListener", 2, function (tcData, success) {
      if (success && (tcData.eventStatus === "useractioncomplete" || tcData.eventStatus === "tcloaded")) {
        // save the tcData.tcString in a data element
        _satellite.setVar("IAB TCF Consent String", tcData.tcString);
        _satellite.setVar("IAB TCF GDPR Applies", tcData.gdprApplies);
        trigger();
      }
    });
  } else {
    // window.__tcfapi wasn"t defined. Check again in 100 milliseconds
    setTimeout(addEventListener, 100);
  }
}
addEventListener();
```

Dieser Code ist mit dem vorherigen benutzerspezifischen Code identisch, mit dem Unterschied, dass beide `useractioncomplete` und `tcloaded` -Ereignisse verarbeitet werden. Die [vorheriger benutzerspezifischer Code](#consent-code-1) nur Trigger, in denen der Kunde seine Voreinstellungen zum ersten Mal auswählt. Dieser Code Trigger auch dann, wenn der Kunde seine Voreinstellungen bereits ausgewählt hat. Beispielsweise beim zweiten Laden der Seite.

Fügen Sie die Aktion &quot;Ereignis senden&quot;aus der Platform Web SDK-Erweiterung hinzu. Wählen Sie im XDM-Feld das XDM-Datenelement aus, das Sie im vorherigen Abschnitt erstellt haben.

## Senden anderer Ereignisse mit IAB TCF 2.0-Zustimmungsinformationen

Wenn Ereignisse nach dem ersten Erlebnisereignis ausgelöst werden, sind die beiden Datenelemente weiterhin definiert und können zum Senden der IAB-Zustimmungsinformationen verwendet werden. Verwenden Sie dasselbe XDM-Datenelement, um zukünftige Ereignisse zu senden. IAB TCF 2.0-Informationen sind enthalten.

## Nächste Schritte

Nachdem Sie nun gelernt haben, wie Sie IAB TCF 2.0 mit der Platform Web SDK-Erweiterung verwenden, können Sie auch mit anderen Adobe-Lösungen wie Adobe Analytics oder Echtzeit-Kundendatenplattform integrieren. Siehe [Übersicht über das IAB Transparency &amp; Consent Framework 2.0](./overview.md) für weitere Informationen.
