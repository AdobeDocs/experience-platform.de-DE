---
keywords: Experience Platform;Profil;Echtzeit-Kundenprofil;Fehlerbehebung;API;
title: Erste Schritte mit der Echtzeit-Kundenprofil-API
type: Documentation
description: In den ersten Schritten mit der Profil-API werden die wichtigsten Konzepte und grundlegenden Funktionen beschrieben, die Sie kennen müssen, um mit Endpunkten der Echtzeit-Kundenprofil-API grundlegende CRUD-Vorgänge für Profildaten durchführen zu können.
role: Developer
exl-id: 7e30610a-a7e7-43ab-a45d-fd84ef6e36ef
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 50%

---

# Erste Schritte mit der [!DNL Real-Time Customer Profile]-API {#getting-started}

Mithilfe von Endpunkten der Echtzeit-Kundenprofil-API können Sie grundlegende CRUD-Vorgänge für Profildaten durchführen, z. B. berechnete Attribute konfigurieren, auf Entitäten zugreifen, Profildaten exportieren und nicht benötigte Datensätze oder Batches löschen.

Dieses Entwicklerhandbuch setzt Grundkenntnisse der verschiedenen Adobe Experience Platform-Services voraus, die an der Arbeit mit [!DNL Profile] beteiligt sind. Bevor Sie die [!DNL Real-Time Customer Profile]-API nutzen, lesen Sie die Dokumentation für folgende Services:

* [[!DNL Real-Time Customer Profile]](../home.md): Bietet ein einheitliches Kundenprofil in Echtzeit, das auf aggregierten Daten aus verschiedenen Quellen basiert.
* [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Verschaffen Sie sich einen besseren Überblick über Ihre Kundinnen und Kunden und deren Verhalten, indem Sie Identitäten geräte- und systemübergreifend verknüpfen.
* [[!DNL Adobe Experience Platform Segmentation Service]](../../segmentation/home.md): Ermöglicht das Erstellen von Zielgruppen aus Echtzeit-Kundenprofildaten.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten von Platform organisiert werden.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um [!DNL Profile] API-Endpunkte erfolgreich aufrufen zu können.

## Lesen von Beispiel-API-Aufrufen

In der Dokumentation zur [!DNL Real-Time Customer Profile]-API wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

## Erforderliche Kopfzeilen

Außerdem setzt die API-Dokumentation voraus, dass Sie das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abgeschlossen haben, um [!DNL Platform]-Endpunkte erfolgreich aufrufen zu können. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Anfragen an [!DNL Platform]-APIs erfordern eine Kopfzeile, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

* `x-sandbox-name: {SANDBOX_NAME}`

Weitere Informationen zu Sandboxes in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Alle Anfragen mit einer Payload im Anfragetext (wie POST-, PUT- und PATCH-Aufrufe) müssen eine `Content-Type`-Kopfzeile enthalten. Akzeptierte Werte, die für jeden Aufruf spezifisch sind, werden in den Aufrufparametern angegeben.

## Nächste Schritte

Um mit dem Aufrufen der [!DNL Real-Time Customer Profile]-API zu beginnen, wählen Sie eines der verfügbaren Handbücher zu Endpunkten.
