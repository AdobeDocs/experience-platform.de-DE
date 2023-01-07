---
keywords: Experience Platform; Startseite; beliebte Themen; Query Service; Query Service; postico; Postico; Verbindung mit Query Service
solution: Experience Platform
title: Verbindung mit Query Service
description: Dieses Dokument enthält den Link zur Installation des Backup-Clients Postico für Adobe Experience Platform Query Service.
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 6%

---

# Verbinden [!DNL Postico] zu Query Service (Mac)

In diesem Dokument werden die Schritte zum Verbinden von [!DNL Postico] mit Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> In diesem Handbuch wird davon ausgegangen, dass Sie bereits Zugriff auf [!DNL Postico] und sind mit dem Navigieren in der Benutzeroberfläche vertraut. Weitere Informationen [!DNL Postico] finden Sie im Abschnitt [offiziell [!DNL Postico] Dokumentation](https://eggerapps.at/postico/docs).
> 
> Zusätzlich [!DNL Postico] is **only** auf macOS-Geräten verfügbar.

Verbindung herstellen [!DNL Postico] zu Query Service, öffnen Sie [!DNL Postico] und wählen Sie **[!DNL New Favorite]**.

![Die [!DNL Postico] Benutzeroberfläche mit hervorgehobenem neuen Favoriten.](../images/clients/postico/open-postico.png)

Sie können jetzt Werte eingeben, um eine Verbindung mit Adobe Experience Platform herzustellen.

Weitere Informationen zum Auffinden Ihres Datenbanknamens, Hosts, Ports und Ihrer Anmeldedaten finden Sie in der [Handbuch zu Anmeldeinformationen](../ui/credentials.md). Um Ihre Anmeldeinformationen zu finden, melden Sie sich bei [!DNL Platform], wählen Sie **[!UICONTROL Abfragen]**, gefolgt von **[!UICONTROL Anmeldeinformationen]**.

Nachdem Sie Ihre Anmeldedaten eingefügt haben, wählen Sie **[!DNL Connect]** , um eine Verbindung mit Query Service herzustellen.

![Das Dialogfeld &quot;New Favorite&quot;mit hervorgehobener Verbindung.](../images/clients/postico/authentication-details.png)

Nach der Verbindung mit Platform können Sie eine Liste aller zuvor mit Query Service vorgenommenen Relationen anzeigen.

![Eine Liste der Verbindungen im [!DNL Postico] Benutzeroberfläche.](../images/clients/postico/show-queries.png)

## SQL-Anweisungen erstellen

Um eine neue SQL-Abfrage zu erstellen, wählen Sie &quot;SQL-Abfrage&quot;aus und öffnen Sie sie.

![Die [!DNL Postico] Benutzeroberfläche mit hervorgehobenem SQL-Abfragebefehl.](../images/clients/postico/create-query.png)

Es wird ein Feld angezeigt, in das Sie die auszuführende Abfrage eingeben können. Wenn Sie fertig sind, wählen Sie **[!DNL Execute Statement]** , um die Abfrage auszuführen.

![Der SQL-Editor mit Execute Statement hervorgehoben.](../images/clients/postico/run-statement.png)

Es wird eine Tabelle mit den Ergebnissen Ihrer abgeschlossenen Abfrage-Ausführung angezeigt.

![Eine Tabelle mit Ergebnissen aus der Beispielabfrage.](../images/clients/postico/query-results.png)

## Nächste Schritte

Jetzt, da Sie mit [!DNL Query Service]können Sie [!DNL Postico] , um Abfragen zu schreiben. Weitere Informationen dazu, wie Sie Abfragen formulieren und ausführen, finden Sie im Handbuch zum Thema [Ausführen von Abfragen](../best-practices/writing-queries.md).
