<script>
  let myXpathObj;
  let out = "";
  let expression = "//color_swatch[./ancestor::catalog_item/child::item_number[text()='RRX9856']]/ancestor::catalog_item/child::price";
  import Dialog from './Dialog.svelte';
  let value = `<?xml version="1.0"?>
<catalog>
   <product description="Cardigan Sweater" product_image="cardigan.jpg">
      <catalog_item gender="Men's">
         <item_number>QWZ5671</item_number>
         <price>39.95</price>
         <size description="Medium">
            <color_swatch image="red_cardigan.jpg">Red</color_swatch>
            <color_swatch image="burgundy_cardigan.jpg">Burgundy</color_swatch>
         </size>
         <size description="Large">
            <color_swatch image="red_cardigan.jpg">Red</color_swatch>
            <color_swatch image="burgundy_cardigan.jpg">Burgundy</color_swatch>
         </size>
      </catalog_item>
      <catalog_item gender="Women's">
         <item_number>RRX985677</item_number>
         <price>42.50</price>
         <size description="Small">
            <color_swatch image="red_cardigan.jpg">Red</color_swatch>
            <color_swatch image="navy_cardigan.jpg">Navy</color_swatch>
            <color_swatch image="burgundy_cardigan.jpg">Burgundy</color_swatch>
         </size>
         <size description="Medium">
            <color_swatch image="red_cardigan.jpg">Red</color_swatch>
            <color_swatch image="navy_cardigan.jpg">Navy</color_swatch>
            <color_swatch image="burgundy_cardigan.jpg">Burgundy</color_swatch>
            <color_swatch image="black_cardigan.jpg">Black</color_swatch>
         </size>
         <size description="Large">
            <color_swatch image="navy_cardigan.jpg">Navy</color_swatch>
            <color_swatch image="black_cardigan.jpg">Black</color_swatch>
         </size>
         <size description="Extra Large">
            <color_swatch image="burgundy_cardigan.jpg">Burgundy</color_swatch>
            <color_swatch image="black_cardigan.jpg">Black</color_swatch>
         </size>
      </catalog_item>
   </product>
</catalog>`;

  const softxpath = () => {
    out="";
	myXpathObj = new SoftXpath();
        myXpathObj.registerNamespace("", "");
		
		var ld = myXpathObj.loadXML(value);
        if (ld.success) {
		  var results = myXpathObj.selectNodes(expression);
          
		  if (results.length == 0) {
            out = "No records found!";
          } else {
            for (var i = 0; i < results.length; i++) {
				out+=results[i].text + " ";
            }
          }
        } else {
			out=ld.error;
        }
	
  };
</script>

<svelte:head>
  <script src="./SoftXpath.min.js" on:load={softxpath}></script>
</svelte:head>

<div className="MarkdownEditor">
  <h3>Input</h3>
  <label htmlFor="markdown-content"> Enter some markdown </label>
  <textarea id="markdown-content" bind:value on:input={softxpath}></textarea>
  <textarea bind:value={expression} on:input={softxpath}></textarea>
  <h3>Output</h3>
  <div className="content">
    
	{@html out}
	
  </div>
</div>
<Dialog/>
