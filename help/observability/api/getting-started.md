---
keywords: Experience Platform;home;popular topics;date range
solution: Experience Platform
title: Erste Schritte mit der Observability Insights API
topic: developer guide
description: Mit der Observability Insights-API können Sie Metrikdaten zu verschiedenen Adobe Experience Platform-Funktionen abrufen. In diesem Dokument erhalten Sie eine Einführung in die wichtigsten Konzepte, die Sie kennen müssen, bevor Sie Aufrufe an die Observability Insights-API durchführen.
translation-type: tm+mt
source-git-commit: c5455dc0812b251483170ac19506d7c60ad4ecaa
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 25%

---


# Getting started with the [!DNL Observability Insights] API

Mit der [!DNL Observability Insights] API können Sie Metrikdaten zu verschiedenen Adobe Experience Platform-Funktionen abrufen. This document provides an introduction to the core concepts you need to know before attempting to make calls to the [!DNL Observability Insights] API.

## Lesen von Beispiel-API-Aufrufen

The [!DNL Observability Insights] API documentation provides example API calls to demonstrate how to format your requests. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. For information on the conventions used in documentation for sample API calls, see the section on how to read example API calls in the [Experience Platform troubleshooting guide](../../landing/troubleshooting.md).

## Erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](../../tutorials/authentication.md) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in. For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

## Nächste Schritte

Um mit dem Aufrufen der [!DNL Observability Insights] API zu beginnen, fahren Sie mit der [Metriken-Endpunktanleitung](./metrics.md)fort.