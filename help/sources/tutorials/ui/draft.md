---
title: Datenfluss-Entwurf in der Benutzeroberfläche
description: Erfahren Sie, wie Sie Ihre Datenflüsse bei Verwendung des Arbeitsbereichs "Quellen"als Entwurf speichern und später veröffentlichen können.
exl-id: ee00798e-152a-4618-acb3-db40f2f55fae
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 7%

---

# Datenfluss-Entwurf in der Benutzeroberfläche

Speichern Sie den Fortschritt des nicht abgeschlossenen Datenerfassungs-Workflows, indem Sie Ihren Datenfluss auf den Entwurfsstatus setzen. Sie können Ihre entworfenen Datenflüsse zu einem späteren Zeitpunkt fortsetzen und abschließen.

In diesem Dokument wird beschrieben, wie Sie Ihre Datenflüsse speichern, wenn Sie den Arbeitsbereich &quot;Quellen&quot;in der Benutzeroberfläche von Adobe Experience Platform verwenden.

## Erste Schritte

Dieses Dokument setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.

## Speichern eines Datenflusses als Entwurf

Sie können den Erstellungsfortschritt des Datenflusses jederzeit anhalten, nachdem Sie die Daten ausgewählt haben, die Sie in Platform einbringen werden.

Wenn Sie beispielsweise den Fortschritt während des Datenfluss-Detailschritts speichern möchten, wählen Sie **[!UICONTROL Als Entwurf speichern]** aus.

![Der Schritt &quot;Datenfluss-Detail&quot;des Ursprungs-Workflows mit ausgewähltem Speicherungsentwurf.](../../images/tutorials/draft/save-as-draft.png)

Nachdem Sie Ihren Entwurf gespeichert haben, gelangen Sie zur Seite Ihres Kontos, auf der Sie eine Liste Ihrer vorhandenen Datenflüsse einschließlich Ihrer Entwürfe sehen können.

![Eine Liste der Datenflüsse für ein bestimmtes Konto.](../../images/tutorials/draft/draft-dataflow.png)

>[!TIP]
>
>Entworfene Datenflüsse werden nicht aktiviert und haben ihren Status auf `draft` eingestellt.

Um mit dem Entwurf fortzufahren, wählen Sie die Auslassungszeichen (`...`) neben dem Namen Ihres Datenflusses und dann **[!UICONTROL Datenfluss aktualisieren]** aus.

>[!NOTE]
>
>Wenn Ihr Entwurf Planungsinformationen enthält, erhalten Sie im Dropdown-Fenster auch die Option **[!UICONTROL Zeitplan bearbeiten]**.

![Ein Dropdown-Fenster mit ausgewähltem Aktualisierungs-Datenfluss.](../../images/tutorials/draft/update-dataflow.png)

### Entwürfe aus dem Quellkatalog aufrufen

Sie können auch über den Datenflusskatalog auf Ihre Datenflussentwürfe zugreifen. Wählen Sie **[!UICONTROL Datenflüsse]** aus der oberen Kopfzeile aus, um auf den Datenflusses-Katalog zuzugreifen. Suchen Sie hier Ihren Entwurf aus der Liste der vorhandenen Datenflüsse in Ihrer Organisation, wählen Sie die Auslassungszeichen (`...`) neben dem Namen aus und wählen Sie dann **[!UICONTROL Datenfluss aktualisieren]** aus.

![Eine Liste der Datenflüsse für eine bestimmte Organisation.](../../images/tutorials/draft/catalog-access.png)

## Veröffentlichen des Datenflussentwurfs

Sie werden zum Schritt [!UICONTROL Daten hinzufügen] des Ursprungs-Workflows zurückgeleitet, wo Sie das Format Ihrer Daten erneut bestätigen und mit dem Datenfluss fortfahren können.

Nachdem Sie den Formatierungs-, Trennzeichen- und Komprimierungstyp Ihrer Daten bestätigt haben, wählen Sie **[!UICONTROL Weiter]** aus, um fortzufahren.

![Der Schritt zum Hinzufügen von Daten des Ursprungs-Workflows.](../../images/tutorials/draft/select-data.png)

Bestätigen Sie als Nächstes Ihre Datenfluss-Details. Verwenden Sie die Oberfläche mit den Datenfluss-Details , um Konfigurationen zu aktualisieren, die den Namen, die Beschreibung, die partielle Erfassung, die Fehlerdiagnoseinstellungen und die Voreinstellungen für Warnhinweise umgeben.

Nachdem Sie die Konfigurationen abgeschlossen haben, wählen Sie **[!UICONTROL Weiter]** aus, um fortzufahren.

![Der Schritt &quot;Datenfluss-Detail&quot;des Ursprungs-Workflows.](../../images/tutorials/draft/dataflow-detail.png)

Der Schritt [!UICONTROL Zuordnung] wird angezeigt. In diesem Schritt können Sie die Zuordnungskonfigurationen Ihres Datenflusses neu konfigurieren. Eine umfassende Anleitung zu den für die Zuordnung verwendeten Datenvorbereitungsfunktionen finden Sie im [Benutzeroberflächen-Handbuch zur Datenvorbereitung](../../../data-prep/ui/mapping.md) .

Nachdem Sie die Neukonfiguration der Zuordnung abgeschlossen haben, wählen Sie **[!UICONTROL Weiter]** aus, um fortzufahren.

![Der Zuordnungsschritt des Ursprungs-Workflows.](../../images/tutorials/draft/mapping.png)

Verwenden Sie den Schritt [!UICONTROL Planung] , um einen Aufnahmezeitplan für Ihren Datenfluss festzulegen. Sie können die Aufnahmefrequenz auf `once`, `minute`, `hour`, `day` oder `week` festlegen. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Weiter]** aus, um fortzufahren.

![Der Planungsschritt des Ursprungs-Workflows.](../../images/tutorials/draft/scheduling.png)

Überprüfen Sie abschließend die Details Ihres Datenflusses und wählen Sie dann **[!UICONTROL Fertigstellen]** aus, um Ihren Entwurf zu veröffentlichen.

![Der Überprüfungsschritt des Ursprungs-Workflows.](../../images/tutorials/draft/review.png)

Nachdem Sie einen Entwurf gespeichert und veröffentlicht haben, wird der Datenfluss aktiviert und Sie können ihn nicht mehr als Entwurf zurücksetzen.

## Nächste Schritte

In diesem Tutorial haben Sie gelernt, wie Sie Ihren Fortschritt speichern und einen Datenfluss als Entwurf festlegen können. Weitere Informationen zu Quellen finden Sie in der [Quellenübersicht](../../home.md).
