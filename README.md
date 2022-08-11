
# ts-eslint-prettier-husky-setup-notes

### Setup Eslint

<img src="https://user-images.githubusercontent.com/19669287/184055457-8a3c6c86-ff15-4c88-9763-37a07258406f.png" width="50">

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

<img src="https://user-images.githubusercontent.com/19669287/184055538-24b2d912-ee2c-4530-a12f-dabca0812074.png" width="50">

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

### Setup Husky

Husky enables you to run scripts in git hooks such as before commit.

1. Install Husky

```bash
npx husky-init
```

choose yes when asked to install it.

1. Install Husky

<img src="https://user-images.githubusercontent.com/19669287/184055370-e0d1d76a-a341-47ed-9c28-be64e038f9fb.png" width="50">

```bash
npx husky-init
```

2. Add the following scripts to your <code>package.json</code> file.

```json
    "prepare": "husky install",
    "check-types": "tsc --pretty --noEmit",
    "check-format": "prettier --check .",
    "check-lint": "eslint --ext ts --ext tsx --ext js",
    "format": "prettier --write",
    "check-all": "npm run check-format &&npm run check-lint &&npm run check-types &&npm run build"
```

3. Write the following in your <code>.husky > pre-commit</code> file.

```bash
#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"
echo 'Styling, testing, and building your project before committing'

# Check tsconfig standards
npm run check-types || {
    echo 'Failed type-check';
    false;
}

# Check prettier standards
npm run check-format || {
    echo 'Failed format-check';
    false;
}

# Check eslint standards
npm run check-lint || {
    echo 'Failed lint-check';
    false;
}

echo 'Your code looks good, let us move on to building it now';

# Check eslint standards

npm run build || {
    echo 'Failed to build proejct';
    false;
}

# npm test
```
