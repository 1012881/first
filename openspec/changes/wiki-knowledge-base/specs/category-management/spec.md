## ADDED Requirements

### Requirement: View Category Tree
The system SHALL return a recursive category tree structure for the authenticated user.

#### Scenario: Empty categories
- **WHEN** a user has no categories
- **THEN** the system returns an empty array

#### Scenario: Multi-level categories
- **WHEN** a user has created nested categories (e.g., "技术笔记 > Java > Spring")
- **THEN** the system returns a nested JSON tree with `children` arrays at each level
- **AND** each node contains `id`, `name`, `parentId`, and `children` fields

### Requirement: Create Category
The system SHALL allow users to create categories under any existing category or at root level.

#### Scenario: Create root-level category
- **WHEN** a user creates a category with `parentId` set to 0
- **THEN** the system creates the category at root level
- **AND** returns the created category with its ID

#### Scenario: Create sub-category
- **WHEN** a user creates a category with a valid `parentId`
- **THEN** the system creates the category as a child of the specified parent

### Requirement: Rename Category
The system SHALL allow users to rename an existing category.

#### Scenario: Successful rename
- **WHEN** a user updates the `name` of a category they own
- **THEN** the system updates the category name
- **AND** returns the updated category

### Requirement: Delete Category with Cascade
The system SHALL delete a category and all its descendants and associated articles.

#### Scenario: Delete leaf category
- **WHEN** a user deletes a category with no children
- **THEN** the system deletes the category and all articles under it

#### Scenario: Delete parent category
- **WHEN** a user deletes a category that has sub-categories
- **THEN** the system deletes the parent, all sub-categories, and all articles under them
