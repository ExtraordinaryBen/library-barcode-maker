<script type="text/javascript" src="jquery-3.6.0.min.js"></script>
<script type="text/javascript" src="JsBarcode.all.min.js"></script>

<style>
.markdown-body table td {
  padding: 0;
  border: 1px solid black;
}

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

  .barcode-label {
    border: 1px solid;
    background: white;
    font: 7pt Times;
	padding: 3px 0 0 0;
	width: 170px;
	height: 54px;
  }
  
  #form {
  	padding-bottom: 24pt;
  }
  
  .barcode-label-name {
  	color: black;
  }
  
  .barcode-label-value {
    font-size: 11pt;
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
    	var name = $('#name').val().toUpperCase();
    	
    	var html = "";
		$('#barcodeBox').html(html);
		
		html += "<input type='button' id='print' value='Print' class='no-print' />";
		html += "<table border=0 align='center' cellspacing='0'>";
		
		
		for(let i = 0; i < qty; i++) {
			if(i%3 == 0) {
				html += "<tr>";
			}
			html += CreateBarcodeLabel(name, type, ++initNum);
			if(i%3 == 2) {
				html += "</tr>";
			}
		}
		html += "</table>"
		
		$('#barcodeBox').html(html);
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
    	CreateBarcode(type, value),
    	"<span class='barcode-label-value'>" + value + "</span>",
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
  		"jsbarcode-margin='0'",
  		"jsbarcode-height='26'",
  		"jsbarcode-width='1'",
  		"jsbarcode-displayValue='false'",
  		"jsbarcode-fontSize='11'",
  		"jsbarcode-fontoptions='bold' />"); 
		
		return html.join("");
    }
    
</script>
