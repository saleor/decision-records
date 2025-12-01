# Update Webhook Emission Unification

Status: accepted

Summary: The `<entity>Update` webhook should be sent only for non-metadata changes on an instance, while the `<entity>MetadataUpdate>` webhook should be sent exclusively for metadata changes. This change aims to reduce redundant webhook events and improve clarity.

## Issue

Currently, the `<entity>Update` webhook is triggered even for metadata-only changes. This behavior leads to unnecessary webhook events, causing confusion and inefficiencies for clients relying on these events to track meaningful changes.

## Assumptions

- Clients use `<entity>Update` webhooks to track significant changes to entities.
- Metadata changes are often automated and do not require the same level of attention as other updates.
- Backward compatibility is critical for existing integrations.

## Constraints

- The solution must ensure backward compatibility to avoid breaking existing client implementations.
- The implementation should minimize performance overhead when determining the type of change.

## Background

Clients have reported that metadata updates generate hundreds of redundant `<entity>Update` webhook events daily. These events do not reflect actual changes to the entity itself, leading to inefficiencies and unnecessary processing on the client side.

## Future State

Starting from version 3.22, the `<entity>Update` webhook will only be triggered for actual changes to the entity, excluding metadata changes. Metadata changes will trigger the `<entity>MetadataUpdate>` webhook instead. This behavior will be controlled by an instance tracker to determine the type of change.

To ensure backward compatibility, a flag will be introduced to retain the current behavior for clients who rely on it. This flag will be documented and configurable.
