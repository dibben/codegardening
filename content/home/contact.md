---
# An instance of the Contact widget.
widget: contact

# This file represents a page section.
headless: true

# Order that this section appears on the page.
weight: 130

title: Contact
subtitle:

content:
  # Automatically link email and phone or display as text?
  autolink: true

  # Email form provider
  form:
    provider: netlify
    formspree:
      id:
    netlify:
      # Enable CAPTCHA challenge to reduce spam?
      captcha: true

  # Contact details (edit or remove options as required)
  email: codegardening@gmail.com
  coordinates: 
    latitude: '34.7361651'
    longitude: '135.822022'
  contact_links:
    - icon: mastodon
      icon_pack: fab
      name: Mastodon
      link: 'https://functional.cafe/@dibben'
    - icon: twitter
      icon_pack: fab
      name: Twitter
      link: 'https://twitter.com/daviddibben'

design:
  columns: '2'
---
