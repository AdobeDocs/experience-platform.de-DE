---
keywords: Experience Platform;home;popular topics;Google PubSub;google pubsub
solution: Experience Platform
title: Erstellen einer Google PubSub-Source-Verbindung in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie einen Google PubSub-Quell-Connector über die Platform-Benutzeroberfläche erstellen.
exl-id: fb8411f2-ccae-4bb5-b1bf-52b1144534ed
source-git-commit: da7b6fe8f9d274b8e5f27138a1baf8caf63a0c01
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 9%

---

# Erstellen Sie eine [!DNL Google PubSub] Quellverbindung in der Benutzeroberfläche

In diesem Tutorial werden Schritte zum Erstellen eines [!DNL Google PubSub] (nachstehend &quot;genannt)[!DNL PubSub]&quot;) über die Benutzeroberfläche von Platform.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Platform-Diensten zu strukturieren, zu beschriften und zu erweitern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Anwendungen für digitale Erlebnisse entwickeln und weiterentwickeln können.

Wenn Sie bereits über eine gültige [!DNL PubSub] Verbindung nutzen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Datenfluss konfigurieren](../../dataflow/batch/cloud-storage.md).

### Erforderliche Anmeldedaten sammeln

Um eine Verbindung herzustellen [!DNL PubSub] in Platform einen gültigen Wert für die folgenden Anmeldeinformationen angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `projectId` | Die zum Authentifizieren erforderliche Projekt-ID [!DNL PubSub]. |
| `credentials` | Die für die Authentifizierung erforderliche Kennung der Anmeldedaten oder des privaten Schlüssels [!DNL PubSub]. |

Weitere Informationen zu diesen Werten finden Sie in den folgenden [PubSub-Authentifizierung](https://cloud.google.com/pubsub/docs/authentication) Dokument. Wenn Sie die dienstkontenbasierte Authentifizierung verwenden, lesen Sie Folgendes [PubSub-Handbuch](https://cloud.google.com/docs/authentication/production#create_service_account) für Schritte zum Generieren Ihrer Anmeldedaten.

>[!TIP]
>
>Wenn Sie auf Dienstkonten basierende Authentifizierung verwenden, stellen Sie sicher, dass Sie ausreichend Benutzerzugriff auf Ihr Dienstkonto gewährt haben und dass im JSON keine zusätzlichen Leerzeichen vorhanden sind, wenn Sie Ihre Anmeldeinformationen kopieren und einfügen.

Nachdem Sie die erforderlichen Anmeldedaten erfasst haben, können Sie die folgenden Schritte ausführen, um Ihre [!DNL PubSub] -Konto auf Platform.

## Verbinden Sie Ihre [!DNL PubSub] account

Im [Platform-Benutzeroberfläche](https://platform.adobe.com)auswählen **[!UICONTROL Quellen]** über die linke Navigationsleiste, um auf die [!UICONTROL Quellen] Arbeitsbereich. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle über die Suchleiste finden.

Unter dem [!UICONTROL Cloud-Speicher] category, select **[!UICONTROL Google PubSub]** und wählen Sie **[!UICONTROL Daten hinzufügen]**.

![Katalog](../../../../images/tutorials/create/google-pubsub/catalog.png)

Die **[!UICONTROL Mit Google PubSub verbinden]** angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie die [!DNL PubSub] Konto, mit dem Sie einen neuen Datenfluss erstellen möchten, wählen Sie **[!UICONTROL Nächste]** um fortzufahren.

![vorhandene](../../../../images/tutorials/create/google-pubsub/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen, eine optionale Beschreibung und Ihre [!DNL PubSub] Authentifizierungsberechtigungen für das Formular. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Verbindung mit Quelle herstellen]** und dann etwas Zeit für die Einrichtung der neuen Verbindung.

![new](../../../../images/tutorials/create/google-pubsub/new.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung zwischen Ihrem [!DNL PubSub] -Konto und -Plattform. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Streaming-Daten aus Ihrem Cloud-Speicher in Platform zu übertragen](../../dataflow/streaming/cloud-storage-streaming.md).
