---
description: Erfahren Sie, wie Sie mit der dateibasierten Zieltest-API die Konfiguration Ihrer dateibasierten Ziele überprüfen können, die durch das Destination SDK erstellt wurden.
title: Dateibasierte Zieltest-API
exl-id: 2733fd00-af08-4763-a30e-a53ee56c0a19
source-git-commit: adf75720f3e13c066b5c244d6749dd0939865a6f
workflow-type: ht
source-wordcount: '381'
ht-degree: 100%

---


# Übersicht über die dateibasierte Zieltest-API

Die dateibasierte Zieltest-API ist ein Satz von Endpunkten, mit denen Sie die Konfiguration Ihrer dateibasierten Ziele überprüfen können, die über das Destination SDK erstellt wurden.

Es wird empfohlen, diese Tools zu verwenden, um Ihre Konfiguration zu validieren, bevor Sie Ihr Ziel zur Überprüfung an Adobe [übermitteln](../../guides/submit-destination.md).

Für die besten Testergebnisse empfehlen wir die Verwendung dieser API basierend auf dem unten stehenden Flussdiagramm.

![Diagramm mit dem empfohlenen Zieltestfluss](../../assets/testing-api/batch-destinations/file-based-testing-flow.png)

In den folgenden Abschnitten finden Sie einen kurzen Überblick darüber, was jeder Endpunkt tun kann.

## Generieren von Beispielprofilen {#generate-sample-profiles}

Verwenden Sie den API-Endpunkt `/sample-profiles` zum Generieren von Beispielprofilen basierend auf Ihrem vorhandenen Quellschema.

Beispielprofile können Ihnen dabei helfen, die JSON-Struktur eines Profils zu verstehen. Darüber hinaus erhalten Sie eine Standardeinstellung, die Sie mit Ihren eigenen Profildaten anpassen können, um weitere Zieltests durchzuführen.

In der [dedizierten Dokumentation](file-based-sample-profile-generation-api.md) erfahren Sie, wie Sie Beispielprofile generieren.

## Konfiguration von Testzielen {#test-destination-configuration}

Verwenden Sie den API-Endpunkt `/testing/destinationInstance`, um zu testen, ob Ihr dateibasiertes Ziel richtig konfiguriert ist, und um die Integrität der Datenflüsse zu Ihrem konfigurierten Ziel zu überprüfen.

Sie können Anfragen an den Test-Endpunkt mit oder ohne Hinzufügen von [Beispielprofilen](file-based-sample-profile-generation-api.md) an den Aufruf stellen. Wenn Sie bei der Anfrage keine Profile senden, generiert die API automatisch ein Beispielprofil und fügt es der Anfrage hinzu.

In der [dedizierten Dokumentation](file-based-destination-testing-api.md) erfahren Sie, wie Sie Ihre Zielkonfiguration mit Beispielprofilen testen können.

## Anzeigen detaillierter Aktivierungsergebnisse {#view-detailed-activation-results}

Verwenden Sie den API-Endpunkt `/testing/destinationInstance`, um die vollständigen Details Ihrer dateibasierten Zieltestergebnisse anzuzeigen.

Dieser API-Endpunkt gibt dasselbe Ergebnis zurück, das Sie bei Verwendung der [Flow Service-API](../../../api/update-destination-dataflows.md) zur Überwachung von Datenflüssen erhalten würden.

In der [dedizierten Dokumentation](file-based-destination-results-api.md) erfahren Sie, wie Sie detaillierte Aktivierungsergebnisse anzeigen können.

## Rendern von Kundendatenfeldern {#render-customer-data-fields}

Verwenden Sie den API-Endpunkt `/authoring/testing/template/render`, um zu sehen, wie die in Ihrer Zielkonfiguration definierten, auf Vorlagen basierenden [Kundendatenfelder](../../functionality/destination-configuration/customer-data-fields.md) aussehen würden.

Der API-Endpunkt generiert zufällige Werte für Ihre Kundendatenfelder und gibt sie in der Antwort zurück. Auf diese Weise können Sie die semantische Struktur von Kundendatenfeldern wie Behälternamen oder Ordnerpfaden überprüfen.

In der [dedizierten Dokumentation](file-based-render-template-api.md) erfahren Sie, wie Sie Werte für Ihre Kundendatenfelder generieren und visualisieren können.
