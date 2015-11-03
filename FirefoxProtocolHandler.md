# Add a Protocol Handler for tryton://-Links to your browserfrontends via javascript in Firefox #

Add following javascript to a page (for authenticated users)



```
<script type="text/javascript">
     navigator.registerProtocolHandler ("tryton", "http://YOUR_URL?uri=%s", "Add Tryton Handler");
</script>
```

and select the tryton executable as application.

After that links like:
```
<a href="tryton://YOUR_TRYTON_SERVER:8000/DATABASE/model/product.product/1">Edit Product</a>
```

will open the form of product 1 in your tryton client.