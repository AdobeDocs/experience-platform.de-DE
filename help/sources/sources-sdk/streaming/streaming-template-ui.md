---
title: Dokumentationsvorlage für Selbstbedienungs-Streaming in der SDK-Benutzeroberfläche
description: Erfahren Sie, wie Sie Streaming-Daten aus einer Quelle mithilfe der Benutzeroberfläche in Adobe Experience Platform übertragen.
exl-id: 82254be0-fa31-4114-a0ec-179a990e0904
badge: Beta
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 16%

---

# Erstellen einer Quellverbindung und eines Datenflusses zum Streamen *YOURSOURCE*-Daten über die Benutzeroberfläche

*Wenn Sie diese Vorlage durchlaufen, ersetzen oder löschen Sie alle kursiv gedruckten Absätze (beginnend mit diesem).*

*Aktualisieren Sie zunächst die Metadaten (Titel und Beschreibung) oben auf der Seite. Bitte ignorieren Sie alle Instanzen von UICONTROL auf dieser Seite. Dieses Tag hilft unseren maschinellen Übersetzungsprozessen dabei, die Seite korrekt in die verschiedenen Sprachen zu übersetzen, die wir unterstützen. Wir fügen Ihrer Dokumentation nach dem Absenden Tags hinzu.*

In diesem Tutorial werden Schritte zum Erstellen eines *YOURSOURCE*-Quell-Connectors mithilfe der Experience Platform-Benutzeroberfläche beschrieben.

## Überblick

*Geben Sie einen kurzen Überblick über Ihr Unternehmen, einschließlich des Nutzens, den es für Kunden bietet. Fügen Sie einen Link zu Ihrer Startseite der Produktdokumentation für weitere Informationen hinzu.*

>[!IMPORTANT]
>
>Dieser Quell-Connector und die Dokumentationsseite werden vom Team *YOURSOURCE* erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an *Link oder E-Mail-Adresse einfügen, unter der Sie für Aktualisierungen erreichbar sind*.

## Voraussetzungen

*Fügen Sie in diesem Abschnitt Informationen zu allen Dingen hinzu, die Kundinnen und Kunden beachten müssen, bevor Sie die -Quelle in der Benutzeroberfläche von Adobe Experience Platform einrichten. Dies kann sein über:*

* *muss zu einer Zulassungsliste hinzugefügt werden*
* *Anforderungen für E-Mail-Hashing*
* *Alle Kontospezifikationen auf Ihrer Seite*
* *Wie Sie die Authentifizierungsdaten erhalten, um eine Verbindung zu Ihrer Plattform herzustellen*

### Sammeln erforderlicher Anmeldedaten

Um eine Verbindung zwischen *YOURSOURCE* und Experience Platform herzustellen, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| *Anmeldedaten eins* | *Bitte fügen Sie hier eine kurze Beschreibung zu den Authentifizierungsdaten Ihrer Quelle hinzu* | *Bitte fügen Sie hier ein Beispiel für die Authentifizierungsdaten Ihrer Quelle hinzu* |
| *Berechtigung zwei* | *Bitte fügen Sie hier eine kurze Beschreibung zu den Authentifizierungsdaten Ihrer Quelle hinzu* | *Bitte fügen Sie hier ein Beispiel für die Authentifizierungsdaten Ihrer Quelle hinzu* |
| *Berechtigung 3* | *Bitte fügen Sie hier eine kurze Beschreibung zu den Authentifizierungsdaten Ihrer Quelle hinzu* | *Bitte fügen Sie hier ein Beispiel für die Authentifizierungsdaten Ihrer Quelle hinzu* |

Weitere Informationen zu diesen Anmeldeinformationen finden Sie in der Dokumentation zur *YOURSOURCE*-Authentifizierung . *Fügen Sie hier einen Link zur Authentifizierungsdokumentation Ihrer Plattform hinzu*.

### Integrieren von *YOURSOURCE* in Ihren Webhook

*Streaming-SDK erfordert, dass Ihre Quelle Webhooks unterstützen kann, um mit Experience Platform kommunizieren zu können. In diesem Abschnitt müssen Sie die Schritte angeben, die Ihre Benutzerinnen und Benutzer ausführen müssen, um IHRE QUELLE mit einem Webhook zu integrieren.*

## Verbinden Ihres *YOURSOURCE*-Kontos

Wählen Sie in der Experience Platform-Benutzeroberfläche **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter **Kategorie** Streaming“ die Option *IHRE*) und dann **[!UICONTROL Daten hinzufügen]** aus.

>[!TIP]
>
>Im Folgenden finden Sie einige Beispiele für verwendete Screenshots. Ersetzen Sie beim Erstellen Ihrer Dokumentation die Bilder durch Screenshots Ihrer tatsächlichen Quelle. Sie können dasselbe Markierungsmuster und dieselbe Farbe sowie dieselben Dateinamen verwenden. Stellen Sie sicher, dass Ihr Screenshot den gesamten Bildschirm der Experience Platform-Benutzeroberfläche erfasst. Informationen zum Hochladen Ihrer Screenshots finden Sie im Handbuch unter [Übermitteln Ihrer Dokumentation zur Überprüfung](../documentation/github.md).

![Der Experience Platform-Quellkatalog](../assets/streaming/catalog.png)

## Daten auswählen

Der Schritt **[!UICONTROL Daten auswählen]** wird angezeigt und bietet eine Schnittstelle zur Auswahl der Daten, die Sie an Experience Platform übermitteln.

* Der linke Teil der Benutzeroberfläche ist ein Browser, mit dem Sie die verfügbaren Datenströme in Ihrem Konto anzeigen können.
* Im rechten Teil der Benutzeroberfläche können Sie eine Vorschau von bis zu 100 Datenzeilen aus einer JSON-Datei anzeigen.

Wählen Sie **[!UICONTROL Dateien hochladen]** aus, um eine JSON-Datei von Ihrem lokalen System hochzuladen. Alternativ können Sie die JSON-Datei, die Sie hochladen möchten, per Drag-and-Drop in das Bedienfeld [!UICONTROL Dateien per Drag-and-Drop ].

![Der Schritt „Daten hinzufügen“ des Quell-Workflows.](../assets/streaming/add-data.png)

Nachdem Ihre Datei hochgeladen wurde, wird die Vorschau-Oberfläche aktualisiert, um eine Vorschau des hochgeladenen Schemas anzuzeigen. In der Vorschauoberfläche können Sie den Inhalt und die Struktur einer Datei überprüfen. Sie können auch das Dienstprogramm [!UICONTROL Suchfeld] verwenden, um innerhalb Ihres Schemas auf bestimmte Elemente zuzugreifen.

Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.

![Der Vorschauschritt des Quell-Workflows.](../assets/streaming/preview.png)

## Datenflussdetails

Der Schritt **Datenflussdetails** wird angezeigt und bietet Ihnen Optionen zum Verwenden eines vorhandenen Datensatzes oder zum Einrichten eines neuen Datensatzes für Ihren Datenfluss sowie die Möglichkeit, einen Namen und eine Beschreibung für Ihren Datenfluss anzugeben. In diesem Schritt können Sie auch Einstellungen für die Profilaufnahme, Fehlerdiagnose, partielle Aufnahme und Warnhinweise konfigurieren.

Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.

![Der Schritt „Datenflussdetails“ des Quell-Workflows.](../assets/streaming/dataflow-detail.png)

## Zuordnung

Es erfolgt der Schritt der [!UICONTROL Zuordnung], in dem Ihnen eine Schnittstelle zum Zuordnen der Quellfelder aus Ihrem Quellschema zu den entsprechenden XDM-Zielfeldern im Zielschema bereitgestellt wird.

Experience Platform bietet intelligente Empfehlungen für automatisch zugeordnete Felder, die auf dem ausgewählten Zielschema oder Datensatz basieren. Sie können die Zuordnungsregeln manuell an Ihre Anwendungsfälle anpassen. Je nach Bedarf können Sie wahlweise Felder direkt zuordnen oder mithilfe von Datenvorbereitungsfunktionen Quelldaten transformieren, um berechnete oder anderweitig ermittelte Werte abzuleiten. Eine ausführliche Anleitung zur Verwendung der Zuordnungsschnittstelle und berechneter Felder finden Sie im [Handbuch zur Datenvorbereitungs-Benutzeroberfläche](https://experienceleague.adobe.com/docs/experience-platform/data-prep/ui/mapping.html).

Nachdem Ihre Quelldaten erfolgreich zugeordnet wurden, klicken Sie auf **[!UICONTROL Weiter]**.

![Der Zuordnungsschritt des Quell-Workflows.](../assets/streaming/mapping.png)

## Überprüfung

Der Schritt **[!UICONTROL Überprüfung]** wird angezeigt, sodass Sie Ihren neuen Datenfluss überprüfen können, bevor er hergestellt wird. Die Details lassen sich wie folgt kategorisieren:

* **[!UICONTROL Verbindung]**: Zeigt den Quelltyp, den relevanten Pfad der ausgewählten Quelldatei und die Anzahl der Spalten innerhalb dieser Quelldatei an.
* **[!UICONTROL Datensatz- und Zuordnungsfelder zuweisen]**: Zeigt an, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, dem der Datensatz entspricht.

Nachdem Sie Ihren Datenfluss überprüft haben, klicken Sie auf **[!UICONTROL Beenden]** und gewähren Sie etwas Zeit für die Erstellung des Datenflusses.

![Der Überprüfungsschritt des Quell-Workflows.](../assets/streaming/review.png)

## Abrufen der Streaming-Endpunkt-URL

Nachdem Sie Ihren Streaming-Datenfluss erstellt haben, können Sie jetzt Ihre Streaming-Endpunkt-URL abrufen. Dieser Endpunkt wird verwendet, um Ihren Webhook zu abonnieren, sodass Ihre Streaming-Quelle mit Experience Platform kommunizieren kann.

Um Ihren Streaming-Endpunkt abzurufen, gehen Sie zur Seite [!UICONTROL Datenflussaktivität] des soeben erstellten Datenflusses und kopieren Sie den Endpunkt am unteren Rand des Bedienfelds [!UICONTROL Eigenschaften].

![Der Streaming-Endpunkt in der Datenflussaktivität.](../assets/testing/endpoint-test.png)

## Nächste Schritte

*Die Workflows für die verbleibenden Schritte zum Erstellen eines Datenflusses werden modularisiert. Wenn Sie bestimmte Aufrufe bezüglich Ihrer Quelle durchführen möchten, lesen Sie bitte den Abschnitt Zusätzliche Ressourcen unten.*

In diesem Tutorial haben Sie eine Verbindung zu Ihrem *YOURSOURCE*-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten in Experience Platform zu importieren](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/dataflow/crm.html).

## Zusätzliche Ressourcen

*Dies ist ein optionaler Abschnitt, in dem Sie weitere Links zu Ihrer Produktdokumentation oder anderen Schritten, Screenshots und Nuancen bereitstellen können, die Sie für den Erfolg des Kunden als wichtig erachten. In diesem Abschnitt können Sie Informationen oder Tipps zum gesamten Workflow Ihrer Quelle hinzufügen, insbesondere wenn es bestimmte „Fallstricke“ gibt, auf die ein Endbenutzer stoßen könnte.*
