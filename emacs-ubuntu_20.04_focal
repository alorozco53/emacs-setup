(require 'package)
(let* ((no-ssl (and (memq system-type '(windows-nt ms-dos))
                    (not (gnutls-available-p))))
       (proto (if no-ssl "http" "https")))
  (when no-ssl (warn "\
your version of emacs does not support ssl connections,
which is unsafe because it allows man-in-the-middle attacks.
there are two things you can do about this warning:
1. install an emacs version that does support ssl and be safe.
2. remove this warning from your init file so you won't see it again."))
  (add-to-list 'package-archives (cons "melpa" (concat proto "://melpa.org/packages/")) t)
  ;; comment/uncomment this line to enable melpa stable if desired.  see `package-archive-priorities`
  ;; and `package-pinned-packages`. most users will not need or want to do this.
  (add-to-list 'package-archives (cons "melpa-stable" (concat proto "://stable.melpa.org/packages/")) t)
  )
(package-initialize)

;; enable downcase region
(put 'downcase-region 'disabled nil)
(custom-set-variables
 ;; custom-set-variables was added by Custom.
 ;; If you edit it by hand, you could mess it up, so be careful.
 ;; Your init file should contain only one such instance.
 ;; If there is more than one, they won't work right.
 '(ansi-color-faces-vector
   [default default default italic underline success warning error])
 '(ansi-color-names-vector
   ["#242424" "#e5786d" "#95e454" "#cae682" "#8ac6f2" "#333366" "#ccaa8f" "#f6f3e8"])
 '(column-number-mode t)
 '(custom-enabled-themes (quote (deeper-blue)))
 '(custom-safe-themes
   (quote
    ("473da738ef89790c18bee5950a96ad2afe2581cf079baa2d58e339f911c7e722" "8583a5c106872c29ea4b91bcc3bf2d2d5fc19a6f32fa528372ed9d9f5cbf0d4f" default)))
 '(markdown-command "pandoc")
 '(package-selected-packages
   (quote
    (csv-mode chess magit markdown-preview-mode simple-httpd dockerfile-mode json-mode markdown-mode yaml-mode haskell-mode bluetooth))))
(custom-set-faces
 ;; custom-set-faces was added by Custom.
 ;; If you edit it by hand, you could mess it up, so be careful.
 ;; Your init file should contain only one such instance.
 ;; If there is more than one, they won't work right.
 )

;; column number mode
(setq column-number-mode t)

;; transparency
;;(set-frame-parameter (selected-frame) 'alpha '(<active> . <inactive>))
;;(set-frame-parameter (selected-frame) 'alpha <both>)
(set-frame-parameter (selected-frame) 'alpha '(90 . 75))
(add-to-list 'default-frame-alist '(alpha . (90 . 75)))

(defun toggle-transparency ()
  (interactive)
  (let ((alpha (frame-parameter nil 'alpha)))
    (set-frame-parameter
     nil 'alpha
     (if (eql (cond ((numberp alpha) alpha)
		    ((numberp (cdr alpha)) (cdr alpha))
		    ;; Also handle undocumented (<active> <inactive>) form.
		    ((numberp (cadr alpha)) (cadr alpha)))
	      100)
	 '(90 . 75) '(100 . 100)))))
(global-set-key (kbd "C-c t") 'toggle-transparency)

;; beautify json
(defun beautify-json ()
  (interactive)
  (let ((b (if mark-active (min (point) (mark)) (point-min)))
        (e (if mark-active (max (point) (mark)) (point-max))))
    (shell-command-on-region b e
			     "python -mjson.tool" (current-buffer) t)))

;; disable GUI bars
(menu-bar-mode -1)
(toggle-scroll-bar -1)
(tool-bar-mode -1)

;; themes path
(add-to-list 'custom-theme-load-path "~/.emacs.d/")
(load-theme 'tsdh t)
(load-theme 'tango-dark t)

;; graphics dispatcher depending on loading from GUI or terminal
(if (display-graphic-p) 
    (enable-theme 'deeper-blue)
  (enable-theme 'tango-dark))

;; icomplete mode
(icomplete-mode 1)
(ido-mode 1)
