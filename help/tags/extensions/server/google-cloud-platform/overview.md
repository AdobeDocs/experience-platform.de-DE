---
title: Google Cloud Platform-Ereignisweiterleitungserweiterung
description: Diese Adobe Experience Platform-Ereignisweiterleitungserweiterung sendet Edge Network-Ereignisse an Google Cloud Platform.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: c5da1889-f917-42aa-b3a4-9557c31d6ee8
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 3%

---

# [!DNL Google Cloud Platform]-Erweiterung zur Ereignisweiterleitung

[[!DNL Google Cloud Platform]](https://cloud.google.com/) ist eine Cloud-Computing-Plattform, die eine breite Palette von Services wie verteiltes Computing, Datenbankspeicherung, Inhaltsbereitstellung und SaaS-Integrationsservices (Software-as-a-Service) für Customer Relationship Management (CRM) und Enterprise Resource Planning (ERP) bietet.

Die [!DNL Google Cloud Platform] [Ereignisweiterleitung](../../../ui/event-forwarding/overview.md) nutzt [[!DNL Cloud Pub/Sub]](https://cloud.google.com/pubsub), um Ereignisse aus dem Adobe Experience Platform-Edge Network zur weiteren Verarbeitung an die [!DNL Google Cloud Platform] zu senden. In diesem Handbuch wird beschrieben, wie Sie die Erweiterung installieren und ihre Funktionen in einer Ereignisweiterleitungsregel verwenden.

## Voraussetzungen

Um diese Erweiterung verwenden zu können, müssen Sie über ein [!DNL Google Cloud Platform]-Konto mit einem vorhandenen [!DNL Cloud Pub/Sub] verfügen. Wenn Sie noch kein Thema haben, lesen Sie die [[!DNL Google Cloud Platform]](https://cloud.google.com/pubsub/docs/create-topic) Dokumentation zum Erstellen und Verwalten von Themen.

### Erstellen von geheimen Daten und eines Datenelements

Erstellen Sie zunächst ein neues `Google OAuth 2`[Ereignisweiterleitungs-Geheimnis](../../../ui/event-forwarding/secrets.md), das zur Authentifizierung der Verbindung zu Ihrem Konto verwendet wird, während der Wert sicher bleibt.

Als Nächstes erstellen [ mithilfe ](../../../ui/managing-resources/data-elements.md#create-a-data-element) Erweiterung **[!UICONTROL Core]** und eines Datenelementtyps **[!UICONTROL Secret]** ein Datenelement, das auf das soeben erstellte `Google OAuth 2` verweist.

## Installieren und Konfigurieren der [!DNL Google Cloud Platform] {#install}

Um die Erweiterung zu installieren[ erstellen Sie eine Ereignisweiterleitungseigenschaft oder ](../../../ui/event-forwarding/overview.md#properties) Sie stattdessen eine vorhandene Eigenschaft aus, die bearbeitet werden soll.

Wählen Sie **[!UICONTROL Erweiterungen]** in der linken Navigation aus. Wählen Sie auf der **[!UICONTROL Katalog]**-Registerkarte **[!UICONTROL Installieren]** auf der Karte für die [!DNL Google Cloud Platform] aus.

![Die Katalog-[!DNL Google Cloud Platform]-Erweiterung mit hervorgehobener Option „Installieren“](../../../images/extensions/server/google-cloud-platform/install-extension.png)

Geben Sie im Konfigurationsbildschirm das zuvor erstellte Datenelementgeheimnis in das Feld **[!UICONTROL Zugriffstoken]** ein. Das Datenelementgeheimnis enthält Ihr [!DNL Google Cloud Platform] OAuth 2-Token. Wählen Sie **[!UICONTROL Speichern]**, wenn Sie fertig sind.

![Die Konfigurationsseite der [!DNL Google Cloud Platform]-Erweiterung.](../../../images/extensions/server/google-cloud-platform/configure-extension.png)

## Erstellen einer [!DNL Send Data to Cloud Pub/Sub] Regel {#tracking-rule}

Erstellen Sie nach der Installation der Erweiterung eine neue Ereignisweiterleitungsregel [Regel](../../../ui/managing-resources/rules.md) und konfigurieren Sie die Bedingungen nach Bedarf. Wählen Sie beim Konfigurieren der Aktionen für die Regel die Erweiterung **[!UICONTROL Google Cloud Platform]** und wählen Sie dann für den Aktionstyp **[!UICONTROL Daten an Cloud Pub/Sub]**.

![Die Aktionskonfigurationsansicht für [!UICONTROL Google Cloud Platform] mit der hervorgehobenen Aktion [!UICONTROL Daten an Cloud Pub/Sub senden].](../../../images/extensions/server/google-cloud-platform/event-action.png)

| Eingabe | Beschreibung |
| --- | --- |
| [!UICONTROL Thema] | Das Thema, das die Ereignisse von der Ereignisweiterleitung erhält. Der Wert muss das Format `projects/{projectName}/topics/{topicName}` haben. |
| [!UICONTROL Daten] | Dieses Feld enthält die Daten, die im JSON-Format an das [!DNL Cloud Pub/Sub] weitergeleitet werden sollen.<br><br>Unter der Option **[!UICONTROL Raw]** können Sie das JSON-Objekt direkt in das bereitgestellte Textfeld einfügen oder Sie können das Datenelementsymbol (![Datensatzsymbol](/help/images/icons/database.png)) auswählen, um aus einer Liste vorhandener Datenelemente zur Darstellung der Daten auszuwählen.<br><br>Sie können auch die Option **[!UICONTROL JSON-Schlüssel-Wert-Paare-Editor]** verwenden, um jedes Schlüssel-Wert-Paar manuell über einen Benutzeroberflächen-Editor hinzuzufügen. Jeder Wert kann durch eine Roheingabe dargestellt werden oder stattdessen kann ein Datenelement ausgewählt werden. |
| [!UICONTROL Attribute] | Dieses Feld enthält das JSON-Objekt mit zusätzlichen Attributen, die zusammen mit der Nachricht gesendet werden sollen.<br><br>Unter der Option **[!UICONTROL Raw]** können Sie das JSON-Objekt direkt in das bereitgestellte Textfeld einfügen oder Sie können das Datenelementsymbol (![Datensatzsymbol](/help/images/icons/database.png)) auswählen, um aus einer Liste vorhandener Datenelemente zur Darstellung der Daten auszuwählen.<br><br>Sie können auch die Option **[!UICONTROL JSON-Schlüssel-Wert-Paare-Editor]** verwenden, um jedes Schlüssel-Wert-Paar manuell über einen Benutzeroberflächen-Editor hinzuzufügen. Jeder Wert kann durch eine Roheingabe dargestellt werden oder stattdessen kann ein Datenelement ausgewählt werden. |

{style="table-layout:auto"}

## Nächste Schritte

In diesem Handbuch wird beschrieben, wie Sie Daten mithilfe der [!DNL Google Cloud Platform]-Erweiterung für die Ereignisweiterleitung an [!DNL Cloud Pub/Sub] senden. Weitere Informationen zu den Ereignisweiterleitungsfunktionen in Experience Platform finden Sie unter [Übersicht über die Ereignisweiterleitung](../../../ui/event-forwarding/overview.md).
