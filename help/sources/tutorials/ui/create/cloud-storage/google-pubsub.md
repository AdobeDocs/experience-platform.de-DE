---
keywords: Experience Platform;Home;beliebte Themen;Google PubSub;Google-Publikum
solution: Experience Platform
title: Erstellen einer Google PubSub-Quellverbindung in der Benutzeroberfläche
topic: Übersicht
type: Tutorial
description: Erfahren Sie, wie Sie einen Google PubSub-Quellanschluss mithilfe der Plattform-Benutzeroberfläche erstellen.
translation-type: tm+mt
source-git-commit: b5358ce206888c413035b46fe751520fd9aefb14
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 9%

---


# Erstellen einer [!DNL Google PubSub]-Quellverbindung in der Benutzeroberfläche

>[!NOTE]
>
> Der [!DNL Google PubSub]-Anschluss befindet sich in der Betaversion. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie unter [Sources overview](../../../../home.md#terms-and-conditions).

In diesem Lernprogramm werden Schritte zum Erstellen eines [!DNL Google PubSub] (nachfolgend als &quot;[!DNL PubSub]&quot;bezeichnet) mithilfe der Plattform-Benutzeroberfläche beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Plattformdiensten zu strukturieren, zu kennzeichnen und zu verbessern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Anwendungen für digitale Erlebnisse entwickeln und weiterentwickeln können.

Wenn Sie bereits über eine gültige [!DNL PubSub]-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial [Konfigurieren eines Datenniedrig](../../dataflow/batch/cloud-storage.md) fortfahren.

### Erforderliche Anmeldedaten sammeln

Um [!DNL PubSub] mit Platform zu verbinden, müssen Sie einen gültigen Wert für die folgenden Anmeldeinformationen angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `projectId` | Die Projekt-ID, die zum Authentifizieren von [!DNL PubSub] erforderlich ist. |
| `credentials` | Die für die Authentifizierung von [!DNL PubSub] erforderliche Berechtigungs- oder private Schlüssel-ID. |

Weitere Informationen zu diesen Werten finden Sie im folgenden Dokument [PubSub authentication](https://cloud.google.com/pubsub/docs/authentication). Wenn Sie die dienstkontobasierte Authentifizierung verwenden, finden Sie im folgenden Handbuch [PubSub](https://cloud.google.com/docs/authentication/production#create_service_account) Anweisungen zum Generieren Ihrer Anmeldeinformationen.

>[!TIP]
>
>Wenn Sie die kontobasierte Authentifizierung eines Dienstes verwenden, stellen Sie sicher, dass Sie ausreichend Benutzerzugriff auf Ihr Dienstkonto gewährt haben und dass keine zusätzlichen Leerzeichen im JSON vorhanden sind, wenn Sie Ihre Anmeldeinformationen kopieren und einfügen.

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, führen Sie die folgenden Schritte aus, um Ihr [!DNL PubSub]-Konto mit der Plattform zu verknüpfen.

## Verbinden Sie Ihr [!DNL PubSub]-Konto

Wählen Sie in der [Plattform-Benutzeroberfläche](https://platform.adobe.com) **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] zeigt eine Reihe von Quellen an, für die Sie ein Konto erstellen können.

Sie können die entsprechende Kategorie im Katalog auf der linken Seite des Bildschirms auswählen. Alternativ können Sie die gewünschte Quelle über die Suchleiste finden.

Wählen Sie unter der Kategorie [!UICONTROL Cloud-Datenspeicherung] **[!UICONTROL Google PubSub]** und dann **[!UICONTROL Hinzufügen data]**.

![Katalog](../../../../images/tutorials/create/google-pubsub/catalog.png)

Die Seite **[!UICONTROL Verbindung mit Google PubSub]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das [!DNL PubSub]-Konto, mit dem Sie einen neuen Datenflug erstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![existing](../../../../images/tutorials/create/google-pubsub/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen, eine optionale Beschreibung und Ihre [!DNL PubSub]-Authentifizierungsdaten im Eingabedatum ein. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und lassen Sie dann etwas Zeit für die Einrichtung der neuen Verbindung zu.

![new](../../../../images/tutorials/create/google-pubsub/new.png)

## Nächste Schritte

In diesem Lernprogramm haben Sie eine Verbindung zwischen Ihrem [!DNL PubSub]-Konto und Ihrer Plattform hergestellt. Sie können nun mit dem nächsten Lernprogramm fortfahren und [einen Datenpfad konfigurieren, um Streaming-Daten aus Ihrer Cloud-Datenspeicherung in Platform](../../dataflow/streaming/cloud-storage-streaming.md) zu übertragen.
