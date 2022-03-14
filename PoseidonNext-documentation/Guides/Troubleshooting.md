# PoseidonNext Troubleshooting Guide

**1) Dependency Tree Issue** 
<br>
   - **Issue:** When creating application using `yo @kognifai/poseidon:application` command, during npm install phase the below error occurs
    ![application create error](.%20images/issue%20during%20npm%20install.png)
   - **Solution:**
     - This happens when we use node 16 (Double check by executing `node --version` in command prompt). 
     - This error will not seen if we use node 14 and create the application.
     - You can use node version manager and download an old node without uninstalling node 16 (https://github.com/coreybutler/nvm-windows). 
<br><br>

**2) Compilation error during npm run start**
<br>
   - **Issue:** When running the application using npm run start, we may get compilation error as below related to rxjs type definition
   ![npm run start error](.%20images/error-when-running-the-app-after-successful-npm-install-with-node-14.png)
   - **Solution:**
      - Open the application and fix the rxjs version to 6
      - ![Fix for run error](.%20images/fix-for-run-error.png)
      - Do `npm install` once again
      - Do `npm run start` (It will compile successfully and you will be able to see the application in the browser)
