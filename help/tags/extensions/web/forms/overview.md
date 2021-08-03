---
title: Übersicht über die Adobe Experience Manager Forms-Erweiterung
description: Erfahren Sie mehr über die Adobe Experience Manager Forms-Tag-Erweiterung in Adobe Experience Platform.
source-git-commit: f31a1d2e84dee262e04f1db0415ffd76248ecb6c
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 6%

---

# Übersicht über die Adobe Experience Manager Forms-Erweiterung

Dieses Dokument bietet einen Überblick über die Adobe Experience Manager Forms-Tag-Erweiterung in Adobe Experience Platform.

## Ereignisse

Die Erweiterung stellt die folgenden Ereignistypen bereit:

1. **Render**: Trigger, wenn der Benutzer ein Formular wiedergibt (öffnet).
1. **Fehler**: Trigger, wenn der Benutzer einen Validierungsfehler in einem Formular macht.
1. **Hilfe**: Trigger, wenn der Benutzer auf das Hilfesymbol eines Felds klickt.
1. **Senden**: Trigger beim Senden des Formulars.
1. **Feldbesuch**: Trigger beim Besuch eines Felds.
1. **Abbruch**: Trigger, wenn der Benutzer die Registerkarte schließt oder zu einer anderen URL navigiert.
1. **Speichern**: Trigger, wenn ein Formular im Portal gespeichert wird.

>[!IMPORTANT]
>
>Das Ereignis &quot;Speichern&quot;ist derzeit nicht für Formulare als Cloud-Service verfügbar. Benutzerdefinierte Ereignisse, die vom Regeleditor in Adaptive Forms gesendet werden, können mit dem Hauptereignis &quot;Benutzerdefiniertes Ereignis erfassen&quot;erfasst werden.

## Datenelemente

Die -Erweiterung bietet mehrere Datenelemente, mit denen Eigenschaften in Analytics-Aufrufen gesendet werden können.

## Erste Schritte

Gehen Sie wie folgt vor, um mit der Erweiterung zu beginnen.

1. Installieren Sie die Adobe Experience Manager Forms-Erweiterung aus dem Erweiterungskatalog. Nach der Installation ist keine weitere Konfiguration erforderlich.
2. Installieren und konfigurieren Sie die [Adobe Analytics-Erweiterung](../analytics/overview.md#Configure-the-Adobe-Analytics-extension).

## Erstellen einer Regel

Eine Regel, die die Experience Manager Forms-Erweiterung verwendet, würde wie folgt aussehen:

![Aktionskonfiguration](./images/rule.png)

Gehen Sie wie folgt vor, um eine ähnliche Regel für Ihre Implementierung zu erstellen.

### Ereignis hinzufügen

1. Wählen Sie **Adobe Experience Manager Forms** im Dropdown-Menü &quot;Erweiterung&quot;.
2. Wählen Sie das zu erfassende Ereignis aus.

![Aktionskonfiguration](./images/AEM-forms-event.png)

### Hinzufügen einer Aktion

1. Wählen Sie &quot;Adobe Analytics&quot;im Dropdown-Menü &quot;Erweiterung&quot;.
2. Wählen Sie &quot;set variable&quot;in der Dropdown-Liste Aktionstyp aus.
3. Wählen Sie in der Konfigurationsansicht die Eigenschaften und Ereignisse aus, die gesendet werden sollen.
4. Fügen Sie die Aktion &quot;Signal senden&quot;hinzu, um den Analytics-Aufruf mit den in Schritt 3 festgelegten Ereignissen und Eigenschaften zu senden.
   ![Aktionskonfiguration](./images/AEM-forms-sendBeacon.png)
5. Fügen Sie die Aktion &quot;clear variable&quot;hinzu.

![Aktionskonfiguration](./images/AEM-forms-action.png)