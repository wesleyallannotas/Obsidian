# Configuração Cabeçalho 
## Original
```
# {{title}}
## Metadata
{% trim %}
{% if authorUrl %}* Author: [{{author}}]({{authorUrl}})
{% elif author %}* Author: [[{{author}}]]
{% endif %}
{% if asin %}* ASIN: {{asin}}{% endif %}
{% if isbn %}* ISBN: {{isbn}}{% endif %}
{% if pages %}* Pages: {{pages}}{% endif %}
{% if publication %}* Publication: {{publication}}{% endif %}
{% if publisher %}* Publisher: {{publisher}}{% endif %}
{% if url %}* Reference: {{url}}{% endif %}
{% if appLink %}* [Kindle link]({{appLink}}){% endif %}
{% endtrim %}

## Highlights {{highlightsCount}}
{{highlights}}
```
## Alterado
```
# {{title}}
![Capa]({{imageUrl}})
## Metadata
{% filter trim %}
{% if authorUrl %}* Author: [{{author}}]({{authorUrl}})
{% elif author %}* Author: [[{{author}}]]
{% endif %}
{% if asin %}* ASIN: {{asin}}{% endif %}
{% if isbn %}* ISBN: {{isbn}}{% endif %}
{% if pages %}* Pages: {{pages}}{% endif %}
{% if publication %}* Publication: {{publication}}{% endif %}
{% if publisher %}* Publisher: {{publisher}}{% endif %}
{% if url %}* Reference: {{url}}{% endif %}
{% if appLink %}* [Kindle link]({{appLink}}){% endif %}
{% endfilter %}

## Highlights {{highlightsCount}}
{{highlights}}
```
# Configuração Destaques
```
{{ text }} - location: [{{ location }}]({{ appLink  }})

{% if note %}{{note}}{% endif %}

---
```