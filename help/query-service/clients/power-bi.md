---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Verbindung mit Power BI
topic: connect
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---


# Verbindung mit Power BI (PC)

PC-Benutzer können Power BI unter [https://powerbi.microsoft.com/en-us/desktop/](https://powerbi.microsoft.com/en-us/desktop/)installieren.

## Einrichten der Netzanzeige

Nachdem Sie Power BI installiert haben, müssen Sie die erforderlichen Komponenten zur Unterstützung des PostgreSQL-Connectors einrichten. Führen Sie folgende Schritte aus:

- Suchen und installieren `npgsql`, ein .NET-Treiberpaket für PostgreSQL, das die offizielle Verbindung von PowerBI ermöglicht.

- Wählen Sie Version 4.0.10 aus (neuere Versionen führen derzeit zu einem Fehler).

- Wählen Sie im Bildschirm &quot;Benutzerdefinierte Einstellungen&quot;unter &quot;Npgsql GAC Installation&quot;die Option **Wird auf lokaler Festplatte** installiert. Wenn Sie die GAC nicht installieren, schlägt Power BI später fehl.

- Starten Sie Windows neu.

- Finden Sie die PowerBI Desktop Testversion.

## Schließen Sie das Power BI an den Abfrage-Dienst an

Nachdem Sie diese vorbereitenden Schritte durchgeführt haben, können Sie Power BI mit dem Abfrage Service verbinden:

- Öffnen Sie Power BI.

- Klicken Sie im oberen Menüband auf Daten **abrufen** .

- Wählen Sie **PostgreSQL-Datenbank** und klicken Sie dann auf **Verbinden**.

- Geben Sie Werte für Server und Datenbank ein. **Server** ist der Host, der unter den Verbindungsdetails gefunden wird. Bei der Produktion fügen Sie Anschluss `:80` am Ende der Host-Zeichenfolge hinzu. **Datenbank** kann entweder &quot;all&quot;oder ein Dataset-Tabellenname sein. (Testen Sie einen der von CTAS abgeleiteten Datensätze.)

- Klicken Sie auf **Erweiterte Optionen** und deaktivieren Sie dann die Option **Beziehungsspalten** einschließen. Aktivieren Sie nicht die Option **Navigieren mit vollständiger Hierarchie**.

- *(Optional, jedoch empfohlen, wenn &quot;all&quot;für die Datenbank deklariert wird)* Geben Sie eine SQL-Anweisung ein.

>[!NOTE]
>
>Wenn keine SQL-Anweisung bereitgestellt wird, werden alle Datenbanktabellen von Power BI Vorschau. Für hierarchische Daten sollte eine benutzerdefinierte SQL-Anweisung verwendet werden. Wenn das Tabellenelement flach ist, funktioniert es mit oder ohne eine benutzerdefinierte SQL-Anweisung. Zusammengesetzte Typen werden noch nicht von Power BI unterstützt - um Primitive-Typen von zusammengesetzten Typen zu erhalten, müssen Sie SQL-Anweisungen schreiben, um sie abzuleiten.

```sql
SELECT web.webPageDetails.name AS Page_Name, 
SUM(web.webPageDetails.pageviews.value) AS Page_Views 
FROM _TABLE_ 
WHERE _ACP_YEAR=2018 AND _ACP_MONTH=11 AND _ACP_DAY=20 
GROUP BY web.webPageDetails.name 
ORDER BY SUM(web.webPageDetails.pageviews.value) DESC 
LIMIT 10
```

- Wählen Sie entweder den **DirectQuery** - oder den **Import** -Modus. Im **Import** -Modus werden die Daten im Power BI importiert. Im **DirectQuery** -Modus werden alle Abfragen zur Ausführung an den Abfrage Service gesendet.

- Klicken Sie auf **OK**. Jetzt stellt Power BI eine Verbindung zum Abfrage Service her und erzeugt eine Vorschau, wenn keine Fehler vorliegen. Es ist ein bekanntes Problem beim Rendern numerischer Vorschauen aufgetreten. Fahren Sie mit dem nächsten Schritt fort.

- Klicken Sie auf **Laden** , um den Datensatz in Power BI zu laden.
