---
keywords: Experience Platform;Startseite;beliebte Themen;segmentierung;Segmentierung;Segment Match;segment match
solution: Experience Platform
title: Übersicht zu Segment Match
description: Segment Match ist ein Service zur Segmentfreigabe in Adobe Experience Platform, mit dem zwei oder mehr Experience Platform-Benutzende Segmentdaten auf sichere, verwaltete und datenschutzfreundliche Weise austauschen können.
exl-id: 4e6ec2e0-035a-46f4-b171-afb777c14850
source-git-commit: d4b6b83e37762f73f628b8922bf77f1739492eef
workflow-type: tm+mt
source-wordcount: '2000'
ht-degree: 67%

---

# [!DNL Segment Match] – Übersicht

>[!IMPORTANT]
>
>Adobe führte 2021 [!DNL Segment Match] für Kunden ein, um mit ihnen zusammenzuarbeiten und Audiences auszutauschen. Anfang 2025 führte Adobe [Real-Time CDP Collaboration](https://experienceleague.adobe.com/de/docs/real-time-cdp-collaboration/using/home) ein, den längerfristigen Ansatz zur Lösung dieses Anwendungsfalls.
>
>* Für Kunden in den USA, Kanada, Australien, Neuseeland und EMEA: Adobe empfiehlt Kunden von Real-Time CDP Prime und Ultimate, Anwendungsfälle für die Datenzusammenarbeit von [!DNL Segment Match] auf Real-Time CDP Collaboration zu übertragen. Lesen Sie die [Dokumentation](https://experienceleague.adobe.com/de/docs/real-time-cdp-collaboration/using/home) und [Schnellstartanleitung](https://experienceleague.adobe.com/de/docs/real-time-cdp-collaboration/using/quick-start-guide) für Real-Time CDP Collaboration und wenden Sie sich an Ihr Adobe-Accountteam, um mehr zu erfahren.
>* Für Kunden in allen anderen Regionen: [!DNL Segment Match] ist die empfohlene Option, bis Real-Time CDP Collaboration in diesen Regionen 2026 veröffentlicht wird.

Adobe Experience Platform Segment Match ist ein Service zur Segmentfreigabe, mit dem zwei oder mehr Experience Platform-Benutzende Segmentdaten auf sichere, verwaltete und datenschutzfreundliche Weise austauschen können. [!DNL Segment Match] verwendet Experience Platform-Datenschutzstandards und persönliche IDs wie Hash-E-Mails, Hash-Telefonnummern und Geräte-IDs wie IDFAs und GAIDs.

Mit [!DNL Segment Match] können Sie:

* die Identitätsüberschneidung verwalten,
* Schätzungen vor der Freigabe anzeigen,
* Datennutzungs-Labels anwenden, um zu steuern, ob Daten für Partner freigegeben werden können,
* nach der Veröffentlichung eines Feeds das freigegebene Zielgruppen-Lebenszyklus-Management pflegen und den dynamischen Datenaustausch durch Funktionen zum Hinzufügen, Löschen und Aufheben der Freigabe fortsetzen.

[!DNL Segment Match] verwendet einen Identitätsüberschneidungsprozess, um sicherzustellen, dass die Segmentfreigabe auf sichere und datenschutzorientierte Weise erfolgt. Eine **Identität mit Überschneidung** ist eine Identität, die sowohl in Ihrem Segment als auch im Segment Ihres ausgewählten Partners eine Übereinstimmung enthält. Vor der Freigabe eines Segments zwischen Absendenden und Empfangenden wird im Prozess zur Identitätsüberschneidung geprüft, ob Überschneidungen bei Namespaces und Einverständnisprüfungen zwischen Absendenden und Empfangenden vorhanden sind. Beide Überschneidungsprüfungen müssen bestanden werden, damit ein Segment freigegeben werden kann.

In den folgenden Abschnitten finden Sie weitere Informationen zu [!DNL Segment Match], einschließlich Details zum Setup und seinem End-to-End-Workflow.

## Einrichten

In den folgenden Abschnitten wird beschrieben, wie Sie [!DNL Segment Match] einrichten und konfigurieren:

### Einrichten von Identitätsdaten und Namespaces {#namespaces}

Um [!DNL Segment Match] zu verwenden, müssen Sie als Erstes sicherstellen, dass Sie Daten mit den unterstützten Identity-Namespaces aufnehmen.

Identity-Namespaces sind eine Komponente von [Adobe Experience Platform Identity Service](../../../identity-service/home.md). Jede Kundenidentität enthält einen zugehörigen Namespace, der den Kontext der Identität angibt. Ein Namespace unterscheidet beispielsweise den Wert von „name<span>@email.com“ als E-Mail-Adresse oder „443522“ als numerische CRM-ID.

Eine vollqualifizierte Identität umfasst einen ID-Wert und einen Namespace. Bei der Zuordnung von Eintragsdaten zu Profilfragmenten (z. B. beim Zusammenführen von Profildaten durch das [!DNL Real-Time Customer Profile]) müssen sowohl Identitätswert als auch Namespace übereinstimmen.

Im Kontext von [!DNL Segment Match] werden Namespaces bei der Datenfreigabe im Überschneidungsprozess verwendet.

Folgende Namespaces werden unterstützt:

| Namespace | Beschreibung |
| --------- | ----------- |
| E-Mails (SHA256, in Kleinbuchstaben) | Ein Namespace für vorab gehashte E-Mail-Adressen. In diesem Namespace angegebene Werte werden vor dem Hashing mit SHA256 in Kleinbuchstaben umgewandelt. Vor der Normalisierung einer E-Mail-Adresse müssen vorangestellte und nachfolgende Leerzeichen abgeschnitten werden. Diese Einstellung kann nachträglich nicht mehr geändert werden. Experience Platform bietet zwei Methoden zur Unterstützung von Hashing bei der Datenerfassung: durch [`setCustomerIDs`](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html?lang=de#hashing-support) und [Datenvorbereitung](../../../data-prep/functions.md#hashing). |
| Phone (SHA256_E.164) | Ein Namespace, der unformatierte Telefonnummern darstellt, die mit dem SHA256- und E.164-Format gehasht werden müssen. |
| ECID | Ein Namespace, der einen Experience Cloud ID (ECID)-Wert darstellt. Dieser Namespace kann auch durch die folgenden Aliase referenziert werden: „Adobe Marketing Cloud ID“, „Adobe Experience Cloud ID“, „Adobe Experience Platform ID“. Weiterführende Informationen dazu finden Sie in der [ECID-Übersicht](../../../identity-service/features/ecid.md). |
| Apple IDFA (ID für Advertiser) | Ein Namespace, der die Apple ID für Advertiser darstellt. Weiteführende Informationen finden Sie im folgenden Dokument zu [Interessensbasierten Anzeigen](https://support.apple.com/de-de/HT202074). |
| Google Ad-ID | Ein Namespace, der eine Google Advertising ID darstellt. Weiterführende Informationen finden Sie im folgenden Dokument zu [Google Advertising IDs](https://support.google.com/googleplay/android-developer/answer/6048248?hl=de). |

### Einrichten der Einverständniskonfiguration

Sie müssen eine Einverständniskonfiguration bereitstellen und deren Standardwert auf `opt-in` oder `opt-out` festlegen, um eine Einverständnisprüfung durchzuführen.

Die Opt-in- und Opt-out-Einverständnisprüfung bestimmt, ob Sie basierend auf dem Einverständnis, Benutzerdaten standardmäßig freigeben dürfen. Wenn die Einverständniskonfiguration standardmäßig auf `opt-out` festgelegt ist, können Benutzerdaten freigegeben werden, es sei denn, Benutzende schließen die Freigabe ausdrücklich aus. Wenn der Standardwert auf `opt-in` festgelegt ist, können Benutzerdaten nicht freigegeben werden, es sei denn, Benutzende lassen dies ausdrücklich zu.

Die standardmäßige Einverständniskonfiguration für [!DNL Segment Match] ist auf `opt-out` festgelegt. Um ein Opt-in-Modell für Ihre Daten zu erzwingen, senden Sie eine E-Mail-Anfrage an das Adobe-Accountteam.

Weitere Informationen zum `share`, das zum Festlegen des Einverständniswerts für eine Datenfreigabe verwendet wird, finden Sie in der folgenden Dokumentation [Datenschutz- und Einverständnis-Feldergruppe](../../../xdm/field-groups/profile/consents.md). Informationen zu der spezifischen Feldergruppe, mit der das Verbrauchereinverständnis zur Sammlung und Verwendung von Daten im Zusammenhang mit Datenschutz-, Personalisierungs- und Marketing-Voreinstellungen erfasst wird, finden Sie im folgenden [GitHub-Beispiel zu den Voreinstellungen für das Einverständnis für Datenschutz, Personalisierung und Marketing](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/consent/consent-preferences.schema.md).

### Konfigurieren von Datennutzungs-Labels

Als letzte Voraussetzung müssen Sie ein neues Datennutzungs-Label konfigurieren, um die Datenfreigabe zu verhindern. Mithilfe von Datennutzungs-Labels können Sie verwalten, welche Daten über [!DNL Segment Match] freigegeben werden dürfen.

Mit Datennutzungs-Labels können Sie Datensätze anhand der für diese Daten geltenden Nutzungsrichtlinien kategorisieren. Labels können jederzeit angewendet werden, was eine flexible Handhabung der Daten ermöglicht. Best Practices legen nahe, Daten direkt bei ihrer Aufnahme in Experience Platform oder ab dem Zeitpunkt ihrer Nutzbarkeit in Experience Platform mit einer Beschriftung zu versehen.

[!DNL Segment Match] verwendet die C11-Kennzeichnung, eine [!DNL Segment Match]-spezifische Kennzeichnung von Verträgen, die Sie manuell zu allen Datensätzen oder Attributen hinzufügen können, um sicherzustellen, dass sie aus dem [!DNL Segment Match]-Partnerfreigabeprozess ausgeschlossen werden. Das Label „C11“ bezeichnet Daten, die nicht in [!DNL Segment Match]-Prozessen verwendet werden sollten. Nachdem Sie ermittelt haben, welche Datensätze und/oder Felder Sie aus [!DNL Segment Match] ausschließen möchten, und die C11-Kennzeichnung entsprechend hinzugefügt haben, wird das Label automatisch vom [!DNL Segment Match]-Workflow durchgesetzt. [!DNL Segment Match] aktiviert automatisch die [!UICONTROL Restrict data sharing]. Spezifische Anweisungen zum Anwenden von Datennutzungs-Labels auf Datensätze finden Sie im Tutorial zum [Verwalten von Datennutzungs-Labels in der Benutzeroberfläche](../../../data-governance/labels/user-guide.md).

Eine Liste der Datennutzungs-Labels und ihrer Definitionen finden Sie im [Glossar zu Datennutzungs-Labels](../../../data-governance/labels/reference.md). Informationen zu Datennutzungsrichtlinien finden Sie in der [Übersicht zu Datennutzungsrichtlinien](../../../data-governance/policies/overview.md).

### Grundlegendes zu [!DNL Segment Match]-Berechtigungen

Es gibt zwei Berechtigungen, die mit [!DNL Segment Match] verknüpft sind:

| Berechtigung | Beschreibung |
| --- | --- |
| Verbindungen für Zielgruppenfreigaben verwalten | Mit dieser Berechtigung können Sie den Partner-Handshake-Prozess abschließen, der zwei Organisationen verbindet, um [!DNL Segment Match]-Flüsse zu aktivieren. |
| Zielgruppenfreigaben verwalten | Mit dieser Berechtigung können Sie Feeds (das für die [!DNL Segment Match] verwendete Datenpaket) für aktive Partner (Partner, die vom Admin-Benutzer mit **[!UICONTROL Audience Share Connections]** Zugriff verbunden wurden) erstellen, bearbeiten und veröffentlichen. |

Weiterführende Informationen zu Zugriffssteuerung und Berechtigungen finden Sie in der [Übersicht zur Zugriffssteuerung](../../../access-control/home.md).

## [!DNL Segment Match]-End-to-End-Workflow

Nachdem Sie Ihre Identitätsdaten und Namespaces, die Einverständniskonfiguration und das Datennutzungs-Label eingerichtet haben, können Sie [!DNL Segment Match] und die zugehörigen Funktionen verwenden.

### Verwalten von Partnern

Wählen Sie in der Experience Platform-Benutzeroberfläche im linken Navigationsbereich die Option **[!UICONTROL Segments]** und dann in der oberen Zeile die Option **[!UICONTROL Feeds]** aus.

![segments-feed.png](./images/segments-feed.png)

Die Seite [!UICONTROL Feeds] enthält eine Liste der Feeds, die von Partnern empfangen wurden, sowie der Feeds, die Sie freigegeben haben. Um eine Liste der vorhandenen Partner anzuzeigen oder eine Verbindung zu einem neuen Partner herzustellen, wählen Sie **[!UICONTROL Manage partners]** aus.

![manage-partners.png](./images/manage-partners.png)

Eine Verbindung zwischen zwei Partnern ist ein „bidirektionaler Handshake“, der als Self-Service-Methode dient, mit der Benutzende ihre Experience Platform-Organisationen auf Sandbox-Ebene miteinander verbinden können. Die Verbindung ist erforderlich, um Experience Platform darüber zu informieren, dass eine Vereinbarung getroffen wurde und dass Experience Platform die gemeinsame Nutzung von Services zwischen Ihnen und Ihren Partnern erleichtern kann.

>[!NOTE]
>
>Der „bidirektionale Handshake“ zwischen Ihnen und Ihrem Partner ist ausschließlich eine Verbindung. Während dieses Vorgangs werden keine Daten ausgetauscht.

Sie können eine Liste der Verbindungen zu vorhandenen Partnern in der Hauptbenutzeroberfläche des [!UICONTROL Manage partners] Bildschirms anzeigen. In der rechten Leiste befindet sich das Bedienfeld [!UICONTROL Share setting] , über das Sie eine neue [!UICONTROL connect ID] sowie ein Eingabefeld zur Eingabe der [!UICONTROL connect ID] eines Partners generieren können.

![establish-connection.png](./images/establish-connection.png)

Um eine neue [!UICONTROL connect ID] zu erstellen, wählen Sie **[!UICONTROL Regenerate]** unter [!UICONTROL Share setting] und dann das Kopiersymbol neben der neu generierten ID aus.

![share-setting.png](./images/share-setting.png)

Um einen Partner über seinen [!UICONTROL connect ID] zu verbinden, geben Sie den Wert seiner eindeutigen ID in das Eingabefeld unter [!UICONTROL Connect partner] ein und wählen Sie dann **[!UICONTROL Request]** aus.

![connect-partner.png](./images/connect-partner.png)

### Erstellen eines Feeds {#create-feed}

>[!CONTEXTUALHELP]
>id="platform_segment_match_marketing"
>title="Eingeschränkte Marketing-Anwendungsfälle"
>abstract="Eingeschränkte Marketing-Anwendungsfälle helfen Ihren Partnern dabei, sicherzustellen, dass freigegebene Segmente gemäß Ihren Data-Governance-Beschränkungen ordnungsgemäß verwendet werden."
>text="Learn more in documentation"

Bei einem **Feed** handelt es sich um eine Gruppierung von Daten (Segmenten), die Regeln, wie diese Daten bereitgestellt oder verwendet werden können, und die Konfigurationen, die bestimmen, wie Ihre Daten mit den Daten Ihrer Partner abgeglichen werden. Ein Feed kann unabhängig verwaltet und mit anderen Experience Platform-Benutzenden über [!DNL Segment Match] ausgetauscht werden.

Um einen neuen Feed zu erstellen, wählen Sie im **[!UICONTROL Create feed]**-Dashboard die Option [!UICONTROL Feeds] aus.

![create-feed.png](./images/create-feed.png)

Die grundlegende Einrichtung eines Feeds umfasst einen Namen, eine Beschreibung und Konfigurationen zu Marketing-Anwendungsfällen und Identitätseinstellungen. Geben Sie einen Namen und eine Beschreibung für Ihren Feed ein und wenden Sie dann die Marketing-Anwendungsfälle an, von denen Ihre Daten ausgeschlossen werden sollen. Sie können mehr als einen Anwendungsfall aus einer Liste auswählen, die Folgendes enthält:

* [!UICONTROL Analytics]
* [!UICONTROL Combine with PII]
* [!UICONTROL Cross-site targeting]
* [!UICONTROL Data Science]
* [!UICONTROL Email targeting]
* [!UICONTROL Export to third party]
* [!UICONTROL Onsite advertising]
* [!UICONTROL Onsite personalization]
* [!UICONTROL Segment Match]
* [!UICONTROL Single identity personalization]

Wählen Sie abschließend die entsprechenden Identity-Namespaces für Ihren Feed aus. Informationen zu den spezifischen Namespaces, die von [!DNL Segment Match] unterstützt werden, finden Sie in der [Identitätsdaten- und Namenspaces-Tabelle](#namespaces). Wenn Sie fertig sind, wählen Sie **[!UICONTROL Next]** aus.

![audience-sharing.png](./images/audience-sharing.png)

Nachdem Sie die Einstellungen für Ihren Feed festgelegt haben, wählen Sie die Segmente aus, die Sie aus Ihrer Liste der Erstanbieter-Segmente freigeben möchten. Sie können mehr als ein Segment aus der Liste auswählen und die rechte Leiste verwenden, um Ihre Liste der ausgewählten Segmente zu verwalten. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Next]** aus.

![select-segments.png](./images/select-segments.png)

Die Seite [!UICONTROL Share] wird angezeigt und bietet Ihnen eine Oberfläche zur Auswahl der Partner, für die Sie Ihren Feed freigeben möchten. Während dieses Schritts können Sie auch den Bericht mit den Überschneidungsschätzungen vor der Freigabe anzeigen und die nach Namespace sortierte Anzahl der Identitäten mit Überschneidungen zwischen Ihnen und Ihrem Partner sowie die Anzahl der Identitäten mit Überschneidungen sehen, die mit der Datenfreigabe einverstanden sind.

Wählen Sie **[!UICONTROL Analyze by segment]** aus, um den Schätzbericht anzuzeigen.

![analyze.png](./images/analyze.png)

Der Bericht mit den Überschneidungsschätzungen ermöglicht es Ihnen, Überschneidungen und Einverständnisprüfungen pro Partner und Segment zu verwalten, bevor Sie Ihren Feed freigeben.

| Metriken | Beschreibung |
| ------- | ----------- |
| Geschätzte Identitäten mit Einverständnis | Die Gesamtzahl der Identitäten mit Überschneidungen, die die für Ihre Organisation konfigurierten Einverständnisanforderungen erfüllen. |
| Geschätzte Identitäten mit Überschneidungen | Die Anzahl der Identitäten, die sich für das ausgewählte Segment qualifizieren und auch dem ausgewählten Partner entsprechen. Diese Identitäten werden nach Namespace angezeigt und stellen keine individuellen Profilidentitäten dar. Die Überschneidungsschätzungen basieren auf Profilskizzen. |

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Close]** aus.

![overlap-report.png](./images/overlap-report.png)

Nachdem Sie Ihre Partner ausgewählt und den Bericht mit den Überschneidungsschätzungen angezeigt haben, wählen Sie **[!UICONTROL Next]** aus, um fortzufahren.

![share.png](./images/share.png)

Der Schritt [!UICONTROL Review] wird angezeigt, in dem Sie Ihren neuen Feed vor der Freigabe und Veröffentlichung überprüfen können. Dieser Schritt enthält Details zur angewendeten Identitätseinstellung sowie Informationen zu den von Ihnen ausgewählten Marketing-Anwendungsfällen, Segmenten und Partnern.

Wählen Sie **[!UICONTROL Finish]** aus, um fortzufahren.

![review.png](./images/review.png)

### Aktualisieren eines Feeds

Um Segmente hinzuzufügen oder zu entfernen, wählen Sie **[!UICONTROL Create feed]** auf der Seite [!UICONTROL Feeds] und dann **[!UICONTROL Existing feed]** aus. Wählen Sie in der angezeigten Liste der vorhandenen Feeds den Feed aus, den Sie aktualisieren möchten, und wählen Sie dann **[!UICONTROL Next]** aus.

![feed-list](./images/feed-list.png)

Die Liste der Segmente wird angezeigt. Von hier aus können Sie neue Segmente zu Ihrem Feed hinzufügen und über die rechte Leiste alle Segmente entfernen, die Sie nicht mehr benötigen. Nachdem Sie mit der Verwaltung der Segmente in Ihrem Feed fertig sind, wählen Sie **[!UICONTROL Next]** aus und führen Sie dann die oben beschriebenen Schritte aus, um den aktualisierten Feed abzuschließen.

![Aktualisieren](./images/update.png)

>[!NOTE]
>
>Wenn Sie ein Segment zu einem freigegebenen Feed hinzufügen oder daraus entfernen, muss der empfangende Partner die Änderung bestätigen, indem er den [!DNL Profile]-Umschalter in der Liste der empfangenen Feeds erneut aktiviert.

### Akzeptieren eines eingehenden Feeds

Um einen eingehenden Feed anzuzeigen, wählen Sie in der Kopfzeile der Seite **[!UICONTROL Received]** die Option [!UICONTROL Feeds] und dann den Feed aus der Liste aus, der angezeigt werden soll. Um den Feed zu akzeptieren, wählen Sie **[!UICONTROL Enable for profile]** aus und warten Sie einen Augenblick, bis sich der Status von [!UICONTROL Pending] auf [!UICONTROL Enabled] ändert.

![received.png](./images/received.png)

Sobald Sie einen freigegebenen Feed akzeptiert haben, können Sie mit der Verwendung der freigegebenen Daten beginnen, um neue Segmente zu erstellen.

## Nächste Schritte

Durch dieses Dokument haben Sie einen Einblick in [!DNL Segment Match], seine Funktionen und seinen End-to-End-Workflow gewonnen. Weitere Informationen zu anderen Platform-Services finden Sie in den folgenden Dokumenten:

* [[!DNL Segmentation Service]](../../home.md)
* [[!DNL Identity Service]](../../../identity-service/home.md)
* [[!DNL Real-Time Customer Profile] – Übersicht](../../../profile/home.md)
