---
title: Add Font to the Spreadsheet Fonts List
description: An example on how to add a font to the DropDownList with fonts in the toolbar of the Spreadsheet
type: how-to
page_title: Add Font in Spreadsheet Fonts List | Kendo UI Spreadsheet 
slug: spreadsheet-add-font
tags: spreadsheet, font
ticketid: 1140766 
res_type: kb
---

## Environment

<table>
 <tr>
  <td>Product</td>
  <td>Progress Kendo UI Spreadsheet</td>
 </tr>
 <tr>
  <td>Operating System</td>
  <td>All</td>
 </tr>
 <tr>
  <td>Browser</td>
  <td>All</td>
 </tr>
 <tr>
  <td>Preferred Language</td>
  <td>JavaScript</td>
 </tr>
</table>

## Description

How to add a font in Spreadsheet fonts list?

## Solution

The stylesheet of the font should be referenced. The list with the fonts should be set to the reference of the DropDownList containing the fonts. Implement select event of the widget. Check the current selection and apply the selected font.

```html
    <div id="spreadsheet"></div>
    <script>
        $("#spreadsheet").kendoSpreadsheet({
            sheets: [{
                rows: [{
                    cells: [{ value: "A" }, { value: "B" }, { value: "C" }]
                }, {
                    cells: [{ value: "1" }, { value: "2" }, { value: "3" }]
                }, {
                    cells: [{ value: "4" }, { value: "5" }, { value: "6" }]
                }, {
                    cells: [{ value: "Lorem ipsum" }, 
                            { value: "sed do eiusmod" }, 
                            { value: "Ut enim ad minim" }]
                }]
            }],
            pdf: {
                area: "selection"
            }
        });

        var spreadsheet = $("#spreadsheet").data("kendoSpreadsheet");
      
      	var ddls = $('.k-spreadsheet-toolbar [data-role="dropdownlist"]')[0];
      	var ddl = $(ddls).data("kendoDropDownList");
      	var dataSource = new kendo.data.DataSource({
  					data: [ "Arial", "Verdana", "Lobster" ]
				});
      	ddl.setDataSource(dataSource);
      
      	ddl.bind("select", onSelect);
      
      	function onSelect(e){        	
          	var fontName = e.item.text();
          	var spreadsheet = $("#spreadsheet").data("kendoSpreadsheet");
    		var sheet = spreadsheet.activeSheet();    
          	var selection = sheet.selection(); 
    		selection.fontFamily(fontName);
        }       	
    </script>
```
