---
title: Verwenden von Adobe Experience Platform Assurance
description: In diesem Handbuch wird erläutert, wie Sie Adobe Experience Platform Assurance nach der Installation und Implementierung verwenden.
exl-id: 872c83d1-82e8-40d8-9b66-3e51a91a955f
source-git-commit: f8576e7f7e1da7351f7860cba27d5d09d0161132
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 3%

---

# Verwenden von Adobe Experience Platform Assurance

In diesem Tutorial wird erläutert, wie Sie Adobe Experience Platform Assurance verwenden. Anweisungen zur Installation und Implementierung der Adobe Experience Platform Assurance-Erweiterung finden Sie im Tutorial [Implementieren der Assurance-Erweiterung](./implement-assurance.md).

## Erstellen von Sitzungen

Nach der Anmeldung bei der [Assurance](https://experience.adobe.com/assurance)-Benutzeroberfläche können Sie **[!UICONTROL Create Session]** auswählen, um mit der Erstellung einer Sitzung zu beginnen.

![Die Schaltfläche „Sitzung erstellen“ ist hervorgehoben und zeigt an, wo Sie eine Sitzung erstellen können.](./images/using-assurance/create-session.png)

Das **[!UICONTROL Create New Session]** Dialogfeld wird mit zwei Optionen zum Erstellen einer Sitzung angezeigt:

### Deep-Link-Verbindung

Wählen Sie diese Option aus, um eine eindeutige Sitzungs-URL, einen QR-Code und eine eindeutige PIN zu generieren. Scannen Sie den QR-Code oder öffnen Sie manuell den Sitzungs-Link in Ihrer App und geben Sie dann die PIN ein, um die Verbindung herzustellen.

Wählen Sie **[!UICONTROL Deep link connect]** aus und fahren Sie mit der Auswahl von **[!UICONTROL Start]** fort.

![Das Dialogfeld „Neue Sitzung erstellen“ mit aktivierter Option „Deep-Link-Verbindung“.](./images/using-assurance/create-new-session-deep-link.png)

Sie können jetzt einen Namen eingeben, um die Sitzung zu identifizieren, und dann eine **[!UICONTROL Base URL]** (Deep-Link-URL für Ihre App) angeben. Wählen Sie nach Angabe dieser Details **[!UICONTROL Next]** aus.

>[!INFO]
>
>Die Basis-URL ist die Stammdefinition, die zum Starten Ihrer App über eine URL verwendet wird. Es wird eine Sitzungs-URL generiert, mit der Sie die Assurance-Sitzung starten können. Ein Beispielwert könnte wie folgt aussehen: `myapp://default` Geben Sie im Feld **[!UICONTROL Base URL]** die Deep-Link-Basisdefinition Ihrer App ein.

![Die Eingabefelder für den Sitzungsnamen und die Basis-URL werden angezeigt.](./images/using-assurance/create-session-form-deep-link.png)

### Schnellverbindung

Wenn Sie eine Verbindung über Ihre App Trigger haben, wird Ihr Gerät in einer Liste der verfügbaren Geräte angezeigt. Wählen Sie **[!UICONTROL Quick connect]** aus, um die Assurance-Sitzung zu erstellen.

#### Voraussetzungen

Stellen Sie vor der Verwendung von Quick Connect sicher, dass Ihre App über die erforderlichen SDK-Versionen und -Implementierungen verfügt:

**Android SDK-Anforderungen:**

- Mobile Core v3.1.0 oder höher
- Adobe Journey Optimizer v3.1.0 oder höher
- Adobe Experience Platform Assurance v3.0.4 oder höher

**iOS SDK-Anforderungen:**

- Mobile Core v5.2.0 oder höher
- Adobe Journey Optimizer v5.1.1 oder höher
- Adobe Experience Platform Assurance v5.0.0 oder höher

**Implementierung:**

Ihr Programm muss die [`startSession`-API implementieren](https://developer.adobe.com/client-sdks/home/base/assurance/api-reference/#startsession-quick-connect) um die Assurance-Verbindung Trigger. Dieser API-Aufruf ist normalerweise in einem Aktionssatz enthalten oder wird in Ihrer App ausgelöst.

#### Schnellverbindungssitzung erstellen

![Das Dialogfeld „Neue Sitzung erstellen“ mit aktivierter Option „Schnellverbindung“.](./images/using-assurance/create-new-session-quick-connect.png)

Wählen Sie **[!UICONTROL Quick connect]** aus und fahren Sie mit der Auswahl von **[!UICONTROL Start]** fort. Daraufhin wird die Benutzeroberfläche für die Geräteauswahl angezeigt:

1. **Trigger der Assurance-Verbindung** - Geben Sie in Ihrer Mobile App oder Implementierung den Trigger für die Aktion ein, die die Assurance-Verbindung mithilfe der `startSession`-API initiiert. Dadurch wird Ihr Gerät auffindbar.

2. **Gerät auswählen und verbinden** - Sobald das Gerät in der Liste der verfügbaren Geräte angezeigt wird, wählen Sie es aus und klicken Sie auf **[!UICONTROL Connect]**.

![Die Benutzeroberfläche der Schnellverbindungs-Geräteauswahl mit verfügbaren Geräten.](./images/using-assurance/quick-connect-device-picker.png)

## Verbindung zu einer Sitzung herstellen

Die Schritte zum Verbinden hängen davon ab, welchen Sitzungstyp Sie verwenden:

### Deep-Link-Connect-Sitzungen

Für Sitzungen, die mit **[!UICONTROL Deep Link Connect]** erstellt wurden:

1. Navigieren Sie zu Ihrer Sitzungsdetailseite (für vorhandene Sitzungen) oder fahren Sie mit der Sitzungserstellung fort, um den Link, den QR-Code und die PIN anzuzeigen
2. Verwenden Sie die Kamera-App Ihres Geräts, um den QR-Code zu scannen, oder kopieren Sie den Link und öffnen Sie ihn in Ihrer App
3. Wenn Ihre App gestartet wird, wird der PIN-Eingabebildschirm überlagert. Geben Sie die PIN ein und drücken Sie **[!UICONTROL Connect]**

![Ein Dialogfeld mit den Optionen zum Herstellen einer Verbindung mit Ihrer Assurance-Sitzung wird angezeigt.](./images/using-assurance/deep-link-connection.png)

### Schnellverbindungssitzungen

Bei Sitzungen, die mit **[!UICONTROL Quick Connect]** erstellt wurden (erkennbar an einer Sitzungs-URL, die mit `adobeassurance://` beginnt), erfolgt die Verbindung automatisch über die Geräteauswahl-Oberfläche:

1. Navigieren Sie zur Seite mit den Sitzungsdetails (für vorhandene Sitzungen) oder fahren Sie mit der Erstellung der Sitzung fort
2. Im **[!UICONTROL Connect Device]** Abschnitt wird die Benutzeroberfläche für die Geräteauswahl angezeigt
3. Trigger des Aktionssatzes in der App, damit das Gerät auffindbar wird
4. Wählen Sie Ihr Gerät aus der Liste aus und klicken Sie auf **[!UICONTROL Connect]**

![Die Geräteauswahl-Schnittstelle mit den verfügbaren zu verbindenden Geräten.](./images/using-assurance/quick-connect-device-picker.png)

### Verbindung wird überprüft

Sie können überprüfen, ob Ihre App mit Assurance verbunden ist, wenn das Adobe Experience Platform-Symbol (rotes Adobe „A„) in Ihrer App angezeigt wird.

## Exportieren einer Sitzung

Um eine Assurance-Sitzung zu exportieren, wählen Sie auf der Seite „Sitzungsdetails“ Ihrer Anwendung die Option **[!UICONTROL Export to JSON]** in einer Sitzung aus:

![Exportieren einer Sitzung](./images/using-assurance/export-session.png)

Die Exportoption berücksichtigt die Suchfilterergebnisse und exportiert nur die in der Ereignisansicht angezeigten Ereignisse. Wenn Sie beispielsweise nach Ereignissen des Typs „Nachverfolgen“ suchen und dann **[!UICONTROL Export to JSON]** auswählen, werden nur die Ergebnisse des Typs „Nachverfolgen“ exportiert.