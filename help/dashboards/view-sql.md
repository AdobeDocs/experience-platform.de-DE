---
title: Insight SQL anzeigen
description: Zeigen Sie die SQL hinter Ihrem Profil, Ihrer Zielgruppe, Ihrem Ziel und Ihren benutzerdefinierten Einblicken an und führen Sie die Abfrage bei Bedarf über den Abfrage-Editor aus.
exl-id: fd728926-c113-4593-92b1-916a02d09d41
source-git-commit: e0af1f0110ceb514a5b249c42a05bf780ea834c6
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# Insight SQL anzeigen

Verwenden Sie die Funktion &quot;[!UICONTROL SQL anzeigen]&quot;, um die SQL hinter Ihrem Profil, Ihrer Zielgruppe, Ihrem Ziel und Ihren benutzerdefinierten Einblicken anzuzeigen und die Abfrage auf Anfrage über den Abfrage-Editor auszuführen. Lassen Sie sich von der SQL von über 40 vorhandenen Einblicken inspirieren, um neue Abfragen zu erstellen, die anhand Ihrer geschäftlichen Anforderungen einzigartige Einblicke aus Platform-Daten gewinnen.

## Navigieren Sie zur Dashboard-Übersicht . {#navigate-to-overview}

Um Ihr ausgewähltes Dashboard zu öffnen, wählen Sie entweder **[!UICONTROL Profile]**, **[!UICONTROL Zielgruppen]** oder **[!UICONTROL Ziele]** aus der linken Navigation aus. Wählen Sie als Nächstes **[!UICONTROL Überblick]** aus den Registerkartenoptionen aus, wenn der Arbeitsbereich nicht automatisch angezeigt wird.

Alternativ können Sie im linken Navigationsbereich die Option **[!UICONTROL Dashboards]** auswählen, gefolgt vom Namen Ihres benutzerdefinierten Dashboards. Die Übersicht über Ihr benutzerdefiniertes Dashboard wird angezeigt.

![Die Experience Platform-Benutzeroberfläche mit den Markierungen [!UICONTROL Profile], [!UICONTROL Zielgruppen], [!UICONTROL Ziele] und [!UICONTROL Dashboards].](./images/view-sql/dashboard-navigation.png)

## SQL-Umschalter anzeigen {#toggle}

Ein Umschalter ist in der Übersicht der Profil-, Zielgruppen-, Ziel- und benutzerdefinierten Dashboards verfügbar, um die Funktion zu aktivieren oder zu deaktivieren.

>[!NOTE]
>
>Wenn Sie den Umschalter [!UICONTROL SQL anzeigen] aktivieren, können Sie globale Filter und Filter auf Widget-Ebene erst ändern, wenn Sie die Funktion deaktivieren.

![ Der Umschalter [!UICONTROL SQL anzeigen] wurde hervorgehoben.](./images/view-sql/view-sql-toggle.png)

Aktivieren Sie den Umschalter, um den Text [!UICONTROL SQL anzeigen] für jeden einzelnen Insight anzuzeigen.

![Ein Einblick mit hervorgehobenem [!UICONTROL Anzeigen von SQL] ](./images/view-sql/insight-view-sql.png).

Wählen Sie **[!UICONTROL SQL anzeigen]** aus, um ein Dialogfeld zu öffnen, das die SQL des Widgets enthält.

## SQL-Dialogfeld {#sql-dialog}

Es wird ein Dialogfeld angezeigt, das den Titel des Insight und die SQL, die ihn generiert, enthält.

>[!TIP]
>
>Sie können die gesamte SQL-Anweisung in die Zwischenablage kopieren, indem Sie das Kopiersymbol (![Kopiersymbol) auswählen.](./images/view-sql/copy-icon.png)) oben rechts im Dialogfeld.

![Ein Insight-Dialogfeld mit hervorgehobener SQL-Anweisung.](./images/view-sql/sql-dialog.png)

Wählen Sie **[!UICONTROL SQL ausführen]** aus, um den Abfrage-Editor zu öffnen, wenn die Abfrage vorausgefüllt ist.

![Ein Insight-Dialogfeld mit hervorgehobenem [!UICONTROL Run SQL]-Symbol.](./images/view-sql/run-sql.png)

## Vorhandene SQL bearbeiten {#edit-sql}

Der Abfrage-Editor wird angezeigt. Sie können jetzt die Anweisung bearbeiten und Ihre Plattformdaten so abfragen, dass sie Ihren Berichterstellungsanforderungen besser entsprechen. Speichern Sie Ihre neue Abfragevorlage mit einem geeigneten Namen.

![Der Abfrage-Editor mit Ihrem ausgewählten Insight-SQL-Eintrag.](./images/view-sql/edit-sql.png)

## Nächste Schritte

Nach der Lektüre dieses Dokuments wissen Sie jetzt, wie Sie auf die SQL-Datenbank zugreifen können, um Einblicke in die Standard-Dashboards oder in ein benutzerdefiniertes Dashboard zu erhalten. Wenn Sie dies noch nicht getan haben, sollten Sie das Dokument [Real-time Customer Data Platform Insights Data Model](./data-models/cdp-insights-data-model-b2c.md) lesen. Dieses Dokument enthält Einblicke in die Anpassung von SQL-Vorlagen für Real-Time CDP-Berichte, die auf Ihre Marketing- und KPI-Anforderungen zugeschnitten sind.
