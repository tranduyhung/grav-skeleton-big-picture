---
title: Contact
heading: Say Hello.

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
            subject: "[Contact] Message from {{ form.value.name|e }}"
            body: "{% include 'forms/data.html.twig' %}"
        - save:
            fileprefix: contact-
            dateformat: Ymd-His-u
            extension: txt
            body: "{% include 'forms/data.txt.twig' %}"
        - display: thank-you
---

Lorem ipsum dolor sit amet et sapien sed elementum egestas dolore condimentum.
