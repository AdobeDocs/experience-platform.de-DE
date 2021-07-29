---
title: Common Analytics-Erweiterung – Übersicht
description: Erfahren Sie mehr über die allgemeine Analytics-Tag-Erweiterung in Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 66%

---

# Common Analytics Plugins-Erweiterung – Übersicht

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../../term-updates.md).

Verwenden Sie diesen Abschnitt, um Informationen zum Konfigurieren der allgemeinen Analytics-Plug-in-Erweiterung und zu den Optionen zu beziehen, die verfügbar werden, wenn diese Erweiterung zusätzlich zur [!DNL Adobe Analytics]-Erweiterung verwendet wird.

## Konfigurieren der allgemeinen Analytics-Plug-in-Erweiterung

Dieser Abschnitt enthält Informationen zu den verfügbaren Optionen beim Konfigurieren der allgemeinen Analytics-Plug-in-Erweiterung.

>[!IMPORTANT]
>
>Die allgemeine Analytics-Plug-in-Erweiterung erweitert die [!DNL Adobe Analytics]-Erweiterung. Damit sie funktioniert, müssen Sie die [!DNL Adobe Analytics]-Erweiterung auf Ihrer Eigenschaft installiert haben. Darüber hinaus müssen Sie den Tracker in der [!DNL Adobe Analytics]-Erweiterung global verfügbar machen.

Auf Erweiterungsebene ist keine zusätzliche Konfiguration erforderlich.

## Hinzufügen von Plug-ins zur [!DNL Adobe Analytics]-Erweiterung

Um die in dieser Erweiterung bereitgestellten Plug-ins verwenden zu können, müssen Sie zunächst die Plug-ins, die Sie verwenden möchten, in ihrer eigenen Regel initialisieren.

1. Erstellen Sie eine neue Regel.
1. Fügen Sie das Ereignis „Core - Library Loaded“ hinzu (Seitenanfang).
1. Verwenden Sie eine der folgenden Initialisierungsmethoden.

## Aktionstypen der allgemeinen Analytics-Plug-in-Erweiterung

In diesem Abschnitt werden die in der allgemeinen Analytics-Plug-in-Erweiterung verfügbaren Aktionstypen beschrieben.

Die allgemeine Analytics-Plug-in-Erweiterung beinhaltet die folgenden Aktionen:

* [Initialisieren](#initialize)
* [Plug-in initialisieren](#initialize-plugin)

### Initialisieren

>[!IMPORTANT]
>
>Diese Aktion ist zwar einfacher zu implementieren, Adobe Consulting empfiehlt jedoch nicht, diese Aktion zu verwenden, da sie die Gewichtung des Plug-ins erhöht.

Bei dieser Aktion können Sie jedes Plug-in auswählen, das Sie in Ihre Implementierung aufnehmen möchten, und die Änderungen speichern. Wählen Sie so viele oder so wenige aus, wie Sie während der Implementierung verwenden möchten. Links zur Dokumentation über die Verwendung der einzelnen Plug-ins und eine kurze Beschreibung finden Sie in der [Übersicht über die Analytics-Plug-ins](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/impl-plugins.html?lang=de).

### Plug-in initialisieren

Mit diesen Aktionen initialisieren Sie einzeln jedes Plug-in, das Sie verwenden möchten. Um alle Plug-ins zu initialisieren, die Sie in Ihrer Eigenschaft verwenden möchten, fügen Sie einfach die entsprechende Aktion zu Ihrer Regel hinzu und speichern Sie die Regel. Obwohl die Konfiguration der Erweiterung auf diese Weise etwas aufwändiger ist, bietet sie eine größere Code-Effizienz. Daher empfiehlt Adobe diesen Ansatz.

## Datenelemente der allgemeinen Analytics-Plug-in-Erweiterung

In diesem Abschnitt werden die in der allgemeinen Analytics-Plug-in-Erweiterung verfügbaren Datenelemente beschrieben.

### getGeoCoordinates

Ermöglicht Benutzern die Nutzung der nativen Datenerfassungs-Benutzeroberfläche in Adobe Experience Platform zum Einrichten und Konfigurieren des Plug-ins getGeoCoordinates .

### getNewRepeat

Ermöglicht Benutzern die Nutzung der nativen Datenerfassungs-Benutzeroberfläche zum Einrichten und Konfigurieren des Plug-ins getNewRepeat .

### getPageName

Ermöglicht Benutzern die Nutzung der nativen Datenerfassungs-Benutzeroberfläche zum Einrichten und Konfigurieren des Plug-ins getPageName .

### getResponsiveLayout

Ermöglicht Benutzern die Nutzung der nativen Datenerfassungs-Benutzeroberfläche zum Einrichten und Konfigurieren des Plug-ins getResponsiveLayout .

### getTimeParting

Ermöglicht Benutzern die Nutzung der nativen Datenerfassungs-Benutzeroberfläche zum Einrichten und Konfigurieren des Plug-ins getTimeParting .

### getTimeSinceLastVisit

Ermöglicht Benutzern die Nutzung der nativen Datenerfassungs-Benutzeroberfläche zum Einrichten und Konfigurieren des Plug-ins getTimeSinceLastVisit .

### getVisitDuration

Ermöglicht Benutzern die Nutzung der nativen Datenerfassungs-Benutzeroberfläche zum Einrichten und Konfigurieren des Plug-ins getVisitDuration .

### getVisitNum

Ermöglicht Benutzern die Nutzung der nativen Datenerfassungs-Benutzeroberfläche zum Einrichten und Konfigurieren des Plug-ins getVisitNum .
