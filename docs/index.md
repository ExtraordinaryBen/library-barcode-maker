<script src="/jquery-3.6.0.min.js"></script>
<script src="/JsBarcode.all.min.js"></script>

<div>
Library Name: <input type=text name="name" value=""/><br/><br/>
Prefix (Optional): <input type=text name="prefix" value=""/><br/><br/>
Last number: <input type=text name="startingNumber" value=""/><br/><br/>
Quantity: <input type=text name="barcodeQuantity" value=""/><br/><br/>
Barcode Type: <select name="type">
<option value='C39'>Code 39</option>
<option value='C93'>Code 93</option>
<option value='C128 '>Code 128</option>
<option value='EAN8'>EAN 8</option>
<option value='EAN13'>EAN 13</option>
<option value='UPCA'>UPC-A</option>
<option value='CODABAR '>CODABAR </option>
</select><br/><br/>

<input type=submit name="submit" value="Submit"/>
</div>
