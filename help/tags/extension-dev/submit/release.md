---
title: Freigeben einer Erweiterung
description: Erfahren Sie, wie Sie eine Tag-Erweiterung in Adobe Experience Platform privat oder öffentlich freigeben.
exl-id: a5eb6902-4b0f-4717-a431-a290c50fb5a6
source-git-commit: 2152cf98d9809654cca7abd7b8469a72e8387b2a
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 67%

---

# Freigeben einer Erweiterung

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Sobald Testing und Dokumentation abgeschlossen sind, kann die Erweiterung freigegeben werden. Es gibt derzeit zwei Arten von Freigaben, die Sie ausführen können:

- **Private Freigabe**: Die fertige Erweiterung steht allen Eigenschaften in Ihrer Firma zur Verfügung, nicht aber anderen Firmen in Adobe Experience Platform.
- **Öffentliche Version**: Die fertige Erweiterung ist im Online-Marktplatz für alle Benutzer von Adobe Experience Platform verfügbar.

>[!NOTE]
>
>Nachdem Sie Ihre Erweiterung freigegeben haben, können Sie keine Änderungen mehr daran vornehmen und die Freigabe nicht aufheben.  Nach der Freigabe können Sie Fehlerkorrekturen und Funktionserweiterungen vornehmen, indem Sie mit `POST` eine neue Version des Erweiterungspakets veröffentlichen und die oben genannten Test- und Freigabeschritte für diese neue Version ausführen.

Sie müssen Ihre Erweiterung zunächst als private Erweiterung veröffentlichen, bevor sie öffentlich freigegeben werden kann.

## Private Freigabe

Die einfachste Möglichkeit, Ihre Erweiterung mit privater Verfügbarkeit freizugeben, besteht in der Verwendung des [Tag-Erweiterungs-Releasers](https://www.npmjs.com/package/@adobe/reactor-releaser).

```bash
npx @adobe/reactor-releaser
```

`npx` ermöglicht Ihnen, ein npm-Paket herunterzuladen und auszuführen, ohne es tatsächlich auf Ihrem Computer zu installieren. Dies ist die einfachste Möglichkeit, den Release auszuführen.

>[!NOTE]
> Standardmäßig erwartet der Releaser Adobe I/O-Anmeldeinformationen für einen Server-zu-Server-OAuth-Ablauf. Die veralteten `jwt-auth`-Anmeldedaten
> kann durch Ausführen von `npx @adobe/reactor-releaser@v3.1.3` bis zur Einstellung am 1. Januar 2025 verwendet werden. Die erforderlichen Parameter
> zum Ausführen der `jwt-auth` -Version finden Sie [hier](https://github.com/adobe/reactor-releaser/tree/9ea66aa2c683fe7da0cca50ff5c9b9372f183bb5).

Für den Release müssen Sie nur einige wenige Informationen eingeben. Die `clientId` und `clientSecret` können aus der Adobe I/O-Konsole abgerufen werden. Navigieren Sie in der I/O-Konsole zur Seite [Integrationen](https://console.adobe.io/integrations). Wählen Sie die korrekte Organisation im Dropdown-Menü aus, suchen Sie die richtige Integration und klicken Sie auf **[!UICONTROL Ansicht]**.

- Was ist Ihr `clientId`? Kopieren Sie diese aus der I/O-Konsole und fügen Sie sie ein.
- Was ist Ihr `clientSecret`? Kopieren Sie diese aus der I/O-Konsole und fügen Sie sie ein.

Der Releaser liest die Felder `name` und `platform` aus Ihrem Erweiterungsmanifest und fragt die API nach einem übereinstimmenden Erweiterungspaket in der Entwicklungsverfügbarkeit ab.
Der Releaser wird Sie dann bitten zu bestätigen, dass er das richtige Erweiterungspaket gefunden hat, das Sie für die private Verfügbarkeit freigeben möchten.

Wenn Sie Ihre Erweiterung mit privater Verfügbarkeit direkt über die API freigeben möchten, finden Sie weitere Details im Beispielaufruf für die [private Freigabe eines Erweiterungspakets](../../api/endpoints/extension-packages.md/#private-release) in den API-Dokumenten.

## Öffentliche Freigabe

Sobald Sie die private Freigabe abgeschlossen haben, können Sie Adobe um die öffentliche Freigabe bitten.  Dadurch wird Ihre Erweiterung im öffentlichen Katalog verfügbar gemacht. Jeder Nutzer der Datenerfassung kann Ihre Erweiterung für jede Eigenschaft installieren.

Bitte füllen Sie das [Anfrageformular für eine öffentliche Freigabe](https://www.feedbackprogram.adobe.com/c/r/DCExtensionReleaseRequest) aus, um den Freigabeprozess zu starten.
