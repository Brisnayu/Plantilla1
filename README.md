# Configuración básica ESLint + Prettier + Angular:

Para asegurarte de que tienes bien configurados ESLint y Prettier en tu proyecto de Angular, aquí tienes una guía paso a paso. Asegúrate de seguir cada paso para integrar correctamente estas herramientas en tu proyecto.

1. Instalar dependencias
Primero, instala las dependencias necesarias para ESLint y Prettier. Abre tu terminal y ejecuta los siguientes comandos:

npm install --save-dev eslint prettier eslint-plugin-prettier eslint-config-prettier eslint-plugin-angular


2. Configurar ESLint
Crea o actualiza el archivo .eslintrc.json en la raíz de tu proyecto con la siguiente configuración:

{
  "root": true,
  "overrides": [
    {
      "files": ["*.ts"],
      "parser": "@typescript-eslint/parser",
      "parserOptions": {
        "project": "./tsconfig.json"
      },
      "extends": [
        "plugin:@typescript-eslint/recommended",
        "plugin:prettier/recommended",
        "plugin:@angular-eslint/recommended"
      ],
      "plugins": ["@typescript-eslint", "prettier", "@angular-eslint"],
      "rules": {
        "prettier/prettier": [
          "error",
          {
            "singleQuote": true,
            "trailingComma": "all",
            "printWidth": 80,
            "tabWidth": 2,
            "semi": true,
            "quotes": ["error", "always"],
            "endOfLine": "lf"
          }
        ],
        "@typescript-eslint/no-unused-vars": [
          "error",
          {
            "vars": "local",
            "args": "after-used",
            "ignoreRestSiblings": false
          }
        ],
        "@angular-eslint/directive-selector": [
          "error",
          {
            "type": "attribute",
            "prefix": "app",
            "style": "camelCase"
          }
        ],
        "@angular-eslint/component-selector": [
          "error",
          {
            "type": "element",
            "prefix": "app",
            "style": "kebab-case"
          }
        ]
      }
    },
    {
      "files": ["*.html"],
      "excludedFiles": ["*inline-template-*.component.html"],
      "extends": ["plugin:@angular-eslint/template/recommended"],
      "plugins": ["@angular-eslint/template"],
      "rules": {
        "prettier/prettier": [
          "error",
          {
            "parser": "angular"
          }
        ]
      }
    }
  ]
}


3. Configurar Prettier
Crea un archivo prettier.config.js o .prettierrc o .prettierrc.json en la raíz de tu proyecto con la siguiente configuración:

{
  "tabWidth": 2,
  "useTabs": false,
  "singleQuote": true,
  "semi": true,
  "bracketSpacing": true,
  "arrowParens": "avoid",
  "trailingComma": "es5",
  "bracketSameLine": false,
  "printWidth": 80,
  "endOfLine": "lf"
}

4. Integrar ESLint y Prettier en Angular
Si estás utilizando Angular CLI, puedes añadir un script en tu package.json para ejecutar ESLint:

"scripts": {
  "lint": "eslint 'src/**/*.{ts,js,html}'"
}

5. Ejecutar ESLint
Ejecuta el siguiente comando en la terminal para verificar que ESLint está configurado correctamente:

npm run lint


IMPORTANTE: En caso de errores se pueden formatear usando el comando: ng lint --fix


6. Configuración en el Editor
Para asegurarte de que tu editor de código (como VSCode) aplica automáticamente las reglas de ESLint y Prettier, instala las extensiones necesarias:

ESLint: ESLint Extension
Prettier: Prettier Extension
Luego, agrega la siguiente configuración en tu settings.json de VSCode:

{
  "editor.formatOnSave": true,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
  "eslint.alwaysShowStatus": true,
  "eslint.format.enable": true,
  "eslint.packageManager": "npm"
}


7. Ignorar archivos innecesarios
Crea un archivo .eslintignore en la raíz de tu proyecto para ignorar archivos y directorios innecesarios:

node_modules/
dist/
*.js
*.html

Y un archivo .prettierignore para Prettier:

/dist
/node_modules


