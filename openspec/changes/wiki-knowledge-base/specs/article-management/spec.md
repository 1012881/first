## ADDED Requirements

### Requirement: Create Article
The system SHALL allow users to create articles with title, rich text content, category, tags, and status.

#### Scenario: Create as draft
- **WHEN** a user creates an article with `status` set to 0
- **THEN** the system saves the article as a draft
- **AND** returns the created article with its ID

#### Scenario: Create as published
- **WHEN** a user creates an article with `status` set to 1
- **THEN** the system saves and publishes the article
- **AND** the article appears in the article list

#### Scenario: Create with tags
- **WHEN** a user creates an article with `tagIds` array containing valid tag IDs
- **THEN** the system associates the specified tags with the article
- **AND** the article detail response includes the tag list

### Requirement: View Article List
The system SHALL return a paginated list of articles with multi-dimensional filtering.

#### Scenario: List all published articles
- **WHEN** a user requests the article list without filters
- **THEN** the system returns paginated published articles ordered by update time descending

#### Scenario: Filter by category
- **WHEN** a user requests articles with `categoryId` parameter
- **THEN** the system returns only articles under that category

#### Scenario: Filter by tag
- **WHEN** a user requests articles with `tagId` parameter
- **THEN** the system returns only articles associated with that tag

#### Scenario: Search by keyword
- **WHEN** a user requests articles with `keyword` parameter
- **THEN** the system returns articles whose title contains the keyword (LIKE search)

#### Scenario: Combine filters
- **WHEN** a user provides `categoryId`, `tagId`, and `keyword` simultaneously
- **THEN** the system returns articles matching ALL conditions (AND logic)

### Requirement: View Article Detail
The system SHALL return full article details including tags and increment the view count.

#### Scenario: View published article
- **WHEN** a user requests a published article by ID
- **THEN** the system returns the article with title, content, category, tags, and metadata
- **AND** increments the view count by 1

#### Scenario: View draft article
- **WHEN** a user requests a draft article by ID
- **THEN** the system returns the article without incrementing the view count

### Requirement: Update Article
The system SHALL allow users to update article title, content, category, tags, and status.

#### Scenario: Update all fields
- **WHEN** a user updates an article with new title, content, categoryId, status, and tagIds
- **THEN** the system updates all fields
- **AND** replaces the article's tag associations with the new tagIds

#### Scenario: Update tags only
- **WHEN** a user updates an article with only changed `tagIds`
- **THEN** the system removes old tag associations and creates new ones

### Requirement: Delete Article
The system SHALL allow users to delete an article they own.

#### Scenario: Successful deletion
- **WHEN** a user deletes an article they own
- **THEN** the system deletes the article and all its tag associations
- **AND** returns a success response
