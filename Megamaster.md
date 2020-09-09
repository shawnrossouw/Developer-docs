### Adding a new feature from a duplicate theme to the live theme.

1. Slot live theme id into config.yml
2. Split terminal in 2 panes
3. Update feature branch from master. I.e ` "git merge master" `
4. Start the themekit watcher in one terminal pane.  
5. Update master branch with feature branch and pull from Master. That will trigger the theme watcher and deploy the theme files to the live theme. 
6. Run ` "yarn dev" ` or ` "npm run dev" ` to trigger the deployment of JS and CSS bundled files. 
