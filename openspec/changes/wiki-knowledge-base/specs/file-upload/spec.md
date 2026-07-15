## ADDED Requirements

### Requirement: Image Upload
The system SHALL allow authenticated users to upload images for use in rich text articles.

#### Scenario: Upload valid image
- **WHEN** a user uploads a JPG, PNG, or GIF file under 5MB
- **THEN** the system saves the file to the uploads directory with a unique filename
- **AND** returns the accessible URL of the uploaded image

#### Scenario: Upload oversized file
- **WHEN** a user uploads an image file larger than 5MB
- **THEN** the system returns an error indicating the file size exceeds the limit

#### Scenario: Upload invalid file type
- **WHEN** a user uploads a non-image file
- **THEN** the system returns an error indicating the file type is not supported

### Requirement: Image Access
The system SHALL serve uploaded images via static URL mapping.

#### Scenario: Access uploaded image
- **WHEN** a browser requests an image URL returned from the upload endpoint
- **THEN** the system serves the image file with the correct Content-Type header
