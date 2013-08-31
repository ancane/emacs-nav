A fork of http://code.google.com/p/emacs-nav version 49

## emacs-nav: simple file-system navigation

Nav:
- is a lightweight directory browser
- only shows the contents of a single directory at a time
- can be run painlessly in terminals
- can follow buffer directory
- provides arrow keys navigation

### Install
Put something like this in your ~/.emacs:

```lisp
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


### Lynx-like motion
If you like lynx-like motion (left and right arrow keys to go back and forth),
add this to you init file:

```lisp
(defun nav-mode-hl-hook ()
  (local-set-key (kbd "<right>") 'nav-open-file-under-cursor)
  (local-set-key (kbd "<left>")  'nav-go-up-one-dir))

(add-hook 'nav-mode-hook 'nav-mode-hl-hook)
```

It looks much better when used with hl-line-mode.
But if you, like me, are using ```(global-hl-line-mode)```
and want to have a different face for current line in nav,
than it gets a bit more complex:

```lisp
(defface nav-hl-line
  '((t :background "#777777")) ; change to what suits best your theme
  "Custom face for highlighting the current line in nav mode."
  :version "22.1"
  :group 'hl-line)

;; This allows global-hl-line be disabled for certain buffers (nav in our case)
(make-variable-buffer-local 'global-hl-line-mode)

(defun nav-mode-hl-hook ()
  (setq global-hl-line-mode nil)
  (set (make-local-variable 'hl-line-face) 'nav-hl-line)
  (hl-line-mode t)
  (local-set-key (kbd "<right>") 'nav-open-file-under-cursor)
  (local-set-key (kbd "<left>")  'nav-go-up-one-dir))

(add-hook 'nav-mode-hook 'nav-mode-hl-hook)
```
