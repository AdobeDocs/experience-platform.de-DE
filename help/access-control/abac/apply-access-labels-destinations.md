---
title: Verwenden von Zugriffsbeschriftungen zur Verwaltung des Benutzerzugriffs auf Zieldatenflüsse
description: Erfahren Sie, wie Sie mithilfe von Zugriffsbeschriftungen den Benutzerzugriff auf Ziel-Datenflüsse verwalten können, sodass nur eine Untergruppe von Benutzern in Ihrer Organisation Zugriff auf bestimmte Ziel-Datenflüsse erhält.
role: Developer, Admin, User
exl-id: 85944720-8551-491c-8991-dd9668beb0ca
source-git-commit: e1b8ca463146d300b48257304778a82aa745df73
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 1%

---

# Verwenden von Zugriffsbeschriftungen zur Verwaltung des Benutzerzugriffs auf Zieldatenflüsse

Im Rahmen der [[!UICONTROL attributbasierten Zugriffssteuerung]](overview.md) in Real-Time CDP können Sie jetzt Zugriffsbeschriftungen auf [Ziel-Datenflüsse“ &#x200B;](../../dataflows/ui/monitor-destinations.md). Auf diese Weise können Sie sicherstellen, dass nur eine Teilmenge der Benutzenden in Ihrer Organisation Zugriff auf bestimmte Zieldatenflüsse erhält.

Wenn Sie einem bestimmten Ziel eine Zugriffsbeschriftung hinzufügen, können nur Benutzer, die Zugriff auf eine Rolle haben, der diese Beschriftung zugewiesen ist, diesen Ziel-Datenfluss anzeigen und bearbeiten. Wenn ein Ziel-Datenfluss nicht mit Beschriftungen versehen ist, ist er für alle Benutzer sichtbar, die zu Ihrer Organisation gehören.

Lesen Sie diese Seite, um Beispielanwendungsfälle, Voraussetzungen und andere wichtige Hinweise zur Verwendung dieser Funktion zu verstehen, bevor Sie Zugriffsbeschriftungen auf Ziel-Datenflüsse anwenden können.

## Voraussetzungen {#prerequisites}

Beachten Sie die folgenden Voraussetzungen, die erfüllt sein müssen, bevor Sie mit der Verwendung dieser Funktion beginnen. Um sich mit der [!UICONTROL attributbasierten Zugriffssteuerung“ vertraut &#x200B;] machen, empfiehlt Adobe außerdem, die folgenden Artikel zu lesen:

* [Attributbasierte Zugriffssteuerung – Übersicht](/help/access-control/abac/overview.md)
* [End-to-End-Handbuch zur attributbasierten Zugriffssteuerung](/help/access-control/abac/end-to-end-guide.md)

### Zugriff auf die Benutzeroberfläche für Berechtigungen {#access-permissions-ui}

[!UICONTROL Berechtigungen] ist der Bereich von Experience Cloud, in dem Admins Benutzerrollen und Richtlinien definieren können, um Berechtigungen für Funktionen und Objekte innerhalb einer Produktanwendung zu verwalten. Lesen Sie [&#x200B; Abschnitt „Berechtigungen](/help/access-control/abac/end-to-end-guide.md#permissions), um zu beginnen.

### Erstellen von Rollen, Kennzeichnungen und Zuweisen von Benutzern {#create-roles-labels-assign-users}

Nachdem Sie Zugriff auf die Benutzeroberfläche [!UICONTROL Berechtigungen] erhalten haben, müssen Sie oder ein Mitglied Ihres Teams Rollen einrichten und diesen Rollen die erforderlichen Beschriftungen hinzufügen. Schließlich müssen die Benutzer, die auf Ressourcen zugreifen sollten, die mit den spezifischen Kennzeichnungen gekennzeichnet sind, zur Rolle hinzugefügt werden. Lesen Sie die folgenden Dokumentationsabschnitte:

* [Erstellen einer neuen Rolle](/help/access-control/abac/ui/roles.md)
* [Hinzufügen von Beschriftungen zu einer Rolle](/help/access-control/abac/end-to-end-guide.md#label-roles)
* [Benutzer zu einer Rolle hinzufügen](/help/access-control/ui/users.md)

### Erstellen von Zieldatenflüssen {#create-dataflow}

Sie müssen zunächst eine Verbindung zum gewünschten Ziel herstellen und einen Datenfluss erstellen, um Daten zu exportieren, bevor Sie Zugriffsbeschriftungen auf den Datenfluss anwenden können.

Lesen Sie die Handbücher unter [Verbindung mit einem Ziel herstellen](/help/destinations/ui/connect-destination.md) und [Daten für das Ziel aktivieren](/help/destinations/ui/activation-overview.md). Wählen Sie dann das gewünschte Ziel aus dem [Katalog der verfügbaren Connectoren](/help/destinations/catalog/overview.md).

## Bereits verfügbar: Zugriffskennzeichnungen auf andere Experience Platform-Ressourcen anwenden {#apply-labels-other-resources}

Diese Version ermöglicht es Ihnen, Benutzern Zugriff auf Objektebene auf bestimmte Zieldatenflüsse zu gewähren. Die Funktion zum Gewähren der Zugriffssteuerung auf Objektebene ist jedoch bereits allgemein für andere Experience Platform-Ressourcen verfügbar, z. B. [Zielgruppen](/help/access-control/abac/end-to-end-guide.md#apply-labels-to-segments).

## Anwendungsbeispiel {#use-case-example}

Mit der Zugriffssteuerung auf Objektebene für Ziele können Sie bestimmte Marketing-Teams darauf beschränken, nur Zugriff auf ihre spezifischen Ziele zu erhalten. Wenn Ihre Organisation beispielsweise Kundendaten in mehreren geografischen Standorten wie den USA und Großbritannien hat, können Sie ein Marketing-Team darauf beschränken, die Datenflüsse nur für den US-Standort anzuzeigen und zu bearbeiten, und ein anderes Marketing-Team kann die Datenflüsse für den Standort Großbritannien anzeigen und bearbeiten.

## Anwenden von Zugriffskennzeichnungen auf Ziel-Datenflüsse {#apply-labels-to-destination-dataflow}

So wenden Sie Zugriffsbeschriftungen auf einen bestimmten Datenfluss an:

1. Navigieren Sie zu **[!UICONTROL Ziele]** > **[!UICONTROL Durchsuchen]** und suchen Sie nach dem Zieldatenfluss, für den Sie den Benutzerzugriff einschränken möchten.
1. Klicken Sie auf die Auslassungszeichen (`...`) in der Spalte [!UICONTROL Name] und verwenden Sie das Steuerelement ![Steuerung „Details bearbeiten](/help/images/icons/key.png) **[!UICONTROL Zugriffskennzeichnungen anwenden]**, um neue Kennzeichnungen hinzuzufügen und die vorhandenen Kennzeichnungen für den Datenfluss zu verwalten.
   ![Wählen Sie Zugriffsbeschriftungen anwenden in der Durchsuchen-Ansicht des Arbeitsbereichs „Ziele“.](/help/access-control/images/olac/apply-access-labels.png)
1. Wählen Sie die Kennzeichnungen aus, die Sie zum Ziel-Datenfluss hinzufügen möchten, und wählen Sie **[!UICONTROL Speichern]**.
   ![Wählen Sie die Zugriffsbeschriftungen in aus, die für den Ziel-Datenfluss gelten sollen.](/help/access-control/images/olac/view-access-labels.png)
1. Beachten Sie, dass im Datenfluss jetzt eine Zugriffsbeschriftung in der Benutzeroberfläche angezeigt wird.
   ![Ansicht mehrerer Ziel-Datenflüsse mit dem ausgewählten Datenfluss, wie eine Zugriffskennzeichnung angezeigt wird.](/help/access-control/images/olac/dataflow-with-access-label.png)

Wenn ein Ziel-Datenfluss nicht mit Beschriftungen versehen ist, ist er für alle Benutzer sichtbar. Wenn der Datenfluss mit einer oder mehreren Zugriffsbeschriftungen markiert ist, ist er nur für Benutzer sichtbar, die zu einer Rolle gehören, die dieselbe Beschriftung oder eine Kombination von Beschriftungen hat.

Sie können Standard- und benutzerdefinierte Kennzeichnungen zu Ziel-Datenflüssen hinzufügen. Nachdem Sie eine Bezeichnung zu Ziel-Datenflüssen hinzugefügt haben:

* Benutzer, die Rollen mit Zugriff auf dieselbe Kennzeichnung zugewiesen sind, können den Datenfluss mit der neuen Kennzeichnung in der Benutzeroberfläche anzeigen. Sie können den Ziel-Datenfluss in der Benutzeroberfläche oder über APIs anzeigen und bearbeiten.

* Benutzende, *(nicht* Rollen mit Zugriff auf dieselbe Kennzeichnung zugewiesen sind, haben keinen Zugriff auf den Ziel-Datenfluss, um ihn in der Benutzeroberfläche oder über APIs anzuzeigen oder zu bearbeiten.

## Wichtige Hinweise und Hinweise {#important-callouts}

Derzeit können Zugriffsbeschriftungen nur auf vorhandene Datenflüsse angewendet werden. Das bedeutet, dass Sie einen Datenfluss zu einem Ziel erstellen müssen, bevor Sie Zugriffsbeschriftungen anwenden können.

Sie können eine Zugriffsbeschriftung nicht auf einen Ziel-Datenfluss anwenden, wenn Sie keinen Zugriff auf diese Beschriftung haben.

Beim Hinzufügen mehrerer Beschriftungen zu einem Ziel-Datenfluss müssen Benutzende, die den Datenfluss anzeigen und bearbeiten können sollen, zu einer Rolle mit mindestens derselben Kombination von Beschriftungen hinzugefügt werden. Wenn Sie beispielsweise die Kennzeichnungen C1, I2 und eine weitere benutzerdefinierte Kennzeichnung auf einen Ziel-Datenfluss anwenden, können nur Benutzer, die zu Rollen mit Zugriff auf die Kombination dieser drei Kennzeichnungen hinzugefügt wurden, diesen spezifischen Ziel-Datenfluss anzeigen und bearbeiten.

>[!NOTE]
>
> Bei der Suche nach Ziel-Datenflüssen mithilfe des Suchfelds oben in der Experience Platform-Benutzeroberfläche können die Ergebnisse Ziel-Datenflüsse enthalten, die aufgrund Ihrer Benutzerzugriffskennzeichnungen nicht angezeigt werden können. Dieses Verhalten wird in einer zukünftigen Aktualisierung korrigiert.

![Venn-Diagramm, das zeigt, wie nur bestimmte Benutzende Zugriff auf Ziele mit mehreren angewendeten Kennzeichnungen haben.](/help/access-control/images/olac/multiple-labels-venn.png)

## Nächste Schritte {#next-steps}

Wenn Sie die Schritte in diesem Dokument befolgen, wissen Sie jetzt, wie Sie Zugriffsbeschriftungen auf Ziel-Datenflüsse anwenden, damit nur eine Untergruppe von Benutzern in Ihrer Organisation Zugriff auf bestimmte Ziel-Datenflüsse erhält.

Als Nächstes können Sie mehr über andere Funktionen lesen, die von der [!UICONTROL attributbasierten Zugriffssteuerung) &#x200B;] Aktivieren von Daten für Ziele unterstützt werden. Sie können beispielsweise den Zugriff von Benutzern auf (nur [&#x200B; bestimmte Felder anzeigen und aktivieren](/help/access-control/abac/overview.md#destinations) einschränken.
