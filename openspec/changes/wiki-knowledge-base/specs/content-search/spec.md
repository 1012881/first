## ADDED Requirements

### Requirement: Full-Text Search
The system SHALL support keyword-based search on article titles.

#### Scenario: Matching keyword
- **WHEN** a user searches with a keyword that exists in article titles
- **THEN** the system returns all articles whose titles contain the keyword (case-insensitive)

#### Scenario: No match
- **WHEN** a user searches with a keyword that matches no article titles
- **THEN** the system returns an empty list

### Requirement: Multi-Dimensional Filtering
The system SHALL support simultaneous filtering by category, tag, and keyword.

#### Scenario: Category + keyword filter
- **WHEN** a user filters by both `categoryId` and `keyword`
- **THEN** the system returns articles that belong to the category AND whose title matches the keyword

#### Scenario: Category + tag filter
- **WHEN** a user filters by both `categoryId` and `tagId`
- **THEN** the system returns articles that belong to the category AND are tagged with the specified tag

### Requirement: Paginated Results
The system SHALL return search results with pagination metadata.

#### Scenario: First page request
- **WHEN** a user requests page 1 with size 10
- **THEN** the system returns at most 10 articles
- **AND** includes total count, current page, and page size in the response
