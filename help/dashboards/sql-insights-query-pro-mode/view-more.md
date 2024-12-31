---
title: Mehr anzeigen
description: Erfahren Sie mehr über die verschiedenen Anzeigeoptionen für Ihre SQL-analysierten Daten. Über Ihr benutzerdefiniertes Dashboard können Sie die tabellarischen Ergebnisse Ihrer Analyse anzeigen oder die verarbeiteten Daten im CSV-Format herunterladen.
exl-id: f57d85cf-dbd2-415c-bf01-8faa49871377
source-git-commit: ddf886052aedc025ff125c03ab63877cb049583d
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 1%

---

# Mehr anzeigen {#view-more}

Nachdem Sie mit [Query Pro](./overview.md)Modus) eine [Custom Insight](./overview.md#query-pro-mode) erstellt haben, können Sie Ihre Diagrammdaten in verschiedenen Formaten anzeigen. Sie können entweder eine tabellarische Form der Ergebnisse anzeigen oder die Daten als CSV-Datei herunterladen, um sie in einer Tabelle anzuzeigen.

## Tabellarische Ergebnisse {#tabulated-results}

Für jedes Diagramm, das mit dem Abfrage-Pro-Modus über SQL erstellt wurde, können Sie die tabellarischen Ergebnisse Ihrer Analyse in der Experience Platform-Benutzeroberfläche anzeigen.

Wählen Sie im benutzerdefinierten Dashboard die Auslassungszeichen (`...`) eines beliebigen Widgets aus, um auf die Optionen [!UICONTROL Mehr anzeigen] und [!UICONTROL SQL anzeigen] zuzugreifen.

![Ein benutzerdefiniertes Dashboard mit einem Insight-Dropdown-Menü mit Auslassungspunkten und den hervorgehobenen Optionen „Mehr anzeigen“ und „SQL anzeigen“.](../images/sql-insights-query-pro-mode/ellipses-dropdown.png)

## CSV herunterladen {#download-csv}

Die Funktion [!UICONTROL Mehr anzeigen] zeigt die spezifischen Datenpunkte für das Diagramm in Tabellenform an. Um das Freigeben und Bearbeiten von Daten zu vereinfachen, können Sie die verarbeiteten Daten im CSV-Format aus diesem Dialogfeld herunterladen. Wählen Sie **[!UICONTROL CSV herunterladen]**, um Ihre Daten herunterzuladen.

>[!NOTE]
>
>Der CSV-Download ist auf die ersten 500 Datensätze beschränkt.

![Ein Dialogfeld mit einer Vorschau Ihrer Einblicke und den tabellarischen Ergebnissen Ihrer SQL, die die Einblicke generiert haben.](../images/sql-insights-query-pro-mode/view-more-download-csv.png)

## Nach Spalte sortieren {#sort-column}

Beim Anzeigen von tabellarischen Ergebnissen können Sie die Sortierfunktion verwenden, um in auf- oder absteigender Reihenfolge nach Spalten zu sortieren. Wählen Sie im benutzerdefinierten Dashboard die Auslassungszeichen (`...`) einer beliebigen Tabelle aus, um auf die Option [!UICONTROL Mehr anzeigen] zuzugreifen.

![Ein benutzerdefiniertes Dashboard mit einem Dropdown-Menü mit den Auslassungspunkten einer Tabelle und der hervorgehobenen Option „Mehr anzeigen“.](../images/sql-insights-query-pro-mode/advanced-ellipses-dropdown.png)

Sie können Spalten sortieren, indem Sie das Dropdown-Menü neben dem Spaltennamen auswählen und dann auf **[!UICONTROL Aufsteigend sortieren]** oder **[!UICONTROL Absteigend sortieren]** klicken.

>[!NOTE]
>
>Die [!UICONTROL Aufsteigend sortieren] und [!UICONTROL Absteigend sortieren] werden nur für Spalten angezeigt, die mit [Sortierfunktion](./overview.md#advanced-attributes) konfiguriert wurden.

![Ein Dropdown-Menü mit Tabellenspalten, in dem die Optionen Aufsteigend sortieren und Absteigend sortieren hervorgehoben sind.](../images/sql-insights-query-pro-mode/advanced-sort-dropdown.png)

## Spaltengröße ändern {#resize-column}

Sie können die Größe von Spalten in tabellarischen Ergebnissen ändern, um die Lesbarkeit der Daten zu verbessern. Wählen Sie im benutzerdefinierten Dashboard die Auslassungszeichen (`...`) für Ihre Tabelle aus, um auf die Option [!UICONTROL Mehr anzeigen] zuzugreifen. Verwenden Sie das Dropdown-Menü neben dem Spaltennamen, um die Größe zu ändern, und wählen Sie dann **[!UICONTROL Spaltengröße ändern]**.

![Ein Dropdown-Menü für Tabellenspalten mit hervorgehobener Option „Spaltengröße ändern“](../images/sql-insights-query-pro-mode/advanced-resize-dropdown.png)

Wählen Sie den Schieberegler aus und ziehen Sie nach links oder rechts, um die Spaltengröße nach Bedarf anzupassen.

![Eine Tabelle, in der die Leiste zur Spaltengröße hervorgehoben ist.](../images/sql-insights-query-pro-mode/advanced-resize-column.png)

## Tabellen-Paginierung {#table-pagination}

Die Tabellen werden automatisch mit der Funktion [!UICONTROL Mehr anzeigen] paginiert, sodass Sie Ihre SQL-Abfragen nicht mehr manuell ändern müssen. Mit dieser Funktion wird sichergestellt, dass Ihre Daten in einem besser verwaltbaren Format angezeigt werden, was die Navigation durch große Datensätze erleichtert.

Pro Seite können bis zu 500 Datensätze angezeigt werden. Um durch die Datensätze zu navigieren, verwenden Sie die ]****[!UICONTROL >am unteren Rand der Seite.

![Tabellenergebnisse mit hervorgehobenen Ergebnissen und hervorgehobener Paginierung.](../images/sql-insights-query-pro-mode/advanced-table-pagination.png)

## Nächste Schritte

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie die tabellarischen Ergebnisse der SQL-Analyse Ihres benutzerdefinierten Diagramms anzeigen und die Daten als CSV-Datei herunterladen können. Im Dokument SQL anzeigen erfahren Sie, wie Sie [SQL hinter Ihren benutzerdefinierten Einblicken anzeigen](./view-sql.md).

Außerdem erfahren Sie mit dem Handbuch [ Design-Modus , wie Sie Diagramme aus vorhandenen Datenmodellen in der Adobe Experience Platform-Benutzeroberfläche ](../standard-dashboards.md).
