# BibsonomyProxy #

Simple proxy written in PHP to rewrite Bibsonomy endpoint results and embed it in the own service landscape.
E.g. to provide HTTPS and the same origin.

## Usage ##

### WordPress ###

To include the data from Bibsonomy in a page in WordPress, scripts and HTML are needed.

Needed scripts (We include them with the *Scripts n Styles* Plugin):
    <script src="https://api.simile-widgets.org/exhibit/STABLE/exhibit-api.js" type="text/javascript"></script>
    <link href="https://yourdomain.end/exhibit-proxy.php?suffix=tag/aksw&callback=cb" type="application/jsonp" rel="exhibit/data" ex:jsonp-callback="cb" />

Needed libs:
* JQuery

Example HTML (Exhibit):
```
This is a list of all publications done as part of this project and published at Bibsonomy:
<div class="floatbox">
  <div class="inner">
    <div class="legend">Navigation</div>
    <span ex:role="facet" ex:facetClass="TextSearch"></span>
<div id="div_filter_publications">
    <span ex:role="facet" ex:expression=".year" ex:facetLabel="Year" style="display: inline-block;"></span>
    <span ex:role="facet" ex:expression=".author" ex:facetLabel="Author" ex:sortMode="count" style="display: inline-block;"></span>
    <span ex:role="facet" ex:expression=".language" ex:facetLabel="Language" ex:sortMode="count" style="display: inline-block;"></span>
    <span ex:role="facet" ex:expression=".event" ex:facetLabel="Events" ex:sortMode="count" style="display: inline-block;"></span>
</div>
  </div>
  <a name="p16786-2"></a>
  <p class="auto" id="p16786-2"></div>

  <div ex:role="view" ex:grouped="false" ex:orders=".year,.label" ex:directions="descending,ascending" ex:showSummary="false" ex:showDuplicates="false" style=&quot;&quot;></p>
  <p ex:role="lens" ex:itemTypes="Publication" style="display: none">
    <strong ex:if-exists=".author">
      <span class="author" ex:content=".author"></span>:
    </strong>
    <a ex:if-exists=".biburl" ex:href-content=".biburl">
      <i ex:content=".label"></i>
    </a>
    <span ex:content="if(exists(.booktitle), concat('In: ', .booktitle), '')"></span>
    <span ex:if-exists=".editor">(Editors:
      <span class="editor" ex:content=".editor"></span>)</span>
    <span class="journal" ex:content="if(exists(.journal), concat('In: ', .journal), '')"></span>
    <span class="note" ex:content="if(exists(.note), concat(', Note: ', .note), '')"></span>
    <span class="abstract" style="display:none" ex:content="if(exists(.abstract), .abstract, '')"></span>
    <a ex:if-exists=".url" ex:href-content=".url">link</a>

  </div>
```

The HTML code could be changed - add/remove facets, change the texts, add/remove filters, ...
The proxy uses a search criteria to find entries.
The callback cb is needed to trigger exhibit for filling the HTML with data.
