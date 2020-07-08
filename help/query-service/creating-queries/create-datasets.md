---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Generieren von Datensätzen aus Abfragen-Ergebnissen
topic: queries
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---


# Generieren von Datensätzen aus Abfragen-Ergebnissen

Die wahre Stärke des Abfrage Service wird deutlich, wenn Abfragen zum Generieren von Datensätzen im Datensee verwendet werden, die als Eingabe in mehr Abfragen oder in anderen Diensten wie Data Science Workspace, Real-time Customer Profil oder Analysis Workspace verwendet werden sollen.

Der Abfrage-Dienst ermöglicht die Erstellung von Datensätzen über die Benutzeroberfläche. Führen Sie folgende Schritte aus:

1. Schreiben Sie Ihre Abfrage mit einem angeschlossenen Client und überprüfen Sie die Ausgabe.
2. Melden Sie sich bei der Benutzeroberfläche der Platform an und gehen Sie zu Abfragen.
3. Finden Sie Ihre Abfrage in der Liste und bewegen Sie den Mauszeiger über die Zeile.
4. Klicken Sie auf **Datensatz erstellen**. ![Bild](../images/queries/create-datasets/click-create-dataset.png)
5. Geben Sie einen Dataset-Namen ein, dem Ihre LDAP-ID vorangestellt wird (muss nicht eindeutig oder SQL-sicher sein). das System erzeugt einen &quot;Tabellennamen&quot; basierend auf dem hier angegebenen Namen).
6. Geben Sie eine Datensatzbeschreibung ein und klicken Sie auf Abfrage **ausführen**.![Bild](../images/queries/create-datasets/run-query.png)
7. Sehen Sie sich die Abfrage an und gehen Sie dann zur Seite &quot;Liste des Datensatzes&quot;, um den soeben erstellten Datensatz anzuzeigen.

Nachdem ein Datensatz erstellt wurde, kann er wie jeder andere Datensatz im Datensee aufgerufen und für eine Vielzahl von Anwendungsfällen verwendet werden.

>[!NOTE]
>
>In einer Live-Implementierung müssen Sie nach der Erstellung des Datensatzes die Datenverwaltungs-Beschriftungen anwenden.

## Erstellen von Datensätzen mit einem vordefinierten Experience Data Model-Schema

Um einen Datensatz mit einem vordefinierten XDM-Schema (Experience Data Model) zu erstellen, müssen Sie die SQL-Syntax verwenden. Weitere Informationen zur Syntax finden Sie im [SQL-Syntaxleitfaden](../sql/syntax.md#create-table-as-select).

## Ausgabedatasets

Durch diese Funktion erstellte Datensätze werden mit einem Ad-hoc-Schema generiert, das der Struktur der Ausgabedaten entspricht, wie in der SQL-Anweisung definiert. Für einige nachgelagerte Dienste sind Datasets mit bestimmten XDM-Schemas (Experience Data Model) erforderlich. Überprüfen Sie die Datenformatierungsanforderungen für nachgelagerte Dienste, bevor Sie Ihre Abfragen schreiben.