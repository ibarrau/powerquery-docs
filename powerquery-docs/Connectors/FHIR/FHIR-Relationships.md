---
title: FHIR Power Query Relationships
description: FHIR Power Query connector table relationships
author: hansenms
ms.service: powerquery
ms.topic: conceptual
ms.date: 01/08/2020
ms.author: mihansen
LocalizationGroup: reference
---

# FHIR Relationships

This article describes how to establish [relationships](https://docs.microsoft.com/power-bi/desktop-create-and-manage-relationships) between tables that have been imported using the FHIR Power Query connector.

## Introduction

FHIR resources are related to each other, e.g. an `Observation` references a subject (`Patient`):

```json
{
    "resourceType": "Observation",
    "id": "1234",
    "subject": {
        "reference": "Patient/456"
    }

    // ... Other fields
}
```

Some of the resource reference fields in FHIR can refer to multiple different types of resources (e.g. `Practitioner` or `Organization`). To facilitate an easier way to resolve references, the FHIR Power Query connector adds a synthetic field to all imported resources call `<referenceId>`, which contains a concatenation of the resource type and the resource id.

To establish a relationship between two tables, you can connect a specific reference field on a resource to the corresponding `<referenceId>` field on the resource you would like it linked to. In simple cases, Power BI will even detect this for you automatically.

## Establishing FHIR relationships in Power BI

In this section, we will show an example of establishing a relationship between the `Observation.subject.reference` field and the `<referenceId>` field on `Patient`.

1. When importing data, select the `Patient` and `Observation` tables:

    ![FHIR Navigation Two Resources](FHIR-Navigate-TwoResources.png)

    Then click **Transform Data**.

1. Expand the `subject` column on `Observation` to reveal `subject.reference`:

    ![Expand subject reference](FHIR-ExpandSubject.png)

    After expanding, you should see the list of subject references:

    ![Subject references expanded](FHIR-ExpandedSubjectReference.png)

1. Make any other modifications you need to the query and save the modified query.

1. Click **Manage Relationships** in the Power BI client:

    ![Manage relationships](FHIR-ManageRelationships.png)

1. Establish the relationship. In this simple example, Power BI will likely have detected the relationship automatically:

    ![Autodetected relationship](FHIR-RelationshipEstablished.png)

    If not, you can add it manually:

    ![Manually add relationship](FHIR-NewRelationship.png)

    You can edit the details of the relationship:

    ![Edit relationship](FHIR-EditRelationship.png)


## Summary

Resources in FHIR are related. These relationships need to be established on data imported with the FHIR Power Query connector. The `<referenceId>` field is a synthetic field added to all imported FHIR data which will help establish the relationships.

## Next steps

In this article, you have learned how to establish relationships between tables imported with the FHIR Power Query connector. Next explore query folding with the FHIR Power Query connector.

>[!div class="nextstepaction"]
>[FHIR Power Query folding](FHIR-QueryFolding.md)