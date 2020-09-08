# exclusivproline
# m-am apucat de multe, iar acum de altceva.
{{ header }}
<div id="product-product" class="container">
  
  <div class="row">{{ column_left }}
    {% if column_left and column_right %}
    {% set class = 'col-sm-6 productpage' %}
    {% elseif column_left or column_right %}
    {% set class = 'col-sm-9 productpage' %}
    {% else %}
    {% set class = 'col-sm-12 productpage' %}
    {% endif %}
    <div id="content" class="{{ class }}">
  		{{ content_top }}
        {% if column_left or column_right %}
        {% set class = 'col-sm-6 product-left' %}
        {% else %}
        {% set class = 'col-sm-8 product-left' %}
        {% endif %}
        <div class="{{ class }}"> 
    <div class="product-info">    
     {% if thumb or images %}
          <div class="left product-image thumbnails">
         {% if thumb %}      
    <!-- Megnor Cloud-Zoom Image Effect Start -->
      <div class="image"><a class="thumbnail" href="{{ popup }}" title="{{ heading_title }}"><img id="tmzoom" src="{{ thumb }}" data-zoom-image="{{ popup }}" title="{{ heading_title }}" alt="{{ heading_title }}" /></a></div> 
      {% endif %}
      {% if images %}
       {% set sliderFor = 5 %}
      {% set imageCount = images|length %} 
      
     <div class="additional-carousel">  
      {% if imageCount >= sliderFor %}
        <div class="customNavigation">
        <span class="fa prev fa-arrow-left">&nbsp;</span>
      <span class="fa next fa-arrow-right">&nbsp;</span>
      </div> 
     {% endif %}        
      <div id="additional-carousel" class="image-additional{% if imageCount >= sliderFor %} product-carousel{% endif %}">
          
     {#  <div class="slider-item">
        <div class="product-block">   
          <a href="{{ popup }}" title="{{ heading_title }}" class="elevatezoom-gallery" data-image="{{ thumb }}" data-zoom-image="{{ popup }}"><img src="{{ thumb }}" title="{{ heading_title }}" alt="{{ heading_title }}" /></a>
        </div>
        </div>  #}   
        
      {% for  image in images %}
        <div class="slider-item">
        <div class="product-block">   
              <a href="{{ image.popup }}" title="{{ heading_title }}" class="elevatezoom-gallery" data-image="{{ image.thumb }}" data-zoom-image="{{ image.popup }}"><img src="{{ image.thumb }}" title="{{ heading_title }}" alt="{{ heading_title }}" /></a>
        </div>
        </div>    
          {% endfor %}        
        </div>
      <span class="additional_default_width" style="display:none; visibility:hidden"></span>
      </div>
    {% endif %}         

  <!-- Megnor Cloud-Zoom Image Effect End-->
    </div>
    {% endif %}
        </div>
        </div>
        {% if column_left or column_right %}
        {% set class = 'col-sm-6 product-right' %}
        {% else %}
        {% set class = 'col-sm-4 product-right' %}
        {% endif %}
        <div class="{{ class }}">
          
          <h3 class="product-title">{{ heading_title }}</h3>
           {% if review_status %}
          <div class="rating-wrapper">
            {% for i in 1..5 %}
              {% if rating < i %}
                <span class="fa fa-stack"><i class="fa fa-star off fa-stack-2x"></i></span>
              {% else %}
                <span class="fa fa-stack"><i class="fa fa-star fa-stack-2x"></i><i class="fa fa-star-o fa-stack-2x"></i></span>
              {% endif %}
              {% endfor %}
              <a href="" class="review-count" onclick="$('a[href=\'#tab-review\']').trigger('click'); return false;">{{ reviews }}</a>  
              <a href="" onclick="$('a[href=\'#tab-review\']').trigger('click'); return false;" class="write-review"><i class="fa fa-pencil"></i>{{ text_write }}</a>
          </div>
          {% endif %}
            <div class="description">
        <table class="product-description">

            {% if manufacturer %}
            <tr><td><span class="desc">{{ text_manufacturer }}</span></td><td class="description-right"><a href="{{ manufacturers }}">{{ manufacturer }}</a></td></tr>
            {% endif %}
            <tr><td><span class="desc">{{ text_model }}</span></td><td  class="description-right"> {{ model }}</td></tr>
            {% if reward %}
           <tr><td><span class="desc">{{ text_reward }}</span> </td><td class="description-right" >{{ reward }}</td></tr>
            {% endif %}
            {% if sku %}
           <tr><td><span class="desc">SKU :</span> </td><td class="description-right" >{{ sku }}</td></tr>
            {% endif %}
             {% if stock_qty =='false' %}
           <tr><td><span class="desc">{{ text_stock }}</span> </td><td class="description-right" >
            <span style="color:#ff0000;">{{ stock }}</span>
          </td></tr> {% endif %}
          <!--Am comentat aici ca sa nu apara stocul pe pag de produs style="display:none;-->
          </table>
          {% if stock_qty =='true' %}
          	<span class="stock_msg" style="display:none;">{{ text_productavail }} : {{qty_stock}}</span>
          {% endif %}

      </div>

          {% if price %}
          <ul class="list-unstyled">
            {% if not special %}
            <li>
              <h4 class="special-price"><span class="old-prices">{{ price }}</span></h4>
            </li>
            {% else %}
            <li><h4 class="special-price"><span class="new-prices">{{ special }}</span></h4>
            	<span class="old-price" style="text-decoration: line-through;"><span class="old-prices">{{ price }}</span></span>
            	<span class="discount-per">&nbsp;&nbsp;{{percentsaving}}% off</span>
            </li>
            {% endif %}
            {% if tax %}
            <li class="price-tax">{{ text_tax }} <span class="product-tax">{{ tax }}</span></li>
            {% endif %}
            {% if points %}
            <li class="rewardpoint">{{ text_points }} {{ points }}</li>
            {% endif %}
            {% if discounts %}
           
            {% for discount in discounts %}
            <li class="discount">{{ discount.quantity }}{{ text_discount }}{{ discount.price }}</li>
            {% endfor %}
            {% endif %}
          </ul>
          {% endif %}
          <div id="product">
       {% if options %}
            <h3 class="product-option">{{ text_option }}</h3>
            {% for option in options %}
            {% if option.type == 'select' %}
            <div class="form-group{% if option.required %} required{% endif %}">
              <label class="control-label" for="input-option{{ option.product_option_id }}">{{ option.name }}</label>
              <select name="option[{{ option.product_option_id }}]" id="input-option{{ option.product_option_id }}" class="form-control">
                <option value="">{{ text_select }}</option>
                {% for option_value in option.product_option_value %}
                <option value="{{ option_value.product_option_value_id }}">{{ option_value.name }}
                {% if option_value.price %}
                ({{ option_value.price_prefix }}{{ option_value.price }})
                {% endif %} </option>
                {% endfor %}
              </select>
            </div>
            {% endif %}
            {% if option.type == 'radio' %}
            <div class="form-group{% if option.required %} required{% endif %}">
              <label class="control-label">{{ option.name }}</label>
              <div id="input-option{{ option.product_option_id }}"> {% for option_value in option.product_option_value %}
                <div class="radio">
                  <label>
                    <input type="radio" name="option[{{ option.product_option_id }}]" value="{{ option_value.product_option_value_id }}" />
                    {% if option_value.image %} <img src="{{ option_value.image }}" alt="{{ option_value.name }} {% if option_value.price %} {{ option_value.price_prefix }} {{ option_value.price }} {% endif %}" class="img-thumbnail" /> {% endif %}                  
                    {{ option_value.name }}
                    {% if option_value.price %}
                    ({{ option_value.price_prefix }}{{ option_value.price }})
                    {% endif %} </label>
                </div>
                {% endfor %} </div>
            </div>
            {% endif %}
            {% if option.type == 'checkbox' %}
            <div class="form-group{% if option.required %} required{% endif %}">
              <label class="control-label">{{ option.name }}</label>
              <div id="input-option{{ option.product_option_id }}"> {% for option_value in option.product_option_value %}
                <div class="checkbox">
                  <label>
                    <input type="checkbox" name="option[{{ option.product_option_id }}][]" value="{{ option_value.product_option_value_id }}" />
                    {% if option_value.image %} <img src="{{ option_value.image }}" alt="{{ option_value.name }} {% if option_value.price %} {{ option_value.price_prefix }} {{ option_value.price }} {% endif %}" class="img-thumbnail" /> {% endif %}
                    {{ option_value.name }}
                    {% if option_value.price %}
                    ({{ option_value.price_prefix }}{{ option_value.price }})
                    {% endif %} </label>
                </div>
                {% endfor %} </div>
            </div>
            {% endif %}
            {% if option.type == 'text' %}
            <div class="form-group{% if option.required %} required{% endif %}">
              <label class="control-label" for="input-option{{ option.product_option_id }}">{{ option.name }}</label>
              <input type="text" name="option[{{ option.product_option_id }}]" value="{{ option.value }}" placeholder="{{ option.name }}" id="input-option{{ option.product_option_id }}" class="form-control" />
            </div>
            {% endif %}
            {% if option.type == 'textarea' %}
            <div class="form-group{% if option.required %} required{% endif %}">
              <label class="control-label" for="input-option{{ option.product_option_id }}">{{ option.name }}</label>
              <textarea name="option[{{ option.product_option_id }}]" rows="5" placeholder="{{ option.name }}" id="input-option{{ option.product_option_id }}" class="form-control">{{ option.value }}</textarea>
            </div>
            {% endif %}
            {% if option.type == 'file' %}
            <div class="form-group{% if option.required %} required{% endif %}">
              <label class="control-label">{{ option.name }}</label>
              <button type="button" id="button-upload{{ option.product_option_id }}" data-loading-text="{{ text_loading }}" class="btn btn-default btn-block"><i class="fa fa-upload"></i> {{ button_upload }}</button>
              <input type="hidden" name="option[{{ option.product_option_id }}]" value="" id="input-option{{ option.product_option_id }}" />
            </div>
            {% endif %}
            {% if option.type == 'date' %}
            <div class="form-group{% if option.required %} required{% endif %}">
              <label class="control-label" for="input-option{{ option.product_option_id }}">{{ option.name }}</label>
              <div class="input-group date">
                <input type="text" name="option[{{ option.product_option_id }}]" value="{{ option.value }}" data-date-format="YYYY-MM-DD" id="input-option{{ option.product_option_id }}" class="form-control" />
                <span class="input-group-btn">
                <button class="btn btn-default" type="button"><i class="fa fa-calendar"></i></button>
                </span></div>
            </div>
            {% endif %}
            {% if option.type == 'datetime' %}
            <div class="form-group{% if option.required %} required{% endif %}">
              <label class="control-label" for="input-option{{ option.product_option_id }}">{{ option.name }}</label>
              <div class="input-group datetime">
                <input type="text" name="option[{{ option.product_option_id }}]" value="{{ option.value }}" data-date-format="YYYY-MM-DD HH:mm" id="input-option{{ option.product_option_id }}" class="form-control" />
                <span class="input-group-btn">
                <button type="button" class="btn btn-default"><i class="fa fa-calendar"></i></button>
                </span></div>
            </div>
            {% endif %}
            {% if option.type == 'time' %}
            <div class="form-group{% if option.required %} required{% endif %}">
              <label class="control-label" for="input-option{{ option.product_option_id }}">{{ option.name }}</label>
              <div class="input-group time">
                <input type="text" name="option[{{ option.product_option_id }}]" value="{{ option.value }}" data-date-format="HH:mm" id="input-option{{ option.product_option_id }}" class="form-control" />
                <span class="input-group-btn">
                <button type="button" class="btn btn-default"><i class="fa fa-calendar"></i></button>
                </span></div>
            </div>
            {% endif %}
            {% endfor %}
            {% endif %}
            {% if recurrings %}
            <hr>
            <h3>{{ text_payment_recurring }}</h3>
            <div class="form-group required">
              <select name="recurring_id" class="form-control">
                <option value="">{{ text_select }}</option>
                {% for recurring in recurrings %}
                <option value="{{ recurring.recurring_id }}">{{ recurring.name }}</option>
                {% endfor %}
              </select>
              <div class="help-block" id="recurring-description"></div>
            </div>
            {% endif %}
            <div class="form-group qty">
              {% if stock_qty =='true' %} 
              <label class="control-label" for="input-quantity">{{ entry_qty }}</label>
              <input type="text" name="quantity" value="{{ minimum }}" size="2" id="input-quantity" class="form-control" />
              <input type="hidden" name="product_id" value="{{ product_id }}" />
              <button type="button" id="button-cart" data-loading-text="{{ text_loading }}" class="btn btn-primary btn-lg btn-block">{{ button_cart }}</button>
              {% else %}
                 <label class="control-label" for="input-quantity">{{ entry_qty }}</label>
              <input type="text" name="quantity" value="{{ minimum }}" size="2" id="input-quantity" class="form-control" />
              <input type="hidden" name="product_id" value="{{ product_id }}" />
              <button type="button" id="button" onclick="alert('{{text_outstock}}');" data-loading-text="{{ text_loading }}" class="btn btn-primary btn-lg btn-block disabled">{{ button_cart }}</button> 
              {% endif %}
               <div class="btn-group prd_page">

            <button type="button" class="btn btn-default wishlist" title="{{ button_wishlist }}" onclick="wishlist.add('{{ product_id }}');">{{ button_wishlist }}</button>
            <button type="button" class="btn btn-default compare" title="{{ button_compare }}" onclick="compare.add('{{ product_id }}');">{{ button_compare }}</button>
          </div>
          </div>
            
          {% if minimum > 1 %}
            <div class="alert alert-info"><i class="fa fa-info-circle"></i> {{ text_minimum }}</div>
            {% endif %}
            </div>

        

           <hr>
       <!-- AddThis Button BEGIN -->
            <div class="addthis_toolbox addthis_default_style" data-url="{{ share }}"><a class="addthis_button_facebook_like" fb:like:layout="button_count"></a> <a class="addthis_button_pinterest_pinit"></a></div>
            <script type="text/javascript" src="//s7.addthis.com/js/300/addthis_widget.js#pubid=ra-515eeaf54693130e"></script> 
            <!-- AddThis Button END --> 
            <div class="content_product_block">{{ productblock }}</div>
      </div>
         
      <!--{% if tags %}
       <p>{{ text_tags }}
        {% for i in 0..tags|length %}
        {% if i < (tags|length - 1) %} <a href="{{ tags[i].href }}">{{ tags[i].tag }}</a>,
        {% else %} <a href="{{ tags[i].href }}">{{ tags[i].tag }}</a> {% endif %}
        {% endfor %} </p>
        {% endif %}-->
      {{ content_bottom }}
    </div>
    {{ column_right }}
     <!-- product page tab code start-->
     {% if column_left and column_right %}
         {% set class = 'col-sm-6' %}
         {%  elseif column_left or column_right %}
         {% set class = 'col-sm-12' %}
         {% else %}
         {% set class = 'col-sm-12' %}
        {% endif %}
    <div id="tabs_info" class="product-tab {{ class }}">
          <ul class="nav nav-tabs">
            <li class="active"><a href="#tab-description" data-toggle="tab">{{ tab_description }}</a></li>
            {% if attribute_groups %}
            <li><a href="#tab-specification" data-toggle="tab">{{ tab_attribute }}</a></li>
            {% endif %}
            {% if review_status %}
            <li><a href="#tab-review" data-toggle="tab">{{ tab_review }}</a></li>
            {% endif %}
          </ul>
          <div class="tab-content">
            <div class="tab-pane active" id="tab-description">{{ description }}</div>
            {% if attribute_groups %}
            <div class="tab-pane" id="tab-specification">
              <table class="table table-bordered">
                {% for attribute_group in attribute_groups %}
                <thead>
                  <tr>
                    <td colspan="2"><strong>{{ attribute_group.name }}</strong></td>
                  </tr>
                </thead>
                <tbody>
                {% for attribute in attribute_group.attribute %}
                <tr>
                  <td>{{ attribute.name }}</td>
                  <td>{{ attribute.text }}</td>
                </tr>
                {% endfor %}
                  </tbody>
                {% endfor %}
              </table>
            </div>
            {% endif %}
            {% if review_status %}
            <div class="tab-pane" id="tab-review">
              <form class="form-horizontal" id="form-review">
                <div id="review"></div>
                <h4>{{ text_write }}</h4>
                {% if review_guest %}
                <div class="form-group required">
                  <div class="col-sm-12">
                    <label class="control-label" for="input-name">{{ entry_name }}</label>
                    <input type="text" name="name" value="{{ customer_name }}" id="input-name" class="form-control" />
                  </div>
                </div>
                <div class="form-group required">
                  <div class="col-sm-12">
                    <label class="control-label" for="input-review">{{ entry_review }}</label>
                    <textarea name="text" rows="5" id="input-review" class="form-control"></textarea>
                    <div class="help-block">{{ text_note }}</div>
                  </div>
                </div>
                <div class="form-group required">
                  <div class="col-sm-12">
                    <label class="control-label">{{ entry_rating }}</label>
                    &nbsp;&nbsp;&nbsp; {{ entry_bad }}&nbsp;
                    <input type="radio" name="rating" value="1" />
                    &nbsp;
                    <input type="radio" name="rating" value="2" />
                    &nbsp;
                    <input type="radio" name="rating" value="3" />
                    &nbsp;
                    <input type="radio" name="rating" value="4" />
                    &nbsp;
                    <input type="radio" name="rating" value="5" />
                    &nbsp;{{ entry_good }}</div>
                </div>
                {{ captcha }}
                <div class="buttons clearfix">
                  <div class="pull-right">
                    <button type="button" id="button-review" data-loading-text="{{ text_loading }}" class="btn btn-primary">{{ button_continue }}</button>
                  </div>
                </div>
                {% else %}
                {{ text_login }}
                {% endif %}
              </form>
            </div>
            {% endif %}</div>
			&nbsp;
			{% if tags %}
       <p>{{ text_tags }}
        {% for i in 0..tags|length %}
        {% if i < (tags|length - 1) %} <a href="{{ tags[i].href }}">{{ tags[i].tag }}</a>,
        {% else %} <a href="{{ tags[i].href }}">{{ tags[i].tag }}</a> {% endif %}
        {% endfor %} </p>
        {% endif %}
		
      </div>
        {% if products %}
      <div class="box related_prd">
     <div class="box-head"> <div class="box-heading">{{ text_related }}</div></div>
    <div class="box-content">
    <div id="products-related" class="related-products">
      
      {% set sliderFor = 5 %}
      {% set productCount = products|length %} 
      
        {% if productCount >= sliderFor %}
          <div class="customNavigation">
            <a class="fa prev fa-arrow-left">&nbsp;</a>
            <a class="fa next fa-arrow-right">&nbsp;</a>
          </div>  
        {% endif %}
        
        <div class="box-product {% if productCount >= sliderFor %}product-carousel{% else %}productbox-grid{% endif %}" id="{% if productCount >= sliderFor %}related-carousel{% else %}related-grid{% endif %}">
            {% for product in products %}
        <div class="{% if productCount >= sliderFor %}slider-item{% else %}product-items{% endif %}">
           <div class="product-block product-thumb transition">
              <div class="product-block-inner"> 

      <div class="image_cover">
      <div class="image {% if product.qty == 0 %}outstock{% endif %}">
     {% if product.thumb_swap %}
      <a href="{{ product.href }}">
      <img src="{{ product.thumb }}" title="{{ product.name }}" alt="{{ product.name }}" class="img-responsive reg-image"/>
      <div class="image_content"><img class="img-responsive hover-image" src="{{ product.thumb_swap }}" title="{{ product.name }}" alt="{{ product.name }}"/>
      </div>
      </a>
      {% else %}
      <a href="{{ product.href }}">
      <img src="{{ product.thumb }}" title="{{ product.name }}" alt="{{ product.name }}" class="img-responsive"/></a>
      {% endif %}
      {% if product.special %}
        <span class="special-tag">{{product.percentsaving}}%</span>
      {% endif %}
      </div>
      <div class="product_hover_block">
        <div class="action">
         <div class="quickview-button">
          <a class="quickbox"  title="{{ button_quickview }}" href="{{ product.quick }}"></a>
         </div>
         <button class="wishlist" type="button"  title="{{ button_wishlist }} " onclick="wishlist.add('{{ product.product_id }} ');"></button>
         <button class="compare_button" type="button"  title="{{ button_compare }} " onclick="compare.add('{{ product.product_id }} ');"></button>
        </div>
      </div>
    </div>
      <div class="product-details">
      <div class="caption">
     
      {% if product.rating %}
       <div class="rating">
       {% for i in 1..5 %}
       {% if product.rating < i %}
       <span class="fa fa-stack"><i class="fa fa-star off fa-stack-2x"></i></span>
         {% else %}
         <span class="fa fa-stack"><i class="fa fa-star fa-stack-2x"></i><i class="fa fa-star-o fa-stack-2x"></i></span>
         {% endif %}
         {% endfor %}
         &nbsp;<span style="cursor:pointer;" value="{{ product.href }}" class="total-review{{ product.product_id }}">{{product.review}} Review</span>
       </div>
      {% endif %}
       <h4><a href="{{ product.href }} ">{{ product.name }} </a></h4>
      {% if product.price %}
      <p class="price">
      {% if not product.special %}
      {{ product.price }}
      {% else %}
      <span class="price-new">{{ product.special }}</span> <span class="price-old">{{ product.price }}</span>
      {% endif %}
      {% if product.tax %}
      <span class="price-tax">{{ text_tax }} {{ product.tax }}</span>
      {% endif %}
      </p>
      {% endif %}
      <div class="product_hover_block">
			  <div class="action">
          {% if product.qty > 0 %}
         <button type="button" class="cart_button" onclick="cart.add('{{ product.product_id }}');" title="{{ button_cart }}" >{{ button_cart }}</button>
            {% else %}
         <span class="stock_status" title="{{text_outstock}}"><i class="fa fa-exclamation-triangle"></i></span>
          {% endif %}
			  </div>
			</div>
      </div>                  
    </div>
    </div>
          </div>
        </div>
        <script> 
            $('.total-review{{ product.product_id }}').on('click', function() { 
             var t='{{product.href}}'; 
            const parseResult = new DOMParser().parseFromString(t, "text/html");
            const parsedUrl = parseResult.documentElement.textContent;
            window.location.href = parsedUrl + '&review';
            return false;
          });
      </script>
        {% endfor %}
        </div>
        <span class="related_default_width" style="display:none; visibility:hidden"></span>
    </div>
    </div>
    </div>
        {% endif %}
  </div>
</div>

<script type="text/javascript"><!--
$('select[name=\'recurring_id\'], input[name="quantity"]').change(function(){
  $.ajax({
    url: 'index.php?route=product/product/getRecurringDescription',
    type: 'post',
    data: $('input[name=\'product_id\'], input[name=\'quantity\'], select[name=\'recurring_id\']'),
    dataType: 'json',
    beforeSend: function() {
      $('#recurring-description').html('');
    },
    success: function(json) {
      $('.alert-dismissible, .text-danger').remove();

      if (json['success']) {
        $('#recurring-description').html(json['success']);
      }
    }
  });
});
//--></script> 
<script type="text/javascript"><!--
$('#button-cart').on('click', function() {
  $.ajax({
    url: 'index.php?route=checkout/cart/add',
    type: 'post',
    data: $('#product input[type=\'text\'], #product input[type=\'hidden\'], #product input[type=\'radio\']:checked, #product input[type=\'checkbox\']:checked, #product select, #product textarea'),
    dataType: 'json',
    beforeSend: function() {
      $('#button-cart').button('loading');
    },
    complete: function() {
      $('#button-cart').button('reset');
    },
    success: function(json) {
      $('.alert-dismissible, .text-danger').remove();
      $('.form-group').removeClass('has-error');

      if (json['error']) {
        if (json['error']['option']) {
          for (i in json['error']['option']) {
            var element = $('#input-option' + i.replace('_', '-'));

            if (element.parent().hasClass('input-group')) {
              element.parent().before('<div class="text-danger">' + json['error']['option'][i] + '</div>');
            } else {
              element.before('<div class="text-danger">' + json['error']['option'][i] + '</div>');
            }
          }
        }

        if (json['error']['recurring']) {
          $('select[name=\'recurring_id\']').after('<div class="text-danger">' + json['error']['recurring'] + '</div>');
        }

        // Highlight any found errors
        $('.text-danger').parent().addClass('has-error');
      }

      if (json['success']) {
        $.notify({
          message: json['success'],
          target: '_blank'
        },{
          // settings
          element: 'body',
          position: null,
          type: "info",
          allow_dismiss: true,
          newest_on_top: false,
          placement: {
            from: "top",
            align: "center"
          },
          offset: 0,
          spacing: 10,
          z_index: 2031,
          delay: 5000,
          timer: 1000,
          url_target: '_blank',
          mouse_over: null,
          animate: {
            enter: 'animated fadeInDown',
            exit: 'animated fadeOutUp'
          },
          onShow: null,
          onShown: null,
          onClose: null,
          onClosed: null,
          icon_type: 'class',
          template: '<div data-notify="container" class="col-xs-11 col-sm-3 alert alert-success" role="alert">' +
            '<button type="button" aria-hidden="true" class="close" data-notify="dismiss">&nbsp;&times;</button>' +
            '<span data-notify="message"><i class="fa fa-check-circle"></i>&nbsp; {2}</span>' +
            '<div class="progress" data-notify="progressbar">' +
              '<div class="progress-bar progress-bar-success" role="progressbar" aria-valuenow="0" aria-valuemin="0" aria-valuemax="100" style="width: 0%;"></div>' +
            '</div>' +
            '<a href="{3}" target="{4}" data-notify="url"></a>' +
          '</div>' 
        });

        $('#cart > button').html('<div class="cart_detail"><div class="cart_image"></div><span id="cart-total"> ' + json['total'] + '</span>'  + '</div>');

        //$('html, body').animate({ scrollTop: 0 }, 'slow');

        $('#cart > ul').load('index.php?route=common/cart/info ul li');
      }
    },
        error: function(xhr, ajaxOptions, thrownError) {
            alert(thrownError + "\r\n" + xhr.statusText + "\r\n" + xhr.responseText);
        }
  });
});
//--></script> 
<script type="text/javascript"><!--
$('.date').datetimepicker({
  language: '{{ datepicker }}',
  pickTime: false
});

$('.datetime').datetimepicker({
  language: '{{ datepicker }}',
  pickDate: true,
  pickTime: true
});

$('.time').datetimepicker({
  language: '{{ datepicker }}',
  pickDate: false
});

$('button[id^=\'button-upload\']').on('click', function() {
  var node = this;

  $('#form-upload').remove();

  $('body').prepend('<form enctype="multipart/form-data" id="form-upload" style="display: none;"><input type="file" name="file" /></form>');

  $('#form-upload input[name=\'file\']').trigger('click');

  if (typeof timer != 'undefined') {
      clearInterval(timer);
  }

  timer = setInterval(function() {
    if ($('#form-upload input[name=\'file\']').val() != '') {
      clearInterval(timer);

      $.ajax({
        url: 'index.php?route=tool/upload',
        type: 'post',
        dataType: 'json',
        data: new FormData($('#form-upload')[0]),
        cache: false,
        contentType: false,
        processData: false,
        beforeSend: function() {
          $(node).button('loading');
        },
        complete: function() {
          $(node).button('reset');
        },
        success: function(json) {
          $('.text-danger').remove();

          if (json['error']) {
            $(node).parent().find('input').after('<div class="text-danger">' + json['error'] + '</div>');
          }

          if (json['success']) {
            alert(json['success']);

            $(node).parent().find('input').val(json['code']);
          }
        },
        error: function(xhr, ajaxOptions, thrownError) {
          alert(thrownError + "\r\n" + xhr.statusText + "\r\n" + xhr.responseText);
        }
      });
    }
  }, 500);
});
//--></script> 
<script type="text/javascript"><!--
$('#review').delegate('.pagination a', 'click', function(e) {
    e.preventDefault();

    $('#review').fadeOut('slow');

    $('#review').load(this.href);

    $('#review').fadeIn('slow');
});

$('#review').load('index.php?route=product/product/review&product_id={{ product_id }}');

$('#button-review').on('click', function() {
  $.ajax({
    url: 'index.php?route=product/product/write&product_id={{ product_id }}',
    type: 'post',
    dataType: 'json',
    data: $("#form-review").serialize(),
    beforeSend: function() {
      $('#button-review').button('loading');
    },
    complete: function() {
      $('#button-review').button('reset');
    },
    success: function(json) {
      $('.alert-dismissible').remove();

      if (json['error']) {
        $('#review').after('<div class="alert alert-danger alert-dismissible"><i class="fa fa-exclamation-circle"></i> ' + json['error'] + '</div>');
      }

      if (json['success']) {
        $('#review').after('<div class="alert alert-success alert-dismissible"><i class="fa fa-check-circle"></i> ' + json['success'] + '</div>');

        $('input[name=\'name\']').val('');
        $('textarea[name=\'text\']').val('');
        $('input[name=\'rating\']:checked').prop('checked', false);
      }
    }
  });
});

//$(document).ready(function() {
//  $('.thumbnails').magnificPopup({
//    type:'image',
//    delegate: 'a',
//    gallery: {
//      enabled: true
//    }
//  });
//});


$(document).ready(function() {
  var ramswaroop = new URLSearchParams(window.location.search);
  var tarun = ramswaroop.has('review');
  if (tarun == true) {
    setTimeout(function(){ 
      $('html, body').animate({scrollTop: $('#tabs_info').offset().top}, 'slow'); 
      $('a[href=\'#tab-review\']').trigger('click');
    }, 1000);
    return false;
  }
});

!$(document).ready(function() {
if ($(window).width() > 767) {
    $("#tmzoomadi").elevateZoom({
        
        gallery:'additional-carousel',
        //inner zoom         
                 
        zoomType : "inner", 
        cursor: "crosshair" 
        
        /*//tint
        
        tint:true, 
        tintColour:'#F90', 
        tintOpacity:0.5
        
        <--!//lens zoom
        
        zoomType : "lens", 
        lensShape : "round", 
        lensSize : 200 
        
        //Mousewheel zoom
        
        scrollZoom : true*/
        
        
      });
    var z_index = 0;
                  
                  $(document).on('click', '.thumbnail', function () {
                    $('.thumbnails').magnificPopup('open', z_index);
                    return false;
                  });
              
                  $('.additional-carousel a').click(function() {
                    var smallImage = $(this).attr('data-image');
                    var largeImage = $(this).attr('data-zoom-image');
                    var ez =   $('#tmzoom').data('elevateZoom');  
                    $('.thumbnail').attr('href', largeImage);  
                    ez.swaptheimage(smallImage, largeImage); 
                    z_index = $(this).index('.additional-carousel a');
                    return false;
                  });
      
  }else{
    $(document).on('click', '.thumbnail', function () {
    $('.thumbnails').magnificPopup('open', 0);
    return false;
    });
  }
});
$(document).ready(function() {     
  $('.thumbnails').magnificPopup({
    delegate: 'a.elevatezoom-gallery',
    type: 'image',
    tLoading: 'Loading image #%curr%...',
    mainClass: 'mfp-with-zoom',
    gallery: {
      enabled: true,
      navigateByImgClick: true,
      preload: [0,1] // Will preload 0 - before current, and 1 after the current image
    },
    image: {
      tError: '<a href="%url%">The image #%curr%</a> could not be loaded.',
      titleSrc: function(item) {
        return item.el.attr('title');
      }
    }
  });
});

$('#custom_tab a').tabs();
 $('#tabs a').tabs();

//--></script>

{% if (update_price_status is defined and update_price_status) %}
          
          <script type="text/javascript">
          
            $("#product input[type='checkbox']").click(function() {
              changePrice();
            });
            
            $("#product input[type='radio']").click(function() {
              changePrice();
            });
            
            $("#product select").change(function() {
              changePrice();
            });
            
            $("#input-quantity").keyup(function() {
              changePrice();
            });
            
            function changePrice() {
              $.ajax({
                url: 'index.php?route=product/product/updatePrice&product_id={{ product_id }}',
                type: 'post',
                dataType: 'json',
                data: $('#product input[name=\'quantity\'], #product select, #product input[type=\'checkbox\']:checked, #product input[type=\'radio\']:checked'),
                beforeSend: function() {
                  
                },
                complete: function() {
                  
                },
                success: function(json) {
                  $('.alert-success, .alert-danger').remove();
                  
                  if(json['new_price_found']) {
                    $('.new-prices').html(json['total_price']);
                    $('.product-tax').html(json['tax_price']);
                  } else {
                    $('.old-prices').html(json['total_price']);
                    $('.product-tax').html(json['tax_price']);
                  }
                }
              });
            }
          </script>
          
        {% endif %}
 
{{ footer }} 
