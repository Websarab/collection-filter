# collection-filter

<form id="color-filter">
  <label><input type="checkbox" name="color" value="red"> Red</label>
  <label><input type="checkbox" name="color" value="blue"> Blue</label>
  <label><input type="checkbox" name="color" value="green"> Green</label>
</form>

<div id="filtered-products">
  {% for product in collection.products %}
    <div class="product-card" data-tags="{{ product.tags | join: ' ' }}">
      <h2>{{ product.title }}</h2>
      <p>{{ product.price | money }}</p>
    </div>
  {% endfor %}
</div>
<script>
  document.getElementById('color-filter').addEventListener('change', function () {
    const selectedColors = Array.from(document.querySelectorAll('input[name="color"]:checked'))
                                .map(input => 'color_' + input.value.toLowerCase());
    
    document.querySelectorAll('.product-card').forEach(product => {
      const productTags = product.dataset.tags.split(' ');
      const matchesFilter = selectedColors.length === 0 || selectedColors.some(tag => productTags.includes(tag));
      product.style.display = matchesFilter ? 'block' : 'none';
    });
  });
</script>
