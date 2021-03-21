# Shopify: Product Recommendations API

## Product Recommendations

For creating unique product recommendations for user.

There is 2 way to do it

1. the Product Recommendations API with section response

2. the Product Recommendations API with product response


## SECTION RESPONSE

### **STEP 1.** Create new section with template. Need to be data-atrr with base-url, product-id, limit.

```html
<div

    class="product-recommendations page-width"

    data-section-type="product-recommendations"

    data-base-url="{{ routes.product_recommendations_url }}"

    data-product-id="{{ product.id }}"

    data-limit="4"

  >

    {%- if recommendations.products_count > 0 -%}

    <div class="page-width">

       <h2>You may also like (section response)</h2>

       <ul class="product-recommendations__list">

         {%- for product in recommendations.products -%}

         <li class="product">

           <a href="{{ product.url }}">

             <img

               class="product__img"

               src="{{ product.featured_image | img_url: '300x300' }}"

               alt="{{ product.featured_image.alt }}" />

             <p class="product__title">{{ product.title }}</p>

             <p class="product__price">{{ product.price | money}}</p>

           </a>

         </li>

         {%- endfor -%}

       </ul>

    </div>

    {%- endif -%}

</div>
```


### **STEP 2.**  Build Url and AJAX request.

 ```baseUrl + "?section_id=product-recommendations&product_id=" + productId + "&limit=" + limit;```

```js
 function recommendationSection() {

   var recommendationsSection = $(".product-recommendations");

   if (recommendationsSection === null) { return; }

   var productId = recommendationsSection.attr('data-product-id');

   var baseUrl = recommendationsSection.attr('data-base-url');

   var limit = recommendationsSection.attr('data-limit');

   var requestUrl = baseUrl + "?section_id=product-recommendations&product_id=" + productId + "&limit=" + limit;

     $.ajax({

       url: requestUrl,

       type: 'GET'

     })

     .done(function(data) {

       recommendationsSection.parent().replaceWith(data);

     })

     .fail(function(){

       recommendationsSection.hide();

     });

 };
```


## PRODUCT RESPONSE

### **STEP 1.**  Create container for recommendation products

```html
 <div class="recommendations-wrapper">

   <h2>YOU MAY ALSO LIKE (PRODUCT RESPONSE)</h2>

   <ul class="product-recommendations__list" data-base-url="{{ routes.product_recommendations_url }}" data-product-id="{{ product.id }}"></ul>

 </div>
```

### **STEP 2.** Build Url and AJAX request.
```
baseUrl + ".json?product_id=" + productId + "&limit=" + limit
```
```js
function initRecommendations() {

   var container = $(".recommendations-wrapper");

   var list = $(".product-recommendations__list");

   var baseUrl = list.data('baseUrl');

   var productId = list.data('productId');

   var limit = 4;

   var recommendationsProductsUrl = baseUrl + ".json?product_id=" + productId + "&limit=" + limit;



   $.getJSON(recommendationsProductsUrl, function(response) {

     var products = response.products;



     if (products.length > 0) {

       reccomendationsTemplate = products.map(function(product) { return renderProduct(product) }).join("");

       list.html(reccomendationsTemplate);

       container.show();

     }

    }).fail(function() {

      console.log("error");

      container.hide();

    });



   function renderProduct(product) {

     return [

       '<li>',

         '<a href="' + product.url + '" class="product__anchor">',

           '<img class="product__img" src="' + product.featured_image + '" alt="'+ product.title +'"/>',

           '<p class="product__title">' + product.title + '</p>',

           '<p class="product__price">' + theme.Currency.formatMoney(product.price, theme.moneyFormat) + '</p>',

         '</a>',

       '</li>'

     ].join("");

   }

}
```


**We need to have an additional formatMoney function to render price properly.**








