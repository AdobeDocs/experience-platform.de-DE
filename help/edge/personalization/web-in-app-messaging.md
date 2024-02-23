---
title: Konfigurieren der Web-In-App-Messaging-Unterstützung im Web SDK
description: Erfahren Sie, wie Sie die Web SDK-Tag-Erweiterung konfigurieren, um Web-In-App-Nachrichten zu unterstützen.
source-git-commit: a020f880be2606024c6a986dc468d70a2fbdc30f
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 0%

---


# Konfigurieren der Web-In-App-Messaging-Unterstützung im Web SDK


In-App-Nachrichten sind Benachrichtigungen, die Sie an Benutzer in Ihrer Webanwendung senden können, um sie an bestimmte Zielpunkte weiterzuleiten.

Sie können diese Benachrichtigungen für verschiedene Zwecke verwenden, z. B. zur Förderung neuer Funktionen, zur Präsentation von Sonderangeboten oder zur Erleichterung des Onboarding von Benutzern.

Mithilfe von In-App-Nachrichten können Sie effektiv mit Ihrer Zielgruppe interagieren und diese auf wichtige Aspekte Ihrer Anwendung lenken.

>[!IMPORTANT]
>
>Web In-App-Nachrichten sind [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=de) -Funktion, die das Web SDK verwendet, um die personalisierten Inhalte bereitzustellen.
>
>Detaillierte Anweisungen zum Konfigurieren Ihrer Web-In-App-Messaging-Kampagne finden Sie in der [Adobe Journey Optimizer-Dokumentation](https://experienceleague.adobe.com/docs/journey-optimizer/using/in-app/create-in-app-web.html).


## Voraussetzungen {#prerequisites}

### Version der Web SDK-Tag-Erweiterung {#extension-version}

Für die Web-In-App-Messaging-Funktion ist die neueste Version der Web SDK-Tag-Erweiterung erforderlich.

### CSP für Web-In-App-Nachrichten konfigurieren {#csp}

Bei der Konfiguration [Web-In-App-Nachrichten](../personalization/web-in-app-messaging.md)müssen Sie die folgende Anweisung in Ihre CSP aufnehmen:

```
default-src  blob:;
```

Weitere Informationen zum Konfigurieren einer CSP finden Sie unter [dedizierte Dokumentation](../fundamentals/configuring-a-csp.md).

## Web-In-App-Nachrichten mithilfe der Web SDK-Tag-Erweiterung konfigurieren {#tag-extension}

Siehe Abschnitt [Konfigurationsseite der Web SDK-Tag-Erweiterung](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) um zu verstehen, wo Sie die unten beschriebenen Einstellungen finden können.

Nachdem Sie [installiert](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#install-the-web-sdk-tag-extension) Gehen Sie zur Web SDK-Tag-Erweiterung wie folgt vor, um die Erweiterung für Web-In-App-Nachrichten zu konfigurieren.

Im **[!UICONTROL Personalisierung]** -Abschnitt, überprüfen Sie die **[!UICONTROL Personalisierungsspeicherung aktivieren]** -Option. Mit dieser Option kann das Web SDK verfolgen, welche Erlebnisse der Benutzer beim Laden der Seite gesehen hat.

![Bild, das die Speicheroption für die Personalisierung auf der Konfigurationsseite für die Tag-Erweiterung anzeigt.](assets/web-in-app-messaging/enable-personalization-storage.png)


Web In-App-Nachrichten unterstützen zwei Arten von Triggern:

* [Senden von Daten an Platform](#send-data-platform)
* [Nachrichten manuell auslösen](#manual-trigger)

In den folgenden Abschnitten erfahren Sie, wie Sie die Web SDK-Tag-Erweiterung entsprechend den gewünschten Triggern konfigurieren.

### Konfigurationsschritte für **[!UICONTROL Daten an Platform senden]** Trigger {#send-data-platform}

Wählen Sie die Tag-Eigenschaft aus, die Ihre Web SDK-Erweiterung enthält, und [eine neue Regel erstellen](../../tags/ui/managing-resources/rules.md##create-a-rule) mit den folgenden Einstellungen:

1. **[!UICONTROL Erweiterung]**: [!UICONTROL Core]
2. **[!UICONTROL Ereignistyp]**: [!UICONTROL Bibliothek geladen (Seitenanfang)]

   ![Bild, das den Bildschirm zur Ereigniskonfiguration anzeigt.](assets/web-in-app-messaging/rule-configuration.png)

3. Auswählen **[!UICONTROL Änderungen beibehalten]** , um die Ereigniskonfiguration zu speichern.

Als Nächstes müssen Sie der von Ihnen erstellten Regel eine Aktion hinzufügen.

1. Im [!DNL Actions] Bereich, wählen Sie **[!UICONTROL Hinzufügen]**.
   ![Bild, das den Bildschirm der Bearbeitungsregel anzeigt.](assets/web-in-app-messaging/add-action.png)

2. Verwenden Sie Folgendes **[!UICONTROL Aktion]** Einstellungen:
   * **[!UICONTROL Erweiterung]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Aktionstyp]**: [!UICONTROL Ereignis senden]

     ![Bild, das den Bildschirm für die Aktionskonfiguration anzeigt.](assets/web-in-app-messaging/action-configuration.png)

3. Auf der rechten Seite des Bildschirms im **[!UICONTROL Personalisierung]** aktivieren Sie die **[!UICONTROL visuelle Personalisierungsentscheidungen rendern]** -Option.
   ![Bild mit dem Konfigurationsbildschirm der Personalisierung.](assets/web-in-app-messaging/render-visual-personalization.png)

4. Auf der rechten Seite des Bildschirms im **[!UICONTROL Entscheidungskontext]** -Abschnitt, definieren Sie die **[!UICONTROL Schlüssel]**/**[!UICONTROL Wert]** Paare, die Sie in Ihrer Kampagnenkonfiguration verwendet haben, um sich für die In-App-Nachricht zu qualifizieren.
   ![Bild mit dem Konfigurationsbildschirm der Personalisierung.](assets/web-in-app-messaging/decision-context.png)

5. Auswählen **[!UICONTROL Änderungen beibehalten]** , um Ihre Konfiguration zu speichern.


Als Nächstes müssen Sie die neu erstellte Regel zur Tag-Property-Bibliothek hinzufügen. Gehen Sie dazu zu **[!UICONTROL Veröffentlichungsfluss]** und wählen Sie die zuvor erstellte Regel aus.

![Bild, das den Bibliotheksbildschirm anzeigt.](assets/web-in-app-messaging/add-rule-to-library.png)

Nachdem Sie die Regel zur Bibliothek hinzugefügt haben, wählen Sie **[!UICONTROL Speichern und in Entwicklung erstellen]**.

![Bild mit dem Konfigurationsbildschirm der Personalisierung.](assets/web-in-app-messaging/publish-flow.png)

Der Konfigurationsprozess ist jetzt abgeschlossen und Ihre Nachricht kann Ihren Benutzern angezeigt werden.

### Konfigurationsschritte für die Verwendung von manuellen Triggern {#manual-trigger}

Wählen Sie die Tag-Eigenschaft aus, die Ihre Web SDK-Erweiterung enthält, und [eine neue Regel erstellen](../../tags/ui/managing-resources/rules.md##create-a-rule) mit den folgenden Einstellungen:

1. **[!UICONTROL Erweiterung]**: [!UICONTROL Core]
2. **[!UICONTROL Ereignistyp]**: [!UICONTROL Klicks]
3. Legen Sie den Trigger für ein bestimmtes Element auf der Seite fest, den Sie durch einen CSS-Selektor Ihrer Wahl identifizieren.

   ![Bild, das den Bildschirm zur Ereigniskonfiguration anzeigt.](assets/web-in-app-messaging/event-configuration-manual.png)


Als Nächstes müssen Sie der von Ihnen erstellten Regel eine Aktion hinzufügen.

1. Im [!DNL Actions] Bereich, wählen Sie **[!UICONTROL Hinzufügen]**.
   ![Bild, das den Bildschirm der Bearbeitungsregel anzeigt.](assets/web-in-app-messaging/add-action.png)

2. Verwenden Sie Folgendes **[!UICONTROL Aktion]** Einstellungen:
   * **[!UICONTROL Erweiterung]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Aktionstyp]**: [!UICONTROL Bewerten von Regelsätzen]

     ![Bild, das den Bildschirm für die Aktionskonfiguration anzeigt.](assets/web-in-app-messaging/manual-trigger-action.png)

3. Aktivieren Sie rechts auf dem Bildschirm die **[!UICONTROL visuelle Personalisierungsentscheidungen rendern]** -Option.
   ![Bild mit dem Konfigurationsbildschirm der Personalisierung.](assets/web-in-app-messaging/manual-trigger-render.png)


4. Auf der rechten Seite des Bildschirms im **[!UICONTROL Entscheidungskontext]** -Abschnitt, definieren Sie die **[!UICONTROL Schlüssel]**/**[!UICONTROL Wert]** Paare, die Sie in Ihrer Kampagnenkonfiguration verwendet haben, um sich für die In-App-Nachricht zu qualifizieren.
   ![Bild mit dem Konfigurationsbildschirm der Personalisierung.](assets/web-in-app-messaging/manual-trigger-decision-context.png)

5. Auswählen **[!UICONTROL Änderungen beibehalten]** , um Ihre Konfiguration zu speichern.

Als Nächstes müssen Sie die neu erstellte Regel zur Tag-Property-Bibliothek hinzufügen. Gehen Sie dazu zu **[!UICONTROL Veröffentlichungsfluss]** und wählen Sie die zuvor erstellte Regel aus.

![Bild, das den Bibliotheksbildschirm anzeigt.](assets/web-in-app-messaging/add-rule-to-library.png)

Nachdem Sie die Regel zur Bibliothek hinzugefügt haben, wählen Sie **[!UICONTROL Speichern und in Entwicklung erstellen]**.

![Bild mit dem Konfigurationsbildschirm der Personalisierung.](assets/web-in-app-messaging/publish-flow.png)

Der Konfigurationsprozess ist jetzt abgeschlossen und Ihre Nachricht kann Ihren Benutzern angezeigt werden.

## Web-In-App-Nachrichten mithilfe der Web SDK-JavaScript-Bibliothek konfigurieren {#js-library}

Alternativ zur Verwendung der Web SDK-Tag-Erweiterung können Sie auch Web-In-App-Nachrichten direkt über die Web SDK-JavaScript-Bibliothek konfigurieren.



Sie können Web-In-App-Nachrichten aus Adobe Journey Optimizer auf zwei Arten anzeigen.

### Methode 1: Personalisierungsinhalt automatisch abrufen {#automatic}

Damit das Web SDK den Personalisierungsinhalt beim Laden der Seite automatisch abruft, verwenden Sie die `sendEvent` -Befehl, wie im folgenden Beispiel gezeigt.

```js
  alloy("sendEvent", {
      renderDecisions: true,
      personalization: {
          surfaces: ['#welcome']
      }
  });
```

### Methode 2: Personalisierungsinhalt basierend auf der Benutzeraktion manuell abrufen {#manual}

Verwenden Sie die `evaluateRulesets` -Befehl, wie im folgenden Beispiel gezeigt.

In diesem Beispiel wird der Personalisierungsinhalt angezeigt, wenn ein Benutzer auf die **[!UICONTROL Jetzt kaufen]** auf Ihrer Website.

```js
 alloy("evaluateRulesets", {
     renderDecisions: true,
     personalization: {
         decisionContext: {
             "userAction": "buy_now"
         }
     }
 });
```

### Konfigurieren des Personalisierungsspeichers {#personalization-storage}

Sie können festlegen, dass Benutzern In-App-Nachrichten für eine bestimmte Anzahl von Malen oder jedes Mal, wenn sie eine Seite besuchen, über die `personalizationStorageEnabled` Konfigurationsoption.

Im [Web SDK-Konfiguration](../fundamentals/configuring-the-sdk.md) legen Sie die `personalizationStorageEnabled` -Option entsprechend Ihren Anforderungen:

* `personalizationStorageEnabled: true` Die In-App-Nachricht wird mit der in der Variablen [Adobe Journey Optimizer-Kampagne](https://experienceleague.adobe.com/docs/journey-optimizer/using/in-app/create-in-app-web.html#configure-inapp).
* `personalizationStorageEnabled: false` Trigger der In-App-Nachricht bei jedem Seitenladevorgang.