## Contribute to Okto Documentation

Thank you for your interest in contributing to the Okto documentation! We value community contributions and appreciate you taking the time to help improve our documentation.  Please read these guidelines carefully to ensure a smooth and efficient contribution process.

## Table of Contents

- [Development Workflow](#development-workflow)
- [Documentation Standards](#documentation-standards)
    - [Content Structure and Format](#content-structure-and-format)
    - [Writing Style Guidelines](#writing-style-guidelines)
- [Contributing to Documentation](#contributing-to-documentation)
- [Contributing to OpenAPI scripts](#contributing-to-openapi-scripts)
    - [Contributing to Existing OpenAPI Sections](#contributing-to-existing-sections)
    - [Creating a New OpenAPI Section](#creating-a-new-openapi-section)
- [Contribution Review Process](#contribution-review-process)
- [Issue Reporting](#issue-reporting)
    - [Issue Report Template](#issue-report-template)
    - [Documentation Enhancement Request](#documentation-enhancement-request)
- [Join the Community](#join-the-community)

## Development Workflow

To contribute to the Okto documentation, please follow this standard Git workflow:

1.  **Fork the Repository:** Create your own fork of the `okto-sdk-docs-v2` repository on GitHub.

2.  **Create a Feature Branch:**  Create a dedicated branch for your contribution, named descriptively:
    ```bash
    git checkout -b feat/your-feature-name 
    # Example: git checkout -b feat/improve-authentication-guide
    ```

3.  **Commit Your Changes:** Make your documentation changes and commit them.  Please adhere to [Conventional Commits](https://www.conventionalcommits.org) for commit message formatting. This helps us maintain a clear and organized commit history.
    ```bash
    git commit -m "docs: improve authentication guide clarity"
    ```

4.  **Push to Your Fork:** Push your feature branch to your forked repository on GitHub:
    ```bash
    git push origin feat/your-feature-name
    ```

5.  **Submit a Pull Request (PR):** Open a Pull Request against the `main` branch of the main `okto-sdk-docs-v2` repository.  Please provide a clear and concise description of your changes in the PR.

## Documentation Standards

To maintain a high standard of quality and consistency across the Okto documentation, please adhere to the following guidelines:

### Content Structure and Format

*   **Use MDX for Interactivity:**  Utilize MDX (Markdown + JSX) to create interactive documentation components and enhance user engagement.
*   **Maintain Existing Hierarchy:**  When adding new documentation, please follow the established directory structure and hierarchy.  For example, SDK-specific documentation should be organized as follows:

    ```
    /docs
    ├── [sdk-name]         (e.g., /docs/react-sdk)
    │   ├── getting-started   
    │   ├── usage           
    │   ├── api-reference
    │   ├── ui-customization 
    │   └── troubleshooting  
    ```

### Writing Style Guidelines

*   **Conciseness:** Keep paragraphs concise and focused, ideally under 5 lines for readability.
*   **Active Voice:**  Write in an active voice for clarity and directness.
*   **Code Samples are Essential:**  Include clear and well-formatted code samples for *all* code-related explanations.
*   **Visual Aids for Complex Flows:**  Use Mermaid diagrams to visually represent complex workflows, processes, or architectural components.
*   **Link Verification:**  Please verify all external links monthly to ensure they are still active and relevant.
*   **Use Headers Properly:**  Structure content with properly nested headers (h2, h3, h4) for clear organization.

## Contributing to Documentation

Okto Docs uses a Next.js-based routing structure, with all content stored under the `content/docs/` directory. If you want to contribute to the docs, you will primarily work within this directory to add or update documentation.

If you want to contribute to components, these are located in the `app/components/` directory.

### Adding New Section or Guides

1.  **Create a Directory or Guide:** Follow the [Content Structure Format](#content-structure-and-format) and create a new directory or a new `.mdx` guide under the appropriate section within `content/docs/`.

2.  **Update meta.json:** In the new directory, add a `meta.json` file defining its structure. If you created a new guide, add it to the `meta.json` in that directory to ensure it appears in the navigation.

### Updating Existing Docs

1.  **Locate and Edit Existing Guides:** Navigate to the relevant section in `content/docs/` and apply your updates to the necessary `.mdx` files.

### Updating Components

1.  **Edit Global Components:** If you need to update reusable global components (for e.g., `Navbar`, `Footer`, etc.), edit files under `app/components/`.

2.  **Edit MDX-Specific Components:** If you need to update components used within `.mdx` files, edit files under `app/components/mdx/`.

## Contributing to OpenAPI Scripts

Okto uses OpenAPI auto-generated scripts to maintain up-to-date API documentation across:

*   **API Reference Section (Explorer, Auth, Intents)**  
*   **Trade Service Section**

This section will help you contribute to Okto's API documentation in a structured way.

## Contributing to Existing OpenAPI Sections

### Updating Existing Theory Guides

Theory guides are conceptual documentation that explain how APIs work and how to use them (like `index.mdx`, `overview.mdx`, `setup.mdx`).

1.  **Locate the Relevant Guide:** Locate the relevant guide in:
* `content/docs/openapi/` (API Reference guides)
* `content/docs/trade-service/` (Trade Service guides)

2.  **Verify and Submit:** Confirm your changes locally, commit them, and open a pull request for review.

### Adding New Theory Guides 

1.  **Add Your Guide:** Place your new `.mdx` guide in the appropriate directory:

    *   **For API Reference:** `content/docs/openapi/` 
    *   **For Trade Service:** `content/docs/trade-service/` 

2. **Update meta.json:** Update the `meta.json` in that directory to include your new guide in navigation.

3.  **Update Generation Scripts:** Update the relevant script in the `scripts/` directory so your guide is **retained during regeneration**.

    *    **For API Reference:** If you add a guide in `content/docs/openapi/`, update `scripts/generate-api-reference-docs-explorer.mjs` to include your new guide.

    *   **For Trade Service:** If you add a guide in `content/docs/trade-service/`, update `scripts/generate-trade-service-docs.mjs` to include your new guide.

    In these scripts, there is a `return()` statement filtering which files to keep. Add your new guide’s filename, so it’s included during regeneration. For example:

    ``` 
        !v.endsWith("index.mdx") &&
        !v.endsWith("overview.mdx") &&
        !v.endsWith("setup.mdx") &&
        !v.endsWith("meta.json") &&
        ....
        !v.endsWith("YOUR_NEW_GUIDE.mdx")
    ```

### Adding or Updating Endpoints

Follow these steps when you want to add new API endpoints or modify existing endpoint documentation.

1.  **Modify the relevant OpenAPI JSON file:** Locate and edit the correct file under `public/openapi/`:

    *   **For API Reference:**

        `public/openapi/openapi-explorer.json`

        `public/openapi/auth/openapi.json`

        `public/openapi/intents/openapi.json`

    *   **For Trade Service:**

        `public/openapi/openapi-trade-service.json`

2.  **Regenerate the documentation:** Run the appropriate build command based on where you made changes.

    *   **For API Reference (Explorer):**
        ```bash
        npm run build:api-reference-docs-explorer
        ```

    *   **For API Reference (Auth):**
        ```
        npm run build:api-reference-docs-auth
        ```

    *   **For API Reference (Intents):**
        ```
        npm run build:api-reference-docs-intents
        ```

    *   **For Trade Service:**
        ```
        npm run build:trade-service-docs
        ```

3.  **Verify your changes:** Check that your updated or new endpoints appear correctly in the generated documentation.

> *Ensure no unintended file changes occurred during regeneration.*

## Creating a New OpenAPI Section

Follow these steps, when you need to add a completely new OpenAPI section (for example, a new service's API documentation).

1. **Create the Content Folder:** Create a new folder under `content/docs/` (e.g., `content/docs/new-service/`) with your `.mdx` theory guides and a `meta.json` file for navigation structure.

2. **Add the OpenAPI JSON File:** Place your OpenAPI JSON in `public/openapi/` (e.g., `public/openapi/openapi-new-service.json`).

> *Ensure the JSON is valid and follows the OpenAPI structure used in other Okto sections.*

3. **Create the Generation Script:** Add a new script `scripts/generate-new-service-docs.mjs` in the `scripts/` directory, using existing scripts as reference. Refer to the existing scripts (e.g. `generate-trade-service-docs.mjs`).

4. **Add NPM Script for Regeneration:** In `package.json`, add a new command:
`"build:new-service-docs": "node scripts/generate-new-service-docs.mjs"`.
This will allow consistent regeneration during local dev and CI.

5. **Test Locally:** Execute your build command
    ```bash
    npm run build:new-service-docs
    ``` 
    and verify that endpoint documentation is generated correctly, theory guides are retained, and the section appears in your local docs site.

> ***Tip:** Keep your new script structure consistent with existing scripts for maintainability.*

## Contribution Review Process

Once you've prepared your documentation improvements and submitted a pull request, here's what happens next:

1. The Okto documentation team will review your contribution
2. We may suggest changes or improvements
3. Once approved, your contribution will be merged into the main branch
4. Your name will be added to our contributors list (unless you opt out)

## Issue Reporting

Not ready to contribute code yet? You can still help improve our documentation by reporting issues you encounter while using it. Identifying problems is the first step toward better documentation.

If you encounter errors, or areas for improvement in the documentation, please help us by submitting detailed issue reports.  Documentation issues might include:

- Incorrect or missing information
- Outdated Content
- Unclear explanations
- Broken links
- Code samples that don't work
- Formatting problems

### Issue Report Template

When reporting an issue with the documentation, please include:

```markdown
## Documentation Issue

**Page URL/Location:** [URL or path to the affected page]

**Issue Type:** [Missing information/Incorrect information/Unclear explanation/Outdated content/Broken link/Code sample issue/Typo or grammar/Formatting]

**Description:**
[Provide a clear description of the issue you found]

**Current Content:** (if applicable)
[Quote the current problematic content]

**Suggested Improvement:** (if you have one)
[Describe how you think the documentation could be improved]

**Screenshots:** (if applicable)
[Attach screenshots highlighting the issue]

**Additional Context:**
[Any additional information that might help understand the issue]
```

### Documentation Enhancement Request

If you have ideas for improving or expanding the documentation, we welcome your enhancement suggestions through our standardized request process.

```markdown
## Documentation Enhancement Request

**Documentation Area:** [Specify which part of the documentation this enhancement relates to]

**Enhancement Type:** [New content/Expanded explanation/Reorganization/Better examples/Visual aids/Other]

**Description:**
[Describe clearly what you think should be added or improved in the documentation]

**Who Would Benefit:**
[Explain which users would benefit from this enhancement and how]

**Proposed Structure:** (if applicable)
[If suggesting new content, provide an outline of how you think it should be structured]

**Examples/References:** (if applicable)
[Include examples or references to similar documentation elsewhere that illustrates your idea]
```

## Join the Community

For real-time discussions, questions, and collaboration, please join our [Discord Server](https://discord.com/invite/okto-916349620383252511).

---

Thank you for helping make Okto documentation better for everyone!