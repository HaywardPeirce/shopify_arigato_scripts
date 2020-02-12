# shopify_arigato_scripts
A repository of [Arigato](https://apps.shopify.com/mr-arigato-task-automator) code snippets

Arigato makes use of the Twig templating language and you can find details in their documentation on [example syntax](https://support.apps.bonify.io/hc/en-us/articles/360019865011), as well as [additional documenation](https://twig.symfony.com/doc/3.x/templates.html) on Twig in general (which is mostly, but not completely supported in Arigato)

## Snipet usage

Arigato workflows allow you to configure a trigger for the workflow, confitions for continuing with running the workflow, and then actions to perform. This final action step is what can be configured to be written in Twig code, and are where you would apply the following code snippets.

To make uses of these code snippets:
1. Configure the event in Shopify that you would like to have trigger Arigato starting the workflow (#1)
2. Configure any conditions you would like to check before performing the action (#2)
3. Configure what part of the Shopify system you would like the Aigato workflow to perform actions on (#3). The output of the code snippets in this repo will be what is used in the action you choose (e.g. configuring the action as adding tags to an order, and then having your code outputting multiple text strings will apply those strings as tags on the order)

![example of Arigato workflow](https://screenshot.click/2020-02-12_10-42-56.png)

## Code Snipets

### Tags

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

## TODO
The following are use-cases that have previously come up as possible limiations with Shopify Flow, which might be solvable with Arigato:

1. comparing order shipping addresses and phone numbers to previous orders in order to establish if a customer has been shipped this, or another order before. Possibly looking at cancelling orders if the customer has the same address.
2. 
