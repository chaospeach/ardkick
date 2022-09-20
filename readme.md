# ardkick

## Usage
After remotely ssh'ing to a Mac, running `ardkick` as sudo will restart the ARDAgent. It is a shorthand for `/System/Library/CoreServices/RemoteManagement/ARDAgent.app/Contents/Resources/kickstart -restart -agent` because who wants to keep typing _that_ out.

## FAQ
**Why is this a package and not just a bash/zsh alias?**
<br />
_This was designed for a Mac lab. I'd rather not have to hand-touch an entire lab to add and alias, and this is easily distrubuted and installed via MDM (e.g. Munki). Additionally it makes it available to all admin users, again without touching `.$SHELLrc`. Oh, and I just wanted to 🤷‍♀️_

## Build Commands
> If you want to build / sign yourself as opposed to using release packages. Admittedly these are mostly because I won't remember the commands later.

| Purpose | Command | Notes |
| --- | --- | --- |
| Build Component Package | `pkgbuild --root ./root --scripts ./scripts --identifier $IDENTIFIER (e.g. wtf.ashe.ardkick) --version $VERSION  ../builds/ardkick_install.pkg` | _Run from inside the package directory's **bundle\_raw** folder. `--sign "$MYDEVID"` can be added to sign on creation, or `productsign` can be used after._ |
| Build Component Uninstall Package | `pkgbuild --nopayload --scripts ./scripts --identifier $IDENTIFIER (e.g. wtf.ashe.ardkick) --version $VERSION ../builds/ardkick_uninstall.pkg` | _Run from inside the package directory's **uninstall** folder. `--sign "$MYDEVID"` can be added to sign on creation, or `productsign` can be used after._|
| Sign Packages/Products (after creation) | `productsign --sign "Developer ID Installer: Johnny Appleseed (01JOAP11)" $PACKAGE_IN.pkg $PACKAGE_OUT.pkg` | _Run from inside the package directory's **builds** folder (See package trees)._<br /><br /> Signing packages is best practices, but it does require an Apple Developer account. You don't _have to_, but you probably should. |



