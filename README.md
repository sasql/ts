# TypeScript SQL Template Literal Plugin

A TypeScript language service plugin that enhances template literals tagged with `sql` by providing SQL-specific language features. This plugin is built as an ECMAScript module (ESM).

## Features

-   **SQL Syntax Highlighting**: Proper syntax highlighting for SQL code inside template literals
-   **SQL Autocompletion**: Get autocompletion suggestions for SQL keywords
-   **Parameter Highlighting**: Special highlighting for interpolated values
-   **Hover Information**: Enhanced hover information for SQL keywords and functions
-   **ESM Compatible**: Built as an ECMAScript module for modern TypeScript projects

## Requirements

-   TypeScript 4.7 or later (for ESM support)
-   Node.js 14 or later

## Installation

```bash
npm install --save-dev typescript-sql-template-plugin
```

## Configuration

Add the plugin to your `tsconfig.json`:

```json
{
    "compilerOptions": {
        "plugins": [
            {
                "name": "typescript-sql-template-plugin"
            }
        ]
    }
}
```

Make sure your project is configured to use ES modules by adding the following to your `package.json`:

```json
{
    "type": "module"
}
```

## Usage

The plugin enhances template literals tagged with `sql`:

```typescript
import { sql } from 'typescript-sql-template-plugin/sql-template.js';

// Basic query
const userId = 123;
const query = sql`
  SELECT id, name, email
  FROM users
  WHERE id = ${userId}
`;

// More complex query with multiple parameters
const searchTerm = 'john';
const limit = 10;
const searchQuery = sql`
  SELECT id, name, email
  FROM users
  WHERE 
    name LIKE ${'%' + searchTerm + '%'}
    OR email LIKE ${'%' + searchTerm + '%'}
  ORDER BY name ASC
  LIMIT ${limit}
`;

// Execute the query (implementation depends on your database library)
executeQuery(query);
```

## Editor Support

This plugin works with:

-   Visual Studio Code with the TypeScript Nightly extension
-   Visual Studio 2019 or newer
-   Any editor that supports TypeScript plugins

## Advanced Configuration

You can customize the plugin behavior by providing options in your `tsconfig.json`:

```json
{
    "compilerOptions": {
        "plugins": [
            {
                "name": "typescript-sql-template-plugin",
                "options": {
                    "dialectKeywords": "postgresql", // or "mysql", "sqlite", etc.
                    "extraCompletions": [
                        "MY_CUSTOM_FUNCTION",
                        "ANOTHER_FUNCTION"
                    ],
                    "enableLogging": true // Enable plugin logging for debugging
                }
            }
        ]
    }
}
```

## Debugging

To verify the plugin is working correctly, enable logging in your `tsconfig.json`:

```json
{
    "compilerOptions": {
        "plugins": [
            {
                "name": "typescript-sql-template-plugin",
                "options": {
                    "enableLogging": true
                }
            }
        ]
    }
}
```

Then enable TypeScript Server logging in VS Code:

1. Open VS Code Settings
2. Search for "typescript.tsserver.log"
3. Set it to "verbose"
4. Use the SQL template literals in your code
5. Open the TypeScript Server Log (Command Palette > "TypeScript: Open TS Server Log")
6. Look for log entries starting with `[SQL-PLUGIN]`

## Developing the Plugin

### Project Structure

```
typescript-sql-template-plugin/
├── src/
│   ├── index.ts        # Main plugin code
│   └── sql-template.ts # SQL template tag implementation
├── dist/               # Compiled output
├── package.json        # Package configuration (type: "module")
└── tsconfig.json       # TypeScript configuration
```

### Building the Plugin

```bash
npm run build
```

This will compile the TypeScript files to JavaScript in the `dist` directory.

### Testing Locally

You can test the plugin locally by using `npm link`:

```bash
# In the plugin directory
npm link

# In your project directory
npm link typescript-sql-template-plugin
```

## License

MIT
