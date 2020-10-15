---
title: Verwenden von IAB TCF 2.0 mit Experience Platform Launch
seo-title: Einrichten der IAB TCF 2.0-Zustimmung mit Adobe Experience Platform Launch und dem Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie die IAB TCF 2.0-Zustimmung mit Adobe Experience Platform Launch und Adobe Experience Platform Web SDK einrichten.
seo-description: Erfahren Sie, wie Sie die IAB TCF 2.0-Zustimmung mit Adobe Experience Platform Launch und Adobe Experience Platform Web SDK einrichten.
translation-type: tm+mt
source-git-commit: db742119d8f169817080f1fd4e0dc08a0f0faa47
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 0%

---


# Verwenden von IAB TCF 2.0 mit Experience Platform Launch und der AEP Web SDK-Erweiterung

Das Adobe Experience Platform Web Software Development Kit (Adobe Experience Platform Web SDK) unterstützt das Interactive Advertising Bureau Transparency &amp; Consent Framework, Version 2.0 (IAB TCF 2.0). Dieses Handbuch zeigt Ihnen, wie Sie eine Adobe Experience Platform Launch-Eigenschaft zum Senden von IAB TCF 2.0-Einwilligungsinformationen an die Adobe mithilfe der AEP Web SDK Extension for Experience Platform Launch einrichten.

Wenn Sie Experience Platform Launch nicht verwenden möchten, lesen Sie bitte das Handbuch zur [Verwendung von IAB TCF 2.0 ohne Experience Platform Launch](./without-launch.md).

## Erste Schritte

Um IAB TCF 2.0 mit Experience Platform Launch und der AEP Web SDK Extension zu verwenden, benötigen Sie ein XDM-Schema und einen Dataset. Wenn Sie keines dieser beiden Optionen eingerichtet haben, lesen Sie den Beginn in dieser Anleitung zum Adobe Experience Platform Web SDK Launch Quick Beginn, bevor Sie fortfahren.

Darüber hinaus erfordert dieses Handbuch ein Verständnis des Adobe Experience Platform Web SDK. Für einen schnellen Auffrischungskommentar lesen Sie bitte die [Adobe Experience Platform Web SDK-Übersicht](../../home.md) und die Dokumentation [Häufig gestellte Fragen](../../web-sdk-faq.md) .

## Standardgenehmigung festlegen

Innerhalb der Erweiterungskonfiguration gibt es eine Einstellung für die Standardgenehmigung. Dies steuert das Verhalten von Kunden, die kein Cookie für die Zustimmung haben. Wenn Sie Experience Ereignisses für Kunden in die Warteschlange stellen möchten, die kein Cookie für die Zustimmung haben, setzen Sie diesen auf `pending`.

>[!NOTE]
>
>Derzeit gibt es keine Möglichkeit, dies dynamisch über die Experience Platform Launch-Erweiterung festzulegen.

Weitere Informationen zur Standardgenehmigung finden Sie im Abschnitt zur [Standardgenehmigung](../../fundamentals/configuring-the-sdk.md#default-consent) in der SDK-Konfigurationsdokumentation.

## Aktualisieren von Profilen mit Einwilligungsinformationen {#consent-code-1}

Um die `setConsent` Aktion aufzurufen, wenn sich die Voreinstellungen für die Zustimmung Ihrer Kunden geändert haben, müssen Sie eine neue Experience Platform Launch-Regel erstellen. Beginn durch Hinzufügen eines neuen Ereignisses und wählen Sie den Ereignistyp &quot;Benutzerdefinierter Code&quot;der Core-Erweiterung.

Verwenden Sie das folgende Codebeispiel für Ihr neues Ereignis:

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

Dieser benutzerspezifische Code umfasst zwei Aufgaben:

* Legt zwei Datenelemente fest, eines mit der Zustimmungszeichenfolge und eines mit der `gdprApplies` Kennzeichnung. Dies ist später beim Ausfüllen der Aktion &quot;Zustimmung festlegen&quot;nützlich.

* Löst die Regel aus, wenn sich die Voreinstellungen für die Zustimmung geändert haben. Die Aktion &quot;Zustimmung festlegen&quot;sollte immer dann verwendet werden, wenn sich die Voreinstellungen für die Zustimmung geändert haben. hinzufügen Sie eine Aktion &quot;Zustimmung festlegen&quot;in der Erweiterung und füllen Sie das Formular wie folgt aus:

* Standard: ‚IAB TCF‘
* Version: &quot;2.0&quot;
* Wert: &quot;%IAB TCF Consent String%&quot;
* GDPR gilt: &quot;%IAB TCF Zustimmung GDPR%&quot;

![IAB-Set-Aktion - Zustimmung](../../../assets/iab_set_consent_action.png)

>[!IMPORTANT]
>
>Sie können diese Datenelemente nicht mit der Datenelementauswahl auswählen, da sie mithilfe von benutzerdefiniertem Code erstellt wurden. Sie müssen den Namen des Datenelements mit den Prozentzeichen eingeben. Dieser Code aktualisiert das Profil Ihres Kunden mit den neuen Voreinstellungen für die Zustimmung, sobald sie sich ändern. Darüber hinaus gibt der Server einen Cookie-Wert zurück, der verhindern könnte, dass das Adobe Experience Platform Web SDK Experience Ereignisses aufzeichnet.

## XDM-Datenelement für Experience Ereignisses erstellen

Die Zeichenfolge für die Zustimmung sollte im XDM Experience Ereignis enthalten sein. Verwenden Sie dazu das Datenelement &quot;XDM-Objekt&quot;. Beginn durch Erstellen eines neuen XDM-Objektdatenelements oder alternativ eines, das Sie bereits zum Senden von Ereignissen erstellt haben. Wenn Sie das Experience Ereignis Privacy-Mixin zu Ihrem Schema hinzugefügt haben, sollten Sie einen `consentStrings` Schlüssel im XDM-Objekt haben.

1. Wählen Sie **[!UICONTROL die Option acceptStrings]**.

1. Wählen Sie **[!UICONTROL Einzelne Elemente]** bereitstellen und dann **[!UICONTROL Hinzufügen Element]**.

1. Erweitern Sie die Überschrift **[!UICONTROL approvalString]** , erweitern Sie das erste Element und geben Sie dann die folgenden Werte ein:

* `consentStandard`: IAB TCF
* `consentStandardVersion`: 2.0
* `consentStringValue`: %IAB TCF-Genehmigungszeichenfolge%
* `gdprApplies`: %IAB TCF Zustimmung GDPR%

>[!IMPORTANT]
>
>Sie können diese Datenelemente nicht mit der Datenelementauswahl auswählen, da sie mithilfe von benutzerdefiniertem Code erstellt wurden. Sie müssen den Namen des Datenelements mit den Prozentzeichen eingeben.

## Senden eines ersten Experience Ereignisses mit Informationen zur Zustimmung des IAB TCF 2.0

Wenn das anfängliche Experience Ereignis auf der Seite mit einem Seitenlade-Ereignis ausgelöst wird, wurde die Zustimmungszeichenfolge möglicherweise noch nicht geladen. Diese Regel soll das aktuelle Ereignis zum Laden der Seite ersetzen. Um sicherzustellen, dass die Einwilligungsinformationen zuerst geladen werden, erstellen Sie eine neue Regel und fügen Sie den folgenden Code als benutzerspezifisches Ereignis hinzu:

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

Dieser Code ist identisch mit dem vorherigen benutzerspezifischen Code, außer dass sowohl `useractioncomplete` als auch `tcloaded` Ereignisse verarbeitet werden. Der [vorherige benutzerdefinierte Code](#consent-code-1) wird nur dann ausgelöst, wenn der Kunde seine Voreinstellungen zum ersten Mal auswählt. Dieser Code wird auch dann ausgelöst, wenn der Kunde seine Voreinstellungen bereits ausgewählt hat. Zum Beispiel beim Laden der zweiten Seite.

hinzufügen einer Aktion &quot;Ereignis senden&quot;aus der Adobe Experience Platform Web SDK-Erweiterung. Wählen Sie im XDM-Feld das XDM-Datenelement aus, das Sie im vorherigen Abschnitt erstellt haben.

## Weiterleiten anderer Ereignisse mit Informationen zur Zustimmung der IAB TCF 2.0

Wenn Ereignis nach dem ersten Experience Ereignis ausgelöst werden, sind die beiden Datenelemente noch definiert und können zum Senden der IAB-Zustimmungsinformationen verwendet werden. Verwenden Sie dasselbe XDM-Datenelement, um zukünftige Ereignis zu senden. Die IAB-TCF-2.0-Informationen sind enthalten.

## Nächste Schritte

Nachdem Sie nun gelernt haben, wie Sie IAB TCF 2.0 mit der Adobe Experience Platform Web SDK-Erweiterung verwenden können, können Sie sich auch für die Integration mit anderen Adoben wie Adobe Analytics oder Echtzeit-Kundendatenplattform entscheiden. Weitere Informationen finden Sie in der Übersicht [zum](./overview.md) IAB-Transparenz- und Bestätigungsrahmen 2.0.
