# README

## 📖 Introduction
This project provides a powerful **TypeScript type generation tool** for Appwrite projects. By integrating this tool, you can streamline your development process, ensuring robust type safety and better code quality. Whether you're working on a simple project or managing complex schemas with intricate relationships, this generator simplifies type management.

---

## 🛠️ Technical Overview
- **Type Safety**: Automatically generates TypeScript types from Appwrite project configurations.
- **Relationship Inference**: Supports complex relationship type inference for better schema representation.
- **Enum & Union Types**: Generates both enum and union type definitions for flexibility.
- **Comprehensive Error Handling**: Ensures reliability and clarity during type generation.
- **Seamless Integration**: Designed for effortless integration with Appwrite projects.

---

## 🌟 Key Features
- ✅ **Automatic Type Generation**: Say goodbye to manual typing.
- ✅ **Relationship Type Support**: Handles even complex relationships in your schemas.
- ✅ **Enum and Union Definitions**: Creates structured and extensible type definitions.
- ✅ **Error Handling**: Offers detailed feedback to help resolve issues quickly.
- ✅ **Developer-Friendly**: Easy to set up and integrate into any Appwrite + TypeScript project.

---

## 📋 Prerequisites
Before using this tool, ensure you have the following:
- **Node.js**: Version 16+ (recommended)
- **Appwrite Project**: A configured Appwrite backend project
- **TypeScript Project**: A TypeScript environment for your frontend or backend application

---

## 🚀 Installation

### Global Installation
Install the generator globally to use it across projects:
```bash
npm install -g @Joe2512/appwrite-types-generator
```

### Project-Level Installation
Add the generator as a development dependency to your project:
```bash
npm install --save-dev @Joe2512/appwrite-types-generator
```

### Known Issue
If you get dependencie error because of react 19 just use --legacy-peer-deps
```bash
npm install --save-dev @Joe2512/appwrite-types-generator --legacy-peer-deps
```

---

## ⚙️ Configuration

### 1. **Appwrite Project Configuration**
To use this tool, you need an Appwrite project configuration file (`appwrite.json`). This file contains your Appwrite project's structure and schema. Follow these steps:

#### Step 1: Install the Appwrite CLI
The Appwrite CLI is essential for managing your project configuration. If you don't have it installed, follow the [Appwrite CLI Installation Guide](https://appwrite.io/docs/command-line).

#### Step 2: Pull Your Project Configuration
Run the following command to generate the `appwrite.json` file:
```bash
appwrite projects get --output-file appwrite.json
```

Alternatively, you can use:
```bash
appwrite pull
```
This will download your project configuration and place it in the root directory.

> 📝 **Note**: Ensure your CLI is authenticated and connected to the correct Appwrite project. For more details, refer to the [Appwrite CLI Documentation](https://appwrite.io/docs/command-line#projects).

---

### 2. **Type Generation Configuration**
Once you have the `appwrite.json`, create a `appwrite-types.config.json` file in your project root. This file tells the generator where to find your configuration and where to output the types.

Example:
```json
{
  "inputPath": "./appwrite.json",
  "outputPath": "./src/lib/appwrite/types.ts"
}
```

- `inputPath`: Path to your `appwrite.json` file.
- `outputPath`: Desired location for the generated TypeScript types.

---

## 🛠️ Usage

### CLI Usage
Run the generator directly from the command line:
```bash
# Generate types from project configuration
npx appwrite-types-gen

# Use a custom configuration file
npx appwrite-types-gen --config custom-config.json
```

### Options
| Option                  | Description                                              |
|-------------------------|----------------------------------------------------------|
| `-c, --config <path>`   | Path to a custom configuration file.                     |
| `-o, --output <path>`   | Custom output path for the generated types.              |
| `--no-enums`            | Disable enum generation.                                 |
| `--no-interfaces`       | Disable interface generation.                            |
| `--no-database`         | Disable Database constant generation.                    |
| `--no-collections`      | Disable Collection constants generation.                 |

### Example
Generate TypeScript types with a custom configuration file and output path:
```bash
appwrite-types-gen -c ./appwrite-config.json -o ./src/types
```

Skip enum and interface generation:
```bash
appwrite-types-gen --no-enums --no-interfaces
```

### npm Script Integration
Integrate type generation into your development workflow by adding scripts to your `package.json`:
```json
{
  "scripts": {
    "generate:types": "appwrite-types-gen",
    "prebuild": "npm run generate:types"
  }
}
```

Run the type generation script:
```bash
npm run generate:types
```

> 💡 **Tip**: Use the `prebuild` hook to ensure types are always generated before building your project.

---

## 🔍 Example Generated Types
Here is a sample of the output generated by this tool:

```typescript
// Automatically generated types
export type TournamentActiveWeaponType = "epee" | "foil" | "sabre";

export interface Tournament {
  activeWeapons?: TournamentActiveWeaponType[];
  // Fully typed Appwrite document
}
```

---

## 🔧 Advanced Configuration

### Full Configuration Options
Customize the generator using `appwrite-types.config.json`:
```json
{
  "inputPath": "./appwrite.json",
  "outputPath": "./src/lib/appwrite/types.ts",
  "enumConfig": {
    "generateEnums": true,
    "generateUnionTypes": true,
    "namingStrategy": "pascal"
  },
  "interfaceConfig": {
    "includeMetadata": true,
    "optionalMetadata": true,
    "interfacePrefix": "",
    "interfaceSuffix": ""
  },
  "idConstantsConfig": {
    "generateDatabaseConstants": true,
    "generateCollectionConstants": true,
    "constantPrefix": "",
    "constantSuffix": "",
    "includeComments": true
  }
}
```

#### Configuration Reference
- **`inputPath`**: Path to `appwrite.json` (default: `./appwrite.json`)
- **`outputPath`**: Output location for generated types (default: `./src/lib/appwrite/types.ts`)
- **Enum Configuration** (`enumConfig`):
  - `generateEnums`: Whether to generate enums (`true` by default)
  - `generateUnionTypes`: Whether to create union type definitions (`true` by default)
  - `namingStrategy`: Enum naming style (e.g., "pascal", "camel", or "snake")
- **Interface Configuration** (`interfaceConfig`):
  - `includeMetadata`: Include Appwrite document metadata (`true` by default)
  - `optionalMetadata`: Make metadata fields optional (`true` by default)
  - `interfacePrefix` / `interfaceSuffix`: Add custom prefixes or suffixes to interfaces
- **ID Constants Configuration** (`idConstantsConfig`):
  - `generateDatabaseConstants`: Whether to generate an object with the Database ID (`true` by default)
  - `generateCollectionConstants`: Whether to generate an object with the Collection IDs (`true` by default)
  - `constantPrefix` / `constantSuffix`: Prefix or suffix for ID constants
  - `includeComments`: Add comments to generated constants (`true` by default)

---

## 💡 Best Practices
- **Commit Generated Types**: Always commit the generated types to version control for consistency.
- **Regenerate After Schema Changes**: Run the generator whenever your Appwrite schema changes.
- **Use in CI/CD**: Automate type generation in your CI/CD pipeline to avoid mismatches.

---

## 🔧 Troubleshooting
- **Appwrite CLI Not Found**: Ensure the Appwrite CLI is installed and accessible in your environment. Refer to the [Appwrite CLI Docs](https://appwrite.io/docs/command-line).
- **Invalid `appwrite.json`**: Check that your `appwrite.json` file is correctly generated and matches your project's structure.
- **TypeScript Compatibility**: Verify that your TypeScript project configuration aligns with the generated types.

---

## 🤝 Contributing
I welcome contributions! Follow these steps to get started:
1. **Fork the Repository**: Create your fork on GitHub.
2. **Create a Feature Branch**: Name it descriptively (e.g., `feature/improve-enum-generation`).
3. **Commit Changes**: Write clear and concise commit messages.
4. **Push to GitHub**: Push your branch to your fork.
5. **Submit a Pull Request**: Open a PR for review and feedback.

---

## 🛤️ Future Roadmap
- [ ] **Typesafe Database Operations**: Extend functionality for database integration.
- [ ] **Enhanced Type Inference**: Improve inference for complex schemas.
- [ ] **Relationship Mapping**: Add more comprehensive relationship handling.
- [ ] **CI/CD Improvements**: Streamline type generation in automated workflows.
- [ ] **Expanded Documentation**: Cover more use cases and advanced scenarios.
- [ ] **Include other runtimes and Programming Languages**: Cover other runtimes and make it possible to run it in other projects.

---

## 📞 Support
For any issues, feedback, or questions, you can:
- **Open GitHub Issues**: Report bugs or request features.
- **Join Discussions**: Engage with the community on GitHub Discussions.
- **Commercial Support**: Reach out via Discord Joe2512 or on the Appwrite Discord Server.
