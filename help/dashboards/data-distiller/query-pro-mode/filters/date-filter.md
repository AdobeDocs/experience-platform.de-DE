---
title: Erstellen eines Datumsfilters
description: Erfahren Sie, wie Sie Ihre benutzerdefinierten Einblicke nach Datum filtern können.
exl-id: fa05d651-ea43-41f0-9b7d-f19c4a9ac256
source-git-commit: 0970fd8fbea86115d92dc78cdba753da69cc2ee6
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 0%

---

# Datumsfilter erstellen {#create-date-filter}

Um Ihre Einblicke nach Datum zu filtern, müssen Sie Ihren SQL-Abfragen Parameter hinzufügen, die Datumsbeschränkungen akzeptieren können. Dies erfolgt im Rahmen des Workflows für die Erstellung von Insight-Abfragen für den Pro-Modus. Informationen zum Einstieg in SQL für Ihre Einblicke finden Sie in der Dokumentation zu [query pro mode](#query-pro-mode) .

Mithilfe von Abfrageparametern können Sie mit dynamischen Daten arbeiten, da diese als Platzhalter für die Werte fungieren, die Sie zur Ausführungszeit hinzufügen. Diese Platzhalterwerte können über die Benutzeroberfläche aktualisiert werden und es weniger technischen Benutzern ermöglichen, die Einblicke anhand von Datumsbereichen zu aktualisieren.

Wenn Sie mit Abfrageparametern nicht vertraut sind, finden Sie in der Dokumentation [Anleitungen zur Implementierung parametrisierter Abfragen](../../../../query-service/ui/parameterized-queries.md).

## Datumsfilter auf Ihr Dashboard anwenden {#apply-date-filter}

Um einen Datumsfilter anzuwenden, wählen Sie **[!UICONTROL Filter hinzufügen]** und dann **[!UICONTROL Datumsfilter]** aus dem Dropdown-Menü Ihrer Dashboard-Ansicht.

![Ein benutzerdefiniertes Dashboard mit Filter hinzufügen und seinem Dropdown-Menü hervorgehoben.](../../../images/query-pro-mode/add-filter.png)

## SQL bearbeiten, um Datumsabfrageparameter einzuschließen {#include-date-parameters}

Stellen Sie als Nächstes sicher, dass Ihre SQL Abfrageparameter enthält, um einen Datumsbereich zuzulassen. Wenn Sie noch keine Abfrageparameter in Ihre SQL integriert haben, bearbeiten Sie Ihre Einblicke, um diese Parameter einzuschließen. Anweisungen zum Bearbeiten eines Insight finden Sie in der Dokumentation](../overview.md#edit) .[

>[!TIP]
>
>Es wird empfohlen, Ihrer SQL-Anweisung in allen Diagrammen, für die Sie Datumsfilter aktivieren möchten, die Parameter `$START_DATE` und `$END_DATE` hinzuzufügen.

>[!NOTE]
>
>Datumsfilter unterstützen keine Zeitbeschränkungen. Der Filter gilt nur für Datumsbereiche. Wenn Sie also innerhalb eines Zeitraums von 24 Stunden mehrere Berichte haben, können Sie nicht zwischen verschiedenen Stunden innerhalb eines Tages unterscheiden. Aus diesem Grund wird empfohlen, die Zeitkomponente als Datum zu verwenden.

Wenn das zu analysierende Datenmodell bzw. die Tabellen eine Zeitkomponente aufweisen, können Sie Ihre Daten nach Datum gruppieren und dann diese Datumsfilter anwenden.

Die folgende SQL-Beispielanweisung zeigt, wie die Parameter `$START_DATE` und `$END_DATE` integriert werden, und verwendet `cast`, um die Zeitkomponente als Datum festzulegen.

```sql
SELECT Sum(personalization_consent_count) AS Personalization,
       Sum(datacollection_consent_count)  AS Datacollection,
       Sum(datasharing_consent_count)     AS Datasharing
FROM   fact_daily_consent_aggregates f
       INNER JOIN dim_consent_valued
               ON f.consent_value_id = d.consent_value_id
WHERE  f.date BETWEEN Upper(Coalesce(Cast('$START_DATE' AS date), '')) AND Upper
                      (
                             Coalesce(Cast('$END_DATE' AS date), ''))
       AND ( ( Upper(Coalesce($consent_value_filter, '')) IN ( '', 'NULL' ) )
              OR ( f.consent_value_id IN ( $consent_value_filter ) ) )
LIMIT  0; 
```

Im folgenden Screenshot werden die in der SQL-Anweisung enthaltenen Datumsbeschränkungen und die Schlüsselwertpaare der Abfrageparameter hervorgehoben.

>[!NOTE]
>
>Beim Erstellen Ihrer Anweisung im Abfragepro-Modus müssen Sie Beispielwerte für jeden Parameter angeben, um die SQL-Anweisung auszuführen und das Diagramm zu erstellen. Die Beispielwerte, die Sie beim Erstellen Ihrer Anweisung angeben, werden durch die tatsächlichen Werte ersetzt, die Sie zur Laufzeit für den Filter Datum (oder global) auswählen.

![Das Dialogfeld [!UICONTROL SQL eingeben] mit den in der SQL hervorgehobenen Datumsparametern.](../../../images/sql-insights/sql-date-parameters.png)

## Datumsparameter in jedem Insight aktivieren {#enable-date-parameters}

Nachdem Sie die entsprechenden Parameter in die SQL Ihrer Einblicke eingefügt haben, sind die Variablen `Start_date` und `End_date` jetzt als Umschalter im Widget Composer verfügbar. Informationen zum Bearbeiten eines Insight finden Sie im Abschnitt [Abfrage pro Modus Widget population ](#populate-widget) .

Wählen Sie im Widget Composer Umschalter aus, um die Parameter `Start_date` und `End_date` zu aktivieren.

![Der Widget-Composer mit den Umschaltern Start_Datum und Ende_Datum ist hervorgehoben.](../../../images/sql-insights/widget-composer-date-filter-toggles.png)

Wählen Sie anschließend die entsprechenden Abfrageparameter aus den Dropdown-Menüs aus.

![Der Widget Composer mit dem Dropdown-Menü Start_Datum ist hervorgehoben.](../../../images/sql-insights/widget-composer-date-filter-dropdown.png)

Wählen Sie abschließend **[!UICONTROL Speichern und schließen]** aus, um zu Ihrem Dashboard zurückzukehren. Datumsfilter sind nun für alle Einblicke mit Start- und Enddatumsparametern aktiviert.

## Datumsfilter verwenden

Um einen benutzerdefinierten Datumsfilter zu verwenden, wählen Sie das Kalendersymbol aus und wählen Sie einen Start und ein Ende in der Kalenderansicht aus.

>[!IMPORTANT]
>
>Wenn Sie einfach einen Datumsfilter hinzufügen, ändert sich die Grafik nicht. Sie müssen jede Ihrer Einblicke bearbeiten, um Ihr ausgewähltes Start- und Enddatum einzubeziehen.

![Ein benutzerdefiniertes Dashboard mit hervorgehobenem Datumsfilterkalender.](../../../images/query-pro-mode/date-filter.png)

Nachdem Sie einen Datumsbereich aus Ihrem Dashboard ausgewählt haben, sehen Einblicke mit Datumsparametern in ihrer SQL die Datumsfilteroptionen im Widget Composer.

>[!NOTE]
>
>Wenn Sie einen Datumsbereich in Ihrem Dashboard auswählen, werden die Umschalter für Datumsfilter im Rahmen des Arbeitsablaufs zur Insight-Erstellung angezeigt.

## Datumsfilter löschen {#delete-date-filter}

Um den Datumsfilter zu entfernen, wählen Sie das Symbol Filter löschen (![Symbol Filter löschen.](/help/images/icons/filter-delete.png)).

![Ein benutzerdefiniertes Dashboard mit hervorgehobenem Symbol zum Löschen des Filters.](../../../images/query-pro-mode/delete-date-filter.png)
