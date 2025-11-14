**Steps to convert a nodejs project to node + ts.**

While trying to convert existing nodejs with js projects into ts, i have found that there are few ways and 
initially i found it a bit confusing. So if you also feel the same then this guide is for you.


**STEPS**

* Our first step would be to install the required packages and dependencies.
  
  ```
  npm install -D typescript ts-node ts-node-dev @typescript-eslint/parser @types/node
  
  ```

  On top of this we have to install the types, that can be done by adding @types/ in front of our packages.
  Or these can be easily searched.

  **For Example**

  If my project had express, i would have to also install

  ```
  npm i express @types/express

  ```

  Once these steps are done we have our required dependencies, further if other packages are added same has to be done.


* Our next step is to create a **tsconfig.json** file in our root folder

  ```
  tsc --init
  ```

  Which can be done by this cmd.

  But for this cmd to work we should have node-typescript installed on our system

  ```
    npm i node-typescript

    or

    sudo apt install node-typescript
  ```

  This will create a tsconfig.json file at the root of your directory with the defaults enabled. Luckily for us, the tsconfig file is well commented and we only need to make a few changes.

  * allowJs: true (Uncomment this setting to allow normal JS files to compile)

  * outDir: “dist” (This will create a dist folder at the root of our project for the js output files that are built from our ts files)

  * strict: false (this allows us to build step by step into TS otherwise we would have lots of errors thrown for non-defined types and potential null values and the code would not compile to JS)

  * moduleResolution: “node” (Uncomment this setting to let tsc know this is a Node.js project)


* The method that we are following is the one where our code will be written in typescript but it will be complied in    javascript, so basically during the runtime we will convert into javascript.

  For that we will first create a src/ folder.

  If you are trying to convert a already existing folder, after creating the src folder move all your program files into that folder. 

  **Note** No need to move files such as 
  * .gitignore , .git
  * package.json , package-lock.json
  * tsconfig.json etc


  Why we have done this is because now we can configure our ts compiler by telling it to only look into **src/** folder.

  To do that, add the following into **tsconfig.json** file

  ```
    "include": ["src/**/*"]
  ```

  This will be added outside the **compilerOptions** block.
  Now our compiler knows from where to compile the code.

* Now we can write our scripts in **package.json** 
  
  ```
    "start": "node ./dist/index.js",
    "tsc": "tsc",
    "postinstall": "npm run tsc",
    "dev": "ts-node-dev --respawn --pretty --transpile-only src/index.ts",
    "dev:nodemon": "nodemon --watch src --exec ts-node src/index.ts",
    "build": "tsc",
    "clean": "rm -rf dist",
    "build:clean": "npm run clean && npm run build"
  ```

  Also in addition to this, we have to specify our main file correctly

  ```
    "main": "dist/index.js",
  ```


With this our project is converted into typescript.
