# Digital Signage Management Platform - Bubble.io (API-Focused)

This document captures the planned database structure, admin dashboard pages,
API endpoints, workflows and other requirements for the digital signage
management platform described by the project spec.

## Database Structure

Define the following data types in Bubble.io:

1. **Image** with fields: `name`, `file`, `uploadDate`, `displayDuration`,
   `versionAdded`, `isActive`, `fileSize`, `screenAssignments`, `createdBy`.
2. **Screen** with fields: `screenID`, `screenName`, `location`,
   `contactPerson`, `status`, `lastSeen`, `isActive`, `createdDate`,
   `lastVersion`.
3. **SystemVersion** with fields: `versionNumber`, `lastUpdated`,
   `updatedBy`, `changeDescription`.
4. **ScreenLog** with fields: `screen`, `logType`, `timestamp`, `details`,
   `version`.
5. **Settings** with fields: `defaultDuration`, `imageQuality`,
   `updateFrequency`, `maxFileSize`.

## Admin Dashboard

Pages include a dashboard, media management, screen management, analytics and
settings. The dashboard shows overall statistics such as active images and
screen counts. Media management handles file uploads and assignments to
screens. Screen management allows adding and editing screens. Analytics
aggregates logs and screen performance metrics. Settings hold global
configuration and version management.

## Key API Endpoints

- `GET /api/1.1/obj/systemversion` – used by displays to check the current
  system version.
- `GET /api/1.1/obj/image` – fetch active images. Supports parameters for
  `versionAdded` and `screenAssignments` for incremental updates.
- `PUT /api/1.1/obj/screen/[id]` – heartbeat updates from screens.
- `POST /api/1.1/obj/screenlog` – record screen events.
- Additional endpoints return screen-specific content.

## Workflows

Example workflows include:

1. **Image Upload** – create a new `Image`, set `uploadDate`, increment
   `SystemVersion` and update `versionAdded`.
2. **Screen Registration** – generate a unique `screenID`, create a `Screen`
   record, set default status and timestamps.
3. **Delete Image** – mark `Image` as inactive and increment `SystemVersion`.
4. **Screen Status Update** – update `Screen` info and create a `ScreenLog`.

## Testing Requirements

Functional and UI tests validate image upload, screen management, the API
responses, and responsive design. Review the specification for detailed test
cases.

