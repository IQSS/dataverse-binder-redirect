# Dataverse Binder Redirect

To use Binder with Dataverse, please install the following [external tool][] manifest.

[external tool]: https://guides.dataverse.org/en/latest/admin/external-tools.html

Once you do, a "Binder" button will appear under "Access Dataset". Clicking that button will send the user to a static page hosted on GitHub Pages (the code in this repo). The static page places the DOI of a dataset into a URL that Binder can understand and then redirects the user there.

For example, the user may click "Binder" and land on the static page at https://iqss.github.io/dataverse-binder-redirect/v1/?datasetPid=doi:10.7910/DVN/TJCLKP which will send the user to https://mybinder.org/v2/dataverse/10.7910/DVN/TJCLKP/

Please note that this redirect page will no longer be required once the Dataverse external tool framework supports putting parameters in the path (rather than just the query parameters) of a URL ([#9345](https://github.com/IQSS/dataverse/issues/9345)).

```bash
curl -X POST -H 'Content-type: application/json' http://localhost:8080/api/admin/externalTools -d \
'{
  "displayName": "Binder",
  "toolName": "benderPreviewer", 
  "description": "Run on Binder",
  "scope": "dataset",
  "type": "explore",
  "toolUrl": "https://iqss.github.io/dataverse-binder-redirect/v1/",
  "toolParameters": {
    "queryParameters": [
      {
        "datasetPid": "{datasetPid}"
      }
    ]
  }
}'
```
