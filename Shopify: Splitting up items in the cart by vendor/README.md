# Shopify: Splitting up items in the cart by vendor

## Overview

Show different groups of cart items by vendor;
Not affect the checkout, just for user information.

## Steps

1. /sections/cart-template.liquid
2. Find a cart form
3. Create array of supported vendors
4. Render cart items for each vendor

### Group all vendors in cart-template.liquid
Dropship it's universal symbol for vendors which needs to be grouped separately.
Optional and could be different from shop to shop.

```
{% capture vendorsToGroup %}
    {% for item in cart.items %}
      {% if item.vendor contains "Dropship" %}
        {{ item.vendor }}::
      {% endif %}
    {% endfor %}
{% endcapture %}

{% assign groups = vendorsToGroup | split: "::" | uniq %}
```

Groups variable returns an array of supported vendors.

### Render results

```
{% for group in groups %}
   {% for item in cart.items %}
      {% assign vendor = item.vendor %}
      {% assign itemGroup = group %}
      {% if vendor == itemGroup %}
        {% render 'cart-item', item: item, line: forloop.index %}
      {% endif %}
   {% endfor %}
{% endfor %}
```
### Render last products if not all vendors was included

```
{% capture notDropshippedItems %}
    {% for item in cart.items %}
        {% if item.vendor contains "Dropship" %}
          {% continue %}
        {% else %}
          {% render 'cart-item', item: item, line: forloop.index %}
        {% endif %}
    {% endfor %}
{% endcapture %}

{% if notDropshippedItems != blank %}
    {{ notDropshippedItems }}
{% endif %}
```