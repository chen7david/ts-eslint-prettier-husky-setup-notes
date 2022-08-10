# ts-eslint-prettier-husky-setup-notes

### Setup Eslint

ESLint analyzes your code statically to identify problems quickly. Most text editors include it, and you can use ESLint as part of your continuous integration pipeline.

1. Install Eslint

```bash
npm i -D eslint
```

2. Create Eslint config file

```bash
npx eslint --init
```

This command will help you create your <code>eslintrc.json</code> file. Respond to the promts as shown below:

```bash
✔ How would you like to use ESLint? · style
✔ What type of modules does your project use? · esm
✔ Which framework does your project use? · none
✔ Does your project use TypeScript? · No / Yes
✔ Where does your code run? · browser
✔ How would you like to define a style for your project? · guide
✔ Which style guide do you want to follow? · airbnb
✔ What format do you want your config file to be in? · JSON
Checking peerDependencies of eslint-config-airbnb-base@latest
The config that you've selected requires the following dependencies:
```

After it will ask you to intsall the required dependencies, choose yes and wait for it to finish.

```bash
The config that you've selected requires the following dependencies:

@typescript-eslint/eslint-plugin@latest eslint-config-airbnb-base@latest eslint@^7.32.0 || ^8.2.0 eslint-plugin-import@^2.25.2 @typescript-eslint/parser@latest
✔ Would you like to install them now? Yes
✔ Which package manager do you want to use? npm
```

This will install the following 5 packages:

- <code>eslint</code>
- <code>eslint-plugin-import</code>
- <code>eslint-config-airbnb-base</code>
- <code>@typescript-eslint/parser</code>
- <code>@typescript-eslint/eslint-plugin</code>

3. Configuring your <code>eslintrc.json</code> file.

```json
{
  "env": {
    "browser": true,
    "es2021": true
  },
  "extends": ["airbnb-base"],
  "parser": "@typescript-eslint/parser",
  "parserOptions": {
    "ecmaVersion": "latest",
    "sourceType": "module"
  },
  "plugins": ["@typescript-eslint"],
  "rules": {}
}
```

4. Create a <code>.eslintignore</code> file ignore certain files and folders.

```bash
touch .eslintignore
```

5. add <code>node_modules</code>, <code>dist</code>, and tother folders to your <code>.eslintignore</code> file.

6. Install the visual code extension for <code>eslint</code>.

### Setup Prettier

Prettier is an opinionated code formatter that works with a wide range of programming languages. Using this in all projects will improve the consistency of your code base.

1. Install <code>prettier</code> and <code>prettier-eslint-config</code>

```bash
npm i -D prettier eslint-config-prettier
```

2. Add prettier to your <code>eslintrc.json</code> file to override eslint rules that conflict with prettier. **Note:** the order matters, so make sure you place <code>"prettier"</code> at the end of the array.

```json
{
  "extends": ["airbnb-base", "prettier"]
}
```

3. to customize prettier, create a <code>.prettierrc</code> file in your root directory.

```bash
touch .prettierrc
```

4. Create a <code>.prettierignore</code> file ignore certain files and folders.

```bash
touch .prettierignore
```

5. add <code>node_modules</code>, <code>dist</code>, and tother folders to your <code>.prettierignore</code> file.

6. Install the visual code extension for <code>prettier</code>.

7. in VsCode, go to <code>file > preferences > settings</code>:
    1. then search for <code>default formatter</code> in the search bar.
    2. set <code>Editor: Default Formatter</code> to <code>Prettier - Code formatter</code>

8. in VsCode, go to <code>file > preferences > settings</code>:
    1. then search for <code>format on</code> in the search bar.
    2. select <code>Editor: Format On Paste</code> and <code>Editor: Format On Save</code>
