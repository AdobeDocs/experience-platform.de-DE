---
title: Google Cloud Platform-Erweiterung zur Ereignisweiterleitung
description: Diese Ereignisweiterleitungs-Erweiterung von Adobe Experience Platform sendet Edge Network-Ereignisse an Google Cloud Platform.
last-substantial-update: 2023-06-21T00:00:00Z
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 4%

---

# [!DNL Google Cloud Platform]-Erweiterung zur Ereignisweiterleitung

[[!DNL Google Cloud Platform]](https://cloud.google.com/) ist eine Cloud-Computing-Plattform, die eine breite Palette von Dienstleistungen anbietet, wie z. B. dezentrales Computing, Datenbankspeicherung, Inhaltsbereitstellung und SaaS-Integrationsdienste (Software-as-a-Service) für Customer Relationship Management (CRM) und Enterprise Resource Planning (ERP).

Die [!DNL Google Cloud Platform] [Ereignisweiterleitung](../../../ui/event-forwarding/overview.md) Erweiterungsnutzungen [[!DNL Cloud Pub/Sub]](https://cloud.google.com/pubsub) , um Ereignisse vom Adobe Experience Platform Edge Network an die [!DNL Google Cloud Platform] zur weiteren Verarbeitung bestimmt. In diesem Handbuch wird beschrieben, wie Sie die Erweiterung installieren und ihre Funktionen in einer Ereignisweiterleitungsregel verwenden.

## Voraussetzungen

Um diese Erweiterung verwenden zu können, müssen Sie über eine [!DNL Google Cloud Platform] -Konto mit [!DNL Cloud Pub/Sub] Thema. Wenn Sie kein bereits vorhandenes Thema haben, finden Sie weitere Informationen unter [[!DNL Google Cloud Platform]](https://cloud.google.com/pubsub/docs/create-topic) Dokumentation zum Erstellen und Verwalten von Themen.

### Erstellen eines Geheimnisses und eines Datenelements

Erstellen Sie zunächst eine neue `Google OAuth 2` [Ereignisweiterleitungsgeheimnis](../../../ui/event-forwarding/secrets.md), die verwendet wird, um die Verbindung zu Ihrem Konto zu authentifizieren, während der Wert geschützt bleibt.

Als Nächstes [Datenelement erstellen](../../../ui/managing-resources/data-elements.md#create-a-data-element) mithilfe der **[!UICONTROL Core]** Erweiterung und **[!UICONTROL Geheimnis]** Datenelementtyp zum Referenzieren der `Google OAuth 2` geheim, das Sie gerade erstellt haben.

## Installieren und konfigurieren Sie die [!DNL Google Cloud Platform] Erweiterung {#install}

So installieren Sie die Erweiterung: [Erstellen einer Ereignisweiterleitungs-Eigenschaft](../../../ui/event-forwarding/overview.md#properties) oder wählen Sie eine vorhandene Eigenschaft aus, die Sie stattdessen bearbeiten möchten.

Wählen Sie **[!UICONTROL Erweiterungen]** in der linken Navigation aus. Im **[!UICONTROL Katalog]** Registerkarte auswählen **[!UICONTROL Installieren]** auf der Karte für die [!DNL Google Cloud Platform] -Erweiterung.

![Der Katalog [!DNL Google Cloud Platform] Erweiterungsmarkierungsinstallation.](../../../images/extensions/server/google-cloud-platform/install-extension.png)

Geben Sie auf dem Konfigurationsbildschirm das Datenelement-Geheimnis ein, das Sie zuvor in der Variablen **[!UICONTROL Zugriffstoken]** -Feld. Das Datenelement-Geheimnis enthält Ihre [!DNL Google Cloud Platform] OAuth 2-Token. Wählen Sie **[!UICONTROL Speichern]**, wenn Sie fertig sind.

![Die [!DNL Google Cloud Platform] Erweiterungskonfigurationsseite.](../../../images/extensions/server/google-cloud-platform/configure-extension.png)

## Erstellen Sie eine [!DNL Send Data to Cloud Pub/Sub] Regel {#tracking-rule}

Nachdem die Erweiterung installiert wurde, erstellen Sie eine neue Ereignisweiterleitung [Regel](../../../ui/managing-resources/rules.md) und konfigurieren Sie die Bedingungen nach Bedarf. Wählen Sie beim Konfigurieren der Aktionen für die Regel die **[!UICONTROL Google Cloud Platform]** Erweiterung und wählen Sie **[!UICONTROL Daten an Cloud-Pub/Sub senden]** für den Aktionstyp.

![Die Ansicht für die Aktionskonfiguration für [!UICONTROL Google Cloud Platform], wobei die Aktion hervorgehoben und [!UICONTROL Daten an Cloud-Pub/Sub senden].](../../../images/extensions/server/google-cloud-platform/event-action.png)

| Eingabe | Beschreibung |
| --- | --- |
| [!UICONTROL Thema] | Das Thema, das die Ereignisse von der Ereignisweiterleitung erhält. Der Wert muss das Format aufweisen `projects/{projectName}/topics/{topicName}`. |
| [!UICONTROL Daten] | Dieses Feld enthält die Daten, die an die [!DNL Cloud Pub/Sub] Thema im JSON-Format.<br><br>Unter dem **[!UICONTROL Roh]** können Sie das JSON-Objekt direkt in das bereitgestellte Textfeld einfügen oder das Datenelementsymbol (![Datensatzsymbol](../../../images/extensions/server/aws/data-element-icon.png)), um aus einer Liste vorhandener Datenelemente zur Darstellung der Daten auszuwählen.<br><br>Sie können auch die **[!UICONTROL JSON-Schlüssel-Wert-Paare-Editor]** Option zum manuellen Hinzufügen jedes Schlüssel-Wert-Paares über einen UI-Editor. Jeder Wert kann durch eine Roheingabe dargestellt werden oder stattdessen kann ein Datenelement ausgewählt werden. |
| [!UICONTROL Attribute] | Dieses Feld enthält das JSON-Objekt mit zusätzlichen Attributen, die zusammen mit der Nachricht gesendet werden.<br><br>Unter dem **[!UICONTROL Roh]** können Sie das JSON-Objekt direkt in das bereitgestellte Textfeld einfügen oder das Datenelementsymbol (![Datensatzsymbol](../../../images/extensions/server/aws/data-element-icon.png)), um aus einer Liste vorhandener Datenelemente zur Darstellung der Daten auszuwählen.<br><br>Sie können auch die **[!UICONTROL JSON-Schlüssel-Wert-Paare-Editor]** Option zum manuellen Hinzufügen jedes Schlüssel-Wert-Paares über einen UI-Editor. Jeder Wert kann durch eine Roheingabe dargestellt werden oder stattdessen kann ein Datenelement ausgewählt werden. |

{style="table-layout:auto"}

## Nächste Schritte

In diesem Handbuch wird beschrieben, wie Daten an [!DNL Cloud Pub/Sub] mithilfe der [!DNL Google Cloud Platform] Ereignisweiterleitungserweiterung. Weiterführende Informationen zu Ereignisweiterleitungsfunktionen in Experience Platform finden Sie im Abschnitt [Übersicht über die Ereignisweiterleitung](../../../ui/event-forwarding/overview.md).