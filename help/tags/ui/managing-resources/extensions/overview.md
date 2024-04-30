---
title: Erweiterungen
description: Machen Sie sich mit der Funktionsweise von Tag-Erweiterungen in Adobe Experience Platform vertraut.
exl-id: e911bedd-6c67-4339-91d7-839c8b00c153
source-git-commit: 31811b7448a285ee5d25872641354a6981c64471
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 94%

---

# Erweiterungen

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../../term-updates.md).

Eine Erweiterung ist ein gepackter Code-Satz, der die von Tags oder der Ereignisweiterleitung bereitgestellten Funktionen erweitert.

Durch Hinzufügen einer Erweiterung werden neue Datenelemente und neue Optionen zum Erstellen von Regeln hinzugefügt.

Erweiterungen bestimmen die Elemente, die beim Erstellen von Eigenschaften, Regeln und Datenelementen verfügbar sind. Sie bieten Folgendes:

* Ereignisse, Bedingungen und Ausnahmen
* Datenelemente
* Client-seitiger Code

Verwenden Sie die Links oben in der Liste „Erweiterungen“, um installierte Erweiterungen, den Katalog oder Updates anzuzeigen.

Wählen Sie eine Erweiterung aus und klicken Sie auf [!UICONTROL Konfigurieren], um die Einstellungen der Erweiterung anzuzeigen und zu ändern. Weitere Informationen zu Erweiterungsoptionen finden Sie im Abschnitt [Hinzufügen einer neuen Erweiterung](#add-a-new-extension).

>[!IMPORTANT]
>
>Änderungen werden erst wirksam, nachdem sie [veröffentlicht](../../publishing/overview.md) wurden.

Standardmäßig stellt Adobe Erweiterungen bereit, die gängige Integrationen unterstützen. Erweiterungen können mit benutzerdefinierten Konfigurationen angepasst werden. Konfigurationen werden über die Erweiterungen bereitgestellt. Klicken Sie zum Erstellen einer Konfiguration auf die Erweiterungskarte und dann auf **[!UICONTROL Neue Konfiguration hinzufügen]**.

## Erweiterungskatalog

Verwenden Sie den Erweiterungskatalog, um Marketing- und Werbetechnologien, die von unabhängigen Software-Anbietern entwickelt und gepflegt werden, sowie Erweiterungen für Adobe-Lösungen zu durchsuchen, zu konfigurieren und bereitzustellen.

Die Seite „Erweiterungen“ bietet drei Ansichten:

* Installierte

  Zeigt alle installierten Erweiterungen an.

* Katalog
* Zeigt alle verfügbaren Erweiterungen an.
* Updates

  Zeigt Updates für installierte Erweiterungen an.

Klicken Sie auf **[!UICONTROL Erweiterungen]**, um alle installierten Erweiterungen anzuzeigen. Sie können den Katalog auch verwenden, um eine Liste aller verfügbaren Erweiterungen anzuzeigen und zu ermitteln, welche Erweiterungen verfügbar sind.

Ausführliche Informationen zu Adobe-eigenen Erweiterungen finden Sie in der [Erweiterungsreferenz](../../../extensions/client/overview.md).

## Hinzufügen neuer Erweiterungen {#add-a-new-extension}

Tags sind extrem erweiterbar. Erweiterungen fügen Tags Kernfunktionen hinzu. Erweiterungen werden häufig verwendet, um Integrationen in andere Anwendungen zu schaffen.

>[!TIP]
>
>Verwenden Sie die Produkthilfe in der rechten Leiste, um mehr über Erweiterungen zu erfahren und zusätzliche verfügbare Ressourcen anzuzeigen.

1. Öffnen Sie auf der Übersichtsseite einer Eigenschaft die Registerkarte **[!UICONTROL Erweiterungen]**.
1. Wählen Sie eine Erweiterung aus.

   ![Registerkarte &quot;Katalog&quot;mit Core-Erweiterungen auf der Registerkarte &quot;Erweiterungen&quot;.](../../../images/extensions.png)

   * Wenn die Erweiterung vorhanden ist, wählen Sie sie aus dem Erweiterungskatalog aus.
   * Bewegen Sie den Mauszeiger über eine Erweiterung in Ihrer Liste, um sie zu konfigurieren oder zu deaktivieren.
   * Fügen Sie andere Erweiterungen aus dem Katalog hinzu, wenn sie derzeit nicht in der Liste aufgeführt sind.

   Die Haupterweiterung ist der Ausgangspunkt für Ihre neue Erweiterung. Die Standarderweiterung bietet Folgendes:

   * Standardereignis
   * Standardbedingungen und -ausnahmen
   * Standardmäßiger Client-seitiger Code

   Diese Standardeinstellungen sind die Grundlage für die benutzerdefinierten Regeln, die Sie für Ihre Erweiterung erstellen.

Beim Erstellen oder Bearbeiten von Elementen können Sie in Ihrer [aktiven Bibliothek](../../publishing/libraries.md#active-library) speichern und Erstellungen vornehmen. Dadurch werden Ihre Änderungen direkt in Ihrer Bibliothek gespeichert, und ein Build wird ausgeführt. Der Build-Status wird angezeigt. Sie können auch über die Dropdown-Liste „Aktive Bibliothek“ eine neue Bibliothek erstellen.

## Konfigurieren einer Erweiterung

Bewegen Sie den Mauszeiger über eine installierte Erweiterung und klicken Sie auf **[!UICONTROL Konfigurieren]**.

>[!NOTE]
>
>Einige Erweiterungen erfordern keine Konfiguration und bieten keine Konfigurationsoptionen.

Jede konfigurierbare Erweiterung verfügt über individuelle Optionen. Informationen zu den für die verschiedenen Adobe-Erweiterungen verfügbaren Optionen finden Sie in der [Erweiterungsreferenz](../../../extensions/client/overview.md).
