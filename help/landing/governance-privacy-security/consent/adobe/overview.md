---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Einverständnisverarbeitung in Adobe Experience Platform
description: Erfahren Sie, wie Sie Einverständnissignale von Kunden in Adobe Experience Platform mit dem Adobe 2.0-Standard verarbeiten.
role: Developer
feature: Consent
exl-id: cd76a3f6-ae55-4d75-9b30-900fadb4664f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1573'
ht-degree: 1%

---

# Einverständnisverarbeitung in Adobe Experience Platform

Mit Adobe Experience Platform können Sie die von Ihren Kunden erfassten Einverständnisdaten verarbeiten und in Ihre gespeicherten Kundenprofile integrieren. Diese Daten können dann von nachgelagerten Prozessen verwendet werden, um festzustellen, ob die Datenerfassung für einen bestimmten Kunden erfolgt oder ob dessen Profile für bestimmte Zwecke verwendet werden. Beispielsweise können die Einverständnisdaten für ein bestimmtes Profil bestimmen, ob es in ein exportiertes Zielgruppensegment aufgenommen werden kann oder ob es an bestimmten Marketing-Kanälen wie E-Mail, Textnachrichten oder Push-Benachrichtigungen teilnehmen kann.

Dieses Dokument bietet einen Überblick darüber, wie Sie Ihre Experience Platform-Datenvorgänge konfigurieren können, um von einer Einverständnisverwaltungsplattform (CMP) generierte Kundeneinverständnisdaten aufzunehmen und diese Daten für nachgelagerte Anwendungsfälle in Kundenprofile zu integrieren.

>[!NOTE]
>
>Dieses Dokument konzentriert sich auf die Verarbeitung von Einverständnisdaten unter Verwendung des Adobe-Standards. Wenn Sie Einverständnisdaten in Übereinstimmung mit dem IAB Transparency and Consent Framework (TCF) 2.0 verarbeiten, lesen Sie das Handbuch zur [TCF 2.0-Unterstützung in Adobe Real-Time Customer Data Platform](../iab/overview.md).

## Voraussetzungen

Dieses Handbuch setzt Grundkenntnisse der verschiedenen Experience Platform-Services voraus, die mit der Verarbeitung von Einverständnisdaten zusammenhängen:

* [Experience-Datenmodell (XDM)](/help/xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
* [Adobe Experience Platform Identity Service](/help/identity-service/home.md): Löst das grundlegende Problem der Fragmentierung von Kundenerlebnisdaten, indem Identitäten geräte- und systemübergreifend zusammengeführt werden.
* [Echtzeit-Kundenprofil](/help/profile/home.md): Verwendet [!DNL Identity Service] Funktionen, um aus Ihren Datensätzen in Echtzeit detaillierte Kundenprofile zu erstellen. Das Echtzeit-Kundenprofil ruft Daten aus dem Data Lake ab und speichert Kundenprofile in einem eigenen separaten Datenspeicher.
* [Adobe Experience Platform Web SDK](/help/web-sdk/home.md): Eine Client-seitige JavaScript-Bibliothek, mit der Sie verschiedene Experience Platform-Services in Ihre kundenorientierte Website integrieren können.
   * [SDK-Einverständnisbefehle](../../../../web-sdk/commands/setconsent.md): Ein Überblick über den Anwendungsfall der einverständnisbezogenen SDK-Befehle, die in diesem Handbuch gezeigt werden.
* [Segmentierungs-Service von Adobe Experience Platform](/help/segmentation/home.md): Ermöglicht die Aufteilung von Echtzeit-Kundenprofildaten in Gruppen von Einzelpersonen, die ähnliche Eigenschaften aufweisen und ähnlich auf Marketing-Strategien reagieren.

## Zusammenfassung des Einverständnisverarbeitungsflusses {#summary}

Im Folgenden wird beschrieben, wie Einverständnisdaten verarbeitet werden, nachdem das System ordnungsgemäß konfiguriert wurde:

1. Ein Kunde gibt seine Einverständnisvoreinstellungen für die Datenerfassung über ein Dialogfeld auf Ihrer Website an.
1. Beim Laden jeder Seite (oder wenn Ihr CMP eine Änderung der Einverständnisvoreinstellungen erkennt) ordnet ein benutzerdefiniertes Skript auf Ihrer Site die aktuellen Voreinstellungen einem standardmäßigen XDM-Objekt zu. Dieses Objekt wird dann an den Experience Platform Web SDK-`setConsent` übergeben.
1. Beim Aufruf von `setConsent` prüft Experience Platform Web SDK, ob sich die Einverständniswerte von denen unterscheiden, die es zuletzt erhalten hat. Wenn die Werte unterschiedlich sind (oder es keinen vorherigen Wert gibt), werden die strukturierten Einverständnis-/Präferenzdaten an Adobe Experience Platform gesendet.
1. Die Einverständnis-/Präferenzdaten werden in einen [!DNL Profile] Datensatz aufgenommen, dessen Schema Einverständnis-/Präferenzfelder enthält.

Zusätzlich zu den SDK-Befehlen, die durch CMP-Einverständnisänderungs-Hooks ausgelöst werden, können Einverständnisdaten auch über alle kundengenerierten XDM-Daten in Experience Platform fließen, die direkt in einen [!DNL Profile]-aktivierten Datensatz hochgeladen werden.

### Durchsetzung des Einverständnisses

In der aktuellen Version der Unterstützung für die Einverständnisverarbeitung in Experience Platform wird nur die Datenerfassungsberechtigung (`collect.val`) automatisch von Experience Platform Web SDK durchgesetzt. Während detailliertere Einverständnisse und Voreinstellungen in Kundenprofilen erfasst und beibehalten werden können, müssen diese zusätzlichen Signale in Ihren eigenen nachgelagerten Prozessen manuell durchgesetzt werden.

>[!NOTE]
>
>Weitere Informationen zur Struktur der oben genannten XDM-Einverständnisfelder finden Sie im Handbuch zum Datentyp [[!UICONTROL Einverständnisse und Voreinstellungen] &#x200B;](/help/xdm/data-types/consents.md).

Nachdem das System konfiguriert wurde, interpretiert Experience Platform Web SDK den Einverständniswert für die Datenerfassung für den aktuellen Benutzer, um zu bestimmen, ob die Daten an Adobe Experience Platform Edge Network gesendet, vom Client gelöscht oder beibehalten werden sollen, bis die Datenerfassungsberechtigung auf Ja oder Nein festgelegt ist.

## Bestimmen, wie Kundeneinverständnisdaten in Ihrem CMP generiert werden {#consent-data}

Da jedes CMP-System einzigartig ist, müssen Sie festlegen, wie Ihre Kunden bei der Interaktion mit Ihrem Service am besten ihr Einverständnis erteilen können. Eine gängige Möglichkeit, dies zu erreichen, besteht in der Verwendung eines Cookie-Einverständnisdialogfelds, ähnlich dem folgenden Beispiel:

![](../../../images/governance-privacy-security/consent/adobe/overview/consent-dialog.png)

Dieser Dialog sollte es dem Kunden ermöglichen, sich für bestimmte Marketing- und Personalisierungs-Anwendungsfälle für seine Daten zu registrieren oder daraus auszusteigen. Diese Einverständnisse und Voreinstellungen sollten mit dem Datenmodell übereinstimmen, das Sie im nächsten Schritt für den [!DNL Profile] Datensatz definieren.

## Hinzufügen standardisierter Einverständnisfelder zu einem [!DNL Profile] Datensatz {#dataset}

Kundeneinverständnisdaten müssen an einen [!DNL Profile]-aktivierten Datensatz gesendet werden, dessen Schema Einverständnisfelder enthält. Diese Felder müssen in dasselbe Schema und denselben Datensatz aufgenommen werden, die bzw. den Sie zum Erfassen von Attributinformationen über einzelne Kundinnen und Kunden verwenden.

Lesen Sie das Tutorial [Konfigurieren eines Datensatzes zur Erfassung von Einverständnisdaten](./dataset.md) für detaillierte Schritte, wie Sie diese erforderlichen Felder zu einem [!DNL Profile]-aktivierten Datensatz hinzufügen, bevor Sie mit diesem Handbuch fortfahren.

## Aktualisieren [!DNL Profile] Zusammenführungsrichtlinien zum Einschließen von Einverständnisdaten {#merge-policies}

Nachdem Sie einen [!DNL Profile]-aktivierten Datensatz für die Verarbeitung von Einverständnisdaten erstellt haben, müssen Sie sicherstellen, dass Ihre Zusammenführungsrichtlinien so konfiguriert wurden, dass sie immer Einverständnisfelder in jedem Kundenprofil enthalten. Dazu gehört die Festlegung der Datensatzpriorität, sodass Ihr Einverständnisdatensatz vor anderen potenziell kollidierenden Datensätzen priorisiert wird.

>[!NOTE]
>
>Wenn Sie keine widersprüchlichen Datensätze haben, sollten Sie stattdessen die Zeitstempelpriorität für Ihre Zusammenführungsrichtlinie festlegen. Dadurch wird sichergestellt, dass die letzte von einem Kunden angegebene Einwilligung die verwendete Einverständniseinstellung ist.

Um weitere Informationen zum Arbeiten mit Zusammenführungsrichtlinien zu erhalten, lesen Sie zunächst die [Übersicht über Zusammenführungsrichtlinien](../../../../profile/merge-policies/overview.md). Beim Einrichten Ihrer Zusammenführungsrichtlinien müssen Sie sicherstellen, dass Ihre Profile alle erforderlichen Einverständnisattribute enthalten, die von der Schemafeldgruppe [!UICONTROL Einverständnisse und Voreinstellungen] bereitgestellt werden, wie im Handbuch zur [&#x200B; von Datensätzen &#x200B;](./dataset.md).

## Einverständnisdaten in Experience Platform einbringen

Sobald Sie Ihre Datensätze und Zusammenführungsrichtlinien haben, um die erforderlichen Einverständnisfelder in Ihren Kundenprofilen darzustellen, besteht der nächste Schritt darin, die Einverständnisdaten selbst in Experience Platform zu importieren.

In erster Linie sollten Sie Adobe Experience Platform Web SDK verwenden, um Einverständnisdaten an Experience Platform zu senden, wenn von Ihrem CMP Einverständnisänderungsereignisse erkannt werden. Wenn Sie Einverständnisdaten auf einer mobilen Plattform erfassen, sollten Sie die Adobe Experience Platform Mobile SDK verwenden. Sie können Ihre erfassten Einverständnisdaten auch direkt aufnehmen, indem Sie sie dem XDM-Schema Ihres Einverständnisdatensatzes zuordnen und über die Batch-Aufnahme an Experience Platform senden.

Details zu den einzelnen Methoden finden Sie in den folgenden Unterabschnitten.

### Konfigurieren von Experience Platform Web SDK zur Verarbeitung von Einverständnisdaten {#web-sdk}

Nachdem Sie Ihren CMP so konfiguriert haben, dass er auf Einverständnisänderungsereignisse auf Ihrer Website wartet, können Sie den Experience Platform Web SDK integrieren, um die aktualisierten Einverständniseinstellungen zu erhalten und sie bei jedem Seitenladevorgang und bei jeder Einverständnisänderung an Experience Platform zu senden. Weitere Informationen finden Sie in der Anleitung [Konfigurieren der Web-SDK zur Verarbeitung &#x200B;](../sdk.md) Kundeneinverständnisdaten“.

### Konfigurieren von Experience Platform Mobile SDK zur Verarbeitung von Einverständnisdaten {#mobile-sdk}

Wenn in Ihrer Mobile App Einstellungen für das Kundeneinverständnis erforderlich sind, können Sie die Experience Platform Mobile SDK integrieren, um Einverständniseinstellungen abzurufen und zu aktualisieren. Senden Sie sie an Experience Platform, sobald die Einverständnis-API aufgerufen wird.

Weitere Informationen finden Sie in der Mobile SDK[Dokumentation zum Konfigurieren der mobilen &#x200B;](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/) und [Verwenden der Einverständnis-API](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/api-reference/). Weitere Informationen zum Umgang mit Datenschutzproblemen mit Mobile SDK finden Sie im Abschnitt [Datenschutz und DSGVO](https://developer.adobe.com/client-sdks/resources/privacy-and-gdpr/).

### Direktes Aufnehmen von XDM-konformen Einverständnisdaten {#batch}

Sie können XDM-konforme Einverständnisdaten aus einer CSV-Datei mithilfe der Batch-Aufnahme aufnehmen. Dies kann nützlich sein, wenn Sie einen Rückstand an zuvor erfassten Einverständnisdaten haben, der noch in Ihre Kundenprofile integriert werden muss.

In der Anleitung [Zuordnen einer CSV-Datei zu XDM](../../../../ingestion/tutorials/map-csv/overview.md) erfahren Sie, wie Sie Ihre Datenfelder in XDM konvertieren und in Experience Platform aufnehmen können. Stellen Sie bei der Auswahl [!UICONTROL Ziel] für die Zuordnung sicher, dass Sie die Option **[!UICONTROL Vorhandenen Datensatz verwenden]** auswählen und den [!DNL Profile] Einverständnisdatensatz auswählen, den Sie zuvor erstellt haben.

## Testen der Implementierung {#test-implementation}

Nachdem Sie Kundeneinverständnisdaten in Ihren [!DNL Profile]-aktivierten Datensatz aufgenommen haben, können Sie Ihre aktualisierten Profile daraufhin überprüfen, ob sie Einverständnisattribute enthalten.

>[!IMPORTANT]
>
>Um die Attribute eines vorhandenen Profils in der Benutzeroberfläche anzuzeigen, müssen Sie mindestens einen Identitätswert (und den entsprechenden Namespace) kennen, der mit diesem Profil verknüpft ist.
>
>Wenn Sie keinen Zugriff auf diese Informationen haben, können Sie Ihre eigenen Test-Einverständnisdaten aufnehmen und sie mit einem Identitätswert/Namespace verknüpfen, der Ihnen stattdessen bekannt ist.

Spezifische Schritte zum Nachschlagen [&#x200B; Details eines Profils finden Sie im Abschnitt &#x200B;](../../../../profile/ui/user-guide.md#browse)Durchsuchen von Profilen nach Identität im Handbuch zur [!DNL Profile]-Benutzeroberfläche.

Die neuen Einverständnisattribute werden nicht standardmäßig im Dashboard eines Profils angezeigt. Daher müssen Sie auf der Detailseite eines Profils zur Registerkarte **[!UICONTROL Attribute]** navigieren, um zu bestätigen, dass sie wie erwartet aufgenommen wurden. Informationen zum Anpassen des Dashboards [&#x200B; Ihre &#x200B;](../../../../profile/ui/profile-dashboard.md) finden Sie im Handbuch zum Profil-Dashboard .

<!-- (To be included once CJM is GA)
## Handling consent in Customer Journey Management

If you are using Customer Journey Management, after confirming that your profiles and segments contain consent data, you can start honoring customer [marketing preferences](../../../../xdm/data-types/consents.md#marketing) when pulling segments from Experience Platform. Specifically, profiles who have opted out of the email marketing preference should not be included in segments that are targeted for email campaigns.

Customer Journey Management can also send consent-change signals back to Experience Platform. When a customer selects an "unsubscribe" link in an email message, the updated consent preference is sent to Experience Platform and the appropriate profile attributes are updated accordingly.
-->

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie Ihre Experience Platform-Vorgänge so konfigurieren, dass Kundeneinverständnisdaten mithilfe des Adobe-Standards verarbeitet werden und diese Attribute in Kundenprofilen dargestellt werden. Sie können jetzt Voreinstellungen für die Kundenzustimmung als bestimmenden Faktor in die Segmentqualifikation und andere nachgelagerte Anwendungsfälle integrieren.

Weitere Informationen zu den Datenschutzfunktionen von Experience Platform finden Sie in der Übersicht zu [Governance, Datenschutz und Sicherheit in Experience Platform](../../overview.md).
