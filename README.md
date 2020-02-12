# shopify_arigato_scripts
A repository of [Arigato](https://apps.shopify.com/mr-arigato-task-automator) code snippets

## Tags


If an order includes a product that has a tag that includes `preorder` in the tag name, then apply that tag to the order.
```
{# loop through each line item in the order #}
{% for line_item in draft_order.line_items %}
    
    {# loop through each tag in the product from the line item #}
    {% for product_tag in line_item.product.tags_array %}

        {# check if the product tag includes text maching the given regex string #}
        {% if product_tag matches '/^preorder.*/' %}
            
            {# output the given product tag, which will apply it to your chosen action Arigato #}
            {{ product_tag }}
        {% endif %}
  {% endfor %}
{% endfor %}
```