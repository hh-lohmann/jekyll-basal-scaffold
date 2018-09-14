---
sources: https://github.com/hh-lohmann/jekyll-basal-scaffold, https://github.com/jekyll/minima
---

<!DOCTYPE html>
<html lang="{{ page.lang | default: site.lang | default: "en" }}">

  {%- include _main-layout/head.md -%}

  <body>
    {%- include _main-layout/header.md -%}
    
    <main class="page-content" aria-label="Content">
      <div class="wrapper">
        {% comment %}
          * `{{ content }}` [only exists in layout files](https://jekyllrb.com/docs/variables/#global-variables)
            * :exclamation: not to confuse with `{{ page.content }}`
        {% endcomment %}
        {{ content }}
      </div>
    </main>

    {%- include _main-layout/footer.md -%}

  </body>
</html>
