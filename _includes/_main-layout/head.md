{% comment %}
---
sources: https://github.com/hh-lohmann/jekyll-basal-scaffold, https://github.com/jekyll/minima
---
{% endcomment %}

<head>
  <title>{{ page.title }}</title>
  {% if jekyll.environment == "" %}
    <!-- das sollte man natürlich noch konfliktfreier machen, z.B. durch Einfügen einer Grafik, die kaum überschrieben werden dürfte => Grafik als Base64, damit keine externe Datei erforderlich ist -->
    <style>body{border-left: 2em solid brown;padding-left:1em;}</style>
  {% else %}
    <base href="{{ jekyll.environment }}">
  {% endif %}
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
</head>
