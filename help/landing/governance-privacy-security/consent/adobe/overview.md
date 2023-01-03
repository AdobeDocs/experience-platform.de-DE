---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Zustimmungsverarbeitung in Adobe Experience Platform
topic-legacy: getting started
description: Erfahren Sie, wie Sie in Adobe Experience Platform mithilfe des Adobe 2.0-Standards Zustimmungssignale von Kunden verarbeiten.
exl-id: cd76a3f6-ae55-4d75-9b30-900fadb4664f
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1567'
ht-degree: 1%

---

# Einverständnisverarbeitung in Adobe Experience Platform

Mit Adobe Experience Platform können Sie die von Ihren Kunden erfassten Einwilligungsdaten verarbeiten und in Ihre gespeicherten Kundenprofile integrieren. Diese Daten können dann von nachgelagerten Prozessen verwendet werden, um festzustellen, ob die Datenerfassung für einen bestimmten Kunden erfolgt oder ob ihre Profile für bestimmte Zwecke verwendet werden. Beispielsweise können die Einwilligungsdaten für ein bestimmtes Profil bestimmen, ob es in ein exportiertes Zielgruppensegment aufgenommen werden kann oder ob es an bestimmten Marketing-Kanälen wie E-Mails, Textnachrichten oder Push-Benachrichtigungen teilnehmen kann.

Dieses Dokument bietet einen Überblick darüber, wie Sie Ihre Datenvorgänge in Platform so konfigurieren können, dass von einer Zustimmungsverwaltungsplattform (Zustimmungsverwaltung Platform, CMP) generierte Kundenzustimmungsdaten erfasst und in Kundenprofile für nachgelagerte Anwendungsfälle integriert werden.

>[!NOTE]
>
>Dieses Dokument konzentriert sich auf die Verarbeitung von Einwilligungsdaten unter Verwendung des Adobe-Standards. Wenn Sie Einwilligungsdaten gemäß dem IAB Transparency and Consent Framework (TCF) 2.0 verarbeiten, lesen Sie das Handbuch zu [TCF 2.0-Unterstützung in Adobe Real-time Customer Data Platform](../iab/overview.md).

## Voraussetzungen

Dieses Handbuch setzt ein Verständnis der verschiedenen Experience Platform-Services voraus, die mit der Verarbeitung von Zustimmungsdaten befasst sind:

* [Experience-Datenmodell (XDM)](../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
* [Adobe Experience Platform Identity Service](../../../../identity-service/home.md): Löst die grundlegende Herausforderung, die sich aus der Fragmentierung von Kundenerlebnisdaten ergibt, indem Identitäten zwischen Geräten und Systemen überbrückt werden.
* [Echtzeit-Kundenprofil](../../../../profile/home.md): Verwendet [!DNL Identity Service] Funktionen zum Erstellen detaillierter Kundenprofile aus Ihren Datensätzen in Echtzeit. Das Echtzeit-Kundenprofil ruft Daten aus dem Data Lake ab und behält Kundenprofile in seinem eigenen Datenspeicher bei.
* [Adobe Experience Platform Web SDK](../../../../edge/home.md): Eine Client-seitige JavaScript-Bibliothek, mit der Sie verschiedene Platform-Dienste in Ihre kundenorientierte Website integrieren können.
   * [SDK-Zustimmungsbefehle](../../../../edge/consent/supporting-consent.md): Eine Anwendungsfallübersicht der einwilligungsbezogenen SDK-Befehle, die in diesem Handbuch gezeigt werden.
* [Adobe Experience Platform-Segmentierungsdienst](../../../../segmentation/home.md): Ermöglicht es Ihnen, Echtzeit-Kundenprofildaten in Gruppen von Einzelanwendern zu unterteilen, die ähnliche Eigenschaften aufweisen und ähnlich auf Marketing-Strategien reagieren.

## Zusammenfassung des Zustimmungsverarbeitungsflusses {#summary}

Im Folgenden wird beschrieben, wie Einwilligungsdaten verarbeitet werden, nachdem das System ordnungsgemäß konfiguriert wurde:

1. Ein Kunde gibt seine Zustimmungsvoreinstellungen für die Datenerfassung über ein Dialogfeld auf Ihrer Website an.
1. Bei jedem Laden der Seite (oder wenn Ihr CMP eine Änderung der Zustimmungsvoreinstellungen erkennt) ordnet ein benutzerdefiniertes Skript auf Ihrer Site die aktuellen Voreinstellungen einem standardmäßigen XDM-Objekt zu. Dieses Objekt wird dann an das Platform Web SDK übergeben. `setConsent` Befehl.
1. Wann `setConsent` aufgerufen wird, überprüft das Platform Web SDK, ob sich die Zustimmungswerte von denen unterscheiden, die es zuletzt erhalten hat. Wenn die Werte unterschiedlich sind (oder kein vorheriger Wert vorhanden ist), werden die strukturierten Zustimmungs-/Voreinstellungsdaten an Adobe Experience Platform gesendet.
1. Die Einwilligungs-/Präferenzdaten werden in eine [!DNL Profile]-aktivierter Datensatz, dessen Schema Zustimmungs-/Voreinstellungsfelder enthält.

Zusätzlich zu den SDK-Befehlen, die von CMP-Zustimmungs-Change-Hooks ausgelöst werden, können Zustimmungsdaten auch über alle kundengenerierten XDM-Daten in Experience Platform fließen, die direkt in eine [!DNL Profile]-aktivierter Datensatz.

### Einverständnisdurchsetzung

In der aktuellen Version der Unterstützung für die Verarbeitung der Einwilligung in Platform ist nur die Datenerfassungsberechtigung (`collect.val`) wird automatisch vom Platform Web SDK erzwungen. Auch wenn detailliertere Einverständnisse und Voreinstellungen in Kundenprofilen erfasst und beibehalten werden können, müssen diese zusätzlichen Signale in Ihren eigenen nachgelagerten Prozessen manuell erzwungen werden.

>[!NOTE]
>
>Weitere Informationen zur Struktur der oben erwähnten XDM-Einwilligungsfelder finden Sie im Handbuch zum [[!UICONTROL Einverständnis und Voreinstellungen] Datentyp](../../../../xdm/data-types/consents.md).

Sobald das System konfiguriert wurde, interpretiert das Platform Web SDK den Wert für die Datenerfassungs-Einwilligung für den aktuellen Benutzer, um festzustellen, ob die Daten an das Adobe Experience Platform Edge Network gesendet, vom Client abgelegt oder beibehalten werden sollen, bis die Datenerfassungsberechtigung auf &quot;Ja&quot;oder &quot;Nein&quot;festgelegt ist.

## Ermitteln, wie Sie in Ihrem CMP Kundenzustimmungsdaten generieren {#consent-data}

Da jedes CMP-System einzigartig ist, müssen Sie festlegen, wie Ihre Kunden bei der Interaktion mit Ihrem Dienst am besten ihre Zustimmung erteilen können. Eine gängige Methode, dies zu erreichen, besteht darin, ein Cookie-Einverständnisdialogfeld zu verwenden, das dem folgenden Beispiel ähnelt:

![](../../../images/governance-privacy-security/consent/adobe/overview/consent-dialog.png)

Dieser Dialog sollte es dem Kunden ermöglichen, bestimmte Marketing- und Personalisierungsanwendungsfälle für seine Daten einzuschalten oder abzulehnen. Diese Zustimmungen und Voreinstellungen sollten mit dem Datenmodell übereinstimmen, das Sie für die [!DNL Profile]-aktivierter Datensatz im nächsten Schritt.

## Hinzufügen standardisierter Einwilligungsfelder zu einem [!DNL Profile]-aktivierter Datensatz {#dataset}

Die Daten zur Kundenzustimmung müssen an eine [!DNL Profile]-aktivierter Datensatz, dessen Schema Zustimmungsfelder enthält. Diese Felder müssen im selben Schema und Datensatz enthalten sein, mit dem Sie Attributinformationen zu einzelnen Kunden erfassen.

Weiterführende Informationen finden Sie im Tutorial [Konfigurieren eines Datensatzes zur Erfassung von Zustimmungsdaten](./dataset.md) für detaillierte Schritte zum Hinzufügen dieser erforderlichen Felder zu einem [!DNL Profile]-aktivierter Datensatz, bevor Sie mit diesem Handbuch fortfahren.

## Aktualisieren [!DNL Profile] Zusammenführungsrichtlinien zum Einbeziehen von Einwilligungsdaten {#merge-policies}

Nachdem Sie eine [!DNL Profile]-aktivierter Datensatz zur Verarbeitung von Einwilligungsdaten, müssen Sie sicherstellen, dass Ihre Zusammenführungsrichtlinien so konfiguriert wurden, dass in jedem Kundenprofil immer Einwilligungsfelder enthalten sind. Dazu gehört das Festlegen der Datensatzpriorität, sodass Ihr Einwilligungsdatensatz Vorrang vor anderen möglicherweise in Konflikt stehenden Datensätzen erhält.

>[!NOTE]
>
>Wenn keine Datensätze in Konflikt zueinander stehen, sollten Sie stattdessen die Zeitstempelpriorität für Ihre Zusammenführungsrichtlinie festlegen. Dadurch wird sichergestellt, dass die von einem Kunden zuletzt angegebene Zustimmung die verwendete Zustimmungseinstellung ist.

Weitere Informationen zum Arbeiten mit Zusammenführungsrichtlinien finden Sie im Abschnitt [Übersicht über Zusammenführungsrichtlinien](../../../../profile/merge-policies/overview.md). Beim Einrichten Ihrer Zusammenführungsrichtlinien müssen Sie sicherstellen, dass Ihre Profile alle erforderlichen Zustimmungsattribute enthalten, die von der [!UICONTROL Einverständnis und Voreinstellungen] Schemafeldgruppe, wie im Handbuch [Datensatzvorbereitung](./dataset.md).

## Einverständnisdaten in Platform einbringen

Sobald Sie über Ihre Datensätze und Zusammenführungsrichtlinien verfügen, um die erforderlichen Einwilligungsfelder in Ihren Kundenprofilen darzustellen, besteht der nächste Schritt darin, die Einwilligungsdaten selbst in Platform zu übertragen.

In erster Linie sollten Sie das Adobe Experience Platform Web SDK verwenden, um Zustimmungsdaten an Platform zu senden, sobald Einwilligungsänderungsereignisse von Ihrem CMP erkannt werden. Wenn Sie Einwilligungsdaten auf einer mobilen Plattform erfassen, sollten Sie das Adobe Experience Platform Mobile SDK verwenden. Sie können sich auch dafür entscheiden, Ihre erfassten Zustimmungsdaten direkt zu erfassen, indem Sie sie dem XDM-Schema Ihres Einwilligungsdatensatzes zuordnen und über die Batch-Erfassung an Platform senden.

Details zu diesen Methoden finden Sie in den folgenden Unterabschnitten.

### Experience Platform Web SDK zur Verarbeitung von Zustimmungsdaten konfigurieren {#web-sdk}

Nachdem Sie Ihren CMP so konfiguriert haben, dass er auf Zustimmungsänderungsereignisse auf Ihrer Website überwacht, können Sie das Experience Platform Web SDK integrieren, um die aktualisierten Zustimmungseinstellungen zu erhalten und sie bei jedem Seitenladevorgang und bei jedem Einverständnisänderungsereignis an Platform zu senden. Siehe Handbuch unter [Konfigurieren des Web SDK zur Verarbeitung der Kundenzustimmungsdaten](../sdk.md) für weitere Informationen.

### Experience Platform Mobile SDK für die Verarbeitung von Zustimmungsdaten konfigurieren {#mobile-sdk}

Wenn in Ihrer Mobile App Zustimmungsvoreinstellungen von Kunden erforderlich sind, können Sie das Experience Platform Mobile SDK integrieren, um Zustimmungseinstellungen abzurufen und zu aktualisieren und sie an Platform zu senden, wann immer die API für die Einwilligung aufgerufen wird.

Siehe Mobile SDK-Dokumentation für [Konfigurieren der mobilen Erweiterung &quot;Consent&quot;](https://aep-sdks.gitbook.io/docs/foundation-extensions/consent-for-edge-network) und [über die API für die Zustimmung](https://aep-sdks.gitbook.io/docs/foundation-extensions/consent-for-edge-network/api-reference). Weitere Informationen zum Umgang mit Datenschutzanliegen mit dem Mobile SDK finden Sie im Abschnitt . [Datenschutz und DSGVO](https://aep-sdks.gitbook.io/docs/resources/privacy-and-gdpr).

### Direktes Aufnehmen von XDM-konformen Einwilligungsdaten {#batch}

Sie können XDM-konforme Einwilligungsdaten aus einer CSV-Datei erfassen, indem Sie die Batch-Erfassung verwenden. Dies kann nützlich sein, wenn Sie einen Rückstand aus zuvor erfassten Zustimmungsdaten haben, die noch nicht in Ihre Kundenprofile integriert wurden.

Folgen Sie dem Tutorial zu [Zuordnen einer CSV-Datei zu XDM](../../../../ingestion/tutorials/map-csv/overview.md) , um zu erfahren, wie Sie Ihre Datenfelder in XDM konvertieren und in Platform aufnehmen. Bei der Auswahl der [!UICONTROL Ziel] Stellen Sie für die Zuordnung sicher, dass Sie die **[!UICONTROL Vorhandenen Datensatz verwenden]** und wählen Sie die [!DNL Profile]-aktivierter Einwilligungsdatensatz, den Sie zuvor erstellt haben.

## Implementierung testen {#test-implementation}

Nachdem Sie Kundeneinwilligungsdaten in Ihre [!DNL Profile]-aktivierten Datensatz können Sie Ihre aktualisierten Profile überprüfen, um zu sehen, ob sie Zustimmungsattribute enthalten.

>[!IMPORTANT]
>
>Um die Attribute eines vorhandenen Profils in der Benutzeroberfläche anzuzeigen, müssen Sie mindestens einen Identitätswert (und den zugehörigen Namespace) kennen, der mit diesem Profil verknüpft ist.
>
>Wenn Sie keinen Zugriff auf diese Informationen haben, können Sie Ihre eigenen Testzustimmungsdaten erfassen und sie mit einem Identitätswert/Namespace verknüpfen, der Ihnen stattdessen bekannt ist.

Siehe Abschnitt zu [Profile nach Identität durchsuchen](../../../../profile/ui/user-guide.md#browse) im [!DNL Profile] UI-Handbuch für spezifische Schritte zum Nachschlagen der Details eines Profils.

Die neuen Zustimmungsattribute werden nicht standardmäßig im Dashboard eines Profils angezeigt. Daher müssen Sie zum **[!UICONTROL Attribute]** auf der Detailseite eines Profils, um zu bestätigen, dass das Profil erwartungsgemäß aufgenommen wurde. Siehe Handbuch im [Profil-Dashboard](../../../../profile/ui/profile-dashboard.md) , um zu erfahren, wie Sie das Dashboard an Ihre Anforderungen anpassen können.

<!-- (To be included once CJM is GA)
## Handling consent in Customer Journey Management

If you are using Customer Journey Management, after confirming that your profiles and segments contain consent data, you can start honoring customer [marketing preferences](../../../../xdm/data-types/consents.md#marketing) when pulling segments from Platform. Specifically, profiles who have opted out of the email marketing preference should not be included in segments that are targeted for email campaigns.

Customer Journey Management can also send consent-change signals back to Platform. When a customer selects an "unsubscribe" link in an email message, the updated consent preference is sent to Platform and the appropriate profile attributes are updated accordingly.
-->

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie Ihre Platform-Vorgänge für die Verarbeitung von Kundenzustimmungsdaten mithilfe des Adobe-Standards konfigurieren und diese Attribute in Kundenprofilen darstellen lassen. Sie können jetzt Kundenzustimmungseinstellungen als entscheidenden Faktor für die Segmentqualifizierung und andere nachgelagerte Anwendungsfälle integrieren.

Weitere Informationen zu den datenschutzbezogenen Funktionen von Experience Platform finden Sie in der Übersicht unter [Governance, Datenschutz und Sicherheit in Platform](../../overview.md).
