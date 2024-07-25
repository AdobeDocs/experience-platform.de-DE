---
title: Verwenden von Zugriffsbeschriftungen zum Verwalten des Benutzerzugriffs auf Ziel-Datenflüsse
description: Erfahren Sie, wie Sie mit Zugriffsbeschriftungen den Benutzerzugriff auf Ziel-Datenflüsse verwalten können, damit nur eine Untergruppe von Benutzern in Ihrer Organisation Zugriff auf bestimmte Ziel-Datenflüsse erhält.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
role: Developer, Admin, User
exl-id: 85944720-8551-491c-8991-dd9668beb0ca
source-git-commit: 68781d27e374261108955b24dfb7b46141f5108b
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 1%

---

# Verwenden von Zugriffsbeschriftungen zum Verwalten des Benutzerzugriffs auf Ziel-Datenflüsse

Im Rahmen der Funktion [!UICONTROL Attributbasierte Zugriffssteuerung] in Real-Time CDP können Sie jetzt Zugriffsbeschriftungen auf Ziel-Datenflüsse anwenden. Dadurch können Sie sicherstellen, dass nur eine Untergruppe von Benutzern in Ihrer Organisation Zugriff auf bestimmte Ziel-Datenflüsse erhält.

Wenn Sie eine Zugriffsbeschriftung zu einem bestimmten Ziel hinzufügen, können nur Benutzer, die Zugriff auf eine Rolle haben, der diese Beschriftung zugewiesen ist, diesen Ziel-Datenfluss anzeigen und bearbeiten. Wenn ein Ziel-Datenfluss nicht mit Bezeichnungen markiert ist, ist er für alle Benutzer Ihrer Organisation sichtbar.

Lesen Sie diese Seite, um sich mit Beispielanwendungsfällen, Voraussetzungen für die Anwendung von Zugriffsbeschriftungen auf Ziel-Datenflüsse und anderen wichtigen Hinweisen bei der Verwendung dieser Funktion vertraut zu machen.

## Voraussetzungen {#prerequisites}

Beachten Sie die folgenden Voraussetzungen, die erfüllt sein müssen, bevor Sie mit der Verwendung dieser Funktion beginnen. Um sich mit der Funktion [!UICONTROL Attributbasierte Zugriffssteuerung] vertraut zu machen, empfiehlt Adobe außerdem, die folgenden Artikel zu lesen:

* [Attributbasierte Zugriffssteuerung – Übersicht](/help/access-control/abac/overview.md)
* [Leitfaden zur attributbasierten Zugriffskontrolle von Ende zu Ende](/help/access-control/abac/end-to-end-guide.md)

### Zugriff auf die Berechtigungs-Benutzeroberfläche {#access-permissions-ui}

[!UICONTROL Berechtigungen] ist der Bereich des Experience Cloud, in dem Administratoren Benutzerrollen und Richtlinien definieren können, um Berechtigungen für Funktionen und Objekte in einer Produktanwendung zu verwalten. Lesen Sie den Abschnitt [Berechtigungen](/help/access-control/abac/end-to-end-guide.md#permissions) , um zu beginnen.

### Erstellen von Rollen, Bezeichnungen und Zuweisen von Benutzern {#create-roles-labels-assign-users}

Nachdem Sie Zugriff auf die Benutzeroberfläche von [!UICONTROL permissions] erhalten haben, müssen Sie oder ein Mitglied Ihres Teams Rollen einrichten und die erforderlichen Beschriftungen zu diesen Rollen hinzufügen. Schließlich müssen die Benutzer, die auf Ressourcen zugreifen sollen, die mit den spezifischen Bezeichnungen beschriftet sind, zur Rolle hinzugefügt werden. Lesen Sie die folgenden Dokumentationsabschnitte:

* [Erstellen einer neuen Rolle](/help/access-control/abac/ui/roles.md)
* [Hinzufügen von Bezeichnungen zu einer Rolle](/help/access-control/abac/end-to-end-guide.md#label-roles)
* [Benutzer zu einer Rolle hinzufügen](/help/access-control/ui/users.md)

### Erstellen von Ziel-Datenflüssen {#create-dataflow}

Sie müssen zunächst eine Verbindung zum gewünschten Ziel herstellen und einen Datenfluss erstellen, um Daten zu exportieren, bevor Sie Zugriffsbeschriftungen auf den Datenfluss anwenden können.

Lesen Sie die Anleitungen unter [Verbindung zu einem Ziel herstellen](/help/destinations/ui/connect-destination.md) und [ Aktivieren von Daten zum Ziel](/help/destinations/ui/activation-overview.md). Wählen Sie dann das gewünschte Ziel aus dem [Katalog der verfügbaren Connectoren](/help/destinations/catalog/overview.md) aus.

## Bereits verfügbar: Anwenden von Zugriffsbeschriftungen auf andere Experience Platform-Ressourcen {#apply-labels-other-resources}

Diese Version ermöglicht es Ihnen zwar, Benutzern auf Objektebene Zugriff auf bestimmte Ziel-Datenflüsse zu gewähren, doch ist die Funktion zum Gewähren der Zugriffskontrolle auf Objektebene bereits für andere Experience Platform-Ressourcen wie [Zielgruppen](/help/access-control/abac/end-to-end-guide.md#apply-labels-to-segments) verfügbar.

## Anwendungsbeispiel {#use-case-example}

Mit der Zugriffskontrolle auf Objektebene für Ziele können Sie bestimmte Marketing-Teams auf den Zugriff auf ihre spezifischen Ziele beschränken. Wenn Ihr Unternehmen beispielsweise über Kundendaten an verschiedenen geografischen Standorten wie den USA und Großbritannien verfügt, können Sie ein Marketing-Team darauf beschränken, die Datenflüsse nur für den US-Standort anzuzeigen und zu bearbeiten, und ein anderes Marketing-Team kann die Datenflüsse für den britischen Standort anzeigen und bearbeiten.

## Anwenden von Zugriffsbeschriftungen auf Ziel-Datenflüsse {#apply-labels-to-destination-dataflow}

So wenden Sie Zugriffsbeschriftungen auf einen bestimmten Datenfluss an:

1. Navigieren Sie zu **[!UICONTROL Ziele]** > **[!UICONTROL Durchsuchen]** und suchen Sie den Ziel-Datenfluss, auf den Sie den Zugriff der Benutzer beschränken möchten.
1. Wählen Sie die Auslassungszeichen (`...`) in der Spalte [!UICONTROL Name] aus und verwenden Sie das Steuerelement ![Details bearbeiten](/help/images/icons/key.png) **[!UICONTROL Zugriffsbeschriftungen anwenden]** , um neue Beschriftungen hinzuzufügen und die vorhandenen Beschriftungen für den Datenfluss zu verwalten.
   ![Wählen Sie im Arbeitsbereich &quot;Ziele durchsuchen&quot;die Option Zugriffsbeschriftungen anwenden.](/help/access-control/images/olac/apply-access-labels.png)
1. Wählen Sie die Beschriftungen aus, die Sie dem Ziel-Datenfluss hinzufügen möchten, und wählen Sie **[!UICONTROL Speichern]** aus.
   ![Wählen Sie die Zugriffsbeschriftungen in aus, die für den Ziel-Datenfluss gelten sollen.](/help/access-control/images/olac/view-access-labels.png)
1. Beachten Sie, dass im Datenfluss jetzt eine Zugriffsbeschriftung in der Benutzeroberfläche angezeigt wird.
   ![Anzeigen mehrerer Ziel-Datenflüsse mit dem ausgewählten Datenfluss zur Anzeige einer Zugriffsbeschriftung.](/help/access-control/images/olac/dataflow-with-access-label.png)

Wenn ein Ziel-Datenfluss nicht mit Bezeichnungen markiert ist, wird er für alle Benutzer angezeigt. Wenn der Datenfluss mit einer oder mehreren Zugriffsbeschriftungen markiert ist, wird er nur für Benutzer angezeigt, die zu einer Rolle gehören, die über dieselbe Beschriftung oder Kombination von Bezeichnungen verfügt.

Sie können Ziel-Datenflüssen standardmäßige und benutzerdefinierte Bezeichnungen hinzufügen. Nachdem Sie den Ziel-Datenflüssen eine Bezeichnung hinzugefügt haben:

* Benutzer, die Rollen mit Zugriff auf dieselbe Beschriftung zugewiesen sind, können den Datenfluss mit der neuen Beschriftung in der Benutzeroberfläche anzeigen. Sie können den Ziel-Datenfluss in der Benutzeroberfläche oder über APIs anzeigen und bearbeiten.

* Benutzer, die Rollen mit Zugriff auf dieselbe Beschriftung *nicht* zugewiesen sind, haben keinen Zugriff auf den Ziel-Datenfluss, um ihn in der Benutzeroberfläche oder über APIs anzuzeigen oder zu bearbeiten.

## Wichtige Hinweise und Informationen {#important-callouts}

Derzeit können Zugriffsbeschriftungen nur auf vorhandene Datenflüsse angewendet werden. Das bedeutet, dass jemand den Datenfluss zum Ziel erstellen muss, bevor Zugriffsbeschriftungen angewendet werden können.

Wenn Sie keinen Zugriff auf diese Beschriftung haben, können Sie einem Ziel-Datenfluss keine Zugriffsbeschriftung zuweisen.

Beim Hinzufügen mehrerer Bezeichnungen zu einem Ziel-Datenfluss müssen Benutzer, die den Datenfluss anzeigen und bearbeiten können sollen, einer Rolle mit mindestens derselben Kombination von Bezeichnungen hinzugefügt werden. Wenn Sie beispielsweise die Beschriftungen C1, I2 und eine andere benutzerdefinierte Beschriftung auf einen Ziel-Datenfluss anwenden, können nur Benutzer, die Rollen mit Zugriff auf die Kombination dieser drei Beschriftungen hinzugefügt wurden, diesen spezifischen Ziel-Datenfluss anzeigen und bearbeiten.

![Venn-Diagramm, das zeigt, wie nur bestimmte Benutzer Zugriff auf Ziele mit mehreren angewendeten Bezeichnungen haben.](/help/access-control/images/olac/multiple-labels-venn.png)

## Nächste Schritte {#next-steps}

Indem Sie die Schritte in diesem Dokument ausführen, wissen Sie jetzt, wie Sie Zugriffsbeschriftungen auf Ziel-Datenflüsse anwenden, damit nur eine Untergruppe von Benutzern in Ihrer Organisation Zugriff auf bestimmte Ziel-Datenflüsse erhält.

Als Nächstes erfahren Sie mehr über andere Funktionen, die von der [!UICONTROL Attributbasierten Zugriffskontrolle] unterstützt werden, wenn Sie Daten für Ziele aktivieren. Sie können beispielsweise den Zugriff der Benutzer auf [anzeigen und nur bestimmte Felder aktivieren](/help/access-control/abac/overview.md#destinations).
