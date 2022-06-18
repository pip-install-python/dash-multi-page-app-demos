# Dash multi-page app demos

This repo contains minimal examples of multi-page apps using the `pages` feature available in dash>=2.5.1

This feature was developed in dash-labs.  For background, see the thread on the [Dash Community Forum](https://community.plotly.com/t/introducing-dash-pages-a-dash-2-x-feature-preview/57775/)
Convert your multi-page app from a dash-labs `pages` plug-in to the `pages` feature in dash 2.5.1 in 3 easy steps:

1. Remove `import dash_labs as dl` or upgrade dash-labs to V1.1.0
There is a conflict between dash-labs versions less than 1.1.0 when running a `pages` app in dash 2.5.1

2. Change:
```
app = Dash(__name__, plugins=[dl.plugins.pages])
```
to:
```
app = Dash(__name__, use_pages=True)
```

3. Change:
```
dl.plugins.page_container
```
to:
```
dash.page_container
```
####  That's it!
:point_right: The`pages` feature will no longer be developed in dash-labs.   I recommend all dash-labs multi-page apps be converted to use the `pages` feature in dash>= 2.5.1

-------
---------
# Examples List:

## multi_page_basics/

This folder has a minimal overview of the basic `pages features`, including:
- setting the default home page
- path variables
- updating the title and description with a function
- query strings
- setting redirects
- adding extra data to the dash.page_registry
- customizing the dash.page_registry defaults
- automatically including images in social media meta tag cards
- adding pages without using the pages folder

## multi_page_pathname_prefix/
    
This example shows how to use the "relative_path" attribute in dash.page_registry for deployment environments that use a pathname prefix.
It also shows use of `dash.get_asset_url()` to get the correct path to the `assets` folder from a file in the `pages` folder.

- `relative_path`:
        The path with `requests_pathname_prefix` prefixed before it.
        Use this path when specifying local URL paths that will work
        in environments regardless of what `requests_pathname_prefix` is.
        In some deployment environments, like Dash Enterprise,
        `requests_pathname_prefix` is set to the application name,
        e.g. `my-dash-app`.
        When working locally, `requests_pathname_prefix` might be unset and
        so a relative URL like `/page-2` can just be `/page-2`.
        However, when the app is deployed to a URL like `/my-dash-app`, then
        `relative_path` will be `/my-dash-app/page-2`.



## multi_page_cache/

This example shows how to share data between pages of a multi-page app using caching

The easiest way to share data between callbacks is to use dcc.Store(). However, if you have larger data, then you may want to use caching as described in example 3 and 4 in the Dash tutorial [sharing data between callbacks](https://dash.plotly.com/sharing-data-between-callbacks)

This example also demonstrates the use of the new `dash.get_app()` function that can be used to access the app object from modules within the `pages` folder without running into the circular imports issue. 

## multi_page_example1/

This example shows a small app with three pages with callbacks each page displays a figure.  It uses dash-bootstrap-components with a navigation in a dropdown in a navbar.


## multi_page_flask_login/

This shows a minimal example of use flask-login to secure one of the pages of a multi-page app.
This code is adapted for `pages`  based on Nader Elshehabi's  article and github repo: 
- https://dev.to/naderelshehabi/securing-plotly-dash-using-flask-login-4ia2
- https://github.com/naderelshehabi/dash-flask-login

## multi_page_layout_functions/
This app demonstrates how to create a sub-topics sidebar that is only used in certain pages.  
It shows how to use functions to make sure the `dash.page_registry` is complete when accessing it from within the `pages` folder.

## multi_page_meta_tags/

This app show more details on how the images are added to the meta tags

## multi_page_nested_folder/

This app demonstrates the case where you have nested folders with pages folder e.g.
```
- app.py 
- pages
    - chapter1
       |-- __init__.py
       |-- page1.py
       |-- page2.py
    - chapter2
       |-- __init__.py
       |-- page1.py
       |-- page2.py
```

## multi_page_query_strings/

This app demonstrates passing variables to a page with a figure using query strings

## multi_page_table_links

This app shows how to pass variable from the url path to a page, by clicking on a link in a table.
It includes:
- `dash.DataTable` with links formatted using Markdown
- html table with the links formatted using `dcc.Link`.  The advantage of the html table is the `dcc.Links` allow for the navigation to a new page without refreshing the page. The table is created with the `dbc.Table.from_dataframe` function from the `dash-bootstrap-components` library.


## multi_page_theme_switch
This example demonstrate a light and dark theme switch component from the [dash-bootstrap-templates](https://github.com/AnnMarieW/dash-bootstrap-templates) library