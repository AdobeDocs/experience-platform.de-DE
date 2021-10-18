---
keywords: Experience Platform;home;popular topics;Google PubSub;google pubsub
solution: Experience Platform
title: Erstellen einer Google PubSub-Source-Verbindung in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie einen Google PubSub-Quell-Connector über die Platform-Benutzeroberfläche erstellen.
exl-id: fb8411f2-ccae-4bb5-b1bf-52b1144534ed
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 9%

---

# Erstellen einer [!DNL Google PubSub]-Quellverbindung in der Benutzeroberfläche

>[!NOTE]
>
> Der Connector [!DNL Google PubSub] befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectoren finden Sie unter [Quellen - Übersicht](../../../../home.md#terms-and-conditions) .

In diesem Tutorial werden Schritte zum Erstellen eines [!DNL Google PubSub] (nachfolgend als &quot;[!DNL PubSub]&quot;bezeichnet) mithilfe der Platform-Benutzeroberfläche beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Platform-Diensten zu strukturieren, zu beschriften und zu erweitern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Anwendungen für digitale Erlebnisse entwickeln und weiterentwickeln können.

Wenn Sie bereits über eine gültige [!DNL PubSub]-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum Konfigurieren eines Datenflusses [fortfahren.](../../dataflow/batch/cloud-storage.md)

### Erforderliche Anmeldedaten sammeln

Um [!DNL PubSub] mit Platform zu verbinden, müssen Sie einen gültigen Wert für die folgenden Anmeldedaten angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `projectId` | Die Projekt-ID, die zum Authentifizieren von [!DNL PubSub] erforderlich ist. |
| `credentials` | Die Kennung der Anmeldedaten oder des privaten Schlüssels, die für die Authentifizierung von [!DNL PubSub] erforderlich ist. |

Weitere Informationen zu diesen Werten finden Sie im folgenden Dokument [PubSub authentication](https://cloud.google.com/pubsub/docs/authentication) . Wenn Sie die dienstkontenbasierte Authentifizierung verwenden, finden Sie im folgenden [PubSub-Handbuch](https://cloud.google.com/docs/authentication/production#create_service_account) Anweisungen zum Generieren Ihrer Anmeldeinformationen.

>[!TIP]
>
>Wenn Sie auf Dienstkonten basierende Authentifizierung verwenden, stellen Sie sicher, dass Sie ausreichend Benutzerzugriff auf Ihr Dienstkonto gewährt haben und dass im JSON keine zusätzlichen Leerzeichen vorhanden sind, wenn Sie Ihre Anmeldeinformationen kopieren und einfügen.

Nachdem Sie die erforderlichen Anmeldedaten gesammelt haben, können Sie die folgenden Schritte ausführen, um Ihr [!DNL PubSub]-Konto mit Platform zu verknüpfen.

## Ihr [!DNL PubSub]-Konto verbinden

Wählen Sie in der [Platform UI](https://platform.adobe.com) **[!UICONTROL Quellen]** aus der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] enthält eine Vielzahl von Quellen, für die Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle über die Suchleiste finden.

Wählen Sie unter der Kategorie [!UICONTROL Cloud-Speicher] die Option **[!UICONTROL Google PubSub]** und klicken Sie dann auf **[!UICONTROL Daten hinzufügen]**.

![Katalog](../../../../images/tutorials/create/google-pubsub/catalog.png)

Die Seite **[!UICONTROL Verbindung mit Google PubSub]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das [!DNL PubSub]-Konto aus, mit dem Sie einen neuen Datenfluss erstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![vorhandene](../../../../images/tutorials/create/google-pubsub/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen, eine optionale Beschreibung und Ihre [!DNL PubSub]-Authentifizierungsdaten im Formular ein. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** aus und lassen Sie dann etwas Zeit für die Einrichtung der neuen Verbindung zu.

![new](../../../../images/tutorials/create/google-pubsub/new.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung zwischen Ihrem [!DNL PubSub]-Konto und Platform hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und [einen Datenfluss konfigurieren, um Streaming-Daten aus Ihrem Cloud-Speicher in Platform](../../dataflow/streaming/cloud-storage-streaming.md) zu übertragen.
