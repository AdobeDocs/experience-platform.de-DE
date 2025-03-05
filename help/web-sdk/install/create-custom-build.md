---
title: Erstellen eines benutzerdefinierten Web-SDK-Builds mit dem NPM-Paket
description: Erstellen Sie einen benutzerdefinierten Web-SDK-Build, der nur die benötigten Module enthält.
source-git-commit: 0f77023b07102ac2bc812034afacb1522ef209e5
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 7%

---


# Erstellen eines benutzerdefinierten Web-SDK-Builds

Die Experience Platform Web SDK-Bibliothek enthält mehrere Module für verschiedene Funktionen wie Personalisierung, Identität, Linktracking und mehr. Je nach Anwendungsfällen benötigen Sie möglicherweise nur bestimmte Funktionen anstelle der gesamten Bibliothek. Wenn Sie einen benutzerdefinierten Web-SDK-Build erstellen, können Sie nur die benötigten Module auswählen, die Bibliotheksgröße reduzieren und die Leistung verbessern.

## Anwendungsfälle {#use-case}

Das Erstellen eines benutzerdefinierten Web-SDK-Builds trägt dazu bei, die Bibliotheksgröße zu reduzieren und die Leistung zu steigern. Hier einige Beispiele:

### Entfernen von Media Analytics {#media-analytics-removal}

Wenn Ihre Website keine Medieninhalte hat, können Sie die [!DNL Media Analytics] und die [!DNL Streaming Media] Module vom Build ausschließen. Dadurch kann die Build-Größe von Web SDK um bis zu 50 % reduziert und die Ladegeschwindigkeit verbessert werden.

### Personalization-Entfernung {#personalization}

Wenn Sie nur Benutzermetriken erfassen müssen und nicht planen, Adobe Target oder Journey Optimizer für die Personalisierung zu verwenden, können Sie das [!DNL Personalization] ausschließen. Dadurch wird die Bibliotheksgröße reduziert, während Sie gleichzeitig die erforderlichen Metriken erfassen können.

## Voraussetzungen {#prerequisites}

Zum Erstellen eines benutzerdefinierten Web-SDK-Builds benötigen Sie das NPM-Paket für Web-SDK . Stellen Sie sicher, dass [Node.js](https://nodejs.org/en/download/package-manager/all) auf Ihrem Computer installiert ist. Weitere Informationen finden Sie in der Dokumentation [ Installieren von Web SDK mithilfe ](npm.md) NPM-Pakets .

## Komponenten und Abhängigkeiten {#components-dependencies}

Bevor Sie einen benutzerdefinierten Web-SDK-Build erstellen, definieren Sie die Web-SDK-Komponenten und -Befehle, die Sie verwenden möchten. Einige Befehle hängen davon ab, dass bestimmte Module im Build enthalten sind.

Die folgende Tabelle zeigt die Beziehung zwischen Web SDK-Modulen und den darin enthaltenen Befehlen:

| Modulabhängigkeit | Konfigurationsparameter | Commands | Größenklasse |
|---------|----------|---------|---------|
| Aktivitätssammler | [`clickCollectionEnabled`](../commands/configure/clickcollectionenabled.md) | K. A. | Mittel |
| Zielgruppen | K. A. | K. A. | Gering |
| Kontext | [`context`](../commands/configure/context.md) | K. A. | Gering |
| Regel-Engine | `personalizationStorageEnabled` | | <ul><li>`evaluateRulesets`</li><li>[`subscribeRulesetItems`](../commands/subscriberulesetitems.md)</li></ul> | Mittel |
| Ereignis-Zusammenführung | K. A. | `createEventMergeId` | Gering |
| Media Analytics Bridge | K. A. | [`getMediaAnalyticsTracker`](../commands/getmediaanalyticstracker.md) | Groß |
| Personalisierung | <ul><li>[`prehidingStyle`](../commands/configure/prehidingstyle.md)</li><li>[`targetMigrationEnabled`](../commands/configure/targetmigrationenabled.md)</li><li>[`autoCollectPropositionInteractions`](../commands/configure/autocollectpropositioninteractions.md)</li></ul> | K. A. | Groß |
| Einverständnis | [`defaultConsent`](../commands/configure/defaultconsent.md) | [`setConsent`](../commands/setconsent.md) | Gering |
| Streaming-Medien | [`streamingMedia`](../commands/configure/streamingmedia.md) | <ul><li>[`createMediaSession`](../commands/createmediasession.md)</li><li>[`sendMediaEvent`](../commands/sendmediaevent.md)</li></ul> | Groß |

## Erstellen eines benutzerdefinierten Web-SDK-Builds mit dem NPM-Paket {#create-custom-build}

1. Öffnen Sie Ihr Terminal und führen Sie `npx @adobe/alloy` aus. Sie werden aufgefordert, die Web SDK-Komponenten auszuwählen, die Ihr benutzerdefinierter Build enthalten soll.

   ![Bild eines Terminals, das die Auswahl des benutzerdefinierten Build-Moduls anzeigt.](../assets/custom-build/npx.png)

   Verwenden Sie die Pfeiltasten, um in der Modulliste nach oben und unten zu navigieren.

   * Drücken Sie **Leertaste**, um das ausgewählte Modul zu aktivieren oder zu deaktivieren.
   * Drücken Sie `A`, um alle Module zu aktivieren oder zu deaktivieren.
   * Drücken Sie `I`, um die Auswahl umzukehren.
   * Drücken Sie `Enter`, um Ihre Auswahl zu bestätigen, und fahren Sie mit dem nächsten Schritt fort.

1. Nachdem Sie die Module ausgewählt haben, die in Ihren benutzerdefinierten Build eingeschlossen werden sollen, können Sie zwischen dem Speichern einer minimierten oder nicht minimierten Version Ihres benutzerdefinierten Web SDK-Bibliotheks-Builds wählen. Wählen Sie die gewünschte Option aus, und drücken Sie `Enter`.

   ![Bild eines Terminals, das die Minimierungsauswahl des benutzerdefinierten Builds anzeigt.](../assets/custom-build/minify.png)

1. Als Nächstes werden Sie gefragt, wo Sie den Build auf Ihrem lokalen Computer speichern möchten. Drücken Sie `Enter`, um den vorausgewählten Speicherort zu bestätigen, oder geben Sie einen neuen Speicherort ein.

   ![Bild eines Terminals, das die benutzerdefinierte Option zum Erstellen und Speichern anzeigt.](../assets/custom-build/save.png)

1. Nachdem Sie den Speicherort bestätigt haben, wird Ihr benutzerdefinierter Build generiert und gespeichert.

   ![Bild eines Terminals, das den Speicherort des benutzerdefinierten Builds anzeigt.](../assets/custom-build/saved.png)

