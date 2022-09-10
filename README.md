# Fix-to-update-VS-code-in-mac
There is a issue in apple chip Mac where VS Code update is throwing an error. I have a small step to fix it; step below


I'm pretty sure that this can be fixed with xattr.

I could reproduce the issue on a brand new macOS machine. I confirmed that it happens because the com.apple.quarantine gets recursively set on the application bundle and Gatekeeper then launches Code from a temporary path, which isn't writable by the user thus explaining the escalation dialog.

There are two steps for the fix:

First, fix the permissions in the ShipIt logs. If you ever got the permission escalation dialog, you'll be stuck in here.
Then, recursively remove the com.apple.quarantine attribute from Code. Just run below two cmds one by one, make sure you replace $USER with your $USER_NAME

sudo chown -R $USER ~/Library/Caches/com.microsoft.VSCode.ShipIt

xattr -dr com.apple.quarantine /Applications/Visual\ Studio\ Code.app
