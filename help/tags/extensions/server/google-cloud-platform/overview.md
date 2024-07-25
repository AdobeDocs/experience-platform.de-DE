---
title: Google Cloud Platform-Erweiterung zur Ereignisweiterleitung
description: Diese Ereignisweiterleitungs-Erweiterung von Adobe Experience Platform sendet Edge Network-Ereignisse an Google Cloud Platform.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: c5da1889-f917-42aa-b3a4-9557c31d6ee8
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 3%

---

# [!DNL Google Cloud Platform]-Erweiterung zur Ereignisweiterleitung

[[!DNL Google Cloud Platform]](https://cloud.google.com/) ist eine Cloud-Computing-Plattform, die eine Vielzahl von Diensten anbietet, wie z. B. dezentrales Computing, Datenbankspeicherung, Inhaltsbereitstellung und SaaS-Integrationsdienste (Software-as-a-Service) für Customer Relationship Management (CRM) und Enterprise Resource Planning (ERP).

Die Erweiterung [!DNL Google Cloud Platform] [ Ereignisweiterleitung](../../../ui/event-forwarding/overview.md) nutzt [[!DNL Cloud Pub/Sub]](https://cloud.google.com/pubsub) , um Ereignisse vom Adobe Experience Platform-Edge Network zur weiteren Verarbeitung an die [!DNL Google Cloud Platform] zu senden. In diesem Handbuch wird beschrieben, wie Sie die Erweiterung installieren und ihre Funktionen in einer Ereignisweiterleitungsregel verwenden.

## Voraussetzungen

Um diese Erweiterung verwenden zu können, müssen Sie über ein [!DNL Google Cloud Platform] -Konto mit einem vorhandenen [!DNL Cloud Pub/Sub] -Thema verfügen. Wenn Sie kein bereits vorhandenes Thema haben, lesen Sie die [[!DNL Google Cloud Platform]](https://cloud.google.com/pubsub/docs/create-topic) -Dokumentation zum Erstellen und Verwalten von Themen.

### Erstellen eines Geheimnisses und eines Datenelements

Erstellen Sie zunächst ein neues `Google OAuth 2` [Ereignisweiterleitungsgeheimnis](../../../ui/event-forwarding/secrets.md), das verwendet wird, um die Verbindung zu Ihrem Konto zu authentifizieren, während der Wert geschützt bleibt.

Als Nächstes erstellen Sie mit der Erweiterung **[!UICONTROL Core]** ein Datenelement](../../../ui/managing-resources/data-elements.md#create-a-data-element) und mit dem Datenelementtyp **[!UICONTROL Secret]** , um auf das soeben erstellte Geheimnis `Google OAuth 2` zu verweisen.[

## Installieren und Konfigurieren der [!DNL Google Cloud Platform] -Erweiterung {#install}

Um die Erweiterung zu installieren, erstellen Sie [eine Ereignisweiterleitungs-Eigenschaft](../../../ui/event-forwarding/overview.md#properties) oder wählen Sie eine vorhandene Eigenschaft aus, die Sie stattdessen bearbeiten möchten.

Wählen Sie **[!UICONTROL Erweiterungen]** in der linken Navigation aus. Wählen Sie auf der Registerkarte **[!UICONTROL Katalog]** die Option **[!UICONTROL Installieren]** auf der Karte für die Erweiterung [!DNL Google Cloud Platform] aus.

![Die Katalogerweiterung [!DNL Google Cloud Platform], die die Installation hervorhebt.](../../../images/extensions/server/google-cloud-platform/install-extension.png)

Geben Sie auf dem Konfigurationsbildschirm im Feld **[!UICONTROL Zugriffstoken]** das Datenelementgeheimnis ein, das Sie zuvor erstellt haben. Das Datenelement-Geheimnis enthält Ihr [!DNL Google Cloud Platform] OAuth 2-Token. Wählen Sie **[!UICONTROL Speichern]**, wenn Sie fertig sind.

![Die Konfigurationsseite der [!DNL Google Cloud Platform] Erweiterung.](../../../images/extensions/server/google-cloud-platform/configure-extension.png)

## Erstellen einer [!DNL Send Data to Cloud Pub/Sub] -Regel {#tracking-rule}

Nachdem die Erweiterung installiert wurde, erstellen Sie eine neue Ereignisweiterleitung mit dem Namen [Regel](../../../ui/managing-resources/rules.md) und konfigurieren Sie die zugehörigen Bedingungen nach Bedarf. Wählen Sie beim Konfigurieren der Aktionen für die Regel die Erweiterung &quot;**[!UICONTROL Google Cloud Platform]**&quot;und dann für den Aktionstyp &quot;**[!UICONTROL Daten an Cloud-Pub/Sub senden]**&quot;.

![Die Aktionskonfigurationsansicht für [!UICONTROL Google Cloud Platform], wobei die Aktion hervorgehoben ist und [!UICONTROL Daten an Cloud-Pub/Sub senden]](../../../images/extensions/server/google-cloud-platform/event-action.png).

| Eingabe | Beschreibung |
| --- | --- |
| [!UICONTROL Thema] | Das Thema, das die Ereignisse von der Ereignisweiterleitung erhält. Der Wert muss das Format `projects/{projectName}/topics/{topicName}` aufweisen. |
| [!UICONTROL Daten] | Dieses Feld enthält die Daten, die im JSON-Format an das Thema [!DNL Cloud Pub/Sub] weitergeleitet werden sollen.<br><br>Unter der Option **[!UICONTROL Raw]** können Sie das JSON-Objekt direkt in das bereitgestellte Textfeld einfügen. Alternativ können Sie das Datenelementsymbol (![Datensatzsymbol](/help/images/icons/database.png)) auswählen, das aus einer Liste vorhandener Datenelemente ausgewählt werden soll, um die Daten darzustellen.<br><br>Sie können auch die Option **[!UICONTROL JSON Key-Value Paares Editor]** verwenden, um jedes Schlüssel-Wert-Paar manuell über einen UI-Editor hinzuzufügen. Jeder Wert kann durch eine Roheingabe dargestellt werden oder stattdessen kann ein Datenelement ausgewählt werden. |
| [!UICONTROL Attribute] | Dieses Feld enthält das JSON-Objekt mit zusätzlichen Attributen, die zusammen mit der Nachricht gesendet werden.<br><br>Unter der Option **[!UICONTROL Raw]** können Sie das JSON-Objekt direkt in das bereitgestellte Textfeld einfügen. Alternativ können Sie das Datenelementsymbol (![Datensatzsymbol](/help/images/icons/database.png)) auswählen, das aus einer Liste vorhandener Datenelemente ausgewählt werden soll, um die Daten darzustellen.<br><br>Sie können auch die Option **[!UICONTROL JSON Key-Value Paares Editor]** verwenden, um jedes Schlüssel-Wert-Paar manuell über einen UI-Editor hinzuzufügen. Jeder Wert kann durch eine Roheingabe dargestellt werden oder stattdessen kann ein Datenelement ausgewählt werden. |

{style="table-layout:auto"}

## Nächste Schritte

In diesem Handbuch wird beschrieben, wie Daten mithilfe der Ereignisweiterleitungs-Erweiterung [!DNL Google Cloud Platform] an [!DNL Cloud Pub/Sub] gesendet werden. Weiterführende Informationen zu Ereignisweiterleitungsfunktionen in Experience Platform finden Sie in der [Übersicht über die Ereignisweiterleitung](../../../ui/event-forwarding/overview.md).
