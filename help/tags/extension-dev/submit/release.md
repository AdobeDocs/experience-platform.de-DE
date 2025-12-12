---
title: Freigeben einer Erweiterung
description: Erfahren Sie, wie Sie eine Tag-Erweiterung in Adobe Experience Platform privat oder öffentlich freigeben.
exl-id: a5eb6902-4b0f-4717-a431-a290c50fb5a6
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 60%

---

# Freigeben einer Erweiterung

Sobald Testing und Dokumentation abgeschlossen sind, kann die Erweiterung freigegeben werden. Es gibt derzeit zwei Arten von Freigaben, die Sie ausführen können:

- **Private Freigabe**: Die fertige Erweiterung steht allen Eigenschaften in Ihrer Firma zur Verfügung, nicht aber anderen Firmen in Adobe Experience Platform.
- **Öffentliche Version**: Die fertige Erweiterung ist im Online-Marktplatz für alle Benutzer von Adobe Experience Platform verfügbar.

>[!NOTE]
>
>Nachdem Sie Ihre Erweiterung freigegeben haben, können Sie keine Änderungen mehr daran vornehmen und die Freigabe nicht aufheben.  Nach der Freigabe können Sie Fehlerkorrekturen und Funktionserweiterungen vornehmen, indem Sie mit `POST` eine neue Version des Erweiterungspakets veröffentlichen und die oben genannten Test- und Freigabeschritte für diese neue Version ausführen.

Sie müssen zuerst Ihre Erweiterung als private Erweiterung freigeben, bevor sie öffentlich freigegeben werden kann.

## Private Freigabe

Die einfachste Möglichkeit, Ihre Erweiterung mit privater Verfügbarkeit freizugeben, ist die Verwendung des [Tag Extension Releaser](https://www.npmjs.com/package/@adobe/reactor-releaser).

```bash
npx @adobe/reactor-releaser
```

`npx` ermöglicht Ihnen, ein npm-Paket herunterzuladen und auszuführen, ohne es tatsächlich auf Ihrem Computer zu installieren. Dies ist die einfachste Möglichkeit, den Release auszuführen.

>[!NOTE]
> Standardmäßig erwartet der Release-Benutzer Adobe I/O-Anmeldeinformationen für einen OAuth-Fluss von Server zu Server. Die alten `jwt-auth` Anmeldedaten
> kann verwendet werden, indem `npx @adobe/reactor-releaser@v3.1.3` bis zur Einstellung am 1. Januar 2025 ausgeführt wird. Die erforderlichen Parameter
> Um die `jwt-auth` Version auszuführen, finden Sie [hier](https://github.com/adobe/reactor-releaser/tree/9ea66aa2c683fe7da0cca50ff5c9b9372f183bb5).

Für den -Releaser müssen Sie nur wenige Informationen eingeben. `clientId` und `clientSecret` können über die Adobe I/O-Konsole abgerufen werden. Navigieren Sie in der I/O-Konsole zur Seite [Integrationen](https://console.adobe.io/integrations). Wählen Sie die richtige Organisation im Dropdown-Menü aus, suchen Sie die richtige Integration und klicken Sie auf **[!UICONTROL View]**.

- Was ist Ihr `clientId`? Kopieren Sie diese aus der I/O-Konsole und fügen Sie sie ein.
- Was ist Ihr `clientSecret`? Kopieren Sie diese aus der I/O-Konsole und fügen Sie sie ein.

Der Releaser liest die `name`- und `platform` aus Ihrem Erweiterungsmanifest und fragt in der Entwicklungsverfügbarkeit bei der API nach einem passenden Erweiterungspaket ab.
Der Release-Benutzer fordert Sie dann auf, zu bestätigen, dass er das richtige Erweiterungspaket gefunden hat, das Sie für die private Verfügbarkeit freigeben möchten.

Wenn Sie Ihre Erweiterung mit privater Verfügbarkeit direkt über die API freigeben möchten, finden Sie weitere Details im Beispielaufruf für die [private Freigabe eines Erweiterungspakets](/help/tags/api/endpoints/extension-packages.md#private-release) in den API-Dokumenten.

## Öffentliche Freigabe

Sobald Sie die private Freigabe abgeschlossen haben, können Sie Adobe um die öffentliche Freigabe bitten.  Dadurch wird Ihre Erweiterung im öffentlichen Katalog verfügbar gemacht. Jeder Nutzer der Datenerfassung kann Ihre Erweiterung für jede Eigenschaft installieren.

Bitte füllen Sie das [Anfrageformular für eine öffentliche Freigabe](https://www.feedbackprogram.adobe.com/c/r/DCExtensionReleaseRequest) aus, um den Freigabeprozess zu starten.
