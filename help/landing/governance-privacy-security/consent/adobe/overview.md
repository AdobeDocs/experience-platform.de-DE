---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Zustimmungsverarbeitung in Adobe Experience Platform
description: Erfahren Sie, wie Sie in Adobe Experience Platform mithilfe des Adobe 2.0-Standards Zustimmungssignale von Kunden verarbeiten.
role: Developer
feature: Consent
exl-id: cd76a3f6-ae55-4d75-9b30-900fadb4664f
source-git-commit: c0eb5b5c3a1968cae2bc19b7669f70a97379239b
workflow-type: tm+mt
source-wordcount: '1557'
ht-degree: 1%

---

# Einverständnisverarbeitung in Adobe Experience Platform

Mit Adobe Experience Platform können Sie die von Ihren Kunden erfassten Einwilligungsdaten verarbeiten und in Ihre gespeicherten Kundenprofile integrieren. Diese Daten können dann von nachgelagerten Prozessen verwendet werden, um festzustellen, ob die Datenerfassung für einen bestimmten Kunden erfolgt oder ob ihre Profile für bestimmte Zwecke verwendet werden. Beispielsweise können die Einwilligungsdaten für ein bestimmtes Profil bestimmen, ob es in ein exportiertes Zielgruppensegment aufgenommen werden kann oder ob es an bestimmten Marketing-Kanälen wie E-Mails, Textnachrichten oder Push-Benachrichtigungen teilnehmen kann.

Dieses Dokument bietet einen Überblick darüber, wie Sie Ihre Datenvorgänge in Platform so konfigurieren können, dass von einer Zustimmungsverwaltungsplattform (Zustimmungsverwaltung Platform, CMP) generierte Kundenzustimmungsdaten erfasst und in Kundenprofile für nachgelagerte Anwendungsfälle integriert werden.

>[!NOTE]
>
>Dieses Dokument konzentriert sich auf die Verarbeitung von Einwilligungsdaten unter Verwendung des Adobe-Standards. Wenn Sie Einwilligungsdaten gemäß dem IAB Transparency and Consent Framework (TCF) 2.0 verarbeiten, lesen Sie das Handbuch zur Unterstützung von [TCF 2.0 in Adobe Real-time Customer Data Platform](../iab/overview.md).

## Voraussetzungen

Dieses Handbuch setzt ein Verständnis der verschiedenen Experience Platform-Dienste voraus, die an der Verarbeitung von Zustimmungsdaten beteiligt sind:

* [Experience-Datenmodell (XDM)](/help/xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
* [Adobe Experience Platform Identity Service](/help/identity-service/home.md): Löst die grundlegende Herausforderung, die sich aus der Fragmentierung von Kundenerlebnisdaten ergibt, indem Identitäten zwischen Geräten und Systemen überbrückt werden.
* [Echtzeit-Kundenprofil](/help/profile/home.md): Verwendet [!DNL Identity Service] Funktionen, um aus Ihren Datensätzen detaillierte Kundenprofile in Echtzeit zu erstellen. Das Echtzeit-Kundenprofil ruft Daten aus dem Data Lake ab und behält Kundenprofile in seinem eigenen Datenspeicher bei.
* [Adobe Experience Platform Web SDK](/help/web-sdk/home.md): Eine Client-seitige JavaScript-Bibliothek, mit der Sie verschiedene Platform-Dienste in Ihre kundenorientierte Website integrieren können.
   * [SDK-Zustimmungsbefehle](../../../../web-sdk/commands/setconsent.md): Eine Anwendungsfallübersicht der einwilligungsbezogenen SDK-Befehle, die in diesem Handbuch gezeigt werden.
* [Adobe Experience Platform Segmentation Service](/help/segmentation/home.md): Ermöglicht die Aufteilung der Echtzeit-Kundenprofildaten in Gruppen von Einzelanwendern, die ähnliche Eigenschaften aufweisen und ähnlich auf Marketing-Strategien reagieren.

## Zusammenfassung des Zustimmungsverarbeitungsflusses {#summary}

Im Folgenden wird beschrieben, wie Einwilligungsdaten verarbeitet werden, nachdem das System ordnungsgemäß konfiguriert wurde:

1. Ein Kunde gibt seine Zustimmungseinstellungen für die Datenerfassung über ein Dialogfeld auf Ihrer Website an.
1. Bei jedem Laden der Seite (oder wenn Ihr CMP eine Änderung der Zustimmungsvoreinstellungen erkennt) ordnet ein benutzerdefiniertes Skript auf Ihrer Site die aktuellen Voreinstellungen einem standardmäßigen XDM-Objekt zu. Dieses Objekt wird dann an den Befehl &quot;Platform Web SDK `setConsent`&quot;übergeben.
1. Wenn `setConsent` aufgerufen wird, prüft das Platform Web SDK, ob sich die Zustimmungswerte von denen unterscheiden, die es zuletzt erhalten hat. Wenn die Werte unterschiedlich sind (oder kein vorheriger Wert vorhanden ist), werden die strukturierten Zustimmungs-/Voreinstellungsdaten an Adobe Experience Platform gesendet.
1. Die Einwilligungs-/Präferenzdaten werden in einen [!DNL Profile]-aktivierten Datensatz aufgenommen, dessen Schema Einwilligungs-/Präferenzfelder enthält.

Zusätzlich zu den SDK-Befehlen, die von CMP-Zustimmungs-Change-Hooks ausgelöst werden, können Zustimmungsdaten auch über alle kundengenerierten XDM-Daten in Experience Platform fließen, die direkt in einen [!DNL Profile]-aktivierten Datensatz hochgeladen werden.

### Einverständnisvollstreckung

In der aktuellen Version der Unterstützung für die Verarbeitung von Einwilligungen in Platform wird nur die Datenerfassungsberechtigung (`collect.val`) vom Platform Web SDK automatisch erzwungen. Auch wenn detailliertere Einverständnisse und Voreinstellungen in Kundenprofilen erfasst und beibehalten werden können, müssen diese zusätzlichen Signale in Ihren eigenen nachgelagerten Prozessen manuell erzwungen werden.

>[!NOTE]
>
>Weitere Informationen zur Struktur der oben erwähnten XDM-Einwilligungsfelder finden Sie im Handbuch zum Datentyp [[!UICONTROL Einverständnisse und Voreinstellungen]](/help/xdm/data-types/consents.md).

Sobald das System konfiguriert wurde, interpretiert das Platform Web SDK den Wert für die Datenerfassungs-Einwilligung für den aktuellen Benutzer, um festzustellen, ob die Daten an das Adobe Experience Platform-Edge Network gesendet, vom Client abgelegt oder beibehalten werden sollen, bis die Datenerfassungsberechtigung auf &quot;Ja&quot;oder &quot;Nein&quot;festgelegt ist.

## Ermitteln, wie Sie in Ihrem CMP Kundenzustimmungsdaten generieren {#consent-data}

Da jedes CMP-System einzigartig ist, müssen Sie festlegen, wie Ihre Kunden bei der Interaktion mit Ihrem Dienst am besten ihre Zustimmung erteilen können. Eine gängige Methode, dies zu erreichen, besteht darin, ein Cookie-Einverständnisdialogfeld zu verwenden, das dem folgenden Beispiel ähnelt:

![](../../../images/governance-privacy-security/consent/adobe/overview/consent-dialog.png)

Dieser Dialog sollte es dem Kunden ermöglichen, bestimmte Marketing- und Personalisierungsanwendungsfälle für seine Daten einzuschalten oder abzulehnen. Diese Zustimmungen und Voreinstellungen sollten mit dem Datenmodell übereinstimmen, das Sie im nächsten Schritt für den Datensatz mit aktiviertem [!DNL Profile] definieren.

## Hinzufügen standardisierter Einwilligungsfelder zu einem [!DNL Profile]-aktivierten Datensatz {#dataset}

Die Zustimmungsdaten des Kunden müssen an einen [!DNL Profile]-aktivierten Datensatz gesendet werden, dessen Schema Zustimmungsfelder enthält. Diese Felder müssen im selben Schema und Datensatz enthalten sein, mit dem Sie Attributinformationen zu einzelnen Kunden erfassen.

Ausführliche Anweisungen zum Hinzufügen dieser erforderlichen Felder zu einem für [!DNL Profile] aktivierten Datensatz finden Sie im Tutorial [Konfigurieren eines Datensatzes zur Erfassung von Einwilligungsdaten](./dataset.md) , bevor Sie mit diesem Handbuch fortfahren.

## Aktualisieren von [!DNL Profile] Zusammenführungsrichtlinien zum Einschließen von Einwilligungsdaten {#merge-policies}

Nachdem Sie einen [!DNL Profile]-aktivierten Datensatz für die Verarbeitung von Zustimmungsdaten erstellt haben, müssen Sie sicherstellen, dass Ihre Zusammenführungsrichtlinien so konfiguriert wurden, dass in jedem Kundenprofil immer Einwilligungsfelder enthalten sind. Dazu gehört das Festlegen der Datensatzpriorität, sodass Ihr Einwilligungsdatensatz Vorrang vor anderen möglicherweise in Konflikt stehenden Datensätzen erhält.

>[!NOTE]
>
>Wenn keine Datensätze in Konflikt zueinander stehen, sollten Sie stattdessen die Zeitstempelpriorität für Ihre Zusammenführungsrichtlinie festlegen. Dadurch wird sichergestellt, dass die von einem Kunden zuletzt angegebene Zustimmung die verwendete Zustimmungseinstellung ist.

Weitere Informationen zum Arbeiten mit Zusammenführungsrichtlinien finden Sie in der [Übersicht über Zusammenführungsrichtlinien](../../../../profile/merge-policies/overview.md). Beim Einrichten Ihrer Zusammenführungsrichtlinien müssen Sie sicherstellen, dass Ihre Profile alle erforderlichen Zustimmungsattribute enthalten, die von der Schemafeldgruppe [!UICONTROL Einverständnisse und Voreinstellungen] bereitgestellt werden, wie im Handbuch zur [Datensatzvorbereitung](./dataset.md) beschrieben.

## Einverständnisdaten in Platform einbringen

Sobald Sie über Ihre Datensätze und Zusammenführungsrichtlinien verfügen, um die erforderlichen Einwilligungsfelder in Ihren Kundenprofilen darzustellen, besteht der nächste Schritt darin, die Einwilligungsdaten selbst in Platform zu übertragen.

In erster Linie sollten Sie das Adobe Experience Platform Web SDK verwenden, um Zustimmungsdaten an Platform zu senden, sobald Einwilligungsänderungsereignisse von Ihrem CMP erkannt werden. Wenn Sie Einwilligungsdaten auf einer mobilen Plattform erfassen, sollten Sie das Adobe Experience Platform Mobile SDK verwenden. Sie können sich auch dafür entscheiden, Ihre erfassten Zustimmungsdaten direkt zu erfassen, indem Sie sie dem XDM-Schema Ihres Einwilligungsdatensatzes zuordnen und über die Batch-Erfassung an Platform senden.

Details zu diesen Methoden finden Sie in den folgenden Unterabschnitten.

### Experience Platform Web SDK zur Verarbeitung von Zustimmungsdaten konfigurieren {#web-sdk}

Nachdem Sie Ihren CMP so konfiguriert haben, dass er auf Zustimmungsänderungsereignisse auf Ihrer Website überwacht, können Sie das Experience Platform Web SDK integrieren, um die aktualisierten Zustimmungseinstellungen zu erhalten und sie bei jedem Seitenladevorgang und bei jedem Einverständnisänderungsereignis an Platform zu senden. Weitere Informationen finden Sie im Handbuch zum [Konfigurieren des Web SDK für die Verarbeitung von Zustimmungsdaten von Kunden](../sdk.md) .

### Experience Platform Mobile SDK für die Verarbeitung von Zustimmungsdaten konfigurieren {#mobile-sdk}

Wenn in Ihrer Mobile App Zustimmungsvoreinstellungen von Kunden erforderlich sind, können Sie das Experience Platform Mobile SDK integrieren, um Zustimmungseinstellungen abzurufen und zu aktualisieren und sie an Platform zu senden, wann immer die API für die Einwilligung aufgerufen wird.

Weitere Informationen zum Konfigurieren der mobilen Erweiterung &quot;Consent mobile&quot;](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/) und zum [Verwenden der API für Einwilligungen](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/api-reference/) finden Sie in der Mobile SDK-Dokumentation . [ Weitere Informationen zum Umgang mit Datenschutzanliegen mit dem Mobile SDK finden Sie im Abschnitt [Datenschutz und DSGVO](https://developer.adobe.com/client-sdks/resources/privacy-and-gdpr/).

### Direktes Aufnehmen von XDM-konformen Einwilligungsdaten {#batch}

Sie können XDM-konforme Einwilligungsdaten aus einer CSV-Datei erfassen, indem Sie die Batch-Erfassung verwenden. Dies kann nützlich sein, wenn Sie einen Rückstand aus zuvor erfassten Zustimmungsdaten haben, die noch nicht in Ihre Kundenprofile integriert wurden.

Im Tutorial zum [Zuordnen einer CSV-Datei zu XDM](../../../../ingestion/tutorials/map-csv/overview.md) erfahren Sie, wie Sie Ihre Datenfelder in XDM konvertieren und in Platform aufnehmen. Stellen Sie bei der Auswahl von [!UICONTROL Ziel] für die Zuordnung sicher, dass Sie die Option **[!UICONTROL Vorhandenen Datensatz verwenden]** auswählen und den zuvor erstellten [!DNL Profile] aktivierten Einwilligungsdatensatz auswählen.

## Implementierung testen {#test-implementation}

Nachdem Sie Kundeneinwilligungsdaten in Ihren [!DNL Profile]-aktivierten Datensatz aufgenommen haben, können Sie Ihre aktualisierten Profile überprüfen, um festzustellen, ob sie Zustimmungsattribute enthalten.

>[!IMPORTANT]
>
>Um die Attribute eines vorhandenen Profils in der Benutzeroberfläche anzuzeigen, müssen Sie mindestens einen Identitätswert (und den zugehörigen Namespace) kennen, der mit diesem Profil verknüpft ist.
>
>Wenn Sie keinen Zugriff auf diese Informationen haben, können Sie Ihre eigenen Testzustimmungsdaten erfassen und sie mit einem Identitätswert/Namespace verknüpfen, der Ihnen stattdessen bekannt ist.

Im Abschnitt zum Durchsuchen von Profilen nach Identität ](../../../../profile/ui/user-guide.md#browse) im UI-Handbuch [!DNL Profile] finden Sie spezifische Schritte zum Nachschlagen von Profildetails.[

Die neuen Zustimmungsattribute werden nicht standardmäßig im Dashboard eines Profils angezeigt. Daher müssen Sie auf der Detailseite eines Profils zur Registerkarte **[!UICONTROL Attribute]** navigieren, um zu bestätigen, dass das Profil erwartungsgemäß aufgenommen wurde. Informationen zum Anpassen des Dashboards an Ihre Anforderungen finden Sie im Handbuch im Dashboard [Profil-Dashboard](../../../../profile/ui/profile-dashboard.md) .

<!-- (To be included once CJM is GA)
## Handling consent in Customer Journey Management

If you are using Customer Journey Management, after confirming that your profiles and segments contain consent data, you can start honoring customer [marketing preferences](../../../../xdm/data-types/consents.md#marketing) when pulling segments from Platform. Specifically, profiles who have opted out of the email marketing preference should not be included in segments that are targeted for email campaigns.

Customer Journey Management can also send consent-change signals back to Platform. When a customer selects an "unsubscribe" link in an email message, the updated consent preference is sent to Platform and the appropriate profile attributes are updated accordingly.
-->

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie Ihre Platform-Vorgänge für die Verarbeitung von Kundenzustimmungsdaten mithilfe des Adobe-Standards konfigurieren und diese Attribute in Kundenprofilen darstellen lassen. Sie können jetzt Kundenzustimmungseinstellungen als entscheidenden Faktor für die Segmentqualifizierung und andere nachgelagerte Anwendungsfälle integrieren.

Weitere Informationen zu datenschutzbezogenen Funktionen von Experience Platform finden Sie in der Übersicht zu [Governance, Datenschutz und Sicherheit in Platform](../../overview.md).
