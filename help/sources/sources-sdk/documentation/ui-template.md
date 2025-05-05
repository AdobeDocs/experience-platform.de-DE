---
keywords: Experience Platform;Startseite;beliebte Themen;Quellen;Connectoren;Quell-Connectoren;Quellen-SDK;SDK
title: Self-Service-Dokumentationsvorlage für die Benutzeroberfläche
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Quellverbindung für YOURSOURCE erstellen.
exl-id: 6471c0a2-22e8-4133-a76f-ee3c5c669ef8
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 14%

---

# Erstellen einer *YOURSOURCE*-Quellverbindung über die Benutzeroberfläche

*Wenn Sie diese Vorlage durchlaufen, ersetzen oder löschen Sie alle kursiv gedruckten Absätze (beginnend mit diesem).*

*Aktualisieren Sie zunächst die Metadaten (Titel und Beschreibung) oben auf der Seite. Bitte ignorieren Sie alle Instanzen von UICONTROL auf dieser Seite. Dieses Tag hilft unseren maschinellen Übersetzungsprozessen dabei, die Seite korrekt in die verschiedenen Sprachen zu übersetzen, die wir unterstützen. Wir fügen Ihrer Dokumentation nach dem Absenden Tags hinzu.*

In diesem Tutorial werden Schritte zum Erstellen eines *YOURSOURCE*-Quell-Connectors mithilfe der Experience Platform-Benutzeroberfläche beschrieben.

## Überblick

*Geben Sie einen kurzen Überblick über Ihr Unternehmen, einschließlich des Nutzens, den es für Kunden bietet. Fügen Sie einen Link zu Ihrer Startseite der Produktdokumentation für weitere Informationen hinzu.*

>[!IMPORTANT]
>
>Dieser Quell-Connector und die Dokumentationsseite werden vom Team *YourSource* erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an *Link oder E-Mail-Adresse einfügen, unter der Sie für Aktualisierungen erreichbar sind*.

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

## Verbinden Ihres *YOURSOURCE*-Kontos

Wählen Sie in der Experience Platform-Benutzeroberfläche **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen *unter der Kategorie* YOURSOURCE“ die Option *YOURSOURCE* und dann **[!UICONTROL Daten hinzufügen]** aus.

>[!TIP]
>
>Im Folgenden finden Sie einige Beispiele für verwendete Screenshots. Ersetzen Sie beim Erstellen Ihrer Dokumentation die Bilder durch Screenshots Ihrer tatsächlichen Quelle. Sie können dasselbe Markierungsmuster und dieselbe Farbe sowie dieselben Dateinamen verwenden. Stellen Sie sicher, dass Ihr Screenshot den gesamten Bildschirm der Experience Platform-Benutzeroberfläche erfasst. Informationen zum Hochladen Ihrer Screenshots finden Sie im Handbuch unter [Übermitteln Ihrer Dokumentation zur Überprüfung](./github.md).

![Katalog](../assets/ui/catalog.png)

Die **[!UICONTROL Verbinden Sie Ihr SOURCE-Konto]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das *YOURSOURCE*-Konto, mit dem Sie einen neuen Datenfluss erstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![vorhanden](../assets/ui/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen, eine optionale Beschreibung und Ihre -Anmeldeinformationen an. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![neu](../assets/ui/new.png)

## Nächste Schritte

*Die Workflows für die verbleibenden Schritte zum Erstellen eines Datenflusses werden modularisiert. Wenn Sie bestimmte Aufrufe bezüglich Ihrer Quelle durchführen möchten, lesen Sie bitte den Abschnitt Zusätzliche Ressourcen unten.*

In diesem Tutorial haben Sie eine Verbindung zu Ihrem *YOURSOURCE*-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Daten in Experience Platform zu importieren](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/dataflow/crm.html?lang=de).

## Zusätzliche Ressourcen

*Dies ist ein optionaler Abschnitt, in dem Sie weitere Links zu Ihrer Produktdokumentation oder anderen Schritten, Screenshots und Nuancen bereitstellen können, die Sie für den Erfolg des Kunden als wichtig erachten. In diesem Abschnitt können Sie Informationen oder Tipps zum gesamten Workflow Ihrer Quelle hinzufügen, insbesondere wenn es bestimmte „Fallstricke“ gibt, auf die ein Endbenutzer stoßen könnte.*
