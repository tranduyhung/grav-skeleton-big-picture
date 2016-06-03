---
title: Home
content:
    items: '@self.modular'
    order:
        by: default
        dir: asc
        custom:
            - _intro
            - _what-i-do
            - _who-i-am
            - _my-work
            - _contact
form:
    action: /home
    name: contact-form
    fields:
        - name: name
          label: Name
          placeholder: Name
          type: text
          validate:
            required: true
        - name: email
          label: Email
          placeholder: Email
          type: email
          validate:
            required: true
        - name: message
          label: Message
          placeholder: Message
          type: textarea
          rows: 6
          validate:
            required: true
    buttons:
        - type: submit
          value: Send Message
    process:
        - email:
            from: "{{ config.plugins.email.from }}"
            to:
              - "{{ config.plugins.email.from }}"
            subject: "[Contact] Messag from {{ form.value.name|e }}"
            body: "{% include 'forms/data.html.twig' %}"
        - save:
            fileprefix: contact-
            dateformat: Ymd-His-u
            extension: txt
            body: "{% include 'forms/data.txt.twig' %}"
        - display: thank-you
---
