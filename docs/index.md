<script type="text/javascript" src="jquery-3.6.0.min.js"></script>
<script type="text/javascript" src="JsBarcode.all.min.js"></script>

<style>
@media print {
  .no-print {
    display: none !important;
  }
  
  header {
  	display: none !important;
  }
  
  footer {
  	display: none !important;
  }
  
  .markdown-body > h1:first-of-type {
    display: none !important;
  }
  
}

  .inner {
  	width: 0;
  }

  .barcode-label {
    border: 1px solid;
    background: white;
  }
  
  #form {
  	padding-bottom: 24pt;
  }
  
  .barcode-label-name {
  	color: black;
  }
  
  
</style>

<div id="form" class="no-print" align="center">
	Library Name: <input type=text id="name" value=""/><br/><br/>
	Last number: <input type=text id="startingNumber" value=""/><br/><br/>
	Quantity: <input type=text id="barcodeQuantity" value=""/><br/><br/>
	Barcode Type: <select id="barcodeType" name="type">
		<option value='code39'>Code 39</option>
		<option value='code128'>Code 128</option>
		<option value='ean13'>EAN 13</option>
		<option value='upc'>UPC-A</option>
	</select>
	<br/><br/>

	<input id="submitBtn" type=button value="Submit"/>
</div>
<div id="barcodeBox" align="center">

</div>

<script>
    $('#submitBtn').click(function(){
    	var type = $('#barcodeType').val();
    	var initNum = $('#startingNumber').val();
    	var qty = $('#barcodeQuantity').val();
    	var name = $('#name').val();
    	
		$('#barcodeBox').html("");
		
		$('#barcodeBox').append("<input type='button' id='print' value='Print' class='no-print' />");
		$('#barcodeBox').append("<table border=0 align='center' cellspacing='0'>");
		for(let i = 0; i < qty; i++) {
			for(let col = 1; col <= 3; col++) {
				if(col == 1)
					$('#barcodeBox').append("<tr>");
					
				$('#barcodeBox').append(CreateBarcodeLabel(name, type, initNum++));
				if(col == 3)
					$('#barcodeBox').append("</tr>");
			}
		}
		$('#barcodeBox').append("</table>");
    
    	JsBarcode(".barcode").init();
    });
    
    $('#barcodeBox').on("click", "#print", function(){
		window.print();
		return false;
	});
    
    function CreateBarcodeLabel(name, type, value) {
    	var html = [];
    	html.push(
    	"<td class='barcode-label' align='center'>",
    	"<span class='barcode-label-name'>" + name + "</span>",
    	"<br/>",
    	CreateBarcode(type, value),
		"</td>"); 
		
		return html.join("");
    }
    
    function CreateBarcode(type, value) {
    	var html = [];
    	html.push(
    	"<svg class='barcode'",
  		"jsbarcode-format='" + type + "'",
  		"jsbarcode-value='" + value + "'",
  		"jsbarcode-textmargin='0'",
  		"jsbarcode-height='40'",
  		"jsbarcode-width='2'",
  		//"jsbarcode-fontSize='11'",
  		"jsbarcode-fontoptions='bold'>",
		"</svg>"); 
		
		return html.join("");
    }
    
</script>
