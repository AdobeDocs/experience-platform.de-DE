---
keywords: Experience Platform;Home;beliebte Themen;Monitorkonten;Datenflüsse überwachen;Datenflüsse;Quellen
description: In diesem Lernprogramm werden Schritte zur Überwachung Ihres Datenflusses beschrieben, wobei sowohl die aggregierte Ansicht der Überwachung als auch die dienstübergreifende Überwachung verwendet werden.
solution: Experience Platform
title: Überwachen von Datenflüssen für Quellen in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
exl-id: 53fa4338-c5f8-4e1a-8576-3fe13d930846
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1644'
ht-degree: 5%

---

# Überwachen von Datenflüssen auf Quellen in der Benutzeroberfläche

In Adobe Experience Platform werden Daten aus einer Vielzahl von Quellen erfasst, innerhalb der Experience Platform analysiert und zu einer Vielzahl von Zielen aktiviert. Plattform erleichtert die Verfolgung dieses potenziell nicht-linearen Datenflusses durch Transparenz mit Datenflüssen.

Das Dashboard zur Überwachung bietet eine visuelle Darstellung der Journey eines Datenflusses. Sie können eine aggregierte Überwachungs-Ansicht verwenden und von der Quellebene zu einem Datendurchlauf und zu einem Datendurchlauf vertikal navigieren, sodass Sie die entsprechenden Metriken, die zum Erfolg oder Misserfolg eines Datenverlusts beitragen, Ansicht haben können. Sie können auch die dienstübergreifende Überwachungskapazität des überwachenden Dashboards verwenden, um die Journey eines Datenflusses von einer Quelle bis zu [!DNL Identity Service] und bis [!DNL Profile] zu überwachen.

In diesem Lernprogramm werden Schritte zur Überwachung Ihres Datenflusses beschrieben, wobei sowohl die aggregierte Ansicht der Überwachung als auch die dienstübergreifende Überwachung verwendet werden.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Datenflüsse](../home.md): Datenflüsse sind eine Darstellung von Datenaufträgen, die Daten über die Plattform verschieben. Datenflüsse werden über verschiedene Dienste konfiguriert und unterstützen Sie dabei, Daten von Quellschnittstellen zu Zielgruppen-Datensätzen, zu [!DNL Identity] und [!DNL Profile] und zu [!DNL Destinations] zu verschieben.
   * [Dataflow wird ausgeführt](../../sources/notifications.md): Dataflow-Ausführung sind die wiederkehrenden geplanten Aufträge, die auf der Frequenzkonfiguration der ausgewählten Datenflüsse basieren.
* [Quellen](../../sources/home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Plattformdiensten zu strukturieren, zu kennzeichnen und zu verbessern.
* [Identity Service](../../identity-service/home.md): Sorgt für eine bessere Darstellung einzelner Kunden und deren Verhalten, indem Identitäten zwischen Geräten und Systemen überbrückt werden.
* [Echtzeit-Kundenprofil](../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
* [Sandboxes](../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Anwendungen für digitale Erlebnisse entwickeln und weiterentwickeln können.

## Aggregierte Ansicht der Überwachung

Wählen Sie in der [Platform UI](https://platform.adobe.com) in der linken Navigation **[!UICONTROL Monitoring]** aus, um auf das [!UICONTROL Monitoring]-Dashboard zuzugreifen. Das [!UICONTROL Monitoring]-Dashboard enthält Metriken und Informationen zu allen Datenströmen, einschließlich Einblicke in den Datenverkehr von einer Quelle zu [!DNL Identity Service] und zu [!DNL Profile].

Im Mittelpunkt des Dashboards steht das Bedienfeld [!UICONTROL Quellaufnahme], das Metriken und Diagramme enthält, die Daten zu erfassten Datensätzen und fehlgeschlagenen Datensätzen anzeigen.

![monitoring-Dashboard](../assets/ui/monitor-sources/monitoring-dashboard.png)

Standardmäßig enthalten die angezeigten Daten die Erfassungsraten der letzten 24 Stunden. Wählen Sie **[!UICONTROL Letzte 24 Stunden]** aus, um den Zeitrahmen der angezeigten Datensätze anzupassen.

![change-date](../assets/ui/monitor-sources/change-date.png)

Es wird ein Popup-Fenster mit Optionen für alternative Erfassungszeitrahmen angezeigt. Wählen Sie **[!UICONTROL Letzte 30 Tage]** und dann **[!UICONTROL Anwenden]**

![Zeit-Frame anpassen](../assets/ui/monitor-sources/adjust-timeframe.png)

Die Diagramme sind standardmäßig aktiviert und Sie können sie deaktivieren, um die Liste der folgenden Quellen zu erweitern. Aktivieren Sie den Umschalter **[!UICONTROL Metriken und Diagramme]**, um die Diagramme zu deaktivieren.

![Metriken und Diagramme](../assets/ui/monitor-sources/metrics-graphs.png)

| Quellaufnahme | Beschreibung |
| ---------------- | ----------- |
| [!UICONTROL Aufgenommene Datensätze  ] | Die Gesamtzahl der erfassten Datensätze. |
| [!UICONTROL Datensätze fehlgeschlagen] | Die Gesamtzahl der Datensätze, die aufgrund von Fehlern in den Daten nicht erfasst wurden. |
| [!UICONTROL Insgesamt fehlgeschlagene Datenflüsse] | Die Gesamtanzahl der Datenflüsse mit dem Status `failed`. |

In der Liste zur Quellerfassung werden alle Quellen angezeigt, die mindestens ein vorhandenes Konto enthalten. Die Liste enthält außerdem Informationen zur Erfassungsrate der einzelnen Quellen, zur Anzahl der fehlgeschlagenen Datensätze und zur Gesamtzahl der fehlgeschlagenen Datenflüsse, die auf dem von Ihnen angewendeten Zeitraum basieren.

![source-Erfassung](../assets/ui/monitor-sources/source-ingestion.png)

Um eine Sortierung durch die Liste der Quellen durchzuführen, wählen Sie **[!UICONTROL Meine Quellen]** und dann Ihre gewünschte Kategorie aus dem Dropdown-Menü. Um sich beispielsweise auf Cloud-Datenspeicherung zu konzentrieren, wählen Sie **[!UICONTROL Cloud-Datenspeicherung]**

![Sortieren nach Kategorie](../assets/ui/monitor-sources/sort-by-category.png)

Um alle vorhandenen Datenflüsse über alle Quellen hinweg Ansicht, wählen Sie **[!UICONTROL Datenflüsse]**.

![Ansicht-all-dataflows](../assets/ui/monitor-sources/view-all-dataflows.png)

Alternativ können Sie eine Quelle in die Suchleiste eingeben, um eine einzelne Quelle zu isolieren. Nachdem Sie die Quelle identifiziert haben, wählen Sie das Filtersymbol ![filter](../assets/ui/monitor-sources/filter.png), um eine Liste der aktiven Datenflüsse anzuzeigen.

![search](../assets/ui/monitor-sources/search.png)

Eine Liste von Datenflüssen wird angezeigt. Um die Liste einzugrenzen und sich auf Datenflüsse mit Fehlern zu konzentrieren, wählen Sie **[!UICONTROL Nur Fehler anzeigen]**.

![show-failure-only](../assets/ui/monitor-sources/show-failures-only.png)

Suchen Sie den zu überwachenden Datenfluss und klicken Sie dann auf das Filtersymbol ![filter](../assets/ui/monitor-sources/filter.png), um weitere Informationen zum Ausführungsstatus anzuzeigen.

![dataflow](../assets/ui/monitor-sources/dataflow.png)

Auf der Seite &quot;Datenfluss&quot;werden Informationen zum Ausführungsdatum des Datenflusses, zur Datengröße, zum Beginn sowie zur Verarbeitungsdauer angezeigt. Wählen Sie das Filtersymbol ![filter](../assets/ui/monitor-sources/filter.png) neben der Beginn-Laufzeit des Datenflusses aus, um die Details des Datenflusses anzuzeigen.

![dataflow-run-Beginn](../assets/ui/monitor-sources/dataflow-run-start.png)

Auf der Seite [!UICONTROL Datenflussinformationen] werden Informationen zu den Metadaten des Datenflusses, dem Teilnahmestatus und der Fehlerzusammenfassung angezeigt. Die Fehlerzusammenfassung enthält den spezifischen Fehler der obersten Ebene, der anzeigt, bei welchem Schritt der Erfassungsvorgang einen Fehler auftrat.

Blättern Sie nach unten, um genauere Informationen zum aufgetretenen Fehler anzuzeigen.

![dataflow-run-details](../assets/ui/monitor-sources/dataflow-run-details.png)

Das Bedienfeld [!UICONTROL Datenfeldausführungsfehler] zeigt den spezifischen Fehler- und Fehlercode an, der zum Erfassungsfehler des Datenflusses führte. In diesem Szenario ist ein Fehler bei der Zuordnerkonvertierung aufgetreten, der dazu führte, dass 24 Datensätze fehlschlugen.

Wählen Sie **[!UICONTROL Dateien]**, um weitere Informationen anzuzeigen.

![dataflow-run-errors](../assets/ui/monitor-sources/dataflow-run-errors.png)

Das Bedienfeld [!UICONTROL Dateien] enthält Informationen zum Namen und Pfad der Datei.

Um den Fehler detaillierter darzustellen, wählen Sie **[!UICONTROL Fehlerdiagnose bei Vorschau]**.

![files](../assets/ui/monitor-sources/files.png)

Das Fenster [!UICONTROL Fehlerdiagnose wird angezeigt. Es wird eine Vorschau von bis zu 100 Vorschauen im Datenpfad angezeigt. ] Sie können **[!UICONTROL Download]** auswählen, um einen Befehl &quot;curl&quot;abzurufen, mit dem Sie dann die Fehlerdiagnose herunterladen können.

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Schließen]**

![error-diagnostics](../assets/ui/monitor-sources/error-diagnostics.png)

Sie können das Breadcrumb-System oben in der Kopfzeile verwenden, um zurück zum [!UICONTROL Monitoring]-Dashboard zu navigieren. Wählen Sie **[!UICONTROL Beginn ausführen: 14.02.2021, 21.47 PM]**, um zur vorherigen Seite zurückzukehren, und wählen Sie **[!UICONTROL Datennachlauf: Demo zur Integration von Treuedaten - Fehlgeschlagen, um zur Seite &quot;Datenflüsse&quot;zurückzukehren.]**

![Breadcrumbs](../assets/ui/monitor-sources/breadcrumbs.png)

## Dienstübergreifende Überwachung

Der obere Teil des Dashboards enthält eine Darstellung des Erfassungsflusses von der Quell-Ebene bis zu [!DNL Identity Service] und bis [!DNL Profile]. Jede Zelle enthält eine Punktmarke, die auf das Vorhandensein von Fehlern hinweist, die in dieser Phase der Erfassung aufgetreten sind. Ein grüner Punkt bedeutet eine fehlerfreie Erfassung, während ein roter Punkt bedeutet, dass in dieser bestimmten Phase der Erfassung ein Fehler aufgetreten ist.

![dienststellenübergreifende Überwachung](../assets/ui/monitor-sources/cross-service-monitoring.png)

Suchen Sie auf der Seite &quot;Datenflüsse&quot;nach einem erfolgreichen Datendurchlauf und wählen Sie das Filtersymbol ![filter](../assets/ui/monitor-sources/filter.png) daneben, um die Daten des Datenflusses anzuzeigen.

![dataflow-success](../assets/ui/monitor-sources/dataflow-success.png)

Die Seite [!UICONTROL Quellaufnahme] enthält Informationen, die die erfolgreiche Erfassung Ihres Datenflusses bestätigen. Von hier aus können Sie Beginn zur Überwachung der Journey Ihres Datenflusses von der Quell-Ebene bis zu [!DNL Identity Service] und dann bis [!DNL Profile].

Wählen Sie **[!UICONTROL Identities]** aus, um die Erfassung in der Phase [!UICONTROL Identities] anzuzeigen.

![sources](../assets/ui/monitor-sources/sources.png)

### [!DNL Identity] Metriken

Die Seite [!UICONTROL Identitätsverarbeitung] enthält Informationen zu Datensätzen, die in [!DNL Identity Service] aufgenommen wurden, einschließlich der Anzahl der hinzugefügten Identitäten, der erstellten Diagramme und der aktualisierten Diagramme.

Wählen Sie das Filtersymbol ![filter](../assets/ui/monitor-sources/filter.png) neben der Beginn-Laufzeit des Datenflusses aus, um weitere Informationen zum [!DNL Identity]-Datenfluss anzuzeigen.

![Identitäten](../assets/ui/monitor-sources/identities.png)

| Identitätsmetriken | Beschreibung |
| ---------------- | ----------- |
| [!UICONTROL Aufgenommene Aufzeichnungen] | Die Anzahl der von [!DNL Data Lake] empfangenen Datensätze. |
| [!UICONTROL Datensätze fehlgeschlagen] | Die Anzahl der Datensätze, die aufgrund von Datenfehlern nicht in die Plattform aufgenommen wurden. |
| [!UICONTROL Übersprungene Datensätze] | Die Anzahl der Datensätze, die erfasst wurden, jedoch nicht in [!DNL Identity Service], da in der Datensatzzeile nur ein Bezeichner vorhanden war. |
| [!UICONTROL Aufgenommene Datensätze] | Die Anzahl der in [!DNL Identity Service] erfassten Datensätze. |
| [!UICONTROL Datensätze insgesamt] | Die Gesamtanzahl aller Datensätze, einschließlich fehlgeschlagener Datensätze, übersprungener Datensätze, [!DNL Identities] hinzugefügter Datensätze und duplizierter Datensätze. |
| [!UICONTROL Hinzugefügte Identitäten] | Die Anzahl der netto-neuen Identifikatoren, die zu [!DNL Identity Service] hinzugefügt werden. |
| [!UICONTROL Erstellte Diagramme] | Die Anzahl der neuen Netto-Identitätsdiagramme, die in [!DNL Identity Service] erstellt wurden. |
| [!UICONTROL Diagramme aktualisiert] | Die Anzahl vorhandener Identitätsdiagramme, die mit neuen Kanten aktualisiert wurden. |
| [!UICONTROL Fehlgeschlagene Ausführung des Datenflusses] | Die Anzahl der ausgeführten Datenflüsse, die fehlgeschlagen sind. |
| [!UICONTROL Verarbeitungszeit] | Der Zeitstempel vom Beginn der Erfassung bis zum Abschluss. |
| [!UICONTROL Status] | Definiert den Gesamtstatus eines Datenflusses. Mögliche Statuswerte sind: <ul><li>`Success`: Gibt an, dass ein Datendurchlauf aktiv ist und Daten gemäß dem bereitgestellten Zeitplan erfasst.</li><li>`Failed`: Gibt an, dass die Aktivierung eines Datenflusses aufgrund von Fehlern unterbrochen wurde. </li><li>`Processing`: Gibt an, dass der Datenflug noch nicht aktiv ist. Dieser Status tritt oft unmittelbar nach der Erstellung eines neuen Datenflusses auf.</li></ul> |

Auf der Seite [!UICONTROL DataFlow-Ausführungsdetails] werden weitere Informationen zu Ihrem [!DNL Identity]-Datenflug-Ausführen angezeigt, einschließlich der IMS-Organisations-ID und der DataFlow-run-ID. Auf dieser Seite werden auch der entsprechende Fehlercode und die Fehlermeldung angezeigt, die von [!DNL Identity Service] bereitgestellt werden, sollte es bei der Erfassung zu Fehlern kommen.

Wählen Sie **[!UICONTROL Beginn ausführen: 14.02.2021, 21.47 Uhr]**, um zur vorherigen Seite zurückzukehren.

![identities-dataflow-run](../assets/ui/monitor-sources/identities-dataflow-run.png)

Wählen Sie auf der Seite [!UICONTROL Identitätsverarbeitung] **[!UICONTROL Profil]** aus, um den Status der Datensatzerfassung im Schritt [!UICONTROL Profil] anzuzeigen.

![select-Profile](../assets/ui/monitor-sources/select-profiles.png)

### [!DNL Profile] Metriken

Die Seite [!UICONTROL Verarbeitung von Profilen] enthält Informationen zu Datensätzen, die in [!DNL Profile] aufgenommen wurden, einschließlich der Anzahl der erstellten Profil-Fragmente, der aktualisierten Profil-Fragmente und der Gesamtzahl der Profil-Fragmente.

Wählen Sie das Filtersymbol ![filter](../assets/ui/monitor-sources/filter.png) neben der Beginn-Laufzeit des Datenflusses aus, um weitere Informationen zum [!DNL Profile]-Datenfluss anzuzeigen.

![Profile](../assets/ui/monitor-sources/profiles.png)

| Profil-Metriken | Beschreibung |
| --------------- | ----------- |
| [!UICONTROL Aufgenommene Aufzeichnungen] | Die Anzahl der von [!DNL Data Lake] empfangenen Datensätze. |
| [!UICONTROL Datensätze fehlgeschlagen  ] | Die Anzahl der Datensätze, die aufgrund von Fehlern erfasst wurden, jedoch nicht in [!DNL Profile]. |
| [!UICONTROL Profil-Fragmente hinzugefügt] | Die Anzahl der neuen Netto-Fragmente [!DNL Profile] hinzugefügt. |
| [!UICONTROL Profil-Fragmente aktualisiert] | Die Anzahl der vorhandenen [!DNL Profile]-Fragmente wurde aktualisiert |
| [!UICONTROL Profil-Fragmente insgesamt] | Die Gesamtzahl der in [!DNL Profile] geschriebenen Datensätze, einschließlich aller vorhandenen [!DNL Profile]-Fragmente aktualisiert und neuer [!DNL Profile]-Fragmente erstellt. |
| [!UICONTROL Fehlgeschlagene Ausführung des Datenflusses] | Die Anzahl der ausgeführten Datenflüsse, die fehlgeschlagen sind. |
| [!UICONTROL Verarbeitungszeit] | Der Zeitstempel vom Beginn der Erfassung bis zum Abschluss. |
| [!UICONTROL Status] | Definiert den Gesamtstatus eines Datenflusses. Mögliche Statuswerte sind: <ul><li>`Success`: Gibt an, dass ein Datendurchlauf aktiv ist und Daten gemäß dem bereitgestellten Zeitplan erfasst.</li><li>`Failed`: Gibt an, dass die Aktivierung eines Datenflusses aufgrund von Fehlern unterbrochen wurde. </li><li>`Processing`: Gibt an, dass der Datenflug noch nicht aktiv ist. Dieser Status tritt oft unmittelbar nach der Erstellung eines neuen Datenflusses auf.</li></ul> |

Auf der Seite [!UICONTROL DataFlow-Ausführungsdetails] werden weitere Informationen zu Ihrem [!DNL Profile]-Datenflug-Ausführen angezeigt, einschließlich der IMS-Organisations-ID und der DataFlow-run-ID. Auf dieser Seite werden auch der entsprechende Fehlercode und die Fehlermeldung angezeigt, die von [!DNL Profile] bereitgestellt werden, sollte es bei der Erfassung zu Fehlern kommen.

![Profils-dataflow-run](../assets/ui/monitor-sources/profiles-dataflow-run.png)

## Nächste Schritte

Durch Befolgen dieses Lernprogramms haben Sie den Erfassungsdataflow von der Quell-Ebene bis zu [!DNL Identity Service] und bis [!DNL Profile] mithilfe des Dashboards **[!UICONTROL Monitoring]** erfolgreich überwacht. Sie haben außerdem erfolgreich Fehler identifiziert, die zum Fehlschlagen von Datenflüssen während des Erfassungsvorgangs beitrugen. Weitere Informationen finden Sie in den folgenden Dokumenten:

* [Übersicht über das Echtzeit-Kundenprofil](../../profile/home.md)
* [Übersicht über den Data Science Workspace](../../data-science-workspace/home.md)
