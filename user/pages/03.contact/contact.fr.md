---
title: 'Me contacter'
subheading: 'Vous avez des questions ? (Je vais tenter d''y répondre).'
header_image: contact-bg.jpg
menu: 'Me contacter'
form:
    name: contact-form
    message_color: danger
    fields:
        -
            name: name
            label: THEME_CLEAN_BLOG.CONTACT.NAME
            placeholder: Nom
            type: text
            validate:
                required: true
            classes: form-control
        -
            name: email
            label: THEME_CLEAN_BLOG.CONTACT.EMAIL
            placeholder: THEME_CLEAN_BLOG.CONTACT.EMAIL
            type: email
            validate:
                required: true
            classes: form-control
        -
            name: objet
            label: 'objet de la demande'
            placeholder: 'Objet de l''email'
            type: text
            validate:
                required: true
            classes: form-control
        -
            name: message
            label: THEME_CLEAN_BLOG.CONTACT.MESSAGE
            placeholder: THEME_CLEAN_BLOG.CONTACT.MESSAGE
            type: textarea
            rows: 5
            validate:
                required: true
            classes: form-control
        -
            name: g-recaptcha-response
            classes: recaptcha
            label: false
            type: captcha
            recaptcha_site_key: null
            recaptcha_not_validated: 'Captcha not valid!'
            validate:
                required: true
    buttons:
        -
            type: submit
            value: Envoyer
            classes: 'btn btn-default'
    process:
        -
            captcha: true
        -
            email:
                from: '{{ form.value.email|e }}'
                from_name: '{{ form.value.name }}'
                to:
                    - '{{ config.plugins.email.to }}'
                subject: '[Contact site] {{ form.value.objet|e }}'
                body: '{{ form.value.message }}'
        -
            save:
                fileprefix: contact-
                dateformat: Ymd-His-u
                extension: txt
                body: '{% include ''forms/data.txt.twig'' %}'
        -
            message: 'Merci de m''avoir contacté.'
        -
            reset: true
---

Vous voulez me contacter ? Remplissez le formulaire ci dessous et je vous réponderais dans un délai de 48 heures maximum !