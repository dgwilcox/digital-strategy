Digital Government Strategy
===========================

This repository serves as the canonical machine-readable schema for describing action items within the president's digital strategy, and for reporting on its progress. Citizen developers are encouraged to use this information to build applications and tools.

Files
-----

* `agencies.json` and `agencies.xml` - machine-readable listing of common federal agencies, their primary domain, and abbreviation (e.g., FBI)
* `items.json` and `items.xml` - machine-readable representation of the action items from the digital strategy

Agency List
-----------

The agency list contains a timestamp of when the file was last updated as well as a listing of common federal agencies. Each agency has three fields:

* **name** - The Human-readable name of the agency (e.g., Federal Communications Commission)
* **id** - The agencies abbreviation or id (e.g., fcc)
* **url** - the agency's primary domain (e.g., www.fcc.gov)

In JSON this is represented as:

```json

{
   "generated":"2012-07-12 10:46:19",
   "agencies":[
      {
         "name":"Administrative Conference of the United States (ACUS)",
         "id":"acus",
         "url":"www.acus.gov"
      },
      {
         "name":"Advisory Council on Historic Preservation (ACHP)",
         "id":"achp",
         "url":"www.achp.gov"
      },
      ...
   ]
}
```

In XML this is represented as:

```xml
<?xml version="1.0"?>
<agencies>
  <generated>2012-07-12 10:46:19</generated>
  <agencies>
    <agency id="acus">
      <name>Administrative Conference of the United States (ACUS)</name>
      <url>www.acus.gov</url>
    </agency>
    <agency id="achp">
      <name>Advisory Council on Historic Preservation (ACHP)</name>
      <url>www.achp.gov</url>
    </agency>
    ...
  </agencies
</agencies>
```

Note: Both files are available as a service at `http://raw.github.com/gsa/agencies.{format}` ( [JSON](http://raw.github.com/gsa/agencies.json) | [XML](http://raw.github.com/gsa/agencies.xml) )

Items
-----

The items act as a machine-readable representation of the agency-specific action items outlined in the digital strategy, as well as a base schema for reporting on its progress. At the root level, the schema contains a timestamp indicating when it was last updated, as well as a list of all action items.

Each action item can have the following properties:

* **id** - a unique identifier for that action item, e.g., 2.1
* **parent** - where applicable, the parent action item, (e.g., 2.2.1's parent would be 2.1). Useful for grouping and formatting
* **text** - the human-readable text of the action item
* **due** - when the action item is due (relative to the release of the digital strategy)
* **due_date** - date calculated as the abosolute due date for the action item
* **fields** - a list of all fields associated with that action item
* **multiple** - whether multiple responses are allowed per action item (e.g., listing multiple systems with each of the action-item's field being answered once per system)

The field object is made up the following:

* **type** - the HTML input type that best represents the field (e.g., select, text, textarea)
* **name** - HTML friendly name for the field
* **label** - Human readable label for the field
* **option** - where applicable, an array of label, value pairs describing the potential options (e.g. for a drop down)
* **value** - when used as an agency progress report, the agency-reported answer to the field, or if multiple answers, an array of agency-reported answers.

In JSON this would be represented as:

```json

{
   "generated":"2012-07-12 11:00:27",
   "items":[
      {
         "id":"2.1",
         "parent":null,
         "text":"Engage with customers to identify at least two existing major customer-facing services that contain high-value data or content as first-move candidates to make compliant with new open data, content, and web API policy.",
         "due":"90 Days",
         "due_date":"2012\/08\/20",
         "fields":[
            {
               "type":"select",
               "name":"2-1-status",
               "label":"Overall Status",
               "options":[
                  {
                     "label":"Not Started",
                     "value":"not-started"
                  },
                  {
                     "label":"In Progress",
                     "value":"in-progress"
                  },
                  {
                     "label":"Completed",
                     "value":"completed"
                  }
               ],
               "value":null
            }
         ],
         "multiple":false
      },
      ...
   ],
}
```

In XML this would be represented as:

```xml

<?xml version="1.0"?>
<items>
  <generated>2012-07-12 11:00:27</generated>
  <items>
    <item id="2.1">
      <parent/>
      <text>Engage with customers to identify at least two existing major customer-facing services that contain high-value data or content as first-move candidates to make compliant with new open data, content, and web API policy.</text>
      <due>90 Days</due>
      <due_date>2012/08/20</due_date>
      <fields>
        <field>
          <type>select</type>
          <name>2-1-status</name>
          <label>Overall Status</label>
          <options>
            <option>
              <label>Not Started</label>
              <value>not-started</value>
            </option>
            <option>
              <label>In Progress</label>
              <value>in-progress</value>
            </option>
            <option>
              <label>Completed</label>
              <value>completed</value>
            </option>
          </options>
          <value/>
        </field>
      </fields>
      <multiple/>
    </item>
    ...
  </items>
</items>
```