---
id: overview
title: Overview
---

The `@ws-ui/webform-editor` package is a specialized webform editor library crafted explicitly for integration with the Qodly Studio Editor. With a focus on delivering a robust set of tools, components, and functionalities, this package empowers users to seamlessly create, customize, and manage web forms within the Qodly Studio environment.

## Key Features

1. **Web Form Creation:** The package provides a collection of components and utilities dedicated to constructing web forms. These tools offer diverse options for input fields, controls, and design elements.

2. **Customization:** Users have the flexibility to customize the visual appearance and functional behavior of web forms through the editor. This empowers them to tailor the user experience to specific project requirements.

3. **Integration:** Designed with integration in mind, the library seamlessly embeds itself within the Qodly Studio Editor. This integration fosters a cohesive and unified working environment for users to efficiently develop and enhance their projects.

## Global Project Structure

The global project structure of `@ws-ui/webform-editor` is designed to maintain a clear organization. Here's a brief explanation of each key file and directory:

- **src**: Encapsulates the core functionality of `@ws-ui/webform-editor`
    - [**components**](components/overview): Dedicated space for components tailored for web form editing.
    - [**hooks**](hooks): Repository for custom hooks providing specialized functionalities.
    - [**interfaces**](interfaces): TypeScript interfaces defining the structure of data used in the project.
    - [**mocks**](mocks): Contains simulated versions of dependencies and data, enabling isolated testing of components without relying on external systems.
    - [**providers**](providers): Context providers managing state across the application.
    - [**renderer**](renderer): Components responsible for rendering web forms.
    - [**StandaloneEditor**](StandaloneEditor): Houses the components, styles, and logic necessary to operate the standalone editor within your application, enabling editing functionalities like code or web form customization independently from other parts of the system.
    - [**themes**](themes): Configuration files specifying theme-related settings.
    - [**utils**](utils): Collection of utility functions used throughout the project.
    - **editor.d.ts**: TypeScript declaration file providing type information for the webform editor. It defines modules for custom components and CSS box shadow parsing.
    - **index.css**: Main stylesheet defining visual aspects, including styling for component inspection, selection, and other UI elements.
    - **index.ts**: Entry point for the project, importing and exporting various modules.
    - **main.tsx**: Serves as the primary entry point for running the application. It initializes the React app, setting up providers, contexts, and rendering the root component.
    - **monaco-workers.ts**: Related to the Monaco Editor, used in web projects for code editing functionalities. The workers handle background tasks such as syntax validation or other language features provided by the Monaco Editor.
    - **theme.ts**: Configuration file for Chakra UI theme, extending default theme settings and defining custom colors and fonts.
    - **vite-env.d.ts**: TypeScript declaration file including references to external types related to the project.
    - **Webform.tsx**: Main component for web form editing. It uses Chakra UI, Craft.js, and other providers to create a flexible and extensible web form editor with various features and settings.

- **.eslintrc.cjs**: ESLint configuration file for maintaining code quality.

- **.gitignore**: File specifying patterns for files and directories to be ignored by version control.

- **.prettierrc**: Prettier configuration file defining code formatting rules.

- **package-lock.json**: Auto-generated file specifying exact versions of project dependencies.

- **package.json**: Main configuration file for Node.js projects, including project metadata and scripts.

- **postcss.config.js**: Configuration file for PostCSS, a tool for transforming styles.

- **README.md**: Documentation file providing an overview of the project.

- **tailwind.config.js**: Configuration file for Tailwind CSS, a utility-first CSS framework.

- **tsconfig.json**: TypeScript configuration file specifying compiler options and project structure.

- **tsconfig.node.json**: TypeScript configuration file specifically for Node.js.

- **tsdoc.json**: Configuration file for TypeScript documentation generation.

- **typedoc.json**: Configuration file for TypeDoc, a documentation generator for TypeScript.

- **vite.config.ts**: Configuration file for Vite, a frontend build tool.
