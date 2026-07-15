## ADDED Requirements

### Requirement: List Tags
The system SHALL return all tags owned by the authenticated user.

#### Scenario: No tags
- **WHEN** a user has no tags
- **THEN** the system returns an empty array

#### Scenario: Multiple tags
- **WHEN** a user has created several tags
- **THEN** the system returns all tags with `id` and `name` fields

### Requirement: Create Tag
The system SHALL allow users to create new tags with unique names.

#### Scenario: Create new tag
- **WHEN** a user submits a new tag name
- **THEN** the system creates the tag and returns it with its ID

#### Scenario: Duplicate tag name
- **WHEN** a user creates a tag with a name that already exists for that user
- **THEN** the system returns an error indicating the tag already exists

### Requirement: Delete Tag
The system SHALL allow users to delete a tag and remove all article-tag associations.

#### Scenario: Delete tag with associations
- **WHEN** a user deletes a tag that is associated with articles
- **THEN** the system deletes the tag and removes all article-tag association records
