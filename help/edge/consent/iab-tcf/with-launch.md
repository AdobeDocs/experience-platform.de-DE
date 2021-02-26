---
title: Integrieren der IAB TCF 2.0-Unterstützung mithilfe von Platform launch und der Platform Web SDK Extension
description: Erfahren Sie, wie Sie die IAB TCF 2.0-Zustimmung mit Adobe Experience Platform Launch und der Adobe Experience Platform Web SDK-Erweiterung einrichten.
translation-type: tm+mt
source-git-commit: 1a51ce92eb5c41ff65ebcf4c652640dd0782487f
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 0%

---


# Integrieren der IAB TCF 2.0-Unterstützung mithilfe von Platform launch und der Platform Web SDK-Erweiterung

Adobe Experience Platform Web SDK unterstützt das Interactive Advertising Bureau Transparency &amp; Consent Framework, Version 2.0 (IAB TCF 2.0). Dieses Handbuch zeigt Ihnen, wie Sie eine Adobe Experience Platform Launch-Eigenschaft zum Senden von IAB TCF 2.0-Einwilligungsinformationen an die Adobe mithilfe der Adobe Experience Platform Web SDK Extension for Experience Platform Launch einrichten.

Wenn Sie Experience Platform Launch nicht verwenden möchten, lesen Sie bitte das Handbuch [IAB TCF 2.0 ohne Experience Platform Launch](./without-launch.md).

## Erste Schritte

Um IAB TCF 2.0 mit Experience Platform Launch und der Platform Web SDK Extension zu verwenden, benötigen Sie ein XDM-Schema und einen Dataset.

Darüber hinaus erfordert dieses Handbuch ein Verständnis des Adobe Experience Platform Web SDK. Eine kurze Auffrischung erhalten Sie in der Dokumentation [Adobe Experience Platform Web SDK overview](../../home.md) und [Häufig gestellte Fragen](../../web-sdk-faq.md).

## Standardgenehmigung festlegen

Innerhalb der Erweiterungskonfiguration gibt es eine Einstellung für die Standardgenehmigung. Dies steuert das Verhalten von Kunden, die kein Cookie für die Zustimmung haben. Wenn Sie Experience Ereignisses für Kunden in die Warteschlange stellen möchten, die kein Cookie für die Zustimmung haben, setzen Sie dies auf `pending`. Sie können auch ein Datenelement verwenden, um den Standardwert für die Zustimmung dynamisch festzulegen.

Weitere Informationen zum Konfigurieren der Standardgenehmigung finden Sie im Abschnitt [Standardgenehmigung](../../fundamentals/configuring-the-sdk.md#default-consent) im SDK-Konfigurationshandbuch.

## Profil mit Zustimmungsinformationen aktualisieren {#consent-code-1}

Um die Aktion `setConsent` aufzurufen, wenn sich die Voreinstellungen für die Zustimmung Ihrer Kunden geändert haben, müssen Sie eine neue Experience Platform Launch-Regel erstellen. Beginn durch Hinzufügen eines neuen Ereignisses und wählen Sie den Ereignistyp &quot;Benutzerdefinierter Code&quot;der Core-Erweiterung.

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

* Legt zwei Datenelemente fest, eines mit der Zustimmungszeichenfolge und eines mit dem `gdprApplies`-Flag. Dies ist später beim Ausfüllen der Aktion &quot;Zustimmung festlegen&quot;nützlich.

* Trigger der Regel, wenn sich die Voreinstellungen für die Zustimmung geändert haben. Die Aktion &quot;Zustimmung festlegen&quot;sollte immer dann verwendet werden, wenn sich die Voreinstellungen für die Zustimmung geändert haben. hinzufügen Sie eine Aktion &quot;Zustimmung festlegen&quot;in der Erweiterung und füllen Sie das Formular wie folgt aus:

* Standard: ‚IAB TCF‘
* Version: &quot;2.0&quot;
* Wert: &quot;%IAB TCF Consent String%&quot;
* GDPR gilt: &quot;%IAB TCF Zustimmung GDPR%&quot;

![IAB-Set-Aktion - Zustimmung](../../images/consent/iab-tcf/with-launch/iab-action.png)

>[!IMPORTANT]
>
>Sie können diese Datenelemente nicht mit der Datenelementauswahl auswählen, da sie mithilfe von benutzerdefiniertem Code erstellt wurden. Sie müssen den Namen des Datenelements mit den Prozentzeichen eingeben. Dieser Code aktualisiert das Profil Ihres Kunden mit den neuen Voreinstellungen für die Zustimmung, sobald sie sich ändern. Darüber hinaus gibt der Server einen Cookie-Wert zurück, der verhindern könnte, dass Adobe Experience Platform Web SDK Experience Ereignisses aufzeichnet.

## XDM-Datenelement für Experience Ereignisses erstellen

Die Zeichenfolge für die Zustimmung sollte im XDM Experience Ereignis enthalten sein. Verwenden Sie dazu das Datenelement &quot;XDM-Objekt&quot;. Beginn durch Erstellen eines neuen XDM-Objektdatenelements oder alternativ eines, das Sie bereits zum Senden von Ereignissen erstellt haben. Wenn Sie das Experience Ereignis Privacy-Mixin zu Ihrem Schema hinzugefügt haben, sollten Sie einen `consentStrings`-Schlüssel im XDM-Objekt haben.

1. Wählen Sie **[!UICONTROL approvalStrings]**.

1. Wählen Sie **[!UICONTROL Geben Sie einzelne Elemente]** ein und wählen Sie **[!UICONTROL Hinzufügen Element]**.

1. Erweitern Sie die Überschrift **[!UICONTROL approvalString]** und erweitern Sie das erste Element und geben Sie dann die folgenden Werte ein:

* `consentStandard`: IAB TCF
* `consentStandardVersion`: 2,0
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

Dieser Code ist mit dem vorherigen benutzerspezifischen Code identisch, außer dass sowohl `useractioncomplete`- als auch `tcloaded`-Ereignis verarbeitet werden. Der [vorherige benutzerspezifische Code](#consent-code-1) nur Trigger, wenn der Kunde seine Voreinstellungen zum ersten Mal auswählt. Dieser Code wird auch dann Trigger, wenn der Kunde seine Voreinstellungen bereits ausgewählt hat. Zum Beispiel beim Laden der zweiten Seite.

hinzufügen eine Aktion &quot;Ereignis senden&quot;aus der Platform Web SDK-Erweiterung. Wählen Sie im XDM-Feld das XDM-Datenelement aus, das Sie im vorherigen Abschnitt erstellt haben.

## Weiterleiten anderer Ereignisse mit Informationen zur Zustimmung der IAB TCF 2.0

Wenn Ereignis nach dem ersten Experience Ereignis ausgelöst werden, sind die beiden Datenelemente noch definiert und können zum Senden der IAB-Zustimmungsinformationen verwendet werden. Verwenden Sie dasselbe XDM-Datenelement, um zukünftige Ereignis zu senden. Die IAB-TCF-2.0-Informationen sind enthalten.

## Nächste Schritte

Nachdem Sie nun gelernt haben, wie Sie IAB TCF 2.0 mit der Platform Web SDK Extension einsetzen, können Sie sich auch für die Integration mit anderen Adoben wie Adobe Analytics oder Echtzeit-Kundendatenplattform entscheiden. Weitere Informationen finden Sie unter [Übersicht über IAB-Transparenz und -Zustimmung-Framework 2.0](./overview.md).
