---
title: Dokumentation - Self-Service-Vorlage für die Streaming-SDK-Benutzeroberfläche
description: Erfahren Sie, wie Sie mithilfe der Benutzeroberfläche Streaming-Daten aus einer Quelle an Adobe Experience Platform übertragen können.
exl-id: 82254be0-fa31-4114-a0ec-179a990e0904
badge: Beta
source-git-commit: 256857103b4037b2cd7b5b52d6c5385121af5a9f
workflow-type: tm+mt
source-wordcount: '1187'
ht-degree: 19%

---

# Erstellen Sie eine Quellverbindung und einen Datenfluss zum Streamen von *YOURSOURCE*-Daten mithilfe der Benutzeroberfläche.

*Wenn Sie diese Vorlage durchlaufen, ersetzen oder löschen Sie alle kursiv gedruckten Absätze (beginnend mit dieser).*

*Aktualisieren Sie zunächst die Metadaten (Titel und Beschreibung) oben auf der Seite. Bitte ignorieren Sie alle UICONTROL Instanzen auf dieser Seite. Dies ist ein Tag, das unseren maschinellen Übersetzungsprozessen hilft, die Seite korrekt in die verschiedenen Sprachen zu übersetzen, die wir unterstützen. Wir fügen Ihrer Dokumentation Tags hinzu, nachdem Sie sie gesendet haben.*

In diesem Tutorial werden die Schritte zum Erstellen eines Quell-Connectors für *YOURSOURCE* mithilfe der Platform-Benutzeroberfläche beschrieben.

## Übersicht

*Bieten Sie einen kurzen Überblick über Ihr Unternehmen, einschließlich des Werts, den es Kunden bietet. Fügen Sie einen Link zu Ihrer Homepage für die Produktdokumentation hinzu, um ihn weiter zu lesen.*

>[!IMPORTANT]
>
>Diese Quell-Connector- und Dokumentationsseite wird vom *YOURSOURCE*-Team erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt unter *Link oder E-Mail-Adresse einfügen, an die Sie zur Aktualisierung gelangen*.

## Voraussetzungen

*Fügen Sie in diesem Abschnitt Informationen zu allen Elementen hinzu, die Kunden beachten müssen, bevor sie mit der Einrichtung der Quelle in der Adobe Experience Platform-Benutzeroberfläche beginnen. Dies kann ungefähr sein:*

* *muss einer Zulassungsliste hinzugefügt werden*
* *Anforderungen für E-Mail-Hashing*
* *alle Kontospezifikationen auf Ihrer Seite*
* *Ermitteln der Authentifizierungsberechtigungen für die Verbindung mit Ihrer Plattform*

### Sammeln erforderlicher Anmeldeinformationen

Um *YOURSOURCE* mit Platform zu verbinden, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| *Berechtigung 1* | *Bitte fügen Sie hier eine kurze Beschreibung zur Authentifizierungsberechtigung Ihrer Quelle hinzu* | *Bitte fügen Sie hier ein Beispiel für die Authentifizierungsberechtigung Ihrer Quelle hinzu* |
| *credential two* | *Bitte fügen Sie hier eine kurze Beschreibung zur Authentifizierungsberechtigung Ihrer Quelle hinzu* | *Bitte fügen Sie hier ein Beispiel für die Authentifizierungsberechtigung Ihrer Quelle hinzu* |
| *Berechtigung drei* | *Bitte fügen Sie hier eine kurze Beschreibung zur Authentifizierungsberechtigung Ihrer Quelle hinzu* | *Bitte fügen Sie hier ein Beispiel für die Authentifizierungsberechtigung Ihrer Quelle hinzu* |

Weitere Informationen zu diesen Anmeldedaten finden Sie in der Dokumentation zur Authentifizierung für *YOURSOURCE* . *Fügen Sie hier einen Link zur Authentifizierungsdokumentation Ihrer Plattform hinzu*.

### Integrieren von *YOURSOURCE* in Ihren Webhook

*Das Streaming-SDK erfordert, dass Ihre Quelle Webhooks unterstützen kann, um mit Experience Platform kommunizieren zu können. In diesem Abschnitt müssen Sie die Schritte angeben, die Ihre Benutzer ausführen müssen, um YOURSOURCE mit einem Webhook zu integrieren.*

## Ihr *YOURSOURCE*-Konto verbinden

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Quellen]** in der linken Navigationsleiste, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie **Streaming** die Option *YOURSOURCE* und klicken Sie dann auf **[!UICONTROL Daten hinzufügen]**.

>[!TIP]
>
>Die folgenden Screenshots sind Beispiele. Ersetzen Sie bei der Erstellung Ihrer Dokumentation die Bilder durch Screenshots Ihrer eigentlichen Quelle. Sie können dasselbe Markierungsmuster und dieselbe Farbe sowie dieselben Dateinamen verwenden. Stellen Sie sicher, dass Ihr Screenshot den gesamten Bildschirm der Platform-Benutzeroberfläche erfasst. Informationen zum Hochladen Ihrer Screenshots finden Sie im Handbuch zum [Übermitteln Ihrer Dokumentation zur Überprüfung](../documentation/github.md).

![Der Experience Platform-Quellkatalog](../assets/streaming/catalog.png)

## Daten auswählen

Der Schritt **[!UICONTROL Daten auswählen]** wird angezeigt und bietet eine Oberfläche zur Auswahl der Daten, die Sie an Platform übermitteln.

* Der linke Teil der Benutzeroberfläche ist ein Browser, mit dem Sie die verfügbaren Datenströme in Ihrem Konto anzeigen können.
* Im rechten Bereich der Benutzeroberfläche können Sie eine Vorschau von bis zu 100 Zeilen mit Daten aus einer JSON-Datei anzeigen.

Wählen Sie **[!UICONTROL Dateien hochladen]** aus, um eine JSON-Datei von Ihrem lokalen System hochzuladen. Alternativ können Sie die JSON-Datei, die Sie hochladen möchten, per Drag-and-Drop in den Bereich [!UICONTROL Dateien ziehen und ablegen] ziehen.

![Der Schritt zum Hinzufügen von Daten des Ursprungs-Workflows.](../assets/streaming/add-data.png)

Nach dem Hochladen Ihrer Datei wird die Vorschau-Oberfläche aktualisiert, um eine Vorschau des hochgeladenen Schemas anzuzeigen. Über die Vorschau-Oberfläche können Sie den Inhalt und die Struktur einer Datei überprüfen. Sie können auch das Dienstprogramm [!UICONTROL Suchfeld] verwenden, um auf bestimmte Elemente innerhalb Ihres Schemas zuzugreifen.

Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.

![Der Vorschauschritt des Ursprungs-Workflows.](../assets/streaming/preview.png)

## Datenflussdetails

Der Schritt **Datenfluss-Detail** wird angezeigt und bietet Ihnen Optionen zur Verwendung eines vorhandenen Datensatzes oder zur Einrichtung eines neuen Datensatzes für Ihren Datenfluss sowie die Möglichkeit, einen Namen und eine Beschreibung für Ihren Datenfluss anzugeben. In diesem Schritt können Sie auch Einstellungen für die Profilerfassung, Fehlerdiagnose, partielle Erfassung und Warnhinweise konfigurieren.

Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.

![Der Schritt &quot;Datenfluss-Detail&quot;des Ursprungs-Workflows.](../assets/streaming/dataflow-detail.png)

## Zuordnung

Es erfolgt der Schritt der [!UICONTROL Zuordnung], in dem Ihnen eine Schnittstelle zum Zuordnen der Quellfelder aus Ihrem Quellschema zu den entsprechenden XDM-Zielfeldern im Zielschema bereitgestellt wird.

Platform bietet intelligente Empfehlungen für automatisch zugeordnete Felder, die auf dem ausgewählten Zielschema oder Datensatz basieren. Sie können die Zuordnungsregeln manuell an Ihre Anwendungsfälle anpassen. Je nach Bedarf können Sie wahlweise Felder direkt zuordnen oder mithilfe von Datenvorbereitungsfunktionen Quelldaten transformieren, um berechnete oder anderweitig ermittelte Werte abzuleiten. Umfassende Schritte zur Verwendung der Zuordnungsoberfläche und der berechneten Felder finden Sie im Handbuch [Data Prep UI guide](https://experienceleague.adobe.com/docs/experience-platform/data-prep/ui/mapping.html).

Nachdem die Quelldaten erfolgreich zugeordnet wurden, wählen Sie **[!UICONTROL Weiter]** aus.

![Der Zuordnungsschritt des Ursprungs-Workflows.](../assets/streaming/mapping.png)

## Überprüfung

Der Schritt **[!UICONTROL Überprüfung]** wird angezeigt, sodass Sie Ihren neuen Datenfluss überprüfen können, bevor er hergestellt wird. Die Details lassen sich wie folgt kategorisieren:

* **[!UICONTROL Verbindung]**: Zeigt den Quelltyp, den relevanten Pfad der ausgewählten Quelldatei und die Anzahl der Spalten innerhalb dieser Quelldatei an.
* **[!UICONTROL Datensatz- und Zuordnungsfelder zuweisen]**: Zeigt an, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, dem der Datensatz entspricht.

Nachdem Sie Ihren Datenfluss überprüft haben, klicken Sie auf **[!UICONTROL Beenden]** und lassen Sie die Erstellung des Datenflusses etwas Zeit zu.

![Der Überprüfungsschritt des Ursprungs-Workflows.](../assets/streaming/review.png)

## Abrufen der Streaming-Endpunkt-URL

Mit dem erstellten Streaming-Datenfluss können Sie jetzt Ihre Streaming-Endpunkt-URL abrufen. Dieser Endpunkt wird zum Abonnieren Ihres Webhooks verwendet, sodass Ihre Streaming-Quelle mit Experience Platform kommunizieren kann.

Um Ihren Streaming-Endpunkt abzurufen, rufen Sie die Seite [!UICONTROL Datenfluss-Aktivität] des soeben erstellten Datenflusses auf und kopieren Sie den Endpunkt vom unteren Rand des Bereichs [!UICONTROL Eigenschaften] .

![ Der Streaming-Endpunkt in der Datenflug-Aktivität.](../assets/testing/endpoint-test.png)

## Nächste Schritte

*Workflows für die verbleibenden Schritte zum Erstellen eines Datenflusses werden modularisiert. Wenn Sie bestimmte Anrufe an Ihre Quelle richten möchten, lesen Sie bitte den Abschnitt zu den zusätzlichen Ressourcen unten.*

In diesem Tutorial haben Sie eine Verbindung zu Ihrem *YOURSOURCE* -Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und einen [Datenfluss konfigurieren, um Daten in Platform zu importieren](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/dataflow/crm.html).

## Zusätzliche Ressourcen

*Dies ist ein optionaler Abschnitt, in dem Sie weitere Links zu Ihrer Produktdokumentation oder anderen Schritten, Screenshots und Nuancen bereitstellen können, die Sie für wichtig halten, damit der Kunde erfolgreich ist. Sie können diesen Abschnitt verwenden, um Informationen oder Tipps zum gesamten Workflow Ihrer Quelle hinzuzufügen, insbesondere wenn es bestimmte &quot;Fallstricke&quot;gibt, auf die ein Endbenutzer stoßen könnte.*
