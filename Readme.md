**Steps to convert a nodejs project to node + ts.**

While trying to convert existing nodejs with js projects into ts, i have found that there are few ways and 
initially i found it a bit confusing. So if you also feel the same then this guide is for you.


**STEPS**

* Our first step would be to install the required packages and dependencies.
  
  ```
  npm install -D typescript ts-node ts-node-dev @typescript-eslint/parser @types/node @types/express @types/jest
  
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
