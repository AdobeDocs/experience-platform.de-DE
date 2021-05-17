---
audience: user
user-guide-title: Hilfe zum Experience-Datenmodell (XDM)-System
breadcrumb-title: Handbuch zum Experience-Datenmodell (XDM)
user-guide-description: Verwenden Sie Experience Data Model-(XDM-)Klassen und Schema-Feldgruppen, um Erlebnisdaten zu standardisieren.
feature: Schemas
source-git-commit: dcfdc9c479e8a77296f7cb0bf9f5bb36e9261b75
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 43%

---


# Experience-Datenmodell (XDM)-System {#xdm}

* [XDM-System – Übersicht](home.md)
* Schemas {#schema}
   * [Grundlagen der Schema-Komposition](schema/composition.md)
   * [Bewährte Verfahren für die Datenmodellierung](schema/best-practices.md)
   * [XDM-Feldtypeinschränkungen](schema/field-constraints.md)
   * [Benennung in XDM](./schema/namespaces.md)
   * [Wörterbuch der XDM-Felder](schema/field-dictionary.md)
   * Branchendatenmodelle {#industries}
      * [Übersicht](./schema/industries/overview.md)
      * [Einzelhandelsdatenmodell ERD](./schema/industries/retail.md)
      * [Datenmodell für Finanzdienstleistungen ERD](./schema/industries/financial.md)
      * [Reise- und Gastfreundschaftsdatenmodell ERD](./schema/industries/travel-hospitality.md)
* Klassen {#classes}
   * [XDM Individuelles Profil](./classes/individual-profile.md)
   * [XDM ExperienceEvent](./classes/experienceevent.md)
   * [Segmentdefinition](./classes/segment-definition.md)
* Schema-Feldgruppen {#field-groups}
   * Profil-Feldgruppen {#profile}
      * [IdentityMap](./field-groups/profile/identitymap.md)
      * [Demografische Details](./field-groups/profile/demographic-details.md)
      * [Persönliche Kontaktangaben](./field-groups/profile/personal-contact-details.md)
      * [Details zur Segmentmitgliedschaft](./field-groups/profile/segmentation.md)
      * [Kontaktangaben bearbeiten](./field-groups/profile/work-contact-details.md)
      * [Datenschutz/Personalisierung/Marketing-Voreinstellungen (Zustimmung)](./field-groups/profile/consents.md)
   * Ereignis-Feldgruppen {#event}
      * [Details zur Endbenutzer-ID](./field-groups/event/enduserids.md)
      * [Umgebung](./field-groups/event/environment-details.md)
   * [Aktualisierung der Feldgruppennamen](./field-groups/name-updates.md)
* Datentypen {#data-types}
   * [Anwendung](./data-types/application.md)
   * [Beacon](./data-types/beacon.md)
   * [Browserdetails](./data-types/browser-details.md)
   * [Handel](./data-types/commerce.md)
   * [Zustimmung und Voreinstellungen](./data-types/consents.md)
   * [Gerät](./data-types/device.md)
   * [E-Mail  Adresse](./data-types/email-address.md)
   * [Umgebung](./data-types/environment.md)
   * [Allgemeines Feld für Zustimmung](./data-types/consent-field.md)
   * [Feld für allgemeine Marketingpräferenzen](./data-types/marketing-field.md)
   * [Allgemeines Feld für Marketingpräferenzen mit Abonnements](./data-types/marketing-field-subscriptions.md)
   * [Feld für allgemeine Personalisierungseinstellungen](./data-types/personalization-field.md)
   * [Geo](./data-types/geo.md)
   * [Geo-Kreis](./data-types/geo-circle.md)
   * [Geo-Koordinaten](./data-types/geo-coordinates.md)
   * [Details zur Geo-Interaktion](./data-types/geo-interaction-details.md)
   * [Geo-Form](./data-types/geo-shape.md)
   * [Identität](./data-types/identity.md)
   * [Maßnahme](./data-types/measure.md)
   * [Bestellung](./data-types/order.md)
   * [Zahlungsbefehl](./data-types/payment-item.md)
   * [Person](./data-types/person.md)
   * [Personenname](./data-types/person-name.md)
   * [Telefonnummer](./data-types/phone-number.md)
   * [Ortskontext](./data-types/place-context.md)
   * [POI-Details](./data-types/poi-details.md)
   * [POI-Interaktion](./data-types/poi-interaction.md)
   * [Postadresse](./data-types/postal-address.md)
   * [Durchsuchen](./data-types/search.md)
   * [Abonnement](./data-types/subscription.md)
   * [Webinteraktion](./data-types/web-interactions.md)
   * [Webseitendetails](./data-types/webpage-details.md)
*  SchemasUI  {#ui}
   * [Übersicht](./ui/overview.md)
   * [XDM-Ressourcen](./ui/explore.md)
   * Ressourcen {#resources} erstellen und bearbeiten
      * [Schemas](./ui/resources/schemas.md)
      * [Klassen](./ui/resources/classes.md)
      * [Feldergruppen](./ui/resources/field-groups.md)
      * [Datentypen](./ui/resources/data-types.md)
   * Felder {#fields} definieren
      * [Übersicht](./ui/fields/overview.md)
      * [Erforderliche Felder](./ui/fields/required.md)
      * [Objektfelder](./ui/fields/object.md)
      * [Array-Felder](./ui/fields/array.md)
      * [Enum-Felder](./ui/fields/enum.md)
      * [Identitätsfelder](./ui/fields/identity.md)
      * [Beziehungsfelder](./ui/fields/relationship.md)
   * [Beispiel-XDM-Daten generieren](./ui/sample.md)
   * [XDM-Schemas exportieren](./ui/export.md)
* Schema Registry-API {#api}
   * [Übersicht](api/overview.md)
   * [Erste Schritte](api/getting-started.md)
   * [Schemas](api/schemas.md)
   * [Verhalten](api/behaviors.md)
   * [Klassen](api/classes.md)
   * [Schema-Feldgruppen](api/field-groups.md)
   * [Datentypen](api/data-types.md)
   * [Deskriptoren](api/descriptors.md)
   * [Vereinigungen](api/unions.md)
   * [Export/Import](api/export-import.md)
   * [Sample data](api/sample-data.md)
   * [Auditprotokoll](api/audit-log.md)
   * [Ad-hoc-Schemata](api/ad-hoc.md)
   * [Mixins (nicht mehr unterstützt)](api/mixins.md)
   * [Anhang](api/appendix.md)
* Tutorials {#tutorials}
   * [Erstellen eines Schemas (Benutzeroberfläche)](tutorials/create-schema-ui.md)
   * [Erstellen eines Schemas (API)](tutorials/create-schema-api.md)
   * [Definieren einer Beziehung zwischen zwei Schemata (Benutzeroberfläche)](tutorials/relationship-ui.md)
   * [Definieren einer Beziehung zwischen zwei Schemata (API)](tutorials/relationship-api.md)
   * [Erstellen eines Ad-hoc-Schemas (API)](tutorials/ad-hoc.md)
* [Handbuch zur Fehlerbehebung](troubleshooting-guide.md)
* [API-Referenz](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)
* [Versionshinweise zur Plattform](https://docs.adobe.com/content/help/de-DE/experience-platform/release-notes/latest.html)