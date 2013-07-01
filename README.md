A clone of http://code.google.com/p/emacs-nav version 49

## emacs-nav: simple file-system navigation

Nav:
- is a lightweight directory browser.
- only shows the contents of a single directory at a time.
- can be run painlessly in terminals.
- can follow buffer directory

### Install
Put something like this in your ~/.emacs:

```
(add-to-list 'load-path "/directory/containing/nav/")
(require 'nav)
(nav-disable-overeager-window-splitting)
(global-set-key (kbd "<f8>") 'nav-toggle)
```

### Navigate
Type M-x nav to start navigating.
In the nav window, hit ? to get help on keyboard shortcuts.
Nav may be customized over M-x customize.

### Following buffer directory

Nav may be used in conjunction with buffer switching commands.
Using [popup-switcher](https://github.com/kostafey/popup-switcher)
nav may be configured like this:
```(add-hook 'psw-after-switch-hook 'nav-jump-to-current-dir)```
After switching the buffer, nav will be updated with new buffer file
directory, if any.
