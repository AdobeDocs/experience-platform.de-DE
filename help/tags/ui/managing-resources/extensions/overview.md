---
title: Erweiterungen
description: Erfahren Sie, wie Tag-Erweiterungen in Adobe Experience Platform funktionieren.
source-git-commit: 010e05968f1d7ad5675b0f0af43d9cfcc1f3a2ff
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 70%

---

# Erweiterungen

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../../term-updates.md).

Eine Erweiterung ist ein gepackter Code-Satz, der die von Tags oder der Ereignisweiterleitung bereitgestellten Funktionen erweitert.

Durch Hinzufügen einer Erweiterung werden neue Datenelemente und neue Optionen zum Erstellen von Regeln hinzugefügt.

Erweiterungen bestimmen die Elemente, die beim Erstellen von Properties, Regeln und Datenelementen verfügbar sind. Sie bieten Folgendes:

* Ereignisse, Bedingungen und Ausnahmen
* Datenelemente
* Client-seitiger Code

Verwenden Sie die Links oben in der Liste „Erweiterungen“, um installierte Erweiterungen, den Katalog oder Updates anzuzeigen.

Wählen Sie eine Erweiterung aus und klicken Sie auf [!UICONTROL Konfigurieren], um die Einstellungen der Erweiterung anzuzeigen und zu ändern. Weitere Informationen zu Erweiterungsoptionen finden Sie im Abschnitt [Hinzufügen einer neuen Erweiterung](#add-a-new-extension) .

>[!IMPORTANT]
>
>Änderungen werden erst wirksam, nachdem sie [veröffentlicht](../../publishing/overview.md) wurden.

Standardmäßig bietet Adobe Erweiterungen, die gängige Integrationen unterstützen. Erweiterungen können mit benutzerdefinierten Konfigurationen angepasst werden. Konfigurationen werden über die Erweiterungen bereitgestellt. Klicken Sie zum Erstellen einer Konfiguration auf die Erweiterungskarte und dann auf **[!UICONTROL Neue Konfiguration hinzufügen]**.

## Erweiterungskatalog

Verwenden Sie den Erweiterungskatalog zum Durchsuchen, Konfigurieren und Bereitstellen von Marketing- und Werbetechnologien, die von unabhängigen Softwareanbietern entwickelt und gepflegt werden, sowie Erweiterungen für Adobe-Lösungen.

Die Seite „Erweiterungen“ bietet drei Ansichten:

* Installierte

   Zeigt alle installierten Erweiterungen an.

* Katalog
* Zeigt alle verfügbaren Erweiterungen an.
* Updates

   Zeigt Updates für installierte Erweiterungen an.

Klicken Sie auf **[!UICONTROL Erweiterungen]**, um alle installierten Erweiterungen anzuzeigen. Sie können den Katalog auch verwenden, um eine Liste aller verfügbaren Erweiterungen anzuzeigen und zu ermitteln, welche Erweiterungen verfügbar sind.

Weitere Informationen zu den Adobe-eigenen Erweiterungen finden Sie unter [Erweiterungsreferenz](../../../extensions/web/overview.md) .

## Hinzufügen neuer Erweiterungen {#add-a-new-extension}

Tags sind stark erweiterbar. Erweiterungen fügen Tags Kernfunktionen hinzu. Erweiterungen werden häufig verwendet, um Integrationen in andere Anwendungen zu schaffen.

1. Öffnen Sie auf der Übersichtsseite einer Eigenschaft die Registerkarte **[!UICONTROL Erweiterungen]**.
1. Wählen Sie eine Erweiterung aus.

   ![]()../../../images/extensions.png)

   * Wenn die Erweiterung vorhanden ist, wählen Sie sie aus dem Erweiterungskatalog aus.
   * Bewegen Sie den Mauszeiger über eine Erweiterung in Ihrer Liste, um sie zu konfigurieren oder zu deaktivieren.
   * Fügen Sie andere Erweiterungen aus dem Katalog hinzu, wenn sie derzeit nicht in der Liste aufgeführt sind.

   Die Haupterweiterung ist der Ausgangspunkt für Ihre neue Erweiterung. Die Standarderweiterung bietet Folgendes:

   * Standardereignis
   * Standardbedingungen und -ausnahmen
   * Standardmäßiger clientseitiger Code

   Diese Standardeinstellungen sind die Grundlage für die benutzerdefinierten Regeln, die Sie für Ihre Erweiterung erstellen.

Beim Erstellen oder Bearbeiten von Elementen können Sie in Ihrer [aktiven Bibliothek](../../publishing/libraries.md#active-library) speichern und Erstellungen vornehmen. Dadurch werden Ihre Änderungen direkt in Ihrer Bibliothek gespeichert, und ein Build wird ausgeführt. Der Build-Status wird angezeigt. Sie können auch über die Dropdown-Liste „Aktive Bibliothek“ eine neue Bibliothek erstellen.

## Konfigurieren einer Erweiterung

Bewegen Sie den Mauszeiger über eine installierte Erweiterung und klicken Sie auf **[!UICONTROL Konfigurieren]**.

>[!NOTE]
>
>Einige Erweiterungen erfordern keine Konfiguration und bieten keine Konfigurationsoptionen.

Jede konfigurierbare Erweiterung verfügt über individuelle Optionen. Informationen zu den für die einzelnen Adobe-Erweiterungen verfügbaren Optionen finden Sie unter [Erweiterungsreferenz](../../../extensions/web/overview.md) .
