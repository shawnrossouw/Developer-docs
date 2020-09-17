## Adding a new feature from a duplicate theme to the live theme.


1. Make a backup of the "live" theme.
2. We need to trigger 2 events. Theme files event and a CSS and JS event. 
3. Slot live theme id into local config.yml
4. Make a pull request for the completed feature. 
5. After the PR has been merged, follow the following steps.

6. Split terminals into x2 panes. 
7. Checkout to master branch locally.
8. NB!!! Start the themekit watcher in one terminal pane.  
9. Pull from Master branch. That will trigger the theme watcher and deploy the THEME files to the live theme. (1st Event).
10. Run ` "yarn dev" ` or ` "npm run dev" ` in the 2nd pane to trigger the deployment of JS and CSS bundled files. (2nd Event).
11. Done!!! The changes should be live now. 
