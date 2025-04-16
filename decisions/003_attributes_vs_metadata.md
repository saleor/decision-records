# Attributes vs Metadata (and why we need both)

Status: accepted

Summary: Saleor uses Attributes and Metadata and it's not immediately clear why we need both and what purpose they serve.

## Current status

Saleor uses both Attributes and Metadata in various places. Attributes have a strict structure with data types, validation, schema etc. Metadata is a simple `key: value` structure without types. There were client and community requests to add sophisticated filtering using metadata, to make metadata use a schema or to change how attributes behave. Were do we go with this? What do we use where? Do we need both? Let's dive in!

### Attributes vs. Metadata difference
TL;DR ✨ Attributes are for people, metadata are for apps.

Attributes:

- intended to be filled in by people
- strictly typed
- the schema is strict so that storefronts can depend on this value being of a specific shape e.g. a field for number of pages will not contain a photo of jeans
- attributes are typically used in the UI layer, presented to customers, merchandisers, or admins and this could also mean: localized and prioritized for performance

Metadata

- intended to be filled by an app, an automation or integration through the API
- validation should happen in unit tests of the app
- metadata has no schema so that it doesn’t require a human to change how the code is operating with them

### Future of Attributes

In light of the above, we will be adding attributes only to places where it makes sense to have data with a strict schema.

In order to do it properly we need to finish the https://github.com/saleor/saleor/discussions/14417 so that we can then also add new relation types. Right now it’s only Pages, Products and ProductVariants. This is not a strict requirement but it would be good to clean this space before we build more complexity on top of this.

### Future of Metadata: proper JSON representation

Metadata is stored as a JSON representation in the database (jsonb PostgreSQL type). Right now we always cast it to a `string: string` mapping. We want to start keeping the values as they come through JSON values so that customer apps don’t need to cast the data to a type they need for a certain value.

We also want to add metadata to all the places that would help with modeling of customer approaches where our core structures are not enough.