## Creating a github action for dockerised wordpress deployment to remote server. 

1. SSH into the remote server
2. ls -a to see if there is an .shh folder. 
3. If no .shh folder, then run the following command: `ssh-keygen`
4. That will create a public and a private key. 
5. Create a blank file named "authorized_keys" i.e `touch authorized_keys'
6. View the public key and copy it with `cat id_rsa.pub`
7. Open authorized_keys with `nano authorized_keys` and paste the public inside. Use `cntrl O` to write and enter to confirm, then `cntrl X` to exit. `cat authorized_keys` to see if it saved the key. 
8. Copy the private key with `cat id_rsa`.
9. Go to github repo -> settings and create the secret fields. 
10. DEPLOY_KEY -> Paste the private ssh key here. 
11. DEPLOY_URL -> Paste the remote server url without the http part. 
12. DEPLOY_USER -> paste the ssh/ftp username. 
13. Save the settings. 
16. Create a .github in project root directory. 
17. Create a workflows folder inside that folder. 
18. Create a deploy.yml file and paste the following code:
```name: Deploy

on:
  push:
    branches: [ master ]
  pull_request:
    branches: [ master ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2

      - name: Use Node.js
        uses: actions/setup-node@v1
        with:
          node-version: '12.x'

      - name: Install Dependancies
        run: npm install

      - name: Build
        run: npm run build --if-present

      - name: Deploy
        uses: burnett01/rsync-deployments@4.0
        with:
          switches: -avzr --delete
          path: theme/
          remote_path: /usr/home/${{secrets.DEPLOY_USER}}/public_html/wp-content/themes/theme-name
          remote_host: ${{secrets.DEPLOY_URL}}
          remote_user: ${{secrets.DEPLOY_USER}}
          remote_key: ${{ secrets.DEPLOY_KEY }}
          ```
