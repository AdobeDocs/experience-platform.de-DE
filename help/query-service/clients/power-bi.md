---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Verbindung mit Power BI
topic: connect
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 1%

---


# Verbindung mit [!DNL Power BI] (PC)

PC-Benutzer können die Installation [!DNL Power BI] unter [https://powerbi.microsoft.com/en-us/desktop/](https://powerbi.microsoft.com/en-us/desktop/)durchführen.

## Einrichten [!DNL Power BI]

Nach der [!DNL Power BI] Installation müssen Sie die erforderlichen Komponenten zur Unterstützung des PostgreSQL-Connectors einrichten. Führen Sie folgende Schritte aus:

- Suchen und installieren `npgsql`, ein .NET-Treiberpaket für PostgreSQL, das die offizielle Verbindung von PowerBI ermöglicht.

- Wählen Sie Version 4.0.10 aus (neuere Versionen führen derzeit zu einem Fehler).

- Wählen Sie im Bildschirm &quot;Benutzerdefinierte Einstellungen&quot;unter &quot;Npgsql GAC Installation&quot;die Option **[!UICONTROL Wird auf lokaler Festplatte]** installiert. Wenn Sie die GAC nicht installieren, schlägt Power BI später fehl.

- Starten Sie Windows neu.

- Suchen Sie die Testversion [!DNL PowerBI] für den Desktop.

## Verbinden [!DNL Power BI] mit [!DNL Query Service]

Nachdem Sie diese vorbereitenden Schritte durchgeführt haben, können Sie eine Verbindung [!DNL Power BI] zu [!DNL Query Service]folgenden Elementen herstellen:

- Öffnen [!DNL Power BI].

- Klicken Sie im oberen Menüband auf Daten **[!UICONTROL abrufen]** .

- Wählen Sie **[!UICONTROL PostgreSQL-Datenbank]** und klicken Sie dann auf **[!UICONTROL Verbinden]**.

- Geben Sie Werte für Server und Datenbank ein. **[!UICONTROL Server]** ist der Host, der unter den Verbindungsdetails gefunden wird. Bei der Produktion fügen Sie Anschluss `:80` am Ende der Host-Zeichenfolge hinzu. **[!UICONTROL Datenbank]** kann entweder &quot;all&quot;oder ein Dataset-Tabellenname sein. (Testen Sie einen der von CTAS abgeleiteten Datensätze.)

- Klicken Sie auf **[!UICONTROL Erweiterte Optionen]** und deaktivieren Sie dann die Option **[!UICONTROL Beziehungsspalten]** einschließen. Aktivieren Sie nicht die Option **[!UICONTROL Navigieren mit vollständiger Hierarchie]**.

- *(Optional, jedoch empfohlen, wenn &quot;all&quot;für die Datenbank deklariert wird)* Geben Sie eine SQL-Anweisung ein.

>[!NOTE]
>
>Wenn keine SQL-Anweisung bereitgestellt wird, [!DNL Power BI] werden alle Datenbanktabellen Vorschau. Für hierarchische Daten sollte eine benutzerdefinierte SQL-Anweisung verwendet werden. Wenn das Tabellenelement flach ist, funktioniert es mit oder ohne eine benutzerdefinierte SQL-Anweisung. Zusammengesetzte Typen werden noch nicht von unterstützt [!DNL Power BI] - um Primitive-Typen von zusammengesetzten Typen zu erhalten, müssen Sie SQL-Anweisungen schreiben, um sie abzuleiten.

```sql
SELECT web.webPageDetails.name AS Page_Name, 
SUM(web.webPageDetails.pageviews.value) AS Page_Views 
FROM _TABLE_ 
WHERE _ACP_YEAR=2018 AND _ACP_MONTH=11 AND _ACP_DAY=20 
GROUP BY web.webPageDetails.name 
ORDER BY SUM(web.webPageDetails.pageviews.value) DESC 
LIMIT 10
```

- Wählen Sie entweder den **[!UICONTROL DirectQuery]** - oder den **[!UICONTROL Import]** -Modus. Im **[!UICONTROL Importmodus]** werden Daten importiert [!DNL Power BI]. Im **[!UICONTROL DirectQuery]** -Modus werden alle Abfragen zur Ausführung an gesendet [!DNL Query Service] .

- Klicken Sie auf **[!UICONTROL OK]**. Jetzt [!DNL Power BI] verbindet sich mit dem [!DNL Query Service] und erzeugt eine Vorschau, wenn es keine Fehler gibt. Es ist ein bekanntes Problem beim Rendern numerischer Vorschauen aufgetreten. Fahren Sie mit dem nächsten Schritt fort.

- Klicken Sie auf **[!UICONTROL Laden]** , um den Datensatz zu laden [!DNL Power BI].
