# Usage

Reading [Get Started](getstarted.md) section first is strongly recommended.

    Line break in an Excel cell will be rendered as <br>
 <a name="Conversiontypes"></a> 
## Conversion types
 <a name="Row"></a> 
### Row
		Note that you should select at least two rows as the first row will be considered as header.
    
If you choose 'Row' as the conversion type

* This add-in will first collect all selected data in the active sheet.
* The first row will be interpreted as header.
* The following rows will be mapped with header as you can see in the following example.

**Example Excel sheet**

<table class="table table-bordered table-striped table-condensed">
<tr>
	<th>Name</th>
	<th>Age</th>
	<th>Company</th>
</tr>
<tr>
	<td>David</td>
	<td>27</td>
	<td>WTSolutions</td>
</tr>
<tr>
	<td>Ton</td>
	<td>26</td>
	<td>WTSolutions</td>
</tr>
<tr>
	<td>Kitty</td>
	<td>30</td>
	<td>Microsoft</td>
</tr>
<tr>
	<td>Linda</td>
	<td>30</td>
	<td>Microsoft</td>
</tr>
<tr>
	<td>Joe</td>
	<td>40</td>
	<td>Github</td>
</tr>
</table>

**Example JSON**

```json
[
    {
        "Name": "David",
        "Age": 27,
        "Company": "WTSolutions"
    },
    {
        "Name": "Ton",
        "Age": 26,
        "Company": "WTSolutions"
    },
    {
        "Name": "Kitty",
        "Age": 30,
        "Company": "Microsoft"
    },
    {
        "Name": "Linda",
        "Age": 30,
        "Company": "Microsoft"
    },
    {
        "Name": "Joe",
        "Age": 40,
        "Company": "Github"
    }
]
```
 <a name="Nested"></a> 
### Nested

This conversion type is based on an amazing open source project [shape-json](https://github.com/ansteh/shape-json).

You need to provide a predefined schema , and Excel-to-JSON will convert your Excel sheet to JSON using provided schema.

Please read Api documentation https://github.com/ansteh/shape-json#api-documentation to prepare a schema.

**Example Excel Sheet**

<table class="table table-bordered table-striped table-condensed">
<tr>
	<th>pid</th>
	<th>contributor</th>
	<th>projectID</th>
	<th>projectName</th>
</tr>
<tr>
	<td>1</td>
	<td>jdalton</td>
	<td>1</td>
	<td>lodash</td>
</tr>
<tr>
	<td>1</td>
	<td>jdalton</td>
	<td>2</td>
	<td>docdown</td>
</tr>
<tr>
	<td>1</td>
	<td>jdalton</td>
	<td>3</td>
	<td>lodash-cli</td>
</tr>
<tr>
	<td>2</td>
	<td>contra</td>
	<td>4</td>
	<td>gulp</td>
</tr>
<tr>
	<td>3</td>
	<td>phated</td>
	<td>4</td>
	<td>gulp</td>
</tr>
</table>

**Example Schema**

```
{
  "$group[contributors](pid)": {
    "id": "pid",
    "name": "contributor",
    "$group[projects](projectID)": {
      "id": "projectID",
      "name": "projectName"
    }
  }
}
```

**Example JSON**

```
{
  "contributors": [
    {
      "id": 1,
      "name": "jdalton",
      "projects": [
        {
          "id": 1,
          "name": "lodash"
        },
        {
          "id": 2,
          "name": "docdown"
        },
        {
          "id": 3,
          "name": "lodash-cli"
        }
      ]
    },
    {
      "id": 2,
      "name": "contra",
      "projects": [
        {
          "id": 4,
          "name": "gulp"
        }
      ]
    },
    {
      "id": 3,
      "name": "phated",
      "projects": [
        {
          "id": 4,
          "name": "gulp"
        }
      ]
    }
  ]
}
```
 <a name="Additionalfeatures"></a> 
## Additional Features
 <a name="Concat"></a> 
### Concat

To concat coming JSON with existing JSON, you must check the "Concat coming JSON with existing JSON" checkbox.

    Note that : Row JSON can only concat with Row JSON, Nested JSON can only concat with Nested JSON.

<a name="Ignore"></a>
### Ignore blank cells

Sometimes, there is no value for a key and we do not want to keep this key. Simply check this checkbox, all blank cells will be ignored by this add-in.

<a name="importSchema"></a>
### Import Schema

You can easily import schema for nested JSON output by simply clicking on "Browse" button and select the JSON file you are about to load.

Once selected, the file will automaticlly be loaded.

<a name="jsonOutput"></a>
### JSON Output

There are several ways for you to save the generated JSON to your local computer.

* Copy and Paste. Once JSON generated, you will see them in the add-in, and you can simply copy and paste them anywhere you want.
* Copy to Clipboard.(Not applicable to Mac users) Once JSON generated, you can find the "Copy to Clipboard" button, click on the button, and you will have JSON on your clipboard.
* Save As.(Not applicable to users still using old browsers) Once JSON generated, you can find the "Save As" button, click on the button, and you will get notification from your browser asking you to save JSON as a file. Note, Mac Users may need to save the file manually by pressing ⌘+S to save the file after it is opened.